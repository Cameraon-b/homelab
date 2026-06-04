# Cameron's Homelab (AETHER)

A hands-on infrastructure, systems administration, containerization, monitoring, documentation, and automation lab built to develop real-world experience in:

* Systems Administration
* Virtualization
* Networking
* Identity & Access Management
* Containerization
* Monitoring / Observability
* Documentation
* Disaster Recovery
* Automation
* Troubleshooting
* Infrastructure Operations

This project serves as both a **learning environment** and an **engineering portfolio**.

The goal is simple:

**Build. Break. Troubleshoot. Document. Improve. Repeat.**

---

# Current Infrastructure

## Physical Systems

### Nora — Infrastructure Host

Purpose:

Primary infrastructure server and AETHER core host.

Configuration:

* Ubuntu Server
* Headless administration via SSH
* KVM / libvirt virtualization host
* Bridged networking
* Cockpit web management
* Docker Engine
* Docker Compose
* Uptime Kuma monitoring
* SMART disk monitoring

Current Roles:

* Virtualization host
* Active Directory lab host
* Container platform
* Monitoring node
* Documentation platform
* Reverse proxy host
* Backup and recovery platform

IP Address:

```text
192.168.1.137
```

---

### Reeba — Engineering Workstation

Purpose:

Primary engineering and experimentation workstation.

Current Roles:

* Windows 11 administration
* AI experimentation
* OpenClaw / Mira agent node
* Remote infrastructure management
* Kali Linux dual boot
* Networking experimentation
* Active Directory Linux integration

IP Address:

```text
192.168.1.155
```

---

### Cass — Remote Administration & Creative Workstation

Purpose:

Secondary administration workstation and production desktop.

Current Roles:

* Windows 10
* Remote administration
* SSH / Termius access
* Active Directory testing
* Documentation
* AlmaLinux VM host
* Music production
* Development
* Central AETHER management workstation

IP Address:

```text
192.168.1.134
```

---

### Raspberry Pi Systems *(Planned Expansion)*

Future Roles:

* Pi-hole
* DNS services
* Network monitoring
* Automation
* IoT experimentation

---

# Virtual Infrastructure

## AETHER — Core Infrastructure Domain

Production-like Windows domain environment.

### Domain Information

Domain:

```text
aether.lab
```

NetBIOS:

```text
AETHER
```

---

## Virtual Machines on Nora

### WIN-DC01 — Domain Controller

Roles:

* Active Directory Domain Services
* DNS
* Group Policy
* Authentication
* Kerberos

Configured:

* Users
* Security Groups
* Organizational Units
* Delegated Administration
* Password Policies
* Account Lockout Policies

IP Address:

```text
192.168.1.15
```

---

### WIN-CLIENT01 — Domain Client

Roles:

* Domain Authentication
* Endpoint Policy Validation
* Remote Administration Workstation

Configured:

* Domain Joined
* Group Policy Validation
* RSAT Administration Tools

IP Address:

```text
192.168.1.75
```

---

## Additional Domain Systems

### AlmaLinux *(VM on Cass)*

Roles:

* Linux domain authentication
* Cross-platform AD testing
* SSH administration

Configured:

* Joined to AETHER domain
* realmd
* SSSD
* AD login validation

---

### Kali Linux *(Dual Boot on Reeba)*

Roles:

* Linux domain authentication
* Security testing
* Networking experimentation

Configured:

* Joined to AETHER domain
* Winbind
* AD authentication
* SMB share access

---

# Active Directory

## Organizational Units

* Admins
* Users
* Resources
* Policies

---

## Administrative Accounts

* labadmin
* helpdesk01 (Tier 1)
* helpdesk02 (Tier 2)

---

## Security Groups

Administrative Groups:

* GG_IT_Admins
* DnsAdmins

Helpdesk Groups:

* GG_Helpdesk_Tier1
* GG_Helpdesk_Tier2
* GG_Aether_DesktopSupport

Resource Access Groups:

* GG_AetherShare_RW
* GG_AetherShare_RO
* GG_AetherShare_Deny

Remote Access Groups:

* GG_Aether_RDP_Workstations

---

## Delegation Implemented

### Tier 1

* Password resets
* Forced password changes

### Tier 2

* Create users
* Edit users
* Delete users
* Password management

---

## Group Policies

* Aether_Workstation_RDP
* AETHER Wallpaper Policy
* Aether User Restrictions
* Default Domain Policy
* Default Domain Controllers Policy

---

# DNS Infrastructure

Hosted on:

```text
WIN-DC01
```

Current Records:

* wiki.aether.lab
* kuma.aether.lab
* test.aether.lab
* memos.aether.lab

DNS is used for:

* Internal service discovery
* Reverse proxy routing
* Infrastructure monitoring
* Domain services

---

# Container Infrastructure

## Docker Platform (Nora)

Docker is deployed on Nora as a lightweight application platform alongside virtualization.

Configured:

* Docker Engine
* Docker Compose
* Persistent Docker volumes
* Custom Docker bridge networks
* Container lifecycle testing
* Self-hosted services

---

### BookStack

Purpose:

Centralized documentation and institutional memory platform.

Features:

* Infrastructure documentation
* Domain Services documentation
* Operations Runbooks
* Disaster Recovery documentation
* Command References
* Architecture documentation

URL:

```text
wiki.aether.lab
```

---

### Uptime Kuma

Purpose:

Infrastructure monitoring and observability.

Features:

* LAN host monitoring
* HTTP service monitoring
* DNS health checks
* TCP monitoring
* Infrastructure visibility dashboard

Monitored Systems:

* Nora
* WIN-DC01
* WIN-CLIENT01
* Cass
* Reeba
* AlmaLinux
* Kali Linux

URL:

```text
kuma.aether.lab
```

---

### Nginx Proxy Manager

Purpose:

Reverse proxy and service routing.

Features:

* DNS-based service access
* Internal application publishing
* Centralized service routing

Configured Services:

* wiki.aether.lab
* kuma.aether.lab
* memos.aether.lab

---

### Memos

Purpose:

Lightweight internal collaboration and note-sharing platform.

Features:

* Multi-user access
* Persistent storage
* LAN accessibility

Milestone:

First AETHER-hosted application actively used by another user.

URL:

```text
memos.aether.lab
```

---

### Aether Compose Lab

Purpose:

Docker networking, volume, and container experimentation environment.

---

# Documentation Platform

Documentation is maintained through BookStack.

Current Documentation Areas:

* Infrastructure
* Applications
* Domain Services
* Operations Runbooks
* Disaster Recovery
* Command References
* Architecture

BookStack serves as AETHER's institutional memory and primary operational knowledge base.

---

# Backup & Disaster Recovery

AETHER includes a documented backup and recovery strategy.

Protected Assets:

* Host Configuration
* Virtual Machines
* Docker Applications
* Docker Volumes
* Active Directory Infrastructure
* Documentation

Backup Structure:

```text
AETHER/
├── host
├── docker
├── docker-volumes
├── exports
├── full-backups
└── configs
```

Recovery Assets:

* WIN-DC01.xml
* WIN-CLIENT01.xml
* Virtual Machine Backups
* Docker Volume Backups
* Host Configuration Backups

Disaster Recovery Documentation Includes:

* Backup Strategy
* Nora Host Recovery
* Virtual Machine Recovery
* Docker Service Recovery
* Active Directory Recovery
* Recovery Validation Checklist

---

# AI Infrastructure

## ORICA — AI Sandbox

Separate experimental environment for AI-assisted tooling and automation.

### ORICA-AI1

Host:

Reeba

Configured:

* OpenClaw
* OpenAI backend integration
* File automation
* Scripting experiments
* Ruby experimentation

---

## Mira — Local AI Agent Node

Purpose:

Native AI and agent experimentation environment.

Configured:

* OpenClaw
* Local dashboard
* Gateway services
* Workspace automation
* File-based task execution
* Documentation-aware assistance

Current Areas of Exploration:

* Infrastructure analysis
* Knowledge management
* Administrative workflows
* Environment awareness
* Operational recommendations

BookStack serves as Mira's primary knowledge source.

---

# Technologies

## Operating Systems

* Ubuntu Server
* Ubuntu Desktop
* Windows Server
* Windows 10
* Windows 11
* Kali Linux
* AlmaLinux

---

## Virtualization

* KVM
* libvirt
* qcow2
* Bridged networking

---

## Containerization

* Docker Engine
* Docker Compose
* Persistent volumes
* Custom bridge networks
* Self-hosted service deployment

---

## Identity & Access Management

* Active Directory
* Group Policy
* Kerberos
* Role-Based Access Control
* Delegated Administration

---

## Linux Administration

* SSH
* systemd
* journalctl
* smartmontools
* Cockpit

---

## Monitoring & Observability

* Uptime Kuma
* Host monitoring
* Service health checks
* DNS monitoring
* HTTP monitoring
* Infrastructure visibility

---

## Networking

* TCP/IP
* DNS
* SMB Shares
* Bridged virtualization networking
* Docker networking
* Reverse proxy services
* Remote administration

---

## Documentation

* BookStack
* Operations Runbooks
* Disaster Recovery Procedures
* Architecture Documentation
* Command References

---

## Automation & Development

* Git
* GitHub
* Markdown
* OpenClaw
* Ruby
* Bash
* YAML

---

# Current Projects

## Infrastructure Operations

Completed:

* Active Directory deployment
* DNS implementation
* Linux domain integration
* Docker platform deployment
* Monitoring deployment
* Documentation platform deployment
* Backup implementation
* Disaster Recovery planning

In Progress:

* Automation
* Service expansion
* Infrastructure refinement
* AI-assisted operations

---

## Commons Website *(Planned)*

Future goals:

* Self-hosted website
* Technical portfolio
* Photography
* Music
* Development projects

---

## Security Lab *(Planned)*

Future goals:

* SMB enumeration
* LDAP testing
* Kerberos analysis
* Blue-team workflows
* Vulnerability assessment

---

# Journal

Detailed engineering logs, troubleshooting notes, architecture decisions, and infrastructure changes are documented in:

```text
/logs
```

Topics include:

* Server deployment
* Virtualization
* Docker
* Monitoring
* Networking
* Active Directory
* DNS
* Group Policy
* Backup & Recovery
* AI experimentation
* Infrastructure troubleshooting

---

# Key Accomplishments

* Built and administered a Windows Active Directory domain
* Implemented DNS and Group Policy management
* Joined Windows and Linux systems to Active Directory
* Created delegated administrative roles and security groups
* Deployed containerized services using Docker Compose
* Implemented centralized monitoring with Uptime Kuma
* Built a documentation platform using BookStack
* Integrated AI-assisted operations through Mira/OpenClaw
* Implemented backup and disaster recovery procedures
* Created architecture diagrams and operational documentation
* Maintained a detailed engineering log documenting infrastructure growth

---

# Why This Exists

I learn best by building real systems.

This homelab gives me hands-on experience operating, troubleshooting, monitoring, documenting, backing up, and recovering production-like infrastructure while preparing for roles in:

* IT Support
* Systems Administration
* Infrastructure Engineering
* DevOps

---

# About Me

I'm Cameron Beck, based in Missouri, with a background in operations leadership, process optimization, and technical troubleshooting.

I recently completed my Bachelor of Science in Computer Science and am actively building real-world infrastructure experience through this lab as I transition into IT and infrastructure-focused roles.
