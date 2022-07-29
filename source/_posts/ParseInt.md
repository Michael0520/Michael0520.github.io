---
title: JavaScript ParseInt 
description: 將"字串"轉為整數
date: 2021-03-25
categories:
- JavaScript
tags: 
- JavaScript
---


# ParseInt 
將"字串"轉為整數

    parseInt(string,radix(進位));


**string**
* parseInt() 函數可解析一個字串，並返回一個整數。 


**radix**

* 當參數 radix 的值為 0，或沒有設置時，parseInt() 會根據 string 來判斷 radix 的基數。
* 如果string 以 1 ~ 9 的數字開頭，parseInt() 將把它解析為十進制的整數。
* 如果string 以 “0x” 開頭，parseInt() 會把 string 的其餘部分解析為十六進制的整數。
* 如果string 以 0 開頭，那麼 ECMAScript v3 允許parseInt() 的一個實現把其後的字符解析為八進製或十六進制的數字。



**特性**

* 只有字串中的第一個數字會被返回。
* 開頭和結尾的空格是允許的。
* 如果字串的第一個字符不能被轉換為數字，那麼 parseInt()會返回 NaN。
* 在字符串以 “0” 為開始時舊的瀏覽器默認使用八進制。ECMAScript 5，默認為十進制。


```javascript=
parseInt("10")           // 10
parseInt("10.33")        // 10
parseInt("34 45 66")     // 34
parseInt(" 60 ")         // 60
parseInt("40 years")     // 40
parseInt("He was 40")    // NaN
parseInt('010')          // 10
parseInt(010)            // 8 開頭為 0 的 Number 型別會被當作八進制帶入 (參考補充)

parseInt("10",10)        // 10
parseInt("010")          // 10
parseInt("10",8)         // 8
parseInt("0x10")         // 16
parseInt("10",16)        // 16
```