[English](README.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [Français](README.fr.md) | [Español](README.es.md) | [العربية](README.ar.md) | [한국어](README.ko.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [Deutsch](README.de.md)

<div align="center">

# 🛡️ Awesome Security Skills

**ハッカーのように考え、プロのように防御する。**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Security Skills](https://img.shields.io/badge/Security%20Skills-12-blue.svg)](#-スキル概要)
[![Maintained](https://img.shields.io/badge/Maintained-Yes-brightgreen.svg)](CHANGELOG.md)

**サイバーセキュリティ向け AI スキル 12 個** — AI を活用したセキュリティテスト、コード監査、防御のための構造化された実践スキルファイル集。

</div>

---

## 📋 スキル概要

<table>
<thead>
<tr>
<th>カテゴリ</th>
<th>スキル</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="3"><strong>🌐 Web セキュリティ</strong></td>
<td><a href="skills/Web安全/owasp-top10.md">OWASP Top 10</a></td>
<td>OWASP Top 10 の脆弱性を体系的に評価</td>
</tr>
<tr>
<td><a href="skills/Web安全/api-security.md">API セキュリティ</a></td>
<td>REST、GraphQL、gRPC API のセキュリティベストプラクティス</td>
</tr>
<tr>
<td><a href="skills/Web安全/authentication-security.md">認証セキュリティ</a></td>
<td>認証・認可メカニズムの評価</td>
</tr>
<tr>
<td rowspan="3"><strong>🔍 コード監査</strong></td>
<td><a href="skills/代码审计/static-analysis.md">静的解析</a></td>
<td>自動静的コード解析ツールと連携</td>
</tr>
<tr>
<td><a href="skills/代码审计/dependency-audit.md">依存関係監査</a></td>
<td>サードパーティ依存関係の脆弱性スキャン</td>
</tr>
<tr>
<td><a href="skills/代码审计/secure-code-review.md">セキュアコードレビュー</a></td>
<td>手動セキュアコードレビューチェックリスト</td>
</tr>
<tr>
<td rowspan="3"><strong>🎯 ペネトレーションテスト</strong></td>
<td><a href="skills/渗透测试/reconnaissance.md">リコンナンサンス</a></td>
<td>OSINT と情報収集技術</td>
</tr>
<tr>
<td><a href="skills/渗透测试/web-app-testing.md">Web アプリテスト</a></td>
<td>Web アプリケーションのペネトレーションテスト手法</td>
</tr>
<tr>
<td><a href="skills/渗透测试/report-writing.md">レポート作成</a></td>
<td>プロフェッショナルなペネトレーションテストレポートの作成</td>
</tr>
<tr>
<td rowspan="3"><strong>🔧 セキュリティツール</strong></td>
<td><a href="skills/安全工具/burp-suite.md">Burp Suite</a></td>
<td>Web セキュリティテストのための Burp Suite マスター</td>
</tr>
<tr>
<td><a href="skills/安全工具/nmap-scanning.md">Nmap スキャン</a></td>
<td>Nmap によるネットワーク検出とポートスキャン</td>
</tr>
<tr>
<td><a href="skills/安全工具/security-automation.md">セキュリティ自動化</a></td>
<td>自動化セキュリティテストパイプラインとスクリプト</td>
</tr>
</tbody>
</table>

---

## 🚀 クイックスタート

### AI アシスタントとの連携

1. **リポジトリをクローン**:
   ```bash
   git clone https://github.com/your-org/awesome-security-skills.git
   ```

2. **スキルファイルを AI アシスタントに提供**:
   - 関連するスキルファイルの内容を AI 会話にコピー
   - または AI ツールにスキルファイルのパスを指定
   - 例："`skills/Web安全/owasp-top10.md` を読み込んで、その手順に従ってアプリケーションを評価して"

3. **ステップバイステップの手順に従う**:
   - 各スキルには完全なワークフローが含まれています
   - テンプレートを使用して一貫した出力を得ましょう
   - 開始前に落とし穴セクションを確認してください

### AI ツールとの連携

| AI ツール | 連携方法 |
|-----------|---------|
| **Kimi Code** | スキルの内容を会話にコピー |
| **Cursor** | スキルファイルを `.cursorrules` またはプロジェクトコンテキストに追加 |
| **Claude** | システムプロンプトまたは会話にスキルを含める |
| **ChatGPT** | スキルファイルを会話コンテキストとして貼り付け |
| **GitHub Copilot** | コードコメントまたはワークスペースでスキルを参照 |

---

## 📁 プロジェクト構成

```
awesome-security-skills/
├── README.md                           # 本ファイル
├── LICENSE                             # MIT ライセンス
├── CONTRIBUTING.md                     # コントリビュートガイド
├── SECURITY.md                         # セキュリティポリシー
├── CODE_OF_CONDUCT.md                  # 行動規範
├── CHANGELOG.md                        # バージョン履歴
├── .gitignore                          # Git 無視ルール
├── .github/
│   ├── workflows/
│   │   └── ci.yml                      # CI パイプライン
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md              # バグ報告テンプレート
│   │   ├── feature_request.md         # 機能リクエストテンプレート
│   │   └── new_skill.md               # 新スキル提案
│   └── pull_request_template.md        # PR テンプレート
└── skills/
    ├── Web安全/                         # Web セキュリティ
    ├── 代码审计/                         # コード監査
    ├── 渗透测试/                         # ペネトレーションテスト
    └── 安全工具/                         # セキュリティツール
```

---

## 🎓 スキルの構成

各スキルファイルは使いやすさを最大化するための一貫した構成に従っています：

| セクション | 目的 |
|-----------|------|
| **使用タイミング** | スキルを適用するシナリオとトリガー |
| **前提条件** | 必要な知識とアクセス権 |
| **ツール** | ライセンス情報付きの推奨ツール |
| **ステップバイステップ手順** | 詳細な段階別ワークフロー |
| **テンプレート** | すぐに使えるレポートとチェックリストテンプレート |
| **よくある落とし穴** | 避けるべきミス |
| **法的考慮事項** | 認可、開示、コンプライアンス |
| **参考文献** | 権威ある参考リンク |

---

## 🤝 コントリビュート

コントリビューションを歓迎します！ガイドラインは [CONTRIBUTING.md](CONTRIBUTING.md) をご覧ください。

**コントリビュートの方法**:
- 🐛 エラーや古い情報を報告
- ✨ 新スキルを提案
- 📝 既存スキルを改善
- 🌍 他の言語に翻訳
- 🧪 テストケースとサンプルを追加

---

## 🔗 関連プロジェクト

エコシステムの他の優れたプロジェクト：

- **[awesome-security](https://github.com/sbilly/awesome-security)** — セキュリティ関連の優れたソフトウェア、ライブラリ、ドキュメント、書籍、リソースのコレクション。
- **[awesome-web-security](https://github.com/qazbnm456/awesome-web-security)** — Web セキュリティの教材とリソースのリスト。
- **[awesome-pentest](https://github.com/enaqx/awesome-pentest)** — ペネトレーションテストのリソース、ツール、その他の有用なリソースのコレクション。
- **[awesome-hacking](https://github.com/carpedm20/awesome-hacking)** — ハッキングリソースのキュレーションリスト。
- **[awesome-malware-analysis](https://rshipp/awesome-malware-analysis)** — マルウェア分析ツールとリソースのキュレーションリスト。
- **[awesome-threat-intelligence](https://github.com/hslatman/awesome-threat-intelligence)** — 脅威インテリジェンスリソースのキュレーションリスト。
- **[awesome-incident-response](https://github.com/meirwah/awesome-incident-response)** — インシ対応ツールのキュレーションリスト。
- **[awesome-reversing](https://github.com/wtsxDev/reversing)** — リバースエンジニアリングリソースのキュレーションリスト。
- **[awesome-static-analysis](https://github.com/mre/awesome-static-analysis)** — 静的解析ツール、リンター、コード品質チェッカーのキュレーションリスト。
- **[awesome-cyber-skills](https://github.com/Dev115/awesome-cyber-skills)** — サイバーセキュリティスキルを訓練できるハッキング環境のキュレーションリスト。
- **[awesome-ctf](https://github.com/apsdehal/awesome-ctf)** — CTF フレームワーク、ライブラリ、リソース、ソフトウェアのキュレーションリスト。
- **[awesome-bugbounty](https://github.com/djadmin/awesome-bugbounty)** — バグバウンティプログラムとその詳細の完全リスト。
- **[awesome-osint](https://github.com/jivoi/awesome-osint)** — 優れた OSINT ツールのキュレーションリスト。
- **[awesome-devsecops](https://github.com/TaptuIT/awesome-devsecops)** — DevSecOps ツール、リソース、参考資料のキュレーションリスト。

---

## 📜 ライセンス

本プロジェクトは [MIT ライセンス](LICENSE) の下で提供されています。

---

## ⚖️ 法的免責事項

**本リポジトリで提供されるツール、技術、スキルは、認可されたセキュリティテストと教育目的のみを目的としています。** いずれかのセキュリティ評価を実施する前に、システム所有者から明示的な書面による許可を得てください。コンピュータシステムへの不正アクセスは、米国のコンピュータ詐欺・乱用法（CFAA）、英国のコンピュータ乱用法、および世界中の同様の法律を含む、ほとんどの法域で刑事犯罪です。

本プロジェクトのメンテナーとコントリビューターは、本書に含まれる情報の使用による誤用または損害について**一切の責任を負いません**。ユーザーは、すべての適用法令を遵守する全責任を負います。

---

<div align="center">

**セキュリティコミュニティが ❤️ を込めて制作**

[⬆ トップに戻る](#-awesome-security-skills)

</div>
