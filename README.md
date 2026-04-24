# AccuVoca Terminal

## デプロイ手順(貼るだけ版)

1. GitHubで新しいリポジトリを作る(例: `accuvoca-terminal`)
2. この `index.html` をリポジトリのルートに置く(**ファイル名は必ず `index.html`**)
3. リポジトリの **Settings → Pages**
   - Source: `Deploy from a branch`
   - Branch: `main`(または `master`) / `/ (root)`
   - Save
4. 1〜2分待ってから `https://<ユーザー名>.github.io/<リポ名>/` にアクセス

以上。これで動く。

## このファイルについて

- **1枚のHTML**で完結。外部JSファイルなし
- React 18 / ReactDOM / Babel standalone を `unpkg.com` CDN から読み込み
- JetBrains Mono フォントを Google Fonts から読み込み
- それ以外の外部依存は一切なし

もし CDN が読み込めない場合、画面上部に赤いエラーメッセージが出るようにしてあります。

## トラブルシューティング

### 画面が真っ白のまま

F12 で DevTools を開き Console タブ を確認してください。

**よくあるエラー:**

| エラー | 原因 | 対処 |
|---|---|---|
| `Failed to load resource (unpkg.com)` | 広告ブロッカーが unpkg をブロック | ブロッカーの例外設定に追加、または別のCDN(jsdelivr)に差し替え |
| `Refused to execute inline script` | 会社PCのCSPポリシー | 自宅環境や別ブラウザで試す |
| 何も出ないが画面真っ白 | Babel がまだ変換中 | 数秒待つ(初回ロードは 2〜3 秒かかる) |

### GitHub Pages にアクセスしたら 404

- ファイル名が `index.html` になっているか確認(`AccuVoca_Terminal_Standalone.html` 等のままだと 404)
- リポジトリのルートに置かれているか確認(サブフォルダ禁止)
- Settings → Pages で `main / root` が選択されているか確認
- Pages のビルドには 1〜2 分かかる。その間は古い 404 が返る場合あり

### ローカルで開きたい(file://)

`file://` プロトコルでも動くはずですが、ブラウザによっては CDN のCORS制限に引っかかることがあります。
ローカルで試す場合は、ファイルのあるディレクトリで以下を実行:

```bash
python3 -m http.server 8000
# → http://localhost:8000/ にアクセス
```

### Claude Designsで編集しなおしたら再度同じことを?

はい。ただし `screens.jsx`(コンポーネント定義)と本体の画面遷移ロジックが分かれているので、編集した箇所だけこのHTMLの該当部分に差し替えれば再ビルド不要です。
