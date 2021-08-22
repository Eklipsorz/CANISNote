---
title: U30note
tags:
---


1. 當變數要存放primitive型別的資料時，會先在記憶體中的stack區存放primitive 型別的資料，然後再透過定義將變數名稱與該記憶體空間做綁定。

```
let a = '10'
```

在記憶體我們可以這樣表示： 可以看到變數a存放著'10'這字串。
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629620272/blog/variable2Memory/declarationOfA_hzxuvv.png)


若我們在這個基礎上，在新增其他變數去存取其他值的話，其存放順序會按照新增的順序而放，會從變數a之後方開始放入：可以看到每一個變數都會拿到一個獨立的記憶體空間來存放內容。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629620809/blog/variable2Memory/declarationOfMultiVariables_h9evtm.png)





2. 變數如何存放object 型別的資料：

3. 兩者間修改的差異：


4. 複製object的方法：



note：
1. copied by reference 
