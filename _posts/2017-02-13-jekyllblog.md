---
layout: post
title:  "GitHub PagesにJekyllを使ってブログサイトを作る"
date:   2017-02-13 13:55:31 +0900
categories: jekyll update
description: "GitHub PagesにJekyllを使ってブログサイトを作りました。けっこう簡単に作れるのでおすすめ"
---

## GitHub Pagesで静的なサイトを立てる

まずは、GitHub Pagesを使えるようにするには、
自分のGitHubアカウントに
`[ユーザ名].github.io`
というリポジトリを作成します。  
そして、そのリポジトリのmasterブランチに適当なHTMLファイル、
例えばindex.htmlをプッシュすると、

`https://[ユーザ名].github.io/`  
でアクセスすると、プッシュしたHTMLファイルが表示されます。

とても簡単。
ただ、これだけだと自分でHTML, CSSを組まなければいけないので大変。
記事が増えたときの管理も面倒。

## Jekyll で簡単にページを作成する

そこで「Jekyll」の出番です。  
JekyllはMarkdownをHTMLに変換するツールです。  
エンジニアにとっては馴染みがあるMarkdownでサイトは作れるのは非常に楽です。

[Jekyll](https://jekyllrb.com/)

![Jekyll](/public/image/20170213/jekyll.png)

### Jekyll のインストール


以下の手順でインストールします。  
なお、環境はMac OS Sierra 10.12.3 で行なっています。

１．Jekyll, Bundlerをインストール
```
$ sudo gem install jekyll
$ sudo gem install bundler
```

２．不要なファイルを削除しJekyllプロジェクトのひながたを作成
```
$ rm -f [ユーザ名].github.io/index.html
$ jekyll new --force [ユーザ名].github.io
```

３．確認
```
$ cd [ユーザ名].github.io
➜  pinekta.github.io git:(master) ✗ ls -l
total 56
-rw-r--r--  1 keita  staff   953  2 11 13:55 Gemfile
-rw-r--r--  1 keita  staff  1180  2 11 13:55 Gemfile.lock
-rw-r--r--  1 keita  staff  1402  2 11 13:55 _config.yml
drwxr-xr-x  3 keita  staff   102  2 11 13:55 _posts
-rw-r--r--  1 keita  staff   525  2 11 13:55 about.md
-rw-r--r--  1 keita  staff  1231  2 11 13:57 github_pages.md
-rw-r--r--  1 keita  staff    12  2 11 12:23 index.html
-rw-r--r--  1 keita  staff   213  2 11 13:55 index.md
```

４．Jekyllを起動
```
$ jekyll serve
Configuration file: /Users/keita/Documents/gitProjects/pinekta.github.io/_config.yml
Configuration file: /Users/keita/Documents/gitProjects/pinekta.github.io/_config.yml
            Source: /Users/keita/Documents/gitProjects/pinekta.github.io
       Destination: /Users/keita/Documents/gitProjects/pinekta.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 0.57 seconds.
 Auto-regeneration: enabled for '/Users/keita/Documents/gitProjects/pinekta.github.io'
Configuration file: /Users/keita/Documents/gitProjects/pinekta.github.io/_config.yml
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
      Regenerating: 1 file(s) changed at 2017-02-11 14:05:07 ...done in 0.195867 seconds.
```

`Server address: http://127.0.0.1:4000/` にあるとおり、
http://127.0.0.1:4000/ にアクセスすると、Jekyllが生成したページにアクセスすることができます。

![Jekyll default1](/public/image/20170213/jekyll_default1.png)
以下は記事のページです。
![Jekyll default2](/public/image/20170213/jekyll_default2.png)
以下はaboutリンクのページです。
![Jekyll default3](/public/image/20170213/jekyll_default3.png)

シンプルだけれどもよいデザインです。
そのまま使えそうです。

### 記事の追加

記事を追加するには`_posts` ディレクトリにマークダウンファイルを追加します。
```
$ vim _posts/2017-02-16-test.md
```

以下の内容を記載します。
```
---
layout: post
title:  "test"
date:   2017-02-16 09:32:34 +0900
categories: test
---
I do test.
```

すると、トップページに記事が追加されます。

![post1](/public/image/20170213/post1.png)
以下は記事のページです。
![post2](/public/image/20170213/post2.png)

記事のファイル名は
`YYYY-mm-dd-適当な値.md` である必要があります。  
このようにしないとJekyllがうまくファイルを認識してくれません。

また、記事の内容の頭に、記事のレイアウトやタイトル、日付などを記載しなくてはなりません。  
これを正しく記載していないとうまく表示されない可能性があります。

### Jekyll のカスタマイズ

次にタイトルを編集します。

`_config.yml`に各種設定があるので編集します。
```
title: To the backbone
email: h03a081b@gmail.com
description: > # this means to ignore newlines until "baseurl:"
  pinektaのブログ
baseurl: "" # the subpath of your site, e.g. /blog
url: "" # the base hostname & protocol for your site, e.g. http://example.com
twitter_username: pinekta
github_username:  pinekta
```

変更したら再度Jekyllを再起動します。
```
$ jekyll serve
```

これでタイトルなどといったサイト情報の編集ができました。

## テーマの変更

デフォルトのテーマでも十分使えそうだけれども、
もう少しシンプルなテーマを使いたかったので  
[Lanyon](http://lanyon.getpoole.com/) というテーマを使うことにした。

横着して、Lanyonをローカルにcloneしたものをそのままコピーして被せて、
`jekyll serve` したところ、エラーになる。

```
➜  pinekta.github.io git:(master) ✗ jekyll serve
Configuration file: /Users/keita/Documents/gitProjects/pinekta.github.io/_config.yml
Configuration file: /Users/keita/Documents/gitProjects/pinekta.github.io/_config.yml
       Deprecation: You appear to have pagination turned on, but you haven't included the `jekyll-paginate` gem. Ensure you have `gems: [jekyll-paginate]` in your configuration file.
            Source: /Users/keita/Documents/gitProjects/pinekta.github.io
       Destination: /Users/keita/Documents/gitProjects/pinekta.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
Since v3.0, permalinks for pages in subfolders must be relative to the site source directory, not the parent directory. Check https://jekyllrb.com/docs/upgrading/ for more info.
```

ググってみると、GitHubの[Jekyllのイシュー](https://github.com/jekyll/jekyll/issues/4124) に _config.ymlに記述を追加すればいいとあったので、

```
# Gems
gems: [jekyll-paginate]
```

を追加して再度jekyll serveしたところ下記のエラーに...
```
➜  pinekta.github.io git:(master) ✗ jekyll serve
Configuration file: /Users/keita/Documents/gitProjects/pinekta.github.io/_config.yml
Configuration file: /Users/keita/Documents/gitProjects/pinekta.github.io/_config.yml
  Dependency Error: Yikes! It looks like you don't have jekyll-paginate or one of its dependencies installed. In order to use Jekyll as currently configured, you'll need to install this gem. The full error message from Ruby is: 'cannot load such file -- jekyll-paginate' If you run into trouble, you can find helpful resources at https://jekyllrb.com/help/!
jekyll 3.4.0 | Error:  jekyll-paginate
```

そのため、 Gemfileの
```
gem "jekyll", "3.4.0"
```

を下記に変更した。
```
gem "jekyll"
gem "jekyll-paginate"
```

気を取り直して、jekyll serve するとまた下記のエラーが...
```
➜  pinekta.github.io git:(master) ✗ jekyll serve
Configuration file: /Users/keita/Documents/gitProjects/pinekta.github.io/_config.yml
Configuration file: /Users/keita/Documents/gitProjects/pinekta.github.io/_config.yml
            Source: /Users/keita/Documents/gitProjects/pinekta.github.io
       Destination: /Users/keita/Documents/gitProjects/pinekta.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
Since v3.0, permalinks for pages in subfolders must be relative to the site source directory, not the parent directory. Check https://jekyllrb.com/docs/upgrading/ for more info.
```

[GitHubのイシュー](https://github.com/poole/poole/issues/99) によると
permalinkの設定が変わった模様。  
_config.ymlの下記をコメントアウトする。
```
#relative_permalinks: true      # comment out
```

再度、jekyll serveすると

![laynon](/public/image/20170213/laynon.png)
というように新しいテーマで無事表示される。

最終的には、
* ヘッダのハンバーガーメニューとサブタイトルの削除、フッタの追加, aboutページの削除
`_layout/default.html` を修正
* トップページの記事を20語以降は「続きを読む」リンクを表示する
`index.html` を修正 ex.[Liquid truncatewords](http://shopify.github.io/liquid/filters/truncatewords/)

## 複数GitHub Pagesを使いたい場合

[アカウント名].github.io というリポジトリを作ってしまったら、
同じリポジトリを作れないので、GitHub Pagesは一つしか作れない？  
実はそうではない。

リポジトリに「gh-pages」というブランチ名でプッシュすれば、
それがGitHub Pagesとなる。

OSSのGitHub Pagesはこっちのほうが多い思う。

## 独自ドメインにする

GitHub Pagesで作ったサイトを独自ドメインにする場合は、
プロジェクトルートにCNAMEというファイルに設定したドメインを記載するだけです。

つまりこのブログの場合は
```
$ echo blog.pinekta.tech > CNAME
```

そして、設定したいドメイン（blog.pinekta.tech）のAレコードがGitHub PagesのIPにすればOKです。
[GitHub のこのページ](https://help.github.com/articles/setting-up-an-apex-domain/) に書かれているとおり、
```
192.30.252.153
192.30.252.154
```
をIPにしたAレコードをお使いのDNSサーバに設定してください。

ただ、これだけだとHTTPSで使用することはできない。  
`[ユーザ名].github.io` だとHTTPSを使えたが、独自ドメインにすると使えない模様。  
[CloudFlare](https://www.cloudflare.com/) を利用するとできるらしいが、また今度。

## まとめ

Jekyll on GitHub Pages で簡単にブログができる。
