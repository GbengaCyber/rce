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

<img width="1212" alt="image" src="https://github.com/user-attachments/assets/b07ac4b4-9cb3-4834-8fac-9f5f29709d78">
