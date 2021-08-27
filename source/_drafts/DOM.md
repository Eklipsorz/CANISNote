---
title: DOM
tags:
 - HTML
categories:
 - Web Developement
---


DOM (Document Object Model)是將HTML檔案本身內容轉化多個物件或者多個節點，並將這些物件/節點組合成樹狀結構。每一個節點都帶有一些子節點來表示對應元素的類別(class1~classN)、ID(id)、文字內容、原本對應元素在HTML所包含的元素/節點(tag，帶有其他子節點的節點或者帶有子節點集合的標籤):

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630051797/blog/dom/aDomNode_uehzgh.png)


在這裡只有類別名稱和特定ID並不會真的在DOM被當作子節點來看待，其餘元素則會按照parent-child關係來區分父節點和子節，因此我們可以將其餘元素視為該元素下的子節點(Child node1~Child nodeN)，而被對應元素包含的對應元素(tag)也會是該節點下的子節點。

另外我們也根據節點的用途來進一步區分每個節點的種類是為何：
- 





以下面一個例子的p標籤來說明該標籤在DOM架構下的樣子，
```
<html>
   <head>
	<title>DOM</title>
   </head>
   <body>
	<h1>Hello, World!</h1>
  	<p class="text-mute">
    		This is a <em>simple</em> website.
 	</p>
        
</body>
</html>
```

其樣子會是：



## 註解
1. Document Object Model中的Document是指HTML檔案本身

## 參考資料
1. children 和 childNodes 的差別，https://www.geeksforgeeks.org/what-is-the-difference-between-children-and-childnodes-in-javascript/
