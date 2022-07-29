---
title: (Vue) computed 運算
date: 2021-08-06
description: 在 Vue 中，computed 的屬性可以被視為像是 data 一樣，可以 讀取 和 設值，
categories:
- Vue
tags:
- Vue
---
## 簡介

**在 Vue 中，computed 的屬性可以被視為像是 data 一樣，可以 讀取 和 設值，**

**因此在 computed 中可以分成 `getter`（讀取） 和 `setter`（設值），
在沒有寫 setter 的情況下，computed 預設只有 getter ，也就是只能讀取，不能改變設值。**

**雖然說 computed 內的屬性可以被視為像是 data 一樣，**

**但在使用上，一般還是會讓 computed 類似唯讀的狀態，也就是去處理 `data` 資料，然後把它吐出來使用。**

**另外，在 getter 中，要記得搭配使用 `return` 來把值返回出來。**

基本的寫法如下：

預設只有 getter 的 computed

```jsx
const app = Vue.createApp({
  data(){
    return{
    }
  },
	computed: {
		computedData: function(){
				return //...
		}
})
 app.mount('#app');
})

```

有 setter 和 getter 的 computed

```jsx
const app = Vue.createApp({
  data(){
    return{
    }
  },
	computed: {
		computedData: {
			get: function(){
				// 必須使用 return 將值回傳到全域
				return // ...
			},
			set: function(){
				// ...
			}
		}
})
 app.mount('#app');
})
```

## 使用 Computed 將目前的數值運算呈現於畫面上

**計算屬性 Computed**

如果在模版內加入太多的邏輯運算，不但顯得雜亂也難以維護。

例如：在顯示預設的字串「Hello World!」之下，再顯示反轉後的字串。

```html
<div id="app">
  <p>原始訊息：{{ message }}</p>
  <p>反轉訊息：{{ message.split('').reverse().join('') }}</p>
</div>
```

```jsx
const app = Vue.createApp({
  data(){
    return{
      message: 'Hello World!',
    }
  }
})
 app.mount('#app');
```

如程式碼所示，將反轉的邏輯寫在樣版裡面。這看起來似乎把樣版弄得很髒亂(~~有潔癖？~~)，
基於凡是要切乾淨，未來才好維護的理由，

應該要把邏輯寫在一個可以純粹做計算的地方－計算屬性 (computed)。

改寫成這樣…

<iframe height="300" style="width: 100%;" scrolling="no" title="Vue 3 (computed)" src="https://codepen.io/michael-luo/embed/vYmYEwo?default-tab=html%2Cresult&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/michael-luo/pen/vYmYEwo">
  Vue 3 (computed)</a> by Michael Luo (<a href="https://codepen.io/michael-luo">@michael-luo</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

```html
<div id="app">
  <p>原始訊息：{{ message }}</p>
  <p>反轉訊息：{{ reversedMessage }}</p>
</div>
```

```jsx
const app = Vue.createApp({
  data(){
    return{
      text:'測試文字'
    }
  },
  computed:{
    reversedMessage: function(){
      return this.text
        .split('')
        .reverse('')
        .join('')
    },
  }
})
app.mount('#app');
```

是不是看起來清爽很多！？

computed 內 reversedMessage 的 function 內容，

將成為 reversedMessage 的 getter method，每當 message 的值有變化時，

便重新計算 reversedMessage。

computed 會將結果暫存起來，當參考到的資料改變時，computed 才會重新計算。

---

### 上一篇章範例實作改寫：

**使用 computed 來代替 methods 需要重複運算的結構**

```html
<ul>
  <li v-for="product in products">
    {{ product.name }} / {{ product.price }}
    <button type="button" @click="addToCart(product)">加入購物車</button>
  </li>
</ul>
...
<h6>購物車項目</h6>
<ul>
  <li v-for="item in carts">{{ item.name }}</li>
</ul>
total 的值 : {{total}} $
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
    computed: {
      total() {
        let total = 0
        this.carts.forEach(item => {
          total += item.price
        });
        return total
      }
    },
    methods: {
      addToCart(product) {
        this.carts.push(product)
      },
		// 原始代碼
		// addToCart(product) {
		/*   this.carts.push(product)
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
		     },
		*/

    },
  };
  Vue.createApp(App).mount('#app');
```

原先還要透過在 addToCart() 加入 其他的 function 來執行，

確保在每一次新增資料時，都會重新渲染總價格，

更改成 computed 後，相對程式碼就更直覺了！

---

## Computed 常見技巧 - 搜尋

**每當輸入新的關鍵字時，就會自動去運算比對是否有符合的名稱**

- .filter 篩選過濾 : `var newArray = arr.filter((element) => {...})`

```html
<h3>Computed 常見技巧 - 搜尋</h3>
<input type="search" v-model="search">
<ul>
  <li v-for="item in filterProducts">
    {{ item.name }} / {{ item.price }}
  </li>
</ul>
```

```jsx
const App = {
  data() {
    return {
      search: '',
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
    }
  },
  computed: {
    total() {
      let total = 0
      this.carts.forEach(item => {
        total += item.price
      });
      return total
    },
    filterProducts() {

			// 使用 filter 來篩選每個 item
      return this.products.filter(item => {

			// 可以透過 console 看到，每更新一次 input，就會重新遞迴
        console.log(item)

			// 如果參數(this.search)也就是 input 內的數字
			// 有符合 item.name 的話就渲染出
        return item.name.match(this.search)
      })
    }
  },
  methods: {
    addToCart(product) {
      this.carts.push(product)
    },
  },
};
Vue.createApp(App).mount('#app');
```

---

## 讀取 Getter  & 設值 Setter

- Getter
  - **使用 computed 取出 data 運算後，重新渲染到畫面上**  
- Setter
  - **使用 computed 調用 methods 來重新寫入 data**

**如要使用 Getter or Setter 必須將 computed 改為 物件方式 來撰寫**
**試著改寫原先 computed 為物件形式:**

```jsx
// 原始 computed

computed: {
  total() {
    let total = 0
    this.carts.forEach(item => {
      total += item.price
    });
    return total
  }
},
```

```jsx
// 改寫後 computed

computed: {
  total: {
    get() {
      let total = 0
      this.carts.forEach(item => {
        total += item.price
      });
      return total
    }
  },
```

### 範例 1

**使用 computed 建構 get & set 來讀取以及設值**

- 將商品加入購物車，來運算 total 數值
- 使用更新按鈕來將 total 數值更改為 sum 數值 x 0.8
- 當 sum = 0 , 恢復原始的 total 數值

- Demo :
  - <iframe height="300" style="width: 100%;" scrolling="no" title="Vue3 computed getter &amp; setter" src="https://codepen.io/michael-luo/embed/qBmLRbX?default-tab=html%2Cresult&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/michael-luo/pen/qBmLRbX">
  Vue3 computed getter &amp; setter</a> by Michael Luo (<a href="https://codepen.io/michael-luo">@michael-luo</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

```html
<h3>Computed 將目前的數值運算呈現至畫面上</h3>
  <ul>
    <li v-for="product in products">
      {{ product.name }} / {{ product.price }}
      <button type="button" @click="addToCart(product)">加入購物車</button>
  </li>
  </ul>
  ...
  <h6>購物車項目</h6>
  <ul>
    <li v-for="item in carts">{{ item.name }}</li>
  </ul>
  total 的值 : {{total}} $<br>

  <h3>Computed Getter, Setter</h3>
  sum 的值：
  <input type="number" v-model.number="num">
  <button type="button" @click="total = num">更新</button>
  total 的值：{{ total }}<br>
  sum 的值：{{ sum }}
```

```jsx
const App = {
  data(){
    return {
      num: 10,
      sum: 0,
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
      carts:[],
    }
  },
  computed: {
    total: {
      get(){
        // 讀取
        let total = 0
        this.carts.forEach(item => {
          total += item.price
        })

				// 如果 this.sum 存在時顯示 this.sum
        // 如果為 空值的話就顯示 total
        // 意思為當 sum 為 0 時，就會 return 原始 total 數值
        return this.sum || total
      },
      set(val){
				// 寫入
        this.sum = val * 0.8
      }
    }
  },
  methods: {
    addToCart(product) {
      this.carts.push(product)
    },
  }
}
```

範例 1 可以發現：

- computed 中`get()` 監聽的資料被更動時，就會被觸發 `get()`，來讀取資料
- 觸發更新按鈕 `@click="total = num"` 時，
  - 因為 `total = num` 需要更新數值，所以一定會觸發 `set()`
  - 如需要重新渲染畫面時，會先觸發 寫入`set()` ⇒ 讀取`get()`
- 如不需要重新渲染畫面時，只會觸發 `set()`
---

## 一般情況下 getter 觸發的時間點

在一般的情況下，我們可以這樣使用 computed （只有 getter）來更新資料

```html

<!-- template -->
<div id="computed-basic" v-cloak="v-cloak">
  <h3 class="title-border">一般情況 computed getter 被觸發的時間點</h3>
  <form class="pure-form">
    <input type="text" v-model="firstName"/>
    <input type="text" v-model="lastName"/>
  </form>

  <p>{{fullName}}</p>
</div>
```

```jsx
// js: computed-basic
new Vue({
    el: '#computed-basic',
    data: {
        firstName: 'PJ',
        lastName: 'Chen'
    },
    computed: {
        fullName () {
            console.log('computed getter')
            return this.firstName + ' ' + this.lastName
        }
    },
    updated () {
        console.log('updated')
    }
})
```

在這個情況下，我們只要輸入 input 的內容，改變了 `this.firstName` 或 `this.lastName` 時，就會觸發 `getter()`，

也就是說，computed 的 getter 會觀察被寫在裡面的資料，**一般來說，當被觀察的資料改變時，這個 getter 就會被觸發**。

聽起來非常合理，但是我們用 console.log() 看一下，分別看 computed getter 和 updated 的時間點，

你會發現，當我們在 input 輸入資料，會觸發 computed，同時也會觸發這個 vm 的 updated。

![](https://i.imgur.com/sonZFZC.png)

console 圖

# getter 的例外情況：資料變更但 getter 不會被觸發

剛剛我們提到當 getter 裡面被觀察的資料有變更時，就會觸發 computed，

但這個說其實並不完全正確，有些時候畫面更新了，資料變更了，但其實不會觸發 computed 裡面的 getter。

如果我們把 template 中的 fullName 拿掉，換成 firstName 和 lastName 時（程式碼如下）：

```html
<p> firstName: {{ firstName }}, lastName: {{ lastName }} </p>
```

也就是當我們的 `template` 中沒有馬上用到這個 computed 的資料時（這裡的話就是指 fullName），

那麼 Vue 不知道你要用到 fullName ，因此即使我們變更了 `this.firstName` 和 `this.lastName`，依然不會觸發 getter 。

我們可以在 console 中看到，

firstName 和 lastName 資料變更的情況下，只會一直得到 updated 而已，computed 中的 getter 並不會被觸發。

- Demo:
<iframe height="300" style="width: 100%;" scrolling="no" title="Vue3 computed getter &amp; setter debug01" src="https://codepen.io/michael-luo/embed/yLbGKNL?default-tab=html%2Cresult&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/michael-luo/pen/yLbGKNL">
  Vue3 computed getter &amp; setter debug01</a> by Michael Luo (<a href="https://codepen.io/michael-luo">@michael-luo</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>
---

## 一般情況下 setter 觸發的時間點

從 template 中，我們可以看到，我們的 input 是直接綁 v-model="fullName" ，因此他會直接去修改 fullName 的值，

而當前 fullName 是 computed 中的一個屬性，我們說過 computed 中的屬性就和 data 類似可以取值（getter）和設值（setter），

這時候因為我們要對 fullName 設值，自然就會對應到 fullName 裡面的 setter（**如果沒有設定 setter 是無法對 fullName 設值的**）。

簡單來說，**當 computed 的屬性要被設值時，就會觸發 setter**，

從 console 中我們也可以看到，當我在 input 中輸入內容時，fullName 會改變，fullName 改變的情況會觸發 setter ，

接著，因為我的 setter 中所做的事會變更到 getter 中所觀察的資料，這時候才又觸發 getter 執行，最後重新 updated 畫面。

也就是從 setter ⇒ getter ⇒ updated 

- Demo:
<iframe height="300" style="width: 100%;" scrolling="no" title="Vue3 computed  Setter Debug 02" src="https://codepen.io/michael-luo/embed/dyWwwPw?default-tab=html%2Cresult&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/michael-luo/pen/dyWwwPw">
  Vue3 computed  Setter Debug 02</a> by Michael Luo (<a href="https://codepen.io/michael-luo">@michael-luo</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>
---
## 觸發 setter 不必然會觸發 getter

在上面的例子中，我們會先觸發 setter ， 接著觸發 getter，最後 updated 畫面。

但是其實 getter 會被觸發是因為我們在 setter 中變更到了被 getter 所觀察的資料。

也就是說，如果我們的 setter 在執行時，並不會觸發 getter 所觀察的資料的話，那麼 getter 就不會被觸發。

例如，當我把上面程式碼的 `setter` 中對於資料的變更註解掉時：

```jsx
set (value) {
    console.log('computed setter')
    // this.firstName = value.split(' ')[0]
    // this.lastName = value.split(' ')[1]
}
```

那麼即時我們在 input 中輸入內容，都只會觸發 setter 而不會觸發 getter。

換句話說，setter 和 getter 是獨立觸發的，兩個被觸發的時間點是不同的。

---

## 總結

在這篇文章中，我們進一步瞭解了 Vue computed 中的 getter 和 setter，有幾個重點可以整理一下 :

1. getter 和 setter 彼次觸發的時間點是獨立的。 
    1. getter 在大部分的時候是當內部觀察的資料有改變時會被觸發；setter 則是當被觀察的物件本身有改變時會被觸發。
2. getter 在畫面中沒有使用到被觀察的物件時，不會被觸發。

### 參考文章

[Vue.js: 計算屬性 Computed | Summer。桑莫。夏天](https://cythilya.github.io/2017/04/15/vue-computed/)

[那些關於 Vue 的小細節 - Computed 中 getter 和 setter 觸發的時間點](https://pjchender.blogspot.com/2017/05/vue-computed-getter-setter.html)