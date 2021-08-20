---
title: U19note
tags:
---

1. 物件(object)會用雜湊表(hash table)來表示，也就是透過key-value pairs的形式來儲存物件所需的屬性(property)和方法(method)。

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

第一種方法：
```
obj.newproperty = newvalue 	// add new property into obj
```

第二種方法：
```
obj['newproperty'] = newvalue	// add new property into obj
```


5. 使用[]來表示屬性的好處是可以方便在for迴圈或者適用於得用變數來表示屬性的場景
，比如：

```
for (let key in obj) {
	console.log(obj['key'])
}
```


6. 查閱某物件的所有property、value、property: value之方法：


