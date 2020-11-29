---
title: GitHub Pages + Hexo跨設備同步
date: 2020-11-29 15:52:09
categories:
- [Web, Hexo]
tags:
- GitHubPages
- Git
- Hexo
---

利用Hexo建立好GitHub Pages後，如果想要在不同設備上發布文章的話該怎麼做?

<!-- more -->

---

## 前置作業

[GitHub Pages + Hexo搭建NexT主題Blog](https://yafun92386.github.io/2020/11/28/GitHubPags-HexowithNexT/)

發布至GitHub後，可以看到main有Blog相關文件，但之中並不包含Hexo的配置，
因此需上傳Hexo的配置文件，就可以透過git在不同設備上進行同步操作。

---

## 原設備操作

在建置好Hexo的資料夾下上將資料git到GitHub。

### 上傳Hexo配置

```
// git 初始化
$ git init
// 對應遠端位置
$ git remote add origin https://github.com/<username>/<username>.github.io.git
// 新建分支
$ git checkout -b <branchname>
// 添加檔案到git
$ git add .
// 提交
$ git commit -m "<message>"
// 推送
$ git push origin <branckname>
```

---

## 其他設備操作

透過GitHub上的資料，即可在其他設備上進行同步操作。

### 同步資源

#### 初次複製

將GitHub上的資料複製至本機端
```
// 將遠端資料複製下
$ git clone -b <branchname> https://github.com/<username>/<username>.github.io.git
```
> 需安裝Hexo與必須套件，不需初始化:hexo init (已從GitHub上複製下配置參數)

#### 後續同步

```
// 遠端與本地同步
$ git pull origin <branchname>
```

---

同步完資源後，就可以在本機端編寫文章並上傳。

### 編寫文章

```
// 建立新文章編輯
$ hexo new "title"
```

### 同步資源至GitHub

```
// 添加檔案文件
$ git add .
// 提交
$ git commit -m "<message>"
// 推送
$ git push origin <branchname>
```

### 更新Blog

```
$ hexo clean && hexo generate && hexo deploy
```

---

## 參考資料

[如何解決github+Hexo的部落格多終端同步問題](https://www.itread01.com/content/1546966625.html)
[hexo 博客搭建——多设备同步 hexo 搭建的 GitHub 博客](https://lishide.github.io/2018/02/12/hexo-blog-multi-sync/)