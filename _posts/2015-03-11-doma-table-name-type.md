---
layout: post
title: Doma の %expand でスネークケースに変換する
tags:
 - Java
 - Doma
---

Java の規約はキャメルケース、DBの規約がスネークケースなので、なんとか変換したかった

`@Entity(naming = NamingType.SNAKE_LOWER_CASE)`とエンティティに書いとくとうまいことやってくれた

``` java
@Entity(naming = NamingType.SNAKE_LOWER_CASE)
public class HogeEntity {
	@Id
	public Integer id;
	public String hoge;
}
```

こんな感じ

ちなみに継承もできるけど、`@Entity`アノテーションは定義する必要があるっぽい

``` java
@Entity
public class Fuga extends Hoge {
}
```

のようにしておくと、`Fuga`使うときもスネークケースに変換してくれた


ドキュメントにあんまり詳しく書いてなかった気がするのでメモっとく
