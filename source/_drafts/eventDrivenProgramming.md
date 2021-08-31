---
title: eventDrivenProgramming
tags:
---




一個事件(event)是指系統可辨識的行為，而行為則是指某種能和系統進行互動的具體動作，比如滑動、拖曳、點擊等等具體動作，當一個行為可被系統辨識時，代表著系統會透過發送某種信號來告知其他程式一個特定事件發生了或者某種行為發生了，這些接收到信號的程式可以做出某種反應來回應該事件的發生。


## 事件會是異步發生的
事件在電腦世界中是可被允許不需要等待其他行為或者某些系統處理來發生，換言之，事件想發生它就自然發生，並不會因為其他事情而耽誤或者得使它被迫等待。也就是如此，若要開發能接收信號並作出反應的程式，其程式必須要持續保持接收的狀態且不影響呈現其他子功能。


## 事件發生在哪
一個事件本身並不會
另外事件本身並不會被綁定在物件這詞上，但程式實作上會將事件與物件綁定在一塊，使該程式只關注於物件上的同種事件，換言之，當某個行為發生在該綁定物件，那麼




一個以某事件為驅動的程式，勢必會鎖定某些特定元件下的特定事件，然而一開始系統也並不會自動為這些元件建立負責監聽特定事件的程式以及定義當事件發生時，要做些什麼，在這裡我們得透過語法自行建立負責監聽事件的程式-listener 以及 當事件發生時所要做的事件處理-handler。


1. 透過以下語法可以建立負責建立監聽事件的程式並綁定在元素element，其中eventType會以字串形式來表示要監聽何種事件(註xx)，而handler則是以函式物件來表示當事情發生時所要做的處理是什麼，最後的參數
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
- keydown：(
- keyup：放開按鍵時





## 參考資料:

1. https://en.wikipedia.org/wiki/Event_(computing)
2. https://www.informit.com/articles/article.aspx?p=25856&seqNum=7
3. https://developer.mozilla.org/en-US/docs/Web/API/Event
