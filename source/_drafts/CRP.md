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
當瀏覽器收到HTML檔案被切分出來的封包時，瀏覽器不會直接等待完整檔案被拼湊出來，而是邊收邊將收到的內容按照DOM形式來建立一個DOM節點(註1)，每一個節點都各代表一個獨立的內容或者標籤，最後由這些節點按照HTML檔案所指示的巢狀結構來構成對應的樹狀結構，該樹狀結構被稱之為DOM Tree，拿下面的HTML程式碼來當例子的話：

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


## Render Tree

### JavaScript FILE
在產生DOM和CSSOM之後，我們還可以透過JavaScript在Render Tree產生之前來變更DOM或者CSSOM的內容，比如透過

## 註解：
1. DOM (Document Object Model)，一種讓程式語言方便操作網頁元素的介面，其形式是將每一個標籤和內容都轉化為一個物件，最後再根據網頁結構的parent-child關係來重新將這些元件以樹狀形式來結合成一個DOM Tree，樹狀的每一個節點皆為前面所述的物件。






## Reference

1. 瀏覽器如何處理解析URL，https://dev.to/deepika_banoth/what-happens-when-i-type-a-url-in-browser-3i5o
2. 什麼是Critical Rendering Path，https://www.geeksforgeeks.org/critical-rendering-path-flow/
