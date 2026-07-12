# Privilege Escalation

Privilege Escalation (PE) is the process of obtaining higher privileges than those originally assigned to a user, application, or process. Attackers typically begin with a low-privileged account after gaining initial access and exploit security weaknesses to obtain administrative or root privileges.

Successful privilege escalation enables attackers to:

- Access sensitive or confidential information
- Execute administrative commands
- Install malware, backdoors, or persistence mechanisms
- Disable security controls
- Modify or delete files
- Create new privileged accounts
- Move laterally across the environment
- Gain complete control over systems or domains

---

# Privilege Escalation Workflow

```
Initial Access
      │
      ▼
Low-Privilege User
      │
      ▼
System Enumeration
      │
      ▼
Identify Weaknesses
      │
      ▼
Exploit Vulnerability
      │
      ▼
Administrator / Root Access
      │
      ▼
Persistence & Lateral Movement
```

---

# Types of Privilege Escalation

## 1. Vertical Privilege Escalation

Vertical Privilege Escalation occurs when an attacker elevates privileges from a lower-level account to a higher-privileged account.

Example:

```
Guest
   ↓
Standard User
   ↓
Administrator
   ↓
SYSTEM / Root
```

Common techniques include:

- Exploiting operating system vulnerabilities
- Kernel exploits
- Missing security patches
- Weak file permissions
- Weak service permissions
- DLL Hijacking
- SUID abuse (Linux)
- Misconfigured sudo rules
- Password attacks
- Credential theft
- Token impersonation
- UAC bypass
- Exploiting scheduled tasks

---

## 2. Horizontal Privilege Escalation

Horizontal Privilege Escalation occurs when an attacker gains access to another account with the same privilege level.

Example:

```
User A
   │
   └────► User B
```

Although privilege level remains unchanged, attackers may obtain access to valuable information or credentials belonging to another user.

Common techniques include:

- Pass-the-Hash (PtH)
- Pass-the-Ticket (PtT)
- Token impersonation
- Session hijacking
- Credential theft
- Password reuse
- Remote service abuse

---

# Windows Privilege Escalation Techniques

## Operating System Vulnerabilities

- Missing Windows security patches
- Local privilege escalation exploits
- Zero-day vulnerabilities

Examples:

- NoPAC
- PrintNightmare
- PetitPotam
- SAM Account Spoofing

---

## DLL Hijacking

Many Windows applications search for required DLL files in predefined locations instead of using absolute paths.

If an attacker places a malicious DLL in a searched directory before the legitimate DLL, the application loads the malicious DLL, resulting in code execution with the application's privileges.

---

## User Account Control (UAC) Bypass

User Account Control (UAC) limits administrative privileges for applications.

Attackers may bypass UAC through:

- Auto-elevating binaries
- COM object abuse
- Registry hijacking
- Scheduled task abuse

---

## Weak Service Permissions

Examples include:

- Insecure service permissions
- Writable service binaries
- Unquoted service paths
- Weak registry permissions
- Weak service ACLs

---

## Scheduled Task Abuse

Attackers exploit:

- Writable scheduled task files
- Weak permissions
- Misconfigured scheduled tasks
- Elevated scheduled jobs

---

## Token Impersonation

Windows access tokens represent user identities.

Attackers can impersonate privileged tokens to execute commands as another user.

Examples:

- Token Kidnapping
- Incognito
- Potato family attacks

---

## Resource-Based Constrained Delegation (RBCD)

Abusing the **msDS-AllowedToActOnBehalfOfOtherIdentity** attribute allows attackers to impersonate users in Active Directory environments.

---

## Missing Patches

Unpatched Windows systems are vulnerable to known privilege escalation exploits.

Examples include:

- Kernel vulnerabilities
- Driver vulnerabilities
- Service vulnerabilities

---

## Automated Exploitation

Attackers frequently use automated scripts and exploitation frameworks to identify privilege escalation opportunities.

Examples:

- PowerUp
- PowerSploit
- WinPEAS
- PrivescCheck

---

## Execution Flow Hijacking

Manipulating application execution through:

- DLL Search Order Hijacking
- PATH Hijacking
- COM Hijacking
- Registry Hijacking

---

# Linux Privilege Escalation Techniques

Common Linux privilege escalation methods include:

## Kernel Exploits

Exploiting vulnerabilities in the Linux kernel to obtain root privileges.

---

## SUID Misconfiguration

Abusing binaries with the SUID permission bit set.

Example:

```bash
find / -perm -4000 -type f 2>/dev/null
```

---

## Sudo Misconfiguration

Abusing overly permissive sudo rules.

Example:

```bash
sudo -l
```

---

## Weak File Permissions

Examples:

- Writable `/etc/passwd`
- Writable scripts
- Writable configuration files

---

## Weak Service Permissions

Services running as root with insecure permissions.

---

## Cron Job Exploitation

Abusing scheduled cron jobs that execute writable scripts.

---

## PATH Variable Hijacking

Manipulating the PATH environment variable to execute attacker-controlled binaries.

---

## World-Writable Files

Abusing writable files or directories used by privileged processes.

---

## Installed Software Vulnerabilities

Exploiting vulnerable applications installed on the system.

---

## Weak Passwords

- Dictionary attacks
- Password reuse
- Plaintext credentials
- Credential harvesting

---

## Environment Variable Abuse

Manipulating environment variables to influence privileged processes.

---

# Active Directory Privilege Escalation

Common techniques include:

- Resource-Based Constrained Delegation (RBCD)
- NoPAC
- Kerberoasting
- AS-REP Roasting
- DCSync
- DCShadow
- Pass-the-Hash
- Pass-the-Ticket
- Golden Ticket
- Silver Ticket
- Shadow Credentials
- PetitPotam
- NTLM Relay
- AD CS attacks
- Group Policy abuse
- ACL abuse

---

# Privilege Escalation Tools

## Windows

- WinPEAS
- Seatbelt
- PowerUp
- PowerSploit
- PrivescCheck
- SharpUp
- BeRoot
- Sherlock
- Watson
- Windows Exploit Suggester

---

## Linux

- LinPEAS
- LinEnum
- Linux Exploit Suggester
- LES (Linux Exploit Suggester)
- BeRoot
- pspy
- GTFOBins
- LSE (Linux Smart Enumeration)

---

## Credential Extraction

- Mimikatz
- gsecdump
- pwdump
- fgdump
- secretsdump.py
- Meterpreter

---

# Remote Administration Tools

Legitimate administrative tools that may be abused after privilege escalation include:

- PsExec
- RemoteExec
- PDQ Deploy
- DameWare Remote Support
- PowerShell Remoting
- Windows Remote Management (WinRM)
- WMI
- SMB
- SSH

---

# Common Post-Exploitation Activities

After successful privilege escalation, attackers often:

- Dump credentials
- Extract password hashes
- Disable antivirus
- Disable endpoint detection
- Create administrator accounts
- Install persistence mechanisms
- Deploy ransomware
- Install backdoors
- Collect sensitive data
- Perform lateral movement
- Escalate to Domain Administrator
- Maintain long-term access

---

# Related MITRE ATT&CK Techniques

| Technique | MITRE ID |
|------------|----------|
| Abuse Elevation Control Mechanism | T1548 |
| Bypass User Account Control | T1548.002 |
| Exploitation for Privilege Escalation | T1068 |
| Hijack Execution Flow | T1574 |
| Access Token Manipulation | T1134 |
| Scheduled Task Abuse | T1053 |
| DLL Search Order Hijacking | T1574.001 |
| Service Abuse | T1543 |
| Sudo and SUID Abuse | T1548 |
| Valid Accounts | T1078 |

---

# Privilege Escalation Countermeasures

## Principle of Least Privilege

- Grant users only the permissions required to perform their jobs.
- Remove unnecessary administrator rights.

---

## Patch Management

- Regularly install operating system updates.
- Apply security patches promptly.
- Remove unsupported software.

---

## Secure Configuration

- Secure file permissions.
- Secure service permissions.
- Secure registry permissions.
- Secure scheduled tasks.
- Secure sudo configuration.
- Remove unnecessary SUID binaries.

---

## Identity Security

- Enable Multi-Factor Authentication (MFA)
- Use Privileged Access Management (PAM)
- Implement Just Enough Administration (JEA)
- Implement Just-In-Time (JIT) administration
- Rotate privileged credentials
- Monitor privileged account usage

---

## Application Security

- Enable code signing
- Enable application allowlisting
- Block unauthorized DLL loading
- Remove unnecessary software

---

## Monitoring and Detection

- Monitor privilege changes
- Detect abnormal administrator logins
- Monitor service modifications
- Audit scheduled task creation
- Monitor token impersonation
- Enable PowerShell logging
- Enable Sysmon
- Centralize logs in a SIEM

---

## System Hardening

- Disable unnecessary services
- Remove legacy protocols
- Restrict remote administration
- Protect LSASS
- Enable Credential Guard
- Enable Secure Boot
- Enable Windows Defender Application Control (WDAC)

---

# Key Takeaways

- Privilege escalation typically follows initial access.
- It is divided into **Vertical** and **Horizontal** privilege escalation.
- Windows and Linux have different privilege escalation vectors.
- Active Directory provides additional opportunities for privilege escalation through identity and delegation misconfigurations.
- Proper hardening, patching, least privilege, monitoring, and credential protection significantly reduce privilege escalation risk.
