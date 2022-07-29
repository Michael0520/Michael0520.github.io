---
title: (Project) HTML5 Drag and Drop API 
description: HTML5 中的 Drag & Drop API 可以讓我們在瀏覽器中做到拖曳元素、排序元素、或者是讓使用者透過拖拉的方式把要上傳的檔案拉到瀏覽器當中。
date: 2021-03-16
categories:
- JavaScript
- 作品集
tags: 
- JavaScript
- 作品集
---


# HTML5 Drag and Drop API 

## 簡述

HTML5 中的 Drag & Drop API 可以讓我們在瀏覽器中做到拖曳元素、排序元素、或者是讓使用者透過拖拉的方式把要上傳的檔案拉到瀏覽器當中。

在學習 HTML5 Drag & Drop API 時，最重要的是去區分 Drag Source 和 Drop Target，因為它們會需要各自去監聽不同的事件。

![](https://i.imgur.com/awJYLJt.png)

- `Drag Source` 指的是被點擊要拖曳的物件，也就是藍色的圓，通常是一個 element。
- `Drop Target` 指的是拖曳的物件被放置的區域，也就是右邊的綠色區域，通常是一個 div container。

## Drag & Drop 主要事件

Drag & Drop 提供的事件主要包含(`dragstart, drag, dragend, dragenter, dragover, dragleave, drop`)，
其中有些是針對 Drag Source 的，有些則是針對 Drop Target 的，整理如下表：



| x | Drag Source | Drag Target | 解釋|
| :----| :---- | :---- | :----|
| 1 | dragstart |  |始拖曳元素時觸發此事件 (點擊元素的瞬間)
| 2 | drag | dragenter |拖曳元素時觸發此事件
| 3 |  | dragover |當元素拖曳到有效位置放置則觸發此事件
| 4 |  | dragleave |拖曳的元素離開有效的位置時觸發
| 5 |  | drop |  |在有效位置上放置元素時觸發此事件(放下元素)
| 6 | dropend |  | 單元格 當拖曳結束時會觸發此事件



- drag：在 drag source 被拖曳時會持續被觸發。
- dragover：當拖曳的 drag source 到 drop target 上方時會持續被觸發。

**記得要針對被拖曳的物件取消預設行為（default）**


## 參考連結
[[筆記] 製作可拖曳的元素（HTML5 Drag and Drop API）](https://pjchender.blogspot.com/2017/08/html5-drag-and-drop-api.html)
[详解Html5关于拖拽（Drag 和 drop）的使用和事件](https://blog.csdn.net/weixin_41229588/article/details/106574573?ops_request_misc=&request_id=&biz_id=102&utm_term=dragleave&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-5-106574573.pc_search_result_before_js)

