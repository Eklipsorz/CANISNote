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

舉例來說：當設定以下的HTML結構時，並且對flex-container表示flex元素時，class為flex-container的元素會變成flex-container，而內部名為flex-item的元素就變成flex-item元素。

```
<div class="flex-container">
  <div class="flex-item">1</div>
  <div class="flex-item">2</div>
  <div class="flex-item">3</div>
  <div class="flex-item">4</div>
</div>

```

設定完flex-container和flex-item之後，flex-item會按照flex系統所預設(預設設定flex-direction: row)的main-axis和cross-axis之座標軸來排列，其座標軸在預設的情況下，會是如以下圖，在這裡所有的flex-item會以main-axis來進行來進行從左至右的排列。
