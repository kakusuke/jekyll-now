---
layout: post
title: Mapのキーと値を反転する
tags:
 - Java
---

データが1対1で紐付いているような`Map`から、効率的に逆引きしたいことがあった。
ようするに、`Map`のキーと値を反転させた`Map`を作りたい。

``` java
Map<String, Integer> map = new HashMap<>();
map.put("a", 1);
map.put("b", 2);
```

このような`Map`があったとき、Java7 では以下のように書くと思う。

``` java
Map<Integer, String> reversedMap = new HashMap<>();
for (Entry<String, Integer> e : map.entrySet()) {
	if (reversedMap.contains(e.getValue())) {
		throw new IllegalStateException("Duplicate key " + e.getValue());
	}
	reversedMap.put(e.getValue(), e.getKey());
}
```

Java8 ではこんな感じ?

``` java
map.entrySet().stream()
  .collect(Collectors.toMap(e -> e.getValue(), e.getKey());
```

だいぶすっきり書ける。
実は1:1じゃなかった場合とかも、ちゃんと`IllegalStateException`吐いてくれるので便利。
