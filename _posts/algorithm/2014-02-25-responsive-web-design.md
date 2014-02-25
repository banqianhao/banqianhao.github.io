wrong_dad
---
layout : post
category : 技术
title : 响应式设计备忘录
tags: [design, web, css, HTML5]
description: ""
---

#必要准备

为了不让浏览器自动缩放，必须加入下面一行

<meta name="viewport" content="width=device-width,initial-scale=1.0" />

#媒体查询

可以将下面的代码插入任意CSS文件的最后查看效果

body: {
    background-color: grey;
}
@media screen and (max-width: 960px) {
    body {
        background-color: red;
    }
}
@media screen ans (max-width: 768px) {
    body {
        background-color: orange;
    }
}
@media screen and (max-width: 550px) {
    body {
        background-color: yellow;
    }
}
@media screen and (max-width: 320px) {
    body {
        background-color: green;
    }
}


插入方式

<link rel="stylesheet" type="text/css" media="screen" href="style.css" />
<!--是屏幕才加载style.css文件-->
<link rel="stylesheet" type="text/css" media="screen and (orientation: portrait)" href="portrait-style.css" />
<!--纵向放置的设备会加载portrait-style.css文件-->
<link rel="stylesheet" type="text/css" media="screen and (orientation: portrait) ans (max-width: 800px)" href="800px-portrait-style.css" />
<!--进一步限制屏幕尺寸-->
<link rel="stylesheet" type="text/css" media="screen and (orientation: portrait) ans (max-width: 800px), projection" href="800px-portrait-style.css" />
<!--都好分隔几个查询，这里会应用到所有的投影仪-->

还可以使用import，下面的例子将为视口最大宽度为360像素的显示屏设备加载phone.css

@import url("phone.css") screen and (max-width: 360px);

但是这样会增加HTTP请求，影响加载速度。

记住使用全能的max-width属性，除了max-width还有min-width

#HTML全新语义

#<section>
文档中的区域或节
#<nav>
主导航区域
#<article>
一篇文章，一篇完整的内容
#<aside>
侧边栏
#<hgroup>
包裹一组h标签
#<header>
刊头
#<footer>
就是footer
#<address>
标注其与最近祖先的联系信息

#正文部分
<b>加粗
<em>强调内容重点
<i>斜体

