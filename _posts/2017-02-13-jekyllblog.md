---
layout: post
title:  "GitHub PagesにJekyllを使ってブログサイトを作る"
date:   2017-02-13 13:55:31 +0900
categories: jekyll update
---

## GitHub Pagesで静的なサイトを立てる

まずは、GitHub Pagesを使えるようにするには、
自分のGitHubアカウントに
[ユーザ名].github.io
というリポジトリを作成します。
そして、そのリポジトリのmasterブランチに適当なHTMLファイル、
例えばindex.htmlをプッシュすると、

https://[ユーザ名]/
でアクセスすると、プッシュしたHTMLファイルが表示されます。

とても簡単ですね。

## Jekyll で簡単にページを作成する

ただ、これだけですと、
自分でHTML、CSSを組まなければいけないので大変です。
そして、記事が増えた場合の管理など大変です。

それを、簡単にしてくれるのが「Jekyll」です。
JekyllはMarkdownをHTMLに変換するツールです。
エンジニアにとっては馴染みがあるMarkdownでサイトは作れるのは非常に楽ですね。

### Jekyll のインストール

```
sudo gem install jekyll
sudo gem install bundler
```

```
rm -f [ユーザ名].github.io/index.html
jekyll new --force [ユーザ名].github.io
```

```
cd [ユーザ名].github.io
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

```
jekyll serve
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

http://127.0.0.1:4000/
にアクセスすると、Jekyllが生成したページにアクセスすることができます。

![Jekyll デフォルトのページ]

Jekyllのプロジェクトディレクトリ（[ユーザ名].github.io）に
存在するマークダウンファイルがindex.htmlになります。

JekyllのプロジェクトディレクトリにMarkdownファイルを配置すれば、
自動でHTMLに変換されるかと思ったんですが、違うようです。

HTMLに変換するには、Markdownで書いた拡張子mdのファイルの内容の一番最初に以下を追加してください。

```
---
layout: page
title: GitHub PagesにJekyllを使ってブログサイトを作る
permalink: /jekyll/
---
```

layoutはページのレイアウトは何にするか、
titleはページのタイトル
permalinkはページのURLをそれぞれ指定できます。
保存すると、Jekyllが変更をwatchしているので、
すぐに反映されます。

http://127.0.0.1:4000/jekyll/
にアクセスすると、ページが表示されます。
楽ですね。

### Jekyll のカスタマイズ

タイトルが
「Your awesome title」になっているので変更しましょう。

_config.ymlに各種設定があるので以下のように編集します。
```_config.yml
title: To the backbone
email: h03a081b@gmail.com
description: > # this means to ignore newlines until "baseurl:"
  Webエンジニアpinektaの技術的なものからそうでないものまでを書く
baseurl: "" # the subpath of your site, e.g. /blog
url: "" # the base hostname & protocol for your site, e.g. http://example.com
twitter_username: pinekta
github_username:  pinekta
```

_config.ymlですが、こちらは変更をwatchして自動で反映とはならないようです。
```
jekyll serve
```
で設定をリロードさせる必要があります。

テーマを別のものに変更したかったので、
以下のリポジトリのテーマをcloneしたものを[ユーザ名].github.ioのディレクトリにかぶせて再度
jekyll serverしたところ、以下のエラーに遭遇

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

ググってみると、_config.ymlに記述を追加すればいい模様。
https://github.com/jekyll/jekyll/issues/4124
```
# Gems
gems: [jekyll-paginate]
```

を追加して再度jekyll serveしたところ下記のエラーに
```
➜  pinekta.github.io git:(master) ✗ jekyll serve
Configuration file: /Users/keita/Documents/gitProjects/pinekta.github.io/_config.yml
Configuration file: /Users/keita/Documents/gitProjects/pinekta.github.io/_config.yml
  Dependency Error: Yikes! It looks like you don't have jekyll-paginate or one of its dependencies installed. In order to use Jekyll as currently configured, you'll need to install this gem. The full error message from Ruby is: 'cannot load such file -- jekyll-paginate' If you run into trouble, you can find helpful resources at https://jekyllrb.com/help/!
jekyll 3.4.0 | Error:  jekyll-paginate
```

Gemfileを
```
gem "jekyll", "3.4.0"
```

を下記に変更
```
gem "jekyll"
gem "jekyll-paginate"
```

気を取り直して、
jekyll serve するとまた下記のエラーが。
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

https://github.com/poole/poole/issues/99
によると、permalinkの設定が変わった模様。
_config.ymlの下記をコメントアウトする。
```
#relative_permalinks: true      # comment out
```

たぶん、テーマの_config.ymlで書き換えたのがいけなかった模様
再度、jekyll serveすると

![]
というように新しいテーマで表示されました。

これでブログを書いていきます！

https://pages.github.com/

上記にアクセスしたところ、真っ白なページが表示された。
index.mdは不要のこと。
すでにあるjekyllディレトリにテーマのディレクトリをcpで被せたからこうなった様子。
index.mdを消して再度デプロイしなおしたら表示されるようになった。



## 複数GitHub Pagesを使いたい場合は？

[アカウント名].github.io というリポジトリを作ってしまったら、
同じリポジトリを作れないので、GitHub Pagesは一つしか作れない、というわけでもありません。

リポジトリに「gh-pages」というブランチ名でプッシュすれば、
それがGitHub Pagesとなります。


