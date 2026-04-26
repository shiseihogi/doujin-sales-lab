# GitHub + Cloudflare Pages 公開手順

**TASK_ID**: T1SITE1
**目的**: 今日中に `https://doujin-sales-lab.pages.dev/` で公開する。

---

## 0. 前提

- GitHub アカウント: 既存(`shiseihogi`)
- Cloudflare アカウント: 既存(chromeai-lab で連携済)
- Git: ローカルにインストール済み
- リポジトリ名: `doujin-sales-lab`(推奨)
- 公開URL(初期): `https://doujin-sales-lab.pages.dev/`

---

## 1. GitHub リポジトリ作成

ブラウザで:
1. https://github.com/new を開く
2. Repository name: **`doujin-sales-lab`**
3. Description(任意): `同人作家向け売上管理ラボ — 手取りシミュレータ + Excel無料配布`
4. **Public** を選択
5. README / .gitignore / license は **追加しない**(ローカルにあるので)
6. 「Create repository」

---

## 2. ローカルから push

```bash
cd C:\Users\81808\Desktop\New\doujin-sales-lab
git init
git add .
git commit -m "Initial commit: 同人売上管理ラボ MVP公開"
git branch -M main
git remote add origin https://github.com/shiseihogi/doujin-sales-lab.git
git push -u origin main
```

認証はブラウザポップアップ or GitHub CLI(`gh auth login` 済みなら不要)。

---

## 3. Cloudflare Pages 連携

ブラウザで:
1. https://dash.cloudflare.com/ → 「Workers & Pages」 → 「Create application」 → 「Pages」 → 「Connect to Git」
2. **GitHub アカウント連携** → `shiseihogi/doujin-sales-lab` を選択
3. ビルド設定:
   - **Project name**: `doujin-sales-lab`(URL: `doujin-sales-lab.pages.dev`)
   - **Production branch**: `main`
   - **Framework preset**: `None`
   - **Build command**: (空欄)
   - **Build output directory**: `/`(ルート)
   - **Root directory**: (空欄)
4. 「Save and Deploy」

初回デプロイは1〜2分で完了。

---

## 4. デプロイ確認

1. Cloudflare Pages のダッシュボードで「Deployments」タブを確認
2. **Status: Success** を確認
3. 公開URLをクリック → `https://doujin-sales-lab.pages.dev/` が表示される

---

## 5. 短縮URL確認(_redirects 反映)

- `https://doujin-sales-lab.pages.dev/excel` → Excel直DL
- `https://doujin-sales-lab.pages.dev/dl` → Excel直DL
- `https://doujin-sales-lab.pages.dev/download` → トップの Excel配布セクションへ

---

## 6. カスタムドメイン(任意・後日)

今日は `pages.dev` で公開、カスタムドメインは後日でOK。

導入する場合:
1. Cloudflare Pages → プロジェクト → 「Custom domains」
2. ドメイン入力(例: `doujin-sales-lab.com`)
3. CNAME / DNS 設定(Cloudflare がガイド)

---

## 7. トラブルシュート

### 7.1 push できない
- GitHub CLI: `gh auth login` で再認証
- HTTPS なら Personal Access Token、SSH なら ssh-keygen 設定

### 7.2 Cloudflare Pages で 404
- Output directory が `public/` になっていないか確認 → ルート `/` に修正
- `index.html` がリポジトリのルートにあるか確認

### 7.3 Excel ダウンロードでファイルが開く(DL されない)
- `_headers` の `/downloads/*` に `Content-Disposition: attachment` を入れている → これで強制DL
- 反映されない場合はキャッシュクリア → 再デプロイ

### 7.4 シミュレータが動かない
- ブラウザのコンソールで JS エラーを確認
- TailwindCSS CDN が読まれているか
- ファイル直開き(`file://`)では一部機能制限あり → http サーバ経由で確認

---

## 8. 反映までの目安

| 工程 | 時間 |
|---|---|
| GitHub リポジトリ作成 | 1分 |
| ローカル push | 1分 |
| Cloudflare Pages 連携 + 初回デプロイ | 3〜5分 |
| 反映確認 | 1分 |
| **合計** | **〜10分** |

---

## 9. 公開後 push する場合

修正後:
```bash
cd C:\Users\81808\Desktop\New\doujin-sales-lab
git add .
git commit -m "<修正内容を1行で>"
git push
```

Cloudflare Pages は自動再デプロイ(1〜2分で反映)。
