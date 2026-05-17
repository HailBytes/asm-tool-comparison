# BBOT (Bighuge BLS OSINT Tool)

> **Category:** Open-Source Reconnaissance Framework  
> **License:** GPL-3.0  
> **GitHub:** [blacklanternsecurity/bbot](https://github.com/blacklanternsecurity/bbot)  
> **Maintained by:** Black Lantern Security

---

## Overview

BBOT is a modular, recursive OSINT and attack surface mapping framework. Its core innovation is a **recursive scan model** — each discovered asset (subdomain, IP, email) is automatically fed back as input to all relevant modules, enabling deep discovery that static pipelines miss.

BBOT is more developer-friendly than reNgine (Python module system, CLI-first) and less UI-friendly. It's the tool of choice for security engineers who want to build custom recon automation.

---

## Install Difficulty

**Easy-Medium.**

```bash
pip install bbot
bbot -t example.com -f subdomain-enum
bbot -t example.com -f subdomain-enum web-basic
```

Or via Docker:
```bash
docker run blacklanternsecurity/bbot -t example.com -f subdomain-enum
```

---

## Ideal Use Case

- Security engineers building **custom recon pipelines**
- **Deep recursive enumeration** — finding assets 3-4 hops removed from the initial target
- **OSINT investigations** — email addresses, GitHub orgs, AWS S3 buckets, employee names
- **Bug bounty automation** with custom module development
- Researchers who want fine-grained control over module selection

---

## Strengths

| Strength | Detail |
|----------|--------|
| **Recursive engine** | Discovered assets become inputs automatically; finds deeper relationships |
| **Modular** | Python module system; easy to extend with custom modules |
| **OSINT breadth** | Emails, GitHub orgs, social media, cloud assets, not just subdomains |
| **Cloud asset discovery** | S3 buckets, Azure Blobs, GCP storage enumeration |
| **Active community** | Regular releases; Black Lantern Security actively maintains |
| **Good documentation** | Well-documented module system |

---

## Weaknesses

| Weakness | Detail |
|----------|--------|
| **No web UI** | CLI-first; no built-in dashboard for findings management |
| **Smaller community** | Fewer users than Amass or ProjectDiscovery tools |
| **Steeper learning curve** | Module system powerful but complex |
| **No persistent findings DB** | Results in output files; no trending or historical comparison |
| **GPL-3.0** | Copyleft license; commercial embedding requires care |

---

## When to Choose BBOT

- You want **recursive, deep enumeration** that chases every discovered asset
- You need **OSINT breadth** beyond subdomains (emails, cloud, GitHub)
- You're building **custom Python recon modules**
- You prefer a **code-first** approach over a web UI

## When to Choose Something Else

- You want a **web UI and persistent findings** → [reNgine](rengine.md) or [HailBytes ASM](https://hailbytes.com/asm)
- You just need **fast passive subdomain discovery** → [Subfinder](subfinder.md)
- You need **maximum subdomain enumeration** → [Amass](amass.md)
- You need **zero infrastructure management** → [HailBytes ASM](https://hailbytes.com/asm)

---

## Managed Option

There is no official managed/hosted BBOT offering. For a managed ASM platform with comparable capabilities, [HailBytes ASM](https://hailbytes.com/asm) is the closest alternative.

> Want this delivered managed in your AWS/Azure? **[See HailBytes ASM →](https://hailbytes.com/asm)**
