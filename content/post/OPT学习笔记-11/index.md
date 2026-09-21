---
title: OPT学习笔记-11：Lagrange 对偶与 KKT 条件
description: 从下界构造解释 Lagrange 对偶，并证明 Slater 条件下的强对偶及凸优化中的 KKT 最优性条件
slug: opt-notes-11
date: 2026-09-20 23:19:00+0800
math: true
categories:
    - Math
tags:
    - notes
    - OPT
weight: 11
---

锥对偶把约束写成锥中的向量不等式；Lagrange 对偶则直接从一般约束函数出发构造目标值下界。它不仅适用于凸问题，也能用于非凸问题，但强对偶与 KKT 条件需要额外假设。

## Lagrange 函数与对偶函数

考虑问题

$$
\begin{aligned}
p^*=\min_x\quad&f_0(x)\\
\text{s.t.}\quad&f_i(x)\le0,quad i=1,\ldots,m,\\
&h_j(x)=0,quad j=1,\ldots,p.
\end{aligned}
\tag{P}
$$

Lagrange 函数定义为

$$
L(x,\lambda,\mu)
=f_0(x)+\sum_{i=1}^m\lambda_i f_i(x)
+\sum_{j=1}^p\mu_j h_j(x),
$$

其中不等式约束乘子满足 $\lambda\ge0$，等式约束乘子 $\mu$ 可取任意实数。

若 $x$ 原可行，则

$$
L(x,\lambda,\mu)\le f_0(x).
$$

进一步对 $x$ 取下确界，得到对偶函数

$$
g(\lambda,\mu)=\inf_{x\in\mathbb{R}^n}L(x,\lambda,\mu).
$$

对偶问题寻找其中最大的下界：

$$
d^*=\max_{\lambda,\mu}
\{g(\lambda,\mu):\lambda\ge0\}.
\tag{D}
$$

{{< math-block type="theorem" title="Lagrange 弱对偶" label="thm-lagrange-weak-duality" >}}
无论原问题是否凸，都有

$$
d^*\le p^*.
$$

而且 $g$ 是关于 $(\lambda,\mu)$ 的凹函数，所以对偶问题是凸优化问题。
{{< /math-block >}}

{{< math-block type="proof" >}}
对任意原可行 $x$ 和 $\lambda\ge0$，

$$
g(\lambda,\mu)
\le L(x,\lambda,\mu)
\le f_0(x).
$$

先对可行 $x$ 取下确界，再对对偶可行乘子取上确界，得到 $d^*\le p^*$。

对每个固定 $x$，$L(x,\lambda,\mu)$ 是 $(\lambda,\mu)$ 的仿射函数。对偶函数是这一族仿射函数的逐点下确界，因此为凹函数。
{{< /math-block >}}

## Slater 条件与强对偶

以下考虑凸优化问题：$f_0,f_1,\ldots,f_m$ 为凸函数，等式约束写成 $Ax=b$。仿射不等式不要求严格满足；设前 $k$ 个 $f_i$ 为仿射函数。

Slater 条件要求存在 $\hat x$ 使

$$
f_i(\hat x)\le0,quad i=1,\ldots,k,
$$

$$
f_i(\hat x)<0,quad i=k+1,\ldots,m,
\qquad
A\hat x=b.
$$

{{< math-block type="theorem" title="Slater 强对偶定理" label="thm-lagrange-slater" >}}
若凸问题 $(P)$ 的最优值有限且满足 Slater 条件，则

$$
p^*=d^*,
$$

并且对偶最优解可以取得。
{{< /math-block >}}

{{< math-block type="proof" >}}
定义凸集

$$
\mathcal A=left\{(u,v,t):
\begin{array}{l}
\text{存在 }x\text{ 使 }f_i(x)\le u_i,\\
Ax-b=v,\ f_0(x)\le t
\end{array}ight\}.
$$

$\mathcal A$ 的凸性来自 $f_i$ 的凸性与等式映射的仿射性。由原最优值定义，$(0,0,p^*)$ 位于 $\mathcal A$ 的边界，而

$$
\mathcal B=\{(0,0,t):t<p^*\}
$$

与 $\mathcal A$ 不相交。分离定理给出非零向量 $(\lambda,\mu,\nu)$，使

$$
\lambda^\top u+\mu^\top v+\nu t
\ge \nu p^*,qquad (u,v,t)\in\mathcal A.
$$

因为 $u$ 可以沿正方向任意增大，必须有 $\lambda\ge0$；因为 $t$ 可以沿正方向增大，必须有 $\nu\ge0$。Slater 条件排除 $\nu=0$：若 $\nu=0$，将严格可行点代入分离式，会迫使非仿射约束的乘子为零，再由等式与仿射约束的相对内部性质推出全部分离系数为零，矛盾。

故可将分离向量归一化为 $\nu=1$。对任意 $x$，点 $(f(x),Ax-b,f_0(x))$ 属于 $\mathcal A$，从而

$$
L(x,\lambda,\mu)
=f_0(x)+\lambda^\top f(x)+\mu^\top(Ax-b)
\ge p^*.
$$

对 $x$ 取下确界得到 $g(\lambda,\mu)\ge p^*$。弱对偶给出 $g(\lambda,\mu)\le p^*$，因此两者相等，且该乘子达到对偶最优值。
{{< /math-block >}}

Slater 条件是充分而非必要条件。非凸问题通常可能存在对偶间隙，但对偶值仍然是有效下界。

## 互补松弛与鞍点

{{< math-block type="proposition" title="零对偶间隙的两个后果" label="prop-zero-gap" >}}
设 $x^*$ 原最优、$(\lambda^*,\mu^*)$ 对偶最优，且 $p^*=d^*$。则

1. $x^*$ 最小化 $L(x,\lambda^*,\mu^*)$；
2. $\lambda_i^*f_i(x^*)=0$，$i=1,\ldots,m$。
{{< /math-block >}}

{{< math-block type="proof" >}}
由弱对偶推导中的不等式链，

$$
p^*=f_0(x^*)
\ge L(x^*,\lambda^*,\mu^*)
\ge g(\lambda^*,\mu^*)=d^*=p^*.
$$

所以两处不等式都取等。第二处取等说明 $x^*$ 达到 $L$ 的下确界；第一处取等与原可行性给出

$$
\sum_i\lambda_i^*f_i(x^*)=0.
$$

每项都不大于零，因此每项必须为零。
{{< /math-block >}}

## KKT 条件

若所有函数可微，Karush--Kuhn--Tucker 条件为

$$
\begin{aligned}
&f_i(x^*)\le0, &&i=1,\ldots,m,\\
&h_j(x^*)=0, &&j=1,\ldots,p,\\
&\lambda_i^*\ge0, &&i=1,\ldots,m,\\
&\lambda_i^*f_i(x^*)=0, &&i=1,\ldots,m,\\
&\nabla f_0(x^*)+
\sum_{i=1}^m\lambda_i^*\nabla f_i(x^*)+
\sum_{j=1}^p\mu_j^*\nabla h_j(x^*)=0.
\end{aligned}
$$

前两行是原可行性，第三行是对偶可行性，第四行是互补松弛，最后一行是 Lagrange 函数关于 $x$ 的驻点条件。

{{< math-block type="theorem" title="KKT 的必要性" label="thm-kkt-necessity" >}}
若可微问题存在原、对偶最优解且零对偶间隙成立，则这些解满足 KKT 条件。
{{< /math-block >}}

{{< math-block type="proof" >}}
原、对偶可行性由定义得到，互补松弛由上一命题得到。上一命题还表明 $x^*$ 是 $L(\cdot,\lambda^*,\mu^*)$ 的全局极小点；由于该函数可微，一阶必要条件给出

$$
\nabla_xL(x^*,\lambda^*,\mu^*)=0,
$$

即驻点条件。
{{< /math-block >}}

{{< math-block type="theorem" title="凸问题中 KKT 的充分性" label="thm-kkt-sufficiency" >}}
若 $f_0,f_i$ 为凸可微函数，$h_j$ 为仿射函数，且 $(x^*,\lambda^*,\mu^*)$ 满足 KKT 条件，则 $x^*$ 原最优、$(\lambda^*,\mu^*)$ 对偶最优，并且零对偶间隙成立。
{{< /math-block >}}

{{< math-block type="proof" >}}
$L(\cdot,\lambda^*,\mu^*)$ 是凸可微函数。驻点条件意味着 $x^*$ 是它的全局最小点，所以

$$
g(\lambda^*,\mu^*)
=L(x^*,\lambda^*,\mu^*).
$$

利用原可行性、等式约束和互补松弛，

$$
L(x^*,\lambda^*,\mu^*)=f_0(x^*).
$$

于是对偶可行点的目标值等于原可行点的目标值。由弱对偶，两者必分别最优，且对偶间隙为零。
{{< /math-block >}}

因此，对满足 Slater 条件的可微凸问题，$x^*$ 最优当且仅当存在乘子使 KKT 条件成立。

## 等式约束凸二次规划

考虑

$$
\begin{aligned}
\min_x\quad&\frac12x^\top Qx+q^\top x+r\\
\text{s.t.}\quad&Ax=b,
\end{aligned}
$$

其中 $Q\succeq0$。KKT 条件化为线性系统

$$
\begin{pmatrix}
Q&A^\top\\
A&0
\end{pmatrix}
\begin{pmatrix}x\\\mu\end{pmatrix}
=
\begin{pmatrix}-q\\b\end{pmatrix}.
$$

只要该系统存在解，解出的 $x$ 就是全局最优解；在适当的非退化条件下，KKT 矩阵可逆，最优解与乘子唯一。
