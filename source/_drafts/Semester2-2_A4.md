---
title: SemesterA4
tags:
- JavaScript
---


## data-toggle:
1. 點擊或者被挑選時，會額外搭配其他裝飾在被點擊的元件上
2. 這是bootstrap特定語法
3. data-開頭 皆為html5可自訂的屬性

[連結](https://www.geeksforgeeks.org/data-toggle-attributes-in-twitter-bootstrap/)

原文：The data-toggle is an HTML-5 data attribute defined in Bootstrap. The advantage of using this is that, you can select a class or an id and hook up the element with a particular widget. For example, if you select an element and give the property of data-toggle as “collapse”, you’re basically making your div collapsible in just minutes by using Bootstrap.  



## role:
1. html5 語法
2. 當現有的HTML標籤不能充分表達語義性的時候，可以用role來說明該元件是什麼，通常這種情況出現在一些自定義的組件上，這樣可增強組件的可訪問性、可用性和可交互性。

[連結](https://kknews.cc/tech/59y8358.html)


## <pre> 標籤：
會以實際在標籤內部的內容(空白、換行)來呈現

呈現結果會是以html檔案的文字、排版
 是用來保存原始文字內容的格式 (preformatted text)，意思是文字內容中的空白、換行 (whitespace) 都會被保留下來顯示，



```
<pre>
  L          TE
    A       A
      C    V
       R A
       DOU
       LOU
      REUSE
      QUE TU
      PORTES
    ET QUI T'
    ORNE O CI
     VILISÉ
    OTE-  TU VEUX
     LA    BIEN
    SI      RESPI
            RER       - Apollinaire
</pre>


```

結果：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1631549632/blog/semester2-2/resultOfPre_acswhb.png)

原文：
The <pre> HTML element represents preformatted text which is to be presented exactly as written in the HTML file. The text is typically rendered using a non-proportional, or "monospaced, font. Whitespace inside this element is displayed as written.



## trim 可以清掉首尾的空白
當輸入"   "這字串，內容為3個空白時，可透過trim轉換成""



