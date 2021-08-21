---
title: U25note
tags:
---

1. 物件除了擁有屬性以外，還可以擁有一些方法(method)，這些方法都是表現物件本身會有的行為、功能，每個方法都是由特定的函式所構成，而方法本身在物件裡頭會和其他屬性一樣被當成雜湊表上的key值或者變數，只是可以存放函式物件。





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


4. this 變數在object裡指的是目前呼叫函式或者方法的擁有者(owner)物件，適用場景為當某種物件想要在自己方法來使用自己所擁有的屬性的場景，而每個物件的屬性值也不一樣，比如說obj1, obj2, obj3....等等這些物件，這些物件的原型都皆是如下，而這些物件的屬性值又不一樣，這時我們若透過obj1.method1()來呼叫，會得到他自己本身的屬性，而改為obj2.method1()來呼叫，又是另一種不同的屬性值。

```
let/const objName = {
	property1: value1,
		.
	propertyN: valueN,
	method1: function() {
			statement
			return this.property1
		 }

}


```

5. 物件本身可以被當作函式的引數值以及回傳值，那以下的程式碼當例子，我們可以透過funName(objName)來呼叫使用，其結果會印出objName物件的所有屬性值。
```
let/const objName = {
	property1: value1,
		.
	propertyN: valueN
}

function funName(obj) {

	console.log(obj.property1)
		.
	console.log(obj.propertyN)
}
```

而若是拿物件當作回傳值的話，則是以宣告物件的形式來回傳，就如同funName所回傳的型態：
```
function funName(obj) {

	return {
		property1: value1,
			.
		propertyN: valueN
	
	}

}

```




Note: 

1. 利用for迴圈來印出一個物件的所有屬性值並用函式來封裝，假設一個物件屬性如同下面的object，而印出所有屬性值的函式名為showDetail，可以看到利用for迴圈會根據obj所擁有的雜湊表上表示的key來迭代，然後由於key裡頭也有method1，所以得用typeof來檢測是否有函式物件，最後會印出所有屬性值。

```
let/const object = {
	property1: value1,
	property2: value2,
		.
	propertyN: valueN

	method1: function () {

		 }

}

function showDetail (obj) {
  for (let prop in obj) {
    if (typeof user[prop] !== 'function') {
      console.log(user[prop])
    }
  }
}
showDetail(user)
```

2. 利用函式來建立物件：

```
function createPlayer (name, hp, mp) {
  return {
    name: name,
    hp: hp,
    mp: mp
  }
}

const player1 = createPlayer('Magician', 30, 100)
const player2 = createPlayer('Warrior', 100, 30)

console.log(player1) // {name: "Magician", hp: 30, mp: 100}
console.log(player2) // {name: "Warrior", hp: 100, mp: 30}

```



