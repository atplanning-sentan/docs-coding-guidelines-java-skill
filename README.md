# ☕ ATP Java コーディング規約（エージェントスキル版）

[![ATP | Java コーディング規約](https://img.shields.io/badge/ATP-Java_コーディング規約-8e1b46?style=flat-square)](https://www.atp.co.jp/)
[![skill atp-java-coding](https://img.shields.io/badge/skill-atp--java--coding-8e1b46?style=flat-square)](.agents/skills/atp-java-coding/SKILL.md)
[![IBM Bob](https://img.shields.io/badge/IBM_Bob-対応-8e1b46?style=flat-square)](.bob/skills/atp-java-coding/)

**株式会社エーティ・プランニング**  
先端技術本部  
コンサルティング＆アーキテクトグループ（CAG）

本リポジトリは、先端技術本部が制定した Java コーディング規約を、エージェントスキル `atp-java-coding` として配付するものです。規約の参照、実装時の遵守、`src/main/java` のベースライン監査を、スキルの手順に従って行います。

文書版 [docs-coding-guidelines-java](https://github.com/atplanning-sentan/docs-coding-guidelines-java) の内容をスキル構成へ移したものであり、今後の正本はこのスキル版です。

> [!NOTE]
> **公開範囲**  
> 社内・社外を問わず、Java でソフトウェアを開発する者向けに公開しています。

> [!CAUTION]
> **免責**  
> 本リポジトリの内容は、先端技術本部が現時点の best effort で提供するものです。  
> 内容の完全性・正確性・最新性、および特定目的への適合性を保証するものではありません。
>
> 利用・参照は各自の責任で行い、プロジェクトの要件に応じて判断してください。

## 📦 含まれるもの

スキルの正本は [.agents/skills/atp-java-coding/](.agents/skills/atp-java-coding/) です。`.bob/skills/atp-java-coding` と `.claude/skills/atp-java-coding` は、このディレクトリへのシンボリックリンクです。Pull Request テンプレートが参照するのも正本です。

- 正本: [.agents/skills/atp-java-coding/](.agents/skills/atp-java-coding/)
- IBM Bob（正本へのリンク）: [.bob/skills/atp-java-coding/](.bob/skills/atp-java-coding/)
- Claude Code（正本へのリンク）: [.claude/skills/atp-java-coding/](.claude/skills/atp-java-coding/)

### 対応するエージェント

| エージェント | 読む場所 | このリポジトリ |
| --- | --- | --- |
| IBM Bob | `.bob/skills/` | 正本へのリンク |
| Cursor | `.agents/skills/`（互換で `.claude/skills/` も読む） | 正本をそのまま使う |
| Claude Code | `.claude/skills/` | 正本へのリンク |
| OpenAI Codex | `.agents/skills/` | 正本をそのまま使う |
| GitHub Copilot / VS Code | `.agents/skills/` | 正本をそのまま使う |

`.agents/skills/` を読む他のエージェントでも、正本をそのまま使えます。Cursor の読み込み場所は [Cursor の Skills ドキュメント](https://cursor.com/docs/context/skills)、共通の置き場所を読むクライアントの一覧は [Agent Skills support](https://www.skillsboard.sh/agent-skills-support) を参照してください。

以下の相対パスは、正本からの位置です。

### 規約・レビュー

- 手順（実装・修正 / ベースライン監査）: [SKILL.md](.agents/skills/atp-java-coding/SKILL.md)
- 規約（Markdown版）: [references/CODING_RULES.md](.agents/skills/atp-java-coding/references/CODING_RULES.md)
- レビュー判定: [references/REVIEW_CHECKLIST.md](.agents/skills/atp-java-coding/references/REVIEW_CHECKLIST.md)
- 利用ルール: [references/AI_RULES.md](.agents/skills/atp-java-coding/references/AI_RULES.md)

### ビルド連携

- 品質設定一式（Checkstyle / SpotBugs / markdownlint）: [assets/quality/](.agents/skills/atp-java-coding/assets/quality/)
- Maven 品質プラグイン設定: [assets/quality/maven/quality-plugins.xml](.agents/skills/atp-java-coding/assets/quality/maven/quality-plugins.xml)

### 原本

- 原本（Word）: [assets/original/Javaコーディング規約.docx](.agents/skills/atp-java-coding/assets/original/Javaコーディング規約.docx)
- 規約から参照する画像: [assets/images/](.agents/skills/atp-java-coding/assets/images/)

### GitHub 運用

- PRテンプレート: [.github/pull_request_template.md](.github/pull_request_template.md)
- 再利用可能な品質チェック CI: [.github/workflows/reusable-java-quality.yml](.github/workflows/reusable-java-quality.yml)

## 導入方法

### 1. このリポジトリを checkout する

```text
git clone https://github.com/atplanning-sentan/docs-coding-guidelines-java-skill.git
cd <clone 先>
```

チームで規約版を揃えるときは、tag または commit を checkout する。

### 2. 自プロジェクトへスキルを置く

正本 `.agents/skills/atp-java-coding` を、Java プロジェクトの同じパスへコピーする。

IBM Bob で使うときは、`.bob/skills/atp-java-coding` も一緒に置く。正本への相対リンクなので、この位置関係を保てばそのまま使える。

```text
your-app/
├── .agents/skills/atp-java-coding/    ← 正本
└── .bob/skills/atp-java-coding/       ← IBM Bob（正本への相対リンク）
```

Claude Code で使うときは、同様に `.claude/skills/atp-java-coding` を置く。

Cursor、OpenAI Codex、GitHub Copilot / VS Code は、正本だけで読める。

コピーしたスキルは、自プロジェクトのリポジトリに含める。規約を更新するときは、checkout し直した正本でこのディレクトリを置き換える。

### 3. （任意）CI・Maven

他リポジトリから [.github/workflows/reusable-java-quality.yml](.github/workflows/reusable-java-quality.yml) を `workflow_call` で呼び出す。`assets/quality/` をアプリリポジトリの `templates/quality/` にコピーし、[assets/quality/maven/quality-plugins.xml](.agents/skills/atp-java-coding/assets/quality/maven/quality-plugins.xml) を `pom.xml` に取り込む。配置と SpotBugs 除外の手順は [assets/quality/README.md](.agents/skills/atp-java-coding/assets/quality/README.md) を参照する。

## 📖 使い方

### 1. 規約を読む

[references/CODING_RULES.md](.agents/skills/atp-java-coding/references/CODING_RULES.md)

### 2. PRを出す

[.github/pull_request_template.md](.github/pull_request_template.md) に従い、[references/CODING_RULES.md](.agents/skills/atp-java-coding/references/CODING_RULES.md) と [references/REVIEW_CHECKLIST.md](.agents/skills/atp-java-coding/references/REVIEW_CHECKLIST.md) で確認する。

### 3. スキルで実装・監査する

手順の正本は [SKILL.md](.agents/skills/atp-java-coding/SKILL.md) です。

**対象**は本リポジトリではなく、エージェントが開いている **Java アプリケーション** です。ベースライン監査の対象は `src/main/java` で、PR 差分・git 履歴・`src/test` は、依頼で明示されるまで対象外です。

スキルは依頼の種類で手順を分けます。

- **実装・修正**: [AI_RULES.md](.agents/skills/atp-java-coding/references/AI_RULES.md) と [REVIEW_CHECKLIST.md](.agents/skills/atp-java-coding/references/REVIEW_CHECKLIST.md) を読み、変更箇所に関係する章だけ [CODING_RULES.md](.agents/skills/atp-java-coding/references/CODING_RULES.md) を読む。チェックリスト全項目の表は出さない。
- **レビュー・監査・一括確認**: 上記に加え規約本文を読み、`src/main/java` を監査する。出力は §1〜§5、および `REVIEW_CHECKLIST` 全項目の表。

対象の Java プロジェクトを開く。

実装・修正のときは、通常の修正依頼に規約名を添える。

```text
UserService に退会処理を追加してください。
atp-java-coding の規約に従って実装してください。
```

一括レビュー（監査）のときは、次を送る。

```text
atp-java-coding の手順に従い、本ワークスペースの src/main/java を一括レビューしてください。
PR・git 差分・src/test は対象外です。
```

## 📁 ディレクトリ構成

```text
.
├── .agents/skills/atp-java-coding/    # 正本
│   ├── SKILL.md                       # 実装・修正 / ベースライン監査の手順
│   ├── references/
│   │   ├── AI_RULES.md
│   │   ├── CODING_RULES.md
│   │   └── REVIEW_CHECKLIST.md
│   └── assets/
│       ├── original/                  # 原本（Javaコーディング規約.docx）
│       ├── images/                    # 規約から参照する図
│       └── quality/                   # Checkstyle / SpotBugs / markdownlint
├── .bob/skills/atp-java-coding/       # 正本へのシンボリックリンク（IBM Bob）
├── .claude/skills/atp-java-coding/    # 正本へのシンボリックリンク（Claude Code）
└── .github/
    ├── pull_request_template.md
    └── workflows/
        └── reusable-java-quality.yml
```

---

## 変更

規約の変更は Issue から Pull Request で行い、編集は正本 `.agents/skills/atp-java-coding/` だけに行います。`.bob` と `.claude` は正本へのリンクです。

章立ては原本 [Javaコーディング規約.docx](.agents/skills/atp-java-coding/assets/original/Javaコーディング規約.docx) に合わせます。`references/CODING_RULES.md` の説明文は 1文1行、段落の区切りは空行1行とします（表・コードブロック・リストは対象外）。

## 📜 改定履歴

| 日付 | 内容 |
| --- | --- |
| 2026-10-01 | スキル `atp-java-coding` として整備。正本は `.agents/skills/atp-java-coding/`。手順は `SKILL.md`、規約は `references/`、品質設定は `assets/quality/`、原本は `assets/original/`。`.bob` と `.claude` は正本へのシンボリックリンク |
