---
title: Underscore.js 常用方法總結
description: Underscore.js 是一個很精幹的資料庫，"壓縮後只有4KB!!"，它提供了幾十種函數語言程式設計的方法，大大方便了 Javascript 的程式設計，MVC 框架 backbone.js 就是基於這個庫。
date: 2021-03-20
categories:
- JavaScript
tags: 
- JavaScript
---

# Underscore.js 常用方法總結

## 概述

Underscore.js 是一個很精幹的資料庫，**壓縮後只有4KB**。
它提供了幾十種函數語言程式設計的方法，大大方便了 Javascript 的程式設計。
MVC 框架 backbone.js 就是基於這個庫。

它定義了一個下劃線 物件，函式庫的所有方法都屬於這個物件。
這些方法大致上可以分成：
1. 集合（collection）
2. 陣列（array）
3. 函式（function）
4. 物件（object）和工具（utility）五大類。

## 安裝環境
### node.js下安裝

Underscore.js 不僅可以用於瀏覽器環境，還可以用於 node.js。安裝命令如下：
複製程式碼 程式碼如下:

`npm install underscore`

但是，node.js 不能直接使用 `_` 作為變數名，因此要用下面的方法使用 underscore.js。
複製程式碼 程式碼如下:
```javascript=
var u = require(“underscore”);
```

### CDN 引入

```javascript=
<script src="https://cdnjs.cloudflare.com/ajax/libs/underscore.js/1.12.0/underscore-min.js" integrity="sha512-BDXGXSvYeLxaldQeYJZVWXJmkisgMlECofWFXKpWwXnfcp/R708nrs/BtNLH5cb/5TE7aeYRTDBRXu6kRL4VeQ==" crossorigin="anonymous"></script>
```

## method
與集合有關的方法

Javascript 語言的資料集合，**包括兩種結構：陣列和物件**。以下的方法同時適用於這兩種結構。

- `map()`

該方法對集合的每個成員依次進行某種操作，將返回的值依次存入一個新的陣列。
複製程式碼 程式碼如下:
```javascript=
// array
_.map([1, 2, 3], function(num){ return num * 3; });  // [3, 6, 9] 

// object
_.map({one : 1, two : 2, three : 3}, function(num, key){ return num * 3; });  // [3, 6, 9]
```

- `each()`

該方法與map類似，
依次對集合的每個成員進行某種操作，但是不返回值。
複製程式碼 程式碼如下:

```javascript=
// array
_.each([1, 2, 3], alert);    

// object
_.each({one : 1, two : 2, three : 3}, alert);
```

- reduce

該方法依次對集合的每個成員進行某種操作，然後將操作結果累計在某一個初始值之上，全部操作結束之後，返回累計的值。

該方法接受三個引數。第一個引數是被處理的集合，第二個引數是對每個成員進行操作的函式，第三個引數是累計用的變數。

```javascript=
// array
_.reduce([1, 2, 3], function(memo, num){ return memo num; }, 0);  // 6

// object
_.reduce({one : 1, two : 2, three : 3}), function(num, key){ return }
```


reduce方法的第二個引數是操作函式，它本身又接受兩個引數，第一個是累計用的變數，第二個是集合每個成員的值。