---
title: U38note - 將 Bootstrap 導入專案
tags:
---

1. Bootstrap主要提供現成的CSS架構、現成的JavaScript架構、jQuery、Popper，導入方式是透過其BootStrapCDN網址進行導入

2. 如何導入：

a. 內容有head元件的話，

- 先在head套入bootstrap的css:
```
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/css/bootstrap.min.css" integrity="sha384-B0vP5xmATw1+K9KRQjQERJvTumQW0nPEzvF6L/Z6nronJ3oUOFUFpCjEUQouq2+l" crossorigin="anonymous">
```

- 套入bootstrap的js: 載入順序為jQuery、proper、bootstrap本身的js，系統會由上往下讀取，所以必須要按照順序來放
```
<script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/js/bootstrap.min.js" integrity="sha384-+YQ4JLhjyBLPDQt//I+STsc9iw4uQqACwlvpslubQzn4u2UU2UFM80nGisd026JF" crossorigin="anonymous"></script>

```
b. 內容沒有head元件，類似codepen那樣得另外載入，則按照對應的CDN網址傳遞給他，同樣地順序必須是按照a方法那樣。

note:
1. jQuery為一套JavaScript函式庫，能夠簡化HTML與JavaScript之間的操作，BootStrap的JavaScript部分功能依賴其jQuery。

2. Popper 主要提供特效的工具

3. CDN (Content Delivery Networks)，中譯為內容傳遞網路，透過其技術把檔案內容放到伺服器，開放任何人透過快速存取，不用透過本地端的檔案進行載入
