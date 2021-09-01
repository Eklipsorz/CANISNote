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

在這裡，只要使用者在瀏覽器中的任意可見範圍內產生事件，瀏覽器會利用Rendering前後所得到的資料(所有物件在畫面的實際座標、大小等等)來針對該事件所發生的地方或者座標進一步判斷事件是屬於何種元件的，通常當事件的來源處是發生在特定元件內部，那麼會被當作是該元件上的事件，比如鼠標點擊事件點擊到網頁元件，而該網頁元件上的事件就是鼠標點擊事件。

然而預設上，大部分的網頁元件是不存在對應事件

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

### How to bind handler to an event 
JavaScript提供了一些方法來將特殊函式物件綁定在特定事件，在這裡以DOM Level 2為主的方法來進行，其語法如下所示，主要是綁定元素節點element上所發生的某種事件eventType與特定事件處理器(函式物件)進行綁定，同時也利用useCapture來決定要在瀏覽器找到該節點的對應事件處理器時執行(該期間為Capture phase，註xx)/在瀏覽器找到節點且等開始進行
Bubbling phase

```
element.addEventListener(eventType, handler, useCapture)
```



1. 透過addEventListener方法(註xx)可以建立負責建立監聽事件的程式並綁定在元素element，其中eventType會以字串形式來表示要監聽何種事件(註xx)，而handler則是以函式物件來表示當事情發生時所要做的處理是什麼，最後的參數
A Boolean value that specifies whether the event should be executed in the capturing or in the bubbling phase. 

Possible values:
true - The event handler is executed in the capturing phase
false- Default. The event handler is executed in the bubbling phase


```
element.addEventListener(eventType, handler, useCapture)
```

當element上的特定事件eventType發生時，系統會直接執行函式物件handler的內容。


2. 透過以下語法來建立當事件發生時所要做的事件處理-handler，本身是函式物件，形式上可接受匿名、箭頭、擁有函式名稱等函式形式。但該函式物件所傳入的參數會被預設為第一個參數會接收一個事件物件event (event object，註xx)，該物件會儲存事件發生時的資訊，包括引發事件的元件是啥，比如該物件的屬性target會指向發生特定事件的物件，也就是引發handler處理的物件。

```
function funct1 (event) {
	do_something
}
```





除了建立監聽器以外，我們還能透過以下語法來移除該特定元件element上的事件處理-handler，
element.removeEventListener(event, handler, useCapture)

## 不建議的事件驅動






## 註解

1. 事件物件不同於元素節點物件、節點物件，單純就只是儲存"發生在DOM特定元件下"的事件所會有的資訊。
2. 常見的事件種類eventType:
- click：鼠標點擊(元素)
- mousemove：鼠標滑過(元素)
- mouseout：鼠標離開(元素)
- keydown：點擊且長按一個鍵時
- keyup：放開按鍵時

3. 通常特定元件下的事件就表示將

4. addEventListener


## 參考資料:

1. https://en.wikipedia.org/wiki/Event_(computing)
2. https://www.informit.com/articles/article.aspx?p=25856&seqNum=7
3. https://developer.mozilla.org/en-US/docs/Web/API/Event
