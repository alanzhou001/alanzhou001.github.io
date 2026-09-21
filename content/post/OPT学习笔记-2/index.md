---
title: OPT学习笔记-2：仿射集、凸集与凸函数
description: 介绍仿射组合、凸组合、分离超平面、凸函数及其上境图和下水平集刻画
slug: opt-notes-2
date: 2026-09-20 23:10:00+0800
math: true
categories:
    - Math
tags:
    - notes
    - OPT
weight: 1
---

本篇整理仿射几何与凸性中的基本对象。它们是后续凸优化、线性规划和对偶理论的共同语言。

## 三种组合

给定 $x_1,\ldots,x_m\in\mathbb{R}^n$，向量

$$
\sum_{i=1}^m\lambda_i x_i
$$

称为：

- **线性组合**：$\lambda_i\in\mathbb{R}$；
- **仿射组合**：$\sum_i\lambda_i=1$；
- **凸组合**：$\sum_i\lambda_i=1$ 且 $\lambda_i\ge0$。

限制条件逐步增强，因此凸组合一定是仿射组合，仿射组合一定是线性组合。

## 仿射集

{{< math-block type="definition" title="仿射集" label="def-affine-set" >}}
集合 $M\subseteq\mathbb{R}^n$ 称为仿射集，如果对任意 $x,y\in M$ 和 $\lambda\in\mathbb{R}$，都有

$$
(1-\lambda)x+\lambda y\in M.
$$
{{< /math-block >}}

仿射集包含任意两点之间的整条直线。线性子空间必须经过原点，而仿射集可以看作线性子空间的平移。

{{< math-block type="theorem" title="仿射集的平移表示" label="thm-affine-translation" >}}
每个非空仿射集 $M$ 都可唯一写成

$$
M=a+L:=\{a+v:v\in L\},
$$

其中 $a\in M$，$L$ 是线性子空间，并且

$$
L=M-M:=\{x-y:x,y\in M\}.
$$
{{< /math-block >}}

{{< math-block type="proof" >}}
固定 $a\in M$，令 $L=M-a$。显然 $0\in L$。若 $u=x-a$、$v=y-a\in L$，则由仿射性，

$$
a+u+v=-a+x+y=(1-(-1))\frac{x+y}{2}+(-1)a\in M,
$$

故 $u+v\in L$。对任意 $t\in\mathbb{R}$，

$$
a+tu=(1-t)a+tx\in M,
$$

故 $tu\in L$。因此 $L$ 是线性子空间，且 $M=a+L$。

又因为 $M=a+L$，任意 $x-y\in M-M$ 都属于 $L$；反过来任意 $v\in L$ 可写成 $(a+v)-a$，所以 $L=M-M$。这一表达只由 $M$ 决定，故 $L$ 唯一。
{{< /math-block >}}

仿射集的维数定义为与其平行的线性子空间 $L$ 的维数。$\mathbb{R}^n$ 中的 $(n-1)$ 维仿射集称为**超平面**。

{{< math-block type="theorem" title="超平面与线性方程" label="thm-hyperplane" >}}
若 $a\in\mathbb{R}^n\setminus\{0\}$、$b\in\mathbb{R}$，则

$$
H=\{x\in\mathbb{R}^n:a^\top x=b\}
$$

是一个超平面；反之，每个超平面都可写成这种形式。
{{< /math-block >}}

{{< math-block type="proof" >}}
若 $x_0\in H$，则

$$
H=x_0+\operatorname{Null}(a^\top).
$$

由于 $a\ne0$，$\operatorname{Null}(a^\top)$ 的维数为 $n-1$，故 $H$ 是超平面。

反之，任意超平面可写成 $x_0+L$，其中 $\dim L=n-1$。于是 $L^\perp$ 为一维空间，取非零 $a\in L^\perp$ 并令 $b=a^\top x_0$，即可得到 $H=\{x:a^\top x=b\}$。
{{< /math-block >}}

更一般地，线性方程组的解集

$$
M=\{x\in\mathbb{R}^n:Ax=b\}
$$

若非空，则对任意特解 $x_0$ 有 $M=x_0+\operatorname{Null}(A)$，因而是仿射集。

## 凸集

{{< math-block type="definition" title="凸集" label="def-convex-set" >}}
集合 $C\subseteq\mathbb{R}^n$ 称为凸集，如果对任意 $x,y\in C$ 和 $\lambda\in[0,1]$，都有

$$
(1-\lambda)x+\lambda y\in C.
$$
{{< /math-block >}}

几何上，这表示集合中任意两点之间的线段仍完全位于集合中。仿射集、半空间、欧氏球和椭球都是凸集。

{{< math-block type="theorem" title="凸集对任意交封闭" label="thm-convex-intersection" >}}
任意一族凸集的交集仍是凸集。
{{< /math-block >}}

{{< math-block type="proof" >}}
设 $C=\bigcap_{\alpha\in I}C_\alpha$，任取 $x,y\in C$。则对每个 $\alpha$ 都有 $x,y\in C_\alpha$。由 $C_\alpha$ 的凸性，对任意 $\lambda\in[0,1]$，

$$
(1-\lambda)x+\lambda y\in C_\alpha.
$$

因此该点属于所有 $C_\alpha$，也就属于 $C$。
{{< /math-block >}}

有限个闭半空间的交称为**多面体（polyhedron）**：

$$
P=\{x\in\mathbb{R}^n:Ax\le b\}.
$$

线性规划的可行域正是多面体。与交集不同，凸集的并集一般不凸。

## 分离超平面

{{< math-block type="theorem" title="点与闭凸集的分离定理" label="thm-separation" >}}
设 $C\subseteq\mathbb{R}^n$ 非空、闭且凸，$x_0\notin C$。则存在 $a\ne0$ 和 $b\in\mathbb{R}$，使得

$$
a^\top x\le b<a^\top x_0,
\qquad \forall x\in C.
$$
{{< /math-block >}}

{{< math-block type="proof" >}}
由于 $C$ 闭且 $x_0\notin C$，距离最小化问题

$$
\min_{x\in C}\lVert x-x_0\rVert_2
$$

存在最优解 $p\in C$。令 $a=x_0-p\ne0$。对任意 $x\in C$，由凸性知 $p+t(x-p)\in C$（$t\in[0,1]$）。函数

$$
\phi(t)=\lVert x_0-p-t(x-p)\rVert_2^2
$$

在 $t=0$ 处取得区间 $[0,1]$ 上的最小值，因此 $\phi'(0)\ge0$，即

$$
a^\top(x-p)\le0.
$$

所以 $a^\top x\le a^\top p$。取

$$
b=\frac{a^\top p+a^\top x_0}{2},
$$

由于 $a^\top x_0-a^\top p=\lVert x_0-p\rVert_2^2>0$，便有

$$
a^\top x\le a^\top p<b<a^\top x_0.
$$
{{< /math-block >}}

分离定理说明：每个闭凸集都可以表示为一族包含它的闭半空间的交。

## 凸函数

{{< math-block type="definition" title="凸函数与凹函数" label="def-convex-function" >}}
设 $\operatorname{dom}f$ 为凸集。若对任意 $x,y\in\operatorname{dom}f$ 和 $\lambda\in[0,1]$，

$$
f((1-\lambda)x+\lambda y)
\le(1-\lambda)f(x)+\lambda f(y),
$$

则称 $f$ 为凸函数。若不等号反向，则称 $f$ 为凹函数。
{{< /math-block >}}

$f$ 为凹函数当且仅当 $-f$ 为凸函数；同时凸且凹的函数恰为仿射函数。

常见凸函数包括 $e^{ax}$、$-\log x$、$x\log x$、范数以及支撑函数

$$
\sigma_C(z)=\sup_{x\in C}z^\top x.
$$

范数的凸性来自三角不等式；支撑函数的凸性则来自上确界运算：

$$
\sigma_C((1-\lambda)z_1+\lambda z_2)
\le(1-\lambda)\sigma_C(z_1)+\lambda\sigma_C(z_2).
$$

## 上境图与下水平集

{{< math-block type="definition" title="上境图" label="def-epigraph" >}}
函数 $f:S\to\mathbb{R}$ 的上境图定义为

$$
\operatorname{epi}(f)
=\{(x,t)\in\mathbb{R}^{n+1}:x\in S,\ t\ge f(x)\}.
$$
{{< /math-block >}}

{{< math-block type="theorem" title="上境图刻画" label="thm-epigraph" >}}
$f$ 是凸函数，当且仅当 $\operatorname{epi}(f)$ 是凸集。
{{< /math-block >}}

{{< math-block type="proof" >}}
若 $f$ 凸，任取 $(x,s),(y,t)\in\operatorname{epi}(f)$，则 $s\ge f(x)$、$t\ge f(y)$。对 $\lambda\in[0,1]$，

$$
f((1-\lambda)x+\lambda y)
\le(1-\lambda)f(x)+\lambda f(y)
\le(1-\lambda)s+\lambda t,
$$

故上境图凸。

反之，若上境图凸，则 $(x,f(x))$ 和 $(y,f(y))$ 的凸组合仍在上境图中，立即得到凸函数定义中的不等式。
{{< /math-block >}}

函数的 $\alpha$-下水平集为

$$
L_\alpha(f)=\{x\in\operatorname{dom}f:f(x)\le\alpha\}.
$$

{{< math-block type="theorem" title="凸函数的下水平集" label="thm-sublevel" >}}
若 $f$ 为凸函数，则每个下水平集 $L_\alpha(f)$ 都是凸集。
{{< /math-block >}}

{{< math-block type="proof" >}}
任取 $x,y\in L_\alpha(f)$，则 $f(x),f(y)\le\alpha$。于是

$$
f((1-\lambda)x+\lambda y)
\le(1-\lambda)f(x)+\lambda f(y)
\le\alpha,
$$

所以 $(1-\lambda)x+\lambda y\in L_\alpha(f)$。
{{< /math-block >}}

反命题不成立。所有下水平集均凸的函数称为**拟凸函数（quasiconvex function）**，拟凸性弱于凸性。

## 总结

- 仿射集是线性子空间的平移，凸集只要求包含两点之间的线段；
- 凸集对任意交封闭，多面体是有限个半空间的交；
- 分离定理把闭凸集与外部点用超平面分开；
- 凸函数等价于上境图为凸集，并且其下水平集一定凸。

## 参考资料

1. Stephen Boyd and Lieven Vandenberghe, *Convex Optimization*, Cambridge University Press, 2004.
2. Taotao He, *ECON200 Optimization Methods, Lecture 4*.
