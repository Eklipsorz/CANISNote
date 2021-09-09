---
title: 函式所用到的參數建議數量
tags:
 - JavaScript
categories:
 - 開發守則
 - Side Effect
 - Destructuring
---

根據[1]所提的經驗法則裡，一個函式的參數量得盡量保持1~2個參數會比較好維護，參數過多會容易編寫出大量的測試程式去測試每一個參數下的效果。
## 若參數量真超過2個的話

可透過


let us say that a pure function is a function whose output is only determined by its input and has no observable effect on the outside world.
### 解構(Destructuring)


## 額外知識：P


## 額外知識：Side Effect
當一個函式的輸出結果被其他不屬於函式本身的內容所改變或者具有可觀測性的影響會改變函式


具有可觀測性的影響會改變與他們本身之外的事物(其他函式、全域變數、檔案等等)，這種影響便是Side Effect，比如一個函式做了：
1. 改變全域變數
2. 顯示東西於螢幕
3. 改寫檔案
4. 產生一個http的請求
5. 產生額外的process
6. 儲存資料到資料庫中
7. 呼叫具有Side Effect的函式
8. 對DOM進行改變
9. 亂數

這些事情皆為side effect的經典例子，反之，若一個函式不具有可觀測性的影響去改與他們本身以外的事物，該函式就是具有可預測性的pure function，如果你給他們相同的參數，他們會總會回答相同的結果和處理，並不會因為

## 參考資料
1. clean-code-javascript，https://github.com/ryanmcdermott/clean-code-javascript

2. https://dev.to/vonheikemen/dealing-with-side-effects-and-pure-functions-in-javascript-16mg
