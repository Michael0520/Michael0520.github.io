---
title: 'JavaScript - Promise & async , sync'
description: 再次複習 Promise 以及 async , sync 修正過去的學習錯誤
date: 2021-07-07
categories: 
- JavaScript
tags: 
- JavaScript

---

async 與 await 是 JavaScript 中常見的東西，其中也與 Promise 也有關係，所以這邊也會先講一下 Promise 是什麼。

    簡單來講 Promise 就是彼此承諾一件事情，絕對不能違背約定！

![image](https://i.imgur.com/4U8oy4h.png)

## 非同步與同步事件簡介

首先到底非同步與同步事件是什麼東西呢?
JavaScript 是單進程的程式語言(意旨一次只能做一件事情)

### 同步事件

舉例來講 JavaScript 就像下廚差不多，以同步 (async) 來講，
顧客事件就像我要一定要先 :
先切菜 → 再切香菇 → 然後倒高湯 → 最後一定是上菜。

![image](https://i.imgur.com/9xT5arl.png)

### 非同步事件

那非同步呢?
做菜過程除了最後上菜之外，難道我們就一定要先切菜 → 再切香菇 → 然後倒高湯嗎?
不一定!
我們可以先`切香菇或者先到高湯又或者在最後才切菜`等等，
簡單來說就是我們可以先做其他可以先做的事情，然後其他事情不會受到影響。

那剛剛前面有講到 JavaScript 是單進程程式語言，
那他又是如何處理非同步事件的?
在 JavaScript 中，他會先將應該要先處理的東西先處理完，
然後再把需要做非同步處理的事情放進一個叫做事件佇列，又稱事件對列中，
直到前面應該先處理完的事情處理完後再看事件佇列有什麼是準備要做的。

## Promise 是什麼？

我們都有這個經驗…在午餐時間、人滿為患的餐廳裡排隊等候點餐，
點餐完畢後，服務生給我們一個小圓盤，告知當小圓盤開始發光震動的時候，就可以來取餐了。

Promise 可說是這個小圓盤，
當先前承諾的工作完成時，就來通知我們「工作完成了！來進行下一步的任務吧」。

![image](https://i.imgur.com/euZ1Up5.png)

[圖片來源](blog_154bb619d0102wrzw)

### 語法

首先 Promise 是 ES6 新增的一個功能，所以必須使用函式來呼叫，常見的寫法就像這樣 :

```javascript
let newPromise = new Promise((resolve, reject) => {
  // resolve → 代表操作成功，並將值回傳回去
  // reject → 代表失敗，回傳錯誤訊息
})
```

一開始我們無法知道哪一個函式會先被執行完，但是我們又希望他可以照順序來運作，那就可以這樣子寫

```javascript
let runPromise = (name, time, status) => {
  return new Promise((resolve, reject) => {
    if(status) {
      console.log(`${name} 起跑了!`)
      return setTimeout(() => {
        resolve(`${name} 衝了 ${time / 1000}秒`)
      },time);
    } else {
     reject(new Error(`${name} 出現錯誤`));
    };
  });
};

// 小明失敗，就回傳錯誤訊息
runPromise('小明', 3000, false).then((res) => {
  console.log(res);
  
// 換小王，開始跑步
  return runPromise('小王', 1000, true)
}).then((res) => {
  console.log(res);
}).catch((error) => {
  console.log(error);
})

```

### 範例1

函式 add 傳入兩個參數 x 與 y，
回傳得到其相加的結果，如範例所示，`1 + 2` ，
理所當然的是得到 3。

```javascript
function add(x, y) {
  return x + y;
}

console.log(add(1, 2)); // 3
```

但若輸入的兩數，可能要經過冗長計算過程或從伺服器取得或是需要連接到 API ，而無法立即做運算呢？

```javascript
var a = fetchA(); // a 此時尚未取得，值是 undefined
var b = fetchB(); // 2

console.log(add(a, b)); // NaN
```

這樣就會得到 NaN ~~死去~~

> 備註：
> 做加法運算時，非數值的部份會被強制轉型，
> 意即 Number(undefined) 得到 NaN，強制轉型。

那…我們可以改為，等兩數都取到值了，再做相加運算嗎？當然可以。

```javascript
function fetchA(cb) {
  setTimeout(function() {
    // 模擬冗長運算
    return cb(1);
  }, 3000);
}

function fetchB(cb) {
  return cb(2);
}

function add(getX, getY, cb) {
  var x, y;

  getX(function(xVal) {
    x = xVal; // 得到 x
    y && cb(x, y); // 若 y 也取到了，就執行加法運算
  });

  getY(function(yVal) {
    y = yVal; // 得到 y
    x && cb(x, y); // 若 x 也取到了，就執行加法運算
  });
}

add(fetchA, fetchB, function(a, b) {
  console.log(a + b); // 加法運算，印出相加結果
});
```

函式 fetchA 模擬了必須經過冗長運算才能得到結果的狀況，函式 add 等待兩數皆取得結果時，就執行加法運算。

程式碼是不是有點複雜？要檢查 x 又要檢查 y 的！的確，在沒有 promise 的 ~~恐龍~~ 年代 ，
我們是這樣解決等候的問題。

但這樣寫真的太過複雜，看得都頭痛了，有 promise 之後，改寫上面的例子：

```javascript
function fetchA() {
  return new Promise(function(resolve, reject) {
    setTimeout(function() {
      // 模擬冗長運算
      resolve(1);
    }, 3000);
  });
}

function fetchB(cb) {
  return new Promise(function(resolve, reject) {
    resolve(2);
  });
}

function add(xPromise, yPromise) {
  // x 與 y 都取到了
  return Promise.all([xPromise, yPromise]).then(function(values) {
    return values[0] + values[1]; // 執行加法運算
  });
}

add(fetchA(), fetchB()).then(function(sum) {
  console.log(sum); // 印出相加結果
});
```

依舊使用

1. 函式 fetchA 模擬必須經過冗長運算才能得到結果的狀況，
2. 函式 add 彷彿拿了兩個小圓盤（xPromise 與 yPromise）等著取餐，
3. 等兩個小圓盤都發光震動了才去領餐點，也就是執行加法運算。

有 promise 的世界是不是文明多了！？比之前來得方便許多。

## 錯誤處理

承上，then 可接受兩個函式作為參數，

1. 第一個函式用於成功（resolve）時要執行的任務，
2. 第二個函式用於失敗（reject）時要執行的任務，失敗的原因可能是因為取得值的過程出錯或加法運算失敗等，
3. 當然還有一種遲遲未得到結果的延遲狀態（pending），稍後再討論。

```javascript
add(fetchA(), fetchB()).then(
  function(sum) {
    // fulfillment handler
    console.log(sum);
  },
  function(err) {
    // rejection handler
    console.error(err); // 印出錯誤原因
  },
);
```
