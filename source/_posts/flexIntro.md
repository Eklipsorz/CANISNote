---
title: Flex 容器簡介
date: 2021-08-17 23:08:38
tags:
 - JavaScript
---


Flex是種方便排版內容的系統，又別名為FlexBox，它是一維排版，也就是它對於元素的排列方向只會有水平或者垂直這兩個，可以透過屬性來決定它要使用哪種排列方向，但一次只能選一種座標軸來處理，不能像grid一次處理兩個方向，若要透過flex來調整元素至父元素的左下角，會分成兩次處理：第一個就是向左移動，第二就是向下移動，另一個例子就是透過展開元素大小至邊界，大小只能選擇一種方向來擴大。

通常適用場景為網頁局部性的排版，會設定parent元素為flex元素來控制其元素之下的child元素在內部的排版。另外grid則是二維排版，適用於頁面的整體佈局，主要是偏向RWD。

## Flex Container 和 Flex item

```
display: flex;
```

該元素會變成flex-container，而原本被這個元素包含的子元素會變成flex-item，而flex-container和flex-item的樣式若沒特別設定的話，會依照系統給定的flex預設樣式來做變動。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629213605/blog/cssTag/flexElement_hei4op.png)

舉例來說：當設定以下的HTML結構時，並且對flex-container表示flex元素時，class為flex-container的元素會變成flex-container，而內部名為flex-item的元素就變成放置容器的flex-item元素。

```
<div class="flex-container">
  <div class="flex-item">1</div>
  <div class="flex-item">2</div>
  <div class="flex-item">3</div>
  <div class="flex-item">4</div>
</div>

```

設定完flex-container和flex-item之後，flex-item會按照flex系統所預設(預設設定flex-direction: row)的main-axis和cross-axis之座標軸來排列，其座標軸在預設的情況下，會是如以下圖，在這裡所有的flex-item會以main-axis來進行來進行從左至右的排列。


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629300747/blog/cssTag/AxisOfRowVersion_ibcxt9.png)

圖中所有的藍色代表著跟main-axis座標軸相關的事物，而所有黃色代表著跟cross-axis座標軸相關的事物，圓點代表著該座標軸的起點，而箭頭跟線呈現放置的方向，比如藍箭頭向右代表著若item以main-axis為主來放置的話，會從左至右來排列，黃線依此類推。

另外就是每個座標軸都有各自的起點和終點，main-axis座標軸的起點在最左邊，而他的終點為最右邊；cross-axis座標軸的起點在最上邊，而他的終點為最下面


另外當flex-container存不下接下來的item時，會先試著壓縮其他item的大小來放入新的item，然而若壓縮到無法再放時，便會超出container的範疇。

## main-axis更動

我們可以透過flex-direction屬性來更動main-axis的方向是橫向或者直向，它的屬性值：

```
flex-direction: row | row-reverse | column | column-reverse
```

預設上會以row為主，也就是main-axis和cross-axis這兩個定義會是上面章節所提到的，可若是flex-direction是row-reverse的話，main-axis座標軸會被反轉，而cross-axis座標軸則維持原本的方向：


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629300746/blog/cssTag/AxisOfRowReverseVersion_s5lqgj.png)

flex-direction更改為column的話，main-axis座標軸會變成從上至下，也就是main-axis就會是原本的cross-axis，而cross-axis會變成原本的main-axis：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629300747/blog/cssTag/AxisOfColumnVersion_ne5hlr.png)

flex-direction更改為column-reverse的話，除了main-axis座標軸會變成從下至上以外，其餘皆和column的情況相同：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629300746/blog/cssTag/AxisOfColumnReverseVersion_q09vug.png)


## 向cross-axis座標軸進行對齊：

透過align-item語法來讓元素依照flex-direction所指定的cross-axis來位移元素，且flex本身並不會讓每個元素上有間隔，預設上會以stretch為主，若元素有指定大小的話，會依照其指定大小為優先，而不執行stretch。

align-items: stretch | flex-start | flex-end | center

