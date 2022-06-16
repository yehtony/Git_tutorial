# **Git 還原**
###### tags: `Git` `Github`
* [Git 還原](https://w3c.hexschool.com/category/Git%20%E9%82%84%E5%8E%9F)
## **還原檔案**
###  工作目錄新增檔案，但尚未加入追蹤，想清除檔案
#### 1. 顯示未追蹤檔案
> #### git clean -n
``` git
$ git clean -n
Would remove merge.js
```
#### 2. 強制清除檔案
> #### git clean -f (全部) / git clean -f <file name> (單一)
``` git
$ git clean -f merge.js
Removing merge.js
```
### 還原工作目錄上已更改的檔案
#### 1. 顯示目錄檔案
``` git
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   index.html
        modified:   master.js
```
#### 2. 還原檔案
> #### git checkout . (全部) / git checkout -- <file name> (單一)

``` git
$ git checkout .
Updated 2 paths from the index
```
### 檔案已加入索引，想還原到工作目錄
#### 1. 查看索引檔案
> #### git checkout
``` git
$ git checkout
M       all.js
M       index.html
```
#### 2. 還原檔案
> #### git reset HEAD
``` git
$ git reset HEAD
Unstaged changes after reset:
M       all.js
M       index.html
```
## **git reset - 還原版本**
![](https://i.imgur.com/URzgyKY.png)
### 保留檔案
**假如今天想回到前一個版本，但想保留目前版本的檔案
*HEAD^* 表示從HEAD往前推一個commit，^表示回推的數量，ex. ^^^ 表示往回三個版本**
> #### git reset HEAD^
``` git
$ git reset HEAD^
Unstaged changes after reset:
M       all.js
M       index.html
```
![](https://i.imgur.com/jSS0O93.png)
    
**可以看到上個版本檔案被保留下來，但HEAD回到前一個版本；可以把檔案再次commit到數據庫。**
### 不保留檔案
**假如今天想清除整個版本包括檔案**
> #### git reset HEAD^ --hard
``` git
$ git reset HEAD^ --hard
HEAD is now at b25f182 合併網頁
```
![](https://i.imgur.com/c0Tdbn6.png)
    
**可以看到HEAD回到前一個版本，上個版本也完全清除了。**   
:::warning
注意HEAD可以改成SHA-1編號，只接指定版本進行還原；^ 也可以用~代替，或是^後面直接加數字表示回推數量，ex. ^3表示回推三個版本。
:::

