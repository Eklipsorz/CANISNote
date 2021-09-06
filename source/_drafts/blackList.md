---
title: Black List
tags:
---

假設自己接受了著手寫抽獎黑名單系統的後端處理，而這個處理具體是將已先定義的黑名單去比對現有的抽獎者資料，看看哪些是黑名單中出現的抽獎者，若出現則必須剔除，而在這裡會要求你比對的人必須和黑名單中顯示的資料一樣，也就是說若黑名單紀錄著名字、電子郵件、抽獎號碼，那麼若比對的人所擁有的資料也和這些一樣的話，才踢除，否則就保留。


在這套系統中，會給你一小筆資料給你當測資來使用：
```
const players = [
    { name: 'Bernard', email: 'bernard@example.com', ticket: 'XL3558' },
    { name: 'Youchi', email: 'youchi@example.com', ticket: 'AH9188' },
    { name: 'Yenting', email: 'yenting@example.com', ticket: 'LO9903' },
    { name: 'Angela', email: 'angela@example.com', ticket: 'HY7212' },
    { name: 'Yvonne', email: 'yvonne@example.com', ticket: 'CH7684' },
    { name: 'Ellen', email: 'ellen@example.com', ticket: 'BB1750' },
    { name: 'Walter', email: 'walter@example.com', ticket: 'EI5724' },
    { name: 'Walter', email: 'walter@example.com', ticket: 'EI5724' },
    { name: 'Tim', email: 'tim@example.com', ticket: 'CK4592' },
    { name: 'Kevin', email: 'kevin@example.com', ticket: 'TT1804' },
    { name: 'Russell', email: 'russell@example.com', ticket: 'SI0305' }
  ]

```

而黑名單清單測資為：

```
  const blackList = [
    { name: 'Tim', email: 'tim@example.com', ticket: 'CK4592' },
    { name: 'Walter', email: 'walter@example.com', ticket: 'EI5724' }
  ]
```


現在就要你透過這兩種資料進行比對和篩選。


## 實現方法

### 實現方法1：

首先我打算先用email快速篩出符合比較可能是黑名單的人，然後再進一步用其他資料比對可能是的人和黑名單的人兩者資料是否一樣，若一樣則刪除，若不一樣則跳過，另外想透過while進一步持續對下一筆資料做比對刪除。 

```
 let lengthBlackList = blackList.length
    let blackListEmail = []
    
    // 先在新的陣列放入黑名單中每個人的email
    for (let blackListIndex = 0; blackListIndex < lengthBlackList; blackListIndex++) {
      blackListEmail.push(blackList[blackListIndex]['email'])
    }
    
    
    for (let playerIndex = 0; playerIndex < players.length; playerIndex++) {
    
        // 利用存放黑名單的email來比對每個人的email是否一致，若下一個還一致就繼續比對，直到不一致
        while (blackListEmail.includes(players[playerIndex]['email'])) {
    
            // 比對在黑名單的每一個人
            for (let blackListIndex = 0; blackListIndex < lengthBlackList; blackListIndex++) {
  
                // 記錄符合黑名單的人之資料相同數，一開始宣告為1是因為只有email和黑名單的人一致才能進來，
                // 所以可以先宣告為1，接著之後再比對其他屬性的時候，若一樣就+1，直到比完所有屬性
                let samePoint = 1
                for (let property in blackList[blackListIndex]) {
                    
                    // 只比對email以外的屬性
                    if (property !== 'email') {
                        // 記錄相同數
                        samePoint += Number(players[playerIndex][property] === blackList[blackListIndex][property])
                    }
                    
                }
                // 若全相同的話，就刪除這筆，然後跳過黑名單資料比較
                if (samePoint === Object.keys(blackList[blackListIndex]).length) {
                  players.splice(playerIndex, 1)
                  // 將 for (let blackListIndex = 0; ...) 這段迴圈中斷
                  break
                }  
                
            }
    
        }
    }

```


#### 實現1所遇到的bug


1. 當測資無法正常刪除時，內部的while會有機會進入無限循環的情況，比如遇到以下這筆資料，而Walter是黑名單中的人，但因為測資上的ticket和黑名單不同，所以無法在while內部正常被刪除 
```
{ name: 'Walter', email: 'walter@example.com', ticket: 'EI57240' }
```
