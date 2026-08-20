[English](README.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [Français](README.fr.md) | [Español](README.es.md) | [العربية](README.ar.md) | [한국어](README.ko.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [Deutsch](README.de.md)

<div align="center">

# 🛡️ Awesome Security Skills

**Pensez comme un pirate, défendez comme un pro.**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Security Skills](https://img.shields.io/badge/Security%20Skills-12-blue.svg)](#-aperçu-des-compétences)
[![Maintained](https://img.shields.io/badge/Maintained-Yes-brightgreen.svg)](CHANGELOG.md)

**12 compétences IA pour la cybersécurité** — une collection structurée et exploitable de fichiers de compétences pour les tests de sécurité assistés par IA, l'audit de code et la défense.

</div>

---

## 📋 Aperçu des compétences

<table>
<thead>
<tr>
<th>Catégorie</th>
<th>Compétence</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="3"><strong>🌐 Sécurité Web</strong></td>
<td><a href="skills/Web安全/owasp-top10.md">OWASP Top 10</a></td>
<td>Évaluation systématique des vulnérabilités OWASP Top 10</td>
</tr>
<tr>
<td><a href="skills/Web安全/api-security.md">Sécurité API</a></td>
<td>Bonnes pratiques de sécurité pour les API REST, GraphQL et gRPC</td>
</tr>
<tr>
<td><a href="skills/Web安全/authentication-security.md">Sécurité de l'authentification</a></td>
<td>Évaluation des mécanismes d'authentification et d'autorisation</td>
</tr>
<tr>
<td rowspan="3"><strong>🔍 Audit de code</strong></td>
<td><a href="skills/代码审计/static-analysis.md">Analyse statique</a></td>
<td>Outils d'analyse statique automatisée et intégration</td>
</tr>
<tr>
<td><a href="skills/代码审计/dependency-audit.md">Audit des dépendances</a></td>
<td>Scan de vulnérabilités des dépendances tierces</td>
</tr>
<tr>
<td><a href="skills/代码审计/secure-code-review.md">Revue de code sécurisée</a></td>
<td>Liste de contrôle pour la revue de code sécurisée manuelle</td>
</tr>
<tr>
<td rowspan="3"><strong>🎯 Tests de pénétration</strong></td>
<td><a href="skills/渗透测试/reconnaissance.md">Reconnaissance</a></td>
<td>Techniques d'OSINT et de collecte d'informations</td>
</tr>
<tr>
<td><a href="skills/渗透测试/web-app-testing.md">Test d'applications Web</a></td>
<td>Méthodologie de tests de pénétration d'applications Web</td>
</tr>
<tr>
<td><a href="skills/渗透测试/report-writing.md">Rédaction de rapports</a></td>
<td>Rédaction professionnelle de rapports de tests de pénétration</td>
</tr>
<tr>
<td rowspan="3"><strong>🔧 Outils de sécurité</strong></td>
<td><a href="skills/安全工具/burp-suite.md">Burp Suite</a></td>
<td>Maîtrisez Burp Suite pour les tests de sécurité Web</td>
</tr>
<tr>
<td><a href="skills/安全工具/nmap-scanning.md">Scan Nmap</a></td>
<td>Découverte réseau et scan de ports avec Nmap</td>
</tr>
<tr>
<td><a href="skills/安全工具/security-automation.md">Automatisation de sécurité</a></td>
<td>Pipelines et scripts de tests de sécurité automatisés</td>
</tr>
</tbody>
</table>

---

## 🚀 Démarrage rapide

### Utilisation avec les assistants IA

1. **Cloner le dépôt** :
   ```bash
   git clone https://github.com/your-org/awesome-security-skills.git
   ```

2. **Fournir un fichier de compétence à votre assistant IA** :
   - Copiez le contenu du fichier de compétence dans votre conversation IA
   - Ou indiquez le chemin du fichier de compétence à votre outil IA
   - Exemple : "Lisez `skills/Web安全/owasp-top10.md` et suivez sa procédure pour évaluer mon application"

3. **Suivre la procédure pas à pas** :
   - Chaque compétence contient un workflow complet
   - Utilisez les modèles pour des résultats cohérents
   - Consultez la section des pièges courants avant de commencer

### Intégration avec les outils IA

| Outil IA | Méthode d'intégration |
|----------|----------------------|
| **Kimi Code** | Copiez le contenu de la compétence dans la conversation |
| **Cursor** | Ajoutez les fichiers de compétence à `.cursorrules` ou au contexte du projet |
| **Claude** | Incluez la compétence dans le prompt système ou la conversation |
| **ChatGPT** | Collez le fichier de compétence comme contexte de conversation |
| **GitHub Copilot** | Référencez la compétence dans les commentaires de code ou l'espace de travail |

---

## 📁 Structure du projet

```
awesome-security-skills/
├── README.md                           # Ce fichier
├── LICENSE                             # Licence MIT
├── CONTRIBUTING.md                     # Guide de contribution
├── SECURITY.md                         # Politique de sécurité
├── CODE_OF_CONDUCT.md                  # Code de conduite
├── CHANGELOG.md                        # Historique des versions
├── .gitignore                          # Règles d'ignore Git
├── .github/
│   ├── workflows/
│   │   └── ci.yml                      # Pipeline CI
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md              # Modèle de rapport de bug
│   │   ├── feature_request.md         # Modèle de demande de fonctionnalité
│   │   └── new_skill.md               # Proposition de nouvelle compétence
│   └── pull_request_template.md        # Modèle de PR
└── skills/
    ├── Web安全/                         # Sécurité Web
    ├── 代码审计/                         # Audit de code
    ├── 渗透测试/                         # Tests de pénétration
    └── 安全工具/                         # Outils de sécurité
```

---

## 🎓 Structure des compétences

Chaque fichier de compétence suit une structure cohérente pour maximiser l'utilisabilité :

| Section | Objectif |
|---------|----------|
| **Quand l'utiliser** | Scénarios et déclencheurs d'application de la compétence |
| **Prérequis** | Connaissances et accès nécessaires |
| **Outils** | Outils recommandés avec informations de licence |
| **Procédure pas à pas** | Workflow détaillé et phasé |
| **Modèles** | Modèles de rapports et listes de contrôle prêts à l'emploi |
| **Pièges courants** | Erreurs à éviter |
| **Considérations légales** | Autorisation, divulgation et conformité |
| **Lectures complémentaires** | Liens de référence autoritaires |

---

## 🤝 Contribuer

Les contributions sont les bienvenues ! Consultez [CONTRIBUTING.md](CONTRIBUTING.md) pour les directives.

**Comment contribuer** :
- 🐛 Signaler des erreurs ou des informations obsolètes
- ✨ Proposer de nouvelles compétences
- 📝 Améliorer les compétences existantes
- 🌍 Traduire les compétences dans d'autres langues
- 🧪 Ajouter des cas de test et des exemples

---

## 🔗 Voir aussi

Autres projets exceptionnels de l'écosystème :

- **[awesome-security](https://github.com/sbilly/awesome-security)** — Collection de logiciels, bibliothèques, documents, livres et ressources exceptionnels sur la sécurité.
- **[awesome-web-security](https://github.com/qazbnm456/awesome-web-security)** — Liste de ressources et documents sur la sécurité Web.
- **[awesome-pentest](https://github.com/enaqx/awesome-pentest)** — Collection de ressources, outils et autres pépites pour les tests de pénétration.
- **[awesome-hacking](https://github.com/carpedm20/awesome-hacking)** — Liste curatée de ressources passionnantes sur le hacking.
- **[awesome-malware-analysis](https://rshipp/awesome-malware-analysis)** — Liste curatée d'outils et de ressources d'analyse de malware.
- **[awesome-threat-intelligence](https://github.com/hslatman/awesome-threat-intelligence)** — Liste curatée de ressources sur le renforcement des menaces.
- **[awesome-incident-response](https://github.com/meirwah/awesome-incident-response)** — Liste curatée d'outils pour la réponse aux incidents.
- **[awesome-reversing](https://github.com/wtsxDev/reversing)** — Liste curatée de ressources d'ingénierie inverse.
- **[awesome-static-analysis](https://github.com/mre/awesome-static-analysis)** — Liste curatée d'outils d'analyse statique, de linters et de vérificateurs de qualité de code.
- **[awesome-cyber-skills](https://github.com/Dev115/awesome-cyber-skills)** — Liste curatée d'environnements de hacking pour entraîner vos compétences en cybersécurité.
- **[awesome-ctf](https://github.com/apsdehal/awesome-ctf)** — Liste curatée de frameworks, bibliothèques, ressources et logiciels CTF.
- **[awesome-bugbounty](https://github.com/djadmin/awesome-bugbounty)** — Liste complète des programmes de bug bounty et des write-ups.
- **[awesome-osint](https://github.com/jivoi/awesome-osint)** — Liste curatée d'outils OSINT étonnants.
- **[awesome-devsecops](https://github.com/TaptuIT/awesome-devsecops)** — Liste curatée d'outils, de ressources et de références DevSecOps.

---

## 📜 Licence

Ce projet est sous [licence MIT](LICENSE).

---

## ⚖️ Avertissement juridique

**Les outils, techniques et compétences fournis dans ce dépôt sont destinés uniquement aux tests de sécurité autorisés et aux fins éducatives.** Obtenez toujours une autorisation écrite explicite du propriétaire du système avant de mener toute évaluation de sécurité. L'accès non autorisé aux systèmes informatiques est une infraction pénale dans la plupart des juridictions, y compris en vertu du Computer Fraud and Abuse Act (CFAA) aux États-Unis, du Computer Misuse Act au Royaume-Uni et de lois similaires dans le monde entier.

Les mainteneurs et contributeurs de ce projet n'assument **aucune responsabilité** et ne sont **pas responsables** de tout abus ou dommage causé par l'utilisation des informations contenues ici. Les utilisateurs sont seuls responsables de s'assurer qu'ils respectent toutes les lois et réglementations applicables.

---

<div align="center">

**Réalisé avec ❤️ par la communauté sécurité**

[⬆ Retour en haut](#-awesome-security-skills)

</div>
