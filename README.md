# 🛠️ System Admin Toolkit
## **📌 A Collection of PowerShell & Bash Scripts for IT Administrators**

🚀 This repository is designed for **IT Support Levels 1, 2, and 3**, as well as **System Administrators** who need automation, troubleshooting, and maintenance scripts.

---
## 🔹 **Table of Contents**
- [💡 Level 1 (Helpdesk & Support)](#-level-1-helpdesk--support)
- [🛠️ Level 2 (Advanced Troubleshooting & Networking)](#-level-2-advanced-troubleshooting--networking)
- [⚡ Level 3 (Server Admin & Automation)](#-level-3-server-admin--automation)
- [📡 System Administration (Cloud & Infrastructure)](#-system-administration-cloud--infrastructure)

---

## **💡 Level 1 (Helpdesk & Support)**
Basic troubleshooting scripts for common end-user issues.

### 🔧 **Reset Network Adapter** (Windows)
```powershell
# Reset Network Adapter
netsh int ip reset
ipconfig /release
ipconfig /renew
ipconfig /flushdns
```

### 🖥️ **Check System Uptime** (Windows & Linux)
```powershell
# Windows System Uptime
(Get-Date) - (gcim Win32_OperatingSystem).LastBootUpTime
```
```bash
# Linux System Uptime
uptime -p
```

### 🔍 **Clear Temp Files & Recycle Bin** (Windows)
```powershell
# Clears temp files and recycle bin
Remove-Item -Path "$env:TEMP\*" -Recurse -Force
Clear-RecycleBin -Confirm:$false
```

---

## **🛠️ Level 2 (Advanced Troubleshooting & Networking)**
For technicians handling more complex issues.

### 🌐 **Find Public & Private IP Address** (Windows & Linux)
```powershell
# Get Private IP
Get-NetIPAddress | Select-Object IPAddress
```
```bash
# Get Public IP (Linux)
curl -s https://api.ipify.org
```

### 🔍 **Check Open Ports on a Machine** (Windows)
```powershell
# List open ports
netstat -ano | findstr :
```

### 📡 **Ping & Traceroute Test** (Windows & Linux)
```powershell
# Windows Ping Test
Test-Connection -ComputerName google.com -Count 4
```
```bash
# Linux Traceroute
traceroute google.com
```

---

## **⚡ Level 3 (Server Admin & Automation)**
For experienced admins working with **Active Directory, PowerShell automation, and server maintenance**.

### 🛠 **Bulk Create Active Directory Users from CSV**
```powershell
Import-Csv "C:\Users.csv" | ForEach-Object {
    New-ADUser -Name $_.Name -GivenName $_.FirstName -Surname $_.LastName -SamAccountName $_.Username -UserPrincipalName "$($_.Username)@yourdomain.com" -Path "OU=Users,DC=yourdomain,DC=com" -AccountPassword (ConvertTo-SecureString "Password123" -AsPlainText -Force) -Enabled $true
}
```

### 🔐 **Force Password Reset for All Users in an OU**
```powershell
Get-ADUser -Filter * -SearchBase "OU=Users,DC=yourdomain,DC=com" | Set-ADUser -ChangePasswordAtLogon $true
```

### 🔥 **Restart a Remote Computer**
```powershell
Restart-Computer -ComputerName RemotePC -Force
```

---

## **📡 System Administration (Cloud & Infrastructure)**
Cloud and automation scripts for enterprise environments.

### 📌 **Reset Microsoft 365 User Password**
```powershell
Set-MsolUserPassword -UserPrincipalName "user@domain.com" -NewPassword "NewPassword123!" -ForceChangePassword $true
```

### 🔒 **Block User Access in Microsoft 365 Immediately**
```powershell
Set-MsolUser -UserPrincipalName "user@domain.com" -BlockCredential $true
```

### 📂 **Sync OneDrive for All Users**
```powershell
(Get-Process -Name "OneDrive") | Stop-Process -Force
Start-Process -FilePath "C:\Program Files\OneDrive\OneDrive.exe"
```

---

🚀 **This toolkit is always growing! Contributions & suggestions are welcome!**

📫 **Contact:** cameron.vester@tech901.org
