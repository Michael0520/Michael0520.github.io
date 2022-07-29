---
title: (Project) GitHub Finder 
description: 搜索Github用戶，並顯示個人訊息和最新的 Repository。
date: 2021-03-30
categories:
- JavaScript
- 作品集
tags: 
- JavaScript
- 作品集
---

## 功能

- 搜索Github用戶，並顯示個人訊息和最新的Repository。

## 學習到的知識點

- Ajax 實作串接 Github API
- jQuery Ajax

## 簡介

![完成圖](https://i.imgur.com/gooFsQ1.png)

**[Demo](https://)**

## HTML

### 引入 Bootstrap CDN & Bootstrap watch CDN

```html=
    <link
      rel="stylesheet"
      href="https://bootswatch.com/4/litera/bootstrap.min.css"
        />
    <script
      src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta1/dist/js/bootstrap.bundle.min.js"
      integrity="sha384-ygbV9kiqUc6oa4msXn9868pTtWMgiQaeYH7/t7LECLbyPA2x65Kgf80OJFdroafW"
      crossorigin="anonymous"
    ></script>
    <script
      src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.5.4/dist/umd/popper.min.js"
      integrity="sha384-q2kxQ16AaE6UbzuKqyBE9/u/KzioAlnx2maXQHiDX9d4/zp8Ok3f+M7DPm+Ib6IU"
      crossorigin="anonymous"
    ></script>
    <script
      src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta1/dist/js/bootstrap.min.js"
      integrity="sha384-pQQkAEnwaBkjpqZ8RU1fF1AKtTcHJwFl3pblpTlHXybJjHpMYo79HY3hIi4NKxyj"
      crossorigin="anonymous"
    ></script>
```

### 結構

HTML 內容不多，多為用JS動態產生的內容。

```html=
  <body>
    <nav class="navbar navbar-dark bg-primary mb-3">
      <div class="container">
        <a href="#" class="navbar-brand">GitHub Finder</a>
      </div>
    </nav>

    <div class="container searchContainer">
      <div class="search card card-body">
        <h1>Search GitHub Users</h1>
        <p class="lead">
          Enter a username to fetch a user profile and repos from Github
        </p>
        <input
          type="text"
          id="searchUser"
          class="form-control"
          placeholder="GitHub Username..."
        />
      </div>
      <br />
      <div id="profile"></div>
    </div>

    <footer class="mt-5 p-3 text-center bg-light">GitHub Finder &copy;</footer>
  </body>
```

## CSS

使用 [Boots watch](https://bootswatch.com/) CSS UI

## JS

### 宣告變數

> JS

```javascript=
// Search input
const searchUser = document.getElementById("searchUser");
```

### 取得輸入 input 值

```javascript=
// Search input event listener
searchUser.addEventListener("keyup", (e) => {
  // Get input text
  const userText = e.target.value;

  if (userText !== "") {
    console.log(userText);
  }
});
```

### 取得資料

- 過濾取到 API 裡面的資料，使用 keyup 時，會不停的觸發搜尋，如果使用change，輸入完成後按下enter才會執行，就看要做什麼樣的處理去使用監聽事件

- `url('')` 裡面放的資料可以透過網址先觀察，只要更改後面的名字，就可以取到不同人的資料。

![image](https://i.imgur.com/8qakCqW.png)

- `success()` 為成功運行後執行的 function，`insertProfile()`函式利用物件的方法，將 json 檔取出，這邊先過濾一整包資料，因為會出現 no data 的狀況。相較之下， repository 就不會出現沒有資料顯示null的狀況，所以只要這邊做資料過濾就可以。

> `jQuery.ajax(url [, settings])`

| 參數  |  型別  |  說明  |
| -------- | -------- | -------- |
| url  |Quantity | 指定要進行呼叫的位址 |
| data     | Object     | 要傳給 server 的 Key/value 值對     |
| success     | Function     | Ajax 請求完成時 (必需是 success) 呼叫的 callback     |
