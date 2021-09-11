---
title: How to use Web API
tags:
- JavaScript
---


應用程式介面(Application Programming Interface，API)，功能為應用程式向外開放的介面，而API的使用者會是能夠寫程式的開發者，開發者可以透過API去使用其他人的應用程式，就如同使用咖啡機(他人的應用程式)煮咖啡，使用者只需要如何按按鈕(使用API)就能使用咖啡機(他人的應用程式)下所會有的功能以及它所擁有的資訊，比如咖啡豆目前的狀態。

在這裡，API大致上可以區分為使用API的client端和提供API對應服務的server端，client端可以透過API跟server端請求服務，而server端則是收到回應client端的請求並回應對應服務給client端。而若把瀏覽器當作是client，而能透過網路提供API對應服務的主機當作是server，且client和server端之間的請求回應等服務則是使用http/https傳遞協定來進行，那麼這樣子的API，又被稱之為Web API。



而通常每一個對外提供的Web API會由提供API的一方來定義能提供多少服務，如何使用API、API參數是什麼、何種形式來回應調用API的一方等規格，並將這些內容以說明文件形式存放在他們的伺服器來告訴使用者怎麼使用，不論形式、如何使用、參數是為何，回應調用API的client的形式會以XML或者JSON來進行

而建立的網頁應用程式上，其API就會是Web API


而提供API服務的網站會附上文件來說明如何使用它們的API、其參數又是填什麼、會回傳什麼形式的結果，通常會以XML、JSON的形式來回傳結果








