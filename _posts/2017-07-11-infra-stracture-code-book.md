---
layout: post
title:  "『Infrastructure as Code』を読んだ"
date:   2017-07-11 09:40:34 +0900
categories: book
description: "オライリーの『Infrastructure as Code』を読んだ。技術的な要素についてはインフラ界隈をウォッチしていればなんてことはないけれど、チームにどうしたらInfurastructure as Codeを根付かせることができるか、というプラクティスは非常に示唆に富んでいるよい本である。"
---

オライリーの『Infrastructure as Code』を読んだ。
説明している技術的な要素についてはインフラ界隈をウォッチしていればなんてことはない内容だと思う。
この本の内容を簡潔に説明すると、
* デプロイパイプラインを整備せよ
* そのためにテストを書け

という内容に尽きる気がする。

上述したなんてことはないというのはInfrastructure as Codeを構成するもの、たとえばAWSなどのクラウド、Ansibleなどのプロビジョニングツール、Dockerなどのコンテナ、このあたりの情報はなんてことはないものだったけれど、Infrastructure as Codeを実現させるための考え方については非常にためになった。

![infrastructure-as-code](/public/image/20170711/infrastructure_as_code_book.jpg)

システムはバグがつきものだし完璧な設計など存在せずフェーズによって設計は変化・進化していくものなので、
バグの修正やシステムの変更を手早くリリースするためにデプロイパイプラインを整備する。  
そうすれば変化の激しい昨今の流れについていくことができる。  
手作業でサーバーの設定を変更するようなことは、結果的にはバグを埋め込みユーザーへの価値提供が遅くなる。
その結果、変化のペースについていけなくなってしまう。  
デプロイパイプラインを整える、ということは継続的に安全・簡単に低コストで変更を加えることができる土台を用意することを意味する。
つまり、Infrastructure as Codeは競争力の原動力となる。

Infrastructure as Code を実践していくには条件があって、
組織的な観点からの条件と、システムの設計・構造からの条件とに分けられる。  
まず組織的な面から説明すると、
中央集権的な開発体制や職能分割された組織だと、システム全体にわたる権限がないために
Infrastructure as Code が根付かない。
近年のDevOpsでのチーム体制でこそInfrastructure as Codeは真価を発揮する。  
本書で説明してある言葉を借りると
```
「構築するのも運用するのも同じチーム」。「You build it, You run it.」
```
の場合、Infrastructure as Code をチームに根付かせることができる。

システムの設計・構造からの面からだと、
Infrastructure as Code はTDDやXPといったプラクティスと非常に親和性があるので、
それらのプラクティスに則って実践していくとよい。  
また、モノリシックなアーキテクチャーではデプロイパイプラインに限界がくるので、
分割してマイクロサービスにすることで、デプロイパイプラインを疎結合にしInfrastructure as Codeをより深化させることができる。
また、継続的にデプロイするために、本番環境へのデプロイを止めてしまうことはよくないので、
機能が完了していなくとも「機能トグル」といった形でどんどんデプロイするべき、としている。

本の内容は以下のとおり。  
```
第I部 基礎
  第1章 課題と原則
  第2章 ダイナミックインフラストラクチャプラットフォーム
  第3章 インフラストラクチャ定義ツール
  第4章 サーバー構成ツール
  第5章 主要なインフラストラクチャサービス
第Ⅱ部 パターン
  第6章 サーバーのプロビジョニングのパターン
  第7章 サーバーテンプレート管理のパターン
  第8章 サーバーのアップデート/変更のパターン
  第9章 インフラストラクチャ定義のパターン
第Ⅲ部プラクティス
  第10章 インフラストラクチャのためのソフトウェア工学プラクティス
  第11章 インフラストラクチャの変更のテスト
  第12章 インフラストラクチャの変更管理パイプライン
  第13章 インフラストラクチャチームのワークフロー
  第14章 継続性とダイナミックインフラストラクチャ
  第15章 Infrastructure as Code のための組織
```

技術的な要素についてはとりわけすごいものはないけれど、
Infrastructure as Codeをチームで使うようにするにはどうしたらよいか、という示唆に非常に富んでいる本である。
よい本だった。  
今のチームではAMIのテンプレート作成は手作業でやっているので
まずはPackerを使ってテンプレートを作成できないか検討してみようかな。

<a target="_blank"  href="https://www.amazon.co.jp/gp/product/4873117968/ref=as_li_tl?ie=UTF8&camp=247&creative=1211&creativeASIN=4873117968&linkCode=as2&tag=pinekta02-22&linkId=cf3acdda65ee867883450630cf8bd6be"><img border="0" src="//ws-fe.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=JP&ASIN=4873117968&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=pinekta02-22" ></a><img src="//ir-jp.amazon-adsystem.com/e/ir?t=pinekta02-22&l=am2&o=9&a=4873117968" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />
