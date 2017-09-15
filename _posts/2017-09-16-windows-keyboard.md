---
layout: post
title:  "Windowsマシンのキーボードとキーバインド"
date:   2017-09-16 01:12:45 +0900
categories: keyboard
description: "久しぶりにWindowsで開発しているが普段のキーボードじゃ開発できないのでHHKB Lite2かつキーバインドを変更している。おかげで気持ちよく開発できるかも？"
---

久しぶりにWindowsで開発している。  
開発といっても本気で開発するのではなく、過去に作成したコードを拾い上げるために環境を整えている。

普段はBluetoothの小さいキーボードを接続している。  
ブラウザからキーを入力するだけなのでそれで問題なかったのだが、コードを触るならもっと触りやすいキーボードを使いたい。
キータッチが軽くキーストロークも浅い。  
自分の好みはキータッチが多少ありストロークも深いしっかりしたキーボードじゃないとタイピングしていて気持ち良くないのだ。

以前使っていたHHKB Lite2を引っ張り出してきた。  
WindowsでもHHKB Lite2を使っている。  
このキーボードじゃないとダメだ。
Escキーの位置が近いこのキーボードじゃないとダメなんだ。  

Win用のHHKB Lite2は２個ある。（Mac用のHHKB Lite2は１個。）  
以前は職場と自宅の２環境で使っていたが今はMac用のだけ使っている。

![HHKB Lite2](/public/image/20170916/hhkb_lite2.jpg)  

さっそく打ち込んでいくぞ、と思ったらキーバインドが気に入らない。  
「無変換」は「英字」、「変換」は「Kana」であってほしいのだ。  
そして「半角全角」はCtrlになってほしい。  

これらのキーバインドを変更した。
キーバインドはAutoHotKeyを使って変更している。
AutoHotKeyスクリプトは以下のとおり

```
;
; AutoHotkey Version: 1.x
; Language:       English
; Platform:       Win9x/NT
; Author:         A.N.Other <myemail@nowhere.com>
;
; Script Function:
;	Template script (you can customize this template by editing "ShellNew\Template.ahk" in your Windows folder)
;

#NoEnv  ; Recommended for performance and compatibility with future AutoHotkey releases.
SendMode Input  ; Recommended for new scripts due to its superior speed and reliability.
SetWorkingDir %A_ScriptDir%  ; Ensures a consistent starting directory.

; 無変換を半角全角
vk1Dsc07B::vkF3sc029
; 変換を半角全角
vk1Csc079::vkF3sc029
; 半角全角をCtrl
vkF3sc029::Ctrl
; 右Altを右コントロール
RAlt::Ctrl
; Alt + 4 で Alt + F4
!4::!F4
```

このスクリプトをコンパイルして生成されたexeをスタートアップに登録してマシンを立ち上げたときに実行してもらうようにする。  
あれ、スタートアップってどこだっけ？  
Windows 8.1 だと`C:\Users\keita\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup` だったそういえば。
ここに上記のexeのショートカットリンクを配置して起動時に実行されるようにする。

これでようやく開発できる環境が整った。

<a target="_blank"  href="https://www.amazon.co.jp/gp/product/B00008B61F/ref=as_li_tl?ie=UTF8&camp=247&creative=1211&creativeASIN=B00008B61F&linkCode=as2&tag=pinekta02-22&linkId=4c682052f85c1df1937fc0c04f8114be"><img border="0" src="//ws-fe.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=JP&ASIN=B00008B61F&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=pinekta02-22" ></a><img src="//ir-jp.amazon-adsystem.com/e/ir?t=pinekta02-22&l=am2&o=9&a=B00008B61F" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />
