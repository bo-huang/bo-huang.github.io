---
layout: post
title: Git语法复习
date: 2016-12-23 11:28:25 
category: "Git"
comment: true
---

最近慢慢发现Git里面的命令还是丰富的，有时候不会的百度一下，但过一段时间就又忘了。  于是想在这里慢慢总结，也方便以后查看。

**提交本地代码到Github基本命令：**

	git init                 //第一次提交要初始化git      
	git add .                //添加当前路径下的所有文件       
	git commit -m "注释"     //上传修改到本地仓库          
	git push origin master   //将本地仓库上传到github远程仓库

第一次提交时，需要初始化用户名和邮箱：

	git config user.name "用户名"       
	git config user.email "邮箱"

origin 是远程仓库别名：
	
	git remote add origin https://github.com/用户名/仓库名.git    //添加origin         
	git remote rm origin    //移除origin

如果提示没有权限访问远程仓库，可能是没有登录：
	
	git remote add origin https://用户名:密码@github.com/用户名/仓库名.git    //添加远程仓库时带上用户名密码

如果远程仓库中的版本和本地仓库不一致，提交前还要先把远程仓库pull下来

	git pull origin master

合并时会提示: Please enter a commit message to explain why this is necessay      
可以按如下步骤输入解释:

	1. 按键盘字母i进入insert模式
	2. 修改最上面那行黄色合并信息,可以不修改
	3. 按键盘左上角"Esc"
	4. 输入":wq"，按回车键即可

查看当前目录中的文件和本地仓库的差别(即还未提交的本地修改)：

	git status



