---
title: (Vue) Emit 向外層傳遞事件
date: 2021-08-15
description: 可以不用一定要傳遞數值，可以只傳送事件
categories:
  - Vue
tags:
  - Vue
---

<aside>
💡 可以不用一定要傳遞數值，可以只傳送事件
</aside>

- 定義外層事件
- 定義內層事件且將 emit 做命名
- 在 html 標籤加上綁上事件 `v-on:內層 emit 名稱 = "外層事件"`

# Emit 來觸發外部事件

- 先定義外層接收的方法
- 定義內層的 $emit 觸發方法
- 使用 `v-on` 的方式觸發外層方法（口訣：前內、後外）
  - 元件內層的 $emit 會指向到外層的 html 標籤上
  - html 標籤會根據 `v-on:emit-num` 所綁定的事件做觸發

![傳遞事件流程圖](https://i.imgur.com/BiymkjR.png)
傳遞事件流程圖

完整程式碼：

```htmlembedded=
<div id="app">
  {{ num }}
  <button-counter v-on:emit-num="addNum"></button-counter>
</div>
```

```jsx
const app = Vue.createApp({
    data() {
      return {
        num: 0,
      };
    },
    methods: {
      addNum(){
        console.log('觸發 addNum')
        this.num++
      }
    }
  });

  app.component('button-counter', {
    methods: {
      click(){
        console.log('觸發 $emit')
        this.$emit('emit-num')
      }
    },
    template: `<button type="button" 
    @click="click"> add </button>`
  });

  app.mount('#app');
```

# 傳遞資料狀態

將內部資料透過事件渲染到畫面上

- 先定義外層接收的方法
- 定義內層的 $emit 觸發方法
- 使用 `v-on` 的方式觸發外層方法（口訣：前內、後外）
    - 元件內層的 $emit 會指向到外層的 html 標籤上
    - html 標籤會根據 `v-on:emit-num` 所綁定的事件做觸發

![](https://i.imgur.com/sQFAonC.png)


# 命名限制

<aside>
💡 因為 html 內有規定，標籤屬性都只能使用小寫 !

</aside>

props 內的資料假使命名為 `this.$emit('emitText')`
直接新增此名稱上 html 時是無法被讀取到的，可以改用：

1. html 屬性改為：`@emit-text`
2. $emit 名稱改為：`this.$emit('emit-text')`

Demo:

<iframe height="300" style="width: 100%;" scrolling="no" title="Emit 向外層傳遞事件" src="https://codepen.io/michael-luo/embed/eYWqrRa?default-tab=html%2Cresult&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/michael-luo/pen/eYWqrRa">
  Emit 向外層傳遞事件</a> by Michael Luo (<a href="https://codepen.io/michael-luo">@michael-luo</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>