# 一、算法基础理论

1. **算法定义**

- 有限步骤内解决特定问题的明确指令集
- 五大特性：输入、输出、确定性、有限性、可行性

2. **复杂度分析**

- **时间复杂度**：
    - O(g(n)) 表示渐进上界
    - Ω(g(n)) 表示渐进下界
    - θ(g(n)) 表示渐进平均时间复杂度

  ```text
  O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2ⁿ)
  ```

- **空间复杂度**：递归调用栈、辅助空间计算
- **分析方法**：
    - 递归树
    - 主定理（Master Theorem）:
        - 阐述:
          > 如果$a>=1 $ 和$ b>1$ 且 $f(n)$ 是非负函数,$T(n) = aT(n/b)+f(n) $。
            1. $若对某个常数 \epsilon > 0 有 f(n) = O(n^{\log_b a - \epsilon}) ，则 T(n) = \Theta(n^{\log_b a})。$
            2. $若有f(n)=\Theta(n^{\log_b a}),则 T(n) = \Theta(n^{\log_b a}\lg n)$
            3. $若对于某个常数\epsilon>0 有 f(n)=\Omega(n^{\log_b a+\epsilon}),且对于某个常数c<1和所有足够大的n有af(
               n/b)<
               =cf(n),则T(n)=\Theta(f(n))$
        - 举例:

        1. 二分查找:
           $T(n)=T(n/2)+\Theta(1),其中a=1,b=2,f(n)=\Theta(1)$，则 $T(n)=\Theta(\lg n)$
        2. 归并排序:
           $T(n)=2T(n/2)+\Theta(n),其中a=2,b=2,f(n)=\Theta(n),其中f(n)=\Theta(n^{\log_b a}),所以T(n)=\Theta(n{\log^n})$

---

# 二、数据结构

## 1. 线性结构

### 顺序表

- **特点**：
    - **存储结构**：顺序表中的所有元素在内存中以连续的存储空间存储，这种存储方式使得顺序表可以通过索引快速访问任意位置的元素。
    - **内存分配**：通常需要预先分配一块足够大的内存空间来存储元素，这可能导致空间的浪费（如果实际存储的元素较少）或空间不足（如果实际存储的元素超出预分配空间）。
    - **操作效率**：插入和删除操作效率较低，尤其是中间位置的操作，平均时间复杂度为$O(n)$，因为需要移动大量元素来保持存储空间的连续性。
    - **随机访问**：支持快速随机访问，通过索引可以直接定位元素，时间复杂度为$O(1)$。

- **操作**：
    - **查找**：通过索引直接访问元素，时间复杂度为$O(1)$。
    - **插入**
      ：在指定位置插入一个新元素时，需要将该位置及其之后的所有元素向后移动一位，以腾出空间来插入新元素，时间复杂度为$O(n)$。
    - **删除**：删除指定位置的元素时，需要将该位置之后的所有元素向前移动一位，以填补被删除元素留下的空位，时间复杂度为$O(n)
      $。
    - **遍历**：从头到尾依次访问顺序表中的每个元素，时间复杂度为$O(n)$。

- **应用**：
    - **数组**：顺序表是数组的底层实现方式，适用于元素数量相对固定且需要频繁随机访问的场景，如存储学生的成绩、商品的库存等。
    - **栈和队列**：顺序表可以用来实现栈和队列这两种数据结构，通过限制插入和删除操作的位置来满足栈和队列的特性。
    - **矩阵**：在某些情况下，可以使用多维顺序表（即数组）来存储矩阵，方便进行矩阵运算和操作。
- **经典问题**:
    - 最大最小值：在顺序表中，可以使用线性搜索算法找到最大值和最小值，时间复杂度为$O(n)
      $。排序之后可以使用二分查找来快速找到最大值和最小值，时间复杂度为$O(\log n)$。
    -
  排序：在顺序表中，可以使用各种排序算法（如冒泡排序、选择排序、插入排序、归并排序、快速排序等）对元素进行排序，时间复杂度为$O(
  n\log n)$。
    - 搜索：在顺序表中，可以使用线性搜索算法进行搜索，时间复杂度为$O(n)$。
  ---

### 链表

- **特点**：
    - **存储结构**：链表由一系列节点组成，每个节点包含数据和指向下一个节点的引用，这种存储方式使得链表的存储空间可以分散在内存中，不需要连续的存储空间。
    - **内存分配**：链表的存储空间是动态分配的，可以根据实际需要动态地申请和释放节点，避免了空间的浪费和不足问题。
    - **操作效率**：插入和删除操作灵活，时间复杂度为$O(1)$，只需修改相邻节点的指针，而不需要移动大量元素。
    - **随机访问**：不支持随机访问，访问任意节点需要从头开始遍历，时间复杂度为$O(n)$。

- **操作**：
    - **查找**：从头节点开始，依次遍历链表，直到找到目标节点或到达链表末尾，时间复杂度为$O(n)$。
    - **插入**：在指定位置插入一个新节点时，只需修改相邻节点的指针，将新节点插入到链表中，时间复杂度为$O(1)$。
    - **删除**：删除指定位置的节点时，只需修改前驱节点的指针，使其指向被删除节点的后继节点，时间复杂度为$O(1)$。
    - **遍历**：从头节点开始，依次访问链表中的每个节点，时间复杂度为$O(n)$。

- **应用**：
    - **动态数据存储**：适用于元素数量不固定且需要频繁插入和删除元素的场景，如存储待处理的任务列表、动态的用户信息等。
    - **实现复杂数据结构**：链表可以用来实现一些复杂的数据结构，如双向链表、循环链表、链式队列、链式栈等，满足不同的应用场景需求。
    - **内存管理**：在某些内存管理算法中，使用链表来管理空闲内存块，方便动态地分配和回收内存空间。

---

## 2. 非线性数据结构

### 哈希表

- **特点**：
    - **快速查找**
      ：哈希表通过哈希函数将键（key）映射到一个较小范围的整数，通常用作数组的索引，从而实现快速查找、插入和删除操作，平均时间复杂度为O(
      1)。
    - **冲突处理**：由于哈希函数可能会将不同的键映射到同一个索引，因此需要解决冲突问题。常见的冲突解决方法包括链地址法（拉链法）、开放定址法等。
    - **动态扩展**：当哈希表中的元素过多时，可能会导致冲突增加和性能下降，因此需要动态扩展哈希表的大小，重新计算哈希值并重新分配元素。

- **操作**：
    - **插入**：计算键的哈希值，将其映射到哈希表中的某个位置，并将键值对存储在该位置。如果发生冲突，则根据冲突解决方法进行处理。
    - **查找**：计算键的哈希值，直接定位到哈希表中的某个位置，然后查找该位置的链表或其他数据结构，找到对应的键值对。
    - **删除**：计算键的哈希值，定位到哈希表中的某个位置，然后从该位置的链表或其他数据结构中删除对应的键值对。

- **应用**：
    - **快速查找**：用于实现字典、符号表等需要快速查找的数据结构，如Python中的字典类型。
    - **去重**：用于存储唯一元素，快速判断一个元素是否已经存在，如集合（set）数据结构。
    - **缓存**：在缓存系统中，通过哈希表快速查找缓存项，提高系统的性能。

- **经典问题**：
    - **两数之和**：给定一个整数数组和一个目标值，找出数组中和为目标值的两个数的

      ```python
      from typing import List
      def twoSum(nums: List[int], target: int) -> List[int]:
          num_set = set()
          for num in nums:
              complement = target - num
              if complement in num_set:
                  return [complement, num]
              num_set.add(num)
          return []
      ```

    - **三数之和**：给定一个整数数组，找出其中三个数，使它们的和与目标值最接近。

      ```python
      from typing import List
      def threeSum(nums: List[int], target: int) -> List[List[int]]:
          nums.sort()
          res,n = [],len(nums)
          for i in range(len(nums) - 2):
              if i > 0 and nums[i] == nums[i-1]: 
                continue
              left,right = i+1,n-1
              while left < right:
                  s = nums[i] + nums[left] + nums[right]
                  if s == target:
                      res.append([nums[i], nums[left], nums[right]])
                  while left < right and nums[left] == nums[left+1]: 
                      left += 1
                  while left < right and nums[right] == nums[right-1]: 
                      right -= 1
                  if s < target:
                      left += 1
                  if s > target:
                      right -= 1
          return res
      ```

    - **无重复字符的最长子串**：给定一个字符串，找到其中不含有重复字符的最长子串的长度。

---

### 树

- **特点**：
    - **层次结构**：树是一种层次化的数据结构，具有明确的父子关系，每个节点最多有一个父节点，但可以有多个子节点。
    - **递归定义**：树可以递归地定义为一个节点和若干子树的集合，这种递归性质使得树的很多操作可以通过递归算法实现。
    - **多样性**：树有多种类型，如二叉树、二叉搜索树、平衡树、堆等，每种树都有其特定的性质和应用场景。

- **操作**：
    - **遍历**：树的遍历是树的基本操作之一，常见的遍历方式包括前序遍历、中序遍历、后序遍历和层序遍历。遍历可以用于访问树中的所有节点。
    - **插入和删除**：在树中插入或删除节点时，需要根据树的类型和性质进行操作，如在二叉搜索树中插入或删除节点需要保持树的有序性。
    - **查找**：在树中查找特定的节点，如在二叉搜索树中，可以根据节点的值进行快速查找。

- **应用**：
    - **文件系统**：文件系统中的目录结构可以用树来表示，每个节点代表一个文件或目录，父子关系表示文件和目录的包含关系。
    - **组织结构**：在企业或组织中，员工的层级关系可以用树来表示，每个节点代表一个员工，父子关系表示上下级关系。
    - **决策树**：在机器学习和数据分析中，决策树是一种常用的分类和回归模型，通过树的结构来表示决策过程。

---

### 图

- **特点**：
    - **复杂关系**：图是一种用于表示复杂关系的数据结构，可以表示任意两个节点之间的关系，这种关系可以是有向的或无向的。
    - **多样性**：图有多种类型，如无向图、有向图、加权图、无权图等，每种图都有其特定的性质和应用场景。
    - **路径和连通性**：图的很多问题都与路径和连通性有关，如最短路径问题、连通分量问题等。
    - **存储方式**：图可以以邻接矩阵或邻接表两种方式存储，邻接矩阵表示为二维数组，邻接表表示为链表或其他数据结构。

- **操作**：
    - **遍历**：图的遍历包括层次遍历,深度优先搜索（DFS）和广度优先搜索（BFS），用于访问图中的所有节点。

      ```python
      from collections import  deque
      def bfs(graph, start):
        visited = set()
        queue = deque([start])
        while queue:
          node = queue.popleft()
          visited.add(node)
          for neighbor in graph[node]:
            if neighbor not in visited:
              queue.append(neighbor)
      def dfs(graph, start,visited: set):
          visited.add(start)
          for neighbor in graph[start]:
            if neighbor not in visited:
              dfs(graph, neighbor,visited)
      ```

    - **最短路径**：在加权图中，可以使用Dijkstra算法或Bellman-Ford算法计算从一个节点到其他所有节点的最短路径。
    - **连通分量**：在无向图中，可以使用DFS或BFS算法计算图的连通分量，即图中所有相互连通的节点集合。

- **应用**：
    - **社交网络**：在社交网络中，用户之间的关系可以用图来表示，节点代表用户，边代表用户之间的关系，如好友关系、关注关系等。
    - **交通网络**：在交通网络中，城市之间的交通连接可以用图来表示，节点代表城市，边代表交通线路，边的权重可以表示距离、时间或费用等。
    - **网页链接**：在互联网中，网页之间的链接关系可以用图来表示，节点代表网页，边代表网页之间的链接。

- **经典问题**：
    - **最短路径问题**：在加权图中，计算从一个节点到其他所有节点的最短路径。
    - **最小生成树问题**：在无向加权图中，找到一个包含所有节点的最小权重的生成树。
    - **连通分量问题**：在无向图中，计算图的连通分量，即图中所有相互连通的节点集合。

## 3. 高级数据结构

### 栈（Stack）

- **定义**：后进先出（LIFO）的线性数据结构，仅允许在栈顶进行插入（push）和删除（pop）操作。
- **核心操作**：
    - `push(x)`：将元素 `x` 压入栈顶。
    - `pop()`：弹出栈顶元素。
    - `peek()`：查看栈顶元素但不弹出。
    - `isEmpty()`：判断栈是否为空。
- **时间复杂度**：所有操作均为 \(O(1)\)。
- **应用场景**：
    - 函数调用栈（递归/非递归）。
    - 括号匹配、表达式求值（中缀转后缀）。
    - 浏览器前进后退、撤销操作（双栈实现）。

### 队列（Queue）

- **定义**：先进先出（FIFO）的线性数据结构，支持在队尾插入（enqueue）和队首删除（dequeue）。
- **核心操作**：
    - `enqueue(x)`：将元素 `x` 加入队尾。
    - `dequeue()`：移除队首元素。
    - `front()`：获取队首元素。
    - `isEmpty()`：判断队列是否为空。
- **变种**：
    - **双端队列（Deque）**：两端均可插入和删除。
    - **优先队列（Priority Queue）**：按优先级出队（通常用堆实现）。
- **时间复杂度**：普通队列操作均为 \(O(1)\)；优先队列的插入/删除为 \(O(\log n)\)。
- **应用场景**：
    - BFS（广度优先搜索）。
    - 任务调度、消息队列。

### 堆（Heap）

- **定义**：完全二叉树，满足堆性质（父节点值 ≥ 或 ≤ 子节点值）。
- **类型**：
    - **大顶堆**：父节点 ≥ 子节点，根节点为最大值。
    - **小顶堆**：父节点 ≤ 子节点，根节点为最小值。
- **核心操作**：
    - `insert(x)`：插入元素并调整堆结构。
    - `extractMax()/extractMin()`：取出堆顶元素并调整堆。
    - `heapify()`：将无序数组构建为堆。
- **时间复杂度**：
    - 插入/删除：\(O(\log n)\)。
    - 建堆：\(O(n)\)。
- **应用场景**：
    - 优先队列、Top K 问题。
    - 堆排序（时间复杂度 \(O(n \log n)\)）。

### 二叉搜索树（Binary Search Tree, BST）

- **定义**：二叉树，满足：
    - 左子树所有节点值 < 根节点值。
    - 右子树所有节点值 > 根节点值。
    - 左右子树也分别为 BST。
- **核心操作**：
    - `search(x)`：查找值为 `x` 的节点。
    - `insert(x)`：插入新节点。
    - `delete(x)`：删除节点（需处理子节点合并）。
- **时间复杂度**：
    - 平均：$O(log n)$（平衡时）。
    - 最坏：$O(n)$（退化为链表）。
- **缺点**：不平衡时性能退化，需通过平衡二叉树（如 AVL、红黑树）优化。

### 红黑树（Red-Black Tree）

- **定义**：自平衡二叉搜索树，通过颜色和规则保持平衡：
    1. 节点为红或黑。
    2. 根节点和叶子节点（NIL）为黑。
    3. 红节点的子节点必须为黑。
    4. 从任一节点到叶子节点的路径包含相同数量的黑节点。
- **平衡操作**：旋转（左旋/右旋）和颜色调整。
- **时间复杂度**：插入、删除、查找均为 $O(\log n)$。
- **应用场景**：
    - C++ STL `map`/`set`、Java `TreeMap`/`TreeSet`。
    - 数据库索引（如 B 树变种）。

### 树状数组（Fenwick Tree）

- **定义**：用于高效维护前缀和的动态数据结构，基于二进制低位技术（Lowbit）。
- **核心操作**：
    - `update(i, delta)`：将第 `i` 个元素的值增加 `delta`。
    - `query(i)`：查询前 `i` 个元素的前缀和。
- **时间复杂度**：
    - 更新和查询均为 $O(\log n)$。
- **优势**：代码简洁，空间占用小$O(n)$。
- **应用场景**：
    - 动态前缀和、逆序对统计。
    - 替代线段树处理单点更新+区间查询问题。

```python

class BinaryIndexedTree:
    def __init__(self, nums):
        """
        初始化树状数组
        :param nums: 原始数组
        """
        self.n = len(nums)
        self.tree = [0] * (self.n + 1)  # 树状数组从索引1开始
        for i in range(self.n):
            self.update(i, nums[i])

    def lowbit(self, x):
        """
        计算x的lowbit，即x二进制表示中最低位1所对应的值
        :param x: 输入值
        :return: lowbit(x)
        """
        return x & (-x)

    def update(self, index, delta):
        """
        更新数组中index位置的值，增加delta
        :param index: 需要更新的位置（原数组中的索引）
        :param delta: 增加的值
        """
        # 转换为树状数组中的索引
        i = index + 1
        while i <= self.n:
            self.tree[i] += delta
            i += self.lowbit(i)

    def query(self, index):
        """
        查询数组中前index个元素的前缀和
        :param index: 查询前缀和的索引（原数组中的索引）
        :return: 前index个元素的前缀和
        """
        res = 0
        i = index + 1
        while i > 0:
            res += self.tree[i]
            i -= self.lowbit(i)
        return res

    def get_value(self, index):
        """
        获取数组中index位置的值
        :param index: 查询位置的索引
        :return: index位置的值
        """
        if index < 0 or index >= self.n:
            return 0
        return self.query(index) - self.query(index - 1)

    def set_value(self, index, value):
        """
        设置数组中index位置的值为value
        :param index: 设置位置的索引
        :param value: 新的值
        """
        current_value = self.get_value(index)
        self.update(index, value - current_value)
```

### 线段树（Segment Tree）

- **定义**：二叉树结构，用于高效处理区间查询（如区间和、最大值）和区间更新。
- **核心操作**：
    - `build()`：构建线段树。
    - `query(l, r)`：查询区间 `[l, r]` 的聚合值。
    - `update(i, x)`：单点更新。
    - `rangeUpdate(l, r, delta)`：区间更新（需懒惰标记优化）。
- **时间复杂度**：
    - 构建：$O(n)$。
    - 查询/更新：$O(\log n)$。
- **变种**：
    - **懒惰传播（Lazy Propagation）**：优化区间更新。
    - **动态开点**：处理稀疏区间。
- **应用场景**：
    - 区间最值、区间和、区间覆盖问题。
    - 二维线段树（处理矩阵问题）。

```python
class SegmentTree:
    """
    通用线段树（支持区间更新 + 区间查询）
    支持自定义合并函数、懒标记更新函数、默认值
    适用于：区间求和、最大值、最小值、区间加、区间覆盖等场景
    """

    def __init__(self, data, root_func, merge_func=sum, default=0):
        """
        初始化线段树
    
        :param data: 原始数据列表 (list)
        :param root_func: 懒标记应用函数，签名：f(left, right, lazy_value, old_value) -> new_value
                          用于计算：当区间 [left, right] 被赋予 lazy_value 时，节点应变成什么值
                          例如：
                            - 覆盖型：lambda l, r, v, _: v
                            - 增量型（区间加）：lambda l, r, v, old: old + v * (r - l + 1)
        :param merge_func: 合并函数，签名：f(a, b) -> merged_value，如 sum, max, min
        :param default: 查询无效区间时的返回值（单位元），如 0（sum）、-inf（max）、+inf（min）
        """
        self.n = len(data)  # 原始数据长度
        self.merge = merge_func  # 节点合并函数（如求和、最大值）
        self.root_func = root_func  # 懒标记生效函数（决定 lazy 如何影响节点值）
        self.size = 1  # 线段树底层满二叉树的“叶子层”大小（≥n 的最小 2 的幂）
        self.default = default  # 无效查询返回值（如空区间）

        # 计算 size：扩展成满二叉树叶子数
        while self.size < self.n:
            self.size *= 2

        # 初始化线段树数组和懒标记数组（1-based，tree[1] 是根）
        self.tree = [self.default] * (2 * self.size)  # 线段树节点值
        self.lazy = [0] * (2 * self.size)  # 懒标记（默认 0 表示无标记）

        # 叶子节点赋值：原始数据放在 [size, size + n - 1]
        for i in range(self.n):
            self.tree[self.size + i] = data[i]

        # 自底向上构建内部节点：从 size-1 到 1
        for i in range(self.size - 1, 0, -1):
            self.tree[i] = self.merge(self.tree[2 * i], self.tree[2 * i + 1])

    def _push(self, root, left, right):
        """
        懒标记下推函数（Lazy Propagation）
        将当前节点的 lazy 值推给子节点，并更新子节点的 tree 值
    
        :param root: 当前节点编号（1-based）
        :param left: 当前节点管理的左边界（逻辑索引）
        :param right: 当前节点管理的右边界（逻辑索引）
        """
        if self.lazy[root] != 0:  # 有懒标记需要下推
            if left != right:  # 不是叶子节点 → 需要推给左右子树
                mid = (left + right) // 2

                # 更新左子树的 lazy 和 tree 值
                self.lazy[root * 2] = self.lazy[root]
                self.tree[root * 2] = self.root_func(left, mid, self.lazy[root], self.tree[root * 2])

                # 更新右子树的 lazy 和 tree 值
                self.lazy[root * 2 + 1] = self.lazy[root]
                self.tree[root * 2 + 1] = self.root_func(mid + 1, right, self.lazy[root], self.tree[root * 2 + 1])

            # 清空当前节点的 lazy 标记
            self.lazy[root] = 0

    def _update(self, root, start, end, left, right, value):
        """
        递归更新函数：将区间 [left, right] 的值设为 value（或按 root_func 计算）
    
        :param root: 当前节点编号
        :param start: 当前节点管理的区间左端点
        :param end: 当前节点管理的区间右端点
        :param left: 待更新区间的左端点（用户输入）
        :param right: 待更新区间的右端点（用户输入）
        :param value: 要设置/增加的值
        """
        # 区间无交集，直接返回
        if end < left or right < start:
            return

        # 当前节点区间完全被 [left, right] 覆盖
        if left <= start and end <= right:
            # 应用 lazy：更新当前节点值
            self.tree[root] = self.root_func(start, end, value, self.tree[root])
            # 设置懒标记（子节点暂不更新）
            self.lazy[root] = value
            return

        # 递归前先下推懒标记，确保子节点数据最新
        self._push(root, start, end)

        # 递归更新左右子树
        mid = (start + end) // 2
        self._update(root * 2, start, mid, left, right, value)
        self._update(root * 2 + 1, mid + 1, end, left, right, value)

        # 回溯：用子节点更新当前节点
        self.tree[root] = self.merge(self.tree[root * 2], self.tree[root * 2 + 1])

    def update(self, left, right, value):
        """
        对外接口：更新区间 [left, right]（闭区间）
    
        :param left: 更新区间左端点（0-based，原始数组索引）
        :param right: 更新区间右端点
        :param value: 要设置/增加的值
        """
        # 根节点管理 [0, size-1]，递归更新
        self._update(1, 0, self.size - 1, left, right, value)

    def _query(self, node, left, right, query_left, query_right):
        """
        递归查询函数：查询区间 [query_left, query_right] 的合并值
    
        :param node: 当前节点编号
        :param left: 当前节点管理的左边界
        :param right: 当前节点管理的右边界
        :param query_left: 查询区间的左端点
        :param query_right: 查询区间的右端点
        :return: 区间合并值
        """
        # 无交集 → 返回单位元
        if left > query_right or right < query_left:
            return self.default

        # 下推懒标记，确保当前节点值是最新的
        self._push(node, left, right)

        # 当前节点区间完全在查询区间内 → 直接返回
        if left >= query_left and right <= query_right:
            return self.tree[node]

        # 递归查询左右子树
        mid = (left + right) // 2
        leftRes = self._query(node * 2, left, mid, query_left, query_right)
        rightRes = self._query(node * 2 + 1, mid + 1, right, query_left, query_right)

        # 合并左右子树结果
        return self.merge(leftRes, rightRes)

    def query(self, left, right):
        """
        对外接口：查询区间 [left, right] 的合并值
    
        :param left: 查询区间左端点（0-based）
        :param right: 查询区间右端点
        :return: 合并结果（如区间和、最大值等）
        """
        return self._query(1, 0, self.size - 1, left, right)

```

---

## 4.数据结构对应算法

### 栈

#### 表达式求值

```python
def evaluate_expression(expression):
    precedence = {'+': 1, '-': 1, '*': 2, '/': 2, '^': 3}
    expression = expression.replace(' ', '')
    values = []
    ops = []
    i = 0
    n = len(expression)
    while i < n:
        # 处理负号（一元运算符）
        if expression[i] == '-' and (i == 0 or expression[i - 1] == '(' or expression[i - 1] in precedence):
            # 这是一个负号而不是减号
            num_str = '-'
            i += 1
            # 收集数字部分
            while i < n and (expression[i].isdigit() or expression[i] == '.'):
                num_str += expression[i]
                i += 1
            values.append(float(num_str))
            continue

        # 处理数字（正数）
        if expression[i].isdigit() or expression[i] == '.':
            num_str = ''
            while i < len(expression) and (expression[i].isdigit() or expression[i] == '.'):
                num_str += expression[i]
                i += 1
            values.append(float(num_str))
            continue

        # 处理运算符和括号（与原逻辑相同）
        if expression[i] == '(':
            ops.append(expression[i])
        elif expression[i] == ')':
            while ops and ops[-1] != '(':
                apply_operation(values, ops)
            ops.pop()
        else:
            while (ops and ops[-1] != '(' and
                   precedence.get(ops[-1], 0) >= precedence.get(expression[i], 0)):
                apply_operation(values, ops)
            ops.append(expression[i])
        i += 1

    while ops:
        apply_operation(values, ops)

    return values[-1] if values else 0


def apply_operation(values, ops):
    if len(values) < 2 or not ops:
        return

    op = ops.pop()
    b = values.pop()
    a = values.pop()

    if op == '+':
        values.append(a + b)
    elif op == '-':
        values.append(a - b)
    elif op == '*':
        values.append(a * b)
    elif op == '/':
        values.append(a / b)
    elif op == '^':
        values.append(a ** b)

```

#### 单调栈

##### 下一个更大元素

> **问题描述**:
> 给定一个循环数组 nums （ nums[nums.length - 1] 的下一个元素是 nums[0] ），返回 nums 中每个元素的 下一个更大元素 。
> 数字 x 的 下一个更大的元素 是按数组遍历顺序，这个数字之后的第一个比它更大的数，这意味着你应该循环地搜索它的下一个更大的数。如果不存在，则输出
> -1 。

```python
from typing import List


def nextGreaterElements(self, nums: List[int]) -> List[int]:
    stack = []
    n = len(nums)
    nums *= 2
    result = [-1] * n
    for i in range(2 * n):
        while stack and nums[i] > nums[stack[-1]]:
            index = stack.pop()
            if index < n:
                result[index] = nums[i]
        stack.append(i)
    return result
```

### 链表

#### 反转链表

链表可以通过修改节点的指针来反转链表，时间复杂度为$O(n)$。

```python
class ListNode:
    def __init__(self):
        self.next = None


def reverse_list(head: ListNode) -> ListNode:
    pre, cur = None, head
    while cur:
        next = cur.next
        cur.next = pre
        pre, cur = cur, next
    return pre
```

#### 旋转链表

链表可以通过修改节点的指针来旋转链表，时间复杂度为$O(n)$。

```python
from typing import Optional


# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next


class Solution:
    def rotateRight(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        # Edge cases: empty list or rotation count 0
        if not head or k == 0:
            return head

        # Step 1: Calculate the length of the linked list
        n = 0
        cur = head
        while cur:
            n += 1
            cur = cur.next

        # Step 2: Effective rotations (mod n)
        k %= n
        if n == 1 or k == 0:
            return head  # No need to rotate

        # Helper function to reverse a linked list
        def reverse(node: Optional[ListNode]) -> Optional[ListNode]:
            prev, curr = None, node
            while curr:
                nxt = curr.next
                curr.next = prev
                prev, curr = curr, nxt
            return prev

        # Step 3: Reverse the entire list
        new_head = reverse(head)

        # Step 4: Split the list into two parts at k-th node
        pre_node, index_k = None, new_head
        for _ in range(k):
            temp = index_k.next
            index_k.next = pre_node
            pre_node, index_k = index_k, temp

        # Step 5: Reconnect and reverse the second part
        new_head.next = reverse(index_k)

        # The rotated list starts from pre_node
        return pre_node

```

#### 判断链表是否成环

可以使用快慢指针的方法，如果链表存在环，快指针和慢指针一定会相遇，时间复杂度为$O(n)$。

```python
class ListNode:
    def __init__(self):
        self.next = None


def has_cycle(head: ListNode) -> bool:
    fast, slow = head, head
    while fast and fast.next:
        fast, slow = fast.next.next, slow.next
        if fast == slow:
            return True
    return False
```

---

### 树

#### 二叉树的遍历

实现二叉树的前序、中序、后序和层序遍历。

```python
from typing import List


class TreeNode:
    def __init__(self, value: int):
        self.left = None
        self.right = None
        self.value = value


def preorderTraversal(root: TreeNode) -> List[int]:
    if not root:
        return []
    res = [root.val]
    for node in root.children:
        res += preorderTraversal(node)
    return res


def inorderTraversal(root: TreeNode) -> List[int]:
    if not root:
        return []
    res = []
    res += inorderTraversal(root.left)
    res.append(root.val)
    res += inorderTraversal(root.right)
    return res


def postorderTraversal(root: TreeNode) -> List[int]:
    if not root:
        return []
    res = []
    res += postorderTraversal(root.left)
    res += postorderTraversal(root.right)
    res.append(root.val)
    return res


from collections import deque


def levelOrder(root: TreeNode) -> List[List[int]]:
    if not root:
        return []
    res = []
    queue = deque([root])
    while queue:
        level = []
    for _ in range(len(queue)):
        node = queue.popleft()
        level.append(node.val)
        for child in node.children:
            queue.append(child)
    res.append(level)
    return res
```

#### 二叉搜索树的建立

```python
class TreeNode:

    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


def sorted_array_to_bst(nums):
    """
    将一个排好序的数组转换为一棵高度平衡的二叉搜索树。
    
    参数:
        nums: List[int] - 升序排列的数组
    
    返回:
        TreeNode - 高度平衡的二叉搜索树的根节点
    """

    def build_bst(left, right):
        # 递归终止条件
        if left > right:
            return None

        # 选择中间元素作为根节点
        mid = (left + right) // 2
        root = TreeNode(nums[mid])

        # 递归构建左右子树
        root.left = build_bst(left, mid - 1)
        root.right = build_bst(mid + 1, right)

        return root
```

#### 二叉树的类实现(CRUD等操作)

```python
class TreeNode:
    """
    定义二叉树的节点类。
    每个节点包含三个属性：
    - val: 节点的值
    - left: 左子节点
    - right: 右子节点
    """

    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


class BinarySearchTree:
    """
    定义二叉搜索树类。
    提供插入、删除、修改、查找等操作。
    """

    def __init__(self):
        self.root = None  # 初始化根节点为空

    def insert(self, val):
        """
        向 BST 中插入一个值。
        如果树为空，则创建新节点作为根节点。
        否则根据值的大小递归地找到合适的位置插入新节点。
        """
        self.root = self._insert(self.root, val)

    def _insert(self, node, val):
        if not node:  # 如果当前节点为空，创建新节点
            return TreeNode(val)

        if val < node.val:  # 插入左子树
            node.left = self._insert(node.left, val)
        elif val > node.val:  # 插入右子树
            node.right = self._insert(node.right, val)
        # 如果 val == node.val，可以选择忽略（不允许重复值）
        return node

    def delete(self, val):
        """
        从 BST 中删除一个值。
        需要处理三种情况：
        1. 被删除节点是叶子节点：直接移除该节点。
        2. 被删除节点有一个子节点：用子节点替换被删除节点。
        3. 被删除节点有两个子节点：
        找到其前驱节点（左子树中的最大值）或后继节点（右子树中的最小值），
        用前驱/后继的值替换被删除节点，并递归删除前驱/后继节点。
        """
        self.root = self._delete(self.root, val)

    def _delete(self, node, val):
        if not node:  # 如果节点为空，直接返回
            return None

        if val < node.val:  # 在左子树中删除
            node.left = self._delete(node.left, val)
        elif val > node.val:  # 在右子树中删除
            node.right = self._delete(node.right, val)
        else:  # 找到要删除的节点
            # 情况 1 和 2：节点只有一个子节点或没有子节点
            if not node.left:
                return node.right
            if not node.right:
                return node.left

            # 情况 3：节点有两个子节点
            # 找到右子树中的最小值（后继节点）
            min_node = self._find_min(node.right)
            node.val = min_node.val  # 替换当前节点的值
            node.right = self._delete(node.right, min_node.val)  # 删除后继节点

        return node

    def _find_min(self, node):
        """
        找到子树中的最小值节点。
        最小值节点位于左子树的最左侧。
        """
        while node.left:
            node = node.left
        return node

    def update(self, old_val, new_val):
        """
        修改 BST 中的一个值。
        修改操作可以看作是删除旧值并插入新值的组合。
        """
        self.delete(old_val)  # 删除旧值
        self.insert(new_val)  # 插入新值

    def search(self, val):
        """
        查找 BST 中是否存在某个值。
        如果存在，返回对应的节点；否则返回 None。
        """
        return self._search(self.root, val)

    def _search(self, node, val):
        if not node or node.val == val:  # 如果节点为空或找到目标值
            return node

        if val < node.val:  # 在左子树中查找
            return self._search(node.left, val)
        else:  # 在右子树中查找
            return self._search(node.right, val)

    def inorder_traversal(self):
        """
        中序遍历 BST。
        中序遍历的结果是一个升序排列的列表。
        """
        result = []
        self._inorder_traversal(self.root, result)
        return result

    def _inorder_traversal(self, node, result):
        if not node:
            return
        self._inorder_traversal(node.left, result)  # 遍历左子树
        result.append(node.val)  # 访问当前节点
        self._inorder_traversal(node.right, result)  # 遍历右子树
```

---

### 图

#### 最短路径问题

在加权图中，计算从一个节点到其他所有节点的最短路径。

- **Bellman-Ford** 用于计算单源最短路径，支持负权边，但不能处理负权环。时间复杂度为$O(nm)$。空间复杂度为$O(n)$。

  ```python
  def bellman_ford(n, edges, start):
      # n: 节点数 (从 0 到 n-1)
      # edges: 边列表 [(u, v, w), ...] 表示从 u 到 v 权重为 w
      # start: 起点
      INF = float('inf')
      dist = [INF] * n
      dist[start] = 0

      # 松弛操作
      for _ in range(n - 1):
          for u, v, w in edges:
              if dist[u] != INF and dist[u] + w < dist[v]:
                  dist[v] = dist[u] + w

      # 检查负权环
      for u, v, w in edges:
          if dist[u] != INF and dist[u] + w < dist[v]:
              raise ValueError("Graph contains a negative-weight cycle")

      return dist
  ```

- **Dijkstra** 用于计算单源最短路径，只支持正权边，不能处理负权边和负权环。时间复杂度为$O((V+E)\log V)$。空间复杂度为$O(V)$。

  ```python
  import heapq

  def dijkstra(n, edges, start):
      # n: 节点数 (从 0 到 n-1)
      # edges: 邻接表 {u: [(v, w), ...]} 表示从 u 到 v 权重为 w
      # start: 起点
      INF = float('inf')
      dist = [INF] * n
      dist[start] = 0
      pq = [(0, start)]  # (当前距离, 节点)

      while pq:
          current_dist, u = heapq.heappop(pq)
          if current_dist > dist[u]:
              continue
          for v, w in edges.get(u, []):
              if dist[u] + w < dist[v]:
                  dist[v] = dist[u] + w
                  heapq.heappush(pq, (dist[v], v))

      return dist
  ```

- **Floyd-Warshall** 用于计算任意两节点的最短路径，支持正负权边，不能处理负权环。时间复杂度为$O(V^3)$。空间复杂度为$O(V^2)$。

  ```python
  def floyd_warshall(n, edges):
      # n: 节点数 (从 0 到 n-1)
      INF = float('inf')
      dist = [[INF] * n for _ in range(n)]
      for u, v, w in edges:
          dist[u][v] = w
      for k in range(n):
          for i in range(n):
              for j in range(n):
                  dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])
      return dist
  ```

#### 最小生成树问题

在无向加权图中，找到一个包含所有节点的最小权重的生成树。

- **Prim** 用于计算最小生成树，支持正负权边，不能处理负权环。时间复杂度$O(E\log V)$,空间复杂度为$O(E)$

  ```python
  import heapq

  def prim(n, edges):
      # n: 节点数 (从 0 到 n-1)
      # edges: 邻接表 {u: [(v, w), ...]} 表示从 u 到 v 权重为 w
      INF = float('inf')
      visited = [False] * n
      mst_weight = 0
      pq = [(0, 0)]  # (权重, 节点)

      while pq:
          weight, u = heapq.heappop(pq)
          if visited[u]:
              continue
          visited[u] = True
          mst_weight += weight
          for v, w in edges.get(u, []):
              if not visited[v]:
                  heapq.heappush(pq, (w, v))

      return mst_weight
  ```

- **Kruskal** 用于计算最小生成树，支持正负权边，不能处理负权环。时间复杂度$O(E\log E)$,空间复杂度为$O(E+V)$

  ```python
  class UnionFind:
    def __init__(self, n):
        self.parent = list(range(n))
        self.rank = [0] * n

    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]

    def union(self, x, y):
        root_x = self.find(x)
        root_y = self.find(y)
        if root_x != root_y:
            if self.rank[root_x] > self.rank[root_y]:
                self.parent[root_y] = root_x
            elif self.rank[root_x] < self.rank[root_y]:
                self.parent[root_x] = root_y
            else:
                self.parent[root_y] = root_x
                self.rank[root_x] += 1
            return True
        return False

  def kruskal(n, edges):
      # n: 节点数 (从 0 到 n-1)
      # edges: 边列表 [(u, v, w), ...] 表示从 u 到 v 权重为 w
      edges.sort(key=lambda x: x[2])  # 按权重排序
      uf = UnionFind(n)
      mst_weight = 0
      for u, v, w in edges:
          if uf.union(u, v):
              mst_weight += w
      return mst_weight
  ```

#### 最长路径问题

在加权图中，计算从起点到终点的最长路径。

```python
def bellman_ford_longest_path(n, edges, start):
    """
    使用 Bellman-Ford 算法求解最长路径。
    
    参数:
        n: 节点数量 (从 0 到 n-1)。
        edges: 边列表 [(u, v, w), ...] 表示从 u 到 v 权重为 w。
        start: 起点。
    
    返回:
        dist: 每个节点的最长路径距离。
    """

    INF = float('inf')
    dist = [-INF] * n  # 初始化为负无穷
    dist[start] = 0

    # Bellman-Ford 核心逻辑
    for _ in range(n - 1):  # 迭代 n-1 次
        for u, v, w in edges:
            if dist[u] != -INF and dist[u] - w > dist[v]:  # 注意这里是减号
                dist[v] = dist[u] - w

    # 检查是否存在正权环
    for u, v, w in edges:
        if dist[u] != -INF and dist[u] - w > dist[v]:
            raise ValueError("Graph contains a positive-weight cycle")

    # 将结果取反，得到最长路径
    return [-d for d in dist]
```

#### 图中判环问题

在有向加权图中，判断是否存在环。时间复杂度为$O(V+E)$，空间复杂度为$O(V)$。

```python
def has_cycle(graph):
    """
    使用三色法检测有向图中是否存在环。
  
    参数:
        graph: 邻接表表示的图，类型为 dict 或 defaultdict(list)，例如 {0: [1, 2], 1: [2], 2: []}。
  
    返回:
        bool: 如果图中存在环返回 True，否则返回 False。
    """
    WHITE, GRAY, BLACK = 0, 1, 2  # 定义三种颜色状态
    color = [WHITE] * len(graph)  # 初始化所有节点为白色

    def dfs(node):
        if color[node] == GRAY:  # 如果遇到灰色节点，说明存在环
            return True
        if color[node] == BLACK:  # 如果是黑色节点，无需继续访问
            return False

        color[node] = GRAY  # 标记当前节点为灰色
        for neighbor in graph[node]:  # 遍历邻接节点
            if dfs(neighbor):  # 如果发现环，直接返回 True
                return True
        color[node] = BLACK  # 标记当前节点为黑色
        return False

    # 遍历每个节点，检查是否有环
    for node in range(len(graph)):
        if color[node] == WHITE and dfs(node):
            return True  # 存在环

    return False  # 无环
```

#### 图中最大环问题

```python
from collections import defaultdict


def find_largest_cycle(graph):
    """
    使用三色标记法找到图中的最大环。
  
    参数:
        graph: 邻接表表示的图，类型为 dict 或 defaultdict(list)。
    
    返回:
        list: 最大环的节点列表。如果没有环，返回空列表。
    """
    WHITE, GRAY, BLACK = 0, 1, 2  # 定义三种颜色状态
    color = [WHITE] * len(graph)  # 初始化所有节点为白色
    max_cycle = []  # 记录最大环

    def dfs(node, path):
        nonlocal max_cycle
        if color[node] == GRAY:  # 发现环
            cycle_start = path.index(node)
            cycle = path[cycle_start:]
            if len(cycle) > len(max_cycle):  # 更新最大环
                max_cycle = cycle
            return

        if color[node] == BLACK:  # 已经处理过的节点，无需再访问
            return

        color[node] = GRAY  # 标记为灰色
        path.append(node)  # 将当前节点加入路径
        for neighbor in graph[node]:
            dfs(neighbor, path)  # 递归访问邻接节点
        path.pop()  # 回溯，移除当前节点
        color[node] = BLACK  # 标记为黑色

    # 遍历每个节点，寻找最大环
    for node in range(len(graph)):
        if color[node] == WHITE:
            dfs(node, [])
    return max_cycle
```

# 三、算法设计范式

## 1.排序算法

### 基于比较

#### <p style="text-align: center">冒泡排序</p>

冒泡排序通过重复地交换相邻的未排序元素，将较大的元素逐步“冒泡”到数组末尾。

```python
from typing import List


def bubble_sort(arr: List[int]):
    n = len(arr)
    for i in range(n - 1):  # 外层循环控制遍历次数
        flag = False  # 标记是否发生交换
        for j in range(n - 1 - i):  # 内层循环比较相邻元素
            if arr[j] > arr[j + 1]:  # 如果前一个元素大于后一个元素，则交换
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                flag = True  # 发生了交换
        if not flag:  # 如果没有发生交换，说明已经有序，提前退出
            break
```

---

#### <p style="text-align: center">选择排序</p>

选择排序每次从未排序部分中找到最小值，并将其放到已排序部分的末尾。

```python
from typing import List


def selection_sort(arr: List[int]):
    n = len(arr)
    for i in range(n - 1):  # 外层循环控制已排序部分的末尾
        min_index = i  # 假设当前索引为最小值索引
        for j in range(i + 1, n):  # 内层循环寻找未排序部分的最小值
            if arr[j] < arr[min_index]:
                min_index = j
        if min_index != i:  # 如果找到了更小的值，则交换
            arr[i], arr[min_index] = arr[min_index], arr[i]
```

---

#### <p style="text-align: center">快速排序</p>

快速排序基于分治思想，通过选择一个基准值（pivot），将数组分为小于基准值和大于基准值的两部分，递归处理。

```python
from typing import List


def quick_sort(arr: List[int]):
    def _quick_sort_helper(low: int, high: int):
        if low >= high:  # 递归终止条件
            return

        # 选择最后一个元素作为基准值
        pivot = arr[high]
        left = low  # 左指针从 low 开始

        for i in range(low, high):
            if arr[i] < pivot:  # 如果当前元素小于基准值
                arr[left], arr[i] = arr[i], arr[left]  # 将其交换到左侧
                left += 1  # 左指针右移

        # 将基准值放到正确位置
        arr[left], arr[high] = arr[high], arr[left]

        # 递归处理左半部分和右半部分
        _quick_sort_helper(low, left - 1)
        _quick_sort_helper(left + 1, high)

    _quick_sort_helper(0, len(arr) - 1)
```

---

#### <p style="text-align: center">插入排序</p>

插入排序通过构建有序序列，对于未排序数据，在已排序序列中从后向前扫描，找到相应位置并插入。

```python
from typing import List


def insertion_sort(arr: List[int]):
    n = len(arr)
    for i in range(1, n):  # 从第二个元素开始，逐步插入到已排序部分
        key = arr[i]  # 当前待插入的元素
        j = i - 1
        while j >= 0 and arr[j] > key:  # 在已排序部分中找到插入位置
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key  # 插入到正确位置
```

---

#### <p style="text-align: center">堆排序</p>

堆排序利用堆这种数据结构设计的一种排序算法，堆是一个近似完全二叉树的结构。

```python
from typing import List


def heap_sort(arr: List[int]):
    def heapify(arr: List[int], n: int, i: int):
        largest = i  # 初始化最大值为根节点
        left = 2 * i + 1  # 左子节点
        right = 2 * i + 2  # 右子节点
        if left < n and arr[left] > arr[largest]:  # 如果左子节点大于根节点
            largest = left
        if right < n and arr[right] > arr[largest]:  # 如果右子节点大于当前最大值
            largest = right
        if largest != i:  # 如果最大值不是根节点，交换并递归调整
            arr[i], arr[largest] = arr[largest], arr[i]
            heapify(arr, n, largest)

    n = len(arr)
    # 构建最大堆
    for i in range(n // 2 - 1, -1, -1):
        heapify(arr, n, i)
    # 逐个提取元素
    for i in range(n - 1, 0, -1):
        arr[0], arr[i] = arr[i], arr[0]  # 将最大值放到末尾
        heapify(arr, i, 0)  # 调整剩余部分为最大堆
```

---

#### <p style="text-align: center">归并排序</p>

归并排序采用分治法，将数组分成两部分分别排序，然后合并两个有序数组。

```python
from typing import List


def merge_sort(arr: List[int]):
    def _merge(left: List[int], right: List[int]) -> List[int]:
        result = []
        i = j = 0
        while i < len(left) and j < len(right):  # 合并两个有序数组
            if left[i] <= right[j]:
                result.append(left[i])
                i += 1
            else:
                result.append(right[j])
                j += 1
        result.extend(left[i:])  # 添加剩余元素
        result.extend(right[j:])
        return result

    if len(arr) <= 1:  # 递归终止条件
        return arr
    mid = len(arr) // 2
    left_half = merge_sort(arr[:mid])  # 递归排序左半部分
    right_half = merge_sort(arr[mid:])  # 递归排序右半部分
    return _merge(left_half, right_half)  # 合并两个有序部分
```

---

### 不基于比较

#### <p style="text-align: center">计数排序</p>

```python
from typing import List


def counting_sort(arr: List[int]) -> List[int]:
    if not arr:
        return arr  # 如果数组为空，直接返回

    # 找到数组中的最大值和最小值
    max_val = max(arr)
    min_val = min(arr)

    # 创建计数数组，长度为 max_val - min_val + 1
    count = [0] * (max_val - min_val + 1)

    # 统计每个元素出现的次数
    for num in arr:
        count[num - min_val] += 1

    # 根据计数数组重新填充原数组
    index = 0
    for i, cnt in enumerate(count):
        while cnt > 0:
            arr[index] = i + min_val
            index += 1
            cnt -= 1

    return arr
```

#### <p style="text-align: center">基数排序</p>

```python
from typing import List


def radix_sort(arr: List[int]) -> List[int]:
    if not arr:
        return arr  # 如果数组为空，直接返回

    # 获取数组中的最大值，确定最大位数
    max_num = max(arr)
    max_digits = len(str(abs(max_num)))  # 最大数字的位数

    # 辅助函数：按某一位进行计数排序
    def counting_sort_by_digit(arr: List[int], digit: int) -> List[int]:
        buckets = [[] for _ in range(10)]  # 创建 10 个桶

        # 将元素分配到桶中
        for num in arr:
            bucket_index = (num // (10 ** digit)) % 10
            buckets[bucket_index].append(num)

        # 将桶中的元素按顺序合并回原数组
        index = 0
        for bucket in buckets:
            for num in bucket:
                arr[index] = num
                index += 1

        return arr

    # 对每一位进行排序
    for digit in range(max_digits):
        arr = counting_sort_by_digit(arr, digit)

    return arr
```

### 排序算法时间与空间复杂度对比

**参数说明**

1. **$n$**：数组长度。
2. **$k$**：数据范围（如计数排序中的最大值）。
3. **$d$**：数字的最大位数（如基数排序中需要处理的位数）。

| 排序算法         | 最好时间复杂度       | 平均时间复杂度       | 最坏时间复杂度       | 空间复杂度       | 稳定性   |
|------------------|---------------------|---------------------|---------------------|-----------------|----------|
| **冒泡排序**     | $O(n)$             | $O(n^2)$           | $O(n^2)$           | $O(1)$          | 稳定     |
| **选择排序**     | $O(n^2)$           | $O(n^2)$           | $O(n^2)$           | $O(1)$          | 不稳定   |
| **插入排序**     | $O(n)$             | $O(n^2)$           | $O(n^2)$           | $O(1)$          | 稳定     |
| **快速排序**     | $O(n \log n)$      | $O(n \log n)$      | $O(n^2)$           | $O(\log n)$     | 不稳定   |
| **归并排序**     | $O(n \log n)$      | $O(n \log n)$      | $O(n \log n)$      | $O(n)$          | 稳定     |
| **堆排序**       | $O(n \log n)$      | $O(n \log n)$      | $O(n \log n)$      | $O(1)$          | 不稳定   |
| **计数排序**     | $O(n + k)$         | $O(n + k)$         | $O(n + k)$         | $O(k)$          | 稳定     |
| **基数排序**     | $O(d \cdot (n + k))$ | $O(d \cdot (n + k))$ | $O(d \cdot (n + k))$ | $O(n + k)$    | 稳定     |

## 2. 分治法（Divide & Conquer）

- **模板**：
    1. 分解问题
    2. 解决子问题
    3. 合并结果
- **应用**：归并排序、快速排序、Strassen矩阵乘法,斐波拉契数列,跳点问题
- **举例**:

  ```python
  def Fibonacci(n):
      if n <= 1:  # 边界条件
        return 1
      return Fibonacci(n-1) + Fibonacci(n-2)
  ```

## 2. 动态规划（DP）

### 背包问题

1. **0-1背包**

```python
def knapsack_01(W, weights, values):
    n = len(weights)
    dp = [0] * (W + 1)
    for i in range(n):
        for j in range(W, weights[i] - 1, -1):
            dp[j] = max(dp[j], dp[j - weights[i]] + values[i])
    return dp[W]
```

2. **完全背包**

```python
def knapsack_unbounded(W, weights, values):
    n = len(weights)
    dp = [0] * (W + 1)
    for i in range(n):
        for j in range(weights[i], W + 1):
            dp[j] = max(dp[j], dp[j - weights[i]] + values[i])
    return dp[W]
```

3. **分组背包**

```python
def knapsack_grouped(W, groups):
    dp = [0] * (W + 1)
    for group in groups:
        for j in range(W, -1, -1):  # 内层逆序
            for weight, value in group:
                if j >= weight:
                    dp[j] = max(dp[j], dp[j - weight] + value)
    return dp[W]
```

4. **多重背包(二进制优化)**

```python
def knapsack_multiple(W, weights, values, counts):
    n = len(weights)
    new_weights, new_values = [], []

    # 二进制优化拆分
    for i in range(n):
        count = counts[i]
        k = 1
        while k <= count:
            new_weights.append(weights[i] * k)
            new_values.append(values[i] * k)
            count -= k
            k *= 2
        if count > 0:
            new_weights.append(weights[i] * count)
            new_values.append(values[i] * count)

    # 转化为01背包问题求解
    dp = [0] * (W + 1)
    for i in range(len(new_weights)):
        for j in range(W, new_weights[i] - 1, -1):
            dp[j] = max(dp[j], dp[j - new_weights[i]] + new_values[i])
    return dp[W]
```

5. **对比**

| 背包类型      | 物品选择规则                     | 遍历顺序       | 时间复杂度           | 空间复杂度     | 应用场景                           |
|---------------|----------------------------------|----------------|----------------------|----------------|------------------------------------|
| **01背包**    | 每种物品最多选一次               | 内层逆序       | $O(n \cdot W)$      | $O(W)$         | 基础背包问题，物品不可重复选择     |
| **无限背包**  | 每种物品可选多次                 | 内层正序       | $O(n \cdot W)$      | $O(W)$         | 物品数量无限制，允许重复选择       |
| **分组背包**  | 每组最多选一个物品               | 内层逆序       | $O(\text{组数} \cdot W)$ | $O(W)$         | 组内互斥，每组最多选一个           |
| **多重背包**  | 每种物品有固定数量限制           | 内层逆序（优化前：$O(k \cdot W)$，优化后：$O(\log k \cdot W)$） | $O(\sum \log k_i \cdot W)$ | $O(W)$         | 物品数量有限，二进制优化提高效率   |

---

### 最短编辑距离

```python
def min_edit_distance(A, B):
    m, n = len(A), len(B)
    # 初始化 dp 数组
    dp = [[0] * (n + 1) for _ in range(m + 1)]

    # 边界条件
    for i in range(1, m + 1):
        dp[i][0] = i  # 删除 A 中的所有字符
    for j in range(1, n + 1):
        dp[0][j] = j  # 插入 B 中的所有字符

    # 填充 dp 表
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if A[i - 1] == B[j - 1]:
                dp[i][j] = dp[i - 1][j - 1]
            else:
                dp[i][j] = min(dp[i - 1][j] + 1,  # 删除
                               dp[i][j - 1] + 1,  # 插入
                               dp[i - 1][j - 1] + 1)  # 替换
    return dp[m][n]
```

### 最长公共子序列

```python
def longest_common_subsequence(A, B):
    m, n = len(A), len(B)
    # 初始化 dp 数组
    dp = [[0] * (n + 1) for _ in range(m + 1)]

    # 填充 dp 表
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if A[i - 1] == B[j - 1]:
                dp[i][j] = dp[i - 1][j - 1] + 1
            else:
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])

    # 返回结果
    return dp[m][n]
```

### 最长递增子序列

```python
def length_of_LIS(nums):
    if not nums:
        return 0

    n = len(nums)
    dp = [1] * n  # 初始化每个位置的 LIS 长度为 1

    for i in range(1, n):
        for j in range(i):
            if nums[i] > nums[j]:
                dp[i] = max(dp[i], dp[j] + 1)

    return max(dp)


from bisect import bisect_left


# 优化版
def length_of_LIS(nums):
    if not nums:
        return 0
    n = len(nums)
    dp = [1] * n
    lis = []
    for i in range(1, n):
        index = bisect_left(lis, nums[i])
        dp[i] = index + 1
        if index == len(lis):
            lis.append(nums[i])
        else:
            lis[index] = nums[i]
    return len(lis), dp
```

### 最长回文子串

```python
def longest_palindromic_substring_dp(s):
    n = len(s)
    dp = [[False] * n for _ in range(n)]
    longest = ""

    # 填充 dp 表
    for length in range(1, n + 1):  # 子串长度从 1 到 n
        for i in range(n - length + 1):
            j = i + length - 1
            if length == 1:
                dp[i][j] = True  # 单个字符是回文
            elif length == 2:
                dp[i][j] = (s[i] == s[j])  # 两个字符相等时是回文
            else:
                dp[i][j] = (s[i] == s[j] and dp[i + 1][j - 1])

            # 更新最长回文子串
            if dp[i][j] and length > len(longest):
                longest = s[i:j + 1]

    return longest
```

### 数位DP

> 给定范围 [L, R]，求出其中所有数字的数字和（即每个数字的各位数字之和）的总和。

```python
def sum_of_digit_sums(n):
    s = str(n)
    length = len(s)
    # 定义记忆化表 dp[pos][sum][tight]
    dp = [[[None] * 2 for _ in range(100)] for __ in range(length)]

    def dfs(pos, current_sum, tight):
        if pos == length:
            return current_sum  # 返回当前的数字和
        if dp[pos][current_sum][tight] is not None:  # 如果已经计算过，直接返回结果
            return dp[pos][current_sum][tight]

        limit = int(s[pos]) if tight else 9
        total = 0
        for digit in range(0, limit + 1):
            new_tight = tight and (digit == limit)
            total += dfs(pos + 1, current_sum + digit, new_tight)

        dp[pos][current_sum][tight] = total  # 记录结果
        return total

    return dfs(0, 0, True)

```

## 3. 贪心算法

### 霍夫曼编码（最小带权路径）

```python
# 定义一个节点类
class HuffmanNode:
    def __init__(self, char=None, freq=0, left=None, right=None):
        self.char = char  # 字符
        self.freq = freq  # 频率
        self.left = left  # 左子节点
        self.right = right  # 右子节点

    # 比较运算符重载，用于优先队列排序
    def __lt__(self, other):
        return self.freq < other.freq


import heapq


# 构建霍夫曼树
def build_huffman_tree(freq_map):
    # 使用最小堆来存储节点
    heap = []
    for char, freq in freq_map.items():
        heapq.heappush(heap, HuffmanNode(char, freq))  # 将每个字符作为叶子节点加入堆中

    # 合并节点直到只剩下一个根节点
    while len(heap) > 1:
        left = heapq.heappop(heap)
        right = heapq.heappop(heap)
        merged = HuffmanNode(None, left.freq + right.freq, left, right)  # 创建新节点
        heapq.heappush(heap, merged)

    return heap[0]  # 返回霍夫曼树的根节点
```

### 区间调度（最多不重叠区间

> **问题描述**:给定一组区间，每个区间表示为 [start, end]，表示一个任务从 start 时间开始到 end
> 时间结束。要求从中选择尽可能多的区间，使得这些区间互不重叠。

```python
def interval_scheduling(intervals):
    # 按照结束时间排序
    intervals.sort(key=lambda x: x[1])

    # 初始化结果集
    result = []
    current_end = float('-inf')  # 当前已选区间的结束时间

    # 贪心选择
    for start, end in intervals:
        if start >= current_end:  # 如果当前区间与已选区间不重叠
            result.append([start, end])
            current_end = end  # 更新当前结束时间

    return result
```

## 4. 回溯法

- **框架**：

  ```python
  def backtrack(path, choices):
      """
      if 满足条件:
          记录结果
          return
      for 选择 in 选择列表:
          做选择
          backtrack(path, choices)
          撤销选择
      """
      pass 
  ```

### 全排列

```python
def permute(nums):
    def backtrack(path, choices):
        # 如果选择列表为空，说明找到一个排列
        if not choices:
            result.append(path[:])  # 记录结果
            return

        for i in range(len(choices)):
            # 做选择
            num = choices[i]
            path.append(num)
            # 递归
            backtrack(path, choices[:i] + choices[i + 1:])
            # 撤销选择
            path.pop()

    result = []
    backtrack([], nums)
    return result
```

### N皇后

> **问题描述**: 在 N×N 的棋盘上放置 N 个皇后，使得它们互不攻击（即任意两个皇后不在同一行、列或对角线上）。返回所有可能的解决方案。

```python
def solve_n_queens(n):
    def is_valid(row, col):
        # 检查列冲突
        if col in cols:
            return False
        # 检查主对角线冲突 (row - col 相同)
        if row - col in diag1:
            return False
        # 检查副对角线冲突 (row + col 相同)
        if row + col in diag2:
            return False
        return True

    def backtrack(row):
        # 如果已经放置了 N 个皇后，记录当前解
        if row == n:
            result.append(["".join(row) for row in board])
            return

        for col in range(n):
            if is_valid(row, col):
                # 做选择
                board[row][col] = "Q"
                cols.add(col)
                diag1.add(row - col)
                diag2.add(row + col)
                # 递归
                backtrack(row + 1)
                # 撤销选择
                board[row][col] = "."
                cols.remove(col)
                diag1.remove(row - col)
                diag2.remove(row + col)

    # 初始化棋盘
    board = [["."] * n for _ in range(n)]
    cols = set()  # 列集合
    diag1 = set()  # 主对角线集合
    diag2 = set()  # 副对角线集合
    result = []
    backtrack(0)
    return result
```

### 数独求解

>
> **约束条件：**
> 每一行必须包含数字 1 到 9，且不能重复。
> 每一列必须包含数字 1 到 9，且不能重复。
> 每个小宫格（3×3 区块）必须包含数字 1 到 9，且不能重复。

```python
def solve_sudoku(board):
    def is_valid(row, col, num):
        # 检查行和列是否有冲突
        for i in range(9):
            if board[row][i] == num or board[i][col] == num:
                return False
        # 检查 3x3 小方格是否有冲突
        start_row, start_col = 3 * (row // 3), 3 * (col // 3)
        for i in range(start_row, start_row + 3):
            for j in range(start_col, start_col + 3):
                if board[i][j] == num:
                    return False
        return True

    def backtrack():
        for row in range(9):
            for col in range(9):
                if board[row][col] == ".":
                    for num in "123456789":
                        if is_valid(row, col, num):
                            # 做选择
                            board[row][col] = num
                            # 递归
                            if backtrack():
                                return True
                            # 撤销选择
                            board[row][col] = "."
                    return False  # 如果尝试所有数字都失败，返回 False
        return True  # 如果所有格子都填满，返回 True

    backtrack()

```

---

## 5. 二分搜索

### 二分查找

#### 有序数组(元素唯一)

```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

#### 有序数组(元素重复)

```python
def binary_search_left(arr, target):
    left, right = 0, len(arr) - 1
    result = -1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            result = mid
            right = mid - 1
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return result

```

#### 寻找两个有序数组的中间值

```python
from typing import List


class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        if len(nums1) > len(nums2):
            return self.findMedianSortedArrays(nums2, nums1)
        m, n = len(nums1), len(nums2)
        left, right = 0, m
        INF = float('inf')
        left_max, right_min = -INF, INF
        while left <= right:
            i = (left + right) // 2
            j = (m + n + 1) // 2 - i
            num_i = INF if i == m else nums1[i]
            num_i_1 = -INF if i == 0 else nums1[i - 1]
            num_j = INF if j == n else nums2[j]
            num_j_1 = -INF if j == 0 else nums2[j - 1]
            if num_i_1 <= num_j:
                left_max = max(num_i_1, num_j_1)
                right_min = min(num_j, num_i)
                left += 1
            else:
                right -= 1
        return (left_max + right_min) / 2 if (m + n) % 2 == 0 else left_max
```

#### N个有序数组查找第k小数

```python
def count_less_equal(arrays, mid):
    # 统计总共不超过 mid 的元素个数
    total = 0
    for arr in arrays:
        # 使用 bisect_right 找出 <= mid 的元素个数
        import bisect
        total += bisect.bisect_right(arr, mid)
    return total


def kth_smallest_n_arrays_binary(arrays, k):
    # 初始左右边界
    left = min(arr[0] for arr in arrays if arr)
    right = max(arr[-1] for arr in arrays if arr)

    while left < right:
        mid = (left + right) // 2
        cnt = count_less_equal(arrays, mid)
        if cnt < k:
            left = mid + 1
        else:
            right = mid
    return left


if __name__ == '__main__':
    arrays = [
        [1, 4, 7],
        [2, 5, 8],
        [3, 6, 9]
    ]
    k = 5
    print(kth_smallest_n_arrays_binary(arrays, k))  # 输出: 5

```

#### 旋转数组

```python
def search_in_rotated_sorted_array(nums, target):
    left, right = 0, len(nums) - 1

    while left <= right:
        mid = (left + right) // 2

        if nums[mid] == target:
            return mid

        # 左侧子数组有序
        if nums[left] <= nums[mid]:
            if nums[left] <= target < nums[mid]:
                right = mid - 1
            else:
                left = mid + 1
        # 右侧子数组有序
        else:
            if nums[mid] < target <= nums[right]:
                left = mid + 1
            else:
                right = mid - 1

    return -1  # 未找到目标值
```

#### 旋转数组找最小值

```python
from typing import List


class Solution:
    def minInRotateArray(self, rotateArray: List[int]) -> int:
        left, right = 0, len(rotateArray) - 1

        while left < right:
            mid = (left + right) // 2

            if rotateArray[mid] > rotateArray[right]:
                # 最小值在右边
                left = mid + 1
            elif rotateArray[mid] < rotateArray[right]:
                # 最小值在左边
                right = mid
            else:
                # 相等时，缩小右边界（不能确定在哪边）
                right -= 1

        # 最终 left == right，指向最小值
        return rotateArray[left]
```

### 二分除法

> **问题描述**:
> 给定两个整数 dividend 和 divisor，计算它们的商（结果为整数），并满足以下要求：

1. 不使用乘法 $*$、除法 $/$ 和取模 $\%$ 运算符。
2. 结果需要向零取整（即截断小数部分）

```python
def divide(dividend, divisor):
    # 处理特殊情况：溢出
    if divisor == 0:
        raise ZeroDivisionError("division by zero")
    # 确定结果的符号
    negative = (dividend < 0) ^ (divisor < 0)
    dividend, divisor = abs(dividend), abs(divisor)

    quotient = 0
    while dividend >= divisor:
        # 快速找到当前最大的倍数
        temp_divisor, multiple = divisor, 1
        while dividend >= (temp_divisor << 1):  # 左移一位相当于乘以 2
            temp_divisor <<= 1
            multiple <<= 1

        # 减去当前的最大倍数，并累加结果
        dividend -= temp_divisor
        quotient += multiple

    # 调整符号
    return -quotient if negative else quotient

```

### 快速幂

```python
def fast_power(base, exponent):
    result = 1
    while exponent > 0:
        if exponent % 2 == 1:  # 检查指数是否为奇数
            result *= base
        base *= base  # 底数自乘
        exponent //= 2  # 指数右移一位（整除2）
    return result
```

## 6. 滑动窗口

滑动窗口（Sliding
Window）是一种常用的算法技巧，主要用于处理数组、字符串或序列中的子数组、子字符串等问题。它的核心思想是通过维护一个窗口（通常是一个区间或子集），在遍历过程中动态调整窗口的起始和结束位置，从而避免重复计算，提高算法效率。

### 两数之和

> **问题描述**:
> 给定一个有序数组 nums 和一个目标值 target，请在数组中找到两个数，使它们的和等于目标值，并返回这两个数的索引。假设每个输入有且仅有一个解，且同一个元素不能使用两次。

```python
def two_sum_sorted(nums, target):
    # 初始化左右指针
    left, right = 0, len(nums) - 1

    while left < right:
        current_sum = nums[left] + nums[right]

        if current_sum == target:
            return [left, right]  # 返回索引
        elif current_sum < target:
            left += 1  # 和太小，移动左指针
        else:
            right -= 1  # 和太大，移动右指针

    return [-1, -1]  # 如果未找到，返回 [-1, -1]
```

### 三数之和

> **问题描述**:
> 给定一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a ，b ，c ，使得 a + b + c = 0 ？请找出所有和为 0 且 不重复
> 的三元组。

```python
from typing import List


def threeSum(self, nums: List[int]) -> List[List[int]]:
    # 对数组进行排序
    nums.sort()
    result = []
    n = len(nums)

    for i in range(n):
        # 跳过重复的固定数
        if i > 0 and nums[i] == nums[i - 1]:
            continue

        # 固定 nums[i]，寻找两数之和等于 -nums[i]
        target = -nums[i]
        left, right = i + 1, n - 1

        while left < right:
            current_sum = nums[left] + nums[right]

            if current_sum == target:
                # 找到一组满足条件的三元组
                result.append([nums[i], nums[left], nums[right]])

                # 移动指针并跳过重复的数字
                left += 1
                right -= 1
                while left < right and nums[left] == nums[left - 1]:
                    left += 1
                while left < right and nums[right] == nums[right + 1]:
                    right -= 1

            elif current_sum < target:
                left += 1  # 和太小，移动左指针
            else:
                right -= 1  # 和太大，移动右指针

    return result
```

### 统计好子数组的数目

>
> **问题描述**:
> 给你一个整数数组 nums 和一个整数 k ，请你返回 nums 中 好 子数组的数目。
> 一个子数组 arr 如果有 至少 k 对下标 (i, j) 满足 i < j 且 arr[i] == arr[j] ，那么称它是一个 好 子数组。
> 子数组 是原数组中一段连续 非空 的元素序列。

```python
from typing import List
from collections import defaultdict


class Solution:
    def countGood(self, nums: List[int], k: int) -> int:
        left = 0
        pairs = 0
        freq = defaultdict(int)
        res = 0

        for right in range(len(nums)):
            # 更新当前数字的频率，并增加新产生的数对数量
            freq[nums[right]] += 1
            pairs += freq[nums[right]] - 1

            # 当满足条件时，收缩左边界并累加结果
            while pairs >= k:
                res += len(nums) - right  # 当前窗口的所有子数组都满足条件
                freq[nums[left]] -= 1
                pairs -= freq[nums[left]]  # 减去移除元素导致的数对减少
                left += 1

        return res
```

**总结**

滑动窗口的主要适用范围包括：

1. **连续性**：问题涉及连续子数组或子字符串。
2. **窗口特性**：窗口大小可以是固定的或动态变化的。
3. **优化需求**：需要优化时间复杂度，避免暴力枚举。
4. **频率或统计**：需要统计窗口内元素的频率或其他属性。
5. **流式数据处理**：需要处理实时数据或数据流。

## 7.分支限界

分支限界（Branch and Bound）是一种用于解决优化问题的算法，它通过在搜索树中剪枝来提高搜索效率。它通过在搜索过程中对搜索空间进行限制，从而减少搜索的分支数量，提高搜索效率。

### 旅行商问题

```python

import heapq

import math
import copy


def tsp_branch_and_bound(adjacency_matrix):
    n = len(adjacency_matrix)
    pq = []  # 优先队列
    best_cost = math.inf  # 最优解的初始值为无穷大
    best_path = None
    # 初始化根节点
    root_path = [0]  # 从城市0开始
    root_cost = 0
    root_bound = 0  # 初始下界设为0
    root_set = set([i for i in range(1, n)])
    heapq.heappush(pq, (root_bound, root_cost, root_path, root_set))
    while pq:
        bound, cost, path, s = heapq.heappop(pq)
        # 如果当前节点的下界大于等于已知最优解，则剪枝
        if bound >= best_cost:
            continue
        # 扩展当前节点
        last_city = path[-1]
        for next_city in s:
            new_path = path + [next_city]
            new_cost = cost + adjacency_matrix[last_city][next_city]
            new_set = copy.deepcopy(s)
            new_set.remove(next_city)
            # 计算新节点的下界
            new_bound = new_cost
            if len(new_path) == n - 1:
                end = new_set.pop()
                new_cost += adjacency_matrix[new_path[-1]][end] + adjacency_matrix[end][new_path[0]]
                new_path.append(end)[new_path[0]]
                if new_cost < best_cost:
                    best_cost = new_cost
                    best_path = new_path + [new_path[0]]
            else:
                for i in new_set:
                    # 找到未访问城市的最小出边
                    min_edge = min([adjacency_matrix[i][j] for j in new_set if j != i])
                    new_bound += min_edge
                # 将新节点加入优先队列
                if new_bound < best_cost:
                    heapq.heappush(pq, (new_bound, new_cost, new_path, new_set))
    return best_path, best_cost
```

## 前缀和

### 和为K的子数组

> **问题描述**:给你一个整数数组 nums 和一个整数 k ，请你统计并返回 该数组中和为 k 的子数组的个数 。子数组是数组中元素的连续非空序列。

```python
from collections import defaultdict
from typing import List


class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        map = defaultdict(int)
        map[0] = 1
        prefix = 0
        answer = 0
        for num in nums:
            prefix += num
            answer += map[prefix - k]
            map[prefix] += 1
        return answer
```

## 差分

# 四、高级专题

## 1. 数论算法

### 质数筛法

```python
# Definition for singly-linked list.
def sieve_of_eratosthenes(limit):
    # 创建一个布尔数组"prime[0..limit]"并初始化为True。
    # 一个索引如果为质数，则对应的值保持为True；否则设为False。
    prime = [True for _ in range(limit + 1)]
    p = 2
    while (p * p <= limit):
        # 如果prime[p]没有被改变, 则说明p是质数
        if prime[p]:
            # 更新所有p的倍数为非质数
            for i in range(p * p, limit + 1, p):
                prime[i] = False
        p += 1

    # 打印所有质数
    primes = [p for p in range(2, limit + 1) if prime[p]]
    return primes


if __name__ == "__main__":
    limit = 100
    primes = sieve_of_eratosthenes(limit)
    print(primes)
```

### 最大公约数

```python

def gcd(a, b):
    if b == 0:
        return a
    return gcd(b, a % b)
```

## 2. 字符串算法

- **匹配算法**：
    - KMP（部分匹配表）
    - Rabin-Karp（哈希滚动）
- **高级结构**：
    - Trie树（前缀匹配）
    - 后缀数组（DC3算法）

### AC自动机

```python
from collections import deque


class Node:
    def __init__(self):
        self.children = {}
        self.fail = None
        self.is_end = False
        self.output = []  # 当前节点及其fail路径上所有匹配的模式串


class AC_Automaton:
    def __init__(self, words):
        self.root = Node()
        for word in words:
            self.insert(word)
        self.build_fail()

    def insert(self, word):
        cur = self.root
        for ch in word:
            if ch not in cur.children:
                cur.children[ch] = Node()
            cur = cur.children[ch]
        if cur != self.root:
            cur.is_end = True
            cur.output.append(word)  # 将当前模式串加入输出链表

    def build_fail(self):
        for _, node in self.root.children.items():
            node.fail = self.root
        queue = deque([node for node in self.root.children.values()])
        while queue:
            cur = queue.popleft()
            for ch, node in cur.children.items():
                p = cur.fail
                while p is not None:
                    if ch in p.children:
                        node.fail = p.children[ch]
                        break
                    p = p.fail
                if p is None:
                    node.fail = self.root
                node.output += node.fail.output
                queue.append(node)

    def search(self, text):
        cur = self.root
        ans = []
        for ch in text:
            # 如果当前字符不在子节点中，沿着fail指针回溯
            while ch not in cur.children and cur != self.root:
                cur = cur.fail
            cur = cur.children.get(ch, self.root)
            # 检查当前节点及其fail指针指向的节点是否为模式串的结尾
            # 直接检查当前节点的输出链表
            ans.extend(cur.output)
        return ans


if __name__ == '__main__':
    words = ["aa", "bb", "cc", "dd"]
    ac = AC_Automaton(words)
    print(ac.search(text="aabbccdd"))
```

## 2. 计算几何

- 凸包算法（Graham扫描）
- 最近点对问题（分治法）

## 3. 网络流算法

- Ford-Fulkerson方法（最大流）
- 二分图匹配（匈牙利算法）

## 4. NP完全理论

**P** 是能在多项式时间内解决的问题；  
**NP** 是解能在多项式时间内验证的问题，包含 P；  
**NPC** 是 NP 中最难的问题，其他 NP 问题都能规约到它。

核心问题是：是否 **P = NP**？ 目前未知。

### 子集和问题

```python
def canPartition(nums, target):
    # 如果目标值大于数组总和，直接返回 False
    if sum(nums) < target:
        return False

    # 初始化 DP 数组
    dp = [False] * (target + 1)
    dp[0] = True  # 和为 0 的子集总是存在（空集）

    # 动态规划填充 DP 数组
    for num in nums:
        for j in range(target, num - 1, -1):  # 从后向前更新
            dp[j] = dp[j] or dp[j - num]

    # 返回结果
    return dp[target]
```

---

## 5.位运算

> **题目描述**
> 给定一个长度为 $n$ 的数组 `arr` 和 $m$ 个位运算操作（包括按位与 `&`、按位或 `|`、按位异或 `^`
> ），每个操作会对数组中的所有元素进行相应的位运算。请设计一个算法，高效地对数组中的每个元素逐一应用这些操作，并输出最终结果。
> 由于直接对每个元素逐一应用所有操作的时间复杂度为 $O(n \cdot m)$，在 $n$ 和 $m$ 较大时效率较低，请优化你的算法以降低时间复杂度。

```python
def apply_bitwise_operations(arr, operations):
    # 初始化 state_0 和 state_1
    state_0 = [0] * 32  # 从 0 出发的状态
    state_1 = [1] * 32  # 从 1 出发的状态

    # 预处理每一位的状态
    for op, value in operations:
        for i in range(32):
            bit = (value >> i) & 1  # 获取 value 的第 i 位
            if op == '&':
                state_0[i] &= bit
                state_1[i] &= bit
            elif op == '|':
                state_0[i] |= bit
                state_1[i] |= bit
            elif op == '^':
                state_0[i] ^= bit
                state_1[i] ^= bit

    # 更新数组中的每个元素
    for i in range(len(arr)):
        result = 0
        for j in range(32):
            if (arr[i] >> j) & 1:  # 当前元素的第 j 位是 1
                result |= (state_1[j] << j)
            else:  # 当前元素的第 j 位是 0
                result |= (state_0[j] << j)
        arr[i] = result

    return arr
```

## 构造算法

### 1.回文奇偶性不同构造

```python
def precompute_special_palindromes():
    results = []
    max_val = 10 ** 18

    from collections import deque
    # 存储: (当前数字, 最外层数字, 位数)
    queue = deque()

    # 初始化0-9
    for d in range(10):
        results.append(d)
        queue.append((d, d, 1))

    while queue:
        num, outer_digit, digits = queue.popleft()

        if digits >= 18:
            continue

        # 关键修正：包含0！
        if outer_digit & 1:  # 奇数 -> 可以添加0,2,4,6,8
            candidates = [0, 2, 4, 6, 8]
        else:  # 偶数 -> 添加1,3,5,7,9
            candidates = [1, 3, 5, 7, 9]

        new_digits = digits + 2
        power = 10 ** (digits + 1)

        for digit in candidates:
            # 计算新数字: digit + num + digit
            new_num = digit * power + num * 10 + digit

            if new_num > max_val:
                continue

            # 只有当digit != 0时，new_num才是有效数字（无前导零）
            if digit != 0:
                results.append(new_num)

            # 无论digit是否为0，都要继续扩展（0可以作为中间数字）
            queue.append((new_num, digit, new_digits))

    return sorted(set(results))

```

## 实际应用场景

1. **数据库**：B+树索引、外排序
2. **操作系统**：页面置换算法（LRU）
3. **分布式系统**：一致性哈希
4. **AI**：梯度下降（优化算法）

---
