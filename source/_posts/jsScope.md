---
title: JavaScript - Scope 簡介
date: 2021-07-29 01:29:40
tags: JavaScript
---

在電腦編程中，(作用域)Scope是指對應某種entity的name所能夠被合法辨識以及使用的範圍，其中entity是指的是某種記憶體區塊，而name就是variable，換言之，只要我們透過variable就能操控代表記憶體區塊的entity。



## Global vs. Local

根據Scope的範疇，我們主要分為Global和Local，前者指的是合法辨識和使用的範圍是整個程式碼(系統)或者整個檔案，而Local則是範圍被限制在一個小區塊，並不會是整個系統當中。通常只要某個對應entity的名字脫離它本身的scope，系統會自動釋放記憶體。

## difference between var and let

當我們使用var宣告變數時，此時的scope會試著被擴展global或者整個function。比如說：我們宣告一個名為test的函式，且在函式內部用括號建立一個block，然後在內部宣告testval並指派值給他。


```
function test() {

    {
       var testval = 10 
    
    }
    
    console.log(testval)        //result = 10
}
```

一般來說，當block結束之後，便會直接釋放掉block內部的變數，但由於採用var來宣告，這使他變成test函式的local variable，由於這樣，而在執行console.log(testval)的時候能夠讀取出其值為10。


如果說今天把function去掉，而考慮在一個global空間上添加了區塊在其內部宣告testval，此時testval又會因爲var的宣告方式，使它的scope轉變為global。


```
{

  var testval = 10

}

console.log(testval)
```

然而如果這兩個程式碼中所出現的var更改為let，會直接變成那個區塊的local variable，只要系統跳脫區塊之後，其內部所用到記憶體會被釋放。

```
{

  let testval = 10

}

console.log(testval)
```


此時，再讓系統去執行到console時會出現以下錯誤，這告訴我們系統已經釋放掉testval使它無法被合法辨識。

``` 
ReferenceError: testval is not defined
```
## 特例


如果在一個未宣告的變數進行assignment，那麼在執行assignment之前會額外宣告其變數為global variable


參考資料：
1. https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Statements/var


