---
title: OPT学习笔记-10：锥规划应用与半正定松弛
description: 介绍逻辑回归的指数锥表示、鲁棒线性规划的对偶化以及 QCQP 的半正定松弛
slug: opt-notes-10
date: 2026-09-20 23:18:00+0800
math: true
categories:
    - Math
tags:
    - notes
    - OPT
weight: 10
---

锥规划的价值不仅在于统一理论，还在于把许多看似非线性的约束转化为可计算的凸模型。本篇讨论指数锥建模、鲁棒线性规划和半正定松弛。

## 指数锥与逻辑回归

指数锥定义为

$$
K_{\exp}=\operatorname{cl}
\{(x,y,z):y>0, y\exp(x/y)\le z\}.
$$

给定样本 $(a_i,y_i)$，其中 $a_i\in\mathbb{R}^p$、$y_i\in\{-1,1\}$，带 $\ell_2$ 正则的逻辑回归为

$$
\min_\theta
\sum_{i=1}^n\log\bigl(1+exp(-y_i a_i^\top\theta)\bigr)
+\lambda\|\theta\|_2.
$$

令 $u_i=-y_i a_i^\top\theta$，并用 $t_i$ 表示第 $i$ 项损失。关系

$$
t_i\ge\log(1+e^{u_i})
$$

等价于

$$
e^{-t_i}+e^{u_i-t_i}\le1.
$$

引入 $z_{i1},z_{i2}\ge0$，可用两个指数锥约束表示：

$$
(-t_i,1,z_{i1})\in K_{\exp},
\qquad
(u_i-t_i,1,z_{i2})\in K_{\exp},
\qquad
z_{i1}+z_{i2}\le1.
$$

再引入 $r\ge\|\theta\|_2$，原问题成为线性目标 $\sum_i t_i+\lambda r$ 下的指数锥与二阶锥规划。

## 鲁棒线性规划

若第 $i$ 个约束的系数 $a_i$ 不确定，只知道 $a_i\in U_i$，鲁棒约束要求

$$
a_i^\top x\ge b_i,qquad \forall a_i\in U_i.
$$

它等价于

$$
\min_{a_i\in U_i}a_i^\top x\ge b_i.
$$

因此，关键是对内层最小化问题求一个可处理的表示。

### 椭球不确定集

设

$$
U_i=\{\bar a_i+B_iv:\|v\|_2\le1\}.
$$

{{< math-block type="proposition" title="椭球鲁棒约束的 SOCP 表示" label="prop-ellipsoidal-robust" >}}
鲁棒约束 $a_i^\top x\ge b_i$ 对所有 $a_i\in U_i$ 成立，当且仅当

$$
\bar a_i^\top x-\|B_i^\top x\|_2\ge b_i.
$$
{{< /math-block >}}

{{< math-block type="proof" >}}
内层最小值为

$$
\bar a_i^\top x+min_{\|v\|_2\le1}v^\top B_i^\top x.
$$

由 Cauchy--Schwarz 不等式，后项不小于 $-\|B_i^\top x\|_2$。当 $B_i^\top x\ne0$ 时取

$$
v=-\frac{B_i^\top x}{\|B_i^\top x\|_2}
$$

即可达到下界；为零时结论也成立。因此内层最小值恰为 $\bar a_i^\top x-\|B_i^\top x\|_2$。
{{< /math-block >}}

### 多面体与锥不确定集

若

$$
U_i=\{a:D_ia\ge d_i\},
$$

则内层问题及其线性规划对偶为

$$
\min_a\{x^\top a:D_ia\ge d_i\}
=
\max_{\lambda_i\ge0}
\{d_i^\top\lambda_i:D_i^\top\lambda_i=x\}.
$$

在内层问题满足强对偶时，鲁棒约束等价于存在 $\lambda_i\ge0$ 使

$$
D_i^\top\lambda_i=x,
\qquad
d_i^\top\lambda_i\ge b_i.
$$

更一般地，若 $U_i=\{a:D_ia-d_i\in K_i\}$，则把 $\lambda_i\ge0$ 替换为 $\lambda_i\in K_i^*$，便得到相应的锥规划表示。这说明“对所有不确定参数成立”的无限约束，常能通过内层问题的对偶化变成有限个变量与约束。

## QCQP 的矩阵提升

考虑一般二次约束二次规划

$$
\begin{aligned}
\min_x\quad&x^\top Cx+2c^\top x+d\\
\text{s.t.}\quad&x^\top A_ix+2a_i^\top x+b_i\ge0,
\quad i=1,\ldots,m.
\end{aligned}
$$

令 $z=(1,x^\top)^\top$、$X=zz^\top$，并定义

$$
\widetilde C=
\begin{pmatrix}d&c^\top\\c&C\end{pmatrix},
\qquad
\widetilde A_i=
\begin{pmatrix}b_i&a_i^\top\\a_i&A_i\end{pmatrix}.
$$

则目标与约束分别为 $\langle\widetilde C,X\rangle$ 与 $\langle\widetilde A_i,X\rangle$。

{{< math-block type="lemma" title="秩一提升的刻画" label="lem-rank-one-lifting" >}}
对称矩阵 $X$ 可写为

$$
X=\begin{pmatrix}1\\x\end{pmatrix}
\begin{pmatrix}1\\x\end{pmatrix}^{\!\top}
$$

当且仅当 $X\succeq0$、$\operatorname{rank}(X)=1$ 且 $X_{00}=1$。
{{< /math-block >}}

{{< math-block type="proof" >}}
正向显然。反向若 $X\succeq0$ 且秩为 $1$，则存在向量 $z$ 使 $X=zz^\top$。由 $X_{00}=z_0^2=1$，可把 $z$ 的符号整体调整为 $z_0=1$，于是 $z=(1,x^\top)^\top$。
{{< /math-block >}}

因此原 QCQP 等价于

$$
\begin{aligned}
\min_X\quad&\langle\widetilde C,X\rangle\\
\text{s.t.}\quad&\langle\widetilde A_i,X\rangle\ge0,quad i=1,\ldots,m,\\
&X\succeq0,quad X_{00}=1,quad\operatorname{rank}(X)=1.
\end{aligned}
$$

唯一非凸部分是秩一约束。删去它便得到 SDP 松弛；对最小化问题，松弛最优值给出原问题最优值的下界。

## 最大稳定集的 SDP 松弛

图 $G=(V,E)$ 的稳定集是不含相邻节点的集合，最大稳定集大小记为 $\alpha(G)$。其整数模型为

$$
\begin{aligned}
\alpha(G)=\max_x\quad&\sum_{i\in V}x_i\\
\text{s.t.}\quad&x_i+x_j\le1,quad (i,j)\in E,\\
&x_i\in\{0,1\}.
\end{aligned}
$$

利用 $x_i^2=x_i$ 与边上 $x_ix_j=0$，得到 SDP 松弛

$$
\begin{aligned}
\operatorname{SDP}(G)=\max_{x,X}\quad&\sum_i x_i\\
\text{s.t.}\quad&X_{ij}=0,quad(i,j)\in E,\\
&X_{0i}=X_{i0}=X_{ii}=x_i,quad i\in V,\\
&X\succeq0,quad X_{00}=1.
\end{aligned}
$$

{{< math-block type="theorem" title="稳定集界的强弱关系" label="thm-stable-set-bounds" >}}
若 $\operatorname{LP}(G)$ 是上述整数模型的线性松弛，则

$$
\alpha(G)\le\operatorname{SDP}(G)\le\operatorname{LP}(G).
$$
{{< /math-block >}}

{{< math-block type="proof" >}}
对任意稳定集示性向量 $x$，令 $X=(1,x^\top)^\top(1,x^\top)$。它满足全部 SDP 约束，因此 $\alpha(G)\le\operatorname{SDP}(G)$。

反过来，任取 SDP 可行解。半正定矩阵的对角元非负，所以 $x_i=X_{ii}\ge0$。主子矩阵

$$
\begin{pmatrix}1&x_i\\x_i&x_i\end{pmatrix}\succeq0
$$

的行列式非负，给出 $x_i(1-x_i)\ge0$，故 $x_i\le1$。对每条边 $(i,j)$，相应主子矩阵为

$$
\begin{pmatrix}
1&x_i&x_j\\
x_i&x_i&0\\
x_j&0&x_j
\end{pmatrix}\succeq0.
$$

其行列式为 $x_ix_j(1-x_i-x_j)\ge0$。当 $x_ix_j>0$ 时得到 $x_i+x_j\le1$；有一项为零时该不等式也由另一项不超过 $1$ 得到。因此 $x$ 是 LP 松弛的可行解，目标值不超过 $\operatorname{LP}(G)$。
{{< /math-block >}}

SDP 松弛保留了变量之间的二阶相关结构，因而通常比逐变量的 LP 松弛更紧；代价是模型和求解过程也更复杂。
