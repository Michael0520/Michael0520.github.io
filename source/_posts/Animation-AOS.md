---
title: (CSS) Animation AOS
date: 2022-05-21 04:38:48
cover: https://i.pinimg.com/564x/67/2b/cd/672bcd39081503b89173ceb1cf182573.jpg
tags:
  - CSS
---

:::tip
CSS Animation AOS 套件安裝到使用
:::

## Installation

```base
npm install aos --save
```

import :

```javascript
import { createApp } from "vue";
import App from "./App.vue";

// importing AOS
import AOS from "aos";
import "aos/dist/aos.css";

const app = createApp(App);

app.use(AOS.init());

app.mount("#app");
```

document template : (long code)

demo website

```html
<template>
  <div class="hello">
    <!-- card 1 -->
    <div
      data-aos="zoom-in"
      class="card"
      style="width: 18rem; margin: 100px auto;"
    >
      <img
        src="https://images.unsplash.com/photo-1488590528505-98d2b5aba04b?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1500&q=80"
        class="card-img-top"
        alt="..."
      />
      <div class="card-body">
        <h5 class="card-title">Card 1</h5>
        <p class="card-text">
          Some quick example text to build on the card title and make up the
          bulk of the card's content.
        </p>
        <a href="#" class="btn btn-primary">Go somewhere</a>
      </div>
    </div>

    <!-- card 2 -->
    <div
      data-aos="new-animation"
      data-aos-offset="200"
      data-aos-easing="ease-in-out"
      class="card"
      style="width: 18rem; margin: 200px auto;"
    >
      <img
        src="https://images.unsplash.com/photo-1496171367470-9ed9a91ea931?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1500&q=80"
        class="card-img-top"
        alt="..."
      />
      <div class="card-body">
        <h5 class="card-title">Card 2</h5>
        <p class="card-text">
          Some quick example text to build on the card title and make up the
          bulk of the card's content.
        </p>
        <a href="#" class="btn btn-primary">Go somewhere</a>
      </div>
    </div>

    <!-- card  3-->
    <div
      data-aos="fade-right"
      class="card"
      style="max-width: 18rem; margin: 200px auto;"
    >
      <img
        src="https://images.unsplash.com/photo-1496171367470-9ed9a91ea931?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1500&q=80"
        class="card-img-top"
        alt="..."
      />
      <div class="card-body">
        <h5 class="card-title">Card 3</h5>
        <p class="card-text">
          Some quick example text to build on the card title and make up the
          bulk of the card's content.
        </p>
        <a href="#" class="btn btn-primary">Go somewhere</a>
      </div>
    </div>

    <!-- card 4 -->
    <div
      data-aos="fade-left"
      class="card"
      style="width: 18rem; margin: 200px auto;"
    >
      <img
        src="https://images.unsplash.com/photo-1519389950473-47ba0277781c?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1500&q=80"
        class="card-img-top"
        alt="..."
      />
      <div class="card-body">
        <h5 class="card-title">Card 4</h5>
        <p class="card-text">
          Some quick example text to build on the card title and make up the
          bulk of the card's content.
        </p>
        <a href="#" class="btn btn-primary">Go somewhere</a>
      </div>
    </div>
    <!-- card 5 -->
    <div
      data-aos="flip-left"
      class="card"
      style="width: 18rem; margin: 200px auto;"
    >
      <img
        src="https://images.unsplash.com/photo-1593642632823-8f785ba67e45?ixid=MnwxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=889&q=80"
        class="card-img-top"
        alt="..."
      />
      <div class="card-body">
        <h5 class="card-title">Card 5</h5>
        <p class="card-text">
          Some quick example text to build on the card title and make up the
          bulk of the card's content.
        </p>
        <a href="#" class="btn btn-primary">Go somewhere</a>
      </div>
    </div>
  </div>
</template>
```

global init :

```javascript
AOS.init();
// You can also pass an optional settings object
// below listed default settings
AOS.init({
  // Global settings:
  disable: false, // accepts following values: 'phone', 'tablet', 'mobile', boolean, expression or function
  startEvent: "DOMContentLoaded", // name of the event dispatched on the document, that AOS should initialize on
  initClassName: "aos-init", // class applied after initialization
  animatedClassName: "aos-animate", // class applied on animation
  useClassNames: false, // if true, will add content of `data-aos` as classes on scroll
  disableMutationObserver: false, // disables automatic mutations' detections (advanced)
  debounceDelay: 50, // the delay on debounce used while resizing window (advanced)
  throttleDelay: 99, // the delay on throttle used while scrolling the page (advanced)

  // Settings that can be overridden on per-element basis, by `data-aos-*` attributes:
  offset: 120, // offset (in px) from the original trigger point
  delay: 0, // values from 0 to 3000, with step 50ms
  duration: 400, // values from 0 to 3000, with step 50ms
  easing: "ease", // default easing for AOS animations
  once: false, // whether animation should happen only once - while scrolling down
  mirror: false, // whether elements should animate out while scrolling past them
  anchorPlacement: "top-bottom", // defines which position of the element regarding to window should trigger the animation
});
```

基本套用
範例 1：有哪些動畫效果
data-aos：套用哪個動畫效果，官方提供。
在想要套用的元素上，加上 data-aos 屬性及動畫效果，例：

```html
<div class="custom_block" data-aos="fade-up">測試的文字2</div>
```

最後再執行以下 JS 程式：

```javascript
AOS.init();
```

### 範例 2：瞭解 aos 基本屬性

`data-aos-easing`：官方提供。ease 是預設。
`data-aos-duration`：0 ~ 3000 毫秒。400 是預設。
`data-aos-delay`：0 ~ 3000 毫秒。0 是預設。
`data-aos-once`：是否僅執行一次( true 或 false )。false 是預設。

### 範例 3：瞭解 data-aos-offset

- `data-aos-offset`：預設是 120，單位是 px。當螢幕的下方經過該元素之後，這 120 指的是該元素的上方、螢幕的底部，距離是 120px 時，會觸發動畫效果。

以下範例請將 `data-aos-offset` 由 120 改為 0，觀察看看，也就是該元素的上方、螢幕的底部碰到的時候，就觸發動畫效果。
