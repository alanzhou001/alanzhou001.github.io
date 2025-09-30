---
title: 拓扑基
description: 补充映射相关性质，介绍拓扑基相关，定理参照雷逢春《基础拓扑学与应用》
slug: topol-2
date: 2025-09-30 12:31:00+0800
math: true
image: cover.png
categories:
    - Math
tags:
    - Topology
    - notes
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

## 拓扑基(Basis)

{{< math-block type="definition" title="拓扑基" label="basis">}}

对于一个非空集合 $X$，**拓扑基**（或简称**基**）$\mathcal{B}$ 是 $X$ 的幂集 $\mathcal{P}(X)$ 的一个子集，满足以下两个条件：

1. **覆盖条件（Covering Condition）**：
    $\mathcal{B}$ 中的元素的并集必须覆盖整个集合 $X$。换句话说，对于 $X$ 中的任意一点 $x$，**存在** $\mathcal{B}$ 中的一个集合 $B$，使得 $x \in B$。
    $$\bigcup_{B \in \mathcal{B}} B = X$$

2. **交集条件（Intersection Condition）**：
    如果 $B_1$ 和 $B_2$ 是 $\mathcal{B}$ 中的任意两个元素，并且它们的交集 $B_1 \cap B_2$ 不为空，那么对于交集中的任意一点 $x$，**存在** $\mathcal{B}$ 中的第三个元素 $B_3$，使得 $x \in B_3$ 且 $B_3$ 包含于 $B_1 \cap B_2$。
    $$\forall B_1, B_2 \in \mathcal{B}, \forall x \in B_1 \cap B_2, \exists B_3 \in \mathcal{B} \text{ 使得 } x \in B_3 \subseteq B_1 \cap B_2$$

{{< /math-block >}}

如果一个集合族$\mathcal{B}$满足[上述条件](#basis)，则称其为一个**基**，基$\mathcal{B}$生成的拓扑 $\mathcal{T}$ 定义为：

$\mathcal{T}$ 中的一个子集 $U \subseteq X$ 是**开集**，当且仅当它是 $\mathcal{B}$ 中一些元素的**并集**。

$$\mathcal{T} = \left\{ \bigcup_{i \in I} B_i \mid B_i \in \mathcal{B}, I \text{ 为任意指标集} \right\}$$

{{< math-block type="theorem" title="定理1.1.3" label="lemma1.1.3">}}

设$X$为非空集合，$\mathcal{T}_{\mathcal{B}}$是由$X$上的一个拓扑基$\mathcal{B}$生成的拓扑，则$U\subset X$是这个拓扑空间中的开集当且仅当对任意$x\in U$，存在$B_x\in \mathcal{B}$，使得$x\in B_X \subset U$

{{< /math-block >}}

{{< math-block type="proof">}}

第一部分：证明 $1 \implies 2$

（如果 $U$ 是开集，则对 $U$ 中的每一点，存在一个基元素包含该点并包含于 $U$。）

**假设** $U \in \mathcal{T}_{\mathcal{B}}$，即 $U$ 是开集。

根据基 $\mathcal{B}$ **生成拓扑** $\mathcal{T}_{\mathcal{B}}$ 的定义，集合 $U$ 必须是 $\mathcal{B}$ 中一些元素的并集。
    $$\exists I \text{ (指标集) } \text{ 和 } \{B_i\}_{i \in I} \subset \mathcal{B} \text{ 使得 } U = \bigcup_{i \in I} B_i$$

取 $U$ 中任意一点 $x$，$x \in U$。

由于 $x \in U$ 且 $U = \bigcup_{i \in I} B_i$，所以 $x$ 至少属于这个并集中的一个元素。

因此，**存在**某个指标 $j \in I$，使得 $x \in B_j$。

令 $B_x = B_j$。则 $B_x \in \mathcal{B}$（$B_j$ 取自 $\mathcal{B}$），且 $x \in B_x$。

又因为 $B_x = B_j$ 是形成 $U$ 的并集中的一个元素，所以 $B_x \subset \bigcup_{i \in I} B_i = U$。

综上，找到了一个 $B_x \in \mathcal{B}$ 使得 $x \in B_x \subset U$。

由于 $x$ 是 $U$ 中的任意一点，结论成立。

---

第二部分：证明 $2 \implies 1$

（如果对 $U$ 中的每一点，都存在一个基元素包含该点并包含于 $U$，则 $U$ 是开集。）

**假设** 对任意 $x \in U$，存在 $B_x \in \mathcal{B}$，使得 $x \in B_x \subset U$。

证明 $U$ 是 $\mathcal{B}$ 中元素的并集。

考虑所有满足上述条件的 $B_x$ 的集合族 $\{B_x\}_{x \in U}$，并考察它们的并集 $V$:
    $$V = \bigcup_{x \in U} B_x$$

要证 $U = V$。
    - **证明 $U \subset V$：**
        对于 $U$ 中的任意一点 $y$，根据假设，存在 $B_y \in \mathcal{B}$ 使得 $y \in B_y$。
        由于 $B_y$ 是并集 $V = \bigcup_{x \in U} B_x$ 中的一个元素，所以 $y \in V$。
        因此，$U \subset V$。
    - **证明 $V \subset U$：**
        对于并集 $V$ 中的任意一点 $z$，根据 $V$ 的定义，它必然属于某个 $B_{x'}$，其中 $x' \in U$。
        即 $z \in B_{x'}$。
        根据假设，每一个 $B_x$ 都满足 $B_x \subset U$。所以 $B_{x'} \subset U$。
        因此，$z \in U$。
        所以，$V \subset U$。

由于 $U \subset V$ 且 $V \subset U$，所以 $U = V$。

因此，$U = \bigcup_{x \in U} B_x$，即 $U$ 是 $\mathcal{B}$ 中一些元素的并集。

根据基 $\mathcal{B}$ 生成的拓扑 $\mathcal{T}_{\mathcal{B}}$ 的定义，凡是 $\mathcal{B}$ 中元素的并集都是开集。

所以 $U \in \mathcal{T}_{\mathcal{B}}$，即 $U$ 是开集。

综上，条件 $1$ 和条件 $2$ 相互蕴含，因此它们等价，命题得证。

{{< /math-block >}}

{{< math-block type="theorem" title="定理1.1.4" label="lemma1.1.4">}}

设$(X,\mathcal{T})$为一个拓扑空间，$\mathcal{B} \subset \mathcal{T}$，则$\mathcal{B}$是生成拓扑 $\mathcal{T}$的一个拓扑基当且仅当

$$
    & (1) \quad X = \bigcup_{B\in\mathcal{B}}B \\
    & (2) \quad \text{对于 } U\in\mathcal{T} \text{ 和任意 } x\in U \text{，存在 } B_x\in \mathcal{B} \text{，使得 } x\in B_x \subset U.
$$

{{< /math-block >}}

[定理1.1.3](#lemma1.1.3)描述由$X$上的一个拓扑基生成的拓扑中开集的特征；

[定理1.1.4](#lemma1.1.4)，**给定**一个开集族$\mathcal{B}$和一个拓扑$\mathcal{T}$，判定$\mathcal{B}$是$\mathcal{T}$的一个拓扑基.

* 注：验证拓扑基用[定义](#basis)，分别验证**覆盖条件**和**交集条件**.

## 拓扑子空间(subspace)

(又称作诱导拓扑，induced topology)

引例：$(X, \mathcal{T})$是一个拓扑空间. $A \subset X$，$\mathcal{T}_A:=\{U \cap A | U \in \mathcal{T} \}$，$\mathcal{T}_A$是$A$上的拓扑.

{{< math-block type="proof" >}}

$$
    & (i) \phi \in \mathcal{T}_A, A=X \cap A \in \mathcal{T}_A
    & (ii) U_{\lambda} \cap A, \lambda \in \Lambda, U_{\lambda} \in \mathcal{T}. \\
    \bigcup_{\lambda \in \Lambda}(U_{\lambda} \cap A) =(\bigcup_{\lambda \in \Lambda}U_{\lambda})\cap A \in \mathcal{T}_A, since \bigcup_{\lambda \in \Lambda}U_{\lambda} \in \mathcal{T}. 
    & (iii) (U_1 \cap A) \cap (U_2 \cap A) = (U_1 \cap U_2) \cap A \in \mathcal{T}_A, U_1, U_2 \in \mathcal{T}. 
$$

{{< /math-block >}}

{{< math-block type="definition" title="拓扑子空间" label="subspace">}}

称$\mathcal{T}_Y$为子空间拓扑，$(Y, \mathcal{T}_Y)$为拓扑空间$X$的子空间. 若$V \subset Y$，$V \in \mathcal{T}_Y$，则称$V$在$Y$中是开的.

{{< /math-block >}}

{{< math-block type="theorem" title="定理1.2.6" label="subspace-gen">}}

设 $\mathcal{B}$ 为拓扑空间 $(X, \mathcal{T})$ 的一个基，$Y \subset X$，则
$$ \mathcal{B}_Y = \{ B \cap Y | B \in \mathcal{B} \} $$
是$Y$上子空间拓扑$\mathcal{T}_Y$的一个基.

{{< /math-block >}}

{{< math-block type="proof" >}}

$\forall$ 开集 $V \in Y$,  $\exist$ 开集 $U \in X$, 使得 $V=U \cap Y$. $\mathcal{B}$ 为拓扑空间 $(X, \mathcal{T})$ 的一个基, $\exist \mathcal{B}_U \subset \mathcal{B}$, $s.t.$ $U = \bigcup_{B \in \mathcal{B}_U}$. 因此
$$ V = (\bigcup_{B \in \mathcal{B}_U} B) \cap Y = \bigcuo_{B \in \mathcal{B}_U} (B \cap Y) $$.

{{< /math-block >}}

一个~~有趣~~有用的Lemma：

{{< math-block type="theorem" title="子空间拓扑的传递性" >}}

设 $(X, \mathcal{T})$ 是一个拓扑空间，且 $B \subset A \subset X$。
设 $(A, \mathcal{T}_A)$ 和 $(B, \mathcal{T}_B)$ 是 $(X, \mathcal{T})$ 的子空间，并设 $(B, (\mathcal{T}_A)_B)$ 是 $(A, \mathcal{T}_A)$ 的子空间。
则 $(\mathcal{T}_A)_B = \mathcal{T}_B$。（即子空间拓扑具有传递性）。

{{< /math-block >}}

{{< math-block type="proof" >}}

$\subset$ $:$ ($\mathcal{T}_B$ 包含 $(\mathcal{T}_A)_B$)
    任取 $U \in (\mathcal{T}_A)_B$，则存在一个 $A$ 中的开集 $U_1 \in \mathcal{T}_A$，使得 $U = U_1 \cap B$。
    由于 $U_1 \in \mathcal{T}_A$ 是 $A$ 中的开集，故存在一个 $X$ 中的开集 $U_2 \in \mathcal{T}$，使得 $U_1 = U_2 \cap A$。
    因此，
    $$U = (U_2 \cap A) \cap B$$
    由于 $B \subset A$，根据集合论的结合律和幂等律，有 $A \cap B = B$。
    $$U = U_2 \cap (A \cap B) = U_2 \cap B$$
    因为 $U_2 \in \mathcal{T}$ 是 $X$ 中的开集，所以 $U = U_2 \cap B$ 表明 $U$ 是 $B$ 中相对于 $X$ 拓扑 $\mathcal{T}$ 的开集。
    因此，$U \in \mathcal{T}_B$。

$\supset$ $:$ ( $(\mathcal{T}_A)_B$ 包含 $\mathcal{T}_B$)
    任取 $U \in \mathcal{T}_B$，则存在一个 $X$ 中的开集 $U_2 \in \mathcal{T}$，使得 $U = U_2 \cap B$。
    令 $U_1 = U_2 \cap A$。由于 $U_2 \in \mathcal{T}$，根据子空间拓扑的定义，我们有 $U_1 \in \mathcal{T}_A$。
    现在，将 $U$ 表示为 $U_1$ 与 $B$ 的交集：
    $$U = U_2 \cap B$$
    再次利用 $B \subset A$ 推出 $B = A \cap B$：
    $$U = U_2 \cap (A \cap B) = (U_2 \cap A) \cap B$$
    代入 $U_1$：
    $$U = U_1 \cap B$$
    因为 $U_1 \in \mathcal{T}_A$，所以 $U = U_1 \cap B$ 表明 $U$ 是 $B$ 中相对于 $A$ 拓扑 $\mathcal{T}_A$ 的开集。
    因此，$U \in (\mathcal{T}_A)_B$

综合 (1) 和 (2)，得证 $(\mathcal{T}_A)_B = \mathcal{T}_B$。

{{< /math-block >}}

## 乘积空间(Product space)

引例：设 $(X_1, \mathcal{T}_1)$ 和 $(X_2, \mathcal{T}_2)$ 是两个拓扑空间， 
$$ \mathcal{B} = \{ U \times V | U \in \mathcal{T}_1, V \in \mathcal{T}_2 \}.　$$
则 $\mathcal{B}$ 是 $X_1 \times X_2$ 上的一个拓扑基. 

证明略，逐个验证[两个条件](#basis)即可.

{{< math-block type="definition" title="乘积空间" label="product">}}

设 $(X_1, \mathcal{T}_1)$ 和 $(X_2, \mathcal{T}_2)$ 是两个拓扑空间, 称
$$ \mathcal{B} = \{ U \times V | U \in \mathcal{T}_1, V \in \mathcal{T}_2 \}　$$
所生成的$X_1 \times X_2$ 的拓扑 $\mathcal{T}$ 为\textbf{乘积拓扑}，称 $(X_1 \times X_2, \mathcal{T})$ 为 $(X_1, \mathcal{T}_1)$ 和 $(X_2, \mathcal{T}_2)$ 的 \textbf{乘积拓扑空间}，简称为$(X_1, \mathcal{T}_1)$ 和 $(X_2, \mathcal{T}_2)$的 \textbf{积空间}.

{{< /math-block >}}

$X$, $Y$ 是两个拓扑空间，$A \subset X$，$B \subset Y$，则$A \times B$在$X \times Y$上的诱导拓扑与$A \times B$的乘积拓扑等价。

## Hausdoff

{{< math-block type="definition" title="Hausdoff性质" label="hausdoff">}}

设 $(X, \mathcal{T})$ 是一个拓扑空间。如果对于 $X$ 中的\textbf{任意两个不同的点} $x$ 和 $y$ (即 $x \neq y$)，都存在一个开集 $U$ 包含 $x$，以及一个开集 $V$ 包含 $y$，使得这两个开集\textbf{不相交}，则称 $(X, \mathcal{T})$ 是一个 Hausdorff 空间.

符号表示为：
$$
\forall x, y \in X, \quad x \neq y \implies \exists U \in \mathcal{T}, \exists V \in \mathcal{T} \text{ 使得 } \left\{
\begin{array}{l}
x \in U \\
y \in V \\
U \cap V = \emptyset
\end{array}
\right.
$$

{{< /math-block >}}

**性质**：如果一个空间是Hausdoff的，则它的所有单点集都是闭的。

一些例子：

- $\mathbb{R}$上，$\mathcal{B}=\{(n,n+1)|n\in\mathbb{Z}\}$生成的拓扑不是Hausdoff的.
- $\mathbb{R}_{fc}$不是Hausdoff, 但是其上的每一个单点集都是闭的.