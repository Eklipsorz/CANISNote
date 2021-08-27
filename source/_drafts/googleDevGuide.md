---
title: How to use chrome dev to debug
tags:
 - Google
categories:
 - Web Developement
---


1. How to show current DOM

只要在chrome瀏覽著自己想要看的網頁，並對著他右鍵檢查，就能從Elements欄位那邊看到目前DOM內容，比如說若想看以下HTML檔案內容在解析之後會有什麼樣DOM內容的話，
```
<html>
<body>
    <h1>Hello, World!</h1>
    <p class="class1 class2" id="id1">
             <!-- TEST COMMENT -->
            This is a <em>simple</em> website.
           <h3></h3>
           <script>
               document.getElementsByTagName("h3")[0].innerHTML = "hi everyone!!"
           </script>
    </p>
    
</body>
</html>

```
可以對它按右鍵檢查去從Elements那欄位看：你可以看到解析後的h3元素會因為javascript在合併render tree之前就先替h3內容增加"hi everyone!!"這個文字節點。
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630070697/blog/dom/currentDOM_viaElement_w5odr2.png)



2. How to look up the style (CSSOM) of the element 
只要在chrome瀏覽著自己想要看的網頁，並對著他右鍵檢查，再點擊以下按鈕，
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630071414/blog/dom/selectElement_oxy0q4.png)

接著你再點擊你想看的元素就能在styles那邊看到該元素對應的(解析後)樣式:

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630071300/blog/dom/styleOfTheElement_gblqxg.png)



3. How to run javascript in the current frame
只要在chrome瀏覽著自己想要看的網頁，並對著他右鍵檢查，然後到console欄位就能下達javascript指令，預設上可支援BOM和DOM這兩種模型，另外由於window在javascript設定上是全域(Global Object)物件，若沒有額外指示方法或者屬性是哪種節點(物件)的話，預設會認為是window下的屬性或者方法：

比如以下兩種：
- window.alert() 等於 alert()
- window.document 等於 document


