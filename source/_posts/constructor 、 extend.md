---
title: JavaScript constructor 、 extend
description: 一個 class 只能有一個稱為 constructor 
date: 2020-12-08
categories:
- JavaScript
tags: 
- JavaScript
---

###  constructor

> 一個 class 只能有一個稱為 constructor 

###  extends

> extends 關鍵字可用於建立一個自訂類別或內建類別的子類別。
> 
> 其繼承之原型 .prototype 必須是 Object 或 null。



```javascript=
class Square extends Polygon {
constructor(length) {
        // 我們在這裡呼叫了 class 的建構子提供多邊形的長寬值
super(length, length);
        // 注意：在 derived class 中，super() 必須在使用 this 以前被呼叫。不這樣的話會發生錯誤。
this.name = 'Square';
      }

get area() {
    return this.height * this.width;
      }

set area(value) {
    this.area = value;
      } 
    }
```