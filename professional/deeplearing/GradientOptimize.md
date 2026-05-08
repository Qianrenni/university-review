
# 一、梯度下降的基本思想

梯度下降是一种一阶优化算法，用于最小化目标函数 $ f(\theta) $，其中 $ \theta $ 是模型参数。

## 更新规则

$$
\theta_{t+1} = \theta_t - \eta \cdot \nabla_\theta f(\theta_t)
$$

其中：

- $ \theta_t $：第 t 步的参数
- $ \eta $：学习率（learning rate）
- $ \nabla_\theta f(\theta_t) $：当前参数下的梯度

---

# 二、常见优化方法详解

---

## 1. 随机梯度下降（Stochastic Gradient Descent, SGD）

## 原理

使用单个样本或小批量数据计算梯度，以减少计算开销并引入噪声帮助跳出局部极小值。

## 更新公式

$$
\theta_{t+1} = \theta_t - \eta \cdot g_t
$$
其中 $ g_t = \nabla_\theta f(\theta_t) $

## 特点

| 属性 | 描述 |
|------|------|
| 优点 | 简单、高效、适合大规模数据 |
| 缺点 | 收敛慢、容易震荡、难以适应不同参数的学习需求 |

## 适用场景

- 小型网络
- 理论研究
- 对速度要求不高的任务

---

## 2. 动量法（Momentum）

## 原理

引入动量项（历史梯度方向的加权平均），模拟惯性效应，加速收敛并减少震荡。

## 更新公式

$$
v_{t+1} = \beta v_t + (1 - \beta) g_t \\
\theta_{t+1} = \theta_t - \eta \cdot v_{t+1}
$$

通常取 $ \beta = 0.9 $

## 特点

| 属性 | 描述 |
|------|------|
| 优点 | 加快收敛速度、缓解震荡 |
| 缺点 | 可能冲过最优解（overshooting） |
| 直观理解 | 类似于“下坡时滚雪球”——越滚越大，越走越快 |

---

## 3. Nesterov Accelerated Gradient（NAG）

## 原理

先朝动量方向迈出一步，再计算梯度，提前感知“未来”的梯度方向，提高稳定性。

## 更新公式

$$
\theta_{\text{lookahead}} = \theta_t - \eta \cdot v_t \\
g_t = \nabla f(\theta_{\text{lookahead}}) \\
v_{t+1} = \beta v_t + g_t \\
\theta_{t+1} = \theta_t - \eta \cdot v_{t+1}
$$

## 特点

| 属性 | 描述 |
|------|------|
| 优点 | 比 Momentum 更稳定 |
| 缺点 | 实现略复杂 |
| 应用 | 在理论分析和一些高级优化器中被采用 |

---

## 4. AdaGrad（Adaptive Gradient Algorithm）

## 原理

为每个参数分配不同的学习率，对频繁出现的特征降低学习率，对稀疏特征保持高学习率。

## 更新公式

$$
G_t = G_{t-1} + g_t^2 \\
\theta_{t+1} = \theta_t - \frac{\eta}{\sqrt{G_t + \epsilon}} \odot g_t
$$

其中 $ G_t $ 是梯度平方的累积和，$ \epsilon $ 是防止除零的小常数。

## 特点

| 属性 | 描述 |
|------|------|
| 优点 | 自适应调整学习率，适合稀疏数据 |
| 缺点 | 学习率单调递减，后期几乎停止更新 |
| 适用 | NLP、推荐系统中的嵌入层 |

---

## 5. RMSProp（Root Mean Square Propagation）

## 原理

改进 AdaGrad 的问题，使用指数衰减的滑动窗口来控制历史梯度平方的积累。

## 更新公式

$$
E[g^2]_t = \beta E[g^2]_{t-1} + (1 - \beta) g_t^2 \\
\theta_{t+1} = \theta_t - \frac{\eta}{\sqrt{E[g^2]_t + \epsilon}} g_t
$$

通常取 $ \beta = 0.9 $

## 特点

| 属性 | 描述 |
|------|------|
| 优点 | 解决了 AdaGrad 学习率衰减过快的问题 |
| 缺点 | 参数敏感，需调参 |
| 应用 | 强化学习、RNN 等需要动态学习率的任务 |

---

## 6. Adam（Adaptive Moment Estimation）

## 原理

结合动量（一阶矩估计）和 RMSProp（二阶矩估计），同时对梯度的一阶和二阶矩进行指数加权平均，并做偏差修正。

## 更新公式

$$
m_t = \beta_1 m_{t-1} + (1 - \beta_1) g_t \quad \text{(一阶矩)} \\
v_t = \beta_2 v_{t-1} + (1 - \beta_2) g_t^2 \quad \text{(二阶矩)} \\
\hat{m}_t = \frac{m_t}{1 - \beta_1^t}, \quad \hat{v}_t = \frac{v_t}{1 - \beta_2^t} \quad \text{(偏差修正)} \\
\theta_{t+1} = \theta_t - \eta \cdot \frac{\hat{m}_t}{\sqrt{\hat{v}_t} + \epsilon}
$$

常用参数设置：

- $ \beta_1 = 0.9 $
- $ \beta_2 = 0.999 $
- $ \epsilon = 1e-8 $

## 特点

| 属性 | 描述 |
|------|------|
| 优点 | 收敛快、自适应学习率、适合大多数任务 |
| 缺点 | 可能在某些任务上泛化能力不如 SGD with Momentum |
| 应用 | 计算机视觉、自然语言处理、强化学习等广泛领域 |

---

## 7. AdamW（Decoupled Weight Decay）

## 原理

Adam 中的 weight decay 并不是标准形式（与学习率耦合），AdamW 对其进行了分离，使正则化更有效。

## 更新公式

$$
\theta_{t+1} = \theta_t - \eta \cdot \left( \frac{\hat{m}_t}{\sqrt{\hat{v}_t} + \epsilon} + \lambda \theta_t \right)
$$

其中 $ \lambda $ 是权重衰减系数。

## 特点

| 属性 | 描述 |
|------|------|
| 优点 | 更好的泛化性能、更适合大模型 |
| 缺点 | 略复杂 |
| 应用 | 当前主流模型（如 Transformers、Vision Transformers）首选优化器之一 |

---

## 8. AMSGrad

## 原理

Adam 有时会因为 $ v_t $ 不断增大而导致学习率过小。AMSGrad 通过维护一个最大值 $ \hat{v}_t = \max(\hat{v}_{t-1}, v_t) $ 来避免这个问题。

## 更新公式

$$
v_t = \beta_2 v_{t-1} + (1 - \beta_2) g_t^2 \\
\hat{v}_t = \max(\hat{v}_{t-1}, v_t) \\
\theta_{t+1} = \theta_t - \eta \cdot \frac{m_t}{\sqrt{\hat{v}_t} + \epsilon}
$$

## 特点

| 属性 | 描述 |
|------|------|
| 优点 | 收敛性更强 |
| 缺点 | 效果提升有限，实际中较少使用 |

---

## 9. Nadam（Nesterov + Adam）

## 原理

结合 NAG 和 Adam，即在 Adam 的动量部分使用 Nesterov 提前预测的梯度。

## 更新公式

$$
m_t = \beta_1 m_{t-1} + (1 - \beta_1) g_t \\
\tilde{m}_t = \frac{\beta_1 m_t}{1 - \beta_1^{t+1}} + \frac{(1 - \beta_1) g_t}{1 - \beta_1^t} \\
\theta_{t+1} = \theta_t - \eta \cdot \frac{\tilde{m}_t}{\sqrt{v_t} + \epsilon}
$$

## 特点

| 属性 | 描述 |
|------|------|
| 优点 | 结合动量和自适应学习率的优点 |
| 缺点 | 实现较复杂，效果不一定优于 Adam |

---

## 10. LAMB（Layer-wise Adaptive Moments optimizer for Batch normalization）

## 原理

针对大规模 Transformer 模型提出，解决 Adam 在大 batch size 下训练不稳定的问题。它对每一层使用归一化的更新步长。

## 更新公式

$$
r_t = \frac{\|\theta_t\|}{\| \Delta \theta_t \|} \\
\Delta \theta_t = - \eta \cdot \frac{\hat{m}_t}{\sqrt{\hat{v}_t} + \epsilon} \\
\theta_{t+1} = \theta_t + r_t \cdot \Delta \theta_t
$$

## 特点

| 属性 | 描述 |
|------|------|
| 优点 | 大 batch size 下训练更稳定，适合预训练模型 |
| 缺点 | 实现复杂，一般用于特定场景 |

---

# 三、优化器对比总结表

| 优化器 | 是否自适应 | 是否带动量 | 是否支持 Layer-wise 调整 | 是否适合稀疏数据 | 是否适合大模型 |
|--------|-------------|--------------|----------------------------|-------------------|----------------|
| SGD     | ❌           | ❌            | ❌                          | ❌                | ✅              |
| SGD + Momentum | ❌   | ✅            | ❌                          | ❌                | ✅              |
| NAG     | ❌           | ✅            | ❌                          | ❌                | ✅              |
| AdaGrad | ✅           | ❌            | ❌                          | ✅                | ❌              |
| RMSProp | ✅           | ❌            | ❌                          | ✅                | ✅              |
| Adam    | ✅           | ✅            | ❌                          | ✅                | ✅              |
| AdamW   | ✅           | ✅            | ✅                          | ✅                | ✅              |
| AMSGrad | ✅           | ✅            | ❌                          | ✅                | ✅              |
| Nadam   | ✅           | ✅            | ❌                          | ✅                | ✅              |
| LAMB    | ✅           | ✅            | ✅                          | ✅                | ✅              |

---

# 四、选择优化器的建议

| 场景 | 推荐优化器 |
|------|------------|
| 初学者入门 | **Adam / AdamW** |
| 图像分类任务 | **AdamW / SGD with Momentum** |
| NLP 任务 | **Adam / AdamW / LAMB** |
| 预训练大型模型（如 BERT、ViT） | **AdamW / LAMB** |
| 稀疏数据（如推荐系统） | **Adam / RMSProp / AdaGrad** |
| 理论研究 / 精细调参 | **SGD with Momentum / NAG** |
| 大 batch size 训练 | **LAMB** |

---

# 五、PyTorch 示例代码

```python
import torch
import torch.nn as nn
import torch.optim as optim

model = nn.Linear(10, 1)

# SGD
optimizer_sgd = optim.SGD(model.parameters(), lr=0.01)

# SGD + Momentum
optimizer_momentum = optim.SGD(model.parameters(), lr=0.01, momentum=0.9)

# Adam
optimizer_adam = optim.Adam(model.parameters(), lr=0.001)

# AdamW
optimizer_adamw = optim.AdamW(model.parameters(), lr=0.001, weight_decay=1e-2)

# RMSProp
optimizer_rmsprop = optim.RMSprop(model.parameters(), lr=0.01)

# LAMB（需安装第三方库，如 apex 或 torch-optim）
```

---

# 六、进阶阅读建议

- **《Deep Learning》by Ian Goodfellow et al.**：第 8 章专门讲优化方法
- **论文推荐**：
  - [Adam: A Method for Stochastic Optimization](https://arxiv.org/abs/1412.6980)
  - [Decoupled Weight Decay Regularization](https://arxiv.org/abs/1711.05101)
  - [Large Batch Optimization for Deep Learning: Training BERT in 76 minutes](https://arxiv.org/abs/1904.00962)
