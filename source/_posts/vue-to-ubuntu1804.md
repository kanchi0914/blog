---
title: Ubuntu18.04でVue-cliでvue createする際Missing required argumentが出る件の解決メモ
date: 2020-07-11 23:12:52
tags: ubuntu Vue.js 
---

最近自宅のPCにZorin OSというUbuntuベースのLinuxディストリビューションを入れて遊んでいるのですが、その際に出たエラーについてのメモです。
具体的にはVue-cliをインストール後 `vue create` を実行しようとすると以下のようなエラーが出て失敗します。

```
npm ERR! typeerror Error: Missing required argument #1
npm ERR! typeerror at andLogAndFinish (/usr/share/npm/lib/fetch-package-metadata.js:31:3)
```

調べてみると公式でissueが上がっていました。自分が使っているZorin OS 15.2はUbunts18.04がベースになっているのですが、やはり同じ環境でエラーが出ているようです。デフォルトだとaptなどのパッケージマネージャでインストールできるnode.js関連のパッケージが古いらしく、以下のバージョンだとエラーが出るっぽいです。

```
$ node --version
v8.10.0
$ npm --version
3.5.2
```

https://github.com/npm/cli/issues/681

こちらに上がっている解決策を上から順に試していったのですが、最終的に役立ったのはページ下部でeezoo氏が掲示してくれたもので、以下のコマンドを順番に実行するというものでした。

```
sudo npm install -g n
sudo n latest
sudo npm install -g npm
hash -d npm
npm i
```

今のところこれで無事 `vue create` できるようになっています。