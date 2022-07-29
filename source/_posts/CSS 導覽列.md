---
title: CSS NavBar 導覽列
description: 紀錄常用導覽列
date: 2020-11-20
categories:
- CSS
tags: 
- CSS
---

# CSS 導覽列

1. 首先先建立 html 架構

```htmlembedded=
<header class="main-header">
      <div class="main-container">
        <a href="#" class="logo">
          <img
            src="https://picsum.photos/100/100?random=1
            "
            alt="假圖產生器"
          />
        </a>
        <nav class="main-nav">
          <a href="#">貓咪國度</a>
          <a href="#">貓咪生活</a>
          <a href="#">貓咪商品</a>
          <a href="#">貓咪電話</a>
        </nav>
      </div>
    </header>
```

2. 使用套件 live-sever 開啟就會看到目前網頁有一張圖片，變且下方有四個 a 標籤了，

![](https://i.imgur.com/oV3tQIt.png)

---
3. 接下來設定css

```css=
/* 基本的css reset */
    * {
    margin: 0;
    padding: 0;
    list-style: none;
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}
/* 背景漸層色（角度,顏色,顏色） */
    .main-header {
    background: linear-gradient(0deg, green, yellow)
}
    .main-header .main-container {
    display: flex;
    flex-direction: column;
    /* x軸排成直向 */
    align-items: center;
    /* y軸置中 */
    padding: 20px;
    max-width: 1200px;
    /* 避免爆版，先設定最大框度 */
    margin: auto;
}
    .main-header .logo {
    width: 100px;
    /* 圖片完整寬度 */
}

    .main-header .logo img {
    width: 100%;
    /* 圖片完整呈現 */
    vertical-align: middle;
    /*  inline 元素置中    */
}

```