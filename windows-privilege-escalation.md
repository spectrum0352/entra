This is a cleaned, organized, and GitHub-friendly outline. It removes duplicates, corrects terminology, groups related topics, and follows a logical learning path suitable for a Windows Privilege Escalation guide.

# Windows Privilege Escalation

## Introduction

Privilege Escalation is the process of gaining higher privileges on a system after obtaining an initial foothold. In Windows environments, attackers typically elevate from a standard user account to an Administrator or **NT AUTHORITY\SYSTEM** account by exploiting misconfigurations, weak permissions, vulnerable services, scheduled tasks, credential exposure, or operating system vulnerabilities.

> **MITRE ATT&CK Technique:** **T1548 – Abuse Elevation Control Mechanism**
> Related techniques include:
>
> * T1547 – Boot or Logon Autostart Execution
> * T1574 – Hijack Execution Flow
> * T1134 – Access Token Manipulation
> * T1053 – Scheduled Task/Job
> * T1068 – Exploitation for Privilege Escalation

---

# Lab Setup

## Target Environment

* Windows 10
* Windows 11
* Windows Server 2016
* Windows Server 2019
* Windows Server 2022

## Required Tools

### Enumeration

* WinPEAS
* Seatbelt
* PowerUp
* SharpUp
* Watson
* Sherlock
* Windows Exploit Suggester
* PrivescCheck
* AccessChk (Sysinternals)
* Process Explorer
* Autoruns
* Sysinternals Suite

### Exploitation

* Metasploit
* PrintSpoofer
* JuicyPotato
* RoguePotato
* GodPotato
* RottenPotato
* SharpEfsPotato
* Mimikatz
* PsExec

### Development

* Visual Studio
* Visual Studio Code
* Mingw-w64
* Microsoft Build Tools

---

# Types of Windows Privilege Escalation

## 1. Service Misconfigurations

* Insecure Service Permissions
* Weak Service DACL
* Service Binary Replacement
* Unquoted Service Path
* Weak Registry Permissions
* Insecure Service Executables
* DLL Hijacking
* Writable Service Folders

---

## 2. Scheduled Tasks

(MITRE T1053)

### Windows Task Scheduler

* Task Scheduler architecture
* XML task definitions
* Trigger types
* Security context

### Misconfigured Scheduled Tasks

* Writable task binaries
* Weak permissions
* Writable scripts
* Writable folders

### Scheduled Task Abuse

* Binary replacement
* Script modification
* Task creation
* Task execution

### Detection

* Event Logs
* Task Scheduler logs
* Sysmon
* Microsoft Defender

### Mitigation

* Least privilege
* File ACL hardening
* Code signing
* Protected folders

---

# Windows Services

## Insecure Service Properties

* SERVICE_CHANGE_CONFIG
* SERVICE_START
* SERVICE_STOP

---

## Unquoted Service Path

* How Windows parses paths
* Exploitation process
* Detection
* Prevention

---

## Weak Registry Permissions

* Writable registry keys
* Service registry permissions
* Autorun registry permissions

---

## Insecure Service Executables

* Writable executable
* Writable directory
* Binary replacement

---

## Weak GUI Applications

* Auto-update mechanisms
* Writable installation folders
* DLL Search Order Hijacking

---

# Kernel Exploitation

## Windows Kernel

* Kernel architecture
* Ring levels
* User mode vs Kernel mode

---

## Vulnerability Enumeration

* System Information
* Build Number
* Installed Hotfixes
* Missing Security Patches

---

## Exploit Compilation

* Visual Studio
* Mingw
* Cross-compilation
* Payload generation

---

## Kernel Exploit Hunting

* Windows Exploit Suggester
* Watson
* Sherlock
* CVE research
* Exploit-DB
* GitHub PoCs

---

# Logon Autostart Execution

(MITRE T1547)

## Registry Run Keys

* HKLM Run
* HKCU Run
* RunOnce
* RunServices

---

## Startup Folder

* User Startup Folder
* All Users Startup Folder

---

## AlwaysInstallElevated

* Registry configuration
* MSI abuse
* Detection
* Mitigation

---

## Winlogon

* Userinit
* Shell
* Notify Packages

---

# Password Hunting

## Registry

* AutoLogon credentials
* Stored passwords
* Registry secrets

---

## Windows Credential Manager

* cmdkey
* Vault
* RunAs credentials
* Saved RDP credentials

---

## Configuration Files

Search for credentials in:

* XML
* JSON
* YAML
* INI
* TXT
* BAT
* PS1
* CMD
* IIS Config
* Web.config
* Application Config Files

---

## Unattended Installation Files

* Unattend.xml
* Sysprep.xml
* Sysprep.inf
* Unattend.txt

---

## PowerShell History

* ConsoleHost_history.txt

---

## Browser Credentials

* Chrome
* Edge
* Firefox

---

## Database Credentials

* SQL Server
* MySQL
* Oracle

---

## Brute Force

* Local Accounts
* Administrator Account
* Service Accounts
* Password Spraying

---

# ACL & Permission Abuse

## Windows ACL Fundamentals

* Security Descriptor
* DACL
* SACL
* ACE
* SID
* Integrity Levels

---

## Common Permission Abuse

* Weak File ACL
* Weak Folder ACL
* Writable Registry Keys
* Service DACL Abuse
* Scheduled Task Permissions

---

## AccessChk Enumeration

* Files
* Services
* Registry
* Processes
* Named Pipes

---

# User Rights & Privileges

## SeBackupPrivilege

* Read protected files
* Registry backup
* NTDS extraction

---

## SeRestorePrivilege

* Replace protected files
* Registry restoration
* File overwrite

---

## SeTakeOwnershipPrivilege

* Taking ownership of objects

---

## SeImpersonatePrivilege

Token impersonation attacks:

* Rotten Potato
* Juicy Potato
* Rogue Potato
* PrintSpoofer
* SharpEfsPotato
* GodPotato

(MITRE T1134)

---

## SeAssignPrimaryTokenPrivilege

* Token replacement
* Process creation

---

## SeDebugPrivilege

* Process memory access
* SYSTEM process interaction

---

# UAC Bypass

## User Account Control

* UAC internals
* Integrity Levels
* Auto-elevated binaries

### Common UAC Bypass Techniques

* fodhelper.exe
* computerdefaults.exe
* sdclt.exe
* eventvwr.exe
* SilentCleanup
* DLL Hijacking

---

# Registry Hive Attacks

## SAM & SYSTEM Hive Extraction

* reg save
* Volume Shadow Copy
* Offline extraction

---

## HiveNightmare (SeriousSAM)

* CVE-2021-36934
* Exploitation
* Detection
* Mitigation

---

# Additional Privilege Escalation Techniques

## DLL Hijacking

* Search Order Hijacking
* Phantom DLL
* Side Loading

---

## PATH Environment Variable Hijacking

* Writable PATH directories
* Executable replacement

---

## COM Hijacking

* CLSID abuse
* Registry modification

---

## Named Pipe Impersonation

* Token stealing
* Privilege escalation

---

## MSI Installer Abuse

* AlwaysInstallElevated
* Malicious MSI packages

---

## Driver Exploitation

* Vulnerable Drivers
* Bring Your Own Vulnerable Driver (BYOVD)

---

## Device Object Abuse

* Weak device permissions
* Driver vulnerabilities

---

# Enumeration Checklist

* User Information
* Groups
* Privileges
* Processes
* Services
* Drivers
* Installed Software
* Scheduled Tasks
* Startup Applications
* Registry
* File Permissions
* Folder Permissions
* Environment Variables
* Running Ports
* Network Shares
* Credential Storage
* Browser Passwords
* PowerShell History
* Event Logs
* Installed Hotfixes
* Antivirus & EDR
* Windows Defender Configuration

---

# Detection & Mitigation

## Monitoring

* Microsoft Defender for Endpoint
* Microsoft Sentinel
* Sysmon
* Windows Event Logs
* Microsoft Defender XDR

## Hardening

* Least Privilege
* Remove Unnecessary Privileges
* Patch Management
* WDAC
* AppLocker
* Defender ASR Rules
* Credential Guard
* LAPS / Windows LAPS
* Protected Users Group
* Secure ACL Configuration
* Disable AlwaysInstallElevated
* Secure Service Permissions
* Monitor Scheduled Tasks
* Remove Unquoted Service Paths
* Regular Security Audits

---

# Recommended Tools

## Enumeration

* WinPEAS
* Seatbelt
* SharpUp
* PowerUp
* PrivescCheck
* Watson
* Sherlock
* Windows Exploit Suggester
* AccessChk
* Autoruns
* Process Explorer

## Credential Access

* Mimikatz
* LaZagne
* Seatbelt

## Exploitation

* PrintSpoofer
* JuicyPotato
* GodPotato
* PsExec
* Metasploit

---

## MITRE ATT&CK Mapping

| Technique                             | MITRE ID  |
| ------------------------------------- | --------- |
| Abuse Elevation Control Mechanism     | T1548     |
| Scheduled Task/Job                    | T1053     |
| Boot or Logon Autostart Execution     | T1547     |
| Access Token Manipulation             | T1134     |
| Hijack Execution Flow                 | T1574     |
| Exploitation for Privilege Escalation | T1068     |
| DLL Search Order Hijacking            | T1574.001 |
| Create or Modify System Process       | T1543     |
| Valid Accounts                        | T1078     |

This structure is suitable for a comprehensive GitHub repository and can serve as the table of contents for a detailed Windows Privilege Escalation handbook.
