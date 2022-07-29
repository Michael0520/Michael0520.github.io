---
title: JavaScript addEventListener 事件監聽
description: 紀錄學習事件監聽過程
date: 2020-12-08
categories:
- JavaScript
tags: 
- JavaScript
---


# addEventListener 事件監聽
```javaScript
var elBody = document.querySelector('.body');
elBody.addEventListener('click',function(){
  alert('body');
  console.log('body');
},false);

// false (事件氣泡 - event Bubbling) - 從指定元素往外找
// true (事件捕捉 - event capturing) - 從最外面找到指定元素
```
demo: https://codepen.io/michael-luo/pen/eYzBJBr

- 中止冒泡 stopPropagation 
demo: https://codepen.io/michael-luo/pen/pobRWQG

- preventDefault 取消預設觸發
demo: https://codepen.io/michael-luo/pen/zYBNPQd?editors=1111