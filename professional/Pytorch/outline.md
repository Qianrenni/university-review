如果你想要一份 **PyTorch 完整学习大全**，从入门到进阶、理论与实战结合的学习路线和资源汇总，下面是一个系统化的学习指南，适合初学者和进阶者使用。

---

# 🧠 PyTorch 完整学习大全（2025 最新版）

---

## ✅ 一、基础篇

### 1. PyTorch 简介
- 是 Facebook 开发的开源深度学习框架
- 动态计算图（Dynamic Computation Graph）
- 支持 GPU 加速、自动求导、张量运算等
- 与 NumPy 接口类似，易于上手

### 2. 安装 PyTorch
```bash
pip install torch torchvision torchaudio
```
> 官网安装推荐：https://pytorch.org/get-started/locally/

---

## 📚 二、核心知识体系

---

### 1. 张量（Tensor）操作

| 操作 | 示例 |
|------|------|
| 创建 Tensor | `torch.tensor([1,2,3])` |
| 零矩阵 | `torch.zeros(3,4)` |
| 随机数 | `torch.rand(3,4)` |
| 类型转换 | `x.float()`, `x.long()` |
| 索引切片 | `x[:, 1]` |
| reshape | `x.view(-1, 4)` 或 `x.reshape(-1, 4)` |
| GPU支持 | `x.to('cuda')` |

---

### 2. 自动微分（Autograd）

```python
x = torch.randn(3, 4, requires_grad=True)
y = x * 2
z = y.sum()
z.backward()
print(x.grad)
```

---

### 3. 构建神经网络（nn.Module）

```python
import torch.nn as nn

class Net(nn.Module):
    def __init__(self):
        super().__init__()
        self.fc1 = nn.Linear(784, 256)
        self.relu = nn.ReLU()
        self.fc2 = nn.Linear(256, 10)

    def forward(self, x):
        return self.fc2(self.relu(self.fc1(x)))
```

---

### 4. 损失函数（Loss）

| 函数 | 场景 |
|------|------|
| `nn.MSELoss()` | 回归任务 |
| `nn.CrossEntropyLoss()` | 分类任务 |
| `nn.BCEWithLogitsLoss()` | 二分类 |
| `nn.L1Loss()` | L1 损失 |
| `nn.NLLLoss()` | 负对数似然损失 |

---

### 5. 优化器（Optimizer）

```python
import torch.optim as optim

model = Net()
optimizer = optim.Adam(model.parameters(), lr=0.001)
loss = loss_fn(output, target)
loss.backward()
optimizer.step()
optimizer.zero_grad()
```

常用优化器：
- `Adam`
- `SGD`
- `RMSprop`
- `AdamW`

---

### 6. 数据加载（Dataset & DataLoader）

```python
from torch.utils.data import Dataset, DataLoader

class MyDataset(Dataset):
    def __len__(self): ...
    def __getitem__(self, idx): ...

loader = DataLoader(dataset, batch_size=32, shuffle=True)
```

---

### 7. 图像处理工具（torchvision）

- `torchvision.models`: 提供预训练模型（ResNet、VGG 等）
- `torchvision.transforms`: 图像增强
- `torchvision.datasets`: 内置数据集（CIFAR10、MNIST 等）

```python
transform = transforms.Compose([
    transforms.ToTensor(),
    transforms.Normalize((0.5,), (0.5,))
])
dataset = datasets.CIFAR10(root='./data', train=True, transform=transform, download=True)
```

---

## 🚀 三、进阶篇

---

### 1. 自定义层和模型

```python
class CustomLinear(nn.Module):
    def __init__(self, in_dim, out_dim):
        super().__init__()
        self.weight = nn.Parameter(torch.randn(out_dim, in_dim))
        self.bias = nn.Parameter(torch.randn(out_dim))

    def forward(self, x):
        return x @ self.weight.t() + self.bias
```

---

### 2. 权重初始化

```python
def init_weights(m):
    if isinstance(m, nn.Linear):
        torch.nn.init.xavier_uniform_(m.weight)
        m.bias.data.fill_(0.01)

model.apply(init_weights)
```

---

### 3. 模型保存与加载

```python
# 保存
torch.save(model.state_dict(), 'model.pth')

# 加载
model = Net()
model.load_state_dict(torch.load('model.pth'))
model.eval()
```

---

### 4. 使用 GPU（CUDA）

```python
device = 'cuda' if torch.cuda.is_available() else 'cpu'
model.to(device)
x = x.to(device)
```

---

### 5. 可视化（如 TensorBoard）

```bash
pip install tensorboard
```

```python
from torch.utils.tensorboard import SummaryWriter
writer = SummaryWriter()
writer.add_scalar("Loss/train", loss.item(), epoch)
```

---

### 6. 学习率调度器（Learning Rate Scheduler）

```python
scheduler = optim.lr_scheduler.StepLR(optimizer, step_size=30, gamma=0.1)
for epoch in range(100):
    train(...)
    scheduler.step()
```

---

### 7. 多 GPU 训练（DataParallel）

```python
if torch.cuda.device_count() > 1:
    model = nn.DataParallel(model)
```

---

### 8. TorchScript 和 ONNX 导出

```python
script_model = torch.jit.script(model)
torch.jit.save(script_model, "script_model.pt")

# 导出为 ONNX
dummy_input = torch.randn(1, 3, 224, 224)
torch.onnx.export(model, dummy_input, "model.onnx")
```

---

## 🧪 四、实战项目推荐

| 项目 | 技术点 |
|------|--------|
| 手写数字识别（MNIST） | CNN、交叉熵损失、准确率评估 |
| 图像分类（CIFAR10） | ResNet、数据增强、学习率调度 |
| 图像生成（DCGAN） | 反卷积、生成对抗网络 |
| 图像分割（U-Net） | 编码器-解码器结构、Dice Loss |
| 目标检测（YOLO/Faster R-CNN） | 边界框回归、IoU、非极大抑制 |
| NLP 文本分类 | Embedding、LSTM、Attention |
| 时间序列预测 | LSTM、Transformer |
| 强化学习 | DQN、PPO、Gym 环境交互 |

---

## 📘 五、学习资源推荐

### 📚 官方文档
- [PyTorch 官网](https://pytorch.org/)
- [PyTorch 中文社区](https://pytorch-cn.readthedocs.io/)
- [PyTorch 教程官方文档](https://pytorch.org/tutorials/)

### 📺 视频教程
- B站：【PyTorch深度学习快速入门教程（绝对通俗易懂！）】
- YouTube: PyTorch for Deep Learning and Computer Vision by Python Engineer

### 📖 书籍推荐
- 《深度学习入门之PyTorch》
- 《PyTorch深度学习实战》
- 《动手学深度学习》（李沐）配套 PyTorch 实现版本

### 💻 在线平台
- Kaggle（实战练习）
- Google Colab（免费 GPU）
- Papers with Code（论文+代码）
- HuggingFace（模型库）

---

## 🧩 六、进阶方向

| 方向 | 技术栈 |
|------|--------|
| CV | CNN、Transformer、Diffusion Model |
| NLP | Transformer、BERT、GPT、Tokenizers |
| GAN | DCGAN、CycleGAN、StyleGAN |
| RL | DQN、PPO、SAC、RLlib |
| AutoML | NAS、AutoEncoder、Meta Learning |
| 多模态 | CLIP、BLIP、Flamingo |

---

## 🧪 七、建议学习路径（按周计划）

| 周次 | 内容 |
|------|------|
| 第1周 | 张量操作、自动微分、基本网络搭建 |
| 第2周 | 数据加载、图像分类实战（CIFAR10） |
| 第3周 | 卷积神经网络、反卷积、图像生成（GAN） |
| 第4周 | 迁移学习、目标检测、图像分割 |
| 第5周 | NLP 基础、词嵌入、文本分类 |
| 第6周 | Transformer、BERT、机器翻译 |
| 第7周 | 强化学习、多模态、部署优化 |
| 第8周 | 综合项目实战（自选方向） |

---
