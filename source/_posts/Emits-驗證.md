---
title: (Vue) Emits 驗證
date: 2021-08-16
description: 元件驗證
categories:
- Vue
tags:
- Vue
---
當我們要把內層的數值指向化定義到外層時，不是一定要重新 Methods，可以直接寫在 html 上

- 在 template 內加上 $emit 並且帶上事件名稱以及參數，即可觸發
- 在 html 上的元件內加上事件（口訣：前內($emit 的名稱 add)、後外（'addNum()'））

```html
<div id="app">
  <h3>Emits API</h3>
  {{ num }}
  <button-counter @add="addNum"></button-counter>
</div>

<script type="module">
          const app = Vue.createApp({
    data() {
      return {
        num: 0,
      };
    },
    methods: {
      addNum(num) {
        this.num = this.num + num;
      },
    }
  });

  app.component('button-counter', {
    data() {
      return {
        num: 1,
      }
    },
    template: `
      <button type="button"
        @click="$emit('add', num)">add</button>`,
  });

  app.mount('#app');
</script>
```

## 觀察 console 提示

- 建立一個新 button （調整 num 的值 ）
- 加上事件 `@click="num++"` ，會發現當我們在點擊此 button
  - 因為沒有使用 $emit ，所以畫面上並不會重新渲染
  - 在 console 內會爆出提示，告知你新的 button 沒有加上 $emit 來傳遞事件

![](https://i.imgur.com/Ig3jcM0.png)console 提示

- 此時再去按下上個範例 `$emit('add')` ，會發現裡頭的資料已經被改動了
  - 當點了幾下調整 button ，就會將實體 app 的 num 進行 +1
  - 按了五次，實體 app 的 num = 5
  - 再去按下 `$emit('add')` ，會發現每次按下都是為 +5

<iframe height="300" style="width: 100%;" scrolling="no" title="Vue 3 Emits 驗證" src="https://codepen.io/michael-luo/embed/zYzYWGw?default-tab=html%2Cresult&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/michael-luo/pen/zYzYWGw">
  Vue 3 Emits 驗證</a> by Michael Luo (<a href="https://codepen.io/michael-luo">@michael-luo</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

加入判斷式，來加快驗證問題，
假使參數不是 number 的會，就會在 console 爆出警告提示內容

```javascript
emits: {
      add:(num)=>{
        // 不管 true or false 都會運行結果！
        // 但是會跳出提示警告
        if (typeof num !== 'number') {
          console.warn('add 事件參數型別須為 Number')
        }
        return typeof num === 'number'
      }
    },
```
