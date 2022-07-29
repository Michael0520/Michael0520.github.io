---
title: 初探 GitHub
description: 請記得它的 G 跟 H 是大寫，其它字母小寫。它是一個商業網站，是目前全球最大的 Git Server。在這邊，你可以跟其它厲害的開發者們交朋友，你可以幫忙貢獻其它人的專案，其它人也可以回饋到你的專案，建立良性循環。
date: 2020-11-10
categories:
- Git
tags: 
- Git
---

### 延續上篇筆記 ([Git 基礎介紹筆記](https://hackmd.io/@uOQ-3fQDQBu7CciMuKIplg/git_origin))


> #### 在開始介紹 GitHub 之前!
> 請記得它的 G 跟 H 是大寫，其它字母小寫。它是一個商業網站，是目前全球最大的 Git Server。在這邊，你可以跟其它厲害的開發者們交朋友，你可以幫忙貢獻其它人的專案，其它人也可以回饋到你的專案，建立良性循環。
> 
> 同時，它也是開發者最好的履歷。你曾經做過哪些專案、做過哪些貢獻、寫過哪些 Code，一目了然，想要假造非常花工夫。
> 
> 如果你是上傳 Open Source 專案的話，可以完全免費使用。如果想要在上面開私人專案的話則需要收費，費用是每個月 7 塊錢美金。
> 
> 補充：Microsoft 在 2018 年 10 月併購了 GitHub，以往需要付費才能開設私人專案，在 2019 年 1 月宣佈即使是免費帳號也可無限制的開設私人專案。(讚！)

---
首先到 [GitHub](https://github.com/) 上創辦帳號，
要上傳檔案到 GitHub，需要先在上面開一個新的專案。請先在 GitHub 網站的右上角點選「+」號，並選擇「New repository」：

![](https://i.imgur.com/0QK2wEe.png)

Repository name 可填寫任意名稱，只要不重複即可。

存取權限選擇 Public 可免費使用，選擇 Private 則需收每個月 7 元美金的月費。
補充：在 GitHub 被 Microsoft 併購後，現在即使是免費帳號也都可以開立 Private 專案喔。

按下「Create repository」即可新增一新的 Repository。
![](https://i.imgur.com/buflo3j.png)

接下來，會看到的這個引導畫面：
![](https://i.imgur.com/1NSeODQ.png)

> 說明：
>如果是全新開始，請依「create a new repository on the command line」的內容指示進行；如果是要上傳現存專案，則依照「push an existing repository from the command line」選項進行。
畫面中間上面，有兩個按鈕可以切換，分別是「HTTPS」以及「SSH」。至於要選擇哪一個可看個人喜好，但選擇 SSH 的話需要設定 SSH Key，SSH Key 的設定可參閱「GitHub 是什麼？」章節介紹。因為我已經有設定好 SSH Key，所以這裡我選擇「SSH」。

如果仔細觀察，便會發現選擇全新開始跟上傳現有專案這兩個選項的最後兩個步驟是一樣的。

假設我們現在什麼都沒有，要重新開始一個專案，找一個空的目錄，就照著它的說明進行。
首先，先建立一個 README.md 檔案：

`echo "# task08" >> README.md`

這個 README.md 是 GitHub 專案的預設說明頁面，附檔名 .md 表示它是一個 Markdown 格式，Markdown 語法可以很輕鬆的把純文字格式轉換成 HTML 的網頁格式。

接下來這段，就是上個篇章我們熟悉的 Git 了：

```terminal=
$ echo "# task08" >> README.md 
$ls
README.md
$git init
Initialized empty Git repository in /Users/luoziming/coding~/task08/.git/
$git add README.md 
$git commit -m "first commit"
[master (root-commit) 8f46b63] first commit
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
 
```
![](https://i.imgur.com/UoBiisM.png)

在這之前，我們所有的操作都是在自己電腦上，接下來就是要準備把東西推上遠端的 Git 伺服器了。首先，需要設定一個端節的節點，例如：

`git remote add origin https://github.com/Michael0520/task08.git`

> 說明：
`git remote` 指令，顧名思義，主要是跟遠端有關的操作。
`add` 指令是指要加入一個遠端的節點。
在這裡的 origin 是一個「代名詞」，指的是後面那串 GitHub 伺服器的位置。
在慣例上，遠端的節點預設會使用 origin 這個名字。如果是從 Server 上 clone 下來的話，它的預設的遠端節點就會叫 origin。（關於 Clone 的使用，請參閱「從伺服器上取得 Repository」章節說明）

不過別擔心，這只是個慣例，不用這名字或是之後想要改也都可以，
如果想改叫神奇寶貝 ：

`git remote add Pokemon git@github.com:Michael0520/task08.git`

總之，它就是只是指向某個位置的代名詞罷了。設定好遠端節點後，接下來，就是要把東西推上去了：

```iterm=
$ git push -u origin master
Counting objects: 3, done.
Writing objects: 100% (3/3), 224 bytes | 224.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To github.com:Michael0520/task08-git.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
```
![](https://i.imgur.com/8QoHqp2.png)

這個簡單的 Push 指令其實做了幾件事：

1. 把 master 這個分支的內容，推向 origin 這個位置。
2. 在 origin 那個遠端 Server 上，如果 master 不存在，就建立一個叫做 master 的同名分支。
但如果本來 Server 上就存在 master 分支，便會移動 Server 上 master 分支的位置，使它指到目前最新的進度上。
3. 設定 upstream，就是那個 -u 參數做的好事，這個稍候說明。

如果你能理解上面這個指令的意思，你就可以再做一些變化。
例如你的遠端節點叫做 Pokemon，而且你想把 cat 分支推上去：

`git push Pokemon cat`

這樣就會把 cat 分支推上 Pokemon 這個遠端節點所代表的位置，
並且在上面建立一個名為 cat 同名分支（或更新進度）。

回到 GitHub 網站，重新整理一下頁面，剛才那個引導指令的畫面，現在應該會變這樣：

![](https://i.imgur.com/nHHwslq.png)

**這樣就成功完成 `git push` 到 GitHub 上了！**
