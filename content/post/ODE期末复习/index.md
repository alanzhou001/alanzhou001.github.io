---
title: ODE期末复习
description: SJTU MATH2501期末定理与公式整理
slug: hello-world
date: 2025-06-22 20:14:00+0800
math: true
categories:
    - Math
tags:
    - ODE
    - notes
---
#　线性方程

## 齐次线性微分方程组

- 形式：
  $$
  \frac{d\mathbf{x}}{dt}=\mathbf{A}(t)\mathbf{x}
  $$

- 通解：
  $$
  \mathbf{x}(t)=\mathbf{X}(t)\mathbf{c}
  $$

  - $\mathbf{X}(t)$是基解矩阵，判断基解矩阵（线性无关）充要条件：

    $det(\mathbf{X}(t))$恒不为零$\iff$$\exist t_0, det(\mathbf{X}(t))=det(\mathbf{X}(t_0))exp(\int_{t_0}^t tr(\mathbf{A}(\tau)d\tau) \neq 0$

  - 叠加原理（解的线性组合还是解）

## 非齐次线性微分方程组

- 形式：
  $$
  \frac{d\mathbf{x}}{dt}=\mathbf{A}(t)\mathbf{x}+\mathbf{f}(t)
  $$

- 通解：
  $$
  \mathbf{x}(t)=\mathbf{X}(t)\mathbf{c}+\mathbf{x}^*(t)
  $$

  - $\mathbf{x}^*(t)$通过常数变易法求得，
    $$
    \mathbf{x}^*(t)=\mathbf{X}(t)\int_{t_0}^{t}\mathbf{X}^{-1}(\tau)\mathbf{f}(\tau)d\tau
    $$

## 高阶线性微分方程

- 形式：
  $$
  \frac{d^n x}{dt^n}+a_1(t)\frac{d^{n-1} x}{dt^{n-1}}+\cdots+a_n(t)x=f(t)
  $$
  升维降阶：

  令
  $$
  x_1=x, x_2=\frac{dx}{dt}, \cdots, x_n=\frac{d^{n-1} x}{dt^{n-1}}
  $$
  转换为一阶线性微分方程组
  $$
  \frac{d\mathbf{x}}{dt}=\mathbf{A}(t)\mathbf{x}+\mathbf{f}(t)
  $$
  其中
  $$
  \mathbf{A}(t)=\left( \begin{matrix}
  0 & 1 & 0 & \cdots & 0 \\
  0 & 0 & 1 & \cdots & 0 \\
  \vdots & \vdots & \vdots & \vdots & \vdots \\
  0 & 0 & 0 & \cdots & 1 \\
  -a_n(t) & -a_{n-1}(t) & -a_{n-2}(t) & \cdots & -a_1(t) \\
  \end{matrix}\right),
  $$

  $$
  \mathbf{f}(t)=\left(\begin{matrix}
  0 \\
  0 \\
  \vdots \\
  0 \\
  f(t)
  \end{matrix}\right),  \mathbf{x}=\left(\begin{matrix}
  x_1 \\
  x_2 \\
  \vdots \\
  x_{n-1} \\
  x_n
  \end{matrix}\right)
  $$

  对应基解矩阵第一行即为原方程的n个线性无关解，同理，原方程的n个线性无关解通过求导可得基解矩阵.

- 判断基解矩阵（线性无关）充要条件：

  $W(t)=det(\mathbf{X}(t))$恒不为零$\iff$$\exist t_0, W(t)=W(t_0)exp(\int_{t_0}^t tr(\mathbf{A}(\tau)d\tau)=W(t_0)exp(\int_{t_0}^t -a_1(\tau)d\tau) \neq 0$

- 一个特例：
  $$
  \frac{d^2x}{dt^2}+a_1(t)\frac{dx}{dt}+a_2(t)x=0
  $$
  已知一个非零解$x_1(t)$，通解为
  $$
  x(t)=x_1(t)(C_2+C_1\int\frac{1}{x_1^2(t)}e^{-\int a_1(t)dt}dt)
  $$

## 复值解

- 复值线性方程组
  $$
  \frac{d\mathbf{z}}{dt}=\mathbf{A}(t)\mathbf{z}+\mathbf{f}(t)
  $$
  其中
  $$
  \mathbf{z}(t)=\mathbf{x}(t)+i\mathbf{y}(t),  \newline 
  \mathbf{A}(t)=\mathbf{A}_R(t)+i\mathbf{A}_I(t),  \newline 
  \mathbf{f}(t)=\mathbf{f}_R(t)+i\mathbf{f}_I(t).
  $$
  等价于实方程组
  $$
  \frac{d}{dt}\left(\begin{matrix} \mathbf{x} \\ \mathbf{y} \end{matrix}\right)=\left(\begin{matrix} \mathbf{A}_R(t) & -\mathbf{A}_I(t) \\ \mathbf{A}_I(t) & \mathbf{A}_R(t) \end{matrix}\right)\left(\begin{matrix} \mathbf{x} \\ \mathbf{y} \end{matrix}\right)+\left(\begin{matrix} \mathbf{f}_R(t) \\ \mathbf{f}_I(t) \end{matrix}\right)
  $$
  

# 常系数线性方程

## 微分算子处理常系数高阶线性方程

- $\frac{d^n x}{dt^n}+a_1\frac{d^{n-1} x}{dt^{n-1}}+\cdots+a_nx=f(t)$

- 微分算子: $D=\frac{d}{dt}$, $D^n=\frac{d^n}{dt^n}$
- 方程可化为算子形式：$P(D)x=f(t)$, $P(D)\overset{def}{=}D^n+a_1D^{n-1}+\cdots+a_{n-1}D+a_n$

### 齐次问题

- **欧拉待定指数函数法**：寻找形如$x(t)=e^{\lambda t}$的解

- 步骤：

  1. 求解特征方程：
     $$
     P(\lambda)=\lambda^n+a_1\lambda^{n-1}+\cdots+a_{n-1}\lambda+a_n=0
     $$

  2. 设有$r$个互异的实特征根$\lambda_1, \lambda_2 \cdots, \lambda_r$，$l$对互异的复特征根$\alpha_1\pm i\beta_1, \alpha_2\pm i\beta_2, \cdots, \alpha_l\pm i\beta_l$，重数分别为$n_1, n_2, \cdots, n_r$和$m_1, m_2, \cdots, m_l$

  3. 基本解组如下：
     $$
     e^{\lambda_k t},\space te^{\lambda_k t},\space \cdots,\space t^{n_k-1}e^{\lambda_k t}\space\space\space\space (k=1,2,\cdots,r),\newline
     e^{\alpha_jt}cos\beta_jt,\space te^{\alpha_jt}cos\beta_jt,\space \cdots,\space t^{m_j-1}e^{\alpha_jt}cos\beta_jt \space\space\space\space (j=1,2,\cdots,l),\newline
     e^{\alpha_jt}sin\beta_jt,\space te^{\alpha_jt}sin\beta_jt,\space \cdots,\space t^{m_j-1}e^{\alpha_jt}sin\beta_jt \space\space\space\space (j=1,2,\cdots,l)
     $$

### 非齐次问题

求出一个特解

- 算子解法
  $$
  x^*(t)=\frac{1}{P(D)}f(t)
  $$

- 具体算法：

  - 解析法：对$k$次多项式$f_k(t)$，若$\frac{1}{P(x)}$在$x=0$处解析，且可（泰勒）展开为
    $$
    \frac{1}{P(x)}=Q_k(x)+H_k(x)
    $$
    其中$Q_K(x)$为$k$次多项式，$H_k(x)$为$k+1$次以上高阶项，

    有
    $$
    \frac{1}{P(D)}f_k(t)=Q_k(D)f_k(t)
    $$
    (泰勒公式：$f(0)+\frac{f\prime(0)}{1!}x+\cdots+\frac{f^{(n)}(0)}{n!}x^n+\cdots$)

  - 代换法：

    要求$P(\lambda)\neq0$，$\frac{1}{P(D)}e^{\lambda t}=\frac{1}{P(\lambda)}e^{\lambda t}$

  - 二项式法：

    $\frac{1}{P(D)}e^{\lambda t}v(t)=e^{\lambda t}\frac{1}{P(D+\lambda)}v(t)$

    常用技巧：$v(t)=1$

## 常系数线性方程组

$$
\frac{d}{dt}\left(\begin{matrix}x_1 \\ \vdots \\ x_n \end{matrix}\right)=\left(\begin{matrix}a_{11} & \cdots & a_{1n} \\ \vdots && \vdots \\ a_{n1} & \cdots & a_{nn} \end{matrix}\right)\left(\begin{matrix}x_1 \\ \vdots \\ x_n \end{matrix}\right)+\left(\begin{matrix}f_1(t) \\ \vdots \\ f_n(t) \end{matrix}\right)
$$

通解形式：
$$
\mathbf{x}(t)=e^{t\mathbf{A}}\mathbf{c}+e^{t\mathbf{A}}\int_{t_0}^te^{-s\mathbf{A}}\mathbf{f}(s)ds
$$

- 求解$e^{t\mathbf{A}}$：

  - 借助$Jordan$标准型

  - 求$Jordan$链：

    1. 求解$\mathbf{A}$的特征值$\lambda_1, \lambda_2, \cdots, \lambda_s$，重数分别为$n_1, n_2, \cdots, n_s$

    2. 对于$\lambda_i, i=1,2,\cdots, s$求解广义特征向量：
       $$
       (\mathbf{A}-\lambda_i\mathbf{I})^{n_i}\mathbf{\gamma}=\mathbf{0}
       $$
       有$n_i$个线性无关的广义特征向量，$\gamma_1^{(i)}, \gamma_2^{(i)}, \cdots, \gamma_{n_i}^{(i)}$

    3. 对于每一个广义特征向量$\gamma_j^{(i)}, j=1,2,\cdots, n_i; i=1,2,\cdots, s$，求得对应的$Jordan$链：
       $$
       \gamma_{j,0}^{(i)}=\gamma_j^{(i)}, \newline
       \gamma_{j,1}^{(i)}=(\mathbf{A}-\lambda_i\mathbf{I})\gamma_{j,0}^{(i)}, \newline
       \cdots \newline
       \gamma_{j,n_1-1}^{(i)}=(\mathbf{A}-\lambda_i\mathbf{I})\gamma_{j,n_i-2}^{(i)}, \newline
       $$

    4. 对应基解矩阵中的一列：
       $$
       e^{\lambda_i t}[\gamma_{j,0}^{(i)}+\frac{t}{1!}\gamma_{j,1}^{(i)}+\cdots+\frac{t^{n_i-1}}{(n_i-1)!}\gamma_{j,n_i-1}^{(i)}]
       $$

    5. 组装即得基解矩阵

    6. 如有复根，直接取实部即可（欧拉公式：$e^{it}=cost+isint$)

# 动力系统

- 动力系统概念
  $$
  \frac{d\mathbf{x}}{dt}=\mathbf{f}(\mathbf{x})
  $$
  右端函数只与$\mathbf{x}$有关

- **平衡点/奇点**：从该点出发的轨道一直驻留在该点，对应一个定常解$\mathbf{x}(t)\equiv\mathbf{x}_0$

- **闭轨/周期轨**

## Lyapunov稳定性

- 各种稳定性的定义：张伟年p162-163

- 判别
  $$
  \frac{d\mathbf{x}}{dt}=\mathbf{A}\mathbf{x}
  $$
  的零解稳定性情况，若有段函数有高阶部分，判断高阶部分是否满足：
  $$
  \mathbf{R}(t,\mathbf{0})\equiv\mathbf{0}, \lim_{\|\mathbf{x}\| \to \mathbf{0}} 
  \frac{\|\mathbf{R}(t, \mathbf{x})\|}{\|\mathbf{x}\|} = 0
  $$
  若满足则可只考察线性部分.

  - 渐近稳定：当且仅当$\mathbf{A}$的全部特征值实部均为负数
  - 稳定：当且仅当$\mathbf{A}$的全部特征值实部均为非正数，且实部为零的特征值对应的$Jordan$块都是一阶
  - 不稳定：当且仅当$\mathbf{A}$的特征值至少一个实部为正，或至少一个实部为零的特征值对应的$Jordan$块大于一阶

## Lyapunov直接法

构造Lyapunov函数，满足函数定正（至少在一个邻域内）

- 稳定：导数常负
- 渐近稳定：导数定 负
- 不稳定：导数定正

##　平衡点分析

只考虑平面自治系统：
$$
\frac{dx}{dt}=X(x, y), \frac{dy}{dt}=Y(x, y)
$$
平衡点：$X(x,y)=0, Y(x,y)=0$

分析步骤：
$$
\frac{dx}{dt}=ax+by, \frac{dy}{dt}=cx+dy, \newline
\frac{d}{dt}\left(\begin{matrix}x \\ y\end{matrix}\right)=\mathbf{A}\left(\begin{matrix}x \\ y\end{matrix}\right)
$$


1. 通过可逆变换，原方程组变为
   $$
   \frac{d}{dt}\left(\begin{matrix}u \\ v\end{matrix}\right)=\mathbf{J}\left(\begin{matrix}u \\ v\end{matrix}\right)
   $$
   $\mathbf{J}=\mathbf{P^{-1}AP}$

   其中$\mathbf{J}$有三种形式：
   $$
   \left(\begin{matrix}
   \lambda & 0 \\
   0 & \mu \\
   \end{matrix}\right), \left(\begin{matrix}
   \lambda & 0 \\
   1 & \lambda \\
   \end{matrix}\right), \left(\begin{matrix}
   \alpha & \beta \\
   -\beta & \alpha \\
   \end{matrix}\right)
   $$
   即分别对应矩阵$\mathbf{A}$有两个一重特征值，一个二重特征值和一对共轭复特征值

2. 分类讨论

   仅考虑非退化平衡点，$det(\mathbf{A})\neq0$

   1. 第一种

      1. $\lambda=\mu$

         $\lambda<0$, 渐近稳定；$\lambda>0$, 不稳定；

         同时平衡点附近轨道均为过原点直线，方向由$\lambda$正负决定；

         **星形结点/临界结点**

      2. $\lambda\neq\mu, \lambda\mu>0$

         均正，不稳定；均负，稳定；

         抛物线，谁的绝对值小就与对应的轴相切；

         **两向结点/正常结点**

      3. $\lambda\neq\mu, \lambda\mu<0$

         不稳定；

         $\lambda<0, \mu>0$, 渐近$v$轴;$\lambda>0, \mu<0$, 渐近$u$轴;（渐近正方向）

         **鞍点**

   2. 第二种

      **单向结点**

      1. $\lambda<0$

         渐近稳定；

         像正弦函数从两侧逼近原点；

      2. $\lambda>0$

         不稳定

         像负正弦函数向两侧远离原点；

   3. 第三种

      1. $\alpha\neq0$

         **焦点**

         螺旋线，$\beta$正顺负逆

         $\alpha>0$不稳定，$\alpha<0$渐近稳定

      2. $\alpha=0$

         **中心**

         同心圆

         稳定但不渐近稳定

   除**中心**以外的**初等平衡点**（非退化）称为**粗的**，其余为**细的**.

##　极限环

化为极坐标后讨论

转化方式类似首次积分中的方法：
$$
rr\prime=xx\prime+yy\prime, \newline
-r^2\theta\prime=yx\prime-xy\prime
$$

$$
\frac{d^2x}{dt}+2\mu\frac{dx}{dt}+x=f(t)
$$
$f(t)$是$T$-周期函数，$x(t)$是否存在$T$-周期解?（$\mu\geq1$）

判别
$$
\frac{d\mathbf{x}}{dt}=\mathbf{A}\mathbf{x}+\mathbf{f}(\mathbf{x})
$$
的零解稳定性情况是否与$\frac{d\mathbf{x}}{dt}=\mathbf{A}\mathbf{x}$一致，其中$\mathbf{f}(\mathbf{x})=O(x^2)$.
