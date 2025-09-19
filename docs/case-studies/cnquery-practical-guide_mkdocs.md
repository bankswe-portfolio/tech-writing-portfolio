
# Getting Started with cnquery: A Practical Guide

!!! note "Memo on Writing Sample: cnquery Practical Guide"
    This is *not* official Mondoo documentation.

    This guide is a demonstration piece created to showcase my technical writing style. 
    I selected `cnquery`, an open-source tool from Mondoo, because it is publicly available, technically rich, and well suited to illustrating how I approach developer-facing documentation.

    I started from Mondoo’s [official cnquery documentation](https://mondoo.com/docs/cnquery/) and reworked the material into a **Practical Guide**. 
    My focus was not only on clear, step-by-step instructions, but also on adding the context that helps readers understand _what_ to do, _how_ to do it, and most importantly, _why_ it matters. Along the way I emphasized:

    - **Scenario-based workflows** (for example, checking certificate expiry to prevent downtime)
    - **Explanatory bridges** that connect technical steps to developer and security outcomes
    - **Consistent structure and readability** with clear headings, code examples, and outputs
    - **Forward-looking context** showing how standalone use connects to broader security practices

    This guide reflects how I like to approach technical content:

    - Bringing **clarity and depth** to material that can otherwise feel reference-heavy
    - Creating resources that support **both hands-on adoption and higher-level understanding**
    - Structuring content so it’s approachable for newcomers while still valuable for experienced users
    - Thinking “**docs, but beyond docs**” — content that educates, reassures, and helps readers see the bigger picture

# Getting Started with cnquery: A Guided Introduction

**What if your systems could answer your questions directly?**  

Forget juggling scripts or scrolling through endless logs. 
cnquery lets you _ask your infrastructure plain questions_ — and get clear answers, instantly.
It’s part of Mondoo’s mission to make security **actionable, approachable, and trustworthy**.

!!! info "Who this is for"
    New to Mondoo or cnquery. 
    Comfortable with a terminal. Want fast, confident answers without reading a full reference.


**In 10 minutes you’ll:**

- Install cnquery
- Run 3 practical queries (OS, TLS expiry, privileged users)
- Know when to use **cnquery** vs **cnspec**
- See how this scales into the Mondoo Platform

## 1) What is cnquery?

At its core, **cnquery** is an open source, cloud-native command-line tool powered by **[MQL (Mondoo Query Language)](https://mondoo.com/docs/mql/home/)**. 
It integrates with hundreds of resources so you can ask direct questions about cloud, OS, SaaS, containers, and more. 
When you run a query, you point cnquery at a **target**. 
Targets can be your **local machine**, a **remote host** over SSH/WinRM, a **website** for TLS checks, a **cloud account**, a **container**, and more. 


!!! info "Why this matters"
    Most of us cobble together scripts, grep, and half-remembered commands when problems hit.
    cnquery gives you one consistent way to interrogate your systems — without guesswork.

## 2) Install cnquery

Installation scripts come directly from Mondoo’s distribution. 
In most environments they can be run as-is; for stricter environments see [Provider Management](https://mondoo.com/docs/cnquery/providers/).

**Linux & macOS (curl script):**

```bash
bash -c "$(curl -sSL https://install.mondoo.com/sh)"
```

**Windows (PowerShell):**

```powershell
Set-ExecutionPolicy Unrestricted -Scope Process -Force
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072
iex ((New-Object System.Net.WebClient).DownloadString('https://install.mondoo.com/ps1/cnquery'))
Install-Mondoo -Product cnquery
```

**Verify installation:**

```bash
cnquery version
```

**Expected output:**

```text
cnquery vX.Y.Z #e.g. v8.3.0
```

## 3) Your first queries

You can run one-off queries or use the interactive shell. 
One-off mode is perfect for quick checks you might script into automation, while the interactive shell is best for exploring resources and learning the language.

In these examples we use the **local** target (your current machine).  
Other common targets include `ssh user@host`, `host mondoo.com`, `docker`, `k8s`, and cloud providers like `aws`.

!!! info "Common Targets"
    - `local` → your current machine
    - `ssh user@host` → remote Linux/Windows hosts
    - `host <domain>` → websites (for TLS checks)
    - `docker`, `k8s` → containers and clusters
    - `aws`, `gcp`, `azure` → cloud accounts

    See full list in [Supported Query Targets](https://mondoo.com/docs/cnquery/cnquery-supported/).

**Option A — one-off:**

```bash
cnquery run local -c "os.name"
```

**Option B — shell (recommended for exploring):**

```bash
cnquery shell local
help os
```

Then run queries like `os.name`.

!!! info "Why this matters"
    cnquery gives you two ways to work: fast one-off commands that you can drop into scripts, or a dedicated shell for exploration. 
    This flexibility means you can start small and scale up as your needs grow, without changing tools.

### Example 1 — “What OS am I running?”

```bash
cnquery run local -c "os.name"
```

**Output (example):**

```
Ubuntu
```

`os.name` is provided by the OS pack.

!!! info "Why this matters"
    Sometimes the simplest question is the most important. 
    Whether you’re jumping between development, staging, and production machines or auditing servers you haven’t touched in months, this query gives you a consistent way to confirm exactly what system you’re on. 
    No need to recall which platform uses `uname` or `lsb_release` — cnquery provides one universal approach.

### Example 2 — “Are my TLS certs about to expire?”

Check a public host’s certificates (30-day horizon):

```bash
cnquery shell host mondoo.com
tls.certificates.where(notAfter - time.now < 30 * time.day) { subject.dn issuer.dn notAfter }
```

* `host mondoo.com` targets a website (SSL/TLS).  
* `notAfter` is the certificate expiry field; we compare it with `time.now`.

!!! info "Why this matters"
    Few issues cause more disruption than an expired TLS certificate. 
    Customers see a browser warning, trust drops, and your team is forced into emergency response. 
    This query helps you stay ahead by flagging certificates that are close to expiring, giving you time to renew.

### Example 3 — “Who has sudo access?”

On many Linux distros, privileged users belong to the `sudo` group:

```bash
cnquery run local -c 'group("sudo") { members { name } }'
```

This directly queries the `group` resource, then lists its `members`. Swap `sudo → wheel` (RHEL/Fedora) or `Administrators` (Windows).

!!! info "Why this matters"
    Privilege management is a foundation of security. 
    A single unexpected user with administrator rights can open the door to major risk. 
    This query gives you immediate visibility into who holds elevated access, so you can validate against your intended policy without manual parsing.

## 4) Real-world scenario: Responding to a CVE

A CVE affecting `openssl` just dropped. Find impacted hosts fast:

```bash
cnquery run local -c "packages.where(name == 'openssl') { name version }"
```

`packages` is the list of OS packages. Each `package` contains fields like `name` and `version`.

!!! info "Why this matters"
    When a new vulnerability is announced, speed matters. 
    You need to know immediately which of your systems are running affected versions. 
    cnquery lets you search installed packages in seconds, giving you clear visibility and the confidence to prioritize patching quickly — without assembling ad-hoc scripts under pressure.

## 5) Where cnquery fits with the Mondoo Platform

By itself, cnquery gives you instant answers. 
But its real power is as a **springboard into automation**:

* Feed results into cnspec for repeatable compliance checks  
* Pipe data into the **Mondoo Platform** to visualize risks across fleets  
* Turn one-off discoveries (like that expiring cert) into **policies that prevent recurrence**

!!! info "Why this matters"
    cnquery is more than a standalone tool — it’s the entry point into Mondoo’s larger ecosystem. The same queries you run today can evolve into policies, dashboards, and automated workflows tomorrow. You gain immediate visibility while building toward scalable, repeatable security practices.

## 6) FAQ

**When should I use `cnquery` vs `cnspec`?**

Use **cnquery** to *ask questions and explore* with ad‑hoc MQL. 
Use **cnspec** when you want *repeatable policy checks* (benchmarks, remediations, CI/CD gates). 
See examples throughout the cnspec docs

**Do I need to specify a “target”?**

Yes. 
Common ones are `local`, `ssh user@host`, `host <domain>`, cloud providers like `aws`, and many more—see the Supported Query Targets page for examples. 
See the full list in [Supported Query Targets](https://mondoo.com/docs/cnquery/cnquery-supported/).

**Is cnquery safe in production?**

cnquery queries configuration/state; it doesn’t alter your workloads. 
It may write provider plugins unless you disable auto‑update; for strict read‑only environments, **pre‑install providers** and **turn off provider auto‑update**.

## 7) Where to go next

* Learn **[MQL basics](https://mondoo.com/docs/mql/home/)** and **[write effective MQL](https://mondoo.com/docs/mql/mql.write/)**.
* Explore **[Query Your Infrastructure](https://mondoo.com/docs/cnquery/cnquery-query/)** and the **[MQL Resource Reference](https://mondoo.com/docs/mql/resources/)**.
* When you’re ready for policy‑as‑code and continuous assessment, move to **cnspec** and the Mondoo Platform.
