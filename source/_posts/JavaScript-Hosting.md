---
title: JavaScript Hosting 變數提升
description: 一般來說程式語言都是逐行執行的，所以正常都應該先宣告變數或函式才可以使用，但寫過 JS 的人都會發現有件神奇的事，我們可以先執行函式或變數，然後才進行宣告。

date: 2021-04-07 18:01:05
categories:
  - JavaScript
tags:
  - JavaScript
---

## 前言

一般來說程式語言都是逐行執行的，所以正常都應該先宣告變數或函式才可以使用。

但寫過 JS 的人都會發現有件神奇的事，我們可以先執行函式或變數，然後才進行宣告。

一般的解釋是 JS 會執行類似"**提升**"的動作，自動將宣告或賦值的步驟在呼叫的時候執行。
但其實 Hoisting 這個字多少要負些責任讓大家誤會大了。
Hoisting 中文叫做提升，我們先把中文的名字忘一邊。

## Hoisting 的好處

- JavaScript 先宣告變數與函式再使用
- 函式可互相呼叫 (不論宣告的前後順序)

### `is not defined` & `undefined` 差異

在 JS 中，如果使用未宣告的變數：

```javascript
console.log(a);

// ReferenceError: a is not defined
```

使用已宣告、未賦值變數

```javascript
console.log(a);
var a;

// undefined
```

不管變數宣告的位置在哪裡，一開始載入時都會先找到所有「變數」與「函式 function」，並完成宣告，才會開始其他執行動作。
所以即使執行程式在變數之前，也都找得到變數，即稱為「Hosting」。
只有變數宣告可提升，賦值不會

```javascript
var a;
console.log(a);
a = 5;

// undefined

// 執行順序為：
// 1. var a
// 2. console.log(a)
// 3. a = 5
```

函式帶的參數，即視為變數
(如果沒有參數，則以函式內的賦值優先)

```javascript
function test(v) {
  console.log(v);
  var v = 3;
}
test(10);

// 10
// 因為參數帶入 10 ，故等同於先宣告了 var v = 10

// 執行順序為：
// var test = function(v){ console.log(v) var v =3 }
// test(10)
```

函式 function 的宣告優先權高於變數

```javascript
console.log(a);
var a;
function a() {}

// [function: a]
// undefined

// 執行順序為：
// function a(){}
// console.log(a)
// var a = ''
```

用 let 與 const 宣告的變數也會提升，但未賦值前如果使用該變數會出錯

> let 與 const 有 hoisting，
> 與 var 的差別在於提升之後，var 宣告的變數會被初始化為 undefined，而 let 與 const 的宣告不會被初始化為 undefined，而且如果你在「賦值之前」就存取它，就會拋出錯誤。
> 在「提升之後」以及「賦值之前」這段「期間」，
> 如果你存取它就會拋出錯誤，而這段期間就稱做是 TDZ(Temporal Dead Zone)。

```javascript
var a = 10;
function test() {
  console.log(a);
  let a;
}
test();

//  ReferenceError: a is not defined
```

## hoisting 到底是怎麼運作的？

Execution Contexts（以下簡稱 EC）， 每當你進入一個 function 的時候，就會產生一個 EC，裡面儲存跟這個 function 有關的一些資訊，並且把這個 EC 放到 stack 裡面，當 function 執行完以後，就會把 EC 給 pop 出來。
每個 EC 都會有相對應的 variable object（以下簡稱 VO），在裡面宣告的變數跟函式都會被加進 VO 裡面，如果是 function，那參數也會被加到 VO 裡。
對於 function 的參數，它會直接被放到 VO 裡面去，如果有些參數沒有值的話，那它的值會被初始化成 undefined。 如果 VO 裡面找不到，會透過 scope chain 不斷往上尋找，如果每一層都找不到就會拋出錯誤。

## 在進入 EC 的時候(跑 function 程式碼前)，會按照以下順序把東西放到 VO 裡面，新的會覆蓋掉舊的

1. function 的參數：傳什麼進來就是什麼，沒有值的設成 undefined
2. function 宣告放到 VO 裡，如果已經有同名的就覆蓋掉
3. 變數宣告放到 VO 裡，如果已經有同名的則忽略

舉例來說我們熟知的使用方式應該是:

```javascript=
var a = 'Hello World!';

function b() {
    console.log('Called b!');
}

b();
console.log(a);

//  * Called b!
//  * Hello World!
```

到這裡沒有太大的問題
那如果按照 Hoisting 的說法，下面的程式執行應該會產出什麼呢?

```javascript=
b();
console.log(a);

var a = 'Hello World!';

function b() {
    console.log('Called b!');
}

// * Called b!
// * undefined
```

首先會先執行 `function` => `console.log(a)` => `var a ='Hello World!'`

> function 會優先被提升到最上方做執行，其餘的部分就會照正常順序走

這跟 JS 如何初始執行環境有關，
JS 在初始的 context 第一個步驟，就配置給函式還有變數一個記憶體空間。
函式在配置時就會完整放在記憶體空間裡，而變數就只是宣告但尚未賦值。

所以回頭來看，用上面的話來解釋的話，在 JS 初始階段，程式碼應該會被解讀成為以下：

```javascript=
var b = function () {
    console.log('Called b!');
};
var a;

b();
console.log(a);

a = 'Hello World!';
```

## 參考資料

- [我知道你懂 hoisting，可是你了解到多深？](https://github.com/aszx87410/blog/issues/34)
