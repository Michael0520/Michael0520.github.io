---
title: Vue3 屬性綁定 (v-bind)
date: 2021-07-29
description: v-bind 練習
categories:
- Vue
tags:
- Vue
---
# 綁定屬性 `v-bind`

`v-bind` 來綁定圖片：

- 綁定 imageUrl 來快速更改圖片網址，
- 綁定 title 滑鼠游標移上去時會出現圖片名稱

範例程式碼：

```html
<img
  v-bind:src="breakfastShop.imgUrl"
  v-bind:title="breakfastShop.name"
  class="square-img"
  alt=""
/>
```

```jsx
const App = {
  data() {
    return {
      breakfastShop: {
        name: "奇蹟早餐",
        imgUrl:
          "https://images.unsplash.com/photo-1600182610361-4b4d664e07b9?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=200&q=80"
			}
		}
	}
}
```

## 縮寫 `:`

將上方程式碼改為縮寫：

```html
<img
  :src="breakfastShop.imgUrl"
  :title="breakfastShop.name"
  class="square-img"
  alt=""
/>
```

## 更多屬性綁定

使用表單來透過 `v-bind` 綁定 disabled 屬性，透過 button 切換資料狀態，來關閉 submit 按鈕

```html
<form action="">
  <input type="text" value="我要吃蘿蔔糕" />
  <button type="submit" :disabled="isFull">送出</button>
</form>

<button type="button" v-on:click="change('isFull')">
  狀態切換
</button>
```

```jsx
const App = {
  data() {
    return {
			isFull: false,
		}
	}
}
```

![成功切換 disabled 狀態 預覽圖](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e3598ced-29de-47f4-8618-8dd0f8040c28/CleanShot_2021-07-12_at_01.29.41.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211104T115917Z&X-Amz-Expires=86400&X-Amz-Signature=73af609f46cbbe1d4d201de2f0e58eadd66795831775d0556c2a7747b7504257&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22CleanShot_2021-07-12_at_01.29.41.gif%22)

成功切換 disabled 狀態 預覽圖

## 搭配 `v-for`

先使用 `v-for` 渲染多組資料，每組資料會有：

- 圖片
- 商品名稱
- 商品價格
- 我要這個 (checkbox)

範例程式碼：

```html
<table class="table">
  <tbody>
		<!-- v-bind:key 綁定 item.imgUrl 確保不會有重複資料渲染情形發生-->
    <tr v-for="item in products" :key="item.imgUrl">
      <td>
				<!-- v-bind:src 綁定 item.imgUrl 確保不會有重複資料渲染情形發生-->
        <img class="square-img" 
						 :src="item.imgUrl"
						 alt="" />
      </td>
      <td>{{ item.name }}</td>
      <td>{{ item.price }}元</td>
      <td>
        <div class="form-check">
          <input
            class="form-check-input"
            type="checkbox"
            value=""
            id="aa"
          />
          <label class="form-check-label" for="aa">
            我要這個
          </label>
        </div>
      </td>
    </tr>
  </tbody>
</table>
```

```jsx
const App = {
  data() {
    return {
      name: "小明",
      isFull: false,
      link: "小明",
      imageSize: 200,
      dynamic: "disabled",
      products: [
        {
          name: "蛋餅",
          price: 30,
          vegan: false,
          imgUrl:
            "https://images.unsplash.com/photo-1607278967323-8766a3a501e6?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=200&q=80",
        },
        {
          name: "飯糰",
          price: 35,
          vegan: false,
          imgUrl:
            "https://images.unsplash.com/photo-1603245460565-5a7b42a6a6f4?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=200&q=80",
        },
        {
          name: "小籠包",
          price: 60,
          vegan: false,
          imgUrl:
            "https://images.unsplash.com/photo-1595424265370-3e02d3e6c10c?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=200&q=80",
        },
      ],
}
```

## BUG 處理

目前資料都渲染得很成功，但發現了點選 checkbox “我要這個”時，

一直都只有第一欄位被圈選到，

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b8c26c6b-a780-4849-92de-9d8a3af0e608/CleanShot_2021-07-12_at_02.07.19.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211104T115934Z&X-Amz-Expires=86400&X-Amz-Signature=3cad23de0453e69150e774f49d709e53d9198ba4d997bad3e96c80b1a12b9f34&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22CleanShot_2021-07-12_at_02.07.19.gif%22)

### 解決方法

問題出在： `<input>` 以及 `<label>` 綁定的 id 皆為 "aa" ,

當 id 重複時，`label for=""` 就只會對應到第一個 `<input>` ，

所以需要為每一個 `<input>` 綁定一個獨有的 id 

我們可以使用 商品名稱或是圖片連結都可以，這裡我們使用圖片連結來綁定獨有的 id，

確保每一個 label 被點選時，都會對應到特定的 input ，來確保 checkbox 被正確勾選

```html
<input
  class="form-check-input"
  type="checkbox"
  value=""
  :id="item.imgUrl"
/>
<label class="form-check-label" :for="item.imgUrl">
  我要這個
</label>
```

---

## 表達式運用 （串接）

透過表達式，來串接 img URL ，並且變更 URL 之中的資料，

兩行的 img link 差別在於 `resizeImg` 少了 width:200px ，

使用 data 中的 `imageSize` 串接在 URL 當中

範例程式碼：

```html
<!-- 此 input 為一個 scroll bar 可以控制裡頭所綁定的資料做變化-->
<input type="range" min="100" max="1000" v-model="imageSize" />

<br />
<!--  在此 URL 後方加上 data 中的 imageSize 資料 -->
<img :src="`${breakfastShop.resizeImg}&w=${imageSize}`" alt="" />
```

```jsx
// 兩行的 img link 差別在於 resize 少了 width:200px

const App = {
  data() {
    return {
      imageSize: 200,
      breakfastShop: {
        name: "奇蹟早餐",
        imgUrl:
          "https://images.unsplash.com/photo-1600182610361-4b4d664e07b9?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=200&q=80",
        resizeImg:
          "https://images.unsplash.com/photo-1600182610361-4b4d664e07b9?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&q=80",
      }
		}
	}
}
```

## 動態屬性綁定 `:[data]`( 注意大小寫 )

`v-bind` 動態綁定數值語法： `:[data]`

1. 使用 button 觸發事件來切換狀態，且加入三元運算子，讓狀態可以更靈活顯示
2. 將 `<input>` 標籤 `:[data]` 動態綁定上要呈現的屬性

此範例的狀態分為兩種

- `readonly` : input 內的資料只可以看，不能選擇，不能編輯
- `disabled` : input 內的資料只可以看，可以選擇，不能編輯

範例程式碼：

```html
<button
  type="button"
  v-on:click="dynamic = dynamic === 'disabled' ? 'readonly':'disabled'"
>
  切換為 {{ dynamic }}
</button>
<br />
<input type="text" :[dynamic] :value="name" />
```

```jsx
const App = {
  data() {
    return {
      dynamic: "disabled",
		}
	}
}
```

![成功預覽圖](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7e9f0ce3-f664-4887-9b6b-af41363e2892/CleanShot_2021-07-12_at_04.34.50.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211104T120006Z&X-Amz-Expires=86400&X-Amz-Signature=8a02789ef28e2dc1387cc158dd195d21de654587361a4fe1568b6b7e4fc48a80&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22CleanShot_2021-07-12_at_04.34.50.gif%22)

成功預覽圖
