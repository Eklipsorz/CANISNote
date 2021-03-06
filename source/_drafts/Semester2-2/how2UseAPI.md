---
title: How to use Web API
tags:
- JavaScript
---


應用程式介面(Application Programming Interface，API)，功能為應用程式向外開放的介面，而API的使用者會是能夠寫程式的開發者，開發者可以透過API去使用其他人的應用程式，就如同使用咖啡機(他人的應用程式)煮咖啡，使用者只需要如何按按鈕(使用API)就能使用咖啡機(他人的應用程式)下所會有的功能以及它所擁有的資訊，比如咖啡豆目前的狀態。

在這裡，API大致上可以區分為使用API的client端和提供API對應服務的server端，client端可以透過API跟server端請求服務，而server端則是收到client端的請求並回應對應服務給client端。而若把瀏覽器當作是client，而能透過網路提供API對應服務的主機當作是server，且client和server端之間的請求回應等服務則是使用http/https傳遞協定來進行，那麼這樣子的API，又被稱之為Web API。



而通常每一個對外提供的Web API會由提供API的一方來定義能提供多少服務，如何使用API、API參數是什麼、何種形式來回應調用API的一方等規格，並將這些內容以說明文件形式存放在他們的伺服器來告訴使用者怎麼使用，不論形式、如何使用、參數是為何，回應調用API的client的形式會以XML或者JSON來進行，不過由於JSON過於輕量、易於閱讀，使得網頁開發相關語言都支援JSON，主流上會以JSON為主。


## 當client 使用 API時
當client端想透過API去使用server端的某項服務時，client端會跟server端會先於TCP/IP中的三向交握中建立連結，之後client便會正式發送請求的封包給server端，而server端收到請求後便會回傳另一個封包來回應client。

未增加封包後的版本：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1631431354/blog/how2useAPI/client2server_rzjbgc.png)

增加封包後的版本：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1631433951/blog/how2useAPI/detail_client2server_k7juuv.png)


這些封包會是以TCP/IP 應用層形式而規劃出的http封包，而client端和server端這兩者的http封包內容皆不一樣，client端所建立的封包內容會有Request Method、Request URL、Request Headers、Message body，Resqest Method是指想要對目標資源做什麼樣請求，Request URL是具體的目標資源，其URL是用來定義資源在網路環境下的的位置格式，使用這個格式可以在網路上找到對應的目標資源，Request Headers則是進一步定義請求的設定、格式，最後一個Message body是該請求封包的具體詳細請求內容。


server端所建立的封包內容會有Status code、Response Headers、Response Body，Status code則是以數字表示回應client請求的結果/狀態，Response Headers則是進一步定義回應"請求"的設定、格式，而Response Body則是具體詳細的回應內容。


### Resquest Method
Resqest Method是指Client端想要對目標資源做什麼樣請求，具體請求有：
1. GET: 主要向目標資源請求讀取某些資料。
2. POST: 主要告訴對方我要傳東西給你，請看我在Message body儲存的內容來新增。
3. PATCH: 主要告訴對方我要傳東西給你，請看我在Message body儲存的內容來更新。
4. PUT: 透過特定內容來取代目標資源上的被取代內容來達到更新，若被取代內容不存在的話，會增加特定內容至目標資源上。
5. DELETE: 會請求對方刪除某些資源。

如果一個請求被重複發送好幾次，其最後結果會像是下達一個同種請求後的結果，該請求就會是冪等(Idempotent)，而冪等名字是源自於數學的一元運算式的冪等，如果一個請求不會改變伺服器上的狀態和資源，該請求為safe，根據這兩種請求，我們將上述五種請求歸類：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1631438998/blog/how2useAPI/safeAndIdempotent_yonpjf.png)

差別：
1. PATCH vs. PUT ： 前者允許更新一部分內容，後者得必須完整的內容來替代
比如說我們想要修改某個網頁的第一隻動物的名字，而且只修改名字而已(如下)，
{
  "id" : 1,
  "name" : "小白" ,
  "type" : "小型犬" ,
  "birthday" : "2019/1/29"

}
我們可以使用以下兩種方法之一：
```
PATCH http://127.0.0.1:3000/api/animal/1
PUT http://127.0.0.1:3000/api/animal/1
```

當我們使用第一種來將名字修改成大白的話，並將更新內容(如下)填入至Message Body，

```
{
  "name":"大白"
}
```

其結果回如同預期那樣，只修改名字屬性

```
--結果--
{
  "id" : 1,
  "name" : "大白" ,
  "type" : "小型犬" ,
  "birthday" : "2019/1/29"
}
```

但若採用二種方式，把同個更新內容填入至Message Body，

```
{
  "name":"大白"
}
```

其結果會是如下，所有沒被設定的屬性值皆會用預設值，比如null或者容易猜到的，就只有名字大白正確地修改

```
--結果--
{
  "id" : 1,
  "name" : "大白" ,
  "type" :  null ,
  "birthday" : null
}
```
所以若要採取PUT的話，得把全部的屬性值都寫上一輪來做取代，比如：
```
{
  "id" : 1,
  "name":"大白" ,
  "type" : "小型犬" ,
  "birthday" : "2019/1/29"
}
```


參考資料：
https://ithelp.ithome.com.tw/articles/10224134
https://stackoverflow.com/questions/31089221/what-is-the-difference-between-put-post-and-patch



### Request URL 
統一資源定位器(Uniform Resource Locator，URL)，別名網址，定義資源在網路環境下的的位置格式，如同門牌。

格式：
```
[協定類型]://[伺服器位址]:[埠號]/[該伺服器下的檔案路徑(含檔名)]?[查詢/參數]
```

協定類型： 可填入http、https
伺服器位址：可填入IP、由(DNS Server給定的)域名
埠號：當電腦要成為提供多種特定服務的伺服器且不想申請額外伺服器位址來標示這些特定服務時，比如使用者連接位址A就對應服務A，使用者連接位址B就對應服務B等等。取而代之，是透過同一個位址下的不同數字來讓使用者去對應，比如位址搭配1就對應服務A，位址搭配2對應服務B等等，而這個數字就是埠號。
檔案路徑：會以特定目錄/資料夾位置來當作根目錄，並且根據網址給定的路徑來從對方主機的根目錄下找指定檔案路徑。
查詢/參數：這邊會被瀏覽器當作該頁面下的參數來使用，若參數多於1個時會搭配著&符號

### Status Code
Status code則是以數字表示回應client請求的結果/狀態，數字分別有：
1. 200 OK 表示請求成功
2. 400 Bad Request 表示客戶端發送的請求封包出現錯誤(如格式出錯)，伺服器無法處理
3. 403 Forbidden 表示伺服器理解請求，但拒絕執行回應結果(不包含回傳403訊息)
4. 404 Not Found 表示客戶端要求的資源沒在伺服器，而伺服器會回傳該訊息告知client該資源找不到




## Client 發送請求的具體方法
使用Axios和Ajax



### Axios
Axios 是JavaScript第三方函式庫，其函式庫主要能幫助開發者透過它提供的方法來以Ajax和Promise形式來對server端發送HTTP 請求或者 XMLHTTPRequest 請求，前後者會看開發者所處的client端是什麼，若是Node.js來發送請求，則請求會是HTTP請求形式，而若是從瀏覽器本身來發送請求，則請求會是XMLHTTPRequest。


當要開發需要載入該套件時，預設上會添增axios這物件，所以只需要對該物件下的方法來發送請求，比如說要對某伺服器發送GET請求，那麼寫法上會是如下，then、catch是JavaScript promise機制下的語法，

```
axios.get(URL)
  .then(function (response) {
    // handle success
    console.log(response);
    console.log(response.data)
  })
  .catch(function (error) {
    // handle error
    console.log(error);
  })
  .then(function () {
    // always executed
  });
```

當伺服器回應axios.get方法所發送的請求封包的status code是200，就執行第一個then，而函式內的response物件會存放伺服器回應封包的所有內容，其中response物件的data屬性會是Response Body的內容，且內容會以JSON或者XML格式來存放。

而當伺服器回應axios.get方法所發送的請求封包並不是正常接收成功的，那麼就會就會執行第二個，而函式內部的error物件是存放失敗資訊。而最後一個then則是無論是否成功接收，皆會執行的程式碼。

### Ajax


若出現以下訊息，表示本地端並沒有載入jQuery函式庫或者並沒有載入正確的函式庫，如 slim jQery並不支援$.ajax
```
$.ajax is not function
```

## JSON 
JSON (JavaScript Object Notation) 是一種基於JavaScript的物件表示法而獨立衍生出的文字標記法，跟JavaScript沒什麼關係，該格式會如同JavaScript物件表示法那樣使用key-value pair來存放每一筆資料，key在這裏是指字串所構成的屬性，而value會是任意型別的值，能支援的型別有：數值、字串、布林值、物件、陣列(有序且只能放多個任意型別的值/物件)、空值(null)，整體JSON形式會是：

```
{
  "key1": value1,
  "key2": value2,
        .
        .
        .
  "keyN": valueN
}
```

也可以存放陣列：使用[]來表示陣列，該陣列只能夠存放多個值或者多個物件

```
{
  "key1": value1,
  "key2": value2,
        .
  "keyM: 
  [
    valueM1,
    valueM2,
       .
       .
  ]
        .
  "keyN": valueN
}

}

```

而另外，它的語法形式本身對於JavaScript來說就是一個物件，這個物件存放key1: value1 至 keyN: valueN這幾個key-value pair。

## 參考資料
Safe method - https://developer.mozilla.org/en-US/docs/Glossary/Safe/HTTP
Idempotent method - https://tools.ietf.org/html/rfc7231#section-4.2.2
Axios - https://github.com/axios/axios
JSON - https://ithelp.ithome.com.tw/m/articles/10222242