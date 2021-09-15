---
title: Semester2-2_U21-U23
tags:
---

## em 標籤
1. html的標籤之一，屬性inline元素
2. 用途是以特定樣式來強調一行內的文字




## 匿名函式的壞處
1. 除錯會無法顯示發出錯誤訊息的函式名稱
2. 不好自行指定函式做些特定處理，比如對指定函式做記憶體釋放
3. 將函式物件分隔開來，以作後續維護開發，


接著函式命名方式會是表示panel被點擊時

例子： 假設要綁定一個事件處理器至dataPanel上的點擊事件，那麼可以透過函式名來當參數，

```
dataPanel.addEventListener('click', onPanelClicked)
```

並獨立宣告定義一個和參數名一樣的函式，其函式會是事件處理器的內容，而當點擊事件發生時，系統會預設將一個event 物件給函式onPanelClicked中的第一個參數

```
function onPanelClicked (event) {

}
// 預設會給onPanelClicked函式一個參數值
```

## Dataset 是種物件
1. 存放所有data-開頭的屬性和屬性值
2. 一個 HTML 屬性上可以包含多個 data set 屬性