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

(原文： is positioned relative to the nearest positioned ancestor (instead of positioned relative to the viewport.) However, if an absolute positioned element has no positioned ancestor, it uses the document body, and move along with page scrolling.)

其top、bottom、left、right的移動方式會如同設定relative那樣去決定元素的定位。

5. 若position 設定為fixed時，其容器大小會跟著內容而變化，而定位方式會從static改變，且直接在viewport內部定位，定位方式是以元素和viewport這兩者間的邊界作為基準點，通常viewport會由body元素來承擔，整體來說會像是：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629711523/blog/htmlPosition/originFixed_gy0g62.png)

在這情況下設定top、bottom、left、right時，會以最近的邊線當作基準：

當value1為正值，會盡量使元素放置在viewport內部
- top設定為value1，元素的上邊界(border-top)會跟viewport的上邊界在viewport內部保持value1的距離
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629711353/blog/htmlPosition/topFixed_yavtfv.png)

- bottom設定value1，元素的下邊界(border-bottom)會跟viewport的下邊界在viewport內部保持value1的距離
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629711353/blog/htmlPosition/bottomFiexd_h9olxv.png)

- left設定value1，元素的左邊界(border-left)會跟viewport的左邊界在viewport內部保持value1的距離
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629711353/blog/htmlPosition/leftFixed_czb3te.png)

- right設定value1，元素的右邊界(border-right)會跟viewport的右邊界在viewport內部保持value1的距離
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629711353/blog/htmlPosition/rightFixed_bewenm.png)

當value1為負值，其相關邊界會從viewport外部向內部展開，比如說當top的value1為負時，元素上邊界會與viewport上邊界在viewport在外部保持value1的距離。

另外當同時使用top、bottom、left、right時，會自動調整元素高寬來滿足其設定值，比如說若設定類似以下語法時，
```
left: value1
right: value2
```

其結果會是：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629713038/blog/htmlPosition/leftrightFixedExample_gfitur.png)

note:
1. Page Flow/Normal Flow: Flow是指放置內容的方向，而這裡Page Flow是指還沒套用任何CSS樣式的預設HTML放置內容之方向，其方向會是先由上而下來放，再來就從左至右。

2. Viewport (可視區): 是使用者能夠在網頁看到的全部區域(is the user's visible area of a web page)

3. 定位參考點：元素本身放置其他位置的基準點，通常元素會以自身的左上角作為定位參考點：圖中的黑點就是元素的定位參考點，當要位移該元素時，會以那個點來移動，並連帶移動整個元素。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629706579/blog/htmlPosition/positioningPoint_edkots.png)



4. z-index: 該屬性定義另一種維度來控制多個元素在相同位置上的呈現順序-深度，其屬性值越大，就越先呈現，數值越小，就越後呈現，但這不表示多個元素在相同位置的呈現會因為數值大而被覆蓋掉，而是以多個屬性能夠呈現為目標來達到此屬性值的效果。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629713706/blog/htmlPosition/ExportedContentImageFromAC_smdaug.png)


