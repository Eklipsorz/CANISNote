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
利用根元素物件所提供的方法來依據要找的節點n所擁有的特徵為何來尋找該節點n，而在這裡的特徵會是以該節點所擁有的CSS選擇器名稱、對應的標籤名稱、對應標籤下的name屬性值是為何來尋找。


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

不同於Selection，遍歷是利用樹狀結構的節點A以某種方向來存取到節點B，當然，若節點B並非是自己想要找的節點，只是跟要找的節點具有parent-child關係或者sibling關係，那麼可能或許可以從節點B以另一種方向來存取到另一個節點，直到找到你想要找的節點。在這裡以某個節點 m (element m) 為主，方向可以歸類為五種(如下所示)：往父元素節點的方向(橘紅色箭頭)、往前一個兄弟節點的方向(淺藍色箭頭)、往後一個兄弟節點的方向(淺綠色箭頭)、往第一個子元素的方向(深黃色箭頭)、往最後一個子元素的方向(紫紅色箭頭)。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630312874/blog/dom_Manipulation/traverseDirection_oelny2.png)


從這圖可看出，往父元素節點的方向會單純從節點m存取到節點m的父元素節點，往前一個兄弟節點(同為父節點的節點)的方向會從節點m存取到其父元素節點，再從父元素節點存取到在節點m之前的節點，往後一個兄弟節點的方向會從節點m存取到其父元素節點，再從父元素節點存取到節點m之後的節點，緊接著就是對著節點m的子節點進行存取，往第一個子元素的方向是會從節點m存取到節點m的第一個子元素節點，往最後一個子元素的方向則是從節點m存取到節點m的最後一個子元素節點。對於從節點m存取到它的兄弟節點，雖然中間會透過它們的父元素節點，但在實作上不用透過中間節點就能直接從節點m存取到兄弟節點。

### Trap: break and blank


在接下來的幾個小節中，將會談論如何透過節點物件所擁有的一些屬性來進行節點之間的存取，這些屬性將根據上述提到的五種方向來分為五種屬性，另外若嚴格考慮到節點本身是否為元素種類的節點，又會把這五種屬性切分為十種屬性，一半屬性是只存取五種方向的元素種類的節點，另一半屬性則只存取五種方向的任意種類的節點。


### Traverse for each type of node

在本小節中，會描述只存取五種方向的任意種類的節點，任意種類則意味著不論某個節點node想存取任意方向的節點是哪一個種類，只要能夠讓節點node透過自身的屬性去存取到的節點皆能夠存取，在這裡代表五種方向的屬性分別為parentNode、previousSibling、
previousSibling、nextSibling、firstChild、lastChild。

#### node.parentNode 

代表著節點node的父元素節點parentNode，也就是上述提到的"往父元素節點的方向"來存取父元素節點，若該屬性值回傳null，表示節點node目前就是根元素節點，我們可以透過以下類似的語法來存取這個父元素節點：

```
let parent = node.parentNode
```

也可以將node.parentNode整個視為節點node的父元素節點並對該父元素節點進行五種方向的存取，比如這句會直接對父元素節點進行"往父元素節點的方向"來存取其父元素節點。

```
node.parentNode.parentNode
```

#### node.previousSibling

代表著節點node的前一個兄弟節點previousSibling，也就是上述提到的"往前一個兄弟節點的方向"來存取其兄弟節點，若該屬性值回傳null，表示節點node就是第一個兄弟節點，我們可以透過以下類似的語法來存取前一個兄弟節點：

```
let sibling = node.previousSibling
```

也可以將node.previousSibling整個視為節點node的前一個兄弟節點並對該兄弟節點進行五種方向的存取，比如這句會直接對兄弟節點進行"往前一個兄弟節點的方向"來存取它前一個兄弟節點。

```
node.previousSibling.previousSibling
```

#### node.nextSibling

代表著節點node的後一個兄弟節點nextSibling，也就是上述提到的"往後一個兄弟節點的方向"來存取其兄弟節點，若該屬性值回傳null，表示節點node就是最後一個兄弟節點，我們可以透過以下類似的語法來存取後一個兄弟節點：

```
let sibling = node.nextSibling
```

也可以將node.nextSibling整個視為節點node的後一個兄弟節點並對該兄弟節點進行五種方向的存取，比如這句會直接對兄弟節點進行"往後一個兄弟節點的方向"來存取它後一個兄弟節點。

```
node.nextSibling.nextSibling
```

#### node.firstChild

代表著節點node的第一個子元素節點firstChild，也就是上述提到的"往第一個子元素的方向"來存取其子元素節點，若該屬性值回傳null，表示節點node並沒有任何子元素節點，我們可以透過以下類似的語法來存取第一個子元素節點：

```
let child = node.firstChild
```

也可以將node.firstChild整個視為節點node的第一個子元素節點並對該子節點進行五種方向的存取，比如這句會直接對子節點進行"往第一個子元素的方向"來存取它的第一個子元素節點。

```
node.firstChild.firstChild
```


#### node.lastChild

代表著節點node的最後一個子元素節點lastChild，也就是上述提到的"往最後一個子元素的方向"來存取其子元素節點，若該屬性值回傳null，表示節點node並沒有任何子元素節點，我們可以透過以下類似的語法來存取最後一個子元素節點：

```
let child = node.lastChild
```

也可以將node.lastChild整個視為節點node的最後一個子元素節點並對該子節點進行五種方向的存取，比如這句會直接對子節點進行"往最後一個子元素的方向"來存取它的最後一個子元素節點。

```
node.lastChild.lastChild
```

### Traverse for an element node

在本小節中，會描述只存取五種方向的"元素"種類的節點，元素種類則意味著瀏覽器會檢查要存取的節點是否為"元素"種類的節點，若是元素種類的節點則能夠被存取，否則就會跳過不予存取。在這裡代表五種方向的屬性分別為parentElement、previousElementSibling、nextElementSibling、firstElementChild、lastElementChild。


#### node.parentElement
除了只會存取"元素"種類的節點以外，大致上與node.parentNode的功能性相同，會以"往父元素節點的方向"來存取父元素節點，若該屬性值回傳null，表示節點node目前就是根元素節點。

#### node.previousElementSibling
除了只會存取"元素"種類的節點以外，大致上與node.previousSibling的功能性相同，會以"往前一個兄弟節點的方向"來存取其兄弟節點，若該屬性值回傳null，表示節點node就是第一個兄弟節點。


#### node.nextElementSibling
除了只會存取"元素"種類的節點以外，大致上與node.nextSibling的功能性相同，會以"往後一個兄弟節點的方向"來存取其兄弟節點，若該屬性值回傳null，表示節點node就是最後一個兄弟節點。

#### node.firstElementChild
除了只會存取"元素"種類的節點以外，大致上與node.firstChild的功能性相同，會以"往第一個子元素的方向"來存取其子元素節點，若該屬性值回傳null，表示節點node並沒有任何子元素節點。

#### node.lastElementChild
除了只會存取"元素"種類的節點以外，大致上與node.lastChild的功能性相同，會以"往最後一個子元素的方向"來存取其子元素節點，若該屬性值回傳null，表示節點node並沒有任何子元素節點。

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
