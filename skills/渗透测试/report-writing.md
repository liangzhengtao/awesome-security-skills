# Penetration Test Report Writing Skill

> Produce clear, actionable, and professional penetration test reports that communicate findings to both technical and executive audiences.

## When to Use

- Completing a penetration test engagement and delivering results
- Writing a security assessment report for a client or management
- Creating an executive summary for C-level stakeholders
- Documenting vulnerability findings with proof of concept
- Preparing a remediation roadmap for the development team
- Building report templates for a security consulting practice
- Writing a debrief presentation after an engagement
- Creating compliance evidence for PCI-DSS, SOC 2, or HIPAA audits

## Prerequisites

- Completed penetration test with documented findings
- Understanding of the target environment and business context
- Access to screenshots, request/response captures, and tool output
- Knowledge of CVSS scoring methodology
- Familiarity with the audience (executive, technical, compliance)

## Tools

| Tool | Purpose | License |
|------|---------|---------|
| Markdown / LaTeX | Report writing and formatting | Free |
| Dradis | Collaborative reporting platform | GPL / Commercial |
| PlexTrac | Pentest reporting and management | Commercial |
| SysReptor | Automated pentest reporting | Commercial |
| CherryTree | Note-taking during testing | GPL |
| OBS / ShareX | Screenshot and screen recording | GPL / Free |
| Burp Suite | Request/response evidence capture | Community / Pro |
| CVSS Calculator | Severity scoring | Free |

## Step-by-Step Procedure

### Phase 1: Evidence Collection and Organization

1. **During the engagement**, capture evidence for every finding:
   - Screenshots with timestamps.
   - Full HTTP request and response pairs (from Burp/ZAP).
   - Command-line output and terminal screenshots.
   - Network packet captures if relevant.
2. **Organize evidence by finding ID**:
   ```
   evidence/
   ├── VULN-001-sqli/
   │   ├── request.txt
   │   ├── response.txt
   │   ├── screenshot-login.png
   │   └── sqlmap-output.txt
   ├── VULN-002-xss/
   │   ├── payload.txt
   │   └── screenshot-alert.png
   ```
3. **Sanitize evidence**: Remove real user data, passwords, and PII from screenshots and logs.
4. **Verify reproducibility**: Confirm each finding can be reproduced with the documented steps.

### Phase 2: Scoring and Classification

#### CVSS v3.1 Scoring

Use the CVSS calculator (https://www.first.org/cvss/calculator/3.1) for each finding:

| Severity | CVSS Score Range | Color Code |
|----------|-----------------|------------|
| Critical | 9.0 – 10.0 | Red |
| High | 7.0 – 8.9 | Orange |
| Medium | 4.0 – 6.9 | Yellow |
| Low | 0.1 – 3.9 | Blue |
| Informational | 0.0 | Gray |

#### Finding Classification

- **Confirmed**: Vulnerability verified with proof of concept.
- **Potential**: Strong indicators but could not be fully confirmed (explain why).
- **Informational**: Not a vulnerability but a security improvement recommendation.

### Phase 3: Report Structure

#### Document Structure Overview

```
1. Cover Page
2. Table of Contents
3. Executive Summary (1-2 pages)
4. Engagement Overview
5. Scope and Methodology
6. Risk Assessment Summary
7. Detailed Findings
8. Remediation Roadmap
9. Appendices
   A. Tool Inventory
   B. CVSS Scoring Details
   C. Evidence Index
   D. Raw Scan Output (if requested)
```

### Phase 4: Writing Each Section

#### 4.1 Cover Page

```markdown
# Penetration Test Report

## [Client Organization Name]

**Assessment Type**: Web Application Penetration Test
**Classification**: CONFIDENTIAL
**Date**: [Start Date] – [End Date]
**Report Version**: 1.0
**Prepared By**: [Tester / Company Name]
**Document Reference**: PT-[YYYY]-[NNN]

---

This document contains confidential security information. Distribution is
restricted to authorized personnel only. Unauthorized disclosure may result
in legal consequences.
```

#### 4.2 Executive Summary

The executive summary is the most important section. Executives may read only this page.

```markdown
## Executive Summary

### Overview
Between [Start Date] and [End Date], [Testing Company] conducted a penetration
test of [Client]'s [application name] web application. The assessment was
performed to identify security vulnerabilities that could be exploited by
threat actors to compromise the confidentiality, integrity, or availability
of the application and its data.

### Key Findings
The assessment identified **[N] vulnerabilities**: [X] Critical, [Y] High,
[Z] Medium, [W] Low, and [V] Informational.

**Critical Issues:**
1. **SQL Injection in Login Form** — Allows unauthenticated access to the
   entire user database, including passwords and personal information.
2. **Remote Code Execution via File Upload** — An attacker can execute
   arbitrary commands on the server by uploading a malicious file.

### Business Impact
If exploited, the critical vulnerabilities could result in:
- **Data Breach**: Access to [N] user records containing PII and credentials.
- **System Compromise**: Full server takeover leading to lateral movement.
- **Regulatory Exposure**: Potential GDPR/CCPA fines of up to [amount].
- **Reputational Damage**: Public disclosure of security weaknesses.

### Overall Risk Rating: **HIGH**

### Recommendation Summary
Immediate action is required to remediate the [X] Critical and [Y] High
vulnerabilities before the application is exposed to untrusted networks.
A remediation timeline is provided in Section [N].
```

#### 4.3 Detailed Finding Template

Write every finding using this consistent structure:

```markdown
## [VULN-001] SQL Injection in User Authentication

### Metadata
| Field | Value |
|-------|-------|
| Severity | **Critical** |
| CVSS Score | 9.8 (AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H) |
| CWE | CWE-89: SQL Injection |
| OWASP | A03:2021 – Injection |
| Affected URL | `https://target.com/api/auth/login` |
| Parameter | `email` (POST body) |
| Discovered | 2024-01-15 |
| Status | Open |

### Description
The login endpoint at `/api/auth/login` is vulnerable to SQL injection through
the `email` parameter. User-supplied input is directly concatenated into a SQL
query without parameterization or sanitization. This allows an unauthenticated
attacker to execute arbitrary SQL queries against the database.

### Technical Details
The vulnerable code constructs the query as follows:

```python
query = f"SELECT * FROM users WHERE email = '{email}' AND password = '{hashed_pw}'"
cursor.execute(query)
```

### Proof of Concept

**Step 1: Confirm SQL injection**

Request:
```http
POST /api/auth/login HTTP/1.1
Host: target.com
Content-Type: application/json

{"email": "' OR 1=1--", "password": "anything"}
```

Response (HTTP 200):
```json
{
  "token": "eyJ...",
  "user": {"id": 1, "email": "admin@target.com", "role": "admin"}
}
```

**Step 2: Extract data using SQLMap**

```bash
sqlmap -u "https://target.com/api/auth/login" \
  --data='{"email":"test","password":"test"}' \
  --headers="Content-Type: application/json" \
  --batch --dbs
```

Output:
```
[*] information_schema
[*] target_production
[*] target_staging
```

**Step 3: Enumerate user table**

```bash
sqlmap -u [same] -D target_production -T users --dump --batch
```

Result: [N] user records extracted including email, password hash, and PII.

### Impact
- **Authentication Bypass**: Any user account can be accessed, including admin.
- **Data Exfiltration**: Full database access including all user records.
- **Data Modification**: Attacker can insert, update, or delete any record.
- **Potential RCE**: Depending on database configuration, OS command execution
  may be possible via `xp_cmdshell` (MSSQL) or `COPY TO PROGRAM` (PostgreSQL).

### Remediation

**Immediate (within 48 hours):**
1. Replace string concatenation with parameterized queries:
   ```python
   cursor.execute(
       "SELECT * FROM users WHERE email = %s AND password = %s",
       (email, hashed_pw)
   )
   ```
2. Deploy a WAF rule to block common SQL injection patterns.

**Short-term (within 2 weeks):**
3. Implement input validation: email must match RFC 5322 format.
4. Add ORM-level query protections (SQLAlchemy, Django ORM).
5. Enable database query logging for forensic analysis.

**Verification:**
6. Re-test the endpoint with the same payloads to confirm the fix.
7. Run automated SQLi scanner to verify no similar issues exist elsewhere.

### References
- [OWASP SQL Injection](https://owasp.org/www-community/attacks/SQL_Injection)
- [CWE-89](https://cwe.mitre.org/data/definitions/89.html)
- [PortSwigger SQL Injection](https://portswigger.net/web-security/sql-injection)
```

#### 4.4 Remediation Roadmap

```markdown
## Remediation Roadmap

### Immediate (0-48 hours)
| ID | Finding | Severity | Action |
|----|---------|----------|--------|
| VULN-001 | SQL Injection | Critical | Parameterize queries |
| VULN-002 | RCE via Upload | Critical | Remove upload endpoint |

### Short-term (1-2 weeks)
| ID | Finding | Severity | Action |
|----|---------|----------|--------|
| VULN-003 | Stored XSS | High | Implement output encoding |
| VULN-004 | IDOR | High | Add authorization checks |

### Medium-term (1-3 months)
| ID | Finding | Severity | Action |
|----|---------|----------|--------|
| VULN-005 | Weak Password Policy | Medium | Enforce NIST 800-63B |
| VULN-006 | Missing Security Headers | Medium | Configure CSP, HSTS |

### Verification Schedule
- **Immediate fixes**: Re-test within 1 week of remediation.
- **Short-term fixes**: Re-test within 1 month.
- **Medium-term fixes**: Include in next quarterly assessment.
```

### Phase 5: Quality Assurance

1. **Peer review**: Have another tester review the report for accuracy and clarity.
2. **Fact-check**: Verify every finding is reproducible and evidence supports the claims.
3. **Consistency check**: Ensure severity ratings, CVSS scores, and terminology are consistent throughout.
4. **Spelling and grammar**: Use a grammar checker. Typos in a professional report undermine credibility.
5. **Sanitization pass**: Double-check that no real credentials, PII, or client-sensitive data remains in the report.
6. **Classification**: Mark the report with the appropriate confidentiality level.

### Phase 6: Delivery and Follow-up

1. Deliver the report via a secure channel (encrypted email, secure portal).
2. Schedule a walkthrough presentation with the technical team.
3. Schedule a separate executive briefing focusing on business impact.
4. Agree on a remediation retest timeline.
5. Archive all engagement materials per your data retention policy.

## Templates

### Report Quality Checklist

- [ ] Cover page with classification marking
- [ ] Table of contents with page numbers
- [ ] Executive summary is ≤ 2 pages and jargon-free
- [ ] All findings have CVSS scores and CWE references
- [ ] Every finding has reproducible proof of concept
- [ ] All screenshots are legible and annotated
- [ ] Remediation guidance is specific and actionable
- [ ] Remediation roadmap with priorities and timeline
- [ ] Evidence is sanitized (no real PII or credentials)
- [ ] Report reviewed by a peer
- [ ] Classification and distribution markings present

## Common Pitfalls

- **Writing for security professionals only** — The executive summary must be understandable by non-technical stakeholders. Avoid jargon.
- **Vague remediation guidance** — "Fix the SQL injection" is not helpful. Provide specific code changes, configuration settings, or tool recommendations.
- **Missing business impact context** — Technical findings without business impact explanation do not drive action. Always translate to business risk.
- **Inconsistent severity ratings** — Use CVSS consistently. Do not inflate or deflate severity based on personal judgment alone.
- **No reproduction steps** — A finding without reproducible steps will be dismissed as a false positive.
- **Identifying individuals negatively** — Report system and process failures, not individual blame. "The code lacks input validation" not "Developer X wrote bad code."
- **Including real credentials in the report** — Always redact. Even in a confidential report, credentials should be masked.

## Legal Considerations

- **Confidentiality**: Penetration test reports are highly sensitive. Mark them with appropriate classification and restrict distribution.
- **Attorney-Client Privilege**: In some engagements, the report may be prepared under attorney-client privilege. Consult legal counsel on this approach.
- **Liability**: Report findings factually and objectively. Do not overstate severity to sell more services.
- **Retention**: Follow the agreed data retention policy. Destroy evidence and test data after the retention period.
- **Third-Party Disclosure**: Never share a client's report with another client or use findings as examples without explicit permission.
- **Regulatory Reporting**: Some regulations (GDPR Article 33) require breach notification within 72 hours. If the pentest reveals a breach, inform the client's DPO immediately.

## Further Reading

- [OWASP Testing Guide: Reporting](https://owasp.org/www-project-web-security-testing-guide/)
- [PTES: Reporting](http://www.pentest-standard.org/index.php/Reporting)
- [SANS: Penetration Test Reporting](https://www.sans.org/white-papers/)
- [CVSS v3.1 Specification](https://www.first.org/cvss/v3.1/specification-document)
- [NIST SP 800-115: Reporting](https://csrc.nist.gov/publications/detail/sp/800-115/final)
- [Offensive Security Report Templates](https://www.offsec.com/)

---

## 中文版本

### 使用场景

- 渗透测试完成后交付结果报告
- 为客户或管理层撰写安全评估报告
- 为 C 级高管创建执行摘要
- 用 PoC 记录漏洞发现
- 为开发团队制定修复路线图
- 为安全咨询业务构建报告模板
- 编写测试结束后的汇报演示
- 为 PCI-DSS、SOC 2 或 HIPAA 审计创建合规证据

### 核心步骤

1. **证据收集与整理**：测试期间为每个发现捕获证据（截图、HTTP 请求/响应、命令行输出），按发现 ID 组织，脱敏处理（移除真实用户数据和 PII），验证可复现性。
2. **评分与分类**：使用 CVSS v3.1 计算器为每个发现评分（Critical ≥ 9.0、High ≥ 7.0、Medium ≥ 4.0、Low < 4.0），分类为已确认/潜在/信息性。
3. **报告撰写**：按照标准结构编写——封面页、目录、执行摘要（1-2 页无行话）、测试概述、范围与方法论、风险评估摘要、详细发现、修复路线图、附录。
4. **质量保证**：同行评审、事实核查、一致性检查、拼写语法检查、脱敏复核、密级标记。
5. **交付与跟进**：通过安全渠道交付报告，分别安排技术团队和管理层汇报会，约定修复复测时间。

### 模板说明

- **详细发现模板**：每个发现使用统一结构——元数据（CVSS、CWE、OWASP）、漏洞描述、技术细节、分步 PoC、影响分析、分阶段修复方案（立即/短期）和验证步骤。
- **修复路线图模板**：按紧急程度分层——立即（0-48 小时）、短期（1-2 周）、中期（1-3 个月），附复测计划。
- **报告质量检查清单**：11 项逐一核查——封面、目录、执行摘要、CVSS 评分、PoC 可复现、截图标注、修复建议可操作、脱敏等。

### 常见陷阱

- **仅为安全专业人员撰写** — 执行摘要必须让非技术高管能理解，避免使用行话。
- **修复建议模糊** — "修复 SQL 注入"没有帮助，应提供具体的代码修改、配置变更或工具推荐。
- **缺少业务影响上下文** — 没有业务影响解释的技术发现无法驱动行动，必须转化为业务风险。
- **严重等级评分不一致** — 统一使用 CVSS，不要凭个人判断调整严重程度。
- **缺少复现步骤** — 没有可复现步骤的发现会被当作误报忽略。
- **将问题归咎于个人** — 报告系统和流程失败，而非个人过错。
- **报告中包含真实凭据** — 即使是机密报告，凭据也应脱敏处理。
