### Comprehensive Technical Manual for Using Socket

#### Introduction
Socket is a robust security tool designed to protect your software supply chain. It offers visibility, defense-in-depth, and proactive protection for your open source dependencies. Socket is particularly effective at identifying and mitigating supply chain attacks, providing real-time alerts and actionable insights.

### Getting Started

#### Installation
1. **Install Socket CLI**:
   ```bash
   npm install -g @socketsecurity/cli
   ```
   This command will add the `socket` binary to your PATH. You can verify the installation with:
   ```bash
   socket --version
   ```

2. **GitHub Integration**:
   - Install the Socket GitHub App to your repositories to start running checks on pull requests immediately. This provides feedback on any security risks detected in your dependencies.

3. **VS Code Integration**:
   - Install the Socket VS Code Extension from the VS Code Marketplace or OpenVSX registry. This tool allows you to scan projects directly from within VS Code, providing real-time feedback.

4. **CI/CD Integration**:
   - **GitLab**: Add the following to your `.gitlab-ci.yml`:
     ```yaml
     script:
       - socket report create --view --strict
     ```
   - **Bitbucket**: Integrate Socket checks into your pipeline by including the Socket CLI commands in your Bitbucket pipeline configuration.

### Using Socket

#### CLI Commands
1. **Creating a Report**:
   ```bash
   socket report create <paths-to-package-folders-and-files>
   ```
   This command uploads specified `package.json` and lock files to create a Project Health Report.

2. **CI Integration**:
   ```bash
   socket ci
   ```
   This is an alias for `socket report create --view --strict`, which is useful for automating Socket checks in your CI pipelines.

3. **Package Information**:
   ```bash
   socket info <package-name>
   ```
   This command provides detailed information about a package, including supply chain risks and other issues.

### Configuration

#### `socket.yml` Configuration
- **Ignoring Paths**:
  ```yaml
  projectIgnorePaths:
    - "node_modules"
    - ".yarn"
  ```
  Use this key to specify paths that should be ignored during scanning.

- **Trigger Paths**:
  ```yaml
  triggerPaths:
    - "/workspaces/foo"
    - "/workspaces/bar"
  ```
  Define paths that, when modified, should trigger a Pull Request alert scan.

### Alert Management

#### Alert Categories
Socket categorizes alerts into four main types based on severity and impact:
1. **Supply Chain Risk**:
   - Critical: Known malware, typosquats, HTTP dependencies.
   - High: Unsafe packages requiring manual inspection.
   - Medium: Medium-risk issues needing attention in critical applications.
   - Low: Low-risk issues.

2. **Quality Issues**:
   - Critical: Severe issues like invalid package.json or unresolved requires.
   - High/Medium/Low: Varying degrees of quality concerns.

3. **Maintenance Issues**:
   - Critical: Critical maintenance problems making the package unsuitable.
   - High/Medium/Low: Different levels of maintenance issues.

4. **Vulnerabilities**:
   - CVEs categorized by severity (Critical, High, Medium, Low).

#### Responding to Alerts
1. **Block (Critical Issues)**:
   - Known malware, AI-detected potential malware, and critical CVEs should be blocked immediately. Remove these packages from your codebase and notify relevant stakeholders.

2. **Warn (High-Risk Issues)**:
   - Telemetry, new install scripts, and dynamic require usage should prompt a thorough review. Ensure the integrity and necessity of these features before proceeding.

3. **Monitor (Medium/Low-Risk Issues)**:
   - Issues like potential vulnerabilities or maintenance concerns should be monitored over time. Regularly review these alerts and apply updates as needed.

4. **Ignore (Low Priority)**:
   - Minified code, floating dependencies, and other low-risk issues can be noted but do not require immediate action.

### Best Practices

1. **Regular Scanning**:
   - Integrate Socket checks into your CI/CD pipelines to ensure continuous monitoring of your dependencies.

2. **Manual Reviews**:
   - For high-risk alerts, conduct manual code reviews to verify the safety and integrity of the packages.

3. **Stay Updated**:
   - Keep your Socket CLI and integrations updated to benefit from the latest security features and improvements.

### Conclusion
Socket provides a comprehensive solution for securing your software supply chain. By integrating Socket into your development workflow, you can proactively detect and mitigate risks associated with open source dependencies, ensuring the safety and reliability of your software.

For more detailed documentation, visit the [Socket Documentation](https://docs.socket.dev/docs/getting-started).
