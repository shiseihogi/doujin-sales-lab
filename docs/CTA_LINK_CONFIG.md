# CTA リンク差し替えガイド

**TASK_ID**: T1SITE1
**目的**: 公開後にX/note/Brevoフォーム等のリンクを追加・差し替えする手順を一箇所にまとめる。

---

## 1. 現在の CTA リンク

| 場所 | リンク先 | 状態 |
|---|---|---|
| ヒーローボタン①「シミュレータを試す」 | `#simulator`(ページ内アンカー) | ✓ 動作中 |
| ヒーローボタン②「Excelテンプレを無料DL」 | `#download`(ページ内アンカー) | ✓ 動作中 |
| Excel配布カードボタン | `/downloads/doujin_uriage_kanri_v1_1.xlsx` | ✓ 動作中(直DL) |
| ナビ「📥 Excel配布」 | `#download` | ✓ 動作中 |
| 短縮URL `/excel` | `/downloads/doujin_uriage_kanri_v1_1.xlsx` | ✓ `_redirects` 経由 |
| 短縮URL `/dl` | `/downloads/doujin_uriage_kanri_v1_1.xlsx` | ✓ `_redirects` 経由 |
| 運営者・問い合わせ | テキストのみ(X / note リンク未設定) | △ 後日追加 |

---

## 2. X 告知リンクを追加する手順

公開後、X アカウントが固まったら:

### 2.1 ヒーロー上部 / 運営者セクションに追加

`index.html` の運営者セクション(`<section id="contact">`)内、`<dt>問い合わせ</dt>` のブロックを以下に置換:

```html
<dt class="font-bold text-slate-700">問い合わせ・最新情報</dt>
<dd class="md:col-span-2 text-slate-700">
  <a href="https://x.com/<YOUR_HANDLE>" target="_blank" class="underline text-indigo-600">𝕏 <span class="font-mono">@<YOUR_HANDLE></span></a>
  / <a href="https://note.com/<YOUR_NOTE>" target="_blank" class="underline text-indigo-600">note</a>
</dd>
```

`<YOUR_HANDLE>` `<YOUR_NOTE>` を実値に置換 → push → Cloudflare Pages 自動再デプロイ。

---

## 3. Brevo / メールフォームを後日追加する手順

現状は **Excelの直DL**(メール登録不要)。Brevo フォーム導入時:

### 3.1 ボタンを並列で追加する案

`<section id="download">` 内、現在の Excel ダウンロードボタンを保持しつつ、その下に「メルマガ登録(任意)」を追加:

```html
<a href="<BREVO_FORM_URL>" target="_blank"
   class="block mt-3 text-center text-xs underline text-white/80 hover:text-white">
  + メルマガに登録して更新通知を受け取る(任意)
</a>
```

### 3.2 ボタンをフォームに置換する案(将来)

Brevo フォームを iframe または HTML埋め込みで設置可能。`<section id="download">` を改修。

---

## 4. note 記事を追加する手順

### 4.1 ヒーロー下に「note で詳しく読む」を追加

ヒーロー下の `<div class="mt-8 flex flex-wrap gap-3">` に追記:

```html
<a href="https://note.com/<YOUR_NOTE>/n/<NOTE_SLUG>" target="_blank"
   class="px-6 py-3 bg-white/20 text-white border border-white/30 font-bold rounded-lg hover:bg-white/30 transition">
  📝 noteで詳しく読む
</a>
```

---

## 5. Google Drive 直リンクへ変更する場合(代替案)

`/downloads/` を使わず Google Drive 配布にする場合:

1. Google Drive で Excel をアップロード
2. 共有設定: 「リンクを知っている全員」 / 閲覧者
3. 共有リンクを `https://drive.google.com/uc?export=download&id=<FILE_ID>` 形式に書き換え
4. `index.html` の Excel ダウンロードボタン `href` を上記URLに置換

注意: Google Drive 直DLは大容量で警告画面が挟まる場合あり。Excel 22KB なら直接DLされる想定。

---

## 6. 公開後に追加検討する CTA

| 場所 | 候補 | タイミング |
|---|---|---|
| ヒーロー右上 | X フォローボタン | 1週間後 |
| FAQ末尾 | 「もっと質問する→Xへ」 | 1週間後 |
| 運営者カード | プロフィール画像 | 任意 |
| 各カード | 関連note記事リンク | note記事公開時 |
| シミュレータ右下 | 「使い方動画」(YouTube) | 任意 |

---

## 7. 反映フロー

```
1. index.html を編集
2. ローカルで http サーバ起動 → 動作確認
3. git add / commit / push
4. Cloudflare Pages が自動再デプロイ(1-2分)
5. ブラウザでキャッシュクリア後 表示確認
```

---

## 8. リンク死活監視(任意・後日)

- Cloudflare Web Analytics で 404 アクセス数を監視
- 月1回 `/downloads/doujin_uriage_kanri_v1_1.xlsx` の到達確認
- Excel バージョンアップ時は `_redirects` の `/excel` のターゲットを更新
