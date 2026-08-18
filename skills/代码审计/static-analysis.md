# Static Code Analysis Skill

> Leverage automated static analysis tools to detect security vulnerabilities, code quality issues, and compliance violations before code reaches production.

## When to Use

- Integrating security scanning into CI/CD pipelines
- Performing a security audit of an existing codebase
- Establishing a baseline security posture for a project
- Meeting compliance requirements (PCI-DSS 6.3, SOC 2, HIPAA)
- Onboarding new developers with automated guardrails
- Preparing for a penetration test by identifying low-hanging issues
- Evaluating a new language or framework's security tooling
- Post-incident review to find similar patterns elsewhere in the codebase

## Prerequisites

- Access to the source code repository
- Understanding of the project's language, framework, and build system
- Basic knowledge of secure coding patterns (OWASP, CERT)
- Familiarity with CI/CD platforms (GitHub Actions, GitLab CI, Jenkins)

## Tools

| Tool | Languages | Purpose | License |
|------|-----------|---------|---------|
| Semgrep | 30+ | Pattern-based SAST with custom rules | LGPL |
| CodeQL | 10+ | Deep semantic analysis with query language | GitHub (free for open source) |
| SonarQube | 30+ | Comprehensive code quality and security | LGPL / Commercial |
| Bandit | Python | Python-specific security linter | Apache-2.0 |
| ESLint + plugins | JavaScript/TypeScript | Linting with security rules | MIT |
| SpotBugs + FindSecBugs | Java | Bytecode-level security analysis | LGPL |
| Brakeman | Ruby/Rails | Rails-specific vulnerability scanner | MIT |
| gosec | Go | Go security checker | Apache-2.0 |
| Trivy | Config/IaC | Infrastructure-as-code misconfig detection | Apache-2.0 |
| Checkov | Terraform/Cloud | Cloud infrastructure policy checks | Apache-2.0 |

## Step-by-Step Procedure

### Phase 1: Tool Selection and Setup

1. **Identify the technology stack**: List all languages, frameworks, and infrastructure tools in use.
2. **Select primary and secondary tools**:
   - Primary: language-specific tool (Bandit for Python, gosec for Go, etc.)
   - Secondary: general-purpose tool (Semgrep, CodeQL, SonarQube)
   - Infrastructure: Trivy or Checkov for IaC scanning
3. **Install and configure**:
   ```bash
   # Semgrep
   pip install semgrep
   semgrep --config=auto .

   # CodeQL (GitHub)
   gh codeql database create --language=python db-python
   gh codeql database analyze db-python .github/codeql/queries.yml

   # Bandit
   pip install bandit
   bandit -r src/ -f json -o bandit-report.json

   # SonarQube
   sonar-scanner -Dsonar.projectKey=myproject
   ```
4. **Establish baseline**: Run initial scan, triage all findings, and record the baseline.

### Phase 2: Configuration and Customization

1. **Tune rules to reduce noise**:
   - Disable rules that are irrelevant to the project.
   - Adjust severity levels based on context.
   - Create project-specific exclusions (e.g., test directories).
2. **Write custom rules** for project-specific patterns:
   ```yaml
   # Semgrep custom rule example
   rules:
     - id: hardcoded-database-password
       patterns:
         - pattern: |
             DB_PASSWORD = "..."
       message: Hardcoded database password detected.
       severity: ERROR
       languages: [python]
   ```
3. **Configure scan scope**:
   - Include: `src/`, `lib/`, `app/`
   - Exclude: `node_modules/`, `vendor/`, `__pycache__/`, test fixtures
   - Set file size limits to skip generated code.

### Phase 3: CI/CD Integration

1. **Pre-commit hooks**: Run lightweight scans on staged files only.
   ```yaml
   # .pre-commit-config.yaml
   repos:
     - repo: https://github.com/returntocorp/semgrep
       hooks:
         - id: semgrep
           args: ['--config', 'p/security-audit', '--error']
   ```
2. **Pull request checks**: Run full scans on changed files.
   ```yaml
   # GitHub Actions example
   - name: Semgrep Scan
     uses: returntocorp/semgrep-action@v1
     with:
       config: >-
         p/security-audit
         p/owasp-top-ten
         p/secrets
   ```
3. **Nightly full scans**: Scan the entire codebase on a schedule.
4. **Gate policy**: Define which severities block the build (typically High and Critical).

### Phase 4: Finding Analysis and Triage

1. **Categorize findings**:
   - **True Positive**: Real vulnerability, needs fix.
   - **False Positive**: Not actually exploitable in context.
   - **Design Issue**: Requires architectural change, track separately.
2. **Validate critical findings manually**: Automated findings should be confirmed by examining the code path.
3. **Assign severity and priority**:
   - Use CVSS scoring for consistency.
   - Consider exploitability, data sensitivity, and exposure.
4. **Document context**: Record why false positives were dismissed for future reference.

### Phase 5: Common Vulnerability Patterns to Detect

| Category | Pattern | Example |
|----------|---------|---------|
| Injection | Unsanitized user input in SQL/query | `f"SELECT * FROM users WHERE id={user_input}"` |
| Secrets | Hardcoded credentials | `API_KEY = "sk-1234567890"` |
| XSS | Unescaped output in HTML templates | `innerHTML = userInput` |
| Path Traversal | Unsanitized file paths | `open(user_provided_path)` |
| SSRF | Unvalidated URLs in requests | `requests.get(user_url)` |
| Deserialization | Unsafe deserialization | `pickle.loads(untrusted_data)` |
| Weak Crypto | Deprecated algorithms | `hashlib.md5(password)` |
| Insecure Config | Debug mode enabled | `DEBUG = True` in production config |
| Race Conditions | TOCTOU vulnerabilities | File check-then-use patterns |

### Phase 6: Continuous Improvement

1. Track metrics over time: findings per KLOC, mean time to fix, false positive rate.
2. Update tool rules quarterly as new vulnerability patterns emerge.
3. Conduct team retrospectives on common finding patterns.
4. Contribute custom rules back to the community when applicable.
5. Review and update scan configuration with each major project change.

## Templates

### Scan Configuration Template

```yaml
# .semgrep.yml - Project-specific Semgrep configuration
rules:
  - id: sql-injection-python
    patterns:
      - pattern: |
          $CURSOR.execute(f"...{$VAR}...")
    message: Possible SQL injection via f-string formatting.
    severity: ERROR
    languages: [python]
    metadata:
      cwe: "CWE-89"
      owasp: "A03:2021 - Injection"
      confidence: HIGH

  - id: hardcoded-secret-generic
    patterns:
      - pattern-regex: '(?i)(password|secret|api_key|token)\s*=\s*"[^"]{8,}"'
    message: Possible hardcoded secret detected.
    severity: WARNING
    languages: [python, javascript, java]
    metadata:
      cwe: "CWE-798"
```

### Triage Spreadsheet Template

| ID | File:Line | Rule | Severity | Category | Verified | Status | Assignee | Notes |
|----|-----------|------|----------|----------|----------|--------|----------|-------|
| 1 | src/auth.py:45 | sql-injection | Critical | Injection | True Positive | Open | @alice | SQLi in login form |
| 2 | src/utils.py:12 | hardcoded-secret | High | Secrets | False Positive | Dismissed | - | Test fixture value |

### CI/CD Pipeline Template

```yaml
# .github/workflows/security-scan.yml
name: Security Scan
on: [push, pull_request]

jobs:
  semgrep:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: returntocorp/semgrep-action@v1
        with:
          config: >-
            p/security-audit
            p/owasp-top-ten
            .semgrep.yml

  bandit:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: '3.12'
      - run: pip install bandit && bandit -r src/ -f json
```

## Common Pitfalls

- **Ignoring false positives without documentation** — Always record why a finding was dismissed; future auditors will ask.
- **Running only one tool** — No single tool covers all vulnerability types. Layer multiple tools for coverage.
- **Scanning generated code** — Exclude auto-generated files, vendored dependencies, and build outputs.
- **Over-customizing rules to eliminate all warnings** — If you silence everything, you miss real issues. Aim for a manageable noise level, not zero warnings.
- **Not updating tool versions** — Vulnerability databases and rule sets improve constantly; pin versions in CI but update regularly.
- **Treating all findings equally** — A critical SQL injection is not the same as a low-severity unused import. Prioritize ruthlessly.
- **Scanning only new code** — Legacy code harbors the most vulnerabilities. Run periodic full-codebase scans.

## Legal Considerations

- **Code Ownership**: Only scan code you own or have explicit permission to scan. Scanning third-party code (even if included in your repo) may violate licenses.
- **Secret Exposure**: SAST tools may surface real secrets in scan reports. Ensure scan output is stored securely and access-controlled.
- **Compliance Evidence**: Scan reports may be subpoenaed or audited. Maintain accurate records.
- **Open Source Contributions**: When scanning open-source projects, follow responsible disclosure for any findings.
- **False Positive Accuracy**: Report findings accurately; inflating severity for attention undermines trust in the security program.

## Further Reading

- [Semgrep Documentation](https://semgrep.dev/docs/)
- [CodeQL Documentation](https://codeql.github.com/docs/)
- [OWASP Source Code Analysis Tools](https://owasp.org/www-community/Source_Code_Analysis_Tools)
- [CWE/SANS Top 25 Software Errors](https://cwe.mitre.org/top25/)
- [NIST SP 500-218: SAMATE](https://samate.nist.gov/)
- [Google Static Analysis Blog](https://testing.googleblog.com/)

---

## 中文版本

### 使用场景

- 将安全扫描集成到 CI/CD 流水线
- 对现有代码库进行安全审计
- 为项目建立安全态势基线
- 满足合规要求（PCI-DSS 6.3、SOC 2、HIPAA）
- 为新开发者提供自动化安全护栏
- 渗透测试前识别低垂果实
- 事后复盘时在代码库中搜索类似模式

### 核心步骤

1. **工具选型与配置**：根据技术栈选择主力工具（如 Python 用 Bandit，Go 用 gosec），配合通用工具（Semgrep、CodeQL）和基础设施扫描工具（Trivy、Checkov）。
2. **规则调优与定制**：禁用无关规则，调整严重等级，编写项目专用的自定义规则（如硬编码密码检测）。
3. **CI/CD 集成**：设置 pre-commit hook 做轻量扫描，PR 检查做增量扫描，夜间做全量扫描，定义构建阻断策略。
4. **发现分析与分类**：区分真阳性、假阳性和设计问题，手动验证关键发现，使用 CVSS 评分排序。
5. **持续改进**：跟踪指标（每千行代码发现数、修复时间、误报率），定期更新规则。

### 模板说明

- **扫描配置模板（`.semgrep.yml`）**：包含 SQL 注入和硬编码密钥的自定义 Semgrep 规则示例。
- **分类电子表格模板**：用于记录每个发现的文件位置、规则、严重程度、验证状态和负责人。
- **CI/CD 流水线模板**：GitHub Actions 配置示例，集成 Semgrep 和 Bandit 扫描。

### 常见陷阱

- **忽略误报不做记录** — 必须记录每个发现被忽略的原因，后续审计人员会查阅。
- **只用单一工具** — 没有工具能覆盖所有漏洞类型，应分层使用多个工具。
- **扫描生成代码** — 应排除自动生成的文件、vendored 依赖和构建产物。
- **过度自定义规则以消除所有告警** — 如果把所有告警都静音，会遗漏真正的问题。
- **不定期更新工具版本** — 漏洞数据库和规则集持续更新，CI 中应固定版本但定期升级。
- **对所有发现一视同仁** — Critical SQL 注入和低危未使用 import 不可相提并论，必须严格排优先级。
- **只扫描新代码** — 遗留代码中漏洞最多，应定期做全代码库扫描。
