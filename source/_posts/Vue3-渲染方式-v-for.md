---
title: Vue3 渲染方式 (v-for)
date: 2021-07-27
categories:
- Vue
tags:
- Vue
---
## 渲染資料

使用各種指令，將 data 內的資料渲染到 html 裏

```javascript
// 範例 Data

const App = {
    data(){
        return {
            name: "Michael",
            position: "電影院",
            text: "Michael 在電影院看電影",
            rawHtml: "<p>Michael 在電影院看電影</p>",
            products: [
                {
                    name: "玩命關頭9",
                    price: 30,
                    adult: false,
                },
                {
                    name: "咒術迴戰電影版",
                    price: 35,
                    adult: false,
                },
                {
                    name: "黑寡婦",
                    price: 60,
                    adult: false,
                },
                {
                    name: "上流世界",
                    price: 30, 
                    adult: true,
                },
            ],
            productsObj: {
                theFastSaga9: {
                    name: "玩命關頭9",
                    price: 30,
                    adult: false,
                },
                animeMovie: {
                    name: "咒術迴戰電影版",
                    price: 35,
                    adult: false,
                },
                blackWidow: {
                    name: "黑寡婦",
                    price: 60,
                    adult: false,
                },
                mine: {
                    name: "上流世界",
                    price: 30,
                    adult: true,
                },
            },
        };
    },
    methods:{
        say(name) {
            return `${name}在${this.position}看電影`;
        },
    }
}
```

## `v-for`

## 陣列操作

因為 data 中，總共有四個 item ，所以他會渲染四次

```html
<ul>
    <li v-for="(item, index) in products">
        索引值 - 電影名稱 // 電影價格
    </li>
</ul>

<!-- 索引值 - 電影名稱 // 電影價格  --> 
```

使用 `{{}}` 帶入 data 裡頭的資料，以及使用上 index 參數，

但程式語言 0 為第一個數字，所以我們將 `index+1` 就可以正確呈現出 1,2,3,4 了

```html
<ul>
    <li v-for="(item, index) in products">
        {{index + 1 }} - {{item.name}} // {{item.price}}$
    </li>
</ul>
<!--   
1 - 玩命關頭9 // 30$
2 - 咒術迴戰電影版 // 35$
3 - 黑寡婦 // 60$
4 - 上流世界 // 30$
-->

```

## 物件操作

- item:  `theFastSaga9: {name: "玩命關頭9", price: 30, adult: false}`
- key: `productsObj` 裡頭的 `theFastSaga9 , animeMovie ,blackWidow`

```html
<ul>
    <li v-for="(item, index) in productsObj" :key="index">
        {{index }} - {{item.name}} // {{item.price}}$
    </li>
</ul>

<!--   
theFastSaga9 - 玩命關頭9 // 30$
animeMovie - 咒術迴戰電影版 // 35$
blackWidow - 黑寡婦 // 60$
mine - 上流世界 // 30$
-->
```

## 純數值操作

`in 5 (in list)` , 會依照 list 所給定的數值，去做渲染幾次

```javascript
<ul>
    <li v-for="i in 5">{{ i }}</li>
</ul>
```

## `v-for` 與 `key` 的對應

透過 `btn.click.method()` 反轉資料來驗證

1. 將 input 輸入數值，改變資料內容
2. 在使用事件觸發來反轉資料
3. 會發現改變的資料內容，沒有成功被轉換過去

是因為系統判定，這只是反轉資料，沒有改變資料內容，所以沒有重新做渲染

（錯誤）範例程式碼範例：

```html
// 錯誤範例程式碼

<ul>
    <li v-for="(item, key) in products">
        {{ key }} - {{ item.name}} / {{ item.price }} 元
        <input type="text" />
    </li>
</ul>

<button type="button" v-on:click="reverseArray">
    反轉資料內容
</button>

<script>
methods: {
    reverseArray: function () {
        this.products.reverse();
    },
}
</script>
```

![錯誤程式碼 BUG 發生圖](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/21e8f409-63e4-454c-8ab9-3cb26e87aaf1/CleanShot_2021-07-10_at_22.30.06.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211104T120550Z&X-Amz-Expires=86400&X-Amz-Signature=3b292e36f76086f8ea53b12eee4c7e11cee425cea9ebb399218ee87fa1638636&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22CleanShot_2021-07-10_at_22.30.06.gif%22)

錯誤程式碼 BUG 發生圖

## `v-bind` 綁定 key

為了確保資料有無變動，所有資料都會重複做渲染，所以要加上 key值 ( 唯一數值 )，

此範例可以尋找到 `products[]` 裡頭的 name ，就是唯一值，

有了 name，資料就不會重複渲染到，類似於 id，只會存在一個，

使用 `v-bind:key` 可省略為 (`:key`) 來綁定 `item.name`

 `v-for` 基本上都會與 `:key` 同時存在，確保程式碼不會出錯

（正確）範例程式碼範例：

![資料正確的透過反轉，而去變更位子](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/403559b6-cc2e-4c4a-9b6b-776599c58530/CleanShot_2021-07-10_at_22.32.44.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211104T120601Z&X-Amz-Expires=86400&X-Amz-Signature=cd7191d257b64aefa59041fa07f1609aba6a74a7f80f4ded6c4da82afc21da9d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22CleanShot_2021-07-10_at_22.32.44.gif%22)

資料正確的透過反轉，而去變更位子

```html
// 正確範例程式碼

<ul>
    <li v-for="(item, key) in products"
        v-bind:key="item.name">
        {{ key }} - {{ item.name}} / {{ item.price }} 元
        <input type="text" />
    </li>
</ul>
<button type="button" v-on:click="reverseArray">
    反轉資料內容
</button>

<script>
methods: {
    reverseArray: function () {
        this.products.reverse();
    },
}
</script>
```

💡 有相同父元素的子元素必須有獨特的 key。重複的 key 會造成渲染錯誤。

## 在 `<template>` 標籤使用 v-for

有些 html 標籤，會必須搭配多個節點去呈現資料，例如 : 表單元素 `<table>`

v-for 一次只能渲染一個節點，所以會造成資料沒有統一事情

錯誤範例程式碼：

1. 第一個`<tr>` : 顯示 第幾部電影 (index) 、 電影名稱 (item.name)
2. 第二個`<tr>` : 顯示 電影價格 (item.price)、電影是否限制級 (item.adult)

```html
<table class="table">
    <tbody>

    <!-- 表單中屬於不同節點  -->
        <tr>
            <th rowspan="2">1</th>
                <td colspan="2">玩命關頭9</td>
        </tr>

    <!-- 表單中屬於不同節點  -->
        <tr>
                <td>30$</td>
                <td>限制級</td>
        </tr>

    </tbody>
</table>
```

![image](https://i.imgur.com/sJhdMaT.png)
錯誤範例圖

### 確保資料統一更新

為了讓資料可以統一更新在多個節點 `<tr>` ，

使用 `<template>` 去包裹，多個節點 `<tr>` 來同時更新且渲染資料

正確範例程式碼：

```html
<table class="table">
    <tbody>

        <!-- 表單中屬於不同節點  -->
        <template v-for="(item, index) in products" :key="item.name">
            <tr>
                <th rowspan="2">{{index+1}}</th>
                    <td colspan="2">{{item.name}}</td>
            </tr>

            <!-- 表單中屬於不同節點  -->
            <tr>
                <td>{{item.price}}$</td>
                <td>{{item.adult}}</td>
             </tr>
        </template>

    </tbody>
</table>
```

![image](https://i.imgur.com/ioPjOgH.png)
正確範例程式碼

## BUG 發生

🚫 發現 `{{item.adult}}` 只能顯示 true or false ，非常不直覺化

### 條件 (三元) 運算子

為了讓程式碼可以更彈性的渲染，可以使用三元運算子，來判斷顯示任何字串

```jsx
   condition ? exprIfTrue : exprIfFalse
```

- `condition`
    值用來做為條件的表達式

- `exprIfTrue`
    如果 `condition` 的值是 [truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) (等於或是可轉換為 `true`) , `exprIfTrue`  會被執行

- `exprIfFalse`

    如果 `condition` 的值是 [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) (等於或是可轉換為 false) , `exprIfFalse`  會被執行

此範例我們來顯示，如果`{{item.adult}}` :

- 為 true 的話，就顯示 '限制級'
- 為 false 的話，就顯示 '非限制級'

正確範例程式碼：

```html
<table class="table">
    <tbody>

        <!-- 表單中屬於不同節點  -->
        <template v-for="(item, index) in products" :key="item.name">
            <tr>
                <th rowspan="2">{{index+1}}</th>
                   <td colspan="2">{{item.name}}</td>
            </tr>

    <!-- 表單中屬於不同節點  -->
            <tr>
                <td>{{item.price}}$</td>
                <td>{{ item.adult ? '限制級' : '非限制級'}}</td>
            </tr>
        </template>

    </tbody>
</table>
```

![image](https://i.imgur.com/vyQ0Xgo.png)
正確範例圖
