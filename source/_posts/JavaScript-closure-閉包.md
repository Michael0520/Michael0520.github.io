---
title: JavaScript closure 閉包
date: 2021-04-10 06:17:21
description: 閉包是函式記得並存取語彙範疇的能力，可說是指向特定範疇的參考，因此當函式是在其宣告的語彙範疇之外執行時也能正常運作。
categories:
  - JavaScript
tags:
  - JavaScript
---

# 閉包 closure

閉包是函式記得並存取語彙範疇的能力，可說是指向特定範疇的參考，因此當函式是在其宣告的語彙範疇之外執行時也能正常運作。

範例如下。

```javascript=
function foo() {
  var a = 2;

  function bar() {
    console.log(a);
  }

  return bar;
}

var baz = foo();

baz(); // 2
```

說明

- 函式能夠存取的範疇即是其被內嵌後往外推的範圍，例如 bar 被內嵌於 foo 之內，因此 bar 內變數可存取的範圍就是 foo 和全域範疇。因此，基於語彙範疇的變數查找規則，bar 內的 a 在自己的函式範疇內找不到定義的話，可往外層的範疇查找，於是在 foo 內找到了，得到 a 為 2。其中，`console.log(a)` 是執行 RHS 查找。
- JS 引擎的垃圾回收機制會釋放不再使用的記憶體，但閉包為了保留函式記得和存取其語彙範疇的能力，就會予以保留，不做記憶體回收。因此，**bar 仍保留指向 foo 的內層範疇的參考，這個參考就是閉包。**
- 最後，雖然 baz 位於 bar 所定義的範疇之外，但由於閉包的緣故，bar 仍能正常執行，而得到 a 的值。

閉包在 callback 上的應用尤其常見。如下所示， 在程式碼的最後一行 `wait('Hello, 閉包!');` 中傳入字串「Hello, 閉包!」給函式 wait 時，儘管 timer 已離開了所宣告的範疇之內，但仍保留了 timer 存取 wait 傳入參數的值的能力，而印出結果。

```javascript=
function wait(message) {
  setTimeout(function timer() {
    console.log(message);
  }, 1000);
}

wait('Hello, 閉包!');
```

閉包可說是仰賴語彙範疇來撰寫程式碼而得到的必然結果。

## 迴圈與閉包

如果今天要實作一個每秒依序印出數字 1, 2, 3, …, 5 的功能，你會怎麼做呢？

是這樣嗎？

```javascript=
for (var i = 1; i <= 5; i++) {
  setTimeout(function timer() {
    console.log(i);
  }, i * 1000);
}
```

> **這的確是錯誤的。**

由於 `console.log(i)` 中的 i 會存取的範疇是 for 所在的範疇（目前看起來是全域範疇，因為 var 宣告的變數不具區塊範疇的特性），

1. 當 1 秒、2 秒…5 秒後執行 `console.log(i)` 時，就會去取 i 的值，
2. 此時 for 迴圈已跑完，i 變成 6，因此就會每隔一秒印出一個「6」。

若希望每隔一秒印出 1、2、…5，可使用 IIFE 加入新的範疇來修改，意即為每次迭代都建立一個新的函式範疇（但其實我們想要的是建立一個區塊範疇）。

```javascript=
for (var i = 1; i <= 5; i++) {
  (function(j) {
    setTimeout(function timer() {
      console.log(j);
    }, j * 1000);
  })(i);
}
```

既然是要為每次迭代建立區塊範疇，更好的解法就是使用 let，
let 會在每次迭代時重新宣告變數 i，並將上一次迭代的結果作為這一次的初始值。

```javascript=
for (let i = 1; i <= 5; i++) {
  setTimeout(function timer() {
    console.log(i);
  }, i * 1000);
}
```

1. 情境題:

   判斷使用者 input 輸入值判斷是大還是小

```javascript=
function closureGo (x){
    // var x = 10
    return function hi(inputNumber){
        // console.log(x + inputNumber)
        if(x > inputNumber)
            console.log('Big')
        else(x < inputNumber)
            console.log('Small')
    }
}

    var user_1 = closureGo(20)
    // Small
    var user_2 = closureGo(50)
    // Big
```

2. 情境題:

   防止 var 全域變數汙染

```javascript=
    for (var i = 1; i < 10; i++){
        (function(i){
            setTimeout(function(){
                console.log("setTimeout i :",i)
            },1000)
        })(i);
    }
```

## 模組模式（Module Pattern）

模組模式（module pattern）又稱為揭露模組（revealing module），經由建立一個模組實體（module instance，如下範例的 foo），來調用內層函式 doSomething 和 doAnother。而內層函式由於具有閉包的特性，因此可存取外層的變數和函式（something 與 another）。透過模組模式，可隱藏私密資訊，並選擇對外公開的 API。

```javascript=
function CoolModule() {
  var something = 'cool';
  var another = [1, 2, 3];

  function doSomething() {
    console.log(something);
  }

  function doAnother() {
    console.log(another.join(' ! '));
  }

  return {
    doSomething: doSomething,
    doAnother: doAnother,
  };
}

var foo = CoolModule();

foo.doSomething(); // cool
foo.doAnother(); // 1 ! 2 ! 3
```

以上這個例子並不難理解，它等於就是本文開頭 foo、bar 和 baz 的變形而已。

模組模式的另一個變形是 singleton- 包上 IIFE，用於只想要產生單一實體的時候，修改上例如下。

```javascript=
var foo = (function CoolModule() {
  var something = 'cool';
  var another = [1, 2, 3];

  function doSomething() {
    console.log(something);
  }

  function doAnother() {
    console.log(another.join(' ! '));
  }

  return {
    doSomething: doSomething,
    doAnother: doAnother,
  };
})();

foo.doSomething(); // cool
foo.doAnother(); // 1 ! 2 ! 3
```

## 模組依存性載入器（Module Dependency Loader）

既然我們知道了怎麼撰寫模組，那麼，要怎麼管理多個模組呢？
像是在模組中引用其他模組時，可能會因程式碼放置的順序不對、產生相依性問題而導致出錯，該怎麼辦呢？

這裡提出兩個解法-使用模組依存性載入器或 ES6 模組，先來看前者。

模組依存性載入器或管理器（module dependency loader / manager）是指將模組定義的模式包裝成一個友善的 API。範例如下，這是一個簡單的模組依存性載入器。

```javascript=
var MyModules = (function Manager() {
  var modules = {};

  function define(name, deps, impl) {
    for (var i = 0; i < deps.length; i++) {
      deps[i] = modules[deps[i]]; // (1)
    }
    modules[name] = impl.apply(null, deps); // (2)
  }

  function get(name) {
    return modules[name];
  }

  return {
    define: define,
    get: get,
  };
})();
```

說明如下，在 Manager 這個 IIFE 裡面包含了一些變數和函式…

- 變數 modules 存放各個模組所公開的 API，例如：bar 的 hello、foo 的 awesome。
- 函式 define 輸入三個參數:
  1. name、deps 與 impl，name 是模組名稱；
  2. deps 是與此模組相依的模組，以陣列方式傳入；
  3. impl 是用於定義一個外層包裹函式以建立範疇，讓其內的函式能指向這個範疇而產生閉包，最後這個函式 impl 會回傳公開 API 。
  - 標註 (1) 的部份：deps 本來是儲存相依模組名稱的陣列，在這裡改為存放這個相依模組名稱的公開 API。例如：deps 的內容是 `['bar']，deps[0]` 的內容是 'bar'，因此`deps[0] = modules[deps[0]]`可看成是` bar = modules['bar']`，`modules[‘bar’]` 以物件方式儲存 bar 的公開 API，例如：hello 和 world，即是 `bar = modules['bar'] = {hello: ƒ, world: ƒ}`。
  - 標註 (2) 的部份：這裡為模組呼叫定義了一個包裹器函式，用來將回傳值（這個值是指模組的 API）存入以名稱來當作參考的一個模組清單。此模組 impl 會傳入兩個參數，第一個參數是這個函式所要使用的 this 的值，因為在這裡不用 this 所以傳入 null 也是可以的；第二個參數是將相依的模組（與其公開 API）都傳進去，讓這個模組能夠使用其他模組的公開 API。
- get 會依照輸入的模組名稱以物件形式取得其公開的 API，之後就可以指定給特定變數，然後利用這個變數使用存取屬性的方式呼叫這些 API。

以下是示範如何定義模組…關於模組 foo 與 bar，就依照以上規格分別定義之，即可使用這樣的模組依存性載入器管理多個模組了。

```javascript=
// bar 沒有需要任何其他的模組...
MyModules.define('bar', [], function barImpl() {
  function hello(who) {
    return 'Let me introduce: ' + who;
  }

  function world() {
    return 'Hello World';
  }

  return {
    hello: hello,
  };
});

// foo 需要 bar 模組...
MyModules.define('foo', ['bar'], function fooImpl(bar) {
  var hungry = 'hippo';

  function awesome() {
    console.log(bar.hello(hungry).toUpperCase());
  }

  return {
    awesome: awesome,
  };
});

var bar = MyModules.get('bar');
var foo = MyModules.get('foo');

console.log(bar.hello('hippo')); // Let me introduce: hippo

foo.awesome(); // LET ME INTRODUCE: HIPPO
```

這樣就可以要用什麼就指定什麼，不用擔心順序問題了。

## ES6 模組（ES6 Module）

![](https://i.imgur.com/UPtFWkg.png)

在 ES6 中可將個別載入的檔案視為一個模組，每個模組都能匯入（import）其他模組或指定特定的 API 成員，也能匯出（export）自己公開的 API 成員。而瀏覽器或 JavaScript 引擎會經由其內建的模組載入器匯入這個模組檔案。這些模組檔案的內容可視為被包覆在一個閉包內，當被另一個檔案引入和使用時即可在非原先語彙範疇定義處正常運作。

範例如下，
在 foo.js 中載入 bar module 的 hello，並用於其內的 awesome 中，以將結果字串轉為大寫；在 baz.js 載入 foo 與 bar 的完整模組，分別執行 `bar.hello` 與 `foo.awesome()`。

- bar.js

```javascript=
function hello(who) {
  return `Let me introduce: ${who}`;
}

export hello;
```

- foo.js

```javascript=
import hello from 'bar'; // 只會載入 bar module 的 hello

var hungry = 'hippo';

function awesome() {
  console.log(
    hello(hungry).toUpperCase()
  );
}

export awesome;
```

- baz.js

```javascript=
// 載入 foo 與 bar 的完整模組
module foo from 'foo';
module bar from 'bar';

console.log(
  bar.hello('rhino')
); // Let me introduce: rhino

foo.awesome(); // LET ME INTRODUCE: HIPPO
```

這樣就可以要用什麼就載入什麼，不用擔心同名、順序等問題。

注意！模組模式是以函式為基礎來實作的，因此其 API 是在執行時期才能被識別，
所以可在執行時期修改模組內的私有變數和函式；
而 ES6 的模組是靜態的，意即在**編譯時期而非執行時期被識別**，
因此可在編譯時檢查 API 是否存在而丟出錯誤訊息，並且無法在執行時修改模組內的私有變數和函式。

## 學到的知識點

看完這篇文章，我們到底有什麼收穫呢？藉由本文可以理解到…

- 閉包是函式記得並存取語彙範疇的能力，可說是指向特定範疇的參考，因此當函式是在其宣告的語彙範疇之外執行時也能正常運作。
- 迴圈與閉包搭配使用時的謬誤與陷阱。
- 模組模式可經由建立一個模組實體來調用內層函式，而內層函式由於具有閉包的特性，因此可存取外層的變數和函式。透過模組模式，可隱藏私密資訊，並選擇對外公開的 API。
- 利用模組依存性載入器或管理器或 ES6 模組來管理模組

## 參考文章

更多關於 ES6 模組可參考

- [Module 的语法
  ](https://es6.ruanyifeng.com/#docs/module)
- [Module 的加载实现
  ](https://es6.ruanyifeng.com/#docs/module-loader)
