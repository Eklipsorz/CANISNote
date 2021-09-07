---
title: Simulate a Lottary game
tags: 
 - JavaScript
 categoires:
 - Backend
 - Website Development
---


該專案是以模擬樂透抽獎為主軸，開發者得要達成加密名字、加密電子郵件、產生樂透抽獎券號碼、抽出特定玩家賦予特定獎項、贏家公告、賦予參加獎給其他沒抽到的抽獎者等子功能，最後將這些功能組合成所要求的專案，而這些子功能必須滿足特定規格才算完成，另外會額外賦予測資方便調整，其測資以測資小節來說明。


## 各子功能的開發規格
1. 加密名字： 前兩個字必須以明碼顯示，後續字元皆以*來表示，而後續字元數決定*的數量，比如Eklipsorz，那麼Ek以明顯顯示，除了前面兩個以外，後續有7個字元，所以用7個*來表示，將兩者結果結合成Ek*******。

2. 加密電子郵件：電子郵件分為三個部分，使用者名稱、@符號、@後的後綴字，除了@和後綴字皆以明碼來顯示，使用者名稱必須隱藏後半段的字元，改由三個.符號來顯示，前半段則以明碼顯示，當使用者名稱的字元數是單數時，則一半的字元數將會是無條件捨去過後的數字，比如字元數是7，那麼一半的字元數則是3。
```
half =  Math.floor(username.length / 2)
```

3. 產生樂透抽獎券號碼：xxyyyy這六個字元組成，xx是兩個大寫英文字母，而yyyy則是0~9這10個數字，每一組號碼都必須是獨立不重複的，另外可自由擴展大寫英文字母的數量以及數字的數量，比如3個大寫英文字母以及4個數字。

4. 抽出特定玩家賦予特定獎項： 從抽獎名單中隨機挑一位抽獎者來擔任贏家，並賦予特定獎項，其中賦予形式必須是透過公告來告知。
 
5. 贏家公告：公告指定抽獎者以及獲取獎項，公告形式是 

```
抽獎券號碼 | 加密後的名字 | 加密後的電子郵件 | 獎項
```

6. 賦予參加獎給其他沒抽到的抽獎者： 賦予參加獎給剩下沒抽到頭獎、貳獎、叁獎的抽獎者，賦予形式也必須是透過公告來告知。


## 測資
測資會用一個物件陣列來存放每個抽獎者所擁有的資料(名字、電子信箱等)，其中過程中或許會替每個每個物件(抽獎者)增加一個抽獎券這個屬性值。
```
const players = [
  { name: 'Bernard', email: 'bernard@example.com' },
  { name: 'Youchi', email: 'youchi@example.com' },
  { name: 'Yenting', email: 'yenting@example.com' },
  { name: 'Angela', email: 'angela@example.com' },
  { name: 'Yvonne', email: 'yvonne@example.com' },
  { name: 'Ellen', email: 'ellen@example.com' },
  { name: 'Walter', email: 'walter@example.com' },
  { name: 'Kevin', email: 'kevin@example.com' },
  { name: 'Tim', email: 'tim@example.com' },
  { name: 'Russell', email: 'russell@example.com' }
]
```



## 各子功能的實作


### 加密名字實作
主要實作一個名為encodeName的函式，功能會加密並回傳加密後的名字，會接受一個參數值，該值代表著未加密前的名字。其中參數本身string，但由於本身在JS上可以被當作String物件(這跟primitivie type的string名字相似，但實則上性質是不同的)來呼叫該物件特有的方法，比如substr和repeat，在這所用到substr會從第一個字元開始取，直到取到2個字元才停止，剛好可獲取明碼顯示的前兩個字元，後頭用上的*和repeat，則是利用*對於JS的型態的轉化去呼叫String物件的repeat方法，該方法會依照參數來複製字串內容並組成新字串，在這裏複製length - 2個*符號接在前兩個明碼字元。

```
// encodeName(parameter1) 功能為加密接收到的名字
// 參數說明： parameter1 是指要被加密的名字
function encodeName (name) {
  // 以明碼顯示名字前兩個字元，後續字元全用*符號表示
  return  name.substr(0, 2) + '*'.repeat(name.length - 2)
}
```


### 加密電子郵件
主要實作一個名為encodeEmail的函式，功能會加密並回傳加密後的電子郵件，會接受一個參數值，該值會代表著未加密前的電子郵件。同樣地，這裡的參數同樣被當作String物件去調用indexOf、slice、repeat等方法，首先會用indexOfAtSign去獲取@在字串中的索引值，該值會是使用者名稱的字元數，接著利用這字元數進一步獲取一半字元數，並用floor方法去達到規格書的要求，現在我們有了這一半的字元數就能進一步加密，加密方式就用slice從參數的第0個索引值去擷取，ㄧ直到索引值為halfLengthOfUserName才停止擷取，接著在用.和repeat方法來產生3個.符號，最後則繼續用slice將@和@後綴字全曲出來，將這些擷取到的字串和產生出來的新字串結合在一起便是加密後的電子郵件。


```
// encodeEmail(parameter1) 功能為加密接收到的email
// 參數說明： parameter1 是指要被加密的email
function encodeEmail (email) {
  // 請封裝你之前寫好的程式碼，並設計必要參數

    // 找到@的索引值，而該值剛好是email使用者名稱的字元數
    let indexOfAtSign = email.indexOf('@') 

    // 獲取email使用者名稱的一半字元數。
    let halfLengthOfUserName = Math.floor(indexOfAtSign / 2)

    // 使用 "使用者名稱的一半字元以明碼顯示＋3個.符號＋@＋@後綴字" 來組成加密後的email
    let econdedEmail = email.slice(0, halfLengthOfUserName) + 
                       '.'.repeat(3)                        +
                       email.slice(indexOfAtSign, email.length)

    return econdedEmail
}
```

### 產生樂透抽獎券號碼



```
// generateTicketNumber(parameter1, parameter2) 功能為產生獨立且不重複的抽獎
// 券號碼給抽獎者，格式為xxxyyy，xxx代表要填入的英文字母，而yyy代表要填入的數字 
// 參數說明：parameter1~2 是指定抽獎券的號碼格式分別要填多少個英文字母和數字
function generateTicketNumber (literalLength, digitLength) {

    

    // 利用無限迴圈的特性來不斷產生號碼，直到產生出獨立且不重複的號碼為止
    while (true) {
      
        let ticket = ''

        // 產生英文字母來填入號碼裡
        for (let round = 0; round < literalLength; round++) {
            ticket += String.fromCharCode(Math.floor(Math.random() * 26) + 65)
        }

        // 產生數字來填入號碼裡 
        for (let round = 0; round < digitLength; round++) {
            ticket += Math.floor(Math.random() * 10)
        }

        // ticketSet是存放所有已產生且獨立不重複的號碼，用它檢查新產生出來的號碼是否重複
        if (!ticketSet.includes(ticket)) {

            // 將獨立不重複的號碼放到ticketSet
            ticketSet.push(ticket)
            return ticket
        }
    }

}
```


### 抽出特定玩家賦予特定獎項
主要實作一個名為drawWinner的函式，功能會為從指定抽獎者清單抽出贏家並印出指定獎項和其贏家加密資訊，會接受兩個參數，第一個參數是存放所以抽獎者的清單，第二個參數是指定贏家會獲得什麼樣的獎項。當參數傳進去之後，會先透過random方法產生範圍為1~length(抽獎券人數)的亂數，以這個亂數來當抽獎名單的索引值，而挑出來的對應抽獎者就是贏家，另外再透過splice以該索引值來從清單直接取出，接著再把清單的對應抽獎者給刪去，以防止後續重複中獎，最後由這個贏家和第二個參數傳入announceMsg進行印出指定獎項和其贏家的加密資訊。


```
// drawWinner(parameter1, parameter2) 功能為從抽獎者中抽出一位贏家，並給予特定獎項，最後印出贏家資訊
// 參數說明：parameter1 是指存放所有抽獎者的陣列，parameter2 是指定發放獎項是什麼
function drawWinner (players, prize) {

  // 以亂數來抽獎
  let winnerIndex = Math.floor(Math.random() * players.length) 
  // 按照winnerIndex找到對應的贏家
  let winner = players.splice(winnerIndex, 1)[0]

  // 印出贏家資訊
  announceMsg(winner, prize)
}

```

### 贏家公告

主要實作一個名為announceMsg的函式，功能會依照指定贏家和指定獎項來印出其加密後資料和指定獎項，印出格式會依照規格書所定的那樣，該函式會接受兩個參數，第一個參數是指定贏家是誰，第二個參數是指定該贏家獲取的獎項是什麼。當參數傳進去之後，會直接透過console來進一步呼叫加密名字、加密電子郵件的函式來產生加密名字、加密電子信箱來分別印出抽獎券號碼、加密後的資訊、獎項。


```
// announceMsg(parameter1, parameter2) 功能為印出贏家資訊、獎項
// 參數說明：parameter1 是指贏家，parameter2 是指定獲取的獎項是什麼
function announceMsg (winner, prize) {
  // 印出贏家資訊、贏家獲取的獎項是為何
  console.log(`${winner.ticket} | ${encodeName(winner.name)} | ${encodeEmail(winner.email)} | ${prize}`)
}
```

### 賦予參加獎給其他沒抽到的抽獎者

經由drarWinner函式的處理可以把已中獎的人給剔除，那麼剩下來的抽獎者清單players就只剩下還沒中獎的人，所以在這裡直接透過for迴圈以及搭配現有的announceMsg函式直接賦予他們參加獎以及印出相關資訊。


```
for (let player of players) {
  announceMsg(player, '參加獎')
}

```


## 主程式的呼叫方式



