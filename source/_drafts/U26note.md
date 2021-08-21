---
title: U26note.md
tags:
---

1. 繼U22的說明來看，函式是種物件，因此我們可以宣告一個函式的同時將它指派給變數，在這裡我們宣告一個匿名函式這物件並指派給resultFunction。
```
let/const resultFunction = function (variable1,..,variableN) {
				statement
				return value/expression
			   }
```

或者以下面形式來指派函式物件：

```
function funName (variable1,..,variableN) {

	statement
	return value/expression

}


const/let resultFunction = funName

```

2.  一般函式的宣告會在瀏覽器載入頁面前或者執行前先提前宣告(hoisting)，而將函式當作物件來指派的形式則會因為形式上會遵守ECMA規則而不會被提前宣告，只會向其他變數的宣告之先後順序來處理。


3. 由於函式本身可以當做物件，所以可以當做物件上面的屬性指派、當另一個函式的回傳值、當作另一個函式的參數。


a. 當作物件上面的屬性指派：

```
const/let obj = {

	property1: value1,
		.
	propertyN: valueN

	method1: function () {
			do something
		 }
}

```

b. 當作另一個函式的回傳值：

```
function funNameA (variable1,..., variableN) {
	statement
	return value/expression
}

function funNameB (variable1,.., variableN) {
	statement
	return funNameA(value1,.., valueN)

}
```

c. 當作另一個函式的參數：這技術稱之為callback，透過參數來使用函式A的函式B，而函式B被稱之為callback function，比如invokeFunction就是callback function。

```
function funNameA (variable1,..., variableN) {
	statement
	return value/expression
}

function funNameB (variable1,.., variableN) {
	statement
	return funNameA(value1,.., valueN)

}

function invokeFunction (callback) {

	callback(value1,.., valueN)

}

```


