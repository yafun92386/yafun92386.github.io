---
title: "[Markdown] Markdown語法整理"
date: 2020-11-30 18:18:45
categories: 
- [Language, Markdown]
tags: 
- Markdown
--- 

Hexo使用Markdown來編寫文章，因此來整理一些需要的語法。

<!-- more -->

---

Markdown是一種標記式語言，減少標籤、格式指令以強調可讀性。

## 文字樣式

### 標題

#### Stext形式
分為6個層級，於行首插入`#`與空白。
```
# 標題1
## 標題2
...
###### 標題6
```

#### Atx形式
採用底線形式分為最高階`=`和第二階`-`。
```
標題1
===

標題2
---
```

---

### 分隔線

用3個以上的星號`*`、減號`-`、底線`_`來建立分隔線，行內不能有其他符號，可以插入空白。
```
***
---
_ _ _
```

---

### 文字字體

**粗體** `**粗體標示**` 、 `__粗體標示__`

*斜體* `*斜體標示*`

***粗斜體*** `***粗斜體***`

~~刪除線~~ `~~刪除線~~`

<u>底線</u> `<u>底線</u>`

---

### 引言

使用email形式的引言，於行首加上`>`，亦可使用階層、標題、清單關係語法。
```
> If I looked compared to others far, is because I stand on giant’s shoulder. — Newton
>> Imagination is more important than knowledge. — Albert Einstein
```

---

### 程式碼

#### 文字程式碼
輸入1個反引號`` ` ``涵蓋。
```
行內 `程式碼` 使用 `back-ticks` 將文字包起來。
```

#### 段落程式碼
採用3個反引號`` ` ``(英文半形)涵蓋，第一列後可以指定語言類型。
```c
‵‵‵c
# include <stdio.h>
int main()
{
    printf("Hello World!\n");
}
‵‵‵
```

---

### 公式

以`$`涵蓋表示行內公式，`$$`涵蓋表示獨立公式。
> 其餘語法參考:
> [MathJax basic tutorial and quick reference](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)
> [LaTeX/Mathematics](https://en.wikibooks.org/wiki/LaTeX/Mathematics)
> [如何在 Markdown 輸入數學公式及符號](https://blog.maxkit.com.tw/2020/02/markdown.html)
> [LATEX語法筆記](https://hackmd.io/@RintarouTW/%E6%84%9A%E5%8D%83%E6%85%AE%E3%81%AE%E7%AD%86%E8%A8%98%E6%9C%AC/%2F%40RintarouTW%2FLaTeX_%25E8%25AA%259E%25E6%25B3%2595%25E7%25AD%2586%25E8%25A8%2598#Function)

---

## 格式樣式

### 清單

支援有序清單和無序清單，可使用階層式。

#### 有序清單
使用文字接英文句點+空格。
```
1. Red
2. Green
3. Blue
```
> 若段落中以數字+`.`作為開頭，可改為數字+`\.`

#### 無序清單
使用星號`*`、加號`+`、減號`-`+空格。
```
* Red
+ Green
- Blue
```

---

### 待辦事項

[ ] 表示空框框，[x]顯示打勾。
```
- [ ] 尚未完成 
- [x] 完成
- [ ] 待辦
```

---

### 表格

第一列為標題列，第二列以`---`區隔，以`|`增加欄位，欄寬會自動分配不用對齊。
```
| Column 1 | Column 2 | Column 3 |
| -------- | -------- | -------- |
|  Text 1  |  Text 2  |  Text 3  |
```
第二列可決定對齊方式。
```
| Column 1 | Column 2 | Column 3 |
| :------- | :------: | -------: |
|靠左對齊   | 置中對齊 |   靠右對齊|
```

---

### 連結

```
[連結文字](連結網址)
```
```
<連結網址>
```

---

### 圖片

```
![圖片替代文字](圖片連結)
```

---

## 參考資料

[Markdown語法說明](https://markdown.tw/)