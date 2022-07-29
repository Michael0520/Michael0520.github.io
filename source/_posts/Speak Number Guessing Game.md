---
title: (Project) Speak Number Guessing Game
description: 猜數字遊戲，實作使用麥克風音訊來猜數字
date: 2021-03-17
categories:
- JavaScript
- 作品集
tags: 
- JavaScript
- 作品集
---

## 學習到的知識點

### CSS

- display:inline-block

### JS

- `html()` 完全替代 & `append()` 新增追加
- Web Speech API

## 簡介

**猜數字遊戲**
[Demo](https://michael0520.github.io/Speak-Number-Guessing-Game/index.html)

## HTML

### 結構

![基礎HTML 結構圖](https://i.imgur.com/df0xzPk.png)

```html=
    <img src="./img/mic.png" alt="Speak" />

    <h1>Guess a Number Between 1 - 100</h1>

    <h3>Speak the number into you microphone</h3>

    <div id="msg" class="msg">
      <div>You said:</div>
      <span class="box">20</span>
      <div>GO HIGHER</div>
    </div>
```

## CSS

### 起手式

```css=
* {
    box-sizing: border-box;
}

body {
    color: #fff;
    min-height: 100vh;
    align-items: center;
    justify-content: center;
    text-align: center;
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
}
```

### 新增上客製化樣式

完整 css code:

```css=
* {
    box-sizing: border-box;
}

body {
    background: #2f3542 url('./img/bg.jpg') no-repeat left center/cover;
    color: #fff;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
}

h1, h3 {
    margin-bottom: 0;
}

p {
    line-height: 1.5;
    margin: 0;
}

.play-again {
    padding: 8px 15px;
    border: 0;
    background: #f4f4f4;
    border-radius: 5px;
    margin-top: 10px;
}

.msg {
    font-size: 1.5em;
    margin-top: 40px;
}

.box {
    border: 1px solid #dedede;
    display: inline-block;
    font-size: 30px;
    margin: 20px;
    padding: 10px;
}

```

[關於display:inline、block、inline-block的差別](https://ytclion.medium.com/css%E6%95%99%E5%AD%B8-%E9%97%9C%E6%96%BCdisplay-inline-inline-block-block%E7%9A%84%E5%B7%AE%E5%88%A5-1034f38eda82)

## JS

### 產生隨機數 getRandomNumber()

> JS

- `Math.floor()`函式: 回傳小於等於所給數字的最大整數。 ex 9.6213 回傳 9
- `Math.random()`函式: 會隨機產生出 0~1 之間的小數，出來的值永遠不會大於 1 。

```javascript=
const msgEl = document.getElementById("msg");
const randomNum = getRandomNumber();
console.log("Number:", randomNum);

// Generate random number
function getRandomNumber() {

  // 產生的數會是9-99，所以+1，變成隨機產生 1~100 的數字。
  return Math.floor(Math.random() * 100) + 1;
}
```

> jQuery

無轉換的程式碼

```javascript=
const randomNum = getRandomNumber();
console.log("Number:", randomNum);

function getRandomNumber() {
  return Math.floor(Math.random() * 100) + 1;
}
```

### Web Speech API onSpeak()

[Speed API](https://developer.mozilla.org/en-US/docs/Web/API/SpeechRecognition)

![image](https://i.imgur.com/Yt2BOcR.png)

取得 API，然後印出 e，可以觀察到許多資訊，裡面的 result 裡的 transcript 會有我們說的內容，再對 transcript 進行轉換，就可以得到說的內容。

---
Web Speech API有兩個部分

- speechSynthesis 語音合成(文字轉語音)
- speechRecognition 語音識別(非同步語音識別)

1. 先查看瀏覽器是否有支援不需要 prefix (前綴)的  speechRecognition 介面，若沒有則將  webkit 標頭的  webkit.SpeechRecognition 指定給該全域變數。

    > 可以前往 [Can I use](https://caniuse.com/?search=SpeechRecognition) 查看

    ```javascript=
    window.SpeechRecognition =
      window.SpeechRecognition || window.webkitSpeechRecognition;
    ```

2. 使用前要先建構一個物件實體放到 recognition 變數，使用`SpeechRecognition()`建構式建立

    ```javascript=
    let recognition = new window.SpeechRecognition();
    ```

3. 並監聽`result`事件。

    ```javascript=
    recognition.addEventListener("result", onSpeak);
    ```

4. 設定完後要使用 `start()` 才會開始辨識

    ```javascript=
    recognition.start();
    ```

> JS

    ```javascript=
    window.SpeechRecognition =
      window.SpeechRecognition || window.webkitSpeechRecognition;

    let recognition = new window.SpeechRecognition();

    // Start recognition and game
    recognition.start();

    // Capture user speak
    function onSpeak(e) {
      console.log(e);
      const msg = e.results[0][0].transcript;
      console.log(msg);
    }

    // Speak result
    // 藉由 onSpeak 函式取得 speak result
    recognition.addEventListener("result", onSpeak);
    ```

> jQuery

無轉換的程式碼

    ```javascript=
    window.SpeechRecognition =
      window.SpeechRecognition || window.webkitSpeechRecognition;

    let recognition = new window.SpeechRecognition();

    recognition.start();

    function onSpeak(e) {
      console.log(e);
      const msg = e.results[0][0].transcript;
      console.log(msg);
    }

    recognition.addEventListener("result", onSpeak);
    ```

### 將得到的數字，印在印在頁面上 writeMessage()

> JS

```javascript=
// Write what user speaks
function writeMessage(msg) {
  msgEl.innerHTML = `
    <div>You said: </div>
    <span class="box">${msg}</span>
  `;
}
```

> jQuery

- `.innerHTML =`轉成`.html()`

```javascript=
// Write what user speaks
function writeMessage(msg) {
  $("#msg").html(`
    <div>You said: </div>
    <span class="box">${msg}</span>
  `);
}
```

## 判斷說出的值 checkNumber()

> JS

- `.start()`只會開啟一次辨識，設定 functoin，結束時就啟動 `start()`。
- +是將 string 轉成數字，等同於 parseInt
- isNaN 函式會判斷某個數值是不是 NaN

```javascript=
function onSpeak(e) {
  const msg = e.results[0][0].transcript;
  writeMessage(msg);
  // 加上這行
  checkNumber(msg);
}

// Check msg against number
// 判斷輸入的內容
function checkNumber(msg) {
  const num = +msg;

  // Check if valid number
  // 判斷是否為數字
  if (Number.isNaN(num)) {
    msgEl.innerHTML += "<div>That is not a valid number</div>";
    return;
  }

  // Check in range
  // 判斷數字有無超過範圍
  if (num > 100 || num < 1) {
    msgEl.innerHTML += "<div>Number must be between 1 and 100</div>";
    return;
  }

  // Check number
  // 如果是數字，就判斷是否與隨機數相等，不等於就判斷大於還是小於。
  if (num === randomNum) {
    document.body.innerHTML = `
      <h2>Congrats! You have guessed the number! <br><br>
      It was ${num}</h2>
      <button class="play-again" id="play-again">Play Again</button>
    `;
  } else if (num > randomNum) {
    msgEl.innerHTML += "<div>GO LOWER</div>";
  } else {
    msgEl.innerHTML += "<div>GO HIGHER</div>";
  }
}

// End SR service
// 每判斷一次又會再重新執行 start()
// 所以可以持續判斷聲音
// 不加這行就只能判斷一次就需要 reload
recognition.addEventListener("end", () => recognition.start());
```

> jQuery

- `.innerHTML +=`轉成`.append()`
- `.innerHTML +=` 轉成 `.html()`

`append()`跟`html()`乍看之下有點像，但他們其實不一樣。
`append()`是追加 (+=) 的概念，而`html()`是完全替換 (=)。

[jQuery `append()` 用法及代碼示例](https://vimsky.com/zh-tw/examples/usage/jquery-append-method.html)
[`.html()`](https://api.jquery.com/html/)

Example:

```javascript=
<!-- html() 完全替代-->

// Q:
<p id=”1″>
  <p>123</p>
</p>

$("#1").html("<span>456</span>");

// A:
<p id=”1″>
  <span>456</span>
</p>

// // // // //

<!-- append() 追加新增-->
// Q:
<p id="1">
  <span>456</span>
</p>

$("#1").append("<span></span>");

// A:
<p id="1">
  <p>123</p>
  <span>456</span>
</p>
```

此部分的 Code

```javascript=
function checkNumber(msg) {
  const num = +msg;

  // Check if valid number
  if (Number.isNaN(num)) {
    $("#msg").append("<div>That is not a valid number</div>");
    return;
  }

  // Check in range
  if (num > 100 || num < 1) {
    $("#msg").append("<div>Number must be between 1 and 100</div>");
    return;
  }

  // Check number
  if (num === randomNum) {
    $("body").html(`
      <h2>Congrats! You have guessed the number! <br><br>
      It was ${num}</h2>
      <button class="play-again" id="play-again">Play Again</button>
    `);
  } else if (num > randomNum) {
    $("#msg").append("<div>GO LOWER</div>");
  } else {
    $("#msg").append("<div>GO HIGHER</div>");
  }
}
recognition.addEventListener("end", () => recognition.start());
```

### 設定重新開始 Button

當數字相等時，會出現 reload 按鈕。
當按鈕`(.play-again)`被觸發時，整個 window 就 reload。

> JS

```javascript=
document.body.addEventListener("click", (e) => {
  if (e.target.id == "play-again") {
    window.location.reload();
  }
});
```

> jQuery

- `.addEventListener("click")`轉成`.click()`

```javascript=
$("body").click(function (e) {
  if (e.target.id == "play-again") {
    window.location.reload();
  }
});
```

## 參考文章

[jQuery `append()` 用法及代碼示例](https://vimsky.com/zh-tw/examples/usage/jquery-append-method.html)

[`.html()`](https://api.jquery.com/html/)

[`window.location.Reload()` 和 `window.location.href` 區別](https://www.itread01.com/p/1330644.html)

[Can I use](https://caniuse.com/?search=SpeechRecognition)

[關於 display:inline、block、inline-block的差別](https://ytclion.medium.com/css%E6%95%99%E5%AD%B8-%E9%97%9C%E6%96%BCdisplay-inline-inline-block-block%E7%9A%84%E5%B7%AE%E5%88%A5-1034f38eda82)