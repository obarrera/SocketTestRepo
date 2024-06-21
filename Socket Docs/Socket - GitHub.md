## How to Guide: Using Socket in Your GitHub Workflow

### Introduction

Integrating Socket into your GitHub workflow enhances your CI/CD pipeline by adding security checks for vulnerabilities and risks associated with third-party dependencies. This guide provides step-by-step instructions on setting up and using Socket in your GitHub repository, utilizing the information provided and ensuring best practices for security.

### Prerequisites

Before you begin, ensure you have the following:
- A Socket account with API access.
- A GitHub repository.
- Administrator permissions to configure GitHub Actions and manage secrets.
- Node.js and npm installed on your local machine.

### Step 1: Setting Up Socket

#### 1.1 Sign Up and Log In
1. Visit the [Socket website](https://docs.socket.dev/docs/getting-started) and sign up for an account.
2. Log in to your account to access the Socket dashboard.

#### 1.2 Install Socket CLI
1. Open your terminal.
2. Run the following command to install the Socket CLI globally:
   ```bash
   npm install -g @socketsecurity/cli
   ```

### Step 2: Installing Socket GitHub App

#### 2.1 Install the Socket App
1. Follow the [installation instructions](https://docs.socket.dev/docs/socket-for-github-installation) to add Socket to your GitHub repository.
2. Navigate to the [Socket GitHub App](https://github.com/marketplace/socket) and click on "Install".
3. Select the repositories you want to integrate with Socket.

### Step 3: Configuring GitHub Actions

#### 3.1 Create or Update GitHub Actions Workflow
1. Create or edit the `.github/workflows/socket-security.yml` file in the root directory of your repository.
2. Add the following configuration to enable Socket security scans:

```yaml
name: socket-security-workflow
run-name: Socket Security Github Action
on: [push, issue_comment]
jobs:
  socket-security:
    permissions:
      contents: read
      pull-requests: read
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: '3.12'
      - name: Install Socket CLI
        run: pip install socketsecurity --upgrade
      - name: Check if Default Branch
        if: steps.branch-names.outputs.is_default == 'true'
        run: echo "DEFAULT_BRANCH=1" >> $GITHUB_ENV
      - uses: actions/github-script@v7
        id: get_pr_data
        with:
          script: |
              let data = (
                await github.rest.repos.listPullRequestsAssociatedWithCommit({
                  commit_sha: context.sha,
                  owner: context.repo.owner,
                  repo: context.repo.repo,
                })
              ).data[0];
              if (data === undefined) {
                data = {
                  'number': null,
                  'title': null
                }
              }
              return data;
      - name: Save Pull Request Number
        run: |
          echo "PR_NUMBER=${{ fromJson(steps.get_pr_data.outputs.result).number || github.event.issue.number }}"  >> $GITHUB_ENV
      - name: Run scan
        env:
          SOCKET_SECURITY_API_KEY: ${{ secrets.SOCKET_SECURITY_API_KEY }}
          GH_API_TOKEN: ${{ secrets.GH_API_TOKEN }}
          COMMIT_MESSAGE: ${{ github.event.head_commit.message }}
        run: |
          socketcli --scm github --repo ${{ github.event.repository.name }} --branch "${{ github.ref_name }}" $(if [ ! -z $DEFAULT_BRANCH ]; then echo "--default_branch"; fi) --pr_number $(if [ -z $PR_NUMBER ]; then echo 0; else echo $PR_NUMBER;fi) --committer "$GITHUB_ACTOR" --commit_message "$COMMIT_MESSAGE" --target_path $GITHUB_WORKSPACE
```

### Step 4: Secure Environment Variables

#### 4.1 Add Secrets to GitHub Repository
1. Go to **Settings > Secrets and variables > Actions** in your GitHub repository.
2. Add the following secrets:
   - `SOCKET_SECURITY_API_KEY`: Your Socket API key.
   - `GH_API_TOKEN`: Your GitHub API token.

### Step 5: Running the Workflow

#### 5.1 Commit and Push Changes
1. Commit your changes to `.github/workflows/socket-security.yml` and push them to your GitHub repository.

```bash
git add .github/workflows/socket-security.yml
git commit -m "Add Socket security scan to GitHub Actions workflow"
git push origin main
```

#### 5.2 Monitor Workflow Execution
1. Navigate to the **Actions** tab in GitHub.
2. Monitor the execution of the workflow. The Socket security scan will run as part of the workflow, checking for vulnerabilities and risks.

### Step 6: Reviewing Results

#### 6.1 View Workflow Logs
1. Once the workflow has run, click on the workflow run to view the detailed logs.
2. Look for the output of the `socketcli` command to see the results of the security scan.

#### 6.2 Addressing Issues
1. If vulnerabilities or risks are detected, review the detailed report provided by Socket.
2. Take necessary actions to address the identified issues, such as updating dependencies or removing risky packages.

### Socket for GitHub: Key Features

#### Telemetry Detection
Socket can detect when a package is collecting telemetry, alerting you and providing actionable information on how to disable it.

![Telemetry Detection](https://files.readme.io/955a9f7-telemetry.png)

#### Protestware Detection
Socket identifies packages that contain protestware, helping you evaluate whether to keep or remove them.

![Protestware Detection](https://files.readme.io/0c13b9f-protestware.png)

#### Install Script Detection
Socket detects when a package introduces an install script, which is a common vector for malware.

![Install Script Detection](https://files.readme.io/0b4b9de-install-script.png)

#### Native Code Detection
Socket alerts you when a package includes native code, which can be difficult to audit and may pose security risks.

![Native Code Detection](https://files.readme.io/edaf42e-native-code.png)

#### Typosquat Detection
Socket detects potential typosquatting in package names to prevent malicious packages from entering your codebase.

![Typosquat Detection](https://files.readme.io/cacee13-typosquat.png)

### Advanced Configuration with `socket.yml`

#### Project Ignore Paths
The `projectIgnorePaths` key is an array of strings used to ignore folders or files. This is useful to exclude certain directories from being scanned.

```yaml
projectIgnorePaths:
  - "node_modules"
  - ".yarn"
  - "dist"
  - "build"
```

#### Trigger Paths
The `triggerPaths` key is an array of strings used to match against files modified in pull requests to determine if a Pull Request alert scan should be performed.

```yaml
triggerPaths:
  - "/workspaces/foo"
  - "/workspaces/bar"
```

#### Issue Rules
The `issueRules` key allows you to enable or disable issue alerts in your pull requests.

```yaml
issueRules:
  didYouMean: true
  installScripts: true
  telemetry: true
  troll: true
  malware: true
  hasNativeCode: true
```

### Additional Resources

- **Ignoring Pull Request Alerts**: Learn how to [ignore specific alerts](https://docs.socket.dev/docs/ignoring-pull-request-alerts) that you deem non-critical.
- **Using socket.yml**: Customize your Socket configuration with the [socket.yml](https://docs.socket.dev/docs/socket-yml) file to tailor security scans to your needs.
- **What to Do with Socket Alerts**: Refer to the guide on [handling Socket alerts](https://docs.socket.dev/docs/what-to-do-with-socket-alerts) to understand the best practices for responding to detected issues.
- **Permissions**: Ensure you understand and configure the necessary [permissions](https://docs.socket.dev/docs/permissions) for Socket to operate effectively in your repository.

### Best Practices

1. **Run Security Scans Regularly**: Integrate Socket scans in your workflow to run on every push or pull request to catch vulnerabilities early.
2. **Fail on High Severity Issues**: Configure your workflow to fail if high severity vulnerabilities are detected, preventing insecure code from being merged or deployed.
3. **Keep Dependencies Updated**: Regularly update your dependencies to ensure you are using the latest secure versions.
4. **Review Reports**: Regularly review the security reports generated by Socket to stay informed about potential risks.

By following this guide, you can effectively integrate Socket into your GitHub workflow, enhancing your CI/CD pipeline with robust security checks for third-party dependencies.

For more detailed information, visit the [Socket Documentation](https://docs.socket.dev/docs/getting-started).
