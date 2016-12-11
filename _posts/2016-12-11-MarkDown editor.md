---
layout: post
title: Markdown 编辑工具
date: 2016-12-11 14:50:57  
category: "Markdown"
comment: true

---




Windows系统下，推荐大家用[MarkDownPad2][]，它支持多种markdown处理器。之前用**简书**，发现在简书上写的文章发布到github pages上后排版就变乱了。原因是github pages上的Markdown处理器是[kramdown][]，简书上使用的肯定也不是markdown standard（具体是什么处理器还没去研究），两者都是在markdown standard的基础上进行了语法扩展。所以在简书上写的文章不能直接应用到github pages上。

[MarkDownPad2]: http://markdownpad.com/  
[kramdown]: https://kramdown.gettalong.org/documentation.html

对于系统为Windows8及以上的电脑，需要先安装awesomium_v1.6.6_sdk_win这个平台，可以在我的百度网盘中去下载，里面还提供了MarkdownPad2的激活码.

- 链接：<http://pan.baidu.com/s/1eRO1rpw>
- 密码：ht2k

***Tips:***

- **如果你使用的不是kramdown，那么你必须在_config.yml中将其修改为markdown: kramdown**
- **可以在Tools->Options->Markdown中设置markdown processor**

我的 markdown processor 设置是：  
![processor](/images/posts/markdown_processor.bmp)  
*markdown rendering mode 选择 standard 是想尽量符合 markdown 标准语法的使用习惯。*






