---
title: (Vue) 事件觸發 v-on
date: 2021-08-01
description: 事件觸發練習
categories:
- Vue
tags:
- Vue
---
## 觸發事件與縮寫

 可以將 `<v-on:click>` 改寫為使用縮寫符號為 `<@click>`

使用按鈕觸發事件將 box 改變資料狀態，box 綁定判斷特定樣式動態加上

- 將按鈕新增`<v-on:click>`觸發事件來更動資料狀態
- 加上 `:class` 去判斷是否增加特定樣式

範例程式碼：

```html
<div class="box" :class="{ rotate: isTransform }"></div>
<hr />
<button class="btn btn-outline-primary" @click="changeClass">
  選轉物件
</button>
```

```jsx
const App = {
  data() {
    return {
      isTransform: true,
    };
  },
  methods: {
    changeClass() {
      this.isTransform = !this.isTransform;
    },
  }
}
```

## 帶入參數

- 點選按鈕觸發事件，`@click` 事件有內部資料
- 將 `@click` 內部資料傳送給 `methods.change(key)` ，讓 key 值存取
- 最後執行 `methods.change()` 裡頭的事件

範例程式碼：

```html
<div class="box" :class="{ rotate: isTransform }"></div>
<hr />
<button class="btn btn-outline-primary" @click="change('isTransform')">
  選轉物件
</button>
```

```jsx
const App = {
  data() {
    return {
      isTransform: true,
    };
  },
  methods: {
    change(key) {
      this[key] = !this[key];
    },
  }
}
```

![image](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/209af3f8-161a-4133-8cf3-c22523449c14/CleanShot_2021-07-14_at_06.14.24.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211104T104426Z&X-Amz-Expires=86400&X-Amz-Signature=b96d355ae56884586987ffc566425ec32af165cc3a419320e0d8b2105dece270&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22CleanShot_2021-07-14_at_06.14.24.gif%22)

不同方法，相同執行效果範例圖

<aside>
💡 兩個方法效果相同，可以依照需求來使用動態或是靜態來改變資料狀態

</aside>

## 原生 DOM 事件

`<v-on>` 可以搭配原生 JS 所擁有的事件來做觸發

- 使用 `<v-on:change>` 搭配 `<input>` 來更新資料內容
  - `@change` 離開 focus 狀態時，才會觸發事件
- 使用 `<v-on:sumbit>` 搭配 `<input>` 來傳送資料內容
  - `prevent` : 將原生 html 預設的 form submit 時會重新整理頁面的效果給蓋掉

<aside>
💡 <v-on:sumbit> ：寫在外層 form 表單上，
輸入完資料可以使用 enter 來快速送出表單，可以不一定要寫在 button 上

</aside>

範例程式碼：

```html
<h4>input change 事件</h4>
<input type="text" @change="onChange" />

<h4>form submit 事件</h4>
<form @submit.prevent="submitForm">
  <input type="text" v-model="name" />
  <button>送出表單</button>
</form>
```

```jsx
const App = {
  data() {
    return {
      name: "小明",
    };
  },
  methods: {
    onChange(evt) {
      alert(evt.target.value);
    },
    submitForm() {
      console.log("表單已送出", `name 為 ${this.name}`);
    },
  }
}
```

## 動態事件

`@[event]="methods"` 類似組裝事件的方法，拆分為：

- 觸發方式
- 事件名稱

將事件使用 `[ event ]` 放入，對應到 `data.methods.event` ，來執行觸發事件

範例程式碼：

```html
<h3>動態事件 []</h3>

<!-- 可省略此行，為了好觀看而添加上  -->
<input type="text" v-model="event" />

<input type="text" @[event]="dynamicEvent" />
```

```jsx
const App = {
  data() {
    return {
      event: "click",
    };
  },
  methods: {
    dynamicEvent() {
      console.log("這是一個動態事件", this.event);
    },
  }
}
```

## 動態物件方法

`@="{自定義名稱: key, 自定義名稱: key}"` 類似於組裝物件的方法，拆分為：

- `@` (v-on)
- {自定義事件名稱 : key}  key 值 會對應到 `data.methods`

<aside>
💡 此方法無法傳入參數 ！！

</aside>

範例程式碼：

```html
<h3>動態物件方法 {}</h3>
<button class="box" @="{mousedown:down,mouseup:up}"></button>
```

```jsx
const App = {
  data() {
    return {
    };
  },
  methods: {
    down() {
      console.log("按下");
    },
    up() {
      console.log("放開");
    },
  }
}
```

## v-on 修飾符

### 按鍵修飾符

### 別名修飾

- 別名修飾 - .enter, .tab, .delete, .esc, .space, .up, .down, .left, .right

使用 `@keyup.enter` 來增加修飾，代表只有透過 enter 按鍵，才會觸發 `<v-on>` 

範例程式碼：

```html
<h6 class="mt-3">別名修飾</h6>
<input
  type="text"
  class="form-control"
  v-model="text"
  @keyup.enter="trigger('enter')"
/>
```

```jsx
const App = {
  data() {
    return {
    };
  },
  methods: {
    trigger: function (name) {
      console.log(name, "此事件被觸發了");
    },
  },
};
```

### 相應按鍵時才觸發的監聽器

- 修飾符來實現僅在按下相應按鍵時才觸發鼠標或鍵盤事件的監聽器 - .ctrl, .alt, .shift, .meta

需要搭配多組按鍵才會去做觸發 `<v-on>` ，
前後順序撰寫無差別，主要 enter 鍵搭配副鍵 .shift 來搭配使用觸發

範例程式碼：

```html
<h6 class="mt-3">相應按鍵時才觸發的監聽器</h6>
<input
  type="text"
  class="form-control"
  v-model="text"
  @keyup.shift.enter="trigger('shift + Enter')"
/>
```

```jsx
const App = {
  data() {
    return {
    };
  },
  methods: {
    trigger: function (name) {
      console.log(name, "此事件被觸發了");
    },
  },
};
```

### 特定鍵

- keyAlias - 只當事件是從特定鍵觸發時才觸發。

特定按鈕才會做觸發，此範例使用 h 按鍵來做特定按鍵觸發

範例程式碼：

```html
<h6 class="mt-3">特定鍵</h6>
<input
  type="text"
  class="form-control"
  v-model="text"
  @keyup.h="trigger('h')"
/>
```

```jsx
const App = {
  data() {
    return {
    };
  },
  methods: {
    trigger: function (name) {
      console.log(name, "此事件被觸發了");
    },
  },
};
```

## 滑鼠修飾符

- .left 只當點擊鼠標左鍵時觸發。
- .right 只當點擊鼠標右鍵時觸發。
- .middle 只當點擊鼠標中鍵時觸發。

此範例使用滑鼠右鍵來觸發事件，只要在 box 內透過滑鼠右鍵點擊，即可觸發事件

範例程式碼：

```html
<h6 class="mt-3">滑鼠修飾符</h6>
<div class="p-3 bg-primary">
  <span class="box" @click.right="trigger('right button')"> </span>
</div>
```

```jsx
const App = {
  data() {
    return {
    };
  },
  methods: {
    trigger: function (name) {
      console.log(name, "此事件被觸發了");
    },
  },
};
```

## 事件修飾符

- .stop - 調用 `event.stopPropagation()`。
- **.prevent - 調用 `event.preventDefault()`。**
- .capture - 添加事件偵聽器時使用 capture 模式。
- .self - 只當事件是從偵聽器綁定的元素本身觸發時才觸發回調。
- .once - 只觸發一次回調。

此範例使用 `.prevent` 來達成移除 `<a>` 連結的點擊預設效果（預設點擊後回到最上方），

但其餘的冒泡機制依然會留存

範例程式碼：

```html
<a href="#" @click.prevent="trigger('prevent')"
  >加入 Prevent</a
>
```

## 預設情境

一般情況下如果不加上任何的修飾符，

運作流程會依照預設的冒泡事件，來由內而外觸發 DOM 事件元素

範例程式碼：

```html
<div class="p-3 bg-primary" @click="trigger('div')">
<span
  class="box d-flex align-items-center justify-content-center"
  @click="trigger('box')"
>
  <button
    class="btn btn-outline-secondary"
    @click="trigger('button')"
  >
    按我
  </button>
</span>
</div>

<!-- button 此事件被觸發了  -->
<!-- box 此事件被觸發了  -->
<!-- div 此事件被觸發了  -->
```

> 下方四個範例會透過修飾符，來避免預設事件發生，導致誤抓資料
> 

### stopPropagation （防止向外尋找）

在`<v-on>` 後方加上 `.stop` 來調用 `event.stopPropagation()`進行事件修飾

- 點擊 div 區塊：會發生 div 此事件被觸發了
- 點擊 box 區塊：會發生 box 此事件被觸發了
- 點擊 button 區塊：會發生 button 此事件被觸發了以及 box 此事件被觸發了
    - 因為 `.stop` 是加在外層 box 身上，所以由內而外會停在外層 box 元素上
    - 所以會有兩個 DOM 事件被觸發

範例程式碼：

```html
<h6 class="mt-3">stopPropagation (防止向外尋找)</h6>
<div class="p-3 bg-primary" @click="trigger('div')">
  <span
    class="box d-flex align-items-center justify-content-center"
    @click.stop="trigger('box')"
  >
    <button
      class="btn btn-outline-secondary"
      @click="trigger('button')"
    >
      按我
    </button>
  </span>
</div>

<!-- button 此事件被觸發了  -->
<!-- box 此事件被觸發了  -->
```

### 事件偵聽器時使用 capture 模式 （事件改為由外而內）

在`<v-on>` 後方加上 `.capture` 來調用 `event.stopPropagation()`進行事件修飾

將事件偵測 改為由外而內 ，

當最外層被觸發時，因為已經沒有在外一層了，所以僅會觸發當下 DOM 事件

範例程式碼：

```html
<h6 class="mt-3">
  事件偵聽器時使用 capture 模式 (事件改為由外而內)
</h6>
<div class="p-3 bg-primary" @click.capture="trigger('div')">
  <span
    class="box d-flex align-items-center justify-content-center"
    @click.capture="trigger('box')"
  >
    <button
      class="btn btn-outline-secondary"
      @click.capture="trigger('button')"
    >
      按我
    </button>
  </span>
</div>

<!-- div 此事件被觸發了  -->
<!-- box 此事件被觸發了  -->
<!-- button 此事件被觸發了  -->
```

### 事件偵聽器時使用 self 模式 (只會觸發自己範圍內的)

相比前幾個，這個就比較直覺化，`.self` 就只會觸發當下所觸及的 DOM 事件

所以如果點擊 button 那就只會觸發 button 的 DOM 事件

範例程式碼：

```html
<h6 class="mt-3">
  事件偵聽器時使用 self 模式 (只會觸發自己範圍內的)
</h6>
<div class="p-3 bg-primary" @click.self="trigger('div')">
  <span
    class="box d-flex align-items-center justify-content-center"
    @click.self="trigger('box')"
  >
    <button
      class="btn btn-outline-secondary"
      @click.self="trigger('button')"
    >
      按我
    </button>
  </span>
</div>
```

### 事件偵聽器只觸發一次 once

意思就是只會觸發一次 DOM 事件，

嘗試透過點擊來觸發 DOM 事件會發現它只會觸發一次，之後不管再點選哪個元素，

都將不會再被觸發，除非重新整理畫面或是重新生成此元件

範例程式碼：

```html
<h3 class="mt-3">事件偵聽器只觸發一次 once</h3>
<div class="p-3 bg-primary" @click.once="trigger('div')">
  <span
    class="box d-flex align-items-center justify-content-center"
    @click.once="trigger('box')"
  >
    <button
      class="btn btn-outline-secondary"
      @click.once="trigger('button')"
    >
      按我
    </button>
  </span>
</div>
```

# v-on DOM 事件

當我們使用原生 JS DOM 來做觸發事件時，就會產生原生 JS 會預設進行的事件處理

<aside>
💡 例如 click Event : 就會帶入到我們滑鼠所進行的操作
</aside>

[HTML DOM Event Object](https://www.w3schools.com/jsref/dom_obj_event.asp)

更多的原生 JS DOM 事件

## 原生 DOM 事件

創建個區塊且新增三個按鈕，帶上不同的修飾符，來查看在 console 內會如何執行：

- 選擇物件：MouseEvent
- 按鈕事件：KeyboardEvent

    
![](https://i.imgur.com/yHp6Zoj.png)
console 內的 event 資料預覽圖

<aside>
💡 當沒有參數時，預設第一個則是 dom 事件參數

</aside>

- 自訂參數：可以使用自定義參數`'props'`，以及使用者使用的事件觸發`$event`

![](https://i.imgur.com/Hbuiuy6.png)
console 內的 event 資料預覽圖

範例程式碼：

```html
<div class="box" :class="{ rotate: isTransform }"></div>
<hr>

<!-- 當沒有參數時，預設第一個則是 dom 事件參數 -->
<button class="btn btn-outline-primary" @click="changeClass">選擇物件</button>
<button class="btn btn-outline-primary" @keyup.enter="changeClass">按鈕事件</button>

<!-- 當如果有參數時，則可以使用 $event -->
<button class="btn btn-outline-primary" @click="changeClassWithEvent('這段是自訂參數', $event)">自訂參數</button>
```

```jsx
const App = {
  data() {
    return {
      isTransform: true,
    }
  },
  methods: {
    changeClass: function(e) {
      console.log('dom', e);
      this.isTransform = !this.isTransform;
    },
		changeClassWithEvent(parameter, e) {
      console.log(parameter, e);
    },
	}
}
```
 
## 取得原生 input 數值

取得 user 輸入在 input 內的資料，

透過 console 來查看資料狀態，打開 target 再往下去尋找 value 就可以看到我們剛剛輸入的內容了

透過 `e.target.value` 就可以正確搜尋到 input 內的數值了，

裡頭還有許多的方法可以去做使用，讓我們更靈活的可以去分析且篩選所要的 input 資料內容

    
![](https://i.imgur.com/xjVXAux.png)
console 內的 target.value 狀態預覽圖

範例程式碼：

```html
<h3>取得原生 input 數值</h3>
<input type="text" @change="inputEvent" />
```

```jsx
const App = {
  data() {
    return {
    }
  },
  methods: {
    inputEvent(e) {
      console.log(e.target.value);
    },
	}
}
```

## 監聽按鍵事件

監聽使用者在 input 內是按了哪一個按鍵，查看 console 內有個 methods 為 keycode，

可以透過 keyCode 觀察到目前使用者是輸入了哪個按鍵

    
![](https://i.imgur.com/KphOBXA.png)
console 內的 keyCode 狀態預覽圖

範例程式碼：

```html
<h3>監聽按鍵事件</h3>
<input type="text" @keyup="keyboardEvent" />
```

```jsx
const App = {
  data() {
    return {
    }
  },
  methods: {
    keyboardEvent(e) {
      console.log(e.keyCode);
    },
	}
}
```