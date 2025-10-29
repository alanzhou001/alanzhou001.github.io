---
title: 紧性
description: 拓扑中紧性（compactness）定义与性质
slug: topol-6
date: 2025-10-29 21:36:00+0800
math: true
image: cover.jpg
categories:
    - Math
tags:
    - Topology
    - notes
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

封面画师：[Novi](https://www.pixiv.net/artworks/113735140)

## 紧性

{{< math-block type="definition" title="Definition 4.3.1 紧致空间" label="compactness">}}

**开覆盖 (Open Cover)**
设 $X$ 是一个拓扑空间 (topol. space)，$A \subset X$。
$\mathcal{O}$ 是 $X$ 中的一组开集 (a collection of open sets of $X$)。
如果 $A$ 包含在 $\mathcal{O}$ 中所有开集的并集内，则 $\mathcal{O}$ 称为 $A$ 的一个**开覆盖** (open cover)。

**子覆盖 (Subcover)**
如果 $\mathcal{O}$ 覆盖了 $A$，$\mathcal{O}'$ 是 $\mathcal{O}$ 的一个子族 (subcollection) 且 $\mathcal{O}'$ 也覆盖了 $A$，则 $\mathcal{O}'$ 是 $\mathcal{O}$ 的一个**子覆盖** (subcover)。

**紧致空间 (Compact Space)**
一个拓扑空间 $X$ 是**紧致的** (compact)，如果 $X$ 的每一个开覆盖都有一个**有限子覆盖** (a finite subcover)。

{{< /math-block >}}

**例 (Eg.)：**

1. $E^1$ **不是紧致的** (is not compact)。

    **证明：** 考虑开覆盖 $\mathcal{O} = \{(-n, n) | n \in \mathbb{Z}^+\}$。
    $\bigcup_{n=1}^{\infty} (-n, n) = E^1$，所以 $\mathcal{O}$ 是 $E^1$ 的一个开覆盖。
    如果 $\mathcal{O}$ 有一个有限子覆盖 $\mathcal{O}' = \{(-n_1, n_1), \ldots, (-n_k, n_k)\}$。
    令 $N = \max\{n_1, \ldots, n_k\}$。则 $\bigcup_{i=1}^{k} (-n_i, n_i) = (-N, N)$。
    由于 $(-N, N) \neq E^1$（例如，点 $N+1$ 不被覆盖），故 $\mathcal{O}$ 没有有限子覆盖。
    因此 $E^1$ 不是紧致的。

2. 设 $X = \{x_1, x_2, \ldots, x_n\}$ 是一个有限集，则 $X$ 上的任何拓扑都是**紧致的** (is compact)。

    **证明：** 设 $\mathcal{O}$ 是 $X$ 的任意开覆盖。对于 $\forall x_i \in X$，必存在 $U_i \in \mathcal{O}$ 使得 $x_i \in U_i$。由于 $X$ 只有 $n$ 个点，我们只需选择 $\{U_1, U_2, \ldots, U_n\}$ 这 $n$ 个开集即可覆盖 $X$。这是一个有限子覆盖。

3. $\mathbb{R}_{fc}$（具有**共有限拓扑** (cofinite topology) 的实数集 $\mathbb{R}$）是**紧致的** (is compact)。

    **证明：**
    设 $\mathcal{O}$ 是 $\mathbb{R}_{fc}$ 的一个开覆盖 (open cover)。
    由于 $\mathcal{O}$ 覆盖了 $\mathbb{R}$，$\exists U \in \mathcal{O}$ 使得 $U \neq \emptyset$。
    根据共有限拓扑的定义，非空开集 $U$ 的补集 $\mathbb{R} \setminus U$ 是**有限集**。
    记 $\mathbb{R} \setminus U = \{y_1, y_2, \ldots, y_m\}$。
    $\forall y_i \in \mathbb{R} \setminus U$ (即 $y_i$ 是未被 $U$ 覆盖的点)，由于 $\mathcal{O}$ 覆盖了 $\mathbb{R}$， $\exists V_i \in \mathcal{O}$ 使得 $y_i \in V_i$。
    考虑 $\mathcal{O}' = \{V_1, V_2, \ldots, V_m, U\}$。$\mathcal{O}'$ 是 $\mathcal{O}$ 的一个有限子集（包含 $m+1$ 个元素）。
    $$\bigcup_{i=1}^{m} V_i \cup U = (\mathbb{R} \setminus U) \cup U = \mathbb{R}$$
    因此 $\mathcal{O}'$ 是 $\mathcal{O}$ 的一个有限子覆盖。
    所以 $\mathbb{R}_{fc}$ 是紧致的。