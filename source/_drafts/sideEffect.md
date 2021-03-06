---
title: sideEffect
tags:
---

當一個函式n滿足以下任意條件時，就能判定該函式本身具有Side Effect性質的：
1. 函式n本身的輸出結果會被不屬於函式n本身的內容所改變
2. 具有可觀測性的影響去改變函式本身以外的東西

反之，若一個函式不具有可觀測性的影響去改變與他們本身以外的事物且其輸出結果只被函式本身所改變，那麼該函式就是具有可預測性的pure function，若你給他們相同的參數，他們會總會回答相同的結果和處理。具有Side Effect性質的函式雖然很容易被外在改變或者改變外在，但並不表示全然都是壞的，有些時候我們必須得借用這性質去呼叫/使用外在事物，比如一個函式可以根據功能切分出多個子功能，每個子功能皆以函式來代表，這形式寫法很容易因功能獨立而方便找出問題，另一個好例子就是存入資料更新至資料庫、透過使用者的互動來改變介面。

```
function some_process() {
  const data = get_data_somehow();
  const clean_data = computation(data);
  const result = save(clean_data);

  return result;
}
```


## 例子
比如一個函式做了以下事情，皆具有Side Effect：
1. 改變全域變數
2. 顯示東西於螢幕
3. 改寫檔案
4. 產生一個http的請求
5. 產生額外的process
6. 儲存資料到資料庫中
7. 呼叫具有Side Effect的函式
8. 對DOM進行操作
9. 亂數

## Side Effect 帶來什麼樣的開發問題
1. 很容易被外在影響，除錯時很難從函式本身去追蹤，必須向外追蹤
2. 很容易改變其他事物，會容易產生不可預期的結果
3. 會因為執行過程過於複雜而降低可讀性






https://zhuanlan.zhihu.com/p/379503009

https://dev.to/vonheikemen/dealing-with-side-effects-and-pure-functions-in-javascript-16mg