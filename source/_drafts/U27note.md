---
title: U27note
tags:
---


1. undefined 是種資料型別，這個型別下的內容會是undefined，它是用來告訴系統某些變數已經被宣告，但內容上沒有被指派或者用值去定義，預設上，當變數只有宣告卻沒指派內容時，系統會預設undefined給該變數。

2. null 是種資料型別，但實際上是另一種物件型別，這個型別下的內容會是null，它是用來告訴系統某些物件是不存在的或者告訴系統目前指向的物件是不存在的。


3. undefined 和 null 可以與自己相等，換言之，會符合以下式子：

```
(undefined === undefined)
(null === null)
```


note:

1. 宣告和定義：
宣告(Declaration)：告訴系統一個名字(identifier)以及該名字對應什麼樣型別的資料
定義(Definition)：將名字對應至一個記憶體區塊或者實體

2. 檢查物件的條件式：

```
const result = null

if (result && typeof result === 'object') {
	console.log('This is an object!!')
} else {
	console.log('This is null')
}

```
