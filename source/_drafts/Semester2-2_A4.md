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
3. 形式為如下，value會是某種表單元件，下達後該label元件會與指定表單元件進行綁定

```
<label for="value">
```

example1:

```
<form>
  <label for="male">Male</label>
  <input type="radio" name="sex" id="male" />
  <br />
  <label for="female">Female</label>
  <input type="radio" name="sex" id="female" />
</form>

```

原文：

1. the for attribute specifies which form element a label is bound to.
2. for: The value of the for attribute must be a single id for a labelable form-related element in the same document as the <label> element. So, any given label element can be associated with only one form control.


## font-awesome 圖示會依賴版本
有些圖示會依據版本太舊而不顯示，比如只在最新版本出現的圖示不會出現舊版本



## css 變數宣告/使用
1. 如同字面上的意思，可以透過CSS樣式表來宣告變數和使用變數，同時也允許JavaScript存取，代表其變數會存在CSSOM或者Rendering Tree(質疑？)
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

4. 這些變數具有scope，和javascript一樣具有global和local，以選擇器對應的元件當作js中由括號
構成的區塊或者區域，而被該元件包含的元件內容則是另一個被包含著的區塊或者，這是local區方法，而global則是一率是： :root會指向整份網頁檔案，也就是html selector
```
:root {

}
```

區域的例子，分別為html和css檔案，其內容分別為如下

css 檔案內容，其中body和div是選擇器名稱會分別對html檔案中的body和div這兩個標籤
```
body {
    --bgColor: limegreen;
}

div {
    background: var(--bgColor);
}
```

html 檔案內容
```
<body>
    <div>Div 1</div>
    <div>Div 2</div>
</body>
```


在css中我們宣告bgColor在body樣式表中，而使用該變數的元件是div，由於body先包含了div，所以我們可以用js的角度來看他們的scope:

```
{                               // 代表body元件
  let bgColor = limegreen
  {                             // 代表div元件
      use bgColor
  }

}
```
在div元件中，我們可以如同javascript的scope原則來套用，其結果是可以正常使用body元件下宣告的bgColor變數內容。

而若是兩者反著來呢？ html內容保持不變，但由body包含的div元件來宣告bgColor變數，但body元件無法正常存取其變數內容，因為宣告在該scope內會在body之前被釋放或者本來就不存在這變數。

```
body {
    background: var(--bgColor);
}

div {
    --bgColor: limegreen;
}
```


[CSS Variables](https://w3c.hexschool.com/blog/21985acb)
[var()](https://developer.mozilla.org/en-US/docs/Web/CSS/var())
[CSS Var](https://blog.logrocket.com/css-variables-scoping/)

## 如何在使用者互動替換偽元素的樣式
1. 使用var方法
https://ithelp.ithome.com.tw/articles/10200426
https://stackoverflow.com/questions/4481485/changing-css-pseudo-element-styles-via-javascript


## 其他資料：
https://ithelp.ithome.com.tw/articles/10209328
https://ithelp.ithome.com.tw/articles/10244631
https://vuejs.org/v2/guide/render-function.html
