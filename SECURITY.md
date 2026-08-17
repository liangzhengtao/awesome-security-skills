# Security Policy

## Responsible Disclosure

If you discover a security vulnerability in this project or in the tools/techniques described in the skill files, we ask that you follow responsible disclosure practices.

### Reporting a Vulnerability

**Do NOT open a public GitHub issue for security vulnerabilities.**

Instead, please report security vulnerabilities by emailing the maintainers privately. Include:

1. A description of the vulnerability
2. Steps to reproduce the issue
3. Potential impact assessment
4. Suggested fix (if available)

We will acknowledge your report within **48 hours** and provide a detailed response within **7 days** indicating the next steps in handling your report.

### Disclosure Timeline

- **Day 0**: Vulnerability reported
- **Day 2**: Acknowledgment of report
- **Day 7**: Initial assessment and triage
- **Day 30**: Target fix deadline
- **Day 90**: Public disclosure (if fix is available)

We request that reporters give us a reasonable amount of time to address the issue before public disclosure.

## Scope

### In Scope

- This repository and its contents (skill files, templates, configurations)
- The GitHub Actions CI/CD pipeline
- Any scripts or automation included in the repository

### Out of Scope

- Third-party tools referenced in skill files
- Systems and applications that users test using these skills
- Social engineering attacks against maintainers or contributors

## Security Best Practices for Users

When using the skills in this repository:

1. **Always obtain written authorization** before testing any system.
2. **Stay within the defined scope** of your engagement.
3. **Do not commit sensitive data** (credentials, API keys, personal data) to this repository.
4. **Verify tool integrity** — download tools from official sources and verify checksums.
5. **Use isolated environments** for testing (VMs, containers, dedicated test networks).
6. **Follow applicable laws** in your jurisdiction regarding computer security testing.

## Skill File Security

Each skill file includes a **Legal Considerations** section. Read this section carefully before applying any skill. Key points:

- All testing requires explicit written authorization
- Stay within authorized scope at all times
- Handle discovered data responsibly
- Follow responsible disclosure for any findings
- Maintain confidentiality of assessment results

## Acknowledgments

We thank all security researchers who responsibly disclose vulnerabilities and help improve this project.
