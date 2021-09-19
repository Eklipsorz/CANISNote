---
title: Semester2-2_MovieList
tags:
---



## 收藏功能描述：
對某電影按下+之後，便會將該電影加入至收藏清單中，爾後點到收藏清單網頁時，便會以清單內容來渲染頁面，換言之，我們在那頁面上看到我們曾收藏的電影，在這頁面中，+按鈕會由x按鈕所代替，當我們按下x時，就會從收藏清單移除，接著重新渲染整個收藏的頁面。

在這裡我們切分三個部分來畫UML上的時序圖 (Sequence Diagram)：
1. 當我們在首頁按下+時，系統會做些什麼
2. 當我們進入收藏頁面時，系統會做什麼
3. 當我們在收藏頁面按下x時，系統會做些什麼



### 當我們在首頁按下+時，系統會做些什麼
在這邊的時序圖會用使用者、+按鈕、顯示資料的區塊Data-Panel、瀏覽器額外提供的儲存空間localStorage，當我們點擊+按鈕時，便會觸發由button所產生的事件委派，而被委派的元件會是Data-Panel，同時也會傳button本身的節點當作其參數，而該節點上存有對應電影的id。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1631868189/blog/temp/plusBtnClickedEvent_jadcab.png)


一開始，Data-Panel會先從localStorage取得最新的收藏資料，該收藏資料原本是以陣列的形式轉換成JSON格式字串存入localStorage，若沒有資料的話，就會拿到空陣列。

```
const array = JSON.parse(localStorage.getItem('favoriteMovies')) || []
```

接著會檢查陣列中是否存在button對應的電影ID，若存在的話，就會直接回傳錯誤訊息給使用者，也就是執行紅色部分
```
  if (array.some(item => item.id === id)) {
    return alert('此電影已在收藏清單中')
  }

```
但若不存在的話，則會執行藍色部分，內容會將對應ID放進陣列array中，並轉換成JSON格式的字串傳入localStorage
```
const movie = movies.find(movie => movie.id === id)

list.push(movie)
localStorage.setItem('favoriteMovies', JSON.stringify(list))
```

### 當我們進入收藏頁面時，系統會做什麼
在這邊的時序圖會用使用者、收藏頁面本身Favorite Website、瀏覽器額外提供的儲存空間localStorage，

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1631880445/blog/temp/favoriteLoadedEvent_oaatb0.png)

當我們讀取該頁面時，該頁面會立刻從localStorage取得收藏清單並轉成JS能讀取的陣列，若取得不到的話，會是空陣列，

```
const movies = JSON.parse(localStorage.getItem('favoriteMovies')) || []
```

接著在以該陣列的內容渲染頁面
```
renderMovieList(movies)
```


### 當我們在收藏頁面按下x時，系統會做些什麼

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1631867989/blog/temp/removeBtnClickedEvent_h8dhc0.png)



## 分頁器功能描述：
1. 當要顯示的內容太多時，會讓整體的讀取效能變差，因此使用pagination 來將指定顯示項目分割成指定數量的項目之集合，並將這些集合轉化成頁數，第一頁代表著0~N-1個項目，第二頁代表著N ~ 2N-1 個項目，後面依此類推。
2. 正是使用分頁器之前，會宣告每頁能放多少個項目，比如說以電影分頁來說的話，一頁會放12個電影
```
const MOVIES_PER_PAGE = 12
```

3. 分頁器開發主要有幾個注意要點，並以時序圖來表示
  - 當前的網頁是否要以分頁來顯示以及其頁數
  - 當點選分頁器時，會以點選的頁數來選特定項目
  - 若目前處在搜尋狀態時，顯示要以搜尋結果為主


### 當前的網頁是否要以分頁來顯示以及其頁數
在這邊的時序圖會用使用者、首頁、分頁器、顯示資料的區塊Data-Panel，當我們讀取首頁時，系統會立即利用API來獲取所有電影資料並放入陣列Array中，


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1631885051/blog/temp/indexLoadedEvent_auohbx.png)


接著利用該陣列的元素數量amount來渲染分頁器的總頁數，

```
/* 渲染分頁器，根據項目數量amount來決定渲染多少頁 */
function renderPaginator(amount) {

  const numberOfPages = Math.ceil(amount / MOVIES_PER_PAGE)
  let rawHTML = ''

  for (let page = 1; page <= numberOfPages; page++) {
    rawHTML += `
			<li class="page-item"><a class="page-link" href="#" data-page=${page}>${page}</a></li>
		`
  }

  paginator.innerHTML = rawHTML

}
```

最後在將資料區塊渲染成第一頁的特定項目，其中getMoviesByPage(1)會從movies取得第一頁的項目，然後再以那些項目來渲染

```
renderMovieList(getMoviesByPage(1))
```


### 當點選分頁器時，會以點選的頁數來選特定項目
在這邊的時序圖會用使用者、首頁、分頁器、顯示資料的區塊Data-Panel，當我們點擊分頁器上的頁數時，系統會立刻將被點擊的頁數指派給currentPage這變數，並判斷目前filteredMovies的元素數量來判斷目前是否正處于搜尋狀態，若處於搜尋狀態的話，那麼movies會是fileredMovies，否則就是原本的movies本身。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1631888199/blog/temp/paginatorClickedEvent_jwrbxt.png)

不論是何種，最後都會依造第一頁來渲染電影。



### 若目前處在搜尋狀態時，顯示要以搜尋結果為主
在這邊的時序圖會用使用者、搜尋用的輸入欄、搜尋用的提交按鈕、搜尋用的提交表單、分頁器、顯示資料的區塊(Data-Panel)，當我們在輸入欄輸入我們想找的電影名稱並按下提交按鈕時，會直接觸發表單的提交事件，接著該事件處理器內容會從輸入欄獲取值並放入keyword這變數，然後利用keyword來從movies裡找到符合的電影資料放入陣列filteredMovies，若陣列長度為0，就告訴使用者找不到，但若陣列長度大於0，就以filterMovies的資料來重新渲染頁數和當下所應該有的第一頁。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1631888735/blog/temp/submitClickedEvent_lznhkp.png)




### 補充

1. getMoviesByPage(page)，會回傳指定頁數的項目


```
function getMoviesByPage(page) {

	const startPageIndex = (page - 1) * MOVIES_PER_PAGE

	return movies.slice(startPageIndex, startPageIndex + MOVIES_PER_PAGE)

}
```


2. renderPaginator會根據amount大小來渲染多少個頁數

const paginator = document.querySelector(‘#paginator’)

function renderPaginator(amount) {
	
	const numberOfPages = Math.ceil(amount / MOVIES_PER_PAGE)
	let rawHTML = ‘’

	for (let page = 1; page <= numberOfPages; page++) {
		rawHTML += `
			<li class="page-item"><a class="page-link" href=“#” data-page=${page}>${page}</a></li>
		`
	}

	paginator.innerHTML = rawHTML
}