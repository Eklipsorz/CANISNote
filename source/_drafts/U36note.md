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

而top、bottom、left、right在這裡的表現，會以橘點為主：

a. value1為正值時，
- 當top被設定為value1時，元素的黑點會以橘點為中心向下移動至value1
- 當bottom被設定為value1時，元素的黑點會以橘點為中心向上移動至value1
- 當left被設定為value1時，元素的黑點會以橘點為中心向右移動至value1
- 當right被設定value1時，元素的黑點會以橘點為中心向左移動至value1

b. 當value1為負值時，top、bottom、left、right的移動方向會變成反方向，比如當top被設定為目前為負值的value1時，元素的黑點會以橘點為中心向上移動至value1。



4. 若position 設定為absolute時，其容器大小會跟著內容而變化，而定位方式會從static改變，且以離該元素最近的定位父元素(ancestor element，其position被設定static以外的值)所擁有定為參考點為基準點(圖中橘點)來定位，並由基準點(橘點)構成該元素能夠移動的範圍，而且不會為了不違反Page Flow或者HTML上結構的規定而改變定位。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629708899/blog/htmlPosition/absoluteStartPoint_ihsj9c.png) 

若一直都找不到合適的父元素(ancestor element)的話，會以body本身的定位參考點來當作基準點：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629709253/blog/htmlPosition/bodyStartPoint_en0fzx.png)


note:
1. Page Flow/Normal Flow: Flow是指放置內容的方向，而這裡Page Flow是指還沒套用任何CSS樣式的預設HTML放置內容之方向，其方向會是先由上而下來放，再來就從左至右。

2. Viewport (可視區): 是使用者能夠在網頁看到的全部區域(is the user's visible area of a web page)

3. 定位參考點：元素本身放置其他位置的基準點，通常元素會以自身的左上角作為定位參考點：圖中的黑點就是元素的定位參考點，當要位移該元素時，會以那個點來移動，並連帶移動整個元素。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629706579/blog/htmlPosition/positioningPoint_edkots.png)



4. 
