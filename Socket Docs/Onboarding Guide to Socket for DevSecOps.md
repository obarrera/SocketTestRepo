## Comprehensive Onboarding Guide to Socket for DevSecOps

### Introduction

Socket is a powerful tool designed to enhance the security of your software development lifecycle by detecting and mitigating risks associated with third-party dependencies. This guide will walk you through the process of onboarding Socket into your DevSecOps practices, providing step-by-step instructions, best practices, and a suggested security policy configuration.

### Prerequisites

Before you begin, ensure you have the following:
- Access to your code repository (GitHub, GitLab, or Bitbucket).
- Administrator permissions for installing integrations and managing repository settings.
- Node.js and npm installed on your local machine for running Socket CLI.

### Step 1: Getting Started with Socket

**1.1 Sign Up and Log In**
- Visit the [Socket website](https://docs.socket.dev/docs/getting-started) and sign up for an account.
- Log in to your account to access the Socket dashboard.

**1.2 Install Socket CLI**
- Open your terminal and run the following command to install the Socket CLI globally:
  ```bash
  npm install -g @socketsecurity/cli
  ```

### Step 2: Integrating Socket into Your GitHub Repository

**2.1 Installation**
- Follow the [installation instructions](https://docs.socket.dev/docs/socket-for-github-installation) to add Socket to your GitHub repository.
- Navigate to the GitHub Marketplace and find the Socket app.
- Click on "Install" and select the repositories you want to integrate with Socket.

**2.2 Configuration**
- Socket will automatically start scanning your repositories for vulnerabilities and supply chain risks.
- You can configure the settings and alert thresholds from the Socket dashboard.

### Step 3: Integrating Socket into Your GitLab Pipeline

**3.1 Install Socket CLI**
- Ensure the Socket CLI is installed in your project’s dependencies.

**3.2 Pipeline Configuration**
- Modify your `.gitlab-ci.yml` file to include Socket scans in your pipeline stages. Example configuration:
  ```yaml
  stages:
    - test
    - security

  socket_security_scan:
    stage: security
    script:
      - npm install -g @socketsecurity/cli
      - socket scan
    only:
      - branches
      - merge_requests
  ```

**3.3 Secure Environment Variables**
- Store and reference API keys or tokens securely using GitLab’s CI/CD settings.

### Step 4: Integrating Socket into Your Bitbucket Pipeline

**4.1 Install Socket CLI**
- Add the Socket CLI as a dependency to your project.

**4.2 Pipeline Configuration**
- Update your `bitbucket-pipelines.yml` file to run Socket scans. Example configuration:
  ```yaml
  pipelines:
    default:
      - step:
          name: Security Scan
          script:
            - npm install -g @socketsecurity/cli
            - socket scan
          caches:
            - node
  ```

**4.3 Secure Variables**
- Use Bitbucket’s repository settings to manage API keys and sensitive data securely.

### Step 5: Enhanced Monitoring with Socket SIEM Connector

**5.1 Installation**
- Clone the SIEM connector repository:
  ```bash
  git clone https://github.com/SocketDev/socket-siem-connector.git
  cd socket-siem-connector
  ```

**5.2 Configuration**
- Install dependencies and configure the connector to integrate with your SIEM solution:
  ```bash
  npm install
  export SOCKET_API_KEY=your_api_key
  export SIEM_ENDPOINT=your_siem_endpoint
  node index.js
  ```

### Step 6: Automating Security Checks with Git Cronjob

**6.1 Setup**
- Clone the Git cronjob repository:
  ```bash
  git clone https://github.com/socketdev-demo/git-cronjob.git
  cd git-cronjob
  ```

**6.2 Configuration**
- Customize the script to target your repositories and include necessary authentication:
  ```bash
  export REPO_URL=your_repository_url
  export SOCKET_API_KEY=your_api_key
  ```

**6.3 Schedule Cronjob**
- Schedule the cronjob for regular scans (e.g., daily at midnight):
  ```bash
  0 0 * * * /path/to/git-cronjob/scan.sh
  ```

### Language Support

Socket supports various programming languages and package managers. Refer to the [language support documentation](https://docs.socket.dev/docs/language-support) to ensure your projects are compatible.

### Frequently Asked Questions (FAQ)

Visit the [FAQ section](https://docs.socket.dev/docs/faq) for answers to common questions about using Socket, troubleshooting issues, and optimizing your security scans.

### Suggested Security Policy Configuration

#### Block 🚫

| Alert                          | Alert Info                                                                                             | Category          | Severity |
|--------------------------------|-------------------------------------------------------------------------------------------------------|-------------------|----------|
| Known malware                  | This package is malware. We have asked the package registry to remove it.                              | Supply chain risk | Critical |
| Protestware or potentially unwanted behavior | This package is a joke, parody, or includes undocumented or hidden behavior unrelated to its primary function. | Supply chain risk | High     |
| AI detected potential malware  | AI has identified this package as malware. This is a strong signal that the package may be malicious.  | Supply chain risk | High     |
| Potential Typo Squat           | Package name is similar to other popular packages and may not be the package you want.                | Supply chain risk | Critical |
| Obfuscated code                | Obfuscated files are intentionally packed to hide their behavior. This could be a sign of malware.    | Supply chain risk | High     |
| Shell access                   | This module accesses the system shell. Accessing the system shell increases the risk of executing arbitrary code. | Supply chain risk | Critical |
| Network access                 | This module accesses the network.                                                                     | Supply chain risk | High     |
| Native code                    | Contains native code which could be a vector to obscure malicious code, and generally decrease the likelihood of reproducible or reliable installs. | Supply chain risk | High     |

#### Warn ⚠️

| Alert                        | Alert Info                                                                                                                                                                                                 | Category          | Severity |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|----------|
| Bin Script Shell Injection   | This package re-exports a well-known shell command via an npm bin script. This is possibly a supply chain risk.                                                                                            | Supply chain risk | High     |
| HTTP dependency              | Contains a dependency which resolves to a remote HTTP URL which could be used to inject untrusted code and reduce overall package reliability.                                                             | Supply chain risk | Critical |
| Git dependency               | Contains a dependency which resolves to a GitHub URL. Dependencies fetched from GitHub specifiers are not immutable and can be used to inject untrusted code or reduce the likelihood of a reproducible install. | Supply chain risk | Critical |
| Telemetry                    | This package contains telemetry which tracks how it is used.                                                                                                                                               | Supply chain risk | High     |
| AI detected security risk    | AI has determined that this package may contain potential security issues or vulnerabilities.                                                                                                              | Supply chain risk | High     |
| High entropy strings         | Contains high entropy strings. This could be a sign of encrypted data, leaked secrets, or obfuscated code.                                                                                                  | Supply chain risk | Medium   |
| New author                   | A new npm collaborator published a version of the package for the first time. New collaborators are usually benign additions to a project, but do indicate a change to the security surface area of a package. | Supply chain risk | Medium   |
| Unstable ownership           | A new collaborator has begun publishing package versions. Package stability and security risk may be elevated.                                                                                             | Supply chain risk | Medium   |

#### Monitor 👁️

| Alert                     | Alert Info                                                                                                           | Category      | Severity |
|---------------------------|---------------------------------------------------------------------------------------------------------------------|---------------|----------|
| Critical CVE              | Contains a Critical Common Vulnerability and Exposure (CVE).                                                         | Vulnerability | Critical |
| High CVE                  | Contains a high severity Common Vulnerability and Exposure (CVE).                                                    | Vulnerability | High     |
| Medium CVE                | Contains a medium severity Common Vulnerability and Exposure (CVE).                                                  | Vulnerability | Medium   |
| Low CVE                   | Contains a low severity Common Vulnerability and Exposure (CVE).                                                     | Vulnerability | Low      |
| Non-existent author       | The package was published by an npm account that no longer exists.                                                   | Supply chain risk | Medium   |
| Unresolved Require        | Package imports a file which does not exist and may not work as is. It could also be importing a file that will be created at runtime which could be a vector for running malicious code. | Quality       | Critical |
| Environment variable access | Package accesses environment variables, which may be a sign of credential stuffing or data theft.                   | Supply chain risk | High     |
| Dynamic require           | Dynamic require can indicate the package is performing dangerous or unsafe dynamic code execution.                   | Supply chain risk | High     |

#### Ignore ❌

| Alert                      | Alert Info                                                                                               | Category          | Severity |
|----------------------------|-----------------------------------------------------------------------------------------------------------|-------------------|----------|
| Install scripts            | Install scripts are run when the package is installed. The majority of malware in npm is hidden in install scripts. | Supply chain risk | High     |
| Deprecated license         | License is deprecated which may have legal implications regarding the package's use.                      | Legal risk        | Medium   |
| Unpopular package          | This package is not very popular.                                                                         | Supply chain risk | Low      |
| Trivial Package            | Packages less than 10 lines of code are easily copied into your own project.                              | Quality risk      | Low      |
| Minified code              | This package contains minified
