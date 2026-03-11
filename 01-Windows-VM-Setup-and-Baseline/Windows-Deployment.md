# Windows 10 Endpoint Setup & Baseline Telemetry

## Objective
Build a Windows 10 virtual machine and configure it to generate endpoint telemetry using **Sysmon** for security monitoring.

This system will later be used as a **target endpoint for detection and investigation labs**.

---

# 1. Windows 10 Virtual Machine Build

## Create the Virtual Machine

1. Open **VirtualBox** (or VMware).
2. Create a new VM with the following configuration:

| Setting | Value |
|---|---|
| Type | Microsoft Windows |
| Version | Windows 10 (64-bit) |
| RAM | 4096 MB (minimum) |
| CPU | 2 cores |
| Disk | 50 GB (dynamically allocated) |

3. Attach the official **Windows 10 ISO**.
4. Start the VM and complete installation.

![image](https://github.com/miholmestech/SOC-Analyst-Projects-/blob/main/01-Windows-VM-Setup-and-Baseline/screenshots/01-windows-setup.png)

### Windows Setup Choices

During the Windows setup process:

- Select **Offline Account**
- Skip **Microsoft sign-in**
- Skip extras such as:
  - Cortana
  - OneDrive
  - Suggested services

---

# 2. Prepare the System for Logging

Open **PowerShell as Administrator**.

### Check PowerShell Execution Policy

```powershell
Get-ExecutionPolicy
```

If the policy is **Restricted**, change it:

```powershell
Set-ExecutionPolicy RemoteSigned
```

When prompted, enter:

```
Y
```

This allows locally created scripts and signed scripts to run.


![image](https://github.com/miholmestech/SOC-Analyst-Projects-/blob/main/01-Windows-VM-Setup-and-Baseline/screenshots/03-windows-setup.png)

---

# 3. VirtualBox Display Troubleshooting

The VM initially had **screen scaling issues**.

### Install Guest Additions

While the VM is running:

```
Devices → Insert Guest Additions CD Image
```

Inside Windows:

1. Open **File Explorer**
2. Navigate to:

```
This PC
```

3. Open the **VirtualBox Guest Additions CD**
4. Run:

```
VBoxWindowsAdditions.exe
```

Enable:

- Direct3D Support

After installation:

- Reboot the VM

Display scaling was restored using:

```
Right Ctrl + F (twice)
```
It took a while to take effectduring loading, but the scaling issues were resolved.


![image](https://github.com/miholmestech/SOC-Analyst-Projects-/blob/main/01-Windows-VM-Setup-and-Baseline/screenshots/04-windows-setup.png)

---

# 4. Install Sysmon

Sysmon provides detailed **endpoint telemetry** such as:

- Process creation
- Network connections
- File creation
- Registry modifications

### Create Sysmon Directory

```powershell
mkdir C:\Sysmon
```

Move the following files into:

```
C:\Sysmon
```

Required files:

- `Sysmon64.exe` (downloaded from Microsoft Sysinternals)
- `sysmonconfig.xml` (SwiftOnSecurity configuration)


![image](https://github.com/miholmestech/SOC-Analyst-Projects-/blob/main/01-Windows-VM-Setup-and-Baseline/screenshots/sysmon-install%20.png)

---

# 5. Install Sysmon Service

From **Administrator PowerShell** inside `C:\Sysmon`:

```powershell
sysmon64.exe -accepteula -i sysmonconfig.xml
```

### Installation Output

```
Configuration file validated.
Sysmon64 installed.
SysmonDrv installed.
Starting SysmonDrv.
SysmonDrv started.
Starting Sysmon64.
Sysmon64 started.
```

![image](https://github.com/miholmestech/SOC-Analyst-Projects-/blob/main/01-Windows-VM-Setup-and-Baseline/screenshots/sysmon-install-2.png)

---

# 6. Verify Sysmon Service

Attempted verification using:

```powershell
sc query sysmon64
```

No response was returned.

---

# 7. Verify Sysmon Telemetry via Event Viewer

Although the following command was used to check the Sysmon service:

```powershell
sc query sysmon64
```

No response was returned.

To confirm that Sysmon was still functioning correctly, the logs were verified directly in **Event Viewer**.

### Steps

1. Open **Event Viewer**
2. Navigate to:

```
Applications and Services Logs
→ Microsoft
→ Windows
→ Sysmon
→ Operational
```

3. Review the event logs.

### Observed Events

| Event ID | Description |
|---|---|
| 1 | Process Create |

---

# 8. Validation

Although the `sc query sysmon64` command did not return a response, verification through **Event Viewer** confirmed that Sysmon was successfully generating endpoint telemetry. Event ID 1 (Process Create) events were observed in the Sysmon Operational log, confirming that Sysmon was installed and functioning correctly.

This validation confirmed that the Windows endpoint was successfully configured to generate security-relevant telemetry for future detection and investigation exercises.




