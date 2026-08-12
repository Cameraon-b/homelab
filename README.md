# AETHER

*An evolving local-first infrastructure, operations, and automation lab.*

<img width="1290" height="839" alt="AETHER Network Architecture Diagram" src="https://github.com/Cameraon-b/homelab/blob/main/diagrams/Aether%20Network%20Architecture%20Diagram%206.0.png" />

---

## Overview

AETHER is my personal homelab and infrastructure environment built to develop hands-on experience in systems administration, IT operations, networking, virtualization, automation, security, and infrastructure engineering.

What began as a single Ubuntu server and a handful of experiments has grown into a small production-inspired environment with centralized identity, virtual machines, containerized services, monitoring, documentation, remote access, asset management, ticketing, backups, internal DNS, and AI-assisted operational workflows.

The goal is not to collect technologies for their own sake.

AETHER is designed as an interconnected environment where systems have defined purposes, dependencies, documentation, monitoring, recovery considerations, and operational history.

The working philosophy is:

> **Build. Break. Troubleshoot. Document. Improve. Repeat.**

---

## Why AETHER Exists

I recently completed a Bachelor of Science in Computer Science and am transitioning from operations leadership into IT and infrastructure-focused work.

My professional interests are centered around:

- IT support and workplace technology
- Systems administration
- Infrastructure engineering
- Networking
- Linux and Windows administration
- Automation
- DevOps and site reliability concepts
- AI-assisted infrastructure operations

My immediate goal is to build a strong foundation in professional IT and systems administration. Long term, I want to grow toward increasingly advanced infrastructure, automation, DevOps/SRE, and AI-assisted systems engineering while maintaining a strong understanding of the systems underneath the automation.

AETHER gives me a place to practice those skills on systems that actually need to remain usable.

---

# Design Principles

AETHER follows several principles:

- **Architecture before implementation**
- **Local-first whenever practical**
- **Documentation is part of engineering**
- **Every service should have a defined purpose**
- **Infrastructure should be observable**
- **Infrastructure should be recoverable**
- **Changes should leave an operational record**
- **Automation should remain understandable and auditable**
- **AI agents should operate through defined identities and permissions**
- **AI agents assist rather than silently control systems**
- **Humans remain the final authority**

---

# Architecture

AETHER has evolved into several interconnected layers.

## Identity & Access

- Windows Server Active Directory
- Internal DNS
- Group Policy
- Kerberos authentication
- Delegated administration
- Windows domain clients
- Linux domain integration

## Compute & Virtualization

- Ubuntu Server
- Windows workstations
- KVM / libvirt
- Windows Server virtual machines
- Kali Linux virtual machine
- Docker Engine
- Docker Compose

## Networking & Remote Access

- Internal DNS namespace
- Ethernet switching
- Bridged virtual networking
- Nginx Proxy Manager
- WireGuard VPN
- FreedomBox
- SSH
- RustDesk

## Operations

- GLPI
- BookStack
- Uptime Kuma
- Homepage
- Memos
- AETHER operational logs
- Backup and recovery workflows

## Development & Automation

- Git
- GitHub
- Gitea
- VS Code
- Python
- Bash
- Docker Compose
- Local LLMs
- OpenAI integration
- AI-assisted engineering workflows
- Nexus development

---

# Physical Systems

## Nora — Infrastructure Host

**Role:** Primary AETHER server and always-on infrastructure host.

Nora is the operational core of the environment.

### Current Responsibilities

- Ubuntu Server
- Docker hosting
- KVM / libvirt virtualization
- Active Directory VM hosting
- BookStack
- GLPI
- Uptime Kuma
- Nginx Proxy Manager
- Homepage
- Gitea
- Memos
- RustDesk infrastructure
- Nexus development and services
- Backup operations
- SSH administration

Nora is intentionally treated as infrastructure rather than as a general-purpose workstation.

---

## Reeba — Engineering & AI Workstation

**Role:** Primary engineering workstation and host for Mira/OpenClaw.

### Current Responsibilities

- Windows 11
- VS Code
- Git workflows
- Infrastructure administration
- Remote AETHER administration
- OpenClaw
- Mira
- Local LLM experimentation
- Development work
- Dedicated Minecraft server

Reeba also hosts selected workloads that do not belong on Nora's core infrastructure platform.

---

## Cass — AI & Development Workstation

**Role:** Secondary workstation and home of Hermes.

### Current Responsibilities

- Windows 10
- Hermes
- LM Studio
- Local LLM experimentation
- Infrastructure administration
- Development
- Music production

Cass provides a second AI-capable workstation within AETHER and serves as Hermes' primary host.

---

## Iris — VPN Gateway

**Role:** Secure remote access gateway into AETHER.

Iris is a Raspberry Pi running FreedomBox and WireGuard.

It provides encrypted remote access to the private AETHER network without requiring individual internal services to be exposed directly to the public internet.

---

## Atlas — Ethernet Switch

**Role:** Physical switching layer for the wired AETHER network.

Atlas connects AETHER's primary systems and provides the physical foundation for the increasingly Ethernet-based environment.

---

# Virtual Infrastructure

## Active Directory

AETHER operates the internal domain:

```text
aether.lab
```

The domain provides:

- Active Directory Domain Services
- DNS
- Group Policy
- Authentication
- Kerberos
- Organizational Units
- Security groups
- Delegated administration
- Windows and Linux identity integration

### Current Virtual Machines

- **WIN-DC01** — Domain controller and DNS server
- **WIN-CLIENT01** — Domain-joined Windows client
- **Pan** — Kali Linux security, networking, and administration VM

Pan also serves as a Linux domain-integration environment and a platform for security and networking exploration.

---

# Services

AETHER operates a growing collection of internal services.

| Service | Purpose |
|---|---|
| **BookStack** | Operational documentation and institutional knowledge |
| **GLPI** | Ticketing, asset management, and IT operations |
| **Uptime Kuma** | Infrastructure and service monitoring |
| **Homepage** | Internal service portal |
| **Nginx Proxy Manager** | Reverse proxy and internal service routing |
| **Gitea** | Local Git hosting |
| **Memos** | Lightweight notes and operational capture |
| **RustDesk** | Self-hosted remote administration |
| **Nexus** | Developing coordination and audit layer |
| **Minecraft Server** | Persistent family application hosted on Reeba |

Services are increasingly treated as managed infrastructure rather than isolated applications.

For each service, AETHER increasingly considers:

- Purpose
- Hosting
- Dependencies
- DNS and networking
- Authentication
- Monitoring
- Backups
- Recovery
- Documentation
- Troubleshooting
- Change history

---

# IT Operations

One of the biggest changes in AETHER has been the transition from simply **building systems** to **operating systems**.

## GLPI

GLPI serves as AETHER's IT service management and asset platform.

It is being developed as the operational record for:

- Physical computers
- Virtual machines
- Displays and peripherals
- Network equipment
- Infrastructure assets
- Incidents
- Technical issues
- Planned work
- Documentation tasks
- Projects and goals

The intent is for GLPI to increasingly answer:

> **What exists, what is happening, and what needs attention?**

---

## BookStack

BookStack serves as AETHER's primary knowledge base and institutional memory.

It contains:

- Architecture documentation
- System inventories
- Service documentation
- Operational runbooks
- Networking documentation
- Active Directory documentation
- Troubleshooting records
- Backup and recovery procedures
- Learning and reference material
- Historical AETHER records

As AETHER grew, BookStack itself became an information-management project. Documentation that had accumulated organically is being restructured around clearer distinctions between current inventory, architecture, services, operations, learning material, and historical records.

---

## Uptime Kuma

Uptime Kuma provides visibility into the availability of AETHER services.

Monitoring is treated as part of operating infrastructure rather than something added only after a service fails.

---

## Operational Logs

AETHER maintains chronological engineering logs documenting the environment as it changes.

The logs record:

- Deployments
- Configuration changes
- Failures
- Troubleshooting
- Migrations
- Architectural decisions
- Experiments
- Lessons learned

They intentionally preserve historical context rather than being rewritten whenever the current architecture changes.

---

# Documentation Model

AETHER documentation exists at two levels.

## Internal Operational Documentation

BookStack contains the full internal knowledge base.

It is intended to answer questions such as:

- What systems exist?
- What does each system do?
- How are systems connected?
- How is a service administered?
- What does it depend on?
- How was it configured?
- What has gone wrong before?
- How can it be recovered?
- Why was an architectural decision made?

## Public Documentation

Selected BookStack documentation is being converted into sanitized Markdown for this repository.

The goal is not to publish the internal wiki verbatim.

Instead, the public documentation provides a view into the engineering and operational side of AETHER while excluding credentials, sensitive configuration, and unnecessary internal details.

The public documentation and engineering logs serve complementary purposes:

> **Logs show the journey. Documentation shows the resulting system.**

---

# Backup & Disaster Recovery

AETHER includes backup and recovery planning for critical infrastructure.

Current work includes protection of:

- Host configuration
- Docker application data
- Databases
- Virtual machines
- Active Directory
- BookStack documentation
- Application data
- Minecraft world data

Backups are increasingly treated as incomplete until there is also an understood restoration process.

For significant changes, AETHER uses application-specific rollback points where appropriate. These can include:

- Database dumps
- Application-data archives
- Configuration capture
- Container image identification
- Checksums
- Recovery documentation

The objective is not simply to possess backups, but to understand how systems could actually be restored.

---

# Networking

Networking work within AETHER includes:

- TCP/IP
- Internal DNS
- Ethernet switching
- Bridged VM networking
- Reverse proxying
- SSH
- SMB
- WireGuard
- Remote administration
- Client/server architecture
- Internal service naming

AETHER uses the internal namespace:

```text
aether.lab
```

The long-term goal is for systems and services to have clear identities rather than requiring administration through memorized IP addresses and ports.

---

# AI & Automation

AETHER also serves as a laboratory for exploring how AI systems can participate safely and usefully in a technical environment.

Both Cass and Reeba support local LLM experimentation, while individual agents have distinct responsibilities and identities within AETHER.

The emphasis is not unrestricted autonomous infrastructure control.

The focus is on:

- Knowledge management
- Technical research
- Documentation
- Analysis
- Planning
- Software development
- Troubleshooting
- Operational support
- Human-reviewed automation

---

## Hermes — Engineering Assistant

**Primary host:** Cass

Hermes serves as an engineering and development assistant within AETHER.

His responsibilities include:

- Technical analysis
- Software development assistance
- Design work
- Architecture support
- Infrastructure workflow assistance
- Troubleshooting
- Technical writing
- Helping translate ideas into structured implementation plans

Hermes is primarily used as a technical collaborator rather than an autonomous infrastructure operator.

---

## Mira — Keeper of the Thread

**Primary host:** Reeba  
**Runtime:** OpenClaw

Mira serves as AETHER's knowledge steward.

Her responsibilities include:

- Reading and maintaining BookStack
- Reconciling documentation
- Reviewing Git repositories
- Maintaining knowledge of current AETHER architecture
- Identifying missing or conflicting documentation
- Preparing documentation updates
- Supporting troubleshooting through existing operational knowledge
- Maintaining continuity between AETHER's current state and historical development

Mira operates through her own service identities rather than borrowing administrator accounts.

Her role is to preserve the thread connecting:

> **What AETHER was → what changed → why it changed → what AETHER is now.**

---

# Nexus

Nexus is an ongoing AETHER development project exploring coordination between humans, AI agents, infrastructure systems, and operational records.

The long-term objective is not to create an AI superuser with unrestricted control over the environment.

Instead, Nexus is intended to become a coordination and audit layer where agent capabilities can be deliberately exposed, controlled, and recorded.

The underlying model is:

> **Agents propose. Humans approve. Systems record what happened.**

Areas of exploration include:

- Agent identity
- Permissions
- Human approval boundaries
- Tool access
- Knowledge retrieval
- Operational context
- Audit trails
- Multi-agent coordination

Nexus remains an evolving project rather than a finished platform.

---

# Technologies

## Operating Systems

- Ubuntu Server
- Windows Server
- Windows 11
- Windows 10
- Kali Linux

## Infrastructure

- Docker
- Docker Compose
- KVM
- libvirt
- Active Directory
- DNS
- Group Policy
- Kerberos
- WireGuard
- FreedomBox

## Networking & Administration

- TCP/IP
- DNS
- SMB
- SSH
- Reverse proxies
- Bridged networking
- Remote administration
- Ethernet switching

## Operations

- GLPI
- BookStack
- Uptime Kuma
- Homepage
- Nginx Proxy Manager
- RustDesk
- Cockpit

## Development

- Git
- GitHub
- Gitea
- VS Code
- Python
- Bash
- Ruby
- JavaScript
- SQL
- YAML

## AI & Automation

- OpenAI
- OpenClaw
- LM Studio
- Local LLMs
- AI-assisted development
- Agent workflows
- Nexus

---

# Repository Structure

The repository evolves alongside the lab.

```text
homelab/
├── bookstack/
│   ├── architecture/
│   ├── inventory/
│   ├── services/
│   ├── operations/
│   ├── networking/
│   ├── projects/
│   └── reference/
│
├── diagrams/
│
├── logs/
│
└── README.md
```

### `bookstack/`

Sanitized public versions of selected operational documentation from AETHER's internal BookStack knowledge base.

### `diagrams/`

Architecture and network diagrams showing how AETHER has evolved.

### `logs/`

The chronological engineering history of AETHER, including deployments, failures, migrations, troubleshooting, architectural decisions, and lessons learned.

---

# Current Focus

AETHER is transitioning from rapid infrastructure expansion toward greater **operational maturity**.

Current priorities include:

1. Expanding and maintaining the GLPI asset inventory.
2. Using GLPI to manage incidents, technical work, and infrastructure goals.
3. Restructuring and improving BookStack documentation.
4. Publishing a sanitized version of operational documentation to GitHub.
5. Improving backup and recovery procedures.
6. Continuing networking, Linux, Windows, and infrastructure administration practice.
7. Developing Nexus as a coordination and audit layer.
8. Introducing automation where it genuinely improves operations.
9. Improving security and access-control practices.
10. Building projects that translate directly into professional IT and systems administration skills.

---

# What I Am Learning

AETHER has increasingly taught me that infrastructure engineering is not primarily about installing software.

Installing a service is often the easy part.

The harder problems are:

- Understanding dependencies
- Maintaining consistent configuration
- Troubleshooting across system boundaries
- Managing identities and permissions
- Documenting decisions
- Protecting data
- Monitoring systems
- Planning changes
- Tracking assets
- Managing operational work
- Recovering from failure
- Keeping an environment understandable as it grows

The lab is intentionally becoming more operational and less focused on isolated experimentation over time.

---

# Career Direction

My immediate goal is to establish myself professionally in IT and infrastructure.

I am particularly interested in roles involving:

- Internal IT
- IT support
- Systems administration
- Workplace technology
- Infrastructure support
- Networking
- Server administration
- Data center and hands-on infrastructure work

From there, I want to continue developing deeper infrastructure skills and eventually grow toward senior systems administration, infrastructure engineering, DevOps/SRE, and infrastructure automation.

My computer science background gives me a foundation in software development and programming that I intend to continue developing alongside my infrastructure career.

I am particularly interested in the intersection between the two:

> **Understanding systems deeply enough to operate them manually, then using software and automation to operate them better.**

AETHER is where I practice doing that.

---

# About Me

I'm Cameron Beck, based in Missouri.

I hold a Bachelor of Science in Computer Science and have a professional background in operations leadership, process improvement, technical troubleshooting, documentation, training, and team support.

I am currently transitioning into IT and infrastructure-focused work while using AETHER to develop practical experience beyond the classroom.

This repository documents that transition in real time.

**AETHER is not a finished project. It is the environment I use to keep learning.**
