---
title: "[Shell] Windows上的Linux - WSL(Windows Subsystem for Linux)"
date: 2020-11-29 19:11:27
categories: 
- Tool
tags: 
- Windows
- Linux
- Ubuntu
- Shell
- Terminal
--- 

習慣Linux指令後就回不去了，不想裝VM又不肯灌系統? 那就用WSL吧!

<!-- more -->

---

Windows Subsystem for Linux (WSL)
: 在Windows 10上與Linux相容的核心介面。

## 1. 安裝WSL

GUI :
設定-更新與安全性-開發人員專用-開發人員模式
設定-應用程式-程式和功能-
開啟或關閉Windows功能-適用於Linux的Windows(Windows子系統Linux版)

CMD :
```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

Microsoft Store安裝Ubuntu-啟動-enter username & password

> 預設安裝路徑為:
> `C:\Users\{windowsuser}\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\LocalState\rootfs\home\{linuxuser}\`

---

可以啟用多索引標籤的Terminal，又能自訂樣式(哭)

## 2. 安裝Windows Terminal

Microsoft Store安裝Windows Terminal

下拉選單開啟設定(setting.json)包含:

> `global setting`:設置默認Profile
> `profiles`:下拉選單可開啟的shell profile、環境裡terminal顯示
> `schemes`:配色主題
> `actions`:自定義快捷鍵

### 2.1 自定義terminal環境設定

> 背景存放路徑:
> `C:\Users\{username}\AppData\Local\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\RoamingState`

```
"useAcrylic": true, // Windows壓克力效果著色
"acrylicOpacity": 0.8, // 壓克力效果透明度
"colorScheme": "One Half Dark", // 配色主題
"backgroundImage": "ms-appdata:///roaming/ubuntu.jpg", // 背景圖
"backgroundImageStretchMode": "uniformToFill", // 伸縮模式:按比例放大
"backgroundImageOpacity": 0.3 // 圖片透明度
```

---

## 參考資料

[Windows Subsystem for Linux](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux)
[Windows終端機概觀](https://docs.microsoft.com/zh-tw/windows/terminal/)
[新生代 Windows 终端：Windows Terminal 的全面自定义](https://sspai.com/post/59380)

