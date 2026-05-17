# Use Case: Bug Bounty Reconnaissance

> **Profile:** Solo researcher or small team hunting on HackerOne, Bugcrowd, or private programs

---

## The Problem

Bug bounty recon is about **breadth, speed, and automation at scale**. You're competing with hundreds of other researchers on the same scope. The researchers who find the most bugs have automated pipelines that continuously discover and test new assets faster than manual enumeration.

Key requirements:
- Maximum subdomain enumeration coverage
- Fast HTTP probing to filter live hosts
- Automated vulnerability scanning across discovered assets
- Continuous monitoring for new assets added to scope
- Low cost (most researchers aren't paying $50K/year for enterprise ASM)

---

## Recommended Toolchain

### The Standard Pipeline

```
Target Domain
    │
    ├─► Subfinder + Amass (passive enumeration)
    │       │
    │       ▼
    ├─► DNSx (DNS resolution + wildcard filtering)
    │       │
    │       ▼
    ├─► HTTPX (HTTP probing, status codes, tech detection)
    │       │
    │       ▼
    ├─► Nuclei (vulnerability scanning)
    │       │
    │       ▼
    └─► Manual review of high/critical findings
```

### Automated Platform Option

For researchers on large programs (e.g., 100k+ subdomain scopes), [reNgine](https://github.com/yogeshojha/rengine) or [BBOT](https://github.com/blacklanternsecurity/bbot) can replace the bash pipeline with a persistent, scheduled platform.

---

## Tool Recommendations by Budget

| Budget | Recommended Setup |
|--------|------------------|
| **$0/month** | Subfinder + Amass + DNSx + HTTPX + Nuclei (all open source) |
| **$49/month** | Add Shodan API key for better passive coverage |
| **$100–500/month** | Self-hosted reNgine on a VPS (persistent, continuous monitoring) |
| **$500+/month** | [HailBytes ASM](https://hailbytes.com/asm) managed platform — worth it for full-time researchers managing dozens of programs |

---

## Step-by-Step: Fast Recon Setup

### 1. Passive Discovery

```bash
# Install ProjectDiscovery tools
go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
go install -v github.com/owasp-amass/amass/v4/...@master
go install -v github.com/projectdiscovery/httpx/cmd/httpx@latest
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest

# Enumerate
subfinder -d target.com -o subfinder.txt
amass enum -passive -d target.com -o amass.txt
cat subfinder.txt amass.txt | sort -u > all-subs.txt

echo "Found $(wc -l < all-subs.txt) subdomains"
```

### 2. HTTP Probing

```bash
cat all-subs.txt | httpx -silent -status-code -title -tech-detect -o live-hosts.txt
```

### 3. Vulnerability Scanning

```bash
nuclei -update-templates
cat live-hosts.txt | nuclei -severity critical,high -o nuclei-results.txt
```

### 4. Continuous Monitoring (reNgine)

Self-host reNgine to run this pipeline automatically on a schedule and alert you on new subdomains or findings:

```bash
git clone https://github.com/yogeshojha/rengine
cd rengine && cp .env.sample .env
# Edit .env with your API keys
docker-compose up -d
```

---

## What Researchers Miss Without Automation

| Asset Type | Manual Miss Rate | Automated Coverage |
|------------|:---:|:---:|
| New subdomains added mid-program | High | ✅ Continuous monitoring |
| Newly deployed endpoints | High | ✅ Scheduled scans |
| CVEs in discovered tech stacks | Medium | ✅ Nuclei templates updated daily |
| Cloud storage (S3, Azure Blobs) | High | ✅ BBOT cloud modules |

---

## Bug Bounty vs. ASM: When to Upgrade

You've outgrown bash scripts when:
- You're managing 5+ programs simultaneously
- You're missing new assets added between your manual scans
- You want to track findings trends over time
- You want to share recon with team members

At that point, [reNgine](../tools/rengine.md) (self-hosted) or [HailBytes ASM](https://hailbytes.com/asm) (managed) becomes cost-effective.

---

> **Want this delivered managed in your AWS/Azure?**  
> [HailBytes ASM](https://hailbytes.com/asm) gives you enterprise ASM infrastructure without the infrastructure management. [Learn more →](https://hailbytes.com/asm)
