---
title: 基本網路知識 (先用已接觸來添增)
tags:
- Network
categories:
- Website Development
---




TCP/IP 在傳輸層的標頭會是：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1631371279/blog/TCP_IP/tcp_ipHeader_rwqwcl.png)

Source port: 來源埠號
Destination port: 目的埠號
Sequence Number(序列號): 該序號用來標示封包傳遞順序好用來比較哪些封包是重複且無用的，正常的封包傳遞會不斷以一個數字遞增，比如5,6,7。該值一開始會由亂數來決定
Acknowledgment Number(回應序號)：用來表示回應封包的序號或者順序，數值通常會是接收過來的封包所擁有的序號+1，讓被回應方知道對方已收到代表那序號的封包並做了第一次的檢查


TCP Flag在這裡又稱之為Control Bit，共八個bit，每一個bit都各用來告訴接收方和傳送方該封包內容是屬於哪一個類型，當某個bit上顯示為1，則表示該封包是該bit所對應的封包類型，若為0則不表示該類型，這些bit分別為


1. SYN (Synchronize sequence numbers): 若為1的話，則告知對方傳送方想透過序號同步的方式來與對方建立連結，通常會搭配ACK，若SYN和ACK皆為1的話，則表示傳送方與我方的連結已建立，並且我方想進一步與對方進行連結。


2. ACK (Acknowledgment field significant)：若為1的話，則告知對方此封包內的回應號碼(Acknowledgement number)是正確的，換言之，告知對方此封包內容就是回應內容，若為0的話，則表示沒回應內容。

3. RST (Reset the connection): 若為1的話，則表示目前內容是有問題的。
4. URG (Urgent Pointer field significant)
5. PSH (Push Function)
6. FIN (No more data from sender)
7. ECE
8. CWR

這些bit在TCP/IP標頭中的位置：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1631374337/blog/TCP_IP/tcpflag_wumylp.png)


## 三向交握

使用TCP/IP的主機在傳輸層對另一個支援TCP/IP的主機進行封包傳送前，必須先透過三向交握(Three-way Handshake)的過程建立連接(connection)來確保雙方在接下來的傳送是能夠得到保證。
而這裡的連接根據[RFC 793 Transmission Control Protocol](https://datatracker.ietf.org/doc/html/rfc793) 文檔中所定義的，連接是一種資訊綜合體，裡面包含著socket(雙方各自要求的URL和Port)、序號(sequence number)、窗口大小(window size)，而這個綜合體會用來初始化並維護往後傳送封包所需的資料，比如成功建立連接後，雙方會以綜合體所提供的資料來初始化自己封包的序號、窗口大小等相關資料。


三向交握是指三種不同的封包序號確認，交握有兩個目的，第一個目的是確認server和client這兩端的傳送和接收功能都是正常的，第二個目的就是避免由過舊重複的封包而引發的混亂問題，換言之就是這些封包內容會影響著資訊綜合體或者連接，而這些過舊重複的封包往往會是傳送方因網路延遲而重複發送的封包，這些封包帶有比較舊的內容，比如序號等。而交握最主要的目的是第二個。


### 三向交握的過程
(以下圖參考於draveness大佬，並不會將此文發布在正式文章中，等自身具有夠多知識補充時，再來將圖塑造成自己的)


正常來說，若不考慮過舊重複的封包下，三向交握會是如下，首先client端會以SYN的形式來發送封包向server端要求建立兩者連結，其封包的SYN值會是以亂數的方式來產生，而這也就是目前client端的序號，過段時間後，server端會收到該封包，並以ACK+SYN的(回應和請求對方與自己連結)形式來發送封包，ACK值會是從client端那邊封包取出來的SYN值並且加一，然後再另外將自己的序號(以亂數產生)存放該封包下的SYN值，最後client收到server這邊的封包並以ACK形式來回傳封包，表示連結建立，這時的封包會回傳client端和server端目前的序號給server


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1631379121/blog/TCP_IP/normal_ThreeWayHandShake_cubyfd.png)



若考慮有過舊重複的封包下，三向交握會是如下，大致上都和若不考慮過舊重複的封包的情況一樣，不一樣的地方是在當client端因網路因素而重複發送建立請求，當這個情形發生時，一定會有另一個重複的封包，當server端收到重複且過舊的封包時，會把它當做正常的請求建立封包並以ack的形式去回傳給client，而client端這時會檢查該封包的SYN值是不是client目前最新的序號，若不是的話，則會以RST形式傳封包告訴server端，上一個封包內容有問題，請重新接收封包，若下一個接收的封包還是同樣的問題，就會是同樣的手法去處理，直到接到SYN值是client最新的序號後才會繼續下一個流程來檢查。


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1631379122/blog/TCP_IP/duplicate_ThreeWayHandShake_l86upz.png)




https://hulitw.medium.com/learning-tcp-ip-http-via-sending-letter-5d3299203660