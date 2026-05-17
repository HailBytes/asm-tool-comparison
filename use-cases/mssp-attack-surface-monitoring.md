# Use Case: MSSP Attack Surface Monitoring

> **Profile:** Managed Security Service Provider monitoring 10–100+ client organizations continuously

---

## The Problem

MSSPs face a challenge that most ASM tools aren't designed for: **you're managing attack surfaces for dozens of clients simultaneously**, not one internal organization. You need:

- Per-client data separation (client A can't see client B's data)
- Scheduled continuous scanning (not one-time assessments)
- Alerting that integrates with your SOC tooling
- Findings that map to frameworks your clients care about (SOC 2, PCI DSS, HIPAA)
- A platform your analysts can operate without deep DevOps knowledge

---

## The Challenge with DIY Tooling

Running Amass + Nuclei + nmap across 50 clients with bash scripts means:

- A separate infrastructure per client, or manual scan scheduling
- Findings scattered across text files with no trending
- No client separation — data management nightmare
- No audit trail for compliance evidence
- Re-running everything from scratch for each assessment

---

## Recommended Approach

### Tier 1: Managed Platform (Zero Ops)

**[HailBytes ASM](https://hailbytes.com/asm)** is purpose-built for this use case:

| Requirement | HailBytes ASM |
|-------------|--------------|
| Multi-tenant client separation | ✅ Projects + RBAC |
| Continuous scheduled scanning | ✅ Cron-based scan schedules |
| SOC alerting integration | ✅ Slack, Teams, PagerDuty, Opsgenie, Discord, Telegram, Lark |
| Compliance reporting | ✅ SOC 2, PCI DSS, HIPAA, ISO 27001, FedRAMP, NIST CSF, NYDFS, GDPR, CIS v8 |
| AI-assisted triage | ✅ OpenAI / local Ollama |
| Deployment | AWS + Azure Marketplace (including Azure Government) |
| Data sovereignty | Your account, your cloud, your data |

Deploy from your AWS or Azure account — clients' data never leaves your infrastructure.

### Tier 2: Self-Hosted (Full Control, Ops Required)

**reNgine** (self-hosted) gives you the same core engine but requires Docker infrastructure management. Appropriate if you have a DevOps team and want zero licensing costs.

### Tier 3: Point Tools (High Overhead)

Cobbling together Amass + Nuclei + nmap per client — works, but doesn't scale. Most MSSPs start here and move to a platform after client #5.

---

## Workflow Recommendation

```
1. ONBOARD CLIENT
   └─ Create project in HailBytes ASM (or reNgine)
   └─ Add seed domains/IPs
   └─ Configure scan engine (light daily / full weekly)

2. CONTINUOUS MONITORING
   └─ Daily: subdomain + port change detection
   └─ Weekly: full vuln scan pass
   └─ Alert on: new subdomains, new open ports, new critical/high findings

3. MONTHLY CLIENT REPORT
   └─ Export compliance evidence report (SOC 2 / PCI DSS / HIPAA as applicable)
   └─ Review trending (findings up/down vs last month)
   └─ Deliver findings summary to client stakeholders

4. QUARTERLY ASM REVIEW
   └─ Full scope revalidation
   └─ Update seed domains (acquisitions, new product lines)
   └─ Adjust scan engine configuration
```

---

## Tool Comparison for MSSP Use

| Requirement | HailBytes ASM | reNgine OSS | Amass+Nuclei DIY | Censys ASM |
|-------------|:---:|:---:|:---:|:---:|
| Multi-tenant | ✅ | ✅ | ❌ | ✅ |
| Managed (no DevOps) | ✅ | ❌ | ❌ | ✅ |
| Compliance reports | ✅ (10 frameworks) | ❌ | ❌ | ~ |
| Data sovereignty | ✅ (your cloud) | ✅ | ✅ | ❌ |
| AWS/Azure Marketplace | ✅ | ❌ | ❌ | ❌ |
| Price model | Marketplace hourly | Free (infra cost) | Free (infra cost) | Enterprise contract |

---

> **Want this delivered managed in your AWS/Azure?**  
> [HailBytes ASM](https://hailbytes.com/asm) deploys in minutes from the AWS or Azure Marketplace. Your account, your data, zero vendor lock-in. [Deploy now →](https://hailbytes.com/asm)
