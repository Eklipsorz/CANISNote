---
title: JavaScript - 解構賦值 (Destructuring Assignment)
tags:
- JavaScript
---

在JavaScript中，解構(Destructuring)指的是從存放多個物件或者值的集合抽取出一小部分的過程，過程中不會如同字面上的分解而真的去影響集合本身或者分解其集合，而賦值(Assignment)是指將特定內容賦予某個物件或者變數，兩者合在一起就是指從存放多個物件或多個值的集合提取出來當作特定變數的指派內容，在這裏指的集合可以是指物件、陣列。然而，當一個集合經過提取後，會根據集合種類來決定賦值的方式和形式是什麼，在這我們分兩小節來說明



## 對陣列進行解構賦值
若想對陣列進行解構賦值，得用以下語法才能實現，這個語法會先看這一系列的變數(var1, ....., varN)是否有被宣告，有被宣告可以不用額外使用var/let/const來宣告，若沒被宣告的話，得額外添加var/let/const來宣告，其變數性質會依據其宣告關鍵字不同而改變，若是使用const關鍵字來宣告var1至varN，這些變數會是const性質
，在這裏，var1至varN是來接受從陣列array提取過來的值，

```
var/let/const [var1, ...., varN] = array;
```

而由於系統會將上面array看作是存放多值或者多種物件的集合，所以我們可以把array看成[value1, ... ,valueM]，解構會依照陣列索引值順序來抽取，而順序會是由索引值0至索引值M-1，

```
var/letc/const [var1, .... , varN] = [value1, .... , valueM];
```

而賦值則是將每次抽取到的內容按照變數宣告的順序來指派，也就是說當系統抽取從陣列中抽取出value1時，便會指派value1給var1，而下一個抽取的值value2，會指派給var2，而這個抽取和賦予的動作在理論上會持續到min(N, M)次抽取賦予，而N是指左手邊的變數數量，而M則是指陣列中的索引值數量，換言之，當左手邊的變數量不夠去接收抽取內容時和當右手邊抽取的內容不夠抽取賦值給左手邊宣告的變數時兩種情況之一發生的話，就會停止抽取賦值 不過在停止抽取和賦予之前，其過程會如同：

```
var/let/const var1 = value1;
var/let/const var2 = value2;
var/let/const var3 = value3;
            .
            .
            .
```

另外當右手邊抽取的內容不夠抽取賦值給左手邊宣告的變數時，左手邊剩下沒拿到值的變數所存的內容皆預設為undefined，如同未指派內容的變數一樣

### 例子


```
const array = [1, 2, 3, 4, 5];
let [var1, var2, var3] = array;
```

假使宣告一個擁有五個數字的陣列，並且用三個變數去接收抽取後的內容，抽取和賦值的動作會持續到var3=3才停止，而最後結果會是：

```
let var1 = 1;
let var2 = 2;
let var3 = 3;
```

而若是宣告一個擁有三個數字的陣列，並且用五個變數去接收抽取後的內容，抽取和賦值動會因為能抽取的內容都被抽取光了，所以也到了var3=3才停止，而最後結果也是相同，只是造成停止動作的因素是不同的，另外剩下的var4和var5會因爲沒拿到指派值而被預設為undefined。


### 應用


1. 可以在兩個變數之間進行內容的交換：

```
let var1 = value1;
let var2 = value2;

[var2, var1] = [var1, var2];
```


## 對物件進行解構賦值


https://javascript.info/destructuring-assignment
https://pjchender.blogspot.com/2017/01/es6-object-destructuring.html
