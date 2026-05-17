# Subfinder

> **Category:** Open-Source Passive Subdomain Discovery Tool  
> **License:** MIT  
> **GitHub:** [projectdiscovery/subfinder](https://github.com/projectdiscovery/subfinder)  
> **Maintained by:** ProjectDiscovery

---

## Overview

Subfinder is a fast, passive subdomain enumeration tool from ProjectDiscovery. It queries dozens of passive sources (crt.sh, VirusTotal, Shodan, Censys, SecurityTrails, etc.) to quickly build a subdomain list — without touching the target directly.

It's narrower than Amass (fewer data sources, no active DNS) but significantly faster for quick reconnaissance.

---

## Install Difficulty

**Very Easy.**

```bash
go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest

# or via Docker
docker pull projectdiscovery/subfinder
```

---

## Ideal Use Case

- Quick passive subdomain discovery before a pentest
- Building a fast target list to feed into httpx + Nuclei
- Bug bounty initial scope mapping
- Part of a larger automation pipeline

---

## Strengths

| Strength | Detail |
|----------|--------|
| **Speed** | Significantly faster than Amass for passive enumeration |
| **MIT license** | Fully permissive |
| **ProjectDiscovery ecosystem** | Pairs naturally with httpx, naabu, nuclei |
| **Simple output** | Clean one-subdomain-per-line output; easy to pipe |
| **API key support** | Add keys for Shodan, Censys, VirusTotal for better coverage |

---

## Weaknesses

| Weakness | Detail |
|----------|--------|
| **Passive only** | No active DNS brute force; lower coverage than Amass |
| **No persistence** | Results are point-in-time text output |
| **No vuln scanning** | Discovery only |
| **Fewer sources than Amass** | Amass aggregates more data sources overall |

---

## When to Choose Subfinder

- You need **fast passive enumeration** (minutes, not hours)
- You want the **ProjectDiscovery toolchain** (subfinder → httpx → nuclei)
- You need **simple CLI output** to pipe into other tools

## When to Choose Something Else

- You need **maximum coverage** → [Amass](amass.md)
- You need a **full pipeline** → [reNgine](rengine.md) (subfinder runs inside it)
- You need **persistent monitoring** → [HailBytes ASM](https://hailbytes.com/asm)

---

## In the reNgine / HailBytes ASM Ecosystem

Subfinder is one of the primary discovery tools in reNgine's enumeration phase, alongside Amass, assetfinder, findomain, and others. The platform handles API keys, output correlation, and persistence automatically.

> Want this delivered managed in your AWS/Azure? **[See HailBytes ASM →](https://hailbytes.com/asm)**
