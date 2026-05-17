# reNgine

> **Category:** Open-Source Reconnaissance Framework  
> **License:** GPL-3.0  
> **GitHub:** [yogeshojha/rengine](https://github.com/yogeshojha/rengine)  
> **Latest Stable:** v2.2+

---

## Overview

reNgine is a full-pipeline automated reconnaissance framework designed for pentesters and red teamers. It orchestrates 30+ tools — subfinder, amass, naabu, nmap, httpx, nuclei, dalfox, gf, and more — into a unified Django/Celery platform with a web UI, multi-tenant project support, and scheduled scanning.

Unlike point tools (Amass, Nuclei), reNgine is a *platform*: it stores all findings in PostgreSQL, correlates data across tools, and presents a unified view of your attack surface over time.

---

## Install Difficulty

**Medium-High.** Docker Compose-based, but requires:
- A Linux host with Docker + Docker Compose installed
- Domain configuration (for TLS in production)
- Reasonable RAM (4GB minimum, 8GB recommended for full scans)
- familiarity with environment variables / .env configuration

```bash
git clone https://github.com/yogeshojha/rengine && cd rengine
cp .env.sample .env    # edit secrets
docker-compose up -d
```

Managed alternative: [HailBytes ASM](https://hailbytes.com/asm) — deploy from AWS/Azure Marketplace with no Docker expertise needed.

---

## Ideal Use Case

- Pentest firms running recurring ASM engagements
- MSSPs monitoring multiple client attack surfaces continuously
- Red teams that want a persistent, correlated findings database
- Anyone who wants to replace a bash-script recon pipeline with a structured platform

---

## Strengths

| Strength | Detail |
|----------|--------|
| **Full pipeline** | Subdomain enum → port scan → web crawl → vuln scan in one workflow |
| **30+ tools integrated** | subfinder, amass, naabu, nmap, httpx, nuclei, dalfox, gf, gau, waybackurls, and more |
| **Multi-tenant** | Projects per client; RBAC with role-based access |
| **AI analysis** | v2.1+ integrates OpenAI GPT or local Ollama for finding triage and report summaries |
| **Scheduled scans** | Cron-based continuous monitoring; diff alerts on new findings |
| **Web UI** | Full Django web app; no CLI knowledge needed for day-to-day use |
| **Compliance** | (HailBytes fork) 10 compliance framework reports including HIPAA, SOC 2, PCI DSS, FedRAMP, NYDFS, GDPR, ISO 27001, CIS v8, NIST CSF 2.0 |
| **Alert integrations** | Slack, Teams, Discord, Telegram, Lark, PagerDuty, Opsgenie |

---

## Weaknesses

| Weakness | Detail |
|----------|--------|
| **Self-hosting burden** | Docker Compose setup is non-trivial; updates require maintenance |
| **Resource intensive** | Full scans on large targets can max out RAM/CPU on small hosts |
| **GPL-3.0 license** | Copyleft; commercial embedding requires careful legal review |
| **Setup time** | First-run experience is slow; no 1-click cloud deployment in OSS version |
| **UI complexity** | Web UI has a learning curve; overwhelming for simple one-off scans |

---

## When to Choose reNgine

- You want a **self-hosted, full-pipeline ASM platform**
- You run **recurring engagements** and need persistent findings history
- You need **multi-tenant** client separation
- You're comfortable with Docker and willing to manage your own infrastructure
- You want **LLM-assisted triage** without paying SaaS prices

## When to Choose Something Else

- You just need **subdomain enumeration** → use [Amass](amass.md) or [Subfinder](subfinder.md) — faster and simpler
- You just need **vulnerability scanning** → use [Nuclei](nuclei.md) standalone
- You need **zero DevOps overhead** → use [HailBytes ASM](https://hailbytes.com/asm) (managed reNgine)
- You need **passive internet-wide data** → use [Shodan](shodan.md) or [Censys](censys.md)
- You're doing a quick one-off recon → Amass + Nuclei CLI is faster to spin up

---

## Managed Option

**[HailBytes ASM](https://hailbytes.com/asm)** is the enterprise-managed version of reNgine. Same core engine, hardened for production:

- Deploy in minutes from AWS Marketplace or Azure Marketplace (including Azure Government)
- Multi-tenant from day one: one platform, all your clients
- Automatic updates — you're never stuck on an old version
- 10 compliance frameworks with exportable evidence reports
- Enterprise support included

> Want this delivered managed in your AWS/Azure? **[See HailBytes ASM →](https://hailbytes.com/asm)**
