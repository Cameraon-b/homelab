# Cameron's Homelab

A hands-on infrastructure, systems administration, and automation lab built to develop real-world experience in:

- systems administration
- virtualization
- networking
- identity and access management
- automation
- troubleshooting
- infrastructure operations

This project is part of my transition from operations leadership into IT, infrastructure, and eventually DevOps.

The goal is simple:

**Build. Break. Troubleshoot. Document. Improve. Repeat.**

---

# Current Infrastructure

## Physical Systems

### Nora — Infrastructure Host

Purpose:

Primary infrastructure server.

Configuration:

- Ubuntu Server
- Headless administration via SSH
- KVM / libvirt virtualization host
- Bridged networking
- Cockpit web management
- SMART disk monitoring

---

### Reeba — Engineering Workstation

Purpose:

Primary engineering and experimentation workstation.

Current Roles:

- Windows administration
- virtualization
- AI experimentation
- ORICA management
- remote infrastructure management

---

### Cass — Remote Administration & Creative Workstation

Purpose:

Secondary administration workstation and production desktop.

Current Roles:

- Windows 10
- remote administration
- SSH / Termius access
- Active Directory testing
- documentation
- music production
- development

---

### Windows / Kali Workstation

Purpose:

Security testing and future offensive/defensive experimentation.

Current Roles:

- dual boot
- penetration testing
- networking experimentation

---

### Raspberry Pi Systems *(planned expansion)*

Future Roles:

- Pi-hole
- DNS services
- network monitoring
- automation
- IoT experimentation

---

# Virtual Infrastructure

## AETHER — Core Infrastructure Domain

Production-like Windows domain environment.

### Domain Information

Domain:

`aether.lab`

NetBIOS:

`AETHER`

---

### Virtual Machines

#### WIN-DC01 — Domain Controller

Roles:

- Active Directory Domain Services
- DNS
- Group Policy
- Authentication
- Kerberos

Configured:

- users
- security groups
- organizational units
- delegated administration
- password policies
- account lockout policies

---

#### WIN-CLIENT01 — Domain Client

Roles:

- domain authentication
- endpoint policy validation
- remote administration workstation

Configured:

- domain joined
- Group Policy validation
- mapped network drives
- RSAT administration tools

---

### Current Active Directory Structure

Organizational Units:

- Admins
- Users
- Resources
- Policies

Administrative Accounts:

- `labadmin`
- `helpdesk01` *(Tier 1)*
- `helpdesk02` *(Tier 2)*

Security Groups:

- `GG_Aether_Helpdesk_T1`
- `GG_Aether_Helpdesk_T2`
- `GG_AetherShare_RW`
- `GG_AetherShare_RO`
- `GG_AetherShare_Deny`

Delegation Implemented:

Tier 1:

- password resets
- forced password changes

Tier 2:

- create users
- edit users
- delete users
- password management

---

## ORICA — AI Sandbox

Separate experimental environment.

Purpose:

AI-assisted automation, scripting, and agent experimentation.

Host:

Reeba

VM:

`ORICA-AI1`

OS:

Ubuntu

Configured:

- OpenClaw
- OpenAI backend integration
- file automation
- scripting experiments
- Ruby experimentation

---

# Technologies

## Operating Systems

- Ubuntu Server
- Windows Server
- Windows 10 Enterprise
- Windows 11
- Kali Linux

---

## Virtualization

- KVM
- libvirt
- qcow2 snapshots
- bridged networking

---

## Identity & Access Management

- Active Directory
- Group Policy
- Kerberos
- role-based access control
- delegated administration

---

## Linux Administration

- SSH
- systemd
- journalctl
- smartmontools
- Cockpit

---

## Networking

- TCP/IP
- DNS
- SMB shares
- bridged virtualization networking
- remote administration

---

## Automation / Development

- Git
- GitHub
- Markdown
- OpenClaw
- Ruby
- Bash

---

# Current Projects

## Active Directory Infrastructure

Completed:

- domain controller deployment
- domain client integration
- organizational unit design
- delegated administration
- Group Policy enforcement
- password and lockout policies
- mapped network shares

In Progress:

- workstation administration
- computer object delegation
- PowerShell remoting
- Remote Desktop policies

---

## Host Operations

Completed:

- Cockpit deployment
- storage monitoring
- SMART diagnostics
- live infrastructure logging

In Progress:

- preventative SATA maintenance
- hardware reliability validation

---

## Security Lab *(planned)*

Future goals:

- join Kali systems to domain
- SMB enumeration
- LDAP testing
- Kerberos analysis
- blue-team / red-team workflows

---

## Personal Hosting *(planned)*

Future goals:

- self-hosted website
- portfolio
- photography
- music
- development projects

---

# Journal

Detailed engineering logs, troubleshooting notes, architecture decisions, and infrastructure changes are documented in:

`/logs`

Topics include:

- server deployment
- virtualization
- networking
- Active Directory
- delegation
- Group Policy
- monitoring
- AI experimentation
- infrastructure troubleshooting

---

# Why This Exists

I learn best by building real systems.

This homelab gives me hands-on experience operating, troubleshooting, and documenting production-like infrastructure while preparing for roles in:

- IT Support
- Systems Administration
- Infrastructure Engineering
- DevOps

---

# About Me

I'm Cameron Beck, based in Missouri, with a background in operations leadership, process optimization, and technical troubleshooting.

I recently completed my Bachelor of Science in Computer Science and am actively building real-world infrastructure experience through this lab.

GitHub:

:contentReference[oaicite:4]{index=4}
