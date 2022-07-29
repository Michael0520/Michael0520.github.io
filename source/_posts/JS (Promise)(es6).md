---
title: JavaScript (Promise)(es6)
description: 紀錄實作過的 Promise 應用以及結合 ES6 語法
date: 2020-12-10
categories:
- JavaScript
tags: 
- JavaScript
---

下篇筆記 [async(非同步),sync(同步)](https://hackmd.io/7Sn_JrQ2T7uD5HZhMFwdvg?both)

### ES5

```javascript=
// parameter 參數 (外部) foo
// argument 引數 (內部) (arg1,arg2)

function foo (arg1,arg2){
    return arg1+arg2
}
console.log(foo(1,2))
// 此 function 意思為
// 名字為 foo (的function) 裡頭會有兩個變數(arg1,arg2)
// 關鍵 return (回傳) 
// 會印出 1+2 = 3
```

### ES6 (arrow function)

```javascript=
const foo => (arg1,arg2){
    return arg1+arg2
}
console.log(foo(1,2))
```

> * #### setTimeout (延遲觸發 function)
> 
```javascript=
setTimeout(
    () => {
    console.log('in setTimeout')    
    },
    1000 //1000毫秒
)
```

### Promise( 承諾 )

> #### ( true 做什麼事情， false 做什麼事情)

> ### Promise 一寫完就會開始執行

**語法：**

```javascript=
const myPromise = new Promise((resolve,reject)
    const x=1
    if(x > 1){
        resolve('成功了')
    } else {
        reject(new Error('失敗了'))
        // new Error 存放失敗事件
    })
// 上方 Promise 一寫完就馬上會被執行
// resolve() true 做什麼事
// reject() false 做什麼事

myPromise.then().catch()
// then() true做什麼事情，又 true 就會再進到下個 then()
// 可寫無數個 then()
// catch() false 要做什麼事情
// catch() 做完事情，變成 true，就會再進到下個 then()

 .then((data)=>{ 
 // true 再進到下一個 then()
     return data+1
 })
 .then((data)=>{ 
     throw new Error()//拋出一個錯誤
         return data // 所以會到 catch
 })
.catch((error)=>{ 
// 執行完，變成 true 就再進到下個 then()
     return data-1
 })
.then((data)=>{
     return data+1
 })
```
---

### function 搭配 Promise

> ### (!important) function 被呼叫才會執行

> ### (!important) Promise 一寫完就會執行

```javascript=
const getMyPromise = (a,b) => new Promise ((resolve,reject) => {
    const x = a + b
    if(x > 0){
    resolve('成功了')
    } else {
        reject('失敗了')
    }
})

getMyPromise() //這樣 function 才會被呼叫
getMyPromise(1,2) // 1+2=3, x>0,return('成功了')
getMyPromise(1,-10) // 1+(-10)=-9,x<0,return ('失敗了')

```

---

## async (function return Promise 的簡寫)
 
> #### `async`(非同步) / `await`(等待)

```javascript=
const getMyNewPromise = async (a,b) =>{
    const x = a + b
    if(x > 0){
        return('成功！')
    } else{
        throw new Error('有錯誤！')
    }
}
getMyPromise() //這樣 function 才會被呼叫
getMyPromise(1,2) // 1+2=3, x>0,return('成功了')
getMyPromise(1,-10) // 1+(-10)=-9,x<0,return ('失敗了')


// 上述此 async function 意思是
// getMyNewPromise 裡有兩個數值 (a,b)
// const x = a + b
// if else , if (x > 0)
// 就會 return('成功')
// else 錯誤的話就會拋出一個錯誤顯示('有錯誤！')
```

### 上述 async 加上(await)寫法
> #### (async function)會傳一個 Promsie

引用情境：

```javascript=
const getMyNewPromise = async (a,b) => {
    
    try{
        const user = await getUser()
        } catch(error){
        
        }
        // try{} catch + (Promise) {} 語法
        // 如果發生錯誤，也會告知你是在發生了什麼錯誤，不會直接跳出發生錯誤
    
    const user = await getUser()
    
    const x = a + b
    if(x > 0){
        return('成功！')
    } else{
        throw new Error('有錯誤！')
    }
}
```

### callback (回調)

```javascript=
const bar = (a, b, successCallback, failureCallback) => 
    const x = a + b
    if( x > 0){
        successCallback('成功了')
    } else{
        failureCallback(new Error('失敗了'))
    }
}
bar(
    1,2,
    (data)=>{
        console.log('I am callback')
    },
    (error) => {
        console.log('I am callback')
    }.
)

// ＊＊等 arg1() 都執行好，在執行 bar() 即可
// 先定義好要用的 function
// 成功再來執行這個 function ，失敗再來執行這個 function


// ＊＊情境式解釋，要設定活動頁面裏廣告彈出的畫面，
// bar() 可以不需理會裡頭活動頁面(arg1)還要去執行什麼事情，
```

### 結論：(如何判斷 function 是否為 async)

**return 回來的話如果是一個 Promise 那就是 async
如果不是 Promise 那就是一般的 function**