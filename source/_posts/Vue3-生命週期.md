---
title: (Vue) 生命週期
date: 2021-08-10
description: 紀錄 Vue 生命週期順序以及在做什麼事情
categories:
- Vue
tags:
- Vue
---
## beforeCreate

實例初始化立即叫用，但是還為創建實例，
任何的 Vue實體 都還未配置(像是 `data`、`methods` ...都還無法使用)

## created

Vue 的實例已經完成創建，
這時 Vue實體中的配置除了 `$el` 外已全部配置
(`data`、`methods` ...已初始化，可以取得其資料)，`$el` 要在掛載模板後才會配置

## beforeMount

在 Vue 實體中的定義掛載到目標元素之前，
`$el` 會是還未被 Vue 實體中定義渲染的初始設定模板

## mounted

Vue 實體中的定義已經成功掛載到目標元素，
`$el` 已透過 Vue 實體中的定義渲染成真正的頁面
(像是 `v-model`、`v-bind`、`{{ }}` .... 等都已經成功渲染或是綁定完成)

## beforeUpdate

在資料更新前(像是變更 `data` 裡面變數的值之前)

## updated

我們變動的值已經變更上去並更新畫面了

## beforeDestroy

在 Vue 實體被銷毀之前，功能都還完整存在

## destroyed

此時 Vue 實體已經被銷毀，
雖然畫面還是會存在，不過已解除綁定，任何操作也無法更新畫面了
(有點類似 Vue 歸 Vue，DOM 歸 DOM 的概念，
所以儘管 Vue 的值再怎麼去變更，也只是 Vue 裡面在做的事情，畫面已經不會去管，
無雙向綁定的效果了)

# v-if  VS  v-show

- v-show : 只有透過新增 CSS `"display: none"` 來顯示/隱藏元件
- v-if : 完整的移除元件 ，使用此方式才能完整的觸發生命週期

v-show Demo 觀察變化：

<iframe height="300" style="width: 100%;" scrolling="no" title="Vue3 v-show Demo" src="https://codepen.io/michael0520/embed/BadYBNo?default-tab=html%2Cresult&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/michael0520/pen/BadYBNo">
  Vue3 v-show Demo</a> by Michael0520 (<a href="https://codepen.io/michael0520">@michael0520</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

# Keep Alive

維持生命週期

```html
<keep-alive>
	<child v-if="isShowing"></child>
</keep-alive>
```