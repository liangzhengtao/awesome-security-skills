# API Security Best Practices Skill

> Secure REST, GraphQL, and gRPC APIs against common attack vectors with systematic assessment and hardening.

## When to Use

- Designing a new API and need a security baseline
- Auditing an existing API for security vulnerabilities
- Implementing authentication and authorization for APIs
- Preparing for an API-centric penetration test
- Integrating API security into CI/CD pipelines
- Responding to an API-related security incident
- Building an API security governance program

## Prerequisites

- Understanding of RESTful API design principles
- Familiarity with OAuth 2.0 / OpenID Connect flows
- Knowledge of JSON Web Tokens (JWT) structure
- Access to the API source code or a running instance (authorized testing)
- Basic understanding of rate limiting and throttling concepts

## Tools

| Tool | Purpose | License |
|------|---------|---------|
| Postman | API testing and collection-based security checks | Proprietary Free |
| Burp Suite | Intercepting proxy for API traffic manipulation | Community / Pro |
| OWASP ZAP | Automated API scanning with OpenAPI import | Apache-2.0 |
| JWT.io / jwt_tool | JWT token inspection and attack | MIT |
| Arjun | Hidden API parameter discovery | MIT |
| Kiterunner | API endpoint and wordlist-based brute forcing | MIT |
| Schema Validator | OpenAPI/Swagger spec validation | Various |

## Step-by-Step Procedure

### Phase 1: API Discovery and Documentation

1. Collect all API documentation (OpenAPI/Swagger, RAML, GraphQL schemas).
2. If no docs exist, use passive traffic analysis to reconstruct endpoints.
3. Enumerate API versions (`/v1/`, `/v2/`, `/internal/`).
4. Map all endpoints with their HTTP methods, parameters, and expected responses.
5. Identify authentication requirements per endpoint.
6. Use Kiterunner with API-specific wordlists to discover undocumented routes.

### Phase 2: Authentication and Authorization Testing

#### Token Security

- Inspect JWT tokens: check algorithm (`alg` header), verify none of `none` attack is possible.
- Test for algorithm confusion (RS256 → HS256 key confusion).
- Verify token expiration, audience (`aud`), and issuer (`iss`) claims are validated.
- Check if tokens can be reused after logout or password change.
- Test refresh token rotation and revocation.

#### OAuth 2.0 / OIDC Flows

- Verify `state` parameter is used and validated in authorization code flow.
- Check redirect URI validation (open redirect via `redirect_uri` manipulation).
- Test for authorization code interception.
- Verify PKCE is used for public clients.
- Check for token leakage in referrer headers or browser history.

#### Access Control

- Test BOLA (Broken Object Level Authorization): access resources with other users' IDs.
- Test BFLA (Broken Function Level Authorization): call admin endpoints with regular user tokens.
- Verify that API keys are not used as the sole authentication mechanism for sensitive operations.
- Check if GraphQL introspection is disabled in production.

### Phase 3: Input Validation and Injection

1. Test all parameters for injection attacks:
   - SQL injection in query parameters, path parameters, and request bodies.
   - NoSQL injection in JSON payloads (`{"$gt": ""}`, `{"$ne": null}`).
   - Command injection in file names or processing parameters.
   - XML/XXE injection if XML payloads are accepted.
2. Test for mass assignment: send extra fields in PUT/PATCH requests (`{"role": "admin"}`).
3. Validate file upload endpoints:
   - File type validation (MIME type and extension).
   - File size limits.
   - Storage location (should not be web-accessible).
   - Filename sanitization.
4. Test GraphQL-specific attacks:
   - Query depth attacks (deeply nested queries).
   - Batch query abuse.
   - Field suggestion information disclosure.

### Phase 4: Rate Limiting and Resource Abuse

1. Test rate limiting on authentication endpoints (login, token refresh, password reset).
2. Verify rate limits on expensive operations (search, export, report generation).
3. Test for rate limit bypass via:
   - IP rotation / X-Forwarded-For header manipulation.
   - API key rotation.
   - Distributed requests across multiple tokens.
4. Check for pagination limits (can a client request `?limit=1000000`?).
5. Test for denial of service via large payloads or complex queries.

### Phase 5: Data Exposure and Error Handling

1. Verify responses do not leak internal data (stack traces, database errors, internal IPs).
2. Check if API returns more data than needed (mass assignment in responses).
3. Test error handling: send malformed JSON, invalid content types, missing headers.
4. Verify that 4xx/5xx responses do not include sensitive debug information.
5. Check CORS configuration: verify allowed origins are restrictive, not wildcard `*`.

### Phase 6: Transport and Infrastructure

1. Verify HTTPS is enforced (no HTTP fallback).
2. Check for HSTS headers.
3. Verify TLS certificate validity and strength.
4. Test for HTTP request smuggling if behind a reverse proxy.
5. Check for caching of sensitive API responses in CDN or proxy layers.

## Templates

### API Security Assessment Report

```markdown
## API Security Assessment

### Scope
- **API Name**: [Name]
- **Base URL**: `https://api.example.com/v1`
- **Documentation**: [Link to OpenAPI spec]
- **Auth Method**: Bearer JWT / API Key / OAuth 2.0

### Endpoint Inventory
| Method | Path | Auth Required | Tested | Findings |
|--------|------|---------------|--------|----------|
| GET | /users/{id} | Yes | ☐ | |
| POST | /auth/login | No | ☐ | |
| PUT | /users/{id} | Yes | ☐ | |

### Findings

#### [HIGH] BOLA on /api/v1/users/{id}
- **Endpoint**: `GET /api/v1/users/{id}`
- **Description**: Any authenticated user can access any other user's profile by changing the ID.
- **PoC**: As user A (ID=100), request `GET /api/v1/users/200` returns user B's data.
- **Remediation**: Validate that the authenticated user owns the requested resource.

### Recommendations Summary
1. Implement object-level authorization on all resource endpoints.
2. Add rate limiting: 100 req/min per user, 10 req/min for auth endpoints.
3. Disable GraphQL introspection in production.
4. Enforce HTTPS-only with HSTS.
```

### Rate Limit Testing Script

```bash
#!/bin/bash
# Test rate limiting on a target endpoint
ENDPOINT="https://api.example.com/v1/auth/login"
TOKEN="Bearer eyJ..."

for i in $(seq 1 200); do
  STATUS=$(curl -s -o /dev/null -w "%{http_code}" \
    -X POST "$ENDPOINT" \
    -H "Authorization: $TOKEN" \
    -H "Content-Type: application/json" \
    -d '{"username":"test","password":"test"}')
  echo "Request $i: HTTP $STATUS"
  if [ "$STATUS" = "429" ]; then
    echo "Rate limit triggered at request $i"
    break
  fi
done
```

## Common Pitfalls

- **Trusting client-side validation only** — Always validate inputs server-side. Client-side checks are trivially bypassed.
- **Forgetting about legacy API versions** — Old `/v1/` endpoints may lack security controls added to `/v2/`.
- **Ignoring GraphQL attack surface** — GraphQL introspection can reveal the entire schema; disable it in production.
- **Over-relying on API keys** — API keys are identification, not authentication. Pair them with proper auth.
- **Not testing with different user roles** — Always test endpoints with at least admin, regular user, and unauthenticated perspectives.
- **Missing error normalization** — Ensure errors return generic messages; detailed errors aid attackers.

## Legal Considerations

- **Authorization Required**: API testing must be explicitly authorized by the API owner.
- **Third-Party APIs**: Never test APIs you do not own or have no written permission to test.
- **Rate Limit Bypass Testing**: Can impact service availability; coordinate with the operations team.
- **Data in Transit**: Testing may expose real user data in API responses; handle with care and do not store.
- **Cloud Provider Terms**: Some cloud providers (AWS, GCP, Azure) have specific acceptable use policies for security testing.
- **GraphQL Specifics**: Denial-of-service testing via query complexity can affect shared infrastructure; get approval first.

## Further Reading

- [OWASP API Security Top 10](https://owasp.org/API-Security/)
- [OWASP REST Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/REST_Security_Cheat_Sheet.html)
- [API Security Best Practices (CISA)](https://www.cisa.gov/)
- [Auth0 API Security Guide](https://auth0.com/docs/secure/tokens)
- [PortSwigger API Security Academy](https://portswigger.net/web-security/api-testing)
