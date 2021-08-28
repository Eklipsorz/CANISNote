---
title: DOM-OBJ-HowToManAttribute
tags:
 - HTML
---


Draft:
透過JS來操控元素節點所擁有的屬性樣式(節點)


NODE.classList 指元素節點所擁有的屬性之一，其值會對應著具有live特性的DOMTokenList物件(註1)，該物件會儲存其對應元素使用的所有樣式名稱，每一個使用的樣式會以單獨一個元素儲存在DOMTokenList物件。


NODE.classList.add(className1,....classNameN)：對元素節點所擁有的DOMTokenList進行其他樣式名稱的增加，

1. NODE.classList - 查看目前所有 class 名稱，會回傳類似陣列的清單
2. NODE.classList.add(className1, ..... )
3. NODE.classList.remove(className1, .... )
4. NODE.className = classNameValue


5. NODE.style.styleName:






## 註解
1. DOMTokenList物件是類似於陣列的物件但又不是陣列，儲存該物件的元素皆會以index做為綁定，可以透過index來存取對應元素。
