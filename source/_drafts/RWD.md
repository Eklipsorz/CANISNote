---
title: RWD
tags:
---



隨著移動裝置的使用率飆升，這也代表著不同螢幕尺寸的裝置也將越來越多，而螢幕尺寸又會影響使用者對於網站的前端佈局設定，因此為了讓網頁佈局能夠更適應螢幕尺寸，就有人提出了RWD(Responsive Web Design)以及AWD(Adaptive Web Design)這兩種概念：


- RWD概念：透過CSS的控制而使當螢幕尺寸改變時，網站必須能夠自動回應最適當的前端佈局。
	- 優點：一致的介面、網頁，透過單一的網頁來方便管理以及加強SEO
	- 缺點：開發上要在同一份網頁上考量更多更複雜的因素以及能呈現的內容有限
- AWD概念：根據螢幕尺寸的不同而區分出不同版本的網站，每個版本的網站皆適應特定螢幕尺寸。
	- 優點：每一種獨立出來的網頁可以針對特定螢幕尺寸做更大的優化
	- 缺點：維護上會因為版本區分太多而使其成本更大且不易管理

## Mobile first and breakpoint

在這裡只針對RWD來討論，RWD的核心是Mobile First，得優先考量最小尺寸的裝置-手機，在尺寸較小的情況下，什麼內容最應該先被呈現，隨後等考量的尺寸慢慢變大時，再來增加更多呈現內容，然而每一種裝置的尺寸都不盡相同，因此會依照統計的方式來對每一種裝置的尺寸再一次分好幾類來方便開發，每一類會以某種特定尺寸標準或者breakpoint來區分目前裝置是屬於哪一類，常見的breakpoint會以320px、480px、720px、768px、960px、1024px等等作為寬度來區分，這種breakpoint適用於比較大型的內容排版，因此被稱之為major breakpoint。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629897360/blog/rwd/majorBreakPoint_euitnt.png)

開發上可以根據每一種breakpoint來設計不同的內容排版，然而除了會以單一值的breakpoint作為區分以外，同一種breakpoint的排版可能又會因為實際裝置尺寸而使部分元件排版跑掉，比如元素的邊距、文字超過頁面寬度等等，因此又會多區分一個breakpoint，而這個breakpoint主要適用於比較細微的排版，而因此被稱之為minor breakpoint

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629897366/blog/rwd/minorAndMajorBreakPoint_lg8fps.png)

## breakpoint 實作方式：

其實作會以@media語法來達成，該語法會帶有使用裝置條件式(Media Queries)以及一些CSS屬性，當此語法被讀取時會判斷目前使用裝置是什麼以及其尺寸是為何來判定是否滿足於條件式，若滿足的話，則將採用CSS-Code。
```
@media not|only mediatype and (mediafeature and|or|not mediafeature) {
  CSS-Code;
}
```

在這裡的mediatype可以是all、print、screen、speech，而mediafeature可以是min-width、max-width、min-height、max-height、orientation=portrait、orientation=landscape等特徵值，這些特徵的說明分別如下所示，而and、or、not則是指邏輯條件上的且、或、不是。

```
1. min-width 用於任何寬度大於或等於設定值的瀏覽器。
2. max-width 用於任何寬度小於或等於設定值的瀏覽器。
3. min-height 用於任何高度大於或等於設定值的瀏覽器。
4. max-height 用於任何高度小於或等於設定值的瀏覽器。
5. orientation=portrait  用於任何高度大於或等於寬度的瀏覽器。
6. orientation=landscape 用於任何寬度大於高度的瀏覽器。
```

範例：
- 若使用裝置的螢幕尺寸小於等於600px，則採用styles
```
@media (max-width: 600px) { .../* styles */ }
```
- 若使用裝置是螢幕且螢幕尺寸小於等於600px，則採用styles
```
@media screen and (max-width: 600px) { .../* styles */ }
```

- 若使用裝置是螢幕且螢幕尺寸是大於等於600px且小於等於1000px的話，則採用於styles
```
@media screen and (min-width: 600px) and (max-width: 1000px) { .../* styles */}
```

除此以外，Media Queries也可以搭配負責載入外部資源的@import，當滿足於Media Queries的話，就會載入外部資源，否則就不載入。

```
@import url|string list-of-mediaqueries;
```

範例：當使用裝置是螢幕且尺寸小於等於670px時，便載入styles.css至目前檔案中。

```
@import url('styles.css') screen and (max-width: 670px);
```


Draft:
1. 定義預設的 viewport 尺寸: viewport
2. media queries



Note:
1. google 在2015年宣布"行動裝置友善"網站的搜尋排序將優於傳統網站，並提供行動指南以及檢測網站行動裝置友善的網站。
- 行動指南： https://developers.google.com/webmasters/mobile-sites/
- 檢測網站行動裝置友善的網站：https://search.google.com/test/mobile-friendly

Question:
1. breakpoint為啥會以寬度作為標準？
2. media和link的效能
