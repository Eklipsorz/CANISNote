---
title: note
tags:
---

# 型別轉換與三個等號

Description:
1. Type checking： The process of verifying and enforcing the constraints of types，換言之，確定變數是何種資料型態的階段。

2. Type checking會發生在編譯期間或者執行期間，若某程式語言發生在編譯期間，其程式語言會是靜態語言(statically typed language)；若發生在執行期間，其程式語言會是動態語言(dynamically typed language)


3. JavaScript 是動態語言，可以不必在開發過程指定變數為什麼樣的資料型態，執行過程中會由系統根據指派內容來改變其變數的資料型態。

4. JavaScript由於系統會根據指派內容來改變其變數的資料型態，若開發上沒做特別的型別檢查會衍生出預期外的結果，比如它會把原本預期為數字型態的變數轉換成字串型態。

5. JavaScript會根據單一值或者表達式來變動型態，單一值的話會根據其值的型態是什麼來決定變數，而表達式則是會利用以下特性來決定型態：

1. 運算子處理的優先權，括號優先權最大，其次是乘除，再來就是加減
2. 先被處理的資料所擁有的型態以及內容是什麼？ 其內容若能在數值系統表達數字的話，則會被看待為數字型態，否則就依照有沒有字串型態的參數來決定，都沒有的話，會以數字型態來處理，否則就以字串型態

note：
a. 會在boolean系統視為true的內容，有非空內容的字串、非0的數字、非Null物件。
b. 會在boolean系統視為false的內容，有空字串、0、NaN、null、undefined。 
c. 若在boolean系統視為false的內容，可以在數值系統表達0
d. 若在boolean系統視為true的內容，只有true才能表達1


例子1：

```
console.log(100 + false +  '0')
```

系統會先替第一個運算子(operator)抓取100和false，而false在這裡它會試著轉化為數字型態的0，所以會是數字型態的100(100+0)，接著就是100 + '0'，由於'0'本身是字串且無法被轉化成數值，所以會以字串的型態來表達，其最後結果會是'1000'

例子2：

```
console.log('a' + false + 0)
```

一樣地，系統會先第一個運算子抓取了'a'和false，在這裡其中一個單一值為字串，所以字串的形式來處理，其結果會是'afalse'，接下來換下一個運算子，'afalse' + 0，由於'afalse'本身也是字串，所以也是以字串的型態來處理，最後結果為'afalse0'