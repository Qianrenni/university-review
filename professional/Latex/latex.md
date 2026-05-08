
# ✅ 一、LaTeX 数学公式的两种形式

## 1. 行内公式（Inline Math）

用于将公式嵌入文字中。

**语法：**

```markdown
这是一个行内公式：$ E = mc^2 $
```

**效果：**  
这是一个行内公式：$ E = mc^2 $

---

## 2. 块级公式 / 显示公式（Display Math）

独占一行的公式，居中显示。

**语法：**

```markdown
这是一个块级公式：
$$
E = mc^2
$$
```

**效果：**  
这是一个块级公式：
$$
E = mc^2
$$

---

# ✅ 二、常用 LaTeX 公式语法示例

| 类型 | LaTeX 语法 | 效果 | 说明 |
|------|------------|------|------|
| 指数 | `$x^2$` | $x^2$ | 支持多字符上标：`x^{10}` |
| 下标 | `$x_1$` | $x_1$ | 同样支持多字符下标：`x_{ij}` |
| 分式 | `$\frac{a}{b}$` | $\frac{a}{b}$ | 可嵌套使用 |
| 根号 | `$\sqrt{x+y}$` | $\sqrt{x+y}$ | 平方根 |
| n次根号 | `$\sqrt[n]{x}$` | $\sqrt[n]{x}$ | n 次根号 |
| 求和符号 | `$\sum_{i=1}^n i$` | $\sum_{i=1}^n i$ | 上下标在行内与显示公式中不同 |
| 积分符号 | `$\int_a^b f(x) dx$` | $\int_a^b f(x) dx$ | 支持多重积分 `\iint`, `\iiint` |
| 极限 | `$\lim_{x \to 0} f(x)$` | $\lim_{x \to 0} f(x)$ | 常用于极限表达 |
| 绝对值 | `$|x|$` 或 `\vert x \vert` | $|x|$ 或 $\vert x \vert$ | 推荐用 `\left| ... \right|` 自动调整大小 |
| 大括号 | `$\left( \frac{a}{b} \right)$` | $\left( \frac{a}{b} \right)$ | 自适应大小括号 |
| 花体字母 | `$\mathcal{ABC}$` | $\mathcal{ABC}$ | 常用于集合或变换 |
| 黑板粗体 | `$\mathbb{R}, \mathbb{Z}$` | $\mathbb{R}, \mathbb{Z}$ | 表示数集（需导入 `amsfonts`） |
| 粗体字母 | `$\mathbf{v}$` | $\mathbf{v}$ | 用于向量、矩阵 |
| 斜体取消 | `$\mathrm{d}x$` | $\mathrm{d}x$ | 微分符号推荐写法 |
| 对数函数 | `$\log_2 x$` | $\log_2 x$ | 可以换成 `\ln x` |
| 三角函数 | `$\sin x, \cos x, \tan x$` | $\sin x, \cos x, \tan x$ | 使用内置函数名保持正体 |
| 集合关系 | `$\in, \notin, \subset, \subseteq, \cup, \cap$` | $\in, \notin, \subset, \subseteq, \cup, \cap$ | 集合操作符 |
| 逻辑符号 | `$\forall, \exists, \Rightarrow, \Leftrightarrow, \neg$` | $\forall, \exists, \Rightarrow, \Leftrightarrow, \neg$ | 常见逻辑符号 |
| 矩阵 | `\begin{bmatrix} a & b \\ c & d \end{bmatrix}` | $\begin{bmatrix} a & b \\ c & d \end{bmatrix}$ | 使用 `bmatrix` 表示带方括号的矩阵 |
| 分段函数 |

```latex
f(x) = 
\begin{cases}
x^2, & x < 0 \\
x+1, & x \geq 0
\end{cases}
```

| $f(x) =
\begin{cases}
x^2, & x < 0 \\
x+1, & x \geq 0
\end{cases}$ | 使用 `cases` 环境表示分段函数 |
| 箭头 | `$\rightarrow, \leftarrow, \Rightarrow, \Leftarrow$` | $\rightarrow, \leftarrow, \Rightarrow, \Leftarrow$ | 常用于映射、推导 |
| 导数 | `$f'(x), f''(x), \dot{x}, \ddot{x}$` | $f'(x), f''(x), \dot{x}, \ddot{x}$ | 点导数常用于物理 |
| 转义空格 | `$a\ b$` | $a\ b$ | 插入手动空格 |
| 加粗数学符号 | `$\boldsymbol{\alpha}, \boldsymbol{A}$` | $\boldsymbol{\alpha}, \boldsymbol{A}$ | 需要 `\usepackage{amsmath}` |

---

# ✅ 三、矩阵等复杂公式示例

## 示例 1：矩阵

```latex
$$
A = \begin{bmatrix}
    a_{11} & a_{12} \\
    a_{21} & a_{22}
\end{bmatrix}
$$
```

效果：
$$
A = \begin{bmatrix}
    a_{11} & a_{12} \\
    a_{21} & a_{22}
\end{bmatrix}
$$

---

## 示例 2：多行公式（用 `aligned`）

```latex
$$
\begin{aligned}
    f(x) &= x^2 + 2x + 1 \\
         &= (x + 1)^2
\end{aligned}
$$
```

效果：
$$
\begin{aligned}
    f(x) &= x^2 + 2x + 1 \\
         &= (x + 1)^2
\end{aligned}
$$

---

# ✅ 四、注意事项

- Markdown 中默认不支持 LaTeX，需要使用支持公式的解析器或编辑器，如：
  - VSCode 插件（Markdown Preview Enhanced）
  - Typora
  - Jupyter Notebook
  - Obsidian（需开启设置）
  - 在网页端发布时，可使用 MathJax 或 KaTeX 渲染
- 如果你在 GitHub 上写 Markdown，默认是**不支持 LaTeX 公式的**。
- 推荐工具：
  - [Overleaf](https://overleaf.com)（在线 LaTeX 编辑器）
  - [LaTeX 公式可视化编辑器](https://www.codecogs.com/latex/eqneditor.php)

---
