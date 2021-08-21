---
title: U25note
tags:
---

1. 物件除了擁有屬性以外，還可以擁有一些方法(method)，這些方法都是表現物件本身會有的行為、功能，每個方法都是由特定的函式所構成。





2. 定義一個物件所擁有的方法只需要將函式物件指派給特定屬性或者method，形式上可以像是以下的method1和method2，這兩個都是函式，第一個宣告名為funName的函式物件給method1，而第二個則是宣告一個匿名(不取特定的函式名稱)的函式物件給method2，該函式被稱之為匿名函式(anonymous function)。

```
let/const objName = {
	property1: value1,
	property2: value2,
		.
	propertyN: valueN
	
	method1: function funName(variable1, variable2, ..., variableN) {
					
					statemenet
					return value/expression
		 }
	method2: function (variable1, variable2, ...., variable N) {
					statement
					return value/expression
		 }
}
```

3. 使用/呼叫/調用一個物件特有的方法，只需要把被指派函式物件的method name當作是函式呼叫就能達成：拿上面的形式來說的話，若要使用method1或者method2，就按照下面的語法：

```
objName.method1(variable1, variable2, variable3, .... , variableN)
objName.method2(variable1, variable2, variable3, .... , variableN)
```
