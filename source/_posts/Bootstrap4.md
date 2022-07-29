---
title: Bootstrap
description: 紀錄 BootStrap 學習過程。
date: 2021-04-08
categories:
- BootStrap
tags: 
- BootStrap
---



[Bootstrap官網](https://getbootstrap.com/docs/4.5/getting-started/introduction/)

以下是選單翻譯：

1. Getting started 快速開始
2. Layout 排版
3. Content 內容
4. Components 元件
5. Utilities 通用類別
6. Extend 擴增
7. Migration 更版紀錄

---

### 起手式，放入( Css & Js ) CDN

* Css:

```html=
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/css/bootstrap.min.css" integrity="sha384-TX8t27EcRE3e/ihU7zmQxVncDAy5uIKz4rEkgIXeMed4M0jlfIDPvg6uqKI2xXr2" crossorigin="anonymous">
```

* Js:

```htmlembedded=
<script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/js/bootstrap.min.js" integrity="sha384-w1Q4orYjBQndcko6MimVbzY0tgp4pWB4lZ7lr30WKz0vr/aWKhXdBNmNb5D92v7s" crossorigin="anonymous"></script>
```

---

### 語意化標題

1. `<s>` 刪除線在文字上
2. `<u>` 文字下底線
3. `<small>` 極小文字
4. `<strong>` 粗體
5. `<b>` 突出顯示、而不增加重要性
6. `<i>` 語音、技術用語
7. `<span>` 行內元素，沒有任何語意
8. `<em>` 文字斜體

---

## 常用切版

### 1. 常見 list 清單

```htmlembedded=
<ul class="list-unstyled"> 
<!-- 此 class語意為清除 ul 格式 -->
  <li>Lorem ipsum dolor sit amet</li>
  <li>Consectetur adipiscing elit</li>
  <li>Integer molestie lorem at massa</li>
  <li>Facilisis in pretium nisl aliquet</li>
  <li>Nulla volutpat aliquam velit
    <ul>
      <li>Phasellus iaculis neque</li>
      <li>Purus sodales ultricies</li>
      <li>Vestibulum laoreet porttitor sem</li>
      <li>Ac tristique libero volutpat at</li>
    </ul>
  </li>
  <li>Faucibus porta lacus fringilla vel</li>
  <li>Aenean sit amet erat nunc</li>
  <li>Eget porttitor lorem</li>
</ul>
```

### 2. 描述清單

```htmlmixed=
<dl class="row">
  <dt class="col-sm-3">Description lists</dt>
  <dd class="col-sm-9">A description list is perfect for defining terms.</dd>

  <dt class="col-sm-3">Euismod</dt>
  <dd class="col-sm-9">
    <p>Vestibulum id ligula porta felis euismod semper eget lacinia odio sem nec elit.</p>
    <p>Donec id elit non mi porta gravida at eget metus.</p>
  </dd>

  <dt class="col-sm-3">Malesuada porta</dt>
  <dd class="col-sm-9">Etiam porta sem malesuada magna mollis euismod.</dd>

  <dt class="col-sm-3 text-truncate">Truncated term is truncated</dt>
<!--此class 意思為 dt 標題超出邊框的字體會自動隱藏  -->
  <dd class="col-sm-9">Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa justo sit amet risus.</dd>

  <dt class="col-sm-3">Nesting</dt>
  <dd class="col-sm-9">
    <dl class="row">
      <dt class="col-sm-4">Nested definition list</dt>
      <dd class="col-sm-8">Aenean posuere, tortor sed cursus feugiat, nunc augue blandit nunc.</dd>
    </dl>
  </dd>
</dl>
```

---

## Image

### 1. 圖片自適應縮放 (img-fluid)

```htmlembedded=
<img src="..." class="img-fluid" alt="Responsive image">
```

> `img-fluid` :
    會自動設定 max-width:100% 以及     height:auto
> 圖片不管大小都要加上
> 圖片過大的話就加上 width:?px 讓他小一點即可

### 2. 頭像效果(thumbnail)（圖片四周留白邊）

```htmlmixed=
<img src="..." alt="..." class="img-thumbnail">
```

### 3. 圓角效果(rounded)

```htmlembedded=
<img src="..." class="rounded float-left" alt="...">
<img src="..." class="rounded float-right" alt="...">
```

#### 很重要(!)

> 上方圓角效果使用 float 去做排版，
因此連續使用的話，
必須得在父層加上清除浮動 class="clear-fix"，版面才會正常

## 4. 置中做法(超常用！)

```htmlembedded=
<div class="text-center">
<!-- 文字置中 -->
  <img src="..." class="img-fluid mx-auto d-block" alt="...">
<!-- 1.自適應大小 2.margin right&left :auto 3.display:block   -->
</div>
```

## 5. 圖片描述 (figure)

![image](https://i.imgur.com/mfwTWf3.png)

> 外層使用 figure class名稱
`<fitcaption>`:圖片描述

```htmlembedded=
<figure class="figure">
  <img src="..." class="figure-img img-fluid rounded" alt="...">
  <figcaption class="figure-caption">A caption for the above image.</figcaption>
</figure>
```

---

## 6. Table

> [更多Table資料](https://getbootstrap.com/docs/4.5/content/tables/)

表格架構:
![image](https://i.imgur.com/0pZdRP1.png)
範例：
![image](https://i.imgur.com/ziJdHYM.png)

```htmlmixed=
<table class="table">
  <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">First</th>
      <th scope="col">Last</th>
      <th scope="col">Handle</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">1</th>
      <td>Mark</td>
      <td>Otto</td>
      <td>@mdo</td>
    </tr>
    <tr>
      <th scope="row">2</th>
      <td>Jacob</td>
      <td>Thornton</td>
      <td>@fat</td>
    </tr>
    <tr>
      <th scope="row">3</th>
      <td>Larry</td>
      <td>the Bird</td>
      <td>@twitter</td>
    </tr>
  </tbody>
</table>
```

* 滾動卷軸(table-responsive)

```htmlembedded=
<div class="table-responsive">
  <table class="table">
    ...
  </table>
</div>
```

超大裝置:`<div class="table-responsive-xl">`
大裝置:`<div class="table-responsive-lg">`
中裝置:`<div class="table-responsive-md">`
小裝置:`<div class="table-responsive-sm">`

---

## Grid 網格

Width:960px
分成12 直欄位

> 以下範例：
![image](https://i.imgur.com/9aGIAay.png)

```css=
column Width:60px
Gutter Width:20px
Gutter on outside:10px
```

### 重點(！)

#### 1. class="col-xx" 外層是 class="row"

#### 2. class="row" 裡面是 class="col-xx"

#### 3.頁面內容請放在 class="col-xx" 的內層

#### 主要原因為空間補回以及 flex

* [code 範例](https://codesandbox.io/s/demobst4grid-forked-b32eg)

---
## RWD

  1. Extra small <=576px(col-*)
  2. Small 576~767px (col-sm-*)
  3. Medium 768~991px (col-md-*)
  4. Large 992~1199px (col-lg-*)
  5. Extra large ≥1200px (col-xl-*)

## flex 屬性

1. display flex
2. flex-direction
3. justify-content
4. align-items
5. flex-wrap
6. align-content(限制 wrap)

組合範例圖：

1. 外層屬性 (控制外層)
![截圖](https://i.imgur.com/PmuHzrU.png)

2. 內層屬性 (控制內層)
![截圖](https://i.imgur.com/cSfMu5E.png)

[code 範例](https://codesandbox.io/s/demobst4gridrwd-b32eg?file=/index.html)

### 補充

order(排列順序):

  ```htmlembedded=
<div class="container">
      <div class="row">
        <div class="col-3 order-2">
          <div class="box">第二張圖</div>
        </div>
        <div class="col-3 order-1">
          <div class="box">第一張圖</div>
        </div>
        <div class="col-3 order-3">
          <div class="box">第三張圖</div>
        </div>
      </div>
    </div>
```

flex-wrap(換行):

  ```htmlembedded=
 <div class="d-flex flex-wrap bg-secondary">
        <div class="col-sm-3 box-auto">1</div>
        <div class="col-sm-3 box-auto">2</div>
        <div class="col-sm-3 box-auto">3</div>
        <div class="col-sm-3 box-auto">4</div>
        <div class="col-sm-3 box-auto">5</div>
        <div class="col-sm-3 box-auto">6</div>
        <div class="col-sm-3 box-auto">7</div>
      </div>
```

align-content(內元件統一對齊)

==重點:必須得要有 flex-wrap 才可以使用==

```htmlembedded=
   <div class="d-flex flex-wrap align-content-center" style="height: 100vh">
   // 套上高度，方便觀看
        <div class="col-sm-3 box-auto">11231</div>
        <div class="col-sm-3 box-auto">2123</div>
        <div class="col-sm-3 box-auto">313</div>
        <div class="col-sm-3 box-auto">313</div>
      </div>
    </div>
```

---

## container(主要是被用來定義最外層的容器)

使用上非為兩大類：

1. container-fluid(滿版寬度)
2. container-(階段固定寬度

---

## margin & padding (spacing 妙用！)

語法：class = {property  p or m }-{sides 方向}-{size 大小}

1. property

* m - for classes that set margin
* p - for classes that set padding

2. sides

* t - for classes that set margin-top or padding-top
* b - for classes that set margin-bottom or padding-bottom
* s - for classes that set margin-left or padding-left in LTR, margin-right or padding-right in RTL
* e - for classes that set margin-right or padding-right in LTR,margin-left or padding-left in RTL
* x - for classes that set both *-left and *-right
* y - for classes that set both *-top and *-bottom blank - for classes that set a margin or padding on all 4 sides of the element

1. sizes

* 0 - for classes that eliminate the margin or padding by setting it to 0
* 1 - (by default) for classes that set the margin or padding to $spacer * .25
* 2 - (by default) for classes that set the margin or padding to $spacer * .5
* 3 - (by default) for classes that set the margin or padding to $spacer
* 4 - (by default) for classes that set the margin or padding to $spacer * 1.5
* 5 - (by default) for classes that set the margin or padding to $spacer * 3
* auto - for classes that set the margin to auto (You can add more sizes by adding entries to the $spacers Sass map variable.)

語法簡寫:

```htmlembedded=
.mt-0 { 
  margin-top: 0 !important;
}

.ms-1 {        // 一個 spacer = 1rem(16px)
  margin-left: ($spacer * .25) (16px * 0.25);
}

.px-2 {        // x = left & right
  padding-left: ($spacer * .5) !important;
  padding-right: ($spacer * .5) !important;
}

.py-2 {        // x = top & bottom
  padding-top: ($spacer * .5) !important;
  padding-bottom: ($spacer * .5) !important;
}

.p-3 {        
  padding: $spacer !important;
}
```

實作範例：

```htmlembedded=
<!-- 使用m-0 來去掉 p段落原始存在的 margin -->
<!-- 使用 mt-2 來隔開兩個 box -->
<div class="container">
      <div class="box p-2">
        <p class="">
          Lorem, ipsum dolor sit amet consectetur adipisicing elit. Animi magni
          ullam voluptas, nihil eum, reiciendis esse adipisci, necessitatibus
          quidem culpa vel aut error repudiandae similique ea accusantium quia
          unde dolorum.
        </p>
        <p class="m-0">
          Lorem, ipsum dolor sit amet consectetur adipisicing elit. Animi magni
          ullam voluptas, nihil eum, reiciendis esse adipisci, necessitatibus
          quidem culpa vel aut error repudiandae similique ea accusantium quia
          unde dolorum.
        </p>
      </div>
      <div class="box p-2 mt-2">
        <p class="m-0">
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Quas vitae
          rerum assumenda harum saepe minima sint omnis esse, aut fugit? Ab
          voluptatem magnam quos veniam laudantium, enim rem nisi ipsam.
        </p>
      </div>

      <!-- 第一個靠左，兩個靠右 -->
      <!-- 先使用 justify-content-end -->
      <!-- 藉由 margin auto 特性來推擠  -->
      <div class="row mt-2 justify-content-end">
        <div class="col-2">
          <div class="box">1</div>
        </div>
        <div class="col-2 ml-auto">
          <div class="box">2</div>
        </div>
        <div class="col-2">
          <div class="box">3</div>
        </div>
      </div>
    </div>
    <!-- 置中用法 -->
      <!-- 使用 mx-auto 加上固定寬度，來置中-->
      <div class="box mx-auto p-1" style="width: 200px">
        Lorem ipsum dolor sit amet consectetur, adipisicing elit. Ratione at in,
        quidem fugit odio reiciendis quisquam id. Iste, nobis perspiciatis.
      </div>
```

實作範例：

1. [相簿排版](https://codepen.io/michael-luo/pen/JjRRLqY)