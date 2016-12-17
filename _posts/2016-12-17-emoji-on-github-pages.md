---
layout: post
title: Jekyll中使用emoji
date: 2016-12-17 14:23:38  
category: "Jekyll"
comment: true
---

因为平时写东西的时候习惯用一些表情，这样可以表达出很多文字表达不出来的心情（其实是博主语文水平有限，写不出来那么生动的句式）。但通过前面的学习，发现Markdown中并没有介绍如何添加表情，那是不是就不能在github pages中使用表情了呢？

在[这里][1]我找到了答案:

> You can use emoji within any Jekyll page or post, just like you would in a comment or issue within a repository on GitHub.

[1]: https://help.github.com/articles/emoji-on-github-pages/ "emoji-on-github-pages"

原来Jekyll是支持emoji表情的，不过首先需要在_config.yml中添加：

> gems: ['jemoji']

#### 如何在文章中添加表情？

在需要插入表情的地方输入 `:EMOJICODE:`, EMOJICODE指某一个表情对应的代码。

例如：

- `:+1:` :+1:
- `:laughing:` :laughing:
- `:relaxed:` :relaxed:
- `:stuck_out_tongue_winking_eye:` :stuck_out_tongue_winking_eye:
- and so on...

##### 那么我们又怎么知道每一个表情分别对应的emojicode呢?  

[这里][2]给出了详细的emoji和code的对照表。

[2]: http://www.webpagefx.com/tools/emoji-cheat-sheet/ "emoji-cheat-sheet"

接下来就可以在你的文章中尽情使用表情啦:stuck_out_tongue_winking_eye:
