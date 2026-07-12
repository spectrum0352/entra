# Azure RBAC (Role-Based Access Control)

## Table of Contents

* Overview
* Azure RBAC Learning Resources
* Azure RBAC Concepts
* Azure Built-in Roles
* Microsoft Entra Roles vs Azure RBAC Roles
* Managed Identities
* Azure Key Vault RBAC
* Local Accounts vs Active Directory Accounts
* RBAC Standard Operating Procedure (SOP)
* Recommended RBAC Group Design
* Privileged Identity Management (PIM)
* Azure RBAC Best Practices
* Monitoring and Auditing
* Frequently Asked Questions

---

# Azure Role-Based Access Control (Azure RBAC)

Azure Role-Based Access Control (Azure RBAC) is the authorization system used to manage access to Azure resources. RBAC enables organizations to assign permissions based on the principle of least privilege, ensuring users, groups, service principals, and managed identities have only the permissions required to perform their tasks.

RBAC can be assigned at multiple scopes:

* Management Group
* Subscription
* Resource Group
* Individual Resource

Permissions assigned at a higher scope are inherited by child resources.

---

# Microsoft Learn Resources

* [https://learn.microsoft.com/azure/role-based-access-control/](https://learn.microsoft.com/azure/role-based-access-control/)
* [https://learn.microsoft.com/training/modules/secure-azure-resources-with-rbac/](https://learn.microsoft.com/training/modules/secure-azure-resources-with-rbac/)

Topics include:

* Access management for Azure resources
* List existing role assignments
* Assign Azure roles
* Custom Azure roles
* Azure RBAC best practices

---

# Azure RBAC Concepts

Azure RBAC provides authorization through:

* Security Principals

  * Users
  * Groups
  * Service Principals
  * Managed Identities

* Role Definitions

  * Built-in Roles
  * Custom Roles

* Scope

  * Management Group
  * Subscription
  * Resource Group
  * Resource

* Role Assignment

```
Security Principal
        │
        ▼
Role Assignment
        │
        ▼
Role Definition
        │
        ▼
Scope
```

---

# Azure Built-in Roles

| Role                        | Description                                       |
| --------------------------- | ------------------------------------------------- |
| Owner                       | Full management access including role assignments |
| Contributor                 | Manage all resources except RBAC assignments      |
| Reader                      | View resources only                               |
| User Access Administrator   | Manage RBAC assignments only                      |
| Reader and Data Access      | Read resources including storage data             |
| Virtual Machine Contributor | Manage virtual machines only                      |
| Network Contributor         | Manage networking resources                       |
| Storage Account Contributor | Manage storage accounts                           |
| Key Vault Administrator     | Full Key Vault management                         |
| Key Vault Secrets Officer   | Manage secrets                                    |
| Security Administrator      | Configure Microsoft Defender security settings    |
| Security Reader             | Read security posture and alerts                  |

---

# Azure RBAC vs Microsoft Entra Roles

These are different authorization systems.

## Azure RBAC

Controls access to Azure resources.

Examples:

| Role                      | Purpose                  |
| ------------------------- | ------------------------ |
| Owner                     | Full resource management |
| Contributor               | Manage resources         |
| Reader                    | View resources           |
| User Access Administrator | Assign Azure roles       |

Scope:

* Management Group
* Subscription
* Resource Group
* Resource

---

## Microsoft Entra Roles

Control administration of Microsoft Entra ID (formerly Azure AD).

Examples:

| Role                            | Purpose                   |
| ------------------------------- | ------------------------- |
| Global Administrator            | Full Entra administration |
| Privileged Role Administrator   | Manage privileged roles   |
| User Administrator              | Manage users and groups   |
| Authentication Administrator    | Authentication methods    |
| Security Administrator          | Manage identity security  |
| Cloud Application Administrator | Enterprise Applications   |
| Billing Administrator           | Billing and subscriptions |

Scope:

* Microsoft Entra Tenant

---

# Managed Identity

Managed Identity eliminates the need to store credentials in applications.

Types:

## System Assigned

* One identity per Azure resource
* Lifecycle tied to resource
* Automatically deleted

Examples:

* Azure VM
* App Service
* Function App

---

## User Assigned

* Standalone Azure resource
* Can be attached to multiple resources
* Independent lifecycle

---

## Common Use Cases

* Access Azure Key Vault
* Access Storage Account
* Access SQL Database
* Access Azure Monitor
* Access Microsoft Graph
* Access Event Hub

Benefits:

* No password management
* Automatic credential rotation
* Supports Azure RBAC
* Secure authentication

---

# Azure Key Vault Authorization

Azure Key Vault supports two authorization models.

## Azure RBAC (Recommended)

Uses Azure RBAC roles.

Examples:

* Key Vault Administrator
* Key Vault Secrets Officer
* Key Vault Secrets User
* Key Vault Crypto Officer

Advantages:

* Centralized permission management
* PIM integration
* Auditing
* Conditional Access support

---

## Access Policies (Legacy)

Older authorization model.

Microsoft recommends using Azure RBAC for new deployments.

---

# Analyze Azure Role Permissions

Useful commands:

```powershell
Get-AzRoleAssignment
```

```powershell
Get-AzRoleDefinition
```

Azure CLI

```bash
az role assignment list
```

```bash
az role definition list
```

---

# Why Are Local Accounts Easier to Compromise than Active Directory Accounts?

Local accounts are generally more vulnerable because:

* Authentication occurs locally.
* Password policies may be weaker.
* Often lack centralized monitoring.
* No centralized account lockout.
* Less visibility into suspicious logins.
* Cannot leverage enterprise identity protections.

Microsoft Entra ID or Active Directory accounts benefit from:

* Centralized authentication
* MFA
* Conditional Access
* Identity Protection
* Smart Lockout
* Continuous monitoring
* Security analytics

**Note:** A properly secured local account with technologies such as Windows LAPS, BitLocker, Secure Boot, and strong password policies can still provide strong security. The comparison assumes a typical enterprise deployment.

---

# Azure RBAC Standard Operating Procedure (SOP)

## 1. Purpose

The purpose of this SOP is to implement Azure RBAC according to the Principle of Least Privilege.

Objectives:

* Reduce excessive permissions
* Improve governance
* Meet compliance requirements
* Protect Azure resources

---

## 2. Scope

Applies to:

* Management Groups
* Subscriptions
* Resource Groups
* Azure Resources
* Users
* Groups
* Service Principals
* Managed Identities

---

## 3. Roles and Responsibilities

### Security Team

* Create custom roles
* Review role assignments
* Audit permissions

### Resource Owners

* Identify required permissions
* Approve access requests

### Users

* Use assigned permissions responsibly
* Avoid privilege escalation

---

## 4. RBAC Procedures

### Step 1 — Identify Required Permissions

Determine:

* Required resources
* Required actions
* Required duration

Grant only necessary permissions.

---

### Step 2 — Use Built-in Roles

Prefer Microsoft built-in roles whenever possible.

Only create custom roles if required.

---

### Step 3 — Create Custom Roles

If needed:

* Define allowed actions
* Exclude unnecessary permissions
* Document purpose
* Test before production

---

### Step 4 — Assign Roles

Assign roles to:

* Microsoft Entra Groups (preferred)
* Managed Identities
* Service Principals

Avoid assigning roles directly to users whenever possible.

---

### Step 5 — Review Permissions

Review:

* Monthly
* Quarterly
* After employee role changes
* After projects complete

Remove unused access.

---

# Monitoring and Auditing

Monitor using:

* Azure Activity Log
* Microsoft Entra Sign-in Logs
* Audit Logs
* Azure Monitor
* Microsoft Sentinel
* Defender for Cloud

Audit:

* Privileged role assignments
* Failed role assignments
* Unauthorized changes
* Custom role usage

---

# Recommended RBAC Group Design

## Global Read-Only Group

| Group                  | Role   |
| ---------------------- | ------ |
| gr-company-all-readers | Reader |

---

## DevOps

### Production

| Group          | Default Role |
| -------------- | ------------ |
| gr-devops-prod | Reader       |

Eligible through PIM:

* Contributor

---

### Non-Production

| Group             | Role        |
| ----------------- | ----------- |
| gr-devops-nonprod | Contributor |

---

## Security

### Production

| Group            | Role                   |
| ---------------- | ---------------------- |
| gr-security-prod | Security Administrator |

---

### Non-Production

| Group               | Role                   |
| ------------------- | ---------------------- |
| gr-security-nonprod | Security Administrator |

---

## Network Team

| Group      | Role                |
| ---------- | ------------------- |
| gr-network | Network Contributor |

---

## Migration Team

| Group        | Role        |
| ------------ | ----------- |
| gr-migration | Contributor |

---

## Administrators

Permanent Owner assignments should be avoided.

Instead:

* Reader by default
* Owner via Microsoft Entra PIM
* Time-limited activation

---

# Privileged Identity Management (PIM)

Production environments should use Microsoft Entra PIM.

Recommended configuration:

* Eligible assignments
* Just-In-Time elevation
* MFA required
* Approval workflow
* Business justification
* Ticket number
* Activation duration (1–8 hours)
* Notifications
* Access reviews

Never assign permanent Owner or Global Administrator roles unless absolutely required.

---

# Azure RBAC Best Practices

* Apply the Principle of Least Privilege.
* Assign roles to groups instead of individual users.
* Use built-in roles whenever possible.
* Minimize the number of custom roles.
* Use PIM for privileged roles.
* Enable MFA for privileged accounts.
* Perform periodic access reviews.
* Remove inactive accounts promptly.
* Monitor Azure Activity Logs and Microsoft Entra Audit Logs.
* Enable Microsoft Defender for Cloud recommendations.
* Use Azure Policy to enforce governance.
* Separate Production and Non-Production permissions.
* Avoid permanent Owner assignments.
* Use Managed Identities instead of storing secrets.
* Prefer Azure Key Vault RBAC over legacy access policies.

---

# Frequently Asked Questions (FAQ)

## Is there a single portal that shows every Azure permission a user has?

**Short answer:** No.

There is currently no native Azure or Microsoft Entra portal that provides a complete, tenant-wide view of every effective permission a user has across all Azure resources.

### Available Options

You can use:

* Microsoft Entra Role Assignments
* Azure RBAC IAM blade
* Azure Resource Graph
* Azure Activity Logs
* Microsoft Graph API
* Azure CLI
* Azure PowerShell
* Azure Policy
* Microsoft Entra Access Reviews
* Microsoft Entra Privileged Identity Management
* Microsoft Sentinel
* Third-party Identity Governance solutions

For a comprehensive tenant-wide view, organizations typically build custom reporting using Microsoft Graph, Azure Resource Graph, Azure PowerShell, or Azure CLI, or use Identity Governance platforms.

---

This version is optimized for GitHub Markdown, removes duplicate content, corrects outdated Azure AD terminology to Microsoft Entra ID, updates RBAC guidance to current Microsoft best practices, and provides a cleaner, structured document suitable for technical documentation.
