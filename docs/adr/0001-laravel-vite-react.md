# 0001: Laravel + Vite + Inertia + React を採用する

- 日付：2026-10-04
- 状態：決定

## 背景

開花通知などの定期処理、キュー、共有花壇の反映（WebSocket）、AI API の呼び出しと回数制限など、
サーバー側の処理が多いアプリである。

## 検討した選択肢

1. Next.js ＋ Laravel（フロントと API を分離）
2. Next.js 単体
3. Laravel ＋ Vite ＋ Inertia ＋ React（公式スターターキット）

## 決定

3 を採用する。画面は React（Inertia 経由）、それ以外は Laravel で実装する。

## 理由

- スケジューラ・キュー・Reverb（WebSocket）・認証・レート制限など、必要な機能が Laravel 標準で揃う
- フロントと API を分けないため、API 設計・CORS・トークン管理・2系統のデプロイが不要になる
- ログイン後に使うアプリのため、SEO 目的の SSR の必要性が低い（Next.js の強みが活きにくい）
- 2 は可能だが、キュー・定期処理・WebSocket を外部サービスやライブラリで組み合わせる必要がある
- React は Next.js の経験を活かせる

## 影響

- WebSocket やキューワーカーは常駐プロセスが必要なため、共用レンタルサーバーではなく VPS 以上で運用する
  - 共用サーバーで試す場合は、ポーリングと cron によるキュー処理で代用する
- PWA 化は vite-plugin-pwa などで個別に対応する
- 将来のネイティブアプリ化は Capacitor でラップする想定
- 本番インフラは、試作は Xserver VPS または AWS Lightsail、本格運用は AWS（ECS / RDS for MariaDB）を想定
