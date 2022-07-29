---
title: Expense Tracker
description: 可以紀錄支出與收入的記帳簿。
date: 2021-02-23
categories:
- JavaScript
- 作品集
tags: 
- JavaScript
- 作品集
---


# Expense Tracker

## 使用到的技能樹

### HTML
- label
### CSS
- first-of-type
- input [type=" "]
- outline
### JS
- jQuery
- map()，filter()，reduce()
- math.random()
- math.floor()
- LocalStorage

## 簡介

### [Demo](https://michael0520.github.io/Expense_Tracker/index.html)
可以紀錄支出與收入的記帳簿。
![](https://i.imgur.com/OmsGG2R.png)


## HTML

### 上半部架構
![](https://i.imgur.com/aozmZ1k.png)

```htmlembedded=
    <h2>Expense Tracker</h2>

    <div class="container">
      <h4>Your Balance</h4>
      <h1 id="balance">$0.00</h1>

      <div class="inc-exp-container">
        <div>
          <h4>Income</h4>
          <p id="money-plus" class="money plus">+$0.00</p>
        </div>
        <div>
          <h4>Expense</h4>
          <p id="money-minus" class="money minus">-$0.00</p>
        </div>
```

### 下半部架構

#### js 動態增加 li
![](https://i.imgur.com/ExlbcZk.png)

```htmlembedded=
 <h3>History</h3>
        <ul id="list" class="list">
          <li class="minus">
            Cash <span>-$400</span><button class="delete-btn">x</button>
          </li>
        </ul>
```

#### 表單輸入框與 submit 按鈕
![](https://i.imgur.com/XryPhar.png)

```htmlembedded=
<h3>Add new transaction</h3>
        <form id="form">
          <div class="form-control">
            <label for="text">Text</label>
            <input type="text" id="text" placeholder="Enter text..." />
          </div>

          <div class="form-control">
            <label for="amount"
              >Amount <br />
              (negative - expense , positive - income)
            </label>
            <input type="number" id="amount" placeholder="Enter amount..." />
          </div>
          <button class="btn">Add transaction</button>
        </form>
```

## CSS

### 設立常用顏色變數＆起手式

```css=
:root {
    --box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
}

* {
    box-sizing: border-box;
}

body {
    background-color: #f7f7f7;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    margin: 0;
    font-family: sans-serif;
}
```

### 快速置中

30px 為上下預留的距離，左右使用 auto，讓網頁自己計算就會達成置中的效果。

```css=
.container {
  margin: 30px auto;
  width: 350px;
}
```

### first-of-type選擇器

這邊的效果為，選擇到 income 的 div，所以使用到 first-of-type，然後在使用 border-right。
![](https://i.imgur.com/JMBEMUX.png)

```css=
.inc-exp-container > div:first-of-type {
  border-right: 1px solid #dedede;
}
```

### 用 type 選擇 input

可以快速篩選元素，去加上樣式
```css=
input[type='text'], input[type='number'] {
    border: 1px solid #dedede;
    border-radius: 2px;
    display: block;
    font-size: 16px;
    padding: 10px;
    width: 100%;
}
```
### opacity 來預設消失元素，使用偽元素來條件式顯示

```css=
.delete-btn {
/* 預設消失 */
    opacity: 0;
/*   0.3 秒後顯示出，增加使用者體驗   */
    transition: opacity 0.3s ease;
}

/* 滑鼠滑入後來顯示 */
.list li:hover .delete-btn {
    opacity: 1;
}
```



### 去除點選的預設外框

瀏覽器都會有個預設外框，
outline 設定為 0，就可以取消了

```css=
.btn:focus,
.delete-btn:focus {
  outline: 0;
}
```

以下為此專案的完整 CSS code ：

```css=
:root {
    --box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
}

* {
    box-sizing: border-box;
}

body {
    background-color: #f7f7f7;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    margin: 0;
    font-family: sans-serif;
}

.container {
    margin: 30px auto;
    width: 350px;
}

h1 {
    /* 字首 1px */
    letter-spacing: 1px;
    margin: 0;
}

h3 {
    border-bottom: 1px solid #bbb;
    padding-bottom: 10px;
    margin: 40px 0 10px;
}

h4 {
    margin: 0;
    text-transform: uppercase;
}

.inc-exp-container {
    background-color: #fff;
    box-shadow: var(--box-shadow);
    padding: 20px;
    display: flex;
    justify-content: space-between;
    margin: 20px 0;
}

.inc-exp-container>div {
    flex: 1;
    text-align: center;
}

.inc-exp-container>div:first-of-type {
    border-right: 1px solid #dedede;
}

.money {
    font-size: 20px;
    letter-spacing: 1px;
    margin: 5px 0;
}

.money.plus {
    color: #2ecc71;
}

.money.minus {
    color: #c0392b;
}

label {
    display: inline-block;
    margin: 10px 0;
}

input[type='text'], input[type='number'] {
    border: 1px solid #dedede;
    border-radius: 2px;
    display: block;
    font-size: 16px;
    padding: 10px;
    width: 100%;
}

.btn {
    cursor: pointer;
    background-color: #9c88ff;
    box-shadow: var(--box-shadow);
    color: #fff;
    border: 0;
    display: block;
    font-size: 16px;
    margin: 10px 0 30px;
    padding: 10px;
    width: 100%;
}

.btn:focus .delete-btn:focus {
    outline: 0;
}

.list {
    list-style-type: none;
    padding: 0;
    margin-bottom: 40px;
}

.list li {
    background-color: #fff;
    box-shadow: var(--box-shadow);
    color: #333;
    display: flex;
    justify-content: space-between;
    position: relative;
    padding: 10px;
    margin: 10px 0;
}

.list li.plus {
    border-right: 5px solid #2ecc71;
}

.list li.minus {
    border-right: 5px solid #c0392b;
}

.delete-btn {
    cursor: pointer;
    background-color: #e74c3c;
    border: 0;
    color: #fff;
    font-size: 20px;
    line-height: 20px;
    padding: 2px 5px;
    position: absolute;
    top: 50%;
    left: 0;
    transform: translate(-100%, -50%);
    opacity: 0;
    transition: opacity 0.3s ease;
}

.list li:hover .delete-btn {
    opacity: 1;
}
```


## JS

練習 jQuery ，以下將 JS 轉換為 jQuery
### 設定變數

> 原生 JS

```javascript=
const balance = document.getElementById("balance");
const money_plus = document.getElementById("money-plus");
const money_minus = document.getElementById("money-minus");
const list = document.getElementById("list");
const form = document.getElementById("form");
const text = document.getElementById("text");
const amount = document.getElementById("amount");
```

> jQuery

```javascript=
$('#balance')
$('#money-plus')
$('#money-minus')
$('#list')
$('#form')
$('#text')
$('#amount')
```

### 新增資料到 list 上測試

```javascript=
const dummyTransactions = [
 { id :1 , text :'Flower',amount :12 },
 { id :2 , text :'box', amount : -500 },   
]
```

**函式的概念**
1. 判斷輸入的符號 (sign) 為正或負數，產生新的li
2. 判斷輸入的值為正或負數(item)
3. 判斷完後，將 item 放到 list 上

`Math.abs()` 會傳回絕對值
```javascript=
// 新增陣列，測試addTransactionDOM()是否可以運行
const dummyTransactions = [
 { id :1 , text :'Flower',amount :12 },
 { id :2 , text :'box', amount : -500 },   
]

let transactions = dummyTransactions;

// Add transactions to DOM list
// 將動態資料轉換成 li 放到 list
function addTransactionDOM(transaction) {
  // Get sign
  // if 判斷式縮寫 `?(true 執行):(false 執行)`
  // if(transaction.amount < 0) sign 就是 -
  const sign = transaction.amount < 0 ? "-" : "+";
  // 產生新的 li 元素
  const item = document.createElement("li");

  // Add class based on value
  // 把產生新的 li 元素加上 class
  // 判斷當 transactions的value，amount < 0 放minus，> 0 放plus
  item.classList.add(transaction.amount < 0 ? "minus" : "plus");
  
  // 將資料動態讀入，使用${}讀取變數。
  item.innerHTML = `
        ${transaction.text} <span>${sign}${Math.abs(transaction.amount)}
        </span> <button class = "delete-btn" >x</button>
       `;

  //使用appenChild，將item接在list
  list.appendChild(item);
}
```

#### init()

使 transactions (預先做好的資料)，每一筆都丟到    addTransactionDOM()。

預設 listinnerHTML = ""為空值，不設定的話會出現HTML 裡預設的 Cash -400。

> 原生Js

```javascript=
//Init app
function init() {
  // 預設 list 為空，不設定的話會出現 HTML 裡設定 Cash 的 -400 元
  list.innerHTML = "";
  // 將 transactions 裡面的每一筆資料
  // 都執行 addTransactionDOM()
  transactions.forEach(addTransactionDOM);
}

init();
```

### 設定總金額，支出，收入的元素


- `map()`需要回傳一個值，他會透過函式內所回傳的值組合成一個陣列。
- `reduce()` 方法像是一個累加器，可以陣列中每項元素（由左至右）傳入回呼函式，將陣列化為單一值。
- `filter()` 會回傳一個陣列，其條件是 return 後方為 true 的物件，適合用在搜尋符合條件的資料(本範例都是用來搜尋符合的資料)。

>語法：**`.reduce((acc, item) => (acc += item), 0)`**
>> 最後面的 0，是第一次呼叫 callback 時，要傳入的累加器的初始值。若沒有提供初始值，
則原陣列的第一個元素將會被當作初始的累加器。
但最好是都給一個初始值，必免有 bug，目前在這邊的程式不會影響到。


#### updateValues()

1. 使用`map()`取得新函數，函數裡有每一個函數的 amout 數值(未加總)。
2. 使用`reduce()`加總每一個 amout 數值，放到 total 變數，
3. 以 income 做範例，所以先使用`filter()`過濾資料，取得大於0的數。
4. 再來，用`refuce()`加總。
5. `toFixed()`取的小數第二位。
6. 把處理好的 income,total, expense 放到 DOM 裡面更新文字。

```javascript=
// Update the balance,income and expense
function updateValues() {

  // 使用 map 方法回傳一個新 Array，他的內容是舊 Array 的 amount 值
  const amounts = transactions.map((transaction) => transaction.amount);
  
  // 用 reduce 方法，加總所有值的 amount，並 toFixed(2) 取到小數第二位
  // acc += item -> acc = acc + item
  const total = amounts.reduce((acc, item) => (acc += item), 0).toFixed(2);
  const income = amounts
  
    // .filter取得大於零的值
    .filter((item) => item > 0)
    
    // .reduce將 >0 的值 (income) 加總
    .reduce((acc, item) => (acc += item), 0)
    .toFixed(2);

  const expense = (
    amounts
    
    // .filter 取得大於零的值
    .filter((item) => item < 0)
    
    // .reduce 將 <0 的值 (expense) 加總
    .reduce((acc, item) => (acc += item), 0) *
    -1
  ).toFixed(2);
  
  // 將動態更新好的 income, total, expense 放到DOM裡面更新文字
  balance.innerText = `$${total}`;
  money_plus.innerText = `$${income}`;
  money_minus.innerText = `$${expense}`;
}

// Init app
function init() {
  list.innerHTML = "";
  transactions.forEach(addTransactionDOM);
  
  // 要呼叫 updateValues 函式
  updateValues();
}
```

> jQuery

- innerText =改成.text()

```javascript=
function updateValues() {
  const amounts = transactions.map((transaction) => transaction.amount);
  const total = amounts.reduce((acc, item) => (acc += item), 0).toFixed(2);
  const income = amounts

    .filter((item) => item > 0)
    .reduce((acc, item) => (acc += item), 0)
    .toFixed(2);

  const expense = (
    amounts.filter((item) => item < 0).reduce((acc, item) => (acc += item), 0) *
    -1
  ).toFixed(2);
  // balance.innerText = `$${total}`;
  $("#balance").text(`$${total}`);
  $("#money-plus").text(`$${income}`);
  $("#money-minus").text(`$${expense}`);
}
```

#### generateID()

`Math.floor()`會回傳小於等於所給數字的最大整數，
簡單來說就是，**小數無條件捨去到比自身小的最大整數**。

`Math.random()`會隨機產生出 0~1 之間的小數，出來的值永遠不會大於 1。
> 挺方便的隨機產生器

```javascript=
Math.random(); //0.8961082300942438
Math.random(); //0.009676286758744546
```

如果將`Math.random()`產生出來的數，
乘上 2 就會得到 0-2 之間的小數，乘上 3 就會得到 0-3 之間的小數，
再使用`Math.floor()`就會達成無條件取整數。

```javascript=
Math.floor(Math.random()*2); //回傳0或1
Math.floor(Math.random()*3); //回傳0或1或2
Math.floor(Math.random()*5); //回傳0或1或2或3或4
Math.floor(Math.random()*50); //回傳0或1或2或3...或49
```


- 取0-100000000的亂數當作ID。

```javascript=
// Generate random ID
function generateID() {
  return Math.floor(Math.random() * 100000000);
}
```

### 刪除選取的代辦事項

```javascript=
<button class="delete-btn" onclick="removeTransaction(${transaction.id})">
```

假如我們點擊A列表，那A列表的 `transaction.id` 會傳進去 `removeTransaction()` 函式裡。

再使用`filter()`過濾，當原始的 `transaction.id` 們不等於A列表的 id ，就會被回傳。
所以A列表沒有被回傳，再使用`init()`，就被刪除了。

如果沒有呼叫`init()`，畫面是不會重新渲染的，
所以最後要記得加上`init()`函數。


```javascript=
//Remove transaction by ID
function removeTransaction(id) {
  transactions = transactions.filter((transaction) => transaction.id !== id);
  init();
}
```

### submit 監聽事件

> 原生 Js
```javascript=
form.addEventListener("submit", addTransaction);
```

> jQuery

- `.addEventListener("submit",xxx)`轉成`.submit`

```javascript=
$("#form").submit(addTransaction);
```

### 設定 Local Storage 存取資料

從 Localstorage 抓取資料使用 `getItem()`
需要轉換格式使用`JSON.parse`
判斷`getItem()`得到的資料內容是否為空。

```javascript=
const localStorageTransactions = JSON.parse(
  localStorage.getItem("transaction")
);

let transactions =
  localStorage.getItem("transaction") !== null ? localStorageTransactions : [];
```

更新 Localstorage 裡面的資料。

```javascript=
// Update local storage transactions
function updateLocalStorage() {
  localStorage.setItem("transactions", JSON.stringify(transactions));
}
```

在`addTransaction()`，`removeTransaction()`函數裡需要呼叫`updateLocalStorage()`，才能夠更新資料。

