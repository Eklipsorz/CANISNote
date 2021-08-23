---
title: U35note
tags:
---

1. flex container內部可以允許另一個flex container
2. 對於flex-item，它還有一些有用的屬性:flex-basis、flex-grow、order
a. flex-basis: 以main-axis方向為主，來設定item在父容器上的初始長度

b. flex-grow: 指定一個item來根據其數字來調整自己的大小比例，其比例是對於在同一個容器上的其餘元素之間的大小比例。預設值是0，代表保持原來的大小比例，數字越大，item的大小越會比其他元素大。

c. order: 雖沒有flex的前綴字來表示其屬性是flex的，設定數字表示該item在父容器排列的順序，排列數字越小就放得越前面，越大就越後面。
