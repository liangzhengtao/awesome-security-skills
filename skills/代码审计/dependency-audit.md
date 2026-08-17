# Dependency Vulnerability Scanning Skill

> Identify, assess, and remediate known vulnerabilities in third-party libraries and open-source dependencies.

## When to Use

- Setting up automated dependency scanning in CI/CD
- Investigating a CVE that affects a library in use
- Performing a pre-release security audit
- Meeting SBOM (Software Bill of Materials) requirements
- Evaluating the security posture of a new dependency before adoption
- Responding to a supply chain attack incident
- Generating compliance reports for dependency licensing and security

## Prerequisites

- Access to the project's package manager lock files (`package-lock.json`, `requirements.txt`, `Cargo.lock`, `go.sum`, etc.)
- Understanding of semantic versioning and dependency resolution
- Access to the CI/CD pipeline for automation
- Familiarity with CVE, CVSS, and advisory databases

## Tools

| Tool | Ecosystem | Purpose | License |
|------|-----------|---------|---------|
| Dependabot | GitHub-native | Automated PRs for vulnerable deps | Free on GitHub |
| Trivy | Multi-language | Vulnerability and misconfig scanner | Apache-2.0 |
| Snyk | Multi-language | Vulnerability scanning with fix PRs | Freemium |
| Grype | Multi-language | SBOM-based vulnerability scanner | Apache-2.0 |
| npm audit | Node.js | Built-in dependency audit | MIT |
| pip-audit | Python | Python dependency vulnerability scanner | Apache-2.0 |
| cargo-audit | Rust | Rust dependency security checker | Apache-2.0 |
| OWASP Dependency-Check | Java / Multi | CVE-based dependency scanner | Apache-2.0 |
| OSV-Scanner | Multi-language | Google's open-source vuln scanner | Apache-2.0 |
| Syft | Multi-language | SBOM generation | Apache-2.0 |

## Step-by-Step Procedure

### Phase 1: Inventory and SBOM Generation

1. **Generate a Software Bill of Materials (SBOM)**:
   ```bash
   # Using Syft
   syft dir:. -o spdx-json > sbom.spdx.json
   syft dir:. -o cyclonedx-json > sbom.cyclonedx.json

   # Using Trivy
   trivy fs --format cyclonedx --output sbom.json .
   ```
2. **List all direct and transitive dependencies**:
   ```bash
   # npm
   npm ls --all
   # Python
   pip list --format=json
   # Go
   go list -m all
   # Rust
   cargo tree
   ```
3. **Identify dependency sources**: npm registry, PyPI, Maven Central, GitHub releases, private registries.
4. **Record licenses** for each dependency (license compliance is adjacent to security).

### Phase 2: Vulnerability Scanning

1. **Run the primary scanner**:
   ```bash
   # Trivy (all ecosystems)
   trivy fs --scanners vuln .

   # OSV-Scanner
   osv-scanner .

   # npm audit
   npm audit --json

   # pip-audit
   pip-audit --format=json

   # cargo-audit
   cargo audit
   ```
2. **Run a secondary scanner** for cross-validation:
   ```bash
   # Grype with SBOM
   grype sbom:sbom.cyclonedx.json

   # Snyk
   snyk test --all-projects
   ```
3. **Cross-reference findings** across tools to reduce false positives.
4. **Query CVE databases directly** for ambiguous cases:
   - NVD: https://nvd.nist.gov/
   - GitHub Advisory Database: https://github.com/advisories
   - OSV: https://osv.dev/

### Phase 3: Risk Assessment

1. **Evaluate each vulnerability** using these criteria:
   - **CVSS Score**: Base severity (Critical ≥ 9.0, High ≥ 7.0, Medium ≥ 4.0, Low < 4.0).
   - **Exploitability**: Is there a public exploit? Is it actively exploited in the wild?
   - **Reachability**: Does the application actually call the vulnerable code path?
   - **Exposure**: Is the vulnerable component internet-facing or internal only?
   - **Data Sensitivity**: Does the vulnerable component handle sensitive data?
2. **Prioritize based on actual risk**, not just CVSS score:
   - Critical + reachable + internet-facing → Fix immediately
   - High + reachable → Fix within 1 week
   - High + unreachable → Track, fix in next sprint
   - Medium → Fix within 30 days
   - Low → Track, batch in quarterly cleanup
3. **Document reachability analysis**:
   ```bash
   # Check if a vulnerable function is actually called
   grep -r "vulnerable_function_name" src/
   ```

### Phase 4: Remediation

1. **Update the dependency** (preferred):
   ```bash
   # npm
   npm update <package>
   npm audit fix

   # pip
   pip install --upgrade <package>

   # Go
   go get <package>@latest

   # Cargo
   cargo update -p <package>
   ```
2. **If no patch exists**:
   - Check if the vulnerable function is in your call path.
   - Apply a workaround (input validation, WAF rule, feature flag).
   - Fork the dependency and apply the patch locally.
   - Replace the dependency with an alternative.
3. **Verify the fix**:
   - Re-run the scanner to confirm the finding is resolved.
   - Run the project's test suite to confirm no regressions.
   - Check that the update does not introduce new vulnerabilities.

### Phase 5: Automation and Policy

1. **Configure Dependabot** (GitHub):
   ```yaml
   # .github/dependabot.yml
   version: 2
   updates:
     - package-ecosystem: "npm"
       directory: "/"
       schedule:
         interval: "weekly"
       open-pull-requests-limit: 10
       labels:
         - "security"
         - "dependencies"
   ```
2. **Set up automated scanning in CI**:
   ```yaml
   # GitHub Actions
   - name: Trivy Vulnerability Scan
     uses: aquasecurity/trivy-action@master
     with:
       scan-type: 'fs'
       severity: 'CRITICAL,HIGH'
       exit-code: '1'
   ```
3. **Define a dependency policy**:
   - Maximum allowed age for dependencies (e.g., no packages older than 2 years without active maintenance).
   - Minimum stars/downloads for new dependencies.
   - Required security posture (e.g., no packages with known Critical CVEs).
   - License allowlist (MIT, Apache-2.0, BSD; no GPL for proprietary projects).

### Phase 6: Supply Chain Security

1. **Verify package integrity**:
   - Check package signatures and checksums.
   - Verify the publisher identity on npm/PyPI.
   - Look for typosquatting (e.g., `lodash` vs `l0dash`).
2. **Lock dependencies**: Always commit lock files (`package-lock.json`, `Pipfile.lock`, `Cargo.lock`).
3. **Pin versions**: Avoid using `latest` or `*` in production dependencies.
4. **Audit dependency changes**: Review lock file diffs in every PR.
5. **Monitor for supply chain attacks**:
   - Subscribe to security advisories for your ecosystem.
   - Monitor for sudden ownership changes in critical packages.
   - Use tools like Socket.dev for supply chain risk analysis.

## Templates

### Dependency Audit Report

```markdown
## Dependency Security Audit

### Project: [Name]
### Date: [YYYY-MM-DD]
### Scanner(s): Trivy v0.XX, OSV-Scanner v1.XX

### Summary
| Severity | Count | Fixed | Pending | Accepted |
|----------|-------|-------|---------|----------|
| Critical | 2 | 1 | 1 | 0 |
| High | 5 | 3 | 2 | 0 |
| Medium | 12 | 8 | 2 | 2 |
| Low | 20 | 15 | 3 | 2 |

### Critical Findings

#### CVE-2024-XXXXX — [Library Name]
- **Package**: `example-lib@1.2.3`
- **CVSS**: 9.8 (Critical)
- **Description**: Remote code execution via crafted input.
- **Fix**: Upgrade to `example-lib@1.2.4`
- **Reachability**: YES — called in `src/handler.py:42`
- **Command**: `pip install example-lib>=1.2.4`

### Supply Chain Assessment
- Lock file present: [Yes/No]
- Lock file committed: [Yes/No]
- Package signing verified: [Yes/No]
- Typosquatting check: [Clean / Suspicious packages found]
```

### Dependency Policy Template

```markdown
## Dependency Security Policy

### Approval Criteria for New Dependencies
- [ ] No Critical or High CVEs in the last 12 months
- [ ] Actively maintained (commit within last 6 months)
- [ ] ≥ 1000 weekly downloads (npm) or ≥ 500 stars (GitHub)
- [ ] Compatible license (MIT, Apache-2.0, BSD-2/3, ISC)
- [ ] No known supply chain incidents
- [ ] Reviewed by at least one team member

### Update Schedule
- Critical/High CVEs: Within 48 hours of disclosure
- Medium CVEs: Within 30 days
- Low CVEs: Quarterly batch update
- Major version upgrades: Scheduled sprint work

### Exceptions
All exceptions require written approval from the Security Lead with a documented risk acceptance and review date.
```

## Common Pitfalls

- **Ignoring transitive dependencies** — Direct dependencies are only part of the picture. Vulnerabilities in transitive dependencies are equally dangerous.
- **Blindly running `npm audit fix --force`** — Major version updates can break APIs. Always review the changelog and run tests.
- **Not committing lock files** — Without lock files, dependency resolution is non-deterministic and vulnerable to supply chain attacks.
- **Only scanning in CI** — Developers should also run scans locally before committing. Pre-commit hooks are ideal.
- **Treating all Critical CVEs equally** — A Critical CVE in an unreachable code path is lower risk than a High CVE in an internet-facing endpoint.
- **Ignoring unmaintained dependencies** — A library with no updates in 2 years is a liability, even without known CVEs.
- **Not verifying package integrity** — Typosquatting and dependency confusion attacks exploit trust in package names.

## Legal Considerations

- **License Compliance**: Dependency scanning often reveals license information. Ensure all dependencies comply with your project's licensing requirements.
- **SBOM Requirements**: Regulations like the US Executive Order 14028 may require SBOM generation for government software.
- **Vulnerability Disclosure**: If you discover a zero-day in a dependency during scanning, follow responsible disclosure practices.
- **Export Controls**: Some cryptographic libraries may be subject to export control regulations (EAR, ITAR).
- **Private Vulnerability Data**: Scanner reports may contain embargoed vulnerability information; handle according to the embargo timeline.

## Further Reading

- [NIST SP 800-161: Supply Chain Risk Management](https://csrc.nist.gov/publications/detail/sp/800-161/rev-1/final)
- [OWASP Software Component Verification Standard](https://owasp.org/www-project-software-component-verification-standard/)
- [CycloneDX SBOM Standard](https://cyclonedx.org/)
- [SPDX SBOM Standard](https://spdx.dev/)
- [Endor Labs: State of Dependency Management](https://endorlabs.com/)
- [Socket.dev: Supply Chain Security](https://socket.dev/)
