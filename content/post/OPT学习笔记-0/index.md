---
title: OPT学习笔记-0
description: 简要介绍所需数学基础与基本概念
slug: opt-notes-0
date: 2025-06-23 20:00:00+0800
math: true
image: cover.jpg
categories:
    - OPT
tags:
    - notes
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

## Basic Definition

OPT is short for Optimization, and an optimization problem is defined as follow:

{{< math-block type="definition" title="Definition 0: optimization problem" label="def-opt">}}
$$
\min \space f(x) \\
s.t. \space x\in X
$$
where $f: \mathbb{R}^n \to \mathbb{R}$ is called the *objective function (决策函数)*, $x$ is the *decision variable (决策变量)*， and $X$ is the *feasible region (可行域)* . Moreover, $min$ for *minimize* and $s.t.$ for *subject to*.
{{< /math-block >}}

{{< math-block type="definition" title="Definition 1: 全局最优解及最优值 (global) optimal solution & optimal value" label="def-optimal">}}
$x^\*$ is an optimal solution of [1](#def-opt)
$iff. \space x^\* \in X, f(x^\*)\leq f(x), \forall x\in X$
where $f(x^\*)$ is the optimal value of [1](#def-opt).

Some special cases:

- *infeasible(不可行)：* $X = \emptyset$;
- *unbounded(无界)：*$(x^n)_{n=1}^{\infin}\in X$, $f(x^n)\to \infty$;
- *not achieved(无法取得):* not exist $ x^* \in X $, so that $ f(x^*)=inf\{f(x)|x\in X\} $
{{< /math-block >}}

{{< math-block type="definition" title="Definition 2: 局部极小值点" label="def-min">}}
$\bar{x}$ is a *local minimum(局部极小值点)* of function $f$, if there exists $\delta>0$ such that
$$f(\bar{x})\leq f(x), \forall x\in X, ||x-\bar{x}||_2<\delta$$
$\bar{x}$ is a *strict local minimum* of function $f$, if there exists $\delta>0$ such that
$$f(\bar{x})< f(x), \forall x\in X, ||x-\bar{x}||_2<\delta\space and\space x\neq \bar{x}$$
{{< /math-block >}}

## Mathematical Foundations

### Linear Algebra

1. The space $\mathbb{R}^n$
  A **vector** (or point) $x$ in $\mathbb{R}^n$ is an ordered collection of $n$ real numbers, which can be given as $x=(x_1,x_2,x_3,\cdots,x_n)$.

   - **scalar multiplication(数乘)** $a\in \mathbb{R}, x \in \mathbb{R}^n, ax=(ax_1,ax_2,\cdots,ax_n)$

   - **addition(向量加法)**

    $x\in\mathbb{R}^n, y\in\mathbb{R}^n, x+y=(x_1+y_1,x_2+y_2,\cdots,x_n+y_n)$

   - **linear subspace(线性子空间)**

    A nonempty subset $S$ of $\mathbb{R}^n$ is a *linear subspace* iff.
    $$
    x,y\in S, x+y\in S;x\in S,a\in \mathbb{R},ax\in S
    $$
    (对加法和数乘封闭)

   - **linear combinations(线性组合) & span(线性生成空间)**

     $$
     \mathcal{V}=\{v_1,v_2,\cdots,v_m\}\in \mathbb{R}^n, a_1,a_2,\cdots,a_m\in\mathbb{R}
     $$
     $\sum_{i=1}^ma_i\mathcal{v}_i$ is a *linear combination*;

     $$
     span(\mathcal{V}):=\{ a_1\mathcal{v}_1+a_2\mathcal{v}_2+\cdots+a_m\mathcal{v}_m|a_1,a_2,\cdots,a_m\in\mathbb{R} \}
     $$

   - **linear independent(线性无关) & linear dependent(线性相关)**

     *linear independent:* $v=a_1v_1+a_2v_2+\cdots+a_mv_m=\mathbf{0}$ iff. $a_1=a_2=\cdots=a_m=0$

     *linear dependent:* exists a non-zero ${a_k}$, such that $v=\mathbf{0}$.

   - **Basis(基)**

     $\mathcal{V}$ is a *basis* of linear subspace $S$ of $\mathbb{R}^n$, if $span(\mathcal{V})=S$ and $\mathcal{V}$ is linear independent 

   Some useful facts:

   1. The span of $\mathcal{V}$ is a linear subspace of $\mathbb{R}^n$;
   2. $\mathcal{V}$ is linear independent if and only if every $v\in span(\mathcal{V})$ can be uniquely represented as a linear combination of $\mathcal{V}$;
   3. $\mathcal{V}$ is linear independent. If $v\notin span(\mathcal{V})$ the $\mathcal{V}\cup v$ is linear independent;
   4. If $\mathcal{V}$ is linear dependent, there exists a nonzero vector $v\in\mathcal{V}$ such that $v\in span(\mathcal{V\backslash v}), span(\mathcal{V})=span(\mathcal{V\backslash v})$.

{{< math-block type="theorem" title="Theorem 1 (基扩充/缩减定理)" label="theo-basis">}}
Every linear independent subset of $\mathcal{V}$ can be extended to a basis of $span(\mathcal{V})$. The set of $\mathcal{V}$ can be reduced to a basis of $span(\mathcal{V})$.
{{< /math-block >}}

**(重复加入/减去线性无关向量直到构成基)**

{{< math-block type="theorem" title="Proposition 1" >}}
Let $\mathcal{W}$ be a vector space spanned by a finite set $\mathcal{V}$, i.e., $\mathcal{W}=span(\mathcal{V})$. Any linearly independent subset of $\mathcal{W}$ can be extended to form a basis for $\mathcal{W}$ .
{{< /math-block >}}

{{< math-block type="proof" >}}
Let $L=\{v_1,v_2,…,v_k\}$ be a linearly independent set of vectors in W. We want to find a set of vectors ${u_1,u_2,…,u_m}\subseteq \mathcal{V}$ such that the combined set $B=L∪\{u_1,…,u_m\}$ is a basis for $\mathcal{W}$ .

We proceed with the following algorithm:

1. **Check if** $L$ **spans** $\mathcal{W}$ .
   - If $span(L)=\mathcal{W}$, then $L$ is a linearly independent spanning set, which means $L$ is already a basis for $\mathcal{W}$. The proof is complete.

2. **If** $L$ **does not span**  $\mathcal{W}$ **.**
   - If $span(L)\neq\mathcal{W} $, then there must exist at least one vector in $\mathcal{W}$ that is not in the span of $L$. Since $\mathcal{W}=span(\mathcal{V})$, there must be a vector $u_1∈\mathcal{V}$ such that $u_1\notin span(\mathcal{V})$.
   - Let's form a new set $L_1=L∪\{u_1\}=\{v_1,…,v_k,u_1\}$. We claim this new set is also linearly independent.
   - To prove this, consider the equation: 
     $c_1v_1+c_2v_2+⋯+c_kv_k+d_1u_1=0$
   - Case 1: If $d1\neq 0$, we could rearrange the equation to express u1 as a linear combination of the vectors in $L$: 
     $u_1=−d_{11}(c_1v_1+⋯+c_kv_k)$
     This would imply that $u1\in span(L)$, which contradicts our choice of u1.
   - Case 2: Therefore, we must have $d_1=0$. The equation simplifies to: 
     $c_1v_1+c_2v_2+⋯+c_kv_k=0$
     Since $L$ is a linearly independent set, the only solution to this equation is $c_1=c_2=⋯+c_k=0$.
   - Thus, the only solution is that all coefficients ($c_i$ and $d_1$) are zero. This proves that the set $L_1$ is linearly independent.

3. **Repeat the process.**
   - We now repeat the procedure with $L_1$. If $span(L_1)=\mathcal{W}$, we have found our basis. If not, we find another vector $u_2\in V$ such that $u_2\notin span(L_1)$ and form the larger, linearly independent set $L_2=L_1∪\{u_2\}$.

Since W is spanned by a finite set V, it is a finite-dimensional space. Let $dim(\mathcal{W})=n$. Any linearly independent set in $\mathcal{W}$ can contain at most n vectors. Our process starts with a set of k vectors and adds one vector at a time, maintaining linear independence at each step. Therefore, the process is guaranteed to terminate in at most n−k steps, at which point we have a set $B$ that is linearly independent and spans $\mathcal{W}$. By definition, $B$ is a basis for $\mathcal{W}$ that contains the original set $L$.
{{< /math-block >}}

{{< math-block type="theorem" title="Proposition 2" >}}
Any finite set $\mathcal{V}$ that spans a vector space W can be reduced to a basis for $\mathcal{W}$ by removing some of its vectors.
{{< /math-block >}}

{{< math-block type="proof" >}}
Let $\mathcal{V}=\{v_1,v_2,\cdots,v_m\}$ be a set that spans $\mathcal{W}$, i.e., $\mathcal{W}=span(\mathcal{V})$. We want to find a subset $B\subseteq \mathcal{V}$ that is a basis for $\mathcal{W}$.

We can construct the basis $B$ using the following "sifting" algorithm:

1. Initialize an empty set, $B=\empty$.
2. Iterate through each vector $v_i$ in $\mathcal{V}$ for $i=1,\cdots,m$.
3. For each $v_i$, check if it is a linear combination of the vectors already in $B$. That is, check if $v_i\in span(B)$.
   - If **NO**, then $v_i$ is linearly independent of the vectors in $B$. Add $v_i$ to $B$.
   - If **YES**, then vi is a redundant vector (it depends linearly on other vectors). Discard $v_i$.

The final set $B$ produced by this algorithm is a basis for $\mathcal{W}$. We must prove two properties: that $B$ is linearly independent and that it spans $\mathcal{W}$.

- **Linear Independence:** By construction, a vector is only added to $B$ if it is not in the span of the vectors already in $B$. This condition directly ensures that the resulting set $B$ is linearly independent. If $B=\{b_1,\cdots,b_k\}$ were linearly dependent, then by the properties of linear dependence, some vector $b_j$ would be a linear combination of the preceding vectors, $b_j\in span(\{b_1,…,b_{j−1}\})$. But this contradicts the very rule we used to add $b_j$ to the set. Therefore, $B$ must be linearly independent.
- **Spanning Property:** We need to show that $span(B)=span(\mathcal{V})$.
  - Since $B\subseteq\mathcal{V}$, it is clear that $span(B)\subseteq span(V)$.
  - To show $span(V)\subseteq span(B)$, we must show that every vector $v_i\in \mathcal{V}$ is in $span(B)$.
    - If a vector $v_i$ was added to $B$, then $v_i∈B$, so it is trivially in $span(B)$.
    - If a vector $v_i$ was discarded, it was because at the moment of its consideration, it was already a linear combination of the vectors in the current version of $B$. Since the final set $B$ contains all these vectors, it follows that $v_i\in span(B)$.
  - Since every vector in the original spanning set $\mathcal{V}$ can be expressed as a linear combination of vectors in $B$, the span of $\mathcal{V}$ cannot be larger than the span of $B$. Thus, $span(\mathcal{V})\subseteq span(B)$.

Combining the two inclusions, we have $span(B)=span(\mathcal{V})=\mathcal{W}$.

Since $B$ is a linearly independent set that spans $\mathcal{W}$, it is a basis for $\mathcal{W}$.
{{< /math-block >}}

2. Euclidean inner product, Euclidean norm, orthogonal

{{< math-block type="definition" title="Definition 3: Euclidean inner product(欧氏内积)" label="def-product">}}
Given two vectors $x, y \in \mathbb{R}^n$, their **Euclidean inner product** is defined as  
$$
\langle x, y \rangle=\sum_{i=1}^n x_i y_i
$$
{{< /math-block >}}

{{< math-block type="theorem" title="Properties of the inner product" >}}
- **bi-linearity(双线性性):** when $\bar{x}$ is a fixed vector in $\mathbb{R}^n$, the function $<\bar{x}, y>$ is linear in variable $y$; when $\bar{y}$ is a fixed vector in $\mathbb{R}^n$, the function $<x, \bar{y}>$ is linear in variable $x$;
- **symmetry(对称性):** $<x, y>=<y, x>, \forall x, y \in \mathbb{R}^n$;
- **positive definiteness(正定性):** $\forall x \in \mathbb{R}^n, <x, x>\geq 0$, and is zero $iff. x=\mathbf{0}$
{{< /math-block >}}

{{< math-block type="definition" title="Definition 4: Linear function" >}}
A function $f: \mathbb{R}^n \to \mathbb{R}$ is linear if for every $x,y\in \mathbb{R}^n$ and $\apha, \beta \in \mathbb{R}$
$$
f(\alpha x+ \beta y)=\alpha f(x)+ \beta f(y)
$$
{{< /math-block >}}

{{< math-block type="theorem" title="Theorem 2 (线性函数可由向量内积唯一表示)" label="theo-func" >}}
Let $<\cdot , \cdot>$ be the *Euclidean inner product* on $\mathbb{R}^n \to \mathbb{R}$.
- For every vector $a \in \mathbb{R}^n$, $<a,x>$ is a linear function from $\mathb{R}^n \to \mathbb{R}$,
- Let $f(x)$ be a linear function from $\mathb{R}^n \to \mathbb{R}$. Then, there exists a unique vector $a\in \mathbb{R}^n$ so that $f(x)=<a, x>$ for every $x\in \mathbb{R}^n$.
{{< /math-block >}}

{{< math-block type="proof" >}}
1. Let $f(x)=<a, x>$, for every $x, y\in \mathbb{R}^n$ and $\alpha, \beta \in \mathbb{R}$
  $$
  f(\alpha x+ \beta y)=\langle a, \alpha x+ \beta y \rangle \\
  =\alpha \langle a, x \rangle + \langle a, \beta y \rangle \\
  =\alpha f(x) + \beta f(y)
  $$
  $f(x)$ is a linear function;
2. Let $f(x)$ be a linear function,
  $$
  f(x)=f(\sum x_ie_i) \\
  =\sum x_if(e_i) \\
  =\langle a, x \rangle
  $$
  in which $a=(f(e_1),\cdots,f(e_n))$.
{{< /math-block >}}

Extending Theorem 2 from scalar-valued linear functions $f: \mathbb{R}^n \to \mathbb{R}$ to vector-valued linear functions $f: \mathbb{R}^n \to \mathbb{R}^m$, we derive the following corollary:

{{< math-block type="theorem" title="Collary 3" label="coro-3" >}}
- Let $A$ be a $m \times n$ matrix whose row vectors are $a_1^T,\cdots,a_m^T$. Then, $Ax$ is a linear function from $\mathbb{R}^n \to \mathbb{R}^m$
- Let $f(x)$ be a linear function from $\mathbb{R}^n \to \mathbb{R}^m$. Then there exists a unique $m \times n$ matrix $A$ such that $f(x)=AX$.
{{< /math-block >}}
