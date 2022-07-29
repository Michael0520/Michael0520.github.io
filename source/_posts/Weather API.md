---
title: (Project) Weather API
description: 可以直接觀看到台部分地區的當天天氣。
date: 2021-03-25
categories:
- JavaScript
- 作品集
tags: 
- JavaScript
- 作品集
---

## 學習到的知識點

- HTML
  - Bootstrap class
- CSS
  - 偽元素 :hover
  - 跳動效果 ：transform
  - 漸層動畫效果：box-shadow
- JS
  - Fetch
  - 觀看 API 資訊

## 簡介

可以直接觀看到台部分地區的當天天氣。

![完成圖](https://i.imgur.com/XMtbNwL.png)

## HTML

### 結構

[完整 HTML Code](https://github.com/Michael0520/Weather_API/blob/main/index.html)

```htmlembedded=
  <div class="container">
      <h1 class="text-center">Show Weather From Taiwan</h1>
      <div class="row"></div>
    </div>
```

## CSS

[完整 CSS Code](https://github.com/Michael0520/Weather_API/blob/main/style.css)

### 置中背景 & 自適應大小縮放

```css=
    background-image: url();
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center center;
```

### 滑鼠移入到天氣卡片上呈現浮出 & 變色的動畫

```css=
.card {
    /* 背景透明化 */
    background-color: rgb(214, 214, 214);
    /* 邊框透明化     */
    border: 2px solid rgb(170, 170, 170);
    /* 邊框圓角     */
    border-radius: 25px;
    width: 20rem;
    /*  卡片陰影  */
    box-shadow: 0px 0px 25px rgba(0, 0, 0, 0.3);
    transition: 0.4s;
    margin-bottom: 1.3rem;
}

.card:hover {
    /* 將顏色改為白色，增加 hover 差異效果 */
    background-color: #fff;
    /*  hover 之後，增加陰影面積和位移幅度，就可以做出漂浮效果  */
    box-shadow: 3px 3px 20px rgba(0, 0, 0, 0.3);
    transform: translate(-5px, -5px);
}
```

## JS

[完整 JS Code](https://github.com/Michael0520/Weather_API/blob/main/app.js)

### 取得 天氣 API

先到[中央氣象局](https://opendata.cwb.gov.tw/userLogin)註冊並且取得授權碼

1. 註冊完成後，點選try it out，然後輸入Authorization。

![image](https://i.imgur.com/JvXv1ir.png)

1. 因為下面還有許多欄位，一開始不知道還要輸入什麼，
   1. 透過網路找資料上看了其他人的文章也沒有人特別提及。所以，我就直接按下最下面的Execute，讓他產生連結，過程大約需要一分鐘。

![image](https://i.imgur.com/AsG42e2.png)

1. 產生 Request URL後就可以直接複製使用

![image](https://i.imgur.com/lzHY6Kz.png)

- console.log 來查看資料陣列

![image](https://i.imgur.com/G9MJxnL.png)

- 官網有對照表，方便查找需要的資料

![image](https://i.imgur.com/H2Ki9kM.png)

- 使用 Fetch 方法來取得資料

```javascript=
fetch(
"https://opendata.cwb.gov.tw/api/v1/rest/datastore/F-C0032-001?Authorization=CWB-B7CE0CAC-3B18-4745-B65B-190B83AD9DCD&format=JSON&locationName=&elementName="
)
  .then(function (res) {
    return res.json();
  })
  .then(function (data) {
    const weatherData = data.records.location;
```

### 從資料篩選出需要的資料 & 建立變數

- name 縣市的部分
- Rain 降雨機率
- WX 天氣狀況描述
- MinT 最低溫
- MaxT 最高溫

> 因為變數會持續被更動所以使用 `let` 而不是使用 `const`

### 展開運算子搭配 forEach 快速處理整批資料

找出需要的資料且列印出

```javascript=
    [...weatherData].forEach((currentValue, index) => {
      let name = weatherData[index].locationName;
      let Rain =
        weatherData[index].weatherElement[1].time[2].parameter.parameterName;
      let Wx =
        weatherData[index].weatherElement[0].time[2].parameter.parameterName;
      let MinT =
        weatherData[index].weatherElement[2].time[2].parameter.parameterName;
      let MaxT =
        weatherData[index].weatherElement[4].time[2].parameter.parameterName;
      console.log(currentValue);
```

![image](https://i.imgur.com/7xQFSJE.png)

### 判斷天氣降雨機率來加入天氣圖片

> 一樣 img 會持續更動，所以使用 `let` 而不是使用 `const`
>
:bug: 選定天氣，應該使用資料裡的天氣資訊，
但天氣資訊過多複雜，會使迴圈寫得過攏長，未來再回頭來更新，更簡單且精準的判斷方式

```javascript=
      let img;
      if (Rain == 0) {
        img = "img/Sun.svg";
      } else if (Rain > 25 || Rain < 40) {
        img = "img/Clouds.svg";
      } else if (Rain > 50) {
        img = "img/Umbrella.svg";
      } else {
        img = "img/Rain.svg";
      }
```

### 對應得資料加入對應的DOM

```javascript=
 let card = document.querySelector(".row");
      card.innerHTML += `
               
        <div class="card mb-2 text-center mx-auto" style="width: 12rem">
            <img src="${img}" class="card-img-top mx-auto"  style="width:50% " alt="weather">
                <div class="card-body">
                    <h5 class="card-title">${name}</h5>
                    <p class="card-text">tmp: ${MinT}&#8451~${MaxT}&#8451</p>
                    <p class="card-text">降雨機率: ${Rain}%</p>
                    <p class="card-text">tmp: ${Wx}</p>
            </div>
                    </div>
        `;
```

## 參考文章

[Bootstrap 卡片 (Cards)](https://bootstrap5.hexschool.com/docs/5.0/components/card/)
[[CSS3]box-shadow 區塊陰影](https://abgne.tw/css/css3-lab/css3-box-shadow.html)
