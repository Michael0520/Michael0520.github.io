---
title: JavaScript Control & Loop
description: 控制判斷與迴圈。
date: 2021-07-23
categories:
- JavaScript
tags: 
- JavaScript
---


# Control & Loop（控制判斷與迴圈）

var 會產生全域問題, 所以都改用 es6 的 let,const

## Control Flow

JavaScript 用來控制流程的「條件語法」指的是，當指定的條件為 true 時，就會執行後續所指定的指令。 而 JavaScript 的條件語法有兩種︰ if…else 和 switch。


### if..else

如同字面上，如果指定條件為true就執行某件事，否則else就做另一件事。

```javascript=
if (指定條件) {
  陳述式 1;
} else {
  陳述式 2;
}
```

如果有多個不同的條件也可以藉由 else if 來使用複合的陳述式來測試，如下：

```javascript=
if (指定條件1) {
  陳述式 1;
} else if (指定條件 2) {
  陳述式 2;
} else if (指定條件 n) {
  陳述式 n;
} else {
  最後陳述式;
}
```
---
### switch

```javascript=
switch (expression) {
  case value_1:
    statements_1
    [break;]
  case value_2:
    statements_2
    [break;]
    ...
  default:
    statements_def
    [break;]
}
```

例子：
```javascript=
switch (i) {
  case 1:
    alert("i = 1");
    break;
  case 2:
    alert("i = 2");
    break;
  case 3:
    alert("i = 3");
    break;
  default:
    alert("i > 3 or i <= 0");
    break;
}
```
如果變數 i 的值 1，則執行 case 1 區塊的程式碼，以此類推;如果都不在指定的 case 裡面，則會執行 default 區塊的程式碼。

關鍵字 break
當 JavaScript 執行到 break 這個關鍵字的時後，就會直接跳出整個 switch 區塊，繼續往下執行。
如果沒有break，程式會從符合的 case 區塊開始一路往下執行，直到遇到 break 為止。

相較來說 switch 得效能比較好一些

* if…else 會先判斷後再執行
* switch 一定會執行，但還是會先比對 case

---

## Loop

迴圈(loop)指的是，想要重複做某件事情，數值則會依次數而有遞增或遞減的變化來完成結束的條件。
主要分為

* for
* while
* do..while


### for

直接看例子:

```javascript=
for (let i = 0; i < 5; i++) {
  console.log(i);
}
```

先定義初始值 `let i=0`
然後`i < 5`是結束條件，意思就是如果 i 大於等於 5 就會結束。
`i++`為結束每一回合時變動，意思就是`i = i + 1`。

### 用 for 迴圈做加總

從陣列中取出資料，並使用 for 迴圈做加總。

用人物資訊來做練習，
```javascript=
var person = [
  {
    name: "Tim",
    age: 20,
    height: 200,
    gender:boy,
  },
  {
    name: "Mary",
    age: 17
    height: 150,
    gender:girl,
  },
  {
    name: "jessica",
    age: 18,
    height: 150,
    gender:girl,
  },
];

var personTotal = person.length; //先抓取幾個人
console.log(personTotal); //結果會得到 3 人，3 份資料

var ageTotal = 0; //先預設數量為 0
for (var i = 0; i < personTotal; i++) {
  //從第一個開始迴圈；在人數內條件；加總總值
  ageTotal += ((person[i].age)%3); //
}

console.log("今年的平均年齡為: " + ageTotal);
```
---

### while

while 基本上概念與 for 是相同的，看下面兩格結果是相同的例子

```javascript=

// for
for (let i = 0; i < 5; i++) {
  console.log(i);
}

// while
let i = 0;
while (i < 5) {
  console.log(i);
  i += 1;
}
```

`while` 的做法是 `while`(條件){行為}，上面的例子 `i < 5` 是條件，每一次的行為是印出 i 後再讓 `i+1` ，之後當 `i = 4` 這次行為結束後 `i+1` 變成 5 ，下一次開始判斷條件就不符合，迴圈即終止。

兩者相較

`while` 是控制條件的變數在迴圈開始前即存在，迴圈開始後只會定義條件，不會去初始化參數，大多數用在迴圈執行次數『不確定』的時候。
`for` 則在迴圈一開始就定義變數，大多數用在迴圈次數『明確』的狀態。

### do...while

do…while 則是跟 while 幾乎一樣，只是 do…while 可以確保迴圈的第一次行為被執行。

```javascript=
// do...while
let i = 0;
do {
  console.log(i);
  i += 1;
} while (i < 5);
```

**迴圈操作**

break 與 continue 是迴圈中兩種特別的指令

* break
會直接中斷跳離迴圈。
* continue
會讓迴圈跳過這一次的行為繼續執行下一次的迴圈。

Break 例子：如果找到所要的東西，就停止迴圈

```javascript=
while (true) {
  const result = foo();
  if (result == "find it") {
    console.log("找到了，結束迴圈");
    break;
  }
}
```
Continue 例子：假設想要印出 1 ~ 10的數字 ，但是不包括 3 的倍數。

```javascript=
for (let i = 1; i <= 10; i++) {
  // i 能被 3 整除表示 i 是 3 的倍數，遇到 continue 就會跳過這次
  if( i % 3 === 0){
    continue;
  }
  console.log(i);
}
```


## 迴圈應用 - 99乘法表

利用迴圈來印出九九乘法表的結果
這是用到nesting for loops的方式

### for 迴圈

```javascript=
for (var i=1; i < 10; i++) {
    for (var j=1; j < 10; j++) {
        console.log(i + "x" + j + " = " +  i * j)
    }
}
```

### while 迴圈
```javascript=
var i = 1;
while (i < 10) {
    var j = 1;
    while (j < 10) {
        console.log(i + " x " + j + " = " + i * j);
        j++;
    }
    i++;
}
```


### do…while 迴圈
```javascript=
var i = 1;
do {
    var j = 1;
    do {
        console.log(i + " x " + j + " = " + i * j);
        j++;
    }while (j < 10);
    i++;
}while (i < 10);
```

Demo:[ 99 乘法表以及 for迴圈練習](https://codesandbox.io/s/chengshichai-for-huiquan-fc735?file=/all.js)

---
## foreach


```javascript=
// for 

var array = ['小明', '杰倫', '漂亮阿姨', '小美']
for (var i = 0; i < array.length; i++) {
  const item = array[i];
  console.log(i, item);
}
```

```javascript=
// foreach

var array = ['小明', '杰倫', '漂亮阿姨', '小美']
array.forEach(function(item, i) {
  console.log(i, item)
});

//es6寫法

var array = ['小明', '杰倫', '漂亮阿姨', '小美']
array.forEach((item,i) => {
  console.log(i,item)
})
```

---
## 展開符號 … , arg

展開符號能夠把"陣列"與"類陣列"裡的內容給取出來。
以下說明展開符號的幾個用途。
```javascript=
let groupA = ['小明', '杰倫', '阿姨'];
let groupB = ['老媽', '老爸'];

let groupAll = [...groupA, ...groupB];
console.log(groupAll);
    // ['小明', '杰倫', '阿姨','老媽', '老爸']
    
```
## for...in 迭代 物件(arr)
語法：for (const value of arr){}


```javascript=
let iterable = [3, 5, 7];

// 回傳「key」
for (let i in iterable) {
  console.log(i); // "0", "1", "2"
}

// 回傳「value」
for (let i of iterable) {
  console.log(i); // 3, 5, 7
}
```



## for...of 迭代 物件(object)

語法：for (const key of arr){}

```javascript=
// 內層為陣列類型時
let arr = [
    [1, 2, 3],
    [4, 5, 6],
    ['Hello', 'world']
];

for (let [x, y, z] of arr) {
    console.log(x, y, z);
}
// 1, 2, 3
// 4, 5, 6
// 'Hello', 'world', undefined

// 內層為物件類型時
let family = [
    {name: 'ES6', type: 'JavaScript'},
    {name: 'for', type: 'Iterator'}
];

for (let {name, type} of family) {
    console.log(name + ': ' + type);
}
// 'ES6: JavaScript'
// 'for: Iterator'
```

## map() 映射

語法: .map()

回傳會是一個 list



    
## .filter() 保留

語法: .filter()

回傳會是一個 list


