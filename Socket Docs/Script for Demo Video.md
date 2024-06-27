### Script for Demo Video on Triage and Security Policy in Socket

---

#### [Opening Scene: Title Screen]
**Text on Screen:**
"Socket: Triaging Alerts & Security Policy Configuration"
[Background Music Starts]

---

#### [Scene 1: Introduction]
**Narrator:**
"Welcome to this brief demo on how to efficiently triage alerts and configure security policies using Socket."

**Visuals:**
- Display the Socket logo.
- Show a quick preview of the Socket dashboard interface.

---

#### [Scene 2: Accessing Security Policy Page]
**Narrator:**
"To get started, let's navigate to the Security Policy page. This is where you can configure how different types of alerts are handled. We will review an example Security Policy configuration, but it's important for each security policy to be tailored to meet the requirements of your organization."

**Visuals:**
- Screen recording of navigating to the 'Security Policy' page.

---

#### [Scene 3: Overview of Security Policy]
**Narrator:**
"On the Security Policy page, you can see various alert types categorized by severity. You have options to Block, Warn, Monitor, or Ignore these alerts."

**Visuals:**
- Highlight the different alert types and the actions available for each.

---

#### [Scene 4: Blocking an Alert]
**Narrator:**
"When an alert is critical, like 'Known malware', it may be better for your organization to block it immediately to protect your codebase."

**Visuals:**
- Click on a critical 'Known malware' alert.
- Select 'Block' from the dropdown menu.
- Confirm the action.

**Text on Screen:**
"Action: Block"
"Critical alerts are immediately blocked to ensure security."

---

#### [Scene 5: Warning for Alerts]
**Narrator:**
"For high-risk alerts, such as 'Install Scripts', you might want to warn your team to review the package carefully."

**Visuals:**
- Click on a high-risk 'Install Scripts' alert.
- Select 'Warn' from the dropdown menu.
- Confirm the action.

**Text on Screen:**
"Action: Warn"
"High-risk alerts are flagged for team review."

---

#### [Scene 6: Monitoring Alerts]
**Narrator:**
"Medium risk alerts, like 'Network access', can be set to monitor. This keeps track of the alert without immediate action."

**Visuals:**
- Click on a medium risk 'Network access' alert.
- Select 'Monitor' from the dropdown menu.
- Confirm the action.

**Text on Screen:**
"Action: Monitor"
"Monitor alerts to keep an eye on potential issues."

---

#### [Scene 7: Ignoring Alerts]
**Narrator:**
"For low-risk or non-actionable alerts, such as 'Low CVE', you can choose to ignore them."

**Visuals:**
- Click on a low-risk 'Low CVE' alert.
- Select 'Ignore' from the dropdown menu.
- Confirm the action.

**Text on Screen:**
"Action: Ignore"
"Ignore low-risk or non-actionable alerts."

---

#### [Scene 8: Triaging Alerts in Reports and Organizational Alerts]
**Narrator:**
"Sometimes you might need to override your security policy for an individual alert. This is where triaging comes into play. For example, you can triage an alert to ignore it if it's not relevant to your current project. Actions taken in the Reports Alerts or Organizational Alerts pages will override the Security Policy set for that package artifact in that repository."

**Visuals:**
- Navigate to an alert in the 'Reports Alerts' or 'Organizational Alerts' section.
- Show the process of overriding an alert action through triage.

**Text on Screen:**
"Triage: Override Alert Actions"
"Customize alert handling on a case-by-case basis."

---

#### [Scene 9: Alert Actions Overview]
**Narrator:**
"Here's a quick overview of the different alert actions: Ignore, Monitor, Warn, and Block. Each action has different levels of visibility and impact."

**Visuals:**
- Show a table or infographic:

| Alert Action | Shows up in Dashboard | Developers see it (e.g. GitHub comment, CLI prints a warning) | Developers blocked (GitHub PR fails, CLI errors) |
|--------------|------------------------|-------------------------------------------------------------|-----------------------------------------------|
| Ignore       | ❌                     | ❌                                                           | ❌                                             |
| Monitor      | ✅                     | ❌                                                           | ❌                                             |
| Warn         | ✅                     | ✅                                                           | ❌                                             |
| Block        | ✅                     | ✅                                                           | ✅                                             |

---

#### [Scene 10: Summary and Benefits]
**Narrator:**
"By using the alert actions and configuring your security policy, you can ensure that your codebase remains secure and compliant with minimal manual intervention."

**Visuals:**
- Display a summary of the alert actions (Block, Warn, Monitor, Ignore).
- Highlight the benefits of automated security policy enforcement.

---

#### [Closing Scene: Call to Action]
**Narrator:**
"Thank you for watching! Start securing your repositories with Socket today. For more information, visit our documentation."

**Visuals:**
- Display the Socket website URL.
- Show the documentation link: [Socket Documentation](https://docs.socket.dev/docs/getting-started)

**Text on Screen:**
"Secure Your Codebase with Socket"
[Background Music Ends]

---

### End of Script

---

This script provides a detailed guide for creating a demo video on triaging reports alerts and organizational alerts and configuring security policies using Socket. The visual cues and narrated instructions will help viewers understand how to effectively manage alerts and enhance their security practices.
