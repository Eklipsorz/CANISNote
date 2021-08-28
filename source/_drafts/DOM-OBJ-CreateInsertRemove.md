---
title: DOM-OBJ-CreateInsertRemove
tags:
 - HTML
 - JavaScript
---

Draft:

document.createElement(tagName)
建立標籤名稱為tagName的元素節點，但在這個狀態下的元素節點並不會跟任何節點扯上parent或者child這些關係，就只是單純建立一個節點。

回傳形式：以元素節點進行回傳


NODE.innerHTML = value1
指定HTML內容value1給元素(節點)NODE，這相當於在該對應標籤內，指定value1為其標籤內部的內容，其內容會被重新以HTML形式來解析並產出新的DOM

NODE.innerText = value1
指定內容value1給元素節點，這相當於在該對應標籤內，指定value1為其標籤內部的內容，但與innerHTML不同的事情就是不會被重新解析





