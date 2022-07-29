---
title: CSS 人員介紹卡片
description: 紀錄實作 CSS 過程。
date: 2020-12-08
categories:
- CSS
tags: 
- CSS
---

# Css 人員介紹卡片

[解答程式碼網址](https://codepen.io/bad_printer/pen/xxKyXRB)
![完成後的樣子](https://i.imgur.com/qel43Nl.jpg)
---
首先先建立 html 架構，
![](https://i.imgur.com/S3cK4e6.jpg)

```htmlembedded=
<html>
<body>
<div class=wrap>
    <div class=item>
     <img>圖片</img>
        <div class=text>
        <h1>title</h1>
        <p>文字</p>
        </div>
       
    </div>
<!--      -->
    <div class=item>
     <img>圖片</img>
        <div class=text>
        </div>
        <h1>title</h1>
        <p>文字</p>
    </div>
<!--      -->
    <div class=item>
     <img>圖片</img>
        <div class=text>
        <h1>title</h1>
        <p>文字</p>
    </div>
<!--      -->
</div>

</body>
</html>
```

```css=
* {
    margin: 0;
    padding: 0;
    list-style: none;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif
/*   css reset   */
}

html, body {
    height: 100%;
    
/*  為了讓    */
}