---
title: JavaScript-this
date: 2021-05-13
description: this 是函式執行時所屬的物件，其值是在執行時期做綁定，可大致歸納為四個規則以供判斷
categories:
  - JavaScript
tags:
  - JavaScirpt
---

# [JavaScript] this

![](https://i.imgur.com/4wfSKGc.png)

## this 是什麼？

![](https://i.imgur.com/sZpkdAI.png)

> 圖片來源：[What is this meaning of this?](http://www.explodingdog.com/title/whatisthemeaningofthis.html)

this 是函式執行時所屬的物件，其值是在執行時期做綁定，可大致歸納為四個規則以供判斷

## 判斷 this 的四個規則

this 的值可用四種規則判斷：

1. 預設綁定
2. 隱含綁定
3. 明確綁定
4. new 綁定

## 預設綁定（Default Binding）

當其他規則都不適用時，意即不屬於任何物件的方法、沒有使用 bind、call、apply 或 new，
就套用預設綁定，此時 this 的值就是預設值全域物件，在瀏覽器環境底下是 window。

### 範例 1

sayHello 不是某個物件的方法，也沒有使用 bind、call、apply 或 new，
因此 this 的值即 window。

```javascript=
function sayHello() {
  console.log(this);
}

sayHello(); // Window
```

### 範例 2

在函式 sayHello 內嘗試印出 `this.hello`，
由於此時 this 的值是 window，因此等同於查找 `window.hello` 的值，
就會找到在全域範疇所定義的 hello 了，最後就會印出「Hello World」。

```javascript=
function sayHello() {
  console.log(this.hello);
}

var hello = 'Hello World';
sayHello(); // Hello World
```

若在函式內使用 `'use strict'` 宣告成嚴格模式，
則 this 的值會改為 undefined，而非原本預設的全域物件 window。

```javascript=
function sayHello() {
  'use strict';
  console.log(this);
}

sayHello(); // undefined
```

## 嚴格模式（Strict Mode）

在上一個例子中，
我們看到了由於在函式內使用`'use strict'` 宣告成嚴格模式，this 的值改為 undefined，
而非原本預設的全域物件 window，那麼，

什麼是「嚴格模式」呢？

> Javascript 是一種很自由的語言，
> 但也正因如此，不嚴謹的寫法是被允許的。Strict Mode 是在 ES5 新增的，
> 只要加上了 “use strict” 這段文字，JS 引擎就會用嚴格的標準來讀你的 code，
> 避免你寫出不穩定或不夠嚴謹的 code。

一言以蔽之：讓你的 Javascript 更安全。

### 範例 1

在未宣告變數而賦值的狀況下，會無預警的產生一個全域變數，
但若使用嚴格模式（'use strict'）則會禁止這行為外，還會報錯，告知開發者變數尚未被定義。

```javascript=
'use strict';

name = "Michael"; // Uncaught ReferenceError: name is not defined
```

## 隱含綁定（Implicit Binding）

當函式為物件的方法（method）時，在執行階段 this 就會被綁定至該物件。

範例如下，函式 prompt 為物件 user 的方法，在執行階段 this 被綁至 user，
因此 console 時會到 user 查找其屬性 name。

```javascript=
const user = {
  name: 'Michael',
  sayHi: prompt,
};

function prompt() {
  console.log(this.name);
}

user.sayHi(); // 'Michael'
```

只有最頂層（或說是最終層）的物件才是有用的。
如下，prompt 的 this 是最終層的物件 anotherUser。

```javascript=
const anotherUser = {
  name: 'Not Michael!',
  sayHi: prompt,
};

const user = {
  name: 'Michael',
  anotherUser: anotherUser,
};

function prompt() {
  console.log(this.name);
}

user.anotherUser.sayHi(); // 'Not Michael!'
```

### 隱含的失去（Implicitly Lost）

隱含綁定也同時會有「隱含失去」的問題-隱含失去是指函式失去綁定的物件，
退回到預設綁定的狀態，意即 this 是全域物件 window 或嚴格模式下的 undefined。

- 什麼時候會造成隱含的失去呢？

  - 函式只是另一個函式的參考。
  - 參數傳遞中的 callback。
  - DOM element 的事件綁定（event binding）。

#### 範例 1 :函式是另一個函式的參考

bar 是 `obj.foo` 的參考，
並且 bar 的呼叫地點是在全域範疇，因此會套用"預設綁定"的規則。

```javascript=
function foo() {
  console.log(this.a);
}

var obj = {
  name: MyName,
  foo: foo,
};

var bar = obj.foo;
var name = 'Michael, global';
bar(); // 'Michael, global'
```

## 更多資訊可參考下文的[間接參考](https://)部份。

#### 範例 2 :參數傳遞中的 callback

範例如下，`doFoo(fn)` 的 fn 依舊是 `obj.foo` 的參考，
並且 fn 的呼叫地點是在全域範疇，因此會套用 =="預設綁定"== 的規則。

```javascript=
function foo() {
  console.log(this.name);
}

function doFoo(fn) {
  fn();
}

var obj = {
  name: "MyName",
  foo: foo,
};

var name = 'Michael, global';

doFoo(obj.foo); // 'Michael, global'
```

#### 範例 3：DOM element 的事件綁定

事件中的 callback 的 this 是觸發事件的元素（DOM element）。

```htmlmixed=
<button id="button">Click Me!</button>
```

> 點擊按鈕「Click Me!」 後，console 出目前 this 的值。

```javascript=
var el = document.getElementById('button');

el.addEventListener('click', function(e) {
  console.log(this); // "<button id='button'>Click Me!</button>"
});
```

> 關於解法…
> 雖然說 this 有可能會無預警的失去了原先預期綁定的 this 的值，
> 但我們還是可以經由一些方法強制綁定，例如，使用 ==call、apply、bind==，
> 明確指出要綁定給 this 的物件，又或者，
> 可使用[軟綁定](https://)當 this 退化為全域物件時就給予預設值。

## 明確綁定（Explicit Binding）

使用 call、apply、bind，明確指出要綁定給 this 的物件。

### call

將第一個參數設定為函式內的 context，意即設定第一個參數為函式內 this 的值。
與 apply 的差異只在於傳參數的方法 - call 將參數一一傳入，而 apply 將參數使用陣列傳入。

```javascript=
let cat = {
  name: 'Doraemon',
};

let dog = {
  name: 'shiba',
};

function sayHi(num) {
  console.log('Hello, I am ' + this.name);
  console.log('My number is ' + num);
}

sayHi.call(cat, '1');
sayHi.call(dog, '2');

// console

'Hello, I am Doraemon';
'My number is 1';
'Hello, I am shiba';
'My number is 2';
```

### apply

```javascript=
let cat = {
  name: 'Doraemon',
};

let dog = {
  name: 'shiba',
};

function sayHi(args) {
  console.log('Hello, I am ' + this.name);
  console.log('My number is ' + args[0]);
}

sayHi.apply(cat, ['1']);
sayHi.apply(dog, ['2']);

// console

'Hello, I am Doraemon';
'My number is 1';
'Hello, I am shiba';
'My number is 2';
```

### bind (常用)

在執行函式前，綁定要指定的物件，這樣 this 就會是這個物件。

```javascript=
let cat = {
  name: 'Doraemon',
};

let dog = {
  name: 'shiba',
};

function sayHi() {
  console.log('Hello, I am ' + this.name);
}

sayHi.bind(cat)(); // "Hello, I am Doraemon"
sayHi.bind(dog)(); // "Hello, I am shiba"
```

或

```javascript=
var obj = {
  msg = 'Hello!',
}

setTimeout(function() {
  console.log(this.msg);
}.bind(obj), 2000);
```

### 硬綁定（Hard Binding）

硬綁定是指使用 ==bind== 寫死要綁定的物件，可避免函式呼叫時退回到預設綁定。

如下，這裡有一個簡易的綁定 this 的 helper，用來寫死要綁定的物件 obj。

```javascript=
function today(day) {
  console.log(this.todayNumber.day);
  return this.todayNumber + day;
}

// 簡易的綁定 this 的 helper
function bind(fn, obj) {
  return function () {
    return fn.apply(obj, arguments);
  };
}

var obj = {
  todayNumber: 2,
};

var bar = bind(today, obj);
var b = bar(3);

switch (b) {
  case 3:
    console.log(b);
    console.log("Today is Wednesday");
    break;

  case 5:
    console.log(b);
    console.log("Today is  Friday");

    break;
  default:
    console.log("error");
}

// undefined
// 5
// Today is Friday
```

在`bind(today, obj)` 中，

1. 將 today 的 this 強制指定為 obj，並將結果指定給 bar，
2. 因此當執行 `bar(3)` 時，`this.todayNumber` 對 obj 查找屬性 todayNumber（找到為 2，並非退回到全域範疇），
3. 且加上傳入的數字 3，
4. 而得到結果 b 為 5。

call、apply、bind 適用情境與方法，整理如下。

|              | bind                       | call                                                                                                    | apply                                                    |
| ------------ | -------------------------- | ------------------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| 適用狀況     | 函數在執行前先綁定物件做為 | context 較常變動的場景。依照呼叫時的需要帶入不同的物件作為該 function 的 this。在呼叫的當下就立即執行。 | 與 call 相同                                             |
| 傳參數的方式 | 代入指定的物件做為 context | 參數需要一個一個指定 func.call( context, arg1, arg2, … )                                                | 參數使用陣列傳入 func.apply( context, [ arg1, arg2, … ]) |

### API 呼叫的情境（API Call “Contexts”）

許多函式庫的函式都會提供一個參數作為綁定的物件，
這個參數通常稱為情境參數（context argument），
目的是讓開發者不必再使用 bind 來綁定 this 的值。

如下，forEach 傳入兩個參數，分別是要執行的 callback foo 和情境參數 obj，
因此 `console.log` 中的 this 就是 obj

```javascript=
function foo(el) {
  console.log(el, this.id);
}

var obj = {
  id: 'Michael',
};

[1, 2, 3].forEach(foo, obj); // 1 Michael  2 Michael  3 Michael
```

## new 綁定

this 會指向 new 出來的物件。

```javascript=
function myName(name) {
  this.name = name;
  this.sayHi = function () {
    console.log("Hi, I am " + name);
    console.log(this === handsomeGuy);
  };
}

let handsomeGuy = new myName("Michael");

handsomeGuy.sayHi();
// "Hi, I am Michael"
// true
```

## 總結

如何利用以上的規則決定 this 的值呢？規則套用的優先順序，由高至低排列如下

- new 綁定
- 明確綁定
- 隱含綁定
- 預設綁定

## 軟綁定(Soft Binding)

當 this 退化成全域物件時，是否可給定預設值？

硬綁定可避免函式呼叫時不小心退回到預設綁定狀態，
但也減低了設定 this 的值的彈性。

因此，這裡提出一個解法，讓函式能經由隱含綁定或明確綁定的方式設定 this 的值，
而當 this 退化成全域物件時，又能給予一個預設值而非全域物件，
這種不寫死而動態設定預設值的方式，稱之為「軟綁定」。

可以建立一個工具來達到軟綁定的目的:
若 this 是 global、window 或 undefined 就給予預設值。

:bug: ==但範例尚未實作成功==

> 之後回來補上

## 語彙的 this（Lexical this）

所謂的「語彙的 this」是指 this 的值不適用於以上提到的四種規則來做判斷，而是回歸到[語彙範疇](https://ithelp.ithome.com.tw/articles/10206984)的查找，
this 的值並非源自執行時的綁定，
而是定義時包含它的範疇或全域範疇，是無法被覆寫的，
這裡即將要提到的用箭頭函數（arrow function） 來綁定 this 的值就是這樣的狀況。

### 範例

```javascript=
var name = 'Apple';
var obj = {
  name: 'Michael',
  sayHi: function() {
    console.log(`Hi, I am ${this.name}`);
  },
};

obj.sayHi(); // Hi, I am Michael
setTimeout(obj.sayHi, 1000); // Hi, I am Apple
```

其中，我們可以看到 `obj.sayHi()` 印出預期的「Hi, I am Michael」，
但 `setTimeout(obj.sayHi, 1000)` 卻因為上面提過的隱含的失去中的==函式是另一個函式==的參考而失去了原先 this 的綁定。

先來談一些常用的改變 this 的方法…

透過變數儲存目前 this 的值。
使用 bind、call 或 apply，綁定特定的物件作為 this 的值。
透過變數儲存目前 this 的值…這其實不算是「改變」，只能說是「保留」。如果希望存取到外部的 this，可用一個變數 `_this` 儲存起來，稍後再用。

修改上面範例如下，一秒後的確是印出「Hi, I am Michael」。

```javascript=
var obj = {
  name: 'Michael',
  sayHi: function() {
    var _this = this;

    setTimeout(function() {
      console.log(`Hi, I am ${_this.name}`);
    }, 1000);
  },
};

obj.sayHi(); // Hi, I am Michael
```

當然我們也可以用 bind、call 或 apply 來綁定特定的物件作為 this 的值。關於 bind、call 或 apply 的範例可參考上方提過的==明確綁定==的部份。

修改上例如下，一秒後的確是印出「Hi, I am Michael」。

```javascript=
var obj = {
  name: 'Michael',
  sayHi: function() {
    setTimeout(
      function() {
        console.log(`Hi, I am ${this.name}`);
      }.bind(this),
      1000,
    );
  },
};

obj.sayHi(); // Hi, I am Michael
```

### 箭頭函數快速綁定

既然箭頭函數會自動綁定所在範疇，那也就可以這麼修改了…經由箭頭函數就會把 this 綁在 obj 上。

```javascript=
var obj = {
  name: 'Michael',
  sayHi: function() {
    setTimeout(() => {
      console.log(`Hi, I am ${this.name}`);
    }, 1000);
  },
};

obj.sayHi(); // Hi, I am Michael
```

:imp: 但箭頭函數並不是一個所有狀況都適用的超級無敵通用解…

箭頭函數不適用於…

- 箭頭函數會將 this 強制綁定為執行環境。因此，若不希望 this 被綁定為執行環境，基本上都是不適用的，不需要為了少寫幾個字而硬要使用箭頭函數。
- 箭頭函數內的 callback 是匿名的，匿名函式的缺點請看[這裡](https://cythilya.github.io/2018/10/19/function-vs-block-scope/#匿名-vs-具名anonymous-vs-named)。

更多關於箭頭函式的 this，可參考[這裡](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Functions/Arrow_functions#this_不分家)。

## 參考文章

- [What’s THIS in JavaScript ? [上]](https://kuro.tw/posts/2017/10/12/What-is-THIS-in-JavaScript-上/)
- [What’s THIS in JavaScript ? [中]](https://kuro.tw/posts/2017/10/17/What-s-THIS-in-JavaScript-中/)
- [What’s THIS in JavaScript ? [下]](https://kuro.tw/posts/2017/10/20/What-is-THIS-in-JavaScript-下/)
- [你懂 JavaScript 嗎？#16 this](https://cythilya.github.io/2018/10/23/this/)
- [Day16 - 語彙範疇](https://ithelp.ithome.com.tw/articles/10206984)
