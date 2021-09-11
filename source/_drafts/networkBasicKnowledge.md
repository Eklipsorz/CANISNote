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
Sequence Number(序列號): 該序號用來標示封包傳遞順序好用來比較哪些封包是重複且無用的，正常的封包傳遞會不斷以一個數字遞增，比如5,6,7。
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



使用TCP/IP的主機在傳輸層對另一個支援TCP/IP的主機進行封包傳送前，會先透過三向交握(Three-way Handshake)的過程來確保並建立一個機制讓雙方在接下來的傳送是能夠得到保證。









