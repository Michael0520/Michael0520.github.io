---
title: JavaScript Scope 作用域
date: 2021-04-08 18:42:14
description: 撰寫程式一定會非常頻繁的使用變數，變數也有生命週期，或者是說作用域更為適合。
categories:
  - JavaScript
tags:
  - JavaScript
---

## 前言

撰寫程式一定會非常頻繁的使用變數，變數也有生命週期，或者是說作用域更為適合。

什麼是作用域(scope)？意思就是，變數在程式中可以被存取的範圍。
以範圍來區分變數的話，可分為:

- 區域變數
- 全域變數

那區域跟全域又是以什麼為界定來區分的呢?

傳統的後端程式語言，區域變數只在大括號 `{}` 中有效，
在此範圍外，就是全域變數，它是以區塊 `(block){}` 作為區分，
但 JS 卻不是以此做區分，它是用函式 `(function)` 作為區分，
在函式內為區域變數，函式外為全域變數，要達成這樣的條件還有一個前提，變數必須以 `var` 宣告。

```javascript
var scope = "全域";
function getValue() {
  var scope = "區域";
  return scope;
}
console.log(getValue()); // 區域
console.log(scope); // 全域
```

結果顯示，函式回傳的 scope 是區域變數的值，
最後的敘述式 (statement) 回傳的是全域變數的值，由此可知它們是不同的變數，即使名稱一樣。

```javascript=
var scope = '全域';
function getValue1() {
    var scope = '區域1';
    return scope;
}
function getValue2() {
    var scope = '區域2';
    return scope;
}
console.log(getValue1()); // 區域1
console.log(getValue2()); // 區域2
console.log(scope); // 全域
```

`getValue1()` 與 `getValue2()` 裡面都有 scope，不同區域範圍的同名變數，實際上是不同的變數。

即使 scope 被宣告 3 次，但彼此之間沒有關聯，都是獨立的變數。

如果不用 `var` 宣告呢？

```javascript
scope = "全域";
function getValue() {
  scope = "區域";
  return scope;
}
console.log(getValue()); //區域
console.log(scope); //區域
```

結果顯示同一個變數，區域變數。
在 JS 中即使不以 var 宣告，一樣可以執行，但就算在涵式內也視為全域變數，更進一步來說，是 window 全域物件的屬性。

![](https://i.imgur.com/6BQigTE.png)

如此會汙染到我們的全域物件，這不是一個好現象，設計程式應養成好習慣，要加上宣告關鍵字。

剛剛談過了，在 JS 中，變數是以函式區塊做為區域跟全域的區別。

```javascript
if (true) {
  var x = 10;
}
console.log(x); // 10
```

> 變數 x 為全域變數。

![](https://i.imgur.com/6N30d3l.png)

以上的範例如果出現在傳統的後端程式語言中，會發生錯誤，但在 JS 是可以正常執行的。

ES6 新增了宣告關鍵字：let，let 支援區塊範圍。

```javascript=
if (true) {
    let x = 10;
}
console.log(x);

// Uncaught ReferenceError: x is not defined
```

如此一來，在區塊外面，就看不到區塊內的變數了。
在開發 Web 的時候，盡可能的不要汙染到全域物件，才是良好的習慣。

每個變數都有自己的作用域範圍，不論是全域或是區域，在自身的作用域範圍內，可以被存取，除此之外，也可以透過作用域鍊的關係，讓變數可以在其他的作用域範圍被存取。

```javascript=
function a() {
    let val = 2;
    b();
}
function b() {
    console.log(val);
}
let val = 1;
a();
```

以上的範例，輸出的值是多少？
相信很多人看到

```javascript=
let val = 2;
b();
```

會選擇答案是 2，但實際上是 1。

按照程式的執行順序上來看，

1. 宣告 `val=2` 後，直接呼叫 `b()` ，但 `b()` 沒有 `val` 這個變數，
2. 所以它會往呼叫 `b()`的上一行找到 `val=2` ，但答案很顯然地，輸出的是全域變數。

在 JS 中的執行環境有分全域執行環境與區域執行環境，函式內部是區域環境，全域環境是我們一開始在執行 JS ，
瀏覽器所建立的環境，也是最外層的環境。

從上面的範例來看， `a()` 、 `b()` 、變數 `val` 都是宣告在全域環境中，它們位於同一層的執行還境， `a()` 裡面的變數 `val` 是區域變數，是執行環境為 `a()` 的區域變數。

了解函式或變數本身所在的執行環境 (execution contexts) 後，
我們來觀察 `b()` 裡面的 val，
在 `b()` 中，並沒有宣告 `val` ，這表示如果想取 得`val `的值，必須得往其他的區域找，那為何它不找 `a()` 裡面，卻找全域環境？

這是因為，JS 引擎如果在該執行環境找不到變數，**它會往上一層找**。

既然 `a()` 、 `b()` 都是同一層，那當然不會進入函式尋找， `b()` 的上一層是全域環境，所以 JS 引擎會在全域環境中找到了 `val` ，以上才是真正的執行過程。

或許有人會認為在 `a()` 中呼叫 `b()` ，那 `b()` 才會往 `a()` 找 `val` ，我們再仔細看看範例， `b()` 是定義在全域環境中， `a()` 只是呼叫 `b()` 而已，並沒有在函式主體中定義它，重點是函式定義何處，而不是誰呼叫它。

所以我們可以這麼說， `b()` 透過作用域鏈的關係，在它的上一層(全域執行環境)能找到 `val` 。

我們再看另一個例子：

```javascript=
function a() {
    let val = 2;
    function b() {
        console.log(val);
    }
    b();
}
let val = 1;
a(); // 2
```

眼尖的讀者會發現，這是 閉包(closure) ，
關於閉包，下篇文章會討論。
我們先來看看，

1. 在 `a()` 中宣告 `b()` ， `b()` 的上一層就是 `a()` ，
2. 當它需要取得 `val` 的值，自然會透過作用域鏈在它的上一層， `a()` ，找到 `val` 的值。

## 參考資料

[JavaScript Scope 作用域
](https://ithelp.ithome.com.tw/articles/10206604)
