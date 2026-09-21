---
title: OPT学习笔记-12：金融优化中的凸模型与整数模型
description: 讨论协方差矩阵估计、最坏风险、分散化与换手约束，并介绍投资组合整数模型和分支定界法
slug: opt-notes-12
date: 2026-09-20 23:20:00+0800
math: true
categories:
    - Math
tags:
    - notes
    - OPT
weight: 12
---

投资组合问题把本系列中的多种模型连接起来：均值--方差模型是凸二次规划，协方差估计与风险界定可写成 SDP，分散化与换手约束可线性化，而持仓数量和多空状态则需要整数变量。

## 均值--方差模型

设随机收益向量为 $r\in\mathbb{R}^n$，其期望和协方差分别为

$$
\mu=\mathbb E[r],
\qquad
V=\mathbb E[(r-\mu)(r-\mu)^\top].
$$

投资权重为 $x$ 时，期望收益是 $\mu^\top x$，方差是 $x^\top Vx$。禁止卖空的基本模型为

$$
\begin{aligned}
\min_x\quad&x^\top Vx\\
\text{s.t.}\quad&\mu^\top x\ge\bar\mu,\\
&\mathbf1^\top x=1,\quad x\ge0.
\end{aligned}
$$

{{< math-block type="lemma" title="协方差矩阵的刻画" label="lem-covariance-psd" >}}
矩阵 $V$ 是某个随机向量的协方差矩阵，当且仅当 $V$ 对称半正定。
{{< /math-block >}}

{{< math-block type="proof" >}}
若 $V$ 是随机向量 $r$ 的协方差矩阵，则对任意 $z$，

$$
z^\top Vz
=\mathbb E\bigl[(z^\top(r-\mu))^2\bigr]\ge0,
$$

且定义直接给出 $V=V^\top$。

反之，若 $V\succeq0$，可取矩阵平方根 $V^{1/2}$。令 $Z$ 为均值为零、协方差为单位矩阵的随机向量，并令 $r=V^{1/2}Z$，则

$$
\operatorname{Cov}(r)
=V^{1/2}I(V^{1/2})^\top=V.
$$
{{< /math-block >}}

这个结论保证了风险目标是凸函数。

## 最近协方差矩阵

样本噪声或不完整估计可能产生一个并非半正定的矩阵 $\widehat V$。可寻找与它最接近的合法协方差矩阵：

$$
\min_{X\succeq0}\|X-\widehat V\|_F.
$$

引入上界变量 $t$，模型可写为

$$
\begin{aligned}
\min_{X,t}\quad&t\\
\text{s.t.}\quad&X\succeq0,\\
&\|\operatorname{vec}(X-\widehat V)\|_2\le t.
\end{aligned}
$$

它同时使用半正定锥与二阶锥，是一个凸锥规划。

## 不完整信息下的最坏风险

若投资组合 $\bar x$ 已知，但协方差矩阵只知道部分信息，可以在所有候选矩阵中最大化其风险：

$$
\begin{aligned}
\max_V\quad&\bar x^\top V\bar x
=\langle\bar x\bar x^\top,V\rangle\\
\text{s.t.}\quad&L_{ij}\le V_{ij}\le U_{ij},\\
&V\succeq0.
\end{aligned}
$$

目标关于 $V$ 是线性的，元素上下界也是线性的，所以这是 SDP。其他凸先验也可以直接加入，例如：

- 已知某些组合的方差：$\langle y_ky_k^\top,V\rangle=\sigma_k^2$；
- 因子模型：$V=FV_{\mathrm{factor}}F^\top+D$，其中 $V_{\mathrm{factor}}\succeq0$、$D$ 为非负对角矩阵；
- 已知边际方差与相关系数区间时，对 $V_{ij}$ 加线性上下界。

模型的最优值给出与全部已知信息相容的最坏情形风险上界。

## 分散化约束

令 $x_{(1)}\ge\cdots\ge x_{(n)}$ 为 $x$ 的降序排列，并定义前 $r$ 大分量之和

$$
F_r(x)=\sum_{i=1}^r x_{(i)}.
$$

“任意 $r$ 个资产的投资总额不超过 $\alpha$”可写为 $F_r(x)\le\alpha$，但直接枚举子集会产生大量约束。

{{< math-block type="proposition" title="前 r 大分量之和的 LP 表示" label="prop-top-r-lp" >}}
对任意 $x\in\mathbb{R}^n$，

$$
F_r(x)=
\max_y\left\{x^\top y:
0\le y\le1,
\ \mathbf1^\top y=r\right\}.
$$
{{< /math-block >}}

{{< math-block type="proof" >}}
若一个可行解中存在 $x_i>x_j$、$y_i<1$ 且 $y_j>0$，则把

$$
\varepsilon=\min\{1-y_i,y_j\}
$$

的权重从 $j$ 移到 $i$，可行性不变，而目标增加 $\varepsilon(x_i-x_j)>0$。反复交换后，存在最优解在最大的 $r$ 个分量上取 $y_i=1$，其余取零，目标值恰为 $F_r(x)$。
{{< /math-block >}}

这个 LP 的对偶为

$$
F_r(x)=
\min_{t,u}
\left\{rt+\sum_{i=1}^nu_i:
t+u_i\ge x_i,
\ u_i\ge0\right\},
$$

其中 $t$ 为自由变量。因此 $F_r(x)\le\alpha$ 当且仅当存在 $t,u$ 使

$$
rt+\sum_i u_i\le\alpha,
\qquad
t+u_i\ge x_i,
\qquad
u_i\ge0.
$$

原本指数规模的分散化约束由此变成 $O(n)$ 个线性约束。

## 换手约束

设当前持仓为 $x^0$，总换手上限为 $\alpha$：

$$
\sum_{i=1}^n|x_i-x_i^0|\le\alpha.
$$

引入 $u_i\ge0$ 后，可精确线性化为

$$
u_i\ge x_i-x_i^0,
\qquad
u_i\ge x_i^0-x_i,
\qquad
\sum_i u_i\le\alpha.
$$

存在绝对值并不意味着必须使用整数变量；分段线性的凸绝对值可以直接用辅助变量建模。

## 分支定界法

考虑混合整数线性规划

$$
\begin{aligned}
\min_{x,y}\quad&c^\top x+d^\top y\\
\text{s.t.}\quad&Ax+Gy\ge b,\\
&x\in\mathbb Z_+^n,quad y\in\mathbb R_+^p.
\end{aligned}
$$

去掉 $x$ 的整数要求得到 LP 松弛。对最小化问题，松弛最优值是整数问题的下界；任一整数可行解的目标值则给出上界。

若 LP 解中 $x_j^0$ 为分数，分支成

$$
x_j\le\lfloor x_j^0\rfloor
\qquad\text{或}\qquad
x_j\ge\lceil x_j^0\rceil.
$$

每个整数解必属于其中一个分支。搜索树中的节点可在三种情况下剪枝：

1. 松弛不可行；
2. 松弛下界不优于当前最好整数解；
3. 松弛解已经整数，从而得到该节点的最优整数解。

{{< math-block type="proposition" title="分支定界的正确性" label="prop-branch-bound-correctness" >}}
若整数变量的可行取值有界，并且算法最终处理或剪去每个活跃节点，则返回的 incumbent 是全局最优整数解。
{{< /math-block >}}

{{< math-block type="proof" >}}
每次分支把当前节点中的全部整数可行解无遗漏地划分到两个子节点。不可行节点不含候选解；按界剪去的节点不可能包含优于 incumbent 的解；整数松弛解同时达到该节点的下界，因而已是节点内最优整数解。有限有界的整数取值使分支树有限。算法结束时，所有可能优于 incumbent 的整数解都已被检查或被有效界排除，所以 incumbent 全局最优。
{{< /math-block >}}

## 投资组合中的二元变量

若最多允许持有 $K$ 个资产，可引入 $z_i\in\{0,1\}$：

$$
0\le x_i\le u_i z_i,
\qquad
\sum_i z_i\le K.
$$

在多空组合中，写作

$$
x_i=x_i^+-x_i^-,
$$

并使用二元变量防止同一资产同时做多和做空：

$$
0\le x_i^+\le u_i^+z_i^+,
\qquad
0\le x_i^-\le u_i^-z_i^-,
\qquad
z_i^++z_i^-\le1.
$$

固定交易成本、最小持仓规模和整手交易等要求也可以用类似的联动约束表达。此时模型成为混合整数凸规划；连续松弛越紧，分支定界通常越容易在早期剪去节点。
