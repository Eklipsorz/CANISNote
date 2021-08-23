---
title: U32note.md
tags:
---


實作切版步驟：
1. 先將設計稿的區塊按照"由大到小，由外到內“原則來分區塊
2. 切分好區塊後，每個區塊內的樣式按照排版、區塊、內容、動畫的規則來設定




提升程式碼可讀性：
1. 按照區塊內的由外而內之層級(排版->區塊->內容->動畫)來將樣式內的屬性分類靠在一起，甚至添加註解來說明，往後開發時，可從外而內找到好的切入點來開發，例子：
```
/*good example*/
/* Basic comment */
.target-classname,
.other-target {
    /* Positioning */
    position: relative;
    top: 100px;
    left: 100px;
    
    /* Display */
    display: flex;
    justify-content: center;
    
    /* Box Model */
    width: 100px;
    height: 20px;
    border-radius: 3px solid #ccc;
    
    /* Font or other */
    font-size: 18px;
    line-height: 20px;
    color: #333;
    background: #fff;
}
```

不好的範例： 想到什麼屬性就加進來，屬性內沒做任何分類，得花更多時間去找切入點。
```
/*bad example*/
.targetClassName, .other-target {
    color: #333;
    font-size: 18px;
    top: 100px;
    left: 100px;
    line-height: 20px;
    display: flex;
    justify-content: center;
    border-radius: 3px solid #ccc;
    background: #fff;
    width: 100px;
    height: 20px;
    position: relative;
}

```
2. CSS 命名建議: 使用Kebab-case，使用-將兩個英文單字分開，如同烤肉串那樣:
```
/* Camel Case，不建議 */
.targetClassName {
  ...
}
/* Kebab Case，建議 */
.target-class-name {
  ...
}

``` 
3. 斷行與空格: 
- 當多個選擇器套用相同樣式時，建議讓每個選擇器逗號後面夾斷行
- 選擇器與括號之間保持一個空格
- 屬性和屬性值之間保持一個空格

```
 /* Bad */
    .class-one, .class-two, .class-three{ 
        position:relative;
    }
/* Good */
    .class-one,
    .class-two,
    .class-three { 
        position: relative; 
    }

```

note:
a. 排版層級: 
- 定位相關(影響區塊在畫面的位置，position、top/right/bottom/left等)
- 畫面流(影響區塊內的水平、垂直排版，display grid/flex、block/inline-block等)

b. 區塊層級:
- 用於定義區塊本身的樣式呈現
- 如width/height、background、box model、padding/margin等

c. 內容層級:
- 用於定義內容文案的樣式
- font: 字型、字體大小等等的樣式
- 字體排版(line-height、text-indent): 有關行距、行縮相關的結構樣式定義
- color：字體顏色定義

d. 動畫層級：
- 可以用來定義動態整體脈絡中的樣式變化，包括動態需要相關的屬性定義、秒數
