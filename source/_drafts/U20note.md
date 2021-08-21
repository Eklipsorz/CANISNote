---
title: U20note
tags:
---


1. String是由多個字元所組成的陣列，每個元素皆為字元，元素皆會和index作為綁定，你可以直接對字串的某部分進行讀取，但很難直接對他進行部分的寫入變更，得藉由複製以及需要變更的內容混在一起才能達到寫入變更的效果：

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


2. 由多個字元的一般字串很容易被系統當作String物件，所以他可以使用該物件下的一些方法：charAt、indexOf、slice、trim、split、
