---
title: 初探 HTML
description: HTML定義了Internet上每個網頁的內容。
date: 2020-11-06
categories:
- HTML
tags: 
- HTML
---


# HTML

**HTML定義了Internet上每個網頁的內容。**
> 通過使用HTML標籤“標記”原始內容，
您可以告訴網頁瀏覽器您希望如何顯示內容的不同部分。
創建帶有適當標記內容的HTML文檔是開發網頁的第一步。
> 1. 建立且撰寫原始文字檔案，
> 2. 加上了 html 標籤，
> 3. 再透過伺服器上傳才變成網頁
![](https://i.imgur.com/dVp1HJE.png)


> 認識 HTML ，先了解他的結構
HTML 跟人一樣分為`<head> <body>`
> * `<html>` 標籤：包住頁面所有內容，有時也被稱作根元素
> * `<head>`標籤：放跟網頁有關的資訊，例如：顯示於搜尋結果的關鍵字、頁面說明、CSS等等
> * `<body>` 標籤：提供給使用者觀看的網頁內容，例如：文字、圖片、遊戲、可以播放的音樂或其他物件。
> * `<!DOCTYPE html>` 標籤：是告訴網頁這是 html5的網頁
一般的配置長這樣：

```html 
<!DOCTYPE html>
<html>
    <head>
    </head>
    <body>
    </body>
</html>
```

### HTML 標籤

構成一個 HTML 的「元素」需要三格部分構成：
起始標籤、內容、結束標籤

```html
<p> content </p>
```
> 一般 HTML 的標籤分為：
> 1. 塊級元素
> 2. 內聯元素
> 3. 空元素
>> 塊級元素：會自成一行或一塊，例如：
```html
<p></p>
<div></div>
<footer></footer>
```
>> 內聯元素：通常內嵌在塊級元素，不會產生新行或區塊在網頁中，
例如：
```html
<p><a herf></p>
<p><strong> </strong></p>
```
>> 空元素：單標籤組成，例如：
```html
<img src=" " alt=" ">
```
>> 屬性：屬性包含元素的額外訊息，這些訊息不會出現在實際的內容中，需有 =和 "”，例如：
```html
<img src=" " alt=" " > <p class=" " >
```
---

### `<body>` 內的標籤

* **`<p>` 段落**

> 塊級元素
![](https://i.imgur.com/8dcgO5P.png)
> 在 HTML 中最基本的標籤就是 `<p>` ，用來標明這些文字是一個句子

```htmlembedded=
<p> 這樣是不會
有換行效果的</p>
<p>這樣才會</p>
<p>有換行效果</p>
```
* **`h1` 標題**
![](https://i.imgur.com/0FJvdcq.png)
> 透過 Heading 可以標注此行為標題，
並調整大小 & 加粗 Heading 標籤不只一個，從最大的 `<h1>` 一直到字體最小的 `<h6>`
>> **但要注意一點！**
使用 Heading 標籤的重點並非透過標籤調整大小
字體調整，套用 CSS 的樣式就做得到了，還能更客製化
Heading 標籤主要是來標注大標小標的層級關係，協助你分類內容層級關係，在規劃 SEO (搜尋引擎優化)上會運用得到。

* **`ul`列表**
> 屬於原點符號，適合用來表示產品功能或比較等
![](https://i.imgur.com/yVqIMzW.png)
```htmlembedded=
<html>
  <head>
  </head>
  <body>
    <h2>Lists</h2>

    <p>This is how you make an unordered list:</p>

    <ul>
      <li>Add a "ul" element (it stands for unordered list)</li>
      <li>Add each item in its own "li" element</li>
      <li>They don't need to be in any particular order</li>
    </ul>
  </body>
</html>
```

* **`ol` 列表**
> 屬於數字符號，
適合表示步驟、說明，可透過 CSS 常用來製做成表格
![](https://i.imgur.com/GiBeAff.png)
```htmlembedded=
<html>
  <head>
</head>
  <body>
    <h2>Lists</h2>

    <p>This is how you make an unordered list:</p>

    <ul>
      <li>Add a "ul" element (it stands for unordered list)</li>
      <li>Add each item in its own "li" element</li>
      <li>They don't need to be in any particular order</li>
    </ul>
    <p>This is what an ordered list looks like:</p>

    <ol>
      <li>Notice the new "ol" element wrapping everything</li>
      <li>But, the list item elements are the same</li>
      <li>Also note how the numbers increment on their own</li>
      <li>You should be noticing things is this precise order, because this is an ordered list</li>
    </ol>
  </body>
</html>
```
---
### div 

#### div 是塊級元素的大宗，用於規劃區塊
> ![](https://i.imgur.com/IDDtukD.png)
```htmlembedded=
<html>
  <head>
</head>
  <body>
<div>
  <h1>Interneting Is Easy!</h1>
  <h2>Lists</h2>
</div>
<div>
    <p>This is how you make an unordered list:</p>

    <ul>
      <li>Add a "ul" element (it stands for unordered list)</li>
      <li>Add each item in its own "li" element</li>
      <li>They don't need to be in any particular order</li>
    </ul>

    <p>This is what an ordered list looks like:</p>

    <ol>
      <li>Notice the new "ol" element wrapping everything</li>
      <li>But, the list item elements are the same</li>
      <li>Also note how the numbers increment on their own</li>
      <li>You should be noticing things is this precise order, because this is an ordered list</li>
    </ol>
</div>
<div>
    <h2>Inline Elements</h2>

      <p><em>Sometimes</em>, you need to draw attention to a particular word or phrase.</p>
      <p>Regards,<br/>
         The Authors</p>
  <div>
     <hr/>

     <p>P.S. This page might look like crap, but we'll fix that with some CSS soon.</p>
  </div>
  </body>
</html>
```
> id、class 是一種屬性，用來標註塊級元素套用特定的 CSS 樣式
透過 id、class 屬性標注區塊，可讓 CSS 選擇到該區塊進行排版，例如：並排、橫排、固定….等，或是一些樣式變化。
> 例如：
```htmlembedded=
<div class=" group ">
<p id = "123">
```
> 在 CSS 上就可以透過語法標註塊級元素
```css=
.group { ....}
#123 {...}
```
---
### em 斜體

![](https://i.imgur.com/T9mMxVK.png)
```htmlembedded=
<h2>Inline Elements</h2>

<p><em>Sometimes</em>, you need to draw attention to a particular word or
phrase.</p>
```
### strong 強調

![](https://i.imgur.com/nLEsgSu.png)
```htmlembedded=
<p>Other times you need to <strong>strong</strong>ly emphasize the importance of a word or phrase.</p>
```
### 內聯元素也可以包住行內元素，但不能包塊級元素
![](https://i.imgur.com/yBr6lr2.png)

```htmlembedded=
<p><em><strong>And sometimes you need to shout!</strong></em></p>
```
> ### 非常重要＃！
> 使用 '強調' 和 '斜體' 的重點，並非透過標籤調整樣式
使用強調和斜體時，千萬要記得 HTML 的本質！
改變樣式不是 HTML 的工作，HTML 是標示語言，
是用來標示文字賦予它意義讓瀏覽器看懂的！
>
> html 標示的好，
可以去加速網站辨識您的網頁主要在訴說什麼內容，
進而快速去推算並且分類，提升 SEO
>
>>  CSS 才是改變樣式的主要手段，千萬不要搞錯了！
---
### a 連結

> a 為 anchor 是錨的意思，通常會跟的一個屬性叫：herf，表示 a 指向的地方（網址、頁面或段落）
![](https://i.imgur.com/ZzemPYX.png)
```htmlembedded=
<p>This example is about links and <a href='images.html'>images</a>.</p>
```

* `<a herf='images.html（檔名路徑）'>` ：連結到網站的其他頁面
* `<a herf='https://www.medium.com（網址）'>` ：連結到另一個網站
* `<a herf='#123（要連結段落的 id ）'>` ：連結到另一個段落
---
### image 圖片

> `<img>` 標籤通常用於放置圖片，可支援 JPG 、PNG 、 GIF 、 SVG

![](https://i.imgur.com/SQELGLr.png)

```htmlembedded=
<!-- In JPGs section -->
<img src='images/mochi.jpg' width='75' alt='A mochi ball in a bubble'/>

<!-- In GIFs section -->
<img src='images/mochi.gif' width='75' alt='A dancing mochi ball'/>

<!-- In PNGs section -->
<img src='images/mochi.png' width='75' alt='A mochi ball'/>

<!-- In SVGs section -->
<img src='images/mochi.svg' alt='A mochi ball with Bézier handles'/>
```

> src 、width 和 alt 是 `<img>` 的屬性
src 是放檔案路徑，width 是調整檔案寬度，alt 是圖片的說明
>> alt 可以友善視障人士了解圖片內容，且當出現死圖也可以說明圖片內容
可以提升網站 SEO
---
### `<head>` 內的標籤

> 簡單介紹完 body 後，要來介紹一下 `<head>` 內有什麼標籤
`<head>` 標籤在加載網頁時，內容不會顯示在瀏覽器中
因此 `<head>` 通常是放：
瀏覽器頁籤的標題和圖示
網頁的 Metadata（作者、關鍵字、Open Graph Data…..）
連結的檔案（CSS、JS）
---
### title

> 更改網頁頁籤文字
![](https://i.imgur.com/6fnYZq9.png)
```htmlembedded=
<html>
  <head>
    <title>Interneting Is Easy!</title>
  </head>
  <body>
    <!-- Content goes here -->
  </body>
</html>
```
---
### Meta

> 為敘述網頁的標籤，包含作者、文字編碼、網站說明文字、關鍵字….等
常用的屬性有： charset 、 name 、 content 、 http-equiv
>
> 1.charset
`<meta charset="utf-8">` 設定文字編碼
>
> utf-8 為最通用的文字編碼，又稱萬國碼，可支援各語系文字
每個語系有自己的文字編碼，像是繁體中文就叫做 Big-5
但如果使用 Big-5 碼，解譯其他語言就會變成亂碼，如下圖
因此使用 utf-8 會最為合適
![](https://i.imgur.com/pONR5Ao.png)
```htmlembedded=
<html>
  <head>
    <title>Interneting Is Easy!</title>
    <meta charset='UTF-8'/>  
  </head>
  <body>
    <h2>Character Sets</h2>

       <p>You can use UTF-8 to count in Turkish:</p>

       <ol>
         <li>bir</li>
         <li>iki</li>
         <li>üç</li>
         <li>dört</li>
         <li>beş</li>
       </ol>
  </body>
</html>
```
> **2. name & content**
>
> name & content 的應用十分多元，像是：
>
>作者
```htmlembedded=
<meta name="author" content="Kion">
```
>
>網頁摘要
```htmlembedded=
<meta name="description" content="這是顯示在搜尋結果中，網頁標題下的網頁摘要">
```
> meta description 的內容也會成為搜尋的關鍵字之一，但並非是網站排名的因素之一
若沒有特別撰寫，則會從網頁上的內容抓取

---
### Link

> Link 標籤十分常見，凡事要引入 CSS或是外部資源，皆需要透過 Link 標籤連接，應用十分多元
>
> 連接 CSS
```htmlembedded=
<link rel="stylesheet" type="text/css" href="css.css">`
```
>
> 但注意，JS 不是用 `<link>` 喔
```htmlembedded=
<script type="text/javascript" src="script.js"></script>`
```
>
> 設置網頁頁籤 Icon
我 Icon 的圖檔是在這裡轉的：http://tw.faviconico.org/
轉好圖檔後，在 head 引入檔案
```htmlembedded=
<link rel="Shortcut Icon" type="image/x-icon" href="filename.ico">
```
>
> 引入 Icon
我使用的網站是：https://fontawesome.com/
使用方法很簡單，如果你沒有課金就選一個免費的 Icon
記得在 head 引入來源

```htmlembedded=
<link rel=”stylesheet” href=”https://use.fontawesome.com/releases/v5.8.2/css/all.css" integrity=”sha384-oS3vJWv+0UjzBfQzYUhtDYW+Pj2yciDJxpsK1OYPAYjqT085Qq/1cq5FLXAZQ7Ay” crossorigin=”anonymous”>
```

> 接著只要在你再插入圖示的那一行，複製該圖示的程式碼
例如：
```htmlembedded=
<i class=”fab fa-angellist”></i>
```
>  就可以插入 Icon 了！
當然也可以客製化 Icon 大小、顏色喔
https://fontawesome.com/how-to-use/on-the-web/styling/sizing-icons
---
### Open Graph Data 標籤

> 主要用於該網站 URL 被轉貼在社交軟體上，顯示的標題、內容圖片、簡介
甚至可以調整大小
>
>例如：
> 1. 圖片
```htmlembedded=
<meta property="og:image" content="https://developer.cdn.mozilla.net/static/img/opengraph-logo.dc4e08e2f6af.png">
```
> 2. 連結文字描述
```htmlembedded=
<meta property="og:description" content="The Mozilla Developer Network (MDN) provides information about Open Web technologies including HTML, CSS, and APIs for both Web sites and HTML5 Apps. It also documents Mozilla products, like Firefox OS.">
```
> 3. 標題
```htmlembedded=
<meta property="og:title" content="Mozilla Developer Network">
```



