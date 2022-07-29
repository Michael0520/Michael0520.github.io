---
title: (Project) YouTube API
description: 利用 Youtube API，可以搜尋 Youtube 影片。
date: 2021-04-04
categories:
- JavaScript
- 作品集
tags: 
- 作品集
---

## 學習到的知識點
### HTML
### CSS 
- .clearfix
### JS
- $.get
- $.each
- fancy box 套件

## 簡介

利用 Youtube API，可以搜尋 Youtube 影片。

有查看上一頁和下一頁的功能，點擊標題連結可以在該頁撥放影片。

![](https://i.imgur.com/3JMDKbB.png)

[Demp](https://)

## HTML
### 結構

![](https://i.imgur.com/lYjXPdo.png)



```htmlembedded=
  <body>
    <div class="container">
      <header>
        <h1>Search<span> Videos</span></h1>
        <p>Search all Youtube videos</p>
      </header>
      <!--  TODO: 1. Submit 送出後 callbackFunction -->
      <section>
        <form
          id="search-form"
          class="search-form"
          name="search-form"
          onsubmit="return search()"
        >
          <div class="fieldcontainer">
            <input
              type="search"
              id="query"
              class="search-field"
              placeholder="Search Youtube..."
            />
          <input
            type="submit"
            class="search-btn"
            id="search-btn"
            value=""
          ></input>
        </div>
        </form>

        <ul id="results"></ul>
        <div id="buttons"></div>
      </section>

      <footer>
          <p>Copyright &copy; 2021,All Right Reserved</p>
      </footer>
    </div>

    <script src="./app.js"></script>
    <script src="./js/jquery.fancybox.pack.js"></script>
    <script>
        $(document).ready(function () {
          $(".fancybox").fancybox();
        });
      </script>
```
## CSS
[完整 CSS code](https://)

### clearFix

在使用 float 的時候經常會遇到圖片超出預設的寬度，但只要使用 clearfix ，就可以使圖片和容器寬度一樣。

```css=
.clearfix {
  clear: both;
}
```

### box-shadow 套件

[Beautiful CSS box-shadow examples](https://getcssscan.com/css-box-shadow-examples)
## JS

### 動態變化 Search Bar 
**利用 jQuery 在 focus 與 blur（離開焦點）的時候執行 animate 來達到拉長與縮短的效果。**

search bar 是由一個輸入區塊跟搜尋按鈕兩部分組成，輸入區塊的位置用 `width` 百分比控制、按鈕則是用`position: absolute`加上 `right` 的 `px` 來控制。
原始狀態，也就是 blur 時輸入區塊是用`width:45％`、按鈕是用`position: absolute`、`right:360px`。
點擊後變為 focus 狀態，輸入區塊則用`width:100％`、按鈕是用`right:10px`。

- focus 時範例
![Focus 時範例](https://i.imgur.com/rrf5L56.png)

- blur 時範例
![Blur 時範例](https://i.imgur.com/bvbZruW.png)

需要注意搜尋按鈕是用 submit 事件，要用`e.preventDefault()`來停止預設行為的發生。


:bug: *這邊應該是要讓 icon 跟 輸入 input 綁在一起，讓 icon 也能夠往右移，但這邊不曉得出了什麼錯，一直沒辦法用好，之後再回頭修改來讓動畫效果更精緻*

### 取得 YouTube 資料
利用網址可以取得的json資料。

`
https://www.googleapis.com/youtube/v3/search
`

![](https://i.imgur.com/aviL0mD.png)


![](https://i.imgur.com/hPMR0jD.png)


### `$.get` 取得資料

- part: 這個參數是為了避免大家呼叫 API 時得到太多不相關的資訊，所以用 part 來定義要取得的資料範圍。在 - - Search 的情況下，設定為 part:snippet 。
- type：限制搜尋結果為 video、channel 或 playlist
- q：搜尋關鍵字
- key: 金鑰

```javascript=
function search() {

  // * Clear Result
  $("#result").html("");
  $("#buttons").html("");

  // * Get Form Input value
  q = $("#query").val();

  $.get(
    "https://www.googleapis.com/youtube/v3/search",
    {
      part: "snippet,id",
      q: q,
      type: "video",
      key: "AIzaSyBcMsR-AjSrK-Dxyd2o3F8vcF-JueJma4o",
    },
    
    // 取得 data 裡的 Token 方便之後使用
    function (data) {
      var nextPageToken = data.nextPageToken;
      var prevPageToken = data.prevPageToken;

      // Log Data
      console.log(data);
    }
  );
}
```
### `$.each` 讀取每一筆資料

![](https://i.imgur.com/DnNokDZ.png)

```javascript=
$.each(data.items, function (i, item) {

// * Get Output
var output = getOutput(item);

// * Display Result
$("#results").append(output);
});

var buttons = getButtons(prevPageToken, nextPageToken);

// * Display Buttons
$("#buttons").append(buttons);
```

### getOutput () 列印出搜尋資料

過濾資料，取得需要的部分，建立成 output 字串。

在這邊就可以得到影片與內容的資訊，然後更改 video 的樣式。


### fancy box 套件

到[fancy box](http://fancybox.net/) 官網下載檔案，然後放到Project裡。


![](https://i.imgur.com/8h1W3bC.png)

## 參考文章
