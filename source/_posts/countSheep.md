---
title: CodeWars Learning - Counting sheep
date: 2021-08-09 23:20:27
tags: JavaScript
categories: CodeWars
---

## Description

Consider an array/list of sheep where some sheep may be missing from their place. We need a function that counts the number of sheep present in the array (true means present).


For example,

```
[true,  true,  true,  false,
  true,  true,  true,  true ,
  true,  false, true,  false,
  true,  false, false, true ,
  true,  true,  true,  true ,
  false, false, true,  true]
```

The correct answer would be 17.

Hint: Don't forget to check for bad values like null/undefined


## Solution

先宣告兩個變數(numSheep和realNumSheep)來分別存放陣列的長度以及羊的實際數量，其中
realNumSheep被指派為0，接著再利用for迴圈結構來遍歷陣列的元素尋找true的部分，元素為true時，便讓realNumSheep增加，這個直到系統遍歷完整個陣列，即可獲得羊的真實數量。

```
function countSheeps(arrayOfSheep) {
  // TODO May the force be with you
  let numSheep = arrayOfSheep.length
  let realNumSheep = 0
  for (let index = 0; index < numSheep; index++) {
      if (arrayOfSheep[index] === true)
        realNumSheep++
  }
  
  return realNumSheep
}
```


## Clever Solution

與上個解法不同，

```
function countSheeps(arrayOfSheeps) {
  return arrayOfSheeps.filter(Boolean).length;
}
```
