```python
import  torch
```


```python
# 判断是否为张量
print(f'{torch.is_tensor.__name__}')
print(f"[1,2,3] is tensor? {torch.is_tensor([1,2,3])}")
print()
# 判断是否是storage
print(f'{torch.is_storage.__name__}')
print(f"[1,2,3] is storage? {torch.is_storage([1,2,3])}")
print()
# 输出张量元素个数
print(f'{torch.numel.__name__}')
print(f'{torch.tensor([1,2,3])} has {torch.numel(torch.tensor([1,2,3]))} elements')
print(f'torch.randn(1,2,3,4,5) has {torch.numel(torch.randn(1,2,3,4,5))} elements')
```

    is_tensor
    [1,2,3] is tensor? False
    
    is_storage
    [1,2,3] is storage? False
    
    numel
    tensor([1, 2, 3]) has 3 elements
    torch.randn(1,2,3,4,5) has 120 elements
    


```python
# 创建张量
print(f'{torch.tensor.__name__}')
print(f'{torch.tensor([1,2,3])}')
```

    tensor
    tensor([1, 2, 3])
    


```python
print(f'{torch.diag.__name__} 创建对角矩阵')
print(f'{torch.diag(torch.tensor([1,2,3]))}')
```

    diag 创建对角矩阵
    tensor([[1, 0, 0],
            [0, 2, 0],
            [0, 0, 3]])
    


```python
# torch.eye
print(f'{torch.eye.__name__}')
print(f'{torch.eye(3)}')
```

    eye
    tensor([[1., 0., 0.],
            [0., 1., 0.],
            [0., 0., 1.]])
    


```python
# torch.from_numpy
print(f'{torch.from_numpy.__name__}')
import numpy as np
a = np.ones((2,3))
print(f'{torch.from_numpy(a)}')
```

    from_numpy
    tensor([[1., 1., 1.],
            [1., 1., 1.]], dtype=torch.float64)
    


```python
#  torch.linspace 均匀分布
print(f'{torch.linspace.__name__}')
print(f'{torch.linspace(1,10,steps=5)}')
```

    linspace
    tensor([ 1.0000,  3.2500,  5.5000,  7.7500, 10.0000])
    


```python
#  torch.logspace 指数分布
print(f'{torch.logspace.__name__}')
print(f'{torch.logspace(1,10,steps=5)}')
```

    logspace
    tensor([1.0000e+01, 1.7783e+03, 3.1623e+05, 5.6234e+07, 1.0000e+10])
    


```python
#  torch.ones
print(f'{torch.ones.__name__}')
print(f'{torch.ones(2,3)}')
```

    ones
    tensor([[1., 1., 1.],
            [1., 1., 1.]])
    


```python
#  torch.rand
print(f'{torch.rand.__name__} 从0到1均匀分布')
print(f'{torch.rand(2,3)}') #  均匀分布 从0到1
```

    rand 从0到1均匀分布
    tensor([[0.6931, 0.2514, 0.1247],
            [0.8758, 0.9198, 0.4984]])
    


```python
#  torch.randn
print(f'{torch.randn.__name__} 从0到1标准正态分布')
print(f'{torch.randn(2,3)}')
```

    randn 从0到1标准正态分布
    tensor([[ 1.2115,  0.6951, -2.0354],
            [-0.7793,  1.3890,  1.6093]])
    


```python
# torch.randperm
print(f'{torch.randperm.__name__} 从0到n-1的随机排列')
print(f'{torch.randperm(10)}')
```

    randperm 从0到n-1的随机排列
    tensor([6, 8, 2, 4, 5, 0, 1, 3, 9, 7])
    


```python
#  torch.arange
print(f'{torch.arange.__name__}')
print(f'{torch.arange(1,10,2)}')
```

    arange
    tensor([1, 3, 5, 7, 9])
    


```python
#  torch.zeros
print(f'{torch.zeros.__name__}')
print(f'{torch.zeros(2,3)}')
```

    zeros
    tensor([[0., 0., 0.],
            [0., 0., 0.]])
    


```python
#  切片
x=torch.randn(2,3)
print(f'{x}')
print(f"{torch.cat.__name__}")
print(torch.cat([x,x],dim=0))
print(torch.cat([x,x],dim=1))
```

    tensor([[-0.0586, -1.9284,  0.6259],
            [-0.8870, -0.4326,  0.1940]])
    cat
    tensor([[-0.0586, -1.9284,  0.6259],
            [-0.8870, -0.4326,  0.1940],
            [-0.0586, -1.9284,  0.6259],
            [-0.8870, -0.4326,  0.1940]])
    tensor([[-0.0586, -1.9284,  0.6259, -0.0586, -1.9284,  0.6259],
            [-0.8870, -0.4326,  0.1940, -0.8870, -0.4326,  0.1940]])
    


```python
print(f'{torch.chunk.__name__}')
x=torch.randn(2,3)
print(x)
print(torch.chunk(x,2,dim=0))
print(torch.chunk(x,3,dim=1))
```

    chunk
    tensor([[-0.9693,  0.0780,  1.9901],
            [ 0.4267, -0.3499,  0.2463]])
    (tensor([[-0.9693,  0.0780,  1.9901]]), tensor([[ 0.4267, -0.3499,  0.2463]]))
    (tensor([[-0.9693],
            [ 0.4267]]), tensor([[ 0.0780],
            [-0.3499]]), tensor([[1.9901],
            [0.2463]]))
    


```python
print(f'{torch.gather.__name__}')
x=torch.randn(2,3)
print(x)
print(torch.gather(x,0,torch.tensor([[0,1,1],[1,0,1],[0,1,1]])))
print(torch.gather(x,1,torch.tensor([[0,1,1],[1,0,1]])))
```

    gather
    tensor([[-0.7965,  0.4090, -1.6240],
            [-0.1944, -1.1886, -0.9032]])
    tensor([[-0.7965, -1.1886, -0.9032],
            [-0.1944,  0.4090, -0.9032],
            [-0.7965, -1.1886, -0.9032]])
    tensor([[-0.7965,  0.4090,  0.4090],
            [-1.1886, -0.1944, -1.1886]])
    


```python
print(f'{torch.index_select.__name__}')
x=torch.randn(3,4)
print(x)
index=torch.LongTensor([0,2])
print(torch.index_select(x,0,index))
print(torch.index_select(x,1,index))
```

    index_select
    tensor([[-0.7274, -0.8158, -2.2538, -0.7186],
            [ 1.6378,  0.1733,  0.9701,  0.4830],
            [ 0.0057,  0.2284,  1.9706, -0.3888]])
    tensor([[-0.7274, -0.8158, -2.2538, -0.7186],
            [ 0.0057,  0.2284,  1.9706, -0.3888]])
    tensor([[-0.7274, -2.2538],
            [ 1.6378,  0.9701],
            [ 0.0057,  1.9706]])
    


```python
print(f'{torch.masked_select.__name__}')
x=torch.randn(3,4)
print(x)
mask=torch.BoolTensor([[0,1,1,0],[1,0,0,1],[0,1,1,0]])
print(torch.masked_select(x,mask))
```

    masked_select
    tensor([[-0.1915,  0.7371,  0.1350, -0.0878],
            [-1.7266,  0.1996, -0.1849,  0.0876],
            [ 0.2520, -1.0931, -1.0763,  0.4351]])
    tensor([ 0.7371,  0.1350, -1.7266,  0.0876, -1.0931, -1.0763])
    


```python
print(f'{torch.nonzero.__name__}')
x=torch.randint(low=0,high=2,size=(3,4))
print(x)
print(torch.nonzero(x))
```

    nonzero
    tensor([[1, 1, 0, 0],
            [1, 0, 1, 0],
            [1, 0, 1, 1]])
    tensor([[0, 0],
            [0, 1],
            [1, 0],
            [1, 2],
            [2, 0],
            [2, 2],
            [2, 3]])
    


```python
print(f'{torch.split.__name__}')
x=torch.randn(2,3)
print(x)
print(torch.split(x,1,dim=0))
print(torch.split(x,2,dim=1))
print(torch.split(x,1,dim=1))
```

    split
    tensor([[-0.2771, -1.5094, -2.5222],
            [-0.5570,  0.2123,  0.2800]])
    (tensor([[-0.2771, -1.5094, -2.5222]]), tensor([[-0.5570,  0.2123,  0.2800]]))
    (tensor([[-0.2771, -1.5094],
            [-0.5570,  0.2123]]), tensor([[-2.5222],
            [ 0.2800]]))
    (tensor([[-0.2771],
            [-0.5570]]), tensor([[-1.5094],
            [ 0.2123]]), tensor([[-2.5222],
            [ 0.2800]]))
    


```python
print(f'{torch.squeeze.__name__} 去除维度为1的维度')
x=torch.randn(1,2,3,1)
print(x)
print(torch.squeeze(x))
```

    squeeze 去除维度为1的维度
    tensor([[[[-0.0248],
              [ 0.3685],
              [ 1.4184]],
    
             [[-0.3869],
              [ 0.6842],
              [-0.6448]]]])
    tensor([[-0.0248,  0.3685,  1.4184],
            [-0.3869,  0.6842, -0.6448]])
    


```python
print(f'{torch.stack.__name__} 堆叠张量')
x=torch.randn(2,3)
print(x)
print(torch.stack([x,x,x],dim=0))
print(torch.stack([x,x,x],dim=1))
```

    stack 堆叠张量
    tensor([[-1.2111, -0.5053, -0.3529],
            [ 1.0417, -0.3275, -0.4898]])
    tensor([[[-1.2111, -0.5053, -0.3529],
             [ 1.0417, -0.3275, -0.4898]],
    
            [[-1.2111, -0.5053, -0.3529],
             [ 1.0417, -0.3275, -0.4898]],
    
            [[-1.2111, -0.5053, -0.3529],
             [ 1.0417, -0.3275, -0.4898]]])
    tensor([[[-1.2111, -0.5053, -0.3529],
             [-1.2111, -0.5053, -0.3529],
             [-1.2111, -0.5053, -0.3529]],
    
            [[ 1.0417, -0.3275, -0.4898],
             [ 1.0417, -0.3275, -0.4898],
             [ 1.0417, -0.3275, -0.4898]]])
    


```python
print(f'{torch.t.__name__} 转置')
print(torch.t(torch.randn(2,3)))
```

    t 转置
    tensor([[ 0.6616,  0.8110],
            [-1.3972, -0.3666],
            [-1.1807,  0.6383]])
    


```python
print(f'{torch.transpose.__name__} 转置 共享内存')
print(torch.transpose(torch.randn(2,3),0,1))
```

    transpose 转置 共享内存
    tensor([[ 1.5000,  0.2025],
            [ 0.4079,  0.7938],
            [-1.1134, -2.7420]])
    


```python
print(f'{torch.unbind.__name__}')
x=torch.randn(2,3)
print(x)
print(torch.unbind(x,dim=0))
```

    unbind
    tensor([[ 2.4813,  0.7692,  0.6959],
            [ 0.0934, -0.2613,  0.7638]])
    (tensor([2.4813, 0.7692, 0.6959]), tensor([ 0.0934, -0.2613,  0.7638]))
    


```python
print(f'{torch.unsqueeze.__name__} 增加维度')
print(torch.unsqueeze(torch.randn(2,3),dim=0))
```

    unsqueeze 增加维度
    tensor([[[ 0.7041, -0.2160, -1.1871],
             [ 0.2697, -0.3045,  1.0322]]])
    


```python
print(f'{torch.manual_seed.__name__} 设置随机种子')
torch.manual_seed(1)
```

    manual_seed 设置随机种子
    




    <torch._C.Generator at 0x1efc730a6d0>




```python
print(f'{torch.initial_seed.__name__} 获取随机种子')
print(torch.initial_seed())
```

    initial_seed 获取随机种子
    1
    


```python
print(f'{torch.get_rng_state.__name__} 获取随机种子')
print(torch.get_rng_state())
```

    get_rng_state 获取随机种子
    tensor([1, 0, 0,  ..., 0, 0, 0], dtype=torch.uint8)
    


```python
print(f'{torch.bernoulli.__name__} 伯努利分布')
x=torch.rand(2,3)
print(x)
print(torch.bernoulli(x))
```

    bernoulli 伯努利分布
    tensor([[0.9906, 0.2885, 0.8750],
            [0.5059, 0.2366, 0.7570]])
    tensor([[1., 0., 1.],
            [1., 1., 1.]])
    


```python
print(f'{torch.multinomial.__name__} 多项式分布 replacement 表示是否重复抽取')
x=torch.rand(10)
print(x)
print(torch.multinomial(x,num_samples=5,replacement=True))
print(torch.multinomial(x,num_samples=5,replacement=False))
```

    multinomial 多项式分布 replacement 表示是否重复抽取
    tensor([0.7442, 0.5285, 0.6642, 0.6099, 0.6818, 0.7479, 0.0369, 0.7517, 0.1484,
            0.1227])
    tensor([1, 2, 3, 3, 2])
    tensor([5, 3, 2, 1, 4])
    


```python
print(f'{torch.normal.__name__} 离散正态分布')
print(torch.normal(mean=0,std=1,size=(2,3)))
```

    normal 离散正态分布
    tensor([[ 0.3133, -1.1352,  0.3773],
            [-0.2824, -2.5667, -1.4303]])
    


```python
# 序列化
print(f'{torch.save.__name__}')
torch.save(torch.randn(2,3),'test.pt')
print(f'{torch.load.__name__}')
a=torch.load('test.pt')
print(a)
```

    save
    load
    tensor([[ 0.5009,  0.5438, -0.4057],
            [ 1.1341, -1.1115,  0.3501]])
    


```python
# 并行化
print(f'{torch.get_num_threads.__name__} 获取CPU线程数')
print(torch.get_num_threads())
print(f'{torch.set_num_threads.__name__} 设置CPU线程数')
torch.set_num_threads(4)
```

    get_num_threads 获取CPU线程数
    4
    set_num_threads 设置CPU线程数
    


```python
# 张量运算
print(f'{torch.add.__name__} 矩阵相加')
print(f'{torch.abs.__name__} 绝对值')
print(f'{torch.acos.__name__} 反余弦')
print(f'{torch.addcdiv.__name__} 矩阵除法加 ')
print(f'{torch.addcmul.__name__} 矩阵乘法加')
print(f'{torch.asin.__name__} 反正弦')
print(f'{torch.atan.__name__} 反正切')
print(f'{torch.atan2.__name__} 反正切 两个矩阵')
print(f'{torch.ceil.__name__} 向上取整')
print(f'{torch.clamp.__name__} 限制范围')
print(f'{torch.clamp_min.__name__} 限制最小范围')
print(f'{torch.clamp_max.__name__} 限制最大范围')
print(f'{torch.cos.__name__} 余弦')
print(f'{torch.cosh.__name__} 双曲余弦')
print(f'{torch.div.__name__} 除法 张量/数值')
```

    add 矩阵相加
    abs 绝对值
    acos 反余弦
    addcdiv 矩阵除法加 
    addcmul 矩阵乘法加
    asin 反正弦
    atan 反正切
    atan2 反正切 两个矩阵
    ceil 向上取整
    clamp 限制范围
    clamp_min 限制最小范围
    clamp_max 限制最大范围
    cos 余弦
    cosh 双曲余弦
    div 除法 张量/数值
    


```python
print(f'{torch.exp.__name__} 指数')
print(f'{torch.expm1.__name__} 指数减一')
print(f'{torch.floor.__name__} 向下取整')
print(f'{torch.fmod.__name__} 余数')
print(f'{torch.frac.__name__} 小数部分')
print(f'{torch.lerp.__name__} 线性插值')
print(f'{torch.log.__name__} 自然对数')
print(f'{torch.log10.__name__} 10对数')
print(f'{torch.log1p.__name__} 1+x的自然对数')
print(f'{torch.mul.__name__}  张量*数值 张量一一对应')
```

    exp 指数
    expm1 指数减一
    floor 向下取整
    fmod 余数
    frac 小数部分
    lerp 线性插值
    log 自然对数
    log10 10对数
    log1p 1+x的自然对数
    mul  张量*数值 张量一一对应
    


```python
print(f'{torch.neg.__name__} 取反')
print(f'{torch.pow.__name__} 矩阵幂')
print(f'{torch.reciprocal.__name__} 倒数')
print(f'{torch.remainder.__name__} 余数 符号与除数相同')
print(f'{torch.round.__name__} 四舍五入')
print(f'{torch.rsqrt.__name__} 倒数开方')
print(f'{torch.sigmoid.__name__} 矩阵的sigmoid函数')
print(f'{torch.sign.__name__} 符号')
print(f'{torch.sin.__name__} 正弦')
```

    neg 取反
    pow 矩阵幂
    reciprocal 倒数
    remainder 余数 符号与除数相同
    round 四舍五入
    rsqrt 倒数开方
    sigmoid 矩阵的sigmoid函数
    sign 符号
    sin 正弦
    


```python
print(f'{torch.sinh.__name__} 双曲正弦')
print(f'{torch.sqrt.__name__} 开方')
print(f'{torch.tan.__name__} 正切')
print(f'{torch.tanh.__name__} 双曲正切')
print(f'{torch.trunc.__name__} 截断小数部分')
```

    sinh 双曲正弦
    sqrt 开方
    tan 正切
    tanh 双曲正切
    trunc 截断小数部分
    


```python
print(f'{torch.cumprod.__name__} 矩阵累乘')
print(f'{torch.cumsum.__name__} 矩阵累加')
print(f'{torch.dist.__name__} 矩阵距离')
print(f'{torch.mean.__name__} 矩阵平均值')
print(f'{torch.median.__name__} 矩阵中位数')
print(f'{torch.mode.__name__} 矩阵众数')
print(f'{torch.norm.__name__} 矩阵范数')
```

    cumprod 矩阵累乘
    cumsum 矩阵累加
    dist 矩阵距离
    mean 矩阵平均值
    median 矩阵中位数
    mode 矩阵众数
    norm 矩阵范数
    


```python
print(f'{torch.prod.__name__} 矩阵乘积')
print(f'{torch.std.__name__} 矩阵标准差')
print(f'{torch.sum.__name__} 矩阵求和')
print(f'{torch.var.__name__} 矩阵方差')
```

    prod 矩阵乘积
    std 矩阵标准差
    sum 矩阵求和
    var 矩阵方差
    


```python
print(f'{torch.eq.__name__} 元素相等性 输出矩阵' )
print(f'{torch.equal.__name__} 元素相等性 输出布尔值')
print(f'{torch.ge.__name__} 元素大于等于 输出矩阵')
print(f'{torch.gt.__name__} 元素大于 输出矩阵')
print(f'{torch.le.__name__} 元素小于等于 输出矩阵')
```

    eq 元素相等性 输出矩阵
    equal 元素相等性 输出布尔值
    ge 元素大于等于 输出矩阵
    gt 元素大于 输出矩阵
    


```python
print(f'{torch.kthvalue.__name__} 矩阵第k小的值')
print(f'{torch.lt.__name__} 元素小于 输出矩阵')
print(f'{torch.max.__name__} 矩阵最大值')
print(f'{torch.min.__name__} 矩阵最小值')
print(f'{torch.sort.__name__} 矩阵排序')
print(f'{torch.topk.__name__} 矩阵前k大的值')
```

    kthvalue 矩阵第k小的值
    lt 元素小于 输出矩阵
    max 矩阵最大值
    min 矩阵最小值
    sort 矩阵排序
    topk 矩阵前k大的值
    


```python
print(f'{torch.cross.__name__} 矩阵叉积')
```

    cross 矩阵叉积
    


```python
print(f'{torch.histc.__name__} 矩阵直方图')
x=torch.randint(low=0,high=11,size=(10,10),dtype=torch.float64)
print(torch.histc(x,bins=10))
```

    histc 矩阵直方图
    tensor([ 8.,  9.,  9.,  9.,  8.,  6., 13.,  5.,  9., 24.], dtype=torch.float64)
    


```python
print(f'{torch.renorm.__name__} 矩阵范数归一化')
x=torch.ones(3,3)
x[1].fill_(2)
x[2].fill_(3)
print(x)
print(torch.renorm(x,p=2,dim=0,maxnorm=5))
x=torch.tensor([2.8868, 2.8868, 2.8868])
x.pow(2).sum().pow(0.5)
```

    renorm 矩阵范数归一化
    tensor([[1., 1., 1.],
            [2., 2., 2.],
            [3., 3., 3.]])
    tensor([[1.0000, 1.0000, 1.0000],
            [2.0000, 2.0000, 2.0000],
            [2.8868, 2.8868, 2.8868]])
    




    tensor(5.0001)




```python
print(f'{torch.trace.__name__} 矩阵迹')
print(f'{torch.tril.__name__} 矩阵下三角')
print(f'{torch.triu.__name__} 矩阵上三角')
```

    trace 矩阵迹
    tril 矩阵下三角
    triu 矩阵上三角
    


```python
# 矩阵算术
print(f'{torch.addbmm.__name__} 批量矩阵乘法 加')
print(f'{torch.addmm.__name__} 矩阵乘法 加')
print(f'{torch.addmv.__name__} 矩阵-向量乘法 加')
print(f'{torch.addr.__name__} 向量-向量乘法 加')
print(f'{torch.baddbmm.__name__} 批量矩阵乘法 乘')
```

    addbmm 批量矩阵乘法 加
    addmm 矩阵乘法 加
    addmv 矩阵-向量乘法 加
    addr 向量-向量乘法 加
    baddbmm 批量矩阵乘法 乘
    


```python
print(f'{torch.bmm.__name__} 批量矩阵乘法')
x=torch.randint(low=0,high=10,size=(2,2,3))
y=torch.randint(low=0,high=10,size=(2,3,4))
print(x,y)
print(torch.bmm(x,y))
```

    bmm 批量矩阵乘法
    tensor([[[5, 0, 5],
             [7, 6, 0]],
    
            [[9, 0, 1],
             [8, 9, 1]]]) tensor([[[9, 9, 2, 5],
             [7, 6, 3, 5],
             [1, 5, 1, 6]],
    
            [[0, 6, 5, 6],
             [8, 9, 2, 2],
             [5, 2, 3, 1]]])
    tensor([[[ 50,  70,  15,  55],
             [105,  99,  32,  65]],
    
            [[  5,  56,  48,  55],
             [ 77, 131,  61,  67]]])
    


```python
print(f'{torch.dot.__name__} 向量点乘 ')
print(f'{torch.eig.__name__} 矩阵特征值 以及特征向量')
```

    dot 向量点乘 
    eig 矩阵特征值 以及特征向量
    


```python
x=torch.tensor([[1,3],[3,1]],dtype=torch.float64)
theta,v=torch.linalg.eig(x)
print(theta,v) #V向量是按照列顺序排列的且已经归一化
```

    tensor([ 4.0000+0.j, -2.0000+0.j], dtype=torch.complex128) tensor([[ 0.7071+0.j, -0.7071+0.j],
            [ 0.7071+0.j,  0.7071+0.j]], dtype=torch.complex128)
    


```python
print(f'{torch.inverse.__name__} 矩阵求逆')
torch.inverse(torch.diag(torch.tensor([1,2,3,4,5],dtype=torch.float64)))
```

    inverse 矩阵求逆
    




    tensor([[1.0000, 0.0000, 0.0000, 0.0000, 0.0000],
            [0.0000, 0.5000, 0.0000, 0.0000, 0.0000],
            [0.0000, 0.0000, 0.3333, 0.0000, 0.0000],
            [0.0000, 0.0000, 0.0000, 0.2500, 0.0000],
            [0.0000, 0.0000, 0.0000, 0.0000, 0.2000]], dtype=torch.float64)




```python
print(f'{torch.mm.__name__} 矩阵乘法')
x=torch.randint(low=0,high=10,size=(2,3))
y=torch.randint(low=0,high=10,size=(3,4))
print(x,y)
print(torch.mm(x,y))
```

    mm 矩阵乘法
    tensor([[8, 5, 7],
            [9, 5, 6]]) tensor([[8, 4, 9, 6],
            [4, 0, 4, 3],
            [7, 1, 3, 4]])
    tensor([[133,  39, 113,  91],
            [134,  42, 119,  93]])
    


```python
print(f'{torch.mv.__name__} 矩阵-向量乘法')
x=torch.randint(low=0,high=10,size=(2,3))
y=torch.randint(low=0,high=10,size=(3,))
print(x,y)
print(torch.mv(x,y))
```

    mv 矩阵-向量乘法
    tensor([[5, 9, 9],
            [2, 6, 2]]) tensor([0, 9, 8])
    tensor([153,  70])
    


```python
print(f'{torch.matmul.__name__} 矩阵乘法')
torch.matmul(x,y)
```

    matmul 矩阵乘法
    




    tensor([153,  70])




```python
print(f'{torch.svd.__name__} 矩阵奇异值分解')
x=torch.randint(low=0,high=10,size=(2,3),dtype=torch.float64)
print(x)
u,s,v=torch.svd(x)
print(u,s,v,sep='\n') #U向量是按照列顺序排列的,V向量是按照列顺序排列的且已经归一化
```

    svd 矩阵奇异值分解
    tensor([[4., 1., 7.],
            [4., 5., 6.]], dtype=torch.float64)
    tensor([[ 0.6757, -0.7372],
            [ 0.7372,  0.6757]], dtype=torch.float64)
    tensor([11.6077,  2.8741], dtype=torch.float64)
    tensor([[ 0.4869, -0.0857],
            [ 0.3758,  0.9189],
            [ 0.7885, -0.3850]], dtype=torch.float64)
    


```python
u@torch.diag(s)@v.t()
```




    tensor([[4.0000, 1.0000, 7.0000],
            [4.0000, 5.0000, 6.0000]], dtype=torch.float64)




```python
print(f'{torch.symeig.__name__} 实对称 矩阵特征值 以及特征向量')
x=torch.diag(torch.tensor([1,2,3,4,5],dtype=torch.float64))
print(x)
e,v=torch.linalg.eig(x)
print(e,v,sep='\n')
```

    _symeig 实对称 矩阵特征值 以及特征向量
    tensor([[1., 0., 0., 0., 0.],
            [0., 2., 0., 0., 0.],
            [0., 0., 3., 0., 0.],
            [0., 0., 0., 4., 0.],
            [0., 0., 0., 0., 5.]], dtype=torch.float64)
    tensor([1.+0.j, 2.+0.j, 3.+0.j, 4.+0.j, 5.+0.j], dtype=torch.complex128)
    tensor([[1.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j],
            [0.+0.j, 1.+0.j, 0.+0.j, 0.+0.j, 0.+0.j],
            [0.+0.j, 0.+0.j, 1.+0.j, 0.+0.j, 0.+0.j],
            [0.+0.j, 0.+0.j, 0.+0.j, 1.+0.j, 0.+0.j],
            [0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 1.+0.j]], dtype=torch.complex128)
    
