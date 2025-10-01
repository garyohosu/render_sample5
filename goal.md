# Goal
Flask アプリを一から作成し、Render にデプロイできる状態にする。  
ルート `/` にフォームを表示し、ユーザーが名前を入力すると `/greet` ページで「こんにちは、<名前>さん！」と返す。  
デザインには Bootstrap (CDN) を利用して、見栄えをモダンにする。  

# Steps
1. 空のリポジトリに Flask プロジェクトを初期化する。
2. 必要なファイルをすべて作成する：
   - `app.py`
   - `requirements.txt`
   - `Procfile`
   - `templates/base.html`
   - `templates/index.html`
   - `templates/greet.html`
3. git にコミットして GitHub に push する。
4. Render で自動ビルド & デプロイが行われ、Bootstrap でスタイリングされたページが表示される。

# Files to Create

## app.py
```python
from flask import Flask, render_template, request

app = Flask(__name__)

@app.route("/", methods=["GET", "POST"])
def index():
    return render_template("index.html")

@app.route("/greet", methods=["POST"])
def greet():
    name = request.form.get("name", "名無し")
    return render_template("greet.html", name=name)

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

## requirements.txt
```
Flask==3.0.0
gunicorn
```

## Procfile
```
web: gunicorn app:app
```

## templates/base.html
```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <title>{% block title %}{% endblock %}</title>
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body class="bg-light">
    <div class="container py-5">
        {% block content %}{% endblock %}
    </div>
    <!-- Bootstrap JS -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

## templates/index.html
```html
{% extends "base.html" %}

{% block title %}フォーム入力 (Bootstrap版){% endblock %}

{% block content %}
<h1 class="mb-4">名前を入力してください</h1>
<form action="/greet" method="post" class="mb-3">
    <div class="mb-3">
        <input type="text" class="form-control" name="name" placeholder="名前を入力">
    </div>
    <button type="submit" class="btn btn-primary">送信</button>
</form>
{% endblock %}
```

## templates/greet.html
```html
{% extends "base.html" %}

{% block title %}挨拶ページ{% endblock %}

{% block content %}
<h1 class="mb-4">こんにちは、{{ name }}さん！</h1>
<a href="/" class="btn btn-secondary">戻る</a>
{% endblock %}
```

# Git Commands
```bash
git init
git add .
git commit -m "Initial Flask app with Bootstrap"
git branch -M main
git remote add origin git@github.com:<USERNAME>/<REPO>.git
git push -u origin main
```

# Expected Result
Render がリポジトリを自動ビルドし、  
ブラウザで `https://<your-app>.onrender.com/` を開くと以下の動作をする：  

1. `/` にアクセスすると Bootstrap スタイルのフォームが表示される  
2. 名前を入力して送信すると `/greet` に遷移  
3. 「こんにちは、<入力した名前>さん！」が Bootstrap デザインで表示される

