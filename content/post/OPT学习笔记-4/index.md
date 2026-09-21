---
title: OPT学习笔记-4：线性规划的表示与几何
description: 介绍线性规划的一般型和标准型、极点、基本可行解、线性规划基本定理与单纯形法的几何基础
slug: opt-notes-4
date: 2026-09-20 23:12:00+0800
math: true
categories:
    - Math
tags:
    - notes
    - OPT
weight: 1
---

线性规划（linear programming, LP）在线性目标下优化一个多面体。本篇从等价表示出发，说明为什么 LP 的最优解可以在“顶点”中寻找。

## 一般型与标准型

一般形式可写为

$$
\begin{aligned}
\min_x\quad &c^\top x\\
\text{s.t.}\quad &Ax\le b,\\
&Dx=d.
\end{aligned}
$$

其可行域是有限个半空间与超平面的交，因此是多面体。

{{< math-block type="definition" title="线性规划标准型" label="def-lp-standard" >}}
标准型线性规划为

$$
\begin{aligned}
\min_x\quad &c^\top x\\
\text{s.t.}\quad &Ax=b,\\
&x\ge0.
\end{aligned}
$$
{{< /math-block >}}

一般型可以通过两步转成标准型：

1. 自由变量写成 $x_j=x_j^+-x_j^-$，其中 $x_j^+,x_j^-\ge0$；
2. 不等式 $a_i^\top x\le b_i$ 加入松弛变量 $s_i\ge0$，改写为 $a_i^\top x+s_i=b_i$。

这种变换保持最优值，并可在两个问题的最优解之间相互转换。

## 线性规划建模

### 分段线性函数

若

$$
f(x)=\max_{j\in J}(a_j^\top x+b_j),
$$

则最小化 $f$ 可以引入上境变量 $t$：

$$
\begin{aligned}
\min_{x,t}\quad&t\\
\text{s.t.}\quad&a_j^\top x+b_j\le t,\quad j\in J.
\end{aligned}
$$

若约束函数也是若干仿射函数的最大值，同样可拆成有限组线性不等式。

### 现金流匹配

设 $x_j$ 为第 $j$ 种债券的购买量，$p_j$ 为价格，$a_{tj}$ 为第 $t$ 年现金流，$L_t$ 为第 $t$ 年负债。若允许无息结转余额 $s_t$，可建立

$$
\begin{aligned}
\min_{x,s}\quad &\sum_jp_jx_j\\
\text{s.t.}\quad&s_{t-1}+\sum_ja_{tj}x_j-L_t=s_t,\\
&x\ge0,\quad s\ge0,
\end{aligned}
$$

其中 $s_0=0$。这说明许多跨期配置问题可以直接写成 LP。

## 极点与基本可行解

{{< math-block type="definition" title="极点" label="def-extreme-point" >}}
设 $C$ 为凸集。若 $x\in C$ 不能写成两个不同点 $y,z\in C$ 的非平凡凸组合

$$
x=\lambda y+(1-\lambda)z,
\qquad 0<\lambda<1,
$$

则称 $x$ 是 $C$ 的极点。
{{< /math-block >}}

考虑多面体

$$
P=\{x\in\mathbb{R}^n:a_i^\top x\le b_i,\ i=1,\ldots,m\}.
$$

若 $a_i^\top x=b_i$，称第 $i$ 个约束在 $x$ 处是**紧的（active/tight）**。

{{< math-block type="definition" title="基本可行解" label="def-bfs" >}}
若 $x\in P$，并且在 $x$ 处至少有 $n$ 个法向量线性无关的紧约束，则称 $x$ 为基本可行解（basic feasible solution, BFS）。
{{< /math-block >}}

{{< math-block type="theorem" title="极点与基本可行解等价" label="thm-extreme-bfs" >}}
对非空多面体 $P\subseteq\mathbb{R}^n$，点 $x\in P$ 是极点，当且仅当它是基本可行解。
{{< /math-block >}}

{{< math-block type="proof" >}}
先设 $x$ 是 BFS。取 $n$ 个线性无关的紧约束组成矩阵 $A_I$，则 $A_Ix=b_I$ 有唯一解。若

$$
x=\lambda y+(1-\lambda)z,
\quad y,z\in P,
\quad0<\lambda<1,
$$

则 $A_Iy\le b_I$、$A_Iz\le b_I$，而二者的凸组合等于 $b_I$，因此只能有 $A_Iy=A_Iz=b_I$。由唯一性，$y=z=x$，故 $x$ 是极点。

反之，若 $x$ 处紧约束的法向量不能张成 $\mathbb{R}^n$，则存在非零 $d$ 与所有紧约束法向量正交。对不紧约束，由于存在严格余量，可取充分小的 $\varepsilon>0$，使 $x\pm\varepsilon d$ 都仍可行。于是

$$
x=\frac12(x+\varepsilon d)+\frac12(x-\varepsilon d),
$$

且两端点不同，与 $x$ 为极点矛盾。因此紧约束中必有 $n$ 个线性无关的法向量，$x$ 是 BFS。
{{< /math-block >}}

因为每个 BFS 可由 $m$ 个约束中选取 $n$ 个并求解得到，多面体的极点数至多为 $\binom{m}{n}$，因而是有限的。

## 多面体中的直线

{{< math-block type="definition" title="多面体包含直线" label="def-polyhedron-line" >}}
若存在 $x\in P$ 和非零 $d$，使得

$$
x+td\in P,
\qquad\forall t\in\mathbb{R},
$$

则称多面体 $P$ 包含一条直线。
{{< /math-block >}}

{{< math-block type="theorem" title="极点存在性" label="thm-extreme-existence" >}}
非空多面体 $P$ 不包含直线，当且仅当 $P$ 至少有一个极点。
{{< /math-block >}}

{{< math-block type="proof" >}}
若 $P$ 包含直线，则对该直线上的任一点 $x+td$，都有

$$
x+td=\frac12(x+(t-1)d)+\frac12(x+(t+1)d),
$$

故直线上的点都不是极点；对 $P$ 中任意点也可沿该直线方向作同样分解，因此 $P$ 没有极点。

反之，从 $P$ 中任选一点，并在所有可行点中选择一个使线性无关紧约束数最大的点 $x$。若不足 $n$ 个，则存在非零方向 $d$ 与所有紧约束法向量正交。沿 $d$ 或 $-d$ 移动时，原紧约束保持等式。若两个方向都可无限移动，$P$ 就包含直线；否则至少一个方向会首次碰到新的约束，得到一个紧约束秩更高的可行点，与 $x$ 的选择矛盾。故 $x$ 是 BFS，也就是极点。
{{< /math-block >}}

标准型可行域 $\{x:Ax=b,x\ge0\}$ 不包含直线：若 $x+td\ge0$ 对所有实数 $t$ 成立，只能有 $d=0$。因此非空标准型可行域一定有极点。

## 线性规划基本定理

{{< math-block type="theorem" title="线性规划基本定理" label="thm-fundamental-lp" >}}
考虑

$$
\min_{x\in P}c^\top x.
$$

若 $P$ 至少有一个极点，并且问题存在最优解，则至少有一个最优解是 $P$ 的极点。
{{< /math-block >}}

{{< math-block type="proof" >}}
最优解集合

$$
F=\{x\in P:c^\top x=p^*\}
$$

是多面体 $P$ 的一个面。若最优点 $x$ 不是极点，则在保持目标值不变的最优面内沿某个可行方向移动，直到碰到新的线性无关紧约束。每次移动都会增加紧约束的秩；这个过程至多进行 $n$ 次，最终得到一个仍然最优的 BFS，也就是极点。
{{< /math-block >}}

该定理并不是说每个最优解都是极点：当目标等值超平面与多面体的一条边或一个面重合时，整条边或整个面都可能最优。但至少可以选择其中一个极点作为最优解。

## 单纯形法的几何思想

两个极点若共享 $n-1$ 个线性无关紧约束，称为相邻极点。单纯形法的基本过程是：

1. 从一个基本可行解开始；
2. 寻找目标值更优的相邻极点；
3. 沿边移动到该极点；
4. 当不存在改进方向时停止。

线性规划基本定理保证了在存在最优解时，可以在有限的极点集合中寻找答案；具体的换基规则则决定单纯形算法如何选择下一相邻点。

## 总结

- 一般 LP 可通过变量拆分和松弛变量转为标准型；
- 多面体的极点与基本可行解完全等价；
- 不含直线的非空多面体存在极点；
- 若 LP 有最优解且可行域有极点，则存在极点最优解；
- 单纯形法就是沿多面体边在相邻极点之间改进目标值。

## 参考资料

1. Dimitris Bertsimas and John Tsitsiklis, *Introduction to Linear Optimization*.
2. Taotao He, *ECON200 Optimization Methods, Lecture 6*.
