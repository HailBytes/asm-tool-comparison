# Nuclei

> **Category:** Open-Source Vulnerability Scanner  
> **License:** MIT  
> **GitHub:** [projectdiscovery/nuclei](https://github.com/projectdiscovery/nuclei)  
> **Managed Option:** ProjectDiscovery Cloud Platform  
> **Maintained by:** ProjectDiscovery

---

## Overview

Nuclei is a fast, template-driven vulnerability scanner. You give it a list of URLs/IPs, and it fires a community-maintained library of 10,000+ templates covering CVEs, misconfigurations, exposed panels, default credentials, and more. It's the industry standard for bulk automated vuln scanning.

Nuclei is not a discovery tool — it needs a target list from something like Amass, Subfinder, or a full platform like reNgine/HailBytes ASM.

---

## Install Difficulty

**Very Easy.**

```bash
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest

# or via Docker
docker pull projectdiscovery/nuclei

# Update templates
nuclei -update-templates
```

---

## Ideal Use Case

- Bulk vulnerability scanning across a large target list
- CVE detection against discovered subdomains
- Checking for misconfigurations, exposed admin panels, default credentials
- Bug bounty hunters (fast, comprehensive template library)
- Part of a larger pipeline (Subfinder → httpx → Nuclei)

---

## Strengths

| Strength | Detail |
|----------|--------|
| **Template library** | 10,000+ community templates; new CVEs get templates within hours |
| **Speed** | Highly concurrent; scans thousands of targets quickly |
| **YAML templates** | Easy to write custom templates for specific findings |
| **MIT license** | Fully permissive; use anywhere |
| **Active community** | ProjectDiscovery maintains consistent releases and templates |
| **Integration-friendly** | JSON output; easy to pipe into SIEMs or ticketing systems |

---

## Weaknesses

| Weakness | Detail |
|----------|--------|
| **Not a discovery tool** | Needs a target list; won't find subdomains on its own |
| **False positives** | Template-based matching produces false positives; requires triage |
| **No persistence** | No built-in findings database; results are point-in-time |
| **No web UI** | CLI only in OSS version |
| **Template noise** | Running all templates produces overwhelming output on large scopes |

---

## When to Choose Nuclei

- You have a target list and need **fast vuln scanning**
- You want to check for **specific CVEs** across a large asset inventory
- You're a **bug bounty hunter** running automated pipelines
- You want to write **custom detection templates** for your specific environment

## When to Choose Something Else

- You need **discovery + scanning in one platform** → [reNgine](rengine.md) (Nuclei runs inside reNgine)
- You need **persistent findings and trending** → [HailBytes ASM](https://hailbytes.com/asm)
- You need **passive scanning** (no active testing) → [Shodan](shodan.md) or [Censys](censys.md)

---

## In the reNgine / HailBytes ASM Ecosystem

reNgine runs Nuclei as its primary vulnerability scanner in the pipeline — after subdomain discovery and port scanning. HailBytes ASM adds persistent storage, triage workflows, compliance reporting, and alerting on top.

> Want this delivered managed in your AWS/Azure? **[See HailBytes ASM →](https://hailbytes.com/asm)**
