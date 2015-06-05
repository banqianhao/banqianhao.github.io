---
layout: post
category: algorithm
title: 全局最小割算法
tags: [graph, algorithm, math]
---

####问题描述

给出一个无向图$G=(V, E)$，要求删除一些边，使得整个图不联通，同时删去的边尽量少。

###算法一
如果我们可以求出任意一个$s-t$最小割$C$，那么$G$的全局最小割是$C$与$$G-\{ s, t \}$$的全局最小割中较小的一个。

在图$G$中求任意一个$s-t$最小割的方法如下。

设$a$是$V$中任意一个顶点，点集$A$是$V$的一个子集，初始时等于$$\{a\}$$。我们每次在$V-A$中选取一个$w(A, x)$最大的点$x$加入$A$中，直到$A=V$时停止。这里，对于一个不属于$A$的点$x$，有

$$
w\{A, x\} = \sum_{y\in A}w(x, y)
$$

令$x$为倒数第二个加入$A$中的点，$t$为最后一个加入$A$中的点，$t$和其它所有点的连边组成的集合就是一个$s-t$最小割。

如果使用Fibonacci堆存储$V-A$中的点，时间复杂度为$O(mn+n^2\log n)$。

###算法二

这是个概率算法，同样运用点的合并。算法包括$n-2$此迭代。每次迭代中，算法从图的现有边中随机选出一条边并将边的两个顶点合并。每一次迭代会使顶点减少一个，经过$n-2$次迭代之后，图只剩下两个顶点。算法输出连接这两个顶点保留的边的集合。

设$E_i$表示第$i$次迭代时不在最小割集$C$中这一事件，$F_i = \bigcap\_{j=1}^{i} E_j$表示前$i$次迭代中没有缩减$C$中的边。我们需要计算$P(F_{n-2})$。

令$k=\| C \|$，则图中至少有$\frac{nk}{2}$条边。所以

$$
P(E_1) = P(F_1)\ge 1-\frac{2k}{nk}=1-\frac{2}{n}
$$

$$
P(E_2|F_1)\ge 1-\frac{k}{k(n-1)/2}=1-\frac{2}{n-1}
$$

类似地

$$
P(E_i|F_{i-1})\ge 1-\frac{k}{k(n-i+1)/2}=1-\frac{2}{n-i+1}
$$

所以

$$
\begin{align*}
  P(F_{n-2}) =&  P(E_{n-2}\cap F_{n-3})=P(E_{n-2} | F_{n-3})\cdot P(F_{n-3}) \\
  =& P(E_{n-2}|F_{n-3})\cdot P(E_{n-3}|E_{n-4})\cdots P(E_2|F_1)\cdot P(F_1)  \\
  \ge&\prod_{i=1}^{n-2} \left(1-\frac{2}{n-i+1}\right) = \prod_{i=1}^{n-2}\left(\frac{n-i-1}{n-i+1}\right) \\
  =& \left( \frac{n-2}{n} \right)\left( \frac{n-3}{n-1} \right)\left( \frac{n-4}{n-2} \right)\cdots \left( \frac{2}{4} \right)\left( \frac{1}{3} \right)\\
  =&\frac{2}{n(n-1)}.
\end{align*}
$$

假设进行$n(n-1)\ln n$次此随机算法，并输出所有结果的最小者，输出不是一个最小割集的概率是

$$
\left(1-\frac{2}{n(n-1)}\right)^{n(n-1)\ln n}\le e^{-2\ln n}=\frac{1}{n^2}.
$$

这里我们用到了$1-x\le e^{-x}$.




