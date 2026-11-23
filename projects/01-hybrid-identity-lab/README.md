# 01 — Hybrid Identity Lab

**Status:** Ongoing, since April 2025
**Focus:** Identity & Access Management (IAM)

## The problem

I wanted hands-on practice with the identity stack I support in my day
job, beyond theory: a real on-premises directory synced to the cloud,
with the same controls an organisation would enforce — MFA, conditional
access, device management, and group policy — so I can test changes
safely before they matter.

## What I built

- On-premises Active Directory domain, with an OU structure organised
  by department
- Microsoft Entra Connect syncing identities to Entra ID
- MFA and Conditional Access enforced in Entra ID
- Intune for endpoint management (policies in progress)
- Authentik as SSO / identity provider for homelab services
- A hybrid-joined Windows endpoint to test the full join + sync + policy flow

## Controls in place

- **5 Group Policies:** USB restriction, drive mapping, password policy,
  network settings, Control Panel restrictions
- **Entra ID:** MFA + Conditional Access enforced
- **Sync:** Entra Connect active

## What I learned / verified

- How department-based OUs map to real GPO scoping, and what breaks
  when a policy is too broad
- That sync and conditional access are only useful if they are tested
  end-to-end from a real joined endpoint, not just enabled in a portal
- One open item I am still working through: an Entra Connect export
  permission issue on one user account

## What this means for an employer

For an IAM team, this is the work behind the project — and what I am building toward:

- **Identity lifecycle, hands-on:** I have built a directory, synced
  it to the cloud, and tested the full flow from a real joined
  endpoint. I understand what breaks between on-prem and cloud
  identity, because I have debugged it.
- **Enforcing access, not just enabling it:** MFA and Conditional
  Access are enforced here, and GPOs restrict USB, enforce password
  policy, and lock down Control Panel. I think in controls, not
  just in accounts.
- **Troubleshooting sync and permissions:** I am working through a
  real Entra Connect export permission issue on one user. I do not
  hide open items — I track them and fix them.

**In a company, this transfers to:** onboarding / offboarding and
access reviews, MFA and Conditional Access rollouts, GPO
management, and Entra Connect / hybrid identity support — with
testing on a joined endpoint before a change reaches users.

## Next steps

- Finish the Intune policy rollout
- Proxmox OIDC via Authentik as the next SSO step

## Tech

Active Directory · Microsoft Entra ID · Entra Connect · Intune ·
Authentik · Windows · Group Policy
