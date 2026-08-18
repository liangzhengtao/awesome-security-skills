[English](README.md)

<div align="center">

# 🛡️ Awesome Security Skills

**像黑客一样思考，像专家一样防御。**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Security Skills](https://img.shields.io/badge/Security%20Skills-12-blue.svg)](#-技能概览)
[![Maintained](https://img.shields.io/badge/Maintained-Yes-brightgreen.svg)](CHANGELOG.md)

**12 个网络安全 AI 技能** — 一套结构化、可操作的安全技能文件集合，涵盖 AI 辅助安全测试、代码审计和防御。

</div>

---

## 📋 技能概览

<table>
<thead>
<tr>
<th>类别</th>
<th>技能</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="3"><strong>🌐 Web 安全</strong></td>
<td><a href="skills/Web安全/owasp-top10.md">OWASP Top 10</a></td>
<td>系统化评估 OWASP Top 10 漏洞</td>
</tr>
<tr>
<td><a href="skills/Web安全/api-security.md">API 安全</a></td>
<td>REST、GraphQL 和 gRPC API 安全最佳实践</td>
</tr>
<tr>
<td><a href="skills/Web安全/authentication-security.md">认证安全</a></td>
<td>认证和授权机制评估</td>
</tr>
<tr>
<td rowspan="3"><strong>🔍 代码审计</strong></td>
<td><a href="skills/代码审计/static-analysis.md">静态分析</a></td>
<td>自动化静态代码分析工具与集成</td>
</tr>
<tr>
<td><a href="skills/代码审计/dependency-audit.md">依赖审计</a></td>
<td>第三方依赖漏洞扫描</td>
</tr>
<tr>
<td><a href="skills/代码审计/secure-code-review.md">安全代码审查</a></td>
<td>手动安全代码审查清单</td>
</tr>
<tr>
<td rowspan="3"><strong>🎯 渗透测试</strong></td>
<td><a href="skills/渗透测试/reconnaissance.md">信息收集</a></td>
<td>开源情报和信息收集技术</td>
</tr>
<tr>
<td><a href="skills/渗透测试/web-app-testing.md">Web 应用测试</a></td>
<td>Web 应用渗透测试方法论</td>
</tr>
<tr>
<td><a href="skills/渗透测试/report-writing.md">报告撰写</a></td>
<td>专业渗透测试报告撰写</td>
</tr>
<tr>
<td rowspan="3"><strong>🔧 安全工具</strong></td>
<td><a href="skills/安全工具/burp-suite.md">Burp Suite</a></td>
<td>精通 Burp Suite Web 安全测试</td>
</tr>
<tr>
<td><a href="skills/安全工具/nmap-scanning.md">Nmap 扫描</a></td>
<td>使用 Nmap 进行网络发现和端口扫描</td>
</tr>
<tr>
<td><a href="skills/安全工具/security-automation.md">安全自动化</a></td>
<td>自动化安全测试流水线和脚本</td>
</tr>
</tbody>
</table>

---

## 🚀 快速开始

### 与 AI 助手配合使用

1. **克隆仓库**:
   ```bash
   git clone https://github.com/your-org/awesome-security-skills.git
   ```

2. **将技能文件提供给 AI 助手**:
   - 将相关技能文件内容复制到 AI 对话中
   - 或将 AI 工具指向技能文件路径
   - 示例："读取 `skills/Web安全/owasp-top10.md` 并按照其流程评估我的应用"

3. **按照步骤执行**:
   - 每个技能包含完整的工作流程
   - 使用模板确保输出一致
   - 开始前先查看常见陷阱部分

### 与 AI 工具集成

| AI 工具 | 集成方式 |
|---------|---------|
| **Kimi Code** | 将技能内容复制到对话中 |
| **Cursor** | 将技能文件添加到 `.cursorrules` 或项目上下文中 |
| **Claude** | 在系统提示或对话中包含技能 |
| **ChatGPT** | 将技能文件粘贴为对话上下文 |
| **GitHub Copilot** | 在代码注释或工作区中引用技能 |

---

## 📁 项目结构

```
awesome-security-skills/
├── README.md                           # 本文件
├── README.zh.md                        # 中文版
├── LICENSE                             # MIT 许可证
├── CONTRIBUTING.md                     # 贡献指南
├── SECURITY.md                         # 安全政策
├── CODE_OF_CONDUCT.md                  # 行为准则
├── CHANGELOG.md                        # 版本历史
├── .gitignore                          # Git 忽略规则
├── .github/
│   ├── workflows/
│   │   └── ci.yml                      # CI 流水线
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md              # Bug 报告模板
│   │   ├── feature_request.md         # 功能请求模板
│   │   └── new_skill.md               # 新技能提案
│   └── pull_request_template.md        # PR 模板
└── skills/
    ├── Web安全/                         # Web 安全
    ├── 代码审计/                         # 代码审计
    ├── 渗透测试/                         # 渗透测试
    └── 安全工具/                         # 安全工具
```

---

## 🎓 技能结构说明

每个技能文件遵循统一结构以最大化可用性：

| 章节 | 用途 |
|------|------|
| **使用场景** | 应用该技能的场景和触发条件 |
| **前置要求** | 所需知识和访问权限 |
| **工具** | 推荐工具及许可证信息 |
| **分步流程** | 详细的分阶段工作流程 |
| **模板** | 即用的报告和清单模板 |
| **常见陷阱** | 需要避免的错误 |
| **法律考虑** | 授权、披露和合规 |
| **延伸阅读** | 权威参考链接 |

---

## 🤝 贡献

欢迎贡献！请参阅 [CONTRIBUTING.md](CONTRIBUTING.md) 了解指南。

**贡献方式**：
- 🐛 报告错误或过时信息
- ✨ 提议新技能
- 📝 改进现有技能
- 🌍 翻译技能到其他语言
- 🧪 添加测试用例和示例

---

## 🔗 相关项目

生态系统中的其他优秀项目：

- **[awesome-security](https://github.com/sbilly/awesome-security)** — 安全相关的优秀软件、库、文档、书籍和资源集合。
- **[awesome-web-security](https://github.com/qazbnm456/awesome-web-security)** — Web 安全材料和资源列表。
- **[awesome-pentest](https://github.com/enaqx/awesome-pentest)** — 优秀的渗透测试资源、工具和其他闪亮的东西。
- **[awesome-hacking](https://github.com/carpedm20/awesome-hacking)** — 令人愉悦的黑客资源精选列表。
- **[awesome-malware-analysis](https://rshipp/awesome-malware-analysis)** — 优秀的恶意软件分析工具和资源精选列表。
- **[awesome-threat-intelligence](https://github.com/hslatman/awesome-threat-intelligence)** — 优秀的威胁情报资源精选列表。
- **[awesome-incident-response](https://github.com/meirwah/awesome-incident-response)** — 事件响应工具精选列表。
- **[awesome-reversing](https://github.com/wtsxDev/reversing)** — 优秀的逆向工程资源精选列表。
- **[awesome-static-analysis](https://github.com/mre/awesome-static-analysis)** — 静态分析工具、Linter 和代码质量检查器精选列表。
- **[awesome-cyber-skills](https://github.com/Dev115/awesome-cyber-skills)** — 可以训练网络安全技能的黑客环境精选列表。
- **[awesome-ctf](https://github.com/apsdehal/awesome-ctf)** — CTF 框架、库、资源和软件精选列表。
- **[awesome-bugbounty](https://github.com/djadmin/awesome-bugbounty)** — Bug 赏金计划和报告的完整列表。
- **[awesome-osint](https://github.com/jivoi/awesome-osint)** — 惊人的 OSINT 工具精选列表。
- **[awesome-devsecops](https://github.com/TaptuIT/awesome-devsecops)** — 优秀的 DevSecOps 工具、资源和参考精选列表。

---

## 📜 许可证

本项目采用 [MIT 许可证](LICENSE)。

---

## ⚖️ 法律免责声明

**本仓库提供的工具、技术和技能仅用于授权的安全测试和教育目的。** 在进行任何安全评估之前，请务必获得系统所有者的明确书面许可。未经授权访问计算机系统在大多数司法管辖区属于刑事犯罪，包括美国的《计算机欺诈和滥用法》(CFAA)、英国的《计算机滥用法》以及全球类似的法律。

本项目的维护者和贡献者**不承担任何责任**，也**不对**因使用本文所含信息而造成的任何滥用或损害负责。用户完全负责确保遵守所有适用的法律法规。

---

<div align="center">

**由安全社区用 ❤️ 制作**

[⬆ 返回顶部](#-awesome-security-skills)

</div>
