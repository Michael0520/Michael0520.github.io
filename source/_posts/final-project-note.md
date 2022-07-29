---
title: final_project_note
date: 2021-11-25 21:45:22
description: 這篇文章記錄最後專案遇到的問題
categories:
- 作品集
tags:
- 作品集
---

## 功能實作

使用者進入到搜尋頁面，透過右手邊的篩選欄位們，來依據自身需求，調節篩選的選項，取得最符合自身需求的租屋。

電腦版介面功能操作流程圖：

![實作 gif](https://i.imgur.com/C3RprtW.gif)

### 地區篩選

使用者可以透過切換地區，來呈現出對應的房屋資訊。
使用 [`Array.prototype.filter()` 語法]('https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/filter')，過濾資料取得篩選後的資料。

示意 GIF 圖：

![地區篩選流程 GIF](https://i.imgur.com/DiuJ2Fw.gif)

### 捷運篩選

使用者可以透過切換捷運線來呈現出對應的房屋資訊，
且會將對應的捷運站渲染出，達到進階篩選的效果。

    透過 object key & value 的方式，來成功達到點選該捷運線，會渲染出對應的捷運站

捷運 JSON 程式碼：

    ```json
    "MRTCodes": {
        "BL": "板南線",
        "O": "中和蘆洲線",
        "Y": "環狀線",
        "G": "松山新店線",
        "R": "淡水信義線",
        "BR": "文山內湖線"
    },
    "MRTStaions": {
        "Y": [
            "大坪林站",
            "十四張站",
            "秀朗橋站",
            "景平站",
            "景安站",
            "中和站",
            "橋和站",
            "中原站",
            "板新站",
            "板橋站",
            "新埔民生站",
            "頭前庄站",
            "幸福站",
            "新北產業園區站"
        ]
    },
    ```

- 捷運線渲染
  - 使用 Object.keys(object) 語法
  - 來取得 指定 object 的 keys 資料
  - HTML 程式碼：
        ```html
        <!-- v-for render MRT  -->
        <option
            v-for="(option,
            keys) in Object.keys(
                mrtCode
            )"
            :key="keys"
            :value="option"
        >
            {{
                mrtCode[option]
            }}
    </option>
    ```

- 捷運站渲染
  - 使用 changeMRTsLine function 將目前所選取的捷運線，該捷運線內的捷運站
  - 帶入到 捷運站 select 內。
  - HTML 程式碼：

        html:

        ```html
        <option
            v-for="(option,
            keys) in renderMRTsStation"
            :key="keys"
            :value="option"
        >
            {{ option }}
        </option>
        ```

        javascript:

        ```javascript
            // 將目前所選取的捷運線，該捷運線內的捷運站
            changeMRTsLine() {
                this.renderMRTsStation = this.mrtStation[this.selectedMRTsLine];
            },  
        ```

示意 GIF 圖：
![捷運篩選流程 GIF](https://i.imgur.com/ErTDIIx.gif)

### 價格篩選

使用者可以透過滑動滾動條的圓點，來切換要篩選的價格資料，
滾動條擁有兩個圓點，可以呈現出類似價格間距篩選的效果。

    使用套件 [Vue 3 Slider]('https://github.com/vueform/slider')，並且客製化樣式，成功顯示出滑動滾動條，能夠切換資料的效果。

#### format

使用 format 正則表達式，來讓房屋資訊，可以加上特定的數字位數，以及價格標誌，

建立 formatPrice function

- 由於 toFixed 語法，只能轉換數字，所以需要讓參數有個預設值 Number
- 取小數點後方最多二位數，`toFixed(2)`
- 正則表達式：
  - `.replace(/\)` 正則表達式開頭
  - 由於要讓房屋價格在千位數時，加上逗點作區隔，加上`d(?=(\d{3})+\.)/g`
  - 如果為空資料時，將不會顯示任何逗點或是價格標誌`.replace(/\.\d*/, "");`

完整程式碼：

![format 完整程式碼](https://i.imgur.com/4kYHuEi.png)

示意 GIF 圖：

![價格篩選流程 GIF](https://i.imgur.com/MGhWiTS.gif)

### 標籤篩選

使用者可以透過選擇多標籤(tags)，來篩選出擁有多重屬性的房屋資訊。

    使用 [Vue 3 form multiSelect 套件]("https://github.com/vueform/multiselect")，
    來實作多標籤(tags) 篩選的功能，並且加上客製化樣式，成功顯示出表單，能夠新增且刪除 tags 。

### 資料順序篩選

使用者可以透過切換順序顯示方式，來更動資料呈現的順序。

    透過 [array.sort]('https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/sort') 語法，來達到資料所有資料比對，更改為新的排列方式。

完整程式碼：

![資料順序 完整程式碼](https://i.imgur.com/leNZJCA.png)

示意 GIF 圖：

![資料順序篩選流程 GIF](https://i.imgur.com/DmptbbE.gif)

## 切版實作

模仿範例官網的特殊設計設計。

### NavBar 漢堡選單

更改至手機介面時，固定於頁面上方的選單，會變為圖案式的按鈕選單，
透過點擊事件，會切換樣式，達到動畫開關的效果，

- 開啟狀態時：顯示為滿版選單畫面。
- 關閉狀態時：切換為漢堡選單畫面。

        開啟狀態時：使用 `position:fixed` 效果，將選單定版在畫面上，
        透過 CSS 偽元素，來顯示出漢堡選單，漢堡的形狀，
        當點擊事件觸發時，同樣在觸發偽元素，切換 CSS 樣式，
        動畫效果則是使用 `transitionX: 45deg` 來水平移動。

- 流程示意 GIF 圖：
  - ![漢堡選單動畫＆滿版畫面](https://i.imgur.com/C4LuJDq.gif)

- 表單圖標從漢堡圖案轉變為叉叉圖案
  - 將圖標內容垂直翻轉，使用 `transform: translateY(100px);`，就可以完成此效果。
  - 漢堡圖案變化 GIF 圖：

![漢堡圖案變化 GIF](https://i.imgur.com/waKDvVn.gif)

### 破格式設計

- 兩側空白自適應調節寬度

    讓使用眼睛為之一亮的特殊設計。
    將兩側黃色區塊的 sider bar 寫死了寬度，
    使用了 `max-width:1280px` 做設定，達成畫面最大化限制內容呈現的效果，
    根據不同的畫面大小，都能讓畫面保持置中。

示意圖：
![特殊設計](https://i.imgur.com/yWLRJyu.jpg)

- 直式文字
    透過原生 CSS 屬性 `writing-mode: vertical-rl` 效果，來達成將文字改為直式排列。

![直式文字](https://i.imgur.com/oKNnxVn.png)

### 區塊元件化

    將同樣顯示的區塊，元件化組裝到頁面內，透過不同頁面的預設值，來做更動樣式。

![區塊元件化](https://i.imgur.com/wp5JJfK.png)

### RWD 設計

根據不同裝置呈現出適合的畫面。
桌機示意圖：
![桌機示意圖](https://i.imgur.com/XDz1xY6.png)

手機示意圖：
![手機示意圖](https://i.imgur.com/SvB4vOu.png)
