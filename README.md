# Remote Code Execution Detection / Device Isolation 

## 🎯 Objective

This project demonstrates how to detect Remote Code Execution (RCE) events on a Windows VM using Microsoft Defender for Endpoint (MDE) and Kusto Query Language (KQL). It also showcases how to isolate a compromised device.


###  Platforms and Languages Leveraged
- Windows 10 Virtual Machines (Microsoft Azure)
- MDE Platform: Microsoft Defender for Endpoint
- Kusto Query Language (KQL)
---

### 🔧 Create a Windows VM in Azure

    Provision a Windows 10/11 or Server 2019+ VM.

    Size: Small (B1s or similar).

    Public IP enabled to allow scanning (for simulation purposes).

    Enable RDP for access.

  ### 🔥 Disable the Windows Firewall

    ⚠️ Disclaimer: Disabling the firewall is for educational/demo purposes only. This exposes the VM to external threats for visibility.

    Run wf.msc → Turn off Domain, Private, and Public firewall.

### 🛡️ Onboard VM to Microsoft Defender for Endpoint (MDE)

    Use MDE onboarding package for Azure VMs.

    Verify onboarding at: Microsoft 365 Defender Portal

    Run sample hunting query to confirm logs:

<img width="700" alt="image" src="https://github.com/GbengaCyber/rce/blob/main/Screenshot%202025-04-21%20at%2013-22-24%20RCE%20Detection%20with%20KQL.png">

---
### 🧪 Simulate RCE (Remote Code Execution)

We'll simulate an RCE attempt using PowerShell to download and install 7-Zip silently.


![image](https://github.com/user-attachments/assets/ad6b9116-0918-493a-82f8-c040779c8837)

---

### 🔍 Detection with MDE/KQL

Use Advanced Hunting in the MDE Portal.

![image](https://github.com/user-attachments/assets/155876bf-81c9-495a-894d-ed909a4ea6c6)

---

### 🛑 Create Detection Rule

    Go to Advanced Hunting → Detection Rules → Create custom rule

    Use the above query as the condition.

    Choose Alert & Isolate Device as the response.

---

### 🧼 Isolate Compromised Device 

Wait/search for logs. When the logs appear, your machine should be isolated and you can move to the next step. If you can no longer connect to your VM, it’s possible the Detection Rule already executed and isolated your VM. That was the case for me:

Browse to your VM within the MDE Portal (https://security.microsoft.com/machines)
Select the VM and then click the three dots menu. If it’s isolated, observe that you can release your VM from isolation here. For now, click “Action Center” and check out the Investigation Package that was created (if it’s ready).





