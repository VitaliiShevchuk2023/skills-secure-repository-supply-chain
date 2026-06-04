# Secure your Repository&#39;s Supply Chain

<img src="https://octodex.github.com/images/Professortocat_v2.png" align="right" height="200px" />

Hey VitaliiShevchuk2023!

Mona here. I'm done preparing your exercise. Hope you enjoy! 💚

Remember, it's self-paced so feel free to take a break! ☕️

[![](https://img.shields.io/badge/Go%20to%20Exercise-%E2%86%92-1f883d?style=for-the-badge&logo=github&labelColor=197935)](https://github.com/VitaliiShevchuk2023/skills-secure-repository-supply-chain/issues/1)

---

&copy; 2025 GitHub &bull; [Code of Conduct](https://www.contributor-covenant.org/version/2/1/code_of_conduct/code_of_conduct.md) &bull; [MIT License](https://gh.io/mit)


# 🔐 Secure Repository Supply Chain — GitHub Best Practices

> **Module:** Maintain a secure repository by using GitHub best practices  
> **Platform:** GitHub / Microsoft Learn  
> **Level:** Beginner → Intermediate

---

## 📋 Table of Contents

- [Theory](#-theory)
  - [Secure Development Strategy](#secure-development-strategy)
  - [Security Tab Features](#security-tab-features)
  - [Key Security Tools](#key-security-tools)
  - [Automated Security](#automated-security)
- [Hands-on Practice](#️-hands-on-practice)
  - [Prerequisites](#prerequisites)
  - [Task 1: Dependency Graph](#task-1-dependency-graph)
  - [Task 2: Dependabot Alerts](#task-2-dependabot-alerts)
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

**Goal:** View and understand the repository's dependencies

**Steps:**

1. Navigate to your repository
2. Click the **Insights** tab
3. Select **Dependency graph** from the left menu
4. Review the list of dependencies and their transitive dependencies

**Expected result:**
```
Repository → Insights → Dependency graph
├── Dependencies (packages your project depends on)
└── Dependents (packages that depend on your project)
```

**Checklist:**
- [ ] Dependency graph is visible
- [ ] Direct and transitive dependencies are shown

---

### Task 2: Dependabot Alerts

**Goal:** View and understand Dependabot security alerts

**Steps:**

1. Navigate to the **Security** tab of your repository
2. Select **Dependabot alerts** from the left menu
3. Review the list of vulnerabilities
4. Click on an individual alert to view its details

**Alert structure:**
```
Vulnerability name
├── Package: name and version
├── Severity: Critical / High / Medium / Low
├── CVE ID: CVE-XXXX-XXXXX
├── Vulnerability description
└── Recommended fix
```

**Checklist:**
- [ ] Dependabot alerts are enabled
- [ ] At least one alert has been reviewed
- [ ] Severity and recommended fix are understood

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

