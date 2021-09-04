---
title: eventDrivenProgramming
tags:
---




一個事件(event)是指系統可辨識的行為，而行為則是指某種能和系統進行互動的具體動作，比如滑動、拖曳、點擊等等具體動作，當一個行為可被系統辨識時，代表著系統會透過發送某種信號來告知其他程式一個特定事件發生了或者某種行為發生了，這些接收到信號的程式可以做出某種反應來回應該事件的發生。


## 事件會是異步發生的
事件在電腦世界中是可被允許不需要等待其他行為或者某些系統處理來發生，換言之，事件想發生它就自然發生，並不會因為其他事情而耽誤或者得使它被迫等待。也就是如此，若要開發能接收信號並作出反應的程式，其程式必須要持續保持接收的狀態且不影響呈現其他子功能。


## 事件發生在哪

一個事件本身是一筆信號的傳送，當有很多筆信號進行傳送的同時，會有許多程式同時執行，比如呈現畫面上特定元件的程式、執行特定目的的程式等等，預設來說系統並不會讓他們接收到這些信號多花額外的時間來處理不必要的信號處理，但若某種程式的目的就在於這些信號的接收，那麼程式必須要先建立一個子程式去定時接收這些信號，並且判斷這些信號是不是真是自己所要的(比如是不是這些信號的發生座標是在特定元件中)，若是真的想要的信號，則會執行特定的信號處理，也就是事件處理。

## 簡介: 瀏覽器如何知道物件上發生事件


瀏覽器上的網頁會以網頁元件和使用者之間的互動為主，網頁元件指的是DOM節點，而互動則是使用者對著特定元件產生一系列的事件，使該元件能夠以特定的事件處理來回應使用者，比如點擊什麼元件跑出什麼畫面、拖曳什麼元件跑出什麼結果。

在這裡，只要使用者在瀏覽器中的任意可見範圍內產生事件，瀏覽器會利用Rendering前後所得到的資料(所有物件在畫面的實際座標、大小等等)來針對該事件所發生的地方或者座標進一步判斷事件是屬於何種元件的，通常當事件的來源處是發生在特定元件內部，那麼會被當作是該元件上的事件，比如鼠標點擊事件點擊到網頁元件，那麼網頁元件上的事件就是鼠標點擊事件。

然而，當元件上的事件發生時，預設上很有可能是什麼事都不會發生，更別說是回應該事件，因為大部分元件都不會綁定特定事件的事件處理器，所以我們必須手動建立代表事件處理器內容的函式物件以及透過JS所提供的語法將函式物件綁定在元件上的特定事件上，這樣子才會讓該元件碰上相同事件時去執行處理器內容(呼叫函式物件來執行)來回應事件。

## Event Flow


從"簡介: 瀏覽器如何知道物件上發生事件"小節中簡介了瀏覽器是如何判定事件是屬於哪些物件以及判定的基準，所以當使用者對網頁頁面內的一個元件進行互動時，瀏覽器會幫助使用者找到該元件並根據事件種類以及事先註冊好的事件處理器內容來回應使用者所產生的事件。

然而，如果使用者對著巢狀結構下的子元件來進行互動時，比如類似於程式碼中的元素3(element3)，那麼瀏覽器該如何判定這次的互動/事件是屬於哪個元素呢？瀏覽器大可直接根據事件是源自於哪裡來將事件歸類於element3，
```
<element1>
   <element2>
   	<element3>
		content
	</element3>
   </element2>
</element1>

```

可由於是巢狀關係(如下圖)，元素3(element3)被元素2(element2)所包含著，而元素2(element2)被元素1(element1)包含著，嚴格來說，當使用者對元素3(element3)做互動，同樣地也對著另外兩個元素進行互動，更甚至說包含這些元素的元素(比如body)也跟著互動。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630587482/blog/event/threeElements_lohr6c.png)


這時，瀏覽器可以有幾種選擇去決定事件是屬於哪個元件，第一種選擇是按照之前的規則，直接將事件歸類於元素3(element3)，另一種則是讓所有包含元素3的元素也跟著被當作是自己元件上的事件來觸發事件處理器，只是觸發的順序會按照所謂的事件流(event flow)來讓這些元件輪流被觸發，第二種因為後來的瀏覽器大戰而成名，所以主流上會是以第二種為主。



### Event flow是什麼

事件流(Event Flow)指的是在巢狀結構中接收並執行事件的順序，通俗一點就是就頁面上元件的回應事件順序，在這個架構上會在DOM中，把"包含實際發生事件N的元件X"的所有元件都當成發生事件N的元件，但實際上瀏覽器仍會判定該事件N是屬於元件X的，並且依照事件流的順序來發送(代表事件的)信號傳遞給這些元件，讓這些元件能夠去觸發自己對於該事件的事件處理器，傳遞順序上主要分為兩種：第一種為事件捕獲(Event capturing)，另一種為事件冒泡(Event bubbling)，在正式傳遞前，瀏覽器會利用"包含實際發生事件N的元件X"來找到所有元件並是先建立好傳遞路徑：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630598685/blog/event/propagationPath_ixsyik.png)

左邊是未建立路徑的DOM架構(包含了BOM根節點-Window)，右邊則是已建立路徑後的架構，其中被淺紅色選取上的元素則是被當成傳遞路徑，若去除掉剩餘沒被選上的元素，實際傳遞路徑會是：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630598661/blog/event/realPropagationPath_j7xf4k.png)

確定好路徑之後，傳遞順序將會以路徑上的節點進行。


#### 事件捕獲(Event capturing)

原始想法是由Netscape公司提出的概念，當某事件m發生在元素節點X時，會以最上層的元素(節點)為出發點往下傳遞信號。首先會先傳遞信號至Window節點，並試著執行該節點對應事件m的事件處理器內容，若沒有或者執行完畢就接著往下傳訊號給下個節點，而下個接收到信號的是Document節點，同樣地，再試著執行該節點對應事件m的事件處理器內容，若還是沒有或者執行完畢就接著傳訊號給下個節點，而下個節點是body節點，後續的信號傳播會一直傳送至實際發生事件m的元素節點X。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630598612/blog/event/eventCapturing_b480hr.png)

#### 事件冒泡(Event bubbling)

原始想法是由Microsoft公司提出的概念，其命名方式是以氣泡水中的氣泡皆會往上跑為命名，當某事件m發生在元素節點X時，會以實際發生事件的元素節點X往上傳遞信號。首先會先傳遞信號至元素節點X，並試著執行該節點對應事件m的事件處理器內容，若沒有或者執行完畢就接著往上傳訊號給下個節點，而下個接收到信號的是元素節點X的父元素節點，同樣地，再試著執行該節點對應事件m的事件處理器內容，若還是沒有或者執行完畢就接著傳訊號給下個節點，接收、執行內容、傳送信號這個動作會一直持續到整個文件的根節點。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630598612/blog/event/eventBubbling_r3nbai.png)

### 現今解法：對於巢狀關係的事件問題

直到現今，大部分瀏覽器仍採用於Event Flow的概念，甚至將兩種不同方向結合成新的Flow並分為三個階段，第一個階段為捕獲階段(Capturing Phase)，第二個階段為目標階段(Target Phase)，最後一個階段為冒泡階段(Bubbling Phase)，當使用者對某個元件X進行互動時，瀏覽器會先透過第一個階段來傳遞信號，接著就是第二個階段：將信號傳遞至實際發生事件/互動的元件X，最後就是第三個階段傳遞信號。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630599039/blog/event/currentPropagationPath_kopcrh.png)



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


### 移除特定事件的事件處理器

除了建立監聽器以外，我們還能透過以下語法來移除該特定元件element上的事件處理-handler，試著透過移除來獲取多餘的記憶體空間、避免記憶體洩漏問題，移除節點element上所發生的特定事件eventType和對應的事件處理器handler之間的綁定，該綁定必須是已經事先註冊好的才能移除，而useCapture若是true的話，就在capture phase
```
element.removeEventListener(eventType, handler, useCapture)
```

若考慮後續移除的問題，handler所儲存的函式物件必須是命名函式形式，若是匿名或者箭頭函式，反而會找不到對應的事件處理器來移除。



## Event Delegation

當我們想要在同一個元素1下的其中1個元素m增加一個事件處理器時，
```
<element1>
	.
	.
	<elementm>
		content
	</elementm>
	.
	.
</element1>
```

我們可以直接透過以下語法來實現，

```
elementm.addEvenetListener(event, function (value1) {
		// run event-driven content
})
```

可如果有更多來自於element1內部的元素想要自己的事件處理器時，這時你有幾種選擇，第一種就是手動增加事件處理器給每個元素，第二種就是透過for迴圈來給予，第三種則是在不替每個元素增加事件處理器的情況下，來透過基於event flow的事件委派(event delegation)來解決，而這也是在這個章節要討論的。


### Event delegation的概念是什麼

事件委派是一種將父元素element1被其內部的所有子元素委派去擔任他們的監聽器-listener，這個監聽器會負責接收發生在這些子元素上的所有事件，並幫他們執行他們所要有的事件處理器之內容或者幫助他們回應發生在他們身上的事件。換言之，element1本身會綁定事件處理器去監聽信號，而在element1之下的子元素則不綁定事件處理器，但是每當子元素發生事件的時候，都要讓父元素element1收到代表那事件的信號，且由父元素所綁定的事件處理器來回應事件。


### 如何實現概念

我們會利用Event Flow來實現，當事件x發生後，Event Flow會將所有包含發生事件x的元件都傳遞一遍，這剛好可以滿足事件委派的概念"傳遞信號至父元素element1進而執行父元素本身的事件處理器"，然而現今的Event Flow每遇到這狀況時，並不會單純把信號傳遞給父元素，而是按照三個階段來傳遞信號，每一種階段皆會傳遞按照順序輪流傳遞信號給元件們。

```
capture phase -> target phase -> bubbling phase
```

從這些階段來看的話，只有capture phase和bubbling phase這兩個階段能傳遞信號給父元素element1，但我們必須挑選一個合適的階段來進行，當然我們也都能挑兩個階段來處理，但這樣只是會重複引發2次以及2次對應事件的處理，多出一些不必要的花費，因此問題還是回歸原點-到底哪個階段比較合適？

在這裏我們有幾個考量點：第一，傳遞效能、第二，瀏覽器對於capture和bubbling的兼容性分別是如何，第三，這兩者的應用場景。不過我們先來考量第一個點，當我們將前面所提的三個階段合併成一個路徑圖，然後只看看capture phase和bubbling phase，在這張圖當中，傳遞信號會從capture phase開始一直到bubbling phase，若我們分別在這兩階段中的element1設定事件處理器去監聽的話，capture phase肯定會比較bubbling phase來得快，但這個快的前提必須建立在這兩個階段能合併成一個路徑，若瀏覽器本身只能從capture phase和bubbling挑選一個來傳遞信號的話，那麼bubbling肯定會比capture還快。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630741189/blog/event/captureAndBubbling_plctwq.png)

再來就是兼容性問題，capture phase對應著網景公司(Netscape)所提出的event capturing，而bubbling phase對應著微軟(Microsoft)所提出的event bubbling。網景在網景公司和微軟公司之間的瀏覽器大戰中落敗，使得微軟的IE瀏覽器市佔率是最高的(以當時大戰來說)，而當時的IE只支援event bubbling，它憑著自身來壟斷市場以及event flow的使用率，使開發者養成bubbling去思考event flow這件事，然後隨著瀏覽器市場被其他瀏覽器(如chrome, firefox)蠶食後，這壟斷現象才逐漸緩轉，直到今日，現今大部分知名且新版本的瀏覽器都支援著包含capture和bubbling這兩種event flow，但仍有些部份老舊的瀏覽器只支援一種event flow。

最後一種，這兩者的應用場景皆為不同，最主要是要看父子元素間彼此影響的程度來由誰來實現event delegation，假使父元素element1對於事件x的事件處理器代表a，而子元素對於事件x的事件處理器代表b，當a的執行結果會影響著b所代表的處理器執行內容時，會採用於capture phase來實現event delegation讓a先執行，隨後再執行b，因為若採用於bubbling phase讓b先執行，而a隨後執行，會因為a會更動b的執行內容而使預期結果不一致；反之，當b的執行結果會影著a所代表的處理器執行內容，會採用bubbling phase來讓b先執行，隨後再讓a去執行，否則若採用於capture phase，會使預期結果不一致。


從這三點來看，並沒有一定要用event capturing來實現event delegation或者一定要用event bubbling來實現event delegation，而是得根據自己所面臨到的開發目標、環境(瀏覽器、作業系統)來決定event delegation該用什麼來實現。



### 如何透過語法來實際操作基於event flow的事件委派



我們以一個清單來表示我們一直在討論的父元素element1，而它的子元素則是清單中的每一個項目，以這份清單和元素來說明是如何透過語法來實現事件委派，過程中我們將會按照事件委派的概念，不綁定事件處理器給任意子元素，只綁定一個事件處理器給父元素，也就是整份清單，同時進一步透過capture和bubbling這兩種不同方向的event flow來實現委派的功能。

首先，例子的結構會以HTML去呈現：
```
<!-- HTML 檔案 -->
<div class="m-5">
    <ul id="mylist" class="list-unstyled">
        <!-- display todos here -->
    </ul>
</div>
```

接著再以CSS去調整清單樣式，然後再額外替清單增加outline屬性來標示清單的範圍和大小：

```
/* CSS檔案 */
.fa {
  margin: 0 5px;
}

#mylist {
  outline: 2px solid black;
}


li>label[for='item'] {
  width: 150px;
}


```

最後再以JavaScript去填入那六個清單項目給那份清單中：

```
// JS檔案
// 獲取list父元素
let list = document.querySelector('#mylist')

// 定義資料
const listItem = ['listItem1', 'listItem2', 'listItem3', 'listItem4', 'listItem5', 'listItem6']
for (let item of listItem) {
  addItem(item)
}


// 用來添置項目的函式
function addItem (text) {
  let newItem = document.createElement('li')
  newItem.innerHTML = `
    <label for="item">${text}</label>
    <i class="delete fa fa-trash"></i>
  `
  list.appendChild(newItem)
}

```

網頁呈現的結果會是：黑框圍住的範圍是父元素本身，而內部的6個元素則是該父元素的子元素。
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630760897/blog/event/eventDelegationExample_hsxchq.png)






Question：
1. 瀏覽器到底怎判定元件的？
2. 若預設上每個元件都沒設置對應的事件處理，是否可以讓瀏覽器不做後續的事件判斷？

## 註解


4. addEventListener 具有兩點好處：1. 可綁定多個不同事件的事件處理器在同一個元件上，2. 觸發事件的元素和監聽對象的不必要是同一個，也就是具有事件委派的功能。

## 參考資料:

1. https://en.wikipedia.org/wiki/Event_(computing)
2. https://www.informit.com/articles/article.aspx?p=25856&seqNum=7
3. https://developer.mozilla.org/en-US/docs/Web/API/Event
4. https://gomakethings.com/whats-the-difference-between-javascript-event-delegation-bubbling-and-capturing/
5. https://www.zhihu.com/question/39474653
6. https://pjchender.dev/webapis/note-event-capturing-bubbling/
7. https://javascript.info/bubbling-and-capturing
