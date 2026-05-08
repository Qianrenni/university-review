
# 📚 Java 高频面试 & 核心知识体系学习大纲

---

## 🔹 一、基础篇（共62讲）

### ✅ 1. 二分查找系列

- 01-课程介绍
- 02-二分查找_演示
- 03-二分查找_实现
- 04-解决整数溢出_方法1
- 05-解决整数溢出_方法2
- 06~08-选择题目与注意事项

### ✅ 2. 排序算法系列

| 类型 | 视频数量 |
|------|----------|
| 冒泡排序 | 09~15 |
| 选择排序 | 16~18 |
| 插入排序 | 19~21 |
| 希尔排序 | 22 |
| 快速排序 | 23~31 |

### ✅ 3. Java集合框架源码分析

- ArrayList扩容规则
- Iterator：FailFast vs FailSafe
- LinkedList vs ArrayList性能比较（随机访问、增删、空间）
- HashMap：
  - 数据结构原理
  - 哈希计算、扩容、树化、负载因子等
  - 并发问题（丢数据、死链）

### ✅ 4. 设计模式

- 单例模式的多种实现方式（饿汉式、懒汉式、DCL、内部类、枚举）
- volatile的作用（DCL中防止指令重排）
- JDK中的单例体现

---

## 🔹 二、并发编程篇（共38讲）

### ✅ 1. 线程与线程池

- Java线程状态（五种 vs 六种）
- 线程池核心参数详解与演示

### ✅ 2. 多线程同步机制

| 对比项 | 内容 |
|--------|------|
| wait vs sleep | 区别与代码演示 |
| Lock vs synchronized | 区别与阻塞演示 |
| volatile | 可见性、原子性、有序性演示与分析 |

### ✅ 3. 锁优化与底层原理

- 悲观锁 vs 乐观锁（CAS 实现）
- Unsafe 类操作 CAS
- Hashtable vs ConcurrentHashMap（v7 vs v8）

### ✅ 4. ThreadLocal

- 原理、key/value内存释放时机（get/set/remove时）

---

## 🔹 三、JVM 虚拟机篇（共33讲）

### ✅ 1. 内存模型与GC

- JVM内存结构（栈、堆、方法区、PC寄存器等）
- 垃圾回收算法（标记清除、复制、标记整理、分代回收）
- G1垃圾回收器详解
- 三色标记法、并发漏标问题

### ✅ 2. 类加载机制

- 类加载过程（加载、链接、初始化）
- 类加载器（双亲委派机制）
- final修饰变量原理
- 如何避免假冒System类

### ✅ 3. 引用类型

- 强引用、软引用、弱引用、虚引用
- Cleaner、finalize原理与调用机制

---

## 🔹 四、Spring 框架源码解析篇（共66讲）

### ✅ 1. Spring 容器启动流程（refresh全过程）

- Environment、BeanFactory准备
- BeanPostProcessor注册
- 初始化单例Bean
- refresh小结

### ✅ 2. Bean生命周期深度剖析

- 创建Bean实例、依赖注入、初始化阶段
- 销毁Bean的过程
- 不同作用域Bean处理方式

### ✅ 3. Spring事务失效场景分析（共8种）

- 检查异常、try-catch错误、非public方法、本类调用、锁失效等

### ✅ 4. Spring Web MVC执行流程

- 初始化、匹配、执行

### ✅ 5. 注解驱动开发

- Spring、WebMvc、Boot常用注解
- @Configuration配置类细节（代理机制、不能重载、依赖注入失效）

### ✅ 6. 自动装配原理

- @SpringBootApplication、@EnableAutoConfiguration
- Spring Boot自动配置原理

### ✅ 7. 循环依赖专题（共16讲）

- ProxyFactory、AOP、三级缓存机制详解
- Set循环依赖、构造器循环依赖及解决方案（@Lazy、ObjectFactory、Provider、@Scope）

---

## 📌 总结：学习路径推荐

| 学习顺序 | 推荐模块 |
|----------|-----------|
| 第一阶段 | 基础篇（排序 + 集合 + 单例） |
| 第二阶段 | 并发篇（线程池 + Lock + volatile + CAS） |
| 第三阶段 | JVM（内存结构 + GC + 类加载） |
| 第四阶段 | Spring 源码（容器启动 + Bean 生命周期 + 事务 + 循环依赖） |

---
