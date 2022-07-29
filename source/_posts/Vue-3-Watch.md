---
title: (Vue) Watch
date: 2021-08-09
description: watch 監聽器，用以監聽某個數據，並觸發相對應的處理。
categories:
- Vue
tags:
- Vue
---
## **認識 watch 監聽器**

watch 監聽器，用以監聽某個數據，並觸發相對應的處理。

![image](https://i.imgur.com/R5QkfCE.png)

在 watch 物件底下，我們可以使用鍵值(key-value)的方式定義我們想要觀察的值，及相對應的操作。

接著我們從 key，也就是我們想觀察的值說起。

## **Key (欲觀察的值)**

### **觀察 data 中的值**

![image](https://i.imgur.com/vWxmbay.png)


### **觀察 data 中的 Object 底下的值**

- 切記得使用引號包裹，使之為字串。
- 此用法情境表示只想觀察監聽 Object 底下的特定值。
  - 如果要監聽整個 Object 也可以，只是會有額外的事情需要處理，我們留到待會的 Value 設定中再提。

![image](https://i.imgur.com/RtSoQMW.png)

### **觀察 computed 計算後的回傳值**

如果想觀察的值，是需要經過某些特定規則運算後的結果，配合 computed，監聽回傳值也可以。

![image](https://i.imgur.com/QVI55xu.png)

## **value (想做的事情，及一些可選設定)**

### **基本用法**

如果你不需要任何其他設定，那麼直接在 value 的部分寫入 Function 即可。

其中 function 有兩個參數值，分別為改變後的值，及改變前的值。

![image](https://i.imgur.com/VRV5h8x.png)

如果想要額外管理或是複用 function，可以把 function 寫進 methods 管理。

![image](https://i.imgur.com/DTxHOd3.png)

上述的 Function，官網文件皆建議不要使用 Arrow function 來撰寫，

因為 Arrow function 的 this，是在 function 被呼叫時綁定的，可能不會按照期望的指向 Vue 實例。

---

#### 範例 1

即時驗證帳號格式，條件為 3~15 個字，只能使用小寫英文、數字、底線。

![image](https://i.imgur.com/DiXGgpI.png)

---

#### 範例2

使用 watch 來判定輸入字串的長度到達目標時，做出一些事情

1. if 判斷：判斷當字串數量大於等於 10 時， 會將輸入的數值儲存在 `this.name`
    - 小於 10 的話，`this.result` 會持續回傳錯誤提示內容，以及 oldValue 給使用者

```html
<h3>watch 監聽單一變數</h3>
<label for="name">名字須超過十個字</label>
<input type="text" id="name" v-model="tempName">
<div style="color: red; padding-top: 1rem;">

  <p>result: {{ result }}</p>
  <p>name: {{ name }}</p>
</div>
```

```jsx
data (){
  return {
    name: '',
    tempName: '',
    result: '',
  },
  watch: {
    tempName(newValue, oldValue){
      console.log(`new value: ${newValue}, old value: ${oldValue} `)
        if (newValue.length >= 10) {
        this.result = `文字長度為 ${newValue.length} 個字，將儲存在變數中`
        this.name = newValue
      } else {
        this.result = `輸入的文字長度僅有 ${newValue.length} 個字，上一次有 ${newValue.length}個字`
      }
    }
  },

}
```

---

1. 使用 computed 來監聽資料變動，回傳新數值

input 分別綁定資料內的 “商品名稱” 、“商品價格”、“商品素食狀態”，

透過 computed 來針對輸入的數值，回傳訊息

```html
<label for="productName">商品名稱</label><input type="text" v-model="productName"><br>
<label for="productPrice">商品價格</label><input type="number" v-model.number="productPrice"><br>
<label><input type="checkbox" v-model="productVegan"> 素食</label>

<p style="color: red;">Computed result2: {{ result2 }}</p>
```

```jsx
data (){
  return {
    productName: '蛋餅',
    productPrice: 30,
    productVegan: false,
    result2: '',
  },
  computed: {
    result2() {
      return `媽媽買了 ${this.productName}，總共花費 ${this.productPrice} 元，另外這 ${this.productVegan?
        '是' : '不是'}
        素食的`
    }
  },
}
```

1. 使用 Watch 改寫
    1. 因為 Watch 一次只能產生一個數值，而這裡必須監聽 “商品名稱”、“商品價格”、“商品素食狀態”
    2. 所以這裡必須監聽多個數值，來產生多組數值，最後回傳到結果上

```jsx
watch: {
  productName() {
    this.result3 = `媽媽買了 ${this.productName}，總共花費 ${this.productPrice} 元，另外這 ${this.productVegan?
      '是' : '不是'}
      素食的`
  },
  productPrice() {
    this.result3 = `媽媽買了 ${this.productName}，總共花費 ${this.productPrice} 元，另外這 ${this.productVegan?
      '是' : '不是'}
      素食的`
  },
  productVegan() {
    this.result3 = `媽媽買了 ${this.productName}，總共花費 ${this.productPrice} 元，另外這 ${this.productVegan?
      '是' : '不是'}
      素食的`
  },
},
```

可以從範例觀察到，第一次渲染畫面時，不會觸發 watch ，因為裡頭沒有任何數值，也就是沒有被更動過，所以不會被觸發。

## 深層監聽

前提要為一個物件，可選設定包含 `deep`、`immediate`。

- **handler：**放入我們需要處理的程序。
- **deep：**當欲觀察值的特性為 call by reference。
  - 例如 Object 時，需將 deep 值設定為 true，告知 watch 需要深度觀察。
  - 否則會因為特性關係，無法觸發監聽器。
- **immediate：**監聽器預設為當值有所變化時才會觸發。
  - 如果我們希望在初始化完成後，就先觸發，執行 handler，就可以將 immediate 值設為 true。

<aside>
💡 如果想要加上可選設定，需把 value 改寫為物件形式，用以傳入其他值。

</aside>

如下圖：

![image](https://i.imgur.com/Nw4ka7a.png)

### 範例1

如果需要一次監聽多組數值，來回傳，就需要用到深層監聽 deep，
當其中一個數值被改變時，就會回傳資料

```jsx
watch: {
  product: {
    handler(newValue, oldValue) {
      console.log('newValue: ', newValue, 'oldValue: ', oldValue);
      this.result4 = `媽媽買了 ${this.product.name}，總共花費 ${this.product.price} 元，另外這 ${this.product.vegan? '是 true' : '不是 false'} 素食的`
    },
     deep:true
  },
},
```

<iframe height="300" style="width: 100%;" scrolling="no" title="Watch 監聽 deep" src="https://codepen.io/michael-luo/embed/MWmxYOo?default-tab=html%2Cresult&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/michael-luo/pen/MWmxYOo">
  Watch 監聽 deep</a> by Michael Luo (<a href="https://codepen.io/michael-luo">@michael-luo</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

範例會發現如果使用深層監聽屬性 deep ，不會回傳給你舊的數值，只會回傳給你新的數值

## 總結

### **Watch（監聽特定數值變化，來執行複雜運算）**

- 監聽單一 “變數” 觸發事件
- 該函式可同時操作多個變數

### **Computed（多組監聽資料，產生一組結果）**

- 監聽多個變數觸發事件
- 會產生一個值
