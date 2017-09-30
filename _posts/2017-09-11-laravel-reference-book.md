---
layout: post
title:  "『Laravelリファレンス』を読んだ"
date:   2017-09-11 07:12:45 +0900
categories: book
description: "『Laravelリファレンス』を読んだ。Laravelの基本、活用、拡張、テスト、実践的なアプリケーション構築について包括的に解説した本。Laravelがどんなものか知りたいという目的で読むならよい本。"
---

『Laravelリファレンス』を読んだ。  
このフレームワークがどういったものなのか、より詳しく知りたいのであれば読む価値はある本。
養成読本はLaravelの紹介という感じが強かったが、この本は紹介＋こんな使い方です、という感じ。  
フレームワークやPHPがわからないという初級者ではなく、ある程度わかっている中級者向けの本。
DIなどは初級者じゃわからないんじゃないかな…

![laravel-reference-book](/public/image/20170911/laravel_reference_book.jpg)  

Chapter 01からChapter 05まではとてもよい。
Laravelの概念や、フレームワークがどういう機能をサポートしているかが細かく書いてあった。
Laravelがどういうことができるのかを想像させるに十分な内容だった。  
しかしそれ以降の章がわかりづらかった…。  

Chapter 06ではテストについて扱っているのだが、
テストの例がちょっと悪い。実践的なテストではなくて、テストの説明のために作られたようなクラスとテストのため
テストの意義・意図が伝わりづらい。
もう少し意味のあるテストだったらよかったなぁ。  
また、テストのファンクショナルテストのところで、テストのヘルパーメソッドの説明をしているのだが、
メソッドの名の羅列でしかなかったので、メソッドの引数・戻り値・コード例の記載があったらもっとよかった。

Chapter 07ではセキュリティに関して詳細に説明しているが、セキュリティに関しては他の本で知識があるので自分にとっては別の解説があったほうがありがたかったかも。でもここは大事だからこれはこれであり。

あと全体的に図や画面がなくて文章がメインなので図・画像があればもっとよかったかも。

とはいえ、現在Laravelを使ったアプリケーションの開発をしていて、
手元に置いてまさに「リファレンス」として使っている。  
めっちゃ開発に助かっている。ありがたい。

この本の内容は以下のとおり  

```
Chapter 01 Laravelの概要
Chapter 02 Laravelの基本
Chapter 03 データベース
Chapter 04 フレームワークの機能
Chapter 05 フレームワークの拡張
Chapter 06 テスト
Chapter 07 実践的なアプリケーション構築
Chapter 08 Laravelの実践
```

だいたいLaravelというものがわかってきた。  
Laravelというフレームワークの場合、どういう風に設計するのがベストなのか
掴めたのでこの本を読んでよかったと思う。  
とはいえLaravelは進化のスピードが早い。おそらくこの本の内容も陳腐化しているだろう。
ただ概念・フレームワークの根幹など変わらないところはあるはずなのでそれを知ることができたのはよい。  
あとはガリガリ書いていくぞー！

<a target="_blank"  href="https://www.amazon.co.jp/gp/product/4844339451/ref=as_li_tl?ie=UTF8&camp=247&creative=1211&creativeASIN=4844339451&linkCode=as2&tag=pinekta02-22&linkId=d6d66580d50ea487005397bbbedf5d60"><img border="0" src="//ws-fe.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=JP&ASIN=4844339451&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=pinekta02-22" ></a><img src="//ir-jp.amazon-adsystem.com/e/ir?t=pinekta02-22&l=am2&o=9&a=4844339451" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />
