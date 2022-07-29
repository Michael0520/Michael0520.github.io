---
title: JavaScript 中的冒泡事件 (capturing and bubbling)
date: 2021-04-11 20:05:33
description: Javascript 是一種事件驅動 (Event-driven) 的程式語言，簡單來說就是當 user 對網頁做了一些動作 (ex:點擊click)，才會觸發執行要做的動作。
categories:
  - JavaScript
tags:
  - JavaScript
---

Javascript 是一種事件驅動 (Event-driven) 的程式語言，簡單來說就是當 user 對網頁做了一些動作 (ex: 點擊 click)，才會觸發執行要做的動作。
你知道嗎？當你點擊了`ul` `li` 裡面的一個 `a` link，
其實 ul, li, a 都被點到了，因為 ul 包著 li，而 li 包著 a ，所以實際上來說，你點到了整個網頁，這是什麼意思？
這就是 Javascript 中的 **DOM 事件傳遞機制**：「傳遞與冒泡」，

為了證明上述所說，我在這三個元素上綁定 `addEventListener` 事件印出 console：

![](https://i.imgur.com/eM0urBR.png)

如圖所見，在事件上發生的順序，會先觸發了我所點擊的 a link，再依序往回觸發父層 DOM 元素的事件。
事件傳遞機制總共分為三大階段：

- 捕獲階段 (Capture Phase)
- 目標階段 (Target Phase)
- 冒泡階段 (Bubbling Phase)

![](https://i.imgur.com/07NQC8Z.png)

圖片取自[W3](https://www.w3.org/TR/DOM-Level-3-Events/#event-flow)

```javascript=
// PhaseType
const unsigned short      CAPTURING_PHASE                = 1;
const unsigned short      AT_TARGET                      = 2;
const unsigned short      BUBBLING_PHASE                 = 3;
```

- 捕獲階段 (Capture Phase)
  在捕獲階段，DOM 的事件會從祖先層 (window) 開始往下尋找目標 (target)，這個過稱稱為捕獲階段 (CAPTURING_PHASE)。
- 目標階段 (Target Phase)
  在找到目標的時候，就會是目標階段 (AT_TARGET)。
- 冒泡階段 (Bubbling Phase)
  循著原路回去的過程，就是冒泡階段 (BUBBLING_PHASE)。

這個階段的順序，也是常常聽到的口訣：「先捕獲，再冒泡」。

所以我的 `addEventListener` 就是在冒泡階段依序觸發的囉？也不完全是。
其實我們所熟知的 `addEventListener` 還有第三個參數：true/false 可以決定你的監聽要在捕獲階段或是冒泡階段觸發：

- 預設為 false ，則為監聽冒泡階段
- 若改為 true ，就是監聽捕獲階段

來看看剛剛的例子中，我的監聽事件就如平常的方式一樣：

![](https://i.imgur.com/4HmCnej.png)

如果我在每一個 addEventListener 加上了 `true` 的參數，表示我要在捕獲階段就觸發我的動作：

![](https://i.imgur.com/i8Xqlw2.png)

因為捕獲階段是從父層一層一層找下去的，所以觸發的順序跟剛剛相反了。

再看一眼剛剛的事件階段 (eventPhase) 定義：

```javascript=
CAPTURING_PHASE = 1 // 捕獲階段：1
AT_TARGET       = 2 // 目標階段：2
BUBBLING_PHASE  = 3 // 冒泡階段：3
```

把這個 eventPhase 加入剛剛的範例中，來看看我們是不是真的在捕獲階段觸發了我們的動作：

![](https://i.imgur.com/ESGhlsp.png)

如我們的期待，的確是在捕獲階段觸發了父層的事件，也在找到點擊的 alink 的時候成為目標階段。
如果我們再把剛剛沒有設定第三個參數，預設為 false 的 addEventListener 加回去的話，照理說就可以看到整個捕獲與冒泡的過程：

```javascript=
ul.addEventListener("click", function (e) {
  console.log("ul clicked", e.eventPhase);
 }, true);
li.addEventListener("click", function (e) {
  console.log("li clicked", e.eventPhase);
 }, true);
alink.addEventListener("click", function (e) {
  console.log("a link clicked", e.eventPhase);
 }, true);
ul.addEventListener("click", function (e) {
 console.log("ul clicked", e.eventPhase);
});
li.addEventListener("click", function (e) {
 console.log("li clicked", e.eventPhase);
});
alink.addEventListener("click", function (e) {
 console.log("a link clicked", e.eventPhase);
});
```

結果：

![](https://i.imgur.com/viWhUjf.png)

跟想像中的差不多，但是在目標階段這邊有一個小小的地方要注意，就是在 target phase 的時候，
不論你的 addEventListener 設為 true/false 都沒有差別，
可以把 target phase 想像成一個點，捕獲和冒泡想像成一個過程，
在 target phase 這個位置，就不會管 addEventListener 的 true/false，只照著程式的順序執行。

舉例：

```javascript=
alink.addEventListener("click", function (e) {
 console.log("a link clicked when bubbling", e.eventPhase);
});
alink.addEventListener( "click", function (e) {
  console.log("a link clicked when capturing", e.eventPhase);
 }, true);
```

我寫了兩個 alink 的監聽，
第一個監聽為預設是 false，應該會在冒泡階段執行，
第二個則為 true，應該要在捕獲階段執行，執行結果卻會是：

![](https://i.imgur.com/bZTCGA8.png)

表示上述所說，addEventListener 的 true/false 並不影響 target phase 觸發的階段，他不算是捕獲或是冒泡的階段之一。

動手玩玩看：

<iframe height="265" style="width: 100%;" scrolling="no" title="capture &amp; bubbling" src="https://codepen.io/michael-luo/embed/wvgpQBv?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/michael-luo/pen/wvgpQBv'>capture &amp; bubbling</a> by Michael Luo
  (<a href='https://codepen.io/michael-luo'>@michael-luo</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

如果上述的捕獲與冒泡機制你已經理解了，那就會明白取消預設行為和事件傳遞機制是不一樣的事情，如果在這之前你不是特別清楚，希望這篇文章可以讓你更加理解他們之間的差異。

## 參考文章

- [DOM 的事件傳遞機制：捕獲與冒泡
  ](https://blog.techbridge.cc/2017/07/15/javascript-event-propagation/)
- [重新認識 JavaScript: Day 14 事件機制的原理
  ](https://ithelp.ithome.com.tw/articles/10191970)
