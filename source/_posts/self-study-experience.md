---
title: AC平台的自學經驗回顧
date: 2021-12-13 23:07:06
tags:
---


## 引發自學的問題

根據AC平台給予的餐廳平台開發規格來開發其平台的過程中，令我最頭痛的問題就是如何解決以下問題，而這也是這篇文章的開端。
> 使用者在點選刪除按鈕，要有提示視窗提示使用者確定是否刪除，等使用者按下確定刪除才會真的刪除

![示意圖](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1639406983/self-study-experience/example_weayrt.gif)

首先刪除按鈕原本是被一個表單元件所包覆著，而按鈕就是內部的按鈕元件，一般來說當使用者按下刪除按鈕，表單會發生提交事件並做預設事件處理，以POST的方式來轉交資料指定位置至以及導向其指定位置，而我設定的指定位置則是伺服器的合法路由，如下所示：

> /restaurants/{{ this._id }}?_method=DELETE

```
<form action="/restaurants/{{ this._id }}?_method=DELETE" class="delete-form" method="post" data-name="{{this.name}}" style="display: inline;">
      <button type="submit" class="btn btn-danger">Delete</button>
</form>
```

而伺服器當接收到該路由的請求，便會根據路由清單找尋合適的路由來做處理，而這個路由處理的內容如下，主要是根據使用者按下的刪除按鈕之ID來刪除對應的餐廳資料以及重新導向瀏覽所有餐廳的首頁，所以在不做任何處理的情況下，只要刪除按鈕被按下，就會被刪除並重新渲染，而提示視窗的發生必須發生在點擊刪除時才發生，且不能在按下確定之前就刪除餐廳

```
// define route for deleting a restaurant
router.delete('/:id', (req, res) => {

  const reqId = req.params.id

  // find the restaurant by id and delete it
  restaurantModel.findByIdAndRemove(reqId)
    .exec()
    .then(() => res.redirect('/'))
    .catch((error) => console.log(error))
})
```

## 第一次出手與失敗


## 尋找與嘗試


## 努力成果


## 回顧與發現