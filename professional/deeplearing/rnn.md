
# 一、什么是 RNN？

**循环神经网络（RNN）** 是一种专门处理**序列数据**的神经网络结构。与传统前馈网络不同，RNN 具有“记忆”能力，能利用先前输入的信息来影响当前输出。

## 🔍 为什么需要 RNN？

在处理以下类型任务时，传统神经网络无法有效建模：

- 文本生成 / 翻译
- 语音识别
- 时间序列预测
- 视频分析（帧序列）
- 音乐生成

这些任务中，**数据具有时间或顺序依赖性**，而 RNN 正是为解决这类问题而设计。

---

# 二、RNN 的核心思想

## 1. 结构示意

```
Input: x₁ → x₂ → x₃ → ... → xₜ  
          ↓    ↓    ↓         ↓  
Hidden: h₁ → h₂ → h₃ → ... → hₜ  
          ↓    ↓    ↓         ↓  
Output: y₁   y₂   y₃       yₜ
```

每个时间步 $t$，RNN 接收输入 $x_t$ 和上一时刻的状态 $h_{t-1}$，计算当前状态 $h_t$ 并输出 $y_t$。

---

# 三、RNN 的数学表示

一个标准 RNN 的计算过程如下：

$$
h_t = \tanh(W_{hh} h_{t-1} + W_{xh} x_t + b_h)
$$
$$
y_t = W_{hy} h_t + b_y
$$

其中：

- $x_t$：当前时刻输入
- $h_t$：当前时刻隐藏状态（即记忆）
- $W_{xh}, W_{hh}, W_{hy}$：权重矩阵
- $\tanh$：激活函数（也可使用 ReLU）

---

# 四、RNN 的优点与局限性

## ✅ 优点

- 能够建模**序列数据之间的依赖关系**
- 可以处理变长输入（如一句话长度不固定）
- 参数共享机制（不同时间步共享相同参数）

## ❌ 局限性

- **梯度消失 / 梯度爆炸**：难以学习长期依赖关系
- 训练速度慢
- 易过拟合

---

# 五、RNN 的核心问题：梯度消失与爆炸

## 1. 梯度消失（Vanishing Gradient）

- 在反向传播过程中，梯度逐渐趋近于 0
- 导致早期时间步的参数几乎无法更新
- 原因：$\tanh$ 或 Sigmoid 函数导数小于 1，多次链式乘法后趋于 0

## 2. 梯度爆炸（Exploding Gradient）

- 梯度指数级增长，导致参数剧烈震荡
- 解决方法：梯度裁剪（Gradient Clipping）

```python
torch.nn.utils.clip_grad_norm_(model.parameters(), clip_val)
```

---

# 六、改进型 RNN：LSTM 与 GRU

为了解决 RNN 的梯度问题，研究人员提出了两种经典改进模型：

## 1. LSTM（Long Short-Term Memory）

## 核心思想

引入**门控机制**控制信息流：

- **输入门**（Input Gate）：决定哪些新信息进入细胞状态
- **遗忘门**（Forget Gate）：决定哪些旧信息被丢弃
- **输出门**（Output Gate）：决定哪些信息作为输出

## 数学公式（简化）

$$
f_t = \sigma(W_f [h_{t-1}, x_t] + b_f) \\
i_t = \sigma(W_i [h_{t-1}, x_t] + b_i) \\
\tilde{C}_t = \tanh(W_C [h_{t-1}, x_t] + b_C) \\
C_t = f_t \odot C_{t-1} + i_t \odot \tilde{C}_t \\
o_t = \sigma(W_o [h_{t-1}, x_t] + b_o) \\
h_t = o_t \odot \tanh(C_t)
$$

> $\sigma$：Sigmoid 函数，$\odot$：逐元素相乘

---

## 2. GRU（Gated Recurrent Unit）

- LSTM 的简化版本
- 合并了遗忘门和输入门为一个“更新门”
- 更少参数，训练更快

## GRU 公式（简化）

$$
z_t = \sigma(W_z [h_{t-1}, x_t]) \quad \text{（更新门）} \\
r_t = \sigma(W_r [h_{t-1}, x_t]) \quad \text{（重置门）} \\
\tilde{h}_t = \tanh(r_t \cdot h_{t-1} + W x_t) \\
h_t = (1 - z_t) \cdot h_{t-1} + z_t \cdot \tilde{h}_t
$$

---

# 七、PyTorch 中的 RNN 实现

## 1. 使用内置模块

```python
import torch
import torch.nn as nn

# 定义一个简单的 RNN 模型
class SimpleRNN(nn.Module):
    def __init__(self, input_size=10, hidden_size=20, num_layers=1, output_size=1):
        super(SimpleRNN, self).__init__()
        self.rnn = nn.RNN(input_size, hidden_size, num_layers, batch_first=True)
        self.fc = nn.Linear(hidden_size, output_size)

    def forward(self, x):
        out, hidden = self.rnn(x)
        out = self.fc(out)
        return out, hidden
```

## 2. 使用 LSTM 或 GRU 替换

```python
self.rnn = nn.LSTM(input_size, hidden_size, num_layers, batch_first=True)
# 或
self.rnn = nn.GRU(input_size, hidden_size, num_layers, batch_first=True)
```

---

# 八、RNN 的应用场景

| 应用领域 | 示例 |
|----------|------|
| 自然语言处理（NLP） | 文本分类、机器翻译、文本摘要 |
| 语音识别 | 将语音信号转为文本 |
| 时间序列预测 | 股票价格预测、天气预测 |
| 视频处理 | 视频动作识别、视频字幕生成 |
| 音乐生成 | 利用 RNN 生成旋律 |
| 强化学习 | 处理部分可观测环境中的决策问题 |

---

# 九、实战项目推荐

## 1. 文本分类（IMDB 电影评论情感分析）

```python
from torchtext.datasets import IMDB
from torchtext.data.utils import get_tokenizer
from torchtext.vocab import build_vocab_from_iterator

tokenizer = get_tokenizer('basic_english')
train_iter = IMDB(split='train')

def yield_tokens(data_iter):
    for _, text in data_iter:
        yield tokenizer(text)

vocab = build_vocab_from_iterator(yield_tokens(train_iter), specials=["<unk>"])
```

## 2. 时间序列预测（股票价格预测）

```python
import pandas as pd
import numpy as np
from sklearn.preprocessing import MinMaxScaler

df = pd.read_csv("stock.csv")
scaler = MinMaxScaler()
data = scaler.fit_transform(df['Close'].values.reshape(-1,1))

# 构造序列数据
def create_dataset(data, seq_length):
    X, Y = [], []
    for i in range(len(data)-seq_length):
        X.append(data[i:i+seq_length])
        Y.append(data[i+seq_length])
    return np.array(X), np.array(Y)
```

---

# 十、训练技巧与调参建议

| 技巧 | 描述 |
|------|------|
| 批归一化（BatchNorm） | 提升训练稳定性 |
| Dropout | 防止过拟合 |
| 学习率调度器 | 动态调整学习率 |
| 权重初始化 | 使用 Xavier 或 He 初始化提高效果 |
| 梯度裁剪 | 防止梯度爆炸 |
| 双向 RNN（Bidirectional RNN） | 利用前后文信息 |
| 多层堆叠 RNN | 增强模型表达能力 |

---

# 十一、RNN 的局限与替代方案

尽管 RNN 及其变体非常强大，但在现代深度学习中也存在一些更优的替代方案：

| 替代方案 | 优势 |
|----------|------|
| Transformer | 更擅长建模长距离依赖，支持并行训练 |
| CNN（用于序列） | 如 WaveNet、TCN，可提取局部模式 |
| Attention 机制 | 增强对关键信息的关注 |
| State Space Models（SSM） | 新兴架构，适用于超长序列建模 |

---

# 十二、总结：RNN 的关键点

| 组件 | 作用 |
|------|------|
| 输入层 | 接收序列输入 |
| 隐藏层 | 存储历史状态 |
| 输出层 | 输出预测结果 |
| 激活函数 | 引入非线性 |
| 损失函数 | 衡量误差 |
| 优化器 | 更新参数 |
| 反向传播 | 计算梯度 |
| LSTM/GRU | 改进长期记忆能力 |

---

# 十三、拓展学习资源推荐

| 类型 | 地址 |
|------|------|
| 官方文档（PyTorch） | <https://pytorch.org/docs/stable/generated/torch.nn.RNN.html> |
| 中文教程 | <https://zhuanlan.zhihu.com/p/438759613> |
| 视频课程 | 吴恩达《深度学习专项课程》第5课、李宏毅《机器学习》 |
| GitHub 示例 | 搜索关键词 `RNN tutorial pytorch` |
