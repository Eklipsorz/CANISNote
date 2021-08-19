---
title: JS - Data Type
tags:
 - JavaScript
---



/* primitive data type的變數由於所佔的大小會固定所以可以存在只能存放連續空間且固定大小的stack，而object的變數由於所佔的大小不確定，只能先存在可動態變動記憶體大小的heap區塊 */


primitive data type 的變數存在stack，而object則是存在heap。

https://ithelp.ithome.com.tw/articles/10241346






/* old content */


JS是一種Dynamically typed languages，變數的資料型別將會根據指派內容而跟著變動，比如說有時會因爲指派數值給某變數而把該變數變成數值型別，也有時將字串指派給該變數，系統就會把這變數的資料型別轉換為string。


其資料型別中，主要分為primitive data type和object，前者的primitive data type是程式語言原本就有(內建)的型別且對應的內容皆會是one to one，而object則是可以由這些primitive data type而構成一個資料型別集合，比方說，可以用數值、字串、布林合為一個新的型別，而這個型別通常會被賦予有意義的object name。
## 資料型別(Data Type)

在JavaScript的ES6標準中，一共定義了以下6個primitive data type和object：

1. string：字串，由至少1個字元所構成，得用單引號或者雙引號來表示，比如"javascript“這內容會被系統當作字串，另外開頭和結尾都必須是單引號或者雙引號，不能夠混用，比如'javascript"，這會被系統誤判。
2. number：數字，可以是整數或者小數
3. boolean：布林值，只有兩種值：true和false(大小寫有區號)
4. null：空值，只會有一個值null，表示參照不存在
5. undefined：標示其變數並沒有指派內容，它的值會是undefined
6. symbol：這是 ES6 最新定義的型別，是過去的 JavaScript 沒有的，我們暫時不提它
7. object：在 JavaScript 裡物件、陣列、函式都屬於物件型別，物件是多個資料的結構，並且用 key-value pair 的結構來組合多個資料，例如 { a: 1, b: 2 }


## 資料型別的特例


### Primitive Data Type 能使用method和property

部分primitive data type會為了開發方便而衍伸成物件化的primitive type，而原本未被物件化的type可以使用這些物件化所帶有的property和method，比如說string可以使用length屬性和split方法。


參考資料:
1. https://stackoverflow.com/questions/3907613/how-is-a-javascript-string-not-an-object

### 當如果沒指派內容的話

undefined：
當你未在宣告後指派內容給變數時，其內容會由undefined來代替，比如說

```
let mybirthday
console.log(mybirthday)
```

console最後會告訴你這變數內容是undefined，但這跟沒有定義，比如執行後跑出以下的錯誤訊息時，這表示test_date並未宣告。

```
ReferenceError: test_date is not defined
```


### javascript中，字元和字串有差別嗎？

沒有特別為了區分字元和字串而設定兩種不同資料型態，這兩者都會被當作字串來處理，且使用上會用單引號、雙引號、重音號(backtick)，一組字串會由多個字元所組成的陣列，其陣列內容無法透過array[i]來更改，但可以透過相同方式來被讀取。
    
    
![](https://i.imgur.com/8jYNRwN.png)
    
    
參考資料：
1. https://developer.mozilla.org/zhTW/docs/Web/JavaScript/Data_structures


## null的作用是什麼？它是物件嗎

告訴系統說目前指向的物件是不存在的，它在資料型別中算是物件，不算是primitive type。


### null、underfined這二者的差別是什麼

兩者在指派內容上是一樣，但資料型別和用途上是不同，null是物件，而undefined是undefined，前者是告訴某些物件是不存在的或者告訴系統目前所指向/參照的物件是不存在的，後者則是告訴某些變數已經做宣告但卻沒做內容指派，這時變數的內容會被預設成undefined.

參考資料為：
    1. https://blog.csdn.net/erdfty/article/details/81283764
    2. https://stackoverflow.com/questions/5076944/what-is-the-difference-between-null-and-undefined-in-javascript


## 參照(reference)是什麼？
一塊記憶體空間相互綁定的別名，或者說另一個變數的別名。

參考資料為：
1. https://stackoverflow.com/questions/57483/what-are-the-differences-between-a-pointer-variable-and-a-reference-variable-in
    

    
    


## Coercion - 型別強制轉換陷阱


如果故意把兩種不同的資料型別放在一起，比如以下的例子，數字加上字串，最後結果會是字串的2223，也就是説系統直接先將兩個不同資料型別都當作字串來處理，並且按照字串來處理+符號的方式來獲得最後結果，其+代表著兩個不同字串串連在一起形成一個字串。

```
let myAge = 22
let yourAge = '23'
console.log(myAge+yourAge)

```



question：
1. 著名地雷有什麼？
2. 承轉換說明，最後轉換為啥會是字串？
3. 如何強制轉換？有什麼方式？


### 如何檢查該變數的資料型別

可使用typeof語法來檢查，比如下列語法，最後會在螢幕顯示其資料型別

```
let myAge = 22
typeof myAge
```


question:
1. 其語法真只能顯示在螢幕裡？


### 在字串中套入變數形成不同的變數

現在，請試著想像你在寫一個遊戲。玩家的分數儲存在 userScore 這個變數中，而現在需要印出一句話：「Your score is: XXX in this round.」（你這回合的分數是：XXX），有兩個方式可以做到這件事：


#### 方法一：使用＋號

```
let userScore = 9527
let scoreNotificationStart = 'Your score is: ' 
let scoreNotificationEnd = ' in this round.'
console.log(scoreNotificationStart + userScore + scoreNotificationEnd)
```


#### 方法二： Template literal

可以特別標示字串某部分字串代表某些實際存在的變數或者關鍵字。

```
let userScore = 9527
let scoreNotification = `Your score is: ${userScore} in this round.`
console.log(scoreNotification)

```

注意一下，scoreNotification 會是以下面符號或者重音號作為開頭和結尾，而非直接用單引號，否則就無法使${var}發揮正常作用


```
`
```

question:

1.雙重音號代表什麼意思？

    My Answer:
    
    Template literals，允許字串內部可以插入embedded expressions，並且如同字面上的意思，backtick包含的字串會被當作模板使用，並且讓系統去分析裡面是否存在特殊的表達式，若有的話，會先執行並把結果放入該表達式所在的位置。 

    此外若要告訴系統哪些部分內容才是特殊的表達式，必須使用${}或者其他類似可方便讓系統判斷的符號來告訴系統。



    參考資料：
    1. https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals
    2. https://stackoverflow.com/questions/242813/when-should-i-use-double-or-single-quotes-in-javascript
    3. stack vs. heap https://www.geeksforgeeks.org/stack-vs-heap-memory-allocation/
