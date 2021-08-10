---
title: CodeWars Learning - Take a Ten Minute Walk
date: 2021-08-10 22:09:46
tags:
 - JavaScript
categories: CodeWars
---
## Description

You live in the city of Cartesia where all roads are laid out in a perfect grid. You arrived ten minutes too early to an appointment, so you decided to take the opportunity to go for a short walk. The city provides its citizens with a Walk Generating App on their phones -- everytime you press the button it sends you an array of one-letter strings representing directions to walk (eg. ['n', 's', 'w', 'e']). You always walk only a single block for each letter (direction) and you know it takes you one minute to traverse one city block, so create a function that will return true if the walk the app gives you will take you exactly ten minutes (you don't want to be early or late!) and will, of course, return you to your starting point. Return false otherwise.


Note: you will always receive a valid array containing a random assortment of direction letters ('n', 's', 'e', or 'w' only). It will never give you an empty array (that's not a walk, that's standing still!).


## Solution

將東南西北(e、s、w、n)當作x-y座標軸的正負方向，北方和南方是y軸，而東方和西方為x軸，而自己的出發點轉換成(0,0)的座標軸，每當自己往北方走時，y軸的座標就+1；當自己往南方走時，y軸的座標就-1。而自己往東方走時，x軸的座標就+1；反之，自己往西方走時，x軸的座標就-1。當自己走完指定的方向和步數後，其座標還仍為(0,0)就代表著散完步回到出發地。



根據這樣子的規則，我們可以先宣告axis這陣列來定義x-y這兩個座標軸，並且利用陣列內建的foreach以及switch來遍歷自己所走過的方向以及計算當前的座標軸。最後遍歷完之後在檢查看看x-y這兩個座標軸是否皆為0，若為0的話，就是回到出發點或者true，否則就是false。


另外就是題目還指定自己走的步數得是10步，不得少於10步或者多於10步，因此會設定以下的條件式來防止這件事：
```
if (walk.length != 10) {
	return false
} else {
	do something
}
```

整體程式碼為：

```
function isValidWalk(walk) {
  //insert brilliant code here
  
  if (walk.length != 10) {
      return false
  } else {
    let axis = [0, 0]
    
    walk.forEach( element => {
        switch (element) {
            case 'n':
              axis[0]++
              break
            case 's':
              axis[0]--
              break
            case 'e':
              axis[1]++
              break
            case 'w':
              axis[1]--
              break
            }
           
    })

    return axis[0] === 0 && axis[1] === 0
    
  }
  
}
```

另一種解法：



```
```
function isValidWalk(walk) {
  function count(val) {
    return walk.filter(function(a){return a==val;}).length;
  }
  return walk.length==10 && count('n')==count('s') && count('w')==count('e');
}

```
```

