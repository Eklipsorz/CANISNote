---
title: DOM vs. BOM - 樹狀結構簡介
tags:
 - HTML
categories:
 - Web Development
---

DOM是種樹狀結構的模型，其根節點是目前網站的檔案本身-document，而它的子節點會是html標籤，而html標籤下的子節點就是人人熟知的head節點和body節點，再往下細分的話，也就是分別為head內含的meta資料(註1)和body內含的實際網頁呈現資料。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630065451/blog/dom/domHierarchy_tpuaxj.png)


除了DOM以外，還有一種是為了能與瀏覽器本身進行互動的樹狀結構的模型-Browser Object Model，在DOM的基礎下將瀏覽器本身視為一個物件來允許其他語法與它互動，在這個模型下，其根節點是瀏覽器本身(window)，其子節點有DOM根節點-document、frames、history、location、screen，其中document節點子節點會接續著DOM剩下的內容。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630066487/blog/dom/bomHierarchy_kp1icw.png)

然而W3C還未對BOM進行嚴格的規範，基本上瀏覽器對於BOM的實現會有不一致的問題，不過大部分瀏覽器都支援BOM和DOM這兩套模型，當如果要調用DOM的節點時，可以不必從BOM的根節點開始調用，直接從DOM根節點就可以實現了，然而當要調用BOM的節點時，就必須直接從BOM根節點開始進行。

## 註解
1. meta資料指的是定義資料的資料，如同字面上的意思，在網頁裡是負責設定以及定義一些呈現規則、要載入哪些資料的文字內容。
