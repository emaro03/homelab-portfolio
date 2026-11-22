# 03 — Secure Remote Access & SSO

**Status:** Ongoing
**Focus:** Secure external access without exposing services directly

## The problem

I need to reach homelab services from outside my home network without
opening ports to the internet or exposing admin consoles. The answer
is layered access: identity first, then a tunnel, with DNS filtering
on top.

## What I built

- **Authentik** (2026.8.5) as the single sign-on / identity provider
  for homelab services, backed by PostgreSQL
- **Cloudflare Tunnel** for external access — no inbound ports opened
- **Tailscale** and **Twingate** as additional private remote-access
  paths
- **Nginx Proxy Manager** (2.17.1) as the reverse proxy
- **AdGuard Home** for DNS filtering on the local network
- **Portainer** for container management
- All seven services run as Docker containers on a single dedicated
  Docker host, managed with Docker Compose

## Design decisions

- One Docker host for all containers, instead of spreading them
  across hosts — simpler to patch, back up, and reason about
- SSO in front of services, rather than a separate login per service
- No direct exposure of admin consoles: access goes through the
  tunnel / private network + Authentik
- Services I no longer use get removed, not left running — n8n and
  Uptime Kuma were deleted in November 2026

## What this means for an employer

- **Zero-trust thinking in practice:** identity first (Authentik
  SSO), then a private tunnel — no open inbound ports, no admin
  console exposed to the internet. Access is granted to a person
  through identity, not to the world through a port.
- **Layered defence, not one tool:** SSO + tunnel + reverse proxy +
  DNS filtering. If one layer fails, the others still hold.
- **Operational discipline:** services I no longer use get removed,
  not left running and forgotten. That is how attack surface
  actually shrinks.

**In a company, this transfers to:** SSO onboarding for internal
tools, secure remote access for hybrid / remote staff, reverse
proxy and DNS-layer controls, and reducing exposed services —
the same patterns behind a corporate zero-trust rollout, at lab
scale and fully hands-on.

## Tech

Authentik · Cloudflare Tunnel · Tailscale · Twingate ·
Nginx Proxy Manager · AdGuard Home · Docker Compose · Portainer
