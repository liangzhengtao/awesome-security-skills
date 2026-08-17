# Burp Suite Mastery Skill

> Master Burp Suite for web application security testing — from basic proxy interception to advanced scanning, fuzzing, and extension development.

## When to Use

- Setting up a web application testing environment
- Intercepting and modifying HTTP/HTTPS traffic during a pentest
- Automating vulnerability scanning against web targets
- Fuzzing parameters for injection, XSS, and logic flaws
- Analyzing and attacking authentication and session mechanisms
- Developing custom Burp extensions for specialized testing
- Training new security testers on industry-standard tooling
- Replaying and modifying requests during vulnerability analysis

## Prerequisites

- Burp Suite installed (Community or Professional)
- Browser configured with Burp's CA certificate and proxy settings
- Basic understanding of HTTP/HTTPS protocol
- Familiarity with at least one web vulnerability class (XSS, SQLi, etc.)
- Java runtime environment (if using Burp Suite Classic)

## Tools and Extensions

| Extension | Purpose | Free/Paid |
|-----------|---------|-----------|
| Autorize | Automated authorization testing | Free |
| Logger++ | Advanced HTTP logging and filtering | Free |
| Active Scan++ | Enhanced active scan checks | Free |
| Turbo Intruder | High-speed fuzzing with custom Python scripts | Free |
| Param Miner | Hidden parameter discovery | Free |
| Collaborator Everywhere | Inject Collaborator payloads in all requests | Free |
| JSON Web Tokens (JWT) | JWT inspection, editing, and attacks | Free |
| Hackvertor | Advanced encoding/decoding transformations | Free |
| SAML Raider | SAML assertion manipulation | Free |
| Upload Scanner | File upload vulnerability testing | Free |
| Retire.js | Detect vulnerable JavaScript libraries | Free |

## Step-by-Step Procedure

### Phase 1: Initial Setup and Configuration

#### 1.1 Project Configuration

1. **Create a new project** for each engagement:
   - Temporary project (Community) or saved project file (Professional).
   - Name the project with the client and date for organization.
2. **Configure upstream proxy** if behind a corporate proxy:
   - Project Options → Connections → Upstream Proxy Servers.
3. **Set scope** to include only authorized targets:
   - Target → Scope → Add target host/URL prefix.
   - Enable "Use advanced scope control" for fine-grained filtering.
4. **Configure SSL/TLS**:
   - Project Options → TLS → Enable TLS 1.0 if testing legacy systems.
   - Add client certificates if required by the target.

#### 1.2 Browser Setup

1. Install FoxyProxy (Firefox) or Proxy SwitchyOmega (Chrome).
2. Configure proxy: `127.0.0.1:8080`.
3. Install Burp's CA certificate:
   - Browse to `http://burp`.
   - Download `cacert.der`.
   - Import into browser certificate store as a trusted CA.
4. Verify interception: the browser should load pages normally with Burp running.

### Phase 2: Proxy and Traffic Analysis

#### 2.1 Intercepting Requests

1. **Proxy → Intercept**: Toggle "Intercept is on" to pause requests.
2. **Modify requests in-flight**:
   - Edit headers, parameters, cookies, and body before forwarding.
   - Drop requests to test error handling.
3. **Use action menu** to send requests to other Burp tools:
   - Send to Repeater (manual testing).
   - Send to Intruder (automated fuzzing).
   - Send to Scanner (vulnerability scanning).
   - Send to Comparer (diff analysis).

#### 2.2 HTTP History Analysis

1. **Proxy → HTTP history**: Review all captured traffic.
2. **Filter by**:
   - Scope (only in-scope items).
   - MIME type (HTML, JSON, JS, CSS).
   - Status code (focus on 200, 302, 403, 500).
   - Search string (find specific parameters or values).
3. **Use Logger++** for advanced filtering and regex-based searches.

### Phase 3: Manual Testing with Repeater

1. **Send a request to Repeater** from HTTP history or intercept.
2. **Modify and resend**:
   - Change parameter values to test injection.
   - Add/remove headers to test authorization.
   - Modify cookies and tokens to test session management.
3. **Compare responses**: Look at status code, length, content, and timing differences.
4. **Use tabs** to organize different test cases side by side.

#### Key Repeater Techniques

- **SQL Injection Testing**:
  ```
  ' OR 1=1--
  ' UNION SELECT null,null,null--
  ' AND SLEEP(5)--
  ```
- **XSS Testing**:
  ```
  <script>alert(document.domain)</script>
  <img src=x onerror=alert(1)>
  "><svg/onload=alert(1)>
  ```
- **IDOR Testing**:
  ```
  Change /api/users/100 to /api/users/101
  Change user_id=100 to user_id=101 in POST body
  ```

### Phase 4: Automated Scanning

#### 4.1 Active Scanning (Professional)

1. Right-click a request → **Do active scan**.
2. Configure scan settings:
   - **Scan configuration**: Choose audit checks (injection, XSS, CSRF, etc.).
   - **Application login**: Configure credentials for authenticated scanning.
   - **Resource pool**: Set throttling to avoid overwhelming the target.
3. Review results in **Dashboard → Scan results**.
4. **Verify findings manually**: False positives are common in automated scanning.

#### 4.2 Passive Scanning

1. Passive scanning runs automatically on all proxied traffic.
2. Review findings in **Dashboard → Issue activity**.
3. Common passive findings:
   - Missing security headers.
   - Cookie without `Secure`/`HttpOnly` flags.
   - Information disclosure in headers or error messages.
   - Sensitive data in URL parameters.

### Phase 5: Intruder (Fuzzing)

#### 5.1 Attack Types

| Type | Use Case |
|------|----------|
| Sniper | Single position, one payload set (parameter fuzzing) |
| Battering Ram | Single payload set, all positions simultaneously |
| Pitchfork | Multiple payload sets, paired iteration |
| Cluster Bomb | Multiple payload sets, all combinations (credential testing) |

#### 5.2 Common Intruder Tasks

**Directory brute force**:
1. Set position: `GET /§FUZZ§ HTTP/1.1`
2. Load wordlist: SecLists `common.txt`
3. Filter by response length to identify valid directories.

**Credential brute force**:
1. Set positions on username and password fields.
2. Attack type: Cluster bomb.
3. Load username and password wordlists.
4. Filter by status code or response length to identify valid credentials.

**Parameter fuzzing for injection**:
1. Set position on the target parameter.
2. Load payloads: SQL injection, XSS, SSTI, command injection strings.
3. Grep match: Error strings, reflection, timing delays.
4. Use Grep Extract to pull specific data from responses.

#### 5.3 Turbo Intruder (Advanced)

For high-speed fuzzing with custom logic:

```python
# Turbo Intruder script example
def queueRequests(target, wordlists):
    engine = RequestEngine(endpoint=target.endpoint,
                           concurrentConnections=10,
                           requestsPerConnection=100,
                           pipeline=False)
    
    for word in open('/usr/share/seclists/Usernames/top-usernames-shortlist.txt'):
        engine.queue(target.req, word.strip())

def handleResponse(req, interesting):
    if '200' in req.response and 'Welcome' in req.response:
        table.add(req)
```

### Phase 6: Authorization Testing with Autorize

1. Install the Autorize extension.
2. **Configure low-privilege session**: Login as a regular user, send a request to Autorize.
3. **Configure high-privilege session**: Copy the admin user's cookies/headers.
4. **Browse the application as the admin user** while Autorize intercepts.
5. Autorize automatically replays each request with the low-privilege session.
6. **Review results**:
   - **Bypassed**: Response is identical (authorization bypass confirmed).
   - **Enforced**: Response differs (authorization working correctly).
   - **Partial**: Response partially differs (needs manual verification).

### Phase 7: Collaborator for Out-of-Band Testing

1. **Burp Collaborator** provides a unique domain for detecting blind vulnerabilities.
2. **Use cases**:
   - Blind SQL injection: `'; EXEC xp_dirtree('//YOUR.burpcollaborator.net')--`
   - Blind XSS: `<script src=https://YOUR.burpcollaborator.net></script>`
   - SSRF: `http://YOUR.burpcollaborator.net`
   - XXE: `<!ENTITY xxe SYSTEM "http://YOUR.burpcollaborator.net">`
3. **Poll for interactions** in Dashboard → Collaborator.
4. **Use Collaborator Everywhere** extension to automatically inject Collaborator payloads.

### Phase 8: Custom Extension Development

```python
# Simple Burp extension (Jython) that highlights responses containing "admin"
from burp import IBurpExtender, IHttpListener

class BurpExtender(IBurpExtender, IHttpListener):
    def registerExtenderCallbacks(self, callbacks):
        self._callbacks = callbacks
        self._helpers = callbacks.getHelpers()
        callbacks.setExtensionName("Admin Detector")
        callbacks.registerHttpListener(self)
        print("[+] Admin Detector loaded")

    def processHttpMessage(self, toolFlag, messageIsRequest, messageInfo):
        if not messageIsRequest:
            response = messageInfo.getResponse()
            analyzed = self._helpers.analyzeResponse(response)
            body = response[analyzed.getBodyOffset():]
            if "admin" in self._helpers.bytesToString(body).lower():
                messageInfo.setHighlight("red")
                print("[!] Admin content detected in response")
```

## Templates

### Burp Suite Testing Workflow

```markdown
## Burp Suite Testing Workflow

### Pre-Test
- [ ] New project created
- [ ] Scope configured
- [ ] Browser proxy configured
- [ ] CA certificate installed
- [ ] Extensions loaded (Autorize, Logger++, Param Miner)

### Active Testing
- [ ] Application mapped (spider/crawl)
- [ ] Authentication flows recorded
- [ ] Intruder attacks configured
- [ ] Active scan launched
- [ ] Authorization testing (Autorize) running
- [ ] Collaborator payloads deployed

### Post-Test
- [ ] All findings verified manually
- [ ] Evidence collected and organized
- [ ] Scan results exported
- [ ] Project saved or backed up
```

### Burp Suite Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+Shift+R` | Send to Repeater |
| `Ctrl+Shift+I` | Send to Intruder |
| `Ctrl+Shift+D` | Send to Decoder |
| `Ctrl+Shift+C` | Copy as curl command |
| `Ctrl+F` | Search in current view |
| `Ctrl+Shift+F` | Search all items |
| `Space` | Forward intercepted request |
| `Ctrl+F` | Toggle intercept on/off |

## Common Pitfalls

- **Not setting scope** — Without scope, you will capture traffic to all websites, including out-of-scope targets. Always set scope first.
- **Trusting automated scan results** — Burp's scanner produces false positives. Always verify manually.
- **Overwhelming the target** — Default scan and Intruder settings can send thousands of requests. Throttle the request rate.
- **Not saving the project** — Lost Burp sessions cannot be recovered. Save the project regularly or use auto-save.
- **Forgetting to test authenticated areas** — Configure application login settings to maintain authenticated sessions during scanning.
- **Ignoring passive findings** — Passive scanner findings are easy wins. Address missing headers, cookie flags, and information disclosure first.
- **Not using extensions** — Burp's extensions dramatically expand capabilities. Autorize alone saves hours of authorization testing.

## Legal Considerations

- **Authorization**: Only use Burp Suite against applications you own or have explicit written permission to test.
- **Intercepting Third-Party Traffic**: Configuring Burp as a proxy captures all browser traffic. Be aware of what flows through the proxy.
- **Brute Force Testing**: Can lock out accounts and trigger incident response. Coordinate with the client.
- **Data in Proxy Logs**: Burp stores all request/response data, including credentials and PII. Encrypt project files and restrict access.
- **Burp Collaborator**: Uses an external service (PortSwigger's server or a private instance). Be aware of data leaving the testing environment.
- **Professional vs. Community**: The Professional license has specific terms of use. Ensure your license type matches your use case.

## Further Reading

- [PortSwigger Documentation](https://portswigger.net/burp/documentation)
- [PortSwigger Web Security Academy](https://portswigger.net/web-security)
- [Burp Suite Extensions Store](https://portswigger.net/burp/extensions)
- [HackTricks: Burp Suite](https://book.hacktricks.xyz/generic-methodologies-and-resources/external-recon-methodology/burp-suite)
- [SANS: Burp Suite Tips and Tricks](https://www.sans.org/)
- [Burp Suite Unleashed (PortSwigger Blog)](https://portswigger.net/blog)
