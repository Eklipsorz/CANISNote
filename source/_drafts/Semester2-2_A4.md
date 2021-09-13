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
1. 如同字面上的意思，可以透過CSS樣式表來宣告變數和使用變數
2. 宣告變數：其中variableName是變數名稱，名稱前要加--，value是指派給variableName的內容，

```
selector {

  --variableName: value;
}


```

