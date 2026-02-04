# Endpoint Compromise Detection & Threat Containment (SOC Lab 02)

## Objective
Simulate an endpoint security alert on a Windows 10 finance workstation and investigate suspicious PowerShell activity using Sysmon in an environment without EDR or SIEM.

## Environment
- Windows 10 VM (finance user)
- Sysmon with custom configuration
- Event Viewer (Sysmon Operational logs)

## Scenario Summary
Suspicious encoded PowerShell executed on the endpoint, followed by DNS queries and an outbound network connection to 104.18.27.120 over TCP 443. Host-based telemetry was used to assess whether this activity was benign or malicious.

## Investigation Highlights
- Correlated Sysmon Event IDs 1, 3, 11, and 22 for process, file, DNS, and network activity.
- Identified an encoded PowerShell command and outbound HTTPS connection.
- Mapped behavior to MITRE ATT&CK (T1059.001, T1027, potential T1105).
- Overall assessment: suspicious behavior but no confirmed malicious payload based on available evidence.

## Full Report
See the detailed SOC-style report with timeline, indicators, ATT&CK mapping, and containment recommendations:  
[Full SOC-Style Report (Markdown)](./report.md)  <!-- or create report.md and link that instead -->

## Screenshots
Screenshots of key Sysmon events are available in the [`screenshots/`](./screenshots) folder.

