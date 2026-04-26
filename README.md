# 同人売上管理ラボ (Doujin Sales Lab)

**TASK_ID**: T1SITE1
**公開日**: 2026-04-26
**サイト目的**: 同人作家向けに、DLsite / FANZA / BOOTH の手取り比較シミュレータと、売上管理 Excel テンプレを無料配布する検証サイト。

---

## 構成

```
doujin-sales-lab/
├── index.html              # メインページ(全セクション統合)
├── 404.html                # 404ページ
├── _redirects              # Cloudflare Pages リダイレクト
├── _headers                # Cloudflare Pages ヘッダー
├── robots.txt
├── sitemap.xml
├── .gitignore
├── README.md
├── assets/
│   └── favicon.svg
├── downloads/
│   └── doujin_uriage_kanri_v1_1.xlsx   # 配布Excel(v1.1)
└── docs/
    ├── PUBLISH_GUIDE.md            # GitHub + Cloudflare Pages 公開手順
    ├── POSTLAUNCH_CHECKLIST.md     # 公開後チェックリスト
    └── CTA_LINK_CONFIG.md          # CTAリンク差し替えガイド
```

---

## 技術構成

- **静的HTML(単一 `index.html`)** — Astro等のビルド不要
- **TailwindCSS CDN** — ビルド不要、即適用
- **JSシミュレータ** — 既存 `prototype/index.html` のロジックを継承
- **Excel配布** — 直リンク(メール登録不要)
- **Cloudflare Pages 想定** — Build command 空、Output directory ルート(`/`)

---

## ローカル動作確認

```bash
cd C:\Users\81808\Desktop\New\doujin-sales-lab
python -m http.server 8000
# → http://localhost:8000 で表示
```

ファイル直開きでも動作するが、`/downloads/` のリンク確認のため http サーバ経由を推奨。

---

## 主要セクション

1. ファーストビュー(タイトル + CTA 2つ)
2. このサイトでできること(3カード)
3. 同人売上管理で詰まりやすいポイント(6項目)
4. BOOTH / DLsite / FANZA の手数料注意(3カード)
5. 手取りシミュレータ(prototype 継承)
6. Excel配布CTA(直リンク `/downloads/doujin_uriage_kanri_v1_1.xlsx`)
7. FAQ(8問)
8. 注意事項・免責(6箇条)
9. 運営者・問い合わせ
10. フッター

---

## CTAリンクの状態

| ボタン | 現在のリンク | 差し替えタイミング |
|---|---|---|
| 📥 Excelダウンロード(主) | `/downloads/doujin_uriage_kanri_v1_1.xlsx` | 公開時から有効 |
| シミュレータを試す | `#simulator`(ページ内) | 公開時から有効 |
| (将来)note | 未設定 | note 記事公開時 |
| (将来)X | 未設定 | X 告知時 |

詳細: `docs/CTA_LINK_CONFIG.md`

---

## 重要な注意

- BOOTH手数料は公式値(5.6% + ¥45/件、2025/10/28改定後)
- DLsite / FANZA は **2026年4月時点の暫定値** を使用(各管理画面で実数置換推奨)
- 「絶対」「必ず」「儲かる」「税務代行」「JRA公認」等の断定・誇張表現は使用しない
- 確定申告・税務判断は税理士または税務署にご相談ください 旨を必ず表示

---

## 次のステップ

1. **GitHub 公開**: `docs/PUBLISH_GUIDE.md` 参照
2. **Cloudflare Pages 連携**: 同 `PUBLISH_GUIDE.md`
3. **公開後チェック**: `docs/POSTLAUNCH_CHECKLIST.md`
4. **note / X 告知**: チェックリスト全項目クリア後

---

© 2026 Doujin Sales Lab
