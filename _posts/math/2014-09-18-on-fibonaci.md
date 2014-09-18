---
layout: post
title: 求解斐波那契数列
category: 探险指南
tags: [fibonaci, math, recursion]
---

Leonardo [fibonaci] 提出一个问题:

> 在一年之初把性别相反的一对新生兔子放进围栏。从第二个月开始，母兔每月生出一对性别相反的小兔。每对新生兔子也从他们第二个月大开始每月生出一对新兔。求n个月后围栏内兔子的对数。

我们令$f_n$表示第n个月时兔子的对数。先考虑n较小的情况，列出$n=0,n=1...n=14$的情况。

$$
0,1,1,2,3,5,8,13,21,34,55,89,144,233,\cdots
$$

下面我们尝试推导$f\_n$的通项公式。在第n个月时，围栏内的兔子可以分为两部分：第n-1个月开始时已经有的兔子和第n-1个月期间出生的兔子。容易得出

$$
f\_n=f\_{n-1}+f\_{n-2}\quad (n\ge 2)\\\\
f\_0=0,\quad f\_1=1
$$

考虑形式
$$
f\_n-f\_{n-1}-f\_{n-2}=0
$$
解决这个递推关系的一种方法是寻找形式为
$$
f\_n=q^n
$$
的一个解，其中q为一个非零数。将其带入递推式得
$$
q^n-q^{n-1}-q^{n-2}=0
$$
解得
$$
q\_1=\frac{1+\sqrt{5}}{2}\quad q\_2=\frac{1-\sqrt{5}}{2}
$$

两者都是递推关系的解。由于递推关系时线性的和齐次的，通过直接计算得到
$$
f\_n=c\_1\left(\frac{1+\sqrt{5}}{2}\right)^n+c\_2\left(\frac{1-\sqrt{5}}{2}\right)^2
$$
将初始值$f\_0=0,f\_1=1$代入求解得
$$
f_n=\frac{1}{\sqrt{5}}\left(\frac{1+\sqrt{5}}{2}\right)^n-\frac{1}{\sqrt{5}}\left(\frac{1-\sqrt{5}}{2}\right)^n\quad(n\ge 0)
$$

<div style="background-color:#D1D7D7; margin-left:4em; margin-right:2em; padding:2em; border:4px #000000 solid">
令
$$
h_0,h_1,h_2,\cdots ,h_n,\cdots
$$
是一个数列。如果存在量$a_1,a_2,\cdots ,a_k, a_k\ne 0$和量$b_n$，使得
$$
h_n=a_1h_{n-1}+a_2h_{n-2}+\cdots +a_kh_{n-k}+b_n\quad (n\ge 0)
$$
则称该序列满足k阶线性递推关系。
</div>
例如斐波那契数列满足2阶线性递推关系。

解这类递推公式可以借助特征方程和特征根。

具体方法可以查看[这篇文章](/DL/ho1.pdf) 或者阅读组合数学相关书籍。

jekyll 弄公式真是乱七八糟，我都有用latex写博客的冲动了。

