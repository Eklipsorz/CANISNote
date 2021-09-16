---
title: Semester2-2_U21-U23
tags:
---


## 資料清除
重新整理會由於檔案必須重新載入，載入前動態資料(經由互動產生)會被清掉，但只有rendering的話是不會清掉資料

## 透過JS來調用API的方式
1. 當使用某個Server提供Web API時，開發時盡量把Server名、不同種類的API、參數以變數的形式來分割開來，會比較好維護

比如説：
```
const BASE_URL = 'https://movie-list.alphacamp.io'
const INDEX_URL = BASE_URL + '/api/v1/movies/'
const POSTER_URL = BASE_URL + '/posters/'
```

## 搜尋開發方向
1. 使用者輸入字串在輸入欄，然後在按下搜尋，搜尋就立刻啟動
2. 使用者邊輸入字串邊搜尋

## 搜尋過程
1. 首先搜尋一定會具備著輸入欄來給使用者進行輸入，提交按鈕可以選擇不添加或者添加，但在這裡只單獨思考輸入欄就好
2. 若只用輸入欄來讓使用者輸入搜尋的話，很有可能會是鍵盤按下enter才提交，那麼就對輸入欄設定鍵盤事件，當事件發生時，就便將輸入欄的目前字串拿過來當搜尋的關鍵字，並且對目前資料進行搜尋，將符合的資料放入另一個陣列中，再由這個陣列去重新渲染。

## arrary.filter 方法
1. 該方法為陣列所擁有的方法之一，用途是從陣列中的元素中篩選出符合某種條件的元素
2. 只要開始執行，會先產生另一個空陣列b，形式為如下，function是篩選用的函式，而var1則是array的元素，filter會一次將一個在陣列的元素送至function，只要元素讓function回傳true，該元素就會被放入新陣列b，否則就不放，最後回傳結果新陣列b，也就是最一開始的空陣列b

```
array.filter(function(var1))
```

例子：

```
let numbers = [1, 2, 3, 4, 5, 6]
function isLessThan3(number) {
  return number < 3
}
console.log(numbers.filter(isLessThan3)) // [1,2] ，小於 3 的項目才會被保留
```


```
let numbers = [1, 2, 3, 4, 5, 6]
let newNumbers = numbers.filter(number => number < 3)
console.log(newNumbers) // [1,2]

```



## ...A運算式
1. ... A為一元運算式，而A是可迭代物件，比如陣列、類陣列，通常這些物件都可以當陣列使用
2. 假使A存有a1-an這幾個元素，不管A物件存放他們形式如何，都會將他們轉換成(a1, a2, a3, ... ,an)

例子1:
```
let array = [1, 2, 3, 4, 5]

console.log(...array)         // equals to (1, 2, 3, 4, 5) and result is 1 2 3 4 5
```

例子2:

```
const movies = []; //空陣列，空容器

//目標：用 push 方法把 movies 從空陣列變成 [1,2,3]

//方法一
movies.push(1, 2, 3); //傳入 3 個參數：1,2,3

//方法二
movies.push(...[1, 2, 3]); //把陣列用展開運算子打開，打開後就和方法一一模一樣

//方法三
const numbers = [1, 2, 3]; //做一個陣列
movies.push(...numbers); //和方法二同樣意思

```

## coupling
1. 中文意思為耦合性、連結性，自身與其他事物的相互連接程度，在程式語言則是模組間的相互依賴性，而模組可以是函式、外部檔案、不同作用域的變數。
2. 耦合性越高，代表模組間的相互依賴性很高；耦合性越低，代表模組間比較獨立，不會那麼依賴
3. 低耦合會是品質良好的程式碼指標之一，代表可維護性以及可讀性很高。
4. 高耦合的話，當修改高耦合性的程式時，很有可能影響依賴該程式的模組，使它的結果不如預期。



例子：
以我們的程式碼來說，雖然可以直接在 renderMovieList 函式中取到 movies 這個變數，但這裡我們選擇用參數的方式傳入來降低renderMovieList和movies之間的耦合性，因此，函式 renderMovieList 就不會被特定一組資料綁死，如果未來有其他地方需要做類似的 DOM 操作，只要改變傳入的參數就能重
複利用這個函式。簡言之，我們會希望函式盡量不要依賴外部的資料，愈獨立愈好。


方式1：直接使用全域變數，讓renderMovie真的就是為了movies而存在，其他模組難以使用它

```
let movies = []


// 該函式會被全域變數綁定
function renderMovie () {
    // use global variable movies to handle
}
```

方式2：宣告一個參數，全域變數只要以引數的方式傳進去就能得到方式1相同的結果，但這樣子宣告定義方式可以沿用給其他模組使用。
```
// 該函式不會被綁定。
function renderMovie (data) {
    // use data to handle
}


```

參考資料：
https://ithelp.ithome.com.tw/articles/10191761
https://www.javatpoint.com/software-engineering-coupling-and-cohesion



## em 標籤
1. html的標籤之一，屬性inline元素
2. 用途是以特定樣式來強調一行內的文字




## 匿名函式的壞處
1. 除錯會無法顯示發出錯誤訊息的函式名稱
2. 不好自行指定函式做些特定處理，比如對指定函式做記憶體釋放
3. 將函式物件分隔開來，以作後續維護開發，


接著函式命名方式會是表示panel被點擊時

例子： 假設要綁定一個事件處理器至dataPanel上的點擊事件，那麼可以透過函式名來當參數，

```
dataPanel.addEventListener('click', onPanelClicked)
```

並獨立宣告定義一個和參數名一樣的函式，其函式會是事件處理器的內容，而當點擊事件發生時，系統會預設將一個event 物件給函式onPanelClicked中的第一個參數

```
function onPanelClicked (event) {

}
// 預設會給onPanelClicked函式一個參數值
```

## Dataset 是種物件
1. 存放所有data-開頭的屬性和屬性值
2. 一個 HTML 屬性上可以包含多個 data set 屬性


## Img-fluid
1. fluid 為液體的意思，讓圖片像液體一樣，隨著容器而跟著變動其形狀、大小
2. img-fluid 是 bootstrap類別之一，會設定圖片元素的class="img-fluid"，讓圖片顯示尺寸擁有隨著螢幕(父元素)大小而變動的能力
3. img-fluid 樣式實際上是 max-width: 100% 和 height: auto，當螢幕寬度大到超過圖片原尺寸，那麼圖片會保持原來圖片的尺寸，若螢幕寬度小於圖片原尺寸，會讓圖片縮放至跟目前螢幕一樣的寬度或者跟著父元素縮放


## modal-size 決定 modal 視窗大小
1. 這裡提到的modal-size 和 modal皆為 bootstrap 框架的class
2. modal-size只對modal下的modal-dialog類別有效，而modal-dialog是視窗本身，兩者必須同時在一個class中，比如：

```
<element class=“modal-size modal-dialog”>
    context
</element>
```

3. modal-size中的-size可填入none(不填)、-sm、-lg、-xl，每個選項都代表該視窗的最大寬度：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1631765950/blog/temp/Class_jzxqka.png)





## 預設事件處理器
1. 瀏覽器會預設一些事件處理器來對某些元件下的某些事件，其處理器內容也是由瀏覽器來決定
2. 典型例子1: a元件的click事件，當點擊連結就會自動連向指定頁面
3. 典型例子2: form元件的submit事件，當按下代表提交事件的元件時，不論內容如何或者能否傳到指定頁面，都會自動換頁



## form的action屬性和method屬性
1. form是由標籤(label)、輸入欄(input)、按鈕(button)所組成，
2. action屬性是指定當form發生提交時，指定提交內容要傳到何處，例子：當提交時，會把資料傳至action_page.php當檔案的參數來處理

```
<form action="/action_page.php" method="get">
  <label for="fname">First name:</label>
  <input type="text" id="fname" name="fname"><br><br>
  <label for="lname">Last name:</label>
  <input type="text" id="lname" name="lname"><br><br>
  <input type="submit" value="Submit">
</form>
```
  

3. method 指定何種形式來傳提交方式，有GET和POST

一、透過 POST 傳遞資料
```
<form action="接收資料的 PHP 程式" method="post"></form>
```

二、透過 GET 傳遞資料
```
<form action="接收資料的 PHP 程式" method="get"></form>
```
4. 提交事件的發生會是由form內部具有type=submit屬性值的元件來決定，而通常只要對那個元件進行點擊，就發生submit事件，而當發生事件時，event object指向的target會是整個表格，而非那實際上被點擊的元件。
5. 若都正確設定action和method這兩個屬性，會將內容傳遞給指定位置，也就是action所指定的地方，若沒有設定action時，會自動導向回當前頁面

## preventDefault()
1. 是event object的方法，用來去掉/避免/預防event object對應元件所要做的預設處理器內容
2. 其方法可以任意放在指定事件的位置，可以是第一行

```
element.addListenerEvent(event, function(event) {
    event.preventDefault()
    // do something
})
```

也可是放在後頭

```
element.addListenerEvent(event, function(event) {
    
    // do something
    event.preventDefault()
})

```
不論位置如何，只要有放置方法，就會優先去掉/避免/預防預設處理器內容。

3. 但只是告訴瀏覽器不要做預設的事件處理器內容，不會停止事件傳遞

參考資料：

https://www.itread01.com/question/OG0xd3c=.html
https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault
Calling preventDefault during any stage of event flow cancels the event, meaning that any default action normally taken by the implementation as a result of the event will not occur.
