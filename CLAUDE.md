# Corporate Research Agent（企業研究エージェント）

就活の企業研究を自動化するプロジェクト。`/research 企業名` と入力すると、4体の調査エージェントが並列でWeb調査を行い、結果を統合 → 独立した検証エージェント（fact-checker）が出典に当たって裏取り → Notionのデータベースにデザインされたページとして出力する。

## 使い方

```
/research トヨタ自動車
```

## 出力先 Notion

- データベース「企業研究エージェント結果」（就活 > 企業研究エージェント 配下）
  - database_id: `37cedb10-c049-806c-aeee-f05a710b773c`
  - data_source_id: `37cedb10-c049-8056-ac85-000bc042bc44`
- ページ作成は Notion MCP の create-pages を `data_source_id` 親で使う

## 構成

- `.claude/skills/research/SKILL.md` — `/research` コマンド本体（オーケストレーション手順）
- `.claude/skills/research/notion-template.md` — Notionページのデザインテンプレート
- `.claude/agents/` — サブエージェント定義（事業 / 財務 / 採用・社風 / ニュース・競合の調査4体 + 検証1体）
- `output/` — Notionと同内容のMarkdownのローカル保存先（バックアップ兼履歴）

## プロジェクト全体のルール

- 出力はすべて日本語
- すべての事実に出典URLを付ける（面接で使う数字を後から一次情報で確認できるように）
- 財務数値はIR・有価証券報告書などの一次情報を最優先
- 企業理念・Purpose・求める人材像は要約せず**原文を引用**する
- 口コミサイト由来の情報は「傾向」として扱い、断定しない
