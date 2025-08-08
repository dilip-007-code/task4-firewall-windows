# Windows Defender Firewall – Block Port 23 (Telnet) on Windows 

## Objective
To configure Windows Defender Firewall on a Windows  PC to block **port 23** (Telnet) and verify that the port is inaccessible, thereby improving system security.

---

## Tools Used
- Windows  (built-in **Windows Defender Firewall with Advanced Security**)
- PowerShell (for verification)

---

## Steps Followed

1. **Open Firewall Settings**
   - Press **Windows + R**, type `wf.msc`, press **Enter** to open Windows Defender Firewall with Advanced Security.

2. **Create a Rule to Block Port 23**
   - Click **Inbound Rules** in the left panel.
   - Click **New Rule…** in the right panel.
   - Select **Port** and click **Next**.
   - Select **TCP**, type `23` in “Specific local ports” → click **Next**.
   - Select **Block the connection** → click **Next**.
   - Select all profiles (**Domain**, **Private**, **Public**) → click **Next**.
   - Name the rule **Block Telnet (Port 23)** and click **Finish**.

3. **Verify the Rule**
   - Open **PowerShell** as Administrator.
   - Run:
     ```powershell
     Test-NetConnection -ComputerName <your-ip-address> -Port 23
     ```
   - The result should show:
     ```
     TcpTestSucceeded : False
     ```
     confirming the port is blocked.

---

## Screenshots

**Screenshot 1 – Rule Created**  
![Rule Created](screenshots/rule_created.png)  
*Inbound rules list showing “Block Telnet (Port 23)” in Windows Defender Firewall.*

**Screenshot 2 – Test Result**  
![Test Result](screenshots/port_test_failed.png)  
*PowerShell output showing `TcpTestSucceeded : False`, confirming port 23 is blocked.*

---

## Conclusion
Port 23 (Telnet) was successfully blocked using Windows Defender Firewall.  
Any incoming connections on this port are now denied, reducing potential security risks.  
As Telnet is outdated and insecure, keeping this port blocked does not affect normal PC usage.
