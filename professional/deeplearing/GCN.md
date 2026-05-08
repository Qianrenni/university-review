
# 一、什么是分组卷积？

**分组卷积（Grouped Convolution）** 是一种将输入通道划分成多个“组”，并在每个组内独立进行卷积操作的技术。

它最早在 AlexNet 中被提出，用于在两个 GPU 上并行训练模型。后来随着 ResNeXt、ShuffleNet、MobileNet 等轻量级网络的发展，分组卷积成为提升模型效率的重要手段。

---

# 二、为什么需要分组卷积？

## ✅ 核心优势

1. **减少参数数量与计算量**
2. **控制模型复杂度**
3. **增强特征多样性**
4. **加速推理速度**

## 📈 对比传统卷积

| 卷积类型 | 输入通道数 | 输出通道数 | 卷积核大小 | 参数量 |
|----------|-------------|--------------|----------------|--------|
| 普通卷积 | C_in        | C_out        | K×K           | K² × C_in × C_out |
| 分组卷积（G 组） | C_in        | C_out        | K×K（每组）    | K² × (C_in/G) × (C_out/G) × G = K² × C_in × C_out / G |

可以看到，当 G 增大时，参数量和计算量显著减少。

---

# 三、分组卷积的工作原理

## 🔁 数学表示

设输入张量为 $ X \in \mathbb{R}^{N \times C_{in} \times H \times W} $

将输入通道划分为 $ G $ 组：

$$
X = [X_1, X_2, ..., X_G], \quad X_g \in \mathbb{R}^{N \times C_{in}/G \times H \times W}
$$

对每组使用一组独立的卷积核进行卷积：

$$
Y_g = \text{Conv}(X_g), \quad Y_g \in \mathbb{R}^{N \times C_{out}/G \times H \times W}
$$

最后拼接所有输出组得到最终输出：

$$
Y = [Y_1, Y_2, ..., Y_G] \in \mathbb{R}^{N \times C_{out} \times H \times W}
$$

---

# 四、常见的分组卷积变体

## 1. AlexNet 中的原始分组卷积（2组）

- 将卷积层拆分到两个 GPU 并行计算
- 减少内存占用，加快训练速度
- 但限制了跨组的信息交互

---

## 2. ResNeXt 中的“Cardinality”思想

- 引入“基数（Cardinality）”概念：即并行的卷积分支数量
- 每个分支使用相同的拓扑结构（如 bottleneck）
- 最后通过通道拼接融合各分支信息

## 示例结构（ResNeXt Bottleneck Block）

```
Input → 1x1 Conv → BN → ReLU
       ↓
      Grouped 3x3 Conv → BN → ReLU
       ↓
     1x1 Conv → BN → + Shortcut → Output
```

> 其中中间的 `3x3` 卷积是分组卷积，例如设置为 32 组（Card=32）

---

## 3. MobileNetV1 中的深度可分离卷积（Depthwise Separable Convolution）

- 可以看作是一种极端的分组卷积（每组一个通道）
- 包含两步：
  - **深度卷积（Depthwise Conv）**：每个通道单独卷积（group=C_in）
  - **逐点卷积（Pointwise Conv）**：1×1 卷积整合通道信息

## 优点

- 极大减少参数量和计算量
- 非常适合移动端部署

---

## 4. ShuffleNet 中的通道混洗（Channel Shuffle）

- 在分组卷积之后加入通道混洗操作，促进跨组信息交流
- 解决了纯分组卷积导致的信息隔离问题

---

# 五、PyTorch 中实现分组卷积

在 PyTorch 中，只需在 `nn.Conv2d` 中指定 `groups=G` 即可启用分组卷积。

```python
import torch
import torch.nn as nn

# 普通卷积
conv_normal = nn.Conv2d(in_channels=64, out_channels=128, kernel_size=3, padding=1)

# 分组卷积（groups=2）
conv_grouped = nn.Conv2d(
    in_channels=64,
    out_channels=128,
    kernel_size=3,
    padding=1,
    groups=2  # 必须保证 in_channels 和 out_channels 能被 groups 整除
)

# 测试输入
x = torch.randn(1, 64, 32, 32)
y_normal = conv_normal(x)
y_grouped = conv_grouped(x)

print(y_normal.shape)   # (1, 128, 32, 32)
print(y_grouped.shape)  # (1, 128, 32, 32)
```

---

# 六、分组卷积的实际应用场景

| 应用领域 | 模型示例 | 使用方式 |
|----------|-----------|-----------|
| 图像分类 | ResNeXt、MobileNet、ShuffleNet | 替代标准卷积，降低计算成本 |
| 移动端部署 | MobileNet、EfficientNet-Lite | 极致压缩模型大小 |
| 视频识别 | TSception、TimeSformer | 分组处理时空维度 |
| 工业质检 | TinyML、Edge AI | 在资源受限设备上运行深度模型 |
| 自动驾驶 | EfficientDet、YOLOv5 Lite | 提高实时性与能效比 |

---

# 七、进阶技巧与调参建议

| 技巧 | 描述 |
|------|------|
| 合理选择组数（groups） | 通常为 2、4、8 或通道数的因数 |
| 结合通道混洗（Channel Shuffle） | 如 ShuffleNet 所做，避免信息隔离 |
| 控制参数总量 | 分组越大，参数越少，但可能损失精度 |
| 搭配 SE 模块或注意力机制 | 提升轻量化模型的表现力 |
| 使用深度可分离卷积替代普通卷积 | 如 MobileNet、Xception 所用 |
| 模型剪枝 + 分组卷积 | 进一步压缩模型体积 |

---

# 八、总结：分组卷积的关键点

| 项目 | 内容 |
|------|------|
| 定义 | 将输入通道划分为多个组，每组独立进行卷积 |
| 目的 | 减少参数、降低计算量、提高模型效率 |
| 支持框架 | PyTorch、TensorFlow、ONNX 等 |
| 应用场景 | 图像分类、目标检测、移动端部署等 |
| 常见变体 | ResNeXt、MobileNet、ShuffleNet |
| 注意事项 | in/out channels 必须能被 group 整除 |
| 性能权衡 | 组数越大越轻量，但可能影响精度 |

---

# 九、拓展资源推荐

| 类型 | 地址 |
|------|------|
| 官方论文（AlexNet） | <https://papers.nips.cc/paper_files/paper/2012/file/cdbba9af734e7ea3eee53e23dc3f5ce3-Paper.pdf> |
| ResNeXt 论文 | <https://arxiv.org/abs/1611.05431> |
| MobileNet 论文 | <https://arxiv.org/abs/1704.04861> |
| ShuffleNet 论文 | <https://arxiv.org/abs/1807.11164> |
| PyTorch 官方文档 | <https://pytorch.org/docs/stable/generated/torch.nn.Conv2d.html> |
| GitHub 示例 | 搜索关键词 `grouped convolution pytorch tutorial` |
