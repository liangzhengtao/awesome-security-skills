[中文版](README.zh.md)

<div align="center">

# 🛡️ Awesome Security Skills

**Think like a hacker, defend like a pro.**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Security Skills](https://img.shields.io/badge/Security%20Skills-12-blue.svg)](#-skills-overview)
[![Maintained](https://img.shields.io/badge/Maintained-Yes-brightgreen.svg)](CHANGELOG.md)

**12 AI skills for cybersecurity** — a curated collection of structured, actionable skill files for AI-assisted security testing, code auditing, and defense.

</div>

---

## 🇬🇧 Overview

**Awesome Security Skills** provides battle-tested, structured skill files that transform AI assistants into capable cybersecurity practitioners. Each skill is a self-contained playbook covering when to use, required tools, step-by-step procedures, templates, pitfalls, and legal considerations.

These skills are designed for:
- **Security professionals** who want to augment their workflow with AI
- **Developers** building security into their development lifecycle
- **Teams** establishing consistent security testing practices
- **AI assistants** executing security assessments under human guidance

> ⚠️ **Legal Disclaimer**: These skills are provided for **authorized security testing and educational purposes only**. Always obtain explicit written permission before testing any system you do not own. Unauthorized access to computer systems is illegal in most jurisdictions. The authors assume no liability for misuse. See [SECURITY.md](SECURITY.md) for responsible disclosure guidelines.

---

## 📋 Skills Overview

<table>
<thead>
<tr>
<th>Category</th>
<th>Skill</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="3"><strong>🌐 Web Security</strong></td>
<td><a href="skills/Web安全/owasp-top10.md">OWASP Top 10</a></td>
<td>Systematically assess OWASP Top 10 vulnerabilities</td>
</tr>
<tr>
<td><a href="skills/Web安全/api-security.md">API Security</a></td>
<td>REST, GraphQL, and gRPC API security proven patterns</td>
</tr>
<tr>
<td><a href="skills/Web安全/authentication-security.md">Authentication Security</a></td>
<td>Authentication and authorization mechanism assessment</td>
</tr>
<tr>
<td rowspan="3"><strong>🔍 Code Audit</strong></td>
<td><a href="skills/代码审计/static-analysis.md">Static Analysis</a></td>
<td>Automated static code analysis tools and integration</td>
</tr>
<tr>
<td><a href="skills/代码审计/dependency-audit.md">Dependency Audit</a></td>
<td>Third-party dependency vulnerability scanning</td>
</tr>
<tr>
<td><a href="skills/代码审计/secure-code-review.md">Secure Code Review</a></td>
<td>Manual secure code review checklist</td>
</tr>
<tr>
<td rowspan="3"><strong>🎯 Penetration Testing</strong></td>
<td><a href="skills/渗透测试/reconnaissance.md">Reconnaissance</a></td>
<td>OSINT and information gathering techniques</td>
</tr>
<tr>
<td><a href="skills/渗透测试/web-app-testing.md">Web App Testing</a></td>
<td>Web application penetration testing methodology</td>
</tr>
<tr>
<td><a href="skills/渗透测试/report-writing.md">Report Writing</a></td>
<td>Professional penetration test report writing</td>
</tr>
<tr>
<td rowspan="3"><strong>🔧 Security Tools</strong></td>
<td><a href="skills/安全工具/burp-suite.md">Burp Suite</a></td>
<td>Master Burp Suite for web security testing</td>
</tr>
<tr>
<td><a href="skills/安全工具/nmap-scanning.md">Nmap Scanning</a></td>
<td>Network discovery and port scanning with Nmap</td>
</tr>
<tr>
<td><a href="skills/安全工具/security-automation.md">Security Automation</a></td>
<td>Automated security testing pipelines and scripts</td>
</tr>
</tbody>
</table>

---

## 🚀 Quick Start

### Using with AI Assistants

1. **Clone the repository**:
   ```bash
   git clone https://github.com/your-org/awesome-security-skills.git
   ```

2. **Feed a skill to your AI assistant**:
   - Copy the relevant skill file content into your AI conversation
   - Or point your AI tool to the skill file path
   - Example: "Read `skills/Web安全/owasp-top10.md` and follow its procedure to assess my application"

3. **Follow the step-by-step procedure**:
   - Each skill contains a complete workflow
   - Use the templates for consistent output
   - Review the pitfalls section before starting

### Integration with AI Tools

| AI Tool | Integration Method |
|---------|-------------------|
| **Kimi Code** | Copy skill content into conversation |
| **Cursor** | Add skill files to `.cursorrules` or project context |
| **Claude** | Include skill in system prompt or conversation |
| **ChatGPT** | Paste skill file as conversation context |
| **GitHub Copilot** | Reference skill in code comments or workspace |

---

## 📁 Project Structure

```
awesome-security-skills/
├── README.md                           # This file
├── LICENSE                             # MIT License
├── CONTRIBUTING.md                     # Contribution guide
├── SECURITY.md                         # Security policy
├── CODE_OF_CONDUCT.md                  # Code of conduct
├── CHANGELOG.md                        # Version history
├── .gitignore                          # Git ignore rules
├── .github/
│   ├── workflows/
│   │   └── ci.yml                      # CI pipeline
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md              # Bug report template
│   │   ├── feature_request.md         # Feature request template
│   │   └── new_skill.md               # New skill proposal
│   └── pull_request_template.md        # PR template
└── skills/
    ├── Web安全/                         # Web Security
    │   ├── owasp-top10.md
    │   ├── api-security.md
    │   └── authentication-security.md
    ├── 代码审计/                         # Code Audit
    │   ├── static-analysis.md
    │   ├── dependency-audit.md
    │   └── secure-code-review.md
    ├── 渗透测试/                         # Penetration Testing
    │   ├── reconnaissance.md
    │   ├── web-app-testing.md
    │   └── report-writing.md
    └── 安全工具/                         # Security Tools
        ├── burp-suite.md
        ├── nmap-scanning.md
        └── security-automation.md
```

---

## 🎓 How Skills Are Structured

Each skill file follows a consistent structure to maximize usability:

| Section | Purpose |
|---------|---------|
| **When to Use** | Scenarios and triggers for applying the skill |
| **Prerequisites** | Required knowledge and access |
| **Tools** | Recommended tools with licensing info |
| **Step-by-Step Procedure** | Detailed, phased workflow |
| **Templates** | Ready-to-use report and checklist templates |
| **Common Pitfalls** | Mistakes to avoid |
| **Legal Considerations** | Authorization, disclosure, and compliance |
| **Further Reading** | Authoritative reference links |

---

## 🤝 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

**Ways to contribute**:
- 🐛 Report errors or outdated information
- ✨ Propose new skills
- 📝 Improve existing skills
- 🌍 Translate skills to other languages
- 🧪 Add test cases and examples

---

## 🔗 See Also

Other awesome projects in the ecosystem:

- **[awesome-security](https://github.com/sbilly/awesome-security)** — A collection of awesome software, libraries, documents, books, resources and cool stuffs about security.
- **[awesome-web-security](https://github.com/qazbnm456/awesome-web-security)** — A list of web security materials and resources.
- **[awesome-pentest](https://github.com/enaqx/awesome-pentest)** — A collection of awesome penetration testing resources, tools and other shiny things.
- **[awesome-hacking](https://github.com/carpedm20/awesome-hacking)** — A curated list of delightful Hacking resources.
- **[awesome-malware-analysis](https://rshipp/awesome-malware-analysis)** — A curated list of awesome malware analysis tools and resources.
- **[awesome-threat-intelligence](https://github.com/hslatman/awesome-threat-intelligence)** — A curated list of Awesome Threat Intelligence resources.
- **[awesome-incident-response](https://github.com/meirwah/awesome-incident-response)** — A curated list of tools for incident response.
- **[awesome-reversing](https://github.com/wtsxDev/reversing)** — A curated list of awesome reversing resources.
- **[awesome-static-analysis](https://github.com/mre/awesome-static-analysis)** — A curated list of static analysis tools, linters and code quality checkers.
- **[awesome-cyber-skills](https://github.com/Dev115/awesome-cyber-skills)** — A curated list of hacking environments where you can train your cyber skills.
- **[awesome-ctf](https://github.com/apsdehal/awesome-ctf)** — A curated list of CTF frameworks, libraries, resources and software.
- **[awesome-bugbounty](https://github.com/djadmin/awesome-bugbounty)** — A complete list of bug bounty programs and writeups.
- **[awesome-osint](https://github.com/jivoi/awesome-osint)** — A curated list of amazingly awesome OSINT tools.
- **[awesome-devsecops](https://github.com/TaptuIT/awesome-devsecops)** — A curated list of awesome DevSecOps tools, resources, and references.

---

## 📜 License

This project is licensed under the [MIT License](LICENSE).

---

## ⚖️ Legal Disclaimer

**The tools, techniques, and skills provided in this repository are for authorized security testing and educational purposes only.** Always obtain explicit written permission from the system owner before conducting any security assessment. Unauthorized access to computer systems is a criminal offense in most jurisdictions, including under the Computer Fraud and Abuse Act (CFAA) in the United States, the Computer Misuse Act in the United Kingdom, and similar laws worldwide.

The maintainers and contributors of this project assume **no liability** and are **not responsible** for any misuse or damage caused by the use of information contained herein. Users are solely responsible for ensuring they comply with all applicable laws and regulations.

---

<div align="center">

**Made with ❤️ by the security community**

[⬆ Back to Top](#-awesome-security-skills)

</div>
