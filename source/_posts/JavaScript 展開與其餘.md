---
tags: 2022 React 新手讀書會
---

# JavaScript 展開與其餘

展開運算子與其餘運算子都與**陣列**有關，運用的符號都是 `...`

## 展開運算子

### 組合陣列

過去要組合陣列會使用 concat 陣列方法：

```javascript
let adults = ["爸爸", "媽媽"];
let kids = ["妹妹", "弟弟"];
const family = adults.concat(kids);
console.log(family); // ['爸爸', '媽媽', '妹妹', '弟弟']
```

但藉由 ES6 的`展開運算子`語法，下方程式碼也可達到一樣效果，讓程式碼可以更精簡：

```javascript
let adults = ["爸爸", "媽媽"];
let kids = ["妹妹", "弟弟"];
const family = [...adults, ...kids];
console.log(family); // ['爸爸', '媽媽', '妹妹', '弟弟']
```

展開運算子實際上是一次又一次的 `return` 陣列中的值

```javascript
console.log(...adults);
// '爸爸'
// '媽媽'
```

### 淺層複製

陣列有**傳參考**的特性，如果直接將陣列直接賦予到另外一個陣列，當修改其中一個陣列時，另一個也會跟著變動：

```javascript
let kidsA = ["妹妹", "弟弟"];
let kidsB = kidsA;
kidsB.push("姊姊");
console.log(kidsA); // ['妹妹', '弟弟', '姊姊']
console.log(kidsB); // ['妹妹', '弟弟', '姊姊']
```

由於展開運算子會一次一次地將值寫入，所以他可以淺層複製（淺拷貝 shallow copy）：

```javascript
let kidsA = ["妹妹", "弟弟"];
let kidsB = [...kidsA];
kidsB.push("姊姊");
console.log(kidsA); // ['妹妹', '弟弟']
console.log(kidsB); // ['妹妹', '弟弟', '姊姊']
```

### 將類陣列轉成純陣列

像是 DOM 陣列可以透過展開運算子轉變為純陣列，使其可以運用陣列的方法：

```javascript
let doms = document.querySelectorAll("p");
console.log(doms);
let spreadDom = [...doms];
console.log(spreadDom);
```

### 可以將字串拆開

```javascript
let str = "string";
console.log(...str); // 's','t','r','i','n','g'
```

## 其餘運算子

通常運用在**函式傳入參數的定義**中：

```javascript
// ...b：其餘參數，會將不確定的傳入參數值們，轉變為陣列做運算
function printFn(a, ...b) {
  console.log("a: ", a, ", b: ", b);
}

printFn(1, 2, 3);
// a: 1, b: [2, 3]
```

> 注意：在函式傳入參數的定義中，其餘參數需**放在最後**，並且**只能有一個**其餘參數

若是呼叫函式時，其餘參數的值沒有傳入，會變為一個空陣列：

```javascript
printFn(1); // a: 1, b: []
printFn(); // a: undefined, b: []
```

其餘運算子也會運用在**解構賦值**中：

```javascript
const [a, ...b] = [1, 2, 3];
console.log(a); // 1
console.log(b); // [2, 3]

// 若是值沒有對應到，一樣會轉為空陣列
const [a, b, ...c] = [1];
console.log(a); // 1
console.log(b); // undefined
console.log(c); // []
```

> 注意：在解構賦值中，其餘運算子一樣需**放在最後**，並且**只能有一個**

## 題目一

請運用展開運算子，優化下方程式碼

```javascript
const numA = [1, 2, 3];
const numB = [4, 5, 6];
const numbers = numB.concat(numA);
```

<!--
const numbers = [...numB, ...numA];
-->

## 題目二

下方為其餘參數搭配解構賦值的函式，請先嘗試觀察並手動計算出下方答案，再直接使用程式碼觀看解答

```javascript
function sumFn(a, ...[x, y]) {
  // console.log(x,y);
  return a + x * y;
}

sumFn(1, 2, 3);
sumFn(1, 2, 3, 4);
sumFn("1", "2", "3", "4");
sumFn(1);
```

```javascript
sumFn(1, 2, 3); // 7 => sumFn( 1 + (2 * 3))
sumFn(1, 2, 3, 4); // 7 => sumFn( 1 + (2 * 3),undefined)
sumFn("1", "2", "3", "4"); // '16' => sumFn("1" + ("2" * "3")) => sumFn("1" + "6") => 16 (JavaScript is amazing!)
sumFn(1); // NaN => sumFn( 1 + (2 * undefined))
```
