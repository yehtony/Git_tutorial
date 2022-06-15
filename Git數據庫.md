# **Git 數據庫**
###### tags: `Git` `Github`
* [Git 數據庫](https://w3c.hexschool.com/category/repo)
## **Git 流程圖**
![](https://i.imgur.com/8fbdpqz.png)
## **Github - 遠端數據庫**
### [Github](https://github.com/)
## **git remote add - 添加遠端數據庫**
### 1. Github創建數據庫(Repository)  
![](https://i.imgur.com/cVZgBzn.png)
#### Repository URL
![](https://i.imgur.com/nNvYsRR.png)
### 2. 本地新增遠端數據庫
#### Git Bash開啟資料夾，輸入指令
> #### git remote add <repository name> <repository url>  
:::info
``` git
$ git remote add origin https://github.com/yehtony/Git_practice.git
```
*git remote add* 表示在本地添加遠端數據庫 。 
:::
:::success
``` git
$ git remote
origin
```
輸入 *git remote* 可以看到遠端數據庫名稱，代表添加成功。
:::
## **git push - 更新遠端數據庫**
### 當本地資料新於遠端資料，推送本地資料來使資料同步
> #### git push <repository name> <branch name>
:::info
``` git
$ git push -u origin master
Enumerating objects: 10, done.
Counting objects: 100% (10/10), done.
Delta compression using up to 12 threads
Compressing objects: 100% (7/7), done.
Writing objects: 100% (10/10), 905 bytes | 905.00 KiB/s, done.
Total 10 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), done.
To https://github.com/yehtony/Git_practice.git
 * [new branch]      master -> master
branch 'master' set up to track 'origin/master'.
```
*git push* 表示將本地資料推送到遠端數據庫。
*branch 'master' set up to track 'origin/master'* 表示成功將資料推送到遠端數據庫分支。
:::
## **git pull - 抓取遠端數據庫資料**
### 當遠端資料新於本地資料，抓取遠端資料來使資料同步
> #### git pull
:::info
``` git
$ git pull
remote: Enumerating objects: 9, done.
remote: Counting objects: 100% (9/9), done.
remote: Compressing objects: 100% (6/6), done.
Unpacking objects: 100% (6/6), 1.35 KiB | 137.00 KiB/s, done.
remote: Total 6 (delta 1), reused 0 (delta 0), pack-reused 0
From https://github.com/yehtony/Git_practice
   97edecf..312c2b4  master     -> origin/master
Updating 97edecf..312c2b4
Fast-forward
 all.css    | 5 +++--
 index.html | 4 ++--
 2 files changed, 5 insertions(+), 4 deletions(-)
```
*git pull* 表示將遠端資料抓取至本地數據庫。
可以看到 *Updating* 表示成功更新資料
:::
:::success
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
*git log* 可以看到新的 *commit* ，是從遠端抓下來的資料。
:::
## **git clone - 複製遠端數據庫**
#### Repository URL
![](https://i.imgur.com/4X86SRU.png)
#### 新建一個資料夾並以Git Bash開啟
> #### git clone <repository url>
:::info
``` git
$ git clone https://github.com/yehtony/Git_practice.git
Cloning into 'Git_practice'...
remote: Enumerating objects: 16, done.
remote: Counting objects: 100% (16/16), done.
remote: Compressing objects: 100% (12/12), done.
remote: Total 16 (delta 2), reused 9 (delta 1), pack-reused 0
Receiving objects: 100% (16/16), done.
Resolving deltas: 100% (2/2), done.
```
*clone* 遠端數據庫到指定資料夾。
``` git
$ ls
Git_practice/
```
``` git
$ git remote
origin
```
*ls* 可以看到資料夾新增了一個遠端複製下來的數據庫，它擁有一樣的版控，
且用 *git remote* 可以發現本地自動新增了該遠端數據庫。
:::
