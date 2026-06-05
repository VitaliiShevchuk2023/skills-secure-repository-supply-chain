
# 🔐 Secure Repository Supply Chain — GitHub Best Practices

> **Module:** Maintain a secure repository by using GitHub best practices  
> **Platform:** GitHub / Microsoft Learn  
> **Level:** Beginner → Intermediate

> 📘 **Based on:** [Learn how Microsoft supports secure software development as part of a cybersecurity solution](https://learn.microsoft.com/en-us/training/paths/secure-software-development-for-cybersecurity/)  
> This README is derived from the Microsoft Learn learning path above, which covers secure software development practices, GitHub repository security, and the Azure Well-Architected Framework Security pillar as part of a cybersecurity solution.

---

## 📋 Table of Contents

- [Theory](#-theory)
  - [Secure Development Strategy](#secure-development-strategy)
  - [Security Tab Features](#security-tab-features)
  - [Key Security Tools](#key-security-tools)
  - [Automated Security](#automated-security)
  - [Azure Well-Architected Framework — Security Pillar](#azure-well-architected-framework--security-pillar)
    - [Principle 1: Plan Your Security Readiness](#principle-1-plan-your-security-readiness)
    - [Principle 2: Design to Protect Confidentiality](#principle-2-design-to-protect-confidentiality)
    - [Principle 3: Design to Protect Integrity](#principle-3-design-to-protect-integrity)
    - [Principle 4: Design to Protect Availability](#principle-4-design-to-protect-availability)
    - [Principle 5: Sustain and Evolve Your Security Posture](#principle-5-sustain-and-evolve-your-security-posture)
- [Hands-on Practice](#️-hands-on-practice)
  - [Prerequisites](#prerequisites)
  - [Task 1: Dependency Graph](#task-1-dependency-graph)
    - [Activity 1.1: Verify Dependency Graph is enabled](#activity-11--verify-that-dependency-graph-is-enabled)
    - [Activity 1.2: Add a new dependency](#activity-12--add-a-new-dependency-and-view-your-dependency-graph)
  - [Task 2: Dependabot Alerts](#task-2-enable-and-view-dependabot-alerts)
    - [Activity 2.1: View advisories in GitHub Advisory Database](#activity-21--view-security-advisories-in-the-github-advisory-database)
    - [Activity 2.2: Enable Dependabot alerts](#activity-22--enable-dependabot-alerts)
    - [Activity 2.3: Create a security update PR](#activity-23--create-a-pull-request-based-on-a-dependabot-alert)
  - [Task 3: Dependabot Security Updates](#task-3-dependabot-security-updates)
  - [Task 4: Dependabot Version Updates](#task-4-dependabot-version-updates)
- [Knowledge Check](#-knowledge-check)
- [Resources](#-resources)

---

## 📚 Theory

### Secure Development Strategy

Application security is critical. Planning a secure development strategy involves three key aspects:

| Aspect | Description |
|--------|-------------|
| **Knowledge gap** | Cybersecurity is a constantly evolving discipline. An ongoing education and training program is essential |
| **Secure code** | Code must correctly and securely implement features designed with security in mind |
| **Regulatory compliance** | Code must comply with required rules and regulations — both during development and after deployment |

#### The "Shift Left" Principle

```
❌ Traditional approach:
Development → Testing → Deployment → [Security review]

✅ Shift Left approach:
[Security] → Development → [Security] → Testing → [Security] → Deployment
```

> **Shift Left** means moving security checks earlier in the development lifecycle. Catching issues earlier actually reduces the overall time it takes to develop quality software.

---

### Security Tab Features

Navigate to **repository → Security** to access:

| Feature | Purpose |
|---------|---------|
| **Security policies** | `SECURITY.md` file with instructions on reporting vulnerabilities |
| **Dependabot alerts** | Notifications when vulnerable dependencies or malware are detected |
| **Security advisories** | Privately discuss, fix, and publish information about vulnerabilities |
| **Code scanning** | Find, triage, and fix vulnerabilities and errors in your code |
| **Secret scanning** | Detect tokens, credentials, and secrets committed to the repo |

---

### Key Security Tools

#### 1. SECURITY.md

The `SECURITY.md` file in the root of a repository explains how to responsibly disclose security vulnerabilities.

```markdown
## Supported Versions

| Version | Support |
|---------|---------|
| 2.x     | ✅ |
| 1.x     | ❌ |

## Reporting a Vulnerability

Please send reports to security@example.com
Expect a response within 48 hours.
```

#### 2. .gitignore

The `.gitignore` file prevents sensitive data from accidentally being committed to the repository:

```gitignore
# Secrets and configuration
.env
.secrets/
config/local.yml
*.key
*.pem

# Build artifacts
[Dd]ebug/
[Rr]elease/
*.suo

# Dependencies
node_modules/
__pycache__/
```

> ⚠️ **Important:** You should assume that any data committed to GitHub has been compromised. Simply overwriting a commit is not enough to ensure the data won't be accessible in the future.

#### 3. CODEOWNERS

The `CODEOWNERS` file assigns code owners for automatic review requirements:

```
# JS files — reviewed by the js team
*.js    @js-team

# Security components — reviewed by security team
/security/    @security-team

# Infrastructure — reviewed by devops team
/infra/    @devops-team
```

#### 4. Branch Protection Rules

Branch protection rules enforce:
- ✅ Required reviews before merging
- ✅ Passing status checks (CI/CD)
- ✅ Code Owners review enforcement
- ✅ Dismissal of stale approvals on new commits

---

### Automated Security

#### Dependency Graph

GitHub automatically scans common package manifests:

```
package.json          → Node.js / npm
requirements.txt      → Python / pip
Gemfile               → Ruby / Bundler
pom.xml               → Java / Maven
build.gradle          → Java / Gradle
composer.json         → PHP / Composer
```

#### Dependabot Workflow

```
Dependency graph
       ↓
Dependabot scans
       ↓
Cross-references with GitHub Advisory Database
       ↓
Vulnerability found?
  ├── NO  → Continues monitoring
  └── YES → Generates Dependabot Alert
              ↓
         Automatically creates a Pull Request with a fix
```

**Types of Dependabot updates:**
- **Security updates** — fix known vulnerabilities
- **Version updates** — keep dependencies up to date

#### Code Scanning (CodeQL)

CodeQL treats code as data and allows you to:
- Run custom queries against your source code
- Use community-maintained open-source queries
- Integrate directly into your CI/CD pipeline

**Supported languages:**
`C/C++` `C#` `Go` `Java/Kotlin` `JavaScript/TypeScript` `Python` `Ruby` `Swift`

#### Secret Scanning

When a secret is detected:
1. GitHub notifies the service provider that issued the secret
2. The provider validates the credential
3. A decision is made: revoke / issue a new secret / contact you directly

> **Push Protection** is enabled by default on public repositories — blocks commits containing secrets before they are pushed.

---

## 🏛️ Azure Well-Architected Framework — Security Pillar

A Well-Architected workload must be built with a **Zero Trust** approach and follow the **CIA Triad**: Confidentiality, Integrity, and Availability. Even small security problems can cause major damage to brand and reputation.

**Key questions to assess your security strategy:**
- Do your defenses make it hard and costly for attackers to compromise your system?
- Are your security measures effective in limiting the impact of an incident?
- Do you understand how valuable your system is to an attacker?
- Can the workload quickly detect, respond to, and recover from disruptions?

---

### Principle 1: Plan Your Security Readiness

> **Goal:** Make security a part of your design and operations with minimal hassle.

#### Optimize Security Through Segmentation

Use segmentation to plan security boundaries in the workload environment, processes, and team structure to isolate access and function.

| Concept | Description |
|---------|-------------|
| **Need-to-know access** | Grant access only to roles that truly require it |
| **Just-in-time (JIT)** | Provide temporary, time-limited access instead of standing permissions |
| **Network isolation** | Separate components that handle personal data from those that don't |

**Real-world example — Contoso Supermarket:**

> A QA intern with broad security group membership had their account compromised in a social engineering attack. Because of over-provisioned access, the entire application platform deployment was compromised.
>
> **Outcome:** The team redesigned access controls to be need-to-know and JIT, isolated networks by data sensitivity, and contained the blast radius of future compromises.

#### Respond to Incidents Efficiently

Build a security incident response plan using industry frameworks that define the standard operating procedure for:

```
Preparedness → Detection → Containment → Mitigation → Post-incident review
```

#### Codify Secure Operations and Development Practices

Set clear team-level security standards for your workload's life cycle:
- How to write code securely
- How to approve and release changes
- How to handle and classify data
- Which regulations apply to your data types

**Knowledge check answers:**
- Segmentation → isolates access based on **principle of least privilege**
- Fast detection and response → requires a **security incident response plan**
- Secure development practices → ensure code is developed in a **consistent, standard manner** ✅

---

### Principle 2: Design to Protect Confidentiality

> **Goal:** Keep privacy, regulatory, application, and proprietary information safe by limiting access and hiding details when needed.

#### Strictly Limit Access

Apply the principle of least privilege:

```
❌ Standing access:  Full access to all customer data at all times
✅ Just-in-time:     Approved, time-limited, logged access on demand
```

Use **Microsoft Entra ID + RBAC** to enforce:
- Group-based access control
- Approval workflows before granting access
- Automatic access expiration
- Full audit logging of data access

**Real-world example — Contoso Rise Up (SaaS for nonprofits):**

> A disgruntled support employee copied and publicly shared a donor list. Despite ethical access training, standing access made the breach possible.
>
> **Outcome:** RBAC implemented via Microsoft Entra ID. All data access now requires approval, is time-limited, and fully logged. No more standing access to customer data.

#### Identify Confidential Data Through Classification

Label data stores with metadata to indicate type and sensitivity:

| Data Type | Example | Security Level |
|-----------|---------|----------------|
| Internal | Customer list | Medium |
| Customer-owned | Donor lists | High |
| Donor-specific | Mailing addresses | High |
| Non-sensitive | Stock images, templates | Low |

> Reorganize data so that security levels match data sensitivity. Apply **data masking** on key fields so even authorized users only see what they need.

#### Apply Encryption at Every Step of the Data Life Cycle

| State | Protection method |
|-------|------------------|
| **At rest** | Azure Storage Service Encryption |
| **In transit** | HTTPS / TLS |
| **Keys** | Azure Key Vault |

**Real-world example:** A backup accidentally copied to a network share was discovered months later. With proper encryption at rest, the data would have been useless without the decryption key — eliminating the privacy breach risk.

**Knowledge check answers:**
- Access to confidential customer data → **customer service representative** (legitimate business need)
- Data classification → **ongoing process**, not a one-time activity ❌
- Encryption example → **Azure Storage Service Encryption** for storage accounts ✅

---

### Principle 3: Design to Protect Integrity

> **Goal:** Make sure your system stays reliable and does what it's supposed to, without being tampered with or disrupted.

#### Defend Your Supply Chain

Protect your tools, libraries, and build systems from tampering:

```
Build pipeline security checklist:
├── Scan dependencies for CVEs and malware
├── Use anti-malware on build agents (e.g., Windows Defender Application Control)
├── Sign firmware and verify signatures before execution
└── Track software provenance throughout the lifecycle
```

**Real-world example — Contoso Paint Systems (IoT):**

> Open-source tools in firmware and cloud systems were not scanned. Supply chain attacks could have compromised environmental air quality reporting.
>
> **Outcome:** Build processes updated to include CVE and malware scanning. IoT devices upgraded to support certificate-based communication and signed firmware verification.

#### Employ Strong Cryptographic Mechanisms

| Mechanism | Purpose |
|-----------|---------|
| **Encryption** | Protects data from being read if intercepted |
| **Code signing** | Confirms software hasn't been tampered with |
| **Certificates** | Authenticates device and service identity |
| **Digital signatures** | Validates data integrity end-to-end |

> Network segmentation alone is not sufficient — unencrypted communication between IoT devices and control systems is a critical risk even in isolated networks.

#### Optimize the Security of Your Backups

Make backups immutable using **Azure Blob Storage WORM (Write Once, Read Many)**:

```
Backup process with integrity protection:
1. Encrypt the report/backup
2. Store in Azure Blob Storage with WORM setting (immutable)
3. Compute SHA hash of the file
4. Compare hash on restore to verify nothing was altered
```

**Knowledge check answers:**
- Threat scanning → **helps detect vulnerabilities** (not a guarantee) ✅
- Cryptographic controls → **code signing and encryption** ✅
- Immutable backup → **WORM feature in Azure Blob Storage** ✅

---

### Principle 4: Design to Protect Availability

> **Goal:** Use strong security controls to help your system stay up and running, even during a security incident.

#### Enhance Reliability Through Robust Security

Use design patterns that minimize the **blast radius** of an attack:

**Valet Key pattern:**
```
❌ Before: App servers handle all storage requests directly
                → one malicious request can overwhelm all servers

✅ After:  App servers issue scoped, time-limited access tokens
                → malicious requests are contained and isolated
```

Additional controls:
- Input validation and sanitization before data reaches the system
- Rate limiting and request size caps
- Separation of concerns between services

**Real-world example — Contoso Concierge (hotel management):**

> An attacker exploited a bug to serve an oversized fake folio object, exhausting server memory and cascading across all nodes in one region for 4+ hours.
>
> **Outcome:** Valet Key pattern adopted for storage access. Improved input filtering added. Attack surface and blast radius significantly reduced.

#### Proactively Limit Attack Vectors

| Control | What it prevents |
|---------|-----------------|
| **Anti-malware on VMs** | Malware installation and lateral movement |
| **WAF (Web Application Firewall)** | SQL injection, XSS, and other web attacks |
| **Regular patching** | Known CVE exploitation |
| **Vulnerability scanning in CI/CD** | Insecure code reaching production |

#### Secure Your Recovery Strategy

> A recovery environment with relaxed security is itself an attack surface.

Recovery security requirements:
- ✅ Same network and identity protections as production
- ✅ Immutable backup storage (tamper-proof)
- ✅ WAF active during recovery (not only in steady state)
- ✅ Backups scanned for malware before restoration
- ✅ Regular drills to validate recovery procedures

**Knowledge check answers:**
- Contoso's response to overload attack → **design pattern minimizing blast radius** ✅
- Preventative measure for attack vectors → **anti-malware solution** ✅
- Recovery environment security → **must equal production** — False that it can be relaxed ✅

---

### Principle 5: Sustain and Evolve Your Security Posture

> **Goal:** Hackers are always coming up with new methods — your security approach must keep up.

#### Threat Modeling

Use an industry-standard methodology (e.g., STRIDE) to systematically analyze your workload:

```
Threat modeling process:
1. Map all components and data flows
2. Identify potential threats at each point
3. Classify threats by severity and likelihood
4. Prioritize and schedule fixes
5. Validate mitigations in the next cycle
```

**Real-world example — Contoso Rally (Apache Spark analytics):**

> First threat modeling session revealed: insider threat risks in post-Spark data cleanup jobs, and an inactive race team's system still had access to sensitive data.
>
> **Outcome:** Fixes scheduled for next development cycle. Old system decommissioned.

#### Test Controls Yourself

| Test type | Frequency | Purpose |
|-----------|-----------|---------|
| **Vulnerability scanning** | Every deployment | Catch issues before production |
| **Penetration testing** | Quarterly | Validate real-world attack resistance |
| **White-box test** | Annually | Deep internal review with full system knowledge |
| **Anti-malware on dev boxes** | Continuous | Prevent build agent compromise |

#### Get Current and Stay Current

Keep systems patched and tools updated — including components that "just work":

```
Common mistake:
"The Apache Spark jobs work fine — no need to update Python/R packages."

Risk:
Stale packages → known CVEs → unpatched components in production

Fix:
Enforce update and patch schedules for ALL technology in use,
including data processing frameworks and their dependencies.
```

Apply **Security Development Lifecycle (SDL)** reviews periodically to:
- Verify security features are still functioning
- Track asset inventory and their security posture
- Audit provenance, usage, and known weaknesses

**Knowledge check answers:**
- Identifies gaps in security controls → **threat modeling** ✅
- Security testing responsibility → **not the workload team alone** — requires independent experts ✅
- Apache Spark job risk → **not included in the update and patching process** ✅

---

## 🛠️ Hands-on Practice

### Prerequisites

- [ ] A GitHub account
- [ ] Basic knowledge of Git and GitHub
- [ ] Access to a repository with administrator permissions

### Getting Started

Navigate to the exercise template repository and create your own copy:

```
https://github.com/skills/secure-repository-supply-chain
```

1. Click **Use this template** or **Copy Exercise**
2. Select your personal account as the owner
3. Create a **public** repository (private repositories consume Actions minutes)
4. Wait approximately 20 seconds, then refresh the page

---

### Task 1: Dependency Graph

**Goal:** Review existing dependencies and add a new one to observe how the dependency graph updates in real time

> 💡 The dependency graph is a summary of manifest and lock files stored in a repository. It shows all ecosystems and packages the project depends on, as well as repositories that depend on it.

#### Activity 1.1 — Verify that Dependency Graph is enabled

> **Note:** Dependency graph is enabled by default for all new public repositories.

1. Navigate to the **Settings** tab of your repository
2. Click **Advanced Security** in the left sidebar
3. Verify that **Dependency Graph** is set to **Enabled**

#### Activity 1.2 — Add a new dependency and view your dependency graph

1. Navigate to the **Code** tab and open the `code/src/AttendeeSite` folder
2. Open the `package-lock.json` file and click the **Edit** (pencil) icon
3. Locate the `dependencies` map and add the following entry as the **last item** — after the third-to-last closing bracket `}` and before the final two brackets:

```json
,
"follow-redirects": {
  "version": "1.14.1",
  "resolved": "https://registry.npmjs.org/follow-redirects/-/follow-redirects-1.14.1.tgz",
  "integrity": "sha512-HWqDgT7ZEkqRzBvc2s64vSZ/hfOceEol3ac/7tKwzuvEyWx3/4UegXh5oBOIotkGsObyk3xznnSRVADBgWSQVg=="
}
```

> 💡 You can also press the `.` key on any repository page to open the lightweight web editor for editing and committing changes.

4. Commit the change directly to the `main` branch
5. Navigate to the **Insights** tab
6. Select **Dependency graph** from the left sidebar
7. Open the **Dependencies** tab and search for `follow-redirects`
8. Verify the new dependency appears in the graph

**Expected result:**
```
Repository → Insights → Dependency graph → Dependencies
├── ... existing dependencies ...
└── follow-redirects@1.14.1   ← newly added
```

> ⏳ After committing, wait a moment for Mona (the GitHub Actions bot) to check your work and post the next step in the issue comments.

**Checklist:**
- [ ] Dependency graph is enabled in Settings → Advanced Security
- [ ] `follow-redirects` entry added to `package-lock.json`
- [ ] New dependency is visible in the dependency graph
- [ ] GitHub Actions grading workflow completed successfully

---

### Task 2: Enable and View Dependabot Alerts

**Goal:** Understand what Dependabot alerts are, search the GitHub Advisory Database for a known vulnerability, enable alerts on your repository, and create a security update pull request.

> 💡 **What are Dependabot alerts?**  
> Dependabot alerts notify you that your code depends on a package that is insecure. They reference the [GitHub Advisory Database](https://github.com/advisories), which contains known security vulnerabilities and malware grouped into two categories: **GitHub reviewed advisories** and **unreviewed advisories**.  
> If your code depends on a vulnerable package, you should upgrade to a secure version as soon as possible. If your code uses malware, replace the package with a secure alternative.

---

#### Activity 2.1 — View security advisories in the GitHub Advisory Database

1. Navigate to the [GitHub Advisory Database](https://github.com/advisories)
2. Type or paste `follow-redirects` into the advisory search box
3. Click on any of the advisories found to see more information
4. Review the details: **packages affected**, **impact**, **patches**, **workarounds**, and **references**

> 📌 You will notice a long list of advisories for `follow-redirects`. This is actually a good sign — it means the dependency is actively maintained and patches are being released. With Dependabot alerts enabled, you would be notified automatically whenever an update is needed.

**Alert detail structure:**
```
Advisory: [CVE-XXXX-XXXXX]
├── Package:      follow-redirects (npm)
├── Severity:     Critical / High / Medium / Low
├── Impact:       Description of the vulnerability
├── Patches:      Safe versions to upgrade to
├── Workarounds:  Manual mitigations (if any)
└── References:   External CVE links and discussions
```

---

#### Activity 2.2 — Enable Dependabot alerts

1. Navigate to the **Settings** tab of your repository
2. In the left sidebar, click **Advanced Security**
3. Toggle **Dependabot alerts** to **Enabled**
4. Wait approximately **60 seconds** for Dependabot to scan your repository
5. Navigate to the **Security** tab
6. Under **Vulnerability alerts** in the sidebar, select **Dependabot**
7. Review the list of Dependabot alerts for the default branch

> ⏳ Dependabot will now flag any insecure dependencies it detects. These alerts show which packages need attention and suggest safe versions to upgrade to.

---

#### Activity 2.3 — Create a pull request based on a Dependabot alert

1. In the list of Dependabot alerts, click **"Prototype Pollution in minimist"** to view details
2. Click the **Create Dependabot security update** button to generate a pull request
   > ⏳ This may take up to **2 minutes** to complete
3. Once the pull request is open, the alert page updates to show a **Review security update** button
4. Click **Review security update** to open the pull request
5. Review the **Conversation** tab and the **Files changed** tab to understand the update
6. Return to the **Conversation** tab and **merge the pull request**

> ⏳ After merging, wait for Mona (the GitHub Actions bot) to check your work and post progress and the next lesson in the issue comments.

**What happens after merging:**
```
Dependabot security update PR merged
         ↓
Vulnerable dependency version → replaced with patched version
         ↓
Dependabot alert → automatically closed
         ↓
Dependency graph → updated to reflect new version
```

**Checklist:**
- [ ] `follow-redirects` searched in the GitHub Advisory Database
- [ ] At least one advisory reviewed (packages, impact, patches)
- [ ] Dependabot alerts enabled in Settings → Advanced Security
- [ ] Dependabot alerts list reviewed in the Security tab
- [ ] "Prototype Pollution in minimist" alert opened
- [ ] Dependabot security update PR created and merged
- [ ] GitHub Actions grading workflow completed successfully

---

### Task 3: Dependabot Security Updates

**Goal:** Enable automatic security updates

**Steps:**

1. Navigate to repository **Settings**
2. Select **Code security and analysis**
3. Locate **Dependabot security updates**
4. Click **Enable**

**What happens after enabling:**
```
Dependabot detects a vulnerability
         ↓
Automatically creates a Pull Request
         ↓
PR includes:
├── Updated dependency version
├── Changelog with fixes
├── Link to CVE advisory
└── Compatibility score: projects successfully updated
         ↓
You review and merge the PR
```

**Checklist:**
- [ ] Dependabot security updates are enabled
- [ ] A PR from Dependabot appeared (if vulnerabilities exist)
- [ ] PR contains enough information to make a merge decision

---

### Task 4: Dependabot Version Updates

**Goal:** Configure automatic dependency maintenance

**Steps:**

1. Create the file `.github/dependabot.yml` in your repository
2. Add the following configuration:

```yaml
# .github/dependabot.yml
version: 2
updates:
  # npm dependency updates
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"
      day: "monday"
      time: "09:00"
      timezone: "Europe/Berlin"
    open-pull-requests-limit: 5
    labels:
      - "dependencies"
      - "automated"

  # GitHub Actions updates
  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "weekly"
    labels:
      - "github-actions"
      - "dependencies"
```

3. Commit the file to your repository
4. Navigate to **Insights → Dependency graph → Dependabot** to verify the status

**Configuration parameters:**

| Parameter | Description | Example |
|-----------|-------------|---------|
| `package-ecosystem` | Package manager | `npm`, `pip`, `maven` |
| `directory` | Location of the manifest | `/`, `/frontend` |
| `interval` | Check frequency | `daily`, `weekly`, `monthly` |
| `open-pull-requests-limit` | Max number of open PRs | `5` |

**Checklist:**
- [ ] `dependabot.yml` created in `.github/`
- [ ] Configuration is valid (no syntax errors)
- [ ] Dependabot displays the configured update schedule

---

## ✅ Knowledge Check

**1.** What is the best way to make sure you're integrating the most secure versions of your project dependencies?

<details>
<summary>Show answer</summary>

**Enable Dependabot for your repository.**

Dependabot automatically monitors vulnerabilities and creates pull requests with updates. Using `latest` in package files is risky — a new version may break compatibility. Manual verification of each dependency is unreliable and does not scale.
</details>

---

**2.** One of your source projects relies on secrets kept in a folder called `.secrets`. Which file best helps prevent that folder from being accidentally committed?

<details>
<summary>Show answer</summary>

**The `.gitignore` file.**

Add `.secrets/` to `.gitignore`. `SECURITY.md` is a security policy document, `CONTRIBUTING.md` contains contributor guidelines — neither of them prevents commits from being made.
</details>

---

**3.** What does secret scanning do?

<details>
<summary>Show answer</summary>

**It looks for known secrets or credentials committed within the repository.**

Secret scanning detects tokens, API keys, and passwords using known patterns. Finding vulnerabilities in code is the job of code scanning / CodeQL — these are different tools with different purposes.
</details>

---

## 📖 Resources

| Resource | Link |
|----------|------|
| GitHub Exercise | [skills/secure-repository-supply-chain](https://github.com/skills/secure-repository-supply-chain) |
| Dependabot alerts | [Documentation](https://docs.github.com/code-security/dependabot/dependabot-alerts/about-dependabot-alerts) |
| Configuring Dependabot | [Documentation](https://docs.github.com/code-security/dependabot/dependabot-security-updates/configuring-dependabot-security-updates) |
| Secret scanning | [Documentation](https://docs.github.com/code-security/secret-scanning/introduction/about-secret-scanning) |
| Code scanning and CodeQL | [Documentation](https://docs.github.com/code-security/code-scanning/introduction-to-code-scanning/about-code-scanning) |
| Adding a security policy | [Documentation](https://docs.github.com/code-security/getting-started/adding-a-security-policy-to-your-repository) |
| Ignoring files | [Documentation](https://docs.github.com/get-started/git-basics/ignoring-files) |
| Removing sensitive data | [Documentation](https://docs.github.com/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository) |

---

## 🏆 Module Completion Criteria

- [ ] Repository dependency graph reviewed
- [ ] Dependabot alerts reviewed and understood
- [ ] Dependabot security updates enabled
- [ ] Dependabot version updates configured via `dependabot.yml`
- [ ] Automatic grading passed in the Actions tab

---

*Module: Maintain a secure repository by using GitHub best practices | Microsoft Learn*

---

> 📘 **Learning path:** [Learn how Microsoft supports secure software development as part of a cybersecurity solution](https://learn.microsoft.com/en-us/training/paths/secure-software-development-for-cybersecurity/) — Microsoft Learn
