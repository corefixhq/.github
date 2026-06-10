# CoreFix

**Find it at runtime. Fix it in code.**

Hybrid architecture security platform: deterministic scanning pipelines (10+ battle-tested open source scanners) + LLM enrichment layer for AI prioritization, false positive reduction, and auto-fix PR generation. Best-in-class scanners do the detection. LLMs do the thinking. Your team does the merging.

CoreFix runs OpenGrep, Gitleaks, OSV-Scanner, KICS, Kubescape, OWASP ZAP, Nuclei, Nmap, testssl.sh, and SSLyze in parallel — then normalizes, deduplicates across all tools, AI-ranks by real exploitability (not just CVSS), and opens pull requests with verified patches. Code scanning and web app attack testing in one pipeline. From confirmed runtime exploit to merged fix.

---

### What CoreFix does

**Code scanning** — SAST, secrets, dependencies, IaC, Kubernetes manifests. OpenGrep, Gitleaks, OSV-Scanner, KICS, Kubescape running in parallel. Findings normalized, deduplicated, and enriched.

**Web app scanning** — Real attack payloads against your running app. SQL injection, XSS, SSRF, auth bypass, TLS misconfigs, exposed services. OWASP ZAP, Nuclei, Nmap, testssl.sh, SSLyze, OpenAPI Fuzzer.

**AI enrichment** — Every finding scored by actual exploitability, reachability, and data exposure. Not CVSS alone. Your team sees the 15 findings that matter, not 400 raw alerts.

**Fix PRs** — Code patches generated with full codebase context, opened as pull requests. Review the diff, run your tests, merge.

**Runtime-to-code loop** — A confirmed SQL injection on your staging app traced to `src/auth.js:42`, fixed, and merged. No other tool closes this loop automatically.

---

### How it works

**Deterministic layer** — Open source scanners handle detection. Rule-based, reproducible, zero hallucination. OpenGrep runs 3,000+ SAST rules. Gitleaks scans full git history. OSV checks every dependency against the CVE database with reachability analysis. ZAP fires real attack payloads. These produce the same results every time on the same codebase.

**LLM layer** — AI handles everything that needs reasoning. Cross-scanner deduplication (is this OpenGrep finding the same issue ZAP confirmed?), exploitability scoring (is this reachable from a public endpoint?), false positive reduction (does this pattern actually matter in this codebase context?), and fix generation (what's the correct parameterized query for this specific ORM?).

**Why hybrid?** Scanners alone produce 400 noisy alerts. LLMs alone hallucinate vulnerabilities that don't exist. The combination gives you high-recall detection (scanners miss nothing) with high-precision prioritization (LLMs filter the noise).

```
Connect repo + URL
       │
       ▼
  10+ scanners run in parallel                ← Deterministic
  SAST · Secrets · SCA · IaC · K8s · DAST · CVEs · SSL/TLS
       │
       ▼
  Normalize → Deduplicate → AI Prioritize     ← LLM layer
       │
       ▼
  Trace runtime findings → source code        ← Hybrid
       │
       ▼
  Generate fix → Open PR → Merge              ← LLM layer
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
