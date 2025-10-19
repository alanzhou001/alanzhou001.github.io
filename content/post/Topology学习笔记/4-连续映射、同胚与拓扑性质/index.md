---
title: 连续映射、同胚与拓扑性质
description: 连续映射的定义，同胚的定义与性质
slug: topol-4
date: 2025-10-19 16:05:00+0800
math: true
image: cover.jpg
categories:
    - Math
tags:
    - Topology
    - notes
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

## 连续映射

{{< math-block type="definition" title="Definition1.3.1 连续映射" label="cont-map">}}

设 $X$ 和 $Y$ 是两个拓扑空间，$f: X \to Y$ 是一个映射。如果对于 $Y$ 中**任意的开集 $V$**，其原像 $f^{-1}(V)$ 在 $X$ 中都是**开集**，则称 $f$ 是**连续的**（continuous）。

**示例 (Eg.):**

(1) **恒等映射 (Id):** $Id: X \to X, x \mapsto x$ 是**连续的**。

(2) **常值映射 (C):** $C: X \to Y, x \mapsto y_0$ 是**连续的**。

(3) **包含映射 ($\iota$):** 设 $A \subset X$。$\iota: A \to X, a \mapsto a$ 是**连续的**。

(4) **投影映射 ($\pi_i$):** $\pi_1: X \times Y \to X$ 和 $\pi_2: X \times Y \to Y$ 都是**连续的**。

{{< /math-block >}}

{{< math-block type="theorem" title="Lemma: 连续映射的复合" label="mix" >}}

设 $f: X \to Y$ 和 $g: Y \to Z$ 都是**连续映射**，则它们的复合映射 $g \circ f: X \to Z$ 也是**连续的**。

{{< /math-block >}}

{{< math-block type="proof" >}}

$$\forall \text{ open set } V \text{ in } Z, \quad (g \circ f)^{-1}(V) = f^{-1}(g^{-1}(V)) \text{ is open in } X$$

{{< /math-block >}}

**Eg.**

设 $f: X \to Y$ 是连续映射，$A \subset X$。则 $f$ 在 $A$ 上的限制 $f|_A: A \to Y$ 也是**连续的**。

- **证明 (Pf.):** $f|_A$ 是 $f$ 和包含映射 $\iota: A \to X$ 的复合 $f|_A = f \circ \iota$。因为 $f$ 和 $\iota$ 都是连续的，所以 $f|_A$ 也是连续的。

### 连续性的判别

{{< math-block type="theorem" title="Lemma: 基元素判别法 (Basis Criterion)" label="basis-cri" >}}

设 $f: X \to Y$ 是一个映射，$\mathcal{B}$ 是 $Y$ 的一个**基**。则 $f$ 是**连续的** $\iff$ 对于 $\forall B \in \mathcal{B}$，$f^{-1}(B)$ 在 $X$ 中是**开集**。

{{< /math-block >}}

{{< math-block type="proof" >}}

**"$\implies$"：** (连续 $\implies$ 基元素原像开) 基元素 $B$ 本身是开集，由连续定义知 $f^{-1}(B)$ 是开集。

**"$\impliedby$"：** (基元素原像开 $\implies$ 连续) 设 $V$ 是 $Y$ 中任意开集。 $V = \bigcup_i B_i$ ($B_i \in \mathcal{B}$)。则 $f^{-1}(V) = \bigcup_i f^{-1}(B_i)$。由假设，$f^{-1}(B_i)$ 都是开集，故其并集 $f^{-1}(V)$ 也是开集。因此 $f$ 连续。

{{< /math-block >}}

{{< math-block type="theorem" title="Lemma: 闭集判别法 (Closed Set Criterion)" label="close-cri" >}}

设 $f: X \to Y$ 是一个映射。则 $f$ 是**连续的** $\iff$ 对于 $Y$ 中**任意的闭集 $C$**，$f^{-1}(C)$ 在 $X$ 中是**闭集**。

{{< /math-block >}}

{{< math-block type="proof" >}}

**"$\implies$"：** (连续 $\implies$ 闭集原像闭) 设 $C$ 是 $Y$ 中闭集，则 $Y-C$ 是开集。因为 $f$ 连续，$f^{-1}(Y-C) = X - f^{-1}(C)$ 是开集。故 $f^{-1}(C)$ 是闭集。

**"$\impliedby$"：** (闭集原像闭 $\implies$ 连续) 设 $V$ 是 $Y$ 中开集，则 $Y-V$ 是闭集。根据假设，$f^{-1}(Y-V)$ 是闭集。 $f^{-1}(V) = X - f^{-1}(Y-V)$ 是闭集的补集，故 $f^{-1}(V)$ 是开集。因此 $f$ 连续。

{{< /math-block >}}

#### 示例 (Examples)

- **实变函数：** $f: E^1 \to E^1$ (如 $x^n, e^x, \ln x, \sin x, \cos x, \dots$) 都是**连续的**。
- **多元函数：** $f: E^1 \times E^1 \to E^1$ (如 $x+y, xy, x/y (y \ne 0), \dots$) 都是**连续的**。

### 积空间映射的连续性

{{< math-block type="theorem" title="命题" >}}

设 $f: X \to Y_1 \times Y_2$ 的分量映射为 $f_1: X \to Y_1$ 和 $f_2: X \to Y_2$，即 $f(x) = (f_1(x), f_2(x))$。

则 $f$ 是**连续的** $\iff$ **$f_1$ 和 $f_2$ 都是连续的**。

{{< /math-block >}}

{{< math-block type="proof" >}}

**证明 "$\implies$" ( $f$ 连续 $\implies f_1, f_2$ 连续)**
  
投影映射 $\pi_1: Y_1 \times Y_2 \to Y_1$ 和 $\pi_2: Y_1 \times Y_2 \to Y_2$ 都是**连续的**。
  
分量映射可表示为复合：$f_1 = \pi_1 \circ f$ 和 $f_2 = \pi_2 \circ f$。
  
因为[连续映射的复合是连续的](#mix)，故 $f_1$ 和 $f_2$ 都是**连续的**。

**证明 "$\impliedby$" ( $f_1, f_2$ 连续 $\implies f$ 连续)**

设 $\mathcal{B} = \{ U_1 \times U_2 \mid U_1 \in \mathcal{T}_{Y_1}, U_2 \in \mathcal{T}_{Y_2} \}$ 是积空间 $Y_1 \times Y_2$ 的一个基。

我们只需证明对于 $\forall U_1 \times U_2 \in \mathcal{B}$，其原像 $f^{-1}(U_1 \times U_2)$ 在 $X$ 中是开集。

原像可分解为：
$$f^{-1}(U_1 \times U_2) = f_1^{-1}(U_1) \cap f_2^{-1}(U_2)$$

因为 $f_1$ 连续且 $U_1$ 开，所以 $f_1^{-1}(U_1)$ 是 $X$ 中的**开集**。

因为 $f_2$ 连续且 $U_2$ 开，所以 $f_2^{-1}(U_2)$ 是 $X$ 中的**开集**。

两个开集的交集 $f_1^{-1}(U_1) \cap f_2^{-1}(U_2)$ 仍然是 $X$ 中的**开集**。

根据[基元素判别引理](#basis-cri)， $f$ 是**连续的**。

因此，$f$ 连续 $\iff f_1, f_2$ 连续。

{{< /math-block >}}

### 粘合引理 (The Pasting Lemma)

{{< math-block type="theorem" title="粘合引理 (The Pasting Lemma)" label="pasting" >}}

设 $X$ 是一个拓扑空间，且 $A, B$ 是 $X$ 中的两个**闭集**，满足 $A \cup B = X$。

假设 $f: A \to Y$ 和 $g: B \to Y$ 是两个连续映射，且对于 $\forall x \in A \cap B$，$f(x) = g(x)$。

则由此构造的映射 $h: X \to Y$ 是**连续的**。

$$h(x) = \begin{cases} f(x) & x \in A \\ g(x) & x \in B \end{cases}$$

{{< /math-block >}}

{{< math-block type="proof" >}}

我们使用连续映射的[闭集判别法](#close-cri)。设 $C$ 是 $Y$ 中的任意闭集。

**原像分解：** $h^{-1}(C)$ 可以分解为 $f^{-1}(C)$ 和 $g^{-1}(C)$ 的并集：
$$h^{-1}(C) = f^{-1}(C) \cup g^{-1}(C)$$

**验证 $f^{-1}(C)$ 是 $X$ 中的闭集：**

* 因为 $f: A \to Y$ 连续，所以 $f^{-1}(C)$ 是**子空间 $A$** 中的闭集。
* 根据子空间拓扑定义，存在 $X$ 中的闭集 $D_1$，使得 $f^{-1}(C) = D_1 \cap A$。
* 由于 $D_1$ 是 $X$ 中的闭集，且 $A$ 是命题条件给定的 $X$ 中的闭集，故 $f^{-1}(C)$ 是两个 $X$ 中闭集的交集，因此是 $X$ 中的**闭集**。

**验证 $g^{-1}(C)$ 是 $X$ 中的闭集：**

* 同理，因为 $g: B \to Y$ 连续，且 $B$ 是 $X$ 中的闭集，所以 $g^{-1}(C)$ 在 $X$ 中是**闭集**。

**结论：**

* $h^{-1}(C)$ 是 $X$ 中两个闭集的并集 $f^{-1}(C) \cup g^{-1}(C)$。
* 因此 $h^{-1}(C)$ 是 $X$ 中的**闭集**。
* 故 $h$ 是连续的。

{{< /math-block >}}

## 同胚

