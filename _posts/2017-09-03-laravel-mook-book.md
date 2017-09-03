---
layout: post
title:  "『Laravelエキスパート養成読本』を読んだ"
date:   2017-09-03 19:54:21 +0900
categories: book
description: "『Laravelエキスパート養成読本』を読んだ。Laravelがどんなものかを知るためにはいい本だが、これを読んでLaravelのエキスパートになれるわけではないことに注意。本の半分がLaravel4なのでちょっと内容が今では古い。"
---

『Laravel養成読本』を読んだ。  
Laravelを俯瞰するための本としてはよいけれど、
これを参考にしてプロダクトが作れるかというとそこまでLaravelの機能について深く説明はしていないので
実際にLaravelを使ったアプリケーションを作るときはLaravelの公式のドキュメントを読み込む必要がある。  

![laravel-mook-book](/public/image/20170903/laravel_mook_book.jpg)  

出版が2016年と古いこともあり、内容の半分がLaravel4で説明されていて
バージョン5系と4系はディレクトリ構造など違うため参考にならない箇所が多い。
Laravelの雰囲気を感じる程度としては役に立つだろうが…
2017年9月現在ではLaravel5.5まで進んでおりいまさらLaravel4の内容はちょっと役に立たないな。  

この本の見所はChapter 3とChapter 4。  
Chapter 3のLaravelの根幹の概念である、ファサード・IoCコンテナについての説明が非常に為になった。  
最初IoCコンテナって何ぞ？と思っていたが何のことはないただのDIコンテナだった。
同じものを別の言葉が当てられていて非常に紛らわしい。  
ファサードもデザインパターンのファサードと厳密に意味が違う気がするので、
Laravelは概念の名前づけがヘタクソなような気がする。

Chapter 4ではLaravel5の新機能を紹介しており、Laravel4と比べてどう違ったか、
Laravel4からLaravel5に移行するときにどのようなことに気をつけたらいいか書いてある。  

この本の内容は以下のとおり  

```
Chapter 1 Laravelをはじえよう - PHPでの開発が楽しくなる -
Chapter 2 MVCモデルが基礎からわかる - Laravelで作るWebアプリケーション
Chapter 3 IoCコンテナ、ファサード、サービスプロバイダ、Eloquent - Laravelをより理解するために -
Chapter 4 Laravel5の新機能を紹介 - 開発効率アップのエッセンス - 
Chapter 5 実践！REST APIアプリケーション - 手を動かして学ぼう！ -
```

現在ではちょっと内容が古くなってしまったとはいえ、
この本はLaravelを始める前にLaravelはどういうものなのかを知るのにはいい本だと思う。

<a target="_blank"  href="https://www.amazon.co.jp/gp/product/4774173134/ref=as_li_tl?ie=UTF8&camp=247&creative=1211&creativeASIN=4774173134&linkCode=as2&tag=pinekta02-22&linkId=c664be7ef7df143e3c519ff6f50a6032"><img border="0" src="//ws-fe.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=JP&ASIN=4774173134&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=pinekta02-22" ></a><img src="//ir-jp.amazon-adsystem.com/e/ir?t=pinekta02-22&l=am2&o=9&a=4774173134" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />
