---
layout: post
title:  "Route53とCloudFrontで独自ドメインのGitHub PagesをHTTPS化した"
date:   2017-02-21 23:10:42 +0900
categories: AWS
description: "タイトルのとおりHTTPS化した。さすがにいまどきのページでHTTPSにしてないページはどうかと思う。Let's Encryptなどの無料でSSL証明書を取得できるサービスも出てきたのに、平文でやりとりするのはよくない。今回はCloudFrontを利用するので、SSL証明書をAmazon Certificate Manager(ACM)で無料で利用できる。しかも更新は自動だ！"
---

タイトルのとおりHTTPS化した。  
さすがにいまどきのページでHTTPSにしてないページはどうかと思う。  
[Let's Encrypt](https://letsencrypt.org/) などの無料でSSL証明書を取得できるサービスも出てきたのに、平文でやりとりするのはよくない。

今回はCloudFrontを利用するので、SSL証明書をAmazon Certificate Manager(ACM)で **無料で利用できる。**  
しかも **更新は自動だ！**  

今回の作業するにあたって以下の記事が参考になった。  
[Github Pagesでホスティングしつつ、CloudFrontを使ってサイトをSSL対応の独自ドメインにする](http://qiita.com/kechol/items/9609e1ab4a673e05b613)

しかし、ここで問題が発生。  

## 問題

ACMはドメイン認証の証明書を発行するのだが、ドメイン認証をするためのドメインでメールを受信できる必要があるとのこと。  
つまり、`pinekta.tech`ドメインでメールを受信できるよう、メールサーバを立てなければならない…
おぉ、めんどくせー。  
仕方ないのでEC2のインスタンスにメールサーバを構築する。

ついでに証明書の更新がエラーになっていたLet's Encryptも確認する。

## Let's Encryptの更新

Let' Encryptは簡単にSSL証明書の更新ができる。  
コマンドを実行して更新をトライしたところ  
```
./certbot-auto renew --force-renew  && service httpd reload
Error: couldn't get currently installed version for /root/.local/share/letsencrypt/bin/letsencrypt:
Traceback (most recent call last):
  File "/root/.local/share/letsencrypt/bin/letsencrypt", line 7, in <module>
    from certbot.main import main
  File "/root/.local/share/letsencrypt/local/lib/python2.7/dist-packages/certbot/main.py", line 11, in <module>
    import zope.component
  File "/root/.local/share/letsencrypt/local/lib/python2.7/dist-packages/zope/component/__init__.py", line 16, in <module>
    from zope.interface import Interface
ImportError: No module named interface
```

エラー…

以下のページを参考にして解決。  
[Amazon Linux 上の Let’s Encrypt で証明書更新エラーが出た時の対処方法](https://blog.yskw.info/articles/326/)

## メールサーバの構築

おなじみの(自分にとっては)PostfixとDovecotを入れます。
```
# yum -y install postfix dovecot
```

基本的には以下の記事と同じように設定します。

[Amazon Linux on EC2にPostfix+Dovecotでメールサーバー構築](http://qiita.com/shohohoh/items/05b0a3a5d6e6df8f34a8)

設定したのち、テストでメールを送信するも送信がうまく行かない…  
EC2インスタンスのセキュリティグループで22と80と443しか開けていないことを思い出し、セキュリティグループを変更してポートを開ける。  
SMTP, SMTPS, POP3, POP3S, IMTP, IMTPSといったこれらのポートを開けておく。

そしてACMの画面から申請すると、構築したメールサーバにメールが配信されるので、メールクライアントでメールを受信し、AmazonからのACMの認証のリンクを実行し、証明書を有効化する。

ただ、ACMから配信されるメールアドレスはAWSが以下のようなアドレスを決め打ちで送信する。
* administrator@your_domain
* admin@your_domain
* hostmaster@your_domain
* postmaster@your_domain
* webmaster@your_domain

メールのエイリアス設定を変更して、pinektaユーザで受信できるよう変更。

```
# vim /etc/aliases

-----------

postmaster:     pinekta
```
上記、rootからpinektaに変更し、
```
# newaliases
```
で反映して、`pinekta@pinekta.tech` のメールアドレスで `postmaster@pinekta.tech` 宛てのメールを受信できるようにした。

以下のメールが届いたので、URLをクリックして証明書を有効化する。

![ACMのメール](/public/image/20170221/acm_mail.png)
![ACM](/public/image/20170221/acm.png)

## CloudFrontの設定

HTTPSで配信したいため、ACMで証明書を取得する。  
よくある下記の罠に注意！  
**CloudFrontでACMの証明書を使う場合、リージョンはアメリカバージニア北部(us-east-1)で証明書を作成すること**

CloudFrontのディストリビューションを作成し、ドメインを指定しACMで作成した証明書を選択する。そしてOKを押していくとCloudFrontにデータが追加される。  
注意するのは、CloudFrontのOriginal Domainは[ユーザ名].github.ioを指定すること。  

結果的に以下の値で作成。

ディストリビューションの設定
![ディストリビューションの設定1](/public/image/20170221/cf_distribution1.png)
![ディストリビューションの設定2](/public/image/20170221/cf_distribution2.png)

Originの設定
![originの設定](/public/image/20170221/cf_origin.png)

Behaviorの設定
![Behaviorの設定1](/public/image/20170221/cf_behavior1.png)
![Behaviorの設定2](/public/image/20170221/cf_behavior2.png)

## Route53の設定

Route53に設定したblog.pinekta.techのAレコードはGitHub PagesのIPを指定していたが、作成したCloudFrontのDomain NameをAレコードのAliasとして更新する。

![route53の設定](/public/image/20170221/route53.png)

## CNAMEファイルの削除

あと、GitHub PagesのCNAMEファイルを削除すること。  
プロジェクトディレクトリ直下にあるCNAMEファイルを削除し、commitしてpush。

# HTTPS化

`http://blog.pinekta.tech` にアクセスすると  

![https1](/public/image/20170221/https1.png)
![https2](/public/image/20170221/https2.png)

やった！  
httpsにリダイレクトされているし、証明書も問題ない。  

これで普通にblogを運用できる環境になったかな。
