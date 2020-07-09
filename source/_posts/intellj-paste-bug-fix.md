---
title: Mac環境のIntellijで、command+Vのペーストが2回行われる問題を解決する
date: 2020-07-10 00:14:05
tags: kotlin
---

IntelliJは言わずと知れた(?)Java用のIDEで、基本的にはとても優れたエディタで不満も少ないのですが、たまにバグっぽい挙動に遭遇します。気のせいかMac環境ではそれが多く、表題の件もその一つです。

以下のURLはPycharmでの話ですが、自分の環境でも全く同じ現象が起きていて、ペーストするたびに2回同じ文章が貼り付けられることがあり、作業どころではありませんでした。調べた結果無事解決できたので共有します。

https://intellij-support.jetbrains.com/hc/en-us/community/posts/360005165159-PyCharm-pastes-twice

この問題はJetBrainsの日本語公式ブログでも報告されていて、原因は以下のように報告されています。

> 調査中ですが、JetBrains IDE製品バージョン2019.2における大きな変更として、IDEの起動に使用されるJBR(JetBrains IDEに同梱されているJava Runtime/SDK)が今回よりバージョン11ベースになったこと（以前はバージョン８）が影響しているようです。
>
> https://blog.jetbrains.com/ja/2019/07/30/2025/

基本的には記事に書かれている対処法を試せば問題ないと思われます。以下この問題の対処法です。

### 1. Choose Runtime Pluginを導入する

公式ブログの下の方にもコメントで書いていただいている方がいらっしゃいますが、以下を参考にIntelliJにChoose Runtime Pluginというプラグインを導入します。

https://www.jetbrains.com/help/idea/switching-boot-jdk.html?_ga=2.182646182.1637383658.1594286342-248335048.1590988640

### 2.  Runtimeを切り替える

Shitf+Command+AでActionパレットを呼び出し、Choose Runtimeを選択します。

![スクリーンショット 2020-07-10 0.34.32](/images/intellj-paste-bug-fix/2020-07-10_001.png)

Runtimeの選択画面になるので、JBR 8系の中から適当に選びます。たくさん出てくるのでどれを選べばいいか迷いますが、1.8.0~とついているものならどれでも構わないと思います(多分)。自分は以下のやつを選んでます。

![スクリーンショット 2020-07-10 0.37.04](/images/intellj-paste-bug-fix/2020-07-10_002.png)

Runtimeを切り替えた後は再起動し、問題が発生しなくなっていることを確認します。

### 3. UIの設定

上記2の手順までで問題は解決しているのですが、使っているMac OSによってはUI上のフォントなどの見た目が妙な感じになるっぽいので直します。伝わりづらいですが微妙にボケた感じになってます。Catalina 10.15.5での現象です。

![_2020-07-02_14.24.53](/images/intellj-paste-bug-fix/2020-07-02_001.png)

以下のように設定します。

<img src="/images/intellj-paste-bug-fix/2020-07-02_002.png" alt="2020-07-02" style="zoom:67%;" />

設定した後は、完全に元の見た目に戻すことはできませんが、少し見やすくなります。Linuxに入れたIntelliJと同じような見た目になりますね。

![Untitled](/images/intellj-paste-bug-fix/Untitled.png)

エディター上のフォントも変わっているのでこの際に変更します。自分はせっかくなのでJetBrainsが開発しているフォントを使いました。

https://www.jetbrains.com/ja-jp/lp/mono/

これで作業は完了です。この問題は現在でも公式で修正されていないみたいなのですが、早く直るといいですね。