# Secure Code Review Checklist Skill

> Conduct structured, manual secure code reviews using a complete checklist covering the most critical vulnerability classes.

## When to Use

- Performing a manual code review before a major release
- Training developers on secure coding practices through peer review
- Supplementing automated SAST findings with human analysis
- Reviewing security-critical code paths (authentication, authorization, cryptography, payment processing)
- Conducting an incident post-mortem to identify review gaps
- Building a security review culture in a development team
- Evaluating a codebase for acquisition or due diligence

## Prerequisites

- Access to the full source code (read-only at minimum)
- Understanding of the application's architecture and data flow
- Familiarity with the programming language and framework
- Knowledge of the OWASP Top 10 and common vulnerability patterns
- Access to the project's threat model (if available)

## Tools

| Tool | Purpose | License |
|------|---------|---------|
| GitHub/GitLab PR Review | Inline code review with comments | Proprietary / Free |
| Visual Studio Code | IDE with security extensions | MIT |
| Semgrep | Pattern matching for code patterns | LGPL |
| SonarQube | Code quality and security analysis | LGPL / Commercial |
| ThreatSpec | Threat modeling from code annotations | MIT |
| OWASP ASVS | Verification checklist reference | CC-BY-SA-4.0 |

## Step-by-Step Procedure

### Phase 1: Review Preparation

1. **Understand the change scope**:
   - Read the PR description, linked issues, and design documents.
   - Identify which modules, endpoints, and data flows are affected.
   - Determine if the change touches security-critical code.
2. **Classify the review depth**:
   - **Standard**: Bug fix, UI change, non-sensitive feature → focused review.
   - **Enhanced**: Auth, crypto, payment, data handling → deep review with checklist.
   - **Critical**: Architecture change, new auth flow, external integration → full review + threat model update.
3. **Set up the review environment**:
   - Check out the branch locally.
   - Run automated tools (SAST, linter) before manual review.
   - Note any pre-existing issues to avoid re-flagging them.

### Phase 2: Input Validation and Output Encoding

#### Input Validation Checklist

- [ ] All external inputs are validated on the server side.
- [ ] Input validation uses allowlist approach (define what is allowed, reject everything else).
- [ ] String inputs have length limits enforced.
- [ ] Numeric inputs are within expected ranges.
- [ ] File uploads are validated by type, size, and content (not just extension).
- [ ] JSON/XML inputs are validated against a schema.
- [ ] HTTP headers are not trusted for security decisions without validation.

#### Output Encoding Checklist

- [ ] HTML output uses context-appropriate encoding (HTML entity, JavaScript, URL, CSS).
- [ ] SQL queries use parameterized queries or prepared statements (no string concatenation).
- [ ] LDAP queries use proper escaping.
- [ ] OS commands use safe APIs (no shell string concatenation).
- [ ] Template engines auto-escape by default.
- [ ] JSON responses do not include user-controlled data without encoding.

### Phase 3: Authentication and Session Management

- [ ] Passwords are hashed with bcrypt/Argon2id (never MD5, SHA-1, SHA-256 plain).
- [ ] Salt is unique per user and cryptographically random.
- [ ] Session IDs are generated with a CSPRNG (≥ 128 bits of entropy).
- [ ] Session IDs change after authentication (prevent fixation).
- [ ] Sessions have idle and absolute timeouts.
- [ ] Logout invalidates the session server-side.
- [ ] MFA is enforced for admin and privileged operations.
- [ ] Password reset tokens are single-use, time-limited, and random.
- [ ] Account lockout or rate limiting exists on login attempts.
- [ ] No credentials, tokens, or secrets are hardcoded in source code.

### Phase 4: Authorization and Access Control

- [ ] Authorization is enforced on every request, not just at the UI layer.
- [ ] Role checks are performed server-side.
- [ ] Direct object references are validated against the user's permissions (anti-IDOR).
- [ ] Admin endpoints are protected from regular user access.
- [ ] API endpoints enforce the same authorization as the UI.
- [ ] Function-level access control exists (not just URL-level).
- [ ] Multi-tenant data isolation is verified (tenant A cannot see tenant B's data).
- [ ] File access operations validate the user's permission to the file.

### Phase 5: Cryptography and Secrets

- [ ] TLS is enforced for all data in transit (no HTTP fallback).
- [ ] TLS version ≥ 1.2 with strong cipher suites.
- [ ] Encryption at rest for sensitive data (PII, financial, health).
- [ ] AES-256 or equivalent for symmetric encryption.
- [ ] RSA ≥ 2048 bits or ECDSA for asymmetric encryption.
- [ ] No custom cryptographic implementations (use vetted libraries).
- [ ] Cryptographic keys are stored securely (HSM, KMS, vault — not in code or config files).
- [ ] Key rotation is implemented and tested.
- [ ] No secrets in version control (check `.env`, config files, comments).
- [ ] Random number generation uses CSPRNG (`crypto.randomBytes`, `secrets` module).

### Phase 6: Error Handling and Logging

- [ ] Error messages do not reveal internal details (stack traces, SQL errors, file paths).
- [ ] Custom error pages are configured for production.
- [ ] Security events are logged: authentication success/failure, authorization failures, input validation failures.
- [ ] Log entries include: timestamp, source IP, user ID, action, result.
- [ ] Sensitive data (passwords, tokens, PII) is never logged.
- [ ] Logs are sent to a centralized, tamper-proof logging system.
- [ ] Log retention complies with regulatory requirements.

### Phase 7: Data Protection

- [ ] PII is identified and classified.
- [ ] PII is encrypted at rest and in transit.
- [ ] Data minimization: only collect and store what is necessary.
- [ ] Data retention policies are implemented and enforced.
- [ ] Secure data deletion (not just soft delete) is available.
- [ ] Database connections use TLS.
- [ ] Backup encryption is enabled.
- [ ] Cache headers prevent sensitive data caching (`Cache-Control: no-store`).

### Phase 8: Dependency and Configuration

- [ ] All dependencies are pinned to specific versions.
- [ ] Lock files are committed.
- [ ] No known Critical/High CVEs in dependencies.
- [ ] Debug mode is disabled in production configuration.
- [ ] Default credentials are changed.
- [ ] Unnecessary features, endpoints, and services are disabled.
- [ ] CORS policy is restrictive (no wildcard `*`).
- [ ] Security headers are configured (CSP, HSTS, X-Frame-Options, X-Content-Type-Options).

### Phase 9: Race Conditions and Business Logic

- [ ] Critical operations use atomic transactions.
- [ ] No TOCTOU (Time-of-Check to Time-of-Use) vulnerabilities in file operations.
- [ ] Anti-replay mechanisms exist for financial transactions.
- [ ] Rate limiting protects expensive operations.
- [ ] Idempotency keys are used for non-repeatable operations.
- [ ] Multi-step workflows cannot be skipped or reordered.
- [ ] Business logic constraints are enforced server-side (not just client-side).

### Phase 10: API-Specific Checks

- [ ] API responses return only necessary fields (no mass data exposure).
- [ ] Mass assignment protection: API does not blindly accept all request fields.
- [ ] Pagination limits are enforced (no `?limit=999999`).
- [ ] GraphQL introspection is disabled in production.
- [ ] API versioning strategy is documented and followed.
- [ ] Rate limiting is per-user, not just per-IP.

## Templates

### Code Review Checklist (Printable)

```markdown
## Secure Code Review Checklist

### Review Info
- **Reviewer**: _______________
- **Date**: _______________
- **PR/MR**: #_____
- **Module**: _______________
- **Review Depth**: Standard / Enhanced / Critical

### Input Validation & Output Encoding    [ ] Pass  [ ] Fail  [ ] N/A
### Authentication & Sessions             [ ] Pass  [ ] Fail  [ ] N/A
### Authorization & Access Control        [ ] Pass  [ ] Fail  [ ] N/A
### Cryptography & Secrets                [ ] Pass  [ ] Fail  [ ] N/A
### Error Handling & Logging              [ ] Pass  [ ] Fail  [ ] N/A
### Data Protection                       [ ] Pass  [ ] Fail  [ ] N/A
### Dependencies & Configuration          [ ] Pass  [ ] Fail  [ ] N/A
### Race Conditions & Business Logic      [ ] Pass  [ ] Fail  [ ] N/A
### API Security                          [ ] Pass  [ ] Fail  [ ] N/A

### Findings Summary
| # | Category | Severity | File:Line | Description | Status |
|---|----------|----------|-----------|-------------|--------|
| 1 |          |          |           |             |        |

### Verdict:  [ ] Approved  [ ] Approved with Conditions  [ ] Rejected
```

### Review Comment Template

```markdown
**[SECURITY] [SEVERITY] Brief description**

The code at this location has a [vulnerability type] issue because [explanation of the vulnerability].

**Vulnerable Pattern:**
\`\`\`python
# Current (vulnerable)
query = f"SELECT * FROM users WHERE id = {user_id}"
\`\`\`

**Recommended Fix:**
\`\`\`python
# Fixed (parameterized)
cursor.execute("SELECT * FROM users WHERE id = %s", (user_id,))
\`\`\`

**References:**
- CWE-89: Improper Neutralization of Special Elements used in an SQL Command
- OWASP: https://owasp.org/Top10/A03_2021-Injection/
```

## Common Pitfalls

- **Reviewing too much code at once** — Keep review sessions to ≤ 400 lines of code. Beyond that, reviewer effectiveness drops dramatically.
- **Only reviewing diffs** — For security-critical code, review the entire file or module. A diff may miss context that makes the change insecure.
- **Treating the checklist as a pass/fail form** — The checklist is a guide, not a rubber stamp. Use judgment for context-specific risks.
- **Not understanding the data flow** — A function may look safe in isolation but be dangerous when called with untrusted input. Trace the data flow end-to-end.
- **Focusing only on syntax** — Logic flaws and design issues are often more impactful than syntax errors. Think about what the code is supposed to do, not just what it does.
- **Ignoring test code** — Test code can contain hardcoded credentials, test data that resembles real data, and patterns that reveal security assumptions.
- **Not following up on findings** — A finding that is noted but not tracked to completion is a finding that will not be fixed.

## Legal Considerations

- **Code Ownership**: Ensure you have authorization to review the code, especially for proprietary or classified systems.
- **Findings Confidentiality**: Security findings are sensitive. Do not share them outside the authorized team.
- **Third-Party Code**: When reviewing code that interfaces with third-party libraries, document boundary assumptions.
- **Audit Trail**: Maintain review records for compliance purposes. Many frameworks (SOC 2, ISO 27001) require evidence of security reviews.
- **Reviewer Liability**: In some jurisdictions, reviewers may have liability for missed findings in regulated industries. Document your review process thoroughly.

## Further Reading

- [OWASP Code Review Guide](https://owasp.org/www-project-code-review-guide/)
- [OWASP ASVS v4.0](https://owasp.org/www-project-application-security-verification-standard/)
- [Google Engineering Practices: Code Review](https://google.github.io/engineering-practices/review/)
- [SEI CERT Coding Standards](https://wiki.sei.cmu.edu/confluence/display/seccode/)
- [Microsoft Secure Coding Guidelines](https://learn.microsoft.com/en-us/security/engineering/secure-coding-practices)
- [SAFECode: Fundamental Practices for Secure Software Development](https://safecode.org/)

---

## 中文版本

### 使用场景

- 大版本发布前进行人工代码安全审查
- 通过同行评审培训开发者安全编码实践
- 用人工分析补充自动化 SAST 发现
- 审查安全关键代码路径（认证、授权、加密、支付）
- 事故复盘以识别审查盲区
- 在开发团队中建立安全审查文化
- 收购或尽职调查时评估代码库

### 核心步骤

1. **审查准备**：阅读 PR 描述和设计文档，识别受影响的模块和数据流，根据变更类型（标准/增强/关键）确定审查深度。
2. **输入验证与输出编码**：检查所有外部输入的服务端验证（白名单方式），验证 SQL 参数化查询、HTML 输出编码、OS 命令安全 API。
3. **认证与会话管理**：验证密码哈希算法、Session ID 随机性、会话超时、登出失效、MFA 强制执行。
4. **授权与访问控制**：检查每个请求的服务端授权、IDOR 防护、多租户数据隔离、API 授权一致性。
5. **加密与密钥**：验证 TLS 版本和密码套件、静态数据加密、密钥存储（HSM/KMS）、无硬编码密钥。
6. **错误处理与日志**：确认错误信息不泄露内部细节，安全事件被正确记录，敏感数据不被记录。

### 模板说明

- **可打印检查清单模板**：涵盖 10 大审查类别（输入验证、认证、授权、加密、错误处理、数据保护、依赖配置、竞态条件、API 安全），每项标记 Pass/Fail/N/A。
- **审查评论模板**：标准化的安全问题报告格式——包含严重程度、漏洞模式、修复建议和参考链接。

### 常见陷阱

- **一次审查过多代码** — 每次审查会话不超过 400 行代码，超过后审查效率急剧下降。
- **只审查 diff** — 对安全关键代码，应审查整个文件或模块，diff 可能遗漏上下文。
- **将检查清单当作通过/失败表格** — 检查清单是指南而非橡皮图章，需结合上下文判断风险。
- **不理解数据流** — 一个函数单独看可能安全，但被不可信输入调用时就有危险，需端到端追踪数据流。
- **只关注语法** — 逻辑缺陷和设计问题的影响往往超过语法错误。
- **忽略测试代码** — 测试代码中可能包含硬编码凭据、类真实数据和安全假设。
- **不跟进发现结果** — 记录但未追踪到完成的发现，就是不会被修复的发现。
