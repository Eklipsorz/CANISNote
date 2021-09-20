---
title: Semester2-2_U14
tags:
---


## Ajax (Asynchronous JavaScript and XML, AJAX)
1. 綜合了Asynchronous JavaScript 以及 XML這兩種技術，主要是透過以JavaScript來以非同步處理來進行資料交換，而當時資料是以XML為主，所以才有XML，現如今，不限於XML，還能支援JSON格式的資料
2. 應於於網頁上的應用是在前端與後端伺服器溝通


### 早期的Ajax應用方式
1. 利用XMLHttpRequest(XHR)物件來實作
2. 會先建立XHR物件，並使用該物件下的open方法去指定發送封包的形式，最後在用send方法去發送該封包。


```
function reqListener () {
  console.log(this.responseText);
}

var oReq = new XMLHttpRequest();
oReq.addEventListener('load', reqListener);
oReq.open('GET', 'http://www.example.org/example.txt');
oReq.send();
```



## Asynchronous Processing
1. 非同步處理
2. 在這個處理之下，每個任務都能做各自的事情，不用相互等待其他任務完成，同時間上會執行多個任務在執行


## Synchronous Processing
1. 同步處理
2. 在這個處理之下，一次只能做一件任務，每件任務都必須等待其他任務完成，同時間上只會有一個任務在執行


## JavaScript 本身的處理
其執行核心是單執行緒，理論上只能做同步處理的事情，但由於是在瀏覽器這個執行環境上執行的，可以呼叫瀏覽器額外提供的Web API來建立額外的執行序去做特定的處理，比如說：document、XMLHttpReqeuset、setTimeout


參考資料：
https://medium.com/itsems-frontend/javascript-sync-async-22e75e1ca1dc
https://ithelp.ithome.com.tw/m/articles/10200054

## Synchronous Request vs. Asynchronous Request
1. 同步請求，當client端發送請求給server端後，client端必須會保持等待直到server端回應請求，而當server端回應請求時，client端會收到請求做下一個執行任務。
2. 非同步請求，當client端發送請求給server端後，client端不會等待server回應請求而去做下一個執行任務，當server回應請求時，client端會立即做出回應，然後繼續做下一個任務。




## Asynchronous request API
1. jQuery 
2. HTML5 提供的 Fetch API
3. axios


## axios 受歡迎的原因
1. 廣泛的瀏覽器支援
2. 可支援Node.js從後端發送的HTTP Request，這意味著可支援前後端
3. 可直接將回應的JSON轉換成JavaScript的物件