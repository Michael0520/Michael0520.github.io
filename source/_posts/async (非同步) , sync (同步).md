---
title: JavaScript async (非同步) , sync (同步)
description: 紀錄學習非同步過程。
date: 2020-12-10
categories:
- JavaScript
tags: 
- JavaScript
---

上篇[Promise](https://hackmd.io/2q-URsBTTOS3doStyuSTbw)
## 生活範例：
* async(非同步) : 
1. 去醫院掛號
2. 等護士叫，可以先去上廁所
3. 護士叫了，我在過去

* sync(同步) :
1. 去醫院掛號
2. 在櫃檯等，等到護士說好了
3. 我才能去上廁所


# 實作解析：
[撈取資料實作範例](https://codesandbox.io/s/hw2-function-mouxianwang-6904-zuoyejiexiforked-j70zb?file=/src/index.js)
另一個 Js 檔案(utils.js 是資料庫)
---
### try()catch() 捕捉錯誤

語法：
```javascript=
try (用鑰匙開門){

  小妹用自己鑰匙開自己房門成功
  
} catch(){

  小妹用哥哥鑰匙開自己房門失敗
}
```

```javascript=
// foo 透過 async 回傳會得到一個 foo()
// foo() 是一個 promise

const foo = async()=>{
    return {
    a:1,
    b:2
    }
}

// 1. promise 版本

foo().then((data)=>{
    
}).catch(error=>{

})



// 2. async 版本

async()=>{
    try {
        const data2 = await foo ()
    }catch(error){
        return(error)
    }
}
```





---
### 小叮嚀：
1. **.then().catch()是Promise的用法，
async 沒有 .then().catch()，
所以只好用 try() catch() 來捕捉錯誤**

2. **await(等待)，外層一定要有 async(非同步)包裹著**


---