[English](README.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [Français](README.fr.md) | [Español](README.es.md) | [العربية](README.ar.md) | [한국어](README.ko.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [Deutsch](README.de.md)

<div align="center">

# 🛡️ Awesome Security Skills

**Pense como um hacker, defenda como um profissional.**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Security Skills](https://img.shields.io/badge/Security%20Skills-12-blue.svg)](#-skills-overview)
[![Maintained](https://img.shields.io/badge/Maintained-Yes-brightgreen.svg)](CHANGELOG.md)

**12 habilidades de IA para cibersegurança** — uma coleção curada de arquivos de habilidades estruturados e acionáveis para testes de segurança assistidos por IA, auditoria de código e defesa.

</div>

---

## 🇬🇧 Visão Geral

O **Awesome Security Skills** fornece arquivos de habilidades estruturados e comprovados que transformam assistentes de IA em profissionais de cibersegurança capazes. Cada habilidade é um playbook autossuficiente que cobre quando usar, ferramentas necessárias, procedimentos passo a passo, armadilhas e considerações legais.

Estas habilidades são projetadas para:
- **Profissionais de segurança** que desejam aumentar seu fluxo de trabalho com IA
- **Desenvolvedores** integrando segurança no ciclo de vida do desenvolvimento
- **Equipes** estabelecendo práticas consistentes de testes de segurança
- **Assistentes de IA** executando avaliações de segurança sob orientação humana

> ⚠️ **Aviso Legal**: Estas habilidades são fornecidas **apenas para testes de segurança autorizados e fins educacionais**. Sempre obtenha permissão escrita explícita antes de testar qualquer sistema que não seja de sua propriedade. O acesso não autorizado a sistemas de computador é ilegal na maioria das jurisdições. Os autores não assumem nenhuma responsabilidade por uso indevido. Consulte [SECURITY.md](SECURITY.md) para diretrizes de divulgação responsável.

---

## �📋 Visão Geral das Habilidades

<table>
<thead>
<tr>
<th>Categoria</th>
<th>Habilidade</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="3"><strong>🌐 Segurança Web</strong></td>
<td><a href="skills/Web安全/owasp-top10.md">OWASP Top 10</a></td>
<td>Avaliação sistemática das vulnerabilidades OWASP Top 10</td>
</tr>
<tr>
<td><a href="skills/Web安全/api-security.md">API Security</a></td>
<td>Padrões comprovados de segurança para APIs REST, GraphQL e gRPC</td>
</tr>
<tr>
<td><a href="skills/Web安全/authentication-security.md">Authentication Security</a></td>
<td>Avaliação de mecanismos de autenticação e autorização</td>
</tr>
<tr>
<td rowspan="3"><strong>🔍 Auditoria de Código</strong></td>
<td><a href="skills/代码审计/static-analysis.md">Static Analysis</a></td>
<td>Ferramentas de análise estática automatizada e integração</td>
</tr>
<tr>
<td><a href="skills/代码审计/dependency-audit.md">Dependency Audit</a></td>
<td>Varredura de vulnerabilidades em dependências de terceiros</td>
</tr>
<tr>
<td><a href="skills/代码审计/secure-code-review.md">Secure Code Review</a></td>
<td>Checklist de revisão manual de código seguro</td>
</tr>
<tr>
<td rowspan="3"><strong>🎯 Testes de Penetração</strong></td>
<td><a href="skills/渗透测试/reconnaissance.md">Reconnaissance</a></td>
<td>Técnicas de OSINT e coleta de informações</td>
</tr>
<tr>
<td><a href="skills/渗透测试/web-app-testing.md">Web App Testing</a></td>
<td>Metodologia de testes de penetração em aplicações web</td>
</tr>
<tr>
<td><a href="skills/渗透测试/report-writing.md">Report Writing</a></td>
<td>Redação profissional de relatórios de teste de penetração</td>
</tr>
<tr>
<td rowspan="3"><strong>🔧 Ferramentas de Segurança</strong></td>
<td><a href="skills/安全工具/burp-suite.md">Burp Suite</a></td>
<td>Domine o Burp Suite para testes de segurança web</td>
</tr>
<tr>
<td><a href="skills/安全工具/nmap-scanning.md">Nmap Scanning</a></td>
<td>Descoberta de rede e varredura de portas com Nmap</td>
</tr>
<tr>
<td><a href="skills/安全工具/security-automation.md">Security Automation</a></td>
<td>Pipelines e scripts automatizados de testes de segurança</td>
</tr>
</tbody>
</table>

---

## 🚀 Início Rápido

### Usando com Assistentes de IA

1. **Clone o repositório**:
   ```bash
   git clone https://github.com/your-org/awesome-security-skills.git
   ```

2. **Forneça uma habilidade ao seu assistente de IA**:
   - Copie o conteúdo do arquivo de habilidade relevante na sua conversa com IA
   - Ou aponte sua ferramenta de IA para o caminho do arquivo de habilidade
   - Exemplo: "Leia `skills/Web安全/owasp-top10.md` e siga o procedimento para avaliar minha aplicação"

3. **Siga o procedimento passo a passo**:
   - Cada habilidade contém um fluxo de trabalho completo
   - Use os templates para resultados consistentes
   - Revise a seção de armadilhas antes de começar

### Integração com Ferramentas de IA

| Ferramenta de IA | Método de Integração |
|---------|-------------------|
| **Kimi Code** | Copie o conteúdo da habilidade na conversa |
| **Cursor** | Adicione arquivos de habilidade ao `.cursorrules` ou contexto do projeto |
| **Claude** | Inclua a habilidade no prompt do sistema ou conversa |
| **ChatGPT** | Cole o arquivo de habilidade como contexto da conversa |
| **GitHub Copilot** | Referencie a habilidade em comentários de código ou workspace |

---

## 📁 Estrutura do Projeto

```
awesome-security-skills/
├── README.md                           # Este arquivo
├── LICENSE                             # Licença MIT
├── CONTRIBUTING.md                     # Guia de contribuição
├── SECURITY.md                         # Política de segurança
├── CODE_OF_CONDUCT.md                  # Código de conduta
├── CHANGELOG.md                        # Histórico de versões
├── .gitignore                          # Regras de ignorar
├── .github/
│   ├── workflows/
│   │   └── ci.yml                      # Pipeline de CI
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md              # Template de relatório de bug
│   │   ├── feature_request.md         # Template de solicitação de recurso
│   │   └── new_skill.md               # Proposta de nova habilidade
│   └── pull_request_template.md        # Template de PR
└── skills/
    ├── Web安全/                         # Segurança Web
    │   ├── owasp-top10.md
    │   ├── api-security.md
    │   └── authentication-security.md
    ├── 代码审计/                         # Auditoria de Código
    │   ├── static-analysis.md
    │   ├── dependency-audit.md
    │   └── secure-code-review.md
    ├── 渗透测试/                         # Testes de Penetração
    │   ├── reconnaissance.md
    │   ├── web-app-testing.md
    │   └── report-writing.md
    └── 安全工具/                         # Ferramentas de Segurança
        ├── burp-suite.md
        ├── nmap-scanning.md
        └── security-automation.md
```

---

## 🎓 Estrutura das Habilidades

Cada arquivo de habilidade segue uma estrutura consistente para maximizar a usabilidade:

| Seção | Propósito |
|---------|---------|
| **Quando Usar** | Cenários e gatilhos para aplicar a habilidade |
| **Pré-requisitos** | Conhecimento e acesso necessários |
| **Ferramentas** | Ferramentas recomendadas com informações de licenciamento |
| **Procedimento Passo a Passo** | Fluxo de trabalho detalhado e em fases |
| **Templates** | Templates de relatório e checklist prontos para uso |
| **Armadilhas Comuns** | Erros a evitar |
| **Considerações Legais** | Autorização, divulgação e conformidade |
| **Leitura Adicional** | Links de referência autoritativos |

---

## 🤝 Contribuição

Contribuições são bem-vindas! Consulte [CONTRIBUTING.md](CONTRIBUTING.md) para as diretrizes.

**Formas de contribuir**:
- 🐛 Reportar erros ou informações desatualizadas
- ✨ Propor novas habilidades
- 📝 Melhorar habilidades existentes
- 🌍 Traduzir habilidades para outros idiomas
- 🧪 Adicionar casos de teste e exemplos

---

## 🔗 Veja Também

- **[awesome-security](https://github.com/sbilly/awesome-security)** — Coleção de software, documentos e recursos de segurança
- **[awesome-web-security](https://github.com/qazbnm456/awesome-web-security)** — Lista de materiais e recursos de segurança web
- **[awesome-pentest](https://github.com/enaqx/awesome-pentest)** — Coleção de recursos de testes de penetração
- **[awesome-hacking](https://github.com/carpedm20/awesome-hacking)** — Lista curada de recursos de hacking
- **[awesome-malware-analysis](https://rshipp/awesome-malware-analysis)** — Ferramentas e recursos de análise de malware
- **[awesome-threat-intelligence](https://github.com/hslatman/awesome-threat-intelligence)** — Recursos de inteligência de ameaças
- **[awesome-incident-response](https://github.com/meirwah/awesome-incident-response)** — Ferramentas para resposta a incidentes
- **[awesome-reversing](https://github.com/wtsxDev/reversing)** — Recursos de engenharia reversa
- **[awesome-static-analysis](https://github.com/mre/awesome-static-analysis)** — Ferramentas de análise estática e verificação de qualidade
- **[awesome-cyber-skills](https://github.com/Dev115/awesome-cyber-skills)** — Ambientes de treinamento de habilidades cibernéticas
- **[awesome-ctf](https://github.com/apsdehal/awesome-ctf)** — Frameworks e recursos de CTF
- **[awesome-bugbounty](https://github.com/djadmin/awesome-bugbounty)** — Programas de bug bounty e writeups
- **[awesome-osint](https://github.com/jivoi/awesome-osint)** — Ferramentas OSINT incríveis
- **[awesome-devsecops](https://github.com/TaptuIT/awesome-devsecops)** — Ferramentas e recursos de DevSecOps

---

## 📜 Licença

Este projeto está licenciado sob a [MIT License](LICENSE).

---

## ⚖️ Aviso Legal

**As ferramentas, técnicas e habilidades fornecidas neste repositório são para testes de segurança autorizados e fins educacionais apenas.** Sempre obtenha permissão escrita explícita do proprietário do sistema antes de conduzir qualquer avaliação de segurança. O acesso não autorizado a sistemas de computador é um crime na maioria das jurisdições.

Os mantenedores e colaboradores deste projeto **não assumem responsabilidade** e **não são responsáveis** por qualquer uso indevido ou dano causado pelo uso das informações aqui contidas. Os usuários são os únicos responsáveis por garantir que cumprem todas as leis e regulamentos aplicáveis.

---

<div align="center">

**Feito com ❤️ pela comunidade de segurança**

[⬆ Voltar ao Topo](#-awesome-security-skills)

</div>
