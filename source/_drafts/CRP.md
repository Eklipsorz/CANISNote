---
title: Critical Rendering Path (一) 簡介
tags:
 - HTML
 - CSS
 - JavaScript
---


Critical Rendering Path 是瀏覽器如何將網頁檔案轉化成網頁的處理路徑，其路徑包含了Network、HTML轉換至DOM(Document Object Model)樹狀結構、CSS轉換至CSSOM(CSS Object Model)樹狀結構、DOM樹狀結構和CSSOM樹狀結構結合而成的Render Tree、Layout、Paint，每個路徑之間關係會如同下圖所示那樣。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629987931/blog/RenderingPath/Critical_Rendering_Path_ntcjvi.png)

## Network

當一個使用者開始透過URL來瀏覽網頁時，會試著解析URL對應的IP是誰，唯有知道IP是哪個伺服器負責處理網頁以及向誰發送"要求網頁檔案回傳過來"的請求。


而解析URL的流程主要流程為：
- 檢查瀏覽器本身的快取(Cache)是否有URL的對應IP，若沒有則繼續朝下一個目標找
- 檢查(執行目前的瀏覽器)作業系統的快取(Cache)是否有URL的對應IP，若沒有則繼續朝下一個目標
- 檢查離本地端較近的路由器(Router)是否有URL的對應IP，沒有朝下一個目標找
- 對ISP發送請求詢問它那邊的快取是否有對應IP，沒有朝下一個目標找
- 就開始針對ISP的DNS Server進行遞迴式搜查，直到找到對應IP

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629987931/blog/RenderingPath/Critical_Rendering_Path_ntcjvi.png)

當瀏覽器已經得知對應IP是什麼，那麼使用者(瀏覽器)會再重新對該IP來要求伺服器回傳網頁的對應檔(包含了HTML檔案、CSS檔案、JavaScript檔案)給使用者的瀏覽器，而回傳檔案的形式並不會一口氣以一個完整檔案傳過去，而是以固定大小的封包(Packet)形式將原檔案切分成好幾等分傳給使用者的瀏覽器來處理。

## When the browser receive 
這個小節將會以HTML、CSS來獨立描述它們在被接收時，瀏覽器會有什麼樣的表現，主要會有HTML FILE、CSS FILE這個部份。

### HTML FILE to DOM Tree
當瀏覽器收到HTML檔案被切分出來的封包時，瀏覽器不會直接等待完整檔案被拼湊出來，而是邊收邊將收到的內容按照DOM形式來建立一個DOM節點(註1)，每一個節點都各代表一個獨立的內容或者對應標籤，最後由這些節點按照HTML檔案所指示的巢狀結構來構成對應的樹狀結構，該樹狀結構被稱之為DOM Tree，拿下面的HTML程式碼來當例子的話：

```
<html>
  <head>
 	<link rel="stylesheet" href="style.css">
  </head>
  
  <body>
	<h1>This is an example</h1>
  	<p>Critical Rendering Path</p>
	<label>Hello World</label>
  </body>
</html>
```

在解析的過程中，會被轉化為以下樹狀結構：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629973153/blog/RenderingPath/domTreeExample_ep0cvp.png)

### CSS FILE to CSSOM

當瀏覽器收到CSS檔案被切分出來的封包時，瀏覽器會直接等待整個CSS檔案拼湊出來才開始解析，這是因為CSS屬性很容易被後續接收到的內容給覆蓋掉，甚至造成結構性的改變。當開始解析時，也會依據DOM的形式將CSS的類別、標籤、ID、內容獨立成節點來拼湊一個樹狀結構，而這個樹狀結構被稱之為CSSOM。

若以上面為例子來建立特定CSS樣式的話，其內容會是

```
p {
    text-align: center;
    padding: 5%;
    font-size: 2vw;
    border: 2px solid #000;
    color: #308D46;
    font-weight: bold;
}

h1 {
   text-align: center;
   font-size: 10vw;
}

label {
    display: none;
}

```

經過瀏覽器解析的話，其CSSOM會是：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629982746/blog/RenderingPath/cssomTreeExample_lbkboi.png)

### JavaScript  

在產生DOM和CSSOM之後，我們還可以透過JavaScript在Render Tree產生之前來變更DOM或者CSSOM的內容，假設一個HTML檔案內容為以下內容，後頭有個script包覆著的內容，其內容會是JavaScript的語法。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
   
    <title>Document</title>
</head>
<body>
        <h1>hi world</h1>
        <h3></h3>
        <script>
            document.getElementsByTagName("h3")[0].innerHTML = "a123"
        </script>
        
</body>
</html>

```
而其內容是變更原本沒內容的h3標籤元素：在這裡你可以看到內容會被指定為"a123"。

```
document.getElementsByTagName("h3")[0].innerHTML = "a123"
```

而當我們以瀏覽器來讀取整份檔案時，會在DOM Tree裡發現h3標籤元素所儲存的內容變更為"a123"，不再是無內容，從這邊展現出JavaScript可以在合併前影響著DOM和CSSOM

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629989767/blog/RenderingPath/result_javascript_within__html_ijz2jg.png)

若script部分程式碼是擺在h3元素定義之前的話，其script執行的結果會是無法改變h3元素內容。

## Render Tree
在經過解析而獲得DOM以及CSSOM之後，接著會根據兩者對應的標籤、類別、ID是否一樣來尋找同一個網頁元素進行合併，合併後的節點會以DOM節點的形式多增加一個子節點(如同下圖紅框中的節點)來表示父節點(網頁元素)要調整的樣式是為何。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629991053/blog/RenderingPath/newNode_renderTree_otmzal.png)

另外會根據該元素是否能夠正常在瀏覽器顯示來決定該元素是否存在於Render Tree，也就是說當元素本身設定為display: none的屬性時，該元素不會在這個階段挑選為合併後的結果，預設上有這設定的元素有html、head、link、body等元素，所以在合併結果上並不會看到它們。

我們繼續拿DOM和CSS提到的例子來為他們合併成一個Render Tree，在這裡你可以看到叉叉，而它表示著其元素本身是display: none的元素，所以無法成為最終合併後的結果，另外也由於body元素也被跟著剔除，所以會在最終結果上替合併後的新樹添加新的root元素，而在那下的每個節點都會有新加進來的屬性節點，這些節點會在後續paint程序為父節點增添樣式。
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629992018/blog/RenderingPath/renderTreeExample_lnh9md.png)




## 註解：
1. DOM (Document Object Model)，一種讓程式語言方便操作網頁元素的介面，其形式是將每一個標籤和內容都轉化為一個物件，最後再根據網頁結構的parent-child關係來重新將這些元件以樹狀形式來結合成一個DOM Tree，樹狀的每一個節點皆為前面所述的物件。






## Reference

1. 瀏覽器如何處理解析URL，https://dev.to/deepika_banoth/what-happens-when-i-type-a-url-in-browser-3i5o
2. 什麼是Critical Rendering Path，https://www.geeksforgeeks.org/critical-rendering-path-flow/
