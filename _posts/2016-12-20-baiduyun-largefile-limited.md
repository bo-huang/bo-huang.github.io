---
layout: post
title: 让百度网盘支持大文件上传
date: 2016-12-20 21:32:28 
category: "软件"
comment: true
---

今天想上传一个系统镜像文件到百度网盘，却发现百度网盘有单文件4GB的大小限制，必须开通会员才能上传。无奈之下，只能想办法自己写一个上传文件到百度网盘的小工具了。

![largefile_upload_limited](/images/posts/largefile_upload_limited.jpg "largefile_upload_limited")

结果得知百度PCS不再支持新用户接入,这样就无法申请使用API！！！    
百度开发者中心改版公告:<http://developer.baidu.com/forum/topic/show?topicId=135>

![pcs_close](/images/posts/bpcs_close.jpg "bpcs_close")

于是，只好借了一个别人之前申请的开发者账号。

使用REST API上传文件出错：

> {"error_code":31208, "error_msg":"content_type is not exists"}

这是我发送的POST请求：

```

POST https://pcs.baidu.com/rest/2.0/pcs/file?method=upload&path=%2Fapps%2FUniDrive%2F2.txt&access_token=23.26f1432cfea025daacf30d58b71f326d.2592000.1484916550.363287424-1469786 HTTP/1.1  
Host: pcs.baidu.com  
Content-Length: 9  

file=1234

```

在官方文档上也找不到这个错误的原因，向百度PCS技术支持人员发邮件询问也没人理（感觉百度快放弃PCS API的维护了，从今年8月份宣布不再支持新用户接入就可以看出）。

这个时候奇迹发生了，抱着试一试的态度，我将POST改成PUT，结果竟然上传成功了:smile:   
但有个小问题，官方文档说file参数通过body上传，于是很自热的想到body里面应该是 “file = 数据”，但最终上传到网盘中的数据却成了"file = 1234"，于是就把"file="去掉了。

**前面的学习到此结束了，那么如何让百度网盘支持超过4GB的大文件上传呢？**

查阅百度PCS的REST API文档后知道，它提供了两种上传文件的方式，一种是普通上传方式（上面提到的），但这种方式要求上传文件不能超过2GB; 另一种就是分片上传方式，每一分片不能超过2GB。

很显然，这里要使用的就是分片上传方式。    

分片上传首先需要在本地将文件分片，然后上传每一片文件到百度网盘，此时上传的是临时文件，在百度网盘里无法查看（临时文件最后会有百度网盘自动回收，所以不用担心如何删除这些临时文件）。 上传完所有的分片后，再使用另外一个API，将所有上传的临时文件合并。

有关分片上传REST API的详细信息，请看[官方文档][]。

[官方文档]: <http://developer.baidu.com/wiki/index.php?title=docs/pcs/rest/file_data_apis_list#.E5.88.86.E7.89.87.E4.B8.8A.E4.BC.A0.E2.80.94.E6.96.87.E4.BB.B6.E5.88.86.E7.89.87.E5.8F.8A.E4.B8.8A.E4.BC.A0>

---

经过两天的努力终于写好了，项目地址:<https://github.com/bo-huang/bpcs>         
项目程序中都有详细的注释，此处就不再累赘实现过程了。         

**软件主界面：**

![bpcs_ui](/images/posts/bpcs_ui.jpg "bpcs")

[Release版下载地址](https://github.com/bo-huang/bpcs_release)

**说明：分片上传不支持秒传，所以对于小于4G的文件建议用百度网盘客户端上传。**
