[English](README.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [Français](README.fr.md) | [Español](README.es.md) | [العربية](README.ar.md) | [한국어](README.ko.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [Deutsch](README.de.md)

<div align="center">

# 🛡️ Awesome Security Skills

**Думай как хакер, защищайся как профессионал.**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Security Skills](https://img.shields.io/badge/Security%20Skills-12-blue.svg)](#-skills-overview)
[![Maintained](https://img.shields.io/badge/Maintained-Yes-brightgreen.svg)](CHANGELOG.md)

**12 навыков ИИ для кибербезопасности** — тщательно подобранная коллекция структурированных файлов навыков для тестирования безопасности с помощью ИИ, аудита кода и защиты.

</div>

---

## 🇬🇧 Обзор

**Awesome Security Skills** предоставляет проверенные структурированные файлы навыков, которые превращают ИИ-ассистентов в компетентных специалистов по кибербезопасности. Каждый навык — это автономный справочник, охватывающий когда использовать, необходимые инструменты, пошаговые процедуры, шаблоны, подводные камни и юридические аспекты.

Эти навыки предназначены для:
- **Специалистов по безопасности**, которые хотят дополнить свой рабочий процесс ИИ
- **Разработчиков**, внедряющих безопасность в жизненный цикл разработки
- **Команд**, устанавливающих единые практики тестирования безопасности
- **ИИ-ассистентов**, выполняющих оценку безопасности под руководством человека

> ⚠️ **Юридическое предупреждение**: Эти навыки предоставляются **только для авторизованного тестирования безопасности и образовательных целей**. Всегда получайте явное письменное разрешение перед тестированием любой системы, которой вы не владеете. Несанкционированный доступ к компьютерным системам является незаконным в большинстве юрисдикций. Авторы не несут ответственности за неправильное использование. См. [SECURITY.md](SECURITY.md) для правил ответственного раскрытия.

---

## 📋 Обзор навыков

<table>
<thead>
<tr>
<th>Категория</th>
<th>Навык</th>
<th>Описание</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="3"><strong>🌐 Веб-безопасность</strong></td>
<td><a href="skills/Web安全/owasp-top10.md">OWASP Top 10</a></td>
<td>Систематическая оценка уязвимостей OWASP Top 10</td>
</tr>
<tr>
<td><a href="skills/Web安全/api-security.md">API Security</a></td>
<td>Проверенные паттерны безопасности REST, GraphQL и gRPC API</td>
</tr>
<tr>
<td><a href="skills/Web安全/authentication-security.md">Authentication Security</a></td>
<td>Оценка механизмов аутентификации и авторизации</td>
</tr>
<tr>
<td rowspan="3"><strong>🔍 Аудит кода</strong></td>
<td><a href="skills/代码审计/static-analysis.md">Static Analysis</a></td>
<td>Инструменты автоматического статического анализа и интеграция</td>
</tr>
<tr>
<td><a href="skills/代码审计/dependency-audit.md">Dependency Audit</a></td>
<td>Сканирование уязвимостей сторонних зависимостей</td>
</tr>
<tr>
<td><a href="skills/代码审计/secure-code-review.md">Secure Code Review</a></td>
<td>Чек-лист ручного обзора безопасного кода</td>
</tr>
<tr>
<td rowspan="3"><strong>🎯 Тестирование на проникновение</strong></td>
<td><a href="skills/渗透测试/reconnaissance.md">Reconnaissance</a></td>
<td>Техники OSINT и сбора информации</td>
</tr>
<tr>
<td><a href="skills/渗透测试/web-app-testing.md">Web App Testing</a></td>
<td>Методология тестирования на проникновение веб-приложений</td>
</tr>
<tr>
<td><a href="skills/渗透测试/report-writing.md">Report Writing</a></td>
<td>Профессиональное составление отчётов о тестировании</td>
</tr>
<tr>
<td rowspan="3"><strong>🔧 Инструменты безопасности</strong></td>
<td><a href="skills/安全工具/burp-suite.md">Burp Suite</a></td>
<td>Освойте Burp Suite для тестирования веб-безопасности</td>
</tr>
<tr>
<td><a href="skills/安全工具/nmap-scanning.md">Nmap Scanning</a></td>
<td>Обнаружение сети и сканирование портов с помощью Nmap</td>
</tr>
<tr>
<td><a href="skills/安全工具/security-automation.md">Security Automation</a></td>
<td>Автоматизированные пайплайны и скрипты тестирования безопасности</td>
</tr>
</tbody>
</table>

---

## 🚀 Быстрый старт

### Использование с ИИ-ассистентами

1. **Клонируйте репозиторий**:
   ```bash
   git clone https://github.com/your-org/awesome-security-skills.git
   ```

2. **Передайте навык вашему ИИ-ассистенту**:
   - Скопируйте содержимое файла навыка в вашу беседу с ИИ
   - Или укажите вашему ИИ-инструменту путь к файлу навыка
   - Пример: "Прочитай `skills/Web安全/owasp-top10.md` и следуй процедуре для оценки моего приложения"

3. **Следуйте пошаговой процедуре**:
   - Каждый навык содержит полный рабочий процесс
   - Используйте шаблоны для единообразных результатов
   - Изучите раздел с подводными камнями перед началом

### Интеграция с ИИ-инструментами

| ИИ-инструмент | Метод интеграции |
|---------|-------------------|
| **Kimi Code** | Скопируйте содержимое навыка в беседу |
| **Cursor** | Добавьте файлы навыков в `.cursorrules` или контекст проекта |
| **Claude** | Включите навык в системный промпт или беседу |
| **ChatGPT** | Вставьте файл навыка как контекст беседы |
| **GitHub Copilot** | Ссылайтесь на навык в комментариях к коду |

---

## 📁 Структура проекта

```
awesome-security-skills/
├── README.md                           # Этот файл
├── LICENSE                             # Лицензия MIT
├── CONTRIBUTING.md                     # Руководство по вкладу
├── SECURITY.md                         # Политика безопасности
├── CODE_OF_CONDUCT.md                  # Кодекс поведения
├── CHANGELOG.md                        # История версий
├── .gitignore                          # Правила игнорирования
├── .github/
│   ├── workflows/
│   │   └── ci.yml                      # CI-пайплайн
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md              # Шаблон отчёта об ошибке
│   │   ├── feature_request.md         # Шаблон запроса функции
│   │   └── new_skill.md               # Предложение нового навыка
│   └── pull_request_template.md        # Шаблон PR
└── skills/
    ├── Web安全/                         # Веб-безопасность
    │   ├── owasp-top10.md
    │   ├── api-security.md
    │   └── authentication-security.md
    ├── 代码审计/                         # Аудит кода
    │   ├── static-analysis.md
    │   ├── dependency-audit.md
    │   └── secure-code-review.md
    ├── 渗透测试/                         # Тестирование на проникновение
    │   ├── reconnaissance.md
    │   ├── web-app-testing.md
    │   └── report-writing.md
    └── 安全工具/                         # Инструменты безопасности
        ├── burp-suite.md
        ├── nmap-scanning.md
        └── security-automation.md
```

---

## 🎓 Структура навыков

Каждый файл навыка следует единообразной структуре для максимального удобства:

| Раздел | Назначение |
|---------|---------|
| **Когда использовать** | Сценарии и триггеры применения навыка |
| **Необходимые знания** | Требуемые знания и доступ |
| **Инструменты** | Рекомендуемые инструменты с информацией о лицензировании |
| **Пошаговая процедура** | Детальный поэтапный рабочий процесс |
| **Шаблоны** | Готовые к использованию шаблоны отчётов и чек-листы |
| **Распространённые ошибки** | Ошибки, которых следует избегать |
| **Юридические аспекты** | Авторизация, раскрытие, соответствие |
| **Дополнительная литература** | Авторитетные ссылки |

---

## 🤝 Участие

Приветствуются вклады! Смотрите [CONTRIBUTING.md](CONTRIBUTING.md) для руководства.

**Способы участия**:
- 🐛 Сообщайте об ошибках или устаревшей информации
- ✨ Предлагайте новые навыки
- 📝 Улучшайте существующие навыки
- 🌍 Переводите навыки на другие языки
- 🧪 Добавляйте тестовые примеры

---

## 🔗 Также смотрите

- **[awesome-security](https://github.com/sbilly/awesome-security)** — Коллекция программ, библиотек и ресурсов по безопасности
- **[awesome-web-security](https://github.com/qazbnm456/awesome-web-security)** — Список материалов и ресурсов по веб-безопасности
- **[awesome-pentest](https://github.com/enaqx/awesome-pentest)** — Ресурсы и инструменты для тестирования на проникновение
- **[awesome-hacking](https://github.com/carpedm20/awesome-hacking)** — Кураторский список ресурсов по хакингу
- **[awesome-malware-analysis](https://rshipp/awesome-malware-analysis)** — Инструменты и ресурсы анализа вредоносного ПО
- **[awesome-threat-intelligence](https://github.com/hslatman/awesome-threat-intelligence)** — Ресурсы анализа угроз
- **[awesome-incident-response](https://github.com/meirwah/awesome-incident-response)** — Инструменты реагирования на инциденты
- **[awesome-reversing](https://github.com/wtsxDev/reversing)** — Ресурсы реверс-инжиниринга
- **[awesome-static-analysis](https://github.com/mre/awesome-static-analysis)** — Инструменты статического анализа и проверки качества кода
- **[awesome-cyber-skills](https://github.com/Dev115/awesome-cyber-skills)** — Среды обучения навыкам кибербезопасности
- **[awesome-ctf](https://github.com/apsdehal/awesome-ctf)** — Фреймворки и ресурсы CTF
- **[awesome-bugbounty](https://github.com/djadmin/awesome-bugbounty)** — Программы bug bounty и отчёты
- **[awesome-osint](https://github.com/jivoi/awesome-osint)** — Инструменты OSINT
- **[awesome-devsecops](https://github.com/TaptuIT/awesome-devsecops)** — Инструменты и ресурсы DevSecOps

---

## 📜 Лицензия

Проект распространяется под [MIT License](LICENSE).

---

## ⚖️ Юридическое предупреждение

**Инструменты, техники и навыки, представленные в этом репозитории, предназначены только для авторизованного тестирования безопасности и образовательных целей.** Всегда получайте явное письменное разрешение владельца системы перед проведением любой оценки безопасности. Несанкционированный доступ к компьютерным системам является уголовным преступлением в большинстве юрисдикций.

Мейнтейнеры и участники этого проекта **не несут ответственности** за любое неправильное использование или ущерб, вызванный использованием содержащейся здесь информации. Пользователи несут единоличную ответственность за соблюдение всех применимых законов и нормативных актов.

---

<div align="center">

**Создано с ❤️ сообществом безопасности**

[⬆ Наверх](#-awesome-security-skills)

</div>
