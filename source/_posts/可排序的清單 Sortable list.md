---
title: (Project) 可排序的清單 Sortable list
description: 使用者可以隨意拖曳項目到不同位置
date: 2021-03-25
categories: 
- JavaScript
- 作品集
tags: 
- JavaScript
- 作品集
---

![](https://i.imgur.com/PKdS8PJ.png)

**[Demo](https://michael0520.github.io/Storable_List/index.html)**


## 學習到的知識點

### HTML
- `draggable="true"`
- `data-* attribute`
### CSS

### JS
- Drag and Drop API
- `.setAttribute()`
- `.sort()`
- `map()`

## 簡介

使用者可以隨意拖曳項目到不同位置

![](https://i.imgur.com/PKdS8PJ.png)

**[Demo](https://michael0520.github.io/Storable_List/index.html)**



## HTML

### 結構

![](https://i.imgur.com/ZCeJjoU.png)

```htmlembedded=
<body>
    <h1>TOP 10 World's Most Valuable Brands in 2021</h1>
    <p>Drag and drop the items into their corresponding spots</p>
    <!--  JS動態產生ul  -->
    <ul class="draggable-list" id="draggable-list"></ul>
    <button class="check-btn" id="check">
      Check Order
      <i class="fas fa-paper-plane"></i>
    </button>
</body>
```



## JS
**[完整 JS Code](https://github.com/Michael0520/Storable_List/blob/gh-pages/all.js)**

### 宣告變數

> JS

```javascript=
const draggable_list = document.getElementById("draggable-list");
const check = document.getElementById("check");

const richestPeople = [
  "珍煮丹黑糖飲品專賣",
  "陳三鼎黑糖青蛙鮮奶創始店",
  "春水堂人文茶館 Chun Shui Tang",
  "樺達奶茶 Huada Milk Tea",
  "十杯手作茶飲",
  "郭姐茶坊",
  "廖媽媽珍珠奶茶",
  "Queenny葵米 珍珠飲品專售",
  "雙妃奶茶",
  "迷客夏綠光牧場主題飲品",
];

// Store listitems
const listItems = [];

let dragStartIndex;
```

> jQuery

```javascript=
const draggable_list = $('#draggable-list')[0]
const richestPeople = [
  "珍煮丹黑糖飲品專賣",
  "陳三鼎黑糖青蛙鮮奶創始店",
  "春水堂人文茶館 Chun Shui Tang",
  "樺達奶茶 Huada Milk Tea",
  "十杯手作茶飲",
  "郭姐茶坊",
  "廖媽媽珍珠奶茶",
  "Queenny葵米 珍珠飲品專售",
  "雙妃奶茶",
  "迷客夏綠光牧場主題飲品",
];

const listItems = [];

let dragStartIndex;
```
### 將資料更新入 DOM 裡

#### 展開運算子
- 展開運算符(Spread Operator)與其餘運算符(Rest Operator)

是ES6中的其中兩種新特性，雖然這兩種特性的符號是一模一樣的，都是`(...)`三個點，
但使用的情況與意義不同。我們常常在文字敘述或聊天時，
這個`(...)`常用來代表了"無言"、"無窮的想像"或"還有其他更多的"的意思。

- 一個是展開陣列中的值
- 一個是集合其餘的值成為陣列

在 [實作電影定位介面](https://hackmd.io/@Michael0520/Movie_Seat_Booking) 時，也有使用到此技巧。

[解構拆解 ( ...arg ) ](https://eyesofkids.gitbooks.io/javascript-start-from-es6/content/part4/rest_spread.html)

#### `.setAttribute()`
`Element.setAttribute(name, value)`

增加指定名稱和值的新屬性，或者把一個現有的屬性設定為指定的值。

[setAttribute用法介紹](https://codertw.com/%E5%89%8D%E7%AB%AF%E9%96%8B%E7%99%BC/289731/)

#### HTML5 中的 data-* attribute 屬性
在製作網頁的過程中，我們常常會添加一些自己需要用到的屬性名稱，
以方便自己容易理解，為了要避免大家在 HTML 結構中隨意的添加屬性，
在 HTML5 中就多了 `data-* attribte` 這個屬性，其中的 * 就是一個可以自定義的名稱。

例如：`data-key='83'` 或者是 `data-item='1'`。
而這邊的範例就是`data-index`。

> JS

```javascript=
createList();

// Insert list items into DOM
function createList() {
  [...powerfulBrands].forEach((company, index) => {
    // listItem為空的陣列，放入powerfulBrands的陣列。
    const listItem = document.createElement("li");

    listItem.setAttribute("data-index", index);

    listItem.innerHTML = `
        <span class="number">${index + 1}</span>
        <div class="draggable" draggable="true">
          <p class="person-name">${company}</p>
          <i class="fas fa-grip-lines"></i>
        </div>
      `;

    listItems.push(listItem);

    draggable_list.appendChild(listItem);
  });
}
```
![示意圖](https://i.imgur.com/Gll7Gtw.png)


> jQuery

```javascript=
.forEach((company, index) => {
      const listItem = document.createElement("li");

      listItem.setAttribute("data-index", index);

      listItem.innerHTML = `
        <span class="number">${index + 1}</span>
        <div class="draggable" draggable="true">
          <p class="company-name">${company}</p>
          <i class="fas fa-grip-lines"></i>
        </div>
      `;

      listItems.push(listItem);

      draggable_list.appendChild(listItem);
    });
}
```

### `random()` 隨機排列 item 順序

這邊使用的方法是

1. 先產生隨機數
2. 再利用`sort()`方法由小排到大
3. 完成每次都能產生隨機排列的順序

- 當只有`.map((a) => ({ value: a, sort: Math.random() }))`時，company 會印出`map()`賦予的`sort()`，可以注意到都是 random( 0 - 1 之間 )的值。

```javascript=
.map((a) => ({ value: a, sort: Math.random() }))
```
![](https://i.imgur.com/qH0hl2n.png)
- `.map()`每個都取得隨機變數後，利用`sort()`由小排到大。
```javascript=
.sort((a, b) => a.sort - b.sort)
```

![](https://i.imgur.com/hoFQZyx.png)

- 排列完大小後，用`map()`來取出值
```javascript=
.map((a) => a.value)
```
![](https://i.imgur.com/9436rPh.png)


[Array.prototype.sort()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

> JS

```javascript=
[...powerfulBrands]
   // array有sort方法，所以利用random產生sort值
  .map((a) => ({ value: a, sort: Math.random() }))
  // 產生了之後，sort方法比大小，這樣每次重整後的順序都會不同
  .sort((a, b) => a.sort - b.sort)
  // 只取得value
  .map((a) => a.value)
  .forEach((person, index) => {
      console.log(person)
```

> jQuery

```javascript=
[...powerfulBrands]
.map(function (data) {
  return {
    value: data,
    sort: Math.random(),
  };
})
.sort(function (a, b) {
  return a.sort - b.sort;
})
.map(function (data) {
  return data.value;
})
```

### 設定事件監聽
[HTML Drag API](https://developer.mozilla.org/zh-TW/docs/Web/API/HTML_Drag_and_Drop_API)

**[ HTML5 Drag and Drop API 筆記](https://hackmd.io/@Michael0520/Drag_and_Drop_API)**

針對能夠被拖曳的元素，在其 HTML 標籤上添加屬性 draggable="true"

以下整理成表格，方便之後判斷。這次實作沒有運用到dropend。

| x | Drag Source | Drag Target | 解釋|
| :----| :---- | :---- | :----|
| 1 | dragstart |  |始拖曳元素時觸發此事件 (點擊元素的瞬間)
| 2 | drag | dragenter |拖曳元素時觸發此事件
| 3 |  | dragover |當元素拖曳到有效位置放置則觸發此事件
| 4 |  | dragleave |拖曳的元素離開有效的位置時觸發
| 5 |  | drop |  |在有效位置上放置元素時觸發此事件(放下元素)
| 6 | dropend |  | 單元格 當拖曳結束時會觸發此事件

> JS

```javascript=
function addEventListeners() {
  const draggables = document.querySelectorAll(".draggable");
  const dragListItems = document.querySelectorAll(".draggable-list li");

  draggables.forEach((draggable) => {
    draggable.addEventListener("dragstart", dragStart);
  });

  dragListItems.forEach((item) => {
    item.addEventListener("dragover", dragOver);
    item.addEventListener("drop", dragDrop);
    item.addEventListener("dragenter", dragEnter);
    item.addEventListener("dragleave", dragLeave);
  });
}

check.addEventListener("click", checkOrder);
```

> jQuery
> 
:bug: 未來再回頭來查看如何更改為 jQuery UI
[jQuery UI drog 套件](https://www.runoob.com/jqueryui/api-draggable.html)

#### `dragEnter()，dragLeave()`

- `dragenter()`，拖曳元素時觸發的事件。
- `dragleave()`，拖曳的元素離開有效的位置時觸發。

這邊做出的效果是，當拖曳的元素到其他元素上時，會變色。拖曳第一欄到第二欄上時，第二欄就變色。

![](https://i.imgur.com/yYUnDtS.png)


但是當拖曳欄位不在有效範圍時，第二欄的欄位就不會變色。

![](https://i.imgur.com/Zq7pJjU.png)

> JS

```javascript=
function dragEnter() {
  // console.log('Event: ', 'dragenter');
  this.classList.add("over");
}

function dragLeave() {
  // console.log('Event: ', 'dragleave');
  this.classList.remove("over");
}
```

#### `dragStart()，dragDrop()`

- `.closet` : 是一個遍歷的方法，簡單來說就是尋找一個最近的元素

[closet 詳細解說](https://www.w3school.com.cn/jquery/traversing_closest.asp)

- `.getAttribute()`: 增加指定名稱和值的新屬性，所以可以得到 index。

- `dragstart()` : 開始拖曳元素時觸發此事件。
- `drop()` :在有效位置上放置元素時，觸發此事件。
當開始拖曳元素欄位時，就開始記錄 Index，停止拖曳元素時，也記錄當下的 Index。

再利用 `swapItems()`，交換內容。

```javascript=
function dragStart() {
  // console.log('Event: ', 'dragstart');
  dragStartIndex = +this.closest("li").getAttribute("data-index");
  console.log(dragStartIndex)
}

function dragDrop() {
  // console.log('Event: ', 'drop');
  const dragEndIndex = +this.getAttribute("data-index");
  swapItems(dragStartIndex, dragEndIndex);
  this.classList.remove("over");
}
```
當我移動第一個時，`dragStartIndex`的改變，就會跳出 0,1,2,3 以此類推。

![](https://i.imgur.com/IfeYdU7.png)


#### `dragOver()`
避免預設行為，才使用`swapItems()`避免被觸發提交。

`dragOver()` ，當元素拖曳到有效位置放置則觸發此事件。
在 dragOver 函式裡加上避免預設行為的`preventDefault()`，避免被持續觸發。

```javascript=
function dragOver(e) {
  // console.log('Event: ', 'dragover');
  e.preventDefault();
}
```

#### `SwapItems()`
交換 items，使用到`appendChild()`方法。

**注意是拖曳的 listItems[1] 要去替換掉原先的 listItems[0]**
所以 [fromIndex] => 新增上 itemTwo ; [toIndex] => 新增上 itemOne

```javascript=
//Swap list items that are drag and drop
function swapItems(fromIndex, toIndex) {
  const itemOne = listItems[fromIndex].querySelector(".draggable");
  const itemTwo = listItems[toIndex].querySelector(".draggable");

  // console.log(itemOne, itemTwo);
  listItems[fromIndex].appendChild(itemTwo);
  listItems[toIndex].appendChild(itemOne);
}
```
### 檢查順序是否正確 
- `trim()`將字串去除空白
> JS

```javascript=
// Check the order of list items
function checkOrder() {
  listItems.forEach((listItem, index) => {
    const randomBrands = listItem.querySelector(".draggable").innerText.trim();

    if (randomBrands !== powerfulBrands[index]) {
      listItem.classList.add("wrong");
    } else {
      listItem.classList.remove("wrong");
      listItem.classList.add("right");
    }
  });
}

check.addEventListener("click", checkOrder);
```



## CSS

先做 JS 動態更新資料上去後，再回頭來新增樣式

**[完整 CSS Code](https://github.com/Michael0520/Storable_List/blob/gh-pages/style.css)**

### 取消預設 list 樣式
```css=
list-style-type: none;
```

### 放大縮小元素比例 
`flex:flex-grow flex-shrink flex-basic`

- flex: 放大比例 縮小比例 計算元素是否有多餘空間，預設值為auto。

`flex:1`的意思為`flex: 1 1 0`：
數字與`<i class="fas fa-grip-lines"></i>`的空間，最小最大都會是1，所以不會變形。

[flex-css 詳細解說](https://developer.mozilla.org/zh-CN/docs/Web/CSS/flex)

```css=
.draggable-list li {
    background-color: #fff;
    display: flex;
    flex: 1;
}
.draggable {
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 15px;
    flex: 1;
}
```

### Check Button 按下開啟放大動畫 & 取消預設邊框

```css=
.check-btn:active {
    transform: scale(0.98);
}
.check-btn:focus {
    outline: none;
}
```

## 參考文章

[flex-css 詳細解說](https://developer.mozilla.org/zh-CN/docs/Web/CSS/flex)


[解構拆解 ( ...arg ) ](https://eyesofkids.gitbooks.io/javascript-start-from-es6/content/part4/rest_spread.html)

[setAttribute用法介紹](https://codertw.com/%E5%89%8D%E7%AB%AF%E9%96%8B%E7%99%BC/289731/)


[closet 詳細解說](https://www.w3school.com.cn/jquery/traversing_closest.asp)

[Array.prototype.sort()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

[HTML Drag API](https://developer.mozilla.org/zh-TW/docs/Web/API/HTML_Drag_and_Drop_API)

**[ HTML5 Drag and Drop API 筆記](https://hackmd.io/@Michael0520/Drag_and_Drop_API)**

[jQuery UI drog 套件](https://www.runoob.com/jqueryui/api-draggable.html)
