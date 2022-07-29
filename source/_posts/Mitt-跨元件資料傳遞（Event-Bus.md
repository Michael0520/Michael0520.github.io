---
title: (Vue) Mitt 跨元件資料傳遞 Event Bus
date: 2021-08-18
description: 將兩個完全不同的元件，透過外部套件來實作資料傳遞
categories:
- Vue
tags:
- Vue
---

將兩個完全不同的元件，透過外部套件來實作資料傳遞

![image](https://i.imgur.com/Mj8urxt.png)

## 引入 mitt 套件

```jsx
// mitt 套件使用起手式
import 'https://unpkg.com/mitt/dist/mitt.umd.js'; // mitt
// const 自訂名稱 = mitt 方法
const emitter = mitt()
```

## 建立發送資料元件

- 建立內部資料 product
- 建立內部方法 `sendData()`
  - 使用 mitt 語法來傳送資料  `emitter.emit('自定義名稱', 參數)`
- 建立元件來觸發方法

    ```html
    <div class="card">
      <div class="card-body" >
        <!-- click Event  -->
        <button @click="sendData">送出</button>
      </div>
    </div>
    ```

完整程式碼：

```jsx
const cardEmit = {
    data(){
      return{
        product: {
          name: '蛋餅',
          price: 30,
          vegan: false
        },
      }
    },
    methods:{
      sendData() {
        console.log(`sendData 觸發`)
        // 資料往另一個元件做發送
        // emitter.emit('自定義名稱',參數)
        emitter.emit('sendProduct', this.product)
      }
    },
    template:`<div class="card">
      <div class="card-body" >
        <button @click="sendData">送出</button>
      </div>
    </div>`
  }
```

## 建立監聽＆接收資料元件

- 建立接收資料要存放的空間
  - `item:{}`
- 建立監聽（建議放置在 created 內，確保元件在完成創建時，會被監聽到）
- 監聽語法：`emitter.on('自定義名稱', (參數) ⇒ {...})`
- 內部元件新增讀取資料方式
  - `{{item}}`

```jsx
const cardOn = {
    data(){
      return{
        item:{}
      }
    },
    created(){
      // 放置在 created 原因為：
      // 當此元件被創建時，就會啟用此 .on 的監聽方法
      emitter.on('sendProduct',(product) => {
        console.log('card-on',product)
        this.item = product
      })
    },
    template:`<div class="card">
      <div class="card-body">
        item: {{ item }}
        <hr>
        ProductName: {{item.name}}
      </div>
    </div>`
  }
```

<iframe height="300" style="width: 100%;" scrolling="no" title="Mitt 跨元件資料傳遞（Event Bus）" src="https://codepen.io/michael-luo/embed/NWgPdQN?default-tab=html%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/michael-luo/pen/NWgPdQN">
  Mitt 跨元件資料傳遞（Event Bus）</a> by Michael Luo (<a href="https://codepen.io/michael-luo">@michael-luo</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>
