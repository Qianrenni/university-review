
# 一、自编码器（Autoencoder）

## 1. 基本概念

**自编码器（Autoencoder）** 是一种无监督神经网络模型，其目标是通过学习一个低维表示（编码），然后尽可能还原原始输入数据（解码）。它的基本思想是：让神经网络学会一个“压缩-还原”的过程。

## 2. 结构组成

自编码器通常由两部分组成：

- **编码器（Encoder）**：将输入数据 $ x \in \mathbb{R}^n $ 映射为潜在空间的表示 $ z \in \mathbb{R}^k $（$ k < n $）
- **解码器（Decoder）**：将潜在表示 $ z $ 映射回重构数据 $ \hat{x} \in \mathbb{R}^n $

整个流程可以表示为：
$$
z = f(x), \quad \hat{x} = g(z)
$$

其中 $ f $ 和 $ g $ 通常是多层神经网络。

## 3. 损失函数

自编码器的目标是最小化输入与输出之间的差异，通常使用均方误差（MSE）或交叉熵损失：

- **MSE Loss（适用于连续值）**：
  $$
  L(x, \hat{x}) = \|x - \hat{x}\|^2
  $$

- **Binary Cross Entropy Loss（适用于0/1图像）**：
  $$
  L(x, \hat{x}) = -\sum_i x_i \log(\hat{x}_i) + (1 - x_i)\log(1 - \hat{x}_i)
  $$

## 4. 特点

- **无监督学习**：不需要标签数据
- **降维工具**：可用于特征提取和可视化
- **去噪能力**：通过加入噪声再重建，可实现去噪自编码器（Denoising AE）
- **生成能力有限**：由于只是重建输入，不能很好地生成新样本

## 5. 应用场景

- 数据降维（如PCA的非线性扩展）
- 特征提取
- 图像去噪
- 异常检测（重构误差大可能为异常）
- 预训练网络参数

---

# 二、变分自编码器（Variational Autoencoder）

## 1. 背景动机

虽然传统自编码器能有效压缩数据并重构，但它学到的潜在空间往往是不规则的，难以用于生成新的样本。**变分自编码器（VAE）** 通过引入概率建模的思想，使得潜在空间具有良好的结构性和连续性，从而支持更有效的生成任务。

## 2. 核心思想

VAE 不直接学习一个确定性的潜在变量 $ z $，而是学习一个**概率分布**，即给定输入 $ x $ 后，编码器输出的是潜在变量的分布参数（通常是均值 $ \mu $ 和标准差 $ \sigma $），然后从这个分布中采样出 $ z $。

换句话说，VAE 的核心思想是：

> 把编码过程变成一个随机过程，并在训练时优化一个下界（ELBO）来逼近真实后验分布。

## 3. 模型结构

- 编码器输出两个向量：$ \mu_z $ 和 $ \sigma_z $
- 然后通过重参数技巧（reparameterization trick）采样：
  $$
  z = \mu_z + \sigma_z \cdot \epsilon, \quad \text{其中 } \epsilon \sim \mathcal{N}(0, I)
  $$
- 解码器根据 $ z $ 重构输入 $ \hat{x} $

## 4. 概率图模型视角

VAE 假设数据生成过程如下：

- 先从先验分布 $ p(z) $ 中采样 $ z $
- 再根据条件分布 $ p_\theta(x|z) $ 生成数据 $ x $

我们的目标是最大化边缘似然 $ p_\theta(x) $，但该积分不可解。于是我们引入变分分布 $ q_\phi(z|x) $ 来近似真实后验 $ p(z|x) $。

## 5. 损失函数：ELBO（Evidence Lower Bound）

VAE 的训练目标是最大化 ELBO：

$$
\log p_\theta(x) \geq \mathbb{E}_{q_\phi(z|x)}[\log p_\theta(x|z)] - D_{KL}(q_\phi(z|x) \| p(z))
$$

所以 VAE 的损失函数包含两个部分：

- **重构损失（Reconstruction Loss）**：衡量解码器能否正确重构输入
- **KL 散度项（正则化项）**：使编码器输出的分布接近标准正态分布

最终损失形式如下：

$$
\mathcal{L}_{VAE} = \underbrace{\mathbb{E}_{q_\phi(z|x)}[\log p_\theta(x|z)]}_{\text{Reconstruction}} - \underbrace{D_{KL}(q_\phi(z|x) \| p(z))}_{\text{Regularization}}
$$

在实现中，通常写作负号形式：

$$
\mathcal{L}_{VAE} = -\log p_\theta(x|z) + D_{KL}
$$

## 6. 重参数技巧（Reparameterization Trick）

为了使梯度能够通过采样过程传递到编码器参数上，VAE 使用了重参数技巧：

$$
z = \mu_z + \sigma_z \odot \epsilon, \quad \epsilon \sim \mathcal{N}(0, I)
$$

这样，采样操作变成了可微分的操作，允许反向传播。

## 7. 特点

- 潜在空间具有良好结构（近似高斯分布），便于插值、采样和生成
- 支持生成高质量的新样本
- 可以控制生成结果（例如改变某个维度的潜在变量）
- 训练更复杂，需要平衡重构误差和 KL 正则项

## 8. 应用场景

- 图像生成（如人脸、手写数字等）
- 数据增强
- 语音合成
- 图像风格迁移
- 潜在空间插值分析
- 异常检测（结合生成能力）

---

# 三、对比总结：AE vs VAE

| 特性 | 自编码器（AE） | 变分自编码器（VAE） |
|------|----------------|------------------------|
| 学习目标 | 最小化重构误差 | 最大化 ELBO 下界 |
| 潜在空间 | 确定性映射 | 概率分布映射 |
| 生成能力 | 差（仅能重建输入） | 强（可从先验分布采样生成新样本） |
| 插值能力 | 差 | 好 |
| 损失函数 | 重构损失 | 重构损失 + KL 散度 |
| 是否可微采样 | 是（无需特殊处理） | 否，需重参数技巧 |
| 潜在变量分布 | 任意 | 接近标准正态分布 |

---

# 四、代码示例（PyTorch 实现）

## 1. 自编码器（AE）

```python
import torch
import torch.nn as nn

class Autoencoder(nn.Module):
    def __init__(self, latent_dim=2):
        super().__init__()
        self.encoder = nn.Sequential(
            nn.Linear(784, 256),
            nn.ReLU(),
            nn.Linear(256, latent_dim)
        )
        self.decoder = nn.Sequential(
            nn.Linear(latent_dim, 256),
            nn.ReLU(),
            nn.Linear(256, 784),
            nn.Sigmoid()
        )

    def forward(self, x):
        z = self.encoder(x)
        return self.decoder(z)
```

## 2. 变分自编码器（VAE）

```python
class VAE(nn.Module):
    def __init__(self, latent_dim=2):
        super().__init__()
        # Encoder
        self.fc1 = nn.Linear(784, 256)
        self.mu = nn.Linear(256, latent_dim)
        self.logvar = nn.Linear(256, latent_dim)

        # Decoder
        self.decoder = nn.Sequential(
            nn.Linear(latent_dim, 256),
            nn.ReLU(),
            nn.Linear(256, 784),
            nn.Sigmoid()
        )

    def reparameterize(self, mu, logvar):
        std = torch.exp(0.5 * logvar)
        eps = torch.randn_like(std)
        return mu + eps * std

    def forward(self, x):
        h = torch.relu(self.fc1(x))
        mu, logvar = self.mu(h), self.logvar(h)
        z = self.reparameterize(mu, logvar)
        return self.decoder(z), mu, logvar

# Loss function
def vae_loss(recon_x, x, mu, logvar):
    BCE = nn.functional.binary_cross_entropy(recon_x, x, reduction='sum')
    KLD = -0.5 * torch.sum(1 + logvar - mu.pow(2) - logvar.exp())
    return BCE + KLD
```

---

# 五、扩展与进阶

- **β-VAE**：调整 KL 项权重，控制潜在变量的学习强度
- **Conditional VAE（CVAE）**：加入类别标签作为额外输入，实现可控生成
- **Wasserstein Autoencoder（WAE）**：用 W 距离替代 KL 散度，提升生成质量
- **Deep Convolutional VAE（DCVAE）**：使用卷积网络处理图像数据
- **Flow-based VAEs**：结合流模型，获得更灵活的潜在分布
- **Discrete VAE**：处理离散潜在变量

---

# 六、总结

| 模型 | 潜在变量类型 | 是否可生成 | 是否支持插值 | 是否使用KL |
|------|---------------|-------------|----------------|--------------|
| AE   | 确定性         | 否           | 否              | 否            |
| VAE  | 概率分布       | 是           | 是              | 是            |

自编码器适合做特征提取和数据压缩，而变分自编码器则更适合生成任务和潜在空间建模。两者各有优劣，在不同任务中有不同的应用价值。