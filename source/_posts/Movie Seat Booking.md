---
title: (Project) Movie Seat Booking
description: 實作電影訂票系統，包含票價以及訂位功能
date: 2021-02-26
categories:
- JavaScript
- 作品集
tags: 
- JavaScript
- 作品集
---


[Demo](https://michael0520.github.io/Movie-Seat-Booking/index.html)

## HTML

### 建立電影選單

```html=
  <div class="movie-container">
      <label>Pick a movie</label>
      <select id="movie">
        <option value="10">Avengers: Endgame ($10)</option>
        <option value="12">Joker ($12)</option>
        <option value="8">Toy Story 4 ($8)</option>
        <option value="9">The Lion King ($9)</option>
      </select>
    </div>
```

示意圖：
![示意圖](https://i.imgur.com/pL3DdEc.png)

### 建立座位狀態標示

```html=
<ul class="showcase">
      <li >
          <div class="seat"></div>
        <small>N/A</small>
      </li>
      <li >
        <div class="seat selected"></div>
        <small>Selected</small>
      </li>
      <li >
        <div class="seat occupied"></div>
        <small>Occupied</small>
      </li>
</ul>
```

示意圖：
![image](https://i.imgur.com/Papl7Bd.png)

### 建立座位、建立電影螢幕(依照喜好建立數量)

> 以下是實作六個橫排八個直排的座位數量
> 隨機標示座位狀態

```html=
<div class="container">
    <div class="screen"></div>
        <div class="row">
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat occupied"></div>
          <div class="seat occupied"></div>
          <div class="seat occupied"></div>
          <div class="seat"></div>
        </div>
        <div class="row">
          <div class="seat occupied"></div>
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat occupied"></div>
          <div class="seat"></div>
          <div class="seat"></div>
        </div>
        <div class="row">
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat"></div>
        </div>
      </div>
        <div class="row">
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat occupied"></div>
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat"></div>
        </div>
      </div>
        <div class="row">
          <div class="seat occupied"></div>
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat occupied"></div>
        </div>
      </div>
        <div class="row">
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat occupied"></div>
          <div class="seat occupied"></div>
          <div class="seat"></div>
          <div class="seat"></div>
          <div class="seat"></div>
        </div>
    </div>
```

### 建立總價格顯示區塊

```html=
<p class="text">You have selected 
        <!-- 為了顯示總共有選了幾個座位，所以將 0 給綁上 id='count'  -->
        <span id="count">0</span> seats for a price of $
        <!-- 為了顯示總共座位的票卷價格，所以將 0 給綁上 id='total'  -->
        <span id="total">0</span>
</p>
```

html 完成後示意圖：
![image](https://i.imgur.com/fSoMn74.png)

---

## Css

### 選擇 Google fonts 字體

> 選用此字體， import 入 Css

```css=
@import url('https://fonts.googleapis.com/css2?family=Lato:wght@700&display=swap');

/*  因為沒有套入 css reset 所以都務必套入這幾行 Css    */
* {
    box-sizing: border-box;
}

body {
    font-family: 'Lato', sans-serif;
    margin: 0;
}
```

### body Css 撰寫

> 水平置中寫法

```css=
body {
    background-color: #242333;
/* 將所有的 div 排列成直列  */
    display: flex;
    flex-direction: column;
/* 水平置中 */
    align-items: center;
    justify-content: center;
    height: 100vh;
/*      */
    color: #fff;
    font-family: 'Lato', sans-serif;
    margin: 0; 
}
```

### select 下拉式選單加上樣式

> -webkit-appearance，使用系統預設的外觀。
> -webkit-appearance: none，去除瀏覽器的預設樣式。

```css=
.movie-container select {
    background-color: #fff;
    border: 0;
    border-radius: 5px;
    font-size: 14px;
    margin-left: 10px;
    padding: 5px 15px 5px 15px;
/*   注意    */
    -moz-appearance: none;
    -webkit-appearance: none;
    appearance: none;
/*      */
}
```

### 加上座位樣式

```css=
/* 1. 調整座位大小、間距以及背景顏色 */
.seat {
    background-color: #444451;
    height: 12px;
    width: 15px;
    margin: 3px;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
}

/* 2. 讓座位變成橫排 */
.row {
    display: flex;
}
```

#### 單獨修改三種座位樣式的個別顏色

> 因為只有 **'尚未有空位'** 以及 **'座位已被預訂'** 要特定挑出來
> 只需要修改這兩種顏色

```css=
.seat.selected {
    background-color: #6feaf6;
}

.seat.occupied {
    background-color: #fff;
}
```

#### 將座位與其他座位空出距離(看起來像是有走道的樣子)

> 實作：前兩排跟後兩排各有一個走道

1. nth-child()：當選取的元素中間有混雜其他元素，
**像是`<hr>`，在 nth-child 會將其他元素一起做計算**
2. nth-of-type 就較為單純，只會計算選取的元素，
例如選擇`<div>`，就只會選取`<div>`。
3. [`nth-child()` 詳細解說](https://amyhuang-82.medium.com/css%E7%AD%86%E8%A8%98-nth-child%E5%88%B0%E5%BA%95%E6%98%AF%E5%93%AA%E5%80%8B%E5%B0%8F%E5%AD%A9-112a33ad9479)

```css=
.seat:nth-of-type(2) {
    margin-right: 18px;
}
.seat:nth-last-of-type(2) {
    margin-left: 18px;
}
```

![image](https://i.imgur.com/2CYxFNy.png)

#### 讓箭頭滑到座位時，變成手指圖示以及放大(提升使用者體驗)

```css=
.seat:not(.occupied):hover {
    cursor: pointer;
/*  放大 1.2 倍    */
    transform: scale(1.2);
}
```

**這時做完會發現'票卷顯示的座位'滑到時也會大，也會變成手指頭滑鼠**
所以要將'票卷顯示的座位'設定為不放大，手指頭也要去除掉，所以設定為 `cursor: pointer;`

```css=
.showcase .seat:not(.occupied):hover {
    cursor: pointer;
    transform: scale(1);
}
```

### 將票卷顯示列加上樣式

```css=
.showcase {
/* 背景半透明 */
    background-color: rgba(0, 0, 0, 0.1);
    padding: 5px 10px;
    border-radius: 5px;
    color: #777;
    list-style: none;
    display: flex;
/*  讓彼此前方都有個空格    */
    justify-content: space-between;
}

.showcase li {
/* 將票卷圖案以及狀態列變為同一列 */
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 10px;
}

.showcase li small {
    margin-left: 2px;
}
```

![image](https://i.imgur.com/Oj7uMhu.png)

### 電影螢幕加上樣式

```css=
.container {
/* perspective 語法為立體，數字越大越立體 */
    perspective: 1000px;
/* 讓螢幕離座位遠一點    */
    margin-bottom: 30px;

}
.screen {
    background-color: #fff;
    height: 70px;
    width: 100%;
    margin: 15px 0;
/* 翻轉      */
    transform: rotateX(-45deg);
    box-shadow: 0 3px 10px rgba(255, 255, 255, 0.7);
}
```

[rotateX() MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/rotateX())

### 加總文字上樣式

```css=
p.text {
    margin: 5px 0px;
}

p.text span {
    color: #6feaf6;
}
```

Css & HTML 完成圖：

![image](https://i.imgur.com/0e6WJ6l.png)

---

## JS

### 綁定元素

1. const 宣告變數只能一次，不能被更動
2. ticketPrice 不能用 const 宣告，因為 value 之後會更動，所以改用 let
3. parseInt為轉換型別語法，將字串轉為數字，也可以使用 +。

```javascript=
const container = document.querySelector('.container');
const seats = document.querySelectorAll('.row .seat:not(.occupied)')
const count = document.getElementById('count');
const total = document.getElementById('total')
const movieSelect = document.getElementById('movie')

let ticketPrice = +movieSelect.value;
```

### 設定事件監聽

```javascript=
// 點擊後讀取點擊的 container 裡的元素
container.addEventListener("click", e => {
  console.log(e.target);
});
```

### 實作當空位被點選時，變成被選擇的顏色

1. 當選到的空位不是`.occupied`時，加上`selected`的 class
2. 使用 if 判斷式來辨別，按到的是空位條件為 (是空位以及不是被`.occupied`)
 true 的話使用`e.target.classList.toggle`可以打開或是關閉(像是電燈開關)，
3. [classList 詳細解說](http://www.w3big.com/zh-TW/jsref/prop-element-classlist.html)

```javascript=
container.addEventListener('click', e =>{
    if (
        e.target.classList.contains('seat') &&
        !e.target.classList.contains('occupied')
    ) {
        e.target.classList.toggle('selected')
    }
})
```

### 實作動態調整座位數與價錢

> NodeList

會經由 `querySelectorAll()`,`childNodes` 產生
HTMLCollection 會經由 `getElementsByTagName()`,`children` 產生
這兩種皆為類陣列,無法使用陣列型別的 method ,但仍可使用 **索引存取內容**

[NodeList 詳細解說](https://ithelp.ithome.com.tw/articles/10211876)

```javascript=
/*  情境  */

// 點選座位後，讀取到NodeList[]
const selectedSeats = document.querySelectorAll(".row .seat.selected");
// 轉換成1,2,3,4
const selectedSeatsCount = selectedSeats.length;
// 將讀取到的座位數量放到count變數裡
count.innerText = selectedSeatsCount;
```

* 新增 function

```javascript=
// Update total and count
  const updateSelectedCount = (()=>{
      const selectedSeats = document.querySelectorAll('.row .seat.selected')
      const selectedSeatsCount = selectedSeats.length
      count.innerText = selectedSeatsCount
      total.innerText = selectedSeatsCount * ticketPrice
  })

container.addEventListener("click", (e) => {
  if (
    e.target.classList.contains("seat") && !e.target.classList.contains("occupied")
  ) {
    e.target.classList.toggle("selected");
    // if 判定為 true 後來執行此計算價格 function
    updateSelectedCount();
  }
});
```

### 實作動態更換電影時，動態更換價格

```javascript=
// Update total and count
  const updateSelectedCount = (()=>{
      const selectedSeats = document.querySelectorAll('.row .seat.selected')
      const selectedSeatsCount = selectedSeats.length
      count.innerText = selectedSeatsCount
      total.innerText = selectedSeatsCount * ticketPrice
  })

// Movie select event
movieSelect.addEventListener('change', e =>{
    ticketPrice = parseInt(e.target.value)

    updateSelectedCount()
})
```

### 儲存被點選的座位位置

> `[…arr]` 展開運算子。
> ES6 中， “…” 的關鍵字
> 這個關鍵字在不同時間點有不同的效果，
有些時候它會被當作展開運算子  (spread operator) 使用，
有時候則是被當作其餘運算子（rest operator）使用
> 展開運算子，是把許多的 value 轉換成一個新的陣列，
而展開運算子則是可以把陣列中的元素取出。

[解構賦值 Destructuring Assignment 筆記](https://hackmd.io/@uOQ-3fQDQBu7CciMuKIplg/Destructuring_Assignment)

```javascript=
/* Example ...arr */

const arr1 = [1,2,3]
const arr2 = [...arr1,4,5]
console.log(arr2)
// arr2 = [1, 2, 3, 4, 5]

const arr1 = [1,2,3]
const arr2 = [...arr1,4,5]
const arr3 = arr2.map(function(item){
  return item * 2;
})
console.log(arr3)
// arr3 = [2, 4, 6, 8, 10]
```

* 建立 updateSelectedCount function

```javascript=
  const updateSelectedCount = (()=>{
      const selectedSeats = document.querySelectorAll('.row .seat.selected')

// 將藍色座位選取後出現的 nodeList 轉換成 array (Copy seleted seats into array)
// 使用 map 方法印出 array (Map through array)
// 並且使用 indexOf 方法回傳 seat 的索引 (return a new array indexes)
      const seatsIndex = [...selectedSeats].map(( seat => {
          return [...seats].indexOf(seat)
      }))
// 取得座位的位置 ex:[0,1,7,32]
      console.log(seatsIndex)

      const selectedSeatsCount = selectedSeats.length
// How many seats you clicked
      count.innerText = selectedSeatsCount
      total.innerText = selectedSeatsCount * ticketPrice
  })
```

### 使用 Local Storage 存在瀏覽器裡

> Google 開發工具裡的 Application 裡面查看儲存的座位陣列

`locatStorage.setItem(key,value)` 語法，可以將資料寫進瀏覽器裡，
第一個值是 key 的屬性名，第二個值就是相對應的 value

當在 Clent 端操作的 JavaScript 物件要傳遞給 Server 端時，
使用 `JSON.stringify()`將物件（或陣列，甚至是原始型別）序列化為一個 JSON 字串，然後將這個 JSON 字串傳送給 Server 端。

[JSON.stringify 詳細解說](https://cythilya.github.io/2015/05/09/javascript-json-parse-stringify/)

```javascript=
// 加在updateSelectedCount Function裡
localStorage.setItem("selectedSeats", JSON.stringify(seatsIndex));
```

> 可以在Application裡面查看，儲存的 selectedMovieIndex，selectedMoviePrice 陣列。

```javascript=
//Save selected movie index and price

const setMovieData = ((movieIndex,moviePrice)=>{
    localStorage.setItem('selectedMovieIndex',movieIndex)
    localStorage.setItem('selectedMoviePrice',moviePrice)
})
```

### 從Localhost 取資料，使得點選過後的位置可以填充UI

1. 回傳 -1 為，陣列內沒有這個 value 時會回傳索引值。

```javascript=
const arr2 = [1,2,3,4,5]
console.log(arr2.indexOf(100))
// -1
```

1. `Json.parse`將字串轉換成陣列或物件的用法。
2. 把資料存進瀏覽器後，要取出來的話要用 getItem 語法

```javascript=
// Get data from localstorage and populate UI
function populateUI() {

  // 使用getItem取得要使用的key，為上方設定的'selectedSeats'，並指派變數selectedSeats。
  // 使用parse把JSON資料轉換成array
  const selectedSeats = JSON.parse(localStorage.getItem("selectedSeats"));
  
  // 判斷讓藍色座椅是否繼續留著
  // 要使用localstorage裡面儲存的資料判斷是否符合。
  if (selectedSeats !== null && selectedSeats.length > 0) {
  
   // 將所有座位使用forEach一個個印出
   // 並且判斷每個座位的index號碼是否跟selectedSeats的一樣
   // 如果相同則執行加上.selected
    seats.forEach((seat, index) => {
    
    // -1 就是 udefined
      if (selectedSeats.indexOf(index) > -1) {
        seat.classList.add("selected");
      }
    });
  }
 
  // 判斷selectedMovieIndex是否為空
  // 不為空則賦值給selectedMovieIndex下拉式選單選取的電影index
  const selectedMovieIndex = localStorage.getItem("selectedMovieIndex");
  if (selectedMovieIndex !== null) {
    movieSelect.selectedIndex = selectedMovieIndex;
  }
}

```

最後在整個JS最下方呼叫一次updateSelectedCount() 函式，這樣重整網頁時，不需經過事件觸發，直接更新下方文字敘述。
