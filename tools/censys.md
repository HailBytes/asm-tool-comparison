# Censys

> **Category:** Commercial Internet Scanner / ASM Platform  
> **License:** Proprietary  
> **Website:** [censys.io](https://censys.io)  
> **Pricing:** Free tier (limited) · ASM platform: enterprise custom pricing

---

## Overview

Censys is an internet scanning company that operates two products: a passive internet scan database (similar to Shodan) and a commercial ASM platform (Censys ASM) that actively monitors your attack surface using their data.

Censys tends to have stronger IPv6 coverage and more structured certificate data than Shodan, making it complementary rather than directly competitive.

---

## Install Difficulty

**N/A — SaaS product.** Python library available:

```bash
pip install censys
export CENSYS_API_ID=<id>
export CENSYS_API_SECRET=<secret>
censys search "your-domain.com"
```

---

## Ideal Use Case

- **ASM platform** (commercial): Continuous external attack surface monitoring without self-hosting
- **Research**: Structured queries against internet scan data
- **IPv6 exposure auditing**: Better IPv6 coverage than Shodan
- **Certificate transparency analysis**: Robust certificate data for subdomain discovery
- **Complement to Shodan**: Different crawler; catches different things

---

## Strengths

| Strength | Detail |
|----------|--------|
| **Data quality** | High-quality, structured certificate and host data |
| **ASM product** | Full commercial ASM platform (Censys ASM) for enterprise teams |
| **IPv6 coverage** | Better IPv6 scanning coverage than Shodan |
| **API** | Clean, well-documented REST API |
| **Research access** | Free academic/research access with application |

---

## Weaknesses

| Weakness | Detail |
|----------|--------|
| **Price** | Censys ASM is enterprise-priced; not accessible for small firms |
| **SaaS lock-in** | No self-hosted option; your data lives in Censys |
| **Passive database** | Same staleness issues as Shodan for point-in-time queries |
| **No active vuln scanning** | Database queries, not active exploitation testing |
| **Vendor dependency** | Pricing and data access subject to change |

---

## When to Choose Censys

- You need a **commercial ASM platform** with a defined budget
- You want **Shodan-like data with better IPv6/certificate coverage**
- You're doing **large-scale research** (academic access is generous)
- You need **ASM data without any self-hosting**

## When to Choose Something Else

- You need **active vuln scanning** → [Nuclei](nuclei.md) + [reNgine](rengine.md)
- You want a **self-hosted, self-controlled platform** → [reNgine](rengine.md)
- You want **managed ASM without enterprise pricing** → [HailBytes ASM](https://hailbytes.com/asm) (AWS/Azure Marketplace)
- You need **IoT/OT device coverage** → [Shodan](shodan.md)

---

## In the reNgine / HailBytes ASM Ecosystem

reNgine uses the Censys API (when configured) as a passive discovery source, alongside Shodan, crt.sh, and others. You get Censys data coverage as part of the full pipeline.

> Want this delivered managed in your AWS/Azure? **[See HailBytes ASM →](https://hailbytes.com/asm)**
