---
layout: post
title:  "強制的にPHPを勉強するためにやっていたこと"
date:   2017-09-18 19:04:20 +0900
categories: php
description: ""
---

勉強ってやり始めるまでが大変。  
じゃあ強制的に勉強する環境を作ってみよう、と思い立って過去いろいろやってみたことを記す。  

[PHP.netをWebスクレイピングしたものを音声ファイルにしてBGMとする](https://qiita.com/pinekta/items/60d1e5c8462731678a5f)とか、
Chromeで新しいタブを開いたらPHP.netの関数のリファレンスページを開くChrome拡張機能を作ったりとか、
Chromeのプッシュ通知機能を利用して定期的に関数のランダムで通知するChrome拡張機能を作ったりとか、
いろいろやった。  

PHP.netをBGMとしたのはQiitaにもあるので、
今回はその一環で作ったChrome拡張機能について紹介しようと思う。

### newtab-php-functions

新しいタブを開くと、PHP.netの関数のリファレンスページをランダムで開くChrome拡張機能で、
日常的に新しいタブはどんどん開かれるので、PHPの関数を強制的に目にする機会を増やして覚えようという作戦。  
こんな感じ。

![newtab-php-functions](/public/image/20170918/newtab-php-functions.gif)  

こんな感じで新しいタブを開くと次々にPHPの関数が表示される。  
へーこういう関数もあったのかーと思ったりする。

コードは以下に置いてある。  
[newtab-php-functions](https://github.com/pinekta/newtab-php-functions)

コードをちょろっと説明すると、
新しいタブの起動をフックするためにmanifest.jsonの`chrome_url_overrides` に`newtab`の指定をしている。

```json
{
  "manifest_version": 2,
  "name": "New Tab PHP Functions",
  "version": "0.1",
  "description": "When you open new tab, the page what you want to learn is displayed.",
  "incognito": "split",
  "chrome_url_overrides": {
    "newtab": "blank.html"
  }
}
```

でblank.htmlでは

```html
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="utf-8">
    <title>RedirectUrlLists</title>
  </head>
  <body>
      <script src="js/main.js"></script>
  </body>
</html>
```

main.jsを呼び出しているだけ。

```js
document.write('<script src="js/urlList.js"></script>');
document.write('<script src="js/redirect.js"></script>');
```

２つのJavaScriptファイルを読み込んでいる。

```js
var urlList = [
"function.abs",
"function.addslashes",
"function.array",

// 省略

"function.vprintf",
"function.vsprintf"
];
```

配列をここで定義して、

```js
document.location.href = "http://php.net/manual/ja/" + urlList[Math.floor(Math.random () * urlList.length)] + ".php";
```

これだけ。
ランダムにurlListの値を取得し、そのページにリダイレクトさせているだけ。
めっちゃ簡単。

### notify-php-functions

こちらは５分ごとにChromeの通知機能を使ってプッシュ通知を行うという拡張機能。  
作業によってはChromeを使っていないこともあるので、そんなときにも強制的にPHPの関数を目にするようにした。  
こんな感じ。

![notify-php-functions](/public/image/20170918/notify-php-functions.gif)  

拡張機能をONにすると通知が飛んでくる。５分たてば別の関数で通知が飛んでくる。  
通知をクリックすればその関数のページを開く、というようになっている。

コードは以下に置いてある。  
[notify-php-functions](https://github.com/pinekta/notify-php-functions)

これもコードを説明する。  
manifest.jsonで通知を送れるように設定しておく。

```json
{
  "manifest_version": 2,
  "name": "notify-php-functions",
  "version": "0.1",
  "description": "Sometimes the word what you want to learn is displayed.",
  "permissions": [
      "notifications",
      "http://php.net/"
  ],
  "background": {
      "scripts": ["js/background.js"]
  }
}
```

`permissions` で`notifications` を指定することでChromeのプッシュ通知を利用できるようになる。  
あとはphp.netからの情報をスクレイピングするので`http://php.net/` も追加する。  
バックグラウンドで実行するスクリプトは`background`で指定する。  
newtab-php-functionsと同じように対象の関数ページは別ページに定義してありランダムで通知する。
通知部分に関しては以下のとおり。

```js
/**
 * Create Notification
 * @param string functionName
 * @param string title
 * @param string description
 * @param string methodsynopsis
 */
var createNotification = function (functionName, title, description, methodsynopsis) {
    var option = {
        type: "basic",
        title: title,
        message: description + "\r" + methodsynopsis,
        iconUrl: "img/logo.gif"
    };
    var notifications = chrome.notifications;
    notifications.create(title, option, function () {});
    notifications.onClicked.addListener(function (clickedFunctionName) {
        var splits = functionName.split('.');
        var type = splits[0];
        var splitedFunctionName = splits[1].replace(/-/g, '_');
        if (type != 'function') {
            if (type == 'serializable' || type == 'exception') {
                splitedFunctionName = (type.charAt(0).toUpperCase() + type.slice(1)) + '::' + splitedFunctionName;
            } else if (type == "dateinterval") {
                splitedFunctionName = 'DateInterval::' + splitedFunctionName;
            } else if (type == "dateperiod") {
                splitedFunctionName = 'DatePeriod::' + splitedFunctionName;
            } else if (type == "datetime") {
                splitedFunctionName = 'DateTime::' + splitedFunctionName;
            } else if (type == "datetimezone") {
                splitedFunctionName = 'DateTimeZone::' + splitedFunctionName;
            }
        }
        if (clickedFunctionName == splitedFunctionName) {
            window.open("http://php.net/manual/ja/" + functionName + ".php", functionName);
        }
    });
}

/**
 * Notify
 */
var notify = function () {
    var functionName = urlList[Math.floor(Math.random() * urlList.length)];
    $.ajax({
        url: "http://php.net/manual/ja/" + functionName + ".php",
        type: "GET",
        success: function(data) {
            var title = $(data).find('h1').text();
            var description = $(data).find('p.refpurpose').text();
            var methodsynopsis = $(data).find('div.methodsynopsis').text().replace(/[\r\n]/g, "");
            createNotification(functionName, title, description, methodsynopsis);
        },
        error: function() {
            createNotification(functionName, "Error!!!", "Error:", "The URL is invallid.");
        }
    });
};

notify();
var minuteInterval = 5 * (60 * 1000);
var timer = setInterval(notify , minuteInterval);
```

5分に１回notifyメソッドを実行している。そのnotifyメソッドではurlList.jsで定義したページをスクレイピングして関数のタイトルと説明を取得しcreateNotificationメソッドに渡す。そしてcreateNotificationメソッドで`notifications.create`を実行することでプッシュ通知をしている。  

こっちも簡単。

## インストール方法

Chromeのストアには配信していないので、GitHubからcloneしたものを読み込む必要がある。  
![add addon](/public/image/20170918/add-addon.png)
「デベロッパーモード」のチェックボックスをONにすると「パッケージ化されていない拡張機能を読み込む」ボタンが表示されるのでcloneしたリポジトリのディレクトリを指定する。
これで拡張がインストールされる。

## まとめ

やっぱり強制的に勉強できる環境を作るのは大事だね。
これらのChrome拡張や車でphp.netを１ヶ月ほど聴いて勉強したんだけど、
その成果はPHP5技術者認定上級試験にも合格という結果にもあらわれた。  
もちろん↓の黒本はやった。試験勉強本だけどPHPの細かいところまで記載されている良本。

<a target="_blank"  href="https://www.amazon.co.jp/gp/product/4844334670/ref=as_li_tl?ie=UTF8&camp=247&creative=1211&creativeASIN=4844334670&linkCode=as2&tag=pinekta02-22&linkId=d84b29c28d20828dd83f4597a5079fa7"><img border="0" src="//ws-fe.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=JP&ASIN=4844334670&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=pinekta02-22" ></a><img src="//ir-jp.amazon-adsystem.com/e/ir?t=pinekta02-22&l=am2&o=9&a=4844334670" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />
