---
title: 應用 CSS3 Gradients 製作漸層效果
description: 紀錄常用 CSS3 漸層效果
date: 2020-11-15
categories:
- CSS
tags: 
- CSS
---

以前就很喜歡背景有漸層效果的桌布，自從 CSS3 多了這個屬性，
怎麼可以輕易放過呢 ！走過路過也千萬不可以放過啊。就不需要另外放圖片才能實現了。

基本語法邏輯如下：

```css=
background: linear-gradient(direction, color-stop1, color-stop2, ...);
```

### 效果1: 不設定漸層方向屬性(direction)

預設的狀況下，如果不設定 direction ，效果會從 color1 往下延伸到 color2

![漸層預覽圖](https://i.imgur.com/zUsq6dZ.png)
```css=
.gradient {
  background: #f598a8;
  background: -webkit-linear-gradient(#f598a8, #f6edb2);
  background: -o-linear-gradient(#f598a8, #f6edb2);
  background: -moz-linear-gradient(#f598a8, #f6edb2);
  background: linear-gradient(#f598a8, #f6edb2);
}
```

下面的這三種寫法的效果其實是等價的(以chrome測試)

```css=
.gradient {
  background: -webkit-linear-gradient(#f598a8, #f6edb2);
  background: -webkit-linear-gradient(top, #f598a8, #f6edb2);
  background: -webkit-linear-gradient(-90deg,#f598a8, #f6edb2);
}
```
---
### 效果2: 設定漸層方向性

主要有四種方向top / right / left / bottom。我們把上面的例子漸層效果改成由左到右。

![漸層預覽圖](https://i.imgur.com/LWBc4sr.png)

```css=
.gradient {
  background: #f598a8;
  background: -webkit-linear-gradient(left, #f598a8, #f6edb2);
  background: -o-linear-gradient(left, #f598a8, #f6edb2);
  background: -moz-linear-gradient(left, #f598a8, #f6edb2);
  background: linear-gradient(to right, #f598a8, #f6edb2);
}
```

如果覺得只有四種方向好像不夠用，那再來個八卦陣吧，如果我想要漸層從東北到西南勒，沒關係，這也做得到，(咦..怎麼跟上面看起來差不多)

![漸層預覽圖](https://i.imgur.com/hylY2Q6.png)


```css=
.gradient {
  background: #f598a8;
  background: -webkit-linear-gradient(left top, #f598a8, #f6edb2);
  background: -o-linear-gradient(left top, #f598a8, #f6edb2);
  background: -moz-linear-gradient(left top, #f598a8, #f6edb2);
}
```
---
### 效果3: 用角度來控制漸層方向

八卦陣還不夠用？我還要其他角度。好吧，我們還可以用角度來控制方向，從左開始，往下到頂是90deg(等同於bottom)，而往上的方向才是-90deg(等同於top)，所以方向就可以自己控制了喔。

![漸層預覽圖](https://i.imgur.com/TJKAoU8.png)

```css=
.gradient {
  background: #f598a8;
  background: -webkit-linear-gradient(-135deg, #f598a8, #f6edb2);
  background: -o-linear-gradient(-135deg, #f598a8, #f6edb2);
  background: -moz-linear-gradient(-135deg, #f598a8, #f6edb2);
}
```

---
### 效果4: 用多種顏色才做漸層效果

很簡單，就在後面多幾個顏色即可，效果如下
![漸層預覽圖](https://i.imgur.com/fkR3IgA.png)

```css=
.gradient {
  background: #f598a8;
  background: -webkit-linear-gradient(#f598a8, #f6edb2, #f598a8);
  background: -o-linear-gradient(#f598a8, #f6edb2, #f598a8);
  background: -moz-linear-gradient(#f598a8, #f6edb2, #f598a8);
}
```
---
### 效果5: 用百分比來控制漸層效果
在後面加上百分比，可以用來控制顏色所佔的比例

![漸層預覽圖](https://i.imgur.com/qHBYiiy.png)

```css=
.gradient {
  background: -webkit-linear-gradient(#f598a8 30%, #f6edb2 70%);
  background: -o-linear-gradient(#f598a8 30%, #f6edb2 70%);
  background: -moz-linear-gradient(#f598a8 30%, #f6edb2 70%);
}
```

其他的效果包含可以用其他非線性的漸層效果，如圓形或其他等等。

參考資料: [w3cschools](https://www.w3schools.com/css/css3_gradients.asp)