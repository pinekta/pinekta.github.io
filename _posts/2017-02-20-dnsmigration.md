---
layout: post
title:  "DNSをRoute53に移行した"
date:   2017-02-20 20:53:12 +0900
categories: AWS
description: "
いま使っているドメインである、pinekta.tech のDNSはお名前.comのDNSを使っている。勉強のためにAWS Route53にDNSを移行する。別にお名前.comに不満があるわけではない。DNSは無料で使えている。Route53は無料枠はないようだが、約月額64円と安い。64円ならRoute53にしてみよう。"
---

いま使っているドメインである、`pinekta.tech` のDNSはお名前.comのDNSを使っている。  
勉強のためにAWS Route53にDNSを移行する。  
別にお名前.comに不満があるわけではない。DNSは無料で使えている。  
Route53は無料枠はないようだが、[このサイト](https://www.lancork.net/2014/05/amazon-route53-monthly-cost/)によると月額64円と安い。  
64円ならRoute53にしてみよう。

移行の手順は以下が参考になる。  
[お名前.comからAmazon Route 53へドメインを移管する](http://dev.classmethod.jp/cloud/aws/onamae-to-route53/)  
ドメインの取得したてや、移管したばかり、また期限切れのものはRoute53に移管できないとのこと。

1. Route53にドメインを登録する。
2. 登録したドメインにDNSレコードを追加する
3. お名前.comでドメインのアンロック、プライバシー保護の無効、authorization codeの取得、を行う
4. ここで問題が発生…

## 問題

ドメインを移管しようとしたら、な、なんと！  

<img src="/public/image/20170220/transfer.png" alt="Route53 transfer">

**Route53はTLDが.techのものは対応していなかったんだよ！**  
**な、なんだってー！**

## なぜドメインを移管しようとしたかったのか

それは、本ブログはGitHub Pagesを使っているのだが、独自ドメインを使用した場合にそのままではhttpsで通信できないため、Route53とCloudFrontを利用してhttpsにしたかったからである。  
あと、AWSの勉強も兼ねてである。  
仕方ないのでCloudFlareを使うことにする。  
(後述するがCloudFlareは使わなくてもよいがこの時点で気づいていなかった。)

## CloudFlare

<img src="/public/image/20170220/cloudflare.png" alt="CloudFlare" width="600">

トップページにいくと、メールアドレスとパスワードの入力欄があるので入力すると、ドメインの入力が求められる。  
ドメインを入力すると、DNSレコードの検索がウラで行われている間CloudFlareのサービスについての動画を無条件に見せられる。  
動画が終わったあと、DNSレコードの確認が求められるのでOKを押すと、CloudFlareのネームサーバが表示されるのでそれらをメモしておく  

## Route53

ここまでやって思ったが、そもそも
Route53のネームサーバをお名前.comで指定すればよかったことに気づく。  
CloudFlareに設定したWebSite情報を削除する…
そして、Route53にドメインのレコードを登録し、Route53のNSレコードでお名前.comのネームサーバを更新させる。

## 疎通確認

```
➜  ~ dig blog.pinekta.tech

; <<>> DiG 9.8.3-P1 <<>> blog.pinekta.tech
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 42509
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;blog.pinekta.tech.		IN	A

;; ANSWER SECTION:
blog.pinekta.tech.	300	IN	A	192.30.252.153
blog.pinekta.tech.	300	IN	A	192.30.252.154

;; Query time: 195 msec
;; SERVER: 192.168.0.1#53(192.168.0.1)
;; WHEN: Tue Mar  7 09:08:51 2017
;; MSG SIZE  rcvd: 67
```

名前が解決できるようになった。

ネームサーバもRoute53のものになっている。
```
➜  ~ dig pinekta.tech ns

; <<>> DiG 9.8.3-P1 <<>> pinekta.tech ns
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 21632
;; flags: qr rd ra; QUERY: 1, ANSWER: 4, AUTHORITY: 0, ADDITIONAL: 8

;; QUESTION SECTION:
;pinekta.tech.			IN	NS

;; ANSWER SECTION:
pinekta.tech.		172800	IN	NS	ns-1073.awsdns-06.org.
pinekta.tech.		172800	IN	NS	ns-166.awsdns-20.com.
pinekta.tech.		172800	IN	NS	ns-1988.awsdns-56.co.uk.
pinekta.tech.		172800	IN	NS	ns-826.awsdns-39.net.

;; ADDITIONAL SECTION:
ns-1073.awsdns-06.org.	128965	IN	A	205.251.196.49
ns-1073.awsdns-06.org.	129369	IN	AAAA	2600:9000:5304:3100::1
ns-166.awsdns-20.com.	129046	IN	A	205.251.192.166
ns-166.awsdns-20.com.	129005	IN	AAAA	2600:9000:5300:a600::1
ns-1988.awsdns-56.co.uk. 128801	IN	A	205.251.199.196
ns-1988.awsdns-56.co.uk. 128883	IN	AAAA	2600:9000:5307:c400::1
ns-826.awsdns-39.net.	129907	IN	A	205.251.195.58
ns-826.awsdns-39.net.	132497	IN	AAAA	2600:9000:5303:3a00::1

;; Query time: 63 msec
;; SERVER: 192.168.0.1#53(192.168.0.1)
;; WHEN: Tue Mar  7 09:14:43 2017
;; MSG SIZE  rcvd: 346
```

あとは、CloudFrontを利用してSSLにしないといけない。  
イマドキhttpsじゃないってのはなー。
