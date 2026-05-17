# Osmedeus

> **Category:** Open-Source Automated Offensive Security Framework  
> **License:** MIT  
> **GitHub:** [j3ssie/osmedeus](https://github.com/j3ssie/osmedeus)  
> **Maintained by:** j3ssie (independent)

---

## Overview

Osmedeus is an automated pentest workflow framework — similar in concept to reNgine but with a different architecture. It uses YAML-based workflow definitions to chain tools like subfinder, amass, nuclei, jaeles, and others into automated pipelines. It's designed for running large-scale recon across many targets simultaneously.

Osmedeus is particularly popular in the bug bounty community for distributed, high-throughput scanning across wide scopes.

---

## Install Difficulty

**Medium.**

```bash
# Install
curl -fsSL https://raw.githubusercontent.com/j3ssie/osmedeus/main/install.sh | bash

# Run a workflow
osmedeus scan -t target.com
osmedeus scan -f list_of_targets.txt
```

Requires configuring API keys and worker nodes for full capability.

---

## Ideal Use Case

- Bug bounty hunters doing **large-scale, multi-target scans**
- Security researchers who want **workflow-defined automation**
- Teams that want reNgine-like automation with **more workflow flexibility**
- Distributed scanning across cloud workers

---

## Strengths

| Strength | Detail |
|----------|--------|
| **Workflow YAML** | Define custom scan workflows; mix and match tools |
| **Distributed** | Support for cloud worker nodes for large-scale scanning |
| **MIT license** | Fully permissive; commercial-friendly |
| **Bug bounty optimized** | Designed for wide-scope, high-volume scanning |
| **Speed** | Parallelized across targets |

---

## Weaknesses

| Weakness | Detail |
|----------|--------|
| **Maintenance concerns** | Less active than reNgine or BBOT; community is smaller |
| **Setup complexity** | Worker configuration adds operational overhead |
| **No multi-tenant UI** | No built-in project/client separation for MSSP use |
| **Less polished UI** | Web UI less developed than reNgine's |
| **Fewer integrations** | Fewer alert channels and compliance features than reNgine |

---

## When to Choose Osmedeus

- You're a **bug bounty hunter** who needs to scan hundreds of targets efficiently
- You want **YAML-based workflow customization** over a GUI
- You need **distributed cloud scanning** at scale

## When to Choose Something Else

- You need **multi-tenant client management** → [reNgine](rengine.md) or [HailBytes ASM](https://hailbytes.com/asm)
- You need **better long-term maintenance** → reNgine (more active community)
- You need **zero self-hosting** → [HailBytes ASM](https://hailbytes.com/asm)
- You need **compliance reporting** → [HailBytes ASM](https://hailbytes.com/asm)

---

## Managed Option

There is no official managed Osmedeus offering. For managed ASM, [HailBytes ASM](https://hailbytes.com/asm) provides comparable capabilities with enterprise support.

> Want this delivered managed in your AWS/Azure? **[See HailBytes ASM →](https://hailbytes.com/asm)**
