---
title: OPT学习笔记-3：凸优化与凸性判别
description: 介绍凸优化的局部到全局性质、一阶与二阶凸性判别、凸包以及保持凸性的常见运算
slug: opt-notes-3
date: 2026-09-20 23:11:00+0800
math: true
categories:
    - Math
tags:
    - notes
    - OPT
weight: 1
---

凸性最重要的意义，是把局部信息提升为全局结论。本篇讨论凸优化的基本性质、凸包以及判断函数凸性的常用方法。

## 从局部最优到全局最优

{{< math-block type="theorem" title="凸优化中的局部最优即全局最优" label="thm-local-global" >}}
考虑

$$
\min_{x\in X}f(x).
$$

若 $X$ 是凸集、$f$ 在 $X$ 上是凸函数，则任意局部极小值点都是全局极小值点；最优解集合也是凸集。
{{< /math-block >}}

{{< math-block type="proof" >}}
设 $x^*$ 是局部极小值点。若它不是全局极小值点，则存在 $y\in X$ 使 $f(y)<f(x^*)$。由 $X$ 的凸性，对任意 $t\in(0,1)$，

$$
x_t=(1-t)x^*+ty\in X.
$$

当 $t$ 足够小时，$x_t$ 位于 $x^*$ 的局部邻域内；但由凸性，

$$
f(x_t)\le(1-t)f(x^*)+tf(y)<f(x^*),
$$

与局部最优性矛盾。

再设 $x_1,x_2$ 均为全局最优解，最优值为 $p^*$。对任意 $t\in[0,1]$，

$$
f((1-t)x_1+tx_2)
\le(1-t)p^*+tp^*=p^*.
$$

由于 $p^*$ 已是最小值，只能取等号，故最优解集合凸。
{{< /math-block >}}

## 一阶凸性判别

{{< math-block type="theorem" title="全局线性下估计" label="thm-first-order-convexity" >}}
设 $f$ 在开凸集 $C$ 上可微。则 $f$ 在 $C$ 上凸，当且仅当对所有 $x,y\in C$，

$$
f(y)\ge f(x)+\nabla f(x)^\top(y-x).
$$
{{< /math-block >}}

这说明凸函数在任一点的切平面都是函数的全局下界。

{{< math-block type="proof" >}}
若 $f$ 凸，固定 $x,y$ 并令 $g(t)=f(x+t(y-x))$。对 $t\in(0,1]$，凸性给出

$$
g(t)\le(1-t)g(0)+tg(1),
$$

即

$$
\frac{g(t)-g(0)}{t}\le g(1)-g(0).
$$

令 $t\downarrow0$，得到 $\nabla f(x)^\top(y-x)\le f(y)-f(x)$。

反之，假设一阶不等式成立。令 $z=(1-t)x+ty$。分别在 $z$ 处对 $x$ 和 $y$ 应用该不等式：

$$
\begin{aligned}
f(x)&\ge f(z)+\nabla f(z)^\top(x-z),\\
f(y)&\ge f(z)+\nabla f(z)^\top(y-z).
\end{aligned}
$$

第一式乘以 $1-t$，第二式乘以 $t$ 后相加。由于

$$
(1-t)(x-z)+t(y-z)=0,
$$

得到 $(1-t)f(x)+tf(y)\ge f(z)$，故 $f$ 凸。
{{< /math-block >}}

{{< math-block type="theorem" title="凸函数的驻点判别" label="thm-convex-stationary" >}}
若 $f$ 可微且凸，则

$$
\nabla f(x^*)=0
$$

当且仅当 $x^*$ 是全局极小值点。
{{< /math-block >}}

{{< math-block type="proof" >}}
必要性来自无约束优化的一阶必要条件。若 $\nabla f(x^*)=0$，则对任意 $y$，由全局线性下估计，

$$
f(y)\ge f(x^*)+\nabla f(x^*)^\top(y-x^*)=f(x^*),
$$

故 $x^*$ 全局最优。
{{< /math-block >}}

## 凸包

{{< math-block type="definition" title="凸包" label="def-convex-hull" >}}
集合 $S\subseteq\mathbb{R}^n$ 的凸包定义为所有有限凸组合组成的集合：

$$
\operatorname{conv}(S)
=\left\{\sum_{i=1}^m\lambda_i x_i:
x_i\in S,\ \lambda_i\ge0,\ \sum_{i=1}^m\lambda_i=1\right\}.
$$
{{< /math-block >}}

{{< math-block type="theorem" title="凸包的最小性" label="thm-smallest-convex" >}}
$\operatorname{conv}(S)$ 是包含 $S$ 的最小凸集。
{{< /math-block >}}

{{< math-block type="proof" >}}
单点本身是凸组合，所以 $S\subseteq\operatorname{conv}(S)$。两个有限凸组合的凸组合仍可合并成一个有限凸组合，故 $\operatorname{conv}(S)$ 凸。

若凸集 $C$ 包含 $S$，则由凸性，$S$ 中任意有限个点的凸组合也属于 $C$，所以 $\operatorname{conv}(S)\subseteq C$。
{{< /math-block >}}

{{< math-block type="theorem" title="线性优化在凸包上保持最优值" label="thm-linear-convex-hull" >}}
对任意 $a\in\mathbb{R}^n$，

$$
\inf_{x\in S}a^\top x
=\inf_{x\in\operatorname{conv}(S)}a^\top x.
$$
{{< /math-block >}}

{{< math-block type="proof" >}}
因为 $S\subseteq\operatorname{conv}(S)$，右侧不大于左侧。反过来，任取

$$
x=\sum_i\lambda_i x_i\in\operatorname{conv}(S),
$$

则

$$
a^\top x=\sum_i\lambda_i a^\top x_i
\ge\inf_{z\in S}a^\top z.
$$

对凸包中所有 $x$ 取下确界即可得到反向不等式。
{{< /math-block >}}

理论上，任意优化问题都可先做上境图变换，再对可行上境图取凸包，从而变成线性目标下的凸问题。但凸包通常难以显式描述，因此这并不意味着一般非凸问题都容易求解。

## 凸优化问题的标准形式

{{< math-block type="definition" title="凸优化问题" label="def-convex-program" >}}
标准凸优化问题写作

$$
\begin{aligned}
\min_x\quad &f_0(x)\\
\text{s.t.}\quad &f_i(x)\le0,\quad i=1,\ldots,m,\\
&h_j(x)=0,\quad j=1,\ldots,p,
\end{aligned}
$$

其中 $f_0,f_1,\ldots,f_m$ 为凸函数，$h_1,\ldots,h_p$ 为仿射函数。
{{< /math-block >}}

每个不等式约束定义一个凸下水平集，每个等式约束定义一个仿射集，因此可行域是凸集。反过来，一个问题即使可行域碰巧是凸的，也不一定以可识别、可计算的凸形式给出。

## 保持凸性的运算

下列规则可用来快速构造凸函数。

### 非负加权和

若 $f_i$ 凸且 $\alpha_i\ge0$，则

$$
f(x)=\sum_i\alpha_i f_i(x)
$$

凸。证明直接对每个 $f_i$ 使用凸性不等式并加权求和。

### 仿射复合

若 $f$ 凸，则 $g(x)=f(Ax+b)$ 凸，因为仿射映射保持凸组合：

$$
A((1-t)x+ty)+b=(1-t)(Ax+b)+t(Ay+b).
$$

### 逐点上确界

若每个 $f_\alpha$ 都凸，则

$$
f(x)=\sup_\alpha f_\alpha(x)
$$

凸。其上境图满足

$$
\operatorname{epi}(f)=\bigcap_\alpha\operatorname{epi}(f_\alpha),
$$

而凸集的任意交仍凸。

### 单调凸复合

若 $h:\mathbb{R}^k\to\mathbb{R}$ 凸且对每个分量单调不减，$g_i$ 均凸，则

$$
f(x)=h(g_1(x),\ldots,g_k(x))
$$

凸。先由各 $g_i$ 的凸性得到逐分量上界，再依次使用 $h$ 的单调性和凸性即可证明。

## 二阶凸性判别

{{< math-block type="theorem" title="Hessian 判别" label="thm-hessian-convexity" >}}
设 $f$ 在开凸集 $C$ 上二阶连续可微，则

$$
f\text{ 在 }C\text{ 上凸}
\quad\Longleftrightarrow\quad
\nabla^2f(x)\succeq0,\quad\forall x\in C.
$$
{{< /math-block >}}

{{< math-block type="proof" >}}
若 $f$ 凸，固定 $x\in C$ 和任意方向 $d$，令 $g(t)=f(x+td)$。$g$ 是一元凸函数，因此

$$
g''(0)=d^\top\nabla^2f(x)d\ge0.
$$

故 Hessian 半正定。

反之，假设 Hessian 处处半正定。固定 $x,y\in C$，令 $d=y-x$、$g(t)=f(x+td)$。则

$$
g''(t)=d^\top\nabla^2f(x+td)d\ge0,
$$

所以 $g$ 在 $[0,1]$ 上凸，从而

$$
f((1-t)x+ty)=g(t)\le(1-t)g(0)+tg(1).
$$

故 $f$ 凸。
{{< /math-block >}}

由此立即得到：

- 二次函数 $f(x)=x^\top Qx+a^\top x+b$ 在 $Q$ 对称时凸，当且仅当 $Q\succeq0$；
- 椭球 $\{x:x^\top Qx\le r\}$（$Q\succ0$）是凸集；
- 最小二乘目标 $\lVert Ax-b\rVert_2^2$ 的 Hessian 为 $2A^\top A\succeq0$，所以任意驻点都是全局最优解。

## 总结

- 凸问题中局部极小值就是全局极小值；
- 可微凸函数等价于其切平面处处为全局下估计；
- 对可微凸函数，驻点与全局极小值点等价；
- 凸包不会改变线性目标的最优值，但未必容易描述；
- 非负加权和、仿射复合、逐点上确界和单调凸复合保持凸性；
- 二阶连续可微函数可用 Hessian 的半正定性判别凸性。

## 参考资料

1. Stephen Boyd and Lieven Vandenberghe, *Convex Optimization*, Cambridge University Press, 2004.
2. Taotao He, *ECON200 Optimization Methods, Lecture 5*.
