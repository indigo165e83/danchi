# 設計

要件（[requirements/](../requirements/)）を「どう実現するか」に具体化する。図は Mermaid で書く。

## 構成

- 全体に関わる設計は直下に置く（`architecture.md`、`database.md`、`screens.md`）
- 領域ごとの設計は、requirements と同じ領域名のフォルダに置く（`room/`、`plants/`、`ai-residents/`、`items/`）
- `database.md` はテーブルが領域をまたぐため、全体のER図として1か所にまとめる
- 領域のフォルダは、その設計を書くときに作る（空のフォルダは作らない）

## 一覧

| ドキュメント | 内容 | 状態 |
|---|---|---|
| database.md | テーブル設計・ER図（全体） | 未作成 |
| screens.md | 画面一覧・画面遷移 | 未作成 |
| plants/growth-logic.md | 植物の成長ロジック（段階1） | 未作成 |
| room/room.md | 部屋の設計（段階1） | 未作成 |

これらの設計書は、テストのテストベースとしても使う（[test/](../test/) を参照）。
