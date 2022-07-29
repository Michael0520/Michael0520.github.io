---
title: (Project) Youtube Data API - Search Engine
description: 尋找以及創建 YouTube API
date: 2021-04-01
categories:
- JavaScript
- 作品集
tags: 
- 作品集
---



##  Create API key

ref : [Google Cloud Platform](https://console.cloud.google.com/?hl=zh-TW)

1. 確認有沒有專案repository


> 如果沒有要新建立一個專案

![](https://i.imgur.com/FWvuXjr.png)

2. 取用API & Services

- 選單中選取 API 和服務 (API & Services)
- 選擇資訊主頁 (Dashboard)  => 啟用 API 和服務 (Enable APIS & SERVICES)

![](https://i.imgur.com/CuuZG2C.png)


3. 選擇Youtube Data API v3 and 啟用(Enable)

![](https://i.imgur.com/KWSGIu3.png)

4. 新增憑證

- 啟用後進入到 Youtube Data API v3 的管理 (Manage) 頁面並選取憑證 (credentials)

![](https://i.imgur.com/pDEScwD.png)

- API 管理員中的「憑證」頁面 (Credentials in the API Manager)
- 建立憑證(Create credentials) => API key

![](https://i.imgur.com/d5nUZq8.png)

## How to use - Search Engine

### Example: Youtube Search Engine
Link: [YouTube API](/lLA1hRblTPirkVu6SvumlA?both)

### HTTP request

案例如下：


```javascript=
$.get("url",
    {
      part: "snippet, id",
      q: q, //輸入的關鍵字的值
      type: "video",
      key: "Your_API_key"
    },function(){...}
)
```

- part: 這個參數是為了避免大家呼叫 API 時得到太多不相關的資訊，所以用 part 來定義要取得的資料範圍。在 Search 的情況下，設定為 `part:snippet` 。
- snippet 帶有搜尋結果的資訊，頻道 title、id、描述、縮圖、時間等，id：則為影片搜尋結果本身的 id。
- q: 指操作者輸入的關鍵字區塊的值。
- type: 可以選在播放清單或是影片等類型。

官方文件：[Youtube Data API - Search List](https://developers.google.com/youtube/v3/docs/search/list)
查詢各種 request 的內容，也可以直接在上面設定 request 的項目來測試會收到什麼。

### Server Response

Resonpse 則為

![](https://i.imgur.com/NzCFFRW.png)

Response中的items(search Resource)

![](https://i.imgur.com/iSSBBiG.png)


官方文件：[Youtube Data API - Search Resource](https://developers.google.com/youtube/v3/docs/search#resource)

### prevPage & nextPage

可以在 `$.get`裡面的物件加上`{pageToken: token}`

```javascript=
$.get(
  "https://www.googleapis.com/youtube/v3/search",
  {
    part: "snippet, id",
    q: q, // 輸入關鍵字區塊的值
    pageToken:  token, // 需要是回傳的nextPageToken或prevPageToken字串
    type: "video",
    key: "Your_API_key"
  },
)
```

這邊的 token 是要帶回回傳資料中 nextPageToken 或 prevPageToken 的字串。
發出的 request 中要寫入 pageToken 的 request，在這個 callback function 中就可以利用 prevPageToken 跟 nextPageToken 的字串進行上下頁的切換。

###  Video information

發出的 request 中有 `part: 'snippet, id'`。
可以透過 search Resource 中的 snippet 獲得影片的發佈時間、 title、description、縮圖連結等。
也可以透過 id 來獲取種類、頻道、播放清單等的資訊。

![](https://i.imgur.com/Jl4kwyL.png)



## 參考資料

1. 官方資料
- [Getting-started](https://developers.google.com/youtube/v3/getting-started)
- [Search Lists](https://developers.google.com/youtube/v3/docs/search/list)
- [Search resources](https://developers.google.com/youtube/v3/docs/search#resource)

2. 網路資料
Request 中除了 part 參數跟其他的部分: https://ithelp.ithome.com.tw/articles/10194007