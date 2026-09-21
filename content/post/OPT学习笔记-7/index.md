---
title: OPT学习笔记-7：网络流与生成树多面体
description: 从最大流最小割定理出发，讨论整数性、割的线性规划表示与最小生成树多面体
slug: opt-notes-7
date: 2026-09-20 23:15:00+0800
math: true
categories:
    - Math
tags:
    - notes
    - OPT
weight: 7
---

组合优化中的离散对象常常可以由线性不等式精确描述。本篇以最大流和最小生成树为例，说明线性规划为何能够直接给出整数解。

## 最大流问题

设有向图 $G=(V,E)$，源点为 $s$，汇点为 $t$，每条弧 $e$ 的容量为 $u_e\ge0$。流 $x\in\mathbb{R}^E_+$ 满足容量约束

$$
0\le x_e\le u_e,
$$

并在每个中间节点满足流量守恒：

$$
\sum_{e\in\delta^-(v)}x_e
=
\sum_{e\in\delta^+(v)}x_e,
\qquad v\in V\setminus\{s,t\}.
$$

流的值为从源点净流出的总量

$$
|x|=\sum_{e\in\delta^+(s)}x_e-
\sum_{e\in\delta^-(s)}x_e.
$$

最大流问题就是在线性约束下最大化 $|x|$。

## 割与弱对偶

一个 $s$-$t$ 割由集合 $S\subseteq V$ 确定，其中 $s\in S,t\notin S$。其容量为

$$
u(\delta^+(S))=\sum_{e\in\delta^+(S)}u_e.
$$

{{< math-block type="proposition" title="流不超过割容量" label="prop-flow-cut-weak" >}}
对任意可行流 $x$ 与任意 $s$-$t$ 割 $S$，都有

$$
|x|\le u(\delta^+(S)).
$$
{{< /math-block >}}

{{< math-block type="proof" >}}
将 $S\setminus\{s\}$ 中各节点的流量守恒式相加，并与源点的净流出量合并，$S$ 内部弧的贡献相互抵消，得到

$$
|x|=\sum_{e\in\delta^+(S)}x_e-
\sum_{e\in\delta^-(S)}x_e.
$$

因为 $x_e\ge0$ 且 $x_e\le u_e$，

$$
|x|\le\sum_{e\in\delta^+(S)}x_e
\le\sum_{e\in\delta^+(S)}u_e.
$$
{{< /math-block >}}

这就是最大流与最小割之间的弱对偶。

## 增广路与最大流最小割

给定流 $x$，残量图中每条原弧 $(i,j)$ 有正向剩余容量 $u_{ij}-x_{ij}$，并有反向剩余容量 $x_{ij}$。若残量图中存在从 $s$ 到 $t$ 的路径，就可以沿路径增加流量。

{{< math-block type="theorem" title="最大流最小割定理" label="thm-max-flow-min-cut" >}}
最大流的值等于最小 $s$-$t$ 割的容量。
{{< /math-block >}}

{{< math-block type="proof" >}}
从零流开始反复沿残量图中的 $s$-$t$ 路径增广。算法停止时，令 $S$ 为残量图中从 $s$ 可达的节点集合。此时 $t\notin S$，所以 $S$ 是一个 $s$-$t$ 割。

若 $e\in\delta^+(S)$，则其正向剩余容量必须为零，否则终点也可达，故 $x_e=u_e$。若 $e\in\delta^-(S)$，则其反向剩余容量必须为零，否则可以从 $S$ 中的节点沿反向弧到达该弧的起点，故 $x_e=0$。因此

$$
|x|=
\sum_{e\in\delta^+(S)}x_e-
\sum_{e\in\delta^-(S)}x_e
=
\sum_{e\in\delta^+(S)}u_e.
$$

该流的值等于这个割的容量。结合任意流都不超过任意割容量的弱对偶，两者分别为最大流和最小割。
{{< /math-block >}}

{{< math-block type="corollary" title="最大流的整数性" label="cor-max-flow-integrality" >}}
若所有容量 $u_e$ 都是整数，则存在整数最大流。
{{< /math-block >}}

{{< math-block type="proof" >}}
从整数零流出发。每次增广量是路径上剩余容量的最小值；只要当前流与容量为整数，所有剩余容量和增广量也都是整数。因此每次增广后仍得到整数流。流值每次至少增加 $1$，且受总容量限制，所以算法有限步终止；由最大流最小割定理，终止流是整数最大流。
{{< /math-block >}}

从线性规划角度看，最小割可以用节点势 $y_v$ 和弧变量 $z_{ij}$ 表示：

$$
\begin{aligned}
\min_{y,z}\quad&\sum_{(i,j)\in E}u_{ij}z_{ij}\\
\text{s.t.}\quad&y_i-y_j\le z_{ij},\quad (i,j)\in E,\\
&y_s-y_t=1,\quad z\ge0.
\end{aligned}
$$

它与最大流线性规划互为对偶；最优的 $0$-$1$ 节点势对应一个割。

## 最小生成树

现在令 $G=(V,E)$ 为连通无向图。生成树是连接所有节点且不含环的边集。每条边 $e$ 有成本 $c_e$，最小生成树问题为

$$
\min_{T\text{ 为生成树}}\sum_{e\in T}c_e.
$$

记 $E(S)$ 为两个端点都在 $S\subseteq V$ 中的边集。

{{< math-block type="proposition" title="生成树的刻画" label="prop-spanning-tree-characterization" >}}
边集 $T\subseteq E$ 是生成树，当且仅当

$$
|T|=|V|-1,
\qquad
|T\cap E(S)|\le |S|-1,quad
\forall\varnothing\ne S\subseteq V.
$$
{{< /math-block >}}

{{< math-block type="proof" >}}
若 $T$ 是生成树，则任意诱导子图 $(S,T\cap E(S))$ 都是森林。一个含 $|S|$ 个节点的森林至多有 $|S|-1$ 条边，故不等式成立；树本身有 $|V|-1$ 条边。

反之，约束排除了所有环：若 $T$ 含一个节点集为 $S$ 的环，则该环已在 $E(S)$ 中贡献 $|S|$ 条边，与不等式矛盾。因此 $(V,T)$ 是森林。含 $|V|$ 个节点且有 $|V|-1$ 条边的森林恰有一个连通分量，所以它是生成树。
{{< /math-block >}}

由此得到生成树多面体

$$
P_{\mathrm{ST}}=
\left\{x\in\mathbb{R}^E_+:
x(E)=|V|-1,
\ x(E(S))\le |S|-1,
\ \forall\varnothing\ne S\subsetneq V
\right\}.
$$

{{< math-block type="theorem" title="生成树多面体的整数性" label="thm-spanning-tree-polytope" >}}
$P_{\mathrm{ST}}$ 的顶点恰好是生成树的示性向量。因此

$$
P_{\mathrm{ST}}=\operatorname{conv}
\{\chi^T:T\text{ 为 }G\text{ 的生成树}\}.
$$
{{< /math-block >}}

{{< math-block type="proof" >}}
先注意：对任意边集 $F\subseteq E$，令 $(V,F)$ 的连通分量节点集为 $S_1,\ldots,S_q$。由定义中的子图约束，

$$
x(F)\le\sum_{j=1}^qx(E(S_j))
\le\sum_{j=1}^q(|S_j|-1)
=|V|-q=:r(F).
$$

$r(F)$ 正是图拟阵中 $F$ 的秩。

任取成本向量 $c$，按非降序排列边：$c_{e_1}\le\cdots\le c_{e_m}$，并记 $F_k=\{e_1,\ldots,e_k\}$。对任意 $x\in P_{\mathrm{ST}}$，分部求和给出

$$
c^\top x
=c_{e_m}x(E)-
\sum_{k=1}^{m-1}(c_{e_{k+1}}-c_{e_k})x(F_k)
\ge
c_{e_m}(|V|-1)-
\sum_{k=1}^{m-1}(c_{e_{k+1}}-c_{e_k})r(F_k).
$$

Kruskal 算法按这一顺序加入不产生环的边。算法结束所得生成树 $T$ 对每个 $k$ 都满足

$$
|T\cap F_k|=r(F_k),
$$

因为算法在 $F_k$ 内恰好选出其一个极大森林。因此 $\chi^T$ 使上面的下界取等号：每个线性目标在 $P_{\mathrm{ST}}$ 上都有一个生成树示性向量作为最优解。

若 $P_{\mathrm{ST}}$ 存在非整数顶点 $\bar x$，可选择一个使 $\bar x$ 成为唯一最优解的线性目标。但上述论证又为同一目标给出一个整数的生成树最优解，产生矛盾。故所有顶点均为生成树示性向量，结论成立。
{{< /math-block >}}

该描述包含指数多个子集约束，但并不意味着它不可计算。若某个候选点违反约束，可以把寻找违反约束的问题转化为最小割问题；这正是分离算法与割平面方法的基本思想。
