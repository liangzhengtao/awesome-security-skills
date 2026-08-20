[English](README.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [Français](README.fr.md) | [Español](README.es.md) | [العربية](README.ar.md) | [한국어](README.ko.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [Deutsch](README.de.md)

<div align="center">

# 🛡️ Awesome Security Skills

**فكر كهاكر، دافع كمحترف.**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Security Skills](https://img.shields.io/badge/Security%20Skills-12-blue.svg)](#-skills-overview)
[![Maintained](https://img.shields.io/badge/Maintained-Yes-brightgreen.svg)](CHANGELOG.md)

**12 مهارة ذكاء اصطناعي للأمن السيبراني** — مجموعة منتقاة من ملفات المهارات المنظمة والقابلة للتنفيذ لاختبارات أمنية بمساعدة الذكاء الاصطناعي، وتدقيق الشيفرة، والدفاع.

</div>

---

## 🇬🇧 نظرة عامة

يوفر **Awesome Security Skills** ملفات مهارات مُجربة ومنظمة تُحوّل مساعدي الذكاء الاصطناعي إلى متخصصين أمن سيبراني فاعلين. كل مهارة هي دليل تشغيل متكامل يغطي متى تُستخدم، والأدوات المطلوبة، وإجراءات خطوة بخطوة، والقوالب، والمزالق، والاعتبارات القانونية.

تم تصميم هذه المهارات لـ:
- **المتخصصين في الأمن** الذين يرغبون في تعزيز سير عملهم بالذكاء الاصطناعي
- **المطورين** الذين يدمجون الأمان في دورة حياتهم التطويرية
- **الفرق** التي تُنشئ ممارسات اختبار أمني متسقة
- **مساعدي الذكاء الاصطناعي** الذين يُنفذون تقييمات أمنية تحت إشراف بشري

> ⚠️ **إخلاء المسؤولية القانونية**: تُقدَّم هذه المهارات **للاختبار الأمني المعتمد والأغراض التعليمية فقط**. احصل دائمًا على إذن خطي صريح قبل اختبار أي نظام لا تملكه. الوصول غير المصرح به إلى أنظمة الحاسوب غير قانوني في معظم الولايات القضائية. لا يتحمل المؤلفون أي مسؤولية عن سوء الاستخدام. راجع [SECURITY.md](SECURITY.md) لإرشادات الإفصاح المسؤول.

---

## 📋 نظرة عامة على المهارات

<table>
<thead>
<tr>
<th>الفئة</th>
<th>المهارة</th>
<th>الوصف</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="3"><strong>🌐 أمن الويب</strong></td>
<td><a href="skills/Web安全/owasp-top10.md">OWASP Top 10</a></td>
<td>تقييم منهجي لثغرات OWASP العشر الأولى</td>
</tr>
<tr>
<td><a href="skills/Web安全/api-security.md">API Security</a></td>
<td>أنماط مُجربة لأمن واجهات REST وGraphQL وgRPC</td>
</tr>
<tr>
<td><a href="skills/Web安全/authentication-security.md">Authentication Security</a></td>
<td>تقييم آليات المصادقة والتفويض</td>
</tr>
<tr>
<td rowspan="3"><strong>🔍 تدقيق الشيفرة</strong></td>
<td><a href="skills/代码审计/static-analysis.md">Static Analysis</a></td>
<td>أدوات التحليل الثابت الآلي والتكامل</td>
</tr>
<tr>
<td><a href="skills/代码审计/dependency-audit.md">Dependency Audit</a></td>
<td>فحص ثغرات التبعيات من طرف ثالث</td>
</tr>
<tr>
<td><a href="skills/代码审计/secure-code-review.md">Secure Code Review</a></td>
<td>قائمة مراجعة الشيفرة الآمنة اليدوية</td>
</tr>
<tr>
<td rowspan="3"><strong>🎯 اختبار الاختراق</strong></td>
<td><a href="skills/渗透测试/reconnaissance.md">Reconnaissance</a></td>
<td>تقنيات OSINT وجمع المعلومات</td>
</tr>
<tr>
<td><a href="skills/渗透测试/web-app-testing.md">Web App Testing</a></td>
<td>منهجية اختبار اختراق تطبيقات الويب</td>
</tr>
<tr>
<td><a href="skills/渗透测试/report-writing.md">Report Writing</a></td>
<td>كتابة تقارير اختبار اختراق احترافية</td>
</tr>
<tr>
<td rowspan="3"><strong>🔧 أدوات الأمان</strong></td>
<td><a href="skills/安全工具/burp-suite.md">Burp Suite</a></td>
<td>إتقان Burp Suite لاختبار أمن الويب</td>
</tr>
<tr>
<td><a href="skills/安全工具/nmap-scanning.md">Nmap Scanning</a></td>
<td>اكتشاف الشبكات وفحص المنافذ باستخدام Nmap</td>
</tr>
<tr>
<td><a href="skills/安全工具/security-automation.md">Security Automation</a></td>
<td>خطوط أنابيب وبرامج نصية للاختبار الأمني الآلي</td>
</tr>
</tbody>
</table>

---

## 🚀 البدء السريع

### الاستخدام مع مساعدي الذكاء الاصطناعي

1. **استنساخ المستودع**:
   ```bash
   git clone https://github.com/your-org/awesome-security-skills.git
   ```

2. **قدّم مهارة لمساعد الذكاء الاصطناعي**:
   - انسخ محتوى ملف المهارة ذات الصلة في محادثتك مع الذكاء الاصطناعي
   - أو وجّه أداة الذكاء الاصطناعي إلى مسار ملف المهارة
   - مثال: "اقرأ `skills/Web安全/owasp-top10.md` واتبع إجراءاتها لتقييم تطبيقي"

3. **اتبع الإجراء خطوة بخطوة**:
   - تحتوي كل مهارة على سير عمل متكامل
   - استخدم القوالب للحصول على نتائج متسقة
   - راجع قسم المزالق قبل البدء

### التكامل مع أدوات الذكاء الاصطناعي

| أداة الذكاء الاصطناعي | طريقة التكامل |
|---------|-------------------|
| **Kimi Code** | انسخ محتوى المهارة في المحادثة |
| **Cursor** | أضف ملفات المهارات إلى `.cursorrules` أو سياق المشروع |
| **Claude** | أدرج المهارة في موجه النظام أو المحادثة |
| **ChatGPT** | الصق ملف المهارة كسياق للمحادثة |
| **GitHub Copilot** | ارجع للمهارة في تعليقات الكود أو مساحة العمل |

---

## 📁 هيكل المشروع

```
awesome-security-skills/
├── README.md                           # هذا الملف
├── LICENSE                             # رخصة MIT
├── CONTRIBUTING.md                     # دليل المساهمة
├── SECURITY.md                         # سياسة الأمان
├── CODE_OF_CONDUCT.md                  # قواعد السلوك
├── CHANGELOG.md                        # سجل الإصدارات
├── .gitignore                          # قواعد التجاهل
├── .github/
│   ├── workflows/
│   │   └── ci.yml                      # خط أنابيب CI
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md              # قالب بلاغ خلل
│   │   ├── feature_request.md         # قالب طلب ميزة
│   │   └── new_skill.md               # اقتراح مهارة جديدة
│   └── pull_request_template.md        # قالب طلب سحب
└── skills/
    ├── Web安全/                         # أمن الويب
    │   ├── owasp-top10.md
    │   ├── api-security.md
    │   └── authentication-security.md
    ├── 代码审计/                         # تدقيق الشيفرة
    │   ├── static-analysis.md
    │   ├── dependency-audit.md
    │   └── secure-code-review.md
    ├── 渗透测试/                         # اختبار الاختراق
    │   ├── reconnaissance.md
    │   ├── web-app-testing.md
    │   └── report-writing.md
    └── 安全工具/                         # أدوات الأمان
        ├── burp-suite.md
        ├── nmap-scanning.md
        └── security-automation.md
```

---

## 🎓 كيف يتم تنظيم المهارات

يتبع كل ملف مهارة هيكلًا متسقًا لتعظيم سهولة الاستخدام:

| القسم | الغرض |
|---------|---------|
| **متى تستخدم** | السيناريوهات ومحفزات تطبيق المهارة |
| **المتطلبات المسبقة** | المعرفة والوصول المطلوبان |
| **الأدوات** | الأدوات الموصى بها مع معلومات الترخيص |
| **الإجراء خطوة بخطوة** | سير عمل مُفصّل ومرحلي |
| **القوالب** | قوالب تقارير وقوائم جاهزة للاستخدام |
| **المزالق الشائعة** | أخطاء يجب تجنبها |
| **الاعتبارات القانونية** | التفويض، الإفصاح، والامتثال |
| **مزيد من القراءة** | روابط مراجع موثوقة |

---

## 🤝 المساهمة

نرحب بالمساهمات! يرجى رؤية [CONTRIBUTING.md](CONTRIBUTING.md) للإرشادات.

**طرق المساهمة**:
- 🐛 الإبلاغ عن أخطاء أو معلومات قديمة
- ✨ اقتراح مهارات جديدة
- 📝 تحسين المهارات الحالية
- 🌍 ترجمة المهارات إلى لغات أخرى
- 🧪 إضافة حالات اختبار وأمثلة

---

## 🔗 انظر أيضًا

- **[awesome-security](https://github.com/sbilly/awesome-security)** — مجموعة من البرامج والمكتبات والوثائق والكتب والموارد الأمنية الممتازة.
- **[awesome-web-security](https://github.com/qazbnm456/awesome-web-security)** — قائمة بمواد وموارد أمن الويب.
- **[awesome-pentest](https://github.com/enaqx/awesome-pentest)** — مجموعة موارد اختبار الاختراق الممتازة.
- **[awesome-hacking](https://github.com/carpedm20/awesome-hacking)** — قائمة منتقاة من موارد الاختراق الممتعة.
- **[awesome-malware-analysis](https://rshipp/awesome-malware-analysis)** — قائمة أدوات وموارد تحليل البرمجيات الخبيثة.
- **[awesome-threat-intelligence](https://github.com/hslatman/awesome-threat-intelligence)** — قائمة موارد الاستخبارات التهديدية.
- **[awesome-incident-response](https://github.com/meirwah/awesome-incident-response)** — قائمة أدوات الاستجابة للحوادث.
- **[awesome-reversing](https://github.com/wtsxDev/reversing)** — قائمة موارد الهندسة العكسية.
- **[awesome-static-analysis](https://github.com/mre/awesome-static-analysis)** — قائمة أدوات التحليل الثابت وفحص جودة الكود.
- **[awesome-cyber-skills](https://github.com/Dev115/awesome-cyber-skills)** — قائمة بيئات تدريب مهارات الأمن السيبراني.
- **[awesome-ctf](https://github.com/apsdehal/awesome-ctf)** — قائمة أطر وموارد CTF.
- **[awesome-bugbounty](https://github.com/djadmin/awesome-bugbounty)** — قائمة كاملة ببرامج مكافآت الأخطاء.
- **[awesome-osint](https://github.com/jivoi/awesome-osint)** — قائمة أدوات OSINT الممتازة.
- **[awesome-devsecops](https://github.com/TaptuIT/awesome-devsecops)** — قائمة أدوات وموارد DevSecOps.

---

## 📜 الترخيص

مرخص بموجب [MIT License](LICENSE).

---

## ⚖️ إخلاء المسؤولية القانونية

**الأدوات والتقنيات والمهارات المقدمة في هذا المستودع مخصصة للاختبار الأمني المعتمد والأغراض التعليمية فقط.** احصل دائمًا على إذن خطي صريح من مالك النظام قبل إجراء أي تقييم أمني. يُعد الوصول غير المصرح به إلى أنظمة الحاسوب جريمة جنائية في معظم الولايات القضائية.

لا يتحمل القائمون على المشروع والمساهمون **أي مسؤولية** و**ليسوا مسؤولين** عن أي سوء استخدام أو ضرر ناتج عن استخدام المعلومات الواردة هنا. يتحمل المستخدمون وحدهم مسؤولية الامتثال لجميع القوانين واللوائح المعمول بها.

---

<div align="center">

**صنع بـ ❤️ بواسطة مجتمع الأمن**

[⬆ العودة للأعلى](#-awesome-security-skills)

</div>
