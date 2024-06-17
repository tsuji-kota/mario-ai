# ベースイメージとしてMinicondaを使用
FROM continuumio/miniconda3

# 作業ディレクトリを設定
WORKDIR /workspace

# 必要なツールをインストール
RUN apt-get update && apt-get install -y \
    build-essential \
    gfortran \
    && rm -rf /var/lib/apt/lists/*

# conda環境を作成
RUN conda create --name py38 python=3.8

# 環境をアクティベートし、pipをインストール
SHELL ["conda", "run", "-n", "py38", "/bin/bash", "-c"]

# 最新の conda に更新
RUN conda update -n base -c defaults conda

# 必要なファイルをコンテナにコピー
COPY requirements.txt /workspace

# 必要なパッケージをインストール
RUN pip install --upgrade pip
RUN pip install -r /workspace/requirements.txt

# 必要なファイルをコンテナにコピー
COPY . /workspace

# 作業ディレクトリに移動
WORKDIR /workspace

# 必要に応じてPythonスクリプトやコマンドを実行
CMD ["bash"]
