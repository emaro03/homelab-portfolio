# 04 — UniFi Security Case Study: Java4Shell (CVE-2026-114938)

**Status:** Temporary mitigation applied and verified, 22 Nov 2026
**Focus:** Vulnerability assessment, practical risk, and verified mitigation

## The problem

In November 2026 a vulnerability in Java's Base64 decoding
(CVE-2026-114938, "Java4Shell") was reported as affecting Temurin
Java 25. My UniFi Network controller (5.1.42) runs on a bundled
Temurin Java 25, so I needed to know: am I affected, how exposed
am I, and what can I do before Ubiquiti ships a fix?

## What I found

- **Affected version:** Temurin Java 25+36 (September 2025), bundled
  inside the UniFi OS Server install — not a system package, so it
  is not patched by `apt`. The fixed Temurin (25.0.5.1) only arrives
  with a Ubiquiti UniFi update.
- **Practical risk: low.** The UniFi console port is blocked by the
  host firewall (default deny incoming, only SSH allowed), and the
  console is not exposed through Cloudflare. There is no path from
  outside to reach that Java process.
- **Uncertainty I did not bet on:** sources disagreed on whether the
  flaw triggers only with AVX-512 VBMI instructions or also with
  AVX2. My CPU has AVX2, so I did not rely on the CPU as protection.

## The mitigation

A JVM flag that disables the vulnerable fast path and falls back to
the regular implementation:

```
-XX:-UseBASE64Intrinsics
```

Added to `UNIFI_JVM_OPTS` in the UniFi startup defaults, then the
UniFi OS service was restarted (admin console down 1–2 minutes;
Wi-Fi kept working throughout).

## Verification — 22 Nov 2026, ~15:28 AST

- New Java process started with the flag in its command line
- Admin console responds (HTTP 200)
- UniFi API responds (HTTP 200)
- Wi-Fi unaffected

## Caveat

A future UniFi update may overwrite the startup defaults file and
remove the flag. **Re-check the flag after every UniFi update.**
The permanent fix is the Ubiquiti update that bundles the patched Java.

## What this means for an employer

- **Risk-based triage, not panic patching:** I checked first
  whether I was affected, how exposed I was, and what the real
  path to exploitation would be — then acted in proportion to
  the risk. That is SOC work: assess, prioritise, mitigate,
  verify.
- **I do not bet on uncertainty:** sources disagreed on the exact
  trigger. Instead of assuming the safer reading, I applied a
  mitigation that works under either reading.
- **Verification and follow-through:** I verified the fix with a
  live process check and service checks, and I recorded the one
  thing that could undo it — a future update overwriting the
  file — so it gets re-checked. A mitigation without a re-check
  is a future incident.

**In a company, this transfers to:** vulnerability triage and
assessment, applying and verifying temporary mitigations while
waiting for a vendor patch, documenting caveats and re-checks,
and communicating risk clearly to non-technical stakeholders.

## Tech

UniFi Network 5.1.42 · UniFi OS Server · Temurin Java 25 · Linux firewall (UFW)
