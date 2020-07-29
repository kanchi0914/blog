---
title: List<>.ForEach()でcontinueを使いたいときはWhereを使う
date: 2020-07-30 00:41:39
tags: c#
---

いつものようにListのForeachメソッドで処理を書いていて、当然なんですがcontinue文が使えないことに気づきました。  

そういうときはForEachの前にWhere句を挟むとよいようです。例えば、あるリスト(itemsとします)の要素のうち、特定のリスト(ignoredItems)に含まれないもののみ処理を行いたいとき、continueを使うと以下のようになると思いますが、

```c#
List<Item> items = new List<Item>() { ... }
List<Item> ignoredItems = new List<Item>() { ... }

foreach(var item in items){
  if (ignoredItems.Contains(i)) continue;
  ....
}
```

これをForEachメソッドを使う形にすると以下のように書けます。

```c#
items.Where(i => !(ignoredItems.Contains(i))).ToList()
    .ForEach(item => { ... });
```

細かい点ですが、やはりLinqは便利だなと思いました。

ちなみにbreak文を使いたいときは前段にTakeWhile()を挟むといいようです。自分は使ったことないですが…

https://www.urablog.xyz/entry/2018/06/07/070000