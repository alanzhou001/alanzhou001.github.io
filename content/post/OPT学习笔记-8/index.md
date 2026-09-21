---
title: OPT学习笔记-8：匹配、多面体与稳定婚姻
description: 介绍二分图完美匹配、Birkhoff--von Neumann 定理、置换多面体与 Gale--Shapley 稳定匹配算法
slug: opt-notes-8
date: 2026-09-20 23:16:00+0800
math: true
categories:
    - Math
tags:
    - notes
    - OPT
weight: 8
---

本篇继续讨论多面体组合优化。二分图匹配的线性规划松弛天然具有整数顶点；加入偏好后，稳定婚姻问题也存在稳定解，并可由 Gale--Shapley 算法构造。

## 二分图完美匹配

设二分图 $G=(U,W,E)$，其中 $|U|=|W|=n$。完美匹配 $M\subseteq E$ 要求每个节点恰好与一条匹配边相连。令 $x_{ij}$ 表示边 $(i,j)$ 是否被选择，则最小成本完美匹配可写成

$$
\begin{aligned}
\min_x\quad&\sum_{(i,j)\in E}c_{ij}x_{ij}\\
\text{s.t.}\quad&\sum_{j:(i,j)\in E}x_{ij}=1,
&&i\in U,\\
&\sum_{i:(i,j)\in E}x_{ij}=1,
&&j\in W,\\
&x_{ij}\in\{0,1\}.
\end{aligned}
$$

在完全二分图中，把整数约束放松为 $x_{ij}\ge0$，得到双随机矩阵集合。

{{< math-block type="theorem" title="Birkhoff--von Neumann 定理" label="thm-birkhoff-von-neumann" >}}
双随机矩阵多面体

$$
\mathcal B_n=
\left\{X\in\mathbb{R}^{n\times n}_+:
X\mathbf 1=\mathbf 1,
X^\top\mathbf 1=\mathbf 1
\right\}
$$

等于所有置换矩阵的凸包。
{{< /math-block >}}

{{< math-block type="proof" >}}
任取 $X\in\mathcal B_n$，构造支撑二分图：当 $x_{ij}>0$ 时连接行节点 $i$ 与列节点 $j$。对任意行节点集合 $S$，从这些行流出的总权重为 $|S|$；它们只能流入邻居集合 $N(S)$，而每一列接收的总权重为 $1$。因此

$$
|S|\le |N(S)|.
$$

由 Hall 定理，支撑图中存在完美匹配 $M$。令

$$
\varepsilon=\min_{(i,j)\in M}x_{ij}>0,
$$

并记对应置换矩阵为 $P_M$。若 $\varepsilon=1$，则 $X=P_M$。否则

$$
X'=\frac{X-\varepsilon P_M}{1-\varepsilon}
$$

仍是双随机矩阵，并且至少少一个正元素。对正元素个数归纳，$X'$ 是置换矩阵的凸组合，于是

$$
X=\varepsilon P_M+(1-\varepsilon)X'
$$

也是置换矩阵的凸组合。反方向显然成立，因为置换矩阵以及它们的凸组合都是双随机矩阵。
{{< /math-block >}}

因此，二分图完美匹配的线性规划松弛总能取得整数最优解。

## 置换多面体

给定向量 $a\in\mathbb{R}^n$，其所有坐标置换的凸包称为置换多面体：

$$
\operatorname{Perm}(a)
=\operatorname{conv}\{Pa:P\text{ 为置换矩阵}\}.
$$

由 Birkhoff--von Neumann 定理，它也可以写成

$$
\operatorname{Perm}(a)=\{Xa:X\in\mathcal B_n\}.
$$

这说明一个看似需要枚举 $n!$ 个排列的凸包，可以通过 $O(n^2)$ 个变量和约束的扩展表示来描述。

## 稳定婚姻问题

设两侧参与者分别为 $M=\{m_1,\ldots,m_n\}$ 与 $W=\{w_1,\ldots,w_n\}$，每个人都对另一侧给出严格偏好顺序。完美匹配 $\mu$ 中，若存在未被匹配在一起的一对 $(m_i,w_j)$，且

- $m_i$ 更偏好 $w_j$ 而不是当前伴侣 $\mu(m_i)$；
- $w_j$ 更偏好 $m_i$ 而不是当前伴侣 $\mu(w_j)$，

则称 $(m_i,w_j)$ 为**阻挡对**。不存在阻挡对的匹配称为稳定匹配。

### Gale--Shapley 算法

采用 $M$ 方提出申请的版本：

1. 每个尚未匹配且仍有未申请对象的 $m_i$，向自己尚未申请过的最高偏好 $w_j$ 申请；
2. 每个 $w_j$ 在当前暂留对象和新申请者中保留自己最偏好的一位，拒绝其余人；
3. 重复以上过程，直到无人再能申请。

{{< math-block type="theorem" title="Gale--Shapley 定理" label="thm-gale-shapley" >}}
Gale--Shapley 算法有限步终止，并输出一个稳定完美匹配。
{{< /math-block >}}

{{< math-block type="proof" >}}
每个 $m_i$ 至多向每个 $w_j$ 申请一次，所以申请总数至多为 $n^2$，算法必然有限步终止。

终止时不可能有人未匹配。否则存在未匹配的 $m_i$，他必已向所有 $w_j$ 申请并被拒绝。女性一旦收到申请，此后始终暂留某位申请者，因此每位女性都暂留一人；这将使所有男性均被匹配，与 $m_i$ 未匹配矛盾。故结果是完美匹配。

若最终存在阻挡对 $(m_i,w_j)$，则 $m_i$ 比起最终伴侣更偏好 $w_j$，所以他一定更早向 $w_j$ 申请过。$w_j$ 当时拒绝了 $m_i$，或后来为更偏好的申请者放弃了他；而她暂留对象的质量只会随算法进行而提高。因此最终 $w_j$ 更偏好自己的伴侣而不是 $m_i$，与阻挡对的定义矛盾。故输出匹配稳定。
{{< /math-block >}}

该版本还产生 $M$ 方最优的稳定匹配：每个 $m_i$ 得到自己在所有稳定匹配中可能得到的最佳伴侣；相应地，它对 $W$ 方是最差的稳定匹配。

## 稳定匹配多面体

令 $x_{ij}$ 表示 $m_i$ 与 $w_j$ 的匹配权重。记

$$
W_i^-(j)=\{k:w_j\succ_i w_k\},
\qquad
M_j^-(i)=\{k:m_i\succ_j m_k\},
$$

即双方眼中比当前对象更差的人。稳定匹配的示性向量满足

$$
\begin{aligned}
&\sum_jx_{ij}=1,\qquad \sum_ix_{ij}=1,\qquad x_{ij}\ge0,\\
&x_{ij}+\sum_{k\in W_i^-(j)}x_{ik}
+\sum_{k\in M_j^-(i)}x_{kj}\le1,
\qquad \forall i,j.
\end{aligned}
\tag{SM}
$$

最后一组不等式表达稳定性：若 $m_i$ 被分配给比 $w_j$ 更差的人，$w_j$ 就不能也被分配给比 $m_i$ 更差的人。

{{< math-block type="theorem" title="稳定匹配多面体的整数性" label="thm-stable-marriage-polytope" >}}
系统 $(SM)$ 描述的多面体等于所有稳定匹配示性向量的凸包。
{{< /math-block >}}

{{< math-block type="proof" >}}
先验证每个稳定匹配的示性向量均满足 $(SM)$。若 $x_{ij}=1$，同行同列其余变量为零；若 $x_{ij}=0$，而前两个求和中同时各有一项为 $1$，则 $m_i$ 与 $w_j$ 都被分配给比对方更差的人，$(m_i,w_j)$ 会成为阻挡对。因此不等式有效。

反过来任取 $(SM)$ 的可行点 $x$。记

$$
A_{ij}=\sum_{k:w_k\succ_i w_j}x_{ik},
\qquad
B_{ij}=\sum_{k:m_k\succ_j m_i}x_{kj},
$$

即双方分配给“比对方更好的人”的总权重。利用行列和为 $1$，$(SM)$ 的稳定性不等式等价于

$$
A_{ij}+B_{ij}+x_{ij}\ge1.
\tag{1}
$$

对每一行按偏好顺序展开交叉项，可得

$$
\sum_{i,j}x_{ij}A_{ij}
=\frac12\left(n-\sum_{i,j}x_{ij}^2\right).
$$

对每一列同理，$\sum_{i,j}x_{ij}B_{ij}$ 也等于右侧。因此

$$
\sum_{i,j}x_{ij}
\bigl(A_{ij}+B_{ij}+x_{ij}-1\bigr)=0.
$$

其中每一项都非负，所以只要 $x_{ij}>0$，式 $(1)$ 必须取等号。

现在构造一个随机匹配。对每个 $m_i$，按他从最喜欢到最不喜欢的顺序，把 $[0,1)$ 划分成长度分别为 $x_{ij}$ 的区间；边 $(i,j)$ 对应的区间为

$$
I^M_{ij}=[A_{ij},A_{ij}+x_{ij}).
$$

对每个 $w_j$，反过来按她从最不喜欢到最喜欢的顺序划分。令

$$
C_{ij}=\sum_{k:m_i\succ_j m_k}x_{kj}
=1-B_{ij}-x_{ij},
$$

则边 $(i,j)$ 对应 $I^W_{ij}=[C_{ij},C_{ij}+x_{ij})$。当 $x_{ij}>0$ 时，前面的取等关系给出 $C_{ij}=A_{ij}$，故

$$
I^M_{ij}=I^W_{ij}.
$$

从 $[0,1)$ 中均匀抽取一个不在区间端点上的数 $U$，并在 $U\in I^M_{ij}$ 时匹配 $m_i$ 与 $w_j$。每位男性的区间构成一个分割，所以他恰好匹配一人；相同区间也出现在女性一侧，而每位女性的区间同样构成分割，所以没有两位男性匹配同一位女性。由两侧人数相同，所得匹配是完美匹配。

它还是稳定的。若 $(m_i,w_j)$ 是阻挡对，设 $m_i$ 实际匹配到比 $w_j$ 更差的女性，则在男性从优到劣的区间顺序中

$$
U\ge A_{ij}+x_{ij}.
$$

而 $w_j$ 实际匹配到比 $m_i$ 更差的男性，在女性从劣到优的区间顺序中

$$
U<C_{ij}=1-B_{ij}-x_{ij}.
$$

但式 $(1)$ 给出 $C_{ij}\le A_{ij}$，两式矛盾。因此随机生成的匹配稳定。

最后，边 $(i,j)$ 被选中的概率正是区间长度 $x_{ij}$。若随机匹配的示性向量为 $\chi^M$，则

$$
x=\mathbb E[\chi^M].
$$

随机过程只会产生有限多个稳定匹配，所以上式就是稳定匹配示性向量的一个凸组合。于是 $(SM)$ 中每个点都属于稳定匹配凸包，结论成立。
{{< /math-block >}}

这里的整数性比普通二分图匹配更精细：它不仅来自行列和结构，还依赖严格偏好诱导的稳定性不等式。若允许并列偏好或改变稳定性的定义，多面体描述也需要相应调整。
