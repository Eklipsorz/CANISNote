---
title: Semester2-2_U24-U28
tags:
---

## 生存期(Lifetime)
1. 通常會用來描述變數、函式、儲存空間還留在記憶體的時間


## 作用域(Scope)：
1. 通常會用來描述變數、函式、儲存空間能夠被合法辨識的範圍


## localStorage
1. 由瀏覽器額外提供的儲存空間，每個瀏覽器所提供的空間都不同，但都是至少5MB的儲存空間
2. local指的是該快取只能讓client端瀏覽器本身存取到，不會讓其他主機存取到
3. 其空間用來存放key-value pair種類的內容，其中key代表著屬性的字串，而value則是代表著屬性值的字串
4. 利用瀏覽器會先於網頁檔案而執行，其提供的儲存空間只要能被允許存許，每個檔案皆能存取該儲存空間下的屬性和屬性值，所以只要某個檔案A對這空間增加屬性和屬性值，另一個檔案B就能存取A對localStorage所新增的屬性和屬性值。
5. lifetime：理論性該儲存空間會一直存在記憶體一段時間，除非人為的記憶體釋放，否則會一直允許程式碼放資料進去，但放不下會報錯
6. scope：只要在相同的網路協議(http/https)、相同的主機名、相同的埠下，就能讀取/修改到同一份localStorage資料
7. 應用：應用於購物車、選定語言
8. 可從chrome DEV : application->local storage   來讀取local storage的內容  

Unlike cookies, the storage limit is far larger (at least 5MB) and information is never transferred to the server.
Web storage is per origin (per domain and protocol). All pages, from one origin, can store and access the same data.


一般來說一份檔案的變數最多就只能存在整份檔案中，而且若執行完畢或者長時間沒在用該變數時，變數會直接被釋放掉，這時若有其他檔案想要存取該變數的話，那麼可以麻煩一直都會在執行的瀏覽器去儲存變數，而檔案們只要向瀏覽器索要就會拿到，瀏覽器能存這變數的地方叫做local storage

## sessionStorage
1. 是瀏覽器額外提供的儲存空間，該空間可存放資料
2. lifetime: session 表示某種特定活動的時期，在這裡只要關掉視窗或者瀏覽器，就會直接釋放掉該視窗或者瀏覽器下的sessionStorage
3. scope: 只要在相同的協議、相同的主機名、相同的埠下、同一個標籤(視窗)下，就能讀取/修改到同一份sessionStorage資料

其他描述：
生存期
localStorage理論上來說是永久有效的，即不主動清空的話就不會消失，即使儲存的資料超出了瀏覽器所規定的大小，也不會把舊資料清空而只會報錯。但需要注意的是，在移動裝置上的瀏覽器或各Native App用到的WebView裡，localStorage都是不可靠的，可能會因為各種原因（比如說退出App、網路切換、記憶體不足等原因）被清空。
sessionStorage的生存期顧名思義，類似於session，只要關閉瀏覽器（也包括瀏覽器的標籤頁），就會被清空。由於sessionStorage的生存期太短，因此應用場景很有限，但從另一方面來看，不容易出現異常情況，比較可靠。




參考資料：
https://5xruby.tw/posts/localstorage
https://www.itread01.com/p/685158.html
https://codertw.com/前端開發/384983/


## 對於localStorage的操作
1. 由於localStorage本身只能儲存key-value pair形式的字串，所以會利用本身符合key-value pair形式且皆以字串來表示的JSON格式來進行JS和localStorage之間的轉換。
2. 從JS的任意型別的資料轉換至JSON格式的字串，語法會是如下，value會是要轉換JSON格式的資料，會回傳JSON格式的字串
```
JSON.stringify(value)
```
3. 從JSON格式字串(原本有先經過第二點的流程)轉回 JavaScript 原生物件，其語法會是如下，text會是JSON格式的字串，會回傳轉回後的結果

```
JSON.parse(text)
```

4. 對localStorage進行新增/存入一個key-value pair形式的內容，語法為如下，key和value皆要以字串來表示，key代表屬性名稱，value會是代表對應key的屬性值。

若value只是單一值的話，可以直接轉成字串傳入。
```
localStorage.setItem(key, value)
```

但若value使多值的話，就要以JSON格式的字串來傳入。
```
localStorage.setItem(key, JSON.stringify(value))
```

5. 對localStorage進行特定屬性值的存取，其語法為如下，key要存取的屬性名稱，會回傳對應的屬性值，若key不存在會回傳null，另外若屬性值原本就是多值的話，其屬性值肯定是JSON格式的字串，要取出來讓JS正確使用的話，需轉化成JS原生型別/物件

若key對應的值是單一值：
```
localStorage.getItem(key)
```

若key對應的值是JSON格式的字串：
```
JSON.parse(localStorage.getItem(key))
```

6. 對localStorage進行特定屬性的移除，其語法為如下，key要移除的屬性名稱

```
localStorage.removeItem(key) 
```

## C = A || B 
可透過C = A || B 來減少if/else語法的增加，該運算符號會先執行A，若結果能被Boolean的隱性轉換下而成為true，則會停止，並把A內容指派給C，否則就繼續由B當C的指派內容，若兩者原本都是true的話，會優先選擇A來當C的指派內容


例子：當localStorage不存在favoriteMovies這屬性時，就會是空陣列，否則就是從localStorage存放的favoriteMovies屬性值，兩者若都能成立的話，則會左邊的favoriteMovies屬性值
```
const list = JSON.parse(localStorage.getItem('favoriteMovies')) || []
```


## 空陣列在boolean代表著true


## find 方法
1. 陣列的方法之一，會從陣列中尋找符合條件的第一個元素，找到會回傳該元素
2. 形式為以下，function是用來檢查陣列中的每個元素element是否為為想找的元素，當元素element能在function成立就會立刻回傳並指派內容給variable

```
let array = [var1, var2, ..... , varN]
let variable = array.find(function(element))

```

例子：
```
let numbers = [1, 2, 3, 4, 5, 6]
let newNumber = numbers.find((number) => number === 3)
console.log(newNumber)                                    //3
```

## some 方法
1. 陣列的方法之一，會從陣列中尋找符合條件的第一個元素，找到會回傳true，否則為false。
2. 形式為以下，function是用來檢查陣列中的每個元素element是否為為想找的元素，當元素element能在function成立就會立刻回傳true(找到符合function/條件的元素)，否則就是false（找不到符合function/條件的元素)

```
let array = [var1, var2, ..... , varN]
let variable = array.some(function(element))

```

3. some 方法和 find 類似，不過 some 只會回報「陣列裡有沒有 item 通過檢查條件」，有的話回傳 true ，到最後都沒有就回傳 false。


## findIndex 方法
1. 陣列的方法之一，會從陣列中尋找符合條件的第一個元素，找到會回傳該元素所在的索引值，否則為-1
2. 形式為以下，function是用來檢查陣列中的每個元素element是否為為想找的元素，當元素element能在function成立就會立刻回傳該元素所在的索引值。

```
let array = [var1, var2, ..... , varN]
let variable = array.findIndex(function(element))

```


## 箭頭函式，若只有一行程式碼可以縮減{}

```
const movie = movies.find(movie => movie.id === id)
```



## 優良命名方式：

1. 函式：藉由頁數來取得對應項目

```
function getMoviesByPage(page) {

  const startItemIndex = (page - 1) * MOVIES_PER_PAGE
  return movies.slice(startItemIndex, startItemIndex + MOVIES_PER_PAGE)

}

let items = getMoviesByPage(page)
```


2. 函式：根據資料內容來渲染主畫面

```
function rendeMovieList(data) {
  // render something
}

renderMovieList(movies)  // or renderMovie(filteredMovies)
```


3. 函式：移除指定id的電影

```
function removieFavoriteMovie(id) {
  // remove the movie
}
```

4. 全域變數的命名方式：可以全部大寫，方便認出該變數是否為全域

```
const MOVIES_PER_PAGE = 12
```

https://ithelp.ithome.com.tw/articles/10105993
