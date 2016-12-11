---
layout: post
title:  Markdown进阶
date:   2016-12-10 22:57:11
category: "Markdown"
comment: true

---

# 区块元素
### 段落与换行

一个 Markdown **段落** 是由一个或多个连续的文本行组成，它的前后要有一个以上的空行（空行的定义是显示上看起来像是空的，便会被视为空行。比方说，若某一行只包含空格和制表符，则该行也会被视为空行）。普通段落不该用空格或制表符来缩进。

「由一个或多个连续的文本行组成」这句话其实暗示了 Markdown 允许段落内的强迫换行（插入换行符），Markdown **换行** 需要在插入处先按入两个以上的空格然后回车。

### 区块引用

Markdown 标记区块引用是使用类似 email 中用 > 的引用方式。

```
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
> consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
> Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.
> 
> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
> id sem consectetuer libero luctus adipiscing.
```

> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
> consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
> Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.
>
> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
> id sem consectetuer libero luctus adipiscing.

Markdown 也允许你偷懒只在整个段落的第一行最前面加上 > ：

```
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
id sem consectetuer libero luctus adipiscing.
```

> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
id sem consectetuer libero luctus adipiscing.

区块引用可以嵌套，只要根据层次加上不同数量的 > ：

```
> This is the first level of quoting.
>
> > This is nested blockquote.
>
> Back to the first level.
```

> This is the first level of quoting.
> 
> > This is nested blockquote.
> 
> Back to the first level.

引用的区块内也可以使用其他的 Markdown 语法，包括标题、列表、代码区块等:

```
> #### 这是一个标题。
> 
> 1.   这是第一行列表项。
> 2.   这是第二行列表项。
> 
> 给出一些例子代码：
> 
>     printf("code");
```

> #### 这是一个标题。
> 
> 1.   这是第一行列表项。
> 2.   这是第二行列表项。
> 
> 给出一些例子代码：
> 
>     printf("code");

### 列表

**无序列表**使用星号、加号或是减号作为列表标记：

```
*   Red
*   Green
*   Blue
```
等同于：
```
+   Red
+   Green
+   Blue
```
等同于：
```
-   Red
-   Green
-   Blue
```
-   Red
-   Green
-   Blue

**有序列表**则使用数字接着一个英文句点：
```
1.  Bird
2.  McHale
3.  Parish
```
很重要的一点是，你在列表标记上使用的数字并不会影响输出的 HTML 结果:
```
<ol>
<li>Bird</li>
<li>McHale</li>
<li>Parish</li>
</ol>
```

如果你的列表标记写成：
```
1.  Bird
1.  McHale
1.  Parish
```
或甚至是：
```
3. Bird
1. McHale
8. Parish
```
你都会得到完全相同的 HTML 输出。  
建议第一个项目最好还是从 1. 开始，因为 Markdown 未来可能会支持有序列表的 start 属性。

列表项目标记通常是放在最左边，但是其实也可以缩进，最多 3 个空格，项目标记后面则一定要接着至少一个空格或制表符。

**思考:为什么不能是四个以上的空格？**

**列表项目可以包含多个段落，每个项目下的段落都必须缩进 4 个空格或是 1 个制表符：**
```
*   This is a list item with two paragraphs.

    This is the second paragraph in the list item. You're
    only required to indent the first line. Lorem ipsum dolor
    sit amet, consectetuer adipiscing elit.

*   Another item in the same list.
```
*   This is a list item with two paragraphs.

    This is the second paragraph in the list item. You're
    only required to indent the first line. Lorem ipsum dolor
    sit amet, consectetuer adipiscing elit.

*   Another item in the same list.

如果要在列表项目内放进引用，那 > 就需要缩进4个空格或一个制表符：
```
*   A list item with a blockquote:

    > This is a blockquote
    > inside a list item.
```
*   A list item with a blockquote:

    > This is a blockquote
    > inside a list item.
    
如果要放代码区块的话，该区块就需要缩进两次，也就是 8 个空格或是 2 个制表符：
```
*   A list item with a blockcode:

		#include <stdio.h>
		int main()
		{
		  printf("hello");
     	  return 0;
		}
```
*   A list item with a blockcode:

		#include<stdio.h>  
		int main()  
		{  
		  printf("hello");  
		  return 0;  
		}

**思考：为什么要缩进2次？**

### 代码区块

和程序相关的写作或是标签语言原始码通常会有已经排版好的代码区块，通常这些区块我们并不希望它以一般段落文件的方式去排版，而是照原来的样子显示，Markdown 会用 `<pre>` 和 `<code>` 标签来把代码区块包起来。

要在 Markdown 中建立代码区块很简单，只要简单地缩进 4 个空格或是 1 个制表符就可以,一个代码区块会一直持续到没有缩进的那一行（或是文件结尾）:
```
	#include<stdio.h>  
	int main()  
	{  
	  printf("hello");  
	  return 0;  
	}
```
	#include<stdio.h>  
	int main()  
	{  
	  printf("hello");  
	  return 0;  
	}

代码区块中，一般的 Markdown 语法不会被转换，像是星号便只是星号，这表示你可以很容易地以 Markdown 语法撰写 Markdown 语法相关的文件。

### 分割线

你可以在一行中用三个以上的星号、减号、底线来建立一个分隔线，行内不能有其他东西。你也可以在星号或是减号中间插入空格。下面每种写法都可以建立分隔线：
```
* * *

***

*****

- - -

---------------------------------------
``` 
* * *

***

*****

- - -

---------------------------------------

# 区段元素
### 链接
Markdown 支持两种形式的链接语法： **行内式**和**参考式**两种形式。

不管是哪一种，链接文字都是用 [方括号] 来标记。

要建立一个行内式的链接，只要在方块括号后面紧接着圆括号并插入网址链接即可，如果你还想要加上链接的 title 文字，只要在网址后面，用双引号把 title 文字包起来即可，例如：
```
This is [an example](https://www.baidu.com/ "Title") inline link.

[This link](https://www.baidu.com/) has no title attribute.
```
This is [an example](https://www.baidu.com/ "I am a title") inline link.

[This link](https://www.baidu.com/) has no title attribute.

如果你是要链接到同样主机的资源，你可以使用相对路径：
```
See my [About](/about.html) page for details.
```
See my [About](/about.html) page for details.

参考式的链接是在链接文字的括号后面再接上另一个方括号，而在第二个方括号里面要填入用以辨识链接的标记：

```
This is [an example][baidu] reference-style link.
```
接着，在文件的任意处，你可以把这个标记的链接内容定义出来：
```
[baidu]: https://www.baidu.com/  "Optional Title Here"
```
This is [an example][baidu] reference-style link. 
 
[baidu]: https://www.baidu.com/  "Optional Title Here"

链接辨别标签可以有字母、数字、空白和标点符号，但是并不区分大小写。

**隐式链接**标记功能让你可以省略指定链接标记，这种情形下，链接标记会视为等同于链接文字，要用隐式链接标记只要在链接文字后面加上一个空的方括号：
```
This is [an example][] reference-style link.

[an example]: https://www.baidu.com "Optional Title Here"
```
This is [an example][] reference-style link.  

[an example]: https://www.baidu.com "Optional Title Here"
### 图片
图片和链接用法类似，区别是在前面加一个 ！ ：
```
This is ![an example][] reference-style link.

[an example]: https://www.baidu.com "Optional Title Here"
```
This is  a ![dog][] image.

[dog]: http://www.lagou.com/upload/logo/ff80808145e62bd90145ee204ba26e6a.png "I am a dog!"

### 强调
Markdown 使用星号（*）和底线（_）作为标记强调字词的符号。

### 代码

如果要标记一小段行内代码，你可以用反引号把它包起来（`）：
```
Use the `printf()` function.
```
Use the `printf()` function.

如果要在代码区段内插入反引号，你可以用多个反引号来开启和结束代码区段：
```
``There is a literal backtick (`) here.``
```
``There is a literal backtick (`) here.``

代码区段的起始和结束端都可以放入一个空白，起始端后面一个，结束端前面一个，这样你就可以在区段的一开始就插入反引号：
```
A backtick-delimited string in a code span: `` `foo` ``
```
A backtick-delimited string in a code span: `` `foo` ``

到目前为止， Markdown 还没有办法指定图片的宽高，如果你需要的话，你可以使用普通的 <img> 标签。

# 其它
### 自动链接

Markdown 支持以比较简短的自动链接形式来处理网址和电子邮件信箱，只要是用方括号包起来， Markdown 就会自动把它转成链接。一般网址的链接文字就和链接地址一样，例如：

	<https://www.baidu.com>
<https://www.baidu.com>

### 反斜杠

Markdown 可以利用反斜杠来插入一些在语法中有其它意义的符号。

Markdown 支持以下这些符号前面加上反斜杠来帮助插入普通的符号：

	\   反斜线
	`   反引号
	*   星号
	_   底线
	{}  花括号
	[]  方括号
	()  括弧
	#   井字号
	+   加号
	-   减号
	.   英文句点
	!   惊叹号

# 结语

以上就是 Markdown 的的标准语法，当然现在有很多 Markdown 处理器使用的 superset-markdown ，比如：
-  表格标签
-  插入“Enter”段内换行
-  前后各用三个 ```language 高亮代码
-  ……

更多请参考：<https://kramdown.gettalong.org/syntax.html>