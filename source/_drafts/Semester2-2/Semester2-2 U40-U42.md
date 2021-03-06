---
title: Semester2-2  U40-42
tags:
- JavaScript
---

## 迭代器：
1. 是一種允許開發者去遍歷某種容器下的元素物件，而這裡指的迭代是遍歷元素
2. 在ECMAScript 2015的補充內容中，新增兩個協議：iterable protocol、iterator protocol 來妥善分別定義如何讓一個物件變成可迭代的(iterable)/(可被迭代器遍歷的)/是允許js物件能夠自定義自己的迭代行為以及這些可迭代(iterable)的物件如何讓迭代器遍歷他們所存的內容/迭代器協議定義了一種標準的方式來產生一個有限或無限序列的值。
3. Iterable protocol 定義如何讓一個物件變成可迭代的(iterable)/(可被迭代器遍歷的)，具體而言只要在物件a上的key增加[Symbol.iterator]屬性以及對應的屬性值，就能使物件a變成可迭代的，而這個屬性值將會產生一個專門遍歷該物件的迭代器(函式本體)


例子： 下面是未成為iterable的物件，而我們想利用它藉由遍歷來印出1-5這五個數字

```
let range = {
  from: 1,
  to: 5
};
```

若要轉化iterable的物件，就必須添加[Symbol.iterator]屬性以及對應屬性值，其值會定義iterator如何遍歷著obj這物件的元素，內容必須滿足於iterator protocol

```
const range = {
  start: 1,
  end: 5,
};

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

4. iterator protocol 定義著這些可迭代(iterable)的物件如何讓迭代器遍歷他們所存的內容，在這裡的迭代器會是一種物件，它存有next這屬性，而它的屬性值會是無引數函式，而該函式會回傳擁有一至二個屬性的物件，這些屬性分別為value和done，value會是目前遍歷的內容，done則是告知目前還能繼續遍歷，每一次的next呼叫都會讓遍歷到下一個值，假設有三個值要遍歷，那麼只要呼叫三次的next()便能得到這三個值

```
next () {

  // do something

  return {value: value1, done: boolean}

}

```
 

5. 當某個程式碼想要使用某個物件下的迭代器，會先呼叫[Symbol.iterator]()來產生對應物件的迭代器，並且若回傳this的話，便會告訴程式碼說迭代器就是整個物件本身，如同下面的range物件

```

let range = {
  from: 1,
  to: 5,

  [Symbol.iterator]() {
    this.current = this.from;
    return this;
  },

  next() {
    if (this.current <= this.to) {
      return { done: false, value: this.current++ };
    } else {
      return { done: true };
    }
  }
};
```

6. 由於執行 for...of 時會呼叫 @@iterator method，這個 method 會回傳一個 iterator，此 iterator 每次被呼叫時會執行 next method 來回傳一個物件，這個物件的格式是 {done: Boolean, value: any}，其中



參考資料：
https://javascript.info/iterable#array-from
https://www.geeksforgeeks.org/javascript-iterator/
https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Iteration_protocols


## 若物件中的key值與函式名相同時
在這種情況下，可直接將key值和:去除，只留下函式名稱和函式本身，比如：


```
const obj = {

  printSomething: function printSomething(string) {
      console.log(string)
  }

}

```

可直接簡化成


```
const obj = {

  printSomething(string) {
      console.log(string)
  }

}

```
