はじめに
========

[GetFEM++](http://getfem.org)は汎用的で効率的な有限要素法の[C++](https://isocpp.org/)ライブラリです。有限要素法を用いて線形および非線形偏微分方程式を解くためのフレームワークを提供することを目指しています。[GetFEM++](http://getfem.org)ライブラリには多くの文書があり、その多くはさまざまな著者によって寄稿されています。[GetFEM++](http://getfem.org)の文書化に使用されるマークアップは[docutils](http://docutils.sourceforge.net/)プロジェクトによって開発された[reStructuredText](http://docutils.sourceforge.net/rst.html)で、[Sphinx](http://www.sphinx-doc.org/ja/stable/)というツールセットを使用しています。また、ドキュメントは[GNU Free Documentation
License](https://www.gnu.org/licenses/fdl.html)により改変および頒布が許可されています。

そこで、[Sphinx](http://www.sphinx-doc.org/ja/stable/)の国際化機能を使用して[GetFEM++](http://getfem.org)のドキュメント翻訳作業を翻訳プラットホーム[Transifex](https://www.transifex.com)で行いました。操作環境は[Ubuntu](https://www.ubuntu.com/)18.10です。

[GetFEM++](http://getfem.org)プロジェクト
=========================================

[GetFEM++](http://getfem.org)の英語の[Wikipedia](https://en.wikipedia.org/wiki/GetFEM++)を翻訳し、日本語の[Wikipedia](https://ja.wikipedia.org/wiki/GetFEM++)を作成しました。以下に内容を引用します。

> GetFEM++ は Python, Matlab そして
> Scilabのインタフェースを使用可能なC++の汎用ライブラリである。
> このライブラリの目的は有限要素法を用いて線形および非線形偏微分方程式を解くためのフレームワークを提供することである。
> 有限要素近似や数値積分法の選択の柔軟性が特徴の一つである。
> `「GetFEM++ - Wikipedia」(Oct.13,2018 12:01 UTC) より引用`

ライセンスや受賞歴については[ページ](https://ja.wikipedia.org/wiki/GetFEM++)を参照してください。[GetFEM++のチュートリアル](http://www.getfem.org/tutorial/index.html)には解析例が掲載されています。
![solution-thermo.png](https://qiita-image-store.s3.amazonaws.com/0/44756/e6fa4fc7-1c07-9170-32c5-c4f8a4bbd48f.png)
![wheel.png](https://qiita-image-store.s3.amazonaws.com/0/44756/1fdaab18-d531-3fc0-9790-3edbe96a7497.png)


[GetFEM++](http://getfem.org)はソースのホスティングサービスとして[Savannah](https://savannah.gnu.org)を使用しています。GNU[Savannah](https://savannah.gnu.org)についてWikipediaの説明を引用します。

> GNU Savannah
> は、フリーソフトウェアプロジェクトのための協働型ソフトウェア開発管理システムを提供するフリーソフトウェア財団のプロジェクトです。
> 現在は、CVS、GNU arch、Subversion、Git、Mercurial、GNU
> Bazaar、メーリングリスト、ウェブホスティング、ファイルホスティング、バグ管理サービスといった機能を提供しています。
> Savannah
> は、SourceForge.netと同じソフトウェアをベースとしたホスティングサービスシステムである
> Savane を使っています。
>
> `「GNU Savannah - Wikipedia」(Oct.13,2018 11:31 UTC) より引用`

このように、[Savannah](https://savannah.gnu.org)はGNUプロジェクトやフリーソフトのホスティングサービスとして広く使われています。このホスティングサービスでは非開発ユーザの場合、以下のようにして、リポジトリをクローンします。

また、ソースからコンパイルする必要のない場合には以下のように`aptitude`(もしくは`apt`)コマンドによりインストールすることも可能です。

これにより[GetFEM++](http://getfem.org)の[Python](https://www.python.org/)インターフェースとライブラリがインストールされます。

一方、Savannahのプロジェクトの開発に参加するにはの“New User”からユーザー登録が必要です。

開発者としてプロジェクトに参加するには、管理者にメッセージを送信し参加を承認してもらう必要があります。2018年10月現在の[GetFEM++](http://getfem.org)の管理者は [KonstantinosPoulios](http://www.dtu.dk/english/service/phonebook/person?id=65472&tab=2&qt=dtupublicationquery)氏と [Yves Renard](http://math.univ-lyon1.fr/~renard/) 氏です。開発者として権限が与えられたら、[How to contribute / Git repository on Savannah](http://getfem.org/project/index.html)を参考にプロジェクトにコミットをします。開発者として、リポジトリをクローンする場合は以下のようにします。

```
git clone https://git.savannah.nongnu.org/git/getfem.git
```

ここで、`savannah-login`はSavannahに登録したユーザ名です。ただし、何の設定もせずこれを実行すると認証エラーが発生します。このコマンドを実行する前にSavannahに認証鍵を登録しておく必要があります。まずは、ホームディレクトリで`ssh-keygen`コマンドを実行して認証鍵を作成してください。

```
ssh-keygen
```

これにより`/home/developer/.ssh/idrsa.pub`にRSA公開鍵のファイルが作成されます。これを、Savannahにのように作成されたファイルの中身を登録しておくと登録した認証鍵を持つPCでGitの操作が可能になります。登録可能な数は最大5個です。

[GetFEM++](http://getfem.org)プロジェクトでソースの変更を行う際にはGitで以下のようにブランチを作成する規約となっています。

```
git branch devel-me-rewrite-fem-kernel
git checkout devel-me-rewrite-fem-kernel
```

ここで、`name`は開発者の名前、`subject`は開発内容としてください。 [^1]修正後コミットをしてブランチに`push`します。

修正後メーリングリスト`getfem-commits@nongnu.org`に連絡をして`master`ブランチへのマージを管理者にリクエストしてください。*誤って*`master`*ブランチに*`push`*しないように十分注意してください*!!!管理者から注意されて`revert`されるでしょう。

[GetFEM++](http://getfem.org)のコンパイルとテスト方法
=====================================================

[GetFEM++](http://getfem.org)のコンパイルとテスト方法について説明します。まずは、`getfem`のリポジトリ直下にある`autogen.sh`を実行します。実行には`libtoolize`と`automake`が必要になりますので先にインストールしてください。

また、コンパイルに使用するライブラリとして以下のパッケージをインストールします。

-   `libqhull-dev` - calculate convex hulls and related structures
    (development files)

-   `libmumps-dev` - Direct linear systems solver - parallel development
    files

-   `libmumps-ptscotch-dev` - Direct linear systems solver -
    PTScotch-version development files

-   `libmumps-scotch-dev` - Direct linear systems solver -
    Scotch-version development files

-   `libmumps-seq-dev` - Direct linear systems solver - non-parallel
    development files

-   `liblapack-dev` - Library of linear algebra routines 3 - static
    version

-   `libopenblas-dev` - Optimized BLAS (linear algebra) library
    (development files) [^2]

さらに、[Python](https://www.python.org/)のためのヘッダーファイルとスタテックライブラリScipyをインストールします。
[Python](https://www.python.org/)2の場合

-   `python-dev` - header files and a static library for
    Python (default)

-   `python-scipy` - scientific tools for Python

[Python](https://www.python.org/)3の場合

-   `python3-dev` - header files and a static library for
    Python (default)

-   `python3-dev` - header files and a static library for
    Python (default)

をそれぞれインストールしてください。インストール後`./configure`をプロジェクトフォルダで実行して、Makefileを作成します。[Python](https://www.python.org/)2の場合、

```
$ ./configure
```

[Python](https://www.python.org/)3の場合、

```
$ ./configure --enable-python3
```

を実行します。Makefile作成後以下のコマンドでコンパイルとテストの実行をします。

[`automake`](https://www.gnu.org/software/automake/)により整備されたテスト項目が実行され結果がログファイル`tests/test-suite.log`に出力されます。
テストに失敗した場合は`getfem-users@nongnu.org`に`tests/test-suite.log`を添付し報告をしてください(*もちろんメッセージは英語で*!!!)。

[GetFEM++のSphinxドキュメント日本語化プロジェクト](http://www.sphinx-doc.org/ja/stable/intl.html)
=================================================================================================

[`sphinx-intl`](https://pypi.org/project/sphinx-intl/)による翻訳ワークフロー
----------------------------------------------------------------------------

[GetFEM++](http://getfem.org)の[Sphinx](http://www.sphinx-doc.org/ja/stable/)ドキュメントをコンパイルするには`doc`/`sphinx`で以下のコマンドを実行します。

これにより`doc`/`sphinx`/`build`以下の`html`ディレクトリと`pdf`ディレクトリにドキュメントが作成されます。コンパイルされた[Sphinx](http://www.sphinx-doc.org/ja/stable/)ドキュメントを[国際化](http://www.sphinx-doc.org/ja/stable/intl.html)のページを元に翻訳します。一連の作業は[sphinx-intl](https://pypi.org/project/sphinx-intl/)を使用して行います。[sphinx-intl](https://pypi.org/project/sphinx-intl/)は[Sphinx](http://www.sphinx-doc.org/ja/stable/)での翻訳フローを便利にするツールです。(http://www.sphinx-doc.org/ja/stable/_images/translation.png)

`sphinx-intl`のインストールは`pip`を使用して以下のように行います。

```
$ pip install sphinx-intl
```

`aptitude`で`sphinx-intl`をインストールをすることも可能ですが、[Python](https://www.python.org/)2のバージョンを確実にイントールするためにこの方法をとります。次に、`doc/sphinx/Makefile.am`と`doc/sphinx/source/conf.py`に以下の変更を適用します(`「Sphinx と transifex を活用した翻訳手順」(Oct.14,2018 05:45 UTC)を参照`)。
[^3]

``` {language="diff"}
diff --git a/doc/sphinx/Makefile.am b/doc/sphinx/Makefile.am
index adb8259e..2cab2a69 100644
--- a/doc/sphinx/Makefile.am
+++ b/doc/sphinx/Makefile.am
@@ -21,8 +21,10 @@
 # You can set these variables from the command line.
 PYTHON        = python
 SPHINXROOT    = http://svn.python.org/projects
-SPHINXOPTS    =
+LANGUAGE      = en
+SPHINXOPTS    = -D language=$(LANGUAGE)
 SPHINXBUILD   = $(PYTHON) tools/sphinx-build.py
+SPHINXINTL    = sphinx-intl
 PAPER         =
 SOURCES       = $(srcdir)/source
 DISTVERSION   = @VERSION@
@@ -33,8 +35,9 @@ PAPEROPT_a4     = -D latex_paper_size=a4
 PAPEROPT_letter = -D latex_paper_size=letter
 ALLSPHINXOPTS   = -b $(BUILDER) -d build/doctrees $(PAPEROPT_$(PAPER)) \
                   $(SPHINXOPTS) $(SOURCES) build/$(BUILDER)
+I18NSPHINXOPTS  = $(SPHINXOPTS) ./source

-.PHONY: help checkout update images build view html htmlview htmlhelp latex pdf linkcheck clean upload
+.PHONY: help checkout update images build view html htmlview htmlhelp latex pdf linkcheck clean upload gettext


 help:
@@ -85,6 +88,7 @@ images:
        -cd $(srcdir)/source/scilab/images/; make png

 build: $(srcdir)/source/matlab/cmdref.rst $(srcdir)/source/python/cmdref.rst $(srcdir)/source/scilab/cmdref.rst checkout images
+       $(SPHINXINTL) build
        echo # rm -fr build/$(BUILDER)/_images
        echo # rm -fr build/$(BUILDER)/*.png
        mkdir -p build/$(BUILDER) build/doctrees
@@ -110,7 +114,7 @@ htmlhelp: build
 latex: BUILDER = latex
 latex: build
        @echo "Build finished; the LaTeX files are in build/latex."
-       @echo "Run \`make all-pdf' or \`make all-ps' in that directory to" \
+       @echo "Run \`make all-pdf' in that directory to" \
              "run these through (pdf)latex."

 pdf: BUILDER = latex
@@ -122,6 +126,11 @@ linkcheck: BUILDER = linkcheck
 linkcheck: build
        @echo "Link check complete; look for any errors in the above output " \
              "or in build/$(BUILDER)/output.txt."
+gettext:
+       $(SPHINXBUILD) -b gettext $(I18NSPHINXOPTS) locale
+       $(SPHINXINTL) update -p locale -l $(LANGUAGE)
+       @echo
+       @echo "Build finished. The message catalogs are in locale."

 clean:
        -rm -rf build/
```

``` {language="diff"}
diff --git a/doc/sphinx/source/conf.py b/doc/sphinx/source/conf.py
index 14377f9d..fcaf2b7c 100644
--- a/doc/sphinx/source/conf.py
+++ b/doc/sphinx/source/conf.py
@@ -55,7 +55,7 @@ extensions = ['sphinx.ext.pngmath','sphinx.ext.autodoc',
 #source_suffix = '.rst'

 # The encoding of source files.
-#source_encoding = 'utf-8'
+source_encoding = 'utf-8'

 # The master toctree document.
 #master_doc = 'contents'
@@ -75,6 +75,9 @@ extensions = ['sphinx.ext.pngmath','sphinx.ext.autodoc',
 # relative to the source directory
 #locale_dirs = []

+gettext_compact = False
+locale_dirs = ['locale/']
+
 # Add any paths that contain templates here, relative to this directory.
 templates_path = ['.templates']
```

つぎに、以下のコマンドを`doc/sphinx`以下で実行し`locale`ディレクトリ以下を初期設定あるいは更新をします。

このコマンドを実行すると`pot`ファイルの作成と、`./locale/ja/LC_MESSAGES/`以下に`po`のファイルが作成もしくは更新されます。に示すように翻訳者は`po`ファイルの中身を編集します。`po`ファイルの中身は次のようになっています。

    #: src/name.c:36
    msgid "My name is %s.\n"
    msgstr ""

翻訳者はこのファイルを編集し以下のようにします。(`「gettext - Wikipedia」(Oct.13,2018 17:31 UTC) より引用`)

    #: src/name.c:36
    msgid "My name is %s.\n"
    msgstr "私の名前は %sです。\n"

翻訳が完了したら、`make html`もしくは`make latex`コマンドを実行します。`LANGUAGE`の`en`の部分は日本語の翻訳を適用する際には`ja`に変更してください。翻訳を適用する場合は`make pdf`は使用できないため注意してください。`make latex`を実行した後`doc/sphinx/build/latex`以下で`make all-pdf-ja`を実行してください。

[Transifex](https://www.transifex.com)の使用方法
------------------------------------------------

前節で作成した`*.po`ファイルを[Transifex](https://www.transifex.com)を使用して管理します。[Transifex](https://www.transifex.com)のサービスについて[Wikipedia](https://ja.wikipedia.org/wiki/Transifex)の内容を引用します。

> [Transifex](https://www.transifex.com)はWebベースの翻訳プラットフォームであり、ローカライズ管理システムとしても知られている。
> ソフトウェア、文書、Webサイトなど頻繁に更新されるコンテンツと技術的なプロジェクトを対象とし、開発者が使用するツールと統合することにより翻訳ワークフローを自動化している。
> 有料機能とオープンソースプロジェクト用の無料アカウント機能の両方をSaaSとして提供している。
> サイト内では翻訳者が共同作業できるようにするために翻訳対象のファイルホスティングや、フィード、掲示板投稿、翻訳提案や投票などのソーシャル・ネットワーキング・サービスとしての機能が利用できる。
> サイトはDjangoとPythonで構築されている。
> `「Transifex - Wikipedia」(Oct.14,2018 06:28 UTC) より引用`

本プロジェクトで新しくGetFEM++5.3の翻訳プロジェクトのためにのページを作成しました。翻訳の提案などはこちらのページで行うことができます。(https://www.transifex.com/getfem-doc/getfem-53-1/dashboard) 現在ボッチなので参加を歓迎いたします。

[Transifex](https://www.transifex.com)での翻訳結果を反映するためにはクライアントコマンド`tx`を使用します。`tx`コマンドは以下のようにインストールします。

```
$ sudo aptitude install transifex-client
```

インストール後`doc/sphinx`以下で以下のコマンドを実行してください。

このコマンドは設定ファイル`doc/sphinx/.tx/config`を参照して`source/locale`以下に`*.po`ファイルをダウンロードするコマンドです。[^4]APIキーを聞かれた際には[Transifex](https://www.transifex.com)のアカウントのページでAPIキーを発行してください。`po`ファイルをダウンロード後、前節で紹介した手順で翻訳されたドキュメントを作成します。なお本プロジェクトではトラブル防止のため、翻訳の修正を提案する場合は必ず[Transifex](https://www.transifex.com)のWebページから行ってください。`tx push`コマンドは使用しないでください。また、`tx push`をした後に`make gettext`を行うと`po`ファイルが更新されダウンロードした翻訳が消えることがあるため注意してください。

まとめ
======

-   <span>[GetFEM++のWikipediaの日本語版](https://ja.wikipedia.org/wiki/GetFEM++)を作成することによりGetFEM++プロジェクトの目的を紹介した。</span>

-   <span>[GetFEM++](http://getfem.org)のソースのホスティングサービス[Savannah](https://savannah.gnu.org)でプロジェクトに貢献する方法を紹介した。</span>

-   <span>[GetFEM++のSphinxドキュメント日本語化プロジェクト](http://www.sphinx-doc.org/ja/stable/intl.html)の内容について紹介した。</span>


[^1]: プロジェクトへの貢献方法はプログラムの新機能のパッチ作成だけではありません。
    ドキュメントを読んでいる際に気づいたTypo(打ち間違い)の修正も大切な貢献です。
    著者はTypoの修正のために`fixfixmisspell`という`branch`を作成したころ、Typo修正用の公式ブランチとして採用されました。
    詳細は、 <http://getfem.org/project/contribute.html> の“Specific
    branch for doc improvements and typo-fixes”を参照してください。
    自分の小さな提案が採用されることもOSSへの貢献の面白さかと思います。

[^2]: 第14回オープンCAE勉強会@関東（構造など）にて`openblas`を使用すると通常の`blas`より高速になるとの指摘を[@michioga](https://twitter.com/michioga)氏よりいただきました。

[^3]: 変更は2018年10月14日現在はブランチ`devel-tetsuo-translation`にコミットされています。
    コミットのSHA-1ハッシュは`d3d1d625c62e3e974087a7c16e2d13ed294c576d`です。
    管理者の承認が得られた場合`master`にマージされます。

[^4]: `doc/sphinx/.tx/config`はバージョンアップの際にTransifexのページ管理者が更新を行います。
    `doc/sphinx`で以下のコマンドを実行します。
