---
title: JavaScript AJAX
description: 紀錄學習 AJAX 過程。
date: 2020-12-13
categories:
- JavaScript
tags: 
- JavaScript
---

## readyState
0 - 已經產生一個 XMLHttpRequest，但是還沒連結要撈的 資料，接著下 open 指法來設定環境（有三個參數）
1 - 用了open，但是還沒傳資料
2 - 偵測到你有用 send
3 - 資料 loading 中
4 - 你撈到資料了，數據已經接收到

## Get
格式，讀取網址，同步非同步
格式: get (讀取資料)，post (傳送資料到伺服器)

```javascript=
let xhr = new XMLHttpRequest();
xhr.open("get", "網址", false);
//空的資料
xhr.send(null);//空的資料
console.log(xhr.responseText);
```
## Post
```javascript=
var xhr = new XMLHttpRequest();
xhr.open('post','網址',true);
xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded");
xhr.send('email=xxxxx@gmail.com&password=xxx');
```
* **Post js 格式**
![](https://i.imgur.com/KfI4ZT3.png)
* **Post json 格式**
![](https://i.imgur.com/6AP3svI.png)



##  同步非同步
* true - 非同步，
資料不會傳回來，就讓程式繼續往下跑，等到回傳才會自動回傳
* false - 同步，
等資料傳回來，才會讓程式碼繼續往下跑通常使用true不必等到資料回傳才往下跑

demo:
https://codepen.io/michael-luo/pen/RwRyPOg?editors=1010



## http狀態碼
200 - 確定。 用戶端要求成功。
401 - 拒絕存取。 IIS 定義數個不同的 401 錯誤，以表示更詳細的錯誤原因。

更多：https://blog.miniasp.com/post/2009/01/16/Web-developer-should-know-about-HTTP-Status-Code

## Cors 

開了這個權限，其他開發者才能跨網域撈取資料。想知道某筆資料（JSON 或 API）有沒有開 CROS，可以上 test-cros.org 查詢。




