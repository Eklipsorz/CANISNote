---
title: JavaScript - Scope 簡介
date: 2021-07-29 01:29:40
tags: JavaScript
---

在程式語言中，作用域(Scope)是指對應某種實體(entity)的名字(name)所能夠被合法辨識以及使用的範圍，其中實體是指的是某種記憶體區塊，而名字就是變數(variable)名稱，換言之，只要我們透過變數名稱就能操控代表記憶體區塊的實體。在這個簡介中，我們會談到作用域分為哪些以及如何宣告變數的作用域。


根據Scope的區分，我們可以區分為Root Scope、Parent Scope、Child Scope，預設上我們會在Root Scope進行宣告以及定義變數，在這裡所宣告的變數所擁有的作用域會是Root Scope或 Global Scope，而此變數會被稱之為全域變數，若跳脫Scope的範圍或者執行完畢時，其變數所佔用的記憶體會被釋放，若是在Root Scope內部產生另一個Scope並進行變數宣告的話，其額外產生的Scope對於Global Scope而言會是Local Scope，在那裡宣告的變數所擁有的Scope會只有那區塊，而不是Root Scope，而且該變數只要跳脫那Scope，它所佔用的記憶體空間會被釋放掉。


比如首先我們先替Root Scope取名為Scope A，其內部再產生一個名為Scope B的Scope，括號內部又宣告了一個變數b，其變數b的Scope只有括號內部而已。

```
// Scope A: Root Scope
let a = 10

{ // Scope B: Child Scope of Root Scope

    let b = 20

}

```

在這情況下的變數會被稱作為區域變數，且該Scope A對於由括號構成的Scope B而言，Scope A會是他的Parent Scope，而Scope B會是Scope A的Child Scope。若我們繼續沿用上面例子中的Scope B內產生另一個名為Scope C的Scope的話，也就是如下所示：

```
// Scope A: Root Scope
let a = 10

{ // Scope B: Child Scope of Root Scope
    let b = 20 
    { // Scope C: Child Scope of Scope B
        let c = 30
    }
    

}

```

其Scope C會是Scope B的Parent Scope，而Scope C則會是Scope B的Child Scope。




## Root、Parent、Child的變數存取關係
這三者下變數之間的存取關係是依照下列條件：
1. 變數宣告的先後順序
2. 變數所在Scope是哪一種

```
// Scope A: Root Scope
let a = 10

{ // Scope B: Child Scope of Root Scope
    let b = 20 
    { // Scope C: Child Scope of Scope B
        let c = 30
    }
    

}

```


繼續沿用上個例子，當想在Root Scope去印出Scope C下的變數或者 Scope B的變數時，我們有兩種選擇方式：a. 在Scope B前寫印變數的程式、b. 在Scope B後寫出印變數的程式

a. 在Scope B前寫印變數的程式

```
// Scope A: Root Scope
let a = 10

console.log(b)
console.log(c)
{ // Scope B: Child Scope of Root Scope
    let b = 20 
    { // Scope C: Child Scope of Scope B
        let c = 30
    }
    

}

```

b. 在Scope B後寫出印變數的程式


```
// Scope A: Root Scope
let a = 10


{ // Scope B: Child Scope of Root Scope
    let b = 20 
    { // Scope C: Child Scope of Scope B
        let c = 30
    }
    

}
console.log(b)
console.log(c)
```

但這兩種方式皆無法正常印出變數b和變數c，a方式是因爲Scope根本還沒被產生，所以本來就印不出來，而b方式則是因爲Scope內的所有變數皆被釋放，所以也就跟著印不出來，同樣的概念也可以放在只考慮Scope B和 Scope C這兩者上，換言之，沒辦法再Parent Scope沒存取Child Scope以及其Scope內部的Scope下的變數。


同等的，若我們想要在Scope B印出Parent Scope的變數 a，我們會因為Parent Scope的變數a還存在而能夠印出來。

```
// Scope A: Root Scope
let a = 10


{ // Scope B: Child Scope of Root Scope
    let b = 20 
    
    console.log(a)
    { // Scope C: Child Scope of Scope B
        let c = 30
    }
    

}

```

但變數a的宣告定義是放在Scope B後頭的話，也就是像這樣，
```
// Scope A: Root Scope



{ // Scope B: Child Scope of Root Scope
    let b = 20 
    
    console.log(a)
    { // Scope C: Child Scope of Scope B
        let c = 30
    }
    

}
let a = 10
```

在這裡，對於Scope B而言，變數a的宣告定義會被系統認定為還未定義而無法被正常印出，這也代表宣告定義的先後順序會影響存取。 但若是在Child Scope之前就定義好要存取的變數，那麼可以在Child Scope來存取Parent Scope的元素。

若我們考慮至少1個身在同個Scope的Child Scope，這些Child Scope彼此間的存取狀況會是如何？我們先繼續沿用上個例子來假設，首先我們在Scope B產生名為Scope D的Scope，現在我們有Scope C 和 Scope D，當我們想在Scope C存取Scope D的變數時，會因為宣告的先後順序而無法正常存取，而當我們想在Scope D存取Scope C下的變數時，我們會因為Scope C的變數已經被釋放掉而無法正常存取，換言之，Scope C 和 Scope D這兩者間無法彼此存取他們所擁有的變數。

```

// Scope A: Root Scope

let a = 10

{ // Scope B: Child Scope of Root Scope
    let b = 20 
    
    console.log(a)
    { // Scope C: Child Scope of Scope B
        let c = 30
    }

    { // Scope D: Child Scope of Scope B
        let d = 40
    }
    

}

```

### 總結

整體而言，若要存取的變數在Scope之前宣告好的話， 我們可以：
1. 無法在Parent Scope存取Child Scope所定義的變數。
2. Child Scope能夠因為事先宣告的關係而能夠存取位於Parent Scope的變數。
3. 多個在同一個Parent Scope下的Child Scope是無法存取彼此間的變數。


## Root Scope
Scope範圍為整個程式或者整份文件。

## Parent Scope && Child Scope
當某個Scope A內部擁有另一個Scope B時，其Scope A會被Scope B稱作為Parent Scope，而Scope B會被Scope A稱作為Child Scop。

## 如何構成額外的Scope

藉由括號來定義其Scope之範疇
```
{
let a = 20

}

{
let b = 10

}
````


## var vs. let and const
由於ES6才開始重視Scope而新增了let和const這兩者宣告方式，透過任一個方式來宣告變數時，系統會嚴格定義他們的Scope是位於哪裏，而var是在ES6之前就出現的，對於他的Scope定義會比較寬鬆，若用var來宣告變數的話，往往該變數容易出現預期外的結果。

比如說以下這兩個例子，按照先前提到Scope和宣告方式，理論上，第一個程式碼會跑出錯誤，第二個則是得到10，但實際上結果皆為11，這證明var宣告下的變數會出現預期外的效果。

```
var a = 10

{
  a = 11
  

}

console.log(a)
```

```
var a = 10

{
  var a = 11
  

}

console.log(a)
```



/* old content */




## Global vs. Local

根據實體的範疇，我們主要分為全域(Global)和區域(Local)，前者指的是合法辨識和使用的範圍是整個程式碼(系統)或者整個檔案，而區域則是範圍被限制在一個小區塊，並不會是整個檔案或者系統當中，如果某個變數對應的實體擁有全域作用域的話，該變數被稱之為全域變數；反之，如果某個變數對應的實體是擁有區域作用域的話，該變數被稱之為區域變數。

對於程式語言的記憶體管理，通常只要某個對應實體的變數名字脫離它本身的作用域，系統就會自動釋放其記憶體。

## Declaration: var、let、const

對於作用域的宣告，我們會先使用var、let或者const這些關鍵字來宣告一個變數對應某個實體，其作用域會根據宣告的所在而決定，比如說

當我們使用var宣告變數時，此時的作用域會試著被擴展成為全域或者整個函式(function)。我們宣告一個名為test的函式，且在函式內部用括號建立一個區塊(block)，然後在內部宣告testval並指派值給他。


```
function test() {

    {
       var testval = 10 
    
    }
    
    console.log(testval)        //result = 10
}
```

一般來說，當系統脫離該區塊之後，便會試著釋放掉區塊內部的變數，但由於採用var來宣告變數testval，這使他變成test函式的區域變數，而非是原本括號內部的區域變數由於這樣，最後在執行console.log(testval)的時候能夠讀取出其值為10。


如果說今天把函式去掉，而考慮在一個全域空間上添加了區塊在其內部宣告testval，此時testval又會因爲var的宣告方式，使它的作用域轉變為全域。


```
{

  var testval = 10

}

console.log(testval)
```

然而如果這兩個程式碼中所出現的var更改為let，會直接變成那個區塊的區域變數，只要系統跳脫區塊之後，其內部所用到的記憶體會被釋放。

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

而const則是另一種let的版本，跟let不同的是，只要使用const去宣告變數，就一定得先
指派一個實體給變數做對應。若沒指派內容會顯示以下訊息：

```
SyntaxError: Missing initializer in const declaration
```

若成功宣告並指派實體給變數時，之後就無法對該變數的對應內容進行修改，只能存取。


而var、let、const的不同處在於var是ES5標準以前就有的關鍵字，ES標準越前面其嚴謹性會比較鬆散，這使得他的作用域上往往會出現預期以外的事情，比如使區域變數升格為全域變數，而let、const則是ES6標準出現的，其作用域上會嚴格根據宣告所在來決定，當宣告在全域出現，那就是全域變數；若出現在區域上，那就是區域變數。

## 特例
 
1. 如果在一個未宣告的變數進行指派(assignment)，那麼在執行指派之前會額外宣告其變數為全域變數，比如：

```
{
  test = 10
}
console.log(test)
```

輸出結果會顯示test是個儲存10的全域變數。

參考資料：
1. https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Statements/var

2. https://blog.bitsrc.io/understand-scope-in-javascript-e150f889ba72



3. https://8thlight.com/blog/jarkyn-soltobaeva/2017/06/13/scope-and-closures-in-javascript.html
