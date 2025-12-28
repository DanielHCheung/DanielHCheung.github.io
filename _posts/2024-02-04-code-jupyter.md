---
layout: post
title:  "使用VS code打开Jupyter报错Error loading webview"
date:  2024-02-04 06:14:54
categories: python jupyter code
tags: python jupyter code
excerpt: 使用VS code打开Jupyter报错Error loading webview的解决方案。
mathjax: true
---

# Windows操作系统

首先第一步是关掉code，这一步可以把所有文件都保存，然后进一步杀掉code，使用命令```taskkill /im code.exe /f```。删掉之后打开```APPDATA```文件夹，为了方便可以在文件浏览器的地址栏中输入```%appdata%```敲回车。进入code文件夹，删掉以下文件夹

```Cache```, ```CachedData```, ```CachedExtensions```, ```CachedExtensionVSIXs``` (if this folder exists) and ```Code Cache```

![image](https://github.com/AmySang666/amysang666.github.io/assets/119597656/3dbd49c5-542c-4261-98e0-ff0a76f22497)

我已经删掉了（前面的忘了截图，可以翻看参考文献提供的截图）

# Ubuntu

使用Ubuntu操作系统，可以关闭code程序后```killall code```。鉴于笔者较长时间未使用Linux，这一条未必正确。建议翻看参考文献[1]。

# 参考文献

https://stackoverflow.com/questions/67698176/error-loading-webview-error-could-not-register-service-workers-typeerror-fai
