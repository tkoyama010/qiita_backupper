# はじめに:walking_tone1:
先日オープンCAEシンポジウムでGetFEM++のトレーニングの講師をやらせていただきました:beginner:

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">🔊<a href="https://twitter.com/hashtag/%E3%82%AA%E3%83%BC%E3%83%97%E3%83%B3CAE?src=hash&amp;ref_src=twsrc%5Etfw">#オープンCAE</a> シンポジウム2019で <a href="https://twitter.com/hashtag/GetFEM?src=hash&amp;ref_src=twsrc%5Etfw">#GetFEM</a>++のトレーニングを行います。 <br>✅タイトル データー分析と連携できる有限要素法解析ソフト　GetFEM++トレーニング<br>✅日時 12月19日（木）10:00 - 11:30</p>&mdash; ゆうげん🌎💡@2月29日&amp;3月1日 技術書典 (@tkoyama010) <a href="https://twitter.com/tkoyama010/status/1194938750180024320?ref_src=twsrc%5Etfw">November 14, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

このトレーニングでは、環境構築によるトラブルを避けるためGoogleColaboratoryを使用してオンラインで作業をしました:globe_with_meridians:

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">✅資料について<br>🌐Google Colaboratoryで起動をして説明します⬇<a href="https://t.co/aAotZVdMwd">https://t.co/aAotZVdMwd</a><br>VTKで出力した結果を <a href="https://twitter.com/hashtag/mayavi2?src=hash&amp;ref_src=twsrc%5Etfw">#mayavi2</a> で可視化します🔲<br>mayavi2については説明しませんが、以下で詳細を確認できます⬇<a href="https://t.co/pGxX85rvCg">https://t.co/pGxX85rvCg</a></p>&mdash; ゆうげん🌎💡@2月29日&amp;3月1日 技術書典 (@tkoyama010) <a href="https://twitter.com/tkoyama010/status/1201154231505321984?ref_src=twsrc%5Etfw">December 1, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

この資料を作る際、vtkの解析結果をmayavi2と呼ばれる可視化ツールを使用してGoogleColaboratory上に画像として出力しています:bar_chart:
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/44756/20b28eea-5c2c-a800-1562-a7b480526593.png)
この画像を作る際、トラブルシューティングが必要であったため、ここで紹介します:raised_hand:

# インストール:hatching_chick:

GoogleColaboratoryを開き以下のコマンドでインストールをします。簡単ですね:relaxed:

```bash
!pip install mayavi
```

# コマンド実行

:warning:mayavi2の実行にはディスプレイ:desktop:環境が必要です。Google Colaboratoryではディスプレイ環境が提供されていないので仮想ディスプレイを設定します。

```bash
!apt-get -qq -y install xvfb
!pip install pyvirtualdisplay
```
インストール後、以下のように仮想ディスプレイを作成します。

```python
import os
from pyvirtualdisplay import Display
display = Display(visible=0, size=(1024, 480))
display.start()
os.environ["DISPLAY"] = ":" + str(display.display) + "." + str(display.screen)
```

メッシュ画像を表示するため、先にファイル`mesh.vtk`をColaboratory上にアップロードしておきます。

```bash
!mayavi2 --offscreen -d mesh.vtk -m Axes -f ExtractEdges -m Surface \
-s "scene.save('mesh.png', size=(700, 500))"
```
mayaviはコマンドラインに便利なオプションがついています。そのため、簡単なプロットであれば、コマンドラインのみで実行可能です。オプションの詳細については[こちら](https://mayavi-ja.readthedocs.io/ja/latest/application.html#command-line-arguments)を参照してください:writing_hand:

:warning:ただし、今の状態でmayaviを実行するとエラーが発生します。

```
IOError: [Errno 2] No such file or directory: '/tmp/.enthought/mayavi_e3/mayavi.log'
```

ログファイルのファイルかディレクトリが存在しないというエラーですので、先に作成をしてから実行します。

```bash
!mkdir /tmp/.enthought
!mkdir /tmp/.enthought/mayavi_e3
```
ユーザーがログファイルのフォルダを作成するのはスマートではないので、mayavi2のリポジトリにプルリクエストを作成しました。
<blockquote class="twitter-tweet"><p lang="und" dir="ltr"><a href="https://t.co/xh1GQf8Vv0">https://t.co/xh1GQf8Vv0</a></p>&mdash; ゆうげん🌎💡@2月29日&amp;3月1日 技術書典 (@tkoyama010) <a href="https://twitter.com/tkoyama010/status/1208653854364987396?ref_src=twsrc%5Etfw">December 22, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
実行後、再度mayaviを実行すると画像ファイル `mesh.png` が作成されます。この画像をGoogle Colaboratory上に表示すれば、メッシュを可視化することができます。

```python
from IPython.display import Image, display_png
display_png(Image("mesh.png"))
```
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/44756/f608cdc0-1490-2b44-a14c-31ec30da66f2.png)

# Python:snake:を使った可視化
mayaviのmlab pipelineを使えばpythonでvtkを可視化することもできます。ただし、Python3でのプロットではエラーが発生しているため現在調査中です:dizzy_face:Python2では問題なく動作していたため、Python3特有の問題と予想しています。

# まとめ
GoogleColaboratoryでmayavi2を使うのはトラブルが多そうです:dizzy_face:一方でmayavi2は3次元の可視化の機能が充実したvisualizerですので問題を解決すれば可能性が広がると思います:relieved:
