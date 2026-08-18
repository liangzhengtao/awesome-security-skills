# OWASP Top 10 Vulnerability Assessment Skill

> Systematically identify, classify, and remediate the OWASP Top 10 web application security risks.

## When to Use

- Conducting a web application security assessment
- Building a security checklist for a new project
- Reviewing an application against industry-standard benchmarks
- Preparing for a compliance audit (PCI-DSS, SOC 2, HIPAA)
- Training developers on the most critical web security risks
- Prioritizing remediation efforts based on risk severity

## Prerequisites

- Basic understanding of HTTP/HTTPS protocols
- Familiarity with at least one web framework (Django, Spring, Express, etc.)
- Access to the target application (authorized testing only)
- A proxy tool such as Burp Suite or OWASP ZAP

## Tools

| Tool | Purpose | License |
|------|---------|---------|
| OWASP ZAP | Automated and manual vulnerability scanning | Apache-2.0 |
| Burp Suite | Intercepting proxy and scanner | Community Free / Pro |
| Nikto | Web server misconfiguration scanner | GPL |
| SQLMap | SQL injection detection and exploitation | GPL |
| Nuclei | Template-based vulnerability scanner | MIT |
| Semgrep | Static analysis for code-level findings | LGPL |

## Step-by-Step Procedure

### Phase 1: Reconnaissance and Scope Definition

1. Define the scope with the application owner — URLs, APIs, environments.
2. Obtain written authorization (Rules of Engagement document).
3. Map the application surface:
   - Spider/crawl all reachable pages.
   - Enumerate API endpoints from Swagger/OpenAPI specs.
   - Identify entry points: forms, headers, cookies, parameters.
4. Record technology fingerprint: framework, server, language, database.

### Phase 2: Assess Each OWASP Category

#### A01 — Broken Access Control

- Test IDOR by substituting resource IDs (`/api/users/1` → `/api/users/2`).
- Verify directory traversal: `../../etc/passwd` in file path parameters.
- Check for missing function-level access control on admin endpoints.
- Test horizontal and vertical privilege escalation.
- Verify CORS policy does not allow arbitrary origins.

#### A02 — Cryptographic Failures

- Check if sensitive data is transmitted over HTTP instead of HTTPS.
- Verify TLS version (must be ≥ 1.2) and cipher suite strength.
- Inspect password hashing algorithm (bcrypt, scrypt, Argon2 — never MD5/SHA1).
- Look for hardcoded secrets, API keys, or tokens in source code.
- Confirm sensitive data is not logged or cached in plaintext.

#### A03 — Injection

- Test all input fields for SQL injection with single quotes, boolean logic, and time-based payloads.
- Check for OS command injection (`; ls`, `| whoami`).
- Test for LDAP injection, XPath injection, and NoSQL injection.
- Verify server-side template injection (SSTI) in template engines.
- Use SQLMap for automated SQLi detection and validation.

#### A04 — Insecure Design

- Review threat models for business logic flaws.
- Test for race conditions in critical workflows (double-spending, coupon reuse).
- Verify anti-automation controls (rate limiting, CAPTCHA).
- Check multi-step processes for step-skipping attacks.
- Assess whether security controls were considered at design time.

#### A05 — Security Misconfiguration

- Check default credentials on admin panels, databases, and frameworks.
- Verify security headers: `Content-Security-Policy`, `X-Frame-Options`, `Strict-Transport-Security`, `X-Content-Type-Options`.
- Look for directory listing, stack traces, and verbose error messages.
- Confirm unnecessary features, ports, and services are disabled.
- Test for HTTP method tampering (TRACE, DELETE, PUT on unintended endpoints).

#### A06 — Vulnerable and Outdated Components

- Enumerate all third-party dependencies and their versions.
- Cross-reference with CVE databases (NVD, GitHub Advisories, Snyk).
- Check for end-of-life frameworks or libraries.
- Verify that dependency lock files are used and up to date.

#### A07 — Identification and Authentication Failures

- Test for credential stuffing and brute force resistance.
- Verify session management: session fixation, timeout, invalidation on logout.
- Check multi-factor authentication implementation.
- Test password reset flow for token predictability and reuse.
- Verify account lockout policies.

#### A08 — Software and Data Integrity Failures

- Check for insecure deserialization (Java, PHP, .NET object injection).
- Verify CI/CD pipeline integrity (signed commits, verified images).
- Test for unsigned or unverified auto-updates.
- Inspect CDN usage for subresource integrity (SRI) tags.

#### A09 — Security Logging and Monitoring Failures

- Verify that authentication events (success, failure, lockout) are logged.
- Check that logs include sufficient detail (timestamp, source IP, user ID).
- Confirm logs are tamper-proof and centralized.
- Test alerting mechanisms for critical security events.
- Verify log retention meets compliance requirements.

#### A10 — Server-Side Request Forgery (SSRF)

- Test URL input parameters for SSRF by supplying internal addresses (`http://127.0.0.1`, `http://169.254.169.254`).
- Check for DNS rebinding susceptibility.
- Verify allowlist-based URL validation.
- Test for blind SSRF using out-of-band detection (Burp Collaborator, interactsh).

### Phase 3: Reporting and Remediation

1. Classify each finding by OWASP category, severity (CVSS), and confidence.
2. Provide proof-of-concept steps for each vulnerability.
3. Write remediation guidance specific to the technology stack.
4. Prioritize: Critical/High findings first, then Medium, then Low.
5. Present findings to the development team with a walkthrough session.

## Templates

### Finding Report Template

```markdown
## [OWASP-A0X] Finding Title

- **Category**: A0X — Category Name
- **Severity**: Critical / High / Medium / Low
- **CVSS Score**: X.X
- **Affected Endpoint**: `POST /api/v1/endpoint`
- **Parameter**: `user_id`

### Description
[What the vulnerability is and why it matters]

### Proof of Concept
1. Step 1...
2. Step 2...
3. Observed result...

### Impact
[What an attacker can achieve]

### Remediation
[Specific fix for this technology stack]

### References
- OWASP: https://owasp.org/Top10/
- CWE-XXX: https://cwe.mitre.org/
```

### Assessment Checklist

| # | Category | Tested | Finding | Severity |
|---|----------|--------|---------|----------|
| A01 | Broken Access Control | ☐ | | |
| A02 | Cryptographic Failures | ☐ | | |
| A03 | Injection | ☐ | | |
| A04 | Insecure Design | ☐ | | |
| A05 | Security Misconfiguration | ☐ | | |
| A06 | Vulnerable Components | ☐ | | |
| A07 | Auth Failures | ☐ | | |
| A08 | Integrity Failures | ☐ | | |
| A09 | Logging Failures | ☐ | | |
| A10 | SSRF | ☐ | | |

## Common Pitfalls

- **Testing without authorization** — Always obtain written permission before testing any application you do not own.
- **False positives from automated scanners** — Always manually verify scanner findings before reporting.
- **Ignoring business logic flaws** — Automated tools miss logic vulnerabilities; manual testing is essential.
- **Incomplete scope** — Staging environments may differ from production; clarify which environment is in scope.
- **Overlooking API endpoints** — Modern SPAs have most logic in APIs, not traditional page-based flows.
- **Confusing severity levels** — Use CVSS scoring consistently; do not inflate or deflate severity based on intuition.

## Legal Considerations

- **Written Authorization**: Never test without a signed Rules of Engagement (RoE) or contract.
- **Scope Boundaries**: Stay strictly within the agreed scope. Testing out-of-scope systems is unauthorized access.
- **Data Handling**: If you encounter real user data during testing, report it immediately and do not store it.
- **Disclosure**: Follow responsible disclosure timelines (typically 90 days). Do not publish findings without vendor consent.
- **Jurisdiction**: Laws vary by country. The Computer Fraud and Abuse Act (US), Computer Misuse Act (UK), and similar laws apply. Know your local regulations.
- **Safe Harbor**: Negotiate safe harbor clauses in your contract to protect testers from legal repercussions for good-faith testing.

## Further Reading

- [OWASP Top 10:2021 Official](https://owasp.org/Top10/)
- [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [CWE/SANS Top 25](https://cwe.mitre.org/top25/)
- [NIST SP 800-53 Security Controls](https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final)

---

## 中文版本

### 使用场景

- 对 Web 应用进行系统性安全评估
- 为新项目建立安全检查清单
- 按照行业基准（OWASP Top 10）审查应用安全性
- 准备合规审计（PCI-DSS、SOC 2、HIPAA）
- 向开发团队培训最关键的 Web 安全风险
- 根据风险严重程度确定修复优先级

### 核心步骤

1. **侦察与范围定义**：与应用所有者确认测试范围（URL、API、环境），获取书面授权，绘制应用表面（爬取页面、枚举 API 端点），记录技术栈信息。
2. **逐项评估 OWASP 类别**：按 A01–A10 依次检查——访问控制、加密缺陷、注入、不安全设计、安全配置错误、脆弱组件、认证失败、完整性失败、日志不足、SSRF。
3. **报告与修复**：按 OWASP 类别和 CVSS 严重程度分类每个发现，提供 PoC 步骤和针对性修复建议，按优先级排序（Critical → High → Medium → Low）。

### 模板说明

- **发现报告模板**：包含 OWASP 分类、严重程度、CVSS 评分、受影响端点、漏洞描述、PoC、影响分析、修复方案和参考链接。
- **评估检查清单**：涵盖 A01–A10 十大类别，每项标记是否已测试及发现情况。

### 常见陷阱

- **未获授权即进行测试** — 必须在测试前获得书面授权（Rules of Engagement）。
- **盲目信任自动化扫描结果** — 自动化工具会产生误报，必须手动验证每个发现。
- **忽略业务逻辑漏洞** — 自动化工具无法发现逻辑缺陷，手动测试必不可少。
- **测试范围不完整** — 预发布环境可能与生产环境不同，需明确确认测试环境。
- **遗漏 API 端点** — 现代 SPA 的核心逻辑在 API 层，而非传统页面流程。
- **混淆严重等级** — 应使用 CVSS 评分保持一致性，不要凭直觉调整严重程度。
