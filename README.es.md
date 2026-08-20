[English](README.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [Français](README.fr.md) | [Español](README.es.md) | [العربية](README.ar.md) | [한국어](README.ko.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [Deutsch](README.de.md)

<div align="center">

# 🛡️ Awesome Security Skills

**Piensa como un hacker, defiende como un profesional.**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Security Skills](https://img.shields.io/badge/Security%20Skills-12-blue.svg)](#-resumen-de-habilidades)
[![Maintained](https://img.shields.io/badge/Maintained-Yes-brightgreen.svg)](CHANGELOG.md)

**12 habilidades de IA para ciberseguridad** — una colección estructurada y accionable de archivos de habilidades para pruebas de seguridad asistidas por IA, auditoría de código y defensa.

</div>

---

## 📋 Resumen de habilidades

<table>
<thead>
<tr>
<th>Categoría</th>
<th>Habilidad</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="3"><strong>🌐 Seguridad Web</strong></td>
<td><a href="skills/Web安全/owasp-top10.md">OWASP Top 10</a></td>
<td>Evaluación sistemática de vulnerabilidades OWASP Top 10</td>
</tr>
<tr>
<td><a href="skills/Web安全/api-security.md">Seguridad API</a></td>
<td>Mejores prácticas de seguridad para API REST, GraphQL y gRPC</td>
</tr>
<tr>
<td><a href="skills/Web安全/authentication-security.md">Seguridad de autenticación</a></td>
<td>Evaluación de mecanismos de autenticación y autorización</td>
</tr>
<tr>
<td rowspan="3"><strong>🔍 Auditoría de código</strong></td>
<td><a href="skills/代码审计/static-analysis.md">Análisis estático</a></td>
<td>Herramientas de análisis estático automatizado e integración</td>
</tr>
<tr>
<td><a href="skills/代码审计/dependency-audit.md">Auditoría de dependencias</a></td>
<td>Escaneo de vulnerabilidades en dependencias de terceros</td>
</tr>
<tr>
<td><a href="skills/代码审计/secure-code-review.md">Revisión segura de código</a></td>
<td>Lista de verificación para la revisión manual de código seguro</td>
</tr>
<tr>
<td rowspan="3"><strong>🎯 Pruebas de penetración</strong></td>
<td><a href="skills/渗透测试/reconnaissance.md">Reconocimiento</a></td>
<td>Técnicas de OSINT y recopilación de información</td>
</tr>
<tr>
<td><a href="skills/渗透测试/web-app-testing.md">Prueba de apps Web</a></td>
<td>Metodología de pruebas de penetración de aplicaciones Web</td>
</tr>
<tr>
<td><a href="skills/渗透测试/report-writing.md">Redacción de informes</a></td>
<td>Redacción profesional de informes de pruebas de penetración</td>
</tr>
<tr>
<td rowspan="3"><strong>🔧 Herramientas de seguridad</strong></td>
<td><a href="skills/安全工具/burp-suite.md">Burp Suite</a></td>
<td>Domina Burp Suite para pruebas de seguridad Web</td>
</tr>
<tr>
<td><a href="skills/安全工具/nmap-scanning.md">Escaneo con Nmap</a></td>
<td>Descubrimiento de red y escaneo de puertos con Nmap</td>
</tr>
<tr>
<td><a href="skills/安全工具/security-automation.md">Automatización de seguridad</a></td>
<td>Pipelines y scripts automatizados de pruebas de seguridad</td>
</tr>
</tbody>
</table>

---

## 🚀 Inicio rápido

### Uso con asistentes IA

1. **Clonar el repositorio**:
   ```bash
   git clone https://github.com/your-org/awesome-security-skills.git
   ```

2. **Proporcionar un archivo de habilidad a tu asistente IA**:
   - Copia el contenido del archivo de habilidad en tu conversación IA
   - O indica la ruta del archivo de habilidad a tu herramienta IA
   - Ejemplo: "Lee `skills/Web安全/owasp-top10.md` y sigue su procedimiento para evaluar mi aplicación"

3. **Seguir el procedimiento paso a paso**:
   - Cada habilidad contiene un flujo de trabajo completo
   - Usa las plantillas para resultados consistentes
   - Revisa la sección de errores comunes antes de comenzar

### Integración con herramientas IA

| Herramienta IA | Método de integración |
|----------------|----------------------|
| **Kimi Code** | Copia el contenido de la habilidad en la conversación |
| **Cursor** | Agrega archivos de habilidad a `.cursorrules` o al contexto del proyecto |
| **Claude** | Incluye la habilidad en el prompt del sistema o en la conversación |
| **ChatGPT** | Pega el archivo de habilidad como contexto de conversación |
| **GitHub Copilot** | Referencia la habilidad en comentarios de código o en el espacio de trabajo |

---

## 📁 Estructura del proyecto

```
awesome-security-skills/
├── README.md                           # Este archivo
├── LICENSE                             # Licencia MIT
├── CONTRIBUTING.md                     # Guía de contribución
├── SECURITY.md                         # Política de seguridad
├── CODE_OF_CONDUCT.md                  # Código de conducta
├── CHANGELOG.md                        # Historial de versiones
├── .gitignore                          # Reglas de ignorado de Git
├── .github/
│   ├── workflows/
│   │   └── ci.yml                      # Pipeline de CI
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md              # Plantilla de reporte de bug
│   │   ├── feature_request.md         # Plantilla de solicitud de función
│   │   └── new_skill.md               # Propuesta de nueva habilidad
│   └── pull_request_template.md        # Plantilla de PR
└── skills/
    ├── Web安全/                         # Seguridad Web
    ├── 代码审计/                         # Auditoría de código
    ├── 渗透测试/                         # Pruebas de penetración
    └── 安全工具/                         # Herramientas de seguridad
```

---

## 🎓 Estructura de las habilidades

Cada archivo de habilidad sigue una estructura consistente para maximizar la usabilidad:

| Sección | Propósito |
|---------|-----------|
| **Cuándo usarla** | Escenarios y desencadenantes para aplicar la habilidad |
| **Prerrequisitos** | Conocimiento y acceso necesarios |
| **Herramientas** | Herramientas recomendadas con información de licencia |
| **Procedimiento paso a paso** | Flujo de trabajo detallado y por fases |
| **Plantillas** | Plantillas de informes y listas de verificación listas para usar |
| **Errores comunes** | Errores a evitar |
| **Consideraciones legales** | Autorización, divulgación y cumplimiento |
| **Lecturas adicionales** | Enlaces de referencia autorizados |

---

## 🤝 Contribuir

¡Las contribuciones son bienvenidas! Consulta [CONTRIBUTING.md](CONTRIBUTING.md) para las directrices.

**Formas de contribuir**:
- 🐛 Reportar errores u obsolecencias
- ✨ Proponer nuevas habilidades
- 📝 Mejorar habilidades existentes
- 🌍 Traducir habilidades a otros idiomas
- 🧪 Agregar casos de prueba y ejemplos

---

## 🔗 Ver también

Otros proyectos excelentes del ecosistema:

- **[awesome-security](https://github.com/sbilly/awesome-security)** — Colección de software, bibliotecas, documentos, libros y recursos excelentes sobre seguridad.
- **[awesome-web-security](https://github.com/qazbnm456/awesome-web-security)** — Lista de materiales y recursos de seguridad Web.
- **[awesome-pentest](https://github.com/enaqx/awesome-pentest)** — Colección de recursos, herramientas y otras joyas para pruebas de penetración.
- **[awesome-hacking](https://github.com/carpedm20/awesome-hacking)** — Lista curada de recursos fascinantes sobre hacking.
- **[awesome-malware-analysis](https://rshipp/awesome-malware-analysis)** — Lista curada de herramientas y recursos de análisis de malware.
- **[awesome-threat-intelligence](https://github.com/hslatman/awesome-threat-intelligence)** — Lista curada de recursos de inteligencia de amenazas.
- **[awesome-incident-response](https://github.com/meirwah/awesome-incident-response)** — Lista curada de herramientas para respuesta a incidentes.
- **[awesome-reversing](https://github.com/wtsxDev/reversing)** — Lista curada de recursos de ingeniería inversa.
- **[awesome-static-analysis](https://github.com/mre/awesome-static-analysis)** — Lista curada de herramientas de análisis estático, linters y verificadores de calidad de código.
- **[awesome-cyber-skills](https://github.com/Dev115/awesome-cyber-skills)** — Lista curada de entornos de hacking para entrenar tus habilidades en ciberseguridad.
- **[awesome-ctf](https://github.com/apsdehal/awesome-ctf)** — Lista curada de frameworks, bibliotecas, recursos y software CTF.
- **[awesome-bugbounty](https://github.com/djadmin/awesome-bugbounty)** — Lista completa de programas de bug bounty y write-ups.
- **[awesome-osint](https://github.com/jivoi/awesome-osint)** — Lista curada de herramientas OSINT increíbles.
- **[awesome-devsecops](https://github.com/TaptuIT/awesome-devsecops)** — Lista curada de herramientas, recursos y referencias de DevSecOps.

---

## 📜 Licencia

Este proyecto está bajo la [licencia MIT](LICENSE).

---

## ⚖️ Aviso legal

**Las herramientas, técnicas y habilidades proporcionadas en este repositorio son solo para pruebas de seguridad autorizadas y fines educativos.** Siempre obtén permiso escrito explícito del propietario del sistema antes de realizar cualquier evaluación de seguridad. El acceso no autorizado a sistemas informáticos es un delito penal en la mayoría de las jurisdicciones, incluyendo bajo la Ley de Fraude y Abuso Informático (CFAA) en los Estados Unidos, la Ley de Uso Indebido de Computadoras en el Reino Unido y leyes similares en todo el mundo.

Los mantenedores y contribuidores de este proyecto **no asumen ninguna responsabilidad** y **no son responsables** de cualquier mal uso o daño causado por el uso de la información contenida aquí. Los usuarios son los únicos responsables de garantizar el cumplimiento de todas las leyes y regulaciones aplicables.

---

<div align="center">

**Hecho con ❤️ por la comunidad de seguridad**

[⬆ Volver arriba](#-awesome-security-skills)

</div>
