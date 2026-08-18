# Authentication and Authorization Security Skill

> Assess, implement, and harden authentication and authorization mechanisms across web applications, APIs, and services.

## When to Use

- Designing authentication flows for a new application
- Auditing existing login, SSO, and MFA implementations
- Investigating account takeover incidents
- Implementing OAuth 2.0 / OpenID Connect for a platform
- Reviewing session management and token lifecycle
- Migrating from legacy authentication (basic auth, custom tokens) to modern standards
- Evaluating passwordless authentication options (WebAuthn, FIDO2)
- Preparing for compliance audits (PCI-DSS Requirement 8, NIST 800-63B)

## Prerequisites

- Understanding of HTTP authentication mechanisms (cookies, headers, tokens)
- Knowledge of cryptographic hashing and salting principles
- Familiarity with at least one identity provider (Keycloak, Auth0, Azure AD)
- Access to the application source code or a test environment (authorized)

## Tools

| Tool | Purpose | License |
|------|---------|---------|
| Burp Suite | Intercepting and modifying auth flows | Community / Pro |
| Hydra / Medusa | Credential brute-force testing | GPL |
| jwt_tool | JWT analysis, forging, and cracking | MIT |
| Hashcat / John the Ripper | Password hash cracking | MIT / GPL |
| Authoscope | Custom auth testing automation | Apache-2.0 |
| OWASP ASVS | Authentication verification standard | CC-BY-SA-4.0 |

## Step-by-Step Procedure

### Phase 1: Authentication Flow Mapping

1. Document every authentication mechanism in the application:
   - Username/password login forms
   - SSO (SAML, OIDC)
   - API keys and bearer tokens
   - Session cookies
   - Passwordless (magic links, WebAuthn)
2. Map the complete login flow using an intercepting proxy:
   - Client → Identity Provider → Token/Session issuance → Resource access
3. Identify all token types: JWT, opaque tokens, session IDs.
4. Document token storage location (cookies, localStorage, sessionStorage).
5. Record token lifetime, refresh mechanism, and revocation strategy.

### Phase 2: Password Security Assessment

#### Storage Verification

- Confirm passwords are hashed with bcrypt, scrypt, or Argon2id.
- Verify salt is unique per user and sufficiently random (≥ 16 bytes).
- Reject weak algorithms: MD5, SHA-1, SHA-256 without salt.
- Check password policy: minimum length (≥ 12), complexity requirements aligned with NIST 800-63B.

#### Login Flow Testing

- Test for username enumeration via:
  - Different error messages ("user not found" vs "incorrect password").
  - Response timing differences.
  - Account lockout behavior differences.
- Test brute force resistance:
  - Is there account lockout after N failed attempts?
  - Is there progressive delay or CAPTCHA?
  - Can rate limiting be bypassed via IP rotation or header manipulation?
- Test for credential stuffing resistance (check against breach databases).

#### Password Reset Flow

- Verify reset tokens are cryptographically random (≥ 128 bits of entropy).
- Check token expiration (should be ≤ 1 hour).
- Verify tokens are single-use and invalidated after use.
- Test for user enumeration in reset flow.
- Check if old password is required for reset (or if email-only reset is too easy).
- Verify that reset tokens are not leaked in URL parameters or referrer headers.

### Phase 3: Session Management

1. **Session ID Analysis**:
   - Session IDs must be cryptographically random (≥ 128 bits).
   - Test for session fixation: does the ID change after login?
   - Verify session IDs are not predictable or sequential.

2. **Cookie Security**:
   - `Secure` flag is set (HTTPS only).
   - `HttpOnly` flag is set (no JavaScript access).
   - `SameSite` attribute is `Lax` or `Strict`.
   - `Path` scope is appropriately restrictive.
   - `Domain` scope does not allow subdomain access.

3. **Session Lifecycle**:
   - Session timeout is enforced (idle timeout ≤ 30 minutes for sensitive apps).
   - Absolute session timeout exists (≤ 8 hours).
   - Session is invalidated server-side on logout.
   - Concurrent session limits are enforced for sensitive accounts.

### Phase 4: Token Security (JWT / OAuth 2.0)

#### JWT Assessment

- Verify the `alg` header is not `none`.
- Test algorithm confusion attacks (RS256 → HS256).
- Verify the signing key has sufficient entropy (≥ 256 bits for symmetric).
- Check that `exp`, `iat`, `nbf`, `aud`, `iss` claims are validated.
- Test for JWT token reuse after password change or logout.
- Verify tokens are not stored in URL parameters.

#### OAuth 2.0 / OIDC Assessment

- Verify `state` parameter is used, random, and bound to the user session.
- Check redirect URI validation (must be exact match, not pattern-based).
- Test for authorization code interception.
- Verify PKCE (`code_challenge`) is used for public clients.
- Check for token leakage in browser history, referrer headers, or logs.
- Verify `nonce` claim is used and validated in ID tokens.

### Phase 5: Multi-Factor Authentication

1. Verify MFA is enforced for privileged accounts.
2. Test MFA bypass:
   - Can users skip MFA by directly accessing API endpoints?
   - Is MFA enforced on all authentication paths (web, API, SSO)?
   - Can MFA be disabled without re-authenticating?
3. Test TOTP implementation:
   - Is the shared secret sufficiently random?
   - Is the time window reasonable (30 seconds, ±1 step)?
   - Are replay attacks prevented?
4. Test backup/recovery codes:
   - Are they hashed before storage?
   - Are they single-use?
   - Is there a limit on failed attempts?

### Phase 6: Authorization Testing

1. Test for privilege escalation:
   - Vertical: regular user accessing admin functions.
   - Horizontal: user A accessing user B's resources.
2. Verify role-based access control (RBAC) or attribute-based access control (ABAC) is enforced server-side.
3. Test for Insecure Direct Object Reference (IDOR) on all resource endpoints.
4. Check if authorization decisions are cached and if cache can be poisoned.
5. Verify API authorization is consistent across all endpoints and methods.

## Templates

### Authentication Assessment Report

```markdown
## Authentication Security Assessment

### Application: [Name]
### Date: [YYYY-MM-DD]
### Assessor: [Name]

### Authentication Mechanisms Identified
| # | Mechanism | Token Type | Storage | MFA | Status |
|---|-----------|-----------|---------|-----|--------|
| 1 | Username/Password | JWT | HttpOnly Cookie | Optional | Tested |
| 2 | SAML SSO | Session | Server-side | Required | Tested |
| 3 | API Key | Bearer | Header | N/A | Tested |

### Findings

#### [CRITICAL] JWT Algorithm Confusion
- **Location**: `POST /api/auth/login`
- **Description**: JWT accepts `alg: none` and does not verify algorithm.
- **Impact**: Complete authentication bypass.
- **PoC**:
  1. Decode JWT header, change `alg` to `none`.
  2. Remove signature.
  3. Send modified token → access granted.
- **Remediation**: Hardcode the expected algorithm in the verification library.

### Password Policy Evaluation
- Minimum length: [8 / 12 / 16]
- Complexity: [Yes / No]
- Breach database check: [Yes / No]
- Hashing algorithm: [bcrypt / Argon2id / MD5 ❌]

### Compliance Mapping (OWASP ASVS v4.0)
| Requirement | Description | Status |
|-------------|-------------|--------|
| V2.1.1 | Password length ≥ 12 | ☐ |
| V2.1.2 | Password breach check | ☐ |
| V3.1.1 | Session ID randomness | ☐ |
| V3.2.1 | Session invalidation on logout | ☐ |
| V3.3.1 | Anti-CSRF tokens | ☐ |
```

### Credential Strength Testing Script

```bash
#!/bin/bash
# Test account lockout after failed attempts
TARGET="https://example.com/api/auth/login"
USER="testuser@example.com"

for i in $(seq 1 30); do
  RESPONSE=$(curl -s -w "\n%{http_code}" -X POST "$TARGET" \
    -H "Content-Type: application/json" \
    -d "{\"email\":\"$USER\",\"password\":\"wrongpass$i\"}")
  STATUS=$(echo "$RESPONSE" | tail -1)
  BODY=$(echo "$RESPONSE" | head -n -1)
  echo "Attempt $i: HTTP $STATUS"
  if [ "$STATUS" = "423" ] || [ "$STATUS" = "429" ]; then
    echo "Account locked / rate limited at attempt $i"
    break
  fi
done
```

## Common Pitfalls

- **Client-side authorization only** — Authorization must be enforced server-side on every request. Client-side checks are for UX, not security.
- **Not invalidating sessions on logout** — The session/token must be revoked server-side; deleting the cookie client-side is insufficient.
- **Reusing password reset tokens** — Reset tokens must be single-use and invalidated after consumption.
- **Weak JWT signing keys** — Never use short or guessable keys. Use ≥ 256-bit random keys for HMAC; use RSA ≥ 2048 bits.
- **Storing tokens in localStorage** — Vulnerable to XSS. Prefer HttpOnly cookies for web applications.
- **Forgetting to test API authentication** — Many applications secure the UI but leave API endpoints unprotected.
- **Ignoring timing attacks in login** — Use constant-time comparison for password verification to prevent oracle attacks.

## Legal Considerations

- **Brute Force Testing**: Must be authorized. Can trigger incident response and account lockouts affecting real users.
- **Credential Testing**: Never use real user credentials. Use test accounts created for the assessment.
- **MFA Bypass Testing**: May lock users out; coordinate with the support team.
- **Password Cracking**: Only hash files explicitly provided for assessment. Never extract hashes from production databases without authorization.
- **Account Takeover Simulation**: Requires explicit written approval from the organization's leadership.
- **Social Engineering**: Phishing-based auth testing requires separate, explicit authorization and may be regulated differently.

## Further Reading

- [OWASP Authentication Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html)
- [OWASP Session Management Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html)
- [NIST SP 800-63B: Digital Identity Guidelines](https://pages.nist.gov/800-63-3/sp800-63b.html)
- [OWASP ASVS v4.0](https://owasp.org/www-project-application-security-verification-standard/)
- [JWT Proven Patterns (RFC 8725)](https://datatracker.ietf.org/doc/html/rfc8725)
- [OAuth 2.0 Security Best Current Practice](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-security-topics)

---

## 中文版本

### 使用场景

- 为新应用设计认证流程
- 审计现有登录、SSO 和 MFA 实现
- 调查账户接管事件
- 实施 OAuth 2.0 / OpenID Connect
- 审查会话管理和 token 生命周期
- 从遗留认证迁移到现代标准
- 评估无密码认证方案（WebAuthn、FIDO2）
- 准备合规审计（PCI-DSS Requirement 8、NIST 800-63B）

### 核心步骤

1. **认证流程映射**：记录所有认证机制（用户名密码、SSO、API Key、Session Cookie、无密码登录），使用拦截代理绘制完整登录流程。
2. **密码安全评估**：验证使用 bcrypt/scrypt/Argon2id 哈希，测试用户名枚举、暴力破解防护、密码重置流程安全性。
3. **会话管理**：检查 Session ID 随机性、Cookie 安全属性（Secure/HttpOnly/SameSite）、会话超时和登出失效机制。
4. **Token 安全（JWT/OAuth 2.0）**：验证 JWT 算法不为 `none`，测试算法混淆攻击，检查 OAuth 2.0 的 `state` 参数和 redirect URI 验证。
5. **多因素认证**：验证 MFA 是否强制启用，测试 MFA 绕过路径，检查 TOTP 实现和备用恢复码安全性。
6. **授权测试**：测试垂直和水平权限提升，验证 IDOR，检查 API 授权一致性。

### 模板说明

- **认证评估报告模板**：包含认证机制清单、发现详情（JWT 算法混淆示例）、密码策略评估和 OWASP ASVS 合规映射。
- **凭据强度测试脚本**：通过循环失败登录测试账户锁定机制。

### 常见陷阱

- **仅在客户端做授权** — 授权必须在服务端每个请求上执行，客户端检查仅供 UX。
- **登出时未销毁会话** — 必须在服务端撤销 session/token，仅删除客户端 cookie 不够。
- **重复使用密码重置 token** — 重置 token 必须一次性使用且用后失效。
- **JWT 签名密钥过短** — HMAC 密钥至少 256 位，RSA 至少 2048 位。
- **将 token 存储在 localStorage** — 易受 XSS 攻击，Web 应用应优先使用 HttpOnly Cookie。
- **遗忘测试 API 认证** — 很多应用保护了 UI 但 API 端点未设防。
- **忽略登录时序攻击** — 密码验证应使用常量时间比较，防止 oracle 攻击。
