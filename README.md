# Active Directory Home Lab

## Overview

I built this home lab to gain hands-on experience with Windows Server, Active Directory, Windows 11 domain environments, and common IT support troubleshooting scenarios.

Using Oracle VirtualBox, I created a Windows Server 2022 domain controller and a Windows 11 client workstation. I configured the `corp.lab` domain, created and managed users and security groups, joined a workstation to the domain, configured DNS and static IP addressing, practiced account troubleshooting, and implemented Group Policy.

The goal of this project was not only to build an Active Directory environment, but also to practice troubleshooting issues that I could encounter in an IT Support or Help Desk role.

---

## Lab Environment

| System | Configuration |
|---|---|
| Hypervisor | Oracle VirtualBox |
| Domain Controller | Windows Server 2022 |
| Client | Windows 11 Enterprise |
| Domain | `corp.lab` |
| Domain Controller | `DC01` |
| Client Workstation | `CLIENT01` |
| DC01 IP Address | `192.168.10.10` |
| CLIENT01 IP Address | `192.168.10.20` |
| DNS Server | `192.168.10.10` |
| Network | `192.168.10.0/24` |

---

## What I Configured

- Installed Windows Server 2022 and configured Active Directory Domain Services (AD DS)
- Created the `corp.lab` Active Directory forest and domain
- Configured `DC01` as the domain controller and DNS server
- Created Organizational Units (OUs) for users, computers, groups, and departments
- Created and managed domain users and security groups
- Configured static IPv4 addressing and DNS
- Installed and configured a Windows 11 Enterprise client
- Joined `CLIENT01` to the `corp.lab` domain
- Verified domain authentication and DNS resolution
- Reset domain user passwords and required password changes at next logon
- Diagnosed and resolved disabled user accounts
- Configured an account lockout policy and troubleshot a locked account
- Used PowerShell to verify and unlock an Active Directory account
- Created and applied a Group Policy Object (GPO) to the Windows 11 workstation

---

## Troubleshooting Experience

During the project, I intentionally created several problems so I could practice diagnosing and resolving them instead of only configuring the environment.

### APIPA / Network Connectivity

CLIENT01 initially received an APIPA (`169.254.x.x`) address because the isolated lab network did not have a DHCP server. I configured the workstation with the appropriate static IPv4 address and configured its DNS server to point to DC01.

I used commands such as:

`ipconfig /all`

`ping 192.168.10.10`

`nslookup corp.lab`

to verify the network configuration, connectivity to the domain controller, and DNS resolution.

### Active Directory Account Troubleshooting

I practiced several common user account support scenarios, including:

- Disabled user accounts
- Password resets
- Forced password changes
- Account lockouts
- Successful domain login verification

For the account lockout scenario, I configured the domain to lock an account after five unsuccessful login attempts. I then reproduced the issue on CLIENT01 and verified the account status using PowerShell.

Commands used included:

`Get-ADUser jsmith -Properties LockedOut`

`Unlock-ADAccount -Identity jsmith`

After unlocking the account, I verified that the user could successfully authenticate again.

---

## Group Policy

I created a custom Group Policy Object named:

`CORP - Workstation Security Policy`

I configured an interactive logon message for domain workstations and forced CLIENT01 to retrieve the updated policy using:

`gpupdate /force`

After restarting CLIENT01, the custom CORP.LAB authorized-access message appeared before login, confirming that the policy had successfully applied.

---

## Skills Practiced

- Active Directory Domain Services
- Windows Server 2022
- Windows 11 Administration
- User and Group Management
- Organizational Units
- Group Policy
- DNS
- IPv4 Addressing
- Domain Joining
- Authentication Troubleshooting
- Account Lockout Troubleshooting
- PowerShell
- Command Prompt
- VirtualBox
- IT Support Troubleshooting
- Technical Documentation

---

## Project Screenshots

Screenshots documenting the complete build and troubleshooting process are included in this repository.

The screenshots cover the project from the initial Windows Server and Active Directory configuration through Windows 11 domain integration, account troubleshooting, Group Policy, and final environment verification.

---

## Key Takeaway

This project gave me hands-on experience building and supporting a Windows domain environment. More importantly, it helped me practice troubleshooting instead of simply following configuration steps.

I worked through networking, DNS, authentication, password, account lockout, and Group Policy scenarios and verified each solution before moving forward.
