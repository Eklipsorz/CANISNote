---
title: DOM - How To Manipulate Attribute From Object
tags:
 - HTML
categories:
 - Web Development
---


Draft:
透過JS來操控元素節點所擁有的屬性樣式(節點)





## classList

NODE.classList 指元素節點所擁有的屬性之一，其值會對應著具有live特性的DOMTokenList物件(註1)，該物件會儲存其對應元素使用的所有樣式名稱，每一個使用的樣式會以單獨一個元素儲存在DOMTokenList物件。

### classList -  Method 

NODE.classList.add(className1,...., classNameN)：對元素節點所擁有的DOMTokenList進行其他樣式名稱(className1,...classNameN)的增加，而被增加進來的樣式名稱會從DOMTokenList的尾部位開始放入，而參數量(可被放進去的樣式數量)則不限定於1~2個，可以按照開發者的需求而不斷放入。

NODE.classList.remove(className1,..., classNameN)：從DOMTokenList物件刪除指定樣式名稱，而className1至classNameN則是依據開發者而定，沒限定於1~2個。



1. NODE.classList - 查看目前所有 class 名稱，會回傳類似陣列的清單
2. NODE.classList.add(className1, ..... )
3. NODE.classList.remove(className1, .... )
4. NODE.className = classNameValue


## className
NODE.className 屬性是指元素節點所採用的屬性(尤指類別)節點是什麼或者採用的選擇器是什麼，該屬性可允許開發者讀取和寫入，若元素節點NODE搭配多個類別，那麼其值會是下面形式來表示，每一個類別之間都會有空格作為間隔，這代表著對應元素使用著class1、class2、....、classN這幾個類別。
```
"class1 class2 ..... classN"
```

若要替元素節點NODE進行類別或者樣式的變更，則可透過相同規則來進行，另外，每一次的變更會連帶改變具有live特性的DOMTokenList物件。
```
NODE.className = "class1 class2 .... classN"
```


5. NODE.style.styleName:






## 註解
1. DOMTokenList物件是類似於陣列的物件但又不是陣列，儲存該物件的元素皆會以index做為綁定，可以透過index來存取對應元素。


## 參考資料
1. DOMTokenList簡介，https://developer.mozilla.org/en-US/docs/Web/API/DOMTokenList
2. Element.classList 簡介，https://developer.mozilla.org/en-US/docs/Web/API/Element/classList
3. CSSStyleDeclaration 簡介，https://developer.mozilla.org/en-US/docs/Web/API/CSSStyleDeclaration
