[English](README.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [Français](README.fr.md) | [Español](README.es.md) | [العربية](README.ar.md) | [한국어](README.ko.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [Deutsch](README.de.md)

<div align="center">

# 🛡️ Awesome Security Skills

**해커처럼 생각하고, 프로처럼 방어하라.**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Security Skills](https://img.shields.io/badge/Security%20Skills-12-blue.svg)](#-skills-overview)
[![Maintained](https://img.shields.io/badge/Maintained-Yes-brightgreen.svg)](CHANGELOG.md)

**사이버보안을 위한 12가지 AI 스킬** — AI 기반 보안 테스트, 코드 감사, 방어를 위한 구조화되고 실행 가능한 스킬 파일 모음.

</div>

---

## 🇬🇧 개요

**Awesome Security Skills**는 AI 어시스턴트를 유능한 사이버보안 실무자로 변환시켜주는 검증된 구조화된 스킬 파일을 제공합니다. 각 스킬은 사용 시점, 필수 도구, 단계별 절차, 템플릿, 함정, 법적 고려사항을 다루는 독립적인 플레이북입니다.

이 스킬들은 다음과 같은 사람들을 위해 설계되었습니다:
- **보안 전문가** — AI로 워크플로를 강화하려는
- **개발자** — 개발 생명주기에 보안을 내장하려는
- **팀** — 일관된 보안 테스트 관행을 수립하려는
- **AI 어시스턴트** — 인간의 지도 하에 보안 평가를 수행하는

> ⚠️ **법적 고지**: 이 스킬들은 **인가된 보안 테스트 및 교육 목적으로만** 제공됩니다. 소유하지 않은 시스템을 테스트하기 전에 항상 명시적인 서면 허가를 받으세요. 컴퓨터 시스템에 대한 무단 접근은 대부분의 관할권에서 불법입니다. 저자는 오용에 대한 책임을 지지 않습니다. 책임 있는 공개 가이드라인은 [SECURITY.md](SECURITY.md)를 참조하세요.

---

## 📋 스킬 개요

<table>
<thead>
<tr>
<th>카테고리</th>
<th>스킬</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="3"><strong>🌐 웹 보안</strong></td>
<td><a href="skills/Web安全/owasp-top10.md">OWASP Top 10</a></td>
<td>OWASP Top 10 취약점 체계적 평가</td>
</tr>
<tr>
<td><a href="skills/Web安全/api-security.md">API Security</a></td>
<td>REST, GraphQL, gRPC API 보안 검증 패턴</td>
</tr>
<tr>
<td><a href="skills/Web安全/authentication-security.md">Authentication Security</a></td>
<td>인증 및 권한 부여 메커니즘 평가</td>
</tr>
<tr>
<td rowspan="3"><strong>🔍 코드 감사</strong></td>
<td><a href="skills/代码审计/static-analysis.md">Static Analysis</a></td>
<td>자동 정적 코드 분석 도구 및 통합</td>
</tr>
<tr>
<td><a href="skills/代码审计/dependency-audit.md">Dependency Audit</a></td>
<td>서드파티 의존성 취약점 스캐닝</td>
</tr>
<tr>
<td><a href="skills/代码审计/secure-code-review.md">Secure Code Review</a></td>
<td>수동 안전 코드 리뷰 체크리스트</td>
</tr>
<tr>
<td rowspan="3"><strong>🎯 침투 테스트</strong></td>
<td><a href="skills/渗透测试/reconnaissance.md">Reconnaissance</a></td>
<td>OSINT 및 정보 수집 기법</td>
</tr>
<tr>
<td><a href="skills/渗透测试/web-app-testing.md">Web App Testing</a></td>
<td>웹 애플리케이션 침투 테스트 방법론</td>
</tr>
<tr>
<td><a href="skills/渗透测试/report-writing.md">Report Writing</a></td>
<td>전문적인 침투 테스트 보고서 작성</td>
</tr>
<tr>
<td rowspan="3"><strong>🔧 보안 도구</strong></td>
<td><a href="skills/安全工具/burp-suite.md">Burp Suite</a></td>
<td>웹 보안 테스트를 위한 Burp Suite 마스터</td>
</tr>
<tr>
<td><a href="skills/安全工具/nmap-scanning.md">Nmap Scanning</a></td>
<td>Nmap을 활용한 네트워크 탐색 및 포트 스캐닝</td>
</tr>
<tr>
<td><a href="skills/安全工具/security-automation.md">Security Automation</a></td>
<td>자동화된 보안 테스트 파이프라인 및 스크립트</td>
</tr>
</tbody>
</table>

---

## 🚀 빠른 시작

### AI 어시스턴트와 함께 사용하기

1. **저장소 클론**:
   ```bash
   git clone https://github.com/your-org/awesome-security-skills.git
   ```

2. **AI 어시스턴트에게 스킬 전달**:
   - 해당 스킬 파일 내용을 AI 대화에 복사
   - 또는 AI 도구에 스킬 파일 경로 지정
   - 예시: "`skills/Web安全/owasp-top10.md`를 읽고 그 절차에 따라 내 애플리케이션을 평가해 주세요"

3. **단계별 절차 따르기**:
   - 각 스킬은 완전한 워크플로를 포함
   - 일관된 결과를 위해 템플릿 활용
   - 시작 전 함정 섹션 검토

### AI 도구 통합

| AI 도구 | 통합 방법 |
|---------|-------------------|
| **Kimi Code** | 스킬 내용을 대화에 복사 |
| **Cursor** | `.cursorrules` 또는 프로젝트 컨텍스트에 스킬 파일 추가 |
| **Claude** | 시스템 프롬프트 또는 대화에 스킬 포함 |
| **ChatGPT** | 스킬 파일을 대화 컨텍스트로 붙여넣기 |
| **GitHub Copilot** | 코드 주석이나 작업 공간에서 스킬 참조 |

---

## 📁 프로젝트 구조

```
awesome-security-skills/
├── README.md                           # 이 파일
├── LICENSE                             # MIT 라이선스
├── CONTRIBUTING.md                     # 기여 가이드
├── SECURITY.md                         # 보안 정책
├── CODE_OF_CONDUCT.md                  # 행동 강령
├── CHANGELOG.md                        # 버전 이력
├── .gitignore                          # Git 무시 규칙
├── .github/
│   ├── workflows/
│   │   └── ci.yml                      # CI 파이프라인
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md              # 버그 리포트 템플릿
│   │   ├── feature_request.md         # 기능 요청 템플릿
│   │   └── new_skill.md               # 새 스킬 제안
│   └── pull_request_template.md        # PR 템플릿
└── skills/
    ├── Web安全/                         # 웹 보안
    │   ├── owasp-top10.md
    │   ├── api-security.md
    │   └── authentication-security.md
    ├── 代码审计/                         # 코드 감사
    │   ├── static-analysis.md
    │   ├── dependency-audit.md
    │   └── secure-code-review.md
    ├── 渗透测试/                         # 침투 테스트
    │   ├── reconnaissance.md
    │   ├── web-app-testing.md
    │   └── report-writing.md
    └── 安全工具/                         # 보안 도구
        ├── burp-suite.md
        ├── nmap-scanning.md
        └── security-automation.md
```

---

## 🎓 스킬 구조

각 스킬 파일은 사용성을 극대화하기 위해 일관된 구조를 따릅니다:

| 섹션 | 목적 |
|---------|---------|
| **사용 시점** | 스킬 적용을 위한 시나리오 및 트리거 |
| **사전 요구사항** | 필요한 지식 및 접근 권한 |
| **도구** | 라이선스 정보가 포함된 추천 도구 |
| **단계별 절차** | 상세한 단계별 워크플로 |
| **템플릿** | 바로 사용 가능한 보고서 및 체크리스트 템플릿 |
| **흔한 함정** | 피해야 할 실수 |
| **법적 고려사항** | 인가, 공개, 규정 준수 |
| **추가 읽기** | 공식 참조 링크 |

---

## 🤝 기여

기여를 환영합니다! 가이드라인은 [CONTRIBUTING.md](CONTRIBUTING.md)를 참조하세요.

**기여 방법**:
- 🐛 오래된 정보나 오류 신고
- ✨ 새 스킬 제안
- 📝 기존 스킬 개선
- 🌍 다른 언어로 스킬 번역
- 🧪 테스트 케이스 및 예제 추가

---

## 🔗 함께 보기

- **[awesome-security](https://github.com/sbilly/awesome-security)** — 보안 관련 소프트웨어, 라이브러리, 문서, 도서 모음
- **[awesome-web-security](https://github.com/qazbnm456/awesome-web-security)** — 웹 보안 자료 및 리소스 목록
- **[awesome-pentest](https://github.com/enaqx/awesome-pentest)** — 침투 테스트 리소스 및 도구 모음
- **[awesome-hacking](https://github.com/carpedm20/awesome-hacking)** — 해킹 리소스 큐레이션
- **[awesome-malware-analysis](https://rshipp/awesome-malware-analysis)** — 악성코드 분석 도구 및 리소스
- **[awesome-threat-intelligence](https://github.com/hslatman/awesome-threat-intelligence)** — 위협 인텔리전스 리소스
- **[awesome-incident-response](https://github.com/meirwah/awesome-incident-response)** — 사고 대응 도구
- **[awesome-reversing](https://github.com/wtsxDev/reversing)** — 리버싱 리소스
- **[awesome-static-analysis](https://github.com/mre/awesome-static-analysis)** — 정적 분석 도구, 린터, 코드 품질 검사기
- **[awesome-cyber-skills](https://github.com/Dev115/awesome-cyber-skills)** — 사이버 스킬 훈련 환경
- **[awesome-ctf](https://github.com/apsdehal/awesome-ctf)** — CTF 프레임워크 및 리소스
- **[awesome-bugbounty](https://github.com/djadmin/awesome-bugbounty)** — 버그 바운티 프로그램 및 리포트
- **[awesome-osint](https://github.com/jivoi/awesome-osint)** — OSINT 도구 모음
- **[awesome-devsecops](https://github.com/TaptuIT/awesome-devsecops)** — DevSecOps 도구 및 리소스

---

## 📜 라이선스

이 프로젝트는 [MIT License](LICENSE)에 따라 라이선스가 부여됩니다.

---

## ⚖️ 법적 고지

**이 저장소에 제공되는 도구, 기술, 스킬은 인가된 보안 테스트 및 교육 목적으로만 사용됩니다.** 보안 평가를 수행하기 전에 항상 시스템 소유자의 명시적인 서면 허가를 받으세요. 컴퓨터 시스템에 대한 무단 접근은 대부분의 관할권에서 형사 범죄입니다.

이 프로젝트의 관리자와 기여자는 여기에 포함된 정보 사용으로 인한 오용이나 피해에 대해 **일체의 책임을 지지 않습니다**. 사용자는 관련 법률 및 규정을 준수할 전적인 책임이 있습니다.

---

<div align="center">

**보안 커뮤니티가 ❤️를 담아 제작**

[⬆ 맨 위로 돌아가기](#-awesome-security-skills)

</div>
