---
title: JavaScript Event Delegation (事件委派)
date: 2021-04-11 20:08:07
description: Event Delegation（事件委派）是一種受惠於 Event Bubbling 而能減少監聽器數目的方法。

categories: 
- JavaScript
tags:
- JavaScript
---

Event Delegation（事件委派）是一種受惠於 Event Bubbling 而能減少監聽器數目的方法。


<iframe height="265" style="width: 100%;" scrolling="no" title="Event Delegation" src="https://codepen.io/michael-luo/embed/mdRXyXR?height=265&theme-id=dark&default-tab=css,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/michael-luo/pen/mdRXyXR'>Event Delegation</a> by Michael Luo
  (<a href='https://codepen.io/michael-luo'>@michael-luo</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


當我們 click 不同的小區塊時，就會 console 出它們個別的名字，例如：a、b 或 c。

實作方法是將:

click 事件綁在 parent 上，藉由 Event Bubbling 傳遞給 child，而非直接將事件綁定在 child 上。
- 優點是可減少監聽器的數目，
- 缺點是由於需要判斷哪些 child node 是我們有興趣的項目，而必須多寫一些程式碼做判斷。

在此範例中，我們加上一個 `filter.child`，表示只對有`.child`這個 class 的節點有興趣，
而沒有加上`.child`的節點則不被影響，例如`click.subitem`這個節點之後就不會 console 它的名字。
