wrong_dad
---
layout : post
category : ����
title : ��Ӧʽ��Ʊ���¼
tags: [design, web, css, HTML5]
description: ""
---

#��Ҫ׼��

Ϊ�˲���������Զ����ţ������������һ��

<meta name="viewport" content="width=device-width,initial-scale=1.0" />

#ý���ѯ

���Խ�����Ĵ����������CSS�ļ������鿴Ч��

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


���뷽ʽ

<link rel="stylesheet" type="text/css" media="screen" href="style.css" />
<!--����Ļ�ż���style.css�ļ�-->
<link rel="stylesheet" type="text/css" media="screen and (orientation: portrait)" href="portrait-style.css" />
<!--������õ��豸�����portrait-style.css�ļ�-->
<link rel="stylesheet" type="text/css" media="screen and (orientation: portrait) ans (max-width: 800px)" href="800px-portrait-style.css" />
<!--��һ��������Ļ�ߴ�-->
<link rel="stylesheet" type="text/css" media="screen and (orientation: portrait) ans (max-width: 800px), projection" href="800px-portrait-style.css" />
<!--���÷ָ�������ѯ�������Ӧ�õ����е�ͶӰ��-->

������ʹ��import����������ӽ�Ϊ�ӿ������Ϊ360���ص���ʾ���豸����phone.css

@import url("phone.css") screen and (max-width: 360px);

��������������HTTP����Ӱ������ٶȡ�

��סʹ��ȫ�ܵ�max-width���ԣ�����max-width����min-width

#HTMLȫ������

#<section>
�ĵ��е�������
#<nav>
����������
#<article>
һƪ���£�һƪ����������
#<aside>
�����
#<hgroup>
����һ��h��ǩ
#<header>
��ͷ
#<footer>
����footer
#<address>
��ע����������ȵ���ϵ��Ϣ

#���Ĳ���
<b>�Ӵ�
<em>ǿ�������ص�
<i>б��

