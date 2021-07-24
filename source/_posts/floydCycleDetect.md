---
title: Introduction: Floyd Cycle Detection
date: 2020-07-21  15:05:34 
tags:
---


當你想解決任何一個需要檢測在多個相互連接的元素是否存在著循環結構之場景，比如說
1. 道路模型。
2. 由多個有限狀態所組成的數學模型。
3. 有限輸入下在同一個函式$f(x)$所形成的結果，比如集合為$\\{1,2\\}$，且$f(1)=2$以
及$f(2)=1$，在這裏1和2就透過函式關係形成一個循環結構。


我們可以將這些場景轉化成由多個節點構成的List結構，並且大致區分為兩種不同結構：

1. 擁有循環結構的List結構
![](/img/floydCycleDetect/ListAexample.png)

2. 沒擁有循環結構的List結構

![](/img/floydCycleDetect/ListBexample.png)






