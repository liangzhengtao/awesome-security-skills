# Security Automation with Scripts Skill

> Build automated security testing pipelines, custom vulnerability scanners, and operational security tools using Python, Bash, and scripting frameworks.

## When to Use

- Automating repetitive security testing tasks
- Building a continuous security testing pipeline
- Creating custom vulnerability scanners for specific technologies
- Automating compliance checks and configuration audits
- Building incident response automation (detection, triage, containment)
- Orchestrating multiple security tools into a unified workflow
- Automating reconnaissance for bug bounty or pentest engagements
- Creating security dashboards and reporting automation
- Implementing DevSecOps shift-left security checks

## Prerequisites

- Proficiency in at least one scripting language (Python preferred, Bash required)
- Understanding of security testing concepts and common vulnerability classes
- Familiarity with REST APIs, CLI tools, and Unix pipelines
- Knowledge of CI/CD platforms (GitHub Actions, GitLab CI, Jenkins)
- Basic understanding of containerization (Docker) for reproducible environments

## Tools and Libraries

| Tool / Library | Language | Purpose | License |
|----------------|----------|---------|---------|
| Python `requests` | Python | HTTP client for API testing | Apache-2.0 |
| Python `scapy` | Python | Packet crafting and network automation | GPL |
| Python `pwntools` | Python | CTF and exploit development | MIT |
| `nuclei` | CLI | Template-based vulnerability scanning | MIT |
| `ffuf` | CLI | Web fuzzing | MIT |
| `httpx` | CLI | HTTP probing | MIT |
| `subfinder` | CLI | Subdomain enumeration | MIT |
| `trivy` | CLI | Container and dependency scanning | Apache-2.0 |
| `ansible` | Python | Configuration management and compliance | GPL |
| GitHub Actions | YAML | CI/CD security pipeline | Free tier available |
| `cron` | Shell | Scheduled task execution | System |

## Step-by-Step Procedure

### Phase 1: Environment Setup

1. **Create a dedicated security automation environment**:
   ```bash
   mkdir -p ~/security-automation/{scripts,templates,reports,configs}
   cd ~/security-automation
   python -m venv .venv
   source .venv/bin/activate
   pip install requests beautifulsoup4 python-nmap jinja2 pyyaml
   ```
2. **Install Go-based tools** (if not already present):
   ```bash
   go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
   go install -v github.com/projectdiscovery/httpx/cmd/httpx@latest
   go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
   go install -v github.com/ffuf/ffuf/v2@latest
   ```
3. **Establish project structure**:
   ```
   security-automation/
   ├── scripts/           # Custom automation scripts
   ├── templates/         # Nuclei templates, report templates
   ├── reports/           # Generated reports
   ├── configs/           # Tool configurations
   ├── pipelines/         # CI/CD pipeline definitions
   └── requirements.txt   # Python dependencies
   ```

### Phase 2: Automated Reconnaissance Pipeline

```python
#!/usr/bin/env python3
"""
Automated Reconnaissance Pipeline
Collects subdomains, probes live hosts, and discovers endpoints.
"""
import subprocess
import json
import sys
from pathlib import Path
from datetime import datetime

class ReconPipeline:
    def __init__(self, domain, output_dir="reports"):
        self.domain = domain
        self.timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
        self.output_dir = Path(output_dir) / f"{domain}_{self.timestamp}"
        self.output_dir.mkdir(parents=True, exist_ok=True)
        self.subdomains = []
        self.live_hosts = []

    def run_command(self, cmd, output_file=None):
        """Execute a command and optionally save output."""
        print(f"[*] Running: {' '.join(cmd)}")
        result = subprocess.run(cmd, capture_output=True, text=True, timeout=300)
        if output_file:
            (self.output_dir / output_file).write_text(result.stdout)
        return result.stdout.strip().split('\n') if result.stdout.strip() else []

    def enumerate_subdomains(self):
        """Phase 1: Subdomain enumeration."""
        print(f"\n[+] Phase 1: Subdomain Enumeration for {self.domain}")

        # subfinder
        sf_results = self.run_command(
            ["subfinder", "-d", self.domain, "-silent"],
            "subfinder.txt"
        )

        # crt.sh via curl
        crt_cmd = (
            f'curl -s "https://crt.sh/?q=%25.{self.domain}&output=json" '
            f'| jq -r ".[].name_value" | sort -u'
        )
        crt_results = subprocess.run(
            crt_cmd, shell=True, capture_output=True, text=True
        ).stdout.strip().split('\n')

        # Combine and deduplicate
        all_subs = set(sf_results + crt_results)
        self.subdomains = sorted([s for s in all_subs if s and '*' not in s])
        (self.output_dir / "all_subdomains.txt").write_text(
            '\n'.join(self.subdomains)
        )
        print(f"[+] Found {len(self.subdomains)} unique subdomains")
        return self.subdomains

    def probe_live_hosts(self):
        """Phase 2: Probe for live hosts."""
        print(f"\n[+] Phase 2: Probing Live Hosts")

        sub_file = self.output_dir / "all_subdomains.txt"
        self.live_hosts = self.run_command(
            ["httpx", "-l", str(sub_file), "-silent",
             "-status-code", "-title", "-tech-detect",
             "-o", str(self.output_dir / "live_hosts.txt")],
        )
        print(f"[+] Found {len(self.live_hosts)} live hosts")
        return self.live_hosts

    def run_nuclei_scan(self, severity="critical,high,medium"):
        """Phase 3: Vulnerability scanning with Nuclei."""
        print(f"\n[+] Phase 3: Nuclei Vulnerability Scan")

        host_file = self.output_dir / "live_hosts.txt"
        self.run_command(
            ["nuclei", "-l", str(host_file),
             "-severity", severity,
             "-o", str(self.output_dir / "nuclei_results.txt"),
             "-silent"],
            "nuclei_results.txt"
        )

    def run_full_pipeline(self):
        """Execute the complete pipeline."""
        print(f"[*] Starting recon pipeline for {self.domain}")
        self.enumerate_subdomains()
        self.probe_live_hosts()
        self.run_nuclei_scan()
        print(f"\n[+] Pipeline complete. Results in {self.output_dir}/")

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python recon_pipeline.py <domain>")
        sys.exit(1)
    pipeline = ReconPipeline(sys.argv[1])
    pipeline.run_full_pipeline()
```

### Phase 3: Automated Web Vulnerability Scanner

```python
#!/usr/bin/env python3
"""
Automated web vulnerability checks for common issues.
"""
import requests
import sys
from urllib.parse import urljoin
from dataclasses import dataclass, field
from typing import List

@dataclass
class Finding:
    title: str
    severity: str
    url: str
    description: str
    evidence: str = ""

class WebVulnScanner:
    def __init__(self, base_url):
        self.base_url = base_url.rstrip('/')
        self.session = requests.Session()
        self.session.headers['User-Agent'] = 'SecurityAudit/1.0'
        self.findings: List[Finding] = []

    def check_security_headers(self):
        """Check for missing security headers."""
        print("[*] Checking security headers...")
        required_headers = {
            'Strict-Transport-Security': 'Missing HSTS header',
            'Content-Security-Policy': 'Missing CSP header',
            'X-Frame-Options': 'Missing clickjacking protection',
            'X-Content-Type-Options': 'Missing MIME sniffing protection',
            'X-XSS-Protection': 'Missing XSS protection header',
            'Referrer-Policy': 'Missing referrer policy',
        }
        try:
            resp = self.session.get(self.base_url, timeout=10)
            for header, description in required_headers.items():
                if header not in resp.headers:
                    self.findings.append(Finding(
                        title=f"Missing Security Header: {header}",
                        severity="Medium",
                        url=self.base_url,
                        description=description,
                        evidence=f"Header '{header}' not found in response"
                    ))
        except requests.RequestException as e:
            print(f"[!] Error checking headers: {e}")

    def check_directory_listing(self):
        """Check for directory listing on common paths."""
        print("[*] Checking directory listing...")
        common_dirs = ['/images/', '/uploads/', '/backup/', '/admin/',
                       '/static/', '/assets/', '/tmp/', '/test/']
        for path in common_dirs:
            url = urljoin(self.base_url, path)
            try:
                resp = self.session.get(url, timeout=10)
                if resp.status_code == 200 and 'Index of' in resp.text:
                    self.findings.append(Finding(
                        title=f"Directory Listing Enabled: {path}",
                        severity="Medium",
                        url=url,
                        description=f"Directory listing is enabled at {path}",
                        evidence=f"HTTP {resp.status_code} with 'Index of' in response"
                    ))
            except requests.RequestException:
                continue

    def check_information_disclosure(self):
        """Check for information disclosure in headers and error pages."""
        print("[*] Checking information disclosure...")
        # Server header
        try:
            resp = self.session.get(self.base_url, timeout=10)
            server = resp.headers.get('Server', '')
            if server and any(v in server.lower() for v in
                              ['apache/', 'nginx/', 'iis/', 'tomcat/']):
                self.findings.append(Finding(
                    title="Server Version Disclosure",
                    severity="Low",
                    url=self.base_url,
                    description=f"Server header reveals version: {server}",
                    evidence=f"Server: {server}"
                ))
        except requests.RequestException:
            pass

        # Error page disclosure
        try:
            resp = self.session.get(
                urljoin(self.base_url, '/nonexistent_page_12345'),
                timeout=10
            )
            indicators = ['stack trace', 'exception', 'traceback',
                         'debug', 'internal server error']
            for indicator in indicators:
                if indicator.lower() in resp.text.lower():
                    self.findings.append(Finding(
                        title="Error Page Information Disclosure",
                        severity="Medium",
                        url=resp.url,
                        description="Error page contains sensitive information",
                        evidence=f"Found '{indicator}' in error response"
                    ))
                    break
        except requests.RequestException:
            pass

    def generate_report(self):
        """Generate a findings report."""
        report = f"# Vulnerability Scan Report\n\n"
        report += f"**Target**: {self.base_url}\n"
        report += f"**Total Findings**: {len(self.findings)}\n\n"
        for i, f in enumerate(self.findings, 1):
            report += f"## {i}. {f.title}\n"
            report += f"- **Severity**: {f.severity}\n"
            report += f"- **URL**: {f.url}\n"
            report += f"- **Description**: {f.description}\n"
            if f.evidence:
                report += f"- **Evidence**: {f.evidence}\n"
            report += "\n"
        return report

    def run_all(self):
        """Run all checks."""
        self.check_security_headers()
        self.check_directory_listing()
        self.check_information_disclosure()
        return self.generate_report()

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python web_scanner.py <url>")
        sys.exit(1)
    scanner = WebVulnScanner(sys.argv[1])
    print(scanner.run_all())
```

### Phase 4: CI/CD Security Pipeline

```yaml
# .github/workflows/security-automation.yml
name: Security Automation Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]
  schedule:
    - cron: '0 2 * * 1'  # Weekly on Monday at 2 AM

jobs:
  dependency-scan:
    name: Dependency Vulnerability Scan
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run Trivy
        uses: aquasecurity/trivy-action@master
        with:
          scan-type: 'fs'
          severity: 'CRITICAL,HIGH'
          format: 'table'
          exit-code: '1'

  sast-scan:
    name: Static Analysis
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run Semgrep
        uses: returntocorp/semgrep-action@v1
        with:
          config: >-
            p/security-audit
            p/owasp-top-ten
            p/secrets

  container-scan:
    name: Container Image Scan
    runs-on: ubuntu-latest
    if: github.event_name == 'push'
    steps:
      - uses: actions/checkout@v4
      - name: Build image
        run: docker build -t test-image .
      - name: Scan image
        uses: aquasecurity/trivy-action@master
        with:
          image-ref: 'test-image'
          severity: 'CRITICAL,HIGH'
          exit-code: '1'

  secrets-scan:
    name: Secrets Detection
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - name: Run Gitleaks
        uses: gitleaks/gitleaks-action@v2
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

  iac-scan:
    name: Infrastructure as Code Scan
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run Checkov
        uses: bridgecrewio/checkov-action@v12
        with:
          directory: .
          framework: terraform,kubernetes,dockerfile
```

### Phase 5: Compliance Automation

```python
#!/usr/bin/env python3
"""
Automated compliance checks for common security baselines.
"""
import subprocess
import json

class ComplianceChecker:
    def __init__(self):
        self.checks = []
        self.results = []

    def add_check(self, name, category, check_fn):
        self.checks.append({
            "name": name,
            "category": category,
            "fn": check_fn
        })

    def check_ssh_config(self):
        """Verify SSH hardening."""
        issues = []
        try:
            with open('/etc/ssh/sshd_config') as f:
                config = f.read()
            checks = {
                "PermitRootLogin no": "Root login is permitted",
                "PasswordAuthentication no": "Password authentication is enabled",
                "Protocol 2": "SSH protocol version 1 may be enabled",
                "MaxAuthTries 3": "No max authentication attempts limit",
            }
            for setting, issue in checks.items():
                key, expected = setting.split(' ', 1)
                if key.lower() not in config.lower():
                    issues.append(f"Missing: {setting} — {issue}")
        except FileNotFoundError:
            issues.append("SSH config file not found")
        return issues

    def check_firewall(self):
        """Verify firewall is active."""
        issues = []
        result = subprocess.run(
            ["iptables", "-L", "-n"], capture_output=True, text=True
        )
        if "policy ACCEPT" in result.stdout and "Chain INPUT" in result.stdout:
            # Check if there are any rules beyond default policy
            lines = [l for l in result.stdout.split('\n')
                     if l.strip() and not l.startswith('Chain')
                     and not l.startswith('target')]
            if len(lines) < 3:
                issues.append("Firewall has no meaningful rules configured")
        return issues

    def run_all(self):
        """Run all compliance checks."""
        self.add_check("SSH Hardening", "System", self.check_ssh_config)
        self.add_check("Firewall Configuration", "Network", self.check_firewall)

        for check in self.checks:
            print(f"[*] Running: {check['name']}")
            issues = check['fn']()
            self.results.append({
                "check": check['name'],
                "category": check['category'],
                "passed": len(issues) == 0,
                "issues": issues
            })

        # Summary
        passed = sum(1 for r in self.results if r['passed'])
        total = len(self.results)
        print(f"\n[+] Compliance Summary: {passed}/{total} checks passed")
        for r in self.results:
            status = "PASS" if r['passed'] else "FAIL"
            print(f"  [{status}] {r['check']}")
            for issue in r['issues']:
                print(f"       - {issue}")

if __name__ == "__main__":
    checker = ComplianceChecker()
    checker.run_all()
```

### Phase 6: Report Generation Automation

```python
#!/usr/bin/env python3
"""
Automated report generation from scan results.
"""
from jinja2 import Template
from datetime import datetime
from pathlib import Path
import json

REPORT_TEMPLATE = """# Security Scan Report

**Generated**: {{ timestamp }}
**Target**: {{ target }}

## Executive Summary

Total findings: **{{ findings|length }}**

| Severity | Count |
|----------|-------|
{% for sev, count in severity_counts.items() -%}
| {{ sev }} | {{ count }} |
{% endfor %}

## Detailed Findings

{% for finding in findings %}
### {{ loop.index }}. {{ finding.title }}
- **Severity**: {{ finding.severity }}
- **URL**: `{{ finding.url }}`
- **Description**: {{ finding.description }}

{% endfor %}

---
*Report generated by automated security pipeline*
"""

def generate_report(target, findings_file, output_file="report.md"):
    """Generate a markdown report from findings JSON."""
    findings = json.loads(Path(findings_file).read_text())
    severity_counts = {}
    for f in findings:
        sev = f.get('severity', 'Unknown')
        severity_counts[sev] = severity_counts.get(sev, 0) + 1

    template = Template(REPORT_TEMPLATE)
    report = template.render(
        timestamp=datetime.now().isoformat(),
        target=target,
        findings=findings,
        severity_counts=severity_counts
    )
    Path(output_file).write_text(report)
    print(f"[+] Report generated: {output_file}")

if __name__ == "__main__":
    import sys
    if len(sys.argv) < 3:
        print("Usage: python report_gen.py <target> <findings.json>")
        sys.exit(1)
    generate_report(sys.argv[1], sys.argv[2])
```

## Templates

### Project Structure Template

```
security-automation/
├── .github/
│   └── workflows/
│       └── security-scan.yml
├── scripts/
│   ├── recon_pipeline.py
│   ├── web_scanner.py
│   ├── compliance_checker.py
│   ├── report_gen.py
│   └── notification.py
├── templates/
│   ├── nuclei/
│   │   ├── custom-cves.yaml
│   │   └── company-specific.yaml
│   └── reports/
│       └── report_template.md
├── configs/
│   ├── nuclei.yaml
│   ├── ffuf.yaml
│   └── targets.yaml
├── reports/
│   └── .gitkeep
├── requirements.txt
├── Makefile
└── README.md
```

### Makefile Template

```makefile
.PHONY: scan report clean

scan:
	@echo "[*] Running full security scan..."
	python scripts/recon_pipeline.py $(TARGET)
	python scripts/web_scanner.py $(TARGET)

report:
	@echo "[*] Generating report..."
	python scripts/report_gen.py $(TARGET) reports/findings.json

compliance:
	@echo "[*] Running compliance checks..."
	python scripts/compliance_checker.py

clean:
	rm -rf reports/*
```

## Common Pitfalls

- **Hardcoded credentials in scripts** — Never embed API keys, passwords, or tokens in scripts. Use environment variables or secret management tools.
- **No error handling** — Security tools fail for many reasons (network errors, rate limits, authentication). Always implement try/except and retry logic.
- **Overwhelming the target** — Automated tools can generate massive request volumes. Implement rate limiting and respect `robots.txt`.
- **Not logging automation runs** — Every automation run should produce a log with timestamps, inputs, and outputs for audit purposes.
- **Ignoring false positives** — Automated tools produce false positives. Always include a manual review step or a triage mechanism.
- **No version control for scripts** — Treat automation scripts as code. Version control them, review changes, and test before deploying.
- **Brittle parsing** — Do not parse tool output with fragile string splitting. Use JSON output when available, or structured parsers.
- **Not handling authentication** — Many real-world targets require authentication. Design scripts to support session tokens, cookies, and OAuth flows.

## Legal Considerations

- **Authorization for Automation**: Automated scanning generates more traffic than manual testing. Ensure your authorization covers automated tools.
- **Rate Limiting**: Automated tools can cause denial of service. Implement rate limiting in all scripts.
- **Data Handling**: Automation may discover sensitive data. Ensure proper data handling and retention policies.
- **Third-Party API Usage**: Tools like Shodan, Censys, and VirusTotal have rate limits and terms of service. Respect them.
- **CI/CD Secrets**: Storing API keys and credentials in CI/CD pipelines requires proper secret management. Never commit secrets to version control.
- **Scheduled Scanning**: Automated scheduled scans should be coordinated with the operations team to avoid false incident alerts.
- **Attribution**: Automated scans from your infrastructure are attributable to you. Use designated testing infrastructure.

## Further Reading

- [OWASP DevSecOps Guideline](https://owasp.org/www-project-devsecops-guideline/)
- [NIST SP 800-53 Security Controls (Automation)](https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final)
- [GitHub Actions Security Hardening](https://docs.github.com/en/actions/security-guides)
- [Nuclei Template Writing Guide](https://nuclei.projectdiscovery.io/templating-guide/)
- [Python Security Tools (Awesome List)](https://github.com/guardicore/awesome-security-tools)
- [SecLists (Wordlists)](https://github.com/danielmiessler/SecLists)

---

## 中文版本

### 使用场景

- 自动化重复性安全测试任务
- 构建持续安全测试流水线
- 为特定技术栈创建自定义漏洞扫描器
- 自动化合规检查和配置审计
- 构建事件响应自动化（检测、分类、遏制）
- 编排多个安全工具为统一工作流
- 为 Bug Bounty 或渗透测试自动化侦察
- 创建安全仪表盘和报告自动化
- 实施 DevSecOps 左移安全检查

### 核心步骤

1. **环境搭建**：创建专用目录结构（scripts/templates/reports/configs），配置 Python 虚拟环境，安装 Go 工具链（nuclei、httpx、subfinder、ffuf）。
2. **自动化侦察流水线**：编写 Python 类串联子域名枚举（subfinder + crt.sh）、存活主机探测（httpx）、漏洞扫描（nuclei），一键执行完整侦察流程。
3. **自动化 Web 漏洞扫描器**：编写自定义扫描器检查安全 Header 缺失、目录列表、信息泄露（服务器版本、错误页面堆栈跟踪）。
4. **CI/CD 安全流水线**：在 GitHub Actions 中集成依赖扫描（Trivy）、SAST（Semgrep）、容器镜像扫描、密钥泄露检测（Gitleaks）、IaC 扫描（Checkov）。
5. **合规自动化**：编写合规检查器验证 SSH 加固、防火墙配置等安全基线，输出通过/失败摘要。
6. **报告生成自动化**：使用 Jinja2 模板从扫描结果 JSON 自动生成 Markdown 报告。

### 模板说明

- **项目结构模板**：标准目录布局——scripts/（自定义脚本）、templates/（Nuclei 模板、报告模板）、configs/（工具配置）、pipelines/（CI/CD 定义）。
- **Makefile 模板**：封装常用操作——`make scan`（完整扫描）、`make report`（生成报告）、`make compliance`（合规检查）、`make clean`（清理报告）。
- **CI/CD Pipeline 模板**：完整的 GitHub Actions 配置，包含依赖扫描、SAST、容器扫描、密钥检测和 IaC 扫描五个并行 Job。

### 常见陷阱

- **脚本中硬编码凭据** — 绝不要在脚本中嵌入 API Key、密码或 token，使用环境变量或密钥管理工具。
- **缺少错误处理** — 安全工具会因各种原因失败（网络错误、速率限制、认证），必须实现 try/except 和重试逻辑。
- **对目标发包过量** — 自动化工具可产生海量请求，应实施速率限制并遵守 `robots.txt`。
- **不记录自动化运行日志** — 每次运行应产生包含时间戳、输入和输出的日志，用于审计追踪。
- **忽略误报** — 自动化工具会产生误报，必须包含人工审查步骤或分类机制。
- **脚本不做版本控制** — 自动化脚本应视同代码，纳入版本控制、代码审查和测试。
- **脆弱的输出解析** — 不要用脆弱的字符串分割解析工具输出，优先使用 JSON 输出或结构化解析器。
- **不处理认证** — 很多真实目标需要认证，脚本应支持 session token、Cookie 和 OAuth 流程。
