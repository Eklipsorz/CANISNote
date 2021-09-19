---
title: Semester2-2  U40-42
tags:
- JavaScript
---

## 迭代器：
1. 是一種允許開發者去遍歷某種容器下的元素物件，而這裡指的迭代是遍歷元素
2. 在ECMAScript 2015的補充內容中，新增兩個協議：iterable protocol、iterator protocol 來妥善定義如何讓一個物件變成可迭代的(iterable)/(可被迭代器遍歷的)以及這些可迭代(iterable)的物件如何讓迭代器遍歷他們所存的內容。
3. Iterable protocol 定義如何讓一個物件變成可迭代的(iterable)/(可被迭代器遍歷的)，具體而言只要在物件a上的key增加[Symbol.iterator]屬性以及對應的屬性值，就能使物件a變成可迭代的


例子： 下面是未成為iterable的物件，而我們想利用它藉由遍歷來印出1-5這五個數字

```
let range = {
  from: 1,
  to: 5
};
```

若要轉化iterable的物件，就必須添加[Symbol.iterator]屬性以及對應屬性值，其值會定義iterator如何遍歷著obj這物件的元素，內容必須滿足於iterator protocol。

```
range[Symbol.iterator] = function() {

  // ...it returns the iterator object:
  // 2. Onward, for..of works only with this iterator, asking it for next values
  return {
    current: this.from,
    last: this.to,

    // 3. next() is called on each iteration by the for..of loop
    next() {
      // 4. it should return the value as an object {done:.., value :...}
      if (this.current <= this.last) {
        return { done: false, value: this.current++ };
      } else {
        return { done: true };
      }
    }
  };
};

```

最後藉著以下程式碼就能印出
```
for (let num of range) {
  alert(num); // 1, then 2, 3, 4, 5
}
```

4. iterator protocol 定義著這些可迭代(iterable)的物件如何讓迭代器遍歷他們所存的內容，會是以函式物件來表示
 
