---
title: (Project) Typing Game
description: 實作打字遊戲，在有限時間內輸入一模一樣文字，每過一道關卡增加難易度！
date: 2021-03-15
categories:
- JavaScript
- 作品集
tags: 
- JavaScript
- 作品集
---

# Typing Game

## 學習到的知識點
### HTML
- `<input autocomplete="off">`
### CSS
- `display:none`
### JS
- `Math.length()`
- `Math.floor()`
- `setInterval()`

## 簡介
**打字遊戲**
> 有限時間內輸入一模一樣文字

 ![](https://i.imgur.com/sgDI5K6.png)
 
 [Demo](https://michael0520.github.io/Typing_Game/index.html)

## HTML

![](https://i.imgur.com/gCRNKAs.png)

```htmlembedded=
 <button id="settings-btn" class="settings-btn">
      <i class="fas fa-cog"></i>
    </button>

    <div id="settings" class="settings">
      <form id="settings-form">
        <div>
          <label for="difficulty">Difficulty</label>
          <select id="difficulty">
            <option value="easy">Easy</option>
            <option value="medium">Medium</option>
            <option value="hard">Hard</option>
          </select>
        </div>
      </form>
    </div>

    <div class="container">
      <h2>⌨️ Speed Typer ⌨️</h2>
      <small>Type the following:</small>

      <h1 id="word"></h1>
      <input
        type="text"
        id="text"
        autocomplete="off"
        placeholder="Type the word here..."
      />
      <p class="time-container">
        Time left:
        <span id="time">10s</span>
      </p>
      <p class="score-container">
        Score:
        <span id="score">0</span>
      </p>
      <div id="end-game-container" class="end-game-container"></div>
    </div>
```
- `autocomplete = 'off'`

意思為不開啟自動提示輸入的預設功能

## CSS

- -webkit- 私有前綴
- -webkit-appearance: none，去除瀏覽器的預設樣式。
- -moz-appearance: none，去除瀏覽器的預設樣式。

### 起手式
```css=
* {
    box-sizing: border-box;
}
body {
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    margin: 0;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
}
```

完整 Code :

```css=
* {
    box-sizing: border-box;
}

body {
    background-color: #2c3e50;
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    margin: 0;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
}

button {
    cursor: pointer;
    font-size: 14px;
    border-radius: 4px;
    padding: 5px 15px;
}

select {
    width: 200px;
    padding: 5px;
    appearance: none;
    -webkit-appearance: none;
    -moz-appearance: none;
    border-radius: 0;
    background-color: #a7c5e3;
}

select:focus, button:focus {
    outline: 0;
}

.settings-btn {
    position: absolute;
    bottom: 30px;
    left: 30px;
}

.settings {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    background-color: rgba(0, 0, 0, 0.3);
    height: 70px;
    color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    transform: translateY(0);
    transition: transform 0.3s ease-in-out;
}

.settings.hide {
    transform: translateY(-100%);
}

.container {
    background-color: #34495e;
    padding: 20px;
    border-radius: 4px;
    box-shadow: 0 3px 5px rgba(0, 0, 0, 0.3);
    color: #fff;
    position: relative;
    text-align: center;
    width: 500px;
}

.container h2 {
    background-color: rgba(0, 0, 0, 0.3);
    padding: 8px;
    border-radius: 4px;
    margin: 0 0 40px;
}

h1 {
    margin: 0;
}

input {
    border: 0;
    border-radius: 4px;
    font-size: 16px;
    font-weight: bolder;
    width: 300px;
    padding: 12px 20px;
    margin-top: 10px;
}

.score-container {
    position: absolute;
    top: 60px;
    right: 20px;
}

.time-container {
    position: absolute;
    top: 60px;
    left: 20px;
}

.end-game-container {
    background-color: inherit;
    display: none;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    position: absolute;
    top: 0;
    left: 0;
    width:100%;
    height: 100%;
    z-index: 1;
}
```

## JS

### 宣告變數

> JS

這邊使用陣列儲存測驗單字。

```javascript=
const word = document.getElementById("word");
const text = document.getElementById("text");
const scoreEl = document.getElementById("score");
const timeEl = document.getElementById("time");
const endgameEl = document.getElementById("end-game-container");
const settingsBtn = document.getElementById("settings-btn");
const settings = document.getElementById("settings");
const settingsForm = document.getElementById("settings-form");
const difficultySelect = document.getElementById("difficulty");

// List of words for game
const words = [
  "sigh",
  "tense",
  "airplane",
  "ball",
  "pies",
  "juice",
  "warlike",
  "bad",
  "north",
  "dependent",
  "steer",
  "silver",
  "highfalutin",
  "superficial",
  "quince",
  "eight",
  "feeble",
  "admit",
  "drag",
  "loving",
];

// Init word
let randomWord;

// Init score
let score = 0;

// Init time
let time = 10;
```

> jQuery
> 
選擇器
```javascript=
$("#word")
$("#text")
$("#score")
$("#time")
$("#end-game-container")
$("#settings-btn")
$("#settings")
$("#settings-form")
$("#difficulty")
```

### 隨機挑選陣列裡的單字，加到元素的 div 裡

- `getRandomWord()` 隨機產生預設陣列裡的單字
- `addWordToDOM()` 新增文字到選擇器裏

> JS

- `Math.random()`函式：會**隨機產生**出 0~1 之間的小數，出來的值永遠不會大於 1 。
- `Math.floor()`函式：會**無條件捨去**到比自身小的最大整數。 Ex: 4.6213 回傳 4
- `words.length` ：總預設單字量是 20 ，乘上隨機 0-1 之間的數，**再取整數**。

![](https://i.imgur.com/J5YEqBg.png)
```javascript=
// Generate random word from array
function getRandomWord() {
  //回傳隨機的字
  return words[Math.floor(Math.random() * words.length)];
}

//Add word to DOM 將取得的字，放到#word裡。
function addWordToDOM() {
  randomWord = getRandomWord();
  word.innerHTML = randomWord;
}

addWordToDOM();
```

>jQuery

 JS 是用打好的陣列，再去取得測驗字。

1. 這裡使用實作無限滾動頁面取的 API 的方法(搜尋[ random word api ](https://random-word-api.herokuapp.com/home))，得到測驗字串。
2. 再直接將得到的字串放入#word裡。

> 使用`$.ajax`方法。

```javascript=
function getRandomWord() {
  $.ajax({
    url: "https://random-word-api.herokuapp.com/word?number=1",
    method: "get",
    dataType: "json",
    success: function (data) {
      $("#word").text(data);
    },
  });
}
```
### 更新成績，判斷輸入的字是否符合出現的字

- updateScore() 更新成績
- addEventListener的 input 不需要按下 Enter 就會直接輸入。

判斷輸入是正確後，會直接清空輸入框。

```javascript=
// Update score 更新成績
function updateScore() {
  score++;
  scoreEl.innerHTML = score;
}

addWordToDOM();

// Event listeners

// Typing
text.addEventListener("input", (e) => {

  //取得輸入的值
  const insertedText = e.target.value;
  
  //如果輸入的值與隨機單字相同
  if (insertedText === randomWord) {
  
    //更新成績+更換下一個隨機單字，更新成績
    addWordToDOM();
    updateScore();

    // Clear
    //輸入正確，自動清空輸入框，增加體驗
    e.target.value = "";
  }
});
```

> jQuery

- `.innerHTML` = 轉成 `.html`
- `text.addEventListener("input"`轉成 `$("#text").on("input"`
- `e.target.value `轉成 `$(this).val()`
- `e.target.value = ""` 轉成 `$(this).val("")`

```javascript=
function updateScore() {
  score++;
  $("#score").html(score);
}

$("#text").on("input", function () {
  const insertedText = $(this).val();
  const randomWord = $("#word").text();
  if (insertedText === randomWord) {
    updateScore();
    getRandomWord();
    $(this).val("");
  }
});
```
### 此畫面渲染成功時，將提示注意到 input 輸入框
```javascript=
// Focus on text on start
text.focus();
```
### 每秒更新倒數狀態，倒數到0時，出現 gameOver Panel

> JS

- `updateTime()`
- `gameOver()`

1. `setInterval()`固定延遲了某段時間之後，才去執行對應的程式碼，然後「不斷循環」。
2. 使用`setInterval()`才會開始倒數，少了這一行，time 變數就不會更動。
3. 秒數歸 0 時，在 css 預先寫好的 style，讓他出現`(display:flex)`，預設為(display:none)。

```javascript=
// Start counting down
const timeInterval = setInterval(updateTime, 1000);

// Update time
function updateTime() {
  time--;
  timeEl.innerHTML = time + "s";
  // 等於0時，呼叫gameOevr()
  if (time === 0) {
    clearInterval(time);
    //end the game
    gameOver();
  }
}

// Game over,show end screen
// 顯示GameOver的Panel
function gameOver() {
  endgameEl.innerHTML = `
  <h1>Time ran out</h1>
  <p>Your final score is ${score}</p>
  <button onclick="location.reload()">Reload</button>
  `;

  endgameEl.style.display = "flex";
}
```

> jQuery

- `.style.display =`轉成 `.css("display", "flex")`

```javascript=
const timeInterval = setInterval(updateTime, 1000);

function updateTime() {
  var timeEl = $("#time");
  time--;
  timeEl.html(time + "s");
  if (time === 0) {
    clearInterval(time);
    gameOver();
  }
}

function gameOver() {
  const endgameEl = $("#end-game-container");
  endgameEl.html(`
  <h1>Time ran out</h1>
  <p>Your final score is ${score}</p>
  <button onclick="location.reload()">Reload</button>
  `);

  endgameEl.css("display", "flex");
}
```

### 用 Localstorge 去設定與判斷使用者選的難度
> JS

- 宣告 difficulty 變數，並且做判斷。如果困難度為空，就從 localStorage 取得值，如果沒有值，就預設 medium。

```javascript=
// Set difficulty to value in localStorage or medium
let difficulty =
  localStorage.getItem("difficulty") !== null
    ? localStorage.getItem("difficulty")
    : "medium";

// Set difficulty select value
difficultySelect.value =
  localStorage.getItem("difficulty") !== null
    ? localStorage.getItem("difficulty")
    : "medium";
    
// 依照不同的困難度，增加不同的時間。
if (difficulty == "hard") {
  time += 3;
} else if (difficulty == "medium") {
  time += 4;
} else {
  time += 6;
}

updateTime();
```

> jQuery
- .value = 轉成 .val()

```javascript=
let difficulty =
  localStorage.getItem("difficulty") !== null
    ? localStorage.getItem("difficulty")
    : "medium";

$("#difficulty").val(
  localStorage.getItem("difficulty") !== null
    ? localStorage.getItem("difficulty")
    : "medium"
);

    if (difficulty == "hard") {
      time += 3;
    } else if (difficulty == "medium") {
      time += 6;
    } else {
      time += 8;
    }
    updateTime();
```

### 設定與下拉選單的事件監聽

> JS

```javascript=
// Settings btn click
// 按下左下角的齒輪，可以收合settings面板。
settingsBtn.addEventListener("click", () => settings.classList.toggle("hide"));

// Settings select
// 下拉式選單改變時，將值儲存在localStorage
settingsForm.addEventListener("change", (e) => {
  difficulty = e.target.value;
  localStorage.setItem("difficulty", difficulty);
});
```
> jQuery
- `.classList.toggle()` 轉成 `.toggleClass()`
- `.target.value` 轉成 `.val()`

```javascript=
$("#settings-btn").on("click", function () {
  $("#settings").toggleClass("hide");
});

$("#settings-form").on("click", function () {
  difficulty = $("#difficulty").val();
  localStorage.setItem("difficulty", difficulty);
});
```
> 補充：(增加使用者體驗)
最後使用了 settimeout 增加 0.2 秒判斷，輸入單字是否正確時產生的渲染，
讓關卡到達下一關時有一點點的時間差去休息。
## 參考文章

[談談 JavaScript 的 setTimeout 與 setInterval](https://kuro.tw/posts/2019/02/23/%E8%AB%87%E8%AB%87-JavaScript-%E7%9A%84-setTimeout-%E8%88%87-setInterval/)