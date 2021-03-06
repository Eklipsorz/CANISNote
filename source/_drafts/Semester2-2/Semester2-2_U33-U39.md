---
title: Semester2-2_U33-U39
tags:
mathjax: true
---


## MVP (Minimum Viable Product)
用最低的(開發)成本來設計和實現產品


## 封裝(Encapsulation)
1. 封裝的目的： 將繁複的處理合併成特定功能的函式並開放給外部使用，隱藏其內部的函式則只能透過該函式才能調用，防止其他程式碼透過存取而變動該實作或者變數，進而跑出預期外的結果
2. 它可以帶來：
 - 因為只有幾個函式才能呼叫內部分的函式，這樣子的區分會比較容易理解和維護
 - 同時因為這點，可以藉由限制外人不得存取內部函式以及讓開放外部的函式不會輕易修改內部，而獲得程式碼的安全性

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1632032433/blog/temp/encapsulation_yv0bvf.png)


## MVC (Model-View-Controller)
1. 是一種軟體開發方法之一，將程式碼依照功能性來區分出三塊，分別為Model、View、Controller
2. Model負責定義資料以及對資料的處理方法，View負責定義畫面顯示，而Controller則是負責與使用者互動的邏輯，也是應用程式收發 request/response 的核心
3. 在JavaScript實現上，會宣告三種物件來封裝/分類相關的程式碼。

```
const model = {
  // 和資料有關的程式碼
}

const view = {
  // 和介面有關的程式碼
}

const controller = {
  // 和流程有關的程式碼
}
```


原文：
Model：Model 常譯為「模型」，負責和資料庫溝通
View：View 常譯為「視圖」，View 所管理的功能層叫作「表現層 (presentation layer)」，顧名思義是負責管理畫面的呈現，也就是 HTML 樣板 (template)。
Controller：Controller 常譯為「控制器」，它掌握使用者互動邏輯，也是應用程式收發 request/response 的核心。來自路由的 request 會先被送到 Controller，再由 Controller 通知 Model 調度資料，並且把資料傳遞給 View 來產生樣板 (template)，並將呈現資料的 HTML 頁面回傳給客戶端。

https://railsbook.tw/chapters/10-mvc.html


## flex-basis
1. CSS 屬性值，只能在flex元素下的子元素上增加其屬性以及屬性值，預設值為0
2. 調整flex元素下的子元素(flex item)在主軸上的初始大小
3. 當主軸設定row時，就會控制寬度/x軸，當主軸設定column時，就會控制高度/y軸，其值並不會受到box-model所影響
4. 形式上會是以下，number可以填入比例或者數字，而auto則是依據對應元素上的box model來決定

```
flex-basis: number | percent |auto 
```



## flex-grow 
1. CSS 屬性值，只能在flex元素下的子元素上增加其屬性以及屬性值，形式上只允許填入數字，預設值為0
2. 當一個flex容器放完子元素之後仍還有空間可以放置其他子元素，該屬性值會告訴系統這些子元素是否佔滿以及佔滿比例為何
3. 在同一個容器下的子元素會按照以下公式來擴展自己在主軸上的大小：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1631981301/blog/temp/flex-grow_calculation_bzggvi.png)



例子1：
```
<div class="items">
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
</div>
```


```
.items {
  display: flex;
  border: 2px solid #e0e0e0;
  justify-content: space-around;
}

.item {
  height: 100px;
  flex-basis: 100px;
}

.item:nth-child(1) {
  background-color: #5c6bc0
}

.item:nth-child(2) {
  background-color: #d4e157;
  flex-grow: 2;
}

.item:nth-child(3) {
  background-color: #ffca28;
  flex-grow: 1;
}
```

參考資料：
https://www.samanthaming.com/flexbox30/22-flex-grow-calculation/

## flex-shrink
1. CSS 屬性值，只能在flex元素下的子元素上增加其屬性以及屬性值，形式上只允許填入數字，預設值為1
2. 當一個flex容器放完子元素之後且其子元素超出容器所能容納的範圍時，我們可以設定flex-shrink來按比例縮小這些被設定屬性的子元素
3. 當flex container裝不下他的子元素的話，會出現shrunk space(被壓縮空間)，這空間會讓子元素超出父容器所能放的大小，為了能讓這些子元素能夠完整被放入父容器，會以多出來的空間來按這些子元素所佔的大小比例來扣除。flex-shrink 預設為 1

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1631981301/blog/temp/flex-shrink_calculation_x0e9pf.png)


例子：
https://codepen.io/KuanLin/pen/QWWZvKY





## flex 
1. CSS 屬性值，一次可設定flex-basis、flex-grow、flex-shrink這三個值
2. 形式為以下，第一個值代表著flex-grow，第二個值代表著flex-shrink，第三個值則代表著flex-basis
3. flex-shrink 和 flex-grow 讓你可以在設計 RWD 佈局時，在 width 固定的情況下，進行更深入的控制。
```
flex: flex-grow flex-shrink flex-basis;
```

參考資料：
https://zhuanlan.zhihu.com/p/39052660
https://cythilya.github.io/2017/04/06/flexbox-advance/

## align-self
1. CSS 屬性值，只能在flex元素下的子元素上增加其屬性以及屬性值
2. 調整flex容器下的特定子元素之排列，如同align-items會以cross axis來調整，只是不一樣的地方在於align-self只會調整被設定的元素



## vw、vh
1. 一種大小的表示法或者單位，告訴系統被套用的元件其大小來按照視窗大小來調整
2. 形式上會是nvw、nvh，n為數字，nvw代表著元件的寬度以視窗寬度的n％來呈現，而nvh則是代表元件的高度以視窗高度的n%來呈現

參考資料：
https://pjchender.blogspot.com/2015/04/css-3vh-vw.html



## transform
1. CSS 屬性值，只能填入none或者transform function
2. 能調整元件如何旋轉、如何傾斜、如何縮放


## transform function
1. 它是css function之一
2. 回傳值會通常會以矩陣或者數學式來表示
3. 用途只能當transform的屬性值

參考資料:
https://css-tricks.com/get-value-of-css-rotation-through-javascript/



## rotate(a)
1. 它是css transform function之一
2. 會回傳代表著翻轉指定角度的數學式或者矩陣，其中a代表著角度數，若要指定180度，那麼a就會是180deg，整體而言會是

```
selector {
  transform: rotate(180deg);
}
```


## pseudo class
1. 當元件發生特定狀態時，會產生並依照另一種不存在CSSOM的類別來渲染該狀態下的樣式，而這個類別卻像是一般類別那樣能夠正常發揮作用，換言之
CSS而言，它並不存在的，但當特定狀態發生時就會產生其選擇器並依照其選擇器的樣式來修改該類別下的元件，這就是為啥稱作為偽類

## :first-child
1. 是一種偽類(pseudo-class)
2. 形式上會是如下，它會先找到每一個容器下的第一個元素，接著再看看這些元件是否滿足selector，都滿足才以下面的類別來渲染樣式。

```
selector:first-child {
  // some properties and their values
}

```


例子： 


CSS內容：
```
p:first-child {
  background-color: yellow;
}
```

HTML內容：
```
<p>This paragraph is the first child of its parent (body).</p>

<h1>Welcome to My Homepage</h1>
<p>This paragraph is not the first child of its parent.</p>

<div>
  <p>This paragraph is the first child of its parent (div).</p>
  <p>This paragraph is not the first child of its parent.</p>
</div>
```


它會從HTML檔案內容找到每一個容器下的第一個子元素，分別為body下的第一個子元素以及div容器下的第一個元素，接著再看看他們是否滿足selector所指定的，而selector要求的元件是p，這些子元素剛好也都是p，所以滿足並渲染成黃背景。

```
<p>This paragraph is the first child of its parent (body).</p>
<p>This paragraph is the first child of its parent (div).</p>
```


## :last-child
1. 是一種偽類(pseudo-class)
2. 形式上會是如下，它會先找到每一個容器下的最後元素，接著再看看這些元件是否滿足selector，都滿足才以下面的類別來渲染樣式。

```
selector:last-child {
  // some properties and their values
}

```
