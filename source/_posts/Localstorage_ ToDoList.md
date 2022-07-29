---
title: (Project) LocalStorage ToDoList 
description: 透過 LocalStorage 來實作代辦事項，擁有可以記錄以及刪除的功能。
date: 2021-02-24
categories:
- JavaScript
- 作品集
tags: 
- JavaScript
- 作品集
---

# Localstorage: ToDoList

## [Demo](https://michael0520.github.io/ToDoList/index.html)
## 說明專案概要

1. 輸入內容
2. 點擊加入待辦事項
3. 下方依照順序列出待辦事項，並可以點擊刪除

![](https://i.imgur.com/Rk4NVJa.png)

```javascript=
<input type="text" class="textClass" placeholder="請填寫代辦內容" />
<input type="button" class="addList" value="加入代辦" />
<ul class="list"></ul>
```

## 特別注意幾點

1. 一開始要給待辦事項清單一個空陣列，避免爆錯誤
2. 一開始就需要更新一次清單
3. 儲存與刪除清單時都要先將陣列轉為字串再 setItem 進 localstorage
4. 待辦事項清單在新增或刪除後已經是以字串的方式儲存，要調用的時候要先轉回原本陣列型別

```javascript=
// 綁定dom
var list = document.querySelector(".list");
var addList = document.querySelector(".addList");
// 待辦事項清單在新增或刪除後已經是以字串的方式儲存，要調用的時候要先轉回原本陣列型別
var data = JSON.parse(localStorage.getItem("toDoList")) || [];

// 監聽與更新
addList.addEventListener("click", saveItem);
list.addEventListener("click", deleteItem);
updateList(data);

// 加入列表,並同步更新網頁與localStorage
function saveItem(e) {
  e.preventDefault();
  var str = document.querySelector(".textClass").value;
// 避免沒輸入資料，就按新增
    if (str.trim() === "") {
    alert("請輸入事項");
  }
// 把輸入的內容設為物件並push到data陣列中
  var todo = {
    content: str,
  };
  data.push(todo);
  // 加入陣列後需要更新清單
  updateList(data);
  // 更新後將資料轉為字串存到 localstorage
  localStorage.setItem("toDoList", JSON.stringify(data));
}

// 更新網頁內容
function updateList(items) {
  str = "";
  var len = items.length;
  for (var i = 0; i < len; i++) {
    str +=
      '<li><a href="#" data-index=' +
      i +
      ">刪除</a> <span>" +
      items[i].content +
      "</span></li>";
  }
  list.innerHTML = str;
}

// 刪除待辦事項
function deleteItem(e) {
  e.preventDefault();
  // 確認點擊的位置是 a 連結也就是"刪除"
  if (e.target.nodeName !== "A") {
    return;
  }
  var index = e.target.dataset.index;
  // 依照index的位置刪除 1 個 item
  data.splice(index, 1);
  localStorage.setItem("toDoList", JSON.stringify(data));
  updateList(data);
}

```