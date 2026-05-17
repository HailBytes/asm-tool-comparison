# Shodan

> **Category:** Commercial Internet Scanner / Passive Data Source  
> **License:** Proprietary  
> **Website:** [shodan.io](https://www.shodan.io)  
> **Pricing:** Free tier (limited) · Membership $49/mo · Enterprise custom

---

## Overview

Shodan is an internet-wide passive scanner that continuously crawls the entire internet, indexing banners, certificates, and service data from every IP address. It's a search engine for internet-connected devices and exposed services.

Shodan is *not* an active scanner — it queries Shodan's historical database rather than scanning targets in real time. This makes it safe for initial reconnaissance but potentially outdated.

---

## Install Difficulty

**N/A — SaaS product.** Web UI at shodan.io, plus a CLI tool:

```bash
pip install shodan
shodan init <API_KEY>
shodan search "org:TargetCorp"
```

---

## Ideal Use Case

- **Passive reconnaissance**: Know what's exposed without touching the target
- **Quick exposure checks**: "What does the internet see for domain X?"
- **IoT/OT device discovery**: Industrial control systems, cameras, printers
- **Threat intelligence**: Monitoring for exposed credentials, leaked configs
- **M&A due diligence**: Quick external exposure snapshot of an acquisition target

---

## Strengths

| Strength | Detail |
|----------|--------|
| **Passive** | No active scanning; won't trigger IDS/firewall alerts |
| **Speed** | Instant results from a pre-built database |
| **Coverage** | The largest passive internet-scan database in the world |
| **API** | Rich API; integrate into workflows and pipelines |
| **Historical data** | Query past states of a target's infrastructure |
| **IoT/OT coverage** | Unique coverage for non-HTTP services and industrial devices |

---

## Weaknesses

| Weakness | Detail |
|----------|--------|
| **Stale data** | Shodan crawls on its own schedule; data may be weeks or months old |
| **Passive only** | Won't find subdomains not indexed; misses ephemeral assets |
| **No vuln scanning** | Identifies services, not vulnerabilities (beyond banner matching) |
| **Cost** | Serious use requires paid API access |
| **No web app coverage** | HTTP-level vulnerabilities (XSS, SQLi) are invisible to Shodan |
| **SaaS only** | No self-hosted option |

---

## When to Choose Shodan

- You need a **quick, passive external exposure snapshot**
- You're doing **M&A due diligence** and can't actively scan the target
- You need **IoT/OT device visibility** (cameras, PLCs, routers)
- You want to **supplement active scanning** with historical passive data

## When to Choose Something Else

- You need **up-to-date, active scanning** → [reNgine](rengine.md) or [HailBytes ASM](https://hailbytes.com/asm)
- You need **web app vulnerability scanning** → [Nuclei](nuclei.md)
- You need **comprehensive subdomain discovery** → [Amass](amass.md)
- You need **persistent continuous monitoring** → [HailBytes ASM](https://hailbytes.com/asm)

---

## In the reNgine / HailBytes ASM Ecosystem

reNgine queries Shodan (and Censys) as one of its passive subdomain discovery sources. You get Shodan's passive data *plus* active verification and vulnerability scanning — without juggling multiple tools.

> Want this delivered managed in your AWS/Azure? **[See HailBytes ASM →](https://hailbytes.com/asm)**
