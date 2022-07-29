---
title: (Vue) Props 向內層元件傳遞資料狀態
date: 2021-08-14
description: 資料狀態紀錄筆記
categories:
- Vue
tags:
- Vue
---
## 靜態資源

傳入圖片連結範例：

- 在建立好的 app.component 方法內建立 props 變數且帶入一個陣列  array，且新增資料 url
- 將 template 帶上 `<img>` 標籤，且使用 `v-bind:src="url"`
- 在 html 內新增上 template 名稱的標籤
  - 加上屬性為 props 內的資料
  - 在新增上所要傳送的網址資料

![props](https://i.imgur.com/jVmv4qY.png)
傳入同個物件多筆資料範例：( x-template )

- 在資料集內建立一個物件 items ，賦予兩個變數分別為圖片連結以及文字
- 建立 x-template 元件 card，新增上 props 資料為 imgUrl
- 圖片網址使用：元件內使用 v-bind 綁定 imgUrl.url
- 圖片文字使用：因為單純渲染文字所以直接使用花括號 {{ imgUrl.text }} 來渲染資料

```html =
<div id="app">
  <div class="container">
    <div class="row">
      <div class="col-md-4">
        <card :img-url="items"></card>
      </div>
    </div>
  </div>
</div>

<script type="text/x-template" id="card">
<div>
  <img class="card-img-top" :src="imgUrl.url" alt="Card image cap">
  <h1>{{ imgUrl.text }}</h1>
  </div>
</script>

<script type="module">
  
  const app = Vue.createApp({
    data() {
      return {
        items: {
          url:"https://images.unsplash.com/photo-1629212346682-4890b9d73992?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=934&q=80",
          text:"picture.title"
        }
      };
    },
  });

  app.component('card', {
    props: ['imgUrl'],
    template: `#card`
  });

  app.mount('#app');

</script>
```

<iframe height="300" style="width: 100%;" scrolling="no" title="props 傳入同個物件多筆資料" src="https://codepen.io/michael-luo/embed/vYmqoJJ?default-tab=html%2Cresult&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/michael-luo/pen/vYmqoJJ">
  props 傳入同個物件多筆資料</a> by Michael Luo (<a href="https://codepen.io/michael-luo">@michael-luo</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

## 動態資源

切記前內、後外這個口訣

- 前內：v-bind: 所綁定的內層 template 的變數 props 內的資料
- 後外：v-bind:url ="" 所綁定的外層資料，也就是 data 內的資料

![props02](https://i.imgur.com/811PVAJ.png)


## 單向數據流

此範例單向數據流的單向指的是，由外部資料傳入到內部資料來做傳遞資料，
photo2 元件內的 template 有使用到 input 加上 v-model 來綁定 url 參數，企圖使用 v-model 來更新資料，但事實上是無法的，下方會做解釋

```html =
<h3>單向數據流</h3>
<photo2 :url="imgUrl"></photo2>
```

```jsx =
const app = Vue.createApp({
    data() {
      return {
        imgUrl: 'https://images.unsplash.com/photo-1605784401368-5af1d9d6c4dc?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=600&q=80',
      };
    },
  });

  app.component('photo2', {
    props: ['url'],
    template: `<img :src="url" class="img-thumbnail" alt><br>
    <input type="text" v-model="url"> {{ url }}`
  })

  app.mount('#app');
```

當我們往 input 內塞入資料時會爆錯，Props are readonly ( Props 有讀取限制，無法被調整)，外部所定義的資料，當他往內層傳遞時，屬於單向性，無法使用 Vue 指令來操作它

![console爆錯誤內容](https://i.imgur.com/VPwO9sP.png)

console 爆錯內容

# 命名限制

<aside>
💡 因為 html 內有規定，標籤屬性都只能使用小寫 !
</aside>

props 內的資料假使命名為 `props:['imageUrl']`，是無法被讀取到的，
可以將 html 屬性改為 image-url 的命名即可正確顯示，也是可以被正確綁定到資料的！
未來在做 debug 時也可以更快速備查找到。

```html =
<h3>命名限制</h3>

<!-- 錯誤  -->
<photo3 :superUrl="imgUrl"></photo3>

<!-- 正確  -->
<photo3 :super-url="imgUrl"></photo3>

<script type="module">
          // 區域註冊
  const app = Vue.createApp({
    data() {
      return {
        imgUrl: 'https://images.unsplash.com/photo-1605784401368-5af1d9d6c4dc?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=600&q=80',
      };
    },
  });

  app.component('photo3', {

    props: ['superUrl'],
    template: `<img :src="superUrl" class="img-thumbnail" alt>`
  })
  app.mount('#app');
</script>
```
