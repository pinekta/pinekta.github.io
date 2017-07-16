---
layout: post
title:  "『初めてのAnsible』を読んだ"
date:   2017-07-14 09:43:12 +0900
categories: book
description: "オライリーの『初めてのAnsible』を読んだ。内容はとてもわかりやすく、どうAnsibleを使ったらいいのか実践形式で簡単なPlaybookの実行から複雑なPlaybookの実行をとおして教えてくれる。ただ全体的に内容が薄くAnsibleについて知識がある人は読んでも得るものは少ないかもしれない。"
---

オライリーの『初めてのAnsible』を読んだ。
原題は『Ansible: Up and Running』。  
「初めて」はどこから来たのか…。まぁ初心者をターゲットにすると売れるからなぁ。
先日の『Infrastructure as Code』に引き続きインフラ本２つ目。
最近のオライリーのインフラ本は青いね。Docker本も青いし。
てか最近本しか読んでねぇな。オライリーの書評ブログになってるなぁ…子守しながらだと本しか読めない…

![ansible-book](/public/image/20170714/ansible-book.jpg)

本書はタイトルに「初めて」と冠してあるとおり、内容はとてもわかりやすい。  
どうAnsibleを使ったらいいのか実践形式で簡単なPlaybookの実行から複雑なPlaybookの実行をとおして教えてくれる。
また、カスタムモジュールの作り方も記載されてあるので、もしモジュールがない場合はここを読むと役に立ちそう。

実践形式であるが故にAnsibleの細部のモジュールまでの詳細な説明はない。そこは公式のドキュメントで補う必要がありそうだ。
とはいえ、イチからPlaybookを作るよりはAnsible GalaxyからPlaybookを取得してそれを参考にしてカスタマイズしていけばいいと思っているのでそこは気にしなくてもよいかな。

VagrantやEC2、Dockerへのプロビジョニングについても詳しく言及していて業務で使うヒントになった。
また、Ansibleには関係ないけどDjangoのアプリケーションをプロビジョニング・デプロイするという項目があり、
Djangoの勉強にもなった。

本の内容は以下のとおり。  
```
第1章 イントロダクション
第2章 Playbook: 始めてみよう
第3章 インベントリ: サーバーの記述
第4章 変数とファクト
第5章 Mezzanine の紹介: 本書でのテスト用アプリケーション
第6章 Ansible によるMezzanine のデプロイ
第7章 複雑なPlaybook
第8章 ロール: プレイブックのスケールアップ
第9章 Ansible の高速化
第10章 カスタムモジュール
第11章 Vagrant
第12章 Amazon EC2
第13章 Docker
第14章 Playbook のデバッグ
付録A SSH
付録B デフォルトの設定
付録C EC2クレデンシャルのためのIAMロールの利用
付録D Ansible を利用したプロビジョニング方法
付録E Ansible 2.0
付録F 用語集
付録G 参考文献
```

「初めて」とあるとおり、Ansibleを知らない人が読むと概要がほどよくつかめる本ではあるが、
知っているが読むとあまりAnsibleについての発見は多くはなさそう。
できればAnsibleの各モジュールについての説明・使い方などが載っているとよかった。が、そこは公式マニュアルで保管はできるのでいいのかもしれない。

Ansibleは冪等性を全面的に謳っているが、commandやscriptモジュールを利用した場合は冪等にならないし、
独自のモジュールを開発した際も冪等になるように作成しなければいけない。
つまり、コマンドやシェルスクリプト・独自モジュールなど複雑なプロビジョニングをする際は自前で冪等に実装しなければいけないので、そこはAnsibleの冪等性の落とし穴だと思う。

ただAnsibleはとてもよいツールで自分も前々からウォッチしたり自分でも使っているので、
少しずつ業務にもAnsibleを導入していきたい。

<a target="_blank"  href="https://www.amazon.co.jp/gp/product/4873117658/ref=as_li_tl?ie=UTF8&camp=247&creative=1211&creativeASIN=4873117658&linkCode=as2&tag=pinekta02-22&linkId=ba6928b45c8edfdf3fcad97239c9d0ca"><img border="0" src="//ws-fe.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=JP&ASIN=4873117658&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=pinekta02-22" ></a><img src="//ir-jp.amazon-adsystem.com/e/ir?t=pinekta02-22&l=am2&o=9&a=4873117658" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />
