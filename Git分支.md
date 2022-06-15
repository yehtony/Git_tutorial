# **Git 分支**
###### tags: `Git` `Github`
* [Git 分支](https://w3c.hexschool.com/category/branch)
## **HEAD**
### HEAD就是你目前指向的版本狀態，而HEAD可以選擇它指向到

* **分支 (branch)** 
* **commit 版本**

![](https://i.imgur.com/rAhQGnp.png)
#### master是本地預設分支名稱，串起分支內的commit，此時HEAD是跟著master一起前進的，是目前最新的版本。
#### 此時想切換成其他版本，就要用 *git checkout* 移動HEAD，讓它指向其他commit。
## **git checkout - 切換版本**
:::info
``` git
$ git log
commit 312c2b4eb6ef6cdf2158044eb962e41794cd605c (HEAD -> master, origin/master)
Author: YehTony <66704016+yehtony@users.noreply.github.com>
Date:   Tue Jun 14 18:54:39 2022 +0800

    Update index.html

commit 39ed4020684ed4cb909810b71effb84dc69fb735
Author: YehTony <66704016+yehtony@users.noreply.github.com>
Date:   Tue Jun 14 18:54:19 2022 +0800

    Update all.css
```
目前可以看到分支上有兩個版本，且HEAD是指向master，我們現在想讓它移到前一個commit。
:::
#### 這裡我們要透過commit的SHA-1碼來進行checkout，就是commit後的那一串亂碼，它代表了那個commit。
> #### git checkout <commit SHA-1>
:::info
``` git
$ git checkout 39ed4020684ed4cb909810b71effb84dc69fb735
Note: switching to '39ed4020684ed4cb909810b71effb84dc69fb735'.
```
*git checkout* 後可以看到 *switching to* 指定的commit。
:::
:::success
``` git
$ git log
commit 39ed4020684ed4cb909810b71effb84dc69fb735 (HEAD)
Author: YehTony <66704016+yehtony@users.noreply.github.com>
Date:   Tue Jun 14 18:54:19 2022 +0800

    Update all.css
```
``` git
$ git status
HEAD detached at 39ed402
```
查看log和status也會發現版本切換到指定的commit，HEAD也指向現在的commit。
:::
--- 
### ==接下來的部分會以Sourcetree演示，因為以程式碼方式呈現會過於龐雜==
## **git branch - 建立分支**
### 方便進行不同版本的開發與管理
#### 1. 原本的分支master(2個commit，HEAD>master)
![](https://i.imgur.com/eEzTM9h.png)
#### 2. 新增一個分支dev
> #### git branch <branch name>
``` git
$ git branch dev
```
![](https://i.imgur.com/FllFRPr.png)
#### 3. 切換到分支dev
``` git
$ git checkout dev
```
![](https://i.imgur.com/o4teYvL.png)
#### 4. 新增檔案all.js，並且commit
``` git
$ touch all.js
$ git add .
$ git commit -m "新增js"
```
![](https://i.imgur.com/Fl4Mxpl.png)
#### 最後可以看到dev branch新增了版本，而master branch停留在原始版本，這樣我們就可以利用branch來達到更好的版本控制。
## **git branch - 合併分支**
### 用來合併版本
* ### 快轉合併 - fast-forward
    1. dev建立出來時，是跟master在相同的commit上，c2(新增css)可以當做是dev的初始commit位置，假設接下來我們更新了dev。
    2. 過程中，若master沒有任何更新，表示master停留在c2的位置，此時用master去merge dev就會觸發快轉合併。
    * 綜合以上兩點，當你的HEAD位置是merge branch的初始commit，就會觸發快轉合併；簡單來說就是你目前的branch被完全包含於merge branch裡。
#### 1. 切換回master branch
``` git
$ git checkout master
```
![](https://i.imgur.com/gS4KtfF.png)
#### 2. 合併分支
> git merge <branch name>
``` git
$ git merge dev
```
![](https://i.imgur.com/zvV5jvW.png)
#### 此時master移動到c3(新增js)，與dev同步版本。
* ### 非快轉合併 - no-fast-forward
    1. 首先一樣更新dev。
    2. 這次在過程中，master也更新了其他版本，代表master已經不在c2的位置，這時merge dev就會觸發非快轉合併。
    * 與fast-foward相反，當你目前的branch不完全被包含於merge branch裡。

#### ==操作前注意HEAD是指向master==
#### 先變回原始環境(指令之後再解釋)
```
git reset HEAD^ --hard
```
![](https://i.imgur.com/gS4KtfF.png)
#### 1. 新增檔案master.js，並且commit
``` git
$ touch master.js
$ git add .
$ git commit -m "新增js"
```
![](https://i.imgur.com/M6aHGy5.png)
可以看到master branch和dev branch從c2後產生分岔，此時master已經不完全包含於dev。
#### 2. 合併分支
``` git
$ git merge dev
```
此時因為合併衝突會進入merge編輯器並出現下列訊息
``` git
Merge branch 'dev'
# Please enter a commit message to explain why this merge is necessary,
# especially if it merges an updated upstream into a topic branch.
#
# Lines starting with '#' will be ignored, and an empty message aborts
# the commit.
```
輸入指令 *:wq* 離開即可
``` git
:wq
```
![](https://i.imgur.com/fMsEJMO.png)
此時看到master合併了dev的commit並且多了一個commit(c5)，因為c3和c4同時對c2進行修改，必須多出一個c5紀錄這兩個commit，這樣的合併在git中稱為三路合併。