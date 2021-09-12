---
title: How to use Web API
tags:
- JavaScript
---


應用程式介面(Application Programming Interface，API)，功能為應用程式向外開放的介面，而API的使用者會是能夠寫程式的開發者，開發者可以透過API去使用其他人的應用程式，就如同使用咖啡機(他人的應用程式)煮咖啡，使用者只需要如何按按鈕(使用API)就能使用咖啡機(他人的應用程式)下所會有的功能以及它所擁有的資訊，比如咖啡豆目前的狀態。

在這裡，API大致上可以區分為使用API的client端和提供API對應服務的server端，client端可以透過API跟server端請求服務，而server端則是收到回應client端的請求並回應對應服務給client端。而若把瀏覽器當作是client，而能透過網路提供API對應服務的主機當作是server，且client和server端之間的請求回應等服務則是使用http/https傳遞協定來進行，那麼這樣子的API，又被稱之為Web API。



而通常每一個對外提供的Web API會由提供API的一方來定義能提供多少服務，如何使用API、API參數是什麼、何種形式來回應調用API的一方等規格，並將這些內容以說明文件形式存放在他們的伺服器來告訴使用者怎麼使用，不論形式、如何使用、參數是為何，回應調用API的client的形式會以XML或者JSON來進行


## 當client 使用 API時
當client端想透過API去使用server端的某項服務時，client端會跟server端會先於TCP/IP中的三向交握中建立連結，之後client便會正式發送請求的封包給server端，而server端收到請求後便會回傳另一個封包來回應client。

未增加封包後的版本：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1631431354/blog/how2useAPI/client2server_rzjbgc.png)

增加封包後的版本：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1631433951/blog/how2useAPI/detail_client2server_k7juuv.png)


這些封包會是以TCP/IP 應用層形式而規劃出的http封包，而client端和server端這兩者的http封包內容皆不一樣，client端所建立的封包內容會有Request Method、Request URL、Request Headers、Message body，Resqest Method是指想要對目標資源做什麼樣請求，Request URL是具體的目標資源，其URL是用來定義網路資源的位置格式，使用這個格式可以在網路上找到對應的目標資源，Request Headers則是進一步定義請求的設定、格式，最後一個Message body是該請求封包的具體詳細請求內容。


server端所建立的封包內容會有Status code、Response Headers、Response Body，Status code則是以數字表示回應client請求的結果/狀態，Response Headers則是進一步定義回應"請求"的設定、格式，而Response Body則是具體詳細的回應內容。


### Resquest Method
Resqest Method是指Client端想要對目標資源做什麼樣請求，具體請求有：
1. GET: 主要向目標資源請求讀取某些資料
2. POST: 本質上不屬於Idempotent請求，主要告訴對方我要傳東西給你，請看我在Message body儲存的內容來做更新或者新增。
3. PATCH: 
4. PUT: 本質上是屬於Idempotent請求，
5. DELETE: 本質上是屬於Idempotent請求，會請求對方刪除某些資源。


如果一個請求被重複發送好幾次，其最後結果會像是下達一個同種請求後的結果，該請求為Idempotent

https://tools.ietf.org/html/rfc7231#section-4.2.2

而建立的網頁應用程式上，其API就會是Web API


而提供API服務的網站會附上文件來說明如何使用它們的API、其參數又是填什麼、會回傳什麼形式的結果，通常會以XML、JSON的形式來回傳結果





https://medium.com/自稱好人大叔/tech-http-https-restful-8a2cc3dbbf92




