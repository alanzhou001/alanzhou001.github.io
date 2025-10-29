---
title: 内点、闭包、边界点
description: 介绍拓扑空间中内点、闭包、边界点概念，参考雷逢春《基础拓扑学及应用》
slug: topol-3
date: 2025-10-13 20:00:00+0800
math: true
image: cover.jpg
categories:
    - Math
tags:
    - Topology
    - notes
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

封面画师：[リース＠ついった](https://www.pixiv.net/artworks/104538476)

## 内部、闭包和边界(Interior, Closure and Boundary)

### 内部和闭包 (Interior&Closure)

{{< math-block type="definition" title="Definition 1.2.1 内部和闭包 " label="int-cl">}}

（1）设 $X$ 是一个拓扑空间，$A \subset X$ 是一个子集。$A$ 的**内部**，记为 $A^{\circ}$ 或 $\text{int}(A)$，是**包含在 $A$ 中的所有开集的并集**。

$$A^{\circ}=\bigcup_{U~is~open, U\subset A}U$$

**等价描述 (Lemma):**

点 $y \in X$ 属于 $A^{\circ}$ 当且仅当存在一个开集 $U$，使得 $y \in U \subset A$。

（2）设 $X$ 是一个拓扑空间，$A \subset X$ 是一个子集。$A$ 的**闭包**，记为 $\overline{A}$ 或 $\text{cl}(A)$，是**包含 $A$ 的所有闭集的交集**。

$$\overline{A}=\bigcap_{V~is~closed, A\subset V}V$$

**等价描述 (Lemma):**

点 $y \in X$ 属于 $\overline{A}$ 当且仅当 $y$ 的每一个邻域都与 $A$ 相交（即 $U \cap A \ne \emptyset$）。

{{< /math-block >}}

**性质 (Prop.):**

* $A^{\circ}$ 是包含在 $A$ 中的**最大的开集**。
* $A^{\circ}$ 本身是一个**开集**。
* $(A^{\circ})^{\circ}= A^{\circ}$ (内部的内部等于内部)。
* $A$ 是开集当且仅当 $A = A^{\circ}$。
* $\overline{A}$ 是包含 $A$ 的**最小的闭集**。
* $\overline{A}$ 本身是一个**闭集**。
* $\overline{\overline{A}} = \overline{A}$ (闭包的闭包等于闭包)。
* $A$ 是闭集当且仅当 $A = \overline{A}$。
* **极限点关系：** $\overline{A} = A \cup A'$，其中 $A'$ 是 $A$ 的所有**极限点**（或聚点）的集合。

{{< math-block type="theorem" title="一些有用的推论-1" >}}

设 $X$ 是一个拓扑空间，$A, B \subset X$ 是其子集。以下性质成立：

(i) 如果 $U$ 在 $X$ 中是**开集**，$U \subset A$，则 $U \subset A^{\circ}$。

(ii) 如果 $V$ 在 $X$ 中是**闭集**，$V \supset A$，则 $V \supset \overline{A}$。

(iii) $A \subset B \implies A^{\circ} \subset B^{\circ}$。

(iv) $A \subset B \implies \overline{A} \subset \overline{B}$。

(v) $A$ 是**开集** $\iff A = A^{\circ}$。

(vi) $A$ 是**闭集** $\iff A = \overline{A}$。

{{< /math-block >}}

{{< math-block type="proof" >}}

* **(iii) 的证明 (Pf.):**
    $$A^{\circ} \text{ 是开集, } A^{\circ} \subset A \subset B \xrightarrow{(\text{i})} A^{\circ} \subset B^{\circ}$$

* **(iv) 的证明 (Pf.):**
    $$\overline{B} \text{ 是闭集, } \overline{B} \supset B \supset A \xrightarrow{(\text{ii})} \overline{B} \supset \overline{A}$$

* **(v) 的证明 (Pf.):**
    $$\text{"}\implies\text{"}: \text{Since } A \text{ is open, and } A \subset A \xrightarrow{(\text{i})} A \subset A^{\circ} \text{ (且 } A^{\circ} \subset A \text{ 恒成立)}$$   $$\text{"}\impliedby\text{": } A^{\circ} \text{ is open, and } A = A^{\circ} \implies A \text{ is open. }\square$$

{{< /math-block >}}

### Remark

- $A^{\circ}$是$A$中最大的开集。
- $\overline{A}$是包含$A$的最小的闭集。

### 稠密集、可分空间与内部/闭包的等价引理

{{< math-block type="definition" title="Definition 稠密集 (Dense Set)" label="dense">}}

设 $A$ 是拓扑空间 $X$ 的一个子集。如果 $A$ 的**闭包**等于整个空间 $X$，即 $\overline{A} = X$，则称 $A$ 是 $X$ 的一个**稠密集**（dense set）。

{{< /math-block >}}

{{< math-block type="definition" title="Definition 可分空间 (Separable Space)" label="sep-space">}}

一个拓扑空间 $X$，如果它拥有一个**可数的稠密集**（countable dense subset），则称 $X$ 是一个**可分空间**（separable space）。

{{< /math-block >}}

**示例 (Eg.):**

- 在 $\mathbb{R}_{fc}$（有限补拓扑下的实数集）中，每一个**无限子集** $A$ 都是稠密集，即 $\overline{A} = \mathbb{R}$。

### 内部与闭包的等价引理

{{< math-block type="theorem" title="引理" >}}

设 $X$ 是一个拓扑空间，$A \subset X$，$y \in X$。

(i) $y \in A^{\circ} \iff$ 存在一个**开集** $U$，使得 $y \in U \subset A$。

(ii) $y \in \overline{A} \iff$ $y$ 的**每一个邻域**都与 $A$ 相交。

{{< /math-block >}}

{{< math-block type="proof" >}}

**(i) $\implies$**：$y \in A^{\circ}$ 意味着 $y$ 属于包含在 $A$ 内的所有开集的并集，故 $y$ 必属于其中某个开集 $U$ 且 $U \subset A$。

**(i) $\impliedby$**：显然 (若 $y$ 被包含在 $A$ 内的开集 $U$ 包围，则 $y$ 属于包含在 $A$ 内的最大开集 $A^{\circ}$)。

**(ii) $\implies$**：(反证法) 假设 $y \in \overline{A}$ 但存在邻域 $U$ 使得 $U \cap A = \emptyset$。则 $X-U$ 是一个包含 $A$ 的闭集，故 $\overline{A} \subset X-U$，与 $y \in \overline{A}$ 矛盾。

**(ii) $\impliedby$**：(反证法) 假设 $y \notin \overline{A}$。则存在一个包含 $A$ 的闭集 $V_0$ 且 $y \notin V_0$。令 $U = X-V_0$，则 $U$ 是 $y$ 的一个开邻域，且 $U \cap A = \emptyset$，与假设矛盾。

{{< /math-block >}}

### 边界 (Boundary)

{{< math-block type="definition" title="Definition 1.2.5" label="boundary">}}

设 $X$ 是一个拓扑空间，$A \subset X$ 是一个子集。$A$ 的**边界**，记为 $\partial A$，定义为 $A$ 的闭包与 $A$ 的内部的差集：

$$\partial A = \overline{A} - A^{\circ}$$

**等价描述 (Lemma):**

点 $y \in X$ 属于 $\partial A$ 当且仅当 $y$ 的**任何邻域**都同时与 $A$ 和 $X-A$ 相交。

{{< /math-block >}}

{{< math-block type="theorem" title="命题" >}}

设 $X$ 是一个拓扑空间，且 $B \subset A \subset X$。令 $\overline{B}_A$ 和 ${B_A}^{\circ}$ 分别表示 $B$ 在**子空间 $A$** 中的闭包和内部；令 $\overline{B}$ 和 $B^{\circ}$ 分别表示 $B$ 在**全空间 $X$** 中的闭包和内部。则以下关系成立：

(1) **子空间闭包与全空间闭包的关系：**
$$\overline{B}_A = \overline{B} \cap A$$

(2) **子空间内部与全空间闭包的关系：**
$${B_A}^{\circ} = A - \overline{(A-B)}$$

{{< /math-block >}}

{{< math-block type="proof" >}}

(1) 证明 $\overline{B}_A = \overline{B} \cap A$

证明 "$\subset$"：

$\forall x \in \overline{B}_A$，则 $x \in A$。取 $X$ 中 $x$ 的任意邻域 $U$。$U \cap A$ 是 $x$ 在 $A$ 中的邻域。因 $x \in \overline{B}_A$，故 $(U \cap A) \cap B \ne \emptyset$。因 $B \subset A$，所以 $U \cap B \ne \emptyset$。故 $x \in \overline{B}$。因此 $x \in \overline{B} \cap A$。

证明 "$\supset$"：

$\forall x \in \overline{B} \cap A$。取 $x$ 在 $A$ 中的任意邻域 $U_A = U \cap A$ ($U$ 在 $X$ 中开)。因 $x \in \overline{B}$，故 $U \cap B \ne \emptyset$。因 $B \subset A$，故 $U_A \cap B = (U \cap A) \cap B = U \cap B \ne \emptyset$。因此 $x \in \overline{B}_A$。

(2) 证明 ${B_A}^{\circ} = A - \overline{(A-B)}$

证明 (Pf.):

利用补集关系：${B_A}^{\circ} = A - \overline{(A-B)}_A$。应用结论 (1)：$\overline{(A-B)}_A = \overline{(A-B)} \cap A$。故 ${B_A}^{\circ} = A - (\overline{(A-B)} \cap A)$。根据集合论， $A - (C \cap A) = A - C$。最终 ${B_A}^{\circ} = A - \overline{(A-B)}$。

{{< /math-block >}}

**提醒 (Remark)：** **子空间内部与全空间内部的关系不一定成立**，即 ${B_A}^{\circ} \ne B^{\circ} \cap A$。

**反例 (Counterexample):**

* $X = \mathbb{R}_{std}, A = B = \mathbb{Q}$。
* ${B_A}^{\circ} = \mathbb{Q}$。
* $B^{\circ} \cap A = \dot{\mathbb{Q}} \cap \mathbb{Q} = \emptyset \cap \mathbb{Q} = \emptyset$。
* 故 ${B_A}^{\circ} \ne B^{\circ} \cap A$。

{{< math-block type="theorem" title="一些有用的推论-2" >}}

设 $X$ 是一个拓扑空间，$A, B \subset X$。则以下恒等式和包含关系成立：

(i) **补集的内部** (Interior of the complement):
$$\text{int}(X-A) = X - \overline{A}$$
$${(X-A)}^{\circ} = X - \overline{A}$$

(ii) **补集的闭包** (Closure of the complement):
$$\overline{X-A} = X - A^{\circ}$$

(iii) **内部的交集** (Intersection of interiors):
$$A^{\circ} \cap B^{\circ} = {(A \cap B)}^{\circ}}$$

(iv) **内部的并集** (Union of interiors):
$$A^{\circ} \cup B^{\circ} \subset \dot{A \cup B}$$

(v) **闭包的交集** (Intersection of closures):
$$\overline{A} \cap \overline{B} \supset \overline{A \cap B}$$

(vi) **闭包的并集** (Union of closures):
$$\overline{A \cup B} = \overline{A} \cup \overline{B}$$

{{< /math-block >}}

{{< math-block type="proof" >}}

(i) ${(X-A)}^{\circ} = X - \overline{A}$

证明 "$\subset$"：
$\forall x \in {(X-A)}^{\circ}$ (即 $x \in (X-A)^\circ$)，则存在 $x$ 的邻域 $U$，使得 $x \in U \subset X-A$。

因此 $U \cap A = \emptyset$。

根据内部/闭包的等价引理 (previous lemma: $y \in \overline{A} \iff$ 任何邻域交 $A$ 不为空)，$x$ 不属于 $\overline{A}$，即 $x \in X - \overline{A}$。

证明 "$\supset$"：

$\forall x \in X - \overline{A}$。因为 $\overline{A}$ 是闭集，所以 $X - \overline{A}$ 是开集。

且 $X - \overline{A} \subset X-A$。

根据内部的定义（${(X-A)}^{\circ}$ 是包含在 $X-A$ 中的最大的开集），$X - \overline{A}$ 必须包含在 ${(X-A)}^{\circ}$ 中。

因此 $X - \overline{A} \subset {(X-A)}^{\circ}$。

(iii) $A^{\circ} \cap B^{\circ} = {(A \cap B)}^{\circ}}$

证明 "$\subset$"：
$\forall x \in A^{\circ} \cap B^{\circ}$。存在 $x$ 的邻域 $U_1$ 和 $U_2$，使得 $x \in U_1 \subset A$ 且 $x \in U_2 \subset B$。

因此 $x \in U_1 \cap U_2 \subset A \cap B$。

由于 $U_1$ 和 $U_2$ 都是开集，它们的交集 $U_1 \cap U_2$ 也是开集。

根据内部的等价引理，$x \in {(A \cap B)}^{\circ}}$。

证明 "$\supset$"：

因为 $A \cap B \subset A$，根据内部运算的单调性，${(A \cap B)}^{\circ} \subset A^{\circ}$。

同理，因为 $A \cap B \subset B$，所以 ${(A \cap B)}^{\circ} \subset B^{\circ}$。

因此，${(A \cap B)}^{\circ}$ 包含于它们的交集：${(A \cap B)}^{\circ} \subset A^{\circ} \cap B^{\circ}$。

(iv) $A^{\circ} \cup B^{\circ} \subset {(A \cup B)}^{\circ}$

证明 "$\subset$"：

因为 $A \subset A \cup B$，根据内部运算的单调性，$A^{\circ} \subset \dot{A \cup B}$。

同理，因为 $B \subset A \cup B$，所以 $B^{\circ} \subset {(A \cup B)}^{\circ}$。

因此，它们的并集 $A^{\circ} \cup B^{\circ}$ 包含于 ${(A \cup B)}^{\circ}$。

{{< /math-block >}}

**注意：**
**对于 (iv)，** 等号不一定成立
**对于 (v)，** 等号不一定成立。

**反例 (Eg.)：** (说明 (iv) 中不取等号)

设 $X = \mathbb{R}_{std}$（标准拓扑下的实数集）。令 $A=[-1,0]$，$B=(0,1]$。此时$A^{\circ}=(-1,0)$，$B^{\circ}=(0,1)$，因此$A^{\circ} \cup B^{\circ} = (-1,0) \cup (0,1)$。而$A\cup B=[-1,1]$，故 ${(A\cup B)}^{\circ}=(-1,1)$。显然$A^{\circ}\cup B^{\circ}\neq\dot{A\cup B}$，差了一个点 $\{0\}$。

再令 $A=\mathbb{Q}$（有理数集），$B=\mathbb{R}-\mathbb{Q}$（无理数集）。在标准拓扑下，$A^{\circ}=\emptyset$ 且 $B^{\circ}=\emptyset$，因此 $A^{\circ} \cup B^{\circ}=\emptyset$。但$A\cup B=\mathbb{R}$，所以 ${(A\cup B)}^{\circ}=\mathbb{R}$，同样说明了$A^{\circ}\cup B^{\circ}\neq {(A\cup B)}^{\circ}$。

## 极限点与闭包的关系

### 极限点 (Limit Point)

{{< math-block type="definition" title="Definition 极限点" label="limit-point">}}

设 $X$ 是一个拓扑空间，$A \subset X$ 是一个子集，$x \in X$。
$x$ 是 $A$ 的一个**极限点**（limit point，或聚点），如果 $x$ 的**每一个邻域**（nbhd）都与 $A$ 在一个**不同于 $x$ 本身**的点上相交。

**等价描述 (Equiv.):**

$$x \text{ 是 } A \text{ 的一个极限点 } \iff x \in \overline{A - \{x\}}.$$

**符号表示:**

我们用 $A'$ 表示 $A$ 的所有极限点的集合。
则 $A' \subset \overline{A}$。

{{< /math-block >}}

**示例 (Eg.):**

* 在 $E^1$ 中，$A = [0, 1) \cup \{2\}$，则 $2 \notin A'$。
* 在 $E^1$ 中，$A = \mathbb{Q}$，则 $\forall x \in E^1$, $x \in A'$。

### 闭包与极限点集合的关系

{{< math-block type="theorem" title="命题" >}}

设 $X$ 是一个拓扑空间，$A \subset X$。则：
$$\overline{A} = A \cup A'$$

{{< /math-block >}}

{{< math-block type="proof" >}}

证明 "$A \cup A' \subset \overline{A}$"：

因为 $A \subset \overline{A}$ 且 $A' \subset \overline{A}$，所以 $A \cup A' \subset \overline{A}$。

证明 "$\overline{A} \subset A \cup A'$"：
$\forall x \in \overline{A}$，假设 $x \notin A$。根据闭包引理， $x$ 的任意邻域 $U$ 都与 $A$ 相交。因为 $x \notin A$，所以 $U \cap A$ 包含一个异于 $x$ 的点。故 $x$ 是 $A$ 的极限点，即 $x \in A'$。因此 $\overline{A} \subset A \cup A'$。

{{< /math-block >}}

{{< math-block type="theorem" title="推论 (Corollary): 闭集的充要条件" >}}

$A \subset X$ 是一个**闭集** $\iff A' \subset A$。

**证明思路:** $A$ 是闭集 $\iff A = \overline{A} \iff A = A \cup A' \iff A' \subset A$。

{{< /math-block >}}

## 积空间中集合的内部和闭包

{{< math-block type="theorem" title="命题" >}}

设 $X$ 和 $Y$ 是两个拓扑空间，$A \subset X$，$B \subset Y$。则以下关系成立：

(1) **积集合的内部：**
$$(A \times B)^\circ = A^{\circ} \times B^{\circ}$$

(2) **积集合的闭包：**
$$\overline{A \times B} = \overline{A} \times \overline{B}$$

{{< /math-block >}}

{{< math-block type="proof" >}}

(1) 积集合的内部：$(A \times B)^\circ = A^{\circ} \times B^{\circ}$

证明 "$\subset$"：

$\forall (x, y) \in (A \times B)^\circ$，存在开集 $W \subset X \times Y$ 使得 $(x, y) \in W \subset A \times B$。存在基元素 $U \times V$ 使得 $(x, y) \in U \times V \subset W$。因此 $x \in U \subset A$ 且 $y \in V \subset B$。根据内部定义， $x \in A^{\circ}$ 且 $y \in B^{\circ}$，故 $(x, y) \in A^{\circ} \times B^{\circ}$。

证明 "$\supset$"：

$\forall (x, y) \in A^{\circ} \times B^{\circ}$。则 $x \in A^{\circ}$ 且 $y \in B^{\circ}$。因为 $x \in A^{\circ}$，存在 $X$ 中的开集 $U$，使得 $x \in U \subset A$。因为 $y \in B^{\circ}$，存在 $Y$ 中的开集 $V$，使得 $y \in V \subset B$。考虑积集 $U \times V$。 $U \times V$ 是 $X \times Y$ 中的一个**开集**。且 $(x, y) \in U \times V$。同时，由于 $U \subset A$ 且 $V \subset B$，故 $U \times V \subset A \times B$。因此，$(x, y)$ 被包含在 $A \times B$ 内的一个开集 $U \times V$ 中。根据内部的定义，$(x, y) \in (A \times B)^\circ$。

(2) 积集合的闭包：$\overline{A \times B} = \overline{A} \times \overline{B}$

证明 "$\subset$"：(反证法)

假设 $(x, y) \notin \overline{A} \times \overline{B}$，则假设 $x \notin \overline{A}$。存在 $x$ 的邻域 $U$ 使得 $U \cap A = \emptyset$。$U \times Y$ 是 $(x, y)$ 的邻域，且 $(U \times Y) \cap (A \times B) = (U \cap A) \times (Y \cap B) = \emptyset$。故 $(x, y) \notin \overline{A \times B}$，矛盾。

证明 "$\supset$"：

$\forall (x, y) \in \overline{A} \times \overline{B}$。设 $W$ 是 $(x, y)$ 的任意邻域，包含 $U \times V$ ($U, V$ 分别是 $x, y$ 的邻域)。因 $x \in \overline{A}, y \in \overline{B}$，故 $U \cap A \ne \emptyset$ 且 $V \cap B \ne \emptyset$。故 $W \cap (A \times B) \supset (U \times V) \cap (A \times B) = (U \cap A) \times (V \cap B) \ne \emptyset$。因此 $(x, y) \in \overline{A \times B}$。

{{< /math-block >}}
