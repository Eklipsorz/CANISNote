---
title: U22note
tags:
---



1. 函式是種物件，主要是方便封裝可能潛在重複執行的程式碼或者常見功能的程式碼，使用上會有宣告函式以及呼叫宣告過的函式這兩種形式/語法。



2. 宣告一個函式，主要會是以下語法：
```
function funName (variable 1, variable 2, ...., variable N) {
	statement
	return value/expression

}
```

function 為宣告函式的關鍵字，而funName則是你所定義的函式名稱，而variable 1至variable N則是這個函式會用到的參數(Parameter)，這些參數會存在由這個函式所構成的Scope，而statement則是函式要做的處理，而return的部分則是看函式是否需要回傳value或者由expression所代表的value給呼叫者。


3. 呼叫宣告過的函式，主要的語法會是：以上面宣告為例子

```
let/const result = funName(value 1, value 2, ...., value N)
```

其中funName後面這段是典型呼叫函式的方法，此時會構建出名為funName這個函式物件，而value 1至value N在這裡稱之為引數(argument)，這些引數會直接對應函式variable 1至variable N，也就是說：每一個參數會被指派對應位置的value。

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


