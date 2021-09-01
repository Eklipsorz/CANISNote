---
title: eventDrivenProgramming
tags:
---




一個事件(event)是指系統可辨識的行為，而行為則是指某種能和系統進行互動的具體動作，比如滑動、拖曳、點擊等等具體動作，當一個行為可被系統辨識時，代表著系統會透過發送某種信號來告知其他程式一個特定事件發生了或者某種行為發生了，這些接收到信號的程式可以做出某種反應來回應該事件的發生。


## 事件會是異步發生的
事件在電腦世界中是可被允許不需要等待其他行為或者某些系統處理來發生，換言之，事件想發生它就自然發生，並不會因為其他事情而耽誤或者得使它被迫等待。也就是如此，若要開發能接收信號並作出反應的程式，其程式必須要持續保持接收的狀態且不影響呈現其他子功能。


## 事件發生在哪

一個事件本身是一筆信號的傳送，當有很多筆信號進行傳送的同時，會有許多程式同時執行，比如呈現畫面上特定元件的程式、執行特定目的的程式等等，預設來說系統並不會讓他們接收到這些信號多花額外的時間來處理不必要的信號處理，但若某種程式的目的就在於這些信號的接收，那麼程式必須要先建立一個子程式去定時接收這些信號，並且判斷這些信號是不是真是自己所要的(比如是不是這些信號的發生座標是在特定元件中)，若是真的想要的信號，則會執行特定的信號處理，也就是事件處理。

## How to identify which element has occurred an event

瀏覽器上的網頁會以網頁元件和使用者之間的互動為主，網頁元件指的是DOM節點，而互動則是使用者對著特定元件產生一系列的事件，使該元件能夠以特定的事件處理來回應使用者，比如點擊什麼元件跑出什麼畫面、拖曳什麼元件跑出什麼結果。

在這裡，只要使用者在瀏覽器中的任意可見範圍內產生事件，瀏覽器會利用Rendering前後所得到的資料(所有物件在畫面的實際座標、大小等等)來針對該事件所發生的地方或者座標進一步判斷事件是屬於何種元件的，通常當事件的來源處是發生在特定元件內部，那麼會被當作是該元件上的事件，比如鼠標點擊事件點擊到網頁元件，那麼網頁元件上的事件就是鼠標點擊事件。

然而，當元件上的事件發生時，預設上很有可能是什麼事都不會發生，更別說是回應該事件，因為大部分元件都不會綁定特定事件的事件處理器，所以我們必須手動建立代表事件處理器內容的函式物件以及透過JS所提供的語法將函式物件綁定在元件上的特定事件上，這樣子才會讓該元件碰上相同事件時去執行處理器內容(呼叫函式物件來執行)來回應事件。

## 如何綁定事件處理器至特定事件
 
在這裡以DOM Level 2 (註xx) 為主的方法-addEventListener (註xx) 來進行，其語法如下所示，主要是綁定元素節點element上所發生的某種事件eventType與特定事件處理器handler(函式物件)進行兩者間的綁定註冊，同時也利用useCapture來告訴瀏覽器當觸發時何時執行，若是true的話，則會在capture phase階段執行；若是false的話，則是在bubbling phase，預設沒填的話會是false。

```
element.addEventListener(eventType, handler, useCapture)
```

eventType得放入字串，用來代表要將處理器對應至何種事件，常見事件有：

- 'click': 鼠標點擊元素
- 'mousemove': 鼠標滑過元素
- 'mouseout':  鼠標離開元素 
- 'keydown': 點擊且長按一個鍵時
- 'keyup': 放開按鍵時
- 'submit': 提交表單時
- 'focus': 點擊某個輸入框時
- 'input': 輸入框內容改變時
- 'DOMContentLoaded': 當 HTML 下載完成並完整的建立 DOM 模型時觸發

其中'click'、'mousemove'、'mouseout'是滑鼠會產生的事件，'keydown'、'keyup'則是鍵盤會產生的事件，'submit'、'focus'、'input'是瀏覽器上的表單事件，'DOMContentLoaded'則是瀏覽器本身的事件，用來避免HTML下載不完全的問題。

而函式物件hander的第一個參數在瀏覽器中會接收一個事件物件(event object，註xx)，該物件儲存事件發生時的資訊，包括引發事件的元件是啥，比如該物件的屬性target會指向發生特定事件的物件，也就是引發handler處理的物件。

```
function funct1 (event) {
        do_something
}
```

最後當element上的特定事件eventType發生時，系統會直接執行函式物件handler的內容，另外這裏this變數會是呼叫者-發生特定事件的物件。

### 多個 element.addEventListener 在不同參數下的表現

在這小節中，我們將以參數相同數來觀察其方法的表現，而使用的語法會是：

```
element.addEventListener(eventType, handler, useCapture)
```

1. 當多個事件綁定方法中的eventType、handler、useCapture皆一樣時，只能留下一個事件綁定
2. 當多個事件綁定方法中的eventType、handler皆一樣且useCapture皆不一樣時，只會留下兩個事件綁定分別為capture 階段和bubbling 階段，這是因為這兩個階段下的執行時機點皆為不同。
3. 其餘參數的可能性皆視為獨立事件的綁定。

### 另一種綁定事件處理器的方法

在早期，HTML標籤存在著一種可以綁定事件處理器的屬性，比如反應滑鼠點擊事件的onclick，而其屬性值是填入代表事件處理器的函式物件，該物件需要另外加載存有該函式物件的JavaScript文件才能正常執行，而語法會是如下所示，其中property為特定事件的對應屬性名，而handler則是以字串傳入函式名稱。

```
property="handler()"
```

在標籤的呈現上會是：

```
<element property="handler()"> </element>
```

以input和onclick為例的話，input為代表能填入文字的文字區塊或者按鈕，在這裡會被當成按鈕來使用，但按鈕被點擊時，便會按照onclick所指示的事件處理器去執行其內容。

```
<input value="Click me" onclick="greeting()" type="button">
```

在標籤上利用屬性來綁定事件處理器，雖會帶來直觀上的理解以及因語法過於老舊而具有一定容錯率，但具有兩個主要缺點，第一個當存有函式物件(事件處理器)的JavaScript文件太慢加載的話，會因為函式物件不存在而在觸發事件的時候回報錯誤，第二個缺點則是因為內容/結構/事件不能獨立分開(比如HTML語法和JavaScript相關語法不能以不同檔案來分開、負責事件處理的程式碼不能完全存放在JavaScript上)而造成開發維護上的困難以及可讀性很差。


## 移除特定事件的事件處理器

除了建立監聽器以外，我們還能透過以下語法來移除該特定元件element上的事件處理-handler，試著透過移除來獲取多餘的記憶體空間、避免記憶體洩漏問題，移除節點element上所發生的特定事件eventType和對應的事件處理器handler之間的綁定，該綁定必須是已經事先註冊好的才能移除，而useCapture若是true的話，就在capture phase
```
element.removeEventListener(eventType, handler, useCapture)
```

若考慮後續移除的問題，handler所儲存的函式物件必須是命名函式形式，若是匿名或者箭頭函式，反而會找不到對應的事件處理器來移除。



## Event Flow

上述提到瀏覽器可以透過自身機制來判斷某事件是屬於某元件上，但如果考慮到事

藉由前面所述來判斷某物件發生


接著利用這些資訊從BOM的根節點-window節點，若不符合的話，則會往DOM的根節點-document，若還是找不到則繼續往下層-body或者body之下的節點，直到找到符合(信號帶有的)資訊的節點，該節點就會被瀏覽器當作發生事件的節點。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630479314/blog/event/capturePhase_tg6oec.png)

當找到時，瀏覽器便檢查該節點是否有對應事件/信號的事件處理器-handler，若有的話，便會直接執行其處理器內容。預設情況下，網頁元件一開始並不會有任何處理器來綁定任意事件種類，必須透過JS來進行綁定。而這種從上往下找節點
capture phase
bubbling phase

Question：
1. 瀏覽器到底怎判定元件的？
2. 若預設上每個元件都沒設置對應的事件處理，是否可以讓瀏覽器不做後續的事件判斷？

## 註解


4. addEventListener 可綁定多個不同事件的事件處理器在同一個元件上，

unknown
觸發事件的元素和監聽對象的不必要是同一個

## 參考資料:

1. https://en.wikipedia.org/wiki/Event_(computing)
2. https://www.informit.com/articles/article.aspx?p=25856&seqNum=7
3. https://developer.mozilla.org/en-US/docs/Web/API/Event
