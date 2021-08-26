---
title: Critical Rendering Path 簡介
tags:
---


Critical Rendering Path 是瀏覽器如何將網頁檔案轉化成網頁的處理路徑，其路徑包含了Networking、HTML/CSS/JavaScript三者合力形成的DOM(Document Object Model)樹狀結構和CSSOM(CSS Object Model)樹狀結構、DOM樹狀結構和CSSOM樹狀結構結合而成的Render Tree、Layout、Paint，每個路徑之間關係會如同下圖所示那樣。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629966828/blog/RenderingPath/Critical_Rendering_Path_mpepx8.png)



## Networking

當一個使用者開始透過URL來瀏覽網頁時，會試著解析URL對應的IP是誰，唯有知道IP是哪個伺服器負責處理網頁以及向誰發送"要求網頁檔案回傳過來"的請求。


而解析URL的流程主要流程為：
- 檢查瀏覽器本身的快取(Cache)是否有URL的對應IP，若沒有則繼續朝下一個目標找
- 檢查(執行目前的瀏覽器)作業系統的快取(Cache)是否有URL的對應IP，若沒有則繼續朝下一個目標
- 檢查離本地端較近的路由器(Router)是否有URL的對應IP，沒有朝下一個目標找
- 對ISP發送請求詢問它那邊的快取是否有對應IP，沒有朝下一個目標找
- 就開始針對ISP的DNS Server進行遞迴式搜查，直到找到對應IP

若使用者系統並不知道該URL對應的IP是指哪個伺服器，瀏覽器會開始透過網路去發送請求給對應的DNS Server並詢問它該URL對應的IP是什麼，若它查詢到並回傳對應IP給該使用者，使用者再重新對該IP來要求伺服器回傳網頁的對應檔給使用者下的瀏覽器，回傳檔案的形式並不會一口氣以一個完整檔案傳過去，而是以固定大小的封包(Packet)形式將原檔案切分成好幾等分傳給使用者的瀏覽器來處理。





## Reference

1. 瀏覽器如何處理解析URL，https://dev.to/deepika_banoth/what-happens-when-i-type-a-url-in-browser-3i5o
