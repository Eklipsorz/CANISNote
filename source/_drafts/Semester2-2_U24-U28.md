---
title: Semester2-2_U24-U28
tags:
---



## 收藏：
對某電影按下+之後，便將該電影添加至一個陣列中，接著再以該陣列內容重新渲染一次，讓使用者只看到事件後的渲染結果
但若按下+的頁面和顯示最愛電影的頁面是不同的話，那麼陣列就必須多存在localstorage，來讓這兩個頁面都能存取該陣列來顯示，這裡會有幾種結果：






## C = A || B 
可透過C = A || B 來減少if/else語法的增加，該運算符號會先執行A，若結果能被Boolean的隱性轉換下而成為true，則會停止，並把A內容指派給C，否則就繼續由B當C的指派內容，若兩者原本都是true的話，會優先選擇A來當C的指派內容


例子：當localStorage不存在favoriteMovies這屬性時，就會是空陣列，否則就是從localStorage存放的favoriteMovies屬性值，兩者若都能成立的話，則會左邊的favoriteMovies屬性值
```
const list = JSON.parse(localStorage.getItem('favoriteMovies')) || []
```


## 空陣列在boolean代表著true


## find 方法
1. 陣列的方法之一，會從陣列中尋找符合條件的第一個元素
2. 形式為以下，function是用來判定陣列中的每個元素element，當元素element能在function成立就會立刻回傳並指派內容給variable

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

## 



## 箭頭函式，若只有一行程式碼可以縮減{}

```
const movie = movies.find(movie => movie.id === id)
```