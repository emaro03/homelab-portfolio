# Emanuel Almonte — Homelab Portfolio

Electrical Engineer · IT Infrastructure & Cybersecurity
Santo Domingo, Dominican Republic · [LinkedIn](https://www.linkedin.com/in/emaro03) · emaro03@gmail.com

> This portfolio is not a list of things I installed. Each project below
> is hands-on work in identity, patching, secure access, and security
> operations — and each one ends with what that work means for an employer.

## What I bring to a team

- **5+ years in security and infrastructure.** Regional Security
  Technician at the U.S. Embassy in Santo Domingo since June 2022,
  maintaining and deploying physical security systems (access control,
  CCTV, explosives detection, X-ray) and supporting 8 U.S. diplomatic
  missions in the Caribbean. Before that, Automation Engineer (Lead)
  at Domotics (2019–2021), building network and structured-cabling
  infrastructure for smart-building projects.
- **Hands-on identity work, not just theory.** My homelab is where I
  practise IAM every week: Active Directory, Entra ID, MFA,
  Conditional Access, Intune, and SSO — built, broken, fixed, and
  verified by me.
- **A security mindset from operations.** I work in phased rollouts
  with verification, I check the result before moving on, and I
  document what changed and why. That is how I work on production
  systems at the Embassy, and how I run this lab.
- **Currently preparing for CompTIA Security+ SY0-701** (exam booked
  17 Dec 2026).

## How to read this portfolio

For each project you will find: the problem, what I built, the
verified result — and **what this means for an employer**: the skill
it proves and how it transfers to a company environment. Lab work is
labelled as lab work. I do not claim production experience I do not have.

## Projects — and the role each one supports

| # | Project | Role it supports | What it proves |
|---|---------|------------------|----------------|
| 01 | [Hybrid Identity Lab](projects/01-hybrid-identity-lab/) | IAM Engineer / Analyst | Identity lifecycle, MFA + Conditional Access, GPOs, Entra Connect troubleshooting |
| 02 | [Secure Homelab & Patch Automation](projects/02-patch-automation/) | SOC Analyst / SysAdmin | Vulnerability management, automation, finding and fixing silent failures |
| 03 | [Secure Remote Access & SSO](projects/03-secure-remote-access-sso/) | IAM / Infrastructure Engineer | Zero-trust access, SSO, secure remote access without exposed ports |
| 04 | [UniFi Security Case Study — Java4Shell](projects/04-unifi-java4shell-mitigation/) | SOC Analyst / Security Engineer | Risk-based vulnerability assessment, mitigation, and verification |

## Skills this portfolio demonstrates

- **Identity & Access:** Active Directory, Entra ID, Entra Connect,
  MFA, Conditional Access, Intune, Authentik SSO, Group Policy
- **Security operations:** Vulnerability assessment, risk-based
  prioritisation, mitigation and verification, SSH hardening
- **Automation & infrastructure:** Ansible, systemd timers, Proxmox VE,
  Docker Compose, Linux, networking (UniFi)
- **Ways of working:** Phased rollouts, verification before handover,
  clear documentation, troubleshooting under real constraints

## Stack at a glance

- **Virtualisation:** Proxmox VE 9.2.28, single node (Dell OptiPlex 3040, i7-6700T, 12 GB RAM, 1 TB SSD) — no cluster, by design
- **Identity:** Active Directory, Microsoft Entra ID / Entra Connect, Intune, Authentik
- **Automation:** Ansible (controller in a dedicated container host), systemd timer
- **Network:** UniFi Network 5.1.42, UAP-AC-Pro + UAP-AC-LR access points
- **Services:** Docker (single Docker host, 7 containers), Nginx Proxy Manager, AdGuard Home, Portainer
- **Remote access:** Cloudflare Tunnel, Tailscale, Twingate

## What is NOT here

- No internal network addresses, hostnames, or infrastructure details
  that would help an attacker map the lab.
- No credentials, tokens, keys, `.env` files, or Ansible Vault content.
- No claims about tools I have not run. Lab work is labelled as lab work.

> **DRAFT — 22 Nov 2026.** Public, sanitised version. The full private
> documentation lives in a separate private repo and is not published here.

## Contact

- LinkedIn: linkedin.com/in/emaro03
- Email: emaro03@gmail.com
- Location: Santo Domingo, Dominican Republic — open to travel
