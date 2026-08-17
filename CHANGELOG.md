# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2024-01-01

### Added

#### Web 安全 (Web Security) Skills
- **OWASP Top 10** (`skills/Web安全/owasp-top10.md`) — Comprehensive assessment guide for the OWASP Top 10 web application security risks, covering all 10 categories with step-by-step testing procedures.
- **API Security** (`skills/Web安全/api-security.md`) — Best practices for securing REST, GraphQL, and gRPC APIs, including authentication testing, injection attacks, and rate limiting.
- **Authentication Security** (`skills/Web安全/authentication-security.md`) — Complete guide for assessing authentication and authorization mechanisms, covering password security, session management, JWT/OAuth, and MFA.

#### 代码审计 (Code Audit) Skills
- **Static Analysis** (`skills/代码审计/static-analysis.md`) — Guide for leveraging SAST tools (Semgrep, CodeQL, SonarQube, Bandit) in CI/CD pipelines with custom rule writing.
- **Dependency Audit** (`skills/代码审计/dependency-audit.md`) — Systematic approach to identifying and remediating known vulnerabilities in third-party dependencies, including SBOM generation and supply chain security.
- **Secure Code Review** (`skills/代码审计/secure-code-review.md`) — Comprehensive manual code review checklist covering input validation, authentication, authorization, cryptography, error handling, and API security.

#### 渗透测试 (Penetration Testing) Skills
- **Reconnaissance** (`skills/渗透测试/reconnaissance.md`) — Structured approach to passive and active reconnaissance, covering DNS enumeration, OSINT, Google dorking, Shodan, and attack surface compilation.
- **Web Application Testing** (`skills/渗透测试/web-app-testing.md`) — Complete web application penetration testing methodology following OWASP and PTES standards, covering injection, authentication, access control, and client-side testing.
- **Report Writing** (`skills/渗透测试/report-writing.md`) — Professional penetration test report writing guide with templates for executive summaries, detailed findings, remediation roadmaps, and quality checklists.

#### 安全工具 (Security Tools) Skills
- **Burp Suite** (`skills/安全工具/burp-suite.md`) — Mastery guide for Burp Suite covering proxy setup, Repeater, Intruder fuzzing, Autorize for authorization testing, Collaborator for out-of-band attacks, and extension development.
- **Nmap Scanning** (`skills/安全工具/nmap-scanning.md`) — Comprehensive Nmap guide covering host discovery, port scanning, service enumeration, NSE scripting, firewall evasion, and automated assessment scripts.
- **Security Automation** (`skills/安全工具/security-automation.md`) — Guide for building automated security testing pipelines with Python and Bash, including reconnaissance automation, web vulnerability scanning, CI/CD integration, and compliance checking.

#### Community Files
- `README.md` — Bilingual (EN/CN) project overview with skills table, quick start guide, project structure, and links to related awesome projects.
- `LICENSE` — MIT License (liangzhengtao).
- `CONTRIBUTING.md` — Contribution guidelines with skill file structure template and style guide.
- `SECURITY.md` — Responsible disclosure policy and security best practices.
- `CODE_OF_CONDUCT.md` — Contributor Covenant Code of Conduct with ethical use guidelines for security knowledge.
- `CHANGELOG.md` — This file.
- `.gitignore` — Git ignore rules for OS files, IDE files, dependencies, secrets, and scan output.
- `.github/workflows/ci.yml` — GitHub Actions CI pipeline for link checking, markdown linting, and file validation.
- `.github/ISSUE_TEMPLATE/bug_report.md` — Bug report issue template.
- `.github/ISSUE_TEMPLATE/feature_request.md` — Feature request issue template.
- `.github/ISSUE_TEMPLATE/new_skill.md` — New skill proposal issue template.
- `.github/pull_request_template.md` — Pull request template.
