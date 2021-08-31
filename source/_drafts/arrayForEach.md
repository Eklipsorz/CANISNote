---
title: Array Object - forEach method
tags:
 - JavaScript
---


array.forEach(function(currentValue, index,arr), thisValue) 的處理過程等同於

```
for (let i = 0; i < array.length; i++) {

	function(array[i], i, array)
	// array[i] is currentValue
	// i is index
	// arr is array
}
```

回傳值：undefined (因為forEach本身並不會回傳任何東西)

forEach主要有兩個參數，分別為函式物件和this參數，第一個是函式物件(必填)，第二個是指定函式物件的呼叫者是誰的this參數(可選)。

函式物件能填入的參數量為1~3個，以最多的3個來說的話，第一個參數currentValue是指目前傳入函式物件的陣列元素，第二個參數index是指目前陣列元素的對應索引(index)，第三個參數array是指目前陣列，這三個參數名稱可以隨意命名，不論是什麼，系統都會根據參數的對應位置來判定當前參數值是用做什麼。

而函式物件本身可以是匿名、箭頭函式、有函式名稱的函式。
