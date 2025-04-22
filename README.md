# Remote Code Execution Detection / Device Isolation 


# 🧠 Project Explanation
## 🎯 Objective

This project demonstrates how to detect Remote Code Execution (RCE) events on a Windows VM using Microsoft Defender for Endpoint (MDE) and Kusto Query Language (KQL). It also showcases how to isolate a compromised device.


## Platforms and Languages Leveraged
- Windows 10 Virtual Machines (Microsoft Azure)
- MDE Platform: Microsoft Defender for Endpoint
- Kusto Query Language (KQL)
---

## 🚀 Step-by-Step Guide
🔧 Create a Windows VM in Azure

    Provision a Windows 10/11 or Server 2019+ VM.

    Size: Small (B1s or similar).

    Public IP enabled to allow scanning (for simulation purposes).

    Enable RDP for access.

  ## 🔥 Disable the Windows Firewall

    ⚠️ Disclaimer: Disabling the firewall is for educational/demo purposes only. This exposes the VM to external threats for visibility.

    Run wf.msc → Turn off Domain, Private, and Public firewall.

## 🛡️ Onboard VM to Microsoft Defender for Endpoint (MDE)

    Use MDE onboarding package for Azure VMs.

    Verify onboarding at: Microsoft 365 Defender Portal

    Run sample hunting query to confirm logs:

<img width="700" alt="image" src="https://github.com/GbengaCyber/rce/blob/main/Screenshot%202025-04-21%20at%2013-22-24%20RCE%20Detection%20with%20KQL.png">

---
## 🧪 Simulate RCE (Remote Code Execution)

We'll simulate an RCE attempt using PowerShell to download and install 7-Zip silently.


![image](https://github.com/user-attachments/assets/ad6b9116-0918-493a-82f8-c040779c8837)


👉 Guide: detection/powershell_rce_simulation.md
5. 🔍 Detect with KQL

Use Advanced Hunting in the MDE Portal.
📌 Sample KQL Query

DeviceProcessEvents
| where InitiatingProcessFileName =~ "cmd.exe"
| where ProcessCommandLine has "Invoke-WebRequest"
| where ProcessCommandLine has "7z2408-x64.exe"
| project Timestamp, DeviceName, FileName, ProcessCommandLine, InitiatingProcessFileName, InitiatingProcessCommandLine


🛑 Create Detection Rule

    Go to Advanced Hunting → Detection Rules → Create custom rule

    Use the above query as the condition.

    Choose Alert & Isolate Device as the response.

👉 Guide: detection/create_detection_rule.md
7. 🧼 Isolate Compromised Device (Optional but recommended)

If the alert fires, manually or automatically isolate the device to cut off its network access (except to MDE).
