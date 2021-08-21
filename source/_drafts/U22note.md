---
title: U22note
tags:
---



1. 函式是種物件，主要是方便封裝可能潛在重複執行的程式碼或者常見功能的程式碼，使用上會有宣告/定義函式以及呼叫宣告過的函式這兩種形式/語法。


2. 宣告/定義一個函式時，便產生該函式的物件，主要會是以下語法：
```
function funName (variable 1, variable 2, ...., variable N) {
	statement
	return value/expression

}
```

function 為宣告函式的關鍵字，而funName則是你所定義的函式名稱，而variable 1至variable N則是這個函式會用到的參數(Parameter)，這些參數會存在由這個函式所構成的Scope，也就是他們是該函式的區域變數且他們能夠向其他變數那樣會根據指派內容而變動自己型別，而statement則是函式要做的處理，而return的部分則是看函式是否需要回傳value或者由expression所代表的value給呼叫者，也可以是沒有variable 1至variable N這幾個參數的函式：

```
function funName () {
	statement
	return value/expression
}
```



3. 呼叫(call)/調用(invoke)宣告過的函式，在程式語言會被稱之為呼叫者(caller)，而被呼叫的函式則被稱之為被呼叫者(callee)，主要的語法會是：以上面宣告為例子

```
let/const result = funName(value 1, value 2, ...., value N)
```

其中funName後面這段是典型呼叫函式的方法，此時就會找已經建構出的funName函式物件，而value 1至value N在這裡稱之為引數(argument)，這些引數會直接對應函式variable 1至variable N，也就是說：每一個參數會被指派對應位置的value。

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

其中return的部分會傳給呼叫者，再接著間接地傳遞給result這個變數，然而若函式本身不存在return且呼叫者仍想要回傳值的話，呼叫者拿到的回傳值會因為函式本身並沒有return，所以回傳值會是沒有，但系統會預設給它一個undefined，最後result會間接地拿到undefined。

```
function funName (variable 1, variable 2, ...., variable N) {
	statement
}

let/const result = funName(value 1, value 2, ...., value N)
```
4. 使用上的簡化


可以給予預設值給沒有對應value的variable，根據引數和參數對應順序，預設值只能設定給最後幾個參數，形式會是以下，在這裡當funName被呼叫時，該函式中的variable M沒有拿到對應的value時，其內容會是valueM。

```
function funName(variable 1, variable 2,... variable M = valueM){
	statement
	return value/expression
}
```

若預設值的給定是在前面的參數，會因為對應順序而引發不必要的錯誤，比如在這裡函式呼叫給定的引數是value1，對應參數的位置是variable1，而variable 2由於呼叫時沒value2，所以該變數的內容會是undefined。

```
function funName(variable 1 = valueM, variable 2){
	statement
	return value/expression
}

funName(value1)

```


參考資料：
1. A function created with a function declaration is a Function object and has all the properties, methods and behavior of Function objects. See Function for detailed information on functions. https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function
