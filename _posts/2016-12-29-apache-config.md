---
layout: post
title: Apache搭建HTTP服务器
date: 2016-12-29 11:49:43 
category: "Web"
comment: true
---

最近项目中遇到需要自己搭建一个HTTP服务器，从网上查阅资料后决定使用Apache。

### 下载

刚开始直接在网上下载了[2.4.25版本][1]，但一直配置不好。最后换了[httpd-2.2.22-win32-x86-no_ssl版本][2]，随便选的一个低版本。。。

[1]: http://httpd.apache.org/

[2]: http://archive.apache.org/dist/httpd/binaries/win32/

这是一个安装版本，按照提示安装就行。注意在选择“setup type”时选“custom”，这样可以自定义安装路径。

安装完成后，会在windows任务栏右下角自动开启apache monitor。

### 配置

找到Apache的安装目录，打开conf/httpd.conf:

- 第35行，ServerRoot 为Apache的安装路径，这个了解就可以，不用管它；
- 第46行，Listen 80   指定了 80 为Apache的默认监听端口。如果与其他软件冲突，也可以改成其它可用端口；
- 第172行，ServerName 为之前安装时设置的DNS域名（如果没有域名就输入IP，记得跟上端口号），#号为注释，这里去掉#号，修改后的内容如下：        
ServerName 127.0.0.1:80
- 第179行，DocumentRoot  一般为js、css、html、png、gif、jpg等静态资源文件的存放目录，默认就在htdocs文件夹下，可以不更改；
- 第219行，将 Options Indexes FollowSymLinks 注释掉，并在其下追加一行 Options None。作用是为了避免在浏览器中列出 服务端资源 的目录结构；
- 为了支持put请求，还需要做以下更改：
	- 取消下面两行代码的注释

		LoadModule dav_module modules/mod_dav.so      
		LoadModule dav_fs_module modules/mod_dav_fs.so

	- 添加下面两行代码     
	   ![iamge](/images/posts/apache_directory.jpg) 

**补充：Apache服务的卸载**

> 若Apache服务器软件不想用了，想要卸载，需要先卸载apache服务（切记，若直接删除安装路径的文件夹，会有残余文件在电脑，可能会造成不必要的麻烦)     
> 在CMD命令窗口，输入如下（建议先停止服务再删除）：      
sc delete apache
apache是Apache服务器的服务名



