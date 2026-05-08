
# **第五章 特征值与特征向量**

## **§5.1 特征值与特征向量的概念与计算**

在实际问题中，常常会遇到这样的数学模型：对于一个给定的 $ n $ 阶方阵 $ A $，是否存在非零的 $ n $ 维向量 $ \boldsymbol{\alpha} $，使得矩阵 $ A $ 作用于该向量后，结果仍与原向量平行。即是否存在常数 $ \lambda $，使得  
$$
A\boldsymbol{\alpha} = \lambda\boldsymbol{\alpha}
$$
成立。这就是**特征值与特征向量**的问题。

---

### 一、基本概念

#### 定义

设 $ A $ 是一个 $ n $ 阶方阵，如果存在数 $ \lambda $ 和非零 $ n $ 维向量 $ \boldsymbol{\alpha} $，使得  
$$
A\boldsymbol{\alpha} = \lambda\boldsymbol{\alpha},
$$  
则称 $ \lambda $ 为矩阵 $ A $ 的一个**特征值**（eigenvalue），$ \boldsymbol{\alpha} $ 称为 $ A $ 对应于特征值 $ \lambda $ 的一个**特征向量**（eigenvector）。

---

### 二、几何意义

从几何上看，特征向量表示的是在变换 $ A $ 下方向不变的向量，而特征值 $ \lambda $ 表示该向量被拉伸或压缩的比例。例如：

- 若 $ |\lambda| > 1 $，则特征向量被拉长；
- 若 $ |\lambda| < 1 $，则特征向量被压缩；
- 若 $ \lambda = 1 $，则特征向量方向和长度都不变；
- 若 $ \lambda < 0 $，则特征向量反向。

---

### 三、特征值与特征向量的求法

为了求出矩阵 $ A $ 的特征值和特征向量，我们从定义式出发：

$$
A\boldsymbol{\alpha} = \lambda\boldsymbol{\alpha} \Rightarrow (\lambda I - A)\boldsymbol{\alpha} = 0,
$$

其中 $ I $ 是单位矩阵，$ \boldsymbol{\alpha} \neq 0 $。这说明 $ (\lambda I - A) $ 必须是奇异矩阵，即其行列式为零：

$$
\det(\lambda I - A) = 0.
$$

这个方程称为矩阵 $ A $ 的**特征方程**，它的根就是矩阵 $ A $ 的特征值。

---

### 四、求解步骤

1. **写出特征方程**：
   $$
   \det(\lambda I - A) = 0.
   $$

2. **求解特征值**：
   解上述代数方程，得到所有不同的特征值 $ \lambda_1, \lambda_2, \dots, \lambda_k $（可能有重复）。

3. **对每个特征值 $ \lambda_i $，求对应的特征向量**：
   - 求解齐次线性方程组 $ (\lambda_i I - A)\mathbf{x} = 0 $。
   - 找出其基础解系 $ \boldsymbol{\alpha}_1, \boldsymbol{\alpha}_2, \dots, \boldsymbol{\alpha}_r $。
   - 则对应于 $ \lambda_i $ 的全部特征向量为：
     $$
     k_1\boldsymbol{\alpha}_1 + k_2\boldsymbol{\alpha}_2 + \cdots + k_r\boldsymbol{\alpha}_r,\quad (k_1, k_2, \dots, k_r \text{ 不全为零}).
     $$

---

### 五、特征子空间

对于每一个特征值 $ \lambda $，所有对应的特征向量加上零向量构成一个向量空间，称为**特征子空间**，记作 $ V_\lambda $，即：

$$
V_\lambda = \left\{ \boldsymbol{\alpha} \in \mathbb{C}^n \mid A\boldsymbol{\alpha} = \lambda\boldsymbol{\alpha} \right\}.
$$

这是一个子空间，其维数等于基础解系中向量的个数，也即：

$$
\dim(V_\lambda) = n - \text{rank}(\lambda I - A).
$$

---

### 六、代数重数与几何重数

设 $ A $ 是一个 $ n $ 阶矩阵，其**特征多项式**定义为：
$$
f(\lambda) = |\lambda I - A| = (\lambda - \lambda_1)^{k_1}(\lambda - \lambda_2)^{k_2} \cdots (\lambda - \lambda_s)^{k_s}
$$
其中，$ \lambda_1, \lambda_2, \dots, \lambda_s $ 是互不相同的特征值，$ k_1 + k_2 + \cdots + k_s = n $。

称 $ k_i $ 为特征值 $ \lambda_i $ 的**代数重数**。

对于每个特征值 $ \lambda_i $，对应的**特征子空间**定义为：
$$
V_{\lambda_i} = \{ x \in \mathbb{C}^n \mid (A - \lambda_i I)x = 0 \}
$$
该子空间的维数称为 $ \lambda_i $ 的**几何重数**。

可以证明：  
**特征值的几何重数不大于它的代数重数。**

即：如果 $ \lambda_i $ 是矩阵 $ A $ 的一个 $ k_i $ 重特征值（代数重数为 $ k_i $），则对应于 $ \lambda_i $ 的线性无关的特征向量的个数（即特征子空间的维数）不超过 $ k_i $。

换句话说，齐次方程组 $ (A - \lambda_i I)x = 0 $ 的基础解系所含解向量的个数（即解空间的维数）不超过 $ k_i $。

---

### 七、特征多项式的性质

设 $ A $ 是一个 $ n \times n $ 矩阵，其特征多项式为：

$$
f_A(\lambda) = \det(\lambda I - A) = \lambda^n + a_{n-1}\lambda^{n-1} + \cdots + a_1\lambda + a_0.
$$

又设 $ f_A(\lambda) $ 的所有根为 $ \lambda_1, \lambda_2, \dots, \lambda_n $，则：

- **迹（trace）公式**：
  $$
  \lambda_1 + \lambda_2 + \cdots + \lambda_n = \text{tr}(A) = a_{11} + a_{22} + \cdots + a_{nn}.
  $$
- **行列式公式**：
  $$
  \lambda_1 \lambda_2 \cdots \lambda_n = \det(A).
  $$

由此可得：

- 方阵可逆当且仅当其所有特征值均不为零；
- 若 $ A $ 是实对称矩阵，则其特征值均为实数，且存在正交的特征向量基。

这是一个非常经典且重要的矩阵性质，它揭示了**特征值的和等于矩阵的迹（trace）**，而**特征值的乘积等于矩阵的行列式（determinant）**。下面我们来详细地证明这两个公式。

#### 迹（trace）公式的证明

##### 目标

证明：
$$
\lambda_1 + \lambda_2 + \cdots + \lambda_n = \text{tr}(A).
$$

##### 证明

我们从特征多项式出发：

$$
f_A(\lambda) = \det(\lambda I - A) = (\lambda - \lambda_1)(\lambda - \lambda_2)\cdots(\lambda - \lambda_n).
$$

展开右边这个多项式后，其形式是：

$$
f_A(\lambda) = \lambda^n - (\lambda_1 + \lambda_2 + \cdots + \lambda_n)\lambda^{n-1} + \cdots + (-1)^n \lambda_1\lambda_2\cdots\lambda_n.
$$

另一方面，原特征多项式也可写成：

$$
f_A(\lambda) = \lambda^n + a_{n-1}\lambda^{n-1} + \cdots + a_1\lambda + a_0.
$$

比较两个表达式中 $ \lambda^{n-1} $ 项的系数，得：

$$
a_{n-1} = -(\lambda_1 + \lambda_2 + \cdots + \lambda_n).
$$

因此，

$$
\lambda_1 + \lambda_2 + \cdots + \lambda_n = -a_{n-1}.
$$

但另一方面，我们知道特征多项式 $ f_A(\lambda) = \det(\lambda I - A) $ 展开时，$ a_{n-1} $ 实际上就是 $ -\text{tr}(A) $。这是因为：

在计算 $ \det(\lambda I - A) $ 时，$ \lambda^{n-1} $ 项来自于对角线上元素 $ \lambda - a_{ii} $ 中去掉一项 $ -a_{ii} $，其余保持 $ \lambda $，所以：

$$
a_{n-1} = -\sum_{i=1}^n a_{ii} = -\text{tr}(A).
$$

所以最终得出：

$$
\lambda_1 + \lambda_2 + \cdots + \lambda_n = \text{tr}(A).
$$

---

#### 行列式公式的证明

##### 目标

证明：
$$
\lambda_1 \lambda_2 \cdots \lambda_n = \det(A).
$$

##### 证明

同样从特征多项式出发：

$$
f_A(\lambda) = \det(\lambda I - A) = (\lambda - \lambda_1)(\lambda - \lambda_2)\cdots(\lambda - \lambda_n).
$$

将 $ \lambda = 0 $ 代入两边，得到：

$$
f_A(0) = \det(-A) = (-1)^n \det(A),
$$
同时，
$$
f_A(0) = (0 - \lambda_1)(0 - \lambda_2)\cdots(0 - \lambda_n) = (-1)^n \lambda_1 \lambda_2 \cdots \lambda_n.
$$

于是：

$$
(-1)^n \det(A) = (-1)^n \lambda_1 \lambda_2 \cdots \lambda_n,
$$

两边消去 $ (-1)^n $ 得：

$$
\det(A) = \lambda_1 \lambda_2 \cdots \lambda_n.
$$

---

### 八、典型例题解析

#### **例1**  

设  
$$
A = \begin{bmatrix} 1 & 3 \\ 3 & 1 \end{bmatrix},
$$  
求其特征值与特征向量。

**解：**

1. 写出特征方程：
   $$
   \det(\lambda I - A) = \begin{vmatrix} \lambda - 1 & -3 \\ -3 & \lambda - 1 \end{vmatrix} = (\lambda - 1)^2 - 9 = \lambda^2 - 2\lambda - 8.
   $$

2. 解方程：
   $$
   \lambda^2 - 2\lambda - 8 = 0 \Rightarrow \lambda_1 = 4, \quad \lambda_2 = -2.
   $$

3. 对应于 $ \lambda_1 = 4 $ 的特征向量：

   $$
   (4I - A) = \begin{bmatrix} 3 & -3 \\ -3 & 3 \end{bmatrix}, \quad \text{解得} \quad x_1 = x_2.
   $$

   取 $ x_2 = 1 $，得特征向量 $ \boldsymbol{\alpha}_1 = \begin{bmatrix} 1 \\ 1 \end{bmatrix} $。

4. 对应于 $ \lambda_2 = -2 $ 的特征向量：

   $$
   (-2I - A) = \begin{bmatrix} -3 & -3 \\ -3 & -3 \end{bmatrix}, \quad \text{解得} \quad x_1 = -x_2.
   $$

   取 $ x_2 = 1 $，得特征向量 $ \boldsymbol{\alpha}_2 = \begin{bmatrix} -1 \\ 1 \end{bmatrix} $。

---

#### **例2**  

已知矩阵 $ A $ 满足 $ A^2 = A $，证明其特征值只能是 0 或 1。

**证：**  
设 $ \lambda $ 是 $ A $ 的特征值，$ \boldsymbol{\alpha} $ 是对应的特征向量，则：

$$
A\boldsymbol{\alpha} = \lambda\boldsymbol{\alpha} \Rightarrow A^2\boldsymbol{\alpha} = A(\lambda\boldsymbol{\alpha}) = \lambda A\boldsymbol{\alpha} = \lambda^2\boldsymbol{\alpha}.
$$

又因为 $ A^2 = A $，所以：

$$
A^2\boldsymbol{\alpha} = A\boldsymbol{\alpha} = \lambda\boldsymbol{\alpha} \Rightarrow \lambda^2\boldsymbol{\alpha} = \lambda\boldsymbol{\alpha}.
$$

由于 $ \boldsymbol{\alpha} \neq 0 $，两边约去 $ \boldsymbol{\alpha} $，得：

$$
\lambda^2 = \lambda \Rightarrow \lambda(\lambda - 1) = 0 \Rightarrow \lambda = 0 \text{ 或 } 1.
$$

---

### 九、总结

| 内容 | 描述 |
|------|------|
| 特征值 | 使得 $ A\boldsymbol{\alpha} = \lambda\boldsymbol{\alpha} $ 成立的标量 |
| 特征向量 | 对应于某个特征值的非零向量 |
| 特征方程 | $ \det(\lambda I - A) = 0 $ |
| 特征子空间 | 所有属于某特征值的特征向量及其零向量构成的空间 |
| 几何重数 | 特征子空间的维数 |
| 代数重数 | 特征多项式中该根的重数 |

---

## **§5.2 矩阵的相似对角化**

### **一、相似矩阵的基本概念**

在矩阵理论中，**相似矩阵**是一个非常重要的概念。它描述了两个同阶方阵之间的一种等价关系，反映了它们在不同基下的表示形式。通过相似变换，我们可以将一个复杂的矩阵转化为更简单（如对角矩阵）的形式，从而简化计算与分析。

---

#### **定义：**

设 $ A $ 和 $ B $ 是两个 $ n $ 阶方阵，如果存在一个**可逆矩阵** $ P $，使得  
$$
P^{-1}AP = B,
$$  
则称矩阵 $ A $ 与 $ B $ **相似**，记作：
$$
A \sim B.
$$

---

#### **几何意义：**

相似矩阵代表的是**同一个线性变换在不同基下的矩阵表示**。也就是说，如果我们换一组基来表示同一个线性变换，得到的矩阵就可能是原矩阵的相似矩阵。

---

#### **相似关系的性质：**

相似关系是一种**等价关系**，具有以下三条基本性质：

1. **反身性**：$ A \sim A $；
2. **对称性**：若 $ A \sim B $，则 $ B \sim A $；
3. **传递性**：若 $ A \sim B $ 且 $ B \sim C $，则 $ A \sim C $。

其中，前两条是显然成立的。对于第 3 条，证明如下：

设 $ A \sim B $，即存在可逆矩阵 $ P $，使得  
$$
P^{-1}AP = B.
$$  
又设 $ B \sim C $，即存在可逆矩阵 $ Q $，使得  
$$
Q^{-1}BQ = C.
$$  
将 $ B = P^{-1}AP $ 代入上式得：  
$$
C = Q^{-1}(P^{-1}AP)Q = (PQ)^{-1}A(PQ).
$$  
令 $ R = PQ $，则 $ R $ 可逆，且有  
$$
R^{-1}AR = C,
$$  
因此 $ A \sim C $，传递性得证。

---

### **二、相似矩阵的重要性质**

相似矩阵虽然形式不同，但共享许多重要性质，尤其是在特征值、行列式、迹等方面。

#### **定理1：相似矩阵具有相同的特征值**

设 $ A \sim B $，即存在可逆矩阵 $ P $，使得  
$$
B = P^{-1}AP.
$$  
则它们的特征多项式相同，即  
$$
\det(\lambda I - B) = \det(\lambda I - A),
$$  
因此，$ A $ 与 $ B $ 的特征值完全相同。

**证明：**  
$$
\begin{aligned}
\det(\lambda I - B) &= \det(\lambda I - P^{-1}AP) \\
&= \det(P^{-1}(\lambda I - A)P) \\
&= \det(P^{-1}) \cdot \det(\lambda I - A) \cdot \det(P) \\
&= \det(\lambda I - A),
\end{aligned}
$$  
所以特征多项式相同，特征值也相同。

---

### **三、利用相似化简幂运算**

当 $ A \sim \Lambda $（对角矩阵），即存在可逆矩阵 $ P $，使得  
$$
P^{-1}AP = \Lambda,
$$  
那么可以方便地求出 $ A^k $（$ k $ 为正整数）：

$$
A = P\Lambda P^{-1}, \quad A^k = (P\Lambda P^{-1})^k = P\Lambda^k P^{-1}.
$$

因为对角矩阵的幂很容易计算（只需对角线上元素分别取幂），所以这种方法大大简化了矩阵幂的计算。

---

### **四、什么样的矩阵可以对角化？**

我们自然会提出这样的问题：

> 对于给定的 $ n $ 阶矩阵 $ A $，是否存在一个对角矩阵 $ \Lambda $ 和可逆矩阵 $ P $，使得  
> $$
> P^{-1}AP = \Lambda?
> $$

如果存在这样的矩阵 $ \Lambda $ 和 $ P $，我们就说矩阵 $ A $ **可以对角化**。

#### **结论：**

- 若 $ A $ 有 $ n $ 个**线性无关的特征向量**，则 $ A $ 可以对角化。
- 此时，矩阵 $ P $ 的列就是这些线性无关的特征向量，而 $ \Lambda $ 的主对角线元素就是对应的特征值。

---

### **五、应用举例**

#### **例1：** 设  

$$
A = \begin{bmatrix} 4 & 1 \\ 0 & 3 \end{bmatrix},
$$  
判断 $ A $ 是否可以对角化，并求 $ A^{10} $。

**解：**

1. 求特征值：

$$
\det(\lambda I - A) = \begin{vmatrix} \lambda - 4 & -1 \\ 0 & \lambda - 3 \end{vmatrix} = (\lambda - 4)(\lambda - 3),
$$  
所以特征值为 $ \lambda_1 = 4, \lambda_2 = 3 $。

2. 求特征向量：

- 对应 $ \lambda_1 = 4 $，解 $ (A - 4I)\boldsymbol{x} = 0 $，得特征向量 $ \boldsymbol{\alpha}_1 = \begin{bmatrix} 1 \\ 0 \end{bmatrix} $；
- 对应 $ \lambda_2 = 3 $，解 $ (A - 3I)\boldsymbol{x} = 0 $，得特征向量 $ \boldsymbol{\alpha}_2 = \begin{bmatrix} 1 \\ -1 \end{bmatrix} $。

3. 构造矩阵 $ P $ 和 $ \Lambda $：

$$
P = \begin{bmatrix} 1 & 1 \\ 0 & -1 \end{bmatrix}, \quad \Lambda = \begin{bmatrix} 4 & 0 \\ 0 & 3 \end{bmatrix}.
$$

4. 计算 $ A^{10} $：

$$
A^{10} = P\Lambda^{10}P^{-1}.
$$

由于 $ \Lambda^{10} = \begin{bmatrix} 4^{10} & 0 \\ 0 & 3^{10} \end{bmatrix} $，再结合 $ P $ 和 $ P^{-1} $，即可求出 $ A^{10} $。

---

### **六、总结**

| 性质 | 描述 |
|------|------|
| 相似定义 | $ B = P^{-1}AP $，记为 $ A \sim B $ |
| 等价性质 | 反身性、对称性、传递性 |
| 特征值 | 相似矩阵具有相同的特征值 |
| 幂运算 | 若 $ A \sim \Lambda $，则 $ A^k = P\Lambda^kP^{-1} $ |
| 可对角化条件 | 存在 $ n $ 个线性无关的特征向量 |

---

### **二、矩阵的相似对角化**

在矩阵理论中，**矩阵的相似对角化**是研究矩阵是否可以转化为一个与其相似的对角矩阵的过程。这一过程不仅有助于简化矩阵的运算（如求幂、指数等），而且在工程、物理、计算机科学等领域中具有广泛的应用价值。

---

#### 一、基本概念

设 $ A $ 是一个 $ n $ 阶方阵，如果存在一个可逆矩阵 $ P $ 和一个对角矩阵 $ \Lambda $，使得  
$$
P^{-1}AP = \Lambda,
$$  
则称矩阵 $ A $ **可以对角化**，或称 $ A $ 与对角矩阵 $ \Lambda $ **相似**，记作 $ A \sim \Lambda $。

此时，$ \Lambda $ 的主对角线上的元素就是 $ A $ 的全部特征值，而 $ P $ 的列向量是这些特征值对应的线性无关的特征向量。

---

#### 二、可对角化的充要条件

##### **定理3：**

n阶矩阵 $ A $ 能与对角矩阵相似的充分必要条件是：  
**A 有 n 个线性无关的特征向量**。

换句话说：

- 如果 $ A $ 有 n 个线性无关的特征向量，则 $ A $ 可以对角化；
- 否则，$ A $ 不可对角化。

---

#### 三、如何判断矩阵能否对角化？

我们可以通过以下步骤来判断一个矩阵是否能对角化：

##### **1. 求出所有特征值：**

解特征方程：
$$
\det(\lambda I - A) = 0.
$$

得到所有特征值 $ \lambda_1, \lambda_2, \dots, \lambda_k $，其中每个特征值可能有代数重数 $ m_i $。

##### **2. 对每个特征值，求其对应的特征向量：**

对于每个特征值 $ \lambda_i $，求解齐次线性方程组：
$$
(\lambda_i I - A)\mathbf{x} = 0.
$$

找出其基础解系，即对应于该特征值的线性无关的特征向量。

##### **3. 判断总的线性无关特征向量个数是否为 n：**

将所有特征值对应的特征向量合并起来，如果总共有 $ n $ 个线性无关的特征向量，则 $ A $ 可对角化；否则不可对角化。

---

#### 四、几何重数与代数重数的关系

设 $ \lambda_i $ 是 $ A $ 的一个特征值，其：

- **代数重数**：特征多项式中 $ (\lambda - \lambda_i)^{m_i} $ 的次数；
- **几何重数**：对应于 $ \lambda_i $ 的线性无关特征向量的个数，也即 $ (\lambda_i I - A)\mathbf{x} = 0 $ 的基础解系所含向量个数。

##### **定理5：**

n阶矩阵 $ A $ 能与对角矩阵相似的充分必要条件是：  
对于每一个 k 重特征根 $ \lambda_i $，对应的齐次方程组 $ (\lambda_i I - A)\mathbf{x} = 0 $ 的基础解系由 $ k $ 个解向量组成，即几何重数等于代数重数。

##### **推论3：**

n阶矩阵 $ A $ 能与对角矩阵相似的充分必要条件是：  
对于每个 k 重特征根 $ \lambda_i $，都有  
$$
\text{rank}(\lambda_i I - A) = n - k.
$$

---

#### 五、互异特征值与线性无关特征向量

##### **定理4：**

若 $ \lambda_1, \lambda_2, \dots, \lambda_m $ 是矩阵 $ A $ 的互异特征值，且 $ \boldsymbol{\alpha}_1, \boldsymbol{\alpha}_2, \dots, \boldsymbol{\alpha}_m $ 分别是它们对应的特征向量，则这组特征向量是**线性无关的**。

##### **推论1：**

若 n 阶矩阵 $ A $ 的所有特征值都是单根（即互不相同），则 $ A $ 必可对角化。

---

#### 六、对角化的构造方法

如果矩阵 $ A $ 可对角化，我们可以按如下步骤构造 $ P $ 和 $ \Lambda $：

1. 找出 $ A $ 的所有特征值 $ \lambda_1, \lambda_2, \dots, \lambda_n $；
2. 对每个特征值 $ \lambda_i $，找出其对应的特征向量 $ \boldsymbol{p}_i $；
3. 构造可逆矩阵 $ P = [\boldsymbol{p}_1\ \boldsymbol{p}_2\ \cdots\ \boldsymbol{p}_n] $；
4. 构造对角矩阵 $ \Lambda = \text{diag}(\lambda_1, \lambda_2, \dots, \lambda_n) $；
5. 此时有：
   $$
   P^{-1}AP = \Lambda,\quad A^k = P\Lambda^k P^{-1}.
   $$

---

#### 七、典型例题解析

##### **例1：**  

设  
$$
A = \begin{bmatrix} 2 & 1 \\ 0 & 2 \end{bmatrix},
$$  
判断 $ A $ 是否可以对角化。

**解：**

1. 特征值：
   $$
   \det(\lambda I - A) = \begin{vmatrix} \lambda - 2 & -1 \\ 0 & \lambda - 2 \end{vmatrix} = (\lambda - 2)^2.
   $$  
   所以 $ \lambda = 2 $ 是重根（代数重数为2）。

2. 求特征向量：
   $$
   (2I - A) = \begin{bmatrix} 0 & -1 \\ 0 & 0 \end{bmatrix},\quad \text{解得} \ x_2 = 0.
   $$  
   基础解系只有一个向量 $ \boldsymbol{\alpha} = \begin{bmatrix} 1 \\ 0 \end{bmatrix} $，几何重数为1 ≠ 代数重数2。

因此，$ A $ **不能对角化**。

---

##### **例2：**  

设  
$$
A = \begin{bmatrix} 4 & 1 \\ 0 & 3 \end{bmatrix},
$$  
判断 $ A $ 是否可以对角化，并求 $ A^{10} $。

**解：**

1. 特征值：
   $$
   \det(\lambda I - A) = (\lambda - 4)(\lambda - 3),\quad \lambda_1 = 4,\ \lambda_2 = 3.
   $$

2. 特征向量：

- 对 $ \lambda_1 = 4 $，解得 $ \boldsymbol{\alpha}_1 = \begin{bmatrix} 1 \\ 0 \end{bmatrix} $；
- 对 $ \lambda_2 = 3 $，解得 $ \boldsymbol{\alpha}_2 = \begin{bmatrix} 1 \\ -1 \end{bmatrix} $。

3. 构造 $ P $ 和 $ \Lambda $：

$$
P = \begin{bmatrix} 1 & 1 \\ 0 & -1 \end{bmatrix},\quad \Lambda = \begin{bmatrix} 4 & 0 \\ 0 & 3 \end{bmatrix}.
$$

4. 计算 $ A^{10} = P\Lambda^{10}P^{-1} $，即可完成幂运算。

---

#### 八、特殊情况分析

##### **命题：**

若 $ A \neq 0 $，且 $ A^k = 0 $（幂零矩阵），则 $ A $ **不能与对角矩阵相似**。

**证明：**  
若 $ A $ 可对角化，则其特征值全为 0，从而 $ A = 0 $，与 $ A \neq 0 $ 矛盾。

---

#### 九、总结

| 内容 | 描述 |
|------|------|
| 定义 | 若存在可逆矩阵 $ P $，使得 $ P^{-1}AP = \Lambda $，则称 $ A $ 可对角化 |
| 充要条件 | 存在 $ n $ 个线性无关的特征向量 |
| 几何重数 ≤ 代数重数 | 当且仅当两者相等时，才可对角化 |
| 互异特征值 | 对应的特征向量一定线性无关 |
| 应用 | 可用于快速计算矩阵幂、指数等 |

---

## **§5.3 n维向量空间的正交性**

### **一、内积**

在向量空间中，**内积**（inner product）是一个基本而重要的概念，它不仅刻画了两个向量之间的“夹角”关系，还为向量的长度、正交性等几何性质提供了代数定义。它是欧几里得空间中向量运算的核心工具之一。

---

#### 1. 内积的定义

设  
$$
\boldsymbol{\alpha} = (a_1, a_2, \dots, a_n), \quad \boldsymbol{\beta} = (b_1, b_2, \dots, b_n)
$$  
是 $ \mathbb{R}^n $ 中的两个向量，则它们的**内积**定义为：

$$
(\boldsymbol{\alpha}, \boldsymbol{\beta}) = a_1b_1 + a_2b_2 + \cdots + a_nb_n.
$$

在三维空间 $ \mathbb{R}^3 $ 中，也常记作：
$$
\boldsymbol{\alpha} \cdot \boldsymbol{\beta}.
$$

若将向量看作列向量，则内积也可表示为：
$$
(\boldsymbol{\alpha}, \boldsymbol{\beta}) = \boldsymbol{\alpha}^\top \boldsymbol{\beta}.
$$

---

#### 2. 内积的基本性质

对于任意的 $ \boldsymbol{\alpha}, \boldsymbol{\beta}, \boldsymbol{\gamma} \in \mathbb{R}^n $，以及任意实数 $ k \in \mathbb{R} $，内积满足以下四条基本性质：

1. **非负性：**
   $$
   (\boldsymbol{\alpha}, \boldsymbol{\alpha}) \geq 0, \quad \text{且当且仅当 } \boldsymbol{\alpha} = \boldsymbol{0} \text{ 时等号成立}.
   $$

2. **对称性：**
   $$
   (\boldsymbol{\alpha}, \boldsymbol{\beta}) = (\boldsymbol{\beta}, \boldsymbol{\alpha}).
   $$

3. **线性性（加法）：**
   $$
   (\boldsymbol{\alpha} + \boldsymbol{\beta}, \boldsymbol{\gamma}) = (\boldsymbol{\alpha}, \boldsymbol{\gamma}) + (\boldsymbol{\beta}, \boldsymbol{\gamma}).
   $$

4. **齐次性：**
   $$
   (k\boldsymbol{\alpha}, \boldsymbol{\beta}) = k(\boldsymbol{\alpha}, \boldsymbol{\beta}).
   $$

由此还可推出以下两个常用性质：

- $(\boldsymbol{\alpha}, k\boldsymbol{\beta}) = k(\boldsymbol{\alpha}, \boldsymbol{\beta})$；
- $(\boldsymbol{\alpha}, \boldsymbol{\beta} + \boldsymbol{\gamma}) = (\boldsymbol{\alpha}, \boldsymbol{\beta}) + (\boldsymbol{\alpha}, \boldsymbol{\gamma})$。

---

#### 3. 向量的长度（模）

利用内积可以定义向量的**长度**（或称为**模**）：

$$
\|\boldsymbol{\alpha}\| = \sqrt{(\boldsymbol{\alpha}, \boldsymbol{\alpha})} = \sqrt{a_1^2 + a_2^2 + \cdots + a_n^2}.
$$

向量的长度具有以下三条重要性质：

1. **非负性：**
   $$
   \|\boldsymbol{\alpha}\| \geq 0, \quad \text{当且仅当 } \boldsymbol{\alpha} = \boldsymbol{0} \text{ 时 } \|\boldsymbol{\alpha}\| = 0.
   $$

2. **齐次性：**
   $$
   \|k\boldsymbol{\alpha}\| = |k| \cdot \|\boldsymbol{\alpha}\|, \quad \forall k \in \mathbb{R}.
   $$

3. **三角不等式：**
   $$
   \|\boldsymbol{\alpha} + \boldsymbol{\beta}\| \leq \|\boldsymbol{\alpha}\| + \|\boldsymbol{\beta}\|.
   $$

如果 $ \|\boldsymbol{\alpha}\| = 1 $，则称 $ \boldsymbol{\alpha} $ 为**单位向量**。

对于任意非零向量 $ \boldsymbol{\alpha} $，可以通过归一化得到单位向量：
$$
\frac{\boldsymbol{\alpha}}{\|\boldsymbol{\alpha}\|}.
$$

---

#### 4. 柯西-施瓦茨不等式（Cauchy-Schwarz Inequality）

对于任意的 $ \boldsymbol{\alpha}, \boldsymbol{\beta} \in \mathbb{R}^n $，有：

$$
|(\boldsymbol{\alpha}, \boldsymbol{\beta})| \leq \|\boldsymbol{\alpha}\| \cdot \|\boldsymbol{\beta}\|.
$$

等号成立当且仅当 $ \boldsymbol{\alpha} $ 与 $ \boldsymbol{\beta} $ 线性相关。

这个不等式在理论分析和应用中都非常重要，它是定义向量之间夹角的基础。

---

#### 5. 向量的夹角

对于任意两个非零向量 $ \boldsymbol{\alpha}, \boldsymbol{\beta} \in \mathbb{R}^n $，定义它们之间的**夹角** $ \theta $ 为：

$$
\cos\theta = \frac{(\boldsymbol{\alpha}, \boldsymbol{\beta})}{\|\boldsymbol{\alpha}\| \cdot \|\boldsymbol{\beta}\|},
$$

其中 $ 0 \leq \theta \leq \pi $。

特别地：

- 若 $ (\boldsymbol{\alpha}, \boldsymbol{\beta}) = 0 $，则称 $ \boldsymbol{\alpha} $ 与 $ \boldsymbol{\beta} $ **正交**（垂直），记作 $ \boldsymbol{\alpha} \perp \boldsymbol{\beta} $；
- 若 $ \cos\theta > 0 $，说明两向量夹角小于 $ 90^\circ $；
- 若 $ \cos\theta < 0 $，说明两向量夹角大于 $ 90^\circ $。

---

#### 6. 几何意义总结

| 概念 | 定义 | 几何意义 |
|------|------|-----------|
| 内积 | $ (\boldsymbol{\alpha}, \boldsymbol{\beta}) = a_1b_1 + \cdots + a_nb_n $ | 衡量两个向量方向上的“投影”程度 |
| 长度 | $ \|\boldsymbol{\alpha}\| = \sqrt{(\boldsymbol{\alpha}, \boldsymbol{\alpha})} $ | 向量的大小（模长） |
| 单位向量 | $ \frac{\boldsymbol{\alpha}}{\|\boldsymbol{\alpha}\|} $ | 方向不变，长度为1的向量 |
| 正交 | $ (\boldsymbol{\alpha}, \boldsymbol{\beta}) = 0 $ | 两个向量垂直 |
| 夹角 | $ \cos\theta = \frac{(\boldsymbol{\alpha}, \boldsymbol{\beta})}{\|\boldsymbol{\alpha}\| \cdot \|\boldsymbol{\beta}\|} $ | 表示两个向量之间的相对方向关系 |

---

#### 7. 应用举例

##### **例1：**  

已知向量 $ \boldsymbol{\alpha} = (1, 2, 3) $，求其长度。

**解：**
$$
\|\boldsymbol{\alpha}\| = \sqrt{1^2 + 2^2 + 3^2} = \sqrt{1 + 4 + 9} = \sqrt{14}.
$$

##### **例2：**  

判断向量 $ \boldsymbol{\alpha} = (1, 2) $ 和 $ \boldsymbol{\beta} = (-2, 1) $ 是否正交。

**解：**
$$
(\boldsymbol{\alpha}, \boldsymbol{\beta}) = 1 \cdot (-2) + 2 \cdot 1 = -2 + 2 = 0,
$$  
所以 $ \boldsymbol{\alpha} \perp \boldsymbol{\beta} $。

---

#### 8. 总结

| 概念 | 公式 |
|------|------|
| 内积 | $ (\boldsymbol{\alpha}, \boldsymbol{\beta}) = a_1b_1 + a_2b_2 + \cdots + a_nb_n $ |
| 长度 | $ \|\boldsymbol{\alpha}\| = \sqrt{(\boldsymbol{\alpha}, \boldsymbol{\alpha})} $ |
| 单位向量 | $ \frac{\boldsymbol{\alpha}}{\|\boldsymbol{\alpha}\|} $ |
| 正交 | $ (\boldsymbol{\alpha}, \boldsymbol{\beta}) = 0 $ |
| 夹角余弦 | $ \cos\theta = \frac{(\boldsymbol{\alpha}, \boldsymbol{\beta})}{\|\boldsymbol{\alpha}\| \cdot \|\boldsymbol{\beta}\|} $ |

---

### **二、n维向量的正交性**

在 $ n $ 维向量空间中，**正交性**是一个非常重要的几何与代数概念。它不仅揭示了向量之间的“垂直”关系，还为构造正交基、标准正交基、正交变换等提供了理论基础。

---

#### 1. 正交的定义

##### **定义4：**

如果两个向量 $ \boldsymbol{\alpha} $ 和 $ \boldsymbol{\beta} $ 的内积为零，即  
$$
(\boldsymbol{\alpha}, \boldsymbol{\beta}) = 0,
$$  
则称这两个向量是**正交的**，记作：
$$
\boldsymbol{\alpha} \perp \boldsymbol{\beta}.
$$

特别地：

- 零向量 $ \boldsymbol{0} $ 与任何向量都正交；
- 如果两个非零向量正交，则它们的方向相互垂直（在几何上）。

---

#### 2. 正交向量组

##### **定义5：**

设 $ \boldsymbol{\alpha}_1, \boldsymbol{\alpha}_2, \dots, \boldsymbol{\alpha}_m $ 是 $ \mathbb{R}^n $ 中的一组向量，若其中任意两个不同的向量都正交，并且每个向量都不是零向量，则称这组向量为**正交向量组**。

例如，在 $ \mathbb{R}^3 $ 中，向量组  
$$
\boldsymbol{\alpha}_1 = (1, 1, 1),\quad \boldsymbol{\alpha}_2 = (1, -2, 1),\quad \boldsymbol{\alpha}_3 = (-1, 0, 1)
$$  
就是一个正交向量组。

---

#### 3. 正交向量组的线性无关性

##### **定理：**

正交向量组一定是**线性无关的**。

**证明：**  
设 $ \boldsymbol{\alpha}_1, \boldsymbol{\alpha}_2, \dots, \boldsymbol{\alpha}_m $ 是一个正交向量组，且有线性组合  
$$
k_1\boldsymbol{\alpha}_1 + k_2\boldsymbol{\alpha}_2 + \cdots + k_m\boldsymbol{\alpha}_m = \boldsymbol{0}.
$$  
对等式两边分别与 $ \boldsymbol{\alpha}_i $ 做内积，利用正交性得：
$$
(\boldsymbol{\alpha}_i, k_1\boldsymbol{\alpha}_1 + \cdots + k_m\boldsymbol{\alpha}_m) = k_i (\boldsymbol{\alpha}_i, \boldsymbol{\alpha}_i) = 0.
$$  
由于 $ \boldsymbol{\alpha}_i \neq \boldsymbol{0} $，所以 $ (\boldsymbol{\alpha}_i, \boldsymbol{\alpha}_i) > 0 $，从而 $ k_i = 0 $ 对所有 $ i $ 成立。

因此，该向量组线性无关。

> ⚠️ 注意：线性无关的向量组**未必是正交的**。例如：
$$
\boldsymbol{\alpha}_1 = (1, 0, 0),\quad \boldsymbol{\alpha}_2 = (1, 1, 0),\quad \boldsymbol{\alpha}_3 = (1, 1, 1)
$$  
这三个向量线性无关，但不是正交向量组。

---

#### 4. 构造正交向量组的例子

##### **例1：**

在 $ \mathbb{R}^3 $ 中，已知两个正交向量  
$$
\boldsymbol{\alpha}_1 = (1, 1, 1),\quad \boldsymbol{\alpha}_2 = (1, -2, 1),
$$  
求第三个向量 $ \boldsymbol{\alpha}_3 $，使得 $ \boldsymbol{\alpha}_1, \boldsymbol{\alpha}_2, \boldsymbol{\alpha}_3 $ 构成正交向量组。

**解：**  
设 $ \boldsymbol{\alpha}_3 = (x_1, x_2, x_3) $，要求满足：
$$
(\boldsymbol{\alpha}_1, \boldsymbol{\alpha}_3) = 0,\quad (\boldsymbol{\alpha}_2, \boldsymbol{\alpha}_3) = 0.
$$  
列出方程组：
$$
\begin{cases}
x_1 + x_2 + x_3 = 0 \\
x_1 - 2x_2 + x_3 = 0
\end{cases}
$$  
解得：
$$
x_1 = -1,\quad x_2 = 0,\quad x_3 = 1.
$$  
取 $ \boldsymbol{\alpha}_3 = (-1, 0, 1) $，即可构成正交向量组。

---

#### 5. 正交向量组与线性相关性的关系

##### **例2：**

设 $ \boldsymbol{\alpha}_1, \dots, \boldsymbol{\alpha}_r \in \mathbb{R}^n $ 线性无关，$ \boldsymbol{\beta}_1, \dots, \boldsymbol{\beta}_s \in \mathbb{R}^n $ 满足  
$$
(\boldsymbol{\alpha}_i, \boldsymbol{\beta}_j) = 0,\quad \forall i=1,\dots,r,\ j=1,\dots,s.
$$  
且 $ s + r > n $，证明：$ \boldsymbol{\beta}_1, \dots, \boldsymbol{\beta}_s $ 线性相关。

**证：**  
将 $ \boldsymbol{\alpha}_1, \dots, \boldsymbol{\alpha}_r $ 构成矩阵 $ A $，则 $ \boldsymbol{\beta}_j $ 属于齐次线性方程组 $ A\mathbf{x} = \mathbf{0} $ 的解空间。

该解空间的维数为 $ n - r $，而 $ s > n - r $，说明 $ \boldsymbol{\beta}_1, \dots, \boldsymbol{\beta}_s $ 不能线性无关。

---

#### 6. 标准正交向量组

##### **定义6：**

设 $ \boldsymbol{\alpha}_1, \boldsymbol{\alpha}_2, \dots, \boldsymbol{\alpha}_s $ 是 $ \mathbb{R}^n $ 中的一个正交向量组，若每个向量的长度都为1，即  
$$
\|\boldsymbol{\alpha}_i\| = 1,\quad i = 1, 2, \dots, s,
$$  
则称其为**标准正交向量组**。

若 $ s = n $，则称其为 $ \mathbb{R}^n $ 的**标准正交基**。

##### **举例：**

- 在 $ \mathbb{R}^3 $ 中，标准正交基可以是：
  $$
  \boldsymbol{e}_1 = (1, 0, 0),\quad \boldsymbol{e}_2 = (0, 1, 0),\quad \boldsymbol{e}_3 = (0, 0, 1).
  $$
- 另一组标准正交基为：
  $$
  \boldsymbol{f}_1 = \left( \frac{1}{\sqrt{2}}, \frac{1}{\sqrt{2}}, 0 \right),\quad
  \boldsymbol{f}_2 = \left( -\frac{1}{\sqrt{2}}, \frac{1}{\sqrt{2}}, 0 \right),\quad
  \boldsymbol{f}_3 = (0, 0, 1).
  $$

---

#### 7. 向量在标准正交基下的坐标表示

##### **例3：**

设 $ \boldsymbol{\alpha}_1, \boldsymbol{\alpha}_2, \dots, \boldsymbol{\alpha}_n $ 是 $ \mathbb{R}^n $ 的一组标准正交基，任意向量 $ \boldsymbol{\beta} \in \mathbb{R}^n $ 可以唯一地表示为：
$$
\boldsymbol{\beta} = x_1\boldsymbol{\alpha}_1 + x_2\boldsymbol{\alpha}_2 + \cdots + x_n\boldsymbol{\alpha}_n.
$$  
那么，系数 $ x_i $ 可由内积直接得到：
$$
x_i = (\boldsymbol{\beta}, \boldsymbol{\alpha}_i),\quad i = 1, 2, \dots, n.
$$

这就是**向量在标准正交基下的坐标表达式**。

---

#### 8. 总结

| 概念 | 定义 | 特点 |
|------|------|------|
| 正交 | $ (\boldsymbol{\alpha}, \boldsymbol{\beta}) = 0 $ | 方向垂直，适用于任意维空间 |
| 正交向量组 | 两两正交且不含零向量 | 必线性无关 |
| 标准正交向量组 | 正交且单位化 | 可作为标准正交基 |
| 向量在标准正交基下的坐标 | $ x_i = (\boldsymbol{\beta}, \boldsymbol{\alpha}_i) $ | 表达简洁、计算方便 |

---

### **三、施密特正交化方法**

在 $ \mathbb{R}^n $ 中，任意一组**线性无关的向量**都可以作为该空间的一组基。然而，这些基未必具有正交性或单位长度，因此在实际应用中不方便使用。为了将这组基转化为**标准正交基**，可以使用一种非常重要的方法——**施密特正交化方法**（Gram-Schmidt Orthogonalization）。

---

#### 一、基本思想

设 $ \boldsymbol{\alpha}_1, \boldsymbol{\alpha}_2, \dots, \boldsymbol{\alpha}_s $ 是 $ \mathbb{R}^n $ 中一组**线性无关的向量**，我们希望构造一组新的向量：

$$
\boldsymbol{y}_1, \boldsymbol{y}_2, \dots, \boldsymbol{y}_s,
$$  
使得：

- 它们是**两两正交**的；
- 每个 $ \boldsymbol{y}_i $ 都是单位向量（即 $ \|\boldsymbol{y}_i\| = 1 $）；
- 它们与原向量组有相同的**张成空间**（span），即：
  $$
  \text{span}\{\boldsymbol{y}_1, \dots, \boldsymbol{y}_s\} = \text{span}\{\boldsymbol{\alpha}_1, \dots, \boldsymbol{\alpha}_s\}.
  $$

---

#### 二、施密特正交化步骤

##### **1. 构造正交向量组：**

令  
$$
\boldsymbol{\beta}_1 = \boldsymbol{\alpha}_1.
$$  

接着依次构造其余正交向量：

$$
\begin{aligned}
\boldsymbol{\beta}_2 &= \boldsymbol{\alpha}_2 - \frac{(\boldsymbol{\alpha}_2, \boldsymbol{\beta}_1)}{(\boldsymbol{\beta}_1, \boldsymbol{\beta}_1)} \boldsymbol{\beta}_1, \\
\boldsymbol{\beta}_3 &= \boldsymbol{\alpha}_3 - \frac{(\boldsymbol{\alpha}_3, \boldsymbol{\beta}_1)}{(\boldsymbol{\beta}_1, \boldsymbol{\beta}_1)} \boldsymbol{\beta}_1 - \frac{(\boldsymbol{\alpha}_3, \boldsymbol{\beta}_2)}{(\boldsymbol{\beta}_2, \boldsymbol{\beta}_2)} \boldsymbol{\beta}_2, \\
&\vdots \\
\boldsymbol{\beta}_s &= \boldsymbol{\alpha}_s - \sum_{i=1}^{s-1} \frac{(\boldsymbol{\alpha}_s, \boldsymbol{\beta}_i)}{(\boldsymbol{\beta}_i, \boldsymbol{\beta}_i)} \boldsymbol{\beta}_i.
\end{aligned}
$$

最终得到的向量组 $ \boldsymbol{\beta}_1, \boldsymbol{\beta}_2, \dots, \boldsymbol{\beta}_s $ 是一个**正交向量组**。

##### **2. 单位化处理：**

对每个 $ \boldsymbol{\beta}_i $ 进行单位化：

$$
\boldsymbol{y}_i = \frac{\boldsymbol{\beta}_i}{\|\boldsymbol{\beta}_i\|},\quad i = 1, 2, \dots, s.
$$

这样就得到了一组**标准正交向量组** $ \boldsymbol{y}_1, \boldsymbol{y}_2, \dots, \boldsymbol{y}_s $。

---

#### 三、算法流程总结

给定一组线性无关向量 $ \boldsymbol{\alpha}_1, \boldsymbol{\alpha}_2, \dots, \boldsymbol{\alpha}_s \in \mathbb{R}^n $，执行以下步骤：

1. 初始化第一个正交向量：
   $$
   \boldsymbol{\beta}_1 = \boldsymbol{\alpha}_1
   $$

2. 对于 $ k = 2 $ 到 $ s $，计算：

   $$
   \boldsymbol{\beta}_k = \boldsymbol{\alpha}_k - \sum_{i=1}^{k-1} \frac{(\boldsymbol{\alpha}_k, \boldsymbol{\beta}_i)}{(\boldsymbol{\beta}_i, \boldsymbol{\beta}_i)} \boldsymbol{\beta}_i
   $$

3. 单位化每个 $ \boldsymbol{\beta}_i $ 得到单位向量：

   $$
   \boldsymbol{y}_i = \frac{\boldsymbol{\beta}_i}{\|\boldsymbol{\beta}_i\|}
   $$

---

#### 四、典型例题解析

##### **例4：**

已知向量 $ \boldsymbol{\alpha}_1 = (1, 1, 1) \in \mathbb{R}^3 $，要求构造两个额外的向量 $ \boldsymbol{\alpha}_2, \boldsymbol{\alpha}_3 $，使得 $ \boldsymbol{\alpha}_1, \boldsymbol{\alpha}_2, \boldsymbol{\alpha}_3 $ 构成一个正交向量组。

**解：**

1. 考察满足 $ (\boldsymbol{\alpha}_1, \boldsymbol{\alpha}) = 0 $ 的向量，即满足方程：
   $$
   x_1 + x_2 + x_3 = 0.
   $$

2. 解得基础解系为：
   $$
   \xi_1 = (1, 0, -1),\quad \xi_2 = (0, 1, -1).
   $$

3. 对 $ \xi_1, \xi_2 $ 应用施密特正交化：

   - $ \boldsymbol{\alpha}_2 = \xi_1 = (1, 0, -1) $
   - $ \boldsymbol{\alpha}_3 = \xi_2 - \frac{(\xi_2, \boldsymbol{\alpha}_2)}{(\boldsymbol{\alpha}_2, \boldsymbol{\alpha}_2)} \boldsymbol{\alpha}_2 $

     计算：
     $$
     (\xi_2, \boldsymbol{\alpha}_2) = 0 \cdot 1 + 1 \cdot 0 + (-1)(-1) = 1,\quad
     (\boldsymbol{\alpha}_2, \boldsymbol{\alpha}_2) = 1^2 + 0^2 + (-1)^2 = 2.
     $$

     所以：
     $$
     \boldsymbol{\alpha}_3 = (0, 1, -1) - \frac{1}{2}(1, 0, -1) = \left(-\frac{1}{2}, 1, -\frac{1}{2}\right).
     $$

于是，$ \boldsymbol{\alpha}_1 = (1, 1, 1),\ \boldsymbol{\alpha}_2 = (1, 0, -1),\ \boldsymbol{\alpha}_3 = \left(-\frac{1}{2}, 1, -\frac{1}{2}\right) $ 构成一个正交向量组。

---

##### **例5：**

将基  
$$
\boldsymbol{\alpha}_1 = (1, 1, 1),\quad \boldsymbol{\alpha}_2 = (1, 2, 1),\quad \boldsymbol{\alpha}_3 = (0, -1, 1)
$$  
化为 $ \mathbb{R}^3 $ 的**标准正交基**。

**解：**

1. **正交化过程：**

   - $ \boldsymbol{\beta}_1 = \boldsymbol{\alpha}_1 = (1, 1, 1) $

   - $ \boldsymbol{\beta}_2 = \boldsymbol{\alpha}_2 - \frac{(\boldsymbol{\alpha}_2, \boldsymbol{\beta}_1)}{(\boldsymbol{\beta}_1, \boldsymbol{\beta}_1)} \boldsymbol{\beta}_1 $

     计算：
     $$
     (\boldsymbol{\alpha}_2, \boldsymbol{\beta}_1) = 1 \cdot 1 + 2 \cdot 1 + 1 \cdot 1 = 4,\quad
     (\boldsymbol{\beta}_1, \boldsymbol{\beta}_1) = 3.
     $$

     所以：
     $$
     \boldsymbol{\beta}_2 = (1, 2, 1) - \frac{4}{3}(1, 1, 1) = \left( -\frac{1}{3}, \frac{2}{3}, -\frac{1}{3} \right).
     $$

   - $ \boldsymbol{\beta}_3 = \boldsymbol{\alpha}_3 - \frac{(\boldsymbol{\alpha}_3, \boldsymbol{\beta}_1)}{(\boldsymbol{\beta}_1, \boldsymbol{\beta}_1)} \boldsymbol{\beta}_1 - \frac{(\boldsymbol{\alpha}_3, \boldsymbol{\beta}_2)}{(\boldsymbol{\beta}_2, \boldsymbol{\beta}_2)} \boldsymbol{\beta}_2 $

     结果可得：
     $$
     \boldsymbol{\beta}_3 = (-1, 0, 1)
     $$

2. **单位化过程：**

   - $ \boldsymbol{y}_1 = \frac{(1, 1, 1)}{\sqrt{3}} $
   - $ \boldsymbol{y}_2 = \frac{(-1, 2, -1)}{\sqrt{6}} $
   - $ \boldsymbol{y}_3 = \frac{(-1, 0, 1)}{\sqrt{2}} $

最终得到的标准正交基为：
$$
\left\{
\frac{1}{\sqrt{3}}(1, 1, 1),\
\frac{1}{\sqrt{6}}(-1, 2, -1),\
\frac{1}{\sqrt{2}}(-1, 0, 1)
\right\}
$$

---

#### 五、总结

| 步骤 | 内容 |
|------|------|
| 输入 | 线性无关向量组 $ \boldsymbol{\alpha}_1, \dots, \boldsymbol{\alpha}_s $ |
| 正交化 | 构造正交向量组 $ \boldsymbol{\beta}_1, \dots, \boldsymbol{\beta}_s $ |
| 单位化 | 得到标准正交向量组 $ \boldsymbol{y}_1, \dots, \boldsymbol{y}_s $ |
| 输出 | 标准正交基，保持与原向量组相同的张成空间 |

---

### **四、正交矩阵**

在向量空间和矩阵理论中，**正交矩阵**是一类具有特殊性质的方阵，它与标准正交基密切相关。正交矩阵在几何变换（如旋转、反射）、数值计算、信号处理等领域中具有广泛应用。

---

#### 一、定义

##### **定义7：**

设 $ A $ 是一个 $ n \times n $ 的实矩阵，如果满足  
$$
A^\top A = A A^\top = I,
$$  
则称 $ A $ 为**正交矩阵**。

其中：

- $ A^\top $ 表示 $ A $ 的转置；
- $ I $ 是 $ n \times n $ 的单位矩阵。

---

#### 二、正交矩阵的基本性质

1. **可逆性：**
   - 正交矩阵是可逆的，并且其逆矩阵就是它的转置：
     $$
     A^{-1} = A^\top.
     $$

2. **行列式值：**
   - 由于 $ A^\top A = I $，所以有：
     $$
     \det(A^\top A) = (\det A)^2 = \det(I) = 1 \Rightarrow \det A = \pm 1.
     $$

3. **乘积保持正交性：**
   - 若 $ A $ 和 $ B $ 都是 $ n \times n $ 的正交矩阵，则它们的乘积 $ AB $ 也是正交矩阵。
   - 证明思路：利用 $ (AB)^\top(AB) = B^\top A^\top A B = B^\top I B = I $。

4. **充分必要条件：**
   - $ n \times n $ 矩阵 $ A $ 是正交矩阵的充要条件是：**它的行向量组或列向量组构成标准正交向量组**。

---

#### 三、标准正交向量组与正交矩阵的关系

设  
$$
A = \begin{bmatrix}
\boldsymbol{\alpha}_1 \\
\boldsymbol{\alpha}_2 \\
\vdots \\
\boldsymbol{\alpha}_n
\end{bmatrix},
$$  
其中 $ \boldsymbol{\alpha}_1, \boldsymbol{\alpha}_2, \dots, \boldsymbol{\alpha}_n $ 是 $ A $ 的行向量。

那么 $ A $ 是正交矩阵当且仅当这些行向量满足：

- 每个向量长度为1：$ \|\boldsymbol{\alpha}_i\| = 1 $；
- 任意两个不同向量正交：$ (\boldsymbol{\alpha}_i, \boldsymbol{\alpha}_j) = 0,\ i \neq j $。

换句话说，**正交矩阵的行向量组是一个标准正交向量组**。

同样地，若将 $ A $ 的列向量记作 $ \boldsymbol{\beta}_1, \boldsymbol{\beta}_2, \dots, \boldsymbol{\beta}_n $，也有相同的结论。

---

#### 四、典型例题解析

##### **例6：**

判断以下矩阵是否为正交矩阵：

$$
A = \begin{bmatrix}
\frac{1}{\sqrt{3}} & \frac{1}{\sqrt{3}} & \frac{1}{\sqrt{3}} \\
-\frac{1}{\sqrt{6}} & \frac{2}{\sqrt{6}} & -\frac{1}{\sqrt{6}} \\
-\frac{1}{\sqrt{2}} & 0 & \frac{1}{\sqrt{2}}
\end{bmatrix}.
$$

**解：**

观察各**行向量**：

- 第一行：$ \boldsymbol{\alpha}_1 = \left(\frac{1}{\sqrt{3}}, \frac{1}{\sqrt{3}}, \frac{1}{\sqrt{3}}\right) $，长度为1；
- 第二行：$ \boldsymbol{\alpha}_2 = \left(-\frac{1}{\sqrt{6}}, \frac{2}{\sqrt{6}}, -\frac{1}{\sqrt{6}}\right) $，长度为1；
- 第三行：$ \boldsymbol{\alpha}_3 = \left(-\frac{1}{\sqrt{2}}, 0, \frac{1}{\sqrt{2}}\right) $，长度为1；

再验证两两正交：

- $ (\boldsymbol{\alpha}_1, \boldsymbol{\alpha}_2) = 0 $
- $ (\boldsymbol{\alpha}_1, \boldsymbol{\alpha}_3) = 0 $
- $ (\boldsymbol{\alpha}_2, \boldsymbol{\alpha}_3) = 0 $

因此，$ A $ 的行向量组是标准正交向量组，故 $ A $ 是正交矩阵。

---

#### 五、正交矩阵的应用举例

| 应用场景 | 描述 |
|----------|------|
| 几何变换 | 正交矩阵表示**保距离的线性变换**，如旋转、反射等 |
| 特征分解 | 在对称矩阵的谱分解中，特征向量组成的矩阵是正交矩阵 |
| QR 分解 | 将任意矩阵分解为一个正交矩阵与一个上三角矩阵的乘积 |
| 数值稳定性 | 在求解线性方程组时，使用正交矩阵可以避免误差放大 |

---

#### 六、总结

| 性质 | 内容 |
|------|------|
| 定义 | $ A^\top A = A A^\top = I $ |
| 可逆性 | $ A^{-1} = A^\top $ |
| 行列式 | $ \det A = \pm 1 $ |
| 列/行向量 | 必须是标准正交向量组 |
| 乘积 | 正交矩阵的乘积仍为正交矩阵 |
| 应用 | 几何变换、QR分解、特征值计算等 |

---

## **§5.4 实对称矩阵的相似对角化**

### 一、实对称矩阵的基本性质

设 $ A \in \mathbb{R}^{n \times n} $，如果满足  
$$
A^\top = A,
$$  
则称 $ A $ 为**实对称矩阵**。

设 $ A = (a_{ij})_{m \times n} \in \mathbb{C}^{m \times n} $ 是一个复数域上的矩阵，我们定义 **A 的共轭矩阵**为 $ \overline{A} = (\overline{a_{ij}})_{m \times n} $，其中 $ \overline{a_{ij}} $ 表示 $ a_{ij} $ 的共轭复数。

由共轭矩阵的定义及共轭复数的运算性质，可以得出以下常用性质（设 $ A, B $ 为同型矩阵，$ k \in \mathbb{C} $）：

1. $ \overline{A^T} = (\overline{A})^T $；
2. $ \overline{kA} = \overline{k} \cdot \overline{A} $；
3. 若 $ AB $ 有意义，则 $ \overline{AB} = \overline{A} \cdot \overline{B} $。

**证明思路：**

设 $ \lambda $ 是 $ A $ 的一个复特征值，对应的非零特征向量为 $ \boldsymbol{\alpha} \in \mathbb{C}^n $，即：
$$
A\boldsymbol{\alpha} = \lambda\boldsymbol{\alpha}.
$$

取共轭得：
$$
A\overline{\boldsymbol{\alpha}} = \overline{\lambda}\overline{\boldsymbol{\alpha}}.
$$

再转置得：
$$
\overline{\boldsymbol{\alpha}}^\top A = \overline{\lambda} \overline{\boldsymbol{\alpha}}^\top.
$$

用 $ \boldsymbol{\alpha} $ 右乘上式两边，并利用 $ A^\top = A $，可得：
$$
\overline{\boldsymbol{\alpha}}^\top A \boldsymbol{\alpha} = \overline{\lambda} \overline{\boldsymbol{\alpha}}^\top \boldsymbol{\alpha},
\quad \text{而} \quad A\boldsymbol{\alpha} = \lambda\boldsymbol{\alpha} \Rightarrow \overline{\boldsymbol{\alpha}}^\top A \boldsymbol{\alpha} = \lambda \overline{\boldsymbol{\alpha}}^\top \boldsymbol{\alpha}.
$$

所以：
$$
(\lambda - \overline{\lambda}) \|\boldsymbol{\alpha}\|^2 = 0 \Rightarrow \lambda = \overline{\lambda} \Rightarrow \lambda \in \mathbb{R}.
$$

---

### 二、不同特征值对应的特征向量正交

#### **定理2：**

设 $ A $ 是实对称矩阵，$ \lambda_1 \neq \lambda_2 $ 是 $ A $ 的两个不同特征值，对应的特征向量分别为 $ \boldsymbol{\alpha}_1, \boldsymbol{\alpha}_2 $，则有：
$$
\boldsymbol{\alpha}_1^\top \boldsymbol{\alpha}_2 = 0.
$$

**证明思路：**

由定义：
$$
A\boldsymbol{\alpha}_1 = \lambda_1\boldsymbol{\alpha}_1,\quad A\boldsymbol{\alpha}_2 = \lambda_2\boldsymbol{\alpha}_2.
$$

对第一个等式转置后右乘 $ \boldsymbol{\alpha}_2 $ 得：
$$
\boldsymbol{\alpha}_1^\top A \boldsymbol{\alpha}_2 = \lambda_1 \boldsymbol{\alpha}_1^\top \boldsymbol{\alpha}_2.
$$

又因 $ A^\top = A $，所以 $ \boldsymbol{\alpha}_1^\top A = (A\boldsymbol{\alpha}_1)^\top = \lambda_1 \boldsymbol{\alpha}_1^\top $，于是：
$$
\boldsymbol{\alpha}_1^\top A \boldsymbol{\alpha}_2 = \lambda_2 \boldsymbol{\alpha}_1^\top \boldsymbol{\alpha}_2.
$$

比较两式得：
$$
(\lambda_1 - \lambda_2)\boldsymbol{\alpha}_1^\top \boldsymbol{\alpha}_2 = 0 \Rightarrow \boldsymbol{\alpha}_1^\top \boldsymbol{\alpha}_2 = 0.
$$

---

### 三、实对称矩阵一定可以正交对角化

#### **定理3（实对称矩阵的正交对角化）：**

设 $ A \in \mathbb{R}^{n \times n} $ 是实对称矩阵，则存在一个**正交矩阵** $ C $，使得  
$$
C^\top A C = \Lambda,
$$  
其中 $ \Lambda $ 是一个对角矩阵，其主对角线元素是 $ A $ 的所有特征值。

换句话说，**实对称矩阵总可以通过正交变换转化为对角矩阵**。

---

### 四、实对称矩阵的正交对角化步骤

给定一个实对称矩阵 $ A $，我们可以通过以下步骤构造使其对角化的正交矩阵 $ C $：

#### **步骤如下：**

1. **求出 $ A $ 的全部特征值 $ \lambda_1, \lambda_2, \dots, \lambda_n $**；
2. **对每个特征值 $ \lambda_i $，求解齐次线性方程组 $ (\lambda_i I - A)\mathbf{x} = 0 $，得到基础解系；**
3. **对每个基础解系进行施密特正交化和单位化，得到一组标准正交的特征向量；**
4. **将这些标准正交的特征向量按顺序组成列向量，构成矩阵 $ C $，则 $ C $ 是正交矩阵；**
5. **计算 $ C^\top A C $，结果是一个对角矩阵，其对角线上为相应的特征值。**

---

### 五、典型例题解析

#### **例1：**

设  
$$
A = \begin{bmatrix}
3 & 1 & 1 \\
1 & 3 & 1 \\
1 & 1 & 3
\end{bmatrix},
$$  
求正交矩阵 $ C $，使得 $ C^\top A C $ 为对角矩阵。

**解：**

1. **求特征值：**

   解特征方程：
   $$
   \det(\lambda I - A) = (\lambda - 5)(\lambda - 2)^2 = 0.
   $$

   所以特征值为：
   $$
   \lambda_1 = 5,\quad \lambda_2 = \lambda_3 = 2.
   $$

2. **求特征向量：**

   - 对 $ \lambda_1 = 5 $，解 $ (5I - A)\mathbf{x} = 0 $，得基础解系：
     $$
     \boldsymbol{\alpha}_1 = (1, 1, 1).
     $$
   - 对 $ \lambda_2 = 2 $，解 $ (2I - A)\mathbf{x} = 0 $，得基础解系：
     $$
     \boldsymbol{\alpha}_2 = (-1, 1, 0),\quad \boldsymbol{\alpha}_3 = (-1, 0, 1).
     $$

3. **正交化与单位化：**

   - $ \boldsymbol{\beta}_1 = \boldsymbol{\alpha}_1 = (1, 1, 1) $，单位化得：
     $$
     \boldsymbol{y}_1 = \frac{1}{\sqrt{3}}(1, 1, 1).
     $$

   - $ \boldsymbol{\beta}_2 = \boldsymbol{\alpha}_2 = (-1, 1, 0) $，单位化得：
     $$
     \boldsymbol{y}_2 = \frac{1}{\sqrt{2}}(-1, 1, 0).
     $$

   - $ \boldsymbol{\beta}_3 = \boldsymbol{\alpha}_3 - \frac{(\boldsymbol{\alpha}_3, \boldsymbol{\beta}_2)}{(\boldsymbol{\beta}_2, \boldsymbol{\beta}_2)} \boldsymbol{\beta}_2 = \left( -\frac{1}{2}, -\frac{1}{2}, 1 \right) $，单位化得：
     $$
     \boldsymbol{y}_3 = \frac{1}{\sqrt{6}}(-1, -1, 2).
     $$

4. **构造正交矩阵 $ C $：**

   $$
   C = \begin{bmatrix}
   \frac{1}{\sqrt{3}} & -\frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{6}} \\
   \frac{1}{\sqrt{3}} & \frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{6}} \\
   \frac{1}{\sqrt{3}} & 0 & \frac{2}{\sqrt{6}}
   \end{bmatrix}.
   $$

5. **验证对角化：**

   $$
   C^\top A C = \begin{bmatrix}
   5 & 0 & 0 \\
   0 & 2 & 0 \\
   0 & 0 & 2
   \end{bmatrix}.
   $$

---

### 六、实对称矩阵的其他重要结论

#### **定理4：**

若 $ A $ 和 $ B $ 都是实对称矩阵，则 $ AB $ 是实对称矩阵当且仅当 $ AB = BA $。

#### **定理5：**

设 $ A $ 和 $ B $ 都是实对称矩阵，则 $ A $ 与 $ B $ 相似的充要条件是它们具有相同的特征值。

---

### 七、总结

| 性质 | 内容 |
|------|------|
| 定义 | $ A^\top = A $ |
| 特征值 | 都是实数 |
| 不同特征值的特征向量 | 彼此正交 |
| 正交对角化 | 存在正交矩阵 $ C $，使得 $ C^\top A C $ 为对角矩阵 |
| 应用 | 主成分分析、谱聚类、量子力学中的可观测量等 |

---

# **第六章 二次型与二次曲面**

## **§6.1 实二次型及其标准形**

### **一、二次型及其矩阵表示**

在平面解析几何中，二次方程  
$$
ax^2 + 2bxy + cy^2 = d
$$  
表示一条**二次曲线**。为了便于研究该曲线的几何性质，我们可以选择适当的角度 $\theta$，作**坐标变换**（即旋转变换）：  
$$
\begin{cases}
x = x'\cos\theta - y'\sin\theta \\
y = x'\sin\theta + y'\cos\theta
\end{cases}
$$  
将原二次方程化为只含平方项的标准方程：  
$$
a'x'^2 + b'y'^2 = d.
$$  
由 $a'$ 和 $b'$ 的符号很快能判断出此二次曲线表示的是一个**椭圆**或者是**双曲线**。

上述二次方程的左端是一个**二次齐次多项式**，从代数学的观点来看，就是通过一个可逆线性变换将一个二次齐次多项式化为只含平方项的多项式。这样的问题，在许多理论问题或实际应用问题中常会遇到。现在我们把这类问题一般化，讨论 $n$ 个变量的二次齐次多项式的问题。

---

#### 定义1（二次型）

设 $f(x_1, x_2, \dots, x_n)$ 是关于变量 $x_1, x_2, \dots, x_n$ 的一个**二次齐次多项式**，其形式如下：

$$
f(x_1, x_2, \dots, x_n) = a_{11}x_1^2 + 2a_{12}x_1x_2 + \cdots + 2a_{1n}x_1x_n + a_{22}x_2^2 + \cdots + 2a_{2n}x_2x_n + \cdots + a_{nn}x_n^2,
$$

则称 $f$ 为 **n 元实二次型**，简称为**二次型**。

如果所有系数 $a_{ij} \in \mathbb{R}$，则称为**实二次型**；若 $a_{ij} \in \mathbb{C}$，则称为**复二次型**。本章主要讨论**实二次型**。

---

#### 二次型的矩阵表示

令 $A = (a_{ij})$ 是一个 $n \times n$ 的**实对称矩阵**，其中 $a_{ij} = a_{ji}$。定义列向量  
$$
X = \begin{bmatrix} x_1 \\ x_2 \\ \vdots \\ x_n \end{bmatrix},
$$  
则二次型可以写成以下**矩阵形式**：

$$
f(x_1, x_2, \dots, x_n) = X^\top A X,
$$

其中 $A$ 称为该二次型的**矩阵**，而 $X^\top A X$ 称为该二次型的**矩阵表达式**。

例如，二次型  
$$
f(x_1, x_2, x_3) = 2x_1^2 - x_2^2 + 4x_1x_2 - 6x_2x_3 + x_3^2,
$$  
对应的矩阵是：
$$
A = \begin{bmatrix}
2 & 2 & 0 \\
2 & -1 & -3 \\
0 & -3 & 1
\end{bmatrix}.
$$

由于 $\det A \neq 0$，故 $A$ 是非奇异的，其秩为 3，因此该二次型的秩也为 3。

---

#### 可逆线性变换与合同矩阵

对于 $n$ 元二次型 $f(x_1, x_2, \dots, x_n)$，考虑如下的**线性变换**：

$$
\begin{cases}
x_1 = c_{11}y_1 + c_{12}y_2 + \cdots + c_{1n}y_n \\
x_2 = c_{21}y_1 + c_{22}y_2 + \cdots + c_{2n}y_n \\
\vdots \\
x_n = c_{n1}y_1 + c_{n2}y_2 + \cdots + c_{nn}y_n
\end{cases}
$$

令 $X = \begin{bmatrix} x_1 \\ \vdots \\ x_n \end{bmatrix}, Y = \begin{bmatrix} y_1 \\ \vdots \\ y_n \end{bmatrix}, C = (c_{ij})$，则变换可记为：
$$
X = CY.
$$

如果矩阵 $C$ 是可逆的，则称这个变换为**可逆线性变换**。

将二次型 $f(X) = X^\top A X$ 代入变换 $X = CY$，得：

$$
f(X) = (CY)^\top A (CY) = Y^\top (C^\top A C) Y.
$$

令 $B = C^\top A C$，则新的二次型为：
$$
g(Y) = Y^\top B Y.
$$

此时称矩阵 $A$ 与 $B$ 是**合同**的，记作 $A \sim B$，并满足关系：
$$
B = C^\top A C.
$$

---

#### 合同矩阵的性质

设 $A, B$ 为 $n$ 阶实对称矩阵，若存在可逆矩阵 $C$，使得 $B = C^\top A C$，则称 $A$ 与 $B$ **合同**。合同关系具有以下性质：

1. **反身性**：任何 $n$ 阶矩阵 $A$ 都与自身合同；
2. **对称性**：若 $A$ 与 $B$ 合同，则 $B$ 与 $A$ 合同；
3. **传递性**：若 $A$ 与 $B$ 合同，且 $B$ 与 $C$ 合同，则 $A$ 与 $C$ 合同。

这些性质的证明留给读者作为练习。

---

#### 二次型的秩

由于可逆线性变换不改变矩阵的秩，所以二次型经过可逆线性变换后，其对应矩阵的秩保持不变。因此，定义：

> **定义2**：二次型 $f(X) = X^\top A X$ 的矩阵 $A$ 的秩称为该二次型的**秩**。

---

#### 例题讲解

**例1** 设矩阵  
$$
A = \begin{bmatrix} 1 & 2 \\ 2 & -1 \end{bmatrix},
$$  
求一个实可逆矩阵 $C$，使得  
$$
C^\top A C = B = \begin{bmatrix} -2 & 0 \\ 0 & 1 \end{bmatrix}.
$$

**解**：矩阵 $A$ 对应的二次型是  
$$
f(x_1, x_2) = X^\top A X = x_1^2 + 4x_1x_2 - x_2^2.
$$

矩阵 $B$ 对应的二次型是  
$$
g(y_1, y_2) = Y^\top B Y = -2y_1^2 + y_2^2.
$$

考虑作可逆线性变换：  
$$
\begin{cases}
x_1 = y_1 + 2y_2 \\
x_2 = -2y_1 - y_2
\end{cases}
\quad \Rightarrow \quad X = C Y,
$$  
其中  
$$
C = \begin{bmatrix} 1 & 2 \\ -2 & -1 \end{bmatrix}.
$$

验证是否满足 $C^\top A C = B$：

计算 $C^\top = \begin{bmatrix} 1 & -2 \\ 2 & -1 \end{bmatrix}$，

$$
C^\top A C = \begin{bmatrix} 1 & -2 \\ 2 & -1 \end{bmatrix}
\begin{bmatrix} 1 & 2 \\ 2 & -1 \end{bmatrix}
\begin{bmatrix} 1 & 2 \\ -2 & -1 \end{bmatrix}
= \begin{bmatrix} -2 & 0 \\ 0 & 1 \end{bmatrix} = B.
$$

因此所求的实可逆矩阵为  
$$
C = \begin{bmatrix} 1 & 2 \\ -2 & -1 \end{bmatrix}.
$$

---

#### 小结

- 二次型是一个关于多个变量的二次齐次多项式。
- 每个二次型都唯一对应一个实对称矩阵。
- 通过可逆线性变换可以将二次型化为标准形（仅含平方项），其本质是矩阵的合同变换。
- 合同变换不改变二次型的秩。

### **二、用配方法化二次型为标准形**

在各种二次型中，**平方和形式**  
$$
d_1 y_1^2 + d_2 y_2^2 + \cdots + d_n y_n^2
$$  
无疑是最简单的。下面我们将介绍，任何一个实二次型 $ f(X) = X^\top A X $ 都可以通过**可逆线性变换** $ X = CY $ 化为这种平方和形式，这种形式称为**标准形**。

---

#### 定理1（标准形存在性）

> **定理1：** 任一实二次型都可以通过可逆线性变换化为标准形。

该定理的证明可以采用**数学归纳法**与**配方法**来完成，此处略去证明过程。我们通过具体例子说明如何使用**配方法**将二次型化为标准形。

---

#### 例2 用配方法化二次型为标准形

设二次型为：
$$
f(x_1, x_2, x_3) = x_1^2 + 2x_1x_2 + 5x_2^2 + 2x_1x_3 + 6x_2x_3.
$$

**解：**

观察发现变量 $x_1$ 出现较多，尝试以 $x_1$ 为主元进行配方：

$$
f = x_1^2 + 2x_1x_2 + 2x_1x_3 + 5x_2^2 + 6x_2x_3.
$$

对 $x_1$ 配方：

$$
f = (x_1 + x_2 + x_3)^2 - (x_2 + x_3)^2 + 5x_2^2 + 6x_2x_3.
$$

展开并整理：

$$
f = (x_1 + x_2 + x_3)^2 + (5x_2^2 + 6x_2x_3 - x_2^2 - 2x_2x_3 - x_3^2)
= (x_1 + x_2 + x_3)^2 + (4x_2^2 + 4x_2x_3 - x_3^2).
$$

继续对括号内部分配方：

$$
4x_2^2 + 4x_2x_3 - x_3^2 = 4\left(x_2 + \frac{1}{2}x_3\right)^2 - x_3^2 - x_3^2 = 4\left(x_2 + \frac{1}{2}x_3\right)^2 - 2x_3^2.
$$

代入原式得：

$$
f = (x_1 + x_2 + x_3)^2 + 4\left(x_2 + \frac{1}{2}x_3\right)^2 - 2x_3^2.
$$

令新的变量为：
$$
\begin{cases}
y_1 = x_1 + x_2 + x_3 \\
y_2 = x_2 + \frac{1}{2}x_3 \\
y_3 = x_3
\end{cases}
\Rightarrow
\begin{cases}
x_1 = y_1 - y_2 - \frac{1}{2}y_3 \\
x_2 = y_2 - \frac{1}{2}y_3 \\
x_3 = y_3
\end{cases}
$$

对应的变换矩阵为：
$$
C = \begin{bmatrix}
1 & -1 & -\frac{1}{2} \\
0 & 1 & -\frac{1}{2} \\
0 & 0 & 1
\end{bmatrix}.
$$

于是，标准形为：
$$
f = y_1^2 + 4y_2^2 - 2y_3^2.
$$

---

#### 例3 用配方法化二次型为标准形

设二次型为：
$$
f(x_1, x_2, x_3) = 2x_1x_2 + 2x_1x_3 - 6x_2x_3.
$$

**解：**

首先引入新变量使交叉项简化。考虑作如下变换：

$$
\begin{cases}
x_1 = y_1 + y_2 \\
x_2 = y_1 - y_2 \\
x_3 = y_3
\end{cases}
\Rightarrow
X = C Y,
$$  
其中  
$$
C = \begin{bmatrix}
1 & 1 & 0 \\
1 & -1 & 0 \\
0 & 0 & 1
\end{bmatrix}.
$$

代入原式得：

$$
f = 2(y_1 + y_2)(y_1 - y_2) + 2(y_1 + y_2)y_3 - 6(y_1 - y_2)y_3.
$$

计算各项：

- $ (y_1 + y_2)(y_1 - y_2) = y_1^2 - y_2^2 $
- $ (y_1 + y_2)y_3 = y_1y_3 + y_2y_3 $
- $ (y_1 - y_2)y_3 = y_1y_3 - y_2y_3 $

所以：

$$
f = 2(y_1^2 - y_2^2) + 2(y_1y_3 + y_2y_3) - 6(y_1y_3 - y_2y_3)
= 2y_1^2 - 2y_2^2 - 4y_1y_3 + 8y_2y_3.
$$

再配方：

$$
f = 2(y_1 - y_3)^2 - 2(y_2 - 2y_3)^2 + 6y_3^2.
$$

令：
$$
\begin{cases}
z_1 = y_1 - y_3 \\
z_2 = y_2 - 2y_3 \\
z_3 = y_3
\end{cases}
\Rightarrow Y = DZ.
$$

则最终标准形为：
$$
f = 2z_1^2 - 2z_2^2 + 6z_3^2.
$$

---

#### 规范形与惯性指数

一个二次型的标准形不是唯一的，但其**规范形**是唯一的。

> **定义：** 一个实二次型的**规范形**是指将其通过可逆线性变换变为如下形式：
$$
f = y_1^2 + \cdots + y_p^2 - y_{p+1}^2 - \cdots - y_r^2,
$$  
其中 $r \leq n$ 是二次型的秩，$p$ 是正惯性指数，$r - p$ 是负惯性指数，而 $2p - r$ 称为**符号差**。

> **定理2（规范形唯一性）：** 任一实二次型的规范形是**唯一**的。

---

#### 例4 已知规范形求参数

设二次型：
$$
f(x_1, x_2, x_3) = x_1^2 + a x_2^2 + x_3^2 + 2x_1x_2 - 2x_1x_3 - 2a x_2x_3
$$  
其正负惯性指数均为 1，求其规范形及常数 $a$。

**解：**

构造矩阵 $A$：
$$
A = \begin{bmatrix}
1 & 1 & -1 \\
1 & a & -a \\
-1 & -a & 1
\end{bmatrix}.
$$

由题意知其正负惯性指数都为 1，故秩为 2，即 $\text{rank}(A) = 2$。

计算行列式 $\det A$：

$$
\det A =
\begin{vmatrix}
1 & 1 & -1 \\
1 & a & -a \\
-1 & -a & 1
\end{vmatrix}
= 1(a \cdot 1 - (-a)(-a)) - 1(1 \cdot 1 - (-a)(-1)) + (-1)(1 \cdot (-a) - a \cdot (-1))
$$

$$
= a - a^2 - (1 - a) + (-a + a) = a - a^2 - 1 + a = 2a - a^2 - 1.
$$

令 $\det A = 0$ 得：
$$
a^2 - 2a + 1 = 0 \Rightarrow (a - 1)^2 = 0 \Rightarrow a = 1.
$$

验证此时 $\text{rank}(A)$ 是否为 2：

$$
A = \begin{bmatrix}
1 & 1 & -1 \\
1 & 1 & -1 \\
-1 & -1 & 1
\end{bmatrix},
$$  
显然第二行等于第一行，第三行等于第一行的相反数，故 $\text{rank}(A) = 1$，不满足条件。

因此应取 $a = -2$，代入后验证 $\text{rank}(A) = 2$ 成立。

所以正确答案为：  
$$
a = -2,\quad \text{规范形为 } f = y_1^2 - y_2^2.
$$

---

#### 小结

- 配方法是将二次型化为标准形的一种有效手段。
- 标准形不唯一，但规范形是唯一的。
- 惯性指数（正负项个数）和符号差是二次型的重要不变量。
- 利用规范形可以判断二次曲线或曲面的类型（椭圆/双曲线等）。

### **三、用正交变换化二次型为标准形**

#### 定义（正交变换）

设 $ X = CY $ 是一个线性变换，其中 $ C $ 是一个 **n 阶正交矩阵**，即满足  
$$
C^\top C = I,
$$  
则称该变换为**正交变换**。

正交变换具有如下重要性质：

- **保持向量内积不变**：对于任意两个向量 $ \alpha, \beta \in \mathbb{R}^n $，有  
  $$
  (C\alpha, C\beta) = (\alpha, \beta).
  $$
- **保持向量长度和夹角不变**，因此也保持图形的几何形状不变。
- **可逆性强**：由于 $ C^{-1} = C^\top $，计算简便且数值稳定。

---

#### 正交变换化二次型为标准形的理论依据

设实二次型  
$$
f(X) = X^\top A X,
$$  
其中 $ A $ 是一个 $ n \times n $ 的**实对称矩阵**。

由**对称矩阵的谱定理**可知，存在一个**正交矩阵** $ C $，使得  
$$
C^\top A C = \text{diag}(\lambda_1, \lambda_2, \dots, \lambda_n),
$$  
其中 $ \lambda_1, \lambda_2, \dots, \lambda_n $ 是矩阵 $ A $ 的全部**特征值**。

令 $ X = CY $，则  
$$
f(X) = X^\top A X = (CY)^\top A (CY) = Y^\top (C^\top A C) Y = \lambda_1 y_1^2 + \lambda_2 y_2^2 + \cdots + \lambda_n y_n^2.
$$

这就将原二次型通过正交变换化为了**标准形**，其平方项的系数恰好是矩阵 $ A $ 的所有特征值。

---

#### 定理3（正交变换化标准形的存在性）

> **定理3：** 任一实二次型都可以通过**正交变换**化为标准形。

说明：

- 标准形中的平方项系数就是矩阵 $ A $ 的所有特征值；
- 不计特征值排列顺序时，这种标准形是**唯一的**。

---

#### 例5 用正交变换化二次型为标准形

设二次型为：
$$
f(x_1, x_2, x_3) = x_1^2 - 2x_2^2 - 2x_3^2 - 4x_1x_2 + 4x_1x_3 + 8x_2x_3.
$$

**解：**

写出对应的实对称矩阵 $ A $：

$$
A = \begin{bmatrix}
1 & -2 & 2 \\
-2 & -2 & 4 \\
2 & 4 & -2
\end{bmatrix}.
$$

求矩阵 $ A $ 的特征值：

$$
\det(\lambda I - A) =
\begin{vmatrix}
\lambda - 1 & 2 & -2 \\
2 & \lambda + 2 & -4 \\
-2 & -4 & \lambda + 2
\end{vmatrix}.
$$

展开行列式并化简得特征方程为：

$$
(\lambda - 2)^2(\lambda + 7) = 0,
$$  
所以特征值为：  
$$
\lambda_1 = \lambda_2 = 2 \quad (\text{二重}), \quad \lambda_3 = -7.
$$

---

##### 对应于 $\lambda = 2$ 的特征向量

解齐次线性方程组 $(2I - A)\vec{x} = 0$：

$$
(2I - A) =
\begin{bmatrix}
1 & 2 & -2 \\
2 & 4 & -4 \\
-2 & -4 & 4
\end{bmatrix}
\Rightarrow \text{基础解系为：}
\vec{\alpha}_1 = (-2, 1, 0), \quad \vec{\alpha}_2 = (2, 0, 1).
$$

对其进行**施密特正交化**：

- $\vec{\beta}_1 = \vec{\alpha}_1 = (-2, 1, 0)$，
- $\vec{\beta}_2 = \vec{\alpha}_2 - \frac{(\vec{\alpha}_2, \vec{\beta}_1)}{(\vec{\beta}_1, \vec{\beta}_1)} \vec{\beta}_1 = (2, 0, 1) - \frac{-4}{5}(-2, 1, 0) = \left(\frac{2}{5}, \frac{4}{5}, 1\right)$.

再进行**单位化**：

- $\vec{e}_1 = \frac{1}{\sqrt{5}}(-2, 1, 0)$，
- $\vec{e}_2 = \frac{1}{\sqrt{45}}(2, 4, 5)$.

---

##### 对应于 $\lambda = -7$ 的特征向量

解齐次线性方程组 $(-7I - A)\vec{x} = 0$：

$$
(-7I - A) =
\begin{bmatrix}
-8 & 2 & -2 \\
2 & -5 & -4 \\
-2 & -4 & -5
\end{bmatrix}
\Rightarrow \text{基础解系为：}
\vec{\alpha}_3 = (1, 2, -2).
$$

单位化得：
$$
\vec{e}_3 = \frac{1}{\sqrt{9}}(1, 2, -2) = \left(\frac{1}{3}, \frac{2}{3}, -\frac{2}{3}\right).
$$

---

##### 构造正交矩阵 $ C $

将三个单位正交向量按列排成矩阵：

$$
C = \begin{bmatrix}
-\frac{2}{\sqrt{5}} & \frac{2}{\sqrt{45}} & \frac{1}{3} \\
\frac{1}{\sqrt{5}} & \frac{4}{\sqrt{45}} & \frac{2}{3} \\
0 & \frac{5}{\sqrt{45}} & -\frac{2}{3}
\end{bmatrix}.
$$

作正交变换 $ X = CY $，则原二次型变为标准形：

$$
f(X) = 2y_1^2 + 2y_2^2 - 7y_3^2.
$$

---

#### 小结

- 正交变换是一种特殊的可逆线性变换，能保持向量的长度与角度不变；
- 利用对称矩阵的谱定理，可以通过正交变换将实二次型化为标准形；
- 标准形的平方项系数是矩阵的特征值；
- 不考虑特征值顺序时，标准形是唯一的；
- 正交变换法常用于物理、工程等领域，因其良好的几何意义和数值稳定性。

## **§6.2 正定二次型**

### 一、正定二次型的定义

考虑一个实二次型  
$$
f(x_1, x_2, \dots, x_n) = X^\top A X,
$$  
其中 $A$ 是一个 $n \times n$ 的**实对称矩阵**，$X = (x_1, x_2, \dots, x_n)^\top$ 是实向量。

> **定义1（正定二次型）：** 如果对于任意非零实向量 $X \neq 0$，都有  
> $$
> f(X) = X^\top A X > 0,
> $$  
> 则称该二次型为**正定二次型**，对应的矩阵 $A$ 称为**正定矩阵**。

例如：

- $f(x_1, x_2, x_3) = x_1^2 + x_2^2 + x_3^2$ 是正定二次型；
- $g(x_1, x_2) = x_1^2 - x_2^2$ 不是正定二次型。

---

### 二、正定性的判定方法

#### 定理1（特征值判别法）

> **定理1：** 实二次型 $f(X) = X^\top A X$ 是正定的充要条件是：矩阵 $A$ 的所有**特征值都大于零**。

**证明思路：**

- 若 $A$ 所有特征值 $\lambda_i > 0$，则通过正交变换可将 $f(X)$ 化为标准形 $\sum \lambda_i y_i^2$，显然恒正；
- 反之，若存在某个特征值 $\lambda_i \leq 0$，则存在非零向量 $Y$ 使得 $f(X) \leq 0$，矛盾。

---

#### 推论1（惯性指数判别法）

> **推论1：** 实二次型 $f(X)$ 是正定的充要条件是其**正惯性指数为 $n$**。

即标准形中没有负项，只有正平方项。

---

#### 推论2（合同关系判别法）

> **推论2：** 实二次型 $f(X)$ 是正定的充要条件是其矩阵 $A$ 与单位矩阵 $I$ 合同，即存在可逆矩阵 $C$，使得  
> $$
> C^\top A C = I.
> $$

这说明正定矩阵可以通过合同变换变为单位矩阵。

---

#### 定理2（顺序主子式判别法）

> **定义（顺序主子式）：** 对于矩阵 $A = (a_{ij})$，它的第 $k$ 阶顺序主子式是指左上角 $k \times k$ 子矩阵的行列式：
> $$
> P_k = \begin{vmatrix}
a_{11} & a_{12} & \cdots & a_{1k} \\
a_{21} & a_{22} & \cdots & a_{2k} \\
\vdots & \vdots & \ddots & \vdots \\
a_{k1} & a_{k2} & \cdots & a_{kk}
\end{vmatrix}, \quad k = 1, 2, \dots, n.
> $$

> **定理2（顺序主子式判别法）：** 实二次型 $f(X) = X^\top A X$ 是正定的充要条件是：矩阵 $A$ 的所有顺序主子式均大于零：
> $$
> P_1 > 0,\quad P_2 > 0,\quad \dots,\quad P_n > 0.
> $$

---

### 三、典型例题讲解

#### 例1 判断正定性

设二次型  
$$
f(x_1, x_2, x_3) = x_1^2 + 4x_2^2 + 4x_3^2 + 2tx_1x_2 - 2x_1x_3 + 4x_2x_3.
$$  
问当 $t$ 取何值时，该二次型为正定？

**解：** 写出对应矩阵 $A$：

$$
A = \begin{bmatrix}
1 & t & -1 \\
t & 4 & 2 \\
-1 & 2 & 4
\end{bmatrix}.
$$

计算顺序主子式：

- $P_1 = 1 > 0$，
- $P_2 = \begin{vmatrix}1 & t \\ t & 4\end{vmatrix} = 4 - t^2$，
- $P_3 = \det A = 4(4 - t^2) - 2(t)(2) + (-1)(t \cdot 2 - 4 \cdot (-1)) = 16 - 4t^2 - 4t + 2t + 4 = 20 - 4t^2 - 2t.$

令 $P_2 > 0 \Rightarrow 4 - t^2 > 0 \Rightarrow |t| < 2$；  
令 $P_3 > 0 \Rightarrow 20 - 4t^2 - 2t > 0$。

解不等式组得：  
$$
-2 < t < 1.
$$

所以当 $t \in (-2, 1)$ 时，该二次型是正定的。

---

#### 例2 正定矩阵的逆也是正定矩阵

设 $A$ 是正定矩阵，证明 $A^{-1}$ 也是正定矩阵。

**证法一（特征值法）：**  
由于 $A$ 正定，其所有特征值 $\lambda_i > 0$，而 $A^{-1}$ 的特征值为 $1/\lambda_i > 0$，故 $A^{-1}$ 正定。

**证法二（合同变换法）：**  
由正定定义知 $A$ 与单位矩阵合同，即存在可逆矩阵 $P$，使  
$$
A = P^\top P \Rightarrow A^{-1} = (P^\top)^{-1} P^{-1} = (P^{-1})^\top P^{-1},
$$  
即 $A^{-1}$ 也与单位矩阵合同，因此正定。

**证法三（二次型法）：**  
设 $f(X) = X^\top A^{-1} X$，作线性变换 $X = AY$，则  
$$
f(X) = Y^\top A A^{-1} A Y = Y^\top A Y > 0,
$$  
说明 $f(X)$ 正定，因此 $A^{-1}$ 是正定矩阵。

---

### 四、其他类型二次型

除了正定二次型外，还有以下几种常见类型：

> **定义3：**

1. 若对任意非零 $X$，有 $f(X) < 0$，则称 $f(X)$ 为**负定二次型**；
2. 若对任意 $X$，有 $f(X) \geq 0$，则称 $f(X)$ 为**半正定二次型**；
3. 若对任意 $X$，有 $f(X) \leq 0$，则称 $f(X)$ 为**半负定二次型**；
4. 否则称为**不定二次型**。

> **定理4（负定判别法）：** 实二次型 $f(X)$ 是负定的充要条件是：

- 矩阵 $A$ 的所有特征值都小于零；
- 或者其负惯性指数为 $n$；
- 或者满足 $(−1)^k P_k > 0$，$k = 1, 2, \dots, n$。

---

### 五、综合应用举例

#### 例3 判断负定性

设二次型  
$$
f(x_1, x_2, x_3) = -5x_1^2 - 6x_2^2 - 4x_3^2 + 4x_1x_2 + 4x_1x_3.
$$  
判断是否为负定二次型。

**解：** 写出矩阵 $A$：

$$
A = \begin{bmatrix}
-5 & 2 & 2 \\
2 & -6 & 0 \\
2 & 0 & -4
\end{bmatrix}.
$$

计算顺序主子式：

- $P_1 = -5 < 0$，
- $P_2 = \begin{vmatrix}-5 & 2 \\ 2 & -6\end{vmatrix} = 30 - 4 = 26 > 0$，
- $P_3 = \det A = -5(-24) - 2(8) + 2(12) = 120 - 16 + 24 = 128 > 0$。

验证符号规律：

- $(-1)^1 P_1 = 5 > 0$，
- $(-1)^2 P_2 = 26 > 0$，
- $(-1)^3 P_3 = -128 < 0$。

不符合要求，因此该二次型不是负定的。

---

#### 例4 参数条件下正定性分析

设矩阵 $A$ 的特征多项式为  
$$
\det(\lambda I - A) = (\lambda - 2)^2(\lambda),
$$  
即 $A$ 的特征值为 $2, 2, 0$。

构造矩阵 $B = (kI + A)^2$，求 $B$ 相似于什么对角矩阵，并确定 $k$ 为何值时 $B$ 正定。

**解：**  
由于 $A$ 是实对称矩阵，存在正交矩阵 $P$，使得  
$$
P^\top A P = D = \text{diag}(2, 2, 0).
$$

则  
$$
B = (kI + A)^2 = P(kI + D)^2 P^\top,
$$  
即 $B$ 相似于  
$$
\text{diag}((k+2)^2, (k+2)^2, k^2).
$$

要使 $B$ 正定，需所有特征值大于零：

- $(k+2)^2 > 0 \Rightarrow k \neq -2$，
- $k^2 > 0 \Rightarrow k \neq 0$。

综上，当 $k \neq -2$ 且 $k \neq 0$ 时，$B$ 正定。

---

### 六、总结

| 类型 | 条件 |
|------|------|
| 正定 | 所有特征值 > 0，或所有顺序主子式 > 0 |
| 半正定 | 所有特征值 ≥ 0，或所有主子式 ≥ 0 |
| 负定 | 所有特征值 < 0，或 $(-1)^k P_k > 0$ |
| 半负定 | 所有特征值 ≤ 0，或 $(-1)^k P_k ≥ 0$ |
| 不定 | 既有正也有负特征值 |

## **§6.3 曲面与空间曲线**

### **一、曲面**

在三维空间 $\mathbb{R}^3$ 中，满足三元方程  
$$
F(x, y, z) = 0
$$  
的所有有序数组 $(x, y, z)$ 所对应的点的集合  
$$
S = \{(x, y, z) \mid F(x, y, z) = 0\}
$$  
称为**空间中的曲面**。

如果空间曲面 $S$ 与三元方程 $F(x, y, z) = 0$ 满足以下两个条件：

1. **曲面上的任意一点** $(x, y, z)$ 都满足该方程；
2. **所有满足该方程的点** $(x, y, z)$ 都是曲面 $S$ 上的点，

那么称这个方程为**曲面 $S$ 的方程**，而曲面 $S$ 是该方程的**图形**。

---

#### 曲面研究的两个基本问题：

1. **已知几何对象（如球面、柱面等），求其方程；**
2. **已知一个三元方程，研究其所表示的曲面的形状与性质。**

下面我们通过具体例子来说明这两个问题的解决方法。

---

#### 例1：球面的方程

设空间中一点 $M_0(x_0, y_0, z_0)$ 为球心，半径为 $R$，求球面的方程。

**解：** 设 $M(x, y, z)$ 是球面上任一点，则 $M$ 到球心的距离为 $R$，即  
$$
\sqrt{(x - x_0)^2 + (y - y_0)^2 + (z - z_0)^2} = R.
$$  
两边平方得：  
$$
(x - x_0)^2 + (y - y_0)^2 + (z - z_0)^2 = R^2.
$$  
这就是以 $(x_0, y_0, z_0)$ 为球心，半径为 $R$ 的球面的标准方程。

例如：
- 方程 $x^2 + y^2 + z^2 = R^2$ 表示以原点为球心的球面；
- 方程 $x^2 + 2x + y^2 + z^2 - 2z - 2 = 0$，配方后可化为：  
  $$
  (x + 1)^2 + y^2 + (z - 1)^2 = 4,
  $$  
  表示以 $(-1, 0, 1)$ 为球心，半径为 2 的球面。

---

#### 例2：圆柱面的方程

考虑方程  
$$
x^2 + y^2 = R^2.
$$  
在二维平面 $Oxy$ 上，它表示一个圆；但在三维空间中，由于方程不包含变量 $z$，所以对于任意 $z$ 值，只要 $x^2 + y^2 = R^2$ 成立，点 $(x, y, z)$ 就属于该曲面。

因此，该方程表示的是一个**以 $Oxy$ 平面上的圆为准线、母线平行于 $z$ 轴的圆柱面**。

---

#### 一般柱面的定义与方程

若一条动直线 $l$ 沿着某条曲线 $C$ 移动，并始终与某固定直线 $l'$ 平行，则所形成的曲面称为**柱面**。其中：

- 曲线 $C$ 称为**准线**；
- 直线 $l$ 称为**母线**。

**结论：**

- 若方程不含变量 $z$，则母线平行于 $z$ 轴；
- 若方程不含变量 $x$，则母线平行于 $x$ 轴；
- 若方程不含变量 $y$，则母线平行于 $y$ 轴。

---

#### 例3：其他类型的柱面

分析下列方程所表示的曲面类型：

1. **$\frac{x^2}{a^2} + \frac{y^2}{b^2} = 1$**  
   - 在 $Oxy$ 平面上表示椭圆；
   - 不含变量 $z$，故表示**椭圆柱面**，母线平行于 $z$ 轴。

2. **$\frac{x^2}{a^2} - \frac{y^2}{b^2} = 1$**  
   - 在 $Oxy$ 平面上表示双曲线；
   - 同样不含 $z$，故表示**双曲柱面**，母线平行于 $z$ 轴。

3. **$x^2 = 2py$**  
   - 在 $Oxy$ 平面上表示抛物线；
   - 不含 $z$，故表示**抛物柱面**，母线平行于 $z$ 轴。

---

#### 例4：不同坐标平面上的柱面

分析下列方程所表示的曲面类型：

1. **$\frac{y^2}{a^2} + \frac{z^2}{b^2} = 1$**  
   - 准线在 $Oyz$ 平面，表示**椭圆柱面**，母线平行于 $x$ 轴。

2. **$\frac{y^2}{a^2} - \frac{z^2}{b^2} = 1$**  
   - 准线在 $Oyz$ 平面，表示**双曲柱面**，母线平行于 $x$ 轴。

3. **$y^2 = 2pz$**  
   - 准线在 $Oyz$ 平面，表示**抛物柱面**，母线平行于 $x$ 轴。

---

#### 二、旋转曲面

一条平面曲线绕某一坐标轴旋转一周所形成的曲面称为**旋转曲面**。

##### 构造方法：

设曲线 $C$ 是 $Oyz$ 平面上的一条曲线，其方程为  
$$
f(y, z) = 0.
$$  
将该曲线绕 $z$ 轴旋转一周，得到的旋转曲面方程为：  
$$
f(\pm \sqrt{x^2 + y^2}, z) = 0.
$$  

同理：

- 绕 $y$ 轴旋转：  
  $$
  f(y, \pm \sqrt{x^2 + z^2}) = 0.
  $$
- 绕 $x$ 轴旋转：  
  $$
  f(\pm \sqrt{y^2 + z^2}, x) = 0.
  $$

---

#### 例5：圆锥面的方程

设 $Oyz$ 平面上的直线 $y = kz$ 绕 $z$ 轴旋转一周，得到的曲面为：

$$
\pm \sqrt{x^2 + y^2} = kz \Rightarrow x^2 + y^2 = k^2 z^2.
$$  
这就是**圆锥面**的方程。当 $k = 1$ 时，方程变为  
$$
x^2 + y^2 = z^2,
$$  
此时锥面关于 $z$ 轴对称，张角为 $90^\circ$。

---

#### 例6：旋转抛物面

考虑方程  
$$
z = x^2 + y^2.
$$  
可以写成  
$$
z = (\pm \sqrt{x^2 + y^2})^2,
$$  
这表示它是 $Oyz$ 平面上的抛物线 $z = y^2$ 绕 $z$ 轴旋转一周所得的曲面，称为**旋转抛物面**。

同样地，$Oxz$ 平面上的曲线 $z = x^2$ 绕 $z$ 轴旋转一周也形成同样的曲面。

---

#### 总结

| 类型 | 特征 | 示例 |
|------|------|------|
| 球面 | 形式为 $(x - x_0)^2 + (y - y_0)^2 + (z - z_0)^2 = R^2$ | $x^2 + y^2 + z^2 = 1$ |
| 圆柱面 | 缺少一个变量，母线平行于该变量轴 | $x^2 + y^2 = R^2$ |
| 椭圆柱面 | $\frac{x^2}{a^2} + \frac{y^2}{b^2} = 1$ | 母线平行于 $z$ 轴 |
| 双曲柱面 | $\frac{x^2}{a^2} - \frac{y^2}{b^2} = 1$ | 母线平行于 $z$ 轴 |
| 抛物柱面 | $x^2 = 2py$ | 母线平行于 $z$ 轴 |
| 旋转曲面 | 曲线绕坐标轴旋转而成 | $x^2 + y^2 = z^2$（圆锥面）、$z = x^2 + y^2$（旋转抛物面） |


### **二、空间曲线**

在三维空间中，**空间曲线**通常可以看作是两个曲面的交线。设两个曲面 $S_1$ 和 $S_2$ 的方程分别为  
$$
F_1(x, y, z) = 0 \quad \text{和} \quad F_2(x, y, z) = 0,
$$  
则这两个方程联立  
$$
\begin{cases}
F_1(x, y, z) = 0 \\
F_2(x, y, z) = 0
\end{cases}
\tag{6.5}
$$  
就表示它们的交线 $C$，称为曲线 $C$ 的**一般式方程**。

---

#### 1. 空间曲线的一般式与参数式表示

- **一般式**：由两个曲面方程联立给出，如上所述；
- **参数式**：将曲线上动点的坐标 $x, y, z$ 都表示为一个参数 $t$ 的函数：
  $$
  \begin{cases}
  x = x(t), \\
  y = y(t), \\
  z = z(t),
  \end{cases}
  \quad t \in [a, b].
  $$

这是曲线的**参数方程**，常用于描述运动轨迹或复杂形状的空间曲线。

---

#### 例7 分析空间曲线的几何意义

考虑方程组：  
$$
\begin{cases}
x^2 + y^2 = 1, \\
2x + 2y + 3z = 6.
\end{cases}
$$

**分析：**

- 第一个方程 $x^2 + y^2 = 1$ 表示一个**圆柱面**，其准线是 $Oxy$ 平面上的单位圆，母线平行于 $z$ 轴；
- 第二个方程 $2x + 2y + 3z = 6$ 是一个**平面**，它与 $x, y, z$ 轴分别在 $(3, 0, 0)$, $(0, 3, 0)$, $(0, 0, 2)$ 处相交；
- 该方程组表示的是**圆柱面与平面的交线**，即一条空间曲线（见图6.10）。

---

#### 例8 圆柱螺线的参数方程

设空间曲线的参数方程为：  
$$
\begin{cases}
x = a \cos t, \\
y = a \sin t, \\
z = bt,
\end{cases}
\quad t \in \mathbb{R}.
$$

这条曲线称为**圆柱螺线**，它的几何特征如下：

- 它位于圆柱面 $x^2 + y^2 = a^2$ 上；
- 每绕一圈（$t$ 增加 $2\pi$），$z$ 增加 $2\pi b$，这个增量称为**螺距**，记作 $h = 2\pi b$；
- 曲线呈螺旋状上升，常见于弹簧、螺丝等物体表面。

---

#### 2. 空间曲线在坐标平面上的投影

设空间曲线 $C$ 为准线，以它为基础构造一个**母线平行于某一坐标轴的柱面**，该柱面与相应坐标平面的交线就是曲线 $C$ 在该坐标平面上的**投影曲线**。

- **在 $Oxy$ 平面上的投影**：消去 $z$，得到关于 $x, y$ 的方程；
- **在 $Oyz$ 平面上的投影**：消去 $x$，得到关于 $y, z$ 的方程；
- **在 $Oxz$ 平面上的投影**：消去 $y$，得到关于 $x, z$ 的方程。

---

#### 例9 求曲线在 $Oxy$ 平面上的投影

设曲线 $C$ 由以下方程组表示：  
$$
\begin{cases}
x^2 + y^2 - ax = 0, \\
z = f(x, y).
\end{cases}
$$

**解：**

- 方程 $x^2 + y^2 - ax = 0$ 可化为  
  $$
  (x - \frac{a}{2})^2 + y^2 = \left(\frac{a}{2}\right)^2,
  $$  
  这是一个以 $(\frac{a}{2}, 0)$ 为圆心、半径为 $\frac{a}{2}$ 的圆柱面；
- 该圆柱面与 $Oxy$ 平面的交线即为原曲线在 $Oxy$ 平面上的投影；
- 投影曲线为圆：  
  $$
  (x - \frac{a}{2})^2 + y^2 = \left(\frac{a}{2}\right)^2.
  $$

---

#### 例10 求曲线在 $Oxy$ 平面上的投影

设曲线 $C$ 由球面与平面的交线组成：  
$$
\begin{cases}
x^2 + y^2 + z^2 = 16, \\
z = 2.
\end{cases}
$$

**解：**

- 将 $z = 2$ 代入球面方程得：  
  $$
  x^2 + y^2 + 4 = 16 \Rightarrow x^2 + y^2 = 12.
  $$
- 所以曲线在 $Oxy$ 平面上的投影为圆：  
  $$
  x^2 + y^2 = 12.
  $$

---

#### 例11 求曲线在 $Oyz$ 平面上的投影

设曲线 $C$ 由以下方程组表示：  
$$
\begin{cases}
x^2 + y^2 + z^2 = 4, \\
x^2 + y^2 = 3z.
\end{cases}
$$

**解：**

- 从第二个方程得 $x^2 + y^2 = 3z$，代入第一个方程得：  
  $$
  3z + z^2 = 4 \Rightarrow z^2 + 3z - 4 = 0.
  $$
- 解得 $z = 1$ 或 $z = -4$，其中 $z = -4$ 不满足原方程（因为 $x^2 + y^2 \geq 0$），舍去；
- 当 $z = 1$ 时，代入 $x^2 + y^2 = 3z = 3$，得  
  $$
  y^2 = 3 - x^2 \Rightarrow |y| \leq \sqrt{3}.
  $$
- 所以曲线在 $Oyz$ 平面上的投影为直线段：  
  $$
  z = 1, \quad |y| \leq \sqrt{3}.
  $$

---

#### 总结：空间曲线的基本性质

| 类型 | 表达方式 | 特点 |
|------|-----------|------|
| 一般式 | $\begin{cases} F_1(x, y, z) = 0 \\ F_2(x, y, z) = 0 \end{cases}$ | 两曲面交线 |
| 参数式 | $\begin{cases} x = x(t) \\ y = y(t) \\ z = z(t) \end{cases}$ | 描述运动轨迹 |
| 投影 | 消去一个变量后与坐标平面联立 | 得到二维平面上的曲线 |

---

#### 典型应用举例

| 曲线名称 | 参数方程 | 几何意义 |
|----------|------------|-------------|
| 圆柱螺线 | $\begin{cases} x = a \cos t \\ y = a \sin t \\ z = bt \end{cases}$ | 螺旋形路径，常见于机械结构 |
| 圆锥曲线 | $\begin{cases} x = r \cos t \\ y = r \sin t \\ z = kr \end{cases}$ | 锥面上的螺旋线 |
| 球面交线 | $\begin{cases} x^2 + y^2 + z^2 = R^2 \\ ax + by + cz = d \end{cases}$ | 球面与平面交线，通常为圆 |

---

## **§6.4 二次曲面**

在三维空间中，**二次曲面**是由三元二次方程所表示的几何图形。一般形式为：

$$
a_{11}x^2 + a_{22}y^2 + a_{33}z^2 + 2a_{12}xy + 2a_{13}xz + 2a_{23}yz + b_1x + b_2y + b_3z + c = 0,
$$

其中 $ a_{ij}, b_i, c \in \mathbb{R} $。

常见的二次曲面包括：**球面、椭球面、抛物面、双曲面、柱面等**。通过适当的坐标变换（如平移或正交变换），可以将一般的二次方程化为标准形式，从而更清晰地了解其几何特征。

---

### 一、椭球面

#### 标准方程：
$$
\frac{x^2}{a^2} + \frac{y^2}{b^2} + \frac{z^2}{c^2} = 1,\quad (a, b, c > 0)
$$

#### 几何特征：

1. **范围**：  
   $$
   |x| \leq a,\quad |y| \leq b,\quad |z| \leq c.
   $$  
   曲面被限制在六个平面 $x = \pm a$, $y = \pm b$, $z = \pm c$ 所围成的长方体内。

2. **对称性**：  
   关于坐标原点、三个坐标轴和三个坐标面对称。

3. **截痕形状**：  
   - 用平面 $z = z_0$ 截取，得到椭圆：  
     $$
     \frac{x^2}{a^2(1 - z_0^2/c^2)} + \frac{y^2}{b^2(1 - z_0^2/c^2)} = 1.
     $$
   - 类似地，用 $x = x_0$ 或 $y = y_0$ 截取也得到椭圆。

4. **特殊情形**：当 $a = b$ 或 $b = c$ 或 $a = c$ 时，该椭球面是一个**旋转椭球面**。

> 图形示意：见图6.14，呈光滑封闭曲面，类似“拉伸的球”。

---

### 二、抛物面

#### 1. 椭圆抛物面

##### 标准方程：
$$
z = \frac{x^2}{2p} + \frac{y^2}{2q},\quad (p, q > 0)
$$

##### 几何特征：

- **范围**：若 $p, q > 0$，则曲面位于 $Oxy$ 平面上方；若 $p, q < 0$，则在下方。
- **对称性**：关于 $z$ 轴及 $Oyz$、$Oxz$ 平面对称。
- **截痕形状**：
  - 用 $z = z_0$ 截取，得椭圆；
  - 用 $x = x_0$ 或 $y = y_0$ 截取，得抛物线。

> 特殊情况：当 $p = q$ 时，称为**旋转抛物面**，图形如图6.15所示。

---

#### 2. 双曲抛物面（马鞍面）

##### 标准方程：
$$
z = \frac{x^2}{2p} - \frac{y^2}{2q},\quad (p, q > 0)
$$

##### 几何特征：

- **范围**：无界，可向各方向无限延伸。
- **对称性**：关于 $z$ 轴及 $Oyz$、$Oxz$ 平面对称。
- **截痕形状**：
  - 用 $z = z_0$ 截取，得双曲线；
  - 用 $z = 0$ 截取，得两条相交直线；
  - 用 $x = x_0$ 或 $y = y_0$ 截取，得抛物线。

> 图形示意：如图6.16所示，形似“马鞍”，故又名**马鞍面**。

---

### 三、双曲面

#### 1. 单叶双曲面

##### 标准方程：
$$
\frac{x^2}{a^2} + \frac{y^2}{b^2} - \frac{z^2}{c^2} = 1,\quad (a, b, c > 0)
$$

##### 几何特征：

- **范围**：不在椭圆柱面 $\frac{x^2}{a^2} + \frac{y^2}{b^2} = 1$ 内部。
- **对称性**：关于所有坐标轴、坐标面和原点对称。
- **截痕形状**：
  - 用 $z = z_0$ 截取，得椭圆；
  - 用 $x = x_0$ 或 $y = y_0$ 截取，得双曲线；
  - 当 $|x_0| = a$ 或 $|y_0| = b$ 时，交线是两条相交直线。

> 图形示意：如图6.17和6.18所示，具有一个连续的“叶子”状结构。

---

#### 2. 双叶双曲面

##### 标准方程：
$$
\frac{x^2}{a^2} + \frac{y^2}{b^2} - \frac{z^2}{c^2} = -1,\quad (a, b, c > 0)
$$

##### 几何特征：

- **范围**：$|z| \geq c$，即曲面位于两平行平面 $z = \pm c$ 外侧。
- **对称性**：与单叶双曲面相同。
- **截痕形状**：
  - 用 $z = z_0$ 截取，得椭圆；
  - 用 $x = x_0$ 或 $y = y_0$ 截取，得双曲线。

> 图形示意：如图6.19所示，由两个互不相连的“叶片”组成。

---

### 四、典型例题讲解

#### 例1：化二次型为标准形并判断曲面类型

设二次型：
$$
f(x_1, x_2, x_3) = 3x_1^2 + 2x_2^2 + x_3^2 - 4x_1x_2 - 4x_1x_3.
$$

写出对应的矩阵：
$$
A = \begin{bmatrix}
3 & -2 & -2 \\
-2 & 2 & 0 \\
-2 & 0 & 1
\end{bmatrix}.
$$

求特征值与特征向量，得：
- $\lambda_1 = 5$，对应特征向量 $\alpha_1 = (2, -2, 1)$；
- $\lambda_2 = 2$，对应特征向量 $\alpha_2 = (2, 1, -2)$；
- $\lambda_3 = -1$，对应特征向量 $\alpha_3 = (1, 2, 2)$。

将其标准化正交化后构造正交矩阵 $C$，作正交变换 $X = CY$，得标准形：
$$
f = 5y_1^2 + 2y_2^2 - y_3^2.
$$

令 $f = 5$，得：
$$
\frac{y_1^2}{1} + \frac{y_2^2}{\frac{5}{2}} - \frac{y_3^2}{5} = 1.
$$

此为**单叶双曲面**的标准形式。

---

#### 例2：求曲面交线及其投影

设两个曲面分别为：
- 抛物面：$z = 1 - x^2$，
- 抛物柱面：$z = 3x^2 + y^2$。

联立消去 $z$ 得：
$$
1 - x^2 = 3x^2 + y^2 \Rightarrow 4x^2 + y^2 = 1.
$$

这是交线在 $Oxy$ 平面上的**投影柱面方程**。

与 $z = 1 - x^2$ 联立，得交线在空间中的参数方程为：
$$
\begin{cases}
x = x, \\
y = \sqrt{1 - 4x^2}, \\
z = 1 - x^2.
\end{cases}
$$

交线在 $Oxy$ 平面上的投影曲线为：
$$
4x^2 + y^2 = 1,
$$
这是一个椭圆。

> 图形示意：如图6.20所示，交线是一条空间闭合曲线，投影为椭圆。

---

### 总结：常见二次曲面的标准形式与几何特征

| 曲面类型       | 标准方程                                       | 几何特征                                 |
|----------------|------------------------------------------------|------------------------------------------|
| 椭球面         | $\frac{x^2}{a^2} + \frac{y^2}{b^2} + \frac{z^2}{c^2} = 1$ | 封闭、对称、有界                         |
| 椭圆抛物面     | $z = \frac{x^2}{2p} + \frac{y^2}{2q}$        | 开口向上/向下，对称、无界                |
| 双曲抛物面     | $z = \frac{x^2}{2p} - \frac{y^2}{2q}$        | 马鞍形，无界，有双曲线截痕               |
| 单叶双曲面     | $\frac{x^2}{a^2} + \frac{y^2}{b^2} - \frac{z^2}{c^2} = 1$ | 一个连通部分，有椭圆与双曲线截痕         |
| 双叶双曲面     | $\frac{x^2}{a^2} + \frac{y^2}{b^2} - \frac{z^2}{c^2} = -1$ | 两个分离部分，有椭圆与双曲线截痕         |

---
