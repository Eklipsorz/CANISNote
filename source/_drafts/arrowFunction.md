---
title: Arrow Function
tags:
 - JavaScript
---

箭頭函式(Arrow Function)是以匿名函式的基礎下而近一步簡化的語法，箭頭函式只能適用於所有原本適用於匿名函式的寫法，該函式保留了匿名函式的參數、內部的程式、函式物件本身，其形式為：

```
(value1,..., valueN) => {
	do_something
}
```

而對應的匿名函式為：

```
function (value1,..., valueN) {
	do_something
}
```

寫箭頭函式可注意的小細節：
1. 當參數只有一個參數時，可省略"()"括號；但若沒有任何參數以及參數量大於1的話，還是得添加"()"括號:

2. 若內部的程式碼只有一小段，可省略"{}"括號
