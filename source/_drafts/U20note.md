---
title: U20note
tags:
---


1. string本身是immutable型別，內容上是由多個字元所組成的陣列，每個元素皆為字元，元素皆會和index作為綁定，你可以直接對字串的某部分進行讀取，但由於immutable的限制很難直接對它進行寫入變更，得藉由複製以及需要變更的內容混在一起才能達到寫入變更的效果：

a. 直接針對原本字串進行讀取：其中m的值可以填入0 ~ (str.length-1)
```
let str = 'helloworld!'
let test = str[m] 
```

b. 直接針對原本字串進行寫入：這樣子寫會無法變更str第一個字元的內容

```
let str = 'helloworld!'
str[0] = 'A'			// It cannot change anything
```

但可以直接更改str的內容為其他字串

```
str = 'A'
```


2. 由多個字元的一般字串很容易被系統當作String物件，所以他可以使用該物件下的一些方法：charAt、indexOf、slice、trim、split、substring、substr，這些方法並不會更動原本字串的內容。

a. charAt(index): 回傳指定位置index的字元

b. indexOf(searchvalue, start): 從start位置開始找字元searchvalue所在的位置，找到第一個之後便直接回傳其位置

c. slice用法跟陣列一樣

d. trim()：清除字串起始處和結尾處所出現的多餘空白

e. split(separator)：根據separator所指定的字元來分割出好幾個子字串並放入陣列中

f. substring(start, end)：從start位置擷取至end處之前的內容，回傳結果便是擷取後的內容。

g. substr(start, length)：從start位置擷取內容，內容長度到達length個字元時便停止，回傳結果便是擷取內容。
