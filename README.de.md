[English](README.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [Français](README.fr.md) | [Español](README.es.md) | [العربية](README.ar.md) | [한국어](README.ko.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [Deutsch](README.de.md)

<div align="center">

# 🛡️ Awesome Security Skills

**Denke wie ein Hacker, verteidige wie ein Profi.**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Security Skills](https://img.shields.io/badge/Security%20Skills-12-blue.svg)](#-skills-overview)
[![Maintained](https://img.shields.io/badge/Maintained-Yes-brightgreen.svg)](CHANGELOG.md)

**12 KI-Skills für Cybersicherheit** — eine kuratierte Sammlung strukturierter, umsetzbarer Skill-Dateien für KI-gestützte Sicherheitstests, Code-Auditing und Verteidigung.

</div>

---

## 🇬🇧 Überblick

**Awesome Security Skills** bietet bewährte, strukturierte Skill-Dateien, die KI-Assistenten zu fähigen Cybersicherheitsspezialisten machen. Jeder Skill ist ein eigenständiges Handbuch, das abdeckt: Wann verwenden, erforderliche Tools, schrittweise Verfahren, Vorlagen, Fallstricke und rechtliche Überlegungen.

Diese Skills sind konzipiert für:
- **Sicherheitsexperten**, die ihren Workflow mit KI erweitern möchten
- **Entwickler**, die Sicherheit in ihren Entwicklungszyklus integrieren
- **Teams**, die einheitliche Sicherheitstestpraktiken etablieren
- **KI-Assistenten**, die Sicherheitsbewertungen unter menschlicher Anleitung durchführen

> ⚠️ **Rechtlicher Hinweis**: Diese Skills werden **nur für autorisierte Sicherheitstests und Bildungszwecke** bereitgestellt. Holen Sie stets eine ausdrückliche schriftliche Genehmigung ein, bevor Sie ein System testen, das Ihnen nicht gehört. Unbefugter Zugriff auf Computersysteme ist in den meisten Rechtsordnungen illegal. Die Autoren übernehmen keine Haftung für Missbrauch. Siehe [SECURITY.md](SECURITY.md) für Richtlinien zur verantwortungsvollen Offenlegung.

---

## 📋 Skills-Übersicht

<table>
<thead>
<tr>
<th>Kategorie</th>
<th>Skill</th>
<th>Beschreibung</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="3"><strong>🌐 Web-Sicherheit</strong></td>
<td><a href="skills/Web安全/owasp-top10.md">OWASP Top 10</a></td>
<td>Systematische Bewertung der OWASP-Top-10-Schwachstellen</td>
</tr>
<tr>
<td><a href="skills/Web安全/api-security.md">API Security</a></td>
<td>Bewährte Sicherheitsmuster für REST-, GraphQL- und gRPC-APIs</td>
</tr>
<tr>
<td><a href="skills/Web安全/authentication-security.md">Authentication Security</a></td>
<td>Bewertung von Authentifizierungs- und Autorisierungsmechanismen</td>
</tr>
<tr>
<td rowspan="3"><strong>🔍 Code-Auditing</strong></td>
<td><a href="skills/代码审计/static-analysis.md">Static Analysis</a></td>
<td>Automatisierte statische Code-Analyse-Tools und Integration</td>
</tr>
<tr>
<td><a href="skills/代码审计/dependency-audit.md">Dependency Audit</a></td>
<td>Schwachstellen-Scan von Drittanbieter-Abhängigkeiten</td>
</tr>
<tr>
<td><a href="skills/代码审计/secure-code-review.md">Secure Code Review</a></td>
<td>Checkliste für manuellen sicheren Code-Review</td>
</tr>
<tr>
<td rowspan="3"><strong>🎯 Penetrationstests</strong></td>
<td><a href="skills/渗透测试/reconnaissance.md">Reconnaissance</a></td>
<td>OSINT- und Informationssammeltechniken</td>
</tr>
<tr>
<td><a href="skills/渗透测试/web-app-testing.md">Web App Testing</a></td>
<td>Methodik für Penetrationstests von Webanwendungen</td>
</tr>
<tr>
<td><a href="skills/渗透测试/report-writing.md">Report Writing</a></td>
<td>Professionelle Erstellung von Penetrationstest-Berichten</td>
</tr>
<tr>
<td rowspan="3"><strong>🔧 Sicherheitstools</strong></td>
<td><a href="skills/安全工具/burp-suite.md">Burp Suite</a></td>
<td>Meistern Sie Burp Suite für Web-Sicherheitstests</td>
</tr>
<tr>
<td><a href="skills/安全工具/nmap-scanning.md">Nmap Scanning</a></td>
<td>Netzwerkerkennung und Port-Scanning mit Nmap</td>
</tr>
<tr>
<td><a href="skills/安全工具/security-automation.md">Security Automation</a></td>
<td>Automatisierte Sicherheitstest-Pipelines und Skripte</td>
</tr>
</tbody>
</table>

---

## 🚀 Schnellstart

### Verwendung mit KI-Assistenten

1. **Repository klonen**:
   ```bash
   git clone https://github.com/your-org/awesome-security-skills.git
   ```

2. **Skill an Ihren KI-Assistenten weitergeben**:
   - Kopieren Sie den Inhalt der relevanten Skill-Datei in Ihr KI-Gespräch
   - Oder weisen Sie Ihr KI-Tool auf den Pfad der Skill-Datei hin
   - Beispiel: "Lies `skills/Web安全/owasp-top10.md` und folge dem Verfahren, um meine Anwendung zu bewerten"

3. **Schrittweiser Prozedur folgen**:
   - Jeder Skill enthält einen vollständigen Workflow
   - Verwenden Sie die Vorlagen für einheitliche Ergebnisse
   - Überprüfen Sie den Abschnitt zu Fallstricken vor dem Start

### Integration mit KI-Tools

| KI-Tool | Integrationsmethode |
|---------|-------------------|
| **Kimi Code** | Skill-Inhalt in das Gespräch kopieren |
| **Cursor** | Skill-Dateien zu `.cursorrules` oder Projektkontext hinzufügen |
| **Claude** | Skill in System-Prompt oder Gespräch einbeziehen |
| **ChatGPT** | Skill-Datei als Gesprächskontext einfügen |
| **GitHub Copilot** | Skill in Code-Kommentaren oder Workspace referenzieren |

---

## 📁 Projektstruktur

```
awesome-security-skills/
├── README.md                           # Diese Datei
├── LICENSE                             # MIT-Lizenz
├── CONTRIBUTING.md                     # Beitragshandbuch
├── SECURITY.md                         # Sicherheitsrichtlinie
├── CODE_OF_CONDUCT.md                  # Verhaltenskodex
├── CHANGELOG.md                        # Versionshistorie
├── .gitignore                          # Git-Ignore-Regeln
├── .github/
│   ├── workflows/
│   │   └── ci.yml                      # CI-Pipeline
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md              # Bug-Report-Vorlage
│   │   ├── feature_request.md         # Feature-Request-Vorlage
│   │   └── new_skill.md               # Neuer Skill-Vorschlag
│   └── pull_request_template.md        # PR-Vorlage
└── skills/
    ├── Web安全/                         # Web-Sicherheit
    │   ├── owasp-top10.md
    │   ├── api-security.md
    │   └── authentication-security.md
    ├── 代码审计/                         # Code-Auditing
    │   ├── static-analysis.md
    │   ├── dependency-audit.md
    │   └── secure-code-review.md
    ├── 渗透测试/                         # Penetrationstests
    │   ├── reconnaissance.md
    │   ├── web-app-testing.md
    │   └── report-writing.md
    └── 安全工具/                         # Sicherheitstools
        ├── burp-suite.md
        ├── nmap-scanning.md
        └── security-automation.md
```

---

## 🎓 Struktur der Skills

Jede Skill-Datei folgt einer einheitlichen Struktur für maximale Benutzerfreundlichkeit:

| Abschnitt | Zweck |
|---------|---------|
| **Wann verwenden** | Szenarien und Auslöser für die Anwendung des Skills |
| **Voraussetzungen** | Erforderliches Wissen und Zugang |
| **Tools** | Empfohlene Tools mit Lizenzinformationen |
| **Schritt-für-Schritt-Verfahren** | Detaillierter, phasenweiser Workflow |
| **Vorlagen** | Sofort verwendbare Berichts- und Checklisten-Vorlagen |
| **Häufige Fallstricke** | Fehler, die es zu vermeiden gilt |
| **Rechtliche Überlegungen** | Genehmigung, Offenlegung, Compliance |
| **Weiterführende Literatur** | Autoritative Referenzlinks |

---

## 🤝 Mitwirken

Beiträge sind willkommen! Siehe [CONTRIBUTING.md](CONTRIBUTING.md) für Richtlinien.

**Möglichkeiten zum Mitwirken**:
- 🐛 Fehler oder veraltete Informationen melden
- ✨ Neue Skills vorschlagen
- 📝 Bestehende Skills verbessern
- 🌍 Skills in andere Sprachen übersetzen
- 🧪 Testfälle und Beispiele hinzufügen

---

## 🔗 Siehe auch

- **[awesome-security](https://github.com/sbilly/awesome-security)** — Sammlung von Sicherheits-Software, -Bibliotheken und -Ressourcen
- **[awesome-web-security](https://github.com/qazbnm456/awesome-web-security)** — Liste von Web-Sicherheitsmaterialien und -Ressourcen
- **[awesome-pentest](https://github.com/enaqx/awesome-pentest)** — Sammlung von Penetrationstest-Ressourcen und Tools
- **[awesome-hacking](https://github.com/carpedm20/awesome-hacking)** — Kuratierte Liste von Hacking-Ressourcen
- **[awesome-malware-analysis](https://rshipp/awesome-malware-analysis)** — Tools und Ressourcen zur Malware-Analyse
- **[awesome-threat-intelligence](https://github.com/hslatman/awesome-threat-intelligence)** — Ressourcen zur Bedrohungsanalyse
- **[awesome-incident-response](https://github.com/meirwah/awesome-incident-response)** — Tools für Incident Response
- **[awesome-reversing](https://github.com/wtsxDev/reversing)** — Ressourcen für Reverse Engineering
- **[awesome-static-analysis](https://github.com/mre/awesome-static-analysis)** — Statische Analyse-Tools und Code-Qualitätsprüfer
- **[awesome-cyber-skills](https://github.com/Dev115/awesome-cyber-skills)** — Umgebungen zum Training von Cyber-Skills
- **[awesome-ctf](https://github.com/apsdehal/awesome-ctf)** — CTF-Frameworks und Ressourcen
- **[awesome-bugbounty](https://github.com/djadmin/awesome-bugbounty)** — Bug-Bounty-Programme und Writeups
- **[awesome-osint](https://github.com/jivoi/awesome-osint)** — OSINT-Tools
- **[awesome-devsecops](https://github.com/TaptuIT/awesome-devsecops)** — DevSecOps-Tools und Ressourcen

---

## 📜 Lizenz

Dieses Projekt steht unter der [MIT License](LICENSE).

---

## ⚖️ Rechtlicher Haftungsausschluss

**Die in diesem Repository bereitgestellten Tools, Techniken und Skills dienen ausschließlich autorisierten Sicherheitstests und Bildungszwecken.** Holen Sie stets eine ausdrückliche schriftliche Genehmigung des Systemeigentümers ein, bevor Sie eine Sicherheitsbewertung durchführen. Unbefugter Zugriff auf Computersysteme ist in den meisten Rechtsordnungen eine Straftat.

Die Betreiber und Mitwirkenden dieses Projekts übernehmen **keine Haftung** und sind **nicht verantwortlich** für Missbrauch oder Schäden durch die Nutzung der hier enthaltenen Informationen. Die Nutzer sind allein dafür verantwortlich, alle geltenden Gesetze und Vorschriften einzuhalten.

---

<div align="center">

**Mit ❤️ von der Security-Community erstellt**

[⬆ Zurück nach oben](#-awesome-security-skills)

</div>
