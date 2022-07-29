---
title: 初探 CSS 
description:  CSS 語言是專為定義網頁的版面設計（layout）而發明的，你可以透過它指定文件中各項 HTML 元件的視覺樣式。
date: 2020-11-08
categories:
- CSS
tags: 
- CSS
---

# CSS

###### tags: `CSS`

#### CSS 語言是專為定義網頁的版面設計（layout）而發明的，你可以透過它指定文件中各項 HTML 元件的視覺樣式。
#### CSS 的全名是 Cascading Style Sheets，階層樣式表。而所謂的「階層式 (cascading)」，指的是我們可以在同一個元件上套用不同樣式，樣式與樣式之間則存在相對的階層關係。

---
CSS 語法規則
以這段 CSS 為例：

```css
h1 {
 color: #ff6600;
}
```

這段是一個 CSS 宣告的長相：
![](https://i.imgur.com/MEWWPQ8.png)

* 選擇器 (selector) 定義你的樣式對誰有作用，它對應的可能是 HTML 標籤名稱或者是 class 和 id 屬性，我們在後面會再介紹選擇器。`{}`：大括號包圍了一個宣告區域，任何寫在這個區域裡的設定，會對文件裡所有的 `<h1>` 標籤起作用。
* 屬性與值：此圖片說明，我們宣告選擇器，也就是 `<h1>` 的「文字顏色」(color) 屬性的值是 #ff6600。請注意 CSS 是用冒號 ( : ) 而非等號 (=) 來設定。
* 每條宣告用分號 ( ; ) 隔開

---
### 引用 CSS 方式

**1. 外部檔案引入 (建議方法)**

**`<link rel='stylesheet' href='style.css'>`**
> * `<link>` 是一種「後設元素」(meta element)只能放在標頭裡，他可以載入外部檔案。
所以瀏覽器讀取到這一行時，就會自動載入 CSS 文件的全部內容。
> * `rel='stylesheet'` 告訴文件載入的資源是樣式表，所以瀏覽器就知道要用讀 CSS 的方式去處理載入的內容。
> * `href='style.css' href` 屬性和 `<a>` 標籤時的用法一樣，描述路徑，讓瀏覽器找得到檔案。
>
> ![](https://i.imgur.com/X8x2Jej.png)

**2. 內嵌在 html檔案裡**

**`<p style='color: red; font-size: 10pt;'>一段文字</p>`**

> 這種宣告方式只會影響到這一個標籤，而不是所有的 `<p>`。
這是一個很簡便的作法，但 CSS 宣告混合在 HTML 結構中，無法進行管理。你可能會在寫 blog 時偶爾不得不這麼做(因為你無法在別人家的平台上開新檔案)。
> 
> 在 HTML 內嵌 STYLE 標籤，其效果比較可以從下圖看得出來，左邊是用 Sublime 編輯器在 HTML 裡先寫好，文字是紅色與文字 30pt 大。
>
> ![](https://i.imgur.com/lC84z4b.png)

**3. 標頭裡的 style 標籤** 

**`<style></style>`**

> 這樣做會讓你影響到這份 HTML 文件裡所有的 `<p>`，如果你的網站真的只有> 一張，這不失為一個快速的方法。然而，這樣做同樣有讓語法變得冗長，以及在檔案變多時維護困難的問題。當前的趨勢是將 HTML 和 CSS 分開維護，因此，請你習慣建立外部檔案來管理你的 CSS 樣式表。
```htmlembedded=
<head>
<title>CSS 宣告</title>
<style>
p { color: black; font-size: 10pt;}
</style>
</head>
```

---

### 註解 (Comment)
要小心 CSS 的註解方式跟 HTML 不一樣，CSS 的註解是用 /* 與 */ 來包圍：

```css=
body {
 color: #FF6600;    /* 這是 Alpha Camp 最喜歡的橘紅色 */
}
```
---
### 多重選擇 (整理程式碼)
你可以連結宣告多個 CSS 設定：
```css=
h1 {
 font-family: "Helvetica", "Arial", sans-serif;  /* 指定字型 */
 color: green;
}

h2 {
 font-family: "Helvetica", "Arial", sans-serif;
 color: blue;
}
```

font-family 字型選擇的意思，這邊設定的字型要以大多瀏覽器都相容支援的字型為主

但在這裡，有沒有發現字型 (font) 那一行重覆在 h1 和 h2 出現？
也就是說，`<h1>` 與 `<h2>` 的字型其實是一樣，只有文字顏色 (font color) 不一樣。如果你總是這樣寫，當我們需要改變 `<h1>` 與 `<h2>`的字型是，很容易就會改了這邊、漏了那邊。所以，你需要學習做整理和合併：
```css=
h1, h2 {
 font-family: "Helvetica", "Arial", "sans-serif";
}

h1 {
 color: green;
}

h2 {
 color: blue;
}
```

如此一來你就能統一管理 h1 和 h2 的字型了！






