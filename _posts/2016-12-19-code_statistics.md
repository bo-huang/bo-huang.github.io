---
layout: post
title: Git统计代码行数
date: 2016-12-19 11:08:46 
category: "Git"
comment: true
---

之前统计项目代码总行数都是使用“打开每一个.cpp文件，然后拿着计算器做加法”这种蠢办法:cold_sweat:。最近突然想到git作为一个代码托管工具，是不是应该有这个功能呢？

---

---

百度一下发现，还真有统计代码行数的命令。

打开git，进入项目目录，然后输入以下命令，即可显示代码行数：

	find . "(" -name "*.cpp" -or -name "*.h" ")"  -print | xargs wc -l

![code statistics](/images/posts/code_statistics.jpg "code statistics.jpg")