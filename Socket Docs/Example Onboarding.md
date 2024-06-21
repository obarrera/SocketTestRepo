### Slide Deck: Onboarding Presentation for Socket

---

#### Slide 1: Welcome
**Title:** Welcome to Socket

**Content:**
- **Greeting:** Welcome! We are excited to introduce you to Socket, your new ally in securing your software supply chain.
- **Overview:** Today, we'll cover how Socket can help you detect and mitigate supply chain attacks in your dependencies.

---

#### Slide 2: Introduction to Socket
**Title:** What is Socket?

**Content:**
- **Description:** Socket is a comprehensive security tool designed to protect your software from supply chain attacks by analyzing your dependencies for potential risks.
- **Key Features:**
  - Real-time alerts
  - Detailed dependency insights
  - Integration with popular development tools and CI/CD pipelines

---

#### Slide 3: Why Socket?
**Title:** Why Choose Socket?

**Content:**
- **Supply Chain Risks:** Traditional security tools often miss supply chain attacks.
- **Comprehensive Protection:** Socket provides actionable insights, not just alerts.
- **Proactive Defense:** Designed to catch active supply chain attacks in real-time.

---

#### Slide 4: Getting Started
**Title:** Getting Started with Socket

**Content:**
- **Installation:**
  ```bash
  npm install -g @socketsecurity/cli
  ```
- **Verify Installation:**
  ```bash
  socket --version
  ```

---

#### Slide 5: Integrations
**Title:** Integrations

**Content:**
- **GitHub:** Install the Socket GitHub App to scan pull requests.
- **VS Code:** Use the Socket VS Code Extension for real-time scanning.
- **CI/CD Pipelines:**
  - **GitLab:**
    ```yaml
    script:
      - socket report create --view --strict
    ```
  - **Bitbucket:** Add Socket CLI commands to your pipeline configuration.

---

#### Slide 6: Using Socket
**Title:** Using Socket CLI

**Content:**
- **Create a Report:**
  ```bash
  socket report create <paths-to-package-folders-and-files>
  ```
- **CI Integration:**
  ```bash
  socket ci
  ```
- **Package Information:**
  ```bash
  socket info <package-name>
  ```

---

#### Slide 7: Configuring Socket
**Title:** Configuring Socket with `socket.yml`

**Content:**
- **Ignoring Paths:**
  ```yaml
  projectIgnorePaths:
    - "node_modules"
    - ".yarn"
  ```
- **Trigger Paths:**
  ```yaml
  triggerPaths:
    - "/workspaces/foo"
    - "/workspaces/bar"
  ```

---

#### Slide 8: Alert Management
**Title:** Managing Alerts

**Content:**
- **Alert Categories:**
  - **Supply Chain Risk:** Critical, High, Medium, Low
  - **Quality Issues:** Critical, High, Medium, Low
  - **Maintenance Issues:** Critical, High, Medium, Low
  - **Vulnerabilities:** Critical, High, Medium, Low

---

#### Slide 9: Responding to Alerts
**Title:** Responding to Alerts

**Content:**
- **Block (Critical Issues):** Known malware, AI-detected potential malware, critical CVEs.
- **Warn (High-Risk Issues):** Telemetry, new install scripts, dynamic require usage.
- **Monitor (Medium/Low-Risk Issues):** Potential vulnerabilities, maintenance concerns.
- **Ignore (Low Priority):** Minified code, floating dependencies, etc.

---

#### Slide 10: Best Practices
**Title:** Best Practices

**Content:**
- **Regular Scanning:** Integrate Socket into your CI/CD pipelines.
- **Manual Reviews:** Conduct manual code reviews for high-risk alerts.
- **Stay Updated:** Keep your Socket CLI and integrations updated.

---

#### Slide 11: Conclusion
**Title:** Conclusion

**Content:**
- **Summary:** Socket provides comprehensive protection for your software supply chain by offering real-time alerts and actionable insights.
- **Next Steps:** Integrate Socket into your workflow to start securing your dependencies today.

---

#### Slide 12: Q&A
**Title:** Questions & Answers

**Content:**
- **Open Floor:** Address any questions or concerns.
- **Contact Info:** Provide contact details for further support.

---

### Onboarding Script for the Technical Account Manager

#### Slide 1: Welcome
- **Script:** "Welcome everyone! I'm excited to introduce you to Socket, a powerful tool that will help you secure your software supply chain. Let's get started by understanding what Socket is and how it can benefit your development process."

#### Slide 2: Introduction to Socket
- **Script:** "Socket is designed to detect and mitigate supply chain attacks by analyzing your dependencies. Unlike traditional tools, Socket provides real-time alerts and actionable insights, making it easier to secure your software."

#### Slide 3: Why Socket?
- **Script:** "Traditional security tools often miss supply chain attacks. Socket fills this gap by offering comprehensive protection and proactive defense mechanisms against these threats."

#### Slide 4: Getting Started
- **Script:** "To get started with Socket, you need to install the CLI. Use the command `npm install -g @socketsecurity/cli` and verify the installation with `socket --version`."

#### Slide 5: Integrations
- **Script:** "Socket integrates seamlessly with GitHub, VS Code, and CI/CD pipelines like GitLab and Bitbucket. This ensures continuous monitoring and protection throughout your development lifecycle."

#### Slide 6: Using Socket
- **Script:** "With Socket CLI, you can create reports, integrate with CI pipelines, and get detailed package information. These commands help you keep track of dependency risks effectively."

#### Slide 7: Configuring Socket
- **Script:** "Socket can be configured using the `socket.yml` file. You can specify paths to ignore or trigger alerts, making it easier to manage large projects."

#### Slide 8: Alert Management
- **Script:** "Socket categorizes alerts into supply chain risks, quality issues, maintenance issues, and vulnerabilities. Each category is further divided by severity, helping you prioritize actions."

#### Slide 9: Responding to Alerts
- **Script:** "Critical issues should be blocked immediately, high-risk issues should prompt a review, medium and low-risk issues should be monitored, and low priority issues can be noted."

#### Slide 10: Best Practices
- **Script:** "Regularly scan your dependencies, conduct manual reviews for high-risk alerts, and keep your Socket tools updated to ensure maximum protection."

#### Slide 11: Conclusion
- **Script:** "In summary, Socket offers comprehensive protection for your software supply chain. Integrate it into your workflow today to start securing your dependencies."

#### Slide 12: Q&A
- **Script:** "Now, I'd like to open the floor for any questions you might have. Feel free to ask about anything we've covered today or any other concerns you may have."

---

This slide deck and script will help you effectively present the Socket product to new accounts, highlighting its features, integration capabilities, and the comprehensive protection it offers against supply chain attacks.
