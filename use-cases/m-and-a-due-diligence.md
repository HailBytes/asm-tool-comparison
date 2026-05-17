# Use Case: M&A Cybersecurity Due Diligence

> **Profile:** Acquirer, investment firm, or their security advisor assessing the cyber risk of an acquisition target

---

## The Problem

When a company acquires another, it inherits that company's entire attack surface — including vulnerabilities the target may not know about. A 2023 IBM study found that 35% of data breaches involve a third-party or supply chain compromise. Acquirers who skip cyber due diligence routinely discover expensive security debt post-close.

You typically need to:
- Assess the target's **external attack surface** quickly (before close)
- Often **without the target's cooperation** in the early stages
- Produce a **risk-quantified report** for the deal team
- Work within **legal constraints** (active scanning may require authorization)

---

## The Legal Constraint

Active scanning (port scanning, vulnerability scanning) against a company without authorization is legally risky in most jurisdictions. Due diligence ASM typically means:

1. **Passive recon first** — Shodan, Censys, crt.sh, OSINT (always legal)
2. **Active scanning only after authorization** — typically via LOI/NDA clause or post-LOI cooperation

This makes **Shodan and Censys particularly valuable** in the early due diligence phase.

---

## Phase 1: Passive Reconnaissance (Pre-Authorization)

**Tools:** Shodan, Censys, Amass (passive mode), crt.sh, LinkedIn OSINT

```bash
# Passive subdomain discovery (no active scanning)
amass enum -passive -d targetcompany.com -o passive-subs.txt

# Shodan query
shodan search "org:TargetCompany" --fields ip_str,port,org,hostnames

# Certificate transparency
curl "https://crt.sh/?q=%.targetcompany.com&output=json" | \
  python3 -c "import sys,json; [print(c['name_value']) for c in json.load(sys.stdin)]" | \
  sort -u

# Censys query
censys search "targetcompany.com" --index hosts
```

**Deliverable:** External asset inventory (subdomains, IPs, exposed services) from passive sources only.

---

## Phase 2: Authorized Active Assessment (Post-LOI)

Once authorization is obtained (via NDA/LOI clause), run a full ASM assessment:

**Tools:** reNgine or HailBytes ASM

```
Full scan scope:
├─ All identified domains and subdomains
├─ Known IP ranges (from ARIN/RIPE lookup)
└─ Cloud asset enumeration (AWS, Azure, GCP)

Scan outputs:
├─ Complete asset inventory
├─ Open port/service map
├─ Vulnerability findings (CVSS scores)
├─ Technology stack (for known EOL/CVE exposure)
└─ Compliance gap indicators
```

---

## Risk Assessment Framework

Map findings to financial risk for the deal team:

| Finding Category | Risk Level | Example M&A Impact |
|-----------------|:-----------:|-------------------|
| Critical CVE (CVSS 9+) in internet-facing service | 🔴 High | May require immediate remediation funding |
| Exposed admin panels / default credentials | 🔴 High | Active breach risk; may delay close |
| EOL software with known CVEs | 🟡 Medium | Technical debt to factor into deal price |
| Excessive attack surface (hundreds of forgotten subdomains) | 🟡 Medium | Security hygiene concern; ongoing remediation cost |
| Missing MFA on critical systems | 🟡 Medium | Compliance risk if regulated industry |
| Outdated TLS/certificates | 🟢 Low | Operational debt; quick remediation |

---

## Reporting Template

A cyber due diligence report for M&A should include:

1. **Executive Summary** — Overall risk rating (Low/Medium/High/Critical), deal recommendation
2. **Attack Surface Overview** — Total assets discovered, breakdown by category
3. **Critical Findings** — Any finding requiring immediate deal-team attention
4. **Full Findings Table** — CVSS score, asset, description, remediation
5. **Comparison to Industry Baseline** — How does target compare to peers?
6. **Remediation Cost Estimate** — What will it cost to fix the top issues?
7. **Post-Acquisition Roadmap** — 30/60/90-day remediation plan

---

## Tool Comparison for M&A Due Diligence

| Tool | Passive Recon | Active Scan | Report Export | M&A Fit |
|------|:---:|:---:|:---:|---------|
| **Shodan/Censys** | ✅ | ❌ | Limited | Great for Phase 1 |
| **Amass (passive)** | ✅ | ❌ | JSON/text only | Great for Phase 1 |
| **reNgine** | ✅ | ✅ | ❌ (manual) | Phase 2, self-hosted |
| **HailBytes ASM** | ✅ | ✅ | ✅ Compliance exports | Phase 2, managed |
| **Nuclei only** | ❌ | ✅ | JSON/text only | Phase 2 supplement |

---

## Engagement Structure

```
Week 1: Passive OSINT (no authorization needed)
Week 2-3: Authorized active scanning (post-LOI)
Week 4: Report writing and deal-team briefing
```

For portfolio monitoring (ongoing due diligence across multiple investments), [HailBytes ASM](https://hailbytes.com/asm) multi-tenant architecture allows monitoring all portfolio companies from a single platform.

---

> **Want this delivered managed in your AWS/Azure?**  
> [HailBytes ASM](https://hailbytes.com/asm) is used by pentest firms and investment advisors for both one-time due diligence assessments and ongoing portfolio monitoring. Deploy from AWS or Azure Marketplace. [Book a demo →](https://hailbytes.com/asm)
