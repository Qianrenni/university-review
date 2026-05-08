
# 一、什么是图神经网络？

**图神经网络（Graph Neural Network, GNN）** 是一类专门用于处理**图结构数据**的深度学习模型。它能够从图中提取节点、边以及全局信息，并进行端到端的学习。

## 🔍 为什么需要 GNN？

现实世界中许多数据天然具有图结构：

- 社交网络（用户为节点，好友关系为边）
- 分子结构（原子为节点，化学键为边）
- 推荐系统（用户和商品为节点，点击/购买为边）
- 知识图谱（实体为节点，关系为边）

传统神经网络（如 CNN、RNN）无法有效建模这种非欧几里得空间的数据，而 GNN 正是为此设计的。

---

# 二、图数据的基本结构

一个图通常表示为 $ G = (V, E) $，其中：

| 符号 | 含义 |
|------|------|
| $ V $ | 节点集合（Nodes / Vertices） |
| $ E $ | 边集合（Edges） |

每个节点 $ v_i \in V $ 可以有特征向量 $ x_i \in \mathbb{R}^d $，每条边 $ e_{ij} \in E $ 可以有权重或类型等信息。

## 示例：图的邻接矩阵表示

对于包含 $ N $ 个节点的图，可以用一个 $ N \times N $ 的邻接矩阵 $ A $ 表示连接关系：

$$
A_{ij} =
\begin{cases}
1 & \text{如果存在从 } i \text{ 到 } j \text{ 的边} \\
0 & \text{否则}
\end{cases}
$$

---

# 三、GNN 的核心思想

GNN 的核心目标是为每个节点学习一个嵌入向量（Embedding），这个向量融合了该节点自身及其邻居的信息。

## 🔄 消息传递机制（Message Passing）

GNN 的基本计算流程如下：

1. **聚合邻居信息**（Aggregation）  
2. **更新节点表示**（Update）

数学表达如下：

$$
h_i^{(l+1)} = \sigma \left( W^{(l)} \cdot \text{AGGREGATE}_{j \in \mathcal{N}(i)} \left( h_j^{(l)} \right) \right)
$$

其中：

- $ h_i^{(l)} $：第 $ l $ 层中节点 $ i $ 的表示
- $ \mathcal{N}(i) $：节点 $ i $ 的邻居集合
- $ \sigma $：激活函数（如 ReLU）
- $ W^{(l)} $：可学习参数矩阵

---

# 四、GNN 的主要变体

## 1. GCN（Graph Convolutional Network）

- 使用图拉普拉斯矩阵对图结构进行卷积操作
- 适用于无向图
- 公式简化版：

$$
H^{(l+1)} = \sigma \left( \tilde{D}^{-\frac{1}{2}} \tilde{A} \tilde{D}^{-\frac{1}{2}} H^{(l)} W^{(l)} \right)
$$

其中：

- $ \tilde{A} = A + I $
- $ \tilde{D} $：度矩阵

## PyTorch 示例（使用 PyTorch Geometric）

```python
import torch.nn as nn
from torch_geometric.nn import GCNConv

class GCN(nn.Module):
    def __init__(self, num_features, hidden_dim, num_classes):
        super().__init__()
        self.conv1 = GCNConv(num_features, hidden_dim)
        self.conv2 = GCNConv(hidden_dim, num_classes)

    def forward(self, data):
        x, edge_index = data.x, data.edge_index
        x = self.conv1(x, edge_index)
        x = torch.relu(x)
        x = self.conv2(x, edge_index)
        return torch.log_softmax(x, dim=1)
```

---

## 2. GAT（Graph Attention Network）

- 引入注意力机制（Attention），自动学习邻居节点的重要性
- 更灵活，适用于异质图

## 公式示意

$$
e_{ij} = a^\top [W h_i \| W h_j] \quad \text{（注意力系数）}
$$
$$
\alpha_{ij} = \frac{\exp(e_{ij})}{\sum_{k \in \mathcal{N}(i)} \exp(e_{ik})}
$$
$$
h_i' = \sigma\left(\sum_{j \in \mathcal{N}(i)} \alpha_{ij} W h_j \right)
$$

## PyTorch 示例

```python
from torch_geometric.nn import GATConv

class GAT(nn.Module):
    def __init__(self, num_features, hidden_dim, heads=4):
        super().__init__()
        self.conv1 = GATConv(num_features, hidden_dim, heads=heads)
        self.conv2 = GATConv(hidden_dim * heads, hidden_dim, heads=1)

    def forward(self, data):
        x, edge_index = data.x, data.edge_index
        x = self.conv1(x, edge_index)
        x = torch.relu(x)
        x = self.conv2(x, edge_index)
        return torch.log_softmax(x, dim=1)
```

---

## 3. GraphSAGE（Graph Sample and Aggregate）

- 通过采样邻居并聚合其特征来生成节点表示
- 支持大规模图的归纳学习（Inductive Learning）

---

## 4. GGNN（Gated Graph Neural Network）

- 引入门控机制（类似 LSTM），增强记忆能力
- 适用于循环依赖结构

---

## 5. GIN（Graph Isomorphism Network）

- 提出了一种更强的图同构识别能力
- 使用多层感知机（MLP）进行聚合和变换

---

# 五、GNN 的典型任务

| 任务类型 | 输入 | 输出 |
|----------|------|------|
| 节点分类（Node Classification） | 单个图 | 每个节点的类别 |
| 链接预测（Link Prediction） | 图 | 是否存在边 |
| 图分类（Graph Classification） | 多个图 | 整个图的类别 |
| 图回归（Graph Regression） | 多个图 | 连续值输出（如分子能量） |
| 社区发现（Community Detection） | 图 | 节点聚类结果 |

---

# 六、实战项目推荐

## 1. Cora 论文分类（节点级别）

- 图中每个节点代表一篇论文
- 边表示论文之间的引用关系
- 目标是预测论文所属的主题类别

```bash
from torch_geometric.datasets import Planetoid
dataset = Planetoid(root='/tmp/Cora', name='Cora')
```

## 2. MUTAG 分子分类（图级别）

- 每个图代表一个分子结构
- 目标是判断该分子是否具有诱变性

```bash
from torch_geometric.datasets import TUDataset
dataset = TUDataset(root='/tmp/MUTAG', name='MUTAG')
```

---

# 七、GNN 的训练流程详解

## 步骤 1：准备图数据

使用 `PyTorch Geometric` 加载图数据集：

```python
from torch_geometric.data import DataLoader

train_loader = DataLoader(dataset, batch_size=32, shuffle=True)
```

## 步骤 2：定义模型

如前面的 GCN 或 GAT 模型

## 步骤 3：定义损失函数和优化器

```python
criterion = nn.CrossEntropyLoss()
optimizer = torch.optim.Adam(model.parameters(), lr=0.01)
```

## 步骤 4：训练循环

```python
for epoch in range(100):
    for data in train_loader:
        out = model(data)
        loss = criterion(out[data.train_mask], data.y[data.train_mask])
        optimizer.zero_grad()
        loss.backward()
        optimizer.step()
```

---

# 八、GNN 的优势与局限

## ✅ 优势

- 能处理复杂的关系数据
- 支持节点、边、图级别的多种任务
- 可解释性强于黑盒模型

## ❌ 局限

- 对大规模图计算效率低
- 依赖高质量的图结构（噪声敏感）
- 存在“过平滑”问题（Over-smoothing）

---

# 九、进阶技巧与调优建议

| 技巧 | 描述 |
|------|------|
| 跳数控制 | 控制感受野大小（如只聚合 2-hop 邻居） |
| Dropout | 在每一层加入防止过拟合 |
| BatchNorm | 提升训练稳定性 |
| 多跳聚合 | 多层 GNN 聚合更远邻居信息 |
| 图采样 | 处理大规模图时减少计算量 |
| 自监督预训练 | 如 GraphMAE、GRACE 等方式提升效果 |

---

# 十、总结：GNN 的关键点

| 组件 | 作用 |
|------|------|
| 图结构 | 输入数据形式 |
| 消息传递 | 核心计算机制 |
| 聚合函数 | 融合邻居信息 |
| 更新函数 | 更新节点表示 |
| 注意力机制 | 动态调整邻居权重 |
| 损失函数 | 衡量预测误差 |
| 优化器 | 更新参数 |
| 应用场景 | 节点分类、图分类、链接预测等 |

---

# 十一、拓展学习资源推荐

| 类型 | 地址 |
|------|------|
| 官方文档（PyTorch Geometric） | <https://pytorch-geometric.readthedocs.io/en/latest/> |
| 中文教程 | <https://zhuanlan.zhihu.com/p/628797985> |
| 视频课程 | 李宏毅《图神经网络》系列视频 |
| GitHub 示例 | 搜索关键词 `GNN tutorial pytorch geometric` |
