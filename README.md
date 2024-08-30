# プロジェクト概要

このプロジェクトでは、Dockerを使用してLinux環境を構築し、PythonのWSGIサーバーを立てる方法について説明します。さらに、ngrokを使用してローカルサーバーを外部からアクセス可能にする方法も紹介します。

## Dockerを使ったLinux環境の構築

1. **Dockerfileの作成**
    ```Dockerfile
    # ベースイメージとして公式のPythonイメージを使用
    FROM python:3.9-slim

    # 作業ディレクトリを設定
    WORKDIR /app

    # 必要なパッケージをインストール
    COPY requirements.txt .
    RUN pip install --no-cache-dir -r requirements.txt

    # アプリケーションのソースコードをコピー
    COPY . .

    # WSGIサーバーを起動
    CMD ["gunicorn", "--bind", "0.0.0.0:8000", "myapp.wsgi:application"]
    ```

2. **Dockerイメージのビルド**
    ```sh
    docker build -t my-python-app .
    ```

3. **Dockerコンテナの起動**
    ```sh
    docker run -d -p 8000:8000 my-python-app
    ```

## ngrokを使ったローカルサーバーのテスト

1. **ngrokのインストール**
    ngrokの公式サイトからインストーラーをダウンロードし、インストールします。

2. **ngrokの起動**
    ```sh
    ngrok http 8000
    ```

3. **外部アクセス用URLの確認**
    ngrokを起動すると、ターミナルに外部アクセス用のURLが表示されます。このURLを使用して、外部からローカルサーバーにアクセスできます。

以上が、Dockerを使ってLinux環境を構築し、PythonのWSGIサーバーを立てる方法と、ngrokを使ってローカルサーバーをテストする方法です。