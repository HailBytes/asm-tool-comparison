# Amass

> **Category:** Open-Source Subdomain Enumeration Tool  
> **License:** Apache 2.0  
> **GitHub:** [owasp-amass/amass](https://github.com/owasp-amass/amass)  
> **Maintained by:** OWASP

---

## Overview

Amass is the gold standard for subdomain enumeration. It's a CLI tool maintained by OWASP that aggregates data from 50+ passive data sources (certificate transparency logs, DNS brute force, web scraping, APIs) and active DNS resolution to build a comprehensive subdomain map.

It is **not** a full ASM platform — it produces a target list, not a vulnerability report. But for pure subdomain coverage, nothing beats it.

---

## Install Difficulty

**Easy.**

```bash
# via Go
go install -v github.com/owasp-amass/amass/v4/...@master

# via Docker
docker pull caffix/amass

# via apt (Kali/Ubuntu)
apt-get install amass
```

---

## Ideal Use Case

- Building a comprehensive subdomain inventory before a pentest
- Bug bounty scope mapping
- Feeding discovered subdomains into downstream scanners (Nuclei, nmap)
- Passive OSINT enumeration without touching target infrastructure

---

## Strengths

| Strength | Detail |
|----------|--------|
| **Depth of enumeration** | 50+ data sources: Shodan, VirusTotal, Censys, crt.sh, CommonCrawl, and more |
| **OWASP backing** | Well-maintained, widely trusted in the security community |
| **Passive + active modes** | Can enumerate without touching the target (pure passive) |
| **Graph output** | Produces relationship graphs of discovered infrastructure |
| **API integrations** | Free API keys for many sources significantly improve coverage |
| **Apache 2.0 license** | Permissive; commercial-friendly |

---

## Weaknesses

| Weakness | Detail |
|----------|--------|
| **Enumeration only** | No port scanning, no vuln scanning — needs downstream tools |
| **Speed** | Comprehensive scans take hours on large targets |
| **API key management** | Best results require configuring 10+ API keys |
| **No web UI** | CLI only; results in JSON/text output |
| **Memory usage** | Large scans can consume significant RAM |

---

## When to Choose Amass

- You need the **most comprehensive subdomain list** possible
- You want **passive enumeration** (no active scanning)
- You're building a **target inventory** to feed into other tools
- You have API keys for the major passive sources

## When to Choose Something Else

- You need **speed over comprehensiveness** → [Subfinder](subfinder.md) is faster
- You need a **full pipeline** (subdomain → vuln scan) → [reNgine](rengine.md) or [BBOT](bbot.md)
- You need a **managed platform** → [HailBytes ASM](https://hailbytes.com/asm)

---

## In the reNgine / HailBytes ASM Ecosystem

reNgine (and HailBytes ASM) run Amass as one of several enumeration tools in the pipeline, alongside subfinder, assetfinder, and others. You get Amass coverage without managing it separately.

> Want this delivered managed in your AWS/Azure? **[See HailBytes ASM →](https://hailbytes.com/asm)**
