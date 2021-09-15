---
title: Semester2-2_U21-U23
tags:
---


## 透過JS來調用API的方式
1. 當使用某個Server提供Web API時，開發時盡量把Server名、不同種類的API、參數以變數的形式來分割開來，會比較好維護

比如説：
```
const BASE_URL = 'https://movie-list.alphacamp.io'
const INDEX_URL = BASE_URL + '/api/v1/movies/'
const POSTER_URL = BASE_URL + '/posters/'
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