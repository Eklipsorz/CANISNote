---
title: JavaScript - 函式簡介
tags:
- JavaScript
- Function
---

函式是種物件，主要是方便封裝可能潛在重複執行的程式碼或者常見功能的程式碼，使用上會有宣告/定義函式以及呼叫宣告過的函式這兩種形式/語法。

## 如何宣告/定義

宣告/定義一個函式時，便產生該函式的物件，其語法會是：function 為宣告函式的關鍵字，而funName則是你所定義的函式名稱，而variable 1至variable N則是這個函式會用到的參數(Parameter)，這些參數會存在由這個函式所構成的作用域，也就是他們是該函式的區域變數且他們能夠向其他變數那樣會根據指派內容而變動自己型別，而statement則是函式要做的處理，而return的部分則是看函式是否需要回傳value或者由expression所代表的value給呼叫者。

```
function funName (variable 1, variable 2, ...., variable N) {
	statement
	return value/expression

}
```

```
function funName () {
	statement
	return value/expression
}
```


## 如何呼叫/調用
呼叫(call)/調用(invoke)已宣告定義過的函式，被呼叫的函式則被稱之為被呼叫者(callee)，主要的語法會是：以上面已宣告的函式為例子，並且呼叫funName函式。

```
let/const result = funName(value 1, value 2, ...., value N)
```

```
funName(value 1, value 2, ...., value N)
```

當呼叫該函式時，會把value 1至value N傳入對應的函式物件中，在這裡這些變數被稱之為引數(argument)，這些引數會直接對應函式variable 1至variable N，也就是說：每一個參數變數會被指派對應位置的value，而指派形式會看傳入內容是否為primitive type，若是的話，會建立新的記憶體來存內容，並給予對應的參數

```
{
	variable 1 = value 1
	variable 2 = value 2
		.
		.
	variable N = value N

	statement
	return value/expression
}
```

其中return的部分會傳給呼叫者，再接著間接地傳遞給result這個變數值或者表達式代表的內容，然而若函式本身不存在return且呼叫者仍想要回傳值的話，呼叫者拿到的回傳值會因為函式本身並沒有return，所以回傳值會是沒有，但系統會預設給它一個undefined，最後result會間接地拿到undefined。

```
function funName (variable 1, variable 2, ...., variable N) {
	statement
}

let/const result = funName (value 1, value 2, ...., value N)		// return undefined
```

## 另一種宣告的方法


可以給予預設值給沒有對應value的variable，根據引數和參數對應順序，預設值只能設定給最後幾個參數，形式會是以下，在這裡當funName被呼叫時，該函式中的variable M沒有拿到對應的value時，其內容會是valueM。

```
function funName(variable 1, variable 2,... ,variable M = valueM) {
	statement
	return value/expression
}


funName(value1, value2,.... value (M-1)) 						//只傳入 (M-1) 個引數到函式物件
```

