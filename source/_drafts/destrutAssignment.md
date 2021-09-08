---
title: JavaScript - 解構賦值 (Destructuring Assignment)
tags:
- JavaScript
---

在JavaScript中，解構(Destructuring)指的是從存放多個物件或者值的集合抽取出一小部分的過程，而賦值(Assignment)是指將特定內容賦予某個物件或者變數，兩者合在一起就是指從存放多個物件或多個值的集合提取出來當作特定變數的指派內容，在這裏指的集合可以是指物件、陣列。當一個集合經過提取後，會根據集合種類來決定賦值的方式和形式是什麼，在這我們分兩小節來說明


一個集合經過提取後，會根據
Draft：





1. 得使用var/let/const []來宣告被指內容的變數，其變數會遵從var/let/const本質上的規則，而賦值則是用等號和要被提取的集合，等號代表著指派，集合就陣列和物件
```
let [var 1,...., var N] = array/object
```

```

```

另外允許使用表達式(expression)來表達array/object本身，比如說：split會回傳擁有hello和world這個元素的陣列，而它剛好可以成為被解構的對象
```
let [var1, var2] = "hello world!".split(' ')
```


2. Destructuring 本質上擁有分解的意思，但實則上，只是單純從集合中提取資料，並不會真的分解集合本身或者影響集合本身

3. 對於陣列和物件這兩種資料型別來說，解構賦值的解構會是一樣，但抽取內容的賦值形式是不同的，

## 對陣列進行解構賦值
若想對陣列進行解構賦值，得用以下語法才能實現，這個語法會先宣告一系列的變數(var1, ....., varN)來接受從陣列array提取過來的值，而宣告變數的方法並不受限於let，也可以使用var和const，當然地，這些變數的性質會跟隨著var/const/let本身帶有的特性，

```
var/let/const [var1, ...., varN] = array
```

而由於系統會將上面array看作是存放多值或者多種物件的集合，所以我們可以把array看成[value1, ... ,valueM]，解構會依照陣列索引值順序來抽取，而順序會是由索引值0至索引值M-1，

```
var/letc/const [var1, .... , varN] = [value1, .... , valueM]
```

而賦值則是將每次抽取到的內容按照變數宣告的順序來指派，也就是說當系統抽取從陣列中抽取出value1時，便會指派value1給var1，而下一個抽取的值value2，會指派給var2，而這個抽取和賦予的動作在理論上會持續到min(N, M)次抽取賦予，而N是指左手邊的變數數量，而M則是指陣列中的索引值數量，換言之，當左手邊的變數量不夠去接收抽取內容時或者當右手邊抽取的內容不夠抽取給左手邊宣告的變數時，不過在停止抽取和賦予之前，其過程會如同：

```
var/let/const var1 = value1
var/let/const var2 = value2
var/let/const var3 = value3
            .
            .
            .
```


### 例子1


```
const array = [1, 2, 3, 4, 5]
let [var1, var2, var3] = array
```

假使宣告一個擁有五個數字的陣列，並且用三個變數去接收抽取後的內容，其最後結果為





## 對物件進行解構賦值