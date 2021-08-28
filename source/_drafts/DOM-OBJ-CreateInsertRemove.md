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


預設上，瀏覽器會依據讀取的優先順序而決定某些子元素的存放順序，也就是說當瀏覽器讀取左邊的內容時，一開始讀取到element這標籤就建立element節點，接著又從標籤內發現content1這獨立內容(可以是另一個節點、文字、註解，但不會是類別屬性)，瀏覽器讀取到便建立屬於content1節點並當作是element元素的第一個子節點，而隨後讀取到的content2，便轉化成第二個子節點，後面依此類推。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630164255/blog/dom_Manipulation/file2DOM_tpcrw7.png)

後面新增的子節點將會放在子節點N(child node N)之後。

parentNode.appendChild(newNode)：
將元素節點newNode當作是另一個元素節點parentNode的子節點，其子節點會放在目前子節點之後，也就是子節點N(child node N)之後，而新放入的子節點將會是子節點N+1(child node N+1)

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630164722/blog/dom_Manipulation/defaultAddNewNode_eon6un.png)

parentNode.insertBefore(newNode, referenceNode)
將元素節點newNode當作是parentNode子節點，並放在另一個parentNode的子節點referenceNode之前，而child node N會是第N+1個子節點，

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630165095/blog/dom_Manipulation/insertBeforeNode_burnu5.png)

若子節點referenceNode不存在的話，會直接將節點newNode放到所有子節點之後，其動作等同於appendChild(newNode)。

parentNode.replaceChild(newNode, oldNode)
將元素節點newNode當作是parentNode子節點，並將這個新的子節點取代掉另一個parentNode的子節點oldNode，而子節點oldNode將會被移除並釋放記憶體空間。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630166583/blog/dom_Manipulation/replaceChildNode_xhwsxd.png)
