---
title: OPT学习笔记-1：无约束优化与最优性条件
description: 介绍最优解的存在性、无约束优化的一阶与二阶最优性条件，并以最小二乘问题为例说明这些条件的应用
slug: opt-notes-1
date: 2026-09-20 23:00:00+0800
math: true
categories:
    - Math
tags:
    - notes
    - OPT
weight: 1
---

本篇承接 [OPT学习笔记-0](/p/opt-notes-0/)。在已经了解优化问题、全局最优解和局部最优解等基本概念后，我们进一步讨论三个问题：最优解何时存在，如何利用局部微分信息判断一个点是否为局部极小值，以及这些条件如何应用于最小二乘问题。

## 最优解的存在性

考虑优化问题

$$
\begin{aligned}
\min_{x}\quad & f(x)\\
\text{s.t.}\quad & x\in X,
\end{aligned}
$$

其中 $f:\mathbb{R}^n\to\mathbb{R}$ 是目标函数，$X\subseteq\mathbb{R}^n$ 是可行域。

一个优化问题可能因为以下三种原因没有最优解：

1. **不可行（infeasible）**：$X=\varnothing$；
2. **无界（unbounded）**：存在可行序列 $\{x^k\}\subseteq X$，使得 $f(x^k)\to-\infty$；
3. **下确界无法取得（not attained）**：$\inf_{x\in X}f(x)$ 有限，但不存在 $x^*\in X$ 使 $f(x^*)=\inf_{x\in X}f(x)$。

例如，在 $x>0$ 上：

- $\min 1/x$ 的下确界为 $0$，但任何可行点都不能取得它；
- $\min(-\log x)$ 无界，因为 $x\to+\infty$ 时 $-\log x\to-\infty$；
- $\min x\log x$ 在 $x=e^{-1}$ 处取得唯一最优值 $-e^{-1}$。

{{< math-block type="theorem" title="Weierstrass 极值定理" label="thm-weierstrass" >}}
设 $X\subseteq\mathbb{R}^n$ 非空且紧，函数 $f:X\to\mathbb{R}$ 连续，则存在 $x^*\in X$，使得

$$
f(x^*)=\min_{x\in X}f(x).
$$
{{< /math-block >}}

{{< math-block type="proof" >}}
记

$$
f^*=\inf_{x\in X}f(x).
$$

先证明 $f^*>-\infty$。若 $f^*=-\infty$，则存在序列 $\{x^k\}\subseteq X$ 使 $f(x^k)\to-\infty$。由于 $X$ 紧，$\{x^k\}$ 存在收敛子列 $x^{k_j}\to\bar{x}\in X$。由 $f$ 的连续性，

$$
f(x^{k_j})\to f(\bar{x})\in\mathbb{R},
$$

这与 $f(x^{k_j})\to-\infty$ 矛盾，因此 $f^*$ 有限。

根据下确界的定义，对每个正整数 $k$，存在 $x^k\in X$ 使得

$$
f^*\le f(x^k)<f^*+\frac{1}{k}.
$$

仍由紧性，存在子列 $x^{k_j}\to x^*\in X$。连续性给出

$$
f(x^*)=\lim_{j\to\infty}f(x^{k_j})=f^*.
$$

故 $x^*$ 是全局最优解。
{{< /math-block >}}

紧性与连续性都是重要条件。若可行域不闭，例如 $X=(0,1)$、$f(x)=x$，则下确界 $0$ 无法取得；若可行域不有界，例如 $X=\mathbb{R}$、$f(x)=e^{-x}$，也可能出现相同问题。

### 最大化与最小化

最大化问题总能改写为最小化问题：

$$
\max_{x\in X}f(x)=-\min_{x\in X}\bigl(-f(x)\bigr).
$$

因此，只要对目标函数取负号，最小化问题的结论就可以直接用于最大化问题。

### 经济学中的一个应用

若消费者偏好可以由连续效用函数 $u:X\to\mathbb{R}$ 表示，且预算集 $X$ 非空且紧，则由 Weierstrass 极值定理，存在 $x^*\in X$ 使得

$$
u(x^*)=\max_{x\in X}u(x).
$$

也就是说，在这些条件下消费者的最优选择集合非空。

## 无约束优化

无约束优化问题写作

$$
\min_{x\in\mathbb{R}^n}f(x).
$$

由于可行域是整个 $\mathbb{R}^n$，任意方向的小幅移动都是可行的，因此可以利用梯度和 Hessian 矩阵刻画局部最优性。

{{< math-block type="definition" title="局部极小值与严格局部极小值" label="def-local-minimum" >}}
若存在 $\delta>0$，使得对所有满足 $\lVert x-\bar{x}\rVert_2<\delta$ 的 $x$ 都有

$$
f(\bar{x})\le f(x),
$$

则称 $\bar{x}$ 为 $f$ 的一个**局部极小值点**。

若进一步对所有 $x\ne\bar{x}$ 都有

$$
f(\bar{x})<f(x),
$$

则称 $\bar{x}$ 为**严格局部极小值点**。
{{< /math-block >}}

### 必要条件与充分条件

- **必要条件**：如果 $\bar{x}$ 是局部极小值点，那么该条件必须成立；但满足条件的点未必是局部极小值点。
- **充分条件**：如果某点满足该条件，那么它一定是局部极小值点；但局部极小值点未必都满足该条件。

局部且可验证的条件十分重要：一方面，它们可以缩小最优解候选点的范围；另一方面，它们也是设计算法终止准则和搜索方向的基础。

## 一阶必要条件

{{< math-block type="theorem" title="一阶必要条件（FONC）" label="thm-fonc" >}}
设 $f:\mathbb{R}^n\to\mathbb{R}$ 在 $\bar{x}$ 处可微。若 $\bar{x}$ 是 $f$ 的局部极小值点，则

$$
\nabla f(\bar{x})=0.
$$
{{< /math-block >}}

{{< math-block type="proof" >}}
任取方向 $d\in\mathbb{R}^n$，定义一元函数

$$
g(t)=f(\bar{x}+td).
$$

由于 $\bar{x}$ 是 $f$ 的局部极小值点，$t=0$ 是 $g$ 的局部极小值点，故

$$
g'(0)=0.
$$

由链式法则，

$$
g'(0)=\nabla f(\bar{x})^\top d.
$$

因此对任意 $d\in\mathbb{R}^n$ 都有 $\nabla f(\bar{x})^\top d=0$。特别地，取 $d=\nabla f(\bar{x})$，得到

$$
\lVert\nabla f(\bar{x})\rVert_2^2=0,
$$

从而 $\nabla f(\bar{x})=0$。
{{< /math-block >}}

满足 $\nabla f(\bar{x})=0$ 的点称为**驻点（stationary point）**。驻点可能是局部极小值点、局部极大值点或鞍点。例如，$f(x)=x^3$ 在 $x=0$ 处满足 $f'(0)=0$，但 $0$ 不是局部极小值点，因此一阶条件并不充分。

## 二阶必要条件

{{< math-block type="definition" title="正定与半正定矩阵" label="def-psd" >}}
设 $Q\in\mathbb{R}^{n\times n}$ 为对称矩阵：

- 若对任意 $d\in\mathbb{R}^n$ 都有 $d^\top Qd\ge0$，则称 $Q$ **半正定**，记作 $Q\succeq0$；
- 若对任意非零 $d\in\mathbb{R}^n$ 都有 $d^\top Qd>0$，则称 $Q$ **正定**，记作 $Q\succ0$。
{{< /math-block >}}

{{< math-block type="theorem" title="二阶必要条件（SONC）" label="thm-sonc" >}}
设 $f:\mathbb{R}^n\to\mathbb{R}$ 在 $\bar{x}$ 的邻域内二阶连续可微。若 $\bar{x}$ 是 $f$ 的局部极小值点，则

$$
\nabla f(\bar{x})=0,
\qquad
\nabla^2 f(\bar{x})\succeq0.
$$
{{< /math-block >}}

{{< math-block type="proof" >}}
一阶必要条件已经给出 $\nabla f(\bar{x})=0$。

任取 $d\in\mathbb{R}^n$，令 $g(t)=f(\bar{x}+td)$。由于 $t=0$ 是 $g$ 的局部极小值点，一元函数的二阶必要条件给出 $g''(0)\ge0$。由链式法则，

$$
g''(0)=d^\top\nabla^2f(\bar{x})d.
$$

因此对任意 $d$ 都有

$$
d^\top\nabla^2f(\bar{x})d\ge0,
$$

即 $\nabla^2f(\bar{x})\succeq0$。
{{< /math-block >}}

二阶必要条件仍然不充分。例如 $f(x)=x^3$ 在 $x=0$ 处满足

$$
f'(0)=0,
\qquad
f''(0)=0,
$$

但 $0$ 不是局部极小值点。

## 二阶充分条件

在给出二阶充分条件前，需要先说明正定性与特征值之间的关系。

{{< math-block type="theorem" title="对称矩阵的特征值判别" label="thm-eigenvalue-test" >}}
设 $Q\in\mathbb{R}^{n\times n}$ 为实对称矩阵，则：

1. $Q\succeq0$ 当且仅当 $Q$ 的所有特征值均非负；
2. $Q\succ0$ 当且仅当 $Q$ 的所有特征值均为正。

若 $Q\succ0$，并记其最小特征值为 $\lambda_{\min}>0$，则对任意 $d\in\mathbb{R}^n$，

$$
d^\top Qd\ge\lambda_{\min}\lVert d\rVert_2^2.
$$
{{< /math-block >}}

{{< math-block type="proof" >}}
由实对称矩阵的谱定理，存在正交矩阵 $U$ 和实对角矩阵

$$
\Lambda=\operatorname{diag}(\lambda_1,\ldots,\lambda_n)
$$

使得 $Q=U\Lambda U^\top$。对任意 $d$，令 $z=U^\top d$，则

$$
d^\top Qd
=d^\top U\Lambda U^\top d
=z^\top\Lambda z
=\sum_{i=1}^n\lambda_i z_i^2.
$$

若所有 $\lambda_i\ge0$，则上式对任意 $d$ 非负，故 $Q\succeq0$。反之，若某个 $\lambda_j<0$，取对应的单位特征向量 $u_j$，则

$$
u_j^\top Qu_j=\lambda_j<0,
$$

与 $Q\succeq0$ 矛盾。正定情形同理。

当 $Q\succ0$ 时，

$$
d^\top Qd
=\sum_{i=1}^n\lambda_i z_i^2
\ge\lambda_{\min}\sum_{i=1}^n z_i^2
=\lambda_{\min}\lVert d\rVert_2^2,
$$

其中最后一个等号利用了正交变换保持欧氏范数。
{{< /math-block >}}

{{< math-block type="theorem" title="二阶充分条件（SOSC）" label="thm-sosc" >}}
设 $f:\mathbb{R}^n\to\mathbb{R}$ 在 $\bar{x}$ 的邻域内二阶连续可微。若

$$
\nabla f(\bar{x})=0,
\qquad
\nabla^2f(\bar{x})\succ0,
$$

则 $\bar{x}$ 是 $f$ 的严格局部极小值点。
{{< /math-block >}}

{{< math-block type="proof" >}}
记 $H=\nabla^2f(\bar{x})$，并设 $H$ 的最小特征值为 $\lambda_{\min}>0$。对充分小的 $h$，Taylor 展开给出

$$
f(\bar{x}+h)-f(\bar{x})
=\nabla f(\bar{x})^\top h
+\frac12h^\top Hh
+o(\lVert h\rVert_2^2).
$$

由于 $\nabla f(\bar{x})=0$ 且 $H\succ0$，有

$$
f(\bar{x}+h)-f(\bar{x})
\ge\frac12\lambda_{\min}\lVert h\rVert_2^2
+o(\lVert h\rVert_2^2).
$$

根据小 $o$ 项的定义，存在 $\delta>0$，使得当 $0<\lVert h\rVert_2<\delta$ 时，

$$
\left|o(\lVert h\rVert_2^2)\right|
\le\frac14\lambda_{\min}\lVert h\rVert_2^2.
$$

因此

$$
f(\bar{x}+h)-f(\bar{x})
\ge\frac14\lambda_{\min}\lVert h\rVert_2^2>0.
$$

故 $\bar{x}$ 是严格局部极小值点。
{{< /math-block >}}

二阶充分条件不是必要条件。例如 $f(x)=x^4$ 在 $x=0$ 处有严格局部极小值，但

$$
f'(0)=0,
\qquad
f''(0)=0,
$$

Hessian 并不正定。

## 最小二乘问题

给定矩阵 $A\in\mathbb{R}^{m\times n}$ 和向量 $b\in\mathbb{R}^m$，最小二乘问题为

$$
\min_{x\in\mathbb{R}^n}F(x)
=\min_{x\in\mathbb{R}^n}\lVert Ax-b\rVert_2^2.
$$

它常见于数据拟合和线性预测。展开目标函数可得

$$
F(x)=x^\top A^\top Ax-2b^\top Ax+b^\top b,
$$

因此

$$
\nabla F(x)=2A^\top(Ax-b),
\qquad
\nabla^2F(x)=2A^\top A\succeq0.
$$

一阶必要条件给出正规方程

$$
A^\top A\bar{x}=A^\top b.
$$

{{< math-block type="theorem" title="满列秩最小二乘解" label="thm-least-squares" >}}
若 $A$ 的列向量线性无关，则 $A^\top A\succ0$，最小二乘问题存在唯一全局最优解

$$
x^*=(A^\top A)^{-1}A^\top b.
$$
{{< /math-block >}}

{{< math-block type="proof" >}}
对任意非零向量 $d$，由 $A$ 满列秩可知 $Ad\ne0$，因此

$$
d^\top A^\top Ad=\lVert Ad\rVert_2^2>0.
$$

故 $A^\top A\succ0$，从而可逆，正规方程有唯一解

$$
x^*=(A^\top A)^{-1}A^\top b.
$$

令残差 $r=b-Ax^*$。由正规方程，$A^\top r=0$，所以 $r$ 与 $A$ 的列空间正交。对任意 $x$，

$$
Ax-b=A(x-x^*)-r.
$$

利用正交性，

$$
\begin{aligned}
\lVert Ax-b\rVert_2^2
&=\lVert A(x-x^*)-r\rVert_2^2\\
&=\lVert A(x-x^*)\rVert_2^2+\lVert r\rVert_2^2\\
&\ge\lVert r\rVert_2^2
=\lVert Ax^*-b\rVert_2^2.
\end{aligned}
$$

因此 $x^*$ 是全局最优解。又因为 $A$ 满列秩，仅当 $x=x^*$ 时 $A(x-x^*)=0$，故最优解唯一。
{{< /math-block >}}

## 一个二元函数的例子

考虑

$$
f(x_1,x_2)
=\frac12x_1^2+x_1x_2+2x_2^2-4x_1-4x_2-x_2^3.
$$

梯度为

$$
\nabla f(x_1,x_2)
=\begin{pmatrix}
x_1+x_2-4\\
x_1+4x_2-4-3x_2^2
\end{pmatrix}.
$$

令梯度为零。由第一行得 $x_1=4-x_2$，代入第二行：

$$
3x_2-3x_2^2=3x_2(1-x_2)=0.
$$

因此驻点为 $(4,0)$ 和 $(3,1)$。Hessian 矩阵为

$$
\nabla^2f(x_1,x_2)
=\begin{pmatrix}
1&1\\
1&4-6x_2
\end{pmatrix}.
$$

在 $(4,0)$ 处，

$$
\nabla^2f(4,0)
=\begin{pmatrix}1&1\\1&4\end{pmatrix}\succ0,
$$

所以 $(4,0)$ 是严格局部极小值点。在 $(3,1)$ 处，Hessian 的行列式为 $-3<0$，故 Hessian 不定，$(3,1)$ 是鞍点。因此，$f$ 只有一个局部极小值点 $(4,0)$。

## 三类最优性条件之间的关系

记：

- $X_{\mathrm{FONC}}$：满足一阶必要条件的点集；
- $X_{\mathrm{SONC}}$：满足二阶必要条件的点集；
- $X_{\mathrm{LO}}$：局部极小值点集；
- $X_{\mathrm{SOSC}}$：满足二阶充分条件的点集。

则有

$$
X_{\mathrm{FONC}}
\supset
X_{\mathrm{SONC}}
\supset
X_{\mathrm{LO}}
\supset
X_{\mathrm{SOSC}}.
$$

这些包含关系一般都是严格的：

1. $f(x)=-x^2$ 在 $0$ 处满足 FONC，但不满足 SONC；
2. $f(x)=x^3$ 在 $0$ 处满足 SONC，但不是局部极小值点；
3. $f(x)=x^4$ 在 $0$ 处是严格局部极小值点，但不满足 SOSC。

需要注意，这些条件只利用某一点附近的微分信息。对一般非凸函数而言，它们不能单独保证全局最优；后续讨论凸函数时会看到，在凸性条件下，局部信息可以转化为全局结论。

## 总结

- 连续函数在非空紧集上一定能取得全局最优值；
- 无约束可微函数的局部极小值点必须满足 $\nabla f(\bar{x})=0$；
- 二阶可微时，局部极小值点还必须满足 $\nabla^2f(\bar{x})\succeq0$；
- 若驻点处 Hessian 正定，则该点是严格局部极小值点；
- 满列秩最小二乘问题具有唯一全局最优解 $(A^\top A)^{-1}A^\top b$。

## 参考资料

1. Stephen Boyd and Lieven Vandenberghe, *Convex Optimization*, Cambridge University Press, 2004.
2. Taotao He, *ECON200 Optimization Methods, Lecture 3*.
