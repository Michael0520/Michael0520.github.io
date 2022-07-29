---
title: Command Line 指令
description: 紀錄 Command Line 學習過程。
date: 2020-12-08
categories:
- Git
tags: 
- Git
---



#  Command Line 指令

#### 1. `cd` (change directory）
> 用來切換目錄的指令。

**變化型**
> 1. 回到 home 目錄：cd ~ # 屬於使用者底下的資料夾
> 2. 回到根目錄：cd / # 電腦最底層
> 3. 回到上一層資料夾：cd ..

**小訣竅**
> 1. 當輸入 cd 空格 時，按 tab 會幫你自動列出底下的資料夾列表。 會出現像是輸入 ls 的效果，方便查詢 。
> 2. 輸入前幾個字母，再按一次 tab 會幫你自動補完資料夾名稱。（大推!）
> 3. 回到桌面： ~/desktop


---

#### 2. `pwd` （print working directory）
> 顯示目前所在目錄的指令。


---

#### 3. `ls` (list)
> 列出所有檔案和路徑。
顯示後可使用 command ＋右鍵直接點選開啟

**變化型**
> 1. 列出隱藏的目錄：ls -a
> 2. 列出詳細資料：ls -l
> 3. 包上述兩個：ls -la
> 4. 列出 .js 的檔案：ls *.js


---

#### 4. `cat`（catenate）
> 將檔案內容列出的指令。

```
>luo test % cat dog.txt
>i'm a dog!
```
---

#### 5. `mkdir` （make directory）
> 新建資料夾。
> 寫法：`mkdir 資料夾名稱`
> 舉例：`mkdir test01`

---

#### 6. `touch`
> 碰一下檔案
> 寫法：touch 檔名
> 
> 情況一：假設檔案不存在，就會建立一個新的檔案。
> 情況二：假設檔案存在，更改檔案些改時間。

---

#### 7. `code`
> 使用 文字編輯器打開你的檔案

---

#### 8. `tar`
> 壓縮檔案
> 範例：
> ```
> tat -czf (壓縮檔的名字（可命名）,.gz(壓縮檔的格式),要壓縮的檔案名字)
> tar -czf amimals.gz cat.txt
> ```

---
#### 9. `open .`
> 使用finder 打開當前位置的資料夾
---
#### 10. `rm` （remove）
> 刪除檔案，這邊的刪除檔案是「直接刪除」，並不會進到垃圾桶中，因此使用時要小心。

>**變化型：**
> 1. `rmdir` （remove directory）：刪除空資料夾，若資料夾內有檔案就無法刪除。
> 2. `rm -rf` ：刪除整個檔案或整個資料夾 ＃謹慎使用，刪掉就真掰掰了。

>**小訣竅**
> 1. 當刪除的檔名帶有空格或特殊字元時可使用單引號將檔名括起來，舉例：rm '要 刪 除 的 檔 名'。
---
#### 11. `mv`(move)
> **用法一**
> 1. 移動檔案
> 2. 寫法：mv 檔名 路徑 ＃要注意相對路徑跟絕對路徑的差異。
> 3. 舉例：
相對路徑：mv file folder ＃以 desktop 為 home 目錄。
絕對路徑：mv file /Users/luo/desktop
補充說明：將檔案移動到上一層，就必須使用絕對路徑的寫法來移動

> **用法二**
> 1. 改檔名
> 2. 寫法：mv 原檔名 新檔名
> 3. 舉例：mv originalFile newFile

---

#### 12. `clear`
> 清空 Terminal 面版。
 
---

#### 13. `exit`
> 關閉 Termainal 。
> 
---

#### 14. `date`
> 印出現在時間。

---
## 補充：
> 指令後方加上`--help`，會顯示這個指令該如何做使用



