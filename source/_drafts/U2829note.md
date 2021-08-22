---
title: U28note
tags:
---


1. 在數值系統中，當計算的數值超越系統本身的最大值或者最小值的話，會顯示Infinity或者-Infinity，前者是表示正值的無限大，後者是表示負值的無限小。

2. 在數值系統中，NaN(Not A Number)是數值型別，代表著無法表示的數值，更無法與自己相等，必須利用isNaN函式來進行判定。

```
NaN === NaN 	// return false
isNaN(NaN)	// return true
```

3. Math 物件本身帶有一些常用的方法：

a. Math.ceil(x): 利用小數點來無條件進位
b. Math.floor(x): 利用小數點來無條件捨去
c. Math.round(x): 利用小數點來四捨五入
d. Math.sqrt(x): 回傳x的平方根或者對x開更號的結果
e. Math.abs(x): 回傳對x做絕對值的結果
f. Math.random(): 產生0~1之間的亂數值，亂數範圍[0, 1)
g. Math.pow(base, exponent): 回傳base的exponent次方


4. 進位至小數點後第n位或者捨去至小數點後第n位，必須要先對參數乘上n次10，然後做完進位或者捨去後，對其除以n次10，比如說：考慮著下式的結果(266.6666666)，若想對結果擷取至小數點後2位的話，
```
Math.round((baseLength * baseLength * height) / 3)
``` 
只需要先在內部乘上2次的10，也就是100，然後再除以2次的10便能達到結果：

```
Math.round((baseLength * baseLength * height * 100) / 3) / 100
```

另一個方法則是使用toFixed(2)方法來四捨五入進位至小數點後第二位：

```
((baseLength * baseLength * height) / 3).toFixed(2)
```

5. 由於二進制對於浮點數而言，可能會因為需要計算的位數大於系統本身所能有的位數而有所誤差，因此若計算過程涉及浮點數時，請務必檢查是否誤差問題，再來進行後續的開發，若遇到此問題，可以使用if或者使用第四點提到的倍乘方法來解決
