---
title: 分离性与可数性
description: 连续映射的定义，同胚的定义与性质
slug: topol-5
date: 2025-10-26 14:37:00+0800
math: true
image: cover.jpg
categories:
    - Math
tags:
    - Topology
    - notes
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

## 分离性

{{< math-block type="definition" title="Definition3.1.2-1 T3空间" label="t3">}}

设 $X$ 是一个拓扑空间 (topol. space)，如果 $X$ 满足以下条件，则称 $X$ 是**正则空间 (Regular)**（$T_3$空间）：

(i) $X$ 中的单点集 (one-point sets) 是闭集 (closed)；

(ii) $\forall a \in X$， $\forall$ 闭集 $B \subset X$，且 $a \notin B$，存在不相交的开集 $U$ 和 $V$ (disjoint open sets $U$ and $V$)，使得 $a \in U$ 且 $B \subset V$。

{{< /math-block >}}

**Remark：** 正则 (regular) $\Rightarrow$ Hausdorff。

{{< math-block type="definition" title="Definition3.1.2-2 T4空间" label="t4">}}

设 $X$ 是一个拓扑空间 (topol. space)，如果 $X$ 满足以下条件，则称 $X$ 是**正规空间(Normal)**（$T_4$空间）：

(i) $X$ 中的单点集 (one-point sets) 是闭集 (closed)；

(ii) $\forall$ 两个不相交的闭集 $A \subset X$ 和 $B \subset X$ ($A \cap B = \emptyset$)，存在不相交的开集 $U$ 和 $V$ (disjoint open sets $U$ and $V$)，使得 $A \subset U$ 且 $B \subset V$。

{{< /math-block >}}

**Remark：** 正规 (normal) $\Rightarrow$ 正则 (regular)。

{{< math-block type="theorem" title="分离公理 (Separation axiom)" >}}

$$\text{Normal (T}_4) \subset \text{regular} \subset \text{Hausdorff} \quad (\text{注：} \text{T}_3 \text{通常指正则且 } T_1 \text{，} T_2 \text{指 Hausdorff})$$

{{< /math-block >}}

**命题：每个度量空间（metric space）都是正规空间（$T_4$，nomal）**

{{< math-block type="proof" >}}

要证明一个空间 $X$ 是正规空间，需要证明两点：

1. $X$ 中每个单点集都是闭集。
2. $\forall$ 两个不相交的闭集 $A, B \subset X$，存在不相交的开集 $U$ 和 $V$，使得 $A \subset U$ 且 $B \subset V$。

**1. 单点集是闭集：**
在度量空间中，每个单点集都是闭集。

**2. 分离不相交闭集：**
假设 $X$ 是一个度量空间，$A$ 和 $B$ 是 $X$ 中两个不相交的闭集 (disjoint closed sets)。
定义函数 $g: X \rightarrow E^1$ 和 $h: X \rightarrow E^1$:
$$g(x) = d(x, A) := \inf\{d(x, a) | a \in A\}$$
$$h(x) = d(x, B) := \inf\{d(x, b) | b \in B\}$$
定义函数 $f: X \rightarrow E^1$:
$$f(x) = \frac{d(x, A)}{d(x, A) + d(x, B)}$$

整个证明分为三个步骤：

**(i) 证明 $g$ 和 $h$ 是连续的 (continuous)。**

要证明 $g$ 连续，只需证明 $\forall x \in X$ 和 $\forall \epsilon > 0$，存在 $\delta$ 使得 $d(x, y) < \delta \Rightarrow |g(y) - g(x)| < \epsilon$。

对于 $\forall (r, s) \subset E^1$，我们证明 $g^{-1}((r, s))$ 是 $X$ 中的开集。
$\forall x \in g^{-1}((r, s))$，我们找到 $\epsilon > 0$ 使得 $B(x, \epsilon) \subset g^{-1}((r, s))$。
选取 $\epsilon > 0$，使得 $(g(x) - \epsilon, g(x) + \epsilon) \subset (r, s)$。
即满足 $g(x) - \epsilon > r$ 和 $g(x) + \epsilon < s$。

对于 $\forall y \in B(x, \epsilon)$，有 $d(x, y) < \epsilon$。
利用三角不等式证明 $|g(y) - g(x)| < \epsilon$：
$$\begin{aligned} g(y) &= d(y, A) = \inf\{d(y, a) | a \in A\} \\ &\le \inf\{d(y, x) + d(x, a) | a \in A\} \\ &= d(y, x) + \inf\{d(x, a) | a \in A\} \\ &= d(y, x) + d(x, A) \\ &< \epsilon + g(x) \le s \end{aligned}$$
$$\begin{aligned} g(x) &= d(x, A) \le d(x, y) + d(y, A) \\ &< \epsilon + g(y) \\ \Rightarrow g(y) &> g(x) - \epsilon > r \end{aligned}$$
因此 $g(y) \in (r, s)$。故 $B(x, \epsilon) \subset g^{-1}((r, s))$。
所以 $g^{-1}((r, s))$ 是 $X$ 中的开集，$g$ 是连续的。
类似地，$h$ 也是连续的。

**(ii) 证明分母 $d(x, A) + d(x, B) > 0, \forall x \in X$。**

我们知道 $d(x, A) = 0 \iff x \in \overline{A}$。

* “$\Leftarrow$” (即 $x \in A \Rightarrow d(x, A) = 0$) 是显然的 (obvious)。
* “$\Rightarrow$” (即 $d(x, A) = 0 \Rightarrow x \in A$): 假设 $x \notin A$。因为 $A$ 是闭集 (closed)，所以 $X \setminus A$ 是开集。$\exists \epsilon > 0$，使得 $B(x, \epsilon) \subset X \setminus A$。这意味着对于 $A$ 中的所有点 $a$ 都有 $d(x, a) \ge \epsilon > 0$。因此 $d(x, A) = \inf\{d(x, a) | a \in A\} \ge \epsilon > 0$。这与 $d(x, A) = 0$ 矛盾 (Contradiction)。

如果 $d(x, A) + d(x, B) = 0$，则 $d(x, A) = 0$ 且 $d(x, B) = 0$。
根据上面证明的结论， $d(x, A) = 0 \Rightarrow x \in A$ 且 $d(x, B) = 0 \Rightarrow x \in B$。
所以 $x \in A \cap B$。但这与 $A \cap B = \emptyset$ 矛盾 (Contradiction)。
因此 $d(x, A) + d(x, B) > 0, \forall x \in X$。

**(iii) 构造分离开集：**

由 (i) 和 (ii) 可知，$f$ 是连续的 (continuous)。
对于 $\forall a \in A$：
$$f(a) = \frac{d(a, A)}{d(a, A) + d(a, B)} = \frac{0}{0 + d(a, B)} = 0$$
对于 $\forall b \in B$：
$$f(b) = \frac{d(b, A)}{d(b, A) + d(b, B)} = \frac{d(b, A)}{d(b, A) + 0} = 1$$
令 $U = f^{-1}((-\infty, \frac{1}{2}))$， $V = f^{-1}((\frac{1}{2}, +\infty))$。
由于 $f$ 连续，且 $(-\infty, \frac{1}{2})$ 和 $(\frac{1}{2}, +\infty)$ 是 $E^1$ 中的开集，故 $U$ 和 $V$ **都是开集** (Both $U$ and $V$ are open)。

* $A \subset U$ (因为 $f$ 在 $A$ 上取值 $0 < 1/2$)。
* $B \subset V$ (因为 $f$ 在 $B$ 上取值 $1 > 1/2$)。
* $U \cap V = \emptyset$ (因为 $f$ 的值不可能同时小于 $1/2$ 和大于 $1/2$)。

因此， $X$ 是正规空间。

{{< /math-block >}}

## 可数性

{{< math-block type="definition" title="Definition3.1.3 第一可数空间" label="c1">}}

一个拓扑空间 $X$ 在点 $x$ 处具有**可数邻域基** (countable neighborhood basis)，如果存在一个 $x$ 的可数邻域族 $\{U_n\}_{n \in \mathbb{Z}^+}$，使得 $x$ 的任何邻域 $W$ 都包含其中一个 $U_n$，即 $x \in U_n \subset W$。
如果 $X$ 在其每一个点处都具有可数邻域基，则称 $X$ 是**第一可数空间** (first countable)，或满足**第一可数公理** (first countability axiom)。

{{< /math-block >}}

**例 (Eg.)：**
每个**度量空间** $(X, d)$ 都是**第一可数空间** (1st countable)。

{{< math-block type="proof" >}}

$\forall x \in (X, d)$，定义可数邻域族 $\{U_n = B(x, \frac{1}{n})\}_{n \in \mathbb{Z}^+}$。这个族是 $x$ 的一个可数邻域基 (countable nbhd basis)。

**（补充：）** 设 $W$ 是 $x$ 的任意邻域。则存在一个开集 $V$ 使得 $x \in V \subset W$。由于 $V$ 是开集，存在 $\epsilon > 0$ 使得 $B(x, \epsilon) \subset V$。根据阿基米德性质，存在正整数 $N$ 使得 $\frac{1}{N} < \epsilon$。令 $U_N = B(x, \frac{1}{N})$，则 $x \in U_N \subset B(x, \epsilon) \subset V \subset W$。因此 $\{U_n\}$ 是一个可数邻域基。

{{< /math-block >}}

{{< math-block type="definition" title="Definition3.1.4 第二可数空间" label="c1">}}

如果一个空间 $X$ 具有一个**可数基** (countable basis) 作为其拓扑的基，则称 $X$ 是**第二可数空间** (second countable)，或满足**第二可数公理** (second countability axiom)。

**例 (Eg.)：**
$E^n$ 是**第二可数空间** (second countable)。
**证明：** $\mathcal{B} = \{B(x, \frac{1}{k}) | x \in E^n,  x \text{的每个坐标都是有理数}, k \in \mathbb{Z}^+\}$ 是一个可数基 (countable basis)。

{{< /math-block >}}

**命题 (Proposition)：**
**第二可数** (2nd countable) $\Rightarrow$ **第一可数** (1st countable)。

{{< math-block type="proof" >}}

假设 $X$ 是第二可数空间。设 $\mathcal{B}$ 是 $X$ 的一个可数基 (countable basis)。

$\forall x \in X$，定义 $\mathcal{B}_x = \{B \in \mathcal{B} | x \in B\}$。
由于 $\mathcal{B}$ 是可数的， $\mathcal{B}_x$ 也是可数的。

$\mathcal{B}_x$ 是 $x$ 的一个可数邻域基 (countable nbhd basis at $x$)。

**（补充：）** 设 $W$ 是 $x$ 的任意邻域。则 $W$ 是开集（或包含一个开集 $V$）。由于 $\mathcal{B}$ 是基，存在 $B \in \mathcal{B}$ 使得 $x \in B \subset W$。根据 $\mathcal{B}_x$ 的定义， $B \in \mathcal{B}_x$。因此 $\mathcal{B}_x$ 满足可数邻域基的定义，故 $X$ 是第一可数空间。

{{< /math-block >}}

**Remark：**
具有**离散拓扑** (discrete topology) 的 $\mathbb{R}$ 不是第二可数空间 (is not 2nd countable)。但是它却是**可度量化**的 (metrizable)。

{{< math-block type="theorem" >}}

1. **子空间：** 第一（第二）可数空间的子空间是第一（第二）可数空间。
2. **乘积：** 两个第一（第二）可数空间的乘积是第一（第二）可数空间。

{{< /math-block >}}

{{< math-block type="proof" >}}

**第二可数情况 (2nd countable case)**

**(1) 子空间：$X$ 是第二可数 $\Rightarrow A \subset X$ 是第二可数**

设 $X$ 是第二可数空间，$\mathcal{B}$ 是 $X$ 的一个可数基 (countable basis)。

设 $A \subset X$ 是一个子空间 (subspace)。

则 $\mathcal{B}_A = \{B \cap A | B \in \mathcal{B}\}$ 是 $A$ 的拓扑的一个基。
由于 $\mathcal{B}$ 是可数的，因此 $\mathcal{B}_A$ 也是可数的。

所以 $A$ 是第二可数空间。

**(2) 乘积：$X_1, X_2$ 是第二可数 $\Rightarrow X_1 \times X_2$ 是第二可数**

设 $X_1, X_2$ 是第二可数空间。

设 $\mathcal{B}_i$ 是 $X_i$ 的一个可数基，其中 $i=1, 2$。

则 $\mathcal{B} = \{B_1 \times B_2 | B_1 \in \mathcal{B}_1, B_2 \in \mathcal{B}_2\}$ 是乘积空间 $X_1 \times X_2$ 的拓扑的一个基。

由于 $\mathcal{B}_1$ 和 $\mathcal{B}_2$ 都是可数的，因此它们的笛卡尔积 $\mathcal{B}$ 也是可数的。

所以 $X_1 \times X_2$ 是第二可数空间。

**第一可数情况 (1st countable case)**

**(1) 子空间：$X$ 是第一可数 $\Rightarrow A \subset X$ 是第一可数**

$\forall a \in A$，因为 $X$ 是第一可数，所以 $a$ 在 $X$ 中有一个可数邻域基 $\mathcal{U} = \{U_n\}_{n \in \mathbb{Z}^+}$。

我们证明 $\mathcal{U}_A = \{U_n \cap A | U_n \in \mathcal{U}\}$ 是 $a$ 在子空间 $A$ 中的一个可数邻域基。

显然 $\mathcal{U}_A$ 是可数的。

设 $W$ 是 $a$ 在 $A$ 中的任意邻域。根据子空间拓扑的定义，存在 $X$ 中的开集 $V$，使得 $W = V \cap A$。

由于 $V$ 是 $a$ 在 $X$ 中的邻域，且 $\mathcal{U}$ 是 $a$ 在 $X$ 中的可数邻域基，因此 $\exists U_n \in \mathcal{U}$ 使得 $a \in U_n \subset V$。

那么 $a \in U_n \cap A \subset V \cap A = W$。

因此 $\mathcal{U}_A$ 是 $a$ 在 $A$ 中的一个可数邻域基。所以 $A$ 是第一可数空间。

**(2) 乘积：$X_1, X_2$ 是第一可数 $\Rightarrow X_1 \times X_2$ 是第一可数**

$\forall (x_1, x_2) \in X_1 \times X_2$。

由于 $X_i$ 是第一可数， $x_i$ 在 $X_i$ 中有一个可数邻域基 $\mathcal{U}_i = \{U_{i, n}\}_{n \in \mathbb{Z}^+}$，其中 $i=1, 2$。

我们证明 $\mathcal{U} = \{U_{1, n} \times U_{2, m} | n, m \in \mathbb{Z}^+\}$ 是 $(x_1, x_2)$ 在 $X_1 \times X_2$ 中的一个可数邻域基。

由于 $\mathbb{Z}^+ \times \mathbb{Z}^+$ 是可数的，所以 $\mathcal{U}$ 是可数的。

设 $W$ 是 $(x_1, x_2)$ 在 $X_1 \times X_2$ 中的任意邻域。根据乘积拓扑的定义，存在基元素 $B_1 \times B_2$ 使得 $(x_1, x_2) \in B_1 \times B_2 \subset W$，其中 $B_i$ 是 $X_i$ 中的开集。

由于 $\mathcal{U}_i$ 是 $x_i$ 的可数邻域基， $\exists U_{1, n} \in \mathcal{U}_1$ 和 $U_{2, m} \in \mathcal{U}_2$ 使得 $x_1 \in U_{1, n} \subset B_1$ 且 $x_2 \in U_{2, m} \subset B_2$。

那么 $(x_1, x_2) \in U_{1, n} \times U_{2, m} \subset B_1 \times B_2 \subset W$。
因此 $\mathcal{U}$ 是 $(x_1, x_2)$ 的一个可数邻域基。所以 $X_1 \times X_2$ 是第一可数空间。

{{< /math-block >}}

### 两个定理 (Two Theorems)

{{< math-block type="theorem" title="Urysohn 可度量化定理 (Urysohn Metrization Theorem)" >}}

如果一个拓扑空间 $X$ 是**正则空间** (Regular) 且是**第二可数空间** (2nd countable)，则 $X$ 是**可度量化空间** (metrizable)。
$$\text{正则} + \text{第二可数} \implies \text{可度量化}$$

{{< /math-block >}}

{{< math-block type="theorem" title="Tietze 扩张定理 (Tietze Extension THM)" >}}

设 $X$ 是一个**正规空间** (normal space)， $A \subset X$ 是一个闭集 (closed)。
如果 $f: A \rightarrow E^1$ 是一个连续函数 (continuous function)，
那么存在一个连续函数 $F: X \rightarrow E^1$，使得 $F|_A = f$。

{{< /math-block >}}

#### 例 (Eg.)

设 $\mathbb{Z}$ 是整数集，$\mathcal{B} = \{B_{a, b} = \{a + bi | i \in \mathbb{Z}\} | a, b \in \mathbb{Z}, b \neq 0\}$ 是 $\mathbb{Z}$ 上的一个基 (basis)。它生成了 $\mathbb{Z}$ 上的一个拓扑。

{{< math-block type="proof" >}}

**(i) 证明 $\mathcal{B}$ 是拓扑的一个基：**

1. **覆盖性：** $\forall x \in \mathbb{Z}$。取 $b=1$，则 $B_{x, 1} = \{x + 1 \cdot i | i \in \mathbb{Z}\} = \mathbb{Z}$。所以 $\mathbb{Z} = \bigcup_{B \in \mathcal{B}} B$。
2. **交集条件：** 设 $B_{a_1, b_1}, B_{a_2, b_2} \in \mathcal{B}$，且 $x \in B_{a_1, b_1} \cap B_{a_2, b_2}$。
    * $x \in B_{a_1, b_1} \implies x = a_1 + b_1 i_1$
    * $x \in B_{a_2, b_2} \implies x = a_2 + b_2 i_2$
    要找到 $B_{a_3, b_3} \in \mathcal{B}$ 使得 $x \in B_{a_3, b_3} \subset B_{a_1, b_1} \cap B_{a_2, b_2}$。
    令 $b_3 = \text{lcm}(b_1, b_2)$（最小公倍数）， $a_3 = x$。
    则 $B_{x, b_3} = \{x + b_3 i | i \in \mathbb{Z}\}$。
    由于 $b_3$ 是 $b_1$ 的倍数，所以 $B_{x, b_3} \subset B_{x, b_1} = B_{a_1 + b_1 i_1, b_1} = B_{a_1, b_1}$。
    同理，$B_{x, b_3} \subset B_{x, b_2} = B_{a_2, b_2}$。
    所以 $B_{x, b_3} \subset B_{a_1, b_1} \cap B_{a_2, b_2}$。
    故 $\mathcal{B}$ 是 $\mathbb{Z}$ 上的一个基。

**(ii) 判断可数性：**

* $\mathbb{Z}$ 是**第二可数空间** (2nd countable)。
  因为 $\mathcal{B}$ 是**可数**的。基 $\mathcal{B}$ 中的元素由 $(a, b)$ 决定，其中 $a, b \in \mathbb{Z}, b \neq 0$。 $\mathbb{Z} \times (\mathbb{Z} \setminus \{0\})$ 是可数集，故 $\mathcal{B}$ 可数。

**(iii) 判断正则性：**

* $\mathbb{Z}$ 是**正则空间** (regular)。
  
  **单点集是闭集：**
  
  $\forall a \in \mathbb{Z}$，单点集 $\{a\}$ 是闭集。$\mathbb{Z} \setminus \{a\} = \bigcup_{b \neq 0} B_{a+1, b} \cup B_{a-1, b} \cup \cdots$。或更简单地，考虑 $B_{x, 2} = \{x, x \pm 2, \ldots\}$。$\mathbb{Z} \setminus \{a\} = \bigcup_{x \neq a} \{x\}$。
  
  **点与闭集分离：** 
  
  $\forall a \in \mathbb{Z}$， $\forall$ 闭集 $C \subset \mathbb{Z}$， $a \notin C$。令 $V = \mathbb{Z} \setminus C$ 为 $a$ 的开邻域。

**完整证明：**

**证明单点集是闭集 (T1 条件)**

$\forall a \in \mathbb{Z}$，要证明 $\{a\}$ 是闭集，即 $\mathbb{Z} \setminus \{a\}$ 是开集。
$\forall x \in \mathbb{Z} \setminus \{a\}$，我们要找到 $x$ 的一个基元素邻域 $B_{x, b}$，使得 $a \notin B_{x, b}$。
$a \notin B_{x, b} \iff a \neq x + i b \text{ for any } i \in \mathbb{Z}$
$\iff a - x \neq i b \text{ for any } i \in \mathbb{Z}$
$\iff b$ 不能整除 $a - x$。

由于 $a \neq x$，所以 $a - x \neq 0$。我们只需要找到一个 $b \neq 0$ 且 $b$ **不整除** $a-x$。

* 如果 $|a-x| = 1$，取 $b = 2$。 $2$ 不整除 $\pm 1$。
* 如果 $|a-x| > 1$，取 $b = |a-x| + 1$。 $|a-x|$ 不能整除 $|a-x| + 1$。

**例如，取 $b = 2$。**

* 如果 $a$ 和 $x$ 奇偶性不同，即 $|a-x|$ 是奇数，则 $2$ 不整除 $a-x$。此时 $B_{x, 2}$ 是 $x$ 的开邻域且 $a \notin B_{x, 2}$。

因此，$\forall x \in \mathbb{Z} \setminus \{a\}$，都存在 $x$ 的一个开邻域不包含 $a$。所以 $\mathbb{Z} \setminus \{a\}$ 是开集，$\{a\}$ 是闭集。

**证明点与闭集可分离（正则条件的核心）**

$\forall a \in \mathbb{Z}$ 和 $\forall$ 闭集 $C \subset \mathbb{Z}$，且 $a \notin C$。要找到不相交的开集 $U$ 和 $V$，使得 $a \in U$ 且 $C \subset V$。

**关键性质：$B_{a, b}$ 既是开集也是闭集。**
* $B_{a, b}$ 是开集，因为它是基元素。
* $B_{a, b}$ 是闭集，因为它的补集 $\mathbb{Z} \setminus B_{a, b}$ 可以表示为其他基元素的并集：
$$\mathbb{Z} \setminus B_{a, b} = B_{a+1, b} \cup B_{a+2, b} \cup \cdots \cup B_{a+b-1, b}$$
由于每个 $B_{a+k, b}$ 都是开集，所以 $\mathbb{Z} \setminus B_{a, b}$ 是开集，即 $B_{a, b}$ 是闭集。

**构造 $U$ 和 $V$：**
由于 $a \notin C$，且 $C$ 是闭集。我们只需要找到一个基元素 $B_{a, b}$ 满足 $B_{a, b} \cap C = \emptyset$。

1.  对于 $\forall c \in C$，由于 $a \notin C$，所以 $a \neq c$。
2.  由第 1 步证明可知，对于 $\forall c \in C$，存在 $b_c \neq 0$ 使得 $c \notin B_{a, b_c}$，即 $b_c$ 不整除 $c-a$。

为了分离 $a$ 和整个 $C$，我们需要一个包含 $a$ 的开集 $U$ 和包含 $C$ 的开集 $V$。
由于 $B_{a, b}$ 是闭集，其补集 $V = \mathbb{Z} \setminus B_{a, b}$ 也是开集。
我们尝试找到一个 $b$ 使得 $C \subset \mathbb{Z} \setminus B_{a, b}$，即 $C \cap B_{a, b} = \emptyset$。

**（对于任意闭集 $C$ 的证明较为复杂，但根据 $B_{a, b}$ 既开又闭的性质，可以采取以下简化的构造方式，这种方式在 $T_3$ 空间中常用：）**

$\forall a \in \mathbb{Z}$ 且 $C$ 是不包含 $a$ 的闭集。

由于 $C$ 是闭集， $\mathbb{Z} \setminus C$ 是 $a$ 的开邻域。
$\mathbb{Z} \setminus C$ 是开集，可表示为基元素的并：
$$\mathbb{Z} \setminus C = \bigcup_{k} B_{a_k, b_k}$$
由于 $a \in \mathbb{Z} \setminus C$，所以 $a$ 包含在其中一个基元素中。
**因此存在 $B_{a, b} \in \mathcal{B}$ 使得 $a \in B_{a, b} \subset \mathbb{Z} \setminus C$。**

取 $U = B_{a, b}$。则 $U$ 是 $a$ 的开邻域，且 $U \cap C = \emptyset$。
取 $V = \mathbb{Z} \setminus B_{a, b}$。

* $V$ 是开集（因为 $B_{a, b}$ 是闭集）。
* $C \subset V$（因为 $C \cap B_{a, b} = \emptyset$）。
* $U \cap V = \emptyset$。

因此，$a$ 和闭集 $C$ 可以被不相交的开集 $U$ 和 $V$ 分离。
所以 $\mathbb{Z}$ 是正则空间。

{{< /math-block >}}