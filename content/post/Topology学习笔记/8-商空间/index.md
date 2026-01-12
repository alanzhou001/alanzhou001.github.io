---
title: 商空间与商拓扑
description: 拓扑中商空间的定义与例子
slug: topol-8
date: 2026-01-12 22:50:00+0800
math: true
image: cover.jpg
categories:
    - Math
tags:
    - Topology
    - notes
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

封面画师：[竹嶋えく](https://x.com/wttb_tv/status/1990011971828359171)

## 商空间

{{< math-block type="definition" title="Definition 商空间" label="quotient-space">}}

设
$$
(X,\mathcal T)
$$
是一个拓扑空间，$\sim$ 是 $X$ 上的一个**等价关系**。

**商集**定义为
$$
X/\sim=\{[x]\mid x\in X\},
$$
其中
$$
[x]=\{y\in X\mid y\sim x\}
$$
是 $x$ 的等价类。

定义**自然映射（canonical map）**
$$
q:X\to X/\sim,\qquad x\mapsto [x].
$$

**商拓扑的定义：**
定义集合族
$$
\tilde{\mathcal T}
=\Bigl\{\,U\subset X/\sim \;\Big|\; q^{-1}(U)\text{ 在 }X\text{ 中是开集}\Bigr\}.
$$
则
$$
\tilde{\mathcal T}
$$
是 $X/\sim$ 上的一族拓扑，称为由 $q$ 诱导的**商拓扑（quotient topology）**。

赋予商拓扑 $\tilde{\mathcal T}$ 的集合
$$
(X/\sim,\tilde{\mathcal T})
$$
称为一个**商空间（quotient space）**。

自然映射
$$
q:X\to X/\sim
$$
称为**商映射（quotient map）**。

{{< /math-block >}}

**备注（Remark）**

1. 映射
$$
q:X\to X/\sim
$$
总是**满射**。

2. 对任意 $U\subset X/\sim$，
$$
U \text{ 在 } X/\sim \text{ 中是开集}
\;\Longleftrightarrow\;
q^{-1}(U) \text{ 在 } X \text{ 中是开集}.
$$

> $X/\sim$ 上的**商拓扑** $\tilde{\mathcal T}$ 是**使自然映射**
> $$q:X\to X/\sim$$
> **连续的最细（finest）拓扑**。

**证明:**
设 $\tilde{\mathcal T}'$ 是 $X/\sim$ 上的任意一个拓扑，并且
$$
q:(X,\mathcal T)\to (X/\sim,\tilde{\mathcal T}')
$$
是连续的。

由连续性的定义可知：  
对任意
$$
U\in \tilde{\mathcal T}',
$$
都有
$$
q^{-1}(U)\in \mathcal T.
$$

而根据商拓扑的定义，
$$
\tilde{\mathcal T}
=\{\,V\subset X/\sim \mid q^{-1}(V)\in\mathcal T\,\}.
$$
因此对每个 $U\in\tilde{\mathcal T}'$，必有
$$
U\in \tilde{\mathcal T}.
$$

于是得到
$$
\tilde{\mathcal T}' \subset \tilde{\mathcal T}.
$$

这表明：  
任何使 $q$ 连续的拓扑都不可能比 $\tilde{\mathcal T}$ 更细。

因此，$\tilde{\mathcal T}$ 正是 $X/\sim$ 上**使 $q$ 连续的最细拓扑**。

$$
\Box
$$

{{< math-block type="theorem" title="Lemma *" label="star">}}

设 $(X,\mathcal T)$ 是拓扑空间，$\sim$ 是 $X$ 上的等价关系，  
$q:X\to X/\sim$ 为自然映射，并赋予 $X/\sim$ **商拓扑**。

则 $q$ 是一个**商映射（quotient map）**，并且满足以下等价性：

对任意拓扑空间 $Z$ 及映射
$$
f:X/\sim \to Z,
$$
有
$$
f \text{ 连续 } \iff f\circ q:X\to Z \text{ 连续}.
$$

映射关系为
$$
X \xrightarrow{\,q\,} X/\sim \xrightarrow{\,f\,} Z,
$$
其中：

- $q$ 是商映射；
- **判断 $f$ 是否连续，只需判断 $f\circ q$ 是否连续**。

{{< /math-block >}}

{{< math-block type="proof" >}}

$\Rightarrow$:

若 $f$ 连续，而 $q$ 连续（这是商拓扑的定义性质），  
则连续映射的复合仍连续，因此
$$
f\circ q
$$
连续。

---

$\Leftarrow$:

假设
$$
f\circ q:X\to Z
$$
连续。

取任意开集
$$
V\subset Z.
$$
则
$$
(f\circ q)^{-1}(V)=q^{-1}\bigl(f^{-1}(V)\bigr)
$$
在 $X$ 中是开集。

根据**商拓扑的定义**：
$$
U\subset X/\sim \text{ 是开集 }
\iff
q^{-1}(U)\text{ 在 }X\text{ 中是开集},
$$
于是由
$$
q^{-1}\bigl(f^{-1}(V)\bigr)\text{ 在 }X\text{ 中开}
$$
可推出
$$
f^{-1}(V)\text{ 在 }X/\sim\text{ 中开}.
$$

由于 $V$ 是任意开集，这正是 $f$ 连续的定义。

因此
$$
f \text{ 连续}.
$$

{{< /math-block >}}

{{< math-block type="definition" title="Definition 商映射" label="quotient-map">}}

设 $X, Y$ 为拓扑空间。

若映射
$$
f : X \to Y
$$
满足以下条件：

1. **满射性**
$$
f \text{ 是满射（surjective）}
$$

2. **由逆像刻画开集（或闭集）**
对任意 $U \subset Y$，
$$
U \text{ 在 } Y \text{ 中是开集}
\quad \Longleftrightarrow \quad
f^{-1}(U) \text{ 在 } X \text{ 中是开集}.
$$
（等价地，也可以用闭集表述）

则称 $f$ 为一个 **商映射（quotient map）**。

注：[Lemma (*)](#star)在该抽象定义下仍然成立。

{{< /math-block >}}

> **Lemma:** 设$X, Y$是拓扑空间，$f:X \to Y$是一个商映射，在 $X$ 上定义一个等价关系 $\sim_f$，对任意 $x_1, x_2 \in X$，$x_1 \sim_f x_2\quad \Longleftrightarrow \quadf(x_1) = f(x_2).$ 则有$X / \sim_f \;\cong\; Y$。

{{< math-block type="theorem" >}}

设 $f:X\to Y$ 是满射且连续的映射。

1. 若 $f$ 是**开映射**，则 $f$ 是商映射；
2. 若 $f$ 是**闭映射**，则 $f$ 是商映射。

{{< /math-block >}}

{{< math-block type="proof" >}}

设 $U\subset Y$，且 $f^{-1}(U)$ 在 $X$ 中是开集。  
由于 $f$ 是开映射，$f(f^{-1}(U))$ 在 $Y$ 中是开集。  
又因为 $f$ 是满射，有
$$
f(f^{-1}(U)) = U .
$$
因此 $U$ 在 $Y$ 中是开集。  
由商映射的定义，$f$ 是商映射。

{{< /math-block >}}

{{< math-block type="theorem" >}}

设 $f:X\to Y$ 是满射且连续的映射。  
若 $X$ 是紧空间，$Y$ 是 Hausdorff 空间，则 $f$ 是商映射。

{{< /math-block >}}

{{< math-block type="proof" >}}

只需证明 $f$ 是闭映射。

设 $C\subset X$ 是闭集。由于 $X$ 紧，$C$ 也是紧集。  
由 $f$ 的连续性，$f(C)$ 是 $Y$ 中的紧集。  
又因为 $Y$ 是 Hausdorff 空间，紧集在 $Y$ 中必为闭集。

因此 $f$ 是闭映射，从而 $f$ 是商映射。

{{< /math-block >}}

{{< math-block type="theorem" >}}

设 $f:X\to Y$、$g:Y\to Z$ 都是商映射，则复合映射
$$
g\circ f : X\to Z
$$
也是商映射。

{{< /math-block >}}

{{< math-block type="proof" >}}

显然 $g\circ f$ 是满射且连续。

设 $U\subset Z$，且 $(g\circ f)^{-1}(U)$ 在 $X$ 中是开集。  
注意到
$$
(g\circ f)^{-1}(U)=f^{-1}(g^{-1}(U)).
$$
由于 $f$ 是商映射，可得 $g^{-1}(U)$ 在 $Y$ 中是开集；  
再由于 $g$ 是商映射，可得 $U$ 在 $Z$ 中是开集。

因此 $g\circ f$ 是商映射。

{{< /math-block >}}

1. 若 $f_1:X_1\to Y_1$、$f_2:X_2\to Y_2$ 都是商映射，则
$$
f_1\times f_2 : X_1\times X_2 \to Y_1\times Y_2
$$
**不一定**是商映射。

2. 若 $f:X\to Y$ 是商映射且 $X$ 是 Hausdorff 空间，  
则 $Y$ **不一定**是 Hausdorff 空间。

3. 商映射一般**不一定是开映射或闭映射**。

## 例子
