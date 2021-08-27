---
title: DOM vs. BOM - 樹狀結構簡介
tags:
 - HTML
categories:
 - Web Development
---

DOM是種樹狀結構的模型，其根節點是目前網站的檔案本身-document，而它的子節點會是html標籤，而html標籤下的子節點就是人人熟知的head節點和body節點，再往下細分的話，也就是分別為head內含的meta資料(註1)和body內含的實際網頁呈現資料。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630065451/blog/dom/domHierarchy_tpuaxj.png)


除了DOM以外，還有一種是為了能與瀏覽器本身進行互動的樹狀結構的模型，其根節點為瀏覽器本身(window)，

瀏覽器本身(window)，再由它細分好幾個子節點，比如目前讀取的HTML檔案本身-document、frames、history、location、navigator、screen，





## 註解
1. meta資料指的是定義資料的資料，如同字面上的意思，在網頁裡是負責設定以及定義一些呈現規則、要載入哪些資料的文字內容。
