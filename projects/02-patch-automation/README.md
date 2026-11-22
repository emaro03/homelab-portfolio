# 02 — Secure Homelab & Patch Automation

**Status:** Ongoing, since April 2025
**Focus:** Patching, automation, and SSH hardening

## The problem

A homelab with a dozen guests drifts out of date fast if patching is
manual. I wanted patching that runs on its own, on a schedule, with a
clear result — patched, failed, or skipped because a host is off —
instead of silently doing nothing.

## What I built

- Ansible controller in its own dedicated container host
  (Ansible Core 2.21.5)
- Inventory of 10 hosts (VMs and containers)
- A systemd timer running the patch playbook every 48 hours,
  at about 02:00 AST
- Playbook: `apt dist-upgrade` + Docker prune + reboot if required,
  except for the Proxmox node and the Ansible host itself
- SSH key-based authentication everywhere; root login and password
  authentication disabled on guests, root SSH key-only on the node

## Verified result — 22 Nov 2026, 02:00–02:02 AST

- **7 / 7 powered-on hosts patched, 0 failures, in 2 min 41 s**
- The Proxmox node and the UniFi controller installed updates;
  UniFi restarted as part of that
- 3 hosts were stopped (media server, GLPI, SIEM) and were skipped,
  as expected — they show as unreachable in the run, which is not a
  patch failure

## A bug I found and fixed — 21 Nov 2026

The scheduled run had been silently broken since it was created:

1. The timer never passed the `target` variable, so every scheduled
   run failed with `'target' is undefined`. Fixed by passing
   `-e target=all`.
2. The controller never passed its SSH key, so hosts rejected the
   connection. Fixed by setting the Ansible SSH key in the inventory
   group variables.

After the fix, `--list-hosts` resolves all 10 hosts and a ping test
answers 7 / 7 powered-on hosts. The next run was scheduled for
Tue 24 Nov 2026, ~01:59 AST.

## What this means for an employer

- **Vulnerability management that actually runs:** patching on a
  schedule, with a clear result for every host — patched, failed,
  or skipped because it is off. No silent drift.
- **I find silent failures:** the scheduled run had been broken
  since it was created and nobody noticed, because it failed
  quietly. I found the two root causes (a missing variable and a
  missing SSH key), fixed them, and verified the fix with a live
  run — 7 / 7 hosts, 0 failures.
- **Security hygiene as a habit:** key-only SSH, no password logins
  on guests, patching every 48 hours. I apply the same discipline
  to infrastructure that I apply to identity.

**In a company, this transfers to:** patch compliance and
vulnerability remediation, automation of routine maintenance,
hardening baselines, and investigating why an automated job
"ran" but changed nothing — a common SOC / sysadmin problem.

## Tech

Ansible · systemd timers · Proxmox VE · SSH (key-only) · Docker · Linux
