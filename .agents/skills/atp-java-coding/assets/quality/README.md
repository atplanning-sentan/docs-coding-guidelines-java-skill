# 社内 Java / ドキュメント品質設定（assets/quality）

Checkstyle・SpotBugs・markdownlint の **共通設定** です。正本はスキル `atp-java-coding` のこのディレクトリです。

**アプリ向けの Maven スニペット**は [maven/quality-plugins.xml](maven/quality-plugins.xml) を参照してください。

## 方針

- **静的解析**: Checkstyle / SpotBugs の **最小ルール**（`mvn verify` で実行）
- **それ以外**: [CODING_RULES.md](../../references/CODING_RULES.md) と [REVIEW_CHECKLIST.md](../../references/REVIEW_CHECKLIST.md) に基づく **レビュー**（人レビュー含む。生成 AI は任意）

## ディレクトリ構成

| パス | 用途 |
| --- | --- |
| `checkstyle/` | Checkstyle 本体・抑制（プロジェクト非依存） |
| `spotbugs/exclude-filter-spring-template.xml` | SpotBugs 除外テンプレ（パッケージ要置換） |
| `.markdownlint.json` | Markdown lint（設計書向けに緩め） |
| `maven/quality-plugins.xml` | Maven プラグイン設定の参照用スニペット |

## 新規 Java プロジェクトへの導入

### 1. ファイル配置

このディレクトリをアプリリポジトリの `templates/quality/` へコピーする。

```text
your-app/
├── templates/quality/       ← 本ディレクトリをコピー
├── config/spotbugs/
│   └── exclude.xml          ← テンプレから生成（下記）
├── .vscode/settings.json    ← 任意
└── pom.xml
```

### 2. SpotBugs 除外

1. `spotbugs/exclude-filter-spring-template.xml` を `config/spotbugs/exclude.xml` にコピー
2. **`PACKAGE_ROOT_REGEX`** をルートパッケージの正規表現に置換（例: `jp\.co\.example\.app`）
3. プロジェクト固有の `<Match>` を末尾に追加（理由をコメントで記載）

### 3. Maven（`pom.xml`）

[maven/quality-plugins.xml](maven/quality-plugins.xml) を取り込み、パス例:

```xml
<configLocation>templates/quality/checkstyle/checkstyle.xml</configLocation>
<suppressionsLocation>templates/quality/checkstyle/suppressions.xml</suppressionsLocation>
<excludeFilterFile>${project.basedir}/config/spotbugs/exclude.xml</excludeFilterFile>
```

### 4. markdownlint（任意）

```json
"markdownlint.configFile": "templates/quality/.markdownlint.json"
```

### 5. 確認

```powershell
.\mvnw.cmd verify
```

## バージョン（参照）

| ツール | バージョン |
| --- | --- |
| Checkstyle | 10.18.2 |
| maven-checkstyle-plugin | 3.5.0 |
| SpotBugs | 4.8.6 |
| spotbugs-maven-plugin | 4.8.6.0 |

## 改訂履歴

| 日付 | 内容 |
| --- | --- |
| 2026-05-18 | 初版（internal-test-quality-analyzer から templates/quality として登録） |
| 2026-10-01 | 正本をスキル `atp-java-coding` の `assets/quality/` に移した |
