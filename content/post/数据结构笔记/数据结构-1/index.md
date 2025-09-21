---
title: 算法复杂度
description: 介绍算法的**时间复杂度**和**空间复杂度**，并结合Python代码示例进行说明
slug: datastructure-1
date: 2025-09-21 22:10:00+0800
math: true
image: cover.jpg
categories:
    - Data Structures
tags:
    - Algorithm - Data Structures
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

## 什么是算法复杂度？

算法复杂度是衡量算法效率的重要指标，主要分析算法运行时所需的资源，包括：

- **时间**：程序运行所需的时间，即**时间复杂度**。
- **空间**：程序运行所需占用的内存空间，即**空间复杂度**。

在评估算法效率时，关键在于算法本身的优劣。一个高效的算法能在处理大规模数据时，显著减少运行时间。

## 时间复杂度

### 概念与大O表示法

时间复杂度是一种抽象的度量，表示算法的**运算量**与**问题规模**之间的关系。它通常关注当问题规模变得非常大时，运行时间随问题规模增长的规律。

我们使用**大O表示法 (Big O Notation)** 来描述时间复杂度。它忽略具体的运行时间函数，只关注其**数量级**。

- 如果存在正的常数 $c$ 和 $n_0$，使得当 $n\geq n_0$ 时有 $T(n)\leq cf(n)$，则 $T(n)$ 是 $O(f(n))$。
- 计算大O表示法时，我们通常**忽略系数和低次项**，只保留运行时间函数中的**主导部分**。

**大O表示法实例：**

- $T(n)=1000⟹O(1)$
- $T(n)=n+logn+1000⟹O(n)$
- $T(n)=5n^2+27n+1005⟹O(n^2)$

常见时间复杂度关系：

$$ O(1)<O(logn)<O(n)<O(nlogn)<O(n^2)\\<O(n^3)<O(2^n)<O(n)<O(n^n) $$  

### 复杂度计算规则

计算时间复杂度通常遵循以下步骤：

1. **定义标准操作**：选择一种或几种操作作为抽象的运算单位。
2. **计算操作次数**：将标准操作的执行次数表示为问题规模的函数。
3. **取主项**：取出函数的主项，即为大O表示。

以下是简化计算的常用规则：

- **求和定理**：串行执行的程序段，总时间复杂度为各段中最大者。
- **求积定理**：嵌套执行的程序段，总时间复杂度为各段时间复杂度之积。
- **循环语句**：时间复杂度等于循环体的运行时间乘以循环次数。
- **简化方法**：找出程序中运行时间最长的部分，它的时间复杂度就是整个程序的时间复杂度。

### 例子：最大连续子序列求和

这个问题有多种算法，其时间复杂度差异巨大。

**问题描述**：给定一个整数序列 A_1,A_2,...,A_N，求其最大连续子序列的和。

#### 算法一：穷举法 ($O(n^3)$)

``` Python
def maxSubsequenceSum_n3(a):
    maxSum = 0 
    size = len(a)
    for i in range(size):
        for j in range(i, size):
            thisSum = 0
            for k in range(i, j + 1):
                thisSum += a[k]
            if thisSum > maxSum:
                maxSum = thisSum
    return maxSum
```

计算过程：

我们以最内层的核心操作 `thisSum += a[k]` 为标准操作。

- 最内层循环执行 `j−i+1` 次。
- 中间层循环执行 $\sum \_ j = i^{n−1}(j−i+1)$ 次。
- 最外层循环执行 $\sum \_ i= 0^{n−1}\sum \_ j=i^{n−1}(j−i+1)$ 次。
- 该求和表达式的结果约为 $\frac{n^3+3n^2+2n}{6}$。
- 忽略系数和低次项，时间复杂度为 $O(n^3)$。

#### 算法二：优化后的穷举法 ($O(n^2)$)

该算法移除了最内层的循环，通过累加当前子序列的和来优化。

``` Python
def maxSubsequenceSum_n2(a):
    maxSum = 0
    size = len(a)
    for i in range(size):
        thisSum = 0
        for j in range(i, size):
            thisSum += a[j]
            if thisSum > maxSum:
                maxSum = thisSum
    return maxSum
```

计算过程：

我们以 `thisSum += a[j]` 为标准操作。

- 内层循环的总执行次数为 $n+(n−1)+\cdots+1=\frac{n(n+1)}{2}$。
- 该函数的主导项是 $\frac{n^2}{2}$。
- 忽略系数，时间复杂度为 $O(n^2)$。

#### 算法三：线性时间解法 (O(n))

该算法基于一个洞察：如果一个从左端开始的子序列的和是负的，那么它不可能是最大连续子序列的一部分。

``` Python
def maxSubsequenceSum_n(a):
    maxSum = 0
    thisSum = 0
    size = len(a)
    for j in range(size):
        thisSum = max(a[j], thisSum + a[j])
        if thisSum > maxSum:
            maxSum = thisSum
    return maxSum
```

**计算过程：**

- 算法只有一个循环，执行了 `n` 次。
- 循环内部的操作都是常量时间。
- 整个算法的总运行时间与 `n` 成正比。
- 因此，时间复杂度为 $O(n)$。

## 空间复杂度

### 概念与空间换时间

空间复杂度是算法在运行过程中使用的内存空间量，通常以大O表示法描述。它主要分析**额外**占用的内存空间，不包括输入数据本身。

在实际中，我们常常会使用“**以空间换时间**”的策略，即通过增加内存使用来减少算法的运行时间。

### 例子

#### 示例1：O(1)

``` Python
def algorithm_O1(n: int):
    a = 0
    b = [0] * 1000
    if n > 10:
        a = 1
```

**计算过程：**

- 变量 `a` 占用固定空间。
- 列表 `b` 的大小固定为1000个元素，不随 `n` 的变化而改变。
- 算法所需的额外内存空间是一个常量，空间复杂度为 $O(1)$。

#### 示例2：$O(n)$

``` Python
def algorithm_On(n: int):
    if n > 10:
        nums = [0] * n
```

**计算过程：**

- 当 `n > 10` 时，创建了一个大小为 `n` 的列表 `nums`。
- 列表所占用的内存空间与 `n` 的值成正比。
- 因此，空间复杂度为 $O(n)$。

#### 示例3：$O(n^2)$

``` Python
def algorithm_On2(n: int):
    num_matrix = [[0] * n for _ in range(n)]
```

**计算过程：**

- 代码创建了一个 $n\times n$ 的二维列表 `num_matrix`。
- 列表总共包含 $n\times n=n^2$ 个元素。
- 占用的内存空间与 $n^2$ 成正比。
- 因此，空间复杂度为 $O(n^2)$。
