下敷き
===

## 環境構築

1. Sphinx 関連 Python 拡張のインストール

    ```bash
    pip3 install --break-system-packages \
        sphinx \
        sphinx_rtd_theme \
        sphinxcontrib-actdiag \
        sphinxcontrib-blockdiag \
        sphinxcontrib-nwdiag \
        sphinxcontrib-seqdiag \
        myst_parser \
        sphinx_markdown_tables
    ```

2. 日本語フォントのインストール

    ```bash
    sudo apt install -y fonts-ipafont fonts-ipaexfont
    ```

## ドキュメント作成

1. プロジェクト作成

    ```bash
    sphinx-quickstart sphinx-sample
    ```

    対話応答例

    ```text
    Sphinx 7.3.7 クイックスタートユーティリティへようこそ。
    
    以下の設定値を入力してください（Enter キーのみ押した場合、
    かっこで囲まれた値をデフォルト値として受け入れます）。
    
    選択されたルートパス: sphinx-sample
    
    Sphinx 出力用のビルドディレクトリを配置する方法は2つあります。
    ルートパス内にある "_build" ディレクトリを使うか、
    ルートパス内に "source" と "build" ディレクトリを分ける方法です。
    > ソースディレクトリとビルドディレクトリを分ける（y / n） [n]: y
    ### source と build を分けたいので y としています
    
    プロジェクト名は、ビルドされたドキュメントのいくつかの場所にあります。                              
    > プロジェクト名: sphinx-sample
    > 著者名（複数可）: hogehoge                                                                        
    > プロジェクトのリリース []: 1.0.0
    ### 適宜、変更してください
    
    ドキュメントを英語以外の言語で書く場合は、
     言語コードで言語を選択できます。Sphinx は生成したテキストをその言語に翻訳します。
    
    サポートされているコードのリストについては、
    https://www.sphinx-doc.org/en/master/usage/configuration.html#confval-language を参照してください。
    > プロジェクトの言語 [en]: en
    ### 日本語の場合でも ja より en のままのほうが良いらしいです
    
    ファイル /home/lubuntu/work/sphinx-sample/source/conf.py を作成しています。
    ファイル /home/lubuntu/work/sphinx-sample/source/index.rst を作成しています。
    ファイル /home/lubuntu/work/sphinx-sample/Makefile を作成しています。
    ファイル /home/lubuntu/work/sphinx-sample/make.bat を作成しています。
    
    終了：初期ディレクトリ構造が作成されました。
    
    マスターファイル /home/lubuntu/work/sphinx-sample/source/index.rst を作成して
    他のドキュメントソースファイルを作成します。次のように Makefile を使ってドキュメントを作成します。
     make builder
    "builder" はサポートされているビルダーの 1 つです。 例: html, latex, または linkcheck。
    ```

2. config.py 編集

    - テーマを `alabaster` ⇒ `sphinx_rtd_theme` に変更
    - reStructuredText の他に Markdown を使えるようにする
    - reStructuredText で図を描けるようにする

    ```diff
    --- /tmp/conf.py        2024-06-08 22:55:32.988390061 +0900
    +++ source/conf.py      2024-06-08 22:59:57.723278228 +0900
    @@ -14,7 +14,18 @@
     # -- General configuration ---------------------------------------------------
     # https://www.sphinx-doc.org/en/master/usage/configuration.html#general-configuration
     
    -extensions = []
    +extensions = [
    +    'sphinx.ext.autodoc',  # 自動生成ドキュメントの拡張
    +    'sphinx.ext.napoleon', # GoogleスタイルおよびNumpyスタイルのdocstringを解釈するための拡張
    +    'myst_parser',         # MyST (Markedly Structured Text) パーサーを有効化
    +    'sphinx_markdown_tables',
    +    'sphinxcontrib.blockdiag',
    +    'sphinxcontrib.seqdiag',
    +    'sphinxcontrib.actdiag',
    +    'sphinxcontrib.nwdiag',
    +    'sphinxcontrib.rackdiag',
    +    'sphinxcontrib.packetdiag',
    +]
     
     templates_path = ['_templates']
     exclude_patterns = []
    @@ -24,5 +35,11 @@
     # -- Options for HTML output -------------------------------------------------
     # https://www.sphinx-doc.org/en/master/usage/configuration.html#options-for-html-output
     
    -html_theme = 'alabaster'
    +html_theme = 'sphinx_rtd_theme'
     html_static_path = ['_static']
    +
    +source_suffix = {
    +    '.rst': 'restructuredtext',
    +    '.md': 'markdown',  # Markdownの拡張子を設定
    +}
    +
    ```

3. トップページ (index.rst) の修正

    - タイトルの変更
    - 索引リンク、検索リンクの削除

    ```diff
    --- /tmp/sphinx-sample/source/index.rst 2024-06-09 07:10:45.447721634 +0900
    +++ index.rst   2024-06-09 07:18:04.702283724 +0900
    @@ -3,18 +3,10 @@
        You can adapt this file completely to your liking, but it should at least
        contain the root `toctree` directive.
     
    -Welcome to Sphinx Sample's documentation!
    -=========================================
    +Sphinx Sample
    +=============
     
     .. toctree::
        :maxdepth: 2
        :caption: Contents:
     
    -
    -
    -Indices and tables
    -==================
    -
    -* :ref:`genindex`
    -* :ref:`modindex`
    -* :ref:`search`
    ```

4. ドキュメントのビルド

    ```bash
    cd sphinx-sample
    make html
    ```

    ドキュメントをビルドした結果、`./build/html/index.html/` をトップページの HTML ドキュメントが生成されるはずです。
