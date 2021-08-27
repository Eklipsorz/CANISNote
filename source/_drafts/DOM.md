---
title: DOM
tags:
 - HTML
categories:
 - Web Developement
---


DOM (Document Object Model)是將HTML檔案本身內容轉化多個物件或者多個節點，並將這些物件/節點組合成樹狀結構。每一個節點都代表著一個HTML所定義的標籤名稱，並帶有特定類別名稱(class1,...classN)、特定ID(id)、一些子節點(Child node1,..,Child nodeN)以及帶有其他標籤(挾帶其他子節點的節點)：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630048968/blog/dom/aDomNode_kvuecl.png)


在這裡只有類別名稱和特定ID並不會被當作子節點來看待，其餘元素則會按照parent-child關係來區分父節點和子節點，每一個子節點可以是該節點所存的文字內容、該節點原本在HTML形式包含的標籤元素，而該標籤元素又會在DOM視同為另一種子節點的集合來看待。


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


## 註解
1. Document Object Model中的Document是指HTML檔案本身

## 參考資料
1. children 和 childNodes 的差別，https://www.geeksforgeeks.org/what-is-the-difference-between-children-and-childnodes-in-javascript/
