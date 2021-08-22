---
title: U19note
tags:
---

1. 物件(object)會用雜湊表(hash table)來表示，也就是透過key-value pairs的形式來儲存物件所需的屬性(property)和方法(method)，在雜湊表表示以及程式碼形式中會把屬性和方法都視為屬性，而方法只不過是儲存函式物件的屬性。

2. 定義物件語法：使用let/const來宣告物件，再由括號包括物件該有的屬性和方法，property是屬性，而value則是填入屬性的值。

```
let/const objname = {
	property1: value1,
	property2: value2,
		.
		.
	propertyN: valueN
}
```

若沒有property1: value1的話，那麼就會使objname變成空物件，這樣形式的物件在語法上是合法的。

```
let/const objname = {

}
```

3. 讀取/寫入物件屬性方法：主要有兩種方式，第一種為使用.符號，第二種則是使用[]符號來進行。

第一種方法：

```
let value = obj.propertyM	// read propertyM value of object
obj.property1 = value		// overwrite propertyM value of object
```

第二種方法：

```
let value = obj['propertyM']	// read propertyM value of object
obj['property1'] = value	// overwrite propertyM value of object

```




4. 新增物件屬性的語法：第一種方法使用.來表示新屬性，第二種方法使用[]來表示新屬性。

第一種方法： 點記法 (dot notation) 
```
obj.newproperty = newvalue 	// add new property into obj
```

第二種方法： 括號記法 (bracket notation) 
```
obj['newproperty'] = newvalue	// add new property into obj
```


5. 使用[]來表示屬性的好處是可以方便在for迴圈或者適用於得用變數來表示屬性的場景，比如：for...in語法只能列舉某物件下的屬性。

```
for (let key in obj) {
	console.log(obj['key'])
}
```


6. 查閱某物件的所有property、value、property: value之方法：

a. Object.keys(obj)：以一維陣列來回傳obj所擁有的屬性名稱
b. Object.values(obj)：以一維陣列來回傳obj所擁有的屬性對應值
c. Object.entries(obj)：以二維陣列來回傳obj所擁有的[key:value]值，每一個元素皆是[key:value]的一維陣列。
