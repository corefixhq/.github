# CoreFix

**Find it at runtime. Fix it in code.**

CoreFix is a security scanning platform that runs 10+ open source scanners in parallel, attacks your running web application, deduplicates findings across all tools, AI-prioritizes by real exploitability, and opens pull requests to fix what's actually dangerous. From confirmed exploit to merged fix — one pipeline.

---

### What CoreFix does

**Code scanning** — SAST, secrets, dependencies, IaC, Kubernetes manifests. OpenGrep, Gitleaks, OSV-Scanner, KICS, Kubescape running in parallel. Findings normalized, deduplicated, and enriched.

**Web app scanning** — Real attack payloads against your running app. SQL injection, XSS, SSRF, auth bypass, TLS misconfigs, exposed services. OWASP ZAP, Nuclei, Nmap, testssl.sh, SSLyze, OpenAPI Fuzzer.

**AI enrichment** — Every finding scored by actual exploitability, reachability, and data exposure. Not CVSS alone. Your team sees the 15 findings that matter, not 400 raw alerts.

**Fix PRs** — Code patches generated with full codebase context, opened as pull requests. Review the diff, run your tests, merge.

**Runtime-to-code loop** — A confirmed SQL injection on your staging app traced to `src/auth.js:42`, fixed, and merged. No other tool closes this loop automatically.

---

### Repositories

| Repo | What it is |
|---|---|
| **[cfix](https://github.com/corefixhq/cfix)** | Code scanner Docker image — SAST, secrets, SCA, IaC, K8s. Pull and scan in one command. |
| **[cfix-web](https://github.com/corefixhq/cfix-web)** | Web scanner Docker image — DAST, CVEs, port scanning, SSL/TLS, API fuzzing. |
| **[security-tools-mcp](https://github.com/corefixhq/security-tools-mcp)** | Open source MCP server wrapping 50+ security CLI tools for AI agents. Raw output, community-driven. |
| **[cfix-skills](https://github.com/corefixhq/cfix-skills)** | Open source code review skills library for Claude Code, Cursor, and Copilot. Auto-detected by language and framework. |
| **[docs](https://github.com/corefixhq/docs)** | Documentation source for [docs.corefix.dev](https://docs.corefix.dev). |

---

### How it works

```
Connect repo + URL
       │
       ▼
  10+ scanners run in parallel
  SAST · Secrets · SCA · IaC · K8s · DAST · CVEs · SSL/TLS
       │
       ▼
  Normalize → Deduplicate → AI Prioritize
       │
       ▼
  Trace runtime findings → source code
       │
       ▼
  Generate fix → Open PR → Merge
```

Triggers automatically on every push, PR, and release via the GitHub App. Or run locally with Docker — your code never leaves your environment.

---

### Quick start

**Code scanning:**

```bash
docker pull corefixhq/cfix
docker run --rm \
  -e ORG_ID=<your-org-id> \
  -e X_CFIX_API_KEY=<your-api-key> \
  -v $(pwd):/code \
  corefixhq/cfix
```

**Web scanning:**

```bash
docker pull corefixhq/cfix-web
docker run --rm \
  -e ORG_ID=<your-org-id> \
  -e X_CFIX_API_KEY=<your-api-key> \
  corefixhq/cfix-web \
  --target https://your-app.com
```

First results in under 4 minutes.

---

### Scanners integrated

**Code security**

| Scanner | Category |
|---|---|
| OpenGrep | SAST — 30+ languages |
| Gitleaks | Secrets in code and git history |
| OSV-Scanner | Dependency CVEs with reachability |
| KICS | Terraform, Docker, Helm, CloudFormation |
| Kubescape | Kubernetes RBAC, pod security, CIS benchmarks |

**Web application security**

| Scanner | Category |
|---|---|
| OWASP ZAP | DAST — OWASP Top 10 |
| Nuclei | 8,000+ CVE templates |
| Nmap | Port scanning, service discovery |
| testssl.sh | TLS/SSL protocol analysis |
| SSLyze | Certificate chain, key strength |
| OpenAPI Fuzzer | API endpoint fuzzing |

---

### What's coming

- **Auto-fix PRs** — code security findings and runtime-to-code fixes
- **Playground** — browser-based pentesting for developers, AI chat-driven, zero Burp Suite setup
- **Labs** — launch DVWA, Juice Shop, WebGoat, VAmPI as sandboxes to test CoreFix
- **Package health scores** — security health reports and embeddable README badges for open source projects
- **Shadow API detection** — HAR vs OpenAPI spec vs source code route extraction for undocumented endpoint discovery
- **Secret rotation** — exposed credentials automatically rotated via AWS Secrets Manager, GitHub Secrets, Cloudflare, HashiCorp Vault
- **WAF enforcement** — temporary Cloudflare/AWS WAF rules deployed alongside code fixes for immediate protection
- **Cloud drift detection** — IaC vs actual cloud resources, Prowler integration, Terraform fix PRs
- **LLM agent security** — prompt injection, jailbreak, tool-call authorization testing for AI agents
- **OSRP** — Open Secret Rotation Protocol, a proposed standard for universal cross-provider secret revocation
- **`.patcher`** — surgical CVE patches for current dependency versions without breaking upgrades

Full roadmap: [corefix.dev/roadmap](https://corefix.dev/roadmap)

---

### Pricing

**Free for open source** — all scanners, AI enrichment, unlimited scans. No credit card.

**Pay as you go** — $0.03/min runtime + LLM usage. No seats, no monthly fees. Credits never expire. BYOK supported.

[corefix.dev/pricing](https://corefix.dev/pricing)

---

### Open source acknowledgements

CoreFix is built on top of world-class open source security tools. We are grateful to the maintainers of [OpenGrep](https://github.com/opengrep/opengrep), [Gitleaks](https://github.com/gitleaks/gitleaks), [OSV-Scanner](https://github.com/google/osv-scanner), [KICS](https://github.com/Checkmarx/kics), [Kubescape](https://github.com/kubescape/kubescape), [OWASP ZAP](https://github.com/zaproxy/zaproxy), [Nuclei](https://github.com/projectdiscovery/nuclei), [Nmap](https://nmap.org/), [testssl.sh](https://github.com/drwetter/testssl.sh), and [SSLyze](https://github.com/nabla-c0d3/sslyze).

---

### Links

| | |
|---|---|
| **Website** | [corefix.dev](https://corefix.dev) |
| **App** | [app.corefix.dev](https://app.corefix.dev) |
| **Docs** | [docs.corefix.dev](https://docs.corefix.dev) |
| **Docker Hub** | [hub.docker.com/u/corefixhq](https://hub.docker.com/u/corefixhq) |
| **GHCR** | [github.com/orgs/corefixhq/packages](https://github.com/orgs/corefixhq/packages) |
| **Contact** | hello@corefix.dev |

---

*Built with ❤️ in Bangalore, India — for developers everywhere.*
