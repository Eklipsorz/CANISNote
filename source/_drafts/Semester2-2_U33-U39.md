---
title: Semester2-2_U33-U39
tags:
mathjax: true
---

## flex-basis
1. CSS 屬性值，只能在flex元素下的子元素上增加其屬性以及屬性值，預設值為0
2. 調整flex元素下的子元素(flex item)在主軸上的初始大小
3. 當主軸設定row時，就會控制寬度/x軸，當主軸設定column時，就會控制高度/y軸，其值並不會受到box-model所影響
4. 形式上會是以下，number可以填入比例或者數字，而auto則是依據對應元素上的box model來決定

```
flex-basis: number | auto
```



## flex-grow 
1. CSS 屬性值，只能在flex元素下的子元素上增加其屬性以及屬性值，預設值為0
2. 當一個flex容器放完子元素之後仍還有空間可以放置其他子元素，該屬性值會告訴系統這些子元素是否佔滿以及佔滿比例為何
3. 在同一個容器下的子元素會按照以下公式來擴展自己在主軸上的大小：

{% mathjax %}(\frac{\sqrt x}{y^3}){% endmathjax %}



例子：
```
<div class="items">
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
</div>
```


```
.items {
  display: flex;
  border: 2px solid #e0e0e0;
  justify-content: space-around;
}

.item {
  height: 100px;
  flex-basis: 100px;
}

.item:nth-child(1) {
  background-color: #5c6bc0
}

.item:nth-child(2) {
  background-color: #d4e157;
  flex-grow: 2;
}

.item:nth-child(3) {
  background-color: #ffca28;
  flex-grow: 1;
}
```