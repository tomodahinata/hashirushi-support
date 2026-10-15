# はしるし サポートサイト

iPhoneアプリ「はしるし」の公開ページ（静的な HTML）。App Store Connect のサポート URL とプライバシーポリシー URL に入れる（`docs/release/release-checklist.md` §9）。アプリは `AppConfig.legalBaseUrl` の下の `privacy.html`・`support.html` を開く（`src/services/linkService.ts`）ので、公開する場所の直下にこの 2 つの名前で置く。

| file | 中身 |
|---|---|
| `index.html` | アプリの短い紹介とリンク |
| `support.html` | 問い合わせ先とよくある質問（バックアップと戻す・位置・データの基準日・誤りの知らせ方・免責） |
| `privacy.html` | プライバシーポリシー（外部送信の公表文を含む） |
| `style.css` | 共通の見た目（色はアプリの `src/ui/tokens.ts` から） |

## 決まり

- 外部のフォント・解析・script は読み込まない（訪問者の情報を第三者に送らないため。data-inventory §8）。
- 本文の正本は `docs/privacy/data-inventory.md`（§7 の公表文、§8 の骨子、§9 の保存期間、§10 の未決）と `docs/analytics/events.md`。送る event や封筒を変えたら、`privacy.html` の §5 を同じ commit で直し、最終改定日を更新する（events.md §9）。
- 免責文「非公式アプリです。国土交通省・全国「道の駅」連絡会とは関係ありません」は一字一句そのまま（`src/ui/i18n/ja/about.ts` の `DISCLAIMER`）。各頁の footer に置く。
- footer の出典の文は `src/data/generated/credits.ts` の `text` をそのまま写している。駅データを作り直して出典が変わったら、3 つの頁の footer を同じに直す（頁は include を持たないので、3 か所とも同じ文にする）。
- 文言は ux.md の語彙に従う（「無料」「登録」（動詞）「チェックイン」、自分についての「公式」を使わない）。
- 確かめ方: `npx --yes html-validate site/*.html`。
