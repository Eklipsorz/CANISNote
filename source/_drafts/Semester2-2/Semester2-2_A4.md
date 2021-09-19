---
title: SemesterA4
tags:
- JavaScript
---


## data-toggle/data-bs-toggle

1. 這是bootstrap特定語法，並以html5為基礎
2. data-開頭 皆為html5可自訂的屬性
3. 點擊或者被挑選時，會額外搭配其他裝飾在被點擊的元件上
4. 其內容會是bootstrap特定的裝飾名稱，比如讓元件整體看起來像是膠囊狀的pill
5. data-toggle 是bootstrap 4.6版本，而data-bs-toggle是bootstrap 5.x版本

[連結](https://www.geeksforgeeks.org/data-toggle-attributes-in-twitter-bootstrap/)

原文：The data-toggle is an HTML-5 data attribute defined in Bootstrap. The advantage of using this is that, you can select a class or an id and hook up the element with a particular widget. For example, if you select an element and give the property of data-toggle as “collapse”, you’re basically making your div collapsible in just minutes by using Bootstrap.  



## role:
1. html5 語法
2. 當現有的HTML標籤不能充分表達語義性的時候，可以用role來說明該元件是什麼元件，通常這種情況出現在一些自定義的組件上，這樣可增強組件的可訪問性、可用性和可交互性。
3. role能填入特定元件名稱，比如：role="tab"就表示定義一個tablist中的交互式元件

[連結](https://kknews.cc/tech/59y8358.html)
[tab參考資料](https://getbootstrap.com/docs/4.6/components/navs/#pills)

原文：
WAI-ARIA 是一個由W3C編撰的規格，定義一套額外的HTML屬性能用於元素上提供額外的語意及改善可及性，當元素缺乏這些條件時可適用。本規格定義三個主要的特點：

Roles — 這些角色用以定義元素是甚麼或做甚麼事。在這些當中許多被稱為地標角色，大部分重複了HTML5結構化元素的語意值如role="navigation" (<nav>) or role="complementary" (<aside> (en-US)), 但也有其他描述不同的頁面結構者，如role="banner", role="search", role="tabgroup", role="tab"等常見於使用者介面中。



## <pre> 標籤：
1. 會以實際在標籤內部的內容(空白、換行)來呈現，是用來保存原始文字內容的格式 (preformatted text)，意思是文字內容中的空白、換行 (whitespace) 都會被保留下來顯示，
2.  形式為如下，context為任意內容

```
<pre>
  context
</pre>
```



example: 

```
<pre>
  L          TE
    A       A
      C    V
       R A
       DOU
       LOU
      REUSE
      QUE TU
      PORTES
    ET QUI T'
    ORNE O CI
     VILISÉ
    OTE-  TU VEUX
     LA    BIEN
    SI      RESPI
            RER       - Apollinaire
</pre>


```

結果：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1631549632/blog/semester2-2/resultOfPre_acswhb.png)

原文：
The <pre> HTML element represents preformatted text which is to be presented exactly as written in the HTML file. The text is typically rendered using a non-proportional, or "monospaced, font. Whitespace inside this element is displayed as written.



## trim 可以清掉首尾的空白
當輸入"   "這字串，內容為3個空白時，可透過trim轉換成""



## for 屬性:
1. 這是html語法，並且是label標籤上的屬性
2. 功能為擁有該屬性的元件(含其內容)與哪個表單元件(含input元件)進行元件上的(內容)綁定
3. 形式為如下，value會是某種表單元件，下達後該label元件會與指定表單元件(如button、input)進行綁定

```
<label for="value">
```

example1: 當點擊Email address:時，效果會像是點擊了它右邊的輸入欄

```
<label for="emailadd">Email address: </label>
<input type="email" name="emailadd" id="emailadd">
```

原文：

1. the for attribute specifies which form element a label is bound to.
2. for: The value of the for attribute must be a single id for a labelable form-related element in the same document as the <label> element. So, any given label element can be associated with only one form control.


## font-awesome 圖示會依賴版本
有些圖示會依據版本太舊而不顯示，比如只在最新版本出現的圖示不會出現舊版本



## css 變數宣告/使用
1. 如同字面上的意思，可以透過CSS樣式表來宣告變數和使用變數，同時也允許JavaScript存取，代表其變數會存在CSSOM或者Rendering Tree

例子：在todolist.css中利用var來設定變數宣告和指派
```
.list__header {
  /*    Variables       */
  
  --list__input-field-border-color: #ced4da;
  --list__add-item-section--error-display: none;
  --list__add-item-section-error-message-display: none;
}


.list__input-field {
  
  /*    Font or other   */
  border: 1px solid var(--list__input-field-border-color)
}
```
 
結果能在CSSOM找到對應的樣式(google DEV)

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1632059931/blog/temp/var1_in_CSSOM_ss4hdu.png)
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1632059931/blog/temp/var2_in_CSSOM_ehvinn.png)


2. 宣告變數的形式如下，selector是選擇器，其形式會放在選擇器內容中，而variableName是變數名稱，名稱前要加--，value是指派給variableName的內容，

```
selector {

  --variableName: value;
}


```

3. 使用變數的形式如下，var為css函式，其中variableName為要使用的變數名稱，必須用字串表示，而當變數取得失敗時，便以fallBackValue來表示，最後結果會是從變數那邊取的內容並給予propertyM

```
selector {

  propertyM: var('--variableName', fallBackValue )
}

```

4. 這些變數具有scope，和javascript的變數一樣具有global和local，css 的 global 變數則是一率都是:root選擇器(也稱之為html selector)下設定，該選擇器會指向整份網頁檔案，在這裡你可以將它想像成Global Scope，在這裏所有在同份檔案下的選擇器街能夠存取root選擇器內所定義的變數。

```
:root {

}
```

而local變數，則是看選擇器對應元件所包含或者被包含的狀況，假設有兩個選擇器分別對應element1和element2，而element1包含著element2，

```
<element1>
  <element2>context</element2>
</element1>
```
系統會根據這兩者父子關係來構成scope，父元素內部會包含子元素構成的scope，子元素會被父元素的scope所包含著，整體會像是：

```
{                   // element1


  {                 // element2
      
  }

}

```

每個scope之間都如同JS的scope規則那樣，當對應elemenet1的選擇器有設定變數a，而對應element2的選擇想用變數a，此時這兩者scope會像是JS的scope規則一樣，對應element2的選擇器可以利用scope來成功存取到vara的值，

```
{                   // element1
  --bgColor: limegreen;

  {                 // element2
      background: var(--bgColor);
  }

}

```

如果今天換element2去宣告定義，而換element1去使用它宣告過的變數，這種情況element1並不是element2的子元素而不能夠獲取該變數，

```
{                   // element1
  
  background: var(--bgColor);
  
  {                 // element2
      --bgColor: limegreen;
  }

}

```

總結一下，local變數只能夠讓對應元素下的子元素以及後代元素看到，其餘元素則無法獲取，而global變數相當於一個大範圍的local變數，而使用在同一份檔案下的選擇器皆能存取global變數

[CSS Variables](https://w3c.hexschool.com/blog/21985acb)
[var()](https://developer.mozilla.org/en-US/docs/Web/CSS/var())
[CSS Var](https://blog.logrocket.com/css-variables-scoping/)

## 如何在使用者互動替換偽元素的樣式
1. 使用var方法
https://ithelp.ithome.com.tw/articles/10200426
https://stackoverflow.com/questions/4481485/changing-css-pseudo-element-styles-via-javascript


## font-awesome圖示需要載入font-family
awesome最新版本(5.x)使用的內容為"Font Awesome 5 Free"，較舊(4.x)版本得用"FontAwesome"


5.x版本：
```
  .login::before {
    font-family: "Font Awesome 5 Free"; font-weight: 900; content: "\f007";
  }

  .tps::before {
    font-family: "Font Awesome 5 Free"; font-weight: 400; content: "\f1ea";
  }
```

4.x版本：
```
selector {
  font-family: "FontAwesome"; 
}
```

## 其他資料：
https://ithelp.ithome.com.tw/articles/10209328
https://ithelp.ithome.com.tw/articles/10244631
https://vuejs.org/v2/guide/render-function.html
