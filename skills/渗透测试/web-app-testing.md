# Web Application Penetration Testing Skill

> Conduct systematic web application penetration tests following industry-standard methodologies (OWASP, PTES, NIST).

## When to Use

- Performing an authorized penetration test on a web application
- Validating the effectiveness of security controls
- Assessing a web application before launch or after a major update
- Conducting a red team exercise targeting web infrastructure
- Testing compliance with PCI-DSS Requirement 11.3
- Bug bounty hunting on authorized programs
- Post-incident assessment to determine attack scope
- Training security team members on web testing methodology

## Prerequisites

- Signed Rules of Engagement (RoE) and authorization letter
- Access to the target application (credentials if testing authenticated flows)
- Proxy tool configured (Burp Suite or OWASP ZAP)
- Testing environment that mirrors production (preferred)
- Familiarity with HTTP protocol, web technologies, and common vulnerabilities

## Tools

| Tool | Purpose | License |
|------|---------|---------|
| Burp Suite | Intercepting proxy, scanner, and repeater | Community / Pro |
| OWASP ZAP | Open-source web application scanner | Apache-2.0 |
| SQLMap | Automated SQL injection exploitation | GPL |
| Nuclei | Template-based vulnerability scanning | MIT |
| ffuf | Fast web fuzzer for directories and parameters | MIT |
| Commix | Automated command injection exploitation | GPL |
| XSStrike | Advanced XSS detection | GPL |
| Arjun | Hidden parameter discovery | MIT |
| WPScan | WordPress vulnerability scanner | GPL |
| Feroxbuster | Recursive content discovery | MIT |

## Step-by-Step Procedure

### Phase 1: Setup and Proxy Configuration

1. **Configure Burp Suite**:
   - Set up the upstream proxy and CA certificate in the browser.
   - Configure scope to include only in-scope domains.
   - Enable all scan checks for the active scanner.
   - Set up Burp Collaborator for out-of-band testing.
2. **Map the application**:
   - Browse the application manually through the proxy.
   - Spider/crawl all reachable pages.
   - Import OpenAPI/Swagger definitions if available.
   - Record all endpoints, parameters, and HTTP methods.
3. **Identify technology fingerprint**:
   - Server headers, framework artifacts, JavaScript libraries.
   - Check `robots.txt`, `sitemap.xml`, `.well-known/`, `security.txt`.

### Phase 2: Automated Scanning

1. **Run Nuclei with complete templates**:
   ```bash
   nuclei -u https://target.com -t cves/ -t vulnerabilities/ -t misconfigurations/ \
     -severity critical,high,medium -o nuclei_results.txt
   ```
2. **Run Burp Suite active scan** on discovered endpoints.
3. **Run directory brute force**:
   ```bash
   ffuf -u https://target.com/FUZZ -w /usr/share/seclists/Discovery/Web-Content/common.txt \
     -mc 200,301,302,403 -o ffuf_dirs.json -of json
   ```
4. **Discover hidden parameters**:
   ```bash
   arjun -u https://target.com/api/endpoint
   ```
5. **Run CMS-specific scanners** if a CMS is detected:
   ```bash
   # WordPress
   wpscan --url https://target.com --enumerate vp,vt,u --api-token YOUR_TOKEN
   ```

### Phase 3: Manual Testing — Injection Attacks

#### 3.1 SQL Injection

- Test all input parameters: URL params, form fields, cookies, headers.
- Use single quotes, double quotes, boolean logic (`AND 1=1`, `AND 1=2`).
- Test for blind SQLi with time delays: `' OR SLEEP(5)--`
- Use SQLMap for automated detection:
  ```bash
  sqlmap -u "https://target.com/page?id=1" --batch --risk=3 --level=5
  sqlmap -r request.txt --batch --dbs  # From saved Burp request
  ```
- Test for second-order SQLi (stored data used in queries later).
- Check for SQLi in ORDER BY and GROUP BY clauses.

#### 3.2 Cross-Site Scripting (XSS)

- Test all input points for reflected XSS:
  ```html
  <script>alert('XSS')</script>
  <img src=x onerror=alert('XSS')>
  <svg/onload=alert('XSS')>
  javascript:alert('XSS')
  ```
- Test for stored XSS by submitting payloads and revisiting the page.
- Test for DOM-based XSS by analyzing JavaScript source for dangerous sinks:
  ```javascript
  document.write()
  innerHTML
  eval()
  location.href
  ```
- Use XSStrike for advanced detection:
  ```bash
  xsstrike -u "https://target.com/search?q=test"
  ```
- Test filter bypass techniques: encoding, case variation, nested tags, event handlers.

#### 3.3 Command Injection

- Test with command separators: `;`, `|`, `||`, `&&`, `` ` ``, `$()`
- Basic payloads: `; ls`, `| whoami`, `$(id)`, `` `cat /etc/passwd` ``
- Use Commix for automated testing:
  ```bash
  commix -u "https://target.com/ping?host=127.0.0.1"
  ```
- Test blind command injection with time delays and out-of-band callbacks.

#### 3.4 Server-Side Template Injection (SSTI)

- Test with template expressions: `{{7*7}}`, `${7*7}`, `<%= 7*7 %>`
- If `49` is returned, template injection is confirmed.
- Use tplmap for exploitation:
  ```bash
  tplmap -u "https://target.com/greeting?name=test"
  ```

#### 3.5 Server-Side Request Forgery (SSRF)

- Test URL parameters with internal addresses:
  - `http://127.0.0.1`, `http://localhost`, `http://[::1]`
  - `http://169.254.169.254` (AWS metadata)
  - `http://metadata.google.internal` (GCP metadata)
- Use Burp Collaborator or interactsh for blind SSRF detection.
- Test for DNS rebinding and URL parsing inconsistencies.

### Phase 4: Manual Testing — Authentication and Session

1. **Test authentication bypass**:
   - Remove authentication headers/cookies and access protected endpoints.
   - Modify JWT tokens (change user ID, role claims).
   - Test for default credentials on admin panels.
2. **Session management testing**:
   - Check if session ID changes after login (fixation).
   - Test session timeout (idle and absolute).
   - Verify logout invalidates the session server-side.
3. **Password reset testing**:
   - Test for user enumeration in reset flow.
   - Analyze reset token for predictability.
   - Check if tokens expire and are single-use.

### Phase 5: Manual Testing — Access Control

1. **IDOR Testing**:
   - Change resource IDs in URLs and API calls.
   - Test with different user accounts (horizontal privilege escalation).
   - Test admin endpoints with regular user tokens (vertical privilege escalation).
2. **Function-level access control**:
   - Access admin API endpoints directly (bypass UI restrictions).
   - Test HTTP method override headers (`X-HTTP-Method-Override`).
3. **Multi-step process testing**:
   - Skip steps in multi-step workflows.
   - Modify data between steps.
   - Replay completed steps with modified data.

### Phase 6: Manual Testing — Client-Side

1. **CORS testing**:
   - Test with `Origin: https://evil.com` header.
   - Check if `Access-Control-Allow-Origin` reflects arbitrary origins.
   - Verify `Access-Control-Allow-Credentials` is not set with wildcard origin.
2. **Clickjacking**:
   - Check if the application can be framed (`X-Frame-Options`, `Content-Security-Policy: frame-ancestors`).
   - Test by creating an iframe embedding.
3. **Sensitive data exposure**:
   - Check for sensitive data in JavaScript source, HTML comments, and hidden fields.
   - Test for information disclosure in error messages and HTTP headers.
   - Verify cache headers on sensitive pages (`Cache-Control: no-store`).

### Phase 7: Exploitation and Impact Verification

1. For critical findings, develop a proof of concept that demonstrates real impact.
2. **Never cause real damage**: proof of concept should demonstrate access, not destroy data.
3. Document the full attack chain: entry point → exploitation → impact.
4. Test if vulnerabilities can be chained for greater impact (e.g., XSS + CSRF = account takeover).

## Templates

### Penetration Test Finding Template

```markdown
## Finding: [Title]

### Metadata
- **ID**: VULN-001
- **Severity**: Critical / High / Medium / Low / Informational
- **CVSS Score**: X.X (Vector: CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H)
- **CWE**: CWE-XXX
- **OWASP Category**: A0X:2021
- **Status**: Open
- **Discovered**: YYYY-MM-DD

### Affected Asset
- **URL**: `https://target.com/api/v1/users/{id}`
- **Parameter**: `id` (path parameter)
- **Method**: GET

### Description
[Clear description of the vulnerability and its root cause]

### Proof of Concept
**Request (as User A, ID=100):**
```http
GET /api/v1/users/200 HTTP/1.1
Host: target.com
Authorization: Bearer eyJ...[User A token]
```

**Response:**
```json
{
  "id": 200,
  "email": "userb@target.com",
  "ssn": "123-45-6789"
}
```

### Impact
[What can an attacker achieve? Data breach, account takeover, financial loss, etc.]

### Remediation
1. [Specific fix step 1]
2. [Specific fix step 2]
3. [Verification step]

### References
- OWASP: [Link]
- CWE: [Link]
- CVE: [Link if applicable]
```

### Testing Checklist

| Phase | Test | Done | Finding |
|-------|------|------|---------|
| Injection | SQL Injection | ☐ | |
| Injection | XSS (Reflected) | ☐ | |
| Injection | XSS (Stored) | ☐ | |
| Injection | Command Injection | ☐ | |
| Injection | SSTI | ☐ | |
| Injection | SSRF | ☐ | |
| Auth | Auth Bypass | ☐ | |
| Auth | Session Fixation | ☐ | |
| Auth | Password Reset | ☐ | |
| Access | IDOR | ☐ | |
| Access | Privilege Escalation | ☐ | |
| Client | CORS Misconfiguration | ☐ | |
| Client | Clickjacking | ☐ | |
| Info | Error Disclosure | ☐ | |
| Info | Directory Listing | ☐ | |

## Common Pitfalls

- **Relying solely on automated scanners** — Automated tools catch maybe 30-40% of web vulnerabilities. Manual testing is essential.
- **Not testing authenticated areas** — Many vulnerabilities only appear behind authentication. Always test with appropriate user roles.
- **Testing only GET parameters** — POST body, cookies, headers, and HTTP methods are equally important attack surfaces.
- **Causing service disruption** — Aggressive fuzzing and exploitation can crash services. Monitor the target during testing.
- **Not capturing evidence** — Screenshot and record every finding as you discover it. Reproducing issues later may be impossible.
- **Skipping business logic testing** — Automated tools cannot find logic flaws like price manipulation, race conditions in purchasing, or step-skipping in workflows.
- **Not testing error handling** — Sending malformed inputs often reveals stack traces, debug endpoints, and information disclosure.

## Legal Considerations

- **Authorization**: Only test applications with explicit written authorization. The scope document must list all in-scope URLs and IP ranges.
- **Scope Adherence**: Stay within the defined scope. Discovering and testing out-of-scope assets without permission is unauthorized access.
- **Data Handling**: If you access real user data during testing, report it immediately. Do not store, copy, or exfiltrate it.
- **Denial of Service**: Avoid DoS conditions. Use controlled fuzzing rates and monitor application health.
- **Third-Party Services**: If the application uses third-party APIs, do not test those APIs unless explicitly authorized.
- **Disclosure Timeline**: Follow the agreed disclosure timeline (typically 90 days). Do not publish findings publicly without the client's consent.
- **Evidence Security**: Encrypt and securely store all test evidence. Destroy it after the engagement per the contract terms.

## Further Reading

- [OWASP Web Security Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [PortSwigger Web Security Academy](https://portswigger.net/web-security)
- [PTES: Web Application Testing](http://www.pentest-standard.org/index.php/Web_Application_Testing)
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/)
- [HackTricks Web](https://book.hacktricks.xyz/pentesting-web/)
- [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings)

---

## 中文版本

### 使用场景

- 对 Web 应用进行授权渗透测试
- 验证安全控制措施的有效性
- 应用上线前或重大更新后的安全评估
- 红队演练中针对 Web 基础设施的测试
- PCI-DSS Requirement 11.3 合规测试
- 授权 Bug Bounty 项目的漏洞猎捕
- 安全事件后评估攻击范围

### 核心步骤

1. **环境配置**：配置 Burp Suite 代理和浏览器 CA 证书，设置测试范围，手动浏览应用并记录所有端点和技术栈。
2. **自动化扫描**：使用 Nuclei 模板扫描、Burp Suite 主动扫描、目录爆破（ffuf）、隐藏参数发现（Arjun）、CMS 专用扫描器（WPScan）。
3. **手动注入测试**：SQL 注入（单引号、布尔逻辑、时间盲注、SQLMap）、XSS（反射/存储/DOM）、命令注入（Commix）、SSTI（`{{7*7}}`）、SSRF（内部地址、云元数据）。
4. **认证与会话测试**：认证绕过、Session fixation、密码重置流程安全。
5. **访问控制测试**：IDOR、权限提升（垂直/水平）、多步骤流程跳步。
6. **客户端测试**：CORS 配置、Clickjacking、敏感数据暴露。
7. **利用与影响验证**：为关键发现编写 PoC，验证漏洞链可组合性（如 XSS + CSRF = 账户接管）。

### 模板说明

- **渗透测试发现模板**：标准化格式，包含元数据（ID、CVSS、CWE、OWASP）、受影响资产、漏洞描述、PoC 请求/响应、影响分析、分阶段修复方案和参考链接。
- **测试检查清单**：涵盖注入、认证、访问控制、客户端和信息泄露五大类测试项。

### 常见陷阱

- **仅依赖自动化扫描器** — 自动化工具大概只能发现 30-40% 的 Web 漏洞，手动测试必不可少。
- **不测试认证区域** — 很多漏洞只在认证后出现，必须使用适当角色测试。
- **只测试 GET 参数** — POST body、Cookie、Header 和 HTTP 方法同样是重要攻击面。
- **造成服务中断** — 激进的 fuzzing 和利用可能导致服务崩溃，测试期间应监控目标状态。
- **不捕获证据** — 发现漏洞时立即截图和记录，事后复现可能不可能。
- **跳过业务逻辑测试** — 自动化工具无法发现价格篡改、购买竞态条件等逻辑缺陷。
- **不测试错误处理** — 发送畸形输入常会暴露堆栈跟踪、调试端点和信息泄露。
