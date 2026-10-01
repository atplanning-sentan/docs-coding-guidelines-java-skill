---
name: atp-java-coding
description: >-
  ATP先端技術本部の Java コーディング規約に従い、Java の実装・修正と
  src/main/java のベースライン監査を行う。Java、コーディング規約、コードレビュー、
  ルールID（J-XXX）、Checkstyle、SpotBugs に触れたときに使う。
---

# ATP Java コーディング規約

規約本文の正本は、このスキルの `references/` である。規約本文をこのファイルに書き写さない。

Checkstyle / SpotBugs の設定は `assets/quality/`、原典の Word と図は `assets/original/` と `assets/images/` にある。監査や実装のたびにこれらを読まない。アプリへ導入するときは `assets/quality/` を、そのリポジトリの `templates/quality/` にコピーする。

## 手順の選び方

ユーザーがレビュー、監査、一括確認を求めたときだけ「ベースライン監査」に進む。それ以外の Java 実装・修正は「実装・修正」に進む。

## 実装・修正

1. [references/AI_RULES.md](references/AI_RULES.md) と [references/REVIEW_CHECKLIST.md](references/REVIEW_CHECKLIST.md) を読む。
2. 変更箇所に関係する章だけ [references/CODING_RULES.md](references/CODING_RULES.md) を読む。
3. 規約に反する実装はしない。違反を見つけたらルールID（無ければ見出し名）と最小差分の修正を示す。
4. チェックリスト全項目の表は出さない。

## ベースライン監査

1. 上記に加え [references/CODING_RULES.md](references/CODING_RULES.md) を読む。
2. 対象はワークスペースの `src/main/java` 配下の `.java`。別構成なら `pom.xml`、`build.gradle`、README から main ソースを特定する。
3. PR 差分、git 履歴、`src/test`、生成コード、ビルド成果物は、ユーザーが明示するまで対象外。
4. ビルドツール、Java バージョン、主要フレームワーク、Checkstyle / SpotBugs の有無、方式設計に書かれたスコープは、ワークスペースから読めた事実だけを冒頭に列挙する。読めない項目は「不明」とし、それに依存する判定も「不明」とする。
5. Checkstyle または SpotBugs がビルドに無いとき、それらを前提とする条文は「対象外（機械チェック未導入）」とし、チェックリストで評価する。
6. 推測で補完しない。意図が曖昧な箇所は「意図の確認が必要」とする。セキュリティ、性能、保守性を優先する。修正案は最小差分にする。
7. 違反には `REVIEW_CHECKLIST` のルールIDを付ける。ID が無い条文は `CODING_RULES.md` の見出し名を併記する。

### 出力（この順。指摘がゼロでも §3 は省略しない）

## 1. 確認できたプロジェクト前提（箇条書き・事実のみ）
## 2. サマリ（3行以内）
## 3. REVIEW_CHECKLIST 適用結果（表・全項目）

| ルールID | 項目 | 判定 | 根拠（ファイル:行 または 該当なし / 対象外の理由） |

判定は 準拠 / 不適合 / 不明 / 対象外 のいずれか。

## 4. 指摘一覧

### 重大（修正必須）
### 重要（修正推奨）
### 軽微（任意）

各項目は 問題点 / 根拠（ルールID・該当箇所）/ 修正案（最小差分）。

## 5. ルール文書側の所見（短く）

プロジェクト前提で対象外にした規約と、判定に必要だったが文書に無い前提を列挙する。
