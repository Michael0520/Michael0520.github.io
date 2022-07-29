---
title: 學習基礎 Presudo Code
date: 2021-04-29 03:17:48
description: 虛擬碼的風格差異很大，有些會用數學表示法 (mathematical notation)，有些會用口語敘述，有些會接近真正的程式碼。沒有那一種風格是最好的，要看當下的需求來決定。
categories: 
- JavaScript
tags: 
- JavaScirpt
---

虛擬碼的風格差異很大，有些會用數學表示法 (mathematical notation)，有些會用口語敘述，有些會接近真正的程式碼。沒有那一種風格是最好的，要看當下的需求來決定。

學習虛擬碼就像學習程式語言，只要針對不同情境撰寫相對應的虛擬碼，再將其組合起來即可。一般來說，程式設計常見的情境如下：

- 宣告 (declaration)
- 指派 (assignment)
- 代數運算 (algebraic operations)
- 選擇 (selection)
- 迭代 (iteration)
- 函式 (function)
- 類別 (class)
- 陣列 (array)
- 集合 (collections)
我們只要針對這些情境撰寫相對應的虛擬碼，大概就可以抓到虛擬碼的寫法。學習其他人的虛擬碼也是用相同的要訣去拆解各種不同的情境即可。

## 學習重點

這次是挑選常用語法來實作

### LowerCase()

toLowerCase() 方法用來將字串中的英文字母都轉成小寫。

語法：

```javascript=
str.toLowerCase()
```

用法：

```javascript=
console.log('Hello World'.toLowerCase());
// 輸出 'hello world'
```
### UpperCase()

toUpperCase() 方法用來將字串中的英文字母都轉成大寫。

語法：

```javascript=
str.toUpperCase()
```

用法：

```javascript=
console.log('Hello World'.toUpperCase());
// 輸出 'HELLO WORLD'
```

### GetLastWord() 

取得輸入字串的最後一個字元

```javascript=
function GetLastWord(inputValue) {
  return inputValue.charAt(str.length - 1);
}
```


## 實作練習

[Page](https://michael0520.github.io/Presudo_Code_Practice/index.html)