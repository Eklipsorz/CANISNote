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



##