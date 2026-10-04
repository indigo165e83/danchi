# テスト

JSTQB/ISTQB のテストプロセス（計画・分析・設計・実装・実行・完了）に沿ってテストドキュメントを置く。

## テストベース

- [requirements/](../requirements/)：要件（REQ-領域-番号）
- [design/](../design/)：設計

## テスト分析

テストベースからテスト条件を洗い出し、領域ごとのファイルにまとめる（例：`analysis/plants.md`）。

## 方針

- テスト条件には対応する要件IDを書き、Pest のテスト名からも要件IDを参照する
- テスト条件のファイル名は requirements・design と同じ領域名にする
