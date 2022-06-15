
#  **Git 環境架設**
###### tags: `Git` `Github`
* [Git 環境教學](https://w3c.hexschool.com/category/Git%20%E7%92%B0%E5%A2%83%E6%95%99%E5%AD%B8)
## **Git 是什麼**
#### Git是一個分散式版本控制軟體，版本控制能夠記錄檔案的內容變化，並且能夠查詢每個版本所更動的內容。
## **Git 環境建置**
### Git安裝
#### 1. 連接到[Git官網](https://git-scm.com/)
#### 2. 點擊下載按鈕
![](https://i.imgur.com/tJKAt7p.png)
#### 3. 點擊Click here to download
#### 4. 下載後啟動執行檔，一路下一步即可完成安裝
### 確認環境
#### 1. 電腦搜尋列輸入Git Bash並打開
#### 2. 輸入 *git --version*
:::success
``` git
yehto@XuanYe MINGW64 ~
$ git --version
git version 2.36.1.windows.1
```
如果出現Git版本編號代表安裝成功了!
:::
### 設定個人資訊
#### 1. 接續在Git Bash輸入下列指令，引號內換成個人資訊
:::info
``` git
git config --global user.name "您的姓名"
git config --global user.email "您的Email"
```
這樣當Git版本發佈時，會記錄該版本是哪位開發者做的。
:::
#### 2. 輸入 *git config --list*
:::success
``` git
yehto@XuanYe MINGW64 /
$ git config --list
user.name=XuanYe
user.email=yexuanncu@gmail.com
```
可以看到 *user.name* 和 *user.email* 為你輸入之個人資訊
:::