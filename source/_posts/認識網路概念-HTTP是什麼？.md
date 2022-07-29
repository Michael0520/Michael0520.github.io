---
title: 認識網路概念 - HTTP 是什麼？
date: 2021-04-15 15:39:41
description: 超文本傳輸協定 (HTTP) 是一種用來傳輸超媒體文件 (像是HTML文件) 的應用層協定，被設計來讓瀏覽器和伺服器進行溝通，但也可做其他用途，HTTP 遵循標準客戶端—伺服器模式，由客戶端連線以發送請求，然後等待接收回應。
categories:
- Backend
tags:
- Backend
---

超文本傳輸協定 (HTTP) 是一種用來傳輸超媒體文件 (像是HTML文件) 的應用層協定，
被設計來讓瀏覽器和伺服器進行溝通，但也可做其他用途，
HTTP 遵循標準客戶端—伺服器模式，由客戶端連線以發送請求，然後等待接收回應。

HTTP 是一種無狀態協定，意思是伺服器不會保存任兩個請求間的任何資料 (狀態)，
儘管作為 TCP/IP 的應用層，HTTP 亦可應用於其他可靠的傳輸層 (例如 UDP)，只要不會無聲無息地遺失訊息即可。

## 何謂傳輸協定？

舉一些常見的使用案例，分別介紹不同的傳輸協定：
- 國高中時期，玩魔獸爭霸時，有人會負責開房，其他玩家則要連到他的電腦進行遊戲，這則是使用網路傳輸協定 (Internet Protocol) ，簡稱 IP 連線。
- 日常收發電子郵件，如 Gmail，則是使用簡易郵件傳輸協定 (Simple Mail Transfer Protocol)，簡稱 SMTP 。

網路文件交流，如同每天連線到 Facebook 瀏覽社群資料，這則是使用超文本傳輸安全協定 (Hypertext Transfer Protocol Secure)，簡稱 HTTPS ，而他也建立在 HTTP 的基礎上，不過多了更安全的 SSL/TLS 來加密封包資料。

## 隨手可得的網頁 HTTP 內容

隨意打開一個網頁，再從 DevTools 中選擇 Network 頁面，再重新整理網頁，則會跑出許多的項目內容，這都是從伺服器端回傳過來的資源，代表不同的檔案資源（如下圖紅色框內的檔案）。
接著，我們可以點選任一個項目，選擇 Headers 面板，即可查看這筆 Request / Response 裡 HTTP 的詳細資訊。（如下圖橘色框內的資料）。

![](https://i.imgur.com/iEVJ9nC.png)

## HTTP 的組成結構


看過上面的小範例之後， 接下來讓我們仔細介紹 HTTP 的組成結構，分別是 HTTP Request 與 HTTP Response 這兩個大項目，如下圖。

![HTTP 的組成結構（左側為 Request，右側為 Response）](https://i.imgur.com/kVB93H4.png)
> HTTP 的組成結構（左側為 Request，右側為 Response）

### HTTP Request

從客戶端發出 HTTP Request 時，通常會定義以下的資訊，以瀏覽 Google 首頁為例

![HTTP Request 所定義的資訊內容
](https://i.imgur.com/YvNFxCo.png)

> HTTP Request 所定義的資訊內容

讓我們透過日常的郵政系統來比喻，
假如我們今天要寄出一封信件，若我們選擇 ［ GET ］掛號的寄件方式（Method），而地址（URL）是 Google 首頁（www.google.com）， Message Body 則會是信件內容。


上述的內容代表我們要對 www.google.com 做一個［ GET ］的動作，而常見的 Method 方法如下：

- GET：讀取資料
- POST：新增資料（常搭配 form 標籤使用）
- PATCH：修改資料
- PUT：修改資料（若該筆資料不存在，則自動新增資料）
- DELETE：刪除資料

通常一個 Method 會搭配一個 URL，也會對應伺服器端一組特定的資源，而 Message Body 的內容則取決於每次的動作。

若單純是使用 GET 方法瀏覽網頁，則 Message Body 為空，
但是，若以填寫表單為範例，那客戶端就會送出資料，這筆資料就會被傳送到伺服器的資料庫，
此時，我們則會使用 POST 方法將資料送進 Message Body，提交給某個指定的 URL，進而建立資料或更新資料。

### HTTP Response

從伺服器端回傳 HTTP Response 時，通常會定義以下的資訊，以瀏覽 Google 首頁為例。

![HTTP Response 所定義的資訊內容](https://i.imgur.com/B1E35Cx.png)
> HTTP Response 所定義的資訊內容

狀態碼 (status code) 對於一般人來說可能有些陌生，但想必你一定看過 404 Error 的訊息，這就是一種狀態碼的呈現，也是客戶端與伺服器端溝通的狀態情況。

前端開發上時常會看到以下常見幾種狀態碼，不僅有助於我們瞭解網路發生問題的原因，如：

- 1XX 訊息類 (收到請求，請求者繼續執行操作)
- 2XX 成功類 (操作被成功接受並處理)，例如：200 成功回應
- 3XX 重定向類 (需進一步操作才能完成)，例如：301 成功轉向
- 4XX 客戶端錯誤類 (請求語法錯誤或無法完成請求)，例如：404 找不到資源
- 5XX 伺服器錯誤類 (後端的問題)，例如：500 伺服器錯誤

更多狀態碼的資料可參考  [HTTP狀態碼列表](https://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81)。

此外， content-type 這個項目，它則會定義回應格式，例如 text/html、text/plain 或 application/json 等等，客戶端才會知道該如何打開訊息，而 Response Body 通常會是一個一個的程式碼檔案，最終，渲染畫面給使用者看。

## 參考文章


- [HTTP MDN](https://developer.mozilla.org/zh-TW/docs/Web/HTTP)
- [何謂 HTTP 傳輸協定-皮爾斯的自學旅程](https://medium.com/pierceshih/%E7%AD%86%E8%A8%98-%E4%BD%95%E8%AC%82-http-%E5%82%B3%E8%BC%B8%E5%8D%94%E5%AE%9A-1d9b5be3fd24)