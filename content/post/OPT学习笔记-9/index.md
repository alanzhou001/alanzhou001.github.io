---
title: OPT学习笔记-9：锥规划、强对偶与半正定规划
description: 从凸锥诱导的偏序出发，介绍二阶锥规划、锥对偶、Slater 条件与半正定规划
slug: opt-notes-9
date: 2026-09-20 23:17:00+0800
math: true
categories:
    - Math
tags:
    - notes
    - OPT
weight: 9
---

线性规划使用非负正交锥来解释向量不等式。把这个锥替换为更一般的凸锥，就得到锥规划；二阶锥规划和半正定规划都是其中的重要特例。

## 凸锥与锥诱导的偏序

若集合 $K\subseteq\mathbb{R}^m$ 对非负数乘封闭，即 $x\in K,\lambda\ge0$ 蕴含 $\lambda x\in K$，则称 $K$ 为锥。

{{< math-block type="proposition" title="凸锥的等价刻画" label="prop-convex-cone" >}}
$K$ 是凸锥，当且仅当它对加法和非负数乘封闭。
{{< /math-block >}}

{{< math-block type="proof" >}}
若 $K$ 是凸锥，任取 $x,y\in K$。凸性给出 $(x+y)/2\in K$，再乘以 $2$ 得 $x+y\in K$；非负数乘封闭来自锥的定义。

反之，若 $K$ 对加法和非负数乘封闭，则对 $\theta\in[0,1]$ 有 $\theta x,(1-\theta)y\in K$，从而 $\theta x+(1-\theta)y\in K$，故 $K$ 是凸集，也是锥。
{{< /math-block >}}

凸锥 $K$ 在向量空间上诱导关系

$$
a\succeq_K b
\quad\Longleftrightarrow\quad
a-b\in K.
$$

若 $K$ **尖锐**，即 $K\cap(-K)=\{0\}$，上述关系满足反对称性，因而是偏序。一个闭、凸、尖锐且具有非空内部的锥称为**适当锥**。

## Lorentz 锥与二阶锥规划

$m+1$ 维 Lorentz 锥为

$$
\mathcal L^{m+1}
=\{(x,t)\in\mathbb{R}^m\times\mathbb{R}:\|x\|_2\le t\}.
$$

{{< math-block type="proposition" title="Lorentz 锥是适当锥" label="prop-lorentz-proper" >}}
$\mathcal L^{m+1}$ 是闭、凸、尖锐且具有非空内部的锥。
{{< /math-block >}}

{{< math-block type="proof" >}}
范数连续，所以 $\|x\|_2\le t$ 定义闭集。若 $(x,t),(y,s)$ 属于该锥且 $\alpha,\beta\ge0$，由三角不等式

$$
\|\alpha x+\beta y\|_2
\le\alpha\|x\|_2+\beta\|y\|_2
\le\alpha t+\beta s,
$$

故它是凸锥。若 $(x,t)$ 与 $-(x,t)$ 都属于锥，则 $t\ge\|x\|_2$ 且 $-t\ge\|x\|_2$，只能有 $x=0,t=0$，所以锥尖锐。最后，$\{(x,t):\|x\|_2<t\}$ 是其非空内部。
{{< /math-block >}}

形如

$$
\|A_ix-b_i\|_2\le c_i^\top x-d_i
$$

的约束就是一个二阶锥约束。线性目标、若干二阶锥约束与仿射等式共同组成二阶锥规划（SOCP）。

若 $Q\succeq0$，取 $Q=R^\top R$，则凸二次目标可用旋转二阶锥表示。引入 $t$ 后，

$$
\frac12x^\top Qx\le t
\quad\Longleftrightarrow\quad
2t\cdot1\ge\|Rx\|_2^2,quad t\ge0.
$$

因此凸二次规划可以改写为 SOCP。Markowitz 均值--方差模型

$$
\begin{aligned}
\min_x\quad&x^\top Vx\\
\text{s.t.}\quad&\mu^\top x\ge\bar\mu,\\
&\mathbf1^\top x=1
\end{aligned}
$$

在协方差矩阵 $V\succeq0$ 时就是这一情形。

## 对偶锥与弱对偶

{{< math-block type="definition" title="对偶锥" label="def-dual-cone" >}}
集合 $K\subseteq\mathbb{R}^m$ 的对偶锥定义为

$$
K^*=\{\lambda\in\mathbb{R}^m:
\langle\lambda,z\rangle\ge0,
\ \forall z\in K\}.
$$
{{< /math-block >}}

$K^*$ 是经过原点的闭半空间的交，因此总是闭凸锥。若 $K$ 是闭凸锥，则双极定理给出 $(K^*)^*=K$。

考虑原问题与对偶问题

$$
\begin{aligned}
(P)\quad \min_x\quad&\langle c,x\rangle
&\text{s.t.}\quad&Ax-b\in K,\\
(D)\quad \max_\lambda\quad&\langle b,\lambda\rangle
&\text{s.t.}\quad&A^\top\lambda=c,\quad\lambda\in K^*.
\end{aligned}
$$

{{< math-block type="theorem" title="锥规划弱对偶" label="thm-conic-weak-duality" >}}
任意原可行解 $x$ 与对偶可行解 $\lambda$ 都满足

$$
\langle b,\lambda\rangle\le\langle c,x\rangle.
$$
{{< /math-block >}}

{{< math-block type="proof" >}}
因为 $Ax-b\in K$ 且 $\lambda\in K^*$，

$$
0\le\langle\lambda,Ax-b\rangle
=\langle A^\top\lambda,x\rangle-\langle\lambda,b\rangle
=\langle c,x\rangle-\langle\lambda,b\rangle.
$$
{{< /math-block >}}

与线性规划不同，一般锥规划即使最优值有限，也可能存在对偶间隙或最优值不被取得。常用的约束规范是 Slater 条件。

{{< math-block type="theorem" title="Slater 条件下的强锥对偶" label="thm-conic-slater" >}}
设 $K$ 为适当锥。若原问题最优值有限，且存在严格可行点 $\hat x$ 使

$$
A\hat x-b\in\operatorname{int}K,
$$

则原、对偶最优值相等，且对偶最优解可以取得。对偶严格可行时有对称结论。
{{< /math-block >}}

{{< math-block type="proof" >}}
记原最优值为 $p^*$，考虑凸集

$$
\mathcal C=\{(b-Ax+s,p^*-\langle c,x\rangle-r):
x\in\mathbb{R}^n, s\in K, r>0\}.
$$

由 $p^*$ 的定义，$(0,0)\notin\mathcal C$：第一分量为零意味着 $Ax-b=s\in K$，而第二分量为零又意味着 $\langle c,x\rangle=p^*-r<p^*$，产生矛盾。严格可行性保证该集合在约束方向上具有内部点。由严格分离定理，存在非零 $(q,\alpha)$ 使得

$$
\langle q,b-Ax+s\rangle
+\alpha(p^*-\langle c,x\rangle-r)\ge0
$$

对所有 $x,s,r$ 成立。让 $s$ 在 $K$ 中任意变化可得 $q\in K^*$；让 $r>0$ 任意变化可得 $\alpha\le0$。严格可行性排除 $\alpha=0$，故可将分离向量归一化为 $\alpha=-1$。

由于 $x$ 可以任意取值，线性项必须消失，所以 $A^\top q=c$；其余常数项给出 $\langle b,q\rangle\ge p^*$。弱对偶又给出反向不等式，故 $\langle b,q\rangle=p^*$，且 $q$ 是对偶最优解。
{{< /math-block >}}

在强对偶成立时，原、对偶可行解最优等价于**锥互补松弛**：

$$
\langle\lambda,Ax-b\rangle=0.
$$

## 半正定锥与 SDP

在对称矩阵空间 $\mathbb S^m$ 上使用 Frobenius 内积

$$
\langle A,B\rangle=\operatorname{tr}(AB).
$$

半正定锥为

$$
\mathbb S^m_+=\{X\in\mathbb S^m:X\succeq0\}.
$$

{{< math-block type="proposition" title="半正定锥自对偶" label="prop-psd-self-dual" >}}
在 Frobenius 内积下，

$$
(\mathbb S^m_+)^*=\mathbb S^m_+.
$$
{{< /math-block >}}

{{< math-block type="proof" >}}
若 $Y\succeq0$，写成 $Y=RR^\top$。对任意 $X\succeq0$，

$$
\langle X,Y\rangle
=\operatorname{tr}(XRR^\top)
=\operatorname{tr}(R^\top XR)\ge0,
$$

所以 $Y$ 属于对偶锥。反之，若 $Y$ 属于对偶锥，则对每个 $v$，取 $X=vv^\top\succeq0$，得到

$$
v^\top Yv=\langle Y,vv^\top\rangle\ge0.
$$

故 $Y\succeq0$。
{{< /math-block >}}

给定 $A_1,\ldots,A_n,B\in\mathbb S^m$，半正定规划可写为

$$
\begin{aligned}
\min_x\quad&c^\top x\\
\text{s.t.}\quad&\sum_{i=1}^nx_iA_i-B\succeq0.
\end{aligned}
$$

由自对偶性，其对偶为

$$
\begin{aligned}
\max_{\Lambda}\quad&\langle B,\Lambda\rangle\\
\text{s.t.}\quad&\langle A_i,\Lambda\rangle=c_i,quad i=1,\ldots,n,\\
&\Lambda\succeq0.
\end{aligned}
$$

二阶锥约束还能写成线性矩阵不等式

$$
\|z\|_2\le t
\quad\Longleftrightarrow\quad
\begin{pmatrix}
tI&z\\
z^\top&t
\end{pmatrix}\succeq0,
$$

其等价性可由 Schur 补直接验证。因此 LP、SOCP 与 SDP 构成逐层扩展的凸优化模型族。
