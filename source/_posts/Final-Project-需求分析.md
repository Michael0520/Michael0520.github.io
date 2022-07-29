---
title: Final-Project 需求分析
date: 2021-09-28
description: 將 Final Project 規劃版面以及需求分析的紀錄。
categories:
- JavaScript
- 作品集
tags:
- JavaScript
- 作品集
---

## 進度 Update
5/17 週一 
- [x] 補看昨天直播影片 
- [x] 期末專題選題目 
  -  [租房網站](https://9floor.co/)
- [x] 開始進行需求分析 
  - 首頁輪播式照片 (swipper 套件)
  - 因為無會員登入功能，所以將預訂需求改為表單填寫，因此要做"表單驗證"功能
  - 搜尋功能
    - 城市搜尋(ex:台北市)
    - 房型搜尋(ex:四人房，雙人房)
---
## Data 排列
- 城市 city(Taipei)
    - 旅館名稱 hotelId(101)
      - 特色 feature(高樓)
        - memberId(A,B,C,D)
          - 房型 roomlist(套房)
          - 價格 dollars
          - 狀態 status (招募中 true,已招募 false)
---
## Pages 元件
每個 Page 固定有的元件
1. 左上方 `<LogoButton>`，`click()` 會回到 homePage
2. 頁面按照此排列渲染:
    - navbar 下拉式選單
        -   順序：Logo => Booking => About => Service
      - 動態麵包屑 => `click()` 麵包屑會到點選的分頁
    -  輪播 bannerSection( swipper 套件)
    - mainSection
    -  footer
---
## 需求
- homePage
    - bannerSection:
      - 進入頁面是滿版圖片
![](https://i.imgur.com/NZ85tbY.jpg)
      - `<h1>title` 下方有個 開始搜尋 `<button>` 可以跳轉到 bookingPage
      - mainSection (房件渲染):
      - 熱門物件 SecondBannerSeciton(swipper)- 
        >  JS 動態輪播更新，更新圖片以及內容文字:
        - 兩個 `<button>` 
          - 搜尋物件：跳轉到 https:/Booking/${memberId}
          - 服務詳情：跳轉到 servicePage
      - 一般物件 
        - 多類型 RWD 排列:
            - `<mediumSection class="col-sm col-large-2">`
            - `<smallSection class="col-sm-1 col-md-2 col-large-3">`
         - 基本資訊欄位:
           - 旅館名字：`${data.city.hotelId}`
           - 特色：`${data.city.hotelId.feature}`
           - 房型：`${data.city.hotelId.memberId.roomlist}`
           - 價格：`${data.city.hotelId.memberId.dollars}`
           - 狀態：`${data.city.hotelId.memberId.status}`
- serviesPage
    -  固定使用卡片樣式來渲染出所提供的服務內容 
![](https://i.imgur.com/CnwtRmr.png)

    -  footer 上方有個`<contactSection>` 跳轉到 表單驗證 Page
- aboutPage
    - 元件化組裝 ![](https://i.imgur.com/HdeFfPe.png)

- bookingPage
  - `<room-listSection>`
    - 跟 homePage 使用相同的 `<mainSection>`
  - `<room-filter>`
    > JS 判斷條件
    - 城市 `${data.city}`
    - 房型 `${data.city.hotelId.memberId.roomlist}`
    - 價格 `${data.city.hotelId.memberId.dollars}`