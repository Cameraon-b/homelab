# Cameron's Homelab

A hands-on infrastructure, systems administration, containerization, monitoring, and automation lab built to develop real-world experience in:

- systems administration
- virtualization
- networking
- identity and access management
- containerization
- monitoring / observability
- automation
- troubleshooting
- infrastructure operations

This project serves as both a **learning environment** and an **engineering portfolio** 

The goal is simple:

**Build. Break. Troubleshoot. Document. Improve. Repeat.**

---

# Current Infrastructure

## Physical Systems

### Nora — Infrastructure Host

Purpose:

Primary infrastructure server and AETHER core host.

Configuration:

- Ubuntu Server
- headless administration via SSH
- KVM / libvirt virtualization host
- bridged networking
- Cockpit web management
- Docker Engine
- Docker Compose
- Uptime Kuma monitoring
- SMART disk monitoring

Current Roles:

- virtualization host
- Active Directory lab host
- container platform
- monitoring node
- infrastructure management

---

### Reeba — Engineering Workstation

Purpose:

Primary engineering and experimentation workstation.

Current Roles:

- Windows 11 administration
- AI experimentation
- OpenClaw / Mira agent node
- remote infrastructure management
- Kali Linux dual boot
- networking experimentation

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
- AlmaLinux VM host
- music production
- development

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

### Virtual Machines on Nora

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

### Additional Domain Systems

#### AlmaLinux *(VM on Cass)*

Roles:

- Linux domain authentication
- cross-platform AD testing
- SSH administration

Configured:

- joined to AETHER domain
- AD login validation

---

#### Kali Linux *(Dual Boot on Reeba)*

Roles:

- Linux domain authentication
- security testing
- networking experimentation

Configured:

- joined to AETHER domain
- winbind / AD authentication

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

Separate experimental environment for AI-assisted tooling and automation.

### ORICA-AI1

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

## Mira — Local AI Agent Node

Purpose:

Native AI/agent experimentation environment.

Host:

Reeba

OS:

Windows 11

Configured:

- OpenClaw
- local dashboard
- gateway services
- workspace automation
- file-based task execution
- AI-assisted experimentation

---

# Container Infrastructure

## Docker Platform (Nora)

Docker is now deployed on Nora as a lightweight application platform alongside virtualization.

Configured:

- Docker Engine
- Docker Compose
- persistent Docker volumes
- custom Docker bridge networks
- container lifecycle testing
- self-hosted services

Current Services:

### Nginx Test Service

Purpose:

Basic web service deployment and container lifecycle testing.

Features:

- persistent web content via Docker volume
- Compose-managed deployment
- LAN access testing

---

### Uptime Kuma

Purpose:

Infrastructure monitoring and observability.

Features:

- LAN host monitoring
- HTTP service monitoring
- DNS health checks
- SSH / TCP port monitoring
- SSL/TLS validation handling
- infrastructure visibility dashboard

Monitored Systems:

- Nora
- WIN-DC01
- WIN-CLIENT01
- Cass
- Reeba
- AlmaLinux
- Kali Linux
- external connectivity
- internal services

---

# Technologies

## Operating Systems

- Ubuntu Server
- Ubuntu Desktop
- Windows Server
- Windows 10
- Windows 11
- Kali Linux
- AlmaLinux

---

## Virtualization

- KVM
- libvirt
- qcow2 snapshots
- bridged networking

---

## Containerization

- Docker Engine
- Docker Compose
- persistent volumes
- custom bridge networks
- image/container lifecycle
- self-hosted service deployment

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

## Monitoring / Observability

- Uptime Kuma
- host monitoring
- service health checks
- DNS monitoring
- HTTP monitoring
- SSL/TLS troubleshooting
- infrastructure visibility

---

## Networking

- TCP/IP
- DNS
- SMB shares
- bridged virtualization networking
- Docker networking
- remote administration

---

## Automation / Development

- Git
- GitHub
- Markdown
- OpenClaw
- Ruby
- Bash
- YAML

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

## Container Infrastructure

Completed:

- Docker installation on Nora
- container lifecycle testing
- persistent Docker volumes
- custom Docker bridge networks
- Docker Compose deployments
- self-hosted nginx
- Uptime Kuma deployment
- LAN infrastructure monitoring

In Progress:

- reverse proxy research
- internal DNS naming
- containerized application hosting
- future self-hosted services

---

## Host Operations

Completed:

- Cockpit deployment
- storage monitoring
- SMART diagnostics
- live infrastructure logging
- VM memory optimization

In Progress:

- preventative SATA maintenance
- hardware reliability validation

---

## Security Lab *(planned)*

Future goals:

- SMB enumeration
- LDAP testing
- Kerberos analysis
- blue-team / red-team workflows
- internal vulnerability testing

---

## Personal Hosting *(planned)*

Future goals:

- self-hosted website
- portfolio hosting
- photography
- music
- development projects
- reverse proxy services

---

# Journal

Detailed engineering logs, troubleshooting notes, architecture decisions, and infrastructure changes are documented in:

`/logs`

Topics include:

- server deployment
- virtualization
- Docker
- monitoring
- networking
- Active Directory
- delegation
- Group Policy
- AI experimentation
- infrastructure troubleshooting

---

# Why This Exists

I learn best by building real systems.

This homelab gives me hands-on experience operating, troubleshooting, monitoring, and documenting production-like infrastructure while preparing for roles in:

- IT Support
- Systems Administration
- Infrastructure Engineering
- DevOps

---

# About Me

I'm Cameron Beck, based in Missouri, with a background in operations leadership, process optimization, and technical troubleshooting.

I recently completed my Bachelor of Science in Computer Science and am actively building real-world infrastructure experience through this lab as I transition into IT and infrastructure-focused roles.
