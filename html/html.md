Html
==========
全称：HyperText Markup Language  
中文：超文本标记语言  
> 两部分
- 超文本：

    是一种可以显示在计算机显示器或其他电子设备的文本，其中的文字包含有可以链接到其他字段或者文档的超链接，允许从当前阅读位置直接切换到超链接所指向的文字。超文本文档通过超链接相互链接，超链接通常通过鼠标点击、按键设置或触摸屏来点阅。

- 标记语言： 
    是一种将文本（Text）以及文本相关的其他信息结合起来，展现出关于文档结构和数据处理细节的计算机文字编码。（标签语言）

- 基本结构：
```
    <html><!-- html的根标签,代表html文档的结束和开始 -->
	<head><!-- html的头部分 , 设置网页属性,可以设置标题 -->
		<title>hello world</title><!-- 标题 -->
		<!-- 网页的属性: 改变页面的解析码表 -->
		<meta http-equiv="Content-Type" content="text/html;charset=utf-8" >
	</head>
	<body><!-- html的正文部分,放置想要在页面上显示的内容 -->
		hello world!
		<p>段落</p>
		换行<br>
		
		2<sup>3</sup><br/>上标
		2<sub>3</sub><br/>下标
		
		转义字符
		哈&nbsp;&nbsp;&nbsp;&nbsp;哈<br/>
a&lt;bc&gt;d<br/>
	</body>
    </html>
```
