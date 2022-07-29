---
title: (Vue) Methods
date: 2021-08-05
description: Methods 運算
categories:
- Vue
tags:
- Vue
---
## Demo

<iframe height="300" style="width: 100%;" scrolling="no" title="Vue3 Methods" src="https://codepen.io/michael-luo/embed/YzVOagy?default-tab=html%2Cresult&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/michael-luo/pen/YzVOagy">
  Vue3 Methods</a> by Michael Luo (<a href="https://codepen.io/michael-luo">@michael-luo</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

## methods 的結構

- 由 methods 定義的物件
- 內層均是函式

## methods 的觸發方法（點擊、其它 options api、生命週期...）

### 範例 1

建立兩個 button

1. 點擊觸發：基礎點擊事件觸發 methods
2. 呼叫其他的 methods：使用 this.otherMethod 來呼叫它

```html
<button type="button" @click="trigger('Click Methods')"
          class="btn btn-primary">點擊觸發</button>

  <button type="button" @click="callOtherMethod"
          class="btn btn-primary">呼叫另一個 methods</button>
```

```jsx
methods:{
  trigger(name) {
      console.log(name, '此事件被觸發了')
    },
  callOtherMethod() {
    // this.trigger('由 callOtherMethod 觸發')
    this.trigger('callOtherMethod 被觸發')
  },
}
```

### 範例 2

**使用綁定屬性來透過運算渲染出資料，篩選出大於等於 0 的數字到畫面上**

```html
<ul>
  <li v-for="number in filterPositive(numbers)">{{ number }}</li>
</ul>
```

```jsx
const app = Vue.createApp({
  data(){
    return{
      numbers: [-9, 12, 0, 0.5, 8, 2]
    },
    methods:{
      filterNumber(numbers){
        return numbers.filter((number) => number >= 0)
      }
    }
  }
})
 app.mount('#app');
```

## 使用 methods 處理複雜資料

將 products 陣列內的資料透過 `v-for` 來渲染出，

- `addToCart()`：建立新增資料
- `calculate()`：每新增一次資料，重新加總金額

```html
<ul>
  <li v-for="product in products" :key="product.name">
    {{ product.name }} / {{ product.price }}
    <button type="button" @click="addToCart(product)">加入購物車</button>
  </li>
</ul>
...
<h6>購物車項目</h6>
<ul>
  <li v-for="item in carts">{{ item.name }}</li>
</ul>
總金額 {{ sum }}
```

```jsx
const App = {
  data() {
    return {
      products: [{
          name: '蛋餅',
          price: 30,
          vegan: false
        },
        {
          name: '飯糰',
          price: 35,
          vegan: false
        },
        {
          name: '小籠包',
          price: 60,
          vegan: false
        },
        {
          name: '蘿蔔糕',
          price: 30,
          vegan: true
        },
      ],
      carts: [],
      sum: 0,
    }
  },
  methods:{
    addToCart(product) {
      this.carts.push(product)
      this.calculate()
    },
    calculate() {
      // this.calculate()
      console.log('觸發 calculate!')
      let total = 0
      this.carts.forEach(product => {
        total += product.price
      });

      console.log('總金額 ' + total)
      this.sum = total
	},
}
```

## 新增資料`addToCart()`

使用 `.push(product)` 來將所點選到的 item ，新增入購物車內 `carts[]`

務必也要將 Function 帶上 props ，才能夠成功取得該選定的資料

## 每新增一次資料，重新加總價格 `calculate()`

先設立初始化變數來存放總金額 `let total =0`

使用 `.forEach(product)` 一次性將目前所有選定的 item 做運算

## $filter （處理複雜運算）

時常會使用 NT$ 來標示金額，或是會去做折扣運算，

此時我們可以透過 Vue2 語法 $filter 來製作 function，

可以直接使用花括號`{{}}`來帶入 function 以及 data 內的資料去做渲染

```html
<h3>作為 $filter 使用（取代複雜表達式）</h3>
{{ convertToAmount(sum)}}
```

```jsx
const App = {
  data() {
    return {
      products: [{
          name: '蛋餅',
          price: 30,
          vegan: false
        },
        {
          name: '飯糰',
          price: 35,
          vegan: false
        },
        {
          name: '小籠包',
          price: 60,
          vegan: false
        },
        {
          name: '蘿蔔糕',
          price: 30,
          vegan: true
        },
      ],
      carts: [],
      sum: 0,
    }
  },
  methods:{
    addToCart(product) {
      this.carts.push(product)
      this.calculate()
    },
    calculate() {
      console.log('觸發 calculate!')
      let total = 0
      this.carts.forEach(product => {
        total += product.price
      });

      console.log('總金額 ' + total)
      this.sum = total

    // 新增的 Funtion
    convertToAmount(price) {
      return `八折後價格 NT$ ${price * 0.8}`
    }
  },
}
```
