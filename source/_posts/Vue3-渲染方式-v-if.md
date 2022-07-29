---
title: Vue3 渲染方式 (v-if)
date: 2021-07-28
categories:
- Vue
tags:
- Vue
---

Demo:

<iframe height="300" style="width: 100%;" scrolling="no" title="Vue 3 (v-if)" src="https://codepen.io/michael-luo/embed/BaRLYwY?default-tab=html%2Cresult&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/michael-luo/pen/BaRLYwY">
  Vue 3 (v-if)</a> by Michael Luo (<a href="https://codepen.io/michael-luo">@michael-luo</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

## 綁定資料內容，使用動作事件去切換

使用 Button 動態切換綁定的資料狀態，HTML 中的 `v-if-else` 對應切換的綁定狀態做渲染，

- true : 顯示 `<p>` 小明飽了
- false :顯示 `<p>` 小明還沒吃飽

```html
<p v-if="isFull">小明飽了</p>
<p v-else="isFull">小明還沒吃飽</p>

<button type="button" v-on:click="change('isFull')">
  狀態切換
</button>
```

```jsx
const App = {
  data() {
    return {
      name: "小明",
      isFull: true,
    }
  }
```

## 動態綁定且切換多組資料內容

- `<a>` :
  1. `v-on:click` 透過點擊事件，綁定以及更動資料內容
  2. `v-bind:class` 綁定並寫上判斷式，只要符合特定資料內容，就會賦予上特定 class
- `<div>` :
  - `v-if-else` 使用判斷式，篩選出所要顯示的資料
 範例程式碼：

```html
<nav class="nav nav-pills nav-fill">

  <a
    class="nav-link"
    href="#"
    v-bind:class="{ 'active': link === '小明' }"
    v-on:click="link = '小明'"
    >小明</a
  >
  <a
    class="nav-link"
    href="#"
    v-bind:class="{ 'active': link === '小美' }"
    v-on:click="link = '小美'"
    >小美</a
  >
  <a
    class="nav-link"
    href="#"
    v-bind:class="{ 'active': link === '杰倫' }"
    v-on:click="link = '杰倫'"
    >杰倫</a
>
<div>
  {{link}}
  <div v-if="link === '小明'">小明吃早餐</div>
  <div v-else-if="link ==='小美'">小美去百貨公司</div>
  <div v-else-if="link === '杰倫'">杰倫去幫助人</div>
</div>

</nav>
```

```html
const App = {
  data() {
  return {
    name: "小明",
    isFull: true,
    link: "小明",
  }
}
```

![成功後預覽圖](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/268ca7a7-f542-43c4-8d79-6b90213192fb/CleanShot_2021-07-11_at_04.17.01.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211104T120152Z&X-Amz-Expires=86400&X-Amz-Signature=27e20a5ede885b8483c2a1376063b4f2c494499905dc6729f61eff929f065261&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22CleanShot_2021-07-11_at_04.17.01.gif%22)

成功後預覽圖

## `v-if` & `v-for` 混用

使用 `v-for` 一次渲染多組資料，且使用 `v-if` 來篩選所要渲染的資料

⚠️ 不推薦同時使用 v-if 和 v-for，
當 v-if 與 v-for 一起使用時，v-if 具有比 v-for 更高的優先級。

### `<template>` 包裹指令元件

- `v-for`: 將需要使用渲染多組資料的指令，綁定在外層 `<template>`上
- `v-if`: 篩選或是判斷資料且渲染的指令，放在主件 `<li>` 上

```jsx
<ul>
  <template v-for="(item, index) in products" :key="item.name">

    <li v-if="item.price <= 35"> 
      {{ item.name}} / {{ item.price }} 元
    </li>

  </template>
</ul>
```

```jsx
const App = {
  data() {
    return {
      products: [
        {
          name: "蛋餅",
          price: 30,
          vegan: false,
        },
        {
          name: "飯糰",
          price: 35,
          vegan: false,
        },
        {
          name: "小籠包",
          price: 60,
          vegan: false,
        },
        {
          name: "蘿蔔糕",
          price: 30,
          vegan: true,
        },
      ],
    }
  }
```

![image](https://i.imgur.com/uh20pzk.png)

畫面顯示預覽圖

## `v-if` 與 `v-show`

### 特色差異

- `v-if` : 屬於”真正“的條件渲染，
    因為它會確保在切換過程中，條件塊內的事件監聽器和子組件適當地被銷毀和重建。

- 以 HTML 渲染上來說，`v-if`是有條件的渲染的，
    若條件判斷為 true 則渲染；而`v-show`則是無條件渲染，但視條件以 inline style css 隱藏。
- 相比之下，`v-show`就簡單得多，不管初始條件是什麼，元素總是會被渲染，並且只是簡單地基於CSS進行切換。
- `v-if`有更高的切換開銷，而`v-show`有更高的初始渲染開銷。
  - 實務上如果需要非常頻繁地切換，則使用`v-show`較好；
  - 如果在運行時條件很少改變，則使用`v-if`較好。
- `<template>`可用`v-if`決定是否出現，但無法使用`v-show`。

### CSS 隱藏機制

當將 `v-show` 條件為 false 時，資料並沒有刪除，只是使用 css `display:none` 將它隱藏了

範例程式碼：

```html
<p v-show="isFull">小明 飽了</p>
<button type="button" v-on:click="change('isFull')">
  狀態切換
</button>
```

```javascript
const App = {
  data() {
    return {
      isFull: true,
    }
  }
```

![image](https://i.imgur.com/1mYqxQj.png)
v-show 為 false 時，隱藏所使用的 css 設定

Demo:

<iframe height="300" style="width: 100%;" scrolling="no" title="Vue 3 (v-if)" src="https://codepen.io/michael-luo/embed/BaRLYwY?default-tab=html%2Cresult&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/michael-luo/pen/BaRLYwY">
  Vue 3 (v-if)</a> by Michael Luo (<a href="https://codepen.io/michael-luo">@michael-luo</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

### 綁定資料內容，使用動作事件去切換

使用 Button 動態切換綁定的資料狀態，HTML 中的 `v-if-else` 對應切換的綁定狀態做渲染，

- true : 顯示 `<p>` 小明飽了
- false :顯示 `<p>` 小明還沒吃飽

```html
<p v-if="isFull">小明飽了</p>
<p v-else="isFull">小明還沒吃飽</p>

<button type="button" v-on:click="change('isFull')">
  狀態切換
</button>
```

```jsx
const App = {
  data() {
    return {
      name: "小明",
      isFull: true,
    }
  }
```

## 動態綁定且切換多組資料內容

- `<a>` :
    1. `v-on:click` 透過點擊事件，綁定以及更動資料內容
    2. `v-bind:class` 綁定並寫上判斷式，只要符合特定資料內容，就會賦予上特定 class
- `<div>` :
  - `v-if-else` 使用判斷式，篩選出所要顯示的資料

 範例程式碼：

```jsx
<nav class="nav nav-pills nav-fill">

  <a
    class="nav-link"
    href="#"
    v-bind:class="{ 'active': link === '小明' }"
    v-on:click="link = '小明'"
    >小明</a
  >
  <a
    class="nav-link"
    href="#"
    v-bind:class="{ 'active': link === '小美' }"
    v-on:click="link = '小美'"
    >小美</a
  >
  <a
    class="nav-link"
    href="#"
    v-bind:class="{ 'active': link === '杰倫' }"
    v-on:click="link = '杰倫'"
    >杰倫</a
>
<div>
  {{link}}
  <div v-if="link === '小明'">小明吃早餐</div>
  <div v-else-if="link ==='小美'">小美去百貨公司</div>
  <div v-else-if="link === '杰倫'">杰倫去幫助人</div>
</div>

</nav>
```

```javascript
const App = {
  data() {
    return {
      name: "小明",
      isFull: true,
      link: "小明",
    }
  }
```

![成功後預覽圖](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/268ca7a7-f542-43c4-8d79-6b90213192fb/CleanShot_2021-07-11_at_04.17.01.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211104T120152Z&X-Amz-Expires=86400&X-Amz-Signature=27e20a5ede885b8483c2a1376063b4f2c494499905dc6729f61eff929f065261&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22CleanShot_2021-07-11_at_04.17.01.gif%22)

成功後預覽圖

### `v-if` & `v-for` 混用

使用 `v-for` 一次渲染多組資料，且使用 `v-if` 來篩選所要渲染的資料

⚠️ 不推薦同時使用 v-if 和 v-for，
當 v-if 與 v-for 一起使用時，v-if 具有比 v-for 更高的優先級。

### `<template>` 包裹指令元件

- `v-for`: 將需要使用渲染多組資料的指令，綁定在外層 `<template>`上
- `v-if`: 篩選或是判斷資料且渲染的指令，放在主件 `<li>` 上

```javascript
<ul>
  <template v-for="(item, index) in products" :key="item.name">

    <li v-if="item.price <= 35"> 
      {{ item.name}} / {{ item.price }} 元
    </li>

  </template>
</ul>
```

```javascript
const App = {
  data() {
    return {
      products: [
        {
          name: "蛋餅",
          price: 30,
          vegan: false,
        },
        {
          name: "飯糰",
          price: 35,
          vegan: false,
        },
        {
          name: "小籠包",
          price: 60,
          vegan: false,
        },
        {
          name: "蘿蔔糕",
          price: 30,
          vegan: true,
        },
      ],
    }
  }
```

![image](https://i.imgur.com/ybBn4MT.png)
畫面顯示預覽圖

## `v-if` 與 `v-show`

### 特色差異

- `v-if` : 屬於”真正“的條件渲染，
    因為它會確保在切換過程中，條件塊內的事件監聽器和子組件適當地被銷毀和重建。
- 以 HTML 渲染上來說，`v-if`是有條件的渲染的，
    若條件判斷為 true 則渲染；而`v-show`則是無條件渲染，但視條件以 inline style css 隱藏。
- 相比之下，`v-show`就簡單得多，不管初始條件是什麼，元素總是會被渲染，並且只是簡單地基於CSS進行切換。
- `v-if`有更高的切換開銷，而`v-show`有更高的初始渲染開銷。
  - 實務上如果需要非常頻繁地切換，則使用`v-show`較好；
  - 如果在運行時條件很少改變，則使用`v-if`較好。
- `<template>`可用`v-if`決定是否出現，但無法使用`v-show`。

### CSS 隱藏機制

當將 `v-show` 條件為 false 時，資料並沒有刪除，只是使用 css `display:none` 將它隱藏了

範例程式碼：

```html
<p v-show="isFull">小明 飽了</p>
<button type="button" v-on:click="change('isFull')">
  狀態切換
</button>
```

```jsx
const App = {
  data() {
    return {
      isFull: true,
    }
  }
```

![image](https://i.imgur.com/mYxDKy3.png)
v-show 為 false 時，隱藏所使用的 css 設定