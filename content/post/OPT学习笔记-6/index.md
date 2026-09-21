---
title: OPT学习笔记-6：线性规划对偶的博弈论应用
description: 利用线性规划强对偶分析零和矩阵博弈、合作博弈的核心以及超模博弈中的边际分配
slug: opt-notes-6
date: 2026-09-20 23:14:00+0800
math: true
categories:
    - Math
tags:
    - notes
    - OPT
weight: 6
---

上一篇讨论了线性规划对偶。本篇把强对偶用于两类博弈：在零和博弈中，它给出极小极大定理；在合作博弈中，它刻画核心非空的充要条件。

## 零和矩阵博弈

设行玩家选择 $i\in\{1,\ldots,m\}$，列玩家选择 $j\in\{1,\ldots,n\}$。收益矩阵为 $P\in\mathbb{R}^{m\times n}$，$P_{ij}$ 是列玩家获得、行玩家支付的收益。因此行玩家希望最小化收益，列玩家希望最大化收益。

混合策略分别属于概率单纯形

$$
\Delta_m=\{x\in\mathbb{R}^m_+:\mathbf 1^\top x=1\},
\qquad
\Delta_n=\{y\in\mathbb{R}^n_+:\mathbf 1^\top y=1\}.
$$

当双方采用 $x$ 与 $y$ 时，期望收益为 $x^\top Py$。行玩家能够保证的最坏收益为

$$
\min_{x\in\Delta_m}\max_{y\in\Delta_n}x^\top Py,
$$

而列玩家能够保证的收益为

$$
\max_{y\in\Delta_n}\min_{x\in\Delta_m}x^\top Py.
$$

对任意 $x,y$，线性函数在单纯形上的最值都在顶点取得，所以

$$
\max_{y\in\Delta_n}x^\top Py=\max_j(P^\top x)_j,
\qquad
\min_{x\in\Delta_m}x^\top Py=\min_i(Py)_i.
$$

于是双方的问题分别写成

$$
\begin{aligned}
\min_{x,v}\quad &v\\
\text{s.t.}\quad&P^\top x\le v\mathbf 1,\\
&\mathbf 1^\top x=1,\quad x\ge0,
\end{aligned}
\tag{P}
$$

和

$$
\begin{aligned}
\max_{y,w}\quad&w\\
\text{s.t.}\quad&Py\ge w\mathbf 1,\\
&\mathbf 1^\top y=1,\quad y\ge0.
\end{aligned}
\tag{D}
$$

{{< math-block type="theorem" title="von Neumann 极小极大定理" label="thm-minimax" >}}
任意有限零和矩阵博弈都满足

$$
\min_{x\in\Delta_m}\max_{y\in\Delta_n}x^\top Py
=
\max_{y\in\Delta_n}\min_{x\in\Delta_m}x^\top Py.
$$
{{< /math-block >}}

{{< math-block type="proof" >}}
问题 $(P)$ 与 $(D)$ 互为线性规划对偶。两个单纯形均非空且紧，因此两边最优值有限并能取得。由线性规划强对偶，$(P)$ 与 $(D)$ 的最优值相等，这正是所需等式。
{{< /math-block >}}

共同的最优值称为博弈的**值**。若 $x^*$ 与 $y^*$ 分别为两个线性规划的最优解，则

$$
(x^*)^\top Py\le (x^*)^\top Py^*\le x^\top Py^*
$$

对所有 $x\in\Delta_m,y\in\Delta_n$ 成立。因此任一方单独偏离都不会改善自己的收益，$(x^*,y^*)$ 构成 Nash 均衡；反之，每个 Nash 均衡都由双方的安全策略构成，并具有相同的博弈值。

## 合作博弈与核心

设玩家集合为 $N=\{1,\ldots,n\}$。特征函数

$$
v:2^N\to\mathbb{R},\qquad v(\varnothing)=0
$$

给出每个联盟 $S\subseteq N$ 能够独立创造的价值。一个分配 $x\in\mathbb{R}^n$ 属于博弈的**核心**，若

$$
\sum_{i\in N}x_i=v(N),
\qquad
\sum_{i\in S}x_i\ge v(S),\quad \forall S\subseteq N.
$$

第一个条件要求全部价值被分完；第二个条件保证没有联盟愿意退出并自行合作。

称非负权重 $\{\lambda_S\}_{S\subseteq N}$ 是**平衡的**，若每位玩家获得的总权重恰为 $1$：

$$
\sum_{S\ni i}\lambda_S=1,
\qquad i\in N.
$$

{{< math-block type="theorem" title="Bondareva--Shapley 定理" label="thm-bondareva-shapley" >}}
合作博弈 $(N,v)$ 的核心非空，当且仅当对每组平衡权重都有

$$
\sum_{S\subseteq N}\lambda_Sv(S)\le v(N).
$$
{{< /math-block >}}

{{< math-block type="proof" >}}
考虑线性规划

$$
\begin{aligned}
\min_x\quad&\sum_{i\in N}x_i\\
\text{s.t.}\quad&\sum_{i\in S}x_i\ge v(S),\quad S\subseteq N.
\end{aligned}
\tag{P}
$$

由于约束中包含 $S=N$，其最优值至少为 $v(N)$。核心非空恰好等价于该最优值等于 $v(N)$：若存在核心分配，它是目标值为 $v(N)$ 的可行解；反之，目标值为 $v(N)$ 的最优解满足核心的全部条件。

给每个联盟约束配置对偶变量 $\lambda_S\ge0$，得到

$$
\begin{aligned}
\max_\lambda\quad&\sum_{S\subseteq N}\lambda_Sv(S)\\
\text{s.t.}\quad&\sum_{S\ni i}\lambda_S=1,
\quad i\in N,\\
&\lambda_S\ge0.
\end{aligned}
\tag{D}
$$

对偶可行解正是平衡权重。由强对偶，原问题最优值等于所有平衡权重下 $\sum_S\lambda_Sv(S)$ 的最大值。因此原问题最优值为 $v(N)$，当且仅当每组平衡权重都满足题中的不等式。
{{< /math-block >}}

## 超模博弈与边际分配

{{< math-block type="definition" title="超模博弈" label="def-supermodular-game" >}}
若对任意 $A,B\subseteq N$ 都有

$$
v(A)+v(B)\le v(A\cup B)+v(A\cap B),
$$

则称 $(N,v)$ 为超模博弈，也称凸合作博弈。
{{< /math-block >}}

超模性等价于边际收益递增：若 $A\subseteq B$ 且 $i\notin B$，则

$$
v(A\cup\{i\})-v(A)
\le
v(B\cup\{i\})-v(B).
$$

{{< math-block type="theorem" title="超模博弈的核心非空" label="thm-supermodular-core" >}}
每个超模合作博弈都有非空核心。
{{< /math-block >}}

{{< math-block type="proof" >}}
任取玩家排列 $\pi$，记

$$
S_k=\{\pi(1),\ldots,\pi(k)\},\qquad S_0=\varnothing,
$$

并定义边际分配

$$
x_{\pi(k)}=v(S_k)-v(S_{k-1}).
$$

望远镜求和立即给出 $\sum_{i\in N}x_i=v(N)$。任取联盟 $T$，将其中玩家按 $\pi$ 中的顺序写作 $\pi(k_1),\ldots,\pi(k_r)$，并令 $T_\ell=\{\pi(k_1),\ldots,\pi(k_\ell)\}$。由于 $T_{\ell-1}\subseteq S_{k_\ell-1}$，边际收益递增给出

$$
x_{\pi(k_\ell)}
=v(S_{k_\ell})-v(S_{k_\ell-1})
\ge v(T_\ell)-v(T_{\ell-1}).
$$

对 $\ell$ 求和得到

$$
\sum_{i\in T}x_i\ge v(T)-v(\varnothing)=v(T).
$$

因此 $x$ 属于核心。
{{< /math-block >}}

边际分配还提供了核心上线性目标的显式最优解。若成本满足 $c_1\ge c_2\ge\cdots\ge c_n$，按 $1,2,\ldots,n$ 的顺序构造边际分配。对任意核心分配 $z$，分部求和得到

$$
c^\top z
=c_n v(N)+\sum_{k=1}^{n-1}(c_k-c_{k+1})\sum_{i=1}^kz_i
\ge c_n v(N)+\sum_{k=1}^{n-1}(c_k-c_{k+1})v(\{1,\ldots,k\}).
$$

边际分配使每个前缀联盟的不等式取等号，所以它达到该下界，是 $\min\{c^\top z:z\in C(v,N)\}$ 的最优解。
