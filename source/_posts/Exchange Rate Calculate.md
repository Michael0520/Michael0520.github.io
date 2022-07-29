---
title: (Project) Exchange Rate Calculate
description: 使用 json 檔案來實作匯率轉換器。
date: 2021-02-25
categories:
- JavaScript
- 作品集
tags: 
- JavaScript
- 作品集
---

# Exchange Rate Calculate


## [Demo](https://michael0520.github.io/Exchange-Rate-Caclulate/index.html)

## HTML 

### 設定圖片＆選單下拉列＆輸入框
```htmlembedded=
 <img src="./money拷貝.png" alt="" class="money-img" />
    <h1>Exchange Rate Calculator</h1>
    <p>Choose the currency and the amounts to get the exchange rate</p>

    <div class="container">
      <div class="currency">
        <select id="currency-one">
          <option value="AED">AED</option>
          <option value="ARS">ARS</option>
          <option value="AUD">AUD</option>
          <option value="BGN">BGN</option>
          <option value="BRL">BRL</option>
          <option value="BSD">BSD</option>
          <option value="CAD">CAD</option>
          <option value="CHF">CHF</option>
          <option value="CLP">CLP</option>
          <option value="CNY">CNY</option>
          <option value="COP">COP</option>
          <option value="CZK">CZK</option>
          <option value="DKK">DKK</option>
          <option value="DOP">DOP</option>
          <option value="EGP">EGP</option>
          <option value="EUR">EUR</option>
          <option value="FJD">FJD</option>
          <option value="GBP">GBP</option>
          <option value="GTQ">GTQ</option>
          <option value="HKD">HKD</option>
          <option value="HRK">HRK</option>
          <option value="HUF">HUF</option>
          <option value="IDR">IDR</option>
          <option value="ILS">ILS</option>
          <option value="INR">INR</option>
          <option value="ISK">ISK</option>
          <option value="JPY">JPY</option>
          <option value="KRW">KRW</option>
          <option value="KZT">KZT</option>
          <option value="MXN">MXN</option>
          <option value="MYR">MYR</option>
          <option value="NOK">NOK</option>
          <option value="NZD">NZD</option>
          <option value="PAB">PAB</option>
          <option value="PEN">PEN</option>
          <option value="PHP">PHP</option>
          <option value="PKR">PKR</option>
          <option value="PLN">PLN</option>
          <option value="PYG">PYG</option>
          <option value="RON">RON</option>
          <option value="RUB">RUB</option>
          <option value="SAR">SAR</option>
          <option value="SEK">SEK</option>
          <option value="SGD">SGD</option>
          <option value="THB">THB</option>
          <option value="TRY">TRY</option>
          <option value="TWD">TWD</option>
          <option value="UAH">UAH</option>
          <option value="USD" selected>USD</option> // 設定預設值為 USD
          <option value="UYU">UYU</option>
          <option value="VND">VND</option>
          <option value="ZAR">ZAR</option>
        </select>
          <input type="number" id="amount-one" placeholder="0" value="1" />

      </div>
    </div>
```
完成後如下圖：
但還缺少了匯率轉換的選單，
下個部分來製作
![](https://i.imgur.com/lPUTZT6.png)


### 新增轉換按鈕，以及轉換後的選單列以及輸入框

避免兩份資料同步，切記要記得修改 id 以及 class 名稱
```htmlmixed=
<div class="swap-rate-container">
        <button class="btn" id="rate">Swap</button>
        <div class="rate" id="rate"></div>
        // 此區塊為顯示轉換率的數值
      </div>

      <div class="currency">
        <select id="currency-two">
          <option value="AED">AED</option>
          <option value="ARS">ARS</option>
          <option value="AUD">AUD</option>
          <option value="BGN">BGN</option>
          <option value="BRL">BRL</option>
          <option value="BSD">BSD</option>
          <option value="CAD">CAD</option>
          <option value="CHF">CHF</option>
          <option value="CLP">CLP</option>
          <option value="CNY">CNY</option>
          <option value="COP">COP</option>
          <option value="CZK">CZK</option>
          <option value="DKK">DKK</option>
          <option value="DOP">DOP</option>
          <option value="EGP">EGP</option>
          <option value="EUR" selected>EUR</option>
          <option value="FJD">FJD</option>
          <option value="GBP">GBP</option>
          <option value="GTQ">GTQ</option>
          <option value="HKD">HKD</option>
          <option value="HRK">HRK</option>
          <option value="HUF">HUF</option>
          <option value="IDR">IDR</option>
          <option value="ILS">ILS</option>
          <option value="INR">INR</option>
          <option value="ISK">ISK</option>
          <option value="JPY">JPY</option>
          <option value="KRW">KRW</option>
          <option value="KZT">KZT</option>
          <option value="MXN">MXN</option>
          <option value="MYR">MYR</option>
          <option value="NOK">NOK</option>
          <option value="NZD">NZD</option>
          <option value="PAB">PAB</option>
          <option value="PEN">PEN</option>
          <option value="PHP">PHP</option>
          <option value="PKR">PKR</option>
          <option value="PLN">PLN</option>
          <option value="PYG">PYG</option>
          <option value="RON">RON</option>
          <option value="RUB">RUB</option>
          <option value="SAR">SAR</option>
          <option value="SEK">SEK</option>
          <option value="SGD">SGD</option>
          <option value="THB">THB</option>
          <option value="TRY">TRY</option>
          <option value="TWD">TWD</option>
          <option value="UAH">UAH</option>
          <option value="USD">USD</option>
          <option value="UYU">UYU</option>
          <option value="VND">VND</option>
          <option value="ZAR">ZAR</option>
        </select>
        <input type="number" id="amount-two" placeholder="0" /> 
        // 這邊不需要設定 value ，因為 value 由上方做決定
        
      </div>
```

## CSS

### 設定預設顏色& CSS 起手式& 垂直水平置中

```css=
:root {
    --primary-color: #5fbaa7
}

* {
    box-sizing: border-box;
}

body{
    background-color: #f4f4f4;
    font-family: Arial, Helvetica, sans-serif;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    margin: 0;
    padding: 20px;
}
```

### 美化貨幣選項外觀與輸入框

`background: transparent`是黑色且全透明 rgba(0,0,0,0)，
如果一個元素需要將他覆蓋在另外一個元素上，而我們又需要顯示下面的元素，就會使用到此屬性。

```css=
.currency select {
  padding: 10px 30px 10px 10px;
  /*  取消 selected 預設樣式  */
  -moz-appearance: none;
  -webkit-appearance: none;
  appearance: none;
  border: 1px solid #dedede;
  font-size: 16px;
  /*  rgba(0,0,0,0)  */
  background: transparent;
  /*  向下的三角形的 icon  */
  background-image: url("data:image/svg+xml;charset=US-ASCII,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%22292.4%22%20height%3D%22292.4%22%3E%3Cpath%20fill%3D%22%20000002%22%20d%3D%22M287%2069.4a17.6%2017.6%200%200%200-13-5.4H18.4c-5%200-9.3%201.8-12.9%205.4A17.6%2017.6%200%200%200%200%2082.2c0%205%201.8%209.3%205.4%2012.9l128%20127.9c3.6%203.6%207.8%205.4%2012.8%205.4s9.2-1.8%2012.8-5.4L287%2095c3.5-3.5%205.4-7.8%205.4-12.8%200-5-1.9-9.2-5.5-12.8z%22%2F%3E%3C%2Fsvg%3E");
  background-position: right 10px top 50%, 0, 0;
  background-size: 12px auto, 100%;
  background-repeat: no-repeat;
}

/*  輸入選項  */
.currency input {
  border: 0;
  background: transparent;
  font-size: 30px;
  text-align: right;
}
```

### 美化匯率的顯示外觀

`outline: 0`，點下去後，預設會出現的線條外框樣式。

`@media (max-width: 600px)`，當螢幕寬度小於600時，改變輸入框與h1的大小。

```css=
.swap-rate-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.rate {
  color: var(--primary-color);
  font-size: 14px;
  padding: 0 10px;
}

select:focus,
input:focus,
button:focus {
  outline: 0;
}

@media (max-width: 600px) {
  .currency input {
    width: 200px;
  }
  h1 {
    text-align: center;
  }
}

```

## JS


### 設定變數讀取表單變化

`addEventListener` 和電影選位的下拉式選單讀取方法一樣，都是使用change。

- input 事件： 當 input、 textarea 以及帶有 contenteditable 的元素內容被改變時，就會觸發 input 事件。
- change 事件： 當 input、select、textarea、radio、checkbox 等表單元素被改變時觸發。 但與 input 事件不同的是，
>  __input 事件會在輸入框輸入內容的當下觸發__，
 __而 change 事件則是在目前焦點離開輸入框後才觸發。__
 

```javascript=
// 選擇要轉換的匯率1(ex TWD)
const currencyEl_one = document.getElementById("currency-one");
// 匯率的總計1
const amountEl_one = document.getElementById("amount-one");
// 選擇要轉換的匯率2(ex USD)
const currencyEl_two = document.getElementById("currency-two");
// 匯率的總計2
const amountEl_two = document.getElementById("amount-two");
// 顯示匯率的文字
const rateEl = document.getElementById("rate");

//swap button
const swap = document.getElementById("swap");

//Fetch exchage rates and update the DOM
// 取得匯率更新使用(fetch) 以及 把取得的資料更新 DOM
function caclulate() {
  console.log("GOGO");
}

// Event Listeners
//下拉選單的變化是使用change
currencyEl_one.addEventListener("change", caclulate);
// 輸入框是使用input
amountEl_one.addEventListener("input", caclulate);
currencyEl_two.addEventListener("change", caclulate);
amountEl_two.addEventListener("input", caclulate);

// 呼叫函式
caclulate();
```

更動 select 欄位會顯示如下：
![](https://i.imgur.com/AIJVE78.png)

### 透過 Fetch() 串接取得匯率資料

#### 何謂 Fetch?
> - fetch 會使用 ES6 的 Promise 作回應
> - then 作為下一步
> - catch 作為錯誤回應 (404, 500…)
回傳的為 ReadableStream 物件，需要使用不同資料類型使用對應方法，才能正確取得資料物件。

```javascript=
// Fetch 
fetch('https://randomuser.me/api/', {})
  .then((response) => {
    // 這裡會得到一個 ReadableStream 的物件
    console.log(response);
    // 可以透過 blob(), json(), text() 轉成可用的資訊
    return response.json(); 
  }).then((jsonData) => {
    console.log(jsonData);
  }).catch((err) => {
    console.log('錯誤:', err);
});
```

> `fetch` 後方會接 `then()`，這是 Promise 的特性，資料取得後可在 then 裡面接收。
`return response.json();` 的資料則會傳到下一個 `then()`
---
以下為此專案實作：

```javascript=
// Fetch exchange rates and update the DOM
function caclulate(){
    const currency_one = currencyEl_one.value;
    const currency_two = currencyEl_two.value;
// 使用網址更改最後的部分就可以取得更新選擇的資料
    fetch(`https://api.exchangerate-api.com/v4/latest/${currency_one}`)
// 取得的檔案為 json 格式，所以在 fetch 取得檔案之後
// 透過json()的方法處理檔案
    .then(res => res.json()) 
    .then(data => {
// 查看資料是否正確執行
        console.log(data)
    })
}
```

以下為成功切換 select 貨幣執行畫面：
![](https://i.imgur.com/wxy3r4P.png)

[Fetch 詳細解說](https://wcc723.github.io/javascript/2017/12/28/javascript-fetch/)

網址的最後為貨幣的種類，所以在最後設變數，就可以即時取得不同種類的貨幣資料。
https://api.exchangerate-api.com/v4/latest/TWD

會取到的 json 資料，透過語法 json() 變成較容易觀看的格式。

### 顯示出選擇的貨幣匯率 & 計算轉換後的價格

使用ES6語法‵‵，裡面使用$將變數放進去。

`toFixed(N)`為取小數第N位。
```javascript=
 fetch(`https://api.exchangerate-api.com/v4/latest/${currency_one}`)
    .then((res) => res.json())
    .then((data) => {
      console.log(data);
      const rate = data.rates[currency_two];
      rateEl.innerText = `1 ${currency_one} = ${rate} ${currency_two}`;
      amountEl_two.value = (amountEl_one.value * rate).toFixed(2);
    });
}
```

### 點選swap按鈕可以上下顛倒貨幣

設立變數幫助進行調換。

```javascript=
swap.addEventListener("click", () => {
  //先將one放到temp裡
  const temp = currencyEl_one.value;
  //再將two丟到one裡
  currencyEl_one.value = currencyEl_two.value;
  //原先在temp裡面的one放到two裡面，完成交換。
  currencyEl_two.value = temp;
  caclulate();
});
```

[addeventListener 監聽事件詳細解說](https://ithelp.ithome.com.tw/articles/10192175)

