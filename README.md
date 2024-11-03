ReadMe
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


## Markdown 形式の警告ディレクティブ

- reStructuredText の書式は [警告ディレクティブ｜Sphinx の使い方](https://zenn.dev/y_mrok/books/sphinx-no-tsukaikata/viewer/chapter20) で解説されています。
- `tips` と `admonition` は、Markdown の方では対応していないようです。
- 警告ディレクティブの書式例の先頭の全角スペースはコードを表示する都合で入れています。

### Attention

```text
　```{attention}
　表示例
　```
```

### Caution

```text
　```{caution}
　表示例
　```
```

### Danger

```text
　```{danger}
　表示例
　```
```

### Error

```text
　```{error}
　表示例
　```
```

### Hint

```text
　```{hint}
　表示例
　```
```

### Important

```text
　```{important}
　表示例
　```
```

### Note

```text
　```{note}
　表示例
　```
```

### Warning

```text
　```{warning}
　表示例
　```
```

