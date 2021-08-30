---
title: DOM - How to find an Node Object
tags:
 - HTML
 - JavaScript
categoires:
 - Web Development
---



查找DOM元素，有兩種途徑：
1. 利用屬性挑選(Selection)：利用根元素物件的方法依特徵進行指定元素物件的查找。
2. 節點遍歷(Traverse)：選出最前面的元素，往該元素所擁有的子元素開始找，再來找兄弟元素，直到找到需要的元素

附註該文章內容是以目前已知的知識為主，之後會再往後補充。

## Selection

### 屬性查找

#### querySelector 家族語法：
1. document.querySelector(CSS selectors)

- 功能：依據selector給予的名稱來找到與名稱相同的元素，其CSS selectors的欄位是要填入要找的CSS選擇器名稱(註1)。
- 回傳形式：會是以節點形式去回傳結果，若名稱相同的元素有多個的話，只會回傳第一個找到的元素；若沒有元素的話，則會回傳空陣列。


2. document.querySelectorAll(CSS selectors)

- 功能：與document.querySelector一樣，不同的點在於可以挑選所有選擇器名稱相同的元素並放入一個特殊且與Array相似的物件-NodeList(註2、3)，且該NodeList並不具有live特性(註4)，其物件可以像Array使用index來呼叫每一個被放入的元素。
- 回傳形式：會以不具有live特性的NodeList來回傳找到的結果。

#### getElementBy 家族語法：
與querySelector家族不同的是，若能抓到多個相同屬性值的元素，都會放入HTMLCollection 物件(註5)並回傳，而ID的話，因為其值只會在網頁出現一次，所以沒必要放入該物件，直接回傳找到的物件/節點就行，而HTMLCollection 物件跟NodeList 物件是不同的。

a. document.getElementById(elementID):

- 功能：根據elementID來尋找擁有相同ID的元素，找到並回傳該物件。
- 回傳形式：以元素節點的形式回傳。

b. document.getElementsByClassName(classname)

- 功能：根據elementID來尋找擁有相同類別屬性的元素，將找到的元素放入具有live特性的HTMLCollection 物件內並將該物件回傳給呼叫者。
- 回傳形式：以具有live特性的HTMLCollection這物件來回傳。


c. document.getElementsByName(name)
 
- 功能：根據elementID來尋找擁有相同名字(name是種標籤會有的屬性)值的元素，將找到的元素都放入具有live特性的NodeList 物件內並將該物件回傳給呼叫者。
- 回傳形式：以具有live特性的NodeList物件來回傳。

d. document.getElementsByTagName(name)

- 功能：根據elementID來尋找擁有相同標籤的元素，將找到的元素都放入具有live特性的HTMLCollection 物件內並將該物件回傳給呼叫者。
- 回傳形式：以具有live特性的HTMLCollection這物件來回傳。


## Traverse
不同於Selection，遍歷是利用樹狀結構的節點A以某種方向來轉移至節點B，當然，若節點B並非是自己想要找的節點，只是跟要找的節點具有parent-child關係或者sibling關係，那麼可能或許會從節點B以另一種方向來轉移至另一個節點，直到找到你想要找的節點。在這裡以某個節點為主，方向可以歸類為五種：往父元素的方向、往前一個兄弟節點的方向、往後一個兄弟節點的方向、往第一個子元素的方向、往最後一個子元素的方向。

用圖說明每個方向的示意圖
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630310467/blog/dom_Manipulation/traverseDirection_orxjyb.png)

### Traverse over all node
遍歷所有種類的節點

用圖說明節點的種類
parentNode
previousSibling
nextSibling
firstChild
lastChild

### Traverse over all element node
只遍歷元素節點

用途說明只探查元素節點。

parentElement
previousElementSibling
nextElementSibling
firstElementChild
lastElementChild


## 註解

0. 在這裡提到的特徵是指(要被尋找的)元素物件所被挑選的選擇器名稱(含標籤名稱、類別名稱、ID)、擁有的name屬性是什麼。


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

4. 形容NodeList和HTMLCollection的live特性都是指著當物件內的對應元素有所變動時便會自動更新NodeList和HTMLCollection，而這特性並不會是NodeList和HTMLCollection專有的，所以也有可能存在著不具有Live特性的NodeList或者HTMLCollection。


我們拿getElementsByName以及querySelectorAll這兩個方法當作例子，前者方法會產生具有live特性的NodeList，而後者方法會產生不具有live特性的NodeList，而這兩者會出現在以下程式碼中的<script>標籤並放入console來觀測網頁元素內容的變動是否改變NodeList的長度，若有的話，代表其NodeList就具有live特性，而沒有則表示不具有其特性。程式碼是以Kuro Hsu在iT邦提供的程式碼為基礎來修改的。
```
<div id="outer">
	<div name="inner">inner1</div>
        <div name="inner">inner2</div>
        <div name="inner">inner3</div>
        <div name="inner">inner4</div>
        <div name="inner">inner5</div>
</div>

<script>
	getElementsByName/querySelectorAll
</script>

```
首先，我們先來看看getElementsByName的表現以及將程式碼合併成可觀測的程度，在這裡由於querySelectorAll只會挑類別，所以為了和querySelectorAll保持一致的結果，特地讓程式碼去挑選name為inner，且所有div元素的name都是inner。

```
<div id="outer" name="inner">
        <div name="inner">inner1</div>
        <div name="inner">inner2</div>
        <div name="inner">inner3</div>
        <div name="inner">inner4</div>
        <div name="inner">inner5</div>
</div>
      
<script>
      
        // <div id="outer">
        let outerDiv = document.getElementById('outer');
      
        // 所有name為inner的元素
        let allInner = document.getElementsByName('inner');
      
        // 清空前，name為inner的元素還剩多少個
        console.log(allInner.length);    
      
        // 清空 <div id="outer"> 下的節點
        outerDiv.innerHTML = '';
      
        // 清空後，name為inner的元素還剩多少個
	console.log(allInner.length); 
</script>
```

其結果會是：console內顯示javascript的執行過程，你可以發現第一筆印出的資料是表示著(與NodeList相關的)元素變更前的NodeList長度，第二筆則是變更後的長度，可以發現第二筆會因為內部的div被清空而減少許多。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630087942/blog/dom_Manipulation/liveNodeListExample_qxluxa.png)

再來就是改放querySelectorAll以及合併相關程式碼來觀察：
```
<div id="outer" name="inner">
        <div name="inner">inner1</div>
        <div name="inner">inner2</div>
        <div name="inner">inner3</div>
        <div name="inner">inner4</div>
        <div name="inner">inner5</div>
</div>
  
<script>
      
        // <div id="outer">
        let outerDiv = document.getElementById('outer');
      
        // 所有div的元素
        let allInner = document.querySelectorAll('div')
      
        // 清空前，div還剩多少個
        console.log(allInner.length);    
      
        // 清空 <div id="outer"> 下的節點
        outerDiv.innerHTML = '';
      
        // 清空後，div元素還剩多少個
        console.log(allInner.length); 
</script>

```

其結果如下所示：可以發現第一筆和第二筆都維持6，而這6剛好是所有div的元素數
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630087942/blog/dom_Manipulation/notLiveNodeListExample_nxzmrq.png)

如果在這個基礎下，在最後一個console前添加以下程式碼的話，

```
allInner = document.querySelectorAll('div')
```
結果會變成第二筆會因為重新計算而減少許多，這代表著該NodeList是不具有live特性，而前者方法是具有live特性的

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630088620/blog/dom_Manipulation/notLive2Live_mlavsq.png)



5. HTMLCollection 跟 NodeList 是類似於陣列的物件，除了本身只能存元素節點這物件以外，其餘功能性大致和NodeList一樣，擁有：

- 每個元素都有數字index來綁定，好方便透過index去讀取對應的元素
- 擁有length屬性去得知物件目前所存的內容大小 
- 可透過迭代器來對物件內所存的內容進行遍歷(forEach)
 



## 參考資料
1. NodeList物件，https://developer.mozilla.org/en-US/docs/Web/API/NodeList
2. Node object vs. Element object，https://stackoverflow.com/questions/9979172/difference-between-node-object-and-element-object
3. DOM API 查找節點，https://ithelp.ithome.com.tw/articles/10191765
4. querySelectorAll 回傳的NodeList，https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll
5. getElementsByTagName 回傳的HTMLCollection，https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByTagName
6. getElementsByClassName 回傳的HTMLCollection，https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName
7. getElementsByName 回傳的NodeList，https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByName   
