---
title: DOM Object Manipulation
tags:
 - JavaScript
---


查找DOM元素，有兩種途徑：
1. 利用屬性挑選(Selection)：直接選出第一個根元素並利用屬性來直接對樹狀結構進行查找。
2. 節點遍歷(Traverse)：選出最前面的元素，往該元素所擁有的子元素開始找，再來找兄弟元素，直到找到需要的元素





## Selection

### 屬性查找

1. document.querySelector(CSS selectors)

- 功能：依據selector給予的名稱來找到與名稱相同的元素，其CSS selectors的欄位是要填入要找的CSS選擇器名稱(註1)。
- 回傳形式：會是以節點形式去回傳結果，若名稱相同的元素有多個的話，只會回傳第一個找到的元素；若沒有元素的話，則會回傳空陣列。


2. document.querySelectorAll(CSS selectors)
- 功能：與document.querySelector一樣，不同的點在於可以挑選所有選擇器名稱相同的元素並放入一個特殊且與Array相似的物件-NodeList(註2、3)，其物件可以像Array使用index來呼叫每一個被放入的元素。

- 回傳形式：會以NodeList來回傳找到的結果。

3. getElementBy 家族語法:
與querySelector家族不同的是，若能抓到多個相同屬性值的元素，都會放入HTMLCollection 物件(註4)並回傳，而ID的話，因為其值只會在網頁出現一次，所以沒必要放入該物件，直接回傳找到的物件/節點就行，而HTMLCollection 物件跟NodeList 物件是不同的。

a. document.getElementById(elementID):

- 功能：根據elementID來尋找擁有相同ID的元素，找到並回傳該物件。
- 回傳形式：以元素節點的形式回傳。

b. document.getElementsByClassName(classname)

- 功能：根據elementID來尋找擁有相同名字屬性的元素，將找到的元素放入HTMLCollection 物件內並將該物件回傳給呼叫者。
- 回傳形式：以HTMLCollection這物件來回傳。


c. document.getElementsByName(name)
 
- 功能：根據elementID來尋找擁有相同類別名稱的元素，將找到的元素都放入HTMLCollection 物件內並將該物件回傳給呼叫者。
- 回傳形式：以HTMLCollection這物件來回傳。

d. document.getElementsByTagName(name)

- 功能：根據elementID來尋找擁有相同標籤的元素，將找到的元素都放入HTMLCollection 物件內並將該物件回傳給呼叫者。
- 回傳形式：以HTMLCollection這物件來回傳。

## querySelectAll vs. getElementsBy Family

## Traverse



## 註解
1. 其要找的名稱格式是依據CSS如何從名稱挑選選擇器的規則而定，比如要找某類別下的子元素，就是'.class child'，
其中.class為類別名稱，而child則是該類別為class的元素所擁有的子元素，而中間的空格是依據CSS要挑選parent selector下的child selector而加的: 

```
selectorName1 selectorNmae2 {
	/* CSS CODE */
}
```

2. NodeList並不是陣列，只是類似於陣列的特殊物件，能存放所有種類的節點物件，NodeList不能夠新增刪除元素，只能對其物件進行讀取，物件內的每個元素皆由一個數字index來做綁定，可以透過index來直接讀取對應的元素，具體能做的事情：

- 可透過迭代器來對物件內所存的內容進行遍歷(forEach)
- 它擁有length屬性可以知道它存了多少個節點


3. 可以透過Array.isArray來再次檢驗NodeList是否為陣列物件：首先先建構以下的程式碼，再利用chrome所提供的console功能來找到所有類別為card-bodyli元素尋找在它之下li元素來達到模擬querySelectorAll抓取多個相同類別名稱的元素之目的
```
<html>

<head>
  <title>DOM</title>
</head>

<body>

  <div id="my-recipe" class="card-body">
    <h4>Chocolate cake</h4>
    <ul>
      <li>sugar</li>
      <li>cocoa</li>
      <li>flour</li>
      <li>salt</li>
      <li>baking powder</li>
    </ul>
  </div>
  <script src="main.js"></script>
</body>

</html>

```

其querySelectorAll的程式碼會是如下，下達完便會把所有li元素放入NodeList，接著用list變數去指向該物件。

```
let list = document.querySelectorAll('.card-body li')
```

最後再透過isArray方法便能知道NodeList是否為陣列：
```
console.log(Array.isArray(list))
```

結果會是：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630077428/blog/dom_Manipulation/arrayCheckExample_sknq9w.png)

4. HTMLCollection 跟 NodeList 是類似於陣列的物件，除了本身只能存元素節點這物件以外，其餘功能性大致和NodeList一樣，擁有：

- 每個元素都有數字index來綁定，好方便透過index去讀取對應的元素
- 擁有length屬性去得知物件目前所存的內容大小 


## 參考資料
1. NodeList物件，https://developer.mozilla.org/en-US/docs/Web/API/NodeList
2. Node object vs. Element object，https://stackoverflow.com/questions/9979172/difference-between-node-object-and-element-object
3. DOM API 查找節點，https://ithelp.ithome.com.tw/articles/10191765
