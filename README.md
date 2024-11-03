Openstack Memo
===

## ビルドに必要なパッケージのインストール

- venv 環境作成と有効化

    ```bash
    python3 -m venv venv
    source ./venv/bin/activate
    ```

- Python 拡張のインストール

    ```bash
    pip install -r requirements.txt
    ```

- 日本語フォントのインストール

    ```bash
    sudo apt install -y fonts-ipafont fonts-ipaexfont
    ```

## ドキュメントのビルド

- 初期化

    ```bash
    sphinx-quickstart doc \
        --sep \
        --project "Virtual Machine Memo" \
        --author "hogehoge" \
        -v 0.1 \
        --release 0.1 \
        --language='en' \
        --no-batchfile
    ```

- conf.py

    ```python
    extensions = [
        'sphinx.ext.autodoc',  # 自動生成ドキュメントの拡張
        'sphinx.ext.napoleon', # GoogleスタイルおよびNumpyスタイルのdocstringを解釈するための拡張
        'myst_parser',         # MyST (Markedly Structured Text) パーサーを有効化
        'sphinx_markdown_tables',
        'sphinxcontrib.blockdiag',
        'sphinxcontrib.seqdiag',
        'sphinxcontrib.actdiag',
        'sphinxcontrib.nwdiag',
        'sphinxcontrib.rackdiag',
        'sphinxcontrib.packetdiag',
    ]

    source_suffix = {
        '.rst': 'restructuredtext',
        '.md': 'markdown',  # Markdownの拡張子を設定
    }
    ```

- ドキュメントのビルド

    ```bash
    make html
    ```

