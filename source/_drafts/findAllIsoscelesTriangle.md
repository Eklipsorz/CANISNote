---
title: findAllIsoscelesTriangle
tags:
---


我將條件化簡成以下形式來寫在三邊總長20以內尋找所有等邊三角形
```
2 * lengthAB  > lengthC
```

原本程式碼如下所示：
```
// 宣告一個變數來計算等腰三角形的數量，一開始先設定為0
let isoscelesTriangleCount = 0

// 由於有兩邊等長，排列組合上只需要用到一個for迴圈來排出兩個等長的邊之所有可能
// 在這裡lengthAB一同代表著A邊和B邊
for (let lengthAB = 1; lengthAB <= 9; lengthAB++) {

// 在確定兩邊長度以及周長只能在20以內之下，剩餘的邊長最大會到哪
  let maxOfLengthC = 20 - lengthAB * 2 
// 利用for迴圈來排出lengthC在確定兩邊長度以及周長只能在20以內之下的所有可能
  for (let lengthC = 1; lengthC <= maxOfLengthC; lengthC++) {
      // 排除掉三邊等長來增加效能
      if (lengthAB !== lengthC && (2 * lengthAB) > lengthC) {
        
        console.log(`發現等腰三角形！三邊長分別為：${lengthAB}、${lengthAB}、${lengthC}`)
        // 來計算等腰三角形的數量
        isoscelesTriangleCount += 1
      }
  }

}
// 印出總共發現多少個等腰三角形
console.log(`共找到 ${isoscelesTriangleCount} 組等腰三角形`)
```

若繼續使用以上條件式來簡化，可以再一次簡化第三邊的最大長度，首先在滿足條件的三邊下來枚舉後續可能：

```
lengthAB = 1,	lengthC = none
lengthAB = 2,	lengthC = 1
	   .,		  .
	   2,	lengthC	= 3
lengthAB = 3,	lengthC = 1
	   .,		  .
	   3,	lengthC = 5
lengthAB = 4,	lengthC = 1
	   .,		  .
	   4,	lengthC = 7
lengthAB = 5,	lengthC = 1
	   .,		  .
	   5,	lengthC = 9

```
枚舉到length = 5時，三邊總和已經來到19，若要再進一步發展至20的話，只有三邊中任一邊有多加1，但任何一邊加1都會違反三角形的組成或者條件，所以由此可以定論lengthC最大可以到9。

也就是說可以把以下式子省略，
```
maxOfLengthC = 20 - (lengthAB * 2)
```

修改成

```
for (let lengthAB = 1; lengthAB <= 9; lengthAB++) {
	for (let lengthC = 1; lengthC <= 9; lengthC++) {
		if (lengthAB !== lengthC &&
		   (2 * lengthAB) > lengthC && 
		   (2 * lengthAB + lengthC) <= 20 ) {
				
			dosomthing
	
		}
	}

}
```
