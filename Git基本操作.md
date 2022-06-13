# **Git 基礎操作**
###### tags: `Git` `Github`
* [Git 基礎操作](https://w3c.hexschool.com/category/Git%20%E5%9F%BA%E7%A4%8E%E6%93%8D%E4%BD%9C)
## **git init - 新建數據庫**
### 1. 新增一個資料夾，並右鍵點擊資料夾以 *Git Bash* 開啟
![](https://i.imgur.com/d9rmG07.png)
### 2. 輸入 *git init*
:::info
```yehto@XuanYe MINGW64 ~/OneDrive/桌面/NCU/Git課程/git init (master)
yehto@XuanYe MINGW64 ~/OneDrive/桌面/NCU/Git課程/git init (master)
$ git init
Initialized empty Git repository in C:/Users/yehto/OneDrive/桌面/NCU/Git課程/git init/.git/
```
此時新建Repository成功，會在你的資料夾建立一個.git資料夾，任何版本都會透過它進行監控
:::
## **git add & git commit - 提交版本**
### 1. 在資料夾內新增一個檔案
```
$ touch index.html
```
### 2. 輸入 *git status*
:::success
```
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        index.html

nothing added to commit but untracked files present (use "git add" to track)
```
可以看到Untracked files有剛新增的檔案，Untracked的意思是Git偵測到你有新增這筆檔案，但尚未是Git追蹤的對象。
:::
### 3. 輸入 *git add*
* ####  git add <檔案名稱>
:::info
```
$ git add index.html
```
*git add* 將檔案加入索引，就可以將檔案加入到Git追蹤的對象
:::
* #### git add .
:::info
```
$ git add .
```
也可以用 *git add .* 將資料夾內所有檔案加入索引
:::
### 4. 再次輸入 *git status*
:::success
```
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   index.html
```
可以發現檔案從Untracked files變成Changes to be committed，這樣就表示成功加入索引。
:::
### 5. 輸入 *git commit*
* #### git commit -m "<填寫版本資訊>"
:::info
```
$ git commit -m "version 1"
[master (root-commit) 055a2a7] version 1
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 index.html
```
*git commit* 將放在索引的檔案提交(commit)成一個新版本。
:::
### ６. 再再次輸入 *git status*
:::success
```
$ git status
On branch master
nothing to commit, working tree clean
```
發現已經將剛剛的檔案commit成一個版本，所以目前工作目錄上已經清空。
:::
## **git log - 查詢版本**
:::success
```
$ git log
commit 055a2a7d5cc45d85a5da1d57c2e683508754f612 (HEAD -> master)
Author: XuanYe <yexuanncu@gmail.com>
Date:   Mon Jun 13 23:36:39 2022 +0800

    version 1
```
看到剛才commit的版本更新紀錄，表示成功了!
:::