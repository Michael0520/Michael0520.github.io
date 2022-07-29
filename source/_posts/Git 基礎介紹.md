---
title: 初探 Git 基礎介紹
description: 「Git 是一種版本控制系統」，專業一點的可以說是「Git 是一種分散式版本的版本控制系統」。
date: 2020-11-10
categories:
- Git
tags: 
- Git
---


# Git 基礎介紹

### 什麼是 Git？

「Git 是一種版本控制系統」，專業一點的可以說是「Git 是一種分散式版本的版本控制系統」。
「版本控制系統」的英文是「Version Control System」，但這個回答，對沒接觸過的新手來說，有講跟沒講差不多。
到底什麼是「版本」？
要「控制」什麼東西？什麼又是「分散式」？

不管你是不是工程師，只要你是電腦工作者，你每天的工作可能都是每天新增、編輯、修改許多檔案。舉個例子來說，你可能是一名人資部門主管，你有一個叫做 resume 的目錄，裡面專門用來存放面試者的資料。

![](https://i.imgur.com/lHtJBlG.png)

讓我們來看圖說故事。

如圖所示，隨著時間的變化，
1. 一開始這個目錄裡只有 3 個檔案
2. 過兩天增加到 5 個。
3. 不久之後，其中的 2 個被修改了，
4. 過了三個月後又增加到 7 個
5. 最後又刪掉了 1 個，變成 6 個。

這每一個「目錄的狀態變化」，不管是新增或刪除檔案，亦或是修改檔案內容，都稱之為一個「版本」，例如上圖圖例的版本 1 ~ 5。
而所謂的「版本控制系統」，就是指會幫你記錄這些所有的狀態變化，並且可以像搭乘時光機一樣，隨時切換到過去某個「版本」時候的狀態。

簡單的說，Git 就像玩遊戲的時候可以儲存進度一樣。
舉例來說，為了避免打頭目打輸了而損失裝備，又或是打倒頭目卻沒有掉落期望的珍貴裝備，
你也許在每次要去打頭目之前之前記錄一下，在發生狀況的時候可以載入舊進度，再來挑戰一次。

---

## git 指令
### git init （初始化專案）

這個指令會讓我們本機端的專案資料夾成功加入Git系統內，
我們可以看到加入成功後會出現第一個分支master，


### git status (查看狀態)

這個指令可以查看目前位址的狀態是如何，
我們可以看到 目前狀態是

```terminal=
On branch master  //正在 master 分支上
No commits yet   //尚未提交
noting to commit (copy files and use "git add" to track) 
// 沒有任何提交，複製檔案在使用 "git add" 去追蹤檔案
```
![](https://i.imgur.com/tbs9BmT.gif)

接下來我們新增檔案，並且加入到 git 去做追蹤
### git add (將檔案加入 git 版本控制)

我們新增個檔案，指令
```terminal=
echo "add file" >> index.html
（語法+ "新增動機" + >> +檔案名字）
```

使用 `git add 剛剛新增的檔案名字`，來加入 git ，
接著使用 `git status` 來查看顯示目前狀態，
出現了：
```iterm2=
Changes to be commited:
    (use"git rm" --created <file>..."to unstage) 
    //上述 => 使用 git rm 來取消暫存
    new file:  index.html //剛剛成功新增的檔案
```
示意圖如下↓
![](https://i.imgur.com/qwIDlGn.gif)

### git commit 提交更改事件

這個指令可以把更動過的事件，提交給 git 版本庫(存檔的概念)
下方使用的指令是 git commit 的小變化，
為了讓我們可以去更了解每次更改檔案的動機，
可以命名存檔 `git commit -m "動機"`，
![](https://i.imgur.com/BDGC8L6.png)

### git push 發布至遠端專案

此指令可以將我們本地端的專案推送到遠端：github等網站。

### git clone 下載遠端專案

此指令則是可以讓我們從遠端下載專案到本機端。

---
### git branch 查看分支

此指令可以去觀看目前有哪些分支以及分支的名字。
![](https://i.imgur.com/T8TSGca.png)

---
### git branch +"分支名稱" (建立新分支)

![](https://i.imgur.com/ukjC60D.png)

---
### git checkout +"分支名稱" (切換分支)

![](https://i.imgur.com/LESxyil.png)

---

### git branch -d +"分支名稱" (刪除分支)

**小重點：不得刪除當前所在的分支，必須切換到其他分支，才能夠刪除分支**

錯誤狀況示意圖↓
![](https://i.imgur.com/2ESF0Fc.png)

正確切換到其他分支，執行刪除分支示意圖↓
![](https://i.imgur.com/TP2RpqZ.png)
