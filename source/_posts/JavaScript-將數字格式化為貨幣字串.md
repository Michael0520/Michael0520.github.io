---
title: JavaScript 將數字格式化為貨幣字串
date: 2021-11-15 09:22:08
description: Javascript 實作常用的數字格式化
categories:
- JavaScript
tags:
- JavaScript
---

## 簡介

數字以多種方式表示，例如日期/時間、貨幣、數字等等。當將其表示為貨幣值時，其影響會增加，並且變得更具可讀性。
例如，寫為 10000 的貨幣價值的影響要遠小於表示為 $10,000.00 的數字的影響。
它告訴我們有關數字，不同的貨幣符號和不同的逗號分隔的更多資訊。

## Demo

<iframe height="300" style="width: 100%;" scrolling="no" title="Untitled" src="https://codepen.io/michael0520/embed/mdMzxMG?default-tab=html%2Cresult&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/michael0520/pen/mdMzxMG">
  Untitled</a> by Michael0520 (<a href="https://codepen.io/michael0520">@michael0520</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

## 使用 Intl.NumberFormat() 方法將數字格式化為 JavaScript 中的貨幣字串

此方法用於以語言敏感格式表示數字，並根據提供的參數列示貨幣。
它以兩個引數作為輸入：`locales` 和 `options`。

- `locales`：它指定語言和區域設定。它是由語言和區域（由短劃線分隔）組合而成的小字串。
  - 例如，en-IN 語言環境採用印度和英語的格式。
  - 從右起的第一個逗號將千位數分開，其餘的以百位數為單位。
- `options`：這是一個由大量屬性組成的物件，或者我們可以說選項。
  - 將數字格式化為貨幣字串時，需要 3 主要選項。
- `style`：這只是我們數字格式的樣式。根據使用情況，它可以具有 3 個不同的值，十進位制，貨幣，百分比。在我們的例子中，我們將樣式設定為 currency。
- `currency`：它指定要在格式數字字串之前包含的符號的貨幣型別，例如，美元和歐元。
- `minimumFractionDigits`：指定格式化字串中小數點後顯示的最小位數。

```javascript=
const money = 10000;
const currency = function(number){
    return new Intl.NumberFormat('en-IN',
        {style: 'currency',currency: 'US', minimumFractionDigits: 2})
        .format(number);
};
console.log(currency(money));
```

## 使用 toLocaleString() 方法將數字格式化為 JavaScript 中的貨幣字串
此方法與 `Intl.NumberFormat()` 本質上相同，但是由於其處理多個專案的速度較慢而通常不使用。對於單個專案，兩種方法的速度相似。
它具有與 `Intl.NumberFormat()` 相同的引數。由於兩種方法的內部實現方式不同，因此速度有所不同。

```javascript=
const number = 2000;
number.toLocaleString('en-IN', 
    {style: 'currency',
     currency: 'Us', 
     minimumFractionDigits: 2})
console.log(number);
```

## 使用 Numeral.js 庫將數字格式化為 JavaScript 中的貨幣字串
Numeral.js 是用於數字格式化的最廣泛使用的庫之一。
要使用此庫將數字格式設定為貨幣字串，我們首先建立一個數字例項。
該庫使用的標準資料型別在執行格式化之前將數字或字串轉換為數字。
之後，我們可以使用 `format()`` 函式指定貨幣格式。

```htmlembedded=
<script src="//cdnjs.cloudflare.com/ajax/libs/numeral.js/2.0.6/numeral.min.js"></script>

<!-- CDN 中包含 Numeral.js 庫。 -->
```

```javascript=
var number = 1000;
var myNumeral = numeral(number);
// 使用 numeral 方法，帶入參數
var currencyString = myNumeral.format('$0,0.00');
```

我們建立了一個數字，然後呼叫了格式化函式以將數字格式化為帶有 2 個小數點的美元。
上面的程式碼提供了一種更簡潔的方法來指定貨幣格式。