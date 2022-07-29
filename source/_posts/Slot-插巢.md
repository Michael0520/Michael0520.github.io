---
title: (Vue) Slot 插巢
date: 2021-08-17
description: Slot 是一種用於內容分配（Content Distribution / Transclusion）的元件，適用於複雜或巢狀元件的實作上，可以想像成是空間預留的方法，在迭代過程中再把內容塞進去。
categories:
- Vue
tags:
- Vue
---
Slot 是一種用於內容分配（Content Distribution / Transclusion）的元件，適用於複雜或巢狀元件的實作上，可以想像成是空間預留的方法，在迭代過程中再把內容塞進去。

![image](https://i.imgur.com/tXlQYNy.png)

slot 操作簡介圖

## 新增插槽並設定插槽內容

- 在 template 內新增 slot 標籤，
- 接下來在外層 html 內新增上全新的標籤，即可顯示

    ```html
    <h3>Slot 插巢與插巢預設值</h3>
    <card>
      <p>這是由外層定義得資料...</p>
    </card>
    
    <card>
      <p>預設值</p>
    </card>
    ```

    ```jsx
    const app = Vue.createApp({
      });
      app.component('card', {
        template: `<div class="card" style="width: 18rem;">
          <div class="card-header">
            元件 Header
          </div>
          <div class="card-body">
            <slot>
              <p>這是預設值</p>
            </slot>
          </div>
          <div class="card-footer">
            元件 Footer
          </div>
        </div>`
      })
    
      app.mount('#app');
    ```

![插巢賦予值流程圖](https://i.imgur.com/iYNefpl.png)


## 插槽預設值

直接在 `<slot>` 標籤內寫定預設內容，如果模組標籤內沒有任何內容，那麼該 component 的畫面顯示就是該預設內容。


![預設值賦予值流程](https://i.imgur.com/I9KilXP.png)

## 新增多個插巢

html 上必須使用 template 來指向內部的 slot 插巢，加上 `v-slot` 來指向指定的插巢名稱，內層賦予屬性 name ，且標註外層標籤來對應指定的 slot插巢

```html=
<h3>具名插巢</h3>
<card2>
  <template v-slot:header>我喜歡這張卡片</template>
  <!--  預設請加入 default  -->
  <template v-slot:default></template>
  <template v-slot:footer>這是卡片腳</template>
</card2>
```

```html=
app.component('card2', {
    template: `<div class="card" style="width: 18rem;">
      <div class="card-header">
        <slot name="header">元件 Header</slot>
      </div>
      <div class="card-body">
        <slot name="default">這段是預設的文字</slot>
      </div>
      <div class="card-footer">
        <slot name="footer">元件 Footer</slot>
      </div>
    </div>`
  });
```

<aside>
💡 如一開始就是要使用預設文字，可以將 v-slot 指向為 default

</aside>

<iframe height="300" style="width: 100%;" scrolling="no" title="Vue 3 Slot 插巢" src="https://codepen.io/michael-luo/embed/GRERxLR?default-tab=html%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/michael-luo/pen/GRERxLR">
  Vue 3 Slot 插巢</a> by Michael Luo (<a href="https://codepen.io/michael-luo">@michael-luo</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

## Slot Props 插巢傳遞資料狀態

**將元件內部的變數取出使用，稱為 slot prop**

可以先使用 `v-slot:default` 來驗證是否資料有被正確綁定，確認正確綁定後再去嘗試資料傳遞

```html
<card>
  <template #default>
    我想取出元件的值來使用
  </template>
</card>
```

## 取出元件內的資料

將 data 內的 product 資料渲染出

- 先將內部元件定義 `v-slot:product="product"`
- 由外部元件來定義是否要顯示
- 將外部元件新增指令且指向變數 `v-slot:default="slotProps"`
- 在外部內容使用花括弧來綁定資料 `{{slotProps}}`
  - 因為 product 是一個 object ，所以會以 object 形式來做顯示
    ![預覽圖](https://i.imgur.com/H4eritU.png)

```html
<card>
  <template #default="slotProps">
    我想取出元件的值來使用
    {{slotProps}}
  </template>
</card>
```

```jsx
const app = Vue.createApp({
    data() {
      return {
        product: {
          name: '蛋餅',
          price: 30,
          vegan: false
        }
      }
    },
  });

app.component('card', {
    data() {
      return {
        product: {
          name: '蛋餅',
          price: 30,
          vegan: false
        },
      }
    },
    template: `<div class="card" style="width: 18rem;">
      <div class="card-body" >
        <slot :product="product"></slot>
      </div>
    </div>`
  });

app.mount('#app');
```

## 解構＆判斷多資料狀態

- 外層元件
  - 定義資料

```jsx
const app = Vue.createApp({
    data() {
      return {
        product: {
          name: '蛋餅',
          price: 30,
          vegan: false
        }
      }
    },
  });
```

- 在內層元件
  - 新增 props 指向 外層資料 product
  - 新增資料 `veganName : ''`
  - 新增 created() ，當元件被創建時執行
    `this.veganName = this.product.vegan ? '素食' : '非素食';`
    判斷外層資料是否為素食
    - template 加入 slot 綁定兩個資料 product , veganName
- html 上使用 `#default="{product,veganName}` 來渲染資料

<iframe height="300" style="width: 100%;" scrolling="no" title="Slot Props 插巢傳遞資料狀態" src="https://codepen.io/michael-luo/embed/RwgNGvR?default-tab=html%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/michael-luo/pen/RwgNGvR">
  Slot Props 插巢傳遞資料狀態</a> by Michael Luo (<a href="https://codepen.io/michael-luo">@michael-luo</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>
