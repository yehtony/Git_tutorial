# **Git 練習**
###### tags: `Git` `Github`
## **Git 提交版本**
### 步驟
#### 1. 進入資料夾
#### 2. 新增一個html檔
#### 3. 提交第一個版本
#### 4. 新增一個css檔，並編輯html檔(嵌入css檔)
#### 5. 提交第二個版本
### 結果
:::success
``` git
$ git log
commit c0678264182124bf44099cab31d3046bd3d08517 (HEAD -> master)
Author: XuanYe <yexuanncu@gmail.com>
Date:   Tue Jun 14 12:48:55 2022 +0800

    插入css

commit ff91befae862883af788f730e4324ff65eb91929
Author: XuanYe <yexuanncu@gmail.com>
Date:   Tue Jun 14 12:36:50 2022 +0800

    新增html
```
*git log* 會出現兩個版本
:::
:::spoiler 解答
``` git
$ git init
$ touch index.html
$ git add .
$ git commit -m "新增html"
$ touch all.css
# 編輯html檔 #
$ git add .
$ git commit -m "插入css"
```
::: 
## **Git 分支**
### [Learn Git Branching](https://learngitbranching.js.org/?locale=zh_TW)