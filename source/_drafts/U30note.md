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


當要更動已經存放primitive內容的變數時，系統會因為primitive內容本身是immutable而無法直接更動到其內容而另外分配額外記憶體來存放變更內容，並把新的記憶體區塊定義給原本的變數，這會使得這個變數看起來就像是宣告並定義內容給新的變數一樣，而舊的那塊會被回收或者釋放掉。比如說：當我們要將變數a更動為'12'的話，就會另外要塊記憶體存放'12'，而舊的那塊會被回收。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629620809/blog/variable2Memory/reassignVariableA_r3opnp.png)

2. 當一個變數A想儲存變數B所儲存的primitive 內容時，會另外建立一塊記憶體區塊來存放變數B目前儲存到的內容：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629623013/blog/variable2Memory/varA2varB_m32qth.png)

由於這樣的轉移過程等同於把變數B的值複製至變數A上，又被稱之為copied by value或者call by value。


3. 變數如何存放object 型別的資料：當宣告定義一個物件給一個變數時，系統會分配一個記憶體區塊來儲存物件上內容並放在記憶體中的heap區，最後讓變數本身儲存該記憶體區塊的記憶體位址或者參照位址(reference)，但變數本身是儲存在stack區塊：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629624064/blog/variable2Memory/varA2Obj_jn2shi.png)


當要更動存放object資料的變數時，由於object本身沒有immutable特性，所以可以直接對他的屬性做更動，而非建立額外的記憶體區塊去儲存變更後的object內容。


4. 當一個變數A想儲存變數B所儲存的object 內容時，系統可以藉由變數B儲存的參照位址(reference)來對應變數B所儲存的object：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629624896/blog/variable2Memory/varA2varB_obj_zykwlk.png)


這時我們可以透過variableB來操控同一個物件以及變更其內容：

```
variableB.property1 = value
```

這樣的轉移過程就只是把變數B的參照位址傳給變數A來獲得object 內容，所以被稱之為call by reference 或者 copied by reference。

5. 若函式參數是以primitive為主的變數，其變數會透過copied by value來獲得引數內容，而若是以object為主的變數，則透過copied by reference，可以直接變更或者控制該reference對應的物件。

note：
1. 所有primitive 型別的內容皆為immutable，換言之，只要它們一被放入記憶體中，他們對應的記憶體區塊是不允許被修改的，除非重新複製其內容。

2. 承接第一點，若變數對應immutable 內容時，其變數會被稱之為immutable variable，但變數本身並不是immutable。


參考資料：

1. https://developer.mozilla.org/en-US/docs/Glossary/Primitive
2. https://stackoverflow.com/questions/16115512/understanding-javascript-immutable-variable
