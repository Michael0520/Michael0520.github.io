---
title: Vue3 HTML 樣式綁定
date: 2021-07-30
description: 樣式綁定練習
categories:
- Vue
tags:
- Vue
---
# 樣式切換 & 切換 Class

## 物件寫法 1

- key 值是對應 ⇒ className ，物件的值是對應 ⇒ 判斷式
- 遇到 className 有包含 dash(-) 或是 下底線( _ ) 需要額外匡起來成字串

使用兩個 button `v-on:click` 來觸發事件，更改資料狀態，

外層 `<div>` 會根據 `v-bind:class` 物件內的判斷式來加上特定 className，


![](https://i.imgur.com/R5e2QB0.png)
觸發事件，改變資料狀態的流程圖

範例程式碼：

```html
<div class="box" 
		:class="{ rotate : isTransform ,'bg-danger' : boxColor }"></div>

<hr>
<button class="btn btn-outline-primary" 
        v-on:click="change('isTransform')">選轉物件</button>

<button class="btn btn-outline-primary ms-1" 
			  v-on:click="change('boxColor')">切換色彩</button>
```

```jsx
const App = {
  data() {
    return {
      isTransform: true,
      boxColor: false,
    };
  },
  methods: {

// 根據 key 值，去判定 true ,false 加上特定樣式
    change: function (key) {
      this[key] = !this[key];
    }
  }
};
```

![成功後預覽圖](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/35f925a7-f65f-4dbb-8740-bbd46c4ca1d9/CleanShot_2021-07-12_at_13.32.05.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211104T111440Z&X-Amz-Expires=86400&X-Amz-Signature=f1ee96e55090bfcabd90258dc44b9625e9e639a0dcb2aae11244301cb86d90c3&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22CleanShot_2021-07-12_at_13.32.05.gif%22)

成功後預覽圖

## 物件寫法 2

將多組資料狀態，使用 object 來包裹，透過 `v-bind` 來綁定

這裡我們將 `rotate: true,'bg-danger': true` ，

key 值都寫為 true ，那這兩種特定樣式都會加入到綁定區塊上做渲染

範例程式碼：

```html
<h3>物件寫法 2</h5>
  <div class="box" v-bind:class="objectClass"></div>
```

```jsx
const App = {
  data() {
    return {
      isTransform: true,
      boxColor: false,
      objectClass:{
        rotate: true,
        'bg-danger': true,
      },
		}
	}
}
```

## 陣列寫法

`'disabled'` 意思為不可點選的 class 樣式

- 使用陣列來包裹多個 class 樣式
- 建立空陣列，建立 methods 將參數設為 className ，
    
    透過 `v-on:click` 來加入空陣列
    

範例程式碼：

```html
<h4>陣列寫法</h4>
<button class="btn" v-bind:class="['btn-primary','disabled']" >請操作本元件</button>
<button class="btn" v-bind:class="arrayClass" >請操作本元件</button>
<button type="button"
  class="btn btn-outline-primary"
  v-on:click="addClass(['btn-primary', 'disabled'])">為陣列加入 Class</button>
```

```jsx
const App = {
  data() {
    return {
			arrayClass: [],
		}
	},
	methods: {

// 展開 arrayClass 空陣列，新增上 addClass 的 props，組裝成新陣列匯入
    addClass(arr) {
      this.arrayClass.push(...arr);
    }
  },
}
```

![成功預覽圖](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/aa3095df-0371-4b9d-b9aa-10b4ad5700fc/CleanShot_2021-07-12_at_13.59.13.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211104T115815Z&X-Amz-Expires=86400&X-Amz-Signature=a643c418701ef974a46f70d04d75dc3e25587431f5092f29f74ca3c8ab103f26&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22CleanShot_2021-07-12_at_13.59.13.gif%22)

成功預覽圖

## 行內樣式寫法 `:style`

- 單樣式： `v-bind:style="{'key':'className'}"`
    - 如遇到有 key 有 dash(-) ，可以使用小駝峰來撰寫
- 單組元件屬性 object： `v-bind:style="object"`
- 多組元件屬性 object ：`v-bind:style="[object,object,object]"`

```html
<h2>行內樣式</h2>

<h4>綁定行內樣式</h4>

<!-- key 會帶入 style 的屬性 -->
<!-- 值 會帶入 style 相對應的值 -->

<!-- 小駝峰(background-color) => backgroundColor -->
<div class="box" v-bind:style="{'backgroundColor':'red'}" ></div>

<div class="box" v-bind:style="styleObject" ></div>
<div class="box" v-bind:style="[styleObject,styleObject2,styleObject3]" ></div>
```

```jsx
const App = {
  data() {
    return {

      // 行內樣式
      // 使用駝峰式命名
      styleObject: {
        backgroundColor: 'red',
        borderWidth: '5px'
      },
      styleObject2: {
        boxShadow: '10px 10px 10px rgba(0, 0, 0, 0.16)'
      },
      styleObject3: {
        userSelect: 'none'
      }
    };
  },
}
```