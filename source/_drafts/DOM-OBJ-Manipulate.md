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
依據selector給予的名稱來找到與名稱相同的元素，其CSS selectors的欄位是要填入要找的CSS選擇器名稱(註1)，回傳值會是DOM Node，若名稱相同的元素有多個的話，只會挑選一個；若沒有元素的話，則會回傳空陣列。



2. document.querySelectorAll(CSS selectors)
功能性與document.querySelector一樣，不同的點在於可以挑選所有選擇器名稱相同的元素並放入一個特殊且與Array相似的物件-NodeList(註2)，其物件可以像Array使用index來呼叫每一個被放入的元素。

若我們檢驗其回傳值是否為陣列，可以使用下面例子以及chrome進行檢驗：在這個例子會透過query

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

## 註解
1. 其要找的名稱格式是依據CSS如何從名稱挑選選擇器的規則而定，比如要找某類別下的子元素，就是'.class child'，
其中.class為類別名稱，而child則是該類別為class的元素所擁有的子元素，而中間的空格是依據CSS要挑選parent selector下的child selector而加的: 

```
selectorName1 selectorNmae2 {
	/* CSS CODE */
}
```

2. NodeList並不是陣列，只是類似於陣列的特殊物件，其物件不能夠新增刪除元素，只能對其物件進行讀取，物件內的每個元素皆由一個數字index來做綁定，可以透過index來直接讀取對應的元素，具體能做的事情：

- 可透過迭代器來對物件內所存的內容進行遍歷(forEach)
- 它擁有length屬性可以知道它存了多少個節點

## 參考資料
1. NodeList物件，https://developer.mozilla.org/en-US/docs/Web/API/NodeList

