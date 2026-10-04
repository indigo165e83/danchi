# danchi ドキュメント

「バーチャル団地くらし」の設計・技術選定・テスト・開発メモをまとめたドキュメントです。

| ドキュメント | 内容 |
|---|---|
| [requirements/](requirements/) | コンセプト・要件（要件ID付き、領域ごと） |
| [design/](design/) | 全体の設計（テーブル・画面）と領域ごとの設計 |
| [adr/](adr/) | 技術選定の記録（何を、なぜ選んだか） |
| [test/](test/) | テストドキュメント（JSTQB/ISTQB のテストプロセスに準拠） |
| [dev-notes/](dev-notes/) | 開発時の気づき・注意点（日付ごと） |

## 運用ルール

- ドキュメントはコードと同じリポジトリで管理し、関連するコード変更と同じコミットで更新する
- このリポジトリは Public。公開しない内容はリポジトリ直下の `docs-private/`（`.gitignore` で除外、Git 管理外）に書く
- 公開か非公開か迷ったら、まず `docs-private/` に書く。公開してよいと判断したものから `docs/` に移す
- 要件・設計・テスト条件は同じ領域名（room / plants / items / ai-residents など）でそろえる
- 図は Mermaid で書く（GitHub 上でそのまま表示される）
- コミットメッセージは「種類: 日本語の説明」の形式で書く（種類は feat / fix / docs / test / refactor / chore）

## 役割分担

| 置き場所 | 役割 |
|---|---|
| docs | 決まったことを残す |
| Issues | やることを1件ずつ管理する。対応する要件IDを書く |
| Projects ボード | Issues の状態を眺めるだけ。内容は書かない |
| マイルストーン | Issues を開発の段階ごとにまとめる |

詳しい経緯は [ADR-0003](adr/0003-documentation-management.md) を参照。
