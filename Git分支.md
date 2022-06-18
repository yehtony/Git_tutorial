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
:::danger
**註明：接下來的部分會以Sourcetree演示，因為以程式碼方式呈現會過於龐雜**
:::
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
## **git merge - 合併分支(保留分支紀錄)**
### 用來合併版本
:::danger
**註明：接下來會以c來代稱commit，由下到上會依數字小到大表示，例如c1是第一個commit**
:::
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
:::warning
no-ff有兩種情況，無衝突合併和衝突合併。無衝突代表兩個branch在同一檔案之間內容沒有衝突(通常只要修改同一檔案就會發生衝突，除非修改內容一樣)；而衝突代表兩個branch在同一檔案之間有不同修改(內容)，造成合併衝突。
:::
* ### 無衝突合併
    1. 首先一樣更新dev。
    2. 接著在過程中，我們也更新了master(這裡我們用新增檔案的方式來避免衝突)，代表master已經不在c2的位置，這時merge dev就會觸發非快轉合併。
    * 與fast-foward相反，當你目前的branch不完全被包含於merge branch裡。

#### ==操作前注意HEAD是指向master==
#### 先回到初始環境(退回合併前，指令之後再解釋)
``` git
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
此時會進入merge編輯器並出現下列訊息
``` git
Merge branch 'dev'
# Please enter a commit message to explain why this merge is necessary,
# especially if it merges an updated upstream into a topic branch.
#
# Lines starting with '#' will be ignored, and an empty message aborts
# the commit.
```
可以輸入commit說明訊息或直接輸入指令 *:wq* 離開即可
``` git
:wq
```
![](https://i.imgur.com/fMsEJMO.png)

#### 此時看到master合併了dev的commit並且多了一個commit(c5)，因為c3和c4同時對c2進行修改，必須多出一個c5紀錄這兩個commit，這樣的合併在git中稱為三路合併。
* ### 衝突合併
#### 退回合併前
``` git
git reset HEAD^ --hard
```
![](https://i.imgur.com/M6aHGy5.png)
:::danger
**註明：下面我把master的新增js改成新增master.js，避免混淆**
:::
#### 1. 對dev及master進行修改，並各進行一次commit，(這邊我修改了html和css檔)
#### ==記住要先checkout到指定的branch再進行修改，commit前記得先加入(add)==

![](https://i.imgur.com/XLb1HY7.png)

可以看到兩個branch各多了一個commit，c5(dev網頁)、c6(master網頁)，
#### 2. 合併分支
```
$ git merge dev
Auto-merging all.css
CONFLICT (content): Merge conflict in all.css
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```
![](https://i.imgur.com/IOGETYG.png)

**這時會發生衝突，可以看到程式碼出現 *merge conflict in all.css / index.html*，因為兩個branch修改了同一個檔案，所以merge commit無法確認檔案內容。**
    
**這裡有兩種選擇：**
* #### 直接取消合併
```
git merge --abort
```
* #### 修改衝突檔案
我們要打開檔案進行修改，可以看到Stage files裡有警示號的檔案代表衝突，點開進行修改與確認。
``` css=
body {
    background-color: teal;
    color: royalblue;
<<<<<<< HEAD
}

div {
    color: mediumvioletred;
=======
>>>>>>> dev
}
```
可以看到檔案包含了c5與c6的修改內容，從 <<<<<<< *HEAD* 到 ======= 代表HEAD，也就是master的修改內容，而 ======= 到 >>>>>>> *dev* 代表dev的修改內容，這裡我們要決定commit的檔案內容，確認完無誤後儲存檔案。
    
#### 3. 重新commit
將檔案新增到索引後會發現衝突消失了。

![](https://i.imgur.com/MA62LbU.png)
    
這時將修改過的檔案重新commit
    
![](https://i.imgur.com/oLgbvaZ.png)

**合併成功，多出c7(合併網頁)。**
## git rebase - 合併分支(合併分支紀錄)
#### 一樣先退回合併前，並切換到指定的branch
#### ==與merge不同，merge是切換到要merge的分支(master)，rebase是切換到要被merge的版分支(dev)==
#### 1. 合併分支
> #### git rebase <branch name>
``` git
$ git rebase master
```
![](https://i.imgur.com/yI4rOZj.png)
* #### 取消合併
``` git 
git rebase --abort
```
* #### 合併分支
``` git
$ git add .
$ git rebase --continue
```
![](https://i.imgur.com/Uv2ZFmd.png)
    
可以看到個dev合併到分支，但master與dev版本不同。
#### 2. 同步版本
``` git
$ git checkout master
$ git merge dev
```
![](https://i.imgur.com/rj5lj1a.png)
    
**合併成功，兩個branch版本同步，且原本dev分支紀錄清除。**


