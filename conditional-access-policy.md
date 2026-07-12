# Microsoft Entra Conditional Access

## Overview

**Microsoft Entra Conditional Access (CA)** is a policy-based access control framework that protects organizational resources by evaluating multiple identity and security signals before granting access.

Instead of relying only on usernames and passwords, Conditional Access evaluates contextual information such as user identity, device health, location, application, and risk level to make real-time access decisions.

Conditional Access is one of the core technologies used to implement a **Zero Trust** security model.

> Conditional Access policies are evaluated **after successful first-factor authentication** and before access to the requested resource is granted.

---

# How Conditional Access Works

```
User Sign-in
      │
      ▼
First Factor Authentication
      │
      ▼
Evaluate Signals
      │
      ├── User Identity
      ├── Group Membership
      ├── Device
      ├── Location
      ├── Application
      ├── Client App
      ├── User Risk
      ├── Sign-in Risk
      └── Threat Intelligence
      │
      ▼
Conditional Access Policy Evaluation
      │
      ├── Block Access
      ├── Grant Access
      └── Grant Access with Additional Controls
                │
                ├── MFA
                ├── Compliant Device
                ├── Hybrid Joined Device
                ├── Approved Client App
                └── App Protection Policy
```

---

# Why Use Conditional Access?

Conditional Access helps organizations:

- Protect identities and applications
- Reduce the attack surface
- Enforce Zero Trust security
- Control access based on real-time conditions
- Meet compliance and governance requirements
- Improve user productivity
- Reduce security management costs
- Respond automatically to identity risks

---

# Components of a Conditional Access Policy

Every Conditional Access policy consists of three major parts:

1. Assignments
2. Conditions
3. Access Controls

---

# Identity and Security Signals

Conditional Access evaluates multiple signals before making an access decision.

## Identity Signals

- User
- Group membership
- Directory role
- Workload identity
- External guest

## Device Signals

- Device platform
- Device compliance
- Microsoft Entra Hybrid Joined status
- Device ID
- Operating system version
- Manufacturer
- Device model

Supported platforms include:

- Windows
- macOS
- Linux
- Android
- iOS/iPadOS

## Location Signals

- Named locations
- Trusted locations
- Country
- Region
- IP address
- VPN detection

## Application Signals

- Microsoft 365 applications
- Azure Portal
- Custom Enterprise Applications
- SaaS Applications
- All Cloud Apps

## Client Application Signals

- Browser
- Mobile applications
- Desktop applications
- Exchange ActiveSync
- Legacy authentication protocols

## Risk Signals

Collected from Microsoft Entra ID Protection and Microsoft Security products.

Examples include:

- User Risk
- Sign-in Risk
- Impossible Travel
- Anonymous IP
- Malware-linked IP
- Password Spray
- Leaked Credentials
- Atypical Travel
- Token Theft
- Suspicious Sign-ins

Risk-based policies require:

- **Microsoft Entra ID P2 License**

---

# Conditional Access Decisions

A policy can make one of the following decisions.

## Block Access

Access is denied immediately.

Examples:

- High-risk sign-in
- Unsupported country
- Legacy authentication
- Unknown device

---

## Grant Access

Access is allowed without additional controls.

---

## Grant Access with Requirements

Access is granted only if one or more controls are satisfied.

Available controls include:

- Require Multi-Factor Authentication (MFA)
- Require Authentication Strength
- Require device to be compliant
- Require Microsoft Entra Hybrid Joined device
- Require approved client application
- Require App Protection Policy
- Require password change (risk-based)
- Require Terms of Use acceptance

Administrators can require:

- All selected controls
- One of the selected controls

---

# Conditional Access Assignments

Assignments determine who and what the policy applies to.

## Users

Include:

- All users
- Selected users
- Selected groups
- Directory roles
- Guests
- External users
- Workload identities

Exclude:

- Emergency access accounts
- Break-glass accounts
- Service accounts
- Selected users or groups

---

## Target Resources

Policy can apply to:

### Cloud Apps

- All cloud apps
- Selected cloud apps
- Microsoft 365
- Azure Portal
- Custom applications

### User Actions

Examples:

- Register security information
- Register or join devices

### Authentication Context

Authentication Context enables applications such as:

- SharePoint Online
- Microsoft Defender for Cloud Apps

to request stronger authentication only for sensitive actions.

---

# Conditions

Conditions determine **when** the policy should apply.

## User Risk

Examples:

- Low
- Medium
- High

---

## Sign-in Risk

Examples:

- Low
- Medium
- High

---

## Device Platform

Examples:

- Windows
- Linux
- macOS
- Android
- iOS

---

## Locations

Examples:

- India
- United States
- Trusted Office
- Named Locations
- Blocked Countries

---

## Client Apps

Examples:

- Browser
- Mobile App
- Desktop Client
- Exchange ActiveSync
- Other Legacy Clients

---

## Filter for Devices

Filter using:

- Device ID
- Device Name
- Operating System
- OS Version
- Manufacturer
- Model
- Compliance State
- Trust Type

---

# Access Controls

## Grant Controls

Available controls include:

- Require Multi-Factor Authentication
- Require Authentication Strength
- Require Device Compliance
- Require Microsoft Entra Hybrid Joined Device
- Require Approved Client App
- Require App Protection Policy
- Require Password Change (Identity Protection)

Choose:

- Require all selected controls
- Require one selected control

---

## Block Control

Completely deny access.

---

## Session Controls

Session controls help protect active sessions.

Examples include:

- Sign-in Frequency
- Persistent Browser Session
- Continuous Access Evaluation (CAE)
- Application Enforced Restrictions
- Defender for Cloud Apps Session Control
- Limited Browser Experience

---

# Continuous Access Evaluation (CAE)

Continuous Access Evaluation allows Microsoft Entra ID to revoke access immediately after critical security events.

Examples:

- User disabled
- Password changed
- Account deleted
- MFA requirement changes
- High-risk detection

Benefits:

- Reduced token lifetime dependency
- Faster policy enforcement
- Better security

---

# Device-Enforced Restrictions

Organizations can enforce restrictions based on device trust.

Examples:

- Read-only SharePoint access
- Block downloads
- Restrict copy/paste
- Restrict printing
- Require managed device

---

# Security Defaults vs Conditional Access

## Security Defaults

Security Defaults provide basic identity protection without requiring policy configuration.

Features include:

- Require users to register for MFA
- 14-day MFA registration period after first sign-in
- Require administrators to use MFA
- Protect Azure Portal access
- Block legacy authentication
- Require MFA when risk is detected

Security Defaults are intended for smaller organizations without Conditional Access policies.

---

## Conditional Access

Conditional Access provides granular control over authentication and authorization.

Capabilities include:

- User targeting
- Group targeting
- Device targeting
- Risk-based access
- Application-specific policies
- Session controls
- Location restrictions
- Custom authentication requirements

---

# Licensing Requirements

| Feature | License |
|----------|----------|
| Standard Conditional Access | Microsoft Entra ID P1 |
| Risk-Based Conditional Access | Microsoft Entra ID P2 |
| User Risk Policies | Microsoft Entra ID P2 |
| Sign-in Risk Policies | Microsoft Entra ID P2 |
| Identity Protection | Microsoft Entra ID P2 |

---

# Conditional Access Best Practices

- Enable Security Defaults only if Conditional Access is not used.
- Create at least two emergency (break-glass) accounts.
- Exclude emergency accounts from Conditional Access policies.
- Start new policies in **Report-only** mode.
- Test policies with pilot users before production deployment.
- Block legacy authentication protocols.
- Require MFA for all administrators.
- Require MFA for privileged roles.
- Require compliant devices for corporate resources.
- Require Microsoft Entra Hybrid Joined devices where applicable.
- Require App Protection Policies for mobile access.
- Block sign-ins from countries where business is not conducted.
- Use Named Locations for trusted networks.
- Use Authentication Strength policies for phishing-resistant MFA.
- Enable Continuous Access Evaluation.
- Monitor Conditional Access Insights and Reporting.
- Regularly review policy effectiveness and sign-in logs.
- Follow the principle of least privilege.
- Align policies with a Zero Trust security strategy.

---

# Common Conditional Access Policies

## Identity Protection

- Block high-risk users
- Require password reset for compromised accounts
- Require MFA for medium-risk sign-ins

## Multi-Factor Authentication

- Require MFA for all users
- Require MFA for administrators
- Require MFA for Azure Portal access

## Device Protection

- Require compliant devices
- Require Microsoft Entra Hybrid Joined devices
- Block unmanaged devices

## Application Protection

- Require approved client applications
- Require App Protection Policies
- Restrict browser sessions

## Network Protection

- Block legacy authentication
- Block risky countries
- Allow trusted locations
- Restrict anonymous IP addresses

## Administrative Protection

- Require phishing-resistant MFA
- Protect privileged roles
- Secure Azure management interfaces

---

# Policy Lifecycle

1. Plan the policy
2. Create assignments
3. Configure conditions
4. Configure grant controls
5. Configure session controls
6. Enable **Report-only** mode
7. Review sign-in logs and reports
8. Validate with pilot users
9. Enable the policy
10. Continuously monitor and improve

---

# Deployment Modes

| Mode | Description |
|------|-------------|
| Off | Policy is disabled |
| Report-only | Simulates policy without enforcing it |
| On | Policy is actively enforced |

---

# Monitoring and Troubleshooting

Monitor Conditional Access using:

- Microsoft Entra Sign-in Logs
- Conditional Access Insights and Reporting
- Microsoft Sentinel
- Microsoft Defender XDR
- Microsoft Defender for Cloud Apps
- Identity Protection Reports
- Azure Monitor Workbooks

Useful troubleshooting steps:

- Review sign-in logs
- Check policy evaluation results
- Verify exclusions
- Validate device compliance
- Review authentication requirements
- Confirm licensing

---

# Integration with Microsoft Security

Conditional Access integrates with:

- Microsoft Entra ID
- Microsoft Intune
- Microsoft Defender for Endpoint
- Microsoft Defender for Cloud Apps (MDCA)
- Microsoft Defender XDR
- Microsoft Defender for Cloud
- Microsoft Sentinel
- Microsoft Purview

---

# Zero Trust Principles

Conditional Access supports Microsoft's Zero Trust model by enforcing:

- Verify explicitly
- Use least-privileged access
- Assume breach
- Continuously evaluate risk
- Verify device health
- Verify application security
- Verify user identity

---

# Microsoft Learn

Official documentation:

https://learn.microsoft.com/entra/identity/conditional-access/overview
