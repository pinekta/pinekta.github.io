---
layout: post
title:  "『入門 Python 3』を読んだ"
date:   2017-04-06 23:50:32 +0900
categories: book
description: "来週から本格的にPythonでデータ分析を始めることになるので、そのまえにPythonの復習をすることにした。オライリーの『入門 Python 3』を読んだ。原題は『Introducing Python』。"
---

来週から本格的にPythonでデータ分析を始めることになるので、
そのまえにPythonの復習をすることにした。  
オライリーの『入門 Python 3』を読んだ。
原題は『Introducing Python』。

対象としている読者は「プログラミング初心者」らしい。  
さすがオライリー。こんなん初心者殺しやわ。  
オライリーの本で初心者向けというのはだいたいウソ。  
別のプログラミング言語をやったことがある人じゃないと30ページくらいで挫折すると思う。  

![introduction_python3](/public/image/20170406/introduction_python3.jpg)

中級者以上にとっては、今からPythonを学ぶために読む本としてはとてもよいと思う。  

本の内容は以下のとおり。
```
1章 Pyの味
2章 Pyの成分：数値、文字列、変数
3章 Pyの具：リスト、タプル、辞書、集合
4章 Pyの皮：コード構造
5章 Pyの化粧箱：モジュール、パッケージ、プログラム
6章 オブジェクトとクラス
7章 プロのようにデータを操る
8章 データの行き先
9章 ウェブを解きほぐす
10章 システム
11章 並行処理とネットワーク
12章 パイソニスタになろう
付録A Pyアート
付録B ビジネス現場のPy
付録C 科学におけるPy
付録D Python3のインストール
付録E 復習課題の解答
付録F 早見表
```

1章から6章までがPythonの言語についての説明となり、残りの章はライブラリの説明が主となっておりあまり見るべきものはなかった。  
付録だけで120ページほどある。全部で567ページあるうちの120ページほどが付録である。
ここまでくると付録ではなくて新たに章立てしたほうがよいのではないかと思うくらいだ。

最近はPythonを長らく書いていないが、Pythonを書いていたときはとてもいい言語だと思っていた。  
言語仕様がシンプルで美しい。  
そしてスピードも出る。科学計算に強い。Webアプリケーションも書ける。CUIのアプリケーションも書ける。なにより機械学習方面にも強い。  
自分の印象だと隙がない言語。

Pythonは内包表記や後置if文とかがとても良い。  
ただ、Pythonは抽象クラスはライブラリをインポートしないと使えないし、インターフェースがない。  
下位クラスに実装を強制させるような仕組みがない。

また、privateやprotectedといった概念がないし、
constやfinalがない、というところはいただけない。

あとメンバメソッドの第一引数がselfとなるのも若干キモさを感じる。

面白いところは多重継承をサポートしているところ。  
けど実装が煩雑になりそうだ。

しかし、Pythonはとても面白い言語ではあると思うので積極的に使っていきたい。  
また1章から6章までを読んでみようかな。

<a target="_blank"  href="https://www.amazon.co.jp/gp/product/4873117380/ref=as_li_tl?ie=UTF8&camp=247&creative=1211&creativeASIN=4873117380&linkCode=as2&tag=pinekta02-22&linkId=540793ea099253e29fe95682a9829086"><img border="0" src="//ws-fe.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=JP&ASIN=4873117380&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=pinekta02-22" ></a><img src="//ir-jp.amazon-adsystem.com/e/ir?t=pinekta02-22&l=am2&o=9&a=4873117380" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />
