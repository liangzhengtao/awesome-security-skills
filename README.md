<!-- Banner -->
<div align="center">

# 🛡️ Awesome Security Skills

**Think like a hacker, defend like a pro.**

**像黑客一样思考，像专家一样防御。**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Security Skills](https://img.shields.io/badge/Security%20Skills-12-blue.svg)](#-skills-overview)
[![Maintained](https://img.shields.io/badge/Maintained-Yes-brightgreen.svg)](CHANGELOG.md)

**12 AI skills for cybersecurity** — a curated collection of structured, actionable skill files for AI-assisted security testing, code auditing, and defense.

**12 个网络安全 AI 技能** — 一套结构化、可操作的安全技能文件集合，涵盖 AI 辅助安全测试、代码审计和防御。

[English](#-overview) · [中文](#-概述)

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

> ⚠️ **法律声明**: 这些技能仅用于**授权的安全测试和教育目的**。在测试任何不属于您的系统之前，请务必获得明确的书面许可。未经授权访问计算机系统在大多数司法管辖区是非法的。作者对滥用不承担任何责任。有关负责任的披露指南，请参阅 [SECURITY.md](SECURITY.md)。

---

## 📋 Skills Overview / 技能概览

<table>
<thead>
<tr>
<th>Category / 类别</th>
<th>Skill / 技能</th>
<th>Description / 描述</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="3"><strong>🌐 Web 安全</strong><br>Web Security</td>
<td><a href="skills/Web安全/owasp-top10.md">OWASP Top 10</a></td>
<td>Systematically assess OWASP Top 10 vulnerabilities<br>系统化评估 OWASP Top 10 漏洞</td>
</tr>
<tr>
<td><a href="skills/Web安全/api-security.md">API Security</a></td>
<td>REST, GraphQL, and gRPC API security proven patterns<br>REST、GraphQL 和 gRPC API 安全最佳实践</td>
</tr>
<tr>
<td><a href="skills/Web安全/authentication-security.md">Authentication Security</a></td>
<td>Authentication and authorization mechanism assessment<br>认证和授权机制评估</td>
</tr>
<tr>
<td rowspan="3"><strong>🔍 代码审计</strong><br>Code Audit</td>
<td><a href="skills/代码审计/static-analysis.md">Static Analysis</a></td>
<td>Automated static code analysis tools and integration<br>自动化静态代码分析工具与集成</td>
</tr>
<tr>
<td><a href="skills/代码审计/dependency-audit.md">Dependency Audit</a></td>
<td>Third-party dependency vulnerability scanning<br>第三方依赖漏洞扫描</td>
</tr>
<tr>
<td><a href="skills/代码审计/secure-code-review.md">Secure Code Review</a></td>
<td>Manual secure code review checklist<br>手动安全代码审查清单</td>
</tr>
<tr>
<td rowspan="3"><strong>🎯 渗透测试</strong><br>Penetration Testing</td>
<td><a href="skills/渗透测试/reconnaissance.md">Reconnaissance</a></td>
<td>OSINT and information gathering techniques<br>开源情报和信息收集技术</td>
</tr>
<tr>
<td><a href="skills/渗透测试/web-app-testing.md">Web App Testing</a></td>
<td>Web application penetration testing methodology<br>Web 应用渗透测试方法论</td>
</tr>
<tr>
<td><a href="skills/渗透测试/report-writing.md">Report Writing</a></td>
<td>Professional penetration test report writing<br>专业渗透测试报告撰写</td>
</tr>
<tr>
<td rowspan="3"><strong>🔧 安全工具</strong><br>Security Tools</td>
<td><a href="skills/安全工具/burp-suite.md">Burp Suite</a></td>
<td>Master Burp Suite for web security testing<br>精通 Burp Suite Web 安全测试</td>
</tr>
<tr>
<td><a href="skills/安全工具/nmap-scanning.md">Nmap Scanning</a></td>
<td>Network discovery and port scanning with Nmap<br>使用 Nmap 进行网络发现和端口扫描</td>
</tr>
<tr>
<td><a href="skills/安全工具/security-automation.md">Security Automation</a></td>
<td>Automated security testing pipelines and scripts<br>自动化安全测试流水线和脚本</td>
</tr>
</tbody>
</table>

---

## 🚀 Quick Start / 快速开始

### Using with AI Assistants / 与 AI 助手配合使用

1. **Clone the repository / 克隆仓库**:
   ```bash
   git clone https://github.com/your-org/awesome-security-skills.git
   ```

2. **Feed a skill to your AI assistant / 将技能文件提供给 AI 助手**:
   - Copy the relevant skill file content into your AI conversation
   - Or point your AI tool to the skill file path
   - Example: "Read `skills/Web安全/owasp-top10.md` and follow its procedure to assess my application"

3. **Follow the step-by-step procedure / 按照步骤执行**:
   - Each skill contains a complete workflow
   - Use the templates for consistent output
   - Review the pitfalls section before starting

### Integration with AI Tools / 与 AI 工具集成

| AI Tool | Integration Method |
|---------|-------------------|
| **Kimi Code** | Copy skill content into conversation |
| **Cursor** | Add skill files to `.cursorrules` or project context |
| **Claude** | Include skill in system prompt or conversation |
| **ChatGPT** | Paste skill file as conversation context |
| **GitHub Copilot** | Reference skill in code comments or workspace |

---

## 📁 Project Structure / 项目结构

```
awesome-security-skills/
├── README.md                           # This file / 本文件
├── LICENSE                             # MIT License
├── CONTRIBUTING.md                     # Contribution guide / 贡献指南
├── SECURITY.md                         # Security policy / 安全政策
├── CODE_OF_CONDUCT.md                  # Code of conduct / 行为准则
├── CHANGELOG.md                        # Version history / 版本历史
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

## 🎓 How Skills Are Structured / 技能结构说明

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

## 🤝 Contributing / 贡献

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

欢迎贡献！请参阅 [CONTRIBUTING.md](CONTRIBUTING.md) 了解指南。

**Ways to contribute / 贡献方式**:
- 🐛 Report errors or outdated information / 报告错误或过时信息
- ✨ Propose new skills / 提议新技能
- 📝 Improve existing skills / 改进现有技能
- 🌍 Translate skills to other languages / 翻译技能到其他语言
- 🧪 Add test cases and examples / 添加测试用例和示例

---

## 🔗 See Also / 相关项目

Other awesome projects in the ecosystem:

- **[awesome-security](https://github.com/sbilly/awesome-security)** — A collection of awesome software, libraries, documents, books, resources and cool stuffs about security.
- **[awesome-web-security](https://github.com/qazbnm456/awesome-web-security)** — A list of web security materials and resources.
- **[awesome-pentest](https://github.com/enaqx/awesome-pentest)** — A collection of awesome penetration testing resources, tools and other shiny things.
- **[awesome-hacking](https://github.com/carpedm20/awesome-hacking)** — A curated list of delightful Hacking resources.
- **[awesome-malware-analysis](https.com/rshipp/awesome-malware-analysis)** — A curated list of awesome malware analysis tools and resources.
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

## 📜 License / 许可证

This project is licensed under the [MIT License](LICENSE).

本项目采用 [MIT 许可证](LICENSE)。

---

## ⚖️ Legal Disclaimer / 法律免责声明

**The tools, techniques, and skills provided in this repository are for authorized security testing and educational purposes only.** Always obtain explicit written permission from the system owner before conducting any security assessment. Unauthorized access to computer systems is a criminal offense in most jurisdictions, including under the Computer Fraud and Abuse Act (CFAA) in the United States, the Computer Misuse Act in the United Kingdom, and similar laws worldwide.

**本仓库提供的工具、技术和技能仅用于授权的安全测试和教育目的。** 在进行任何安全评估之前，请务必获得系统所有者的明确书面许可。未经授权访问计算机系统在大多数司法管辖区属于刑事犯罪，包括美国的《计算机欺诈和滥用法》(CFAA)、英国的《计算机滥用法》以及全球类似的法律。

The maintainers and contributors of this project assume **no liability** and are **not responsible** for any misuse or damage caused by the use of information contained herein. Users are solely responsible for ensuring they comply with all applicable laws and regulations.

本项目的维护者和贡献者**不承担任何责任**，也**不对**因使用本文所含信息而造成的任何滥用或损害负责。用户完全负责确保遵守所有适用的法律法规。

---

<div align="center">

**Made with ❤️ by the security community**

**由安全社区用 ❤️ 制作**

[⬆ Back to Top / 返回顶部](#-awesome-security-skills)

</div>
