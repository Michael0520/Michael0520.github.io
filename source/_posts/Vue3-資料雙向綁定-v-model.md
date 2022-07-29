---
title: (Vue) 資料雙向綁定 v-model
date: 2021-07-31
description: 資料雙向綁定練習
categories:
- Vue
tags:
- Vue
---
## 綁定文字區塊，透夠輸入資料渲染資料

透過 `<v-model>` 綁定 data ，在 `<input>` 內輸入資料，會同時更動以及渲染資料

```html
<h3>input</h3>
  <input type="text" class="form-control"
        v-model="name">
  {{ name }}

<hr />
<h3>textarea</h3>
<textarea cols="30" rows="3" class="form-control"
        v-model="text"></textarea>
{{ text }}
```

```jsx
const App = {
  data() {
    return {
      name: '小明',
      text: "一段文字敘述",
    }
  }
}
```

![輸入資料時，資料被更新後預覽圖](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/77b5dc5a-394d-46ce-b2ab-87f43971fd8b/CleanShot_2021-07-13_at_05.34.03.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211104T104948Z&X-Amz-Expires=86400&X-Amz-Signature=dc052e23ff2ffe39b7edd2ddad3d1c457b27bef5aef382a138edf4d99611de07&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22CleanShot_2021-07-13_at_05.34.03.gif%22)

輸入資料時，資料被更新後預覽圖

## 綁定 checkbox

### checkbox 單選框

綁定 checkbox 資料狀態，使用三元運算子，來透過有無勾選 checkbox 判斷呈現資料，

```html
<h3>checkbox 單選框</h3>
<p>小明，你是吃飽沒？</p>

<!-- 三元運算子 -->
<p>{{ checkAnswer ? '吃飽了' : '還沒'}}</p>

<div class="form-check">
  <input
    type="checkbox"
    class="form-check-input"
    v-model="checkAnswer"
    id="check1"
  />
  <label class="form-check-label" for="check1">小明回覆</label>
</div>
```

```jsx
const App = {
  data() {
    return {
      checkAnswer: false,
    }
  }
}
```

![成功透過 checkbox 切換判斷呈現資料預覽圖](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fbe14baa-997a-464d-bda5-88a1b199947b/CleanShot_2021-07-13_at_05.43.01.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211104T105017Z&X-Amz-Expires=86400&X-Amz-Signature=600c3b612ab0689e75261dc7237316e9aa0acff92570a9fb90f621c7e36b7502&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22CleanShot_2021-07-13_at_05.43.01.gif%22)

成功透過 checkbox 切換判斷呈現資料預覽圖

## checkbox 單選延伸

直接將資料狀態寫在 html 標籤內，透過有無勾選直接渲染資料，

就不用加上三元運算子去做判斷渲染，

### 特殊狀況

`<input>` 透過 `<v-model>` 綁定了 `data.checkAnswer2` 為空字串，

所以一開始 `<p>` 會隱藏，

透過 checkbox 特性賦予布林值，才透過 html 標籤內賦予的，

布林值判斷式來加入字串後，才會出現 `<p>`

範例程式碼：

```html
<h3>checkbox 單選延伸</h3>
<p>小明，你是吃飽沒？</p>
<p>{{ checkAnswer2 }}</p>
<div class="form-check">
  <input
    type="checkbox"
    class="form-check-input"
    id="check2"
    v-model="checkAnswer2"
    true-value="吃飽了"
    false-value="還沒"
  />
  <label class="form-check-label" for="check2">小明回覆</label>
</div>
```

```jsx
const App = {
  data() {
    return {
      checkAnswer2: "",
    }
  }
}
```

![透過布林值判斷式來加入字串後渲染資料 成功預覽圖](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/68ae2b31-3190-4ed6-8d63-f2b84070af41/CleanShot_2021-07-13_at_05.54.58.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211104T105036Z&X-Amz-Expires=86400&X-Amz-Signature=cf0a3ab7d8c9b6375497b33230b4489acf1c02a36dfb2380bcf8b5d9fa494515&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22CleanShot_2021-07-13_at_05.54.58.gif%22)

透過布林值判斷式來加入字串後渲染資料 成功預覽圖

## checkbox 複選框

多個 `<input>` 使用 `<v-model>` 綁定同一個資料 `data.checkAnswer3` 為空陣列，

顯示區塊使用樣板字面詞  `{{ checkAnswer3.join(' ') }}` ，

使用 checkbox 特性，加上 `value` 值，

當勾選了 checkbox 時，會存取 `value` 值，

再透過 `join('')` 來合併 多組 value 值成新資料，

`data.checkAnswer3` 為空陣列，讓多個 `<input>` 的資料可以一同合併渲染出

<aside>
💡 當取消勾選時，value 也會消失，因而產生資料被刪除的狀況

</aside>

範例程式碼：

```html
<h3>checkbox 複選框</h3>
<p>你還要吃什麼？</p>

<!-- 使用 join('') 來合併 value 值，成新資料  -->
<p>{{ checkAnswer3.join(' ') }}</p>

<div class="form-check">
  <input
    type="checkbox"
    class="form-check-input"
    v-model="checkAnswer3"
    id="check3"
    value="蛋餅"
  />
  <label class="form-check-label" for="check3">蛋餅</label>
</div>
<div class="form-check">
  <input
    type="checkbox"
    class="form-check-input"
    v-model="checkAnswer3"
    id="check4"
    value="蘿蔔糕"
  />
  <label class="form-check-label" for="check4">蘿蔔糕</label>
</div>
<div class="form-check">
  <input
    type="checkbox"
    class="form-check-input"
    v-model="checkAnswer3"
    id="check5"
    value="豆漿"
  />
  <label class="form-check-label" for="check5">豆漿</label>
</div>
```

```jsx
const App = {
  data() {
    return {
      checkAnswer3: [],
    }
  }
}
```

![成功透過勾選存取 value 使用 join('') 成新資料渲染 ](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/82962910-f3cf-44a4-944e-4d20fa103f32/CleanShot_2021-07-13_at_06.16.23.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211104T105054Z&X-Amz-Expires=86400&X-Amz-Signature=9903e3c0a84f5da0d922e628f1407cc3006fed324bf0cdff47ed0e4dbc87d243&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22CleanShot_2021-07-13_at_06.16.23.gif%22)

成功透過勾選存取 value 使用 join('') 成新資料渲染 

## radio 單選框

多個 `<input>` 使用 `<v-model>` 綁定同一個資料 `data.radioAnswer` 為空字串，

來透過勾選內容存取 value 值，顯示資料

在更動勾選內容時，會重新存取資料，覆寫原有資料顯示為新資料

```html
<h3>radio 單選框</h3>
<p>你還要吃什麼？</p>

<p>{{ radioAnswer }}</p>

<div class="form-check">
  <input
    type="radio"
    class="form-check-input"
    id="radio1"
    v-model="radioAnswer"
    value="蛋餅"
  />
  <label class="form-check-label" for="radio1">蛋餅</label>
</div>
<div class="form-check">
  <input
    type="radio"
    class="form-check-input"
    id="radio2"
    v-model="radioAnswer"
    value="蘿蔔糕"
  />
  <label class="form-check-label" for="radio2">蘿蔔糕</label>
</div>
<div class="form-check">
  <input
    type="radio"
    class="form-check-input"
    id="radio3"
    v-model="radioAnswer"
    value="豆漿"
  />
  <label class="form-check-label" for="radio3">豆漿</label>
</div>
```

```jsx
/*
如果 radioAnswer 賦予 "蛋餅" 時，
此表格預設狀態就是會勾選 "蛋餅" 欄位
*/

const App = {
  data() {
    return {
      radioAnswer: "",
    }
  }
}
```

![成功透過勾選存取 value 成新資料，切換內容重新渲染 ](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d0a143ba-3b63-4b3e-9d8d-007700d94639/CleanShot_2021-07-13_at_06.29.47.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211104T105114Z&X-Amz-Expires=86400&X-Amz-Signature=c4b5be1f8696f9c3ee1ef32c354dd7868c8f16730feb9e879d8196878bf8b4ac&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22CleanShot_2021-07-13_at_06.29.47.gif%22)

成功透過勾選存取 value 成新資料，切換內容重新渲染

## select 單選

下拉選單後，選擇資列欄位，使用區塊顯示出

- `<select>` 表單
  - 使用 `<v-model>`綁定 `data.selectAnswer` 為空字串
- `<option>` 預設選項
  - 使用 `value` 值為空字串，可以讓選定此欄位時，清空資料
  - 可以直接輸入文字在顯示區塊內當做預設選項所要顯示的資料
- `<option>` 下拉選項：
  - 使用 `<v-for>`一次渲染多筆資料於 select 內，並且透過花括號來自定義資料顯示於 select 內
  - 使用 `v-bind` 來綁定商品名稱讓選定選項後，只顯示商品名稱，不要顯示完整資料

範例程式碼：

```html
<h3>select 單選</h3>
            <p>你還要吃什麼？</p>
            <p>{{ selectAnswer }}</p>
            <select class="form-select" v-model="selectAnswer">
              <option value="">說吧，你要吃什麼？</option>
              <option
                v-bind:value="item.name"
                v-for="(item, index) in products"
                :key="item.name"
              >
                {{item.name}} / {{item.price}} 元
              </option>
            </select>
```

```jsx
const App = {
  data() {
    return {
      selectAnswer: "",
      products: [
        {
          name: "蛋餅",
          price: 30,
          vegan: false,
        },
        {
          name: "飯糰",
          price: 35,
          vegan: false,
        },
        {
          name: "小籠包",
          price: 60,
          vegan: false,
        },
        {
          name: "蘿蔔糕",
          price: 30,
          vegan: true,
        },
      ],
		}
	}
}
```

![成功切換並顯示資料，回到預設欄位，清空資料預覽圖](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0ee05b5f-231d-4824-a348-ada972d10e82/CleanShot_2021-07-13_at_06.56.19.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211104T105132Z&X-Amz-Expires=86400&X-Amz-Signature=0c9cc7d6bd8c62a7577ef192993ba56c1c41dd3dce87ea463a70c7c75777e5d4&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22CleanShot_2021-07-13_at_06.56.19.gif%22)

成功切換並顯示資料，回到預設欄位，清空資料預覽圖

### disable 不可點選選項

加入 `disable` 屬性，即可讓那則欄位，變成預設選項，且不可點選，

缺點是必須要再新增 methods 來清空資料

```html
<!-- 加入 disabled 屬性  達成預設不可選擇的樣式 -->
<option selected disabled value="">說吧，你要吃什麼？</option>
```

![image](https://i.imgur.com/z26mQLd.png)

預設不可點選欄位

## select 多選

將選定的資料欄位，改為可多選，並且可以顯示多筆選定資料到畫面上

將上方範例做點小修改：

- `<v-model>` 綁定 `data.selectAnswer2`，設為空陣列
- `<option>` 加上多選屬性 `multiple` 即可完成

<aside>
💡 多選需要使用快捷鍵搭配選擇
Windows 下可以使用 ctrl，Mac 則是使用 cmd

</aside>

範例程式碼：

```html
<h3>select 多選</h3>
<p>你還要吃什麼？</p>

<p>{{ selectAnswer2 }}</p>

<select class="form-select" v-model="selectAnswer2" multiple>
  <option selected disabled value="">說吧，你要吃什麼？</option>
  <option
    :value="item.name"
    v-for="item in products"
    :key="item.name"
  >
    {{item.name}} / {{item.price}} 元
  </option>
</select>
```

```jsx
const App = {
  data() {
    return {
      selectAnswer2: [],
      products: [
        {
          name: "蛋餅",
          price: 30,
          vegan: false,
        },
        {
          name: "飯糰",
          price: 35,
          vegan: false,
        },
        {
          name: "小籠包",
          price: 60,
          vegan: false,
        },
        {
          name: "蘿蔔糕",
          price: 30,
          vegan: true,
        },
      ],
    }
  }
}
```

![成功多選資料且顯示預覽圖](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/624d7971-4061-42ae-a2f4-5cdb6219abfd/CleanShot_2021-07-13_at_07.21.52.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211104T105207Z&X-Amz-Expires=86400&X-Amz-Signature=ae02d3aa2ffc0d04ba652da5430e29903c35dbc62707ec3711a013fe7581d8de&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22CleanShot_2021-07-13_at_07.21.52.gif%22)

成功多選資料且顯示預覽圖

## v-model 修飾符

### 延遲 Lazy

基本的雙向綁定資料，會使 input 輸入資料時，同步渲染出一樣資料的顯示區塊，

為了提升使用者體驗，在`<v-model>` 後方加上 `.lazy`，

當在 input 輸入完成時，需要透過點按其他任何區域，來離開 input ，才會渲染資料

```html
<h4 class="mt-3">延遲 Lazy</h4>
{{ lazyMsg }}
<input type="text" class="form-control" v-model.lazy="lazyMsg">
```

```jsx
const App = {
  data() {
    return {
      lazyMsg: '',
    }
  },
};
```

![image](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b80c642b-2fe8-4358-948d-aa4053fbb805/CleanShot_2021-07-13_at_23.30.58.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211104T105219Z&X-Amz-Expires=86400&X-Amz-Signature=3655da90f826cd0eb2cfb75f2c044e4a6991b30f78ecebe3d84b2a2dfd593d5d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22CleanShot_2021-07-13_at_23.30.58.gif%22)

## 純數值 Number

強迫讓 input 只能輸入純數值 number

- input type 屬性改為 number
- `<v-model>` 後方加上 number ，綁定到 number  上

範例程式碼：

```html
<h4 class="mt-3">純數值 Number</h4>
{{ numberMsg }}{{ typeof numberMsg }}
<input type="number" class="form-control" v-model.number="numberMsg" />

<h4 class="mt-3">純文字 Number</h4>
{{ numberMsg }}{{ typeof numberMsg }}
<input type="text" class="form-control" v-model.number="numberMsg" />
```

```jsx
const App = {
  data() {
    return {
      numberMsg: "",
    };
  },
};
```

### 例外發生

如果將上方範例 `<input type>` 屬性再改回 `text` ，`<v-model>` 保持著綁定 `number`

此時會發生一樣可以輸入純文字，但型別沒有被轉換，

必須開頭先輸入 number 才會先吃到型別，後方如果輸入文字，一樣會保持純數值型別

<aside>
💡 為了避免出錯，`<input type>` 綁定什麼屬性
`<v-model>` 就該加上什麼屬性的修飾符

</aside>

![偵測兩種不同 type 綁定效果預覽圖](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6bf22451-d2d6-47ea-ae4f-4cc9aaeae2fe/CleanShot_2021-07-14_at_05.32.59.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211104T105237Z&X-Amz-Expires=86400&X-Amz-Signature=092eac61d2586dd913ed6f689dfa00c665dc08e17edce64dc6671274438a4444&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22CleanShot_2021-07-14_at_05.32.59.gif%22)

偵測兩種不同 type 綁定效果預覽圖

## 修剪 Trim

刪除掉輸入文字前後的空白

將 `<v-model>` 後方加上修飾符 `.trim` ，就可以完成此效果了

如果想使用 `<.trim>` 效果以及 `<input type>`綁定特殊屬性效果可以重複疊加

範例程式碼：

```jsx
<h4 class="mt-3">修剪 Trim</h4>
這是一段{{ trimMsg }}緊黏的文字
<input type="text" class="form-control" v-model.trim="trimMsg" />

<h4 class="mt-3">修剪 Trim</h4>
這是一段{{ trimMsg }}緊黏的數字
<input type="number" class="form-control" v-model.trim.number="trimMsg" />
```

```jsx
const App = {
  data() {
    return {
      trimMsg: "",
    };
  },
};
```

![兩種型別加上修飾來取得輸入資料 預覽圖](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/50d884f2-1b5c-44ca-b662-4ed85eacebfd/CleanShot_2021-07-14_at_05.47.21.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211104T111317Z&X-Amz-Expires=86400&X-Amz-Signature=4c533b2d53440b7d19680617f0671de617f1125930c0df42a2525c0d1bade4fc&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22CleanShot_2021-07-14_at_05.47.21.gif%22)

兩種型別加上修飾來取得輸入資料 預覽圖