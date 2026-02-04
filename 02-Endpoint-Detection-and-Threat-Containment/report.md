# Report

This project simulates an endpoint security alert triggered on a Windows 10 workstation used by a member of the finance team in an environment without EDR or SIEM tooling. I investigated the alert using host-based telemetry to determine whether the activity was benign or indicative of a potential threat, and documented the resulting analysis and containment actions.

## Timeline of events

~11:04:11 – Sysmon Event ID 11 (FileCreate): File creation observed (Process ID 8904).

~11:04:16 – Sysmon Event ID 1 (Process Create): PowerShell.exe process created (Process ID 2996).

~11:04:16 – Sysmon Event ID 11 (FileCreate): File creation associated with PowerShell.exe (Process ID 2996).

~11:04:20 – Sysmon Event ID 22 (DNS Query): DNS request issued by PowerShell.exe (Process ID 2996).

~11:04:21 – Sysmon Event ID 3 (Network Connection): Outbound network connection from PowerShell.exe (Process ID 2996).

## Observed indicators and behavioral findings

PowerShell executed with encoded command (Sysmon Event ID 1).

Outbound network connection initiated by PowerShell.exe to IP 104.18.27.120 on TCP 443 (Sysmon Event ID 3).  

DNS query preceding external connection (Sysmon Event ID 22).  

File creation activity following PowerShell execution (Sysmon Event ID 11).

These indicators were observed and assessed in context, but no clearly malicious verdict was supported by the available evidence (destination IP belongs to a common Cloudflare-backed service rather than a known threat infrastructure)

## MITRE ATT&CK mapping

**T1059.001 – PowerShell**  
Sub-technique of: [T1059](https://attack.mitre.org/techniques/T1059)  
Tactic: Execution  
Evidence: PowerShell process creation observed with suspicious command-line arguments (Event ID 1).

**T1027 – Obfuscated Files or Information**  
Tactic: Defense Evasion  
Evidence: Base64-encoded command observed in PowerShell execution (Event ID 1).

**T1105 – Ingress Tool Transfer**  
Tactic: Command and Control  
Evidence: Powershell.exe initiated DNS queries and outbound network connections to an external destination followed by file creation activity (Sysmon Event IDs 22, 3, and 11), which can be consistent with downloading or staging external content.[web:51]

## Containment and remediation recommendations

Isolate the affected endpoint from the network pending further investigation.

Implement EDR tooling to improve endpoint visibility.

Centralize logs in a SIEM for correlation and alerting.

Restrict or monitor PowerShell usage via policy.

Provide user security awareness training for finance personnel.

