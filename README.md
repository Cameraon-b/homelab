# AETHER

*A local-first infrastructure, development, and AI operations platform.*

<img width="1290" height="839" alt="Aether Network Architecture Diagram 6.0" src="https://github.com/Cameraon-b/homelab/blob/main/diagrams/Aether%20Network%20Architecture%20Diagram%206.0.png" />
---

## Overview

AETHER is my self-hosted homelab built to gain hands-on experience in systems administration, infrastructure engineering, networking, virtualization, automation, and AI-assisted operations.

What began as a single Ubuntu server running a few virtual machines has gradually evolved into a local-first platform where I build software, document infrastructure, monitor services, experiment with AI agents, and develop operational workflows.

Rather than simply collecting technologies, AETHER focuses on integrating them into a cohesive engineering environment.

The philosophy is simple:

> **Build. Break. Troubleshoot. Document. Improve. Repeat.**

---

## Goals

- Build production-inspired infrastructure
- Learn by solving real operational problems
- Develop strong documentation habits
- Practice disaster recovery and troubleshooting
- Explore AI-assisted systems administration
- Build a technical portfolio demonstrating real-world engineering practices

---

# Current Architecture

AETHER is organized into several layers:

### Infrastructure

- Ubuntu Server
- Windows Server Active Directory
- Internal DNS
- Docker Engine
- KVM / libvirt virtualization
- Reverse proxy services

### Core Services

- Homepage
- BookStack
- Gitea
- NexusAI
- Uptime Kuma
- Memos
- RustDesk Server

### AI & Automation

- Hermes
- Mira
- Nova
- Local LLM experimentation
- LM Studio
- OpenAI integration
- NexusAI coordination layer

### Development

- Git
- GitHub
- Gitea
- VS Code
- Docker Compose
- Markdown documentation

---

# Infrastructure Overview

AETHER currently consists of three primary physical systems along with several virtual machines and containerized services.

The infrastructure follows a **local-first philosophy**. Core services remain available across the LAN even if internet connectivity is unavailable.

Primary capabilities include:

- Active Directory domain services
- Internal DNS
- Virtualization
- Docker application hosting
- Infrastructure monitoring
- Documentation platform
- Local Git hosting
- AI experimentation
- Disaster recovery

---

# Physical Systems

## Nora — Infrastructure Host

**Purpose**

Primary infrastructure server and always-on host for AETHER.

**Configuration**

- Ubuntu Server
- Headless administration via SSH
- KVM / libvirt virtualization
- Bridged networking
- Docker Engine
- Docker Compose
- Cockpit
- SMART monitoring

**Current Roles**

- Virtualization host
- Active Directory lab host
- Docker platform
- Monitoring node
- Reverse proxy host
- Documentation platform
- Local Git hosting
- Backup platform

---

## Reeba — Engineering Workstation

**Purpose**

Primary engineering workstation used for software development and AI experimentation.

**Current Roles**

- Windows 11 administration
- VS Code development
- Git workflows
- Mira agent node
- Kali Linux dual boot
- Remote infrastructure management
- Linux Active Directory testing

---

## Cass — Operations Workstation

**Purpose**

Secondary engineering workstation focused on AI experimentation and infrastructure management.

**Current Roles**

- Hermes engineering assistant
- LM Studio
- Local LLM experimentation
- Active Directory administration
- Music production
- General development

---

# Virtual Infrastructure

## Windows Active Directory Domain

Domain:

```
aether.lab
```

The Windows domain provides:

- Active Directory Domain Services
- DNS
- Group Policy
- Authentication
- Kerberos
- Delegated Administration

Current virtual machines include:

- WIN-DC01
- WIN-CLIENT01

Additional Linux systems joined to the domain:

- AlmaLinux
- Kali Linux

---

# Container Services

Docker services currently hosted on Nora include:

| Service | Purpose |
|----------|---------|
| Homepage | Central landing page for all AETHER services |
| BookStack | Infrastructure documentation |
| Gitea | Local Git hosting |
| NexusAI | AI coordination platform |
| Uptime Kuma | Infrastructure monitoring |
| Nginx Proxy Manager | Reverse proxy |
| Memos | Internal notes |
| RustDesk Server | Self-hosted remote desktop |

---

# AI Infrastructure

AETHER includes an experimental AI operations layer designed around collaboration rather than autonomous control.

Current agents include:

### Hermes

Engineering assistant responsible for:

- Software development
- Technical analysis
- Infrastructure workflows
- Local and cloud reasoning

### Mira

Documentation assistant responsible for:

- BookStack maintenance
- Documentation generation
- Knowledge management
- Public documentation publishing

### Nova

Architecture review and systems reasoning.

Primary responsibilities include:

- Architecture discussions
- Design validation
- Engineering review
- Long-term planning

These agents coordinate through **NexusAI**, an internal messaging and workflow platform.

The guiding principle is:

> **Agents propose. Humans approve. Systems record what happened.**

---

# Documentation

Documentation exists at two levels.

## Internal Documentation

BookStack serves as AETHER's operational knowledge base.

It contains:

- Infrastructure documentation
- Operations runbooks
- Disaster recovery procedures
- Architecture notes
- Command references
- Engineering logs

## Public Documentation

The `/docs` directory contains sanitized documentation generated from BookStack.

This allows operational documentation to remain complete while sharing engineering practices publicly.

---

# Backup & Disaster Recovery

AETHER includes documented backup and recovery procedures covering:

- Host configuration
- Virtual machines
- Docker applications
- Docker volumes
- Active Directory
- Documentation

Recovery documentation includes:

- Backup Strategy
- Nora Host Recovery
- Virtual Machine Recovery
- Docker Service Recovery
- Active Directory Recovery
- Recovery Validation Checklist

---

# Technologies

## Operating Systems

- Ubuntu Server
- Windows Server
- Windows 11
- Windows 10
- Kali Linux
- AlmaLinux

## Infrastructure

- Docker
- Docker Compose
- KVM
- libvirt
- Active Directory
- DNS
- Group Policy
- Kerberos

## Networking

- TCP/IP
- DNS
- SMB
- Reverse Proxy
- SSH
- Remote Administration

## Documentation

- BookStack
- Markdown
- Operations Runbooks
- Disaster Recovery
- Architecture Documentation

## Development

- Git
- GitHub
- Gitea
- Python
- Bash
- Ruby
- YAML

---

# Repository Structure

```
homelab/
├── docs/
│   ├── infrastructure/
│   ├── services/
│   ├── networking/
│   ├── operations/
│   ├── architecture/
│   └── projects/
│
├── logs/
│
├── images/
│
└── README.md
```

---

# Current Projects

## Completed

- Active Directory deployment
- DNS implementation
- Linux domain integration
- Docker platform deployment
- Homepage deployment
- Local Git hosting with Gitea
- Infrastructure monitoring
- Documentation platform
- Self-hosted RustDesk server
- Backup implementation
- Disaster recovery planning

## In Progress

- AI-assisted operations
- NexusAI development
- Public documentation generation
- Architecture Decision Records (ADRs)
- Local-first AI infrastructure
- Service expansion
- Infrastructure refinement

---

# Design Principles

AETHER follows several guiding principles:

- Local-first whenever practical
- Documentation is part of engineering
- Infrastructure should be recoverable
- Automation should remain observable
- AI agents assist rather than control
- Humans remain the final decision makers

---

# Why This Exists

I learn best by building real systems.

AETHER gives me hands-on experience designing, deploying, operating, troubleshooting, documenting, monitoring, backing up, and recovering production-inspired infrastructure while preparing for roles in:

- IT Support
- Systems Administration
- Infrastructure Engineering
- DevOps

---

# About Me

I'm Cameron Beck, based in Missouri, with a background in operations leadership, process optimization, and technical troubleshooting.

I recently completed my Bachelor of Science in Computer Science and am actively building real-world infrastructure experience through AETHER as I transition into IT and infrastructure-focused roles.
