---
layout: post
title:  "『Effective Python』を読んだ"
date:   2017-04-15 21:12:04 +0900
categories: book
description: "『Effective Python』を読んだ。Pythonicな書き方、お作法を学ぶのによい本。"
---

『Effective Python』を読んだ。  
メインで扱っている言語がPHPとJavaScriptで、これらのコードの書き方の作法はわかっているがPythonのそれはわかっていない。  
Pythonらしい書き方、行儀のよいPythonコードの書き方を学ぶためにこの本を読んだ。  

よく、他の言語から入ってきた人が書いたコードで
「あーこれPHPじゃこんなやり方しないよなー。ちょっといけてねーなー」と思うことがよくあり、
自分の書いたPythonコードがそう思われたくない。  
Pythonicな書き方を学ぶにはこの本がよい、と風の噂で聞いたので読んでみた。

![effective_python](/public/image/20170415/effective_python.jpg)

中級者・上級者向けの本であるためか、Pythonの文法・基本的な知識がないと読めない本である。  
一番自分が知りたかったPythonicな書き方というものは最低限知れたのかなと思う。  
最低限というのは、小さい単位でコードを分割したときの場合においてPythonicに書けそうだが、
大規模のコードだとどのようになるのか、どのような書き方がベストなのか、というのがイメージしづらかった。  
このへんはDjangoで何かアプリを書いてみて、自分なりに噛み砕きながら理解していくしかなさそう。
Pythonでこの辺を記してある本をさがすか。

さて、この本の感想だが、Pythonを扱うならぜひ読んでおくべき本だと思う。  
Pythonicな書き方について1章にわたって解説されている。  
この章は必読に値する。

本の内容は以下のとおり。
```
1章 Python流思考（Pythonic Thinking）
2章 関数
3章 クラスと継承
4章 メタクラスと属性
5章 並行性と並列性
6章 組み込みモジュール
7章 協働作業（コラボレーション）
8章 本番運用準備
```

1章はもちろんのこと『2章 関数』『3章 クラスと継承』『4章 メタクラスと属性』『6章 組み込みモジュール』は読み応えがあった。  
Pythonの良いところとして、メタクラスやデコレーターを使って既存のクラス・メソッドを変更せずに振る舞いを変えることができるのがとても良いと思っていて、それが4章と6章で言及されていて大変ためになった。

5章はPythonでより速度を出すには、マシンの性能をうまく使うには、ということを処理の並列化によって実現するにあたって注意すべきことが書いてあり、いまのところそれほど性能が求められるようなものを書く予定はないが、今後必ず役に立つと思う。  
Pythonのパフォーマンスについては、オライリーから『ハイパフォーマンスPython』や『Cython - Cとの融合によるPythonの高速化』といった書籍がありいつか読んでみたい。

<a target="_blank"  href="https://www.amazon.co.jp/gp/product/4873117569/ref=as_li_tl?ie=UTF8&camp=247&creative=1211&creativeASIN=4873117569&linkCode=as2&tag=pinekta02-22&linkId=a0ef74a6850e678f28fe7bb501e8f401"><img border="0" src="//ws-fe.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=JP&ASIN=4873117569&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=pinekta02-22" ></a><img src="//ir-jp.amazon-adsystem.com/e/ir?t=pinekta02-22&l=am2&o=9&a=4873117569" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />
