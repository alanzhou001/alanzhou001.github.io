---
title: K连贯性方法(Konsistency)及其在六度分隔问题中的探索性研究（待补完）
description: K连贯性方法(Konsistency)及其在六度分隔问题中探索最差情形下的六度连接。
slug: Konsistency
date: 2026-01-01 23:06:00+0800
math: true
image: cover.jpg
categories:
    - Math
tags:
    - Topology
    - Data Structure
    - Math
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

封面画师：[wukloo](https://www.pixiv.net/artworks/60752234)

{{< math-block type="definition" title="定义 1（图与邻接）" >}}
设 $G=(V,E)$ 为有限简单无向图，其中 $V$ 为顶点集，$E\subseteq{{u,v}:u,v\in V, u\neq v}$ 为边集。若 ${u,v}\in E$，则称 $u$ 与 $v$ 相邻，记为$u\sim v$。
{{< /math-block >}}

------

{{< math-block type="definition" title="定义 2（闭邻域）" >}}
对任意顶点 $k\in V$，定义其闭邻域为
$$
N[k] := {k}\cup{v\in V:\ v\sim k}.
$$
{{< /math-block >}}

------

{{< math-block type="definition" title="定义 3（支配集）" >}}
集合 $K\subseteq V$ 称为图 $G$ 的一个支配集，若满足
$$
\forall v\in V,\quad \exists k\in K \text{ 使得 } v\in N[k].
$$
即，图中每一个顶点要么属于 $K$，要么与 $K$ 中的某个顶点相邻。
{{< /math-block >}}

------

{{< math-block type="definition" title="定义 4（划分）" >}}
称一族非空集合 ${S_k}_{k\in I}$ 为 $V$ 的一个划分，若满足：

1. $S_k\neq\varnothing$，对所有 $k\in I$；
2. $S_{k_1}\cap S_{k_2}=\varnothing$，对所有 $k_1\neq k_2$；
3. $\bigcup_{k\in I} S_k = V$。
{{< /math-block >}}

------

{{< math-block type="definition" title="定义 5（k-星型中心）" >}}
设 $S\subseteq V$ 为非空集合。若存在 $k\in S$ 使得
$$
\forall v\in S\setminus{k},\quad k\sim v,
$$
则称 k 为集合 S 的一个 **k-星型中心**。
{{< /math-block >}}

------

{{< math-block type="theorem" title="定理 1（由支配集诱导的 k-中心星型划分）" >}}
设 $G=(V,E)$ 为有限简单无向图，且 $K\subseteq V$ 为其一个支配集。则存在一个映射
$$
f:V\to K
$$
满足
$$
\forall v\in V,\quad v\in N[f(v)].
$$
令
$$
S_k := {v\in V:\ f(v)=k},\qquad k\in K,
$$
并定义
$$
K' := {k\in K:\ S_k\neq\varnothing}.
$$
则集合族 ${S_k}_{k\in K'}$ 构成 $V$ 的一个划分，且对每个 $k\in K'$，顶点 $k$ 是子集 $S_k$ 的 k-星型中心。
{{< /math-block >}}

------

{{< math-block type="proof" >}}
由于 $K$ 是 $G$ 的支配集，按定义对任意 $v\in V$，存在至少一个 $k\in K$ 使得 $v\in N[k]$。据此，对每个 $v\in V$ 任取一个满足上述条件的顶点 $k\in K$，并定义映射
$$
f(v)=k.
$$
由构造立即可得
$$
\forall v\in V,\quad v\in N[f(v)].
$$

接下来验证集合族 ${S_k}_{k\in K'}$ 的性质。

首先，对任意$v\in V$，由 $f(v)\in K$ 且 $v\in S_{f(v)}$，可得
$$
V=\bigcup_{k\in K}S_k=\bigcup_{k\in K'}S_k,
$$
从而覆盖性成立。

其次，由于 $f$ 为函数，对任意不同的 $k_1,k_2\in K$，有
$$
S_{k_1}\cap S_{k_2}
={v\in V:\ f(v)=k_1 \text{ 且 } f(v)=k_2}
=\varnothing,
$$
故集合两两不交。

再次，由 $K'$ 的定义可知，对所有$k\in K'$，均有$S_k\neq\varnothing$。因此 ${S_k}_{k\in K'}$ 构成 $V$ 的一个划分。

最后，取任意 $k\in K'$ 及任意$v\in S_k$。由 $S_k$ 的定义，有 $f(v)=k$。结合映射 $f$ 的构造性质，得
$$
v\in N[k],
$$
即要么 $v=k$，要么 $v\sim k$。因此，对所有$v\in S_k\setminus{k}$，均有 $k\sim v$，从而 $k$ 为 $S_k$ 的 k-星型中心。

定理得证。
{{< /math-block >}}

---

## Min–max 星型中心划分的优化建模

### 1. 预备定义与符号

设 \(G=(V,E)\) 为有限简单无向图，\(|V|=n\)。定义邻接指示函数
\[
a_{vk} =
\begin{cases}
1, & v = k \text{ 或 } \{v,k\} \in E, \\
0, & \text{否则}.
\end{cases}
\]
注意 \(a_{vk}=1\) 当且仅当 \(v \in N[k]\)，即顶点 \(v\) 与顶点 \(k\) 至多一跳可达（允许 \(v=k\)）。

称顶点 \(k\) 为集合 \(S \subseteq V\) 的 **\(k\)-星型中心**，若对任意 \(v \in S \setminus \{k\}\)，均有 \(\{v,k\} \in E\)。等价地，
\[
\forall v \in S,\quad a_{vk}=1.
\]

---

### 2. Min–max 优化问题的原始形式

给定一个正整数 \(m\)（中心数或子群体数的预算），考虑如下问题：

> **问题 \((\mathcal{P}_m)\)：Min–max 星型中心划分**
\[
\min_{\{S_k\},\,K}\ \max_{k \in K} |S_k|
\]
满足
\[
\begin{aligned}
&K \subseteq V,\quad |K| \le m, \\
&\{S_k\}_{k \in K} \text{ 构成 } V \text{ 的一个划分}, \\
&k \in S_k \quad \forall k \in K, \\
&S_k \subseteq N[k] \quad \forall k \in K.
\end{aligned}
\]

其中约束 \(S_k \subseteq N[k]\) 保证每个子群体 \(S_k\) 以 \(k\) 为中心，且所有成员与 \(k\) 至多一跳相邻。

> **说明**  
> 若不对 \(|K|\) 加以限制，则可取 \(K=V\)、\(S_k=\{k\}\)，使目标值恒为 1，从而问题退化。因此中心数预算 \(m\) 是获得非平凡解的必要条件。

---

### 3. 0–1 变量的 Min–max 指派模型

引入如下决策变量：
- \(y_k \in \{0,1\}\)：若 \(y_k=1\)，则选择顶点 \(k\) 作为某一子群体的中心；
- \(x_{vk} \in \{0,1\}\)：若 \(x_{vk}=1\)，则将顶点 \(v\) 分配给中心 \(k\)。

定义中心 \(k\) 的群体规模（负载）为
\[
L_k(x) := \sum_{v \in V} x_{vk}.
\]

则问题 \((\mathcal{P}_m)\) 等价地可表述为如下 min–max 整数优化问题：

> **问题 \((\mathcal{IP}_m)\)：Min–max 星型指派模型**
\[
\min_{x,y}\ \max_{k \in V} L_k(x)
\]
满足
\[
\begin{aligned}
&\sum_{k \in V} x_{vk} = 1 
&& \forall v \in V 
&& \text{(每个顶点恰分配给一个中心)} \\
&x_{vk} \le a_{vk} 
&& \forall v,k \in V 
&& \text{(一跳可达 / 星型约束)} \\
&x_{vk} \le y_k 
&& \forall v,k \in V 
&& \text{(只能分配给被选中的中心)} \\
&\sum_{k \in V} y_k \le m 
&& 
&& \text{(中心数预算)} \\
&x_{kk} = y_k 
&& \forall k \in V 
&& \text{(选中心则中心属于其群体)} \\
&x_{vk} \in \{0,1\},\ y_k \in \{0,1\} 
&& \forall v,k \in V.
\end{aligned}
\]

在该模型中，对每个满足 \(y_k=1\) 的顶点 \(k\)，集合
\[
S_k := \{v \in V : x_{vk}=1\}
\]
构成一个非空子群体，且由约束 \(x_{vk} \le a_{vk}\) 可知 \(S_k \subseteq N[k]\)，因此 \(k\) 是 \(S_k\) 的 \(k\)-星型中心。由 \(\sum_k x_{vk}=1\) 可知这些子群体构成 \(V\) 的一个划分（忽略空集）。

---

### 4. Min–max 的标准线性化形式

引入一个标量上界变量 \(T\) 将 min–max 目标转化为等价形式：

**等价形式 \((\mathcal{IP}_m^T)\)**
\[
\min_{x,y,T}\ T
\]
满足问题 \((\mathcal{IP}_m)\) 的全部约束，并额外加入
\[
\sum_{v \in V} x_{vk} \le T \quad \forall k \in V.
\]

在最优解处，有
\[
T^\star = \min_{x,y}\ \max_{k \in V} L_k(x),
\]
从而该模型与原 min–max 目标等价。

---

## 基于小世界模型的 \(k\)-方法六度分隔定理推导

本节在前述 **定义 1–5、定理 1** 以及 **Min–max 星型中心模型** 的基础上，  
**保持此前给出的足够条件不变**，在 **Newman–Watts 小世界模型** 下，  
以**完全展开的概率不等式（Chernoff 界 + 并集界）**形式，给出“六度分隔”的严格推导。

---

## Newman–Watts 小世界模型

设顶点集
\[
V=\{0,1,\dots,n-1\}
\]
按模 \(n\) 排列成环，定义环距离
\[
\mathrm{dist}_{\mathrm{ring}}(u,v)=\min\{|u-v|,\,n-|u-v|\}.
\]

给定参数 \(r\in\mathbb{N}\)、\(p\in(0,1)\)，随机图
\[
G\sim \mathrm{NW}(n,r,p)
\]
按如下规则生成：

1. **局部边（确定性）**  
   若 \(\mathrm{dist}_{\mathrm{ring}}(u,v)\le r\) 且 \(u\neq v\)，则加入边 \(\{u,v\}\)；
   此时每个顶点局部度为 \(2r\)。

2. **长程边（随机）**  
   对所有尚未相连的顶点对 \(\{u,v\}\)，独立地以概率 \(p\) 加入边。

---

## 第一层 \(k\)：确定性星型划分

设
\[
s := 2r+1, \qquad m := \left\lceil \frac{n}{s} \right\rceil .
\]

将环按顺序划分为 \(m\) 个连续区块
\[
B_1,\dots,B_m,
\quad |B_i|\le s.
\]
在每个区块 \(B_i\) 中选取一个中心 \(k_i\)，定义
\[
K_1 := \{k_1,\dots,k_m\}.
\]

{{< math-block type="lemma" title="引理 7.1（块内星型支配）" >}}
对任意 \(i\)，有
\[
B_i \subseteq N_G[k_i].
\]
{{< /math-block >}}

{{< math-block type="proof" >}}
由于 \(|B_i|\le 2r+1\)，且 \(k_i\) 取块中点，任意 \(v\in B_i\) 满足
\[
\mathrm{dist}_{\mathrm{ring}}(v,k_i)\le r,
\]
从而 \(\{v,k_i\}\in E\)。证毕。
{{< /math-block >}}

因此
\[
\forall v\in V,\quad \mathrm{dist}_G(v,K_1)\le 1.
\]

---

## 群体图的构造与边概率下界

定义 **群体图**
\[
H=(V_H,E_H),
\quad V_H := K_1.
\]

若原图中存在 \(u\in B_i, v\in B_j\) 使得 \(\{u,v\}\in E(G)\)，则在 \(H\) 中加入边 \(\{k_i,k_j\}\)。

---

{{< math-block type="lemma" title="引理 7.2（群体图边概率下界）" >}}
设
\[
p' := 1-(1-p)^{(s-1)^2}.
\]
则对任意 \(i\neq j\)，有
\[
\mathbb{P}\big(\{k_i,k_j\}\in E_H\big) \ge p'.
\]
{{< /math-block >}}

{{< math-block type="proof" >}}
区块 \(B_i,B_j\) 至少包含 \((s-1)^2\) 对"非局部相邻"的顶点对。  
每一对以概率 \(p\) 独立连边，因此
\[
\mathbb{P}(\text{无任何跨块边})
=(1-p)^{|B_i||B_j|}
\le (1-p)^{(s-1)^2}.
\]
取补事件即得结论。
{{< /math-block >}}

---

## 群体图上的扩张性分析

以下分析在 **Erdős–Rényi 下界模型**
\[
\widetilde H \sim G(m,p')
\]
中进行；由于“直径 \(\le 4\)”是单调递增事件，  
由耦合原理可将结论转移到真实群体图 \(H\)。

---

### 度集中性（Chernoff 界）

令
\[
d := (m-1)p'.
\]

对任意固定顶点 \(x\in V(\widetilde H)\)，其度
\[
\deg(x)\sim \mathrm{Bin}(m-1,p').
\]

对任意 \(0<\delta<1\)，Chernoff 界给出
\[
\mathbb{P}\big(\deg(x)\le (1-\delta)d\big)
\le \exp\!\left(-\frac{\delta^2 d}{2}\right).
\]

取 \(\delta=\tfrac12\)，得
\[
\mathbb{P}\big(\deg(x)\le d/2\big)
\le \exp\!\left(-\frac{d}{8}\right).
\]

若
\[
d \ge 16\log m,
\]
则
\[
\mathbb{P}\big(\deg(x)\le d/2\big)\le m^{-2}.
\]

由并集界，
\[
\mathbb{P}\big(\exists x:\deg(x)\le d/2\big)
\le m\cdot m^{-2}=m^{-1}.
\]

**结论：** 以概率至少 \(1-m^{-1}\)，
\[
\delta(\widetilde H)\ge d/2.
\]

---

### 两步球的期望增长

固定顶点 \(x\)，在事件 \(\deg(x)\ge d/2\) 上考虑
\[
\Gamma_1(x) := \{x\}\cup N(x),
\quad |\Gamma_1(x)|\ge d/2.
\]

对任意顶点 \(y\notin \Gamma_1(x)\)，其不与 \(\Gamma_1(x)\) 中任意点相连的概率为
\[
\mathbb{P}\big(y\notin \Gamma_2(x)\mid \Gamma_1(x)\big)
=(1-p')^{|\Gamma_1(x)|}
\le \exp\!\left(-p'|\Gamma_1(x)|\right)
\le \exp\!\left(-\frac{p'd}{2}\right).
\]

因此
\[
\mathbb{E}\big[m-|\Gamma_2(x)|\mid \deg(x)\ge d/2\big]
\le m\exp\!\left(-\frac{p'd}{2}\right).
\]

---

### 两步球达到 \(m^{2/3}\) 的概率下界

设足够条件
\[
d \ge C\, m^{1/3}\log m
\quad (C>0\ \text{充分大}),
\]
注意
\[
p'd \asymp \frac{d^2}{m}.
\]

则
\[
\frac{p'd}{2}
\ge \frac{C^2}{2}\, m^{-1/3}\log^2 m.
\]

于是
\[
m\exp\!\left(-\frac{p'd}{2}\right)
\le m\exp\!\left(-\tfrac{C^2}{2}m^{-1/3}\log^2 m\right)
\le m^{-10}
\]
当 \(C\) 充分大时成立。

由 Markov 不等式，
\[
\mathbb{P}\big(|\Gamma_2(x)|\le m^{2/3}\big)
\le \mathbb{P}\big(m-|\Gamma_2(x)|\ge m-m^{2/3}\big)
\le \frac{m^{-10}}{m^{1/3}}
\le m^{-9}.
\]

---

### 第三步覆盖全图

在事件 \(|\Gamma_2(x)|\ge m^{2/3}\) 上，对任意顶点 \(z\notin \Gamma_2(x)\)，
\[
\mathbb{P}\big(z\notin \Gamma_3(x)\big)
=(1-p')^{|\Gamma_2(x)|}
\le \exp\!\left(-p'm^{2/3}\right).
\]

而
\[
p'm^{2/3}
\asymp \frac{d}{m}\cdot m^{2/3}
=d\,m^{-1/3}
\ge C\log m.
\]

因此
\[
\mathbb{P}\big(z\notin \Gamma_3(x)\big)\le m^{-C}.
\]

再用并集界：
\[
\mathbb{P}\big(\Gamma_3(x)\neq V\big)
\le m\cdot m^{-C}
= m^{1-C}.
\]

取 \(C\ge 12\)，得
\[
\mathbb{P}\big(\Gamma_3(x)=V\big)\ge 1-m^{-11}.
\]

---

### 群体图直径界

对所有 \(x\in V(\widetilde H)\) 再次使用并集界，
\[
\mathbb{P}\big(\exists x:\Gamma_3(x)\neq V\big)
\le m\cdot m^{-11}
= m^{-10}.
\]

因此，以概率至少 \(1-m^{-10}\)，
\[
\operatorname{rad}(\widetilde H)\le 3
\quad\Rightarrow\quad
\operatorname{diam}(\widetilde H)\le 6.
\]

进一步，采用“两点各自两步球相交”的标准估计（同上步骤 8.3–8.4），
可将直径改进为
\[
\operatorname{diam}(\widetilde H)\le 4
\]
仍以多项式高概率成立。

---

## 回推到原图：六度分隔

由于
\[
\forall v\in V,\quad \mathrm{dist}_G(v,K_1)\le 1,
\]
且以高概率
\[
\operatorname{diam}(H)\le 4,
\]
对任意 \(u,v\in V\)，记其块中心为 \(k(u),k(v)\)，则
\[
\mathrm{dist}_G(u,v)
\le
\mathrm{dist}_G(u,k(u))
+\mathrm{dist}_H(k(u),k(v))
+\mathrm{dist}_G(k(v),v)
\le 1+4+1=6.
\]

---

{{< math-block type="theorem" title="定理（小世界模型中的六度分隔，k-收缩证明）" >}}
设
\[
G\sim \mathrm{NW}(n,r,p),
\quad s=2r+1,\quad m=\left\lceil\frac{n}{s}\right\rceil,
\quad p'=1-(1-p)^{(s-1)^2}.
\]
若存在常数 \(C>0\) 使得
\[
(m-1)p' \ge C\, m^{1/3}\log m,
\]
则存在常数 \(c>0\)，使得
\[
\mathbb{P}\big(\operatorname{diam}(G)\le 6\big)
\ge 1-m^{-c}.
\]

等价地：在该参数区间内，以高概率任意两点之间存在一条长度不超过 \(6\) 的路径，即中间 \(k\)-节点链条长度最多为 \(5\)。
{{< /math-block >}}

------

## 讨论与局限性（Discussion and Limitations）

本文所得到的充分条件
$$
(m-1)p' \ge Cm^{1/3}\log m
$$
在定量意义上是较强的，尤其是在将其还原为 Newman–Watts 小世界模型的原始参数 ((n,r,p)) 后可以看到，该条件对局部连接半径 (r) 与长程边概率 (p) 的协同作用提出了较高要求。与已有文献中关于小世界网络“平均距离”或“典型节点对距离”为 (O(\log n)) 的结果相比，本文的条件并非最优，且在某些参数区间内明显偏保守。

然而，这种条件的“偏强”本质上源于本文目标命题的严格性。本文所证明的并非平均意义或概率意义下的距离界，而是以高概率成立的**全局直径上界**，即保证任意两点之间的最短路径长度不超过 6。众所周知，相较于平均距离或随机选点对的距离估计，直径这样的最坏情形指标通常需要显著更强的结构假设，因此该结果在逻辑上是合理且一致的。

从方法论角度看，本文的主要优势在于其结构化与可解释性。证明全过程严格基于 (k)-星型中心的支配划分与图收缩操作，避免了对谱方法、分支过程近似或渐近距离公式的依赖。每一层收缩都对应一个清晰的网络操作：局部星型支配、群体级压缩以及在压缩图上的快速扩张。这种分层机制直观地揭示了小世界网络中“局部高聚类 + 稀疏长程随机边”如何通过层级化结构转化为全局的短路径性质。

此外，(k)-收缩框架与本文给出的 min–max 优化模型在形式上高度一致，使得该理论不仅具有概率论意义，也具备潜在的算法与优化解释。这种统一视角为网络分层建模、群体抽象、以及大规模网络的多尺度分析提供了新的可能性。

需要强调的是，本文给出的参数阈值应被视为一种“可证明的充分条件”，而非刻画六度分隔现象的精确边界。通过更精细的概率估计、更弱的目标结论（例如只约束典型距离而非直径），或在其他小世界模型与度分布假设下，本文所采用的 (k)-中心收缩思路仍有较大的改进空间。因此，本文的结果更适合作为一种概念性与方法论上的证明范式，展示六度分隔现象如何在明确的层级支配结构中被严格推出，而非对现实社会网络的参数进行最终刻画。

尽管**支配集**、**图收缩（graph coarsening）**以及**小世界网络的距离性质分析**均已在现有文献中得到广泛研究，但**通过反复的星型中心支配与收缩来推导统一的常数级直径上界**这一做法，在现有研究中尚未出现。本文提出的 **(k)-收缩（(k)-contraction）框架**可被视为一种统一性的视角，它将**基于支配的覆盖结构**与**多层次图收缩方法**相结合，同时保持了对**路径长度的显式、可解释刻画**。
