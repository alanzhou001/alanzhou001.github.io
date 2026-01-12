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

### 紧子集

{{< math-block type="definition" title="紧子集" label="compact-set">}}

$X$ 是一个拓扑空间，$A \subset X$, 称$A$在$X$中是紧的(compact)，或是$X$中的一个紧致子集(a compact set)，如果$A$在子空间拓扑中是紧的。

{{< /math-block >}}

{{< math-block type="theorem" title="Lemma: 紧子集" label="compact-set-lemma">}}

设$X$是一个拓扑空间，$A \subset X$，则$A$在$X$中是紧的，当且仅当任何由$X$中开集组成的、覆盖$A$的开覆盖，都存在一个有限子覆盖。

{{< /math-block >}}

{{< math-block type="theorem" title="Proposition" >}}

设$X$是一个拓扑空间且紧的，$Y$是拓扑空间，$f: X \to Y$连续，则
$$
f(X)在Y中是紧的
$$

*连续映射保持紧性

{{< /math-block >}}

{{< math-block type="proof" >}}

取任意一个 $f(X)$ 在 $Y$ 中的开覆盖 $\mathcal{O}$，即
$$
f(X)\subset \bigcup_{U\in\mathcal{O}} U,
$$
其中每个 $U$ 都是 $Y$ 中的开集。

由于 $f$ 连续，对任意 $U\in\mathcal{O}$，其原像 $f^{-1}(U)$ 是 $X$ 中的开集。于是
$$
\{,f^{-1}(U)\mid U\in\mathcal{O},\}
$$
是一族 $X$ 中的开集，并且它覆盖 $X$：对任意 $x\in X$，有 $f(x)\in f(X)\subset \bigcup_{U\in\mathcal{O}}U$，因此存在某个 $U\in\mathcal{O}$ 使得 $f(x)\in U$，从而 $x\in f^{-1}(U)$。故
$$
X\subset \bigcup_{U\in\mathcal{O}} f^{-1}(U).
$$

因为 $X$ 紧，上述开覆盖存在有限子覆盖：存在 $U_1,\dots,U_n\in\mathcal{O}$，使得
$$
X=\bigcup_{i=1}^n f^{-1}(U_i).
$$

两边取 $f$ 的像，得
$$
f(X)=f!\left(\bigcup_{i=1}^n f^{-1}(U_i)\right)
= \bigcup_{i=1}^n f\bigl(f^{-1}(U_i)\bigr)
\subset \bigcup_{i=1}^n U_i.
$$
所以 $U_1,\dots,U_n$ 是 $\mathcal{O}$ 的一个有限子覆盖。

因此，任意 $f(X)$ 的开覆盖都有有限子覆盖，说明 $f(X)$ 在 $Y$ 中紧.

{{< /math-block >}}

{{< math-block type="theorem" title="Corollary">}}

$X_1, X_2$是拓扑空间，$X_1 \cong X_2$，则$X_1$是紧的$\Longleftrightarrow$ $X_2$是紧的

{{< /math-block >}}

### 几个性质

- **紧空间**上的**闭子集**是**紧的**
- **Hausdorff空间**的**紧子集**是**闭的**
- **紧且 Hausdorff** 的拓扑空间中，一个子集当且仅当它是**闭集**时才是**紧的**。

{{< math-block type="theorem" >}}

设 $X$ 是一个**紧致（compact）**拓扑空间，$Y$ 是一个 **Hausdorff** 拓扑空间。  
若映射
$$
f: X \to Y
$$
是**连续的双射**，则 $f$ 是一个**同胚（homeomorphism）**。

{{< /math-block >}}

{{< math-block type="proof" >}}

要证明 $f$ 是同胚，只需证明 $f^{-1}$ 连续。  
等价地，只需证明 $f$ 是一个**闭映射**。

设 $C \subset X$ 是闭集。

因为 $X$ 紧，且 $C$ 是 $X$ 的闭子集，所以  
$$
C \text{ 在 } X \text{ 中是紧的。}
$$

由于 $f$ 连续，紧集在连续映射下的像仍然紧，因此  
$$
f(C) \text{ 在 } Y \text{ 中是紧的。}
$$

又因为 $Y$ 是 Hausdorff 空间，紧集在 Hausdorff 空间中必为闭集，所以  
$$
f(C) \text{ 在 } Y \text{ 中是闭的。}
$$

因此，$f$ 将任意闭集映为闭集，即 $f$ 是闭映射。

结合 $f$ 连续且为双射，可得 $f^{-1}$ 连续，从而 $f$ 是同胚。

{{< /math-block >}}

{{< math-block type="theorem" >}}

设 $X$ 是一个**紧致（compact）**拓扑空间，$Y$ 是一个 **Hausdorff** 拓扑空间。  
若映射
$$
f: X \to Y
$$
是**连续且单射（injective）**的，则 $f$ 是一个**嵌入（embedding）**。

{{< /math-block >}}

{{< math-block type="proof" >}}

要证明 $f$ 是嵌入，只需证明
$$
f: X \to f(X)
$$
是一个同胚。

由于 $f$ 是连续的双射，从 $X$ 到 $f(X)$，且 $f(X)$ 作为 $Y$ 的子空间仍是 Hausdorff 空间，因此只需证明 $f$ 是闭映射。

设 $C \subset X$ 是闭集。

因为 $X$ 紧，且 $C$ 是 $X$ 的闭子集，所以
$$
C \text{ 在 } X \text{ 中是紧的。}
$$

由于 $f$ 连续，紧集在连续映射下的像仍然紧，因此
$$
f(C) \text{ 在 } f(X) \text{ 中是紧的。}
$$

又因为 $f(X)$ 是 Hausdorff 空间，紧集在 Hausdorff 空间中必为闭集，所以
$$
f(C) \text{ 在 } f(X) \text{ 中是闭的。}
$$

因此，$f$ 将任意闭集映为闭集，即
$$
f: X \to f(X)
$$
是闭映射。

结合 $f$ 连续且为双射，可得其逆映射连续，从而
$$
f: X \to f(X)
$$
是同胚。

因此 $f$ 是一个嵌入。

{{< /math-block >}}

{{< math-block type="theorem" >}}

设 $X$ 是一个 **Hausdorff** 拓扑空间，$\{C_\lambda\}_{\lambda\in\Lambda}$ 是 $X$ 中的一族**紧子集**。  
则
$$
\bigcap_{\lambda\in\Lambda} C_\lambda
$$
在 $X$ 中是**紧的**。

{{< /math-block >}}

{{< math-block type="proof" >}}

由于 $X$ 是 Hausdorff 空间，而每个 $C_\lambda$ 都是紧的，因此
$$
C_\lambda \text{ 在 } X \text{ 中是闭集。}
$$

于是有
$$
\bigcap_{\lambda\in\Lambda} C_\lambda
$$
是 $X$ 中闭集的交，因此仍是闭集。

任取某个固定的 $\lambda_0 \in \Lambda$，显然有
$$
\bigcap_{\lambda\in\Lambda} C_\lambda \subset C_{\lambda_0}.
$$

由于 $C_{\lambda_0}$ 是紧空间，而
$$
\bigcap_{\lambda\in\Lambda} C_\lambda
$$
是 $C_{\lambda_0}$ 中的闭子集，所以
$$
\bigcap_{\lambda\in\Lambda} C_\lambda
$$
在 $C_{\lambda_0}$ 中是紧的。

而紧性在子空间意义下保持，因此
$$
\bigcap_{\lambda\in\Lambda} C_\lambda
$$
在 $X$ 中也是紧的。

{{< /math-block >}}

{{< math-block type="theorem" >}}

设 $X,Y$ 是拓扑空间，则
$$
X \times Y \text{ 是紧的 } \Longleftrightarrow X \text{ 和 } Y \text{ 都是紧的。}
$$

{{< /math-block >}}

{{< math-block type="proof" >}}

$\Rightarrow$:

设
$$
X \times Y \text{ 是紧的。}
$$
考虑投影映射
$$
\pi_1: X \times Y \to X,\quad (x,y)\mapsto x,
$$
$$
\pi_2: X \times Y \to Y,\quad (x,y)\mapsto y.
$$
显然 $\pi_1,\pi_2$ 都是连续且满射。

由于紧集在连续映射下的像仍然是紧的，因此
$$
X=\pi_1(X\times Y),\quad Y=\pi_2(X\times Y)
$$
都是紧的。

---

$\Leftarrow$:

现在设
$$
X \text{ 和 } Y \text{ 都是紧的。}
$$
令 $\mathcal{O}$ 是 $X\times Y$ 的一个开覆盖。

**第一步：固定 $x\in X$，构造 $W_x$**

由于
$$
\{x\}\times Y
$$
与 $Y$ 同胚，因此是紧的。于是存在有限个开集
$$
W_x \subset \mathcal{O}
$$
使得
$$
\{x\}\times Y \subset \bigcup W_x.
$$

对任意 $y\in Y$，因为 $(x,y)\in \bigcup W_x$，存在
$$
U_y \times V_y \subset W_x
$$
使得
$$
(x,y)\in U_y \times V_y,
$$
其中 $U_y$ 是 $X$ 中 $x$ 的邻域，$V_y$ 是 $Y$ 中 $y$ 的邻域。

由于
$$
\{V_y \mid y\in Y\}
$$
是 $Y$ 的一个开覆盖，而 $Y$ 紧，存在有限子覆盖
$$
Y=\bigcup_{j=1}^n V_{y_j}.
$$

令
$$
R_x=\bigcap_{j=1}^n U_{y_j},
$$
则 $R_x$ 是 $X$ 中的开集，且 $x\in R_x$。

并且有
$$
R_x \times Y \subset \bigcup W_x.
$$

---

**第二步：利用 $X$ 的紧性**

由上述构造，
$$
\{R_x \mid x\in X\}
$$
是 $X$ 的一个开覆盖。由于 $X$ 紧，存在有限个点
$$
x_1,\dots,x_m \in X
$$
使得
$$
X=\bigcup_{i=1}^m R_{x_i}.
$$

于是
$$
X\times Y
= \left(\bigcup_{i=1}^m R_{x_i}\right)\times Y
= \bigcup_{i=1}^m (R_{x_i}\times Y)
\subset \bigcup_{i=1}^m \bigcup W_{x_i}.
$$

右端是 $\mathcal{O}$ 的有限子集的并，因此 $\mathcal{O}$ 存在有限子覆盖。

---

由紧性的定义可知
$$
X\times Y \text{ 是紧的。}
$$

{{< /math-block >}}

{{< math-block type="theorem" title="Corollary">}}

设 $X_i$ 是拓扑空间，$i=1,2,\dots,n$。则
$$
X_1 \times X_2 \times \cdots \times X_n \text{ 是紧的}
$$
当且仅当
$$
X_i \text{ 是紧的}, \quad \forall\, i=1,2,\dots,n.
$$

{{< /math-block >}}

## Lebesgue引理

{{< math-block type="theorem" title="Lebesgue引理">}}

设 $(X,d)$ 是一个**紧致度量空间**，$\mathcal O$ 是 $X$ 的一个**开覆盖**。  
则存在一个常数
$$
\varepsilon > 0
$$
使得对任意 $x\in X$，都存在某个 $U\in\mathcal O$，满足
$$
B(x,\varepsilon)\subset U.
$$

---

**备注（Remark）**
这里的 $\varepsilon$ 只依赖于 $(X,d)$ 和开覆盖 $\mathcal O$，  
**与具体点 $x\in X$ 无关**。

该常数 $\varepsilon$ 称为 **Lebesgue 数（Lebesgue constant / Lebesgue number）**。

{{< /math-block >}}

## 一点紧致化

{{< math-block type="definition" title="Locally compact" label="local-cmpc>}}

设 $X$ 是一个拓扑空间。称 $X$ 是**局部紧的（locally compact）**，如果对任意 $x\in X$，存在一个**紧子集** $C\subset X$，使得
$$
x \in \operatorname{int}(C).
$$

等价地，$X$ 是局部紧的，当且仅当：

对任意 $x\in X$，存在一个开集 $U$ 和一个紧集 $C$，使得
$$
x \in U \subset C.
$$

{{< /math-block >}}

> 所有紧空间都是局部紧的；
> $E^n$是局部紧的，$\forall x \in E^n$，$C=B(x,1), U=B(x,1)$

{{< math-block type="theorem" title="Alexandroff 一点紧致化">}}

设 $(X,\mathcal T)$ 是一个 **Hausdorff** 拓扑空间，取一点 $\infty\notin X$，令
$$
Y = X \cup \{\infty\}.
$$
定义 $Y$ 上的拓扑
$$
\mathcal T_\infty
= \mathcal T \,\cup\, \{\,Y\setminus C \mid C \text{ 是 } X \text{ 中的紧子集}\,\}.
$$

则有以下结论：

(1) $(Y,\mathcal T_\infty)$ 是一个拓扑空间

(2) $X$ 从 $(Y,\mathcal T_\infty)$ 继承的子空间拓扑与原拓扑一致，即
$$
(\mathcal T_\infty)_X = \mathcal T.
$$

(3) $(Y,\mathcal T_\infty)$ 是紧的

(4) 若 $(X,\mathcal T)$ 是**局部紧的**，则 $(Y,\mathcal T_\infty)$ 是 **Hausdorff** 空间

(5) 若 $(X,\mathcal T)$ 是**非紧的**，则
$$
X \subsetneq Y,
$$
即新加入的一点 $\infty$ 不是多余的

---

## 备注（Remark）

该构造称为 **一点紧化（one-point compactification）** 或 **Alexandroff 紧化**。  
当 $X$ 是局部紧 Hausdorff 空间时，$(Y,\mathcal T_\infty)$ 是一个 **紧 Hausdorff 空间**，且 $X$ 是 $Y$ 的一个稠密开子空间。

{{< /math-block >}}
