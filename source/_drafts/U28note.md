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


4. 
