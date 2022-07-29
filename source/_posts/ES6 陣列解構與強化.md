---
tags: 2022 React 新手讀書會
---

# ES6 陣列解構與強化

陣列同樣也有解構賦值的寫法，本次讀書會使用到的 React Hooks 也經常被使用。

## 陣列解構

以前我們要讀取陣列裡面的值，都會使用如下程式碼來取值：

```javascript
const family = ["爸", "媽", "姊姊", "哥哥"];

// 一般會這樣寫
const papa = family[0];
const mama = family[1];
const sister = family[2];
const brother = family[3];
```

但藉由 ES6 的`陣列解構`語法，下方程式碼也可達到一樣效果，讓程式碼可以更精簡：

```javascript
const family = ["爸", "媽", "姊姊", "哥哥"];

// 縮寫版
const [papa, mama, sister, brother] = family;

console.log(papa); // '爸爸'
console.log(sister); // '姊姊'
```

若是遇到空的變數，會將值跳過

```javascript
const family = ["爸", "媽", "姊姊", "哥哥"];
const [papa, , , brother] = family;

console.log(papa); // '爸爸'
console.log(brother); // '哥哥'
```

若是左邊的變數數量多餘右邊的值，會將多出來的變數賦予 `undefined`

```javascript
const family = ["爸", "媽", "姊姊", "哥哥"];
const [papa, , , brother, grandpa] = family; // 有五個變數

console.log(papa); // '爸爸'
console.log(brother); // '哥哥'
console.log(grandpa); // undefined
```

若是值為**字串**，會將字串拆解為一個一個字元

```javascript
const family = "family";
const [papa, , , brother, grandpa] = family;

console.log(papa); // 'f'
console.log(brother); // 'i'
console.log(grandpa); // 'l'
```

**可以輕易互換變數**

```javascript
let papa = "爸爸";
let mama = "媽媽";

[papa, mama] = [mama, papa];

console.log(papa); // '媽媽'
console.log(mama); // '爸爸'
```

## Demo

1. 優化下方將陣列內的值賦予到變數上的寫法

   ```javascript
   // 舊寫法
   const students = ["安妮", "露璐", "努努", "索娜", "艾希"];
   const lulu = students[1];
   const nunu = students[2];
   const ashe = students[4];

   // 新寫法
   const [, lulu, nunu, , ashe] = students;
   console.log(lulu);
   console.log(nunu);
   ```

2. 運用陣列解構賦值，將下方 numbers 變數內 1 和 5 對調，變為 `[5, 7, 1]`

   ```javascript
   // 新寫法
   let numbers = [1, 7, 5];
   [numbers[0], numbers[1], numbers[2]] = [numbers[2], numbers[1], numbers[0]];
   console.log(numbers);
   ```
