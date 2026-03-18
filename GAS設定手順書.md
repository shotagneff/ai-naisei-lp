# GAS・Xserver 設定手順書
## AI内製化研修 for 経営・事業責任者

---

## STEP 1：GASのCONFIG値を差し替える

Google Apps Scriptを開き、`form-sheet.gs` の冒頭にある `CONFIG` の以下2箇所を差し替えてください。

### 差し替え前
```javascript
const CONFIG = {
  downloadUrl: '',   // ← 未設定
  consultUrl:  '',   // ← 未設定
  ...
};
```

### 差し替え後
```javascript
const CONFIG = {
  downloadUrl: 'https://drive.google.com/file/d/14k4CbmoMJTvxgGW7nfot3_w5eCMnefSD/view?usp=sharing',
  consultUrl:  'https://seekad.co.jp/ai-training-management/consultation-form.html',
  ...
};
```

差し替え後、**「デプロイ」→「デプロイを管理」→「編集」→「バージョン：新しいバージョン」→「デプロイ」** を実行してください。

> ⚠️ 再デプロイしないと変更が反映されません。

---

## STEP 2：Xserverへのファイルアップロード

### 2-1. ファイルマネージャーにログイン

1. [Xserverサーバーパネル](https://www.xserver.ne.jp/login_server.php) にログイン
2. 「ファイル管理」→「ファイルマネージャー」を開く
3. `public_html/` に移動

### 2-2. フォルダを作成

`public_html/` の中に **`ai-training-management`** という名前のフォルダを作成する。

### 2-3. ファイルをアップロード

添付の `ai-training-management.zip` を解凍し、中のファイルをすべて `ai-training-management/` フォルダにアップロードする。

アップロードするファイル一覧：
```
index.html
form.html
consultation-form.html
program-guide-mockup-pc.png
program-guide-mockup-horizontal.png
```

### 2-4. 動作確認

以下のURLにアクセスして表示を確認する：

| ページ | URL |
|---|---|
| LP | https://seekad.co.jp/ai-training-management/ |
| 資料請求フォーム | https://seekad.co.jp/ai-training-management/form.html |
| 無料相談フォーム | https://seekad.co.jp/ai-training-management/consultation-form.html |

---

## STEP 3：フォーム送信テスト

1. テスト用のメールアドレスで資料請求フォームを送信
2. スプレッドシートの「資料DL送信」タブにデータが記録されているか確認
3. お礼メール（資料DLリンク付き）が届くか確認
4. 同様に無料相談フォームもテスト

---

## 補足：ステップメールの内容変更

スプレッドシートの以下のタブで件名・本文・送信タイミングを自由に変更できます。GASの再デプロイは不要です。

| タブ名 | 対象 |
|---|---|
| ステップメール設定 | 資料請求後のステップメール（2日後・5日後・7日後） |
| ステップメール設定_相談 | 無料相談後のステップメール（翌日・3日後・5日後） |

使えるプレースホルダー：
- `{name}` — 受信者の氏名
- `{downloadUrl}` — 資料DLリンク
- `{consultUrl}` — 無料相談フォームURL
