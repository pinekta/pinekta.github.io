---
layout: post
title:  "『実践Node.jsプログラミング』を読んだ"
date:   2017-02-14 19:59:30 +0900
categories: Node.js book
description: "『実践Node.jsプログラミング』という本を読んだ。非常にいい本だった。Node.jsの本ならおそらくこの本が一番ではないだろうか。クライアントJavaScriptは書き慣れていたので、Node.jsも簡単だと思っていたが 実際やってみるとそうではなかった。そのためにこの本を読んでみたのだが、非常にためになった。"
---

『実践Node.jsプログラミング』という本を読んだ。  
非常にいい本だった。  
Node.jsの本ならおそらくこの本が一番ではないだろうか。  

<img src="/public/image/20170214/nodejs_book.jpg" alt="nodejs_book" width="300"/>

今までNode.jsをちょくちょく触ることはあったが、  
本格的に使用したことはなかった。

クライアントJavaScriptは書き慣れていたので、  
Node.jsも簡単だと思っていたが、
実際やってみるとそうではなかった。  
そのためにこの本を読んでみたのだが、  
非常にためになった。  

JavaScriptの初心者には厳しいが、クライアントJavaScriptは書き慣れている  
かつNode.jsで書いた事がなくてこれから書く・勉強したいという人にぜひ読んでもらいたい本である。  

本の内容は以下のとおり。  

```
第Ⅰ部 Nodeの基礎知識  
  第１章 Node.jsに、ようこそ！  
  第２章 マルチルーム・チャットアプリの構築  
  第３章 Nodeプログラミングの基礎知識  
第Ⅱ部 NodeでWebアプリケーションを開発する  
  第４章 Webアプリケーションの構築  
  第５章 アプリケーションのデータをストアする  
  第６章 Connect  
  第７章 Connectの組み込みミドルウェア  
  第８章 Express  
  第９章 Expressの高度な使い方  
  第１０章 Nodeアプリケーションをテストする  
  第１１章 Webアプリケーションでテンプレートを使う  
第Ⅲ部 NodeでWebアプリケーションを開発する  
  第１２章 Nodeアプリケーションのデプロイと可用性  
  第１３章 WebサーバばかりがNodeではない  
  第１４章 Nodeのエコシステム  
```

Node.jsの流儀を知らない人は、第３章を読むとよい。  
プログラムの分割や分割されたモジュールの読み込みの仕方、  
非同期で実行されるNode.jsで同期的に実行するやり方など、  
Node.jsのハマりどころについて詳細に解説されている。

また、Node.jsのフレームワークであるExpressの詳細な説明がある。  
Expressが利用するConnectの詳細な説明もあるので、Expressを勉強にもなる。  

この本はExpressを使ったWebアプリケーション作成について多くの紙面を割いているが、  
個人的には第１３章も面白いと思う。  
Node.jsはWebアプリケーションだけではないということをこの章が示している。  

Socket.ioでのリアルタイムでのやりとりが可能であることや、簡単にTCPのサーバ・クライアントが書けるということが記載されている。  

Node.jsはJavaScriptなので非常にとっつきやすい言語かと思ったが、実際はそうではなくクセが強いが、  
ローレベルなものからリアルタイムアプリケーションまで作れる、とても面白いものだと思う。  
何かNode.jsで作りたくなった。  

<a target="_blank"  href="https://www.amazon.co.jp/gp/product/479812947X/ref=as_li_tl?ie=UTF8&camp=247&creative=1211&creativeASIN=479812947X&linkCode=as2&tag=pinekta02-22&linkId=d8aab24a58166cd1dc5b14183a48d751"><img border="0" src="//ws-fe.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=JP&ASIN=479812947X&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=pinekta02-22" ></a><img src="//ir-jp.amazon-adsystem.com/e/ir?t=pinekta02-22&l=am2&o=9&a=479812947X" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />
