---
title: Semester2-1_FinalExam
tags:
- JavaScript
---



## Col-12 會直接換行
以下面例子來說明的話，原本不考慮12的話，會是一列中佔滿2欄，但由於每一欄都佔著12格，這已經超過一列能放的格數，因此會自動換行

```
  <div class="container">
    <div class="row color-panel">
      <div class="col-12 d-flex justify-content-center">
        <span style="background-color: red;" class="rectangle-outline">R</span>
        <input type="range" id="red-slider" min=" 0" max="255" value="128" class="mx-2 slider">
        <span style="background-color: red;" class="rectangle-outline longer-rectangle-outline"
          id="red-decimal">128</span>
      </div>

      <div class="col-12 d-flex justify-content-center">
        <span style="background-color: green;" class="rectangle-outline">G</span>
        <input type="range" id="green-slider" min=" 0" max="255" value="128" class="mx-2 slider">
        <span style="background-color: green;" class="rectangle-outline longer-rectangle-outline"
          id="green-decimal">128</span>
      </div>
  </div>
```

結果會是：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1632238307/blog/temp/resultOfCol-12_e4v6wo.png)


## CSS Attribute Selector
1. 選擇器之一，會挑選屬性符合條件以及挑選對象是指定元件
2. 形式上會是以下，會先挑選元件是否element，若符合就看看該元件是否有指定屬性attribute且是否符合value，都符合就採用此樣式

```
element[attribute=value] {
    property1: value1;
    property2: value2;
            .
            .
    propertyN: valueN;
}
```


3. 例子：


會挑選擁有target屬性的a元件：
```
a[target] {
  background-color: yellow;
}

```

會挑選type屬性值為text的input元件
```
input[type="text"] {

  /* Display */
  /* Box Model */
  width: 90%;
  opacity: 0.28;

}
```



## :disabled 偽類
1. 所有無法被挑選、點擊、輸入等方式來激活自己的元件，都會被系統辨識為disabled
2. 當元件處於disabled，便可以用disabled偽類來渲染其樣式，形式為:

```
element:diabled {
    property1: value1;
    property2: value2;
            .
            .
    propertyN: valueN;
}
```


原文：The :disabled CSS pseudo-class represents any disabled element. An element is disabled if it can't be activated (selected, clicked on, typed into, etc.) or accept focus. The element also has an enabled state, in which it can be activated or accept focus.



## CSS: attr方法
1. 是CSS函式之一，其回傳值會被指定給CSS屬性。
2. 可以從指定(HTML)標籤下所擁有的屬性獲取對應屬性值，並將其值代入至CSS屬性，當HTML的屬性變動時，其相關的CSS屬性值會跟著變動，形式為：attribute of tag on html是指html下標籤的屬性
```
selector {

  property: attr(attribute of tag on html)

}
```
3. 例子：

首先我們可以先在某個標籤下指定一個屬性值，在這裏指定result-text屬性給HTML檔案，然後在CSS檔案中添加attr(result-text)，告訴系統它要從HTML檔案內容取出#808080，並將此值給予content這css屬性，另外可以在JS調用setAttribute來修改HTML檔案內容下的result-text屬性值，藉由這樣來連同更動CSS檔案的content屬性

HTML檔案內容
```
<div class="col-12 d-flex justify-content-center show-hex-partition" id="result-textarea" result-text="#808080">
```

CSS檔案內容
```
selector {
  content: attr(result-text);
}
```

JS檔案內容：
```
resultTextArea.setAttribute('result-text', colorHex)
```

https://www.oxxostudio.tw/articles/201706/pseudo-element-3.html

https://developer.mozilla.org/zh-TW/docs/Web/CSS/attr()