# Flask Greet App on Render

ワンクリックで Render にデプロイできます。

[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://dashboard.render.com/blueprint?repo=https://github.com/garyohosu/render_sample5)

## ローカル実行

```bash
python3 -m venv .venv
. .venv/bin/activate
pip install -r requirements.txt
python app.py
```

## Render での作成手順（Blueprint）
- 上の「Deploy to Render」ボタンをクリック
- サービス名を確認（`flask-greet-app`）。リージョン `oregon`、プラン `free` を選択
- Build Command: `pip install -r requirements.txt`
- Start Command: `gunicorn app:app`
- Health Check Path: `/`
- Auto Deploy: `commits`（デフォルト）
- Create Web Service → Build & Deploy 開始

デプロイ後、`/` でフォーム、`/greet` で挨拶が表示されます。
