---
layout: post
title: 局域网内其他计算机访问本地站点
date: 2016-12-30 20:27:18 
category: "Web"
comment: true
---

昨天把本地http服务器配置好了，然后今天也成功将本地服务器接入项目。接下来就要考虑如何让外网访问本地服务器了，这个只需配置下路由器的端口转发就行，但在这之前需要先搞定如何让局域网内其他计算机能够访问本地服务器。

刚开始以为本地通过http://127.0.0.1:1027能够访问服务器，那么局域网内其他计算机应该也可以访问。于是在另一台电脑上输入我的局域网IP地址http://192.168.1.110:1027，结果访问不了。

查阅资料后发现，原来127.0.0.1是本地回送地址，指本主机，而192.168.1.110指本主机在局域网中的IP地址。也即在浏览器中输入http://127.0.0.1:1027是不经过路由器转发的，而http://192.168.1.110:1027要通过路由器转发，这样也就解释了http://127.0.0.1:1027可以访问而http://192.168.1.110:1027不能访问的合理性（这个概念好像在上大学的时候还知道:dizzy_face:）。

现在再来解释为什么http://192.168.1.110:1027不能访问。

当部署一个本地局域网站点或服务（如：端口为1027）时，默认防火墙是不允许其他应用访问本地站点的，这时需要对防火墙进行修改，新增1027端口的访问权限。

### 修改防火墙设置

1. 打开防火墙：控制面板->windows防火墙
2. 选择"高级设置"

	![windows_firewall_1](/images/posts/20161230/windows_firewall_1.jpg "windows firewall")

3. 规则类型：入站规则->新建规则

	![windows_firewall_2](/images/posts/20161230/windows_firewall_2.jpg "windows firewall")

4. 选择“端口”

	![windows_firewall_3](/images/posts/20161230/windows_firewall_3.jpg "windows firewall")

5. 选择“TCP”，填写"特定本地端口"，如1027

	![windows_firewall_4](/images/posts/20161230/windows_firewall_4.jpg "windows firewall")

6. 操作：允许连接
7. 配置文件：域、专用、公用
8. 填写名称描述

最后通过http://192.168.1.110:1027可以访问到本地服务器了:

![result](/images/posts/20161230/windows_firewall_result.jpg "windows firewall")

