---
title: Python flask 環境安裝
date: 2021-05-02
description: 此文章僅限 Mac 系統安裝方法。
categories:
  - Backend
tags:
  - Backend
---

## 1. Python 環境準備 (MAC)

我們要在 Mac 環境安裝

- Python3
- pip3

### 使用 homebrew 安裝 Python 3

```base
brew install python
```

> 檢查目前 Python 的版本

```base
python --version
```

> 如果顯示的版本是 Python 2，那麼試著下面的指令

```base
python3 --version
```

> 看看是否是 Python 3

### 確認 pip 是否安裝成功

pip 是 python 的套件管理工具，但是並非等於 npm，更加類似於 mac 的 homebrew，或是 ubuntu 中的 apt install 這樣的工具

這次我們要使用的 python 版本為 python3 ，所以要安裝 pip3

```base
pip3 install pipenv
```

![image](https://i.imgur.com/Vx59LO4.png)

如果顯示的是 3.x 版本，是正確的

如果不是的話，試著使用 `pipenv`，看看顯示的是否是 Python 3.x 版本而非 2.x 版本

![image](https://i.imgur.com/Ae1LvMJ.png)

原因在於 Python 2 已經停止維護，所以無論是 Python 的版本或是 pip 的版本，都需要使用 3.x 以上的版本。

## 3. 安裝 pipenv 管理工具 (通用)

pipenv 可以看作是 node.js 中的 npm (Node Package Manager)

然而實作上不太一樣，這是 python 獨有的背景與設計。

但是使用方式跟 npm 很相似

輸入安裝指令後

```base
pipenv install flask
```

開始安裝畫面

![image](https://i.imgur.com/Bhb2q39.png)

接著，我們看看資料夾多了什麼東西

```base
❯ ls
01 installation.md Pipfile            Pipfile.lock       img
```

增加了兩個 Pipfile 與 Pipfile.lock  這兩個檔案

輸入 `cat Pipfile` 後，即可發現剛剛安裝的 flask 已經安裝完畢

![image](https://i.imgur.com/hLxAS1r.png)
