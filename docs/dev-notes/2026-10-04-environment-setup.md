# 2026-10-04 開発環境の構築

## 構成

- Laravel 13 ＋ React スターターキット（Inertia、TypeScript、Tailwind、shadcn/ui）
- 認証機能：Email verification / Registration / Two-factor authentication / Passkeys / Password confirmation（すべて有効）
- teams support：使わない（団地・部屋・住人の関係は独自に設計する）
- Sail（コンテナ内 PHP 8.5）、MariaDB、Mailpit
- テスト：Pest
- その他：Wayfinder（ルートを TypeScript から型付きで呼べる）、Laravel Boost（AI コーディング支援）

## 構築手順

```bash
laravel new danchi                        # スターターキット：React
cd danchi
php artisan sail:install --with=mariadb
sail up -d
sail artisan migrate
sail artisan sail:add mailpit
sail up -d
sail npm run dev
```

`.env` の変更点：

```
APP_URL=http://localhost
MAIL_MAILER=smtp
MAIL_HOST=mailpit
MAIL_PORT=1025
```

## 気づき・注意点

- `laravel new` でDBを聞かれない場合、SQLite が既定になりマイグレーションも SQLite に実行される。
  `php artisan sail:install --with=mariadb` で `.env` が MariaDB 用に書き換わる
- `composer run dev` はホストの PHP で動かす場合のコマンド。Sail では `sail up -d` と `sail npm run dev` を使う
- `APP_URL` の初期値は `http://localhost:8000`。Sail では `http://localhost` に直す（確認メールのリンクに使われる）
- Mailpit 追加前に送られたメールは届かない。追加後に確認画面の「Resend verification email」で再送する
- Mailpit の受信箱：http://localhost:8025
- `laravel new` 実行時はホストの PHP（8.4）、アプリの実行はコンテナ内の PHP（8.5）が使われる
- 他の Sail プロジェクトとはポートが衝突するため、片方ずつ起動する（[ADR-0002](../adr/0002-local-dev-environment.md)）
- `sail down -v` は DB のデータまで消える。普段は `sail stop` を使う
- Laravel Boost の AI 用ファイル（`CLAUDE.md`、`AGENTS.md`、`.mcp.json`、`boost.json` など）は `.gitignore` 済み。
  別環境では `sail artisan boost:install` で再生成する
- フォントの警告（`fontaine` package）は任意の最適化機能の案内で、動作には影響しない
- Git の初回コミット前に `.gitignore` へ `/docs-private/` を追加した（後から追加しても追跡済みファイルには効かないため）
