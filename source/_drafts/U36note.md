---
title: U36note
tags:
---


1. position 在CSS樣式中是一種屬性，它負責定義元素的定位方式，其參數為以下，通常會搭配top、bottom、left、right這四種屬性來指定位置在哪，若元素沒特別指定position時，系統預設上會指定元素為position為static。

```
position: static | relative | absolute | fixed
top: value
bottom: value
left: value
right: value
```

2. 若position 設定為static時，其容器大小並不會跟著內容而變化，而定位方式會依照原有的Page Flow來排定，在這情況下不會受到top、bottom、left、right任一種影響。

3. 若position 設定為relative時，其容器大小並不會跟著內容而變化，而定位方式會從static改變，且以static模式下的元素之定位參考點為基準點(下圖橘點)來定位，由該橘點來構成其元素能夠位移的範圍(橘框)：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629707392/blog/htmlPosition/relativeStartPoint_nsc1nk.png)

若

```
top: 30px
left

```

note:
1. Page Flow/Normal Flow: Flow是指放置內容的方向，而這裡Page Flow是指還沒套用任何CSS樣式的預設HTML放置內容之方向，其方向會是先由上而下來放，再來就從左至右。

2. Viewport (可視區): 是使用者能夠在網頁看到的全部區域(is the user's visible area of a web page)

3. 定位參考點：元素本身放置其他位置的基準點，通常元素會以自身的左上角作為定位參考點：圖中的黑點就是元素的定位參考點，當要位移該元素時，會以那個點來移動，並連帶移動整個元素。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629706579/blog/htmlPosition/positioningPoint_edkots.png)
