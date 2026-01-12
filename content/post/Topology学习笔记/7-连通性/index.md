---
title: 连通性
description: 拓扑中连通性，道路连通，连通分支与道路连通分支
slug: topol-7
date: 2026-01-12 17:55:00+0800
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

## 连通空间

{{< math-block type="definition" title="Definition 4.1.1 连通空间" label="connecttedness">}}

设 $X$ 是一个拓扑空间。  
如果存在**非空且不交的开集** $U,V \subset X$，使得
$$
U \cap V = \varnothing,
\qquad
U \cup V = X,
$$
则称 $X$ 是**不连通的（disconnected）**，并称集合对
$$
\{U,V\}
$$
为 $X$ 的一个**分离（separation）**。

如果不存在这样的开集对，则称 $X$ 是**连通的（connected）**。

{{< /math-block >}}

e.g.
> 平凡拓扑的实数空间$$\mathbb{R}$$是连通的。
> **基为所有区间 $[a,b]$（$a<b$）** 的拓扑的实数集$$\mathbb{R}$$是不连通的。

{{< math-block type="theorem" >}}

设 $X$ 是一个拓扑空间，则
$$
X \text{ 不连通}
\;\Longleftrightarrow\;
\text{存在一个非空、既开又闭且真包含于 } X \text{ 的子集 } A \subset X.
$$

{{< /math-block >}}

{{< math-block type="proof" >}}

$\Rightarrow$:

若 $X$ 不连通，则存在一对分离
$$
U,V \subset X
$$
满足
$$
U \neq \varnothing,\quad V \neq \varnothing,\quad
U \cap V = \varnothing,\quad
U \cup V = X.
$$
此时 $U$ 是开集，且
$$
U^c = V
$$
也是开集，因此 $U$ 同时是闭集。又因为 $U \neq \varnothing$ 且 $U \neq X$，所以 $U$ 是一个非空、既开又闭且真包含于 $X$ 的子集。

$\Leftarrow$:

反之，设存在
$$
A \subset X
$$
满足
$$
A \neq \varnothing,\quad A \neq X,
$$
且 $A$ 既是开集又是闭集。令
$$
V = X \setminus A,
$$
则 $V$ 也是非空开集，并且
$$
A \cap V = \varnothing,\qquad A \cup V = X.
$$
因此 $\{A,V\}$ 构成 $X$ 的一个分离，说明 $X$ 不连通。

{{< /math-block >}}

> 例：$\mathbb{E}^1$ 的连通性：

{{< math-block type="proof" >}}
设
$$
\mathbb{E}^1
$$
表示带通常拓扑的一维欧氏空间。假设反设其不连通，则存在一个非空、既开又闭且真包含的子集
$$
A \subset \mathbb{E}^1.
$$

取
$$
b \in A,\qquad (b,+\infty)\cap A \neq \varnothing,
$$
并定义
$$
d = \inf\{a \in A \mid a>b\}.
$$
由于 $A$ 在 $\mathbb{E}^1$ 中是闭集，可得
$$
d \in A.
$$
于是
$$
d>b,\qquad [b,d)\cap A = \varnothing,
$$
从而 $d$ 不是 $A$ 的内点，即
$$
d \notin \operatorname{int}(A).
$$
这与 $A$ 是开集矛盾。

因此假设不成立，$\mathbb{E}^1$ 必为连通空间。

{{< /math-block >}}

### 连通子集

{{< math-block type="definition" title="Definition 4.1.2" >}}

设 $X$ 是一个拓扑空间，$A \subset X$。  
称 $A$ **在 $X$ 中是连通的**（或称 $A$ 是 $X$ 的一个**连通子集**），如果 $A$ 在其**子空间拓扑**下是连通的。

也就是说，$A$ 在 $X$ 中连通，当且仅当不存在 $A$ 中的两个非空不交开集 $U,V$，使得
$$
U \cap V = \varnothing,
\qquad
U \cup V = A.
$$

{{< /math-block >}}

{{< math-block type="Lemma" >}}

设 $X$ 是一个拓扑空间，$A \subset X$。  
则 $A$ **在 $X$ 中不连通** 当且仅当存在 $X$ 中的开集 $U,V$，满足
$$
U \cap A \neq \varnothing,\qquad
V \cap A \neq \varnothing,
$$
$$
A \subset U \cup V,
$$
并且
$$
(U \cap A)\cap (V \cap A)=U\cap V\cap A=\varnothing.
$$

---

**说明（Separation）**
满足上述条件的开集对
$$
\{U,V\}
$$
称为 **$A$ 在 $X$ 中的一个分离（separation of $A$ in $X$）**。

---

**直观理解**
该引理说明：

- $A$ 在子空间拓扑下不连通  
  $\Longleftrightarrow$  
- 可以用 **$X$ 中的两个开集** 把 $A$ “撕开”，并且这两个开集在 $A$ 内分别截到两块非空、互不相交的部分。

这正是“子空间连通性”用 **母空间开集** 表述的等价刻画。

{{< /math-block >}}

{{< math-block type="theorem" >}}

设 $X,Y$ 是拓扑空间，映射
$$
f: X \to Y
$$
是连续的。若
$$
X \text{ 是连通的},
$$
则
$$
f(X) \text{ 在 } Y \text{ 中是连通的。}
$$

{{< /math-block >}}

{{< math-block type="proof" >}}

反设 $f(X)$ 在 $Y$ 中不连通。  
则存在一对分离 $\{U,V\}$，其中 $U,V$ 是 $Y$ 中的开集，满足
$$
U \cap f(X) \neq \varnothing,\qquad
V \cap f(X) \neq \varnothing,
$$
$$
U \cup V = f(X),\qquad
U \cap V \cap f(X) = \varnothing.
$$

由于 $f$ 连续，$f^{-1}(U)$ 与 $f^{-1}(V)$ 是 $X$ 中的开集。  
又因为
$$
U \cap f(X) \neq \varnothing,\qquad
V \cap f(X) \neq \varnothing,
$$
可得
$$
f^{-1}(U) \neq \varnothing,\qquad
f^{-1}(V) \neq \varnothing.
$$

并且
$$
f^{-1}(U) \cap f^{-1}(V)
= f^{-1}(U \cap V)
= \varnothing,
$$
以及
$$
f^{-1}(U) \cup f^{-1}(V)
= f^{-1}(U \cup V)
= f^{-1}(f(X))
= X.
$$

因此 $\{f^{-1}(U),f^{-1}(V)\}$ 构成 $X$ 的一个分离，这与 $X$ 连通矛盾。

故假设不成立，$f(X)$ 必为连通的。

{{< /math-block >}}

**性质：**连通性随同胚传递。

{{< math-block type="theorem" title="引理" >}}

设 $X$ 是一个拓扑空间，$A \subset B \subset X$。  
设 $\{U,V\}$ 是 $B$ 在 $X$ 中的一个分离，即
$$
U,V \text{ 在 } X \text{ 中是开集},\qquad
U \cap B \neq \varnothing,\quad V \cap B \neq \varnothing,
$$
$$
B \subset U \cup V,\qquad
U \cap V \cap B = \varnothing.
$$
若
$$
A \text{ 在 } X \text{ 中是连通的},
$$
则必有
$$
A \subset U \quad \text{或} \quad A \subset V.
$$

等价地，
$$
A \cap U = \varnothing \quad \text{或} \quad A \cap V = \varnothing.
$$

{{< /math-block >}}

{{< math-block type="proof" >}}

由于 $\{U,V\}$ 是 $B$ 在 $X$ 中的一个分离，有
$$
U \cap B \neq \varnothing,\quad V \cap B \neq \varnothing,
$$
$$
B \subset U \cup V,\qquad
U \cap V \cap B = \varnothing.
$$

反设
$$
A \cap U \neq \varnothing \quad \text{且} \quad A \cap V \neq \varnothing.
$$
由于 $U,V$ 在 $X$ 中是开集，$A \cap U$ 与 $A \cap V$ 在 $A$ 的子空间拓扑中是开集。

并且
$$
(A \cap U) \cap (A \cap V)
= A \cap (U \cap V)
\subset A \cap (U \cap V \cap B)
= \varnothing,
$$
同时
$$
A \subset B \subset U \cup V
\;\Longrightarrow\;
A = (A \cap U) \cup (A \cap V).
$$

于是 $\{A \cap U,\, A \cap V\}$ 构成 $A$ 在 $X$ 中的一个分离，这与
$$
A \text{ 在 } X \text{ 中连通}
$$
相矛盾。

因此反设不成立，只能有
$$
A \cap U = \varnothing \quad \text{或} \quad A \cap V = \varnothing.
$$

由 $B \subset U \cup V$ 立刻得到
$$
A \cap U = \varnothing \;\Longleftrightarrow\; A \subset V,
\qquad
A \cap V = \varnothing \;\Longleftrightarrow\; A \subset U.
$$

故结论成立。

{{< /math-block >}}

> 如果 $B$ 被 $U$ 和 $V$ “撕成两块”，而 $A$ 又是 $B$ 里的一个连通部分，那么 $A$ 不可能横跨这两块，只能完整地落在其中一侧。

{{< math-block type="theorem" title="命题" >}}

设 $X$ 是一个拓扑空间，$A \subset X$ 在 $X$ 中是连通的。  
若
$$
A \subset B \subset \overline{A},
$$
则
$$
B \text{ 在 } X \text{ 中是连通的。}
$$
特别地，
$$
\overline{A} \text{ 在 } X \text{ 中是连通的。}
$$

{{< /math-block >}}

{{< math-block type="proof" >}}

反设 $B$ 在 $X$ 中不连通。  
则存在 $B$ 在 $X$ 中的一个分离 $\{U,V\}$，其中 $U,V$ 是 $X$ 中的开集，满足
$$
U \cap B \neq \varnothing,\qquad
V \cap B \neq \varnothing,
$$
$$
B \subset U \cup V,\qquad
U \cap V \cap B = \varnothing.
$$

由于 $A \subset B$ 且 $A$ 在 $X$ 中是连通的，根据前述引理，必有
$$
A \subset U \quad \text{或} \quad A \subset V.
$$

不妨设
$$
A \subset V,
$$
等价地，
$$
A \cap U = \varnothing.
$$

由 $U \cap B \neq \varnothing$，可取
$$
x \in U \cap B.
$$
又因为
$$
B \subset \overline{A},
$$
所以
$$
x \in \overline{A}.
$$

但 $x \in U$，而 $U$ 是开集且
$$
U \cap A = \varnothing,
$$
这与 $x \in \overline{A}$ 矛盾。

因此假设不成立，$B$ 必为连通的。

特别地，取
$$
B = \overline{A},
$$
即可得 $\overline{A}$ 在 $X$ 中连通。

{{< /math-block >}}

> 连通集的“缝合能力”很强——只要一个集合 $B$ 被夹在 $A$ 与其闭包之间，就不可能把 $B$ 撕成两块；因此连通性在取闭包时保持不变。
> $\overline{A}=A \cup A'$，$B=A \cup \{some limit points of A \}$

{{< math-block type="theorem" title="引理" >}}

设 $X$ 是一个拓扑空间，$\{C_\lambda\}_{\lambda\in\Lambda}$ 是 $X$ 中的一族**连通子集**，并且满足
$$
\bigcap_{\lambda\in\Lambda} C_\lambda \neq \varnothing.
$$
则
$$
\bigcup_{\lambda\in\Lambda} C_\lambda
$$
在 $X$ 中是**连通的**。

{{< /math-block >}}

{{< math-block type="proof" >}}

反证，设
$$
\bigcup_{\lambda\in\Lambda} C_\lambda
$$
在 $X$ 中不连通。  
则存在 $X$ 中的开集 $U,V$，构成其一个分离，即
$$
U \cap \bigcup_{\lambda\in\Lambda} C_\lambda \neq \varnothing,\qquad
V \cap \bigcup_{\lambda\in\Lambda} C_\lambda \neq \varnothing,
$$
$$
\bigcup_{\lambda\in\Lambda} C_\lambda \subset U \cup V,
\qquad
U \cap V \cap \bigcup_{\lambda\in\Lambda} C_\lambda = \varnothing.
$$

由于每个 $C_\lambda$ 在 $X$ 中是连通的，根据前述关于连通子集的引理，对每个 $\lambda\in\Lambda$，必有
$$
C_\lambda \subset U \quad \text{或} \quad C_\lambda \subset V,
$$
等价地，
$$
C_\lambda \cap V = \varnothing \quad \text{或} \quad C_\lambda \cap U = \varnothing.
$$

取
$$
x \in \bigcap_{\lambda\in\Lambda} C_\lambda,
$$
该点存在是由假设保证的。  
由于
$$
x \in \bigcup_{\lambda\in\Lambda} C_\lambda \subset U \cup V,
$$
必有
$$
x \in U \quad \text{或} \quad x \in V.
$$

不妨设
$$
x \in U.
$$
则对任意 $\lambda\in\Lambda$，都有
$$
x \in C_\lambda \cap U,
$$
从而
$$
C_\lambda \cap U \neq \varnothing.
$$
因此不可能有 $C_\lambda \subset V$，只能是
$$
C_\lambda \subset U.
$$

于是得到
$$
\bigcup_{\lambda\in\Lambda} C_\lambda \subset U,
$$
从而
$$
\left(\bigcup_{\lambda\in\Lambda} C_\lambda\right) \cap V = \varnothing,
$$
这与
$$
V \cap \bigcup_{\lambda\in\Lambda} C_\lambda \neq \varnothing
$$
矛盾。

矛盾说明假设不成立，因此
$$
\bigcup_{\lambda\in\Lambda} C_\lambda
$$
在 $X$ 中是连通的。

{{< /math-block >}}

{{< math-block type="定理" >}}

设 $X,Y$ 是拓扑空间，则
$$
X \times Y \text{ 是连通的}
\;\Longleftrightarrow\;
X \text{ 和 } Y \text{ 都是连通的}.
$$

{{< /math-block >}}

{{< math-block type="proof" >}}

$\Rightarrow$：

设
$$
X \times Y \text{ 是连通的}.
$$
考虑投影映射
$$
\pi_1: X \times Y \to X,\quad (x,y)\mapsto x,
$$
$$
\pi_2: X \times Y \to Y,\quad (x,y)\mapsto y.
$$
显然 $\pi_1,\pi_2$ 都是**连续且满射**。

由于**连续映射保持连通性**，可得
$$
X = \pi_1(X \times Y),\qquad
Y = \pi_2(X \times Y)
$$
均为连通空间。

---

$\Leftarrow$：

现设
$$
X \text{ 和 } Y \text{ 都是连通的}.
$$
任取一点
$$
x_0 \in X.
$$

对任意 $y \in Y$，集合
$$
X \times \{y\}
$$
与 $X$ 同胚，因此是连通的。

定义
$$
C_y = (\{x_0\} \times Y)\ \cup\ (X \times \{y\}).
$$
由于
$$
(\{x_0\} \times Y) \cap (X \times \{y\})
= \{(x_0,y)\} \neq \varnothing,
$$
根据“**有公共点的连通集并仍连通**”的引理，得到
$$
C_y \text{ 是连通的}.
$$

注意到
$$
\bigcup_{y\in Y} C_y = X \times Y,
$$
且
$$
\bigcap_{y\in Y} C_y = \{x_0\} \times Y \neq \varnothing.
$$
再次应用同一引理，可知
$$
X \times Y
$$
是连通的。

---

综上，
$$
X \times Y \text{ 连通 } \Longleftrightarrow X \text{ 和 } Y \text{ 连通}.
$$

{{< /math-block >}}

## 连通分支

{{< math-block type="definition" title="Definition 4.1.3 连通分支" >}}

设 $X$ 是一个拓扑空间，$x,y\in X$。定义关系
$$
x \sim_c y
$$
当且仅当**存在 $X$ 的一个连通子集** $C_{x,y}$，使得
$$
x,y \in C_{x,y}.
$$

关系 $\sim_c$ 是 $X$ 上的一个**等价关系**，即满足：

1. 自反性：$$x \sim_c x.$$
2. 对称性：$$x \sim_c y \;\Longrightarrow\; y \sim_c x.$$
3. 传递性：若$$x \sim_c y \quad \text{且} \quad y \sim_c z,$$，则$$x \sim_c z.$$

---

由上述命题，$\sim_c$ 是一个等价关系。  
$\sim_c$ 的**等价类**称为 $X$ 的一个**连通分支**（或**连通分量**, connected component）。

---

备注（Remark）

(1)
任意一个连通子集都包含于某个连通分支中。

(2)
拓扑空间 $X$ 是连通的，当且仅当
$$
X \text{ 恰好只有一个连通分支}.
$$

{{< /math-block >}}

---

> **Lemma 1(连通性):** $X$的连通分支是连通的。
> **pf:** 取 $x_0 \in C$。根据连通分支的定义，对任意 $x \in C$，存在一个连通子集 $C_x \subset X$，使得$$x_0,\, x \in C_x.$$ 由连通分支的定义可知$$C_x \subset C.$$ 因此$$C = \bigcup_{x \in C} C_x.$$ 又注意到$$\bigcap_{x \in C} C_x \supset \{x_0\} \neq \varnothing. $$ 根据“**有公共点的连通子集的并仍连通**”这一引理，得到$$C \text{ 是连通的。}$$

---

> **Lemma 2(极大性):** 设 $C$ 是 $X$ 的一个连通分支，$A \subset X$ 在 $X$ 中连通，且$C \subset A.$则$A = C.$
> **pf:**只需证明 $A \subset C$。  任取$$x_0 \in C.$$由于 $A$ 连通且 $x_0 \in A$，对任意 $a \in A$，都有$$x_0 \sim_c a.$$由连通分支的定义可知$$a \in C.$$因此$$A \subset C.$$结合 $C \subset A$，得到$$A = C.$$

---

> **Lemma 3(闭性):** 设 $C$ 是 $X$ 的一个连通分支，则$C \text{ 在 } X \text{ 中是闭集。}$
> **pf:**由引理 1，$C$ 是连通的，因此其闭包$\overline{C}$也是连通的。显然有$C \subset \overline{C}.$而 $C$ 是连通分支，按定义它是**包含自身的最大连通子集**，因此只能有$\overline{C} = C.$从而$C \text{ 是闭集。}$

---

## 道路连通

{{< math-block type="definition" title="Definition 4.2.1 道路连通" label="compactness">}}

**Path：**

设 $X$ 是一个拓扑空间。  
称映射
$$
\alpha:[0,1]\to X
$$
为 $X$ 中的一条**路径（path）**，如果 $\alpha$ 是连续映射。

其中：
$$
\alpha(0) \quad \text{称为起点}, \qquad \alpha(1) \quad \text{称为终点}.
$$

注意：**路径不是仅仅指像集 $\alpha([0,1])$，而是包含参数化信息的映射本身。**

**Path connected：**

在拓扑空间 $X$ 中，若对任意
$$
x,y\in X,
$$
都存在一条路径
$$
\alpha:[0,1]\to X
$$
满足
$$
\alpha(0)=x,\qquad \alpha(1)=y,
$$
则称 $X$ 是**路径连通的（path connected）**。

**Path Connected Subset：**

设 $A\subset X$。  
若 $A$ 在其**子空间拓扑**下是路径连通的，则称 $A$ 是 $X$ 的一个**路径连通子集**。

{{< /math-block >}}

{{< math-block type="theorem" title="命题" >}}

$$
f:X\to Y
$$
是连续映射。  
若
$$
X \text{ 是路径连通的},
$$
则
$$
f(X) \text{ 在 } Y \text{ 中是路径连通的}.
$$

{{< /math-block >}}

{{< math-block type="proof" >}}

任取
$$
y_0,y_1\in f(X).
$$
则存在
$$
x_0,x_1\in X
$$
使得
$$
f(x_0)=y_0,\qquad f(x_1)=y_1.
$$

由于 $X$ 是路径连通的，存在一条路径
$$
\alpha:[0,1]\to X
$$
满足
$$
\alpha(0)=x_0,\qquad \alpha(1)=x_1.
$$

考虑复合映射
$$
f\circ\alpha:[0,1]\to Y.
$$
由于 $f$ 与 $\alpha$ 都连续，$f\circ\alpha$ 连续，且
$$
(f\circ\alpha)(0)=y_0,\qquad (f\circ\alpha)(1)=y_1.
$$

因此 $f\circ\alpha$ 是 $f(X)$ 中一条从 $y_0$ 到 $y_1$ 的路径，说明
$$
f(X) \text{ 是路径连通的}.
$$

{{< /math-block >}}

> 道路连通可被同胚传递

### 道路连通分支

{{< math-block type="definition" title="道路连通分支" >}}

设 $X$ 是一个拓扑空间，$x,y\in X$。  
定义关系
$$
x \sim_p y
$$
当且仅当**存在一条路径** $\alpha:[0,1]\to X$，使得
$$
\alpha(0)=x,\qquad \alpha(1)=y.
$$

关系 $\sim_p$ 是 $X$ 上的一个**等价关系**，即满足：
(i) 自反性：$x \sim_p x.$  
(ii) 对称性：$x \sim_p y \;\Longrightarrow\; y \sim_p x.$  
(iii) 传递性：若$x \sim_p y \quad\text{且}\quad y \sim_p z $，则$x \sim_p z.$

由上述命题，$\sim_p$ 是一个等价关系。  
$\sim_p$ 的等价类称为 $X$ 的一个**路径分支**（或**路径分量**, path component）。

{{< /math-block >}}

**备注（Remarks）**

1. 任意路径连通子集都包含于某一个路径分支中。
2. 拓扑空间 $X$ 是路径连通的，当且仅当$X \text{ 只有一个路径分支}.$
3. 每个路径分支一定是连通的，但一般而言$\text{连通分支} \;\supsetneq\; \text{路径分支}.$

**直观理解**

- $x\sim_p y$：可以**沿着一条连续轨迹**从 $x$ 走到 $y$；
- 路径分支是“能用连续路径走到一起的最大块”；
- 在 $\mathbb{R}^n$ 等良性空间中，路径分支与连通分支一致；
- 在病态空间中，二者可能不同（例如拓扑学家正弦曲线）。

> **Lemma 1(路径连通性):** 设 $X$ 是拓扑空间，$P$ 是 $X$ 的一个路径分支，则$P$是路径连通的.
> **Lemma 2(极大性 / 最大性):** 设 $P$ 是 $X$ 的一个路径分支，$A\subset X$ 是路径连通子集，且$ P\subset A.$ 则$A=P.$

### 连通（Connected）与路径连通（Path Connected）

{{< math-block type="theorem" >}}

若拓扑空间 $X$ 是**路径连通的**，则 $X$ 是**连通的**：
$$
\text{path connected} \;\Longrightarrow\; \text{connected}.
$$

{{< /math-block >}}

{{< math-block type="proof" >}}

反证，设 $X$ 是路径连通的，但 **不连通**。  
则存在 $X$ 的一个分离
$$
\{U,V\},
$$
满足
$$
U\neq\varnothing,\quad V\neq\varnothing,\quad
U\cap V=\varnothing,\quad
U\cup V=X,
$$
且 $U,V$ 都是 $X$ 中的开集。

取
$$
x\in U,\qquad y\in V.
$$
由于 $X$ 是路径连通的，存在一条路径
$$
a:[0,1]\to X
$$
使得
$$
a(0)=x,\qquad a(1)=y.
$$

考虑原像集合
$$
a^{-1}(U),\qquad a^{-1}(V).
$$
由于 $a$ 连续，$U,V$ 开，有
$$
a^{-1}(U),\ a^{-1}(V)\ \text{是 }[0,1]\text{ 中的开集}.
$$
并且
$$
0\in a^{-1}(U),\quad 1\in a^{-1}(V),
$$
所以
$$
a^{-1}(U)\neq\varnothing,\qquad a^{-1}(V)\neq\varnothing.
$$

又因为
$$
U\cap V=\varnothing,\quad U\cup V=X,
$$
得到
$$
a^{-1}(U)\cap a^{-1}(V)=\varnothing,
$$
$$
a^{-1}(U)\cup a^{-1}(V)=[0,1].
$$
因此
$$
\{a^{-1}(U),\,a^{-1}(V)\}
$$
构成了区间 $[0,1]$ 的一个分离。

但 $[0,1]$ 在通常拓扑下是**连通的**，不可能存在这样的分离，矛盾。

故假设不成立，从而
$$
X \text{ 连通}.
$$

{{< /math-block >}}

**存在拓扑空间是连通的，但不是路径连通的。**

- 反例：[拓扑学家的曲线](https://zh.wikipedia.org/wiki/%E6%8B%93%E6%89%91%E5%AD%A6%E5%AE%B6%E6%AD%A3%E5%BC%A6%E6%9B%B2%E7%BA%BF)

| 性质 | 含义 | 关系 |
|---|---|---|
| 连通 | 不能被分成两个不交的开集 | 较弱 |
| 路径连通 | 任意两点可由连续路径连接 | 较强 |
| 逻辑关系 |  | 路径连通 $\Rightarrow$ 连通 |
| 反例 |  | 拓扑学家正弦曲线 |

## 局部道路连通（Locally Path Connected）

{{< math-block type="definition" title="Definition 局部道路连通" >}}

设 $X$ 是一个拓扑空间。  
如果对任意
$$
x\in X
$$
以及 $x$ 的任意一个邻域
$$
U
$$
都存在一个**路径连通的邻域**
$$
V
$$
满足
$$
x\in V\subset U,
$$
则称 $X$ 是**局部路径连通的（locally path connected）**。

{{< /math-block >}}

{{< math-block type="theorem" >}}

设 $X$ 是一个拓扑空间。若
$$
X \text{ 连通且局部路径连通},
$$
则
$$
X \text{ 是路径连通的}.
$$

{{< /math-block >}}

{{< math-block type="proof" >}}

反证，设 $X$ **不是**路径连通的。  
则 $X$ 可分解为若干个互不相交的路径分支：
$$
X=\bigcup_{\lambda\in\Lambda} P_\lambda,
$$
其中每个 $P_\lambda$ 是 $X$ 的一个路径分支，并且
$$
|\Lambda|\ge 2.
$$

任选其中一个路径分支 $P_{\lambda_0}$。

---

第一步：$P_{\lambda_0}$ 是开集

任取
$$
x\in P_{\lambda_0}.
$$
由于 $X$ 是**局部路径连通的**，存在一个路径连通的邻域
$$
V
$$
满足
$$
x\in V.
$$
由于 $V$ 是路径连通的，并且 $x\in P_{\lambda_0}$，根据路径分支的极大性，必有
$$
V\subset P_{\lambda_0}.
$$
因此 $x$ 有一个包含于 $P_{\lambda_0}$ 的开邻域，从而
$$
P_{\lambda_0} \text{ 是开集}.
$$

---

第二步：$P_{\lambda_0}$ 是闭集

对任意 $\lambda\neq\lambda_0$，同理可知
$$
P_\lambda \text{ 是开集}.
$$
因此
$$
\bigcup_{\lambda\neq\lambda_0} P_\lambda
$$
是开集，而
$$
X\setminus P_{\lambda_0}=\bigcup_{\lambda\neq\lambda_0} P_\lambda.
$$
这说明
$$
P_{\lambda_0} \text{ 是闭集}.
$$

---

第三步：得到矛盾

由构造可知：
$$
P_{\lambda_0}\neq\varnothing,\qquad
P_{\lambda_0}\neq X,
$$
且 $P_{\lambda_0}$ 同时是
$$
\text{非空、开、闭、真子集}.
$$
这与
$$
X \text{ 是连通的}
$$
矛盾。

---

因此假设不成立，$X$ 必为路径连通空间。

{{< /math-block >}}

### 结论总结

一般情形下：
$$
\text{路径连通} \;\Longrightarrow\; \text{连通},
$$
但反向不成立；

**若额外假设局部路径连通性**，则
$$
\text{连通} \;\Longrightarrow\; \text{路径连通};
$$

因此在局部路径连通空间中：
$$
\text{连通} \iff \text{路径连通}.
$$
