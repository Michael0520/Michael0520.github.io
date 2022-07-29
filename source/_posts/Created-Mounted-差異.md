---
title: (Vue) Created & Mounted 差異
date: 2021-08-07
description: Demo Created & Mounted 差異
categories:
- Vue
tags:
- Vue
---
## Demo

<iframe height="300" style="width: 100%;" scrolling="no" title="Vue mounted &amp; created 差異" src="https://codepen.io/michael-luo/embed/wvdXbyK?default-tab=html%2Cresult&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/michael-luo/pen/wvdXbyK">
  Vue mounted &amp; created 差異</a> by Michael Luo (<a href="https://codepen.io/michael-luo">@michael-luo</a>)
  on <a href="https://codepen.io">CodePen</a>.

</iframe>

- created 會顯示 `null`
- mounted 會顯示 `<div class="box"></div>`

因為 created 的生命週期不包含渲染 HTML ，是在渲染 HTML 之前執行，
mounted 則是已經完成 HTML 的渲染，即在渲染 HTML 之後執行，
個人建議若資料需要與 DOM 或 HTML 部分做交互 會建議把初始化放在 mounted 中執行，
若不需要 則建議在 created 中就初始化 因為 created 比 mounted 更早執行。