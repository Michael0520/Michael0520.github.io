---
title: (Project) Music Player
description: 一個有唱盤會旋轉的音樂播放器。
date: 2021-03-02
categories:
- JavaScript
- 作品集
tags: 
- JavaScript
- 作品集
---


## 學習到的知識點

Music Player 比較著多在 CSS 的教學，因此 CSS 部分會比較多紀錄。

### HTML

- 從 fontAwesome 引入圖片

### CSS

- linear-gradient
- animation
- animation-play-state
- ::after偽元素
- z-index

### JS

- jQuery
- clientX，screenX，pageX
- favicon

## 簡介

一個有唱盤會旋轉的音樂播放器。

## [Demo](https://)

## HTML 架構

### 音樂名字與 Progress info 進度條

包住整個結構的`.container`，與存放 progress bar。

```html=
<h1>Music Player</h1>
    <div class="music-container" id="music-container">
      <div class="music-info">
        <h4 id="title"></h4>
        <div class="progress-container" id="progress-container">
          <div class="progress" id="progress"></div>
        </div>
      </div>

      <audio src="./music/ukulele.mp3"></audio>
      
      </div>
```

### 音樂封面照與播放 Button

圖片容器`.img-container`，還有三個從 FontAwesome 網站引入的撥放、倒退、快轉鍵。

```html=
  <div class="img-container">
        <img src="./images/ukulele.jpg" alt="music-cover" id="cover" />
      </div>
      <div class="navigation">
        <button id="prev" class="action-btn">
          <i class="fas fa-backwar"></i>
        </button>
        <button id="prev" class="action-btn action-btn-big">
          <i class="fas fa-play"></i>
        </button>
        <button id="prev" class="action-btn">
          <i class="fas fa-foward"></i>
        </button>
      </div>
```

### CSS 樣式

#### 起手式

```css=
@import url("https://fonts.googleapis.com/css?family=Lato&display=swap");

* {
  box-sizing: border-box;
}
```

#### 背景漸層

```css=
body {
  background-image: linear-gradient(
    0deg,
    rgba(247, 247, 247, 1) 23.8%,
    rgba(252, 221, 221, 1) 92%
  );
```

### 置中

```css=
@import url("https://fonts.googleapis.com/css?family=Lato&display=swap");

* {
  box-sizing: border-box;
}

body {
  background-image: linear-gradient(
    0deg,
    rgba(247, 247, 247, 1) 23.8%,
    rgba(252, 221, 221, 1) 92%
  );
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-family: "Lato", sans-serif;
  margin: 0;
}
```

### 外層容器

#### `.music-container`

- `relative` 可以定位到上層元素`.music-container`，而不會定位到最外層導致跑版。

- `z-index` 層疊樣式表

[z-index 詳細說明](https://developer.mozilla.org/zh-CN/docs/Web/CSS/z-index)

```css=
.music-container {
  background-color: #fff;
  border-radius: 15px;
  box-shadow: 0 20px 20px 0 rgba(252, 169, 169, 0.6);
  display: flex;
  padding: 20px 30px;
  position: relative;
  margin: 100px 0;
  z-index: 10;
}
```

### 音樂圖片上樣式

- 圖片設置跟外容器一樣寬

使用`width: inherit`，瀏覽器會將上層元素`img-container`的寬度賦值給他，
就不需要再`img-container`上設定`position:relative`。

- 定位照片

> 使用絕對定位

```css=
position: absolute;
bottom: 0;
left: 0;
```

- 加上動畫

> 使用 animation
>
>>- 動畫名稱 `animation-name`
>>- 動畫持續時間 `name-duration`
>>- 動畫加速度函式 `animation-timing-function`
>>- 動畫播放次數  `animation-iteration-count`
>>- `animation-play-state` 為動畫播放或暫停狀態。
>>- `running`：預設值，表示動畫運行。
>>- `paused`：表示動畫暫停

```css=
/* Example */
animation: rotate 3s linear infinite;
animation-play-state: paused;
```

- 音樂播放時開始旋轉

透過 JS 來控制，
按下播放音樂的 Button 觸發監聽，動態將`.play`的 class 新增上去。

```css=
/* 旋轉動畫 */
.music-container.play .img-container img {
  animation-play-state: running;
}
```

完整 code :

```css=
.img-container {
  position: relative;
  width: 110px;
}

.img-container img {
  border-radius: 50%;
  object-fit: cover;
  height: 110px;
  width: inherit;
  position: absolute;
  bottom: 0;
  left: 0;
  animation: rotate 3s linear infinite;
  animation-play-state: paused;
}

.music-container.play .img-container img {
  animation-play-state: running;
}
```

### 設置 CD 圖片正中心的白點

將圖片上的白點移到中間，使用到偽元素`::after`來新增。

```css=
.img-container::after {
  content: "";
  background-color: #fff;
  border-radius: 50%;
  position: absolute;
  bottom: 100%;
  left: 50%;
  width: 20px;
  height: 20px;
  transform: translate(-50%, 50%);
}
```

### 設定 CD 旋轉動畫

```css=
@keyframes rotate {
  from {
    transform: rotate(0deg);
  }

  to {
    transform: rotate(360deg);
  }
}
```

### 播放按鈕欄

- 消除點擊後預設出現的藍色邊框

```css=
.action-btn:focus {
  outline: 0;
}
```

完整 code :

```css=
.navigation {
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1;
}

.action-btn {
  background-color: #fff;
  border: 0;
  color: #dfdbdf;
  font-size: 20px;
  cursor: pointer;
  padding: 10px;
  margin: 0 20px;
}

/* 放大播放按鈕 & 更改為深色*/
.action-btn.action-btn-big {
  color: #cdc2d0;
  font-size: 30px;
}

.action-btn:focus {
  outline: 0;
}
```

### Music Info

- 跳出式視窗
要做出跳出式視窗的效果(按下播放時，才出現)，
一開始要設定`transform: translateY(0%)，opacity: 0`，不讓 Info 面板出現。

`transform`的座標別於我們一般認知的座標，
以下面這張圖為例，右下在一般認知裡為(`100,-100)`，
但`transform`原點在左上，所以往他的右下為`(100,100)`，相反的往他的左上為`(-100,-100)`。

![image](https://i.imgur.com/VU5Tlnu.png)

> `transition:ease-in`效果，意思為緩慢的開始。
> `calc()`為動態計算，不用在一個一個計算現在的寬度為多少

`width: calc(100% - 40px)`，100% 為上層元素的最大寬度，
可以和`max()`、`min()`、`clamp`或是 CSS 的變數互相搭配，中間是減號，前後要留兩個空格。

[`calc()` 詳細解說](https://developer.mozilla.org/zh-CN/docs/Web/CSS/calc())

完整 Code :

```css=
/* 未播放時不出現 */
.music-info {
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 15px 15px 0 0;
  position: absolute;
  top: 0;
  left: 20px;
  width: calc(100% - 40px);
  padding: 10px 10px 10px 150px;
  opacity: 0;
  transform: translateY(0%);
  transition: transform 0.3s ease-in, opacity 0.3s ease-in;
  z-index: 0;
}

/* 播放時出現*/
.music-container.play .music-info {
  opacity: 1;
  transform: translateY(-100%);
}

/* 去除h4的預設margin */
.music-info h4 {
  margin: 0;
}
```

### Progress 播放進度條

`.progress`裡面的`width`改變他的長度，會使用Js動態改變。

`transition`: 新增效果的 CSS 屬性 | 效果的持續時間 | 動畫執行的計算方式

```css=
/* 外面的白色框框 */
.progress-container {
  background: #fff;
  border-radius: 5px;
  cursor: pointer;
  margin: 10px 0;
  height: 4px;
  width: 100%;
}

/* 裡面的進度條 */
.progress {
  background-color: #fe8daa;
  border-radius: 5px;
  height: 100%;
  width: 0%;
  transition: width 0.1s linear;
}
```

### JS 功能

> 盡可能都採用 jQuery 撰寫

#### 設定變數

- 選取元素

> JS

```javascript=
const musicContainer = document.getElementById("music-container");
const playBtn = document.getElementById("play");
const prevBtn = document.getElementById("prev");
const nextBtn = document.getElementById("next");

const audio = document.getElementById("audio");
const progress = document.getElementById("progress");
const progressContainer = document.getElementById("progress-container");
const title = document.getElementById("title");
const cover = document.getElementById("cover");
```

> jQuery

```javascript=
$("#musicContainer")
$("#playBtn")
$("#prevBtn")
$("#nextBtn")
$("#audio")
$("#progress")
$("#progressContainer")
$("#title")
$("#cover")
```

### 創建歌曲陣列，設立編號，呼叫 loadSong()

```javascript=
// Song titles
const songs = ["hey", "summer", "ukulele"];

// Keep track of song
let songIndex = 0;

// Initially load song details into DOM
// 呼叫loadSong函數，依照編號數字來呼叫歌曲
loadSong(songs[songIndex]);

// 此時因為 songIndex = 0 ，所以會顯示 'hey'
```

![image](https://i.imgur.com/5yniELP.png)

### 載入歌曲 loadSong()

- 將歌曲的名字，音檔，照片讀入。

> JS

```javascript=
// Update song details
function loadSong(song) {
  // Can change the song
  title.innerText = song;
  audio.src = `music/${song}.mp3`;
  cover.src = `images/${song}.jpg`;
}
```

> jQuery

- `audio.src` =轉成`$("#audio").attr()`

> :bug:這裡有遇到錯誤，不曉得為何更改為 `.attr()`
> 無法成功取得音樂以及圖片，但原生 JS 就沒有問題

```javascript=
function loadSong(song) {
  $('#title').text(song)
  $('#audio').attr(`music/${song}.mp3`)
  $('#cover').attr(`images/${song}.jpg`)
}
```

### 設定事件監聽

> JS

```javascript=
// Event Listeners
playBtn.addEventListener("click", (e) => {
  e.preventDefault();
  
  const isPlaying = musicContainer.classList.contains("play");

  if (isPlaying) {
    pauseSong();
  } else {
    playSong();
  }
});
```

> jQuery

- `playBtn.addEventListener("click"` 轉成`$("#playBtn").click(function(){`
- `.classList.contains`轉成`.hasClass`

```javascript=

$("#playBtn").click(function (e) {
  e.preventDefault();
  const isPlaying = $("musicContainer").hasClass("play");
  if (isPlaying == true) {
    pauseSong();
  } else {
    playSong();
  }
});
```

### 播放歌曲 playSong()，暫停歌曲 pauseSong()

- 播放和暫停功能一樣，只有 icon 交換和`audio.play()`，`audio.pause()`不同。

> JS

```javascript=
// Play song
function playSong() {
  musicContainer.classList.add("play");
  playBtn.querySelector("i.fas").classList.remove("fa-play");
  playBtn.querySelector("i.fas").classList.add("fa-pause");

  audio.play();

// Pause song
function pauseSong() {
  musicContainer.classList.remove("play");
  playBtn.querySelector("i.fas").classList.add("fa-play");
  playBtn.querySelector("i.fas").classList.remove("fa-pause");

  audio.pause();
}
```

> jQuery

id 去找到 i ， 再將圖檔替換掉。

- `playBtn.querySelector("i.fas")` 轉成 `$("#play").find("i").attr("class", "fas fa-pause")`
- `audio.play()`轉成`$("#audio")[0].play();`
`.play` 跟 `.pause` 都是 DOM 的操作方法。
- `$queryselector` 為 jQuery 物件而不是原始的DOM元素，所以我們需要成 `$("#audio")[0].play()`。

意思為: 利用 jQuery 選擇器，得到 id 為 audio 的第一個DOM對象。

> BUG : :bug: 此段 jQuery 寫錯誤，先跳過

```javascript=
// example 原生JS DOM 轉換為 jQuery DOM
// 
// 1. 假設，我的頁面中a標籤包含img，並含有src屬性
// 2. $(this)為 jQuery 選定此物件 $('#desktop a') 的方法
// 3. find(element) 是返回一個用於匹配元素的 DOM 元素
//    這樣就可以取到想要的src地址了。
  $("#desktop a ").each(function(index){
    var imgurl=$(this).find('img').attr('src');
      alert(imgurl);
  }
```

[JS DOM 轉換為 jQuery](https://codertw.com/%E5%89%8D%E7%AB%AF%E9%96%8B%E7%99%BC/252289/)

```javascript=
function playSong() {
  $("#music-container").addClass("play");
  $("#play").find("i").attr("class", "fas fa-pause");
  $("#audio")[0].play();
}

function pauseSong() {
  $("#music-container").removeClass("play");
  $("#play").find("i").attr("class", "fas fa-play");
  $("#audio")[0].pause();
}
```

### 前一首prevSong()、下一首歌nextSong()

> JS

利用 songIndex，控制歌曲的撥放。

```javascript=
// Next song
function nextSong() {
  songIndex++;
  // 如果songIndex大於總數2時
  if (songIndex > songs.length - 1) {
  // 就歸0
    songIndex = 0;
  }
  // 重新更換歌曲名字，音檔，圖片
  loadSong(songs[songIndex]);
  playSong();
}

// Previous song
function prevSong() {
  songIndex--;
  // 如果songIndex小於0時
  if (songIndex < 0) {
  // 總數3-1=2，會撥放第3首音樂，形成一個循環
    songIndex = songs.length - 1;
  }
  loadSong(songs[songIndex]);
  playSong();
}

// Change song
prevBtn.addEventListener("click", prevSong);
nextBtn.addEventListener("click", nextSong);
```

> jQuery

- 事件監聽`prevBtn.addEventListener("click", prevSong)轉成$("#next").click(function(){nextSong();})`

```javascript=
// Next song
function nextSong() {
  songIndex++;
  if (songIndex > songs.length - 1) {
    songIndex = 0;
  }
  loadSong(songs[songIndex]);
  playSong();
}

// Previous song
function prevSong() {
  songIndex--;
  if (songIndex < 0) {
    songIndex = songs.length - 1;
  }
  loadSong(songs[songIndex]);
  playSong();
}

// Change song
$("#pre").click(function(){
    prevSong();
});
$("#next").click(function(){
    nextSong();
});
```

### 進度條

> JS

- duration 是整首歌的時間
- currentTime 指的是過了多久的時間

滑鼠相對於事件源元素（srcElement）的 x , y 坐標

- `event.offsetX`
- `event.offsetY`

[JS 一秒區分 `clientX,offsetX,screenX,pageX`之間關係](https://kknews.cc/zh-tw/news/r3pzzr.html)

[Audio duration Property](https://www.w3schools.com/Jsref/prop_audio_duration.asp)

```javascript=
// Update progress bar
// e.srcElement 代表當前的事件來源
function updateProgress(e) {
  const { duration, currentTime } = e.srcElement;
  
// (當下的音樂時間/總時長)*100就會得到百分比
  const progressPercent = (currentTime / duration) * 100;
  
// 百分比變數放到progress上
  progress.style.width = `${progressPercent}%`;
}

// Time/song update
audio.addEventListener("timeupdate", updateProgress);
```

> jQuery
.on 就是 addEventListener

- `audio.addEventListener()`轉成`$("#audio").on()`
- `const { duration, currentTime } = e.srcElement`轉成
`const duration = $("#audio")[0].duration;`
`const progressPercent = $("#audio")[0].currentTime;`
- `progress.style.width = ()`轉成`$("#progress").css`

```javascript=
  $("#audio").on("timeupdate", function () {

  const duration = $("#audio")[0].duration;
  const progressPercent = $("#audio")[0].currentTime;

  const progressPercent = (currentTime / duration) * 100;

  $("#progress").css(width, `${progressPercent}%`);
});
```

### 操作進度條

> JS

```javascript=
// 滑鼠點擊進度條移動 Set progress bar
function setProgress(e) {

  // this 指向 progress-container 它的 width 就是 216
  const width = this.clientWidth;
  
  // clickX 為滑鼠點擊 progress-container 的位置
  const clickX = e.offsetX;
  
  // duration will get from audio api
  // 音檔總時長
  const duration = audio.duration;
  
  // 算出百分比
  audio.currentTime = (clickX / width) * duration;
}

// Click on progress bar
progressContainer.addEventListener("click", setProgress);
```

> jQuery

- 使用到.offset().left

`this.clientWidth 轉成 $('#progress-container').width()`

```javascript=
// 取得progress-container的長度
    const width = $('#progress-container').width() 
// offsetX. 為點擊物件最左側的距離
    const offsetX = $(e.target).offset().left;
// clickX 為點擊的位置，與畫面最左側的距離
    const clickX = e.pageX 
// 取得歌曲的總長度
    const duration = $('#audio')[0].duration;
// 利用距離算出百分比
    const percent = ((clickX - offsetX) / width)
    $('#audio')[0].currentTime = percent * duration 
});
```

### 播放完畢後，自動跳下一首

> JS

```javascript=
audio.addEventListener("ended", nextSong);
```

> Jquery

- `audio.addEventListener() 轉成 $("audio").on`

```javascript=
$("audio").on("ended",function(){
    nextSong();
})
```

## 參考文章

### CSS 文章

- z-index 詳細說明:
  - [z-index 詳細說明](https://developer.mozilla.org/zh-CN/docs/Web/CSS/z-index)

- calc()詳細解說
  - [`calc()` 詳細解說](https://developer.mozilla.org/zh-CN/docs/Web/CSS/calc())

### JS 文章

- JS DOM 轉換為 jQuery
  - [JS DOM 轉換為 jQuery](https://codertw.com/%E5%89%8D%E7%AB%AF%E9%96%8B%E7%99%BC/252289/)

- JS 一秒區分 `clientX,offsetX,screenX,pageX`之間關係
  - [JS 一秒區分 `clientX,offsetX,screenX,pageX`之間關係](https://kknews.cc/zh-tw/news/r3pzzr.html)

- Audio duration Property
  - [Audio duration Property](https://www.w3schools.com/Jsref/prop_audio_duration.asp)
