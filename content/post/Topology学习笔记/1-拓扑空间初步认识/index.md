---
title: 拓扑空间初步认识
description: 介绍拓扑空间及拓扑空间中基本概念
slug: topol-1
date: 2025-08-29 16:00:00+0800
math: true
image: cover.png
categories:
    - Math
tags:
    - Topology
    - notes
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

笔记主要参考尤承业《基础拓扑学讲义》，为便于查找，所有定义、定理等编号与原书保持一致。

## 拓扑空间

{{< math-block type="definition" title="Definition 1.1 拓扑空间 " label="def-topol">}}

设$X$是一非空集合. $X$的一个**子集族**$\tau$称为$X$的一个**拓扑**，如果它满足

（1） $X$，$\emptyset$都包含在$ \tau $ 中；  
（2） $ \tau $ 中任意多个成员的并集仍在$ \tau $ 中；  
（3） $ \tau $ 中有限多个成员的交集仍在$ \tau $ 中.  

集合$X$和它的一个拓扑$ \tau $一起称为一个**拓扑空间**，记作$(X, \tau)$. 称$\tau $中的成员为这个拓扑空间的**开集**.

(*注*：这里定义了拓扑空间中的**开集**)

{{< /math-block >}}

定义[1.1](#def-topol)中三个条件称为**拓扑公理**. 其中（3）可等价为（3'）  
    （3'）$\tau $中两个成员的交集仍在$\tau $ 中.

证明如下：

{{< math-block type="proof">}}

“$\tau$ 对**有限个**成员的交封闭” $\Leftrightarrow$ “$\tau$ 对**任意两个**成员的交封闭”.

$\Rightarrow$ 假设 $\tau$ 中任意有限个集合的交仍在 $\tau$ 中。则特别地，任取 $U, V \in \tau$，$U \cap V$ 也是有限交，故 $U \cap V \in \tau$.

$\Leftarrow$ 反过来，假设 $\tau$ 中任意两个集合的交仍在 $\tau$ 中，即如果 $U, V \in \tau$，则 $U \cap V \in \tau$. 我们将证明 $\tau$ 对任意有限个集合的交闭.  
归纳地证明：  

当 $n = 2$ 时，结论显然成立（即假设中的条件）.

假设任意 $n$ 个开集 $U_1, \dots, U_n \in \tau$ 有 $\bigcap_{i=1}^n U_i \in \tau$.  
考虑 $n+1$ 个开集 $U_1, \dots, U_n, U_{n+1} \in \tau$. 由归纳假设，$V := \bigcap_{i=1}^n U_i \in \tau$.  
再利用两个集合的交闭性，得到：  
$$
\bigcap_{i=1}^{n+1} U_i = V \cap U_{n+1} \in \tau.
$$
因此，对任意有限个开集，其交仍在 $\tau$ 中.

由此，两者等价.

{{< /math-block >}}

- 总结：给出集合的一个拓扑即规定哪些子集是开集，同时满足三条公理。
- 一些例子：
  - $2^X$，**离散拓扑**，记作$\tau_t$；
  - $(X, \emptyset)$，**平凡拓扑**，记作$\tau_s$;
  - $X$是无穷集合，$\tau_f= \{ A^c \mid A是X的有限子集 \} \cup \{ \emptyset \} $, **余有限拓扑**；
  - $X$是不可数无穷集合，$\tau_c= \{ A^c \mid A是X的可数子集 \} \cup \{ \emptyset \} $, **余可数拓扑**；
  - $\mathbf{R}$是全体实数集，$\tau_e= \{ U \mid U是若干个开区间的并集 \} $，“若干个”可以是无穷、有限、零，**欧氏拓扑**，记作$\mathbf{E}^1=(\mathbf{R}, \tau_e)$

给出**余有限拓扑**的证明:

{{< math-block type="proof">}}

验证拓扑三公理.

(1)
由定义可知$\emptyset\in\tau$ ；  
$X\in\tau$，因为 $X^c=\emptyset\in\tau$ .

(2)
设 $U_{i, i\in I}\subseteq\tau$. 若存在 $i_0$ 使 $U_{i_0}=\emptyset$，不影响并集的开性，故不妨设对每个 $i$，$U_i\neq\emptyset$ 且 $X\setminus U_i$ 有限.
则
$$
X\setminus \bigcup_{i\in I} U_i
= \bigcap_{i\in I} (X\setminus U_i).
$$
右侧是（可能是无限个）有限集的交集. 任取 $j\in I$，有
$$
\bigcap_{i\in I} (X\setminus U_i)\ \subseteq\ X\setminus U_j,
$$
因此该交集是某个有限集的子集，从而也是有限集. 于是 $X\setminus \bigcup_{i\in I} U_i$ 有限，即 $\bigcup_{i\in I} U_i\in\tau$.

(3)
取有限个 $U_1,\dots,U_n\in\tau$. 同理有
$$
X\setminus \bigcap_{k=1}^n U_k
= \bigcup_{k=1}^n (X\setminus U_k),
$$
右侧为有限个有限集的并，仍为有限集. 故 $\bigcap_{k=1}^n U_k\in\tau$.

综上，$\tau$ 满足拓扑的三条公理，故为 $X$ 上的一个拓扑.

{{< /math-block >}}

## 度量拓扑

**回忆：** 度量空间三条性质（定义）  

- 正定性
- 对称性
- 三角不等式

{{< math-block type="definition" title="度量空间中的开球" label="circle">}}

设$(X, d)$是一个度量空间，$x_0 \in X，$\epsilon $是一正数，称$X$的子集
$$
B(x_0, \epsilon) := \{x_0\in X \mid d(x_0, x)<\epsilon \}
$$

为以$x_0$为心，$\epsilon$为半径的**球形邻域**.

{{< /math-block >}}

{{< math-block type="theorem" title="引理" label="circle-capcup">}}

$(X, d)$的任意两个球形邻域的交集是若干个球形邻域的并集.

{{< /math-block >}}

{{< math-block type="proof">}}

设$U=B(x_1, \epsilon_1)\cap B(x_2, \epsilon_2)$. $\forall x\in U$，则$\epsilon_i-d(x, x_i)>0(i=1, 2)$. 记$\epsilon_x =min\{\epsilon_1-d(x, x_1), \epsilon_2-d(x, x_2)\}$，有$B(x, \epsilon_x)\subset U$. 于是
$$
U=\bigcap_{x\in U}B(x, \epsilon_x).
$$

{{< /math-block >}}

规定$X$的子集族$\tau_d=\{U \mid U是若干个开球的并集\}$.

{{< math-block type="theorem" title="命题1.1 度量空间上的拓扑" label="measure-topol">}}

$\tau_d$是$X$上的一个拓扑.

{{< /math-block >}}

{{< math-block type="proof">}}

验证三条公理.
（1），（2）均由定义可直接验证. 下证公理（3）.

设$U_{\alpha}, U_{\beta} \in \tau_d$， $$U_{\alpha}=\bigcup_{\alpha}B(x_{\alpha}, \epsilon_{\alpha}), U_{\beta}=\bigcup_{\beta}B(x_{\beta}, \epsilon_{\beta})$$，则有

$$
\begin{align*}
U_{\alpha}\cap U_{\beta}=(\bigcup_{\alpha}B(x_{\alpha}, \epsilon_{\alpha}))\cap \bigcup_{\beta}B(x_{\beta}, \epsilon_{\beta}) \\
=\bigcup_{\alpha, \beta}(B(x_{\alpha}, \epsilon_{\alpha})\cap B(x_{\beta}, \epsilon_{\beta})).
\end{align*}
$$

由[引理](#circle-capcup), $B(x_{\alpha}, \epsilon_{\alpha})\cap B(x_{\beta}, \epsilon_{\beta}) \in \tau_d$,

因此，$U_{\alpha}\cap U_{\beta} \in \tau_d$.

{{< /math-block >}}

## 拓扑空间中的基本概念

下述概念在实分析中均出现过，替换开集概念为拓扑空间中的[开集](#def-topol)即可.

1. 闭集
2. 领域、内点和内部
3. 聚点和闭包
4. 序列收敛性

### 重要性质


{{< math-block type="theorem" title="命题1.2 拓扑空间中闭集的性质" label="close">}}

1. $X$与$\emptyset$都是闭集；
2. **任意多**个闭集的**交集**都是闭集；
3. **有限个**闭集的**并集**是闭集.

{{< /math-block >}}

{{< math-block type="theorem" title="命题1.3" label="close">}}

1. 若$A \subset B$，则$A^{\circ} \subset B^{\circ}$；
2. $A^{\circ}$是包含在$A$中所有开集的并集，是包含在$A$中的最大开集；
3. $A^{\circ}=A \iff A$是开集；
4. $(A\cap B)^{\circ}=A^{\circ}\cap B^{\circ}$
5. $(A\cup B)^{\circ} \supset A^{\circ}\cup B^{\circ}$

{{< /math-block >}}

{{< math-block type="definition" title="笛卡尔积" label="c-product">}}

$X_1 \times X_2 \times \cdots X_n:=\{(x_1, x_2, \cdots x_n) | x_i\in X_i\} $

{{< /math-block >}}

{{< math-block type="theorem" title="笛卡尔积分配律" label="c-distribute">}}

$$1. A\cup(\bigcap_{\lambda \in \Lambda}B_\lambda)= \bigcap_{\lambda \in \Lambda}(A\cup B_\lambda) \\
2. A\cap(\bigcup_{\lambda \in \Lambda}B_\lambda)= \bigcup_{\lambda \in \Lambda}(A\cap B_\lambda) \\
3. A\times(\bigcap_{\lambda \in \Lambda}B_\lambda)= \bigcap_{\lambda \in \Lambda}(A\times B_\lambda) \\
4. A\times(\bigcup_{\lambda \in \Lambda}B_\lambda)= \bigcup_{\lambda \in \Lambda}(A\times B_\lambda) \\
5. A\times(B_1 \backslash B_2)=(A\times B_1)\backslash (A\times B_2)
$$

{{< /math-block >}}

 