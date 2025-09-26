---
title: 线性表
description: 介绍线性表结构
slug: datastructure-2
date: 2025-09-26 23:23:00+0800
math: true
image: cover.jpg
categories:
    - Data Structures
tags:
    - Algorithm - Data Structures
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

## 线性表的概念

线性表（Linear List）是一种最基本、最常用的数据结构。

- **定义**：线性结构是一种有序的数据项集合 1。其中除了首尾数据项外，每个数据项都有**唯一的前驱**和**后继**。
- **首尾特性**：首数据项没有前驱，尾数据项没有后继。
- **线性**：新的数据项加入时，只会加入到原有某个数据项之前或之后，不会有分叉，也不会独立于原有数据集。
- **术语**：
  - **表的大小（N）**：表中元素的个数。
  - **首结点**：$A_0$。
  - **尾结点**：$A_{N−1}$。
  - **空表**：元素个数为零的表。
  - **位置（i）**：元素 $A_i$ 在表中的位置。

## 线性表的基本操作

线性表的基本操作可分为四类：构造、读取属性、操纵数据和遍历。

| 操作           | 描述                                  | 类别          |
| -------------- | ---------------------------------    | --------------|
| `create()`     | 创建一个空的线性表。                   | 构造属性       |
| `length()`     | 返回线性表的长度。                     | 读取属性       |
| `search(x)`    | 搜索元素`x` 的位置，不存在返回 `-1`。   | 读取属性       |
| `visit(i)`     | 返回线性表中第 `i` 个数据元素的值。     | 读取属性       |
| `insert(i, x)` | 在第 `i` 个位置插入元素 `x`。           | 操纵数据      |
| `remove(i)`    | 删除第 `i` 个位置的元素。               | 操纵数据       |
| `clear()`      | 删除线性表中的所有数据元素。            | 操纵数据       |
| `traverse()`   | 按序访问线性表的每一数据元素。          | 遍历数据       |  

------

## 线性表的顺序存储实现（Sequential Storage）

### 结构和原理

- **原理**：线性表中的结点存放在存储器上**一块连续的空间中**。
- **特性**：结点的**物理位置**和它的**逻辑位置**是**一致的**。
- **Python 实现**：在 Python 中，通常使用**动态数组**（即 **List**）来实现顺序存储结构。

一个顺序存储结构需要保存三个变量：

  1. **指向数组的指针**（或数组本身，例如 Python 中的 `list`）。
  2. **数组规模**（容量，`capacity`/`maxSize`）。
  3. **数组中的元素个数**（表长，`size`/`length`）。

### Python 实现代码示例 (`LinearList`)

下面是顺序存储结构中一些关键操作的实现和复杂度分析。

#### 构造、求长、清空、访问

这些操作在顺序表中效率很高。

``` Python
class LinearList:
    def __init__(self, maxSize=4):
        self.capacity = maxSize  # 最大容量
        # 用列表存储线性表的元素，这里用 None 填充初始容量
        self.data = [None] * self.capacity
        self.size = 0  # 记录线性表的长度

    def length(self):
        """返回线性表的长度。时间复杂度 O(1)"""
        return self.size

    def clear(self):
        """删除所有数据元素，只需将长度置为 0。时间复杂度 O(1)"""
        self.size = 0

    def visit(self, i):
        """返回第 i 个元素的值。时间复杂度 O(1)"""
        if 0 <= i < self.size: # 边界检查
            return self.data[i] [cite: 263]
        else:
            raise IndexError("Index out of range")

    def search(self, x):
        """在线性表中搜索 x，返回位置或 -1。时间复杂度 O(n)"""
        for i in range(self.size):
            if self.data[i] == x:
                return i
        return -1

    def traverse(self):
        """遍历线性表，按序输出所有元素。时间复杂度 O(n)"""
        for i in range(self.size):
            print(self.data[i], end=' ')
        print()
```

#### 插入操作 (`insert(i, x)`)

在顺序表中插入元素需要移动结点，效率较低。

**步骤**：

1. 检查是否需要**扩容** (`double_space()`)。
2. 从尾部 `$a_{n-1}$` 开始，依次将 `$a_{n-1}, \dots, a_i$` 向后移动一位。
3. 在 `i` 位置放入新元素 `x`。
4. 表长 `size` 加 1。

**扩容策略**：

- **使用倍数扩容（例如扩大一倍）**：总时间复杂度为 $O(n)$，**均摊时间复杂度为 $O(1)$**，性能显著优化。
- **使用常数 C 扩容**：总时间复杂度为 $O(n^2)$，均摊时间复杂度为 $O(n)$。

``` Python
    def double_space(self):
        """扩大数组容量一倍 [cite: 189, 195]"""
        self.capacity *= 2
        new_data = [None] * self.capacity # 重新申请更大规模数组
        for i in range(self.size):
            new_data[i] = self.data[i] # 拷贝原有数据
        self.data = new_data # 释放原有数组空间，使用新数组

    def insert(self, i, x):
        """在第 i 个位置插入元素 x"""
        if self.size == self.capacity:
            self.double_space()

        if 0 <= i <= self.size: # i 的合法取值范围是 0 到 n
            # 移动元素 (从后往前移动)
            for j in range(self.size, i, -1):
                self.data[j] = self.data[j - 1]
            
            self.data[i] = x # 插入新元素 
            self.size += 1
        else:
            raise IndexError("Invalid index")

# 时间复杂度：
# 最好情况 O(1) (i=n, 尾部插入)
# 最坏情况 O(n) (i=0, 头部插入) 
# 平均情况 O(n) [cite: 301]
```

#### 删除操作 (`remove(i)`)

删除操作同样需要移动结点。

**步骤**：

1. 将 `$a_{i+1}, \dots, a_{n-1}$` 依次向前移动一位。
2. 表长 `size` 减 1。

``` Python
    def remove(self, i):
        """删除第 i 个位置的元素"""
        if 0 <= i < self.size: # i 的合法取值范围是 0 到 n-1
            # 移动元素 (从前往后移动)
            for j in range(i, self.size - 1):
                self.data[j] = self.data[j + 1]
            
            # 可选：将原最后一个元素位置置为 None (清理)
            self.data[self.size - 1] = None 
            self.size -= 1
        else:
            raise IndexError("Invalid index")

# 时间复杂度：
# 最好情况 O(1) (i=n-1, 尾部删除)
# 最坏情况 O(n) (i=0, 头部删除)
# 平均情况 O(n)
```

### 顺序存储总结

- **优点**：**定位访问的性能很好**，因为逻辑次序和物理次序一致。`visit(i)`、`length()`、`clear()` 的时间复杂度都是 **$O(1)$**。
- **缺点**：在**插入/删除**时需要移动大量数据，性能不太理想 (**$O(n)$**)。
- **适用场景**：适合**静态的**、**经常做定位访问**的线性表。
- **Python 关联**：Python 中 `list` 的底层实现大致与顺序线性表相同。

------

## 线性表的链接存储实现（Linked Storage）

链接存储通过指针来表示结点间的逻辑关系，**结点的物理位置可能相邻也可能不相邻**。

### 单链表 (Singly Linked List)

#### 单链表结构

- **结点**：包含数据域和指向下一个结点的指针域 (`next`)。
- **头指针**：一个指向链表头结点的指针变量 (`head`)。
- **头结点**：通常在表头额外增加一个特殊结点（不属于线性表组成部分），目的是**简化在表头位置上进行插入和删除的操作**，使之与在其它结点位置上的操作一致。

#### Python 结点和链表类

在 Python 中，通过**引用**的特性实现类似 C 语言指针的效果。

``` Python
class Node:
    """定义链表结点"""
    def __init__(self, data=None):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        """构造函数：创建一个只有头结点的空链表"""
        self.head = Node() # 创建头结点
        # 头结点的 next 默认为 None，表示空表
```

#### 单链表插入操作 (`insert(i, x)`)

插入操作不需要移动数据元素，只需修改两个指针。

**步骤**：

1. 找到第 `i-1` 个结点（即 `current`）,需要 $O(i)$ 的时间。
2. 创建新结点  `new_node`。
3. 新结点的 `next` 指向 `current` 的后继结点。
4. `current` 的 `next` 指向新结点 `new_node`。

``` Python
    def insert(self, i, x):
        """在第 i 个位置插入元素 x"""
        # 边界检查
        if i < 0 or i > self.length():
            raise IndexError("Index out of range")
        
        current = self.head # 从头结点开始
        # 找到要插入位置 i 的前一个节点（i-1）
        for _ in range(i):
            current = current.next
            
        new_node = Node(x)
        # 先武装自己：新结点的 next 指向 current.next
        new_node.next = current.next
        # 再加入队伍：current 的 next 指向新结点
        current.next = new_node

# 时间复杂度：
# 最好情况 O(1) (i=0, 头部插入, 找到头结点 O(1))
# 最坏情况 O(n) (i=n, 尾部插入, 需遍历到倒数第二个结点)
# 平均情况 O(n)
```

#### 单链表删除操作 (`remove(i)`)

删除操作同样只需修改一个指针。

**步骤**：

1. 找到要删除结点 `$a_i$` 的前驱结点 `$a_{i-1}$`（即 `current`），这需要 $O(i)$ 的时间。
2. 将 `$a_{i-1}$` 的 `next` 指针直接指向 `$a_i$` 的后继结点 `$a_{i+1}$`。

``` Python
    def remove(self, i):
        """删除第 i 个位置的元素"""
        if i < 0 or i >= self.length():
            raise IndexError("Index out of range")
        
        current = self.head # 从头结点开始
        # 找到要删除位置 i 的前一个节点（i-1）
        for _ in range(i):
            current = current.next
        
        # current.next 指向 to_delete 的 next，即跳过 to_delete
        current.next = current.next.next

# 时间复杂度：
# 最好情况 O(1) (i=0, 头部删除)
# 最坏情况 O(n) (i=n-1, 尾部删除)
# 平均情况 O(n)
```

#### 访问和搜索操作 (`visit(i)`, `search(x)`)

链表不支持随机存取，访问第 `i` 个元素或搜索元素都需要从头开始遍历。

``` Python
    def visit(self, i):
        """访问线性表的第 i 个元素"""
        if i < 0 or i >= self.length():
            raise IndexError("Index out of range")
        
        current = self.head.next # 从首结点开始
        for _ in range(i):
            current = current.next
        return current.data

# 时间复杂度：
# O(n)，需要遍历 i 次。

    def search(self, x):
        """搜索元素 x 的位置 position"""
        current = self.head.next # 从首结点开始
        position = 0
        while current is not None:
            if current.data == x:
                return position
            current = current.next
            position += 1
        return -1

# 时间复杂度：
# O(n)，最坏情况需要遍历整个链表。
```

### 双链表（Doubly Linked List）

#### 双链表结构

- **结点**：包含数据域、指向**直接前驱**的指针域 (`pre`) 和指向**直接后继**的指针域 (`next`)。
- **头尾结点**：为了消除在表头、表尾插入删除的特殊处理，通常设置**头结点**和**尾结点**。
  - 头结点的 `pre` 为空，`next` 指向首结点。
  - 尾结点的 `next` 为空，`pre` 指向最后一个结点。

#### 双链表插入操作 (`insert(i, x)`)

在双链表中插入新结点 `new_node` 在 `current` 之后，需要修改四个指针（`new_node` 的 `pre`/`next` 和前后结点的 `pre`/`next`）。

``` Python
# 假设 Node 类已添加 self.prev = None 属性

    def insert(self, i, x):
        """在第 i 个位置插入元素 x (在 current 之后插入)"""
        # ... 边界检查 ...
        new_node = Node(x)
        current = self.head # 找到插入位置的前一个 node
        for _ in range(i): 
            current = current.next

        # 1. 先武装自己：新节点的 pre/next 指向前后节点
        new_node.next = current.next
        new_node.prev = current
        
        # 2. 再加入队伍：调整前后节点的 pre/next 指针
        current.next.prev = new_node # current 后一个节点的 pre 指向新节点
        current.next = new_node # current 的 next 指向新节点

# 查找 current 仍需要 O(n)，但修改指针只需要 O(1)。
```

#### 双链表删除操作 (`remove(i)`)

删除操作只需要修改被删除结点的前一个和后一个结点的指针。

``` Python
    def remove(self, i):
        """删除第 i 个位置的元素 current"""
        # ... 边界检查 ...
        current = self.head.next # 从首结点开始
        for _ in range(i): # 找到要删除的 node
            current = current.next
        
        # 将 current 的前驱和后继结点直接连接起来
        current.prev.next = current.next
        current.next.prev = current.prev

# 查找 current 仍需要 O(n)，但删除操作（修改指针）只需要 O(1)。
```

### 循环链表 (Circular Linked List)

- **单循环链表**：末结点的 `next` 指向首结点，形成一个环。
- **双循环链表**：末结点的 `next` 指向头结点，首结点的 `pre` 指向末结点，形成双向环。
- **特性**：可以从任意一个结点开始，顺序向后访问到达任意结点。

------

## 五、 总结比较

| 特点 | 顺序存储 (如 Python List)| 单链表 | 双链表 | 循环链表  |
| ---- | ----------------------- | ----- | ------ | -------- |
| **存储方式**  | 连续存储 | 离散存储 (通过指针连接) | 离散存储 (双向指针)  | 离散存储 (末尾连回头部)  |
| **访问性能**  | | $O(1)$ (随机存取，通过索引直接访问) | $O(n)$ (需从头遍历)  | $O(n)$ (需从头遍历) |
| **插入/删除** | | $O(n)$ (需移动大量数据)  | $O(n)$ (需 $O(n)$ 查找前驱结点，$O(1)$ 修改指针) | $O(n)$ (需 $O(n)$ 查找结点，$O(1)$ 修改指针) |
| **内存效率**  | 好 (但可能因扩容产生开销)  | 差 (需要额外的指针空间)  | 最差 (需要两个指针空间)  | 较差 (需要额外的指针空间) |
| **主要区别**  | 适合**静态**、经常做**定位访问**的场景。 | 只能**单向**访问。 | 可以**双向**访问，删除操作更方便。 | 可以从任何结点开始访问任一结点。|

## 六、 线性表应用：约瑟夫斯环问题

约瑟夫斯环问题是一个经典的线性表应用，它模拟一群人围成一个圈，按规则淘汰，求最后剩下的人的位置。

### 使用数组/列表解决

使用 Python 的 `list` 实现时，每次删除元素 `people.pop(index)`，列表内部都需要移动其后的所有元素。

- **时间复杂度**：$O(N^2)$ (每次淘汰都是 $O(N)$，总共淘汰 $N−1$ 次)。

``` Python
def josephus_list(N, M):
    """使用 Python List 解决约瑟夫斯环问题"""
    people = list(range(1, N + 1)) # [1, 2, ..., N]
    index = 0 # 从第一个人开始

    while len(people) > 1:
        # 计算下一个要淘汰的人的索引
        index = (index + M - 1) % len(people) 
        people.pop(index) # 淘汰该人

    return people[0]

# 示例: josephus_list(7, 3) 返回 4
```

### 使用单循环链表解决

使用单循环链表可以避免删除时移动大量数据的开销。

- **时间复杂度**：$O(N\cdot M)$ (每次淘汰需要 $O(M)$ 步找到要删除的结点，总共淘汰 $N−1$ 次)。
- **注意**：尽管删除操作本身是 $O(1)$，但**寻找**要删除的结点需要 $O(M)$。

``` Python
class Node:
    """定义链表结点，用于约瑟夫斯环问题"""
    def __init__(self, value):
        self.value = value
        self.next = None

def create_circle(N):
    """
    创建 N 个结点的单循环链表。
    编号从 1 到 N。
    """
    if N <= 0:
        return None
    
    # 1. 创建第一个节点
    head = Node(1) [cite: 744]
    current = head [cite: 745]

    # 2. 创建其他节点 (从 2 到 N)
    for i in range(2, N + 1): [cite: 748]
        current.next = Node(i) # 创建其他节点 [cite: 749]
        current = current.next [cite: 750]

    # 3. 形成循环链表：最后一个节点的 next 指向 head
    current.next = head [cite: 751]
    return head

def josephus_linked_list(N, M):
    """
    使用单循环链表解决约瑟夫斯环问题。
    N 为人数，M 为淘汰间隔。
    时间复杂度: O(N*M) [cite: 734]
    """
    if N == 1: 
        return 1
    
    if M == 1: [cite: 756]
        return N [cite: 758] # M=1时，将按序淘汰 1, 2, ..., N-1，最后剩下 N。

    head = create_circle(N) # 创建循环链表
    current = head # 记录当前结点，从编号 1 的结点开始
    prev = None # 记录前一个结点，用于删除操作

    while current.next != current: # 循环直到只剩一个结点
        # 1. 移动 M-1 步，找到要淘汰的节点的前一个节点 (prev)
        # 循环 M-1 次，使 current 停在要淘汰的节点 to_delete 上
        for _ in range(M - 1):
            prev = current
            current = current.next
        
        # 此时 current 为要淘汰的节点 to_delete
        # print(f"淘汰的节点:{current.value}")

        # 2. 淘汰节点：将 prev 的 next 指向 to_delete 的 next
        # to_delete = current
        prev.next = current.next # 删除该节点
        
        # 3. 移动到下一个节点：新的 current 从 prev 的下一个结点（即原 to_delete 的 next）开始下一轮计数
        current = prev.next # 移动到下一个节点

    return current.value # 返回最后剩下的节点的值

# 示例
N = 7 # 人数 [cite: 781]
M = 3 # 每隔 M 个人淘汰一个 [cite: 782]
last_person = josephus_linked_list(N, M)
# print(f"最后剩下的人在原始队伍中的位置是:{last_person}")
# 期望输出结果为 4
```
