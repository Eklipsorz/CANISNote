---
title: '(施工中)Introduction: Floyd Cycle Detection'
date: 2020-07-21 15:05:34 
tags:
mathjax: true
---


當你想解決任何一個需要檢測在多個相互連接的元素是否存在著循環結構之場景，比如說


1. 道路模型。
2. 由多個有限狀態所組成的數學模型。
3. 有限輸入下在同一個函式{% mathjax %}f(x){% endmathjax %}所形成的結果，比如集合為{% mathjax %}\{1,2\}{% endmathjax %}，且{% mathjax %}f(1)=2{% endmathjax %}以及{% mathjax %}f(2)=1{% endmathjax %}，在這裏1和2就透過函
式關係形成一個循環結構。

我們可以將這些場景轉化成由多個節點構成的List結構，並且大致區分為兩種不同結構：
1. 擁有循環結構的List結構 
2. 沒擁有循環結構的List結構


當我們轉換成如此的結構時，我們可以更容易以肉眼看出哪些模型存在著循環，在這裏我們可以知道List A是存在著循環，而List B由於尾巴部分並未跟前幾個節點相接，所以不構成循環。在這裡你或許會選擇以肉眼來辨識，但現實是當面對大量或者複雜的模型時，肉眼看會顯得效率太差，所以最好由電腦進行這樣的重複辨識工作。


可換作是電腦，它要如何辨識呢？畢竟他本身就不存在像人眼那樣的辨識模型，在這裏提供一個方法來幫助電腦辨識：Floyd's Cycle Detection Algorithm， 據說是由Robert W. Floyd所發明的演算法，所以以他的名字來命名，普遍上會以演算法的特色來稱呼：龜兔賽跑算法。顧名思義，這個演算法會假設一隻烏龜和 一隻兔子在這個許多節點構成的List結構進行賽跑，烏龜每次只能走一個節點，而兔子只能走二個節點，如果List結構存在著循環，他們只要跑下去肯定能到循環裡，並
且他們肯定能在循環中碰面或者在同一點會合的話。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1627238046/Algorithm/FloydCycleDetect/CycleExample_thhrj4.png)

然而，如果兔子走到結構中的終點卻沒跟烏龜會合的話，那就表示著結構不存著循環。(如下圖)

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1627238048/Algorithm/FloydCycleDetect/NoCycleExample_vnsu18.png)


乍看之下這方法很簡單，但問題是這方法真能判別循環問題嗎？如果你對此也感到懷疑，歡迎到Proof章節來進行討論，但如果沒有的話，我可以告訴你 這方法確實能判別循環問題，而非是運氣，另外也建議讀者您參考Implementation以及Performance這兩個章節來看其代碼以及成本。



## Proof:How it works?

首先我們先來考慮擁有循環的結構(如下圖)，在循環之前可能會有{% mathjax %}N{% endmathjax %}個點或者沒存在任何節點，而這{% mathjax %}N{% endmathjax %}的值會影響著烏龜和兔子在循環中的初始位置，再來為了很好地地瞭解影響，設定了數字來表示循環中的第幾個節點，以{% mathjax %}0{% endmathjax %}到{% mathjax %}\lambda-1{% endmathjax %}來命名，而{% mathjax %}\lambda{% endmathjax %}則是定義成循環中的長度，在這裡{% mathjax %}\lambda=10{% endmathjax %}。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1627238048/Algorithm/FloydCycleDetect/NandCycle_jisqwr.png)

首先我們先考慮著{% mathjax %}N=0{% endmathjax %}時，兔子和烏龜會在循環的起點會合，並從那裡開始進行他們的賽跑。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1627238046/Algorithm/FloydCycleDetect/N0andCycle_hn1hcj.png)

根據兔子走兩步和烏龜走一步的前提，當兔子走完一圈時，烏龜才走半圈，而兔子再走完下一個完整的圈時，這時烏龜才走完一圈，此時他們倆就在一開始的點會合。

在這裡，我們會發現幾個有趣的觀察結果：

1. 兔子得走完一圈才有辦法跟烏龜會合(p.s 他們倆不動也能會合XD，但這不是在該方法的討論範圍內)
2. 兔子{% mathjax %}H{% endmathjax %}的步數會是烏龜{% mathjax %}T{% endmathjax %}的步數之一倍，換言之，{% mathjax %}H=2T{% endmathjax %}。
3.當兔子{% mathjax %}H{% endmathjax %}和烏龜{% mathjax %}T{% endmathjax %}都走到循環內部時，我們可以對{% mathjax %}H{% endmathjax %}和烏龜{% mathjax %}T{% endmathjax %}使用同餘({% mathjax %}mod\ \lambda{% endmathjax %})的概念(如下式)來 確定是否存在循環，若兩者的餘數都一樣那就表示存在著循環；反之，就是不存在。

{% mathjax %} H ≡ T\ (mod\ \lambda) {% endmathjax %}

將第二個觀察結果納入至{% mathjax %} H ≡ T\ (mod\ \lambda) {% endmathjax %}便會是如下式：

{% mathjax %}2T ≡ T\ (mod\ \lambda){% endmathjax %}

統整這三個觀察結果，我們會發現只要{% mathjax %}T=\lambda{% endmathjax %} 代入上式，兔子和烏龜會在第{% mathjax %}0{% endmathjax %}個節點會合。接下來我們思考另一種情況，如果{% mathjax %}N=1{% endmathjax %}時，這種代入結果會不會有所不同？

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1627238047/Algorithm/FloydCycleDetect/N1andCycle_ttrcay.png)

從上圖可以觀察出當烏龜進入循環時的位置跟兔子所在的位置是不同的：兩者相差一個節點，這對於{% mathjax %}N=0{% endmathjax %}所得出的觀察結果而言，我們可以確定兔子還是得走完一圈才有辦法和烏龜在同一點，而第二、三個觀察結果可能會因為這樣而改變。

當烏龜進入循環的起點時，兔子在循環中的位置會變成({% mathjax %}H'{% endmathjax %}為循環中的新位置，{% mathjax %}H{% endmathjax %}為循環中的舊位置)：

{% mathjax %}H' = H + 1{% endmathjax %}

接著第三個觀察結果會因循環外的節點增加而改變成下式：

{% mathjax %}H + 1 ≡ T\ (mod\ \lambda){% endmathjax %}

在兩者移動的過程中，仍然依照烏龜每走一步，兔子就會走兩步這前提，只是現在兔子比起原本多走了一步，所以我們可以將上式更改成：

{% mathjax %}2T + 1 ≡ T\ (mod\ \lambda$){% endmathjax %}

你會發現這與{% mathjax %}N=0{% endmathjax %}所發現的第二、三個觀察結果有些出入，在這裡第二個觀察結果會變成{% mathjax %}H'=2T+1{% endmathjax %}，而第三個觀察結果就是上式。

那麼式子的改變會不會影響與烏龜會合的情況呢？其實只要我們按照圖上位置來模擬他們移動，最後會發現他們的確會在同
一點會合，只是位置變成第{% mathjax %}\lambda-1{% endmathjax %}個位置，在這裡會是循環中編號9的位置，也就是說上式要達到同餘的效果就只有兩者都走到第九個位置(在這裡我們先假定式子的同餘結果會是{% mathjax %}9{% endmathjax %}，後續推理到{% mathjax %}N=M{% endmathjax %}時來驗證)
