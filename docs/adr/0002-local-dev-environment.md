# 0002: ローカル開発環境に Sail（MariaDB・Mailpit）を使う

- 日付：2026-10-04
- 状態：決定

## 背景

WSL2（Ubuntu 24.04）上で開発する。同じ PC に、別バージョンの Laravel を使う Sail プロジェクトが他にもある。

## 決定

- Laravel Sail（Docker）で開発環境を構築する
- DB は MariaDB、開発用メール確認は Mailpit を使う
- 他の Sail プロジェクトとは同時起動せず、片方ずつ起動する

## 理由

- 将来 VPS や AWS（コンテナ）に載せる際、Docker 構成のまま移行しやすい
- MariaDB をホストに直接インストールせずに済む
- Email verification を有効にしているため、確認メールを受け取れる Mailpit が必要
- Laravel・PHP のバージョンはプロジェクトごとにコンテナ内で独立するため、他プロジェクトに影響しない
- 同時起動はポート変更と Cookie の衝突対策（ホスト名の分離）が必要になり、注意点が増える

## 影響

- 作業するプロジェクトを切り替える際は、`sail stop` してから `sail up -d` する
- 同時起動が必要になった場合は、`APP_PORT` / `FORWARD_DB_PORT` / `VITE_PORT` の変更と、
  `○○.localhost` によるホスト名の分離で対応する
