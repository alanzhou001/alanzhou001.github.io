---
title: OPT学习笔记-5：线性规划对偶
description: 从有效不等式和约束聚合推导线性规划对偶，并介绍弱对偶、强对偶和互补松弛
slug: opt-notes-5
date: 2026-09-20 23:13:00+0800
math: true
categories:
    - Math
tags:
    - notes
    - OPT
weight: 1
---

对偶理论把“求一个最小值”转化为“寻找尽可能大的下界”。在线性规划中，这些下界可以通过对原约束作非负加权得到。

## 从有效不等式出发

考虑原问题

$$
\begin{aligned}
p^*=\min_x\quad&c^\top x\\
\text{s.t.}\quad&Ax\ge b.
\end{aligned}
\tag{P}
$$

{{< math-block type="definition" title="有效不等式" label="def-valid-inequality" >}}
若对集合 $S$ 中所有 $x$ 都有

$$
\alpha^\top x\ge\beta,
$$

则称该不等式是 $S$ 的有效不等式。
{{< /math-block >}}

把 $Ax\ge b$ 的各行乘以非负权重 $\lambda_i$ 后相加，得到

$$
(A^\top\lambda)^\top x\ge b^\top\lambda,
\qquad\lambda\ge0.
$$

如果进一步要求 $A^\top\lambda=c$，则对每个原问题可行点都有

$$
c^\top x\ge b^\top\lambda.
$$

因此 $b^\top\lambda$ 是原问题最优值的下界。寻找这类下界中最大的一个，就得到对偶问题

$$
\begin{aligned}
d^*=\max_\lambda\quad&b^\top\lambda\\
\text{s.t.}\quad&A^\top\lambda=c,\\
&\lambda\ge0.
\end{aligned}
\tag{D}
$$

## 弱对偶

{{< math-block type="theorem" title="弱对偶定理" label="thm-weak-duality-lp" >}}
若 $x$ 是原问题可行解，$\lambda$ 是对偶问题可行解，则

$$
c^\top x\ge b^\top\lambda.
$$

因此 $p^*\ge d^*$。
{{< /math-block >}}

{{< math-block type="proof" >}}
由 $A^\top\lambda=c$、$Ax\ge b$ 和 $\lambda\ge0$，

$$
c^\top x
=(A^\top\lambda)^\top x
=\lambda^\top Ax
\ge\lambda^\top b
=b^\top\lambda.
$$
{{< /math-block >}}

弱对偶立即给出：

- 若原问题无界到 $-\infty$，对偶问题必不可行；
- 若对偶问题无界到 $+\infty$，原问题必不可行；
- 任一原可行解与对偶可行解的目标值之差

$$
c^\top x-b^\top\lambda\ge0
$$

称为**对偶间隙（duality gap）**。

## Farkas 引理

强对偶的关键是：如果目标下界在最优点处有效，那么它可以由紧约束的非负组合生成。

{{< math-block type="theorem" title="Farkas 引理的一种形式" label="thm-farkas" >}}
给定向量 $a_1,\ldots,a_m,c\in\mathbb{R}^n$，下列两者恰有一个成立：

1. 存在 $\lambda\ge0$ 使 $c=\sum_i\lambda_i a_i$；
2. 存在 $d\in\mathbb{R}^n$ 使 $a_i^\top d\ge0$ 对所有 $i$ 成立，但 $c^\top d<0$。
{{< /math-block >}}

{{< math-block type="proof" >}}
令

$$
K=\left\{\sum_i\lambda_i a_i:\lambda_i\ge0\right\}.
$$

$K$ 是闭凸锥。若 $c\notin K$，由点与闭凸集的分离定理，存在 $d$ 将 $c$ 与 $K$ 严格分离。因为 $K$ 是锥且包含 $0$，分离关系可以归一化为

$$
d^\top z\ge0,\quad\forall z\in K,
\qquad d^\top c<0.
$$

特别地 $a_i\in K$，所以 $a_i^\top d\ge0$。反之，若两种情况同时成立，则

$$
c^\top d=\sum_i\lambda_i a_i^\top d\ge0,
$$

与 $c^\top d<0$ 矛盾。
{{< /math-block >}}

## 强对偶

{{< math-block type="theorem" title="线性规划强对偶定理" label="thm-strong-duality-lp" >}}
若原问题 $(P)$ 存在最优解，则对偶问题 $(D)$ 也存在最优解，并且

$$
p^*=d^*.
$$
{{< /math-block >}}

{{< math-block type="proof" >}}
设 $x^*$ 是原问题最优解，令紧约束指标集为

$$
I=\{i:a_i^\top x^*=b_i\}.
$$

先证明 $c$ 属于紧约束法向量生成的锥。否则由 Farkas 引理，存在 $d$ 使

$$
a_i^\top d\ge0\quad(i\in I),
\qquad c^\top d<0.
$$

对 $i\notin I$，约束在 $x^*$ 处有严格余量，因此取足够小的 $\varepsilon>0$ 后，$x^*+\varepsilon d$ 仍满足所有约束；而

$$
c^\top(x^*+\varepsilon d)<c^\top x^*,
$$

与 $x^*$ 最优矛盾。

因此存在 $\lambda_i^*\ge0$（$i\in I$）使 $c=\sum_{i\in I}\lambda_i^*a_i$。对 $i\notin I$ 令 $\lambda_i^*=0$，则 $\lambda^*$ 对偶可行，且

$$
\begin{aligned}
b^\top\lambda^*
&=\sum_{i\in I}b_i\lambda_i^*\\
&=\sum_{i\in I}(a_i^\top x^*)\lambda_i^*\\
&=c^\top x^*=p^*.
\end{aligned}
$$

弱对偶又给出 $d^*\le p^*$，故 $d^*=p^*$，且 $\lambda^*$ 为对偶最优解。
{{< /math-block >}}

强对偶说明，只要找到原、对偶可行解并验证目标值相等，就同时获得两边的最优性证书。

## 互补松弛

{{< math-block type="theorem" title="互补松弛" label="thm-complementary-slackness" >}}
设 $x^*$ 和 $\lambda^*$ 分别是 $(P)$ 与 $(D)$ 的可行解。二者同时最优，当且仅当

$$
\lambda_i^*(a_i^\top x^*-b_i)=0,
\qquad i=1,\ldots,m.
$$
{{< /math-block >}}

{{< math-block type="proof" >}}
原、对偶目标值之差为

$$
\begin{aligned}
c^\top x^*-b^\top\lambda^*
&=(A^\top\lambda^*)^\top x^*-b^\top\lambda^*\\
&=\sum_i\lambda_i^*(a_i^\top x^*-b_i).
\end{aligned}
$$

每一项都非负，因此总和为零当且仅当每一项都为零。由强对偶，零对偶间隙又等价于两边同时最优。
{{< /math-block >}}

互补松弛的含义是：

- 若第 $i$ 个原约束有严格余量，则对应对偶变量必须为零；
- 若第 $i$ 个对偶变量严格为正，则对应原约束必须紧。

## 一般符号规则

对最小化原问题，约束方向决定对偶变量符号：

- 原约束 $a_i^\top x\ge b_i$ 对应 $\lambda_i\ge0$；
- 原约束 $a_i^\top x\le b_i$ 对应 $\lambda_i\le0$；
- 原约束 $a_i^\top x=b_i$ 对应自由对偶变量。

类似地，原变量的符号限制决定对偶约束是等式还是不等式。最稳妥的推导方式不是死记表格，而是重新执行“约束聚合并匹配目标系数”这一步。

## 总结

- 对偶变量是原约束的聚合权重；
- 弱对偶给出任何原、对偶可行解之间的目标值界；
- Farkas 引理保证最优有效不等式可以由紧约束生成；
- 强对偶在线性规划中消除了最优对偶间隙；
- 互补松弛将原约束余量与对偶变量联系起来，并提供最优性证书。

## 参考资料

1. Arkadi Nemirovski, *Lectures on Modern Convex Optimization*.
2. Taotao He, *ECON200 Optimization Methods, Lecture 7*.
