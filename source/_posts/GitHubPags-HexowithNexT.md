---
title: GitHub Pages + Hexo搭建NexT主題Blog
date: 2020-11-28 20:14:56
categories: 
- [Web, Hexo]
tags:
- GitHubPages 
- Git
- Hexo
---


想要做些筆記，留下一點紀錄，於是有了這個網站與這篇文誕生...
<!-- more -->

---

GitHub Pages是GitHub提供的一個網頁代管服務，用以呈現靜態網頁。

## 建立 GitHub Page

在GitHub上建立新專案
專案名稱必須是 `<username>.github.io`

複製專案到local端
```
 $ git clone <github.io>
```

接下來即可建立網頁並上傳到GitHub瀏覽頁面
```
$ git add index.html
$ git commit -m "<message>"
$ git remote add origin <github.io>
$ git push -u origin main
```

---

善用靜態網頁產生器(Static Site Generator, SSG)快速佈署網頁。

## 安裝 Hexo

```
// 先安裝Node Package Manager(Node.js套件管理工具)
$ apt install npm
// 安裝Hexo
$ npm install hexo-cli -g
```
> ```
> // 安裝Hexo發生問題
> throw new TypeError('Console expects a writable stream instance');
> // 更新nodejs version
> $ npm install -g n
> $ n latest
> // reset the command location
> $ PATH="$PATH"
> ```
```
// 建立資料夾
$ hexo init <foldername>
// 安裝套件
$ npm install
// 安裝git佈署套件
$ npm install hexo-deployer-git --save
```

---

### 設定Hexo相關資訊

進入設定好的Hexo資料夾開啟_config.yml編輯

```
# Site
title: 標題
subtitle: 副標題
description: 網站描述
keywords: 網站關鍵字
author: 作者姓名
language: 語言
timezone: 空白使用系統時間
```
```
# URL
url: http://<username>.github.io
```
```
# Deployment
deploy:
  type: git
  repo: https://github.com/<username>/<username>.github.io.git
  branch: main
```

---

預設主題看不慣?那試試眾多開源者貢獻的NexT主題吧!

## 套用 NexT 主題

在`/themes/`資料夾中把NexT主題複製下來
```
$ git clone https://github.com/theme-next/hexo-theme-next.git
```
修改Hexo`_config.yml`中theme成`hexo-theme-next`

---

嘗試自己改改NexT配置，或加入需要的插件

### Next 設置

可以參考 [NexT使用文檔](https://theme-next.iissnan.com/) 設置

---

## 佈署至GitHub
```
// 清除之前建立的靜態檔案
$ hexo clean
// 建立靜態檔案
$ hexo generate
// 佈署至GitHub Pages
$ hexo deploy
```

---

### 參考資料

[GitHub Pages](https://pages.github.com/)
[Hexo](https://hexo.io/zh-tw/)
[hexo-theme-next](https://github.com/theme-next/hexo-theme-next)
[NexT使用文檔](https://theme-next.iissnan.com/)