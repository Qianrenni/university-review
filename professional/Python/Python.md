
# **基础语法与核心概念**

## **数据类型与数据结构**

- **基本数据类型**：
  - 数字（`int`, `float`, `complex`）
  - 字符串（`str`）：字符串操作、格式化（`%`、`format()`、f-string）、切片等。
  - 布尔值（`bool`）
- **复合数据结构**：
  - 列表（`list`）：增删改查、切片、列表推导式。
  - 元组（`tuple`）：不可变性、解包。
  - 字典（`dict`）：键值对操作、字典推导式、默认字典（`defaultdict`）。
  - 集合（`set` 和 `frozenset`）：集合运算（交集、并集、差集等）
    >frozenset 的核心优势在于它的不可变性和可哈希性，这使得它在以下场景中非常有用：
    1. 作为字典的键。
    2. 存储在其他集合中。
    3. 确保集合内容不可变。
    4. 进行集合运算。
    5. 多线程环境下的安全操作。
    6. 集合的比较和去重。。

## **控制流**

- 条件语句（`if-elif-else`）。
- 循环语句（`for` 和 `while`），包括 `break`、`continue` 和 `else` 子句。
- 列表推导式和生成器表达式。

```python
def generateNumber(start,end):
    while start<=end:
        yield start
        start+=1
```

## **函数**

- **定义与调用**：`def` 关键字。
- **参数类型**：
  - 必选参数、默认参数、可变参数（`*args` 和 `**kwargs`）。
- **作用域**：局部变量与全局变量，`global` 和 `nonlocal` 关键字。
  - globl: 全局变量
  - nonlocal: 嵌套函数中访问外部函数的变量
- **匿名函数**：`lambda` 表达式。
- **递归**：递归函数的设计与优化。
    使用迭代替代递归，避免栈溢出。
    使用缓存（Memoization），减少重复计算。
    限制递归深度，防止 RecursionError。
    使用生成器，优化内存使用。
    结合分治法与动态规划，提高递归效率。

## **异常处理**

- `try-except-finally` 结构。
- 自定义异常类。

```python
try:
    num = int(input("请输入一个数字: "))
    result = 10 / num
except ValueError:
    print("输入无效，请输入一个数字！")
except ZeroDivisionError:
    print("除数不能为零！")
else:
    print(f"结果是: {result}")
finally:
    print("这是 finally 块，总会执行。")
```

## **文件读写**

### **1. 基于字节流的文件读写**

#### **1.1 字节流简介**

- **定义**：字节流是以二进制形式读写文件的方式，适用于处理非文本数据（如图片、音频、视频等）或需要精确控制数据格式的场景。
- **模式**：
  - `'rb'`：以只读模式打开二进制文件。
  - `'wb'`：以写入模式打开二进制文件（会覆盖原有内容）。
  - `'ab'`：以追加模式打开二进制文件。
  - `'r+b'` 或 `'rb+'`：以读写模式打开二进制文件。

#### **1.2 示例代码**

- **(1) 写入二进制文件**

```python
# 写入字节数据到文件
data = b'\x00\xFF\x7F\x80'  # 字节数据
with open('binary_file.bin', 'wb') as file:
    file.write(data)
```

- **(2) 读取二进制文件**

```python
# 从文件中读取字节数据
with open('binary_file.bin', 'rb') as file:
    content = file.read()
print(content)  # 输出: b'\x00\xFF\x7F\x80'
```

- **(3) 追加二进制数据**

```python
# 向文件追加字节数据
new_data = b'\x01\x02'
with open('binary_file.bin', 'ab') as file:
    file.write(new_data)
```

#### **1.3 注意事项**

- 字节流直接操作的是原始的字节数据，不会对数据进行任何编码或解码。
- 适合处理非文本文件（如图片、音频、视频等），或者需要逐字节处理数据的场景。

---

### **2. 基于字符流的文件读写**

#### **2.1 字符流简介**

- **定义**：字符流是以文本形式读写文件的方式，适用于处理文本数据。Python 会在内部自动进行字符编码和解码。
- **模式**：
  - `'r'`：以只读模式打开文本文件（默认模式）。
  - `'w'`：以写入模式打开文本文件（会覆盖原有内容）。
  - `'a'`：以追加模式打开文本文件。
  - `'r+'` 或 `'w+'`：以读写模式打开文本文件。

#### **2.2 示例代码**

- **(1) 写入文本文件**

```python
# 写入字符串到文件
text = "Hello, World!"
with open('text_file.txt', 'w', encoding='utf-8') as file:
    file.write(text)
```

- **(2) 读取文本文件**

```python
# 从文件中读取字符串
with open('text_file.txt', 'r', encoding='utf-8') as file:
    content = file.read()
print(content)  # 输出: Hello, World!
```

- **(3) 追加文本数据**

```python
# 向文件追加字符串
new_text = "\nThis is a new line."
with open('text_file.txt', 'a', encoding='utf-8') as file:
    file.write(new_text)
```

#### **2.3 编码与解码**

- **编码**：将字符串转换为字节序列（写入时）。
- **解码**：将字节序列转换为字符串（读取时）。
- 在字符流中，`encoding` 参数指定了使用的字符编码（如 `utf-8`, `ascii`, `latin-1` 等）。如果不指定，默认使用系统的默认编码。

    ```python
    # 使用不同的编码写入和读取文件
    text = "你好，世界！"
    with open('text_file.txt', 'w', encoding='utf-8') as file:
        file.write(text)

    with open('text_file.txt', 'r', encoding='utf-8') as file:
        content = file.read()
    print(content)  # 输出: 你好，世界！
    ```

#### **2.4 注意事项**

- 字符流会根据指定的编码自动进行编码和解码。
- 如果文件包含非 ASCII 字符（如中文、日文等），必须正确设置编码（推荐使用 `utf-8`）。

---

### **3. 字节流与字符流的区别**

| 特性               | 字节流                          | 字符流                          |
|--------------------|---------------------------------|---------------------------------|
| **数据类型**       | 字节（`bytes` 类型）            | 字符（`str` 类型）              |
| **适用场景**       | 非文本文件（图片、音频、视频等） | 文本文件                        |
| **编码/解码**      | 不涉及编码/解码                 | 自动进行编码和解码              |
| **文件模式**       | `'rb'`, `'wb'`, `'ab'` 等       | `'r'`, `'w'`, `'a'` 等          |
| **是否支持换行符** | 不支持自动处理换行符             | 支持自动处理换行符（`\n` -> `\r\n` 等） |

---

### **4. 混合使用字节流与字符流**

有时候需要同时处理字节流和字符流，例如在网络通信中接收字节数据并将其解码为字符串。

**示例：字节流与字符流结合**

```python
# 将字节数据解码为字符串
byte_data = b'Hello, \xe4\xb8\x96\xe7\x95\x8c!'  # 包含 UTF-8 编码的中文
text = byte_data.decode('utf-8')
print(text)  # 输出: Hello, 世界!

# 将字符串编码为字节数据
new_text = "你好，Python!"
new_byte_data = new_text.encode('utf-8')
print(new_byte_data)  # 输出: b'\xe4\xbd\xa0\xe5\xa5\xbd\xef\xbc\x8cPython!'
```

---

# **进阶特性**

## **面向对象编程（OOP）**

### **类与对象**

- **定义类（`class`）、构造函数（`__init__`）**：
  - 类是面向对象编程的核心，用于封装数据和行为。
  - 构造函数 `__init__` 用于初始化对象的属性。

  ```python
  class Person:
      def __init__(self, name, age):
          self.name = name  # 实例属性
          self.age = age

  p = Person("Alice", 30)
  print(p.name)  # 输出：Alice
  ```

- **属性与方法**：
  - **实例属性**：属于某个具体对象。
  - **类属性**：所有实例共享。
  - 方法分为实例方法、类方法（`@classmethod`）、静态方法（`@staticmethod`）。

  ```python
  class Dog:
      species = "Canis familiaris"  # 类属性

      def __init__(self, name, age):
          self.name = name  # 实例属性
          self.age = age

      def bark(self):  # 实例方法
          print(f"{self.name} barks!")
  ```

---

### **继承与多态**

- **单继承与多继承**：
  - 单继承：一个子类继承自一个父类。
  - 多继承：一个子类可以继承多个父类，Python 使用 C3 线性化算法解决方法解析顺序（MRO）。

  ```python
  class Animal:
      def speak(self):
          print("Animal speaks")

  class Dog(Animal):
      def speak(self):
          print("Dog barks")

  d = Dog()
  d.speak()  # 输出：Dog barks
  ```

- **方法重写与 `super()`**：
  - 子类可以重写父类的方法。
  - 使用 `super()` 调用父类的方法。

  ```python
  class Vehicle:
      def start(self):
          print("Vehicle started")

  class Car(Vehicle):
      def start(self):
          super().start()
          print("Car engine running")

  car = Car()
  car.start()
  # 输出：
  # Vehicle started
  # Car engine running
  ```

---

### **特殊方法（魔术方法）**

- **常用魔术方法**：
  - `__str__` 和 `__repr__`：定义对象的字符串表示。
  - `__len__`：定义对象的长度。
  - `__getitem__` 和 `__setitem__`：支持索引操作。

  ```python
  class Point:
      def __init__(self, x, y):
          self.x = x
          self.y = y

      def __str__(self):
          return f"Point({self.x}, {self.y})"

      def __repr__(self):
          return f"Point(x={self.x}, y={self.y})"

  p = Point(1, 2)
  print(str(p))  # 输出：Point(1, 2)
  print(repr(p)) # 输出：Point(x=1, y=2)
  ```

  ```python
  class MyList:
      def __init__(self, data):
          self.data = data

      def __len__(self):
          return len(self.data)

      def __getitem__(self, index):
          return self.data[index]

      def __setitem__(self, index, value):
          self.data[index] = value

  ml = MyList([1, 2, 3])
  print(len(ml))       # 输出：3
  print(ml[1])         # 输出：2
  ml[1] = 10
  print(ml[1])         # 输出：10
  ```

## **描述符**

描述符（Descriptor）是 Python 中一种强大的工具，用于控制对类属性的访问、赋值和删除操作。它通过实现特定的协议（`__get__`、`__set__` 和 `__delete__` 方法）来定义这些行为。描述符通常用于封装属性访问逻辑，提升代码的可复用性和灵活性。

### 描述符的核心概念

1. **描述符协议**：
   - 描述符是一个实现了以下方法之一或多个的类：
     - `__get__(self, instance, owner)`：用于获取属性值。
     - `__set__(self, instance, value)`：用于设置属性值。
     - `__delete__(self, instance)`：用于删除属性值。

2. **工作原理**：
   - 当一个类的属性是描述符实例时，对该属性的访问（读取、写入或删除）会被描述符的方法拦截并处理。
   - 这使得描述符可以自定义属性的行为，比如验证数据、延迟加载、日志记录等。

3. **分类**：
   - **数据描述符**：同时实现了 `__get__` 和 `__set__` 的描述符。
   - **非数据描述符**：只实现了 `__get__` 的描述符。

---

### 示例代码解析

```python
class Descriptor:
    def __get__(self, instance, owner):
        # 获取属性值
        return instance._value

    def __set__(self, instance, value):
        # 设置属性值
        instance._value = value


class MyClass:
    attribute = Descriptor()  # 将描述符绑定到类属性上


obj = MyClass()
obj.attribute = 42  # 调用描述符的 __set__ 方法
print(obj.attribute)  # 调用描述符的 __get__ 方法，输出：42
```

### 分析

1. **描述符类 (`Descriptor`)**：
   - `__get__`：当访问 `obj.attribute` 时被调用，返回 `instance._value`。
   - `__set__`：当执行 `obj.attribute = 42` 时被调用，将值存储在 `instance._value` 中。

2. **使用描述符的类 (`MyClass`)**：
   - `attribute` 是 `Descriptor` 的实例，因此对它的访问和赋值会触发描述符的方法。

3. **实例对象 (`obj`)**：
   - `obj.attribute = 42` 实际上调用了 `Descriptor.__set__` 方法，将值存储在 `obj._value` 中。
   - `print(obj.attribute)` 实际上调用了 `Descriptor.__get__` 方法，返回存储的值。

---

### 描述符的应用场景

1. **属性验证**：
   描述符可以用来确保属性值满足某些条件。

   ```python
   class PositiveNumber:
       def __get__(self, instance, owner):
           return instance._value

       def __set__(self, instance, value):
           if value < 0:
               raise ValueError("Value must be positive")
           instance._value = value

   class Item:
       price = PositiveNumber()

   item = Item()
   item.price = 100  # 正常
   item.price = -10  # 抛出 ValueError
   ```

2. **延迟加载**：
   描述符可以实现延迟加载属性值的功能。

   ```python
   class LazyProperty:
       def __init__(self, func):
           self.func = func

       def __get__(self, instance, owner):
           if instance is None:
               return self
           value = self.func(instance)
           setattr(instance, self.func.__name__, value)
           return value

   class MyClass:
       @LazyProperty
       def expensive_calculation(self):
           print("Calculating...")
           return 42

   obj = MyClass()
   print(obj.expensive_calculation)  # 计算一次
   print(obj.expensive_calculation)  # 直接返回缓存值
   ```

3. **日志记录**：
   描述符可以记录对属性的访问。

   ```python
   class LoggedAttribute:
       def __get__(self, instance, owner):
           print(f"Accessing attribute")
           return instance._value

       def __set__(self, instance, value):
           print(f"Setting attribute to {value}")
           instance._value = value

   class MyClass:
       attribute = LoggedAttribute()

   obj = MyClass()
   obj.attribute = 42
   print(obj.attribute)
   ```

---

## **元编程（Metaprogramming）**

元编程是指"操作代码的代码"，即在运行时动态创建、修改或检查类、函数等程序结构。Python 提供了强大的元编程能力，但应谨慎使用。

### **1. 元类（Metaclass）**

元类是"类的类"，控制类的创建过程。`type` 是 Python 的默认元类。

#### **type 的三种用法**

```python
# 1. 获取对象类型
print(type(42))        # <class 'int'>
print(type("hello"))   # <class 'str'>

# 2. 动态创建类
MyClass = type('MyClass', (), {'x': 10})
obj = MyClass()
print(obj.x)  # 10

# 3. 作为元类基类
class Meta(type):
    def __new__(mcs, name, bases, namespace):
        print(f"Creating class: {name}")
        return super().__new__(mcs, name, bases, namespace)

class MyClass(metaclass=Meta):
    pass
# 输出: Creating class: MyClass
```

#### **__new__ vs __init__**

```python
class Meta(type):
    def __new__(mcs, name, bases, namespace):
        """在类创建时调用（返回新类对象）"""
        print(f"__new__: Creating {name}")
        
        # 可以在这里修改类定义
        namespace['added_by_meta'] = True
        
        return super().__new__(mcs, name, bases, namespace)
    
    def __init__(cls, name, bases, namespace):
        """在类创建后调用（初始化类对象）"""
        print(f"__init__: Initializing {name}")
        super().__init__(name, bases, namespace)

class MyClass(metaclass=Meta):
    x = 10

print(MyClass.added_by_meta)  # True
```

#### **实战：单例模式元类**

```python
class SingletonMeta(type):
    """确保类只有一个实例"""
    _instances = {}
    
    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            instance = super().__call__(*args, **kwargs)
            cls._instances[cls] = instance
        return cls._instances[cls]

class DatabaseConnection(metaclass=SingletonMeta):
    def __init__(self, host="localhost"):
        self.host = host
        print(f"Connected to {host}")

# 两次实例化返回同一对象
db1 = DatabaseConnection()
db2 = DatabaseConnection()
print(db1 is db2)  # True
```

#### **实战：自动注册插件**

```python
class PluginRegistry(type):
    """自动注册所有子类"""
    _plugins = {}
    
    def __new__(mcs, name, bases, namespace):
        cls = super().__new__(mcs, name, bases, namespace)
        if name != "BasePlugin":  # 不注册基类
            PluginRegistry._plugins[name] = cls
        return cls
    
    @classmethod
    def get_plugin(cls, name):
        return cls._plugins.get(name)

class BasePlugin(metaclass=PluginRegistry):
    def execute(self):
        raise NotImplementedError

class EmailPlugin(BasePlugin):
    def execute(self):
        return "Sending email"

class SMSPlugin(BasePlugin):
    def execute(self):
        return "Sending SMS"

# 自动注册
print(PluginRegistry.get_plugin("EmailPlugin"))  # <class 'EmailPlugin'>
print(PluginRegistry.get_plugin("SMSPlugin"))    # <class 'SMSPlugin'>

# 使用
plugin = PluginRegistry.get_plugin("EmailPlugin")()
print(plugin.execute())  # Sending email
```

#### **元类继承与 MRO**

```python
class MetaA(type):
    def __new__(mcs, name, bases, namespace):
        namespace['from_a'] = True
        return super().__new__(mcs, name, bases, namespace)

class MetaB(type):
    def __new__(mcs, name, bases, namespace):
        namespace['from_b'] = True
        return super().__new__(mcs, name, bases, namespace)

# 多重元类继承需要兼容
class CombinedMeta(MetaA, MetaB):
    pass

class MyClass(metaclass=CombinedMeta):
    pass

print(MyClass.from_a)  # True
print(MyClass.from_b)  # True
```

### **2. 描述符协议深化**

#### **描述符优先级**

```python
class DataDescriptor:
    """数据描述符（实现 __set__）"""
    def __get__(self, obj, objtype=None):
        return "data_descriptor_get"
    
    def __set__(self, obj, value):
        print(f"data_descriptor_set: {value}")

class NonDataDescriptor:
    """非数据描述符（只实现 __get__）"""
    def __get__(self, obj, objtype=None):
        return "non_data_descriptor_get"

class MyClass:
    data_desc = DataDescriptor()
    non_data_desc = NonDataDescriptor()

obj = MyClass()

# 优先级：数据描述符 > 实例属性 > 非数据描述符
obj.__dict__['data_desc'] = "instance_attr"
print(obj.data_desc)  # data_descriptor_get（描述符优先）

obj.__dict__['non_data_desc'] = "instance_attr"
print(obj.non_data_desc)  # instance_attr（实例属性优先）
```

#### **property 内部实现**

```python
class Property:
    """简化版 property 实现"""
    def __init__(self, fget=None, fset=None, fdel=None, doc=None):
        self.fget = fget
        self.fset = fset
        self.fdel = fdel
        self.__doc__ = doc
    
    def __get__(self, obj, objtype=None):
        if obj is None:
            return self
        if self.fget is None:
            raise AttributeError("unreadable attribute")
        return self.fget(obj)
    
    def __set__(self, obj, value):
        if self.fset is None:
            raise AttributeError("can't set attribute")
        self.fset(obj, value)
    
    def __delete__(self, obj):
        if self.fdel is None:
            raise AttributeError("can't delete attribute")
        self.fdel(obj)
    
    def getter(self, fget):
        return type(self)(fget, self.fset, self.fdel, self.__doc__)
    
    def setter(self, fset):
        return type(self)(self.fget, fset, self.fdel, self.__doc__)

# 使用
class Circle:
    def __init__(self, radius):
        self._radius = radius
    
    @Property
    def radius(self):
        """Radius of the circle"""
        return self._radius
    
    @radius.setter
    def radius(self, value):
        if value < 0:
            raise ValueError("Radius cannot be negative")
        self._radius = value

c = Circle(5)
print(c.radius)  # 5
c.radius = 10
print(c.radius)  # 10
```

#### **实战：ORM 字段定义**

```python
class Field:
    """ORM 字段描述符"""
    def __init__(self, field_type, default=None, nullable=True):
        self.field_type = field_type
        self.default = default
        self.nullable = nullable
        self.name = None  # 由 __set_name__ 设置
    
    def __set_name__(self, owner, name):
        """Python 3.6+：自动获取属性名"""
        self.name = name
    
    def __get__(self, obj, objtype=None):
        if obj is None:
            return self
        return obj.__dict__.get(self.name, self.default)
    
    def __set__(self, obj, value):
        if value is None and not self.nullable:
            raise ValueError(f"{self.name} cannot be null")
        if value is not None and not isinstance(value, self.field_type):
            raise TypeError(f"{self.name} must be {self.field_type.__name__}")
        obj.__dict__[self.name] = value

class ModelMeta(type):
    """模型元类：收集所有字段"""
    def __new__(mcs, name, bases, namespace):
        cls = super().__new__(mcs, name, bases, namespace)
        fields = {
            attr_name: attr
            for attr_name, attr in namespace.items()
            if isinstance(attr, Field)
        }
        cls._fields = fields
        return cls

class Model(metaclass=ModelMeta):
    def save(self):
        data = {
            name: getattr(self, name)
            for name in self._fields
        }
        print(f"Saving: {data}")

class User(Model):
    id = Field(int, default=0, nullable=False)
    name = Field(str, nullable=False)
    email = Field(str, nullable=True)

user = User()
user.id = 1
user.name = "Alice"
user.email = "alice@example.com"
user.save()  # Saving: {'id': 1, 'name': 'Alice', 'email': 'alice@example.com'}
```

### **3. 动态类与函数创建**

#### **type() 动态创建类**

```python
# 动态创建带方法的类
def greet(self):
    return f"Hello, I'm {self.name}"

def __init__(self, name):
    self.name = name

Person = type('Person', (), {
    '__init__': __init__,
    'greet': greet
})

p = Person("Alice")
print(p.greet())  # Hello, I'm Alice
```

#### **动态添加属性和方法**

```python
class DynamicClass:
    pass

# 添加类属性
DynamicClass.x = 10

# 添加方法
def method(self):
    return "dynamic method"

DynamicClass.method = method

obj = DynamicClass()
print(obj.x)       # 10
print(obj.method())  # dynamic method
```

#### **functools.partial 偏函数**

```python
from functools import partial

def power(base, exponent):
    return base ** exponent

# 创建偏函数
square = partial(power, exponent=2)
cube = partial(power, exponent=3)

print(square(5))  # 25
print(cube(3))    # 27
```

### **4. 装饰器高级模式**

#### **类装饰器实现接口检查**

```python
from abc import ABC, abstractmethod
from typing import Protocol

def enforce_interface(interface_cls):
    """装饰器：确保类实现指定接口"""
    def decorator(cls):
        for name in dir(interface_cls):
            if not name.startswith('_'):
                attr = getattr(interface_cls, name)
                if callable(attr) and not hasattr(cls, name):
                    raise NotImplementedError(
                        f"{cls.__name__} must implement {name}"
                    )
        return cls
    return decorator

class Drawable(Protocol):
    def draw(self) -> None: ...
    def resize(self, factor: float) -> None: ...

@enforce_interface(Drawable)
class Circle:
    def draw(self) -> None:
        print("Drawing circle")
    
    def resize(self, factor: float) -> None:
        print(f"Resizing by {factor}")

# @enforce_interface(Drawable)
# class Square:  # ❌ NotImplementedError
#     def draw(self) -> None:
#         pass
```

#### **重试装饰器**

```python
import time
import functools

def retry(max_attempts=3, delay=1, backoff=2, exceptions=(Exception,)):
    """重试装饰器"""
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            current_delay = delay
            last_exception = None
            
            for attempt in range(max_attempts):
                try:
                    return func(*args, **kwargs)
                except exceptions as e:
                    last_exception = e
                    if attempt < max_attempts - 1:
                        print(f"Attempt {attempt + 1} failed: {e}. Retrying in {current_delay}s...")
                        time.sleep(current_delay)
                        current_delay *= backoff
            
            raise last_exception
        return wrapper
    return decorator

@retry(max_attempts=3, delay=1, backoff=2)
def fetch_data(url):
    import requests
    response = requests.get(url, timeout=5)
    response.raise_for_status()
    return response.json()
```

#### **限流装饰器**

```python
import time
import functools
from collections import deque

def rate_limit(max_calls, period):
    """限流装饰器：限制单位时间内的调用次数"""
    def decorator(func):
        call_times = deque(maxlen=max_calls)
        
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            now = time.time()
            
            # 清理过期记录
            while call_times and call_times[0] <= now - period:
                call_times.popleft()
            
            if len(call_times) >= max_calls:
                wait_time = period - (now - call_times[0])
                raise Exception(f"Rate limit exceeded. Wait {wait_time:.2f}s")
            
            call_times.append(now)
            return func(*args, **kwargs)
        return wrapper
    return decorator

@rate_limit(max_calls=5, period=10)
def api_call():
    print("API called")
    return "success"

# 5 次调用后会触发限流
for i in range(6):
    try:
        api_call()
    except Exception as e:
        print(e)
```

### **5. AST 操作与代码生成**

AST（抽象语法树）允许在编译时分析和转换代码。

#### **基础 AST 分析**

```python
import ast

code = """
def add(a, b):
    return a + b

result = add(1, 2)
"""

# 解析为 AST
tree = ast.parse(code)

# 遍历 AST
for node in ast.walk(tree):
    if isinstance(node, ast.FunctionDef):
        print(f"Function: {node.name}")
        print(f"Arguments: {[arg.arg for arg in node.args.args]}")
    elif isinstance(node, ast.Assign):
        print(f"Assignment to: {node.targets[0].id}")
```

#### **AST 转换：自动添加日志**

```python
import ast
import inspect

class LoggingTransformer(ast.NodeTransformer):
    """为每个函数添加日志语句"""
    def visit_FunctionDef(self, node):
        # 创建日志语句
        log_stmt = ast.parse(
            f'print("Calling {node.name}")'
        ).body[0]
        
        # 插入到函数开头
        node.body.insert(0, log_stmt)
        
        return node

code = """
def add(a, b):
    return a + b

def multiply(a, b):
    return a * b
"""

tree = ast.parse(code)
transformer = LoggingTransformer()
new_tree = transformer.visit(tree)

# 编译并执行
exec(compile(new_tree, '<string>', 'exec'))
add(1, 2)  # 输出: Calling add
```

### **6. 猴子补丁（Monkey Patching）**

#### **动态替换方法**

```python
class Original:
    def greet(self):
        return "Hello"

def new_greet(self):
    return "Hi there!"

# 运行时替换方法
Original.greet = new_greet

obj = Original()
print(obj.greet())  # Hi there!
```

#### **__getattr__ 与 __getattribute__**

```python
class LazyLoader:
    """延迟加载属性"""
    def __init__(self):
        self._cache = {}
    
    def __getattr__(self, name):
        """仅在属性不存在时调用"""
        if name not in self._cache:
            print(f"Loading {name}...")
            self._cache[name] = f"data_{name}"
        return self._cache[name]

obj = LazyLoader()
print(obj.foo)  # Loading foo... \n data_foo
print(obj.foo)  # data_foo（从缓存读取）
print(obj.bar)  # Loading bar... \n data_bar
```

```python
class StrictAccess:
    """严格控制属性访问"""
    def __getattribute__(self, name):
        """每次访问属性都调用"""
        print(f"Accessing: {name}")
        return super().__getattribute__(name)

obj = StrictAccess()
obj.x = 10
print(obj.x)  # Accessing: x \n 10
```

### **7. 元编程最佳实践**

✅ **适用场景**：
- ORM 框架（SQLAlchemy、Django Models）
- 插件系统
- API 客户端自动生成
- 序列化工具

❌ **避免使用**：
- 简单任务（增加复杂度）
- 团队不熟悉元编程
- 调试困难的生产环境

⚠️ **注意事项**：
- 文档清晰说明元编程行为
- 提供 fallback 机制
- 考虑性能影响
- 测试覆盖所有边缘情况

---

## **模块与包**

### **分包**

- 模块导入：`import`、`from ... import ...`。
- 包的结构：`__init__.py` 文件的作用。

| 功能/特性                       | 描述                                                                 |
|--------------------------------|----------------------------------------------------------------------|
| **标识包**                     | 明确标识一个目录为 Python 包（Python 3.3 之前是必需的）。              |
| **初始化包**                   | 在包被导入时执行初始化代码。                                          |
| **定义包接口**                 | 使用 `__all__` 控制 `from package import *` 的行为。                  |
| **组织包结构**                 | 简化导入路径，使用户更容易访问包中的内容。                            |
| **隐式命名空间包**             | Python 3.3+ 支持无 `__init__.py` 的包，但显式使用更推荐。              |

### **文件操作（`os`, `sys`, `shutil`）**

### **正则表达式（`re`）**

### **时间与日期（`datetime`, `time`）**

### **数据序列化（`json`, `pickle`）**

## **迭代器与生成器**

在 Python 中，**迭代器（Iterator）** 和 **生成器（Generator）** 是用于处理序列数据的强大工具。它们允许你逐个访问元素，而不需要一次性将所有数据加载到内存中。

### 迭代器协议

在 Python 中，迭代器是遵循迭代器协议的对象。这个协议要求对象实现两个方法：

- `__iter__()`：返回迭代器对象自身。它使得对象可以被用于 `for` 循环和其他需要迭代的地方。
- `__next__()`：返回容器中的下一个值。如果没有更多元素可返回，则抛出 `StopIteration` 异常。

#### 示例

```python
class MyIterator:
    def __init__(self, max_value):
        self.max_value = max_value
        self.current = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self.current < self.max_value:
            value = self.current
            self.current += 1
            return value
        else:
            raise StopIteration

# 使用自定义迭代器
my_iterator = MyIterator(3)
for number in my_iterator:
    print(number)  # 输出: 0, 1, 2
```

#### 内置函数 `iter()` 和 `next()`

- `iter(object)`：返回一个对象的迭代器。如果对象本身就是一个迭代器，`iter()` 返回该对象。否则，调用对象的 `__iter__()` 方法来获取迭代器。
- `next(iterator)`：从迭代器中获取下一个项目。当没有更多项时，会抛出 `StopIteration` 异常。

#### 示例

```python
my_list = [1, 2, 3]
iterator = iter(my_list)

print(next(iterator))  # 输出: 1
print(next(iterator))  # 输出: 2
print(next(iterator))  # 输出: 3
# print(next(iterator))  # 抛出 StopIteration 异常
```

### 生成器

生成器是一种特殊的迭代器，通过使用 `yield` 关键字来创建。与普通函数不同的是，生成器不会一次返回所有结果，而是每次遇到 `yield` 语句时暂停执行并返回一个值，直到下一次调用 `next()` 继续执行。

#### 使用 `yield` 关键字

```python
def simple_generator():
    yield 1
    yield 2
    yield 3

gen = simple_generator()
print(next(gen))  # 输出: 1
print(next(gen))  # 输出: 2
print(next(gen))  # 输出: 3
# print(next(gen))  # 抛出 StopIteration 异常
```

#### 生成器表达式

类似于列表推导式，生成器表达式提供了一种简洁的方式来创建生成器。不过，与列表推导式不同，生成器表达式使用圆括号而不是方括号，并且只在需要时计算值，从而节省内存。

#### 示例

```python
# 列表推导式
squares_list = [x * x for x in range(5)]
print(squares_list)  # 输出: [0, 1, 4, 9, 16]

# 生成器表达式
squares_gen = (x * x for x in range(5))
print(next(squares_gen))  # 输出: 0
print(next(squares_gen))  # 输出: 1
# 可以继续调用 next() 直到 StopIteration
```

## **装饰器**

装饰器是 Python 中一种强大的工具，用于在不修改原函数或类代码的情况下，动态地增强其功能。装饰器可以应用于函数、方法和类，分别称为**函数装饰器**和**类装饰器**。

---

### **装饰器的核心原理**

装饰器本质上是一个**高阶函数**，即一个接受函数（或类）作为参数并返回一个新的函数（或类）的可调用对象。装饰器的核心思想是通过包装原始对象来扩展其行为。

```python
# 装饰器的基本结构
def decorator(original):
    def wrapper(*args, **kwargs):
        # 增强逻辑
        result = original(*args, **kwargs)
        return result
    return wrapper
```

- `original` 是被装饰的函数或类。
- `wrapper` 是包装后的函数或类。
- `*args` 和 `**kwargs` 用于支持任意数量和类型的参数传递。

---

### **函数装饰器**

函数装饰器用于修饰函数或方法的行为。它是最常见的装饰器形式，适用于日志记录、性能测试、输入验证等场景。

#### **基本示例**

以下是一个简单的函数装饰器，用于打印函数调用信息：

```python
def log(func):
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__} with args={args}, kwargs={kwargs}")
        return func(*args, **kwargs)
    return wrapper

@log
def add(a, b):
    return a + b

result = add(3, 5)
print(f"Result: {result}")
```

**输出：**

```
Calling add with args=(3, 5), kwargs={}
Result: 8
```

#### **带参数的函数装饰器**

如果需要让装饰器本身也接受参数，可以通过再嵌套一层函数实现：

```python
def log_with_message(message):
    def decorator(func):
        def wrapper(*args, **kwargs):
            print(f"{message}: Calling {func.__name__}")
            return func(*args, **kwargs)
        return wrapper
    return decorator

@log_with_message("INFO")
def greet(name):
    print(f"Hello, {name}")

greet("Alice")
```

**输出：**

```
INFO: Calling greet
Hello, Alice
```

#### **使用 `functools.wraps`**

当使用装饰器时，原始函数的元数据（如 `__name__` 和 `__doc__`）可能会丢失。为了解决这个问题，可以使用 `functools.wraps` 来保留这些信息：

```python
from functools import wraps

def log(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

@log
def add(a, b):
    """Add two numbers."""
    return a + b

print(add.__name__)  # 输出: add
print(add.__doc__)   # 输出: Add two numbers.
```

---

### **类装饰器**

类装饰器用于修饰类，能够动态地修改类定义或添加额外的功能。与函数装饰器类似，类装饰器也是一个接受类作为参数的可调用对象。

#### **基本示例**

以下是一个简单的类装饰器，用于为类添加属性和方法：

```python
def add_info(cls):
    cls.new_attribute = "This is a new attribute"
    
    def new_method(self):
        print("This is a new method")
    
    cls.new_method = new_method
    return cls

@add_info
class Person:
    def __init__(self, name):
        self.name = name

p = Person("Alice")
print(p.new_attribute)  # 输出: This is a new attribute
p.new_method()          # 输出: This is a new method
```

#### **修改类的方法**

类装饰器还可以用于修改类的现有方法。例如，在方法调用前后打印日志：

```python
def log_methods(cls):
    for name, method in cls.__dict__.items():
        if callable(method):  # 检查是否为方法
            def make_wrapper(m):
                def wrapper(*args, **kwargs):
                    print(f"Calling method: {m.__name__}")
                    return m(*args, **kwargs)
                return wrapper
            
            setattr(cls, name, make_wrapper(method))
    return cls

@log_methods
class Math:
    def add(self, a, b):
        return a + b
    
    def multiply(self, a, b):
        return a * b

m = Math()
print(m.add(3, 5))       # 输出: Calling method: add \n 8
print(m.multiply(3, 5))  # 输出: Calling method: multiply \n 15
```

#### **自动注册类**

类装饰器常用于将类自动注册到某个全局字典中，便于后续管理：

```python
registry = {}

def register(cls):
    registry[cls.__name__] = cls
    return cls

@register
class Person:
    pass

@register
class Car:
    pass

print(registry)  # 输出: {'Person': <class '__main__.Person'>, 'Car': <class '__main__.Car'>}
```

---

### **装饰器的延展应用**

#### **1. 性能测试装饰器**

以下是一个用于测量函数执行时间的装饰器：

```python
import time

def timer(func):
    def wrapper(*args, **kwargs):
        start_time = time.time()
        result = func(*args, **kwargs)
        end_time = time.time()
        print(f"Execution time: {end_time - start_time:.4f} seconds")
        return result
    return wrapper

@timer
def slow_function():
    time.sleep(2)

slow_function()

#类和方法一起处理
def count_time(func_or_cls):
    # 如果是函数
    if isfunction(func_or_cls):
        @wraps(func_or_cls)
        def wrapper(*args, **kwargs):
            start = time.time()
            result = func_or_cls(*args, **kwargs)
            end = time.time()
            print(f"{func_or_cls.__name__} cost {end - start:.6f}s")
            return result
        return wrapper
    # 如果是类
    elif isclass(func_or_cls):
        cls = func_or_cls
        for name, method in vars(cls).items():
            if callable(method) and not (name.startswith("__") and name.endswith("__")):
                setattr(cls, name, count_time(method))
        return cls
    else:
        raise TypeError("count_time can only decorate functions or classes.")
```

#### **2. 缓存装饰器**

Python 提供了内置的 `functools.lru_cache` 装饰器，用于缓存函数的结果以提高性能：

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(10))  # 输出: 55
```

#### **3. 权限校验装饰器**

以下是一个用于检查用户权限的装饰器：

```python
def require_permission(permission):
    def decorator(func):
        def wrapper(user, *args, **kwargs):
            if permission in user.permissions:
                return func(user, *args, **kwargs)
            raise PermissionError(f"User does not have {permission} permission")
        return wrapper
    return decorator

class User:
    def __init__(self, permissions):
        self.permissions = permissions

@require_permission("admin")
def delete_resource(user):
    print("Resource deleted")

user = User(["admin"])
delete_resource(user)  # 输出: Resource deleted
```

---

### **总结**

1. **装饰器的核心**：
   - 高阶函数（接受函数或类作为参数，并返回新的函数或类）。
   - 动态增强功能，无需修改原始代码。

2. **函数装饰器**：
   - 适用于函数或方法。
   - 常见用途：日志记录、性能测试、输入验证等。

3. **类装饰器**：
   - 适用于类。
   - 常见用途：自动注册、接口检查、动态扩展类行为。

4. **高级特性**：
   - 使用 `functools.wraps` 保留函数元数据。
   - 结合缓存、权限校验等功能实现复杂逻辑。

## **上下文管理器**

- 使用 `with` 语句。

    ```python
    # 不使用 with 语句
    file = open('example.txt', 'r')
    try:
        content = file.read()
        print(content)
    finally:
        file.close()

    # 使用 with 语句
    with open('example.txt', 'r') as file:
        content = file.read()
        print(content)
    ```

- 自定义上下文管理器：
  - 实现 `__enter__` 和 `__exit__` 方法。
  
  ```python
    class TemporaryFile:
        def __init__(self, filename):
            self.filename = filename

        def __enter__(self):
            # 进入上下文时打开文件
            self.file = open(self.filename, 'w')
            return self.file

        def __exit__(self, exc_type, exc_value, traceback):
            #exc_type是异常类型，exc_value是异常值，traceback是异常的堆栈跟踪
            # 退出上下文时关闭文件
            self.file.close()
            print("File closed.")

    # 使用自定义上下文管理器
    with TemporaryFile('temp.txt') as f:
        f.write("Hello, World!")
   ```

  - 使用 `contextlib` 模块。
  
    contextlib.contextmanager 是一个装饰器，允许你通过生成器函数快速创建上下文管理器。

    ```python
    from contextlib import contextmanager
    @contextmanager
    def temporary_file(filename):
        try:
            file = open(filename, 'w')
            yield file  # 将文件对象传递给 with 语句
        finally:
            file.close()
            print("File closed.")

    # 使用上下文管理器
    with temporary_file('temp.txt') as f:
        f.write("Hello, World!")
    ```

---

# **现代 Python 特性（3.8+）**

本章节介绍 Python 3.8 及以上版本引入的重要新特性，帮助开发者编写更简洁、更安全、更具表达力的代码。

## **模式匹配（Pattern Matching, Python 3.10+）**

模式匹配是 Python 3.10 引入的强大功能，通过 `match-case` 语句实现结构化数据解构和条件分支。

### **基础语法**

```python
def http_status_description(status_code: int) -> str:
    match status_code:
        case 200:
            return "OK"
        case 404:
            return "Not Found"
        case 500:
            return "Internal Server Error"
        case _:  # 通配符，类似 default
            return "Unknown Status"

print(http_status_description(404))  # 输出: Not Found
```

### **结构化模式匹配**

#### **列表模式**

```python
def process_command(command: list[str]) -> str:
    match command:
        case ["quit"]:
            return "Exiting..."
        case ["load", filename]:
            return f"Loading {filename}"
        case ["save", filename]:
            return f"Saving {filename}"
        case ["move", x, y]:
            return f"Moving to ({x}, {y})"
        case _:
            return "Unknown command"

print(process_command(["load", "data.txt"]))  # 输出: Loading data.txt
```

#### **字典模式**

```python
def handle_event(event: dict) -> str:
    match event:
        case {"type": "click", "x": x, "y": y}:
            return f"Click at ({x}, {y})"
        case {"type": "keypress", "key": key}:
            return f"Key pressed: {key}"
        case {"type": "resize", "width": w, "height": h}:
            return f"Resized to {w}x{h}"
        case _:
            return "Unknown event"

event = {"type": "click", "x": 100, "y": 200}
print(handle_event(event))  # 输出: Click at (100, 200)
```

#### **类实例模式**

```python
from dataclasses import dataclass

@dataclass
class Point:
    x: int
    y: int

@dataclass
class Circle:
    center: Point
    radius: float

def describe_shape(shape) -> str:
    match shape:
        case Point(x=0, y=0):
            return "Point at origin"
        case Point(x=x, y=y):
            return f"Point at ({x}, {y})"
        case Circle(center=Point(x=0, y=0), radius=r):
            return f"Circle at origin with radius {r}"
        case Circle(center=c, radius=r):
            return f"Circle at ({c.x}, {c.y}) with radius {r}"
        case _:
            return "Unknown shape"

p = Point(3, 4)
c = Circle(Point(0, 0), 5.0)
print(describe_shape(p))  # 输出: Point at (3, 4)
print(describe_shape(c))  # 输出: Circle at origin with radius 5.0
```

### **守卫条件（Guard Clauses）**

```python
def classify_number(n: int) -> str:
    match n:
        case _ if n < 0:
            return "Negative"
        case 0:
            return "Zero"
        case _ if n % 2 == 0:
            return "Positive Even"
        case _:
            return "Positive Odd"

print(classify_number(-5))   # 输出: Negative
print(classify_number(4))    # 输出: Positive Even
print(classify_number(7))    # 输出: Positive Odd
```

### **实战示例：解析 API 响应**

```python
from typing import Any

def parse_api_response(response: dict[str, Any]) -> str:
    """根据 API 响应结构进行不同处理"""
    match response:
        case {"status": "success", "data": data}:
            return f"Success: {data}"
        case {"status": "error", "code": code, "message": msg}:
            return f"Error {code}: {msg}"
        case {"status": "redirect", "url": url}:
            return f"Redirect to: {url}"
        case {"status": _, "details": details} if isinstance(details, dict):
            return f"Status with details: {details}"
        case _:
            return "Invalid response format"

# 测试不同响应
responses = [
    {"status": "success", "data": {"user": "Alice"}},
    {"status": "error", "code": 404, "message": "User not found"},
    {"status": "redirect", "url": "https://example.com"},
]

for resp in responses:
    print(parse_api_response(resp))
```

### **最佳实践与陷阱**

- ✅ **适用场景**：复杂数据结构解构、状态机实现、AST 遍历
- ❌ **避免滥用**：简单 if-elif 足够时不要使用 match-case
- ⚠️ **注意**：模式匹配不会自动转换类型，需确保数据类型一致
- ⚠️ **性能**：对于大量简单分支，if-elif 可能更快

---

## **海象运算符（Walrus Operator, Python 3.8+）**

海象运算符 `:=` 允许在表达式中进行赋值，减少重复计算和代码冗余。

### **基本用法**

```python
# 传统写法：需要两次调用
import re
pattern = r'\d+'
text = "abc123def456"
match = re.search(pattern, text)
if match:
    print(f"Found: {match.group()}")

# 使用海象运算符：一次调用
if (match := re.search(pattern, text)):
    print(f"Found: {match.group()}")
```

### **在 while 循环中的应用**

```python
# 读取文件直到空行
with open('data.txt', 'r') as f:
    while (line := f.readline().strip()):
        print(f"Processing: {line}")

# 处理用户输入
while (user_input := input("Enter command (or 'quit'): ")) != 'quit':
    print(f"Executing: {user_input}")
```

### **在列表推导式中的应用**

```python
import math

# 传统写法：重复计算
numbers = [1, 4, 9, 16, 25]
filtered = [math.sqrt(n) for n in numbers if math.sqrt(n) > 2]

# 使用海象运算符：避免重复计算
filtered = [y for n in numbers if (y := math.sqrt(n)) > 2]
print(filtered)  # 输出: [3.0, 4.0, 5.0]
```

### **正则表达式匹配提取**

```python
import re

text = "Email: user@example.com, Phone: 123-456-7890"

# 提取并验证多个模式
patterns = [
    r'Email: (\S+@\S+\.\S+)',
    r'Phone: (\d{3}-\d{3}-\d{4})',
]

for pattern in patterns:
    if (match := re.search(pattern, text)):
        print(f"Found: {match.group(1)}")
```

### **最佳实践**

- ✅ **适用场景**：避免重复函数调用、简化 while 循环、列表推导式优化
- ❌ **避免**：嵌套过深、降低可读性的复杂表达式
- ⚠️ **优先级**：海象运算符优先级较低，必要时使用括号明确意图

```python
# ❌ 不推荐：可读性差
if (result := some_function()) and (value := result.get('key')):
    pass

# ✅ 推荐：分步赋值
result = some_function()
if result and (value := result.get('key')):
    pass
```

---

## **位置参数与关键字参数增强**

### **强制位置参数（Python 3.8+）**

使用 `/` 分隔符强制某些参数只能通过位置传递：

```python
def power(base, exponent, /):
    """base 和 exponent 必须是位置参数"""
    return base ** exponent

print(power(2, 3))       # ✅ 正确: 8
# print(power(base=2, exponent=3))  # ❌ TypeError

def greet(name, /, greeting="Hello"):
    """name 必须位置传递，greeting 可以关键字传递"""
    return f"{greeting}, {name}!"

print(greet("Alice"))              # ✅ Hello, Alice!
print(greet("Alice", greeting="Hi"))  # ✅ Hi, Alice!
# print(greet(name="Alice"))       # ❌ TypeError
```

### **强制关键字参数**

使用 `*` 分隔符强制某些参数只能通过关键字传递：

```python
def create_user(username, *, email, age):
    """email 和 age 必须是关键字参数"""
    return {"username": username, "email": email, "age": age}

user = create_user("alice", email="alice@example.com", age=30)
print(user)
# ✅ {'username': 'alice', 'email': 'alice@example.com', 'age': 30}

# create_user("alice", "alice@example.com", 30)  # ❌ TypeError
```

### **完整签名设计**

```python
def complex_function(pos1, pos2, /, normal1, normal2, *, kwonly1, kwonly2="default"):
    """
    - pos1, pos2: 仅位置参数
    - normal1, normal2: 位置或关键字均可
    - kwonly1, kwonly2: 仅关键字参数
    """
    pass

# 正确调用
complex_function(1, 2, 3, 4, kwonly1=5, kwonly2=6)
complex_function(1, 2, normal1=3, normal2=4, kwonly1=5)
```

### **最佳实践**

- ✅ **位置参数**：用于语义明确的参数（如 `pow(base, exp)`）
- ✅ **关键字参数**：用于可选配置、布尔标志、多参数函数
- ⚠️ **API 设计**：公共库 API 建议使用关键字参数提高可读性

---

## **联合类型与新语法（Python 3.10+）**

### **联合类型简写**

```python
# Python 3.9 及之前
from typing import Union
def process(value: Union[int, str]) -> Union[int, str]:
    return value

# Python 3.10+：使用 | 运算符
def process(value: int | str) -> int | str:
    return value

# 在 isinstance 检查中使用
def handle(data: int | str | None) -> str:
    if isinstance(data, int):
        return f"Integer: {data}"
    elif isinstance(data, str):
        return f"String: {data}"
    else:
        return "None"
```

### **类型别名新语法（Python 3.12+）**

```python
# Python 3.11 及之前
from typing import TypeAlias
UserId: TypeAlias = int
UserName: TypeAlias = str

# Python 3.12+：直接使用 type 语句
type UserId = int
type UserName = str
type JsonValue = int | float | str | bool | None | list["JsonValue"] | dict[str, "JsonValue"]
```

---

## **其他实用新特性**

### **字典合并运算符（Python 3.9+）**

```python
dict1 = {"a": 1, "b": 2}
dict2 = {"b": 3, "c": 4}

# 合并字典（创建新字典）
merged = dict1 | dict2
print(merged)  # {'a': 1, 'b': 3, 'c': 4}

# 原地更新
dict1 |= dict2
print(dict1)  # {'a': 1, 'b': 3, 'c': 4}

# 等价于（但更简洁）
merged_old = {**dict1, **dict2}
```

### **f-string 调试表达式（Python 3.8+）**

```python
name = "Alice"
age = 30
score = 95.5

# 传统写法
print(f"name={name}, age={age}, score={score}")

# 使用 = 修饰符（自动显示变量名和值）
print(f"{name=}, {age=}, {score=}")
# 输出: name='Alice', age=30, score=95.5

# 支持表达式
items = [1, 2, 3, 4, 5]
print(f"{len(items)=}")  # len(items)=5
print(f"{sum(items)=}")  # sum(items)=15
```

### **时区处理（zoneinfo, Python 3.9+）**

```python
from datetime import datetime
from zoneinfo import ZoneInfo

# 创建带时区的日期时间
utc_now = datetime.now(ZoneInfo("UTC"))
beijing_now = datetime.now(ZoneInfo("Asia/Shanghai"))
new_york_now = datetime.now(ZoneInfo("America/New_York"))

print(f"UTC: {utc_now}")
print(f"Beijing: {beijing_now}")
print(f"New York: {new_york_now}")

# 时区转换
utc_time = datetime(2024, 1, 1, 12, 0, tzinfo=ZoneInfo("UTC"))
beijing_time = utc_time.astimezone(ZoneInfo("Asia/Shanghai"))
print(f"UTC 12:00 in Beijing: {beijing_time}")  # 20:00
```

### **移除前缀和后缀（Python 3.9+）**

```python
text = "Hello, World!"
print(text.removeprefix("Hello, "))  # World!
print(text.removesuffix(" World!"))  # Hello,

# 不匹配时返回原字符串
print(text.removeprefix("Goodbye"))  # Hello, World!

# 实用场景：清理 URL
url = "https://example.com/api/v1/users"
api_base = url.removeprefix("https://").removesuffix("/users")
print(api_base)  # example.com/api/v1
```

### **数学模块新功能（Python 3.8+）**

```python
import math

# 最大公约数（支持多个数）
print(math.gcd(12, 18, 24))  # 6

# 最小公倍数
print(math.lcm(4, 6, 8))  # 24

# 排列组合
print(math.perm(5, 2))  # 20 (P(5,2))
print(math.comb(5, 2))  # 10 (C(5,2))

# 距离计算
print(math.dist([0, 0], [3, 4]))  # 5.0
```

---

# **高级特性与工具**

这部分展示了 Python 在实际开发中的强大能力，尤其是在解决复杂问题时的应用。


## **线程并发与同步**

### **1. 多线程的基本概念**

- **线程**：线程是操作系统能够调度的最小单元。一个进程可以包含多个线程，这些线程共享进程的内存空间。
- **多线程**：在一个进程中创建多个线程，每个线程执行不同的任务，从而实现并发。

Python 的 `threading` 模块提供了对线程的支持，但由于 GIL（全局解释器锁）的存在，Python 的多线程在 CPU 密集型任务中并不能真正实现并行计算，但在 I/O 密集型任务中表现良好。

### **2. `threading` 模块的核心内容**

#### （1）创建线程

可以通过以下两种方式创建线程：

- **继承 `Thread` 类**：自定义一个类继承 `threading.Thread`，重写其 `run()` 方法。
- **使用 `Thread` 构造函数**：直接将目标函数传递给 `Thread` 构造函数。

- 示例 1：继承 `Thread` 类

```python
import threading
import time

class MyThread(threading.Thread):
    def __init__(self, name, delay):
        super().__init__()
        self.name = name
        self.delay = delay

    def run(self):
        print(f"Thread {self.name} started.")
        for i in range(5):
            time.sleep(self.delay)
            print(f"{self.name}: {i}")
        print(f"Thread {self.name} finished.")

# 创建线程实例
thread1 = MyThread("Thread-1", 1)
thread2 = MyThread("Thread-2", 2)

# 启动线程
thread1.start()
thread2.start()

# 等待线程完成
thread1.join()
thread2.join()

print("All threads finished.")
```

- 示例 2：使用 `Thread` 构造函数

```python
import threading
import time

def worker(name, delay):
    print(f"Thread {name} started.")
    for i in range(5):
        time.sleep(delay)
        print(f"{name}: {i}")
    print(f"Thread {name} finished.")

# 创建线程
thread1 = threading.Thread(target=worker, args=("Thread-1", 1))
thread2 = threading.Thread(target=worker, args=("Thread-2", 2))

# 启动线程
thread1.start()
thread2.start()

# 等待线程完成
thread1.join()
thread2.join()

print("All threads finished.")
```

---

#### （2）线程管理方法

`threading.Thread` 提供了一些常用的方法来管理线程：

- `start()`：启动线程，调用线程的 `run()` 方法。
- `join([timeout])`：阻塞主线程，直到子线程完成（或超时）。
- `is_alive()`：检查线程是否还在运行。
- `getName()` 和 `setName(name)`：获取或设置线程名称。

- 示例：线程状态检查

```python
import threading
import time

def worker():
    print(f"Thread {threading.current_thread().name} is running.")
    time.sleep(2)
    print(f"Thread {threading.current_thread().name} is done.")

thread = threading.Thread(target=worker, name="MyWorkerThread")
thread.start()

print(f"Is thread alive? {thread.is_alive()}")
thread.join()
print(f"Is thread alive? {thread.is_alive()}")
```

---

#### （3）线程同步

当多个线程访问共享资源时，可能会出现竞争条件（Race Condition）。为了解决这个问题，可以使用以下同步机制：

- **Lock**：互斥锁，确保同一时间只有一个线程访问共享资源。
- **RLock**：可重入锁，允许同一个线程多次获取锁。

- **Condition**：条件变量，用于线程间的通信。

    ```python
    import threading

    # 创建一个条件变量
    condition = threading.Condition()

    # 共享资源
    shared_resource = False

    def consumer():
        global shared_resource
        with condition:  # 获取条件变量的锁
            print("Consumer is waiting...")
            while not shared_resource:  # 等待条件满足
                condition.wait()  # 类似于 Java 的 wait()
            print("Consumer found the resource ready!")

    def producer():
        global shared_resource
        with condition:  # 获取条件变量的锁
            print("Producer is preparing the resource...")
            shared_resource = True
            condition.notify()  # 唤醒等待的线程，类似于 Java 的 notify()

    # 创建线程
    t1 = threading.Thread(target=consumer)
    t2 = threading.Thread(target=producer)

    # 启动线程
    t1.start()
    t2.start()

    # 等待线程完成
    t1.join()
    t2.join()
    ```

- **Semaphore**：信号量，控制同时访问资源的线程数量。

- 示例：使用 Lock

```python
import threading

# 共享资源
counter = 0
lock = threading.Lock()

def increment():
    global counter
    for _ in range(100000):
        with lock:  # 加锁
            counter += 1

# 创建线程
thread1 = threading.Thread(target=increment)
thread2 = threading.Thread(target=increment)

# 启动线程
thread1.start()
thread2.start()

# 等待线程完成
thread1.join()
thread2.join()

print(f"Final counter value: {counter}")
```

---

#### （4）守护线程（Daemon Thread）

守护线程是一种后台线程，当主线程结束时，守护线程会自动退出。可以通过设置 `daemon=True` 来创建守护线程。

- 示例：守护线程

```python
import threading
import time

def daemon_worker():
    while True:
        print("Daemon thread is running...")
        time.sleep(1)

# 创建守护线程
daemon_thread = threading.Thread(target=daemon_worker, daemon=True)
daemon_thread.start()

print("Main thread is running...")
time.sleep(3)
print("Main thread finished.")
```

输出：

```
Main thread is running...
Daemon thread is running...
Daemon thread is running...
Daemon thread is running...
Main thread finished.
```

注意：守护线程会在主线程结束后自动终止。

---

### **3. 多线程的适用场景**

- **I/O 密集型任务**：如文件读写、网络请求等。由于线程在等待 I/O 操作时会释放 GIL，因此多线程在这种场景下非常有效。
- **GUI 应用程序**：保持界面响应的同时执行后台任务。
- **轻量级任务**：如简单的并发任务。

---

### **4. 注意事项**

1. **GIL 的限制**：
   - Python 的 GIL 使得多线程在 CPU 密集型任务中无法真正并行。如果需要并行计算，可以考虑使用 `multiprocessing` 模块。

2. **线程安全**：
   - 在多线程环境中，访问共享资源时必须加锁，否则可能会导致数据不一致。

3. **调试复杂性**：
   - 多线程程序的调试比单线程程序更复杂，容易出现死锁、竞争条件等问题。

---

### **5. 生产者-消费者模型实战**

```python
import threading
import queue
import time
import random

def producer(q: queue.Queue, num_items: int):
    """生产者：生成数据放入队列"""
    for i in range(num_items):
        item = f"item_{i}"
        q.put(item)
        print(f"Produced: {item}")
        time.sleep(random.uniform(0.1, 0.5))
    q.put(None)  # 发送结束信号

def consumer(q: queue.Queue, worker_id: int):
    """消费者：从队列获取数据处理"""
    while True:
        item = q.get()
        if item is None:
            q.put(None)  # 传递给其他消费者
            break
        print(f"Worker {worker_id} consumed: {item}")
        time.sleep(random.uniform(0.2, 0.8))
        q.task_done()

# 创建队列（线程安全）
q = queue.Queue(maxsize=10)

# 启动生产者和消费者
producer_thread = threading.Thread(target=producer, args=(q, 5))
consumer_threads = [
    threading.Thread(target=consumer, args=(q, i))
    for i in range(2)
]

for t in consumer_threads:
    t.start()
producer_thread.start()

producer_thread.join()
for t in consumer_threads:
    t.join()

print("All tasks completed")
```

---

## **多进程编程（multiprocessing）**

由于 GIL 的存在，Python 多线程无法充分利用多核 CPU。`multiprocessing` 模块通过创建独立进程实现真正的并行计算，适合 CPU 密集型任务。

### **1. 核心组件**

#### **Process：创建进程**

```python
from multiprocessing import Process
import os
import time

def worker(name: str, duration: float):
    """工作函数"""
    print(f"Process {name} (PID: {os.getpid()}) started")
    time.sleep(duration)
    print(f"Process {name} finished")

if __name__ == "__main__":
    # 创建进程
    p1 = Process(target=worker, args=("Task-1", 2))
    p2 = Process(target=worker, args=("Task-2", 3))

    # 启动进程
    p1.start()
    p2.start()

    # 等待完成
    p1.join()
    p2.join()

    print("All processes completed")
```

> ⚠️ **重要**：在 Windows 上必须使用 `if __name__ == "__main__":` 保护，避免递归创建进程。

#### **Pool：进程池**

```python
from multiprocessing import Pool
import time

def square(n: int) -> int:
    """计算平方（模拟 CPU 密集型任务）"""
    time.sleep(1)  # 模拟耗时计算
    return n * n

if __name__ == "__main__":
    numbers = [1, 2, 3, 4, 5, 6, 7, 8]

    # 方法 1：map（保持顺序）
    with Pool(processes=4) as pool:
        results = pool.map(square, numbers)
        print(f"Results: {results}")

    # 方法 2：imap（惰性求值，节省内存）
    with Pool(processes=4) as pool:
        for result in pool.imap(square, numbers):
            print(f"Got: {result}")

    # 方法 3：apply_async（异步，支持回调）
    with Pool(processes=4) as pool:
        async_results = [pool.apply_async(square, (n,)) for n in numbers]
        for ar in async_results:
            print(f"Result: {ar.get()}")  # get() 阻塞直到完成
```

### **2. 进程间通信（IPC）**

#### **Queue：进程安全队列**

```python
from multiprocessing import Process, Queue

def producer(q: Queue):
    """生产者进程"""
    for i in range(5):
        q.put(f"message_{i}")
        print(f"Sent: message_{i}")
    q.put(None)  # 结束信号

def consumer(q: Queue):
    """消费者进程"""
    while True:
        msg = q.get()
        if msg is None:
            break
        print(f"Received: {msg}")

if __name__ == "__main__":
    q = Queue()
    p1 = Process(target=producer, args=(q,))
    p2 = Process(target=consumer, args=(q,))

    p1.start()
    p2.start()
    p1.join()
    p2.join()
```

#### **Pipe：双向管道**

```python
from multiprocessing import Process, Pipe

def sender(conn):
    """发送端"""
    for i in range(3):
        conn.send(f"data_{i}")
        print(f"Sent: data_{i}")
    conn.close()

def receiver(conn):
    """接收端"""
    while True:
        try:
            data = conn.recv()
            print(f"Received: {data}")
        except EOFError:
            break

if __name__ == "__main__":
    parent_conn, child_conn = Pipe()
    p1 = Process(target=sender, args=(parent_conn,))
    p2 = Process(target=receiver, args=(child_conn,))

    p1.start()
    p2.start()
    p1.join()
    p2.join()
```

#### **共享内存：Value 和 Array**

```python
from multiprocessing import Process, Value, Array

def increment(counter: Value, items: Array):
    """修改共享变量"""
    with counter.get_lock():  # 加锁防止竞态条件
        counter.value += 1
    
    for i in range(len(items)):
        items[i] = items[i] * 2

if __name__ == "__main__":
    # 共享整数（'i' 表示 int 类型）
    counter = Value('i', 0)
    
    # 共享数组（'d' 表示 double 类型）
    items = Array('d', [1.0, 2.0, 3.0, 4.0])

    processes = [Process(target=increment, args=(counter, items)) for _ in range(3)]
    
    for p in processes:
        p.start()
    for p in processes:
        p.join()

    print(f"Counter: {counter.value}")      # 3
    print(f"Items: {list(items)}")          # [8.0, 16.0, 24.0, 32.0]
```

#### **Manager：高级共享对象**

```python
from multiprocessing import Process, Manager

def modify_shared_data(shared_dict: dict, shared_list: list):
    """修改管理器创建的共享对象"""
    shared_dict["key"] = "value"
    shared_list.append("item")

if __name__ == "__main__":
    with Manager() as manager:
        # 创建共享字典和列表
        shared_dict = manager.dict()
        shared_list = manager.list()

        processes = [
            Process(target=modify_shared_data, args=(shared_dict, shared_list))
            for _ in range(3)
        ]

        for p in processes:
            p.start()
        for p in processes:
            p.join()

        print(f"Dict: {dict(shared_dict)}")
        print(f"List: {list(shared_list)}")
```

> ⚠️ **性能提示**：Manager 基于代理机制，速度比 Value/Array 慢，但支持更多数据类型。

### **3. 实战：CPU 密集型任务并行化**

```python
from multiprocessing import Pool
import time
import math

def is_prime(n: int) -> bool:
    """判断素数（CPU 密集型）"""
    if n < 2:
        return False
    if n == 2:
        return True
    if n % 2 == 0:
        return False
    for i in range(3, int(math.sqrt(n)) + 1, 2):
        if n % i == 0:
            return False
    return True

def find_primes_in_range(range_start: int, range_end: int) -> list[int]:
    """在范围内查找所有素数"""
    return [n for n in range(range_start, range_end) if is_prime(n)]

if __name__ == "__main__":
    # 串行执行
    start_time = time.time()
    ranges = [(2, 10000), (10000, 20000), (20000, 30000), (30000, 40000)]
    serial_results = []
    for start, end in ranges:
        serial_results.extend(find_primes_in_range(start, end))
    serial_time = time.time() - start_time
    print(f"Serial: {len(serial_results)} primes found in {serial_time:.2f}s")

    # 并行执行
    start_time = time.time()
    with Pool(processes=4) as pool:
        parallel_results = pool.starmap(find_primes_in_range, ranges)
        all_primes = [p for sublist in parallel_results for p in sublist]
    parallel_time = time.time() - start_time
    print(f"Parallel: {len(all_primes)} primes found in {parallel_time:.2f}s")
    print(f"Speedup: {serial_time / parallel_time:.2f}x")
```

### **4. 注意事项与最佳实践**

- ✅ **适用场景**：CPU 密集型任务（数值计算、图像处理、数据分析）
- ❌ **不适用**：I/O 密集型任务（使用 threading 或 asyncio）
- ⚠️ **进程开销**：创建进程比线程开销大，使用进程池复用
- ⚠️ **序列化限制**：进程间通信需要 pickle 序列化，不支持 lambda、闭包等
- ⚠️ **全局状态**：每个进程有独立的内存空间，不共享全局变量
- 🔒 **同步原语**：Lock、RLock、Semaphore、Event、Condition 同样可用

---

## **并发 Futures（concurrent.futures）**

`concurrent.futures` 提供了更简洁的高级接口，统一了线程池和进程池的使用方式，是 Python 3.2+ 推荐的并发编程方式。

### **1. Executor 基类**

```python
from concurrent.futures import ThreadPoolExecutor, ProcessPoolExecutor
import time

def task(name: str, duration: float) -> str:
    """模拟任务"""
    time.sleep(duration)
    return f"Task {name} completed in {duration}s"
```

### **2. ThreadPoolExecutor**

```python
from concurrent.futures import ThreadPoolExecutor, as_completed

# 方法 1：submit + Future
with ThreadPoolExecutor(max_workers=3) as executor:
    future1 = executor.submit(task, "A", 2)
    future2 = executor.submit(task, "B", 1)
    future3 = executor.submit(task, "C", 3)

    # 获取结果（阻塞）
    print(future1.result())  # Task A completed in 2s
    print(future2.result())  # Task B completed in 1s
    print(future3.result())  # Task C completed in 3s

# 方法 2：as_completed（按完成顺序处理）
with ThreadPoolExecutor(max_workers=3) as executor:
    futures = {executor.submit(task, name, dur): name 
               for name, dur in [("A", 2), ("B", 1), ("C", 3)]}
    
    for future in as_completed(futures):
        name = futures[future]
        try:
            result = future.result()
            print(f"{name}: {result}")
        except Exception as e:
            print(f"{name} generated exception: {e}")

# 方法 3：map（保持顺序）
with ThreadPoolExecutor(max_workers=3) as executor:
    names = ["A", "B", "C"]
    durations = [2, 1, 3]
    results = executor.map(task, names, durations)
    for result in results:
        print(result)
```

### **3. ProcessPoolExecutor**

```python
from concurrent.futures import ProcessPoolExecutor, as_completed
import math

def compute_factorial(n: int) -> tuple[int, int]:
    """计算阶乘（CPU 密集型）"""
    return (n, math.factorial(n))

if __name__ == "__main__":
    numbers = [100, 200, 300, 400, 500]

    # 使用进程池并行计算
    with ProcessPoolExecutor(max_workers=4) as executor:
        futures = {executor.submit(compute_factorial, n): n for n in numbers}
        
        for future in as_completed(futures):
            n, result = future.result()
            print(f"{n}! has {len(str(result))} digits")
```

### **4. 超时与取消**

```python
from concurrent.futures import ThreadPoolExecutor, TimeoutError, CancelledError
import time

def slow_task(duration: float) -> str:
    time.sleep(duration)
    return f"Completed after {duration}s"

with ThreadPoolExecutor(max_workers=2) as executor:
    future = executor.submit(slow_task, 5)
    
    try:
        # 设置超时
        result = future.result(timeout=2)
        print(result)
    except TimeoutError:
        print("Task timed out!")
        future.cancel()  # 尝试取消（可能失败）
```

### **5. 回调函数**

```python
from concurrent.futures import ThreadPoolExecutor

def on_complete(future):
    """回调函数"""
    try:
        result = future.result()
        print(f"Callback: {result}")
    except Exception as e:
        print(f"Callback: Exception - {e}")

def task(value: int) -> int:
    return value * 2

with ThreadPoolExecutor(max_workers=2) as executor:
    future = executor.submit(task, 21)
    future.add_done_callback(on_complete)
    # 输出: Callback: 42
```

### **6. 实战：批量 HTTP 请求**

```python
from concurrent.futures import ThreadPoolExecutor, as_completed
import requests
from typing import List

def fetch_url(url: str) -> dict:
    """获取 URL 内容"""
    try:
        response = requests.get(url, timeout=5)
        return {
            "url": url,
            "status": response.status_code,
            "length": len(response.text)
        }
    except Exception as e:
        return {"url": url, "error": str(e)}

def batch_fetch(urls: List[str], max_workers: int = 5) -> List[dict]:
    """批量获取 URLs"""
    results = []
    with ThreadPoolExecutor(max_workers=max_workers) as executor:
        future_to_url = {executor.submit(fetch_url, url): url for url in urls}
        
        for future in as_completed(future_to_url):
            result = future.result()
            results.append(result)
            if "error" in result:
                print(f"Failed: {result['url']} - {result['error']}")
            else:
                print(f"Success: {result['url']} ({result['length']} bytes)")
    
    return results

if __name__ == "__main__":
    urls = [
        "https://httpbin.org/get",
        "https://httpbin.org/post",
        "https://httpbin.org/delay/1",
        "https://httpbin.org/status/200",
        "https://httpbin.org/status/404",
    ]
    
    results = batch_fetch(urls)
    print(f"\nTotal: {len(results)} requests completed")
```

---

## **并发模型对比与选择指南**

### **1. 特性对比表**

| 特性 | threading | multiprocessing | concurrent.futures | asyncio |
|------|-----------|-----------------|-------------------|---------|
| **并行性** | 伪并行（GIL 限制） | 真并行 | 取决于 Executor | 单线程并发 |
| **适用场景** | I/O 密集 | CPU 密集 | 通用 | I/O 密集 |
| **内存开销** | 低（共享内存） | 高（独立内存） | 中到高 | 最低 |
| **创建开销** | 低 | 高 | 中 | 极低 |
| **通信机制** | 共享变量/Queue | Queue/Pipe/Manager | Future | await/async |
| **同步原语** | Lock/RLock/Semaphore | Lock/Queue | Future | Lock/Event |
| **复杂度** | 中 | 高 | 低 | 高 |
| **调试难度** | 中 | 高 | 低 | 高 |
| **可扩展性** | 有限 | 好 | 好 | 极好 |

### **2. 选择决策树**

```
开始
 │
 ├─ 任务是 CPU 密集型？
 │   ├─ 是 → 使用 multiprocessing 或 ProcessPoolExecutor
 │   └─ 否 ↓
 │
 ├─ 任务是 I/O 密集型？
 │   ├─ 是 → 并发量 < 100？
 │   │         ├─ 是 → 使用 threading 或 ThreadPoolExecutor
 │   │         └─ 否 → 使用 asyncio
 │   └─ 否 ↓
 │
 └─ 需要简单 API？
     ├─ 是 → 使用 concurrent.futures
     └─ 否 → 根据具体需求选择
```

### **3. 典型应用场景**

#### **threading 适用场景**
- GUI 应用保持响应
- 少量并发网络请求
- 后台监控任务
- 简单的生产者-消费者模型

#### **multiprocessing 适用场景**
- 数值计算（矩阵运算、统计分析）
- 图像处理与视频编码
- 机器学习模型训练
- 大规模数据解析

#### **concurrent.futures 适用场景**
- 批量文件下载/上传
- API 批量调用
- 并行数据处理管道
- 需要统一接口的混合场景

#### **asyncio 适用场景**
- 高并发 Web 服务器
- WebSocket 实时通信
- 微服务间异步调用
- 爬虫框架

### **4. 混合使用示例**

```python
import asyncio
from concurrent.futures import ProcessPoolExecutor
import time

def cpu_intensive_task(n: int) -> int:
    """CPU 密集型计算（在进程中执行）"""
    return sum(i * i for i in range(n))

async def io_task(name: str, duration: float):
    """I/O 密集型任务（在事件循环中执行）"""
    await asyncio.sleep(duration)
    return f"{name} completed"

async def main():
    loop = asyncio.get_event_loop()
    
    # 在线程池中运行 I/O 任务
    io_future = asyncio.create_task(io_task("IO-1", 1))
    
    # 在进程池中运行 CPU 任务
    with ProcessPoolExecutor() as pool:
        cpu_future = loop.run_in_executor(pool, cpu_intensive_task, 10_000_000)
        
        # 并发执行
        io_result, cpu_result = await asyncio.gather(
            io_future,
            cpu_future
        )
        
        print(f"IO Result: {io_result}")
        print(f"CPU Result: {cpu_result}")

if __name__ == "__main__":
    asyncio.run(main())
```

### **5. 常见陷阱与解决方案**

#### **陷阱 1：GIL 误解**
```python
# ❌ 错误认知：多线程能加速 CPU 密集型任务
def cpu_bound():
    return sum(i * i for i in range(10_000_000))

# 多线程不会更快（受 GIL 限制）
# ✅ 正确做法：使用多进程
from multiprocessing import Pool
with Pool() as pool:
    result = pool.apply(cpu_bound)
```

#### **陷阱 2：忘记 join**
```python
# ❌ 可能导致资源泄漏
thread = threading.Thread(target=worker)
thread.start()
# 忘记 thread.join()

# ✅ 始终等待线程完成
thread.start()
thread.join()
```

#### **陷阱 3：共享状态竞态条件**
```python
# ❌ 不安全
counter = 0
def increment():
    global counter
    counter += 1  # 非原子操作

# ✅ 使用锁保护
lock = threading.Lock()
def increment_safe():
    global counter
    with lock:
        counter += 1
```

#### **陷阱 4：asyncio 中阻塞调用**
```python
import time
import asyncio

# ❌ 阻塞整个事件循环
async def bad_example():
    time.sleep(1)  # 阻塞！

# ✅ 使用异步 sleep
async def good_example():
    await asyncio.sleep(1)  # 非阻塞
```

---

## **asyncio 模块**

异步编程是一种编程范式，允许程序在等待某些操作（如 I/O 操作）完成时继续执行其他任务，而不是阻塞整个程序的执行。这种编程方式特别适用于需要处理大量并发任务的场景，例如网络请求、文件读写等。

Python 提供了 `asyncio` 模块来支持异步编程，并通过 `async` 和 `await` 关键字简化了异步代码的编写。

`asyncio` 是 Python 的一个标准库模块，专门用于编写异步代码。它提供了事件循环、协程、任务调度等功能，帮助开发者高效地管理并发任务。

### 核心概念

1. **事件循环 (Event Loop)**:
   - 事件循环是异步编程的核心，负责调度和运行协程。
   - 它会监听所有任务的状态，并在任务准备好时调用它们。

2. **协程 (Coroutine)**:
   - 协程是异步函数的实现形式，使用 `async def` 定义。
   - 协程不会立即执行，而是返回一个协程对象，必须通过事件循环或 `await` 来运行。

3. **任务 (Task)**:
   - 任务是对协程的封装，允许事件循环并发地运行多个协程。

4. **Future**:
   - 表示一个尚未完成的计算结果，通常由协程返回。

---

### `async` 和 `await` 关键字

- **`async`**:
  - 用于定义一个异步函数（协程）。
  - 使用 `async def` 定义的函数会返回一个协程对象，而不是直接执行函数体。

- **`await`**:
  - 用于暂停当前协程的执行，直到等待的操作完成。
  - `await` 后面通常跟另一个协程或一个 `awaitable` 对象（如 `asyncio.sleep`）。

---

### 示例解析

以下是一个简单的异步编程示例：

```python
import asyncio

async def main():
    print("Start")
    await asyncio.sleep(1)  # 模拟一个耗时操作
    print("End")

asyncio.run(main())
```

### 执行流程

1. **定义协程**:
   - `main()` 是一个异步函数，使用 `async def` 定义。
   - 当调用 `main()` 时，它不会立即执行，而是返回一个协程对象。

2. **运行协程**:
   - `asyncio.run(main())` 启动事件循环，并运行 `main()` 协程。
   - 事件循环接管控制权，开始执行 `main()` 中的代码。

3. **执行 `print("Start")`**:
   - 程序首先打印 `"Start"`。

4. **遇到 `await asyncio.sleep(1)`**:
   - `asyncio.sleep(1)` 是一个异步操作，模拟等待 1 秒钟。
   - `await` 关键字暂停 `main()` 协程的执行，并将控制权交还给事件循环。
   - 在这 1 秒内，事件循环可以运行其他任务（如果有）。

5. **恢复协程**:
   - 1 秒后，`asyncio.sleep(1)` 完成，事件循环恢复 `main()` 协程的执行。
   - 程序继续执行 `print("End")`。

6. **结束程序**:
   - 协程执行完毕，事件循环退出。

---

### 异步编程的优势

1. **提高效率**:
   - 异步编程避免了阻塞等待，利用等待时间执行其他任务，从而提高了程序的整体效率。

2. **适合 I/O 密集型任务**:
   - 对于涉及大量 I/O 操作的任务（如网络请求、文件读写），异步编程能显著减少等待时间。

3. **简化并发**:
   - 使用 `asyncio` 可以轻松管理多个并发任务，而无需复杂的线程或进程管理。

---

### 注意事项

1. **不要阻塞事件循环**:
   - 避免在协程中使用阻塞操作（如 `time.sleep`），否则会阻塞整个事件循环。
   - 应该使用非阻塞的替代方法（如 `asyncio.sleep`）。

2. **任务调度**:
   - 如果需要并发执行多个协程，可以使用 `asyncio.gather` 或 `asyncio.create_task`。

3. **调试复杂性**:
   - 异步代码的执行顺序可能不如同步代码直观，调试时需要注意任务的状态和调度。

---

### 更复杂的示例：并发任务

以下示例展示了如何使用 `asyncio` 并发执行多个任务：

```python
import asyncio

async def task(name, delay):
    print(f"Task {name} started")
    await asyncio.sleep(delay)
    print(f"Task {name} finished")

async def main():
    # 创建多个任务并并发执行
    await asyncio.gather(
        task("A", 2),
        task("B", 1),
        task("C", 3)
    )

asyncio.run(main())
```

### 输出结果

```
Task A started
Task B started
Task C started
Task B finished
Task A finished
Task C finished
```

在这个例子中，三个任务并发执行，但由于每个任务的延迟不同，完成的顺序也不同。

---

## **网络编程**

### **1、核心模块与库**

Python提供了多个模块和库来支持网络编程，以下是几个常用的模块：

#### **1.1 `socket` 模块**

`socket` 是Python中最基础的网络编程模块，用于创建和管理网络连接。它支持TCP和UDP协议。

##### **创建TCP服务器**

以下是一个简单的TCP服务器示例：

```python
import socket

# 创建一个socket对象
server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# 绑定IP地址和端口
server_socket.bind(('127.0.0.1', 8080))

# 开始监听
server_socket.listen(5)
print("服务器已启动，等待客户端连接...")

while True:
    # 接受客户端连接
    client_socket, addr = server_socket.accept()
    print(f"客户端已连接，地址：{addr}")

    # 接收数据
    data = client_socket.recv(1024)
    print(f"收到数据：{data.decode()}")

    # 发送响应
    client_socket.send("Hello from server!".encode())

    # 关闭连接
    client_socket.close()
```

##### **创建TCP客户端**

以下是一个对应的TCP客户端示例：

```python
import socket

# 创建一个socket对象
client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# 连接到服务器
client_socket.connect(('127.0.0.1', 8080))

# 发送数据
client_socket.send("Hello from client!".encode())

# 接收响应
response = client_socket.recv(1024)
print(f"服务器响应：{response.decode()}")

# 关闭连接
client_socket.close()
```

#### **1.2 `selectors` 模块**

当需要处理大量并发连接时，可以使用 `selectors` 模块实现高效的I/O多路复用。例如：

```python
import selectors
import socket

sel = selectors.DefaultSelector()

def accept(sock, mask):
    conn, addr = sock.accept()
    print(f"客户端已连接，地址：{addr}")
    conn.setblocking(False)
    sel.register(conn, selectors.EVENT_READ, read)

def read(conn, mask):
    data = conn.recv(1024)
    if data:
        print(f"收到数据：{data.decode()}")
        conn.send(data)  # 回显数据
    else:
        print("关闭连接")
        sel.unregister(conn)
        conn.close()

sock = socket.socket()
sock.bind(('127.0.0.1', 8080))
sock.listen(100)
sock.setblocking(False)
sel.register(sock, selectors.EVENT_READ, accept)

while True:
    events = sel.select()
    for key, mask in events:
        callback = key.data
        callback(key.fileobj, mask)
```

#### **1.3 `asyncio` 模块**

`asyncio` 是Python中用于编写异步代码的核心库，特别适合处理大量并发连接。它基于事件循环机制，能够高效地管理I/O操作。

示例：使用 `asyncio` 编写一个简单的TCP服务器：

```python
import asyncio

async def handle_client(reader, writer):
    data = await reader.read(100)
    message = data.decode()
    addr = writer.get_extra_info('peername')
    print(f"收到数据：{message}，来自：{addr}")
    writer.write(data)
    await writer.drain()
    writer.close()

async def main():
    server = await asyncio.start_server(handle_client, '127.0.0.1', 8080)
    async with server:
        await server.serve_forever()

asyncio.run(main())
```

---

### **2、高级主题**

#### **2.1 HTTP编程**

Python中的 `http.server` 和 `requests` 模块可以用来处理HTTP请求。

##### **用 `http.server` 创建简单HTTP服务器**

```python
from http.server import HTTPServer, BaseHTTPRequestHandler

class SimpleHTTPRequestHandler(BaseHTTPRequestHandler):
    def do_GET(self):
        self.send_response(200)
        self.end_headers()
        self.wfile.write(b"Hello, world!")

httpd = HTTPServer(('127.0.0.1', 8080), SimpleHTTPRequestHandler)
httpd.serve_forever()
```

##### **使用 `requests` 发送HTTP请求**

```python
import requests

response = requests.get('https://www.example.com')
print(response.status_code)
print(response.text)
```

#### **2.2 WebSocket**

WebSocket是一种全双工通信协议，适合实时通信场景。可以使用 `websockets` 库实现WebSocket服务器和客户端。

##### **WebSocket服务器示例**

```python
import asyncio
import websockets

async def echo(websocket, path):
    async for message in websocket:
        print(f"收到消息：{message}")
        await websocket.send(f"Echo: {message}")

start_server = websockets.serve(echo, "127.0.0.1", 8080)

asyncio.get_event_loop().run_until_complete(start_server)
asyncio.get_event_loop().run_forever()
```

##### **WebSocket客户端示例**

```python
import asyncio
import websockets

async def hello():
    uri = "ws://127.0.0.1:8080"
    async with websockets.connect(uri) as websocket:
        await websocket.send("Hello, server!")
        response = await websocket.recv()
        print(f"收到响应：{response}")

asyncio.get_event_loop().run_until_complete(hello())
```

---

### **3、常见问题与解决方案**

#### **3.1 如何处理高并发？**

- 使用多线程或多进程模型（`threading` 或 `multiprocessing`）。
- 使用异步编程（`asyncio`）。
- 使用事件驱动框架（如 `Twisted` 或 `Tornado`）。

#### **3.2 如何确保安全性？**

- 使用SSL/TLS加密通信（`ssl` 模块）。
- 验证客户端身份（如OAuth、JWT）。
- 对敏感数据进行加密存储。

#### **3.3 如何调试网络程序？**

- 使用日志记录（`logging` 模块）。
- 使用抓包工具（如Wireshark）分析网络流量。
- 使用单元测试验证逻辑正确性。

---

## **加密与解密**

加密与解密是计算机科学和密码学领域中的一个重要概念。加密是指将原始信息转换为不可读的格式的过程，而解密则是将加密后的信息恢复为原始信息的过程。加密的目的是为了保护信息免受未经授权的访问和修改。

**示例**

```python
from Crypto.PublicKey import RSA
from Crypto.Cipher import PKCS1_OAEP
from Crypto.Random import get_random_bytes

# 生成 RSA 密钥对
key = RSA.generate(2048)
private_key = key.export_key()
public_key = key.publickey().export_key()

def encrypt_rsa(plaintext, public_key):
    # 导入公钥并创建加密器
    rsa_key = RSA.import_key(public_key)
    cipher = PKCS1_OAEP.new(rsa_key)
    ciphertext = cipher.encrypt(plaintext.encode())
    return ciphertext

def decrypt_rsa(ciphertext, private_key):
    # 导入私钥并创建解密器
    rsa_key = RSA.import_key(private_key)
    cipher = PKCS1_OAEP.new(rsa_key)
    plaintext = cipher.decrypt(ciphertext)
    return plaintext.decode()

# 测试加密和解密
plaintext = "This is a secret message encrypted with RSA!"
print("Original:", plaintext)

ciphertext = encrypt_rsa(plaintext, public_key)
print("Encrypted:", ciphertext)

decrypted_text = decrypt_rsa(ciphertext, private_key)
print("Decrypted:", decrypted_text)
```

对于对称加密和非对称加密，有许多不同的算法可供选择。以下是一些常见的对称加密和非对称加密算法的例子：

### 对称加密算法

1. **AES (Advanced Encryption Standard)**
   - 高级加密标准，是目前最常用的对称加密算法之一。
   - 支持128、192或256位密钥长度。
   - 广泛应用于数据加密，包括文件加密、数据库加密等。

2. **DES (Data Encryption Standard) 和 3DES (Triple DES)**
   - DES是一种较老的对称加密算法，使用56位密钥，由于密钥长度较短，现在已不安全。
   - 3DES通过应用DES三次来增加安全性，但速度较慢，逐渐被AES取代。

3. **ChaCha20**
   - 一种流加密算法，设计用于提高软件实现的速度和安全性。
   - 在移动设备和网络协议中广泛应用，如在TLS 1.3中作为推荐的加密算法之一。

4. **Blowfish 和 Twofish**
   - Blowfish是一个可变密钥大小的块密码算法，支持从32到448位的密钥长度。
   - Twofish是Blowfish的后继者，支持128位块大小和高达256位的密钥长度。

### 非对称加密算法

1. **RSA (Rivest-Shamir-Adleman)**
   - 最早广泛使用的公钥加密技术之一。
   - 常用于数字签名、密钥交换等场合。密钥长度通常为2048位或更高以确保安全性。

2. **ECC (Elliptic Curve Cryptography)**
   - 椭圆曲线密码学，提供与RSA相似的安全性，但所需的密钥长度更短（例如，256位的ECC密钥被认为与3072位的RSA密钥同样安全）。
   - 更适合于资源受限的环境，如移动设备。

3. **DSA (Digital Signature Algorithm)**
   - 主要用于数字签名，而不是通用的数据加密。
   - DSA只能用来创建和验证数字签名，不能用于加密消息本身。

4. **Diffie-Hellman 密钥交换**
   - 虽然不是直接的加密算法，但它提供了一种方法让双方可以安全地建立共享的秘密密钥，而无需事先交换任何秘密信息。
   - 经常与其它加密算法结合使用，尤其是在SSL/TLS协议中用于密钥协商。

## **数据处理与分析**

- **常用库**：
  - NumPy：数组操作。
  - Pandas：数据分析。
  - Matplotlib/Seaborn：数据可视化。
- 数据清洗与预处理。
- 数据聚合与分组。

## **测试与调试**

- 单元测试：`unittest` 或 `pytest`。
- 调试工具：`pdb`。

## **性能优化**

- **代码优化**：
  - 使用内置函数和库替代手动实现。
  - 避免不必要的循环和冗余计算。
- **内存管理**：
  - 理解垃圾回收机制（引用计数、分代回收）。
  - 使用 `gc` 模块手动控制垃圾回收。

| 特性                     | 描述                                                                 |
|--------------------------|----------------------------------------------------------------------|
| **引用计数**             | 快速释放无引用对象，但无法处理循环引用。                            |
| **分代回收**             | 将对象分为三代，按需扫描，优化性能。                                |
| **循环垃圾检测**         | 使用标记-清除算法清理循环引用对象。                                 |
| **优点**                 | 自动化、高效、适合大多数场景。                                      |
| **缺点**                 | 循环引用需要额外的检测开销；手动干预可能导致复杂性增加。            |

---

# **类型提示与静态检查（Type Hints）**

类型提示是 Python 3.5+ 引入的功能（PEP 484），允许为变量、函数参数和返回值添加类型注解。虽然 Python 仍然是动态类型语言，但类型提示能显著提高代码可读性、可维护性，并借助静态检查工具提前发现错误。

## **1. 基础类型注解**

### **基本类型**

```python
# 变量注解
name: str = "Alice"
age: int = 30
height: float = 1.75
is_student: bool = False

# 函数签名注解
def greet(name: str, age: int) -> str:
    return f"Hello, {name}. You are {age} years old."

# 无返回值的函数
def log_message(message: str) -> None:
    print(f"[LOG] {message}")
```

### **容器类型**

```python
from typing import List, Dict, Set, Tuple

# 列表
names: List[str] = ["Alice", "Bob", "Charlie"]
numbers: List[int] = [1, 2, 3, 4, 5]

# 字典
user_scores: Dict[str, int] = {"Alice": 95, "Bob": 87}

# 集合
unique_ids: Set[int] = {1, 2, 3, 4, 5}

# 元组（固定长度）
coordinate: Tuple[float, float] = (10.5, 20.3)
person_info: Tuple[str, int, float] = ("Alice", 30, 1.75)

# 可变长度元组
int_tuple: Tuple[int, ...] = (1, 2, 3, 4, 5)
```

### **Python 3.9+ 简化语法**

```python
# Python 3.9+ 可以直接使用内置类型，无需从 typing 导入
names: list[str] = ["Alice", "Bob"]
user_scores: dict[str, int] = {"Alice": 95}
unique_ids: set[int] = {1, 2, 3}
coordinate: tuple[float, float] = (10.5, 20.3)
```

## **2. 高级类型**

### **Optional：可选类型**

```python
from typing import Optional

# Optional[X] 等价于 X | None
def find_user(user_id: int) -> Optional[str]:
    """可能返回 None"""
    users = {1: "Alice", 2: "Bob"}
    return users.get(user_id)

user = find_user(1)
if user is not None:
    print(f"Found: {user}")
else:
    print("User not found")
```

### **Union：联合类型**

```python
from typing import Union

# Python 3.10+ 推荐使用 | 语法
def process(value: int | str) -> str:
    if isinstance(value, int):
        return f"Integer: {value}"
    else:
        return f"String: {value}"

# 旧语法（仍有效）
def process_old(value: Union[int, str]) -> Union[int, str]:
    return value
```

### **Any：任意类型**

```python
from typing import Any

# 当类型未知或混合时使用（尽量避免）
def parse_json_value(data: Any) -> Any:
    return data

# ✅ 更好的做法：使用具体类型或 Union
def parse_value(data: int | str | dict) -> str:
    return str(data)
```

### **Callable：可调用对象**

```python
from typing import Callable

def apply_operation(x: int, y: int, operation: Callable[[int, int], int]) -> int:
    """接受一个函数作为参数"""
    return operation(x, y)

def add(a: int, b: int) -> int:
    return a + b

result = apply_operation(10, 20, add)
print(result)  # 30

# Lambda 也符合 Callable
result = apply_operation(10, 20, lambda a, b: a * b)
print(result)  # 200
```

### **Literal：字面量类型**

```python
from typing import Literal

def set_mode(mode: Literal["read", "write", "append"]) -> None:
    """只接受特定的字符串值"""
    print(f"Mode set to: {mode}")

set_mode("read")     # ✅ 正确
# set_mode("delete")  # ❌ mypy 报错
```

## **3. 泛型编程（Generics）**

### **自定义泛型类**

```python
from typing import TypeVar, Generic, List

T = TypeVar('T')

class Stack(Generic[T]):
    """泛型栈"""
    def __init__(self) -> None:
        self._items: List[T] = []
    
    def push(self, item: T) -> None:
        self._items.append(item)
    
    def pop(self) -> T:
        return self._items.pop()
    
    def peek(self) -> T | None:
        return self._items[-1] if self._items else None
    
    def is_empty(self) -> bool:
        return len(self._items) == 0

# 使用
int_stack = Stack[int]()
int_stack.push(1)
int_stack.push(2)
print(int_stack.pop())  # 2

str_stack = Stack[str]()
str_stack.push("hello")
str_stack.push("world")
print(str_stack.pop())  # world
```

### **TypeVar 约束**

```python
from typing import TypeVar

# 限制类型范围
S = TypeVar('S', int, float)  # 只能是 int 或 float

def add_numbers(a: S, b: S) -> S:
    return a + b

result = add_numbers(10, 20)      # ✅ int
result = add_numbers(1.5, 2.5)    # ✅ float
# result = add_numbers(10, 1.5)   # ❌ mypy 报错
```

### **协变与逆变**

```python
from typing import TypeVar, Generic

# 协变（covariant）：用于返回值
T_co = TypeVar('T_co', covariant=True)

class Producer(Generic[T_co]):
    def produce(self) -> T_co:
        ...

# 逆变（contravariant）：用于参数
T_contra = TypeVar('T_contra', contravariant=True)

class Consumer(Generic[T_contra]):
    def consume(self, item: T_contra) -> None:
        ...
```

## **4. Protocol 与结构子类型**

Protocol 允许基于行为（而非继承）的类型检查，实现"鸭子类型"的静态验证。

```python
from typing import Protocol

class Drawable(Protocol):
    """任何具有 draw 方法的类都符合 Drawable 协议"""
    def draw(self) -> None:
        ...

class Circle:
    def draw(self) -> None:
        print("Drawing circle")

class Square:
    def draw(self) -> None:
        print("Drawing square")

# 不需要显式继承
def render(shape: Drawable) -> None:
    shape.draw()

render(Circle())  # ✅ 正确
render(Square())  # ✅ 正确
```

### **实战：可序列化协议**

```python
from typing import Protocol, Any

class Serializable(Protocol):
    def to_dict(self) -> dict[str, Any]:
        ...
    
    @classmethod
    def from_dict(cls, data: dict[str, Any]) -> "Serializable":
        ...

class User:
    def __init__(self, name: str, age: int):
        self.name = name
        self.age = age
    
    def to_dict(self) -> dict[str, Any]:
        return {"name": self.name, "age": self.age}
    
    @classmethod
    def from_dict(cls, data: dict[str, Any]) -> "User":
        return cls(name=data["name"], age=data["age"])

def save_to_database(obj: Serializable) -> None:
    data = obj.to_dict()
    print(f"Saving: {data}")

save_to_database(User("Alice", 30))  # ✅ 符合协议
```

## **5. TypedDict：字典类型化**

```python
from typing import TypedDict

class UserDict(TypedDict):
    name: str
    age: int
    email: str | None

# 类型检查器会验证键和值
user: UserDict = {
    "name": "Alice",
    "age": 30,
    "email": "alice@example.com"
}

# user = {"name": "Alice"}  # ❌ 缺少必需字段
```

### **可选字段**

```python
from typing import TypedDict, NotRequired

class ConfigDict(TypedDict):
    host: str
    port: int
    timeout: NotRequired[float]  # 可选字段

config: ConfigDict = {"host": "localhost", "port": 8080}  # ✅ 正确
```

## **6. NewType：强类型别名**

NewType 创建逻辑上不同的类型，防止类型混淆。

```python
from typing import NewType

UserId = NewType('UserId', int)
ProductId = NewType('ProductId', int)

def get_user(user_id: UserId) -> str:
    return f"User {user_id}"

def get_product(product_id: ProductId) -> str:
    return f"Product {product_id}"

# 正确使用
user = get_user(UserId(123))       # ✅
product = get_product(ProductId(456))  # ✅

# 错误使用（mypy 会捕获）
# user = get_user(ProductId(456))  # ❌ 类型不匹配

# 运行时没有开销（UserId(123) 直接返回 123）
assert UserId(123) == 123
```

## **7. 类型检查工具**

### **mypy 配置与使用**

```bash
# 安装
pip install mypy

# 基本使用
mypy your_script.py

# 严格模式
mypy --strict your_script.py

# 生成配置文件
mypy --init-config
```

#### **mypy.ini 配置示例**

```ini
[mypy]
python_version = 3.11
warn_return_any = True
warn_unused_configs = True
disallow_untyped_defs = True
disallow_incomplete_defs = True
check_untyped_defs = True
disallow_untyped_decorators = True
no_implicit_optional = True
warn_redundant_casts = True
warn_unused_ignores = True
warn_no_return = True
warn_unreachable = True

[mypy.plugins.numpy.*]
ignore_missing_imports = True
```

### **pyright / Pylance**

- Microsoft 开发的类型检查器
- VS Code 默认集成（Pylance）
- 更快的检查速度
- 支持增量检查

```bash
pip install pyright
pyright your_project/
```

### **在 CI/CD 中集成**

```yaml
# .github/workflows/type-check.yml
name: Type Check

on: [push, pull_request]

jobs:
  type-check:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.11'
      - name: Install dependencies
        run: pip install mypy
      - name: Run mypy
        run: mypy --strict src/
```

## **8. 运行时类型检查**

### **pydantic 数据验证**

```python
from pydantic import BaseModel, EmailStr, Field
from datetime import datetime

class User(BaseModel):
    id: int
    name: str = Field(min_length=1, max_length=100)
    email: EmailStr
    age: int = Field(ge=0, le=150)
    created_at: datetime = Field(default_factory=datetime.now)

# 自动验证和转换
user = User(
    id=1,
    name="Alice",
    email="alice@example.com",
    age=30
)

print(user.json())  # JSON 序列化

# 无效数据会抛出 ValidationError
# User(id=1, name="", email="invalid", age=-5)  # ❌ 验证失败
```

### **beartype 装饰器**

```python
from beartype import beartype

@beartype
def greet(name: str, age: int) -> str:
    return f"{name} is {age} years old"

greet("Alice", 30)  # ✅ 正确
# greet(123, "thirty")  # ❌ 运行时抛出 BeartypeCallHintParamViolation
```

## **9. 最佳实践**

### **渐进式类型化策略**

```python
# 阶段 1：为新代码添加类型
def new_feature(param: str) -> int:
    ...

# 阶段 2：为修改的旧代码添加类型
def legacy_function(param: str) -> int:  # 逐步添加
    ...

# 阶段 3：使用 stub 文件为第三方库添加类型
# types-requests, types-PyYAML 等
```

### **何时使用类型提示**

✅ **应该使用**：
- 公共 API 和库接口
- 复杂函数的参数和返回值
- 团队协作项目
- 长期维护的代码

❌ **可以不使用**：
- 简单的脚本
- 原型快速开发
- 动态特性密集的代码（元编程）

### **常见模式**

```python
from typing import TypeVar, Generic, Iterator

# 模式 1：迭代器
T = TypeVar('T')

class LinkedList(Generic[T]):
    def __iter__(self) -> Iterator[T]:
        ...

# 模式 2：上下文管理器
from typing import ContextManager

def open_file(path: str) -> ContextManager[str]:
    ...

# 模式 3：装饰器
from functools import wraps
from typing import Callable, ParamSpec, TypeVar

P = ParamSpec('P')
R = TypeVar('R')

def logger(func: Callable[P, R]) -> Callable[P, R]:
    @wraps(func)
    def wrapper(*args: P.args, **kwargs: P.kwargs) -> R:
        print(f"Calling {func.__name__}")
        return func(*args, **kwargs)
    return wrapper
```

### **避免过度类型化**

```python
# ❌ 过度复杂
def process(data: dict[str, list[tuple[int, dict[str, Any]]]]) -> None:
    ...

# ✅ 使用 TypedDict 和别名简化
from typing import TypedDict

class ItemData(TypedDict):
    values: list[tuple[int, dict[str, Any]]]

def process(data: dict[str, ItemData]) -> None:
    ...
```

## **10. 类型存根（Stub Files）**

为没有类型提示的库创建 `.pyi` 文件：

```python
# mylib.pyi
def calculate(x: int, y: int) -> float: ...
class Calculator:
    def __init__(self, precision: int = ...) -> None: ...
    def compute(self, data: list[float]) -> float: ...
```

---

# **性能分析与优化**

性能优化是生产环境的关键环节。本章节介绍系统化的性能分析方法和优化策略。

## **1. 性能分析工具**

### **cProfile：确定性分析器**

```python
import cProfile
import pstats
from io import StringIO

def slow_function():
    total = 0
    for i in range(1000000):
        total += i
    return total

def fast_function():
    return sum(range(1000000))

# 方法 1：编程方式
pr = cProfile.Profile()
pr.enable()
slow_function()
fast_function()
pr.disable()

# 输出统计信息
s = StringIO()
ps = pstats.Stats(pr, stream=s).sort_stats('cumulative')
ps.print_stats(10)
print(s.getvalue())

# 方法 2：命令行
# python -m cProfile -s cumulative script.py
```

### **timeit：精确计时**

```python
import timeit

# 基本用法
time_taken = timeit.timeit('sum(range(1000))', number=10000)
print(f"Time: {time_taken:.4f}s")

# 比较不同实现
setup = "import math"
stmt1 = "[x**2 for x in range(100)]"
stmt2 = "[math.pow(x, 2) for x in range(100)]"

time1 = timeit.timeit(stmt1, setup=setup, number=100000)
time2 = timeit.timeit(stmt2, setup=setup, number=100000)

print(f"List comprehension: {time1:.4f}s")
print(f"math.pow: {time2:.4f}s")
```

### **memory_profiler：内存分析**

```bash
pip install memory-profiler
```

```python
# 使用装饰器
from memory_profiler import profile

@profile
def memory_intensive():
    a = [1] * (10 ** 6)  # 占用 ~8MB
    b = [2] * (2 * 10 ** 7)  # 占用 ~160MB
    del b
    return a

if __name__ == "__main__":
    memory_intensive()

# 命令行：python -m memory_profiler script.py
```

### **line_profiler：行级分析**

```bash
pip install line-profiler
```

```python
from line_profiler import LineProfiler

def compute():
    total = 0
    for i in range(1000000):  # 耗时行
        total += i
    return total

# 配置
lp = LineProfiler()
lp_wrapper = lp(compute)
lp_wrapper()
lp.print_stats()
```

### **py-spy：采样分析器（无需修改代码）**

```bash
# 安装
pip install py-spy

# 分析运行中的进程
py-spy top --pid 12345

# 生成火焰图
py-spy record -o profile.svg -- python script.py
```

## **2. 算法与数据结构优化**

### **选择合适的数据结构**

```python
import time

# 查找操作：list vs set
data_list = list(range(1000000))
data_set = set(range(1000000))

# List 查找：O(n)
start = time.time()
999999 in data_list
print(f"List lookup: {time.time() - start:.6f}s")  # ~0.01s

# Set 查找：O(1)
start = time.time()
999999 in data_set
print(f"Set lookup: {time.time() - start:.6f}s")   # ~0.000001s
```

### **生成器惰性求值**

```python
import sys

# 列表：一次性加载所有数据到内存
large_list = [x * 2 for x in range(10000000)]
print(f"List size: {sys.getsizeof(large_list)} bytes")  # ~85MB

# 生成器：按需生成，节省内存
large_gen = (x * 2 for x in range(10000000))
print(f"Generator size: {sys.getsizeof(large_gen)} bytes")  # ~200 bytes

# 处理大文件
def read_large_file(filename):
    with open(filename, 'r') as f:
        for line in f:  # 逐行读取，不一次性加载
            yield line.strip()

for line in read_large_file('huge_file.txt'):
    process(line)
```

### **缓存策略**

```python
from functools import lru_cache
import time

# 无缓存：重复计算
def fibonacci_slow(n):
    if n < 2:
        return n
    return fibonacci_slow(n - 1) + fibonacci_slow(n - 2)

# 带缓存：记忆化
@lru_cache(maxsize=None)
def fibonacci_fast(n):
    if n < 2:
        return n
    return fibonacci_fast(n - 1) + fibonacci_fast(n - 2)

start = time.time()
fibonacci_fast(35)
print(f"With cache: {time.time() - start:.4f}s")  # ~0.0001s

start = time.time()
fibonacci_slow(35)
print(f"Without cache: {time.time() - start:.4f}s")  # ~5s
```

#### **自定义缓存失效**

```python
from functools import lru_cache

@lru_cache(maxsize=128)
def get_user(user_id):
    """模拟数据库查询"""
    print(f"Querying database for user {user_id}")
    return {"id": user_id, "name": f"User{user_id}"}

# 清除特定缓存
get_user.cache_clear()

# 查看缓存统计
print(get_user.cache_info())
# CacheInfo(hits=0, misses=0, maxsize=128, currsize=0)
```

## **3. 内存管理深入**

### **__slots__ 减少内存占用**

```python
import sys

class RegularClass:
    def __init__(self, x, y):
        self.x = x
        self.y = y

class SlottedClass:
    __slots__ = ['x', 'y']  # 禁止动态添加属性
    def __init__(self, x, y):
        self.x = x
        self.y = y

obj1 = RegularClass(1, 2)
obj2 = SlottedClass(1, 2)

print(f"Regular: {sys.getsizeof(obj1)} bytes")    # ~56 bytes + dict overhead
print(f"Slotted: {sys.getsizeof(obj2)} bytes")    # ~48 bytes

# 大量实例时差异显著
objects1 = [RegularClass(i, i) for i in range(100000)]
objects2 = [SlottedClass(i, i) for i in range(100000)]
```

### **弱引用打破循环引用**

```python
import weakref
import gc

class Parent:
    def __init__(self):
        self.children = []

class Child:
    def __init__(self, parent):
        # 使用弱引用避免循环引用
        self.parent = weakref.ref(parent)

parent = Parent()
child = Child(parent)
parent.children.append(child)

# 删除强引用后可以被垃圾回收
del parent
gc.collect()
print("Memory freed")
```

### **对象池模式**

```python
class ObjectPool:
    """复用对象，减少创建开销"""
    def __init__(self, factory, max_size=10):
        self._factory = factory
        self._pool = []
        self._max_size = max_size
    
    def acquire(self):
        if self._pool:
            return self._pool.pop()
        return self._factory()
    
    def release(self, obj):
        if len(self._pool) < self._max_size:
            self._pool.append(obj)

# 使用：数据库连接池
import sqlite3

pool = ObjectPool(lambda: sqlite3.connect(':memory:'))

conn = pool.acquire()
conn.execute("CREATE TABLE test (id INTEGER)")
pool.release(conn)
```

## **4. C 扩展与加速**

### **Cython：编译 Python 为 C**

```bash
pip install cython
```

```python
# fib_cython.pyx
def fibonacci(int n):
    cdef int a = 0, b = 1, i
    for i in range(n):
        a, b = b, a + b
    return a

# setup.py
from setuptools import setup
from Cython.Build import cythonize

setup(
    ext_modules=cythonize("fib_cython.pyx")
)

# 编译：python setup.py build_ext --inplace
```

#### **类型声明提升性能**

```python
# 纯 Python：慢
def sum_squares_python(n):
    total = 0
    for i in range(n):
        total += i * i
    return total

# Cython 带类型：快 10-100 倍
def sum_squares_cython(int n):
    cdef long long total = 0
    cdef int i
    for i in range(n):
        total += i * i
    return total
```

### **Numba：JIT 编译数值计算**

```bash
pip install numba
```

```python
from numba import jit
import numpy as np
import time

# 纯 NumPy
def matrix_multiply_numpy(a, b):
    return np.dot(a, b)

# Numba JIT 编译
@jit(nopython=True)
def matrix_multiply_numba(a, b):
    m, n = a.shape
    n, p = b.shape
    result = np.zeros((m, p))
    for i in range(m):
        for j in range(p):
            for k in range(n):
                result[i, j] += a[i, k] * b[k, j]
    return result

# 测试
a = np.random.rand(1000, 1000)
b = np.random.rand(1000, 1000)

start = time.time()
matrix_multiply_numba(a, b)  # 第一次调用包含编译时间
print(f"Numba (warm): {time.time() - start:.4f}s")

start = time.time()
matrix_multiply_numba(a, b)  # 后续调用极快
print(f"Numba (cached): {time.time() - start:.4f}s")
```

### **ctypes：调用 C 库**

```python
import ctypes

# 加载 C 标准库
libc = ctypes.CDLL('msvcrt.dll')  # Windows
# libc = ctypes.CDLL('libc.so.6')  # Linux

# 调用 printf
libc.printf(b"Hello from C!\n")

# 调用数学函数
libc.sqrt.restype = ctypes.c_double
libc.sqrt.argtypes = [ctypes.c_double]
print(libc.sqrt(16.0))  # 4.0
```

## **5. 并发优化**

### **批量 I/O 操作**

```python
import asyncio
import aiohttp
import time

# 串行请求：慢
async def fetch_sequential(urls):
    async with aiohttp.ClientSession() as session:
        results = []
        for url in urls:
            async with session.get(url) as response:
                results.append(await response.text())
        return results

# 并发请求：快
async def fetch_concurrent(urls):
    async with aiohttp.ClientSession() as session:
        tasks = [session.get(url) for url in urls]
        responses = await asyncio.gather(*tasks)
        return [await r.text() for r in responses]
```

### **连接池**

```python
import requests
from requests.adapters import HTTPAdapter
from urllib3.util.retry import Retry

# 配置连接池
session = requests.Session()
adapter = HTTPAdapter(
    pool_connections=10,
    pool_maxsize=100,
    max_retries=Retry(total=3, backoff_factor=1)
)
session.mount('http://', adapter)
session.mount('https://', adapter)

# 复用连接，减少握手开销
for url in urls:
    response = session.get(url)
```

## **6. 基准测试最佳实践**

### **pytest-benchmark**

```bash
pip install pytest-benchmark
```

```python
# test_performance.py
def test_list_comprehension(benchmark):
    result = benchmark(lambda: [x**2 for x in range(1000)])
    assert len(result) == 1000

def test_map_function(benchmark):
    result = benchmark(lambda: list(map(lambda x: x**2, range(1000))))
    assert len(result) == 1000

# 运行：pytest --benchmark-only
```

### **避免基准测试陷阱**

```python
import timeit

# ❌ 错误：包含设置时间
timeit.timeit('import math; [math.sqrt(x) for x in range(1000)]')

# ✅ 正确：分离设置和测试
timeit.timeit(
    '[sqrt(x) for x in range(1000)]',
    setup='from math import sqrt',
    number=10000
)

# ❌ 错误：测试次数太少
timeit.timeit('sum(range(100))', number=10)

# ✅ 正确：足够多次取平均
timeit.repeat('sum(range(100))', number=100000, repeat=5)
```

---

# **软件架构与设计模式**

## **1. SOLID 原则**

### **单一职责原则（SRP）**

```python
# ❌ 违反 SRP：一个类承担多个职责
class UserService:
    def get_user(self, user_id): ...
    def save_user(self, user): ...
    def send_email(self, user): ...
    def generate_report(self): ...

# ✅ 遵循 SRP：职责分离
class UserRepository:
    def get_user(self, user_id): ...
    def save_user(self, user): ...

class EmailService:
    def send_email(self, user): ...

class ReportGenerator:
    def generate_report(self): ...
```

### **开闭原则（OCP）**

```python
from abc import ABC, abstractmethod

# ❌ 违反 OCP：添加新类型需修改现有代码
class PaymentProcessor:
    def process(self, payment_type, amount):
        if payment_type == "credit_card":
            ...
        elif payment_type == "paypal":
            ...
        # 添加新支付方式需修改此处

# ✅ 遵循 OCP：通过扩展而非修改
class PaymentMethod(ABC):
    @abstractmethod
    def process(self, amount: float) -> None:
        ...

class CreditCardPayment(PaymentMethod):
    def process(self, amount: float) -> None:
        print(f"Processing credit card: ${amount}")

class PayPalPayment(PaymentMethod):
    def process(self, amount: float) -> None:
        print(f"Processing PayPal: ${amount}")

# 添加新支付方式只需创建新类
class CryptoPayment(PaymentMethod):
    def process(self, amount: float) -> None:
        print(f"Processing crypto: ${amount}")
```

### **里氏替换原则（LSP）**

```python
# ❌ 违反 LSP：子类行为不符合父类契约
class Rectangle:
    def __init__(self, width, height):
        self._width = width
        self._height = height
    
    @property
    def width(self):
        return self._width
    
    @width.setter
    def width(self, value):
        self._width = value
    
    @property
    def height(self):
        return self._height
    
    @height.setter
    def height(self, value):
        self._height = value

class Square(Rectangle):
    def __init__(self, size):
        super().__init__(size, size)
    
    @Rectangle.width.setter
    def width(self, value):
        self._width = value
        self._height = value  # 破坏父类行为

# ✅ 正确设计：使用共同基类
class Shape(ABC):
    @abstractmethod
    def area(self) -> float:
        ...

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height
    
    def area(self) -> float:
        return self.width * self.height

class Square(Shape):
    def __init__(self, side):
        self.side = side
    
    def area(self) -> float:
        return self.side ** 2
```

### **接口隔离原则（ISP）**

```python
from typing import Protocol

# ❌ 违反 ISP：庞大接口
class Worker(Protocol):
    def work(self): ...
    def eat(self): ...
    def sleep(self): ...

# ✅ 遵循 ISP：细化接口
class Workable(Protocol):
    def work(self): ...

class Eatable(Protocol):
    def eat(self): ...

class Human(Workable, Eatable):
    def work(self): print("Working")
    def eat(self): print("Eating")

class Robot(Workable):
    def work(self): print("Robot working")
    # 不需要实现 eat
```

### **依赖倒置原则（DIP）**

```python
from abc import ABC, abstractmethod

# ❌ 违反 DIP：高层模块依赖低层模块
class MySQLDatabase:
    def connect(self): ...
    def query(self, sql): ...

class UserService:
    def __init__(self):
        self.db = MySQLDatabase()  # 紧耦合

# ✅ 遵循 DIP：依赖抽象
class Database(ABC):
    @abstractmethod
    def connect(self) -> None: ...
    
    @abstractmethod
    def query(self, sql: str) -> list: ...

class MySQLDatabase(Database):
    def connect(self): ...
    def query(self, sql): ...

class PostgreSQLDatabase(Database):
    def connect(self): ...
    def query(self, sql): ...

class UserService:
    def __init__(self, db: Database):  # 依赖注入
        self.db = db
```

## **2. 创建型设计模式**

### **工厂方法模式**

```python
from abc import ABC, abstractmethod

class Notification(ABC):
    @abstractmethod
    def send(self, message: str) -> None:
        ...

class EmailNotification(Notification):
    def send(self, message: str) -> None:
        print(f"Email: {message}")

class SMSNotification(Notification):
    def send(self, message: str) -> None:
        print(f"SMS: {message}")

class NotificationFactory:
    @staticmethod
    def create(notification_type: str) -> Notification:
        factories = {
            "email": EmailNotification,
            "sms": SMSNotification,
        }
        cls = factories.get(notification_type)
        if not cls:
            raise ValueError(f"Unknown type: {notification_type}")
        return cls()

# 使用
notifier = NotificationFactory.create("email")
notifier.send("Hello!")
```

### **单例模式（多种实现）**

```python
# 方法 1：元类
class SingletonMeta(type):
    _instances = {}
    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super().__call__(*args, **kwargs)
        return cls._instances[cls]

class Singleton1(metaclass=SingletonMeta):
    pass

# 方法 2：装饰器
def singleton(cls):
    instances = {}
    def wrapper(*args, **kwargs):
        if cls not in instances:
            instances[cls] = cls(*args, **kwargs)
        return instances[cls]
    return wrapper

@singleton
class Singleton2:
    pass

# 方法 3：模块级别（Python 推荐）
# singleton_instance.py
class Singleton3:
    pass

singleton_instance = Singleton3()

# 其他模块导入：from singleton_instance import singleton_instance
```

## **3. 结构型设计模式**

### **适配器模式**

```python
class EuropeanSocket:
    def plug_in(self):
        return "220V power"

class USSocket:
    def connect(self):
        return "110V power"

class SocketAdapter(EuropeanSocket):
    def __init__(self, us_socket: USSocket):
        self.us_socket = us_socket
    
    def plug_in(self):
        return self.us_socket.connect() + " converted to 220V"

# 使用
us_socket = USSocket()
adapter = SocketAdapter(us_socket)
print(adapter.plug_in())
```

### **装饰器模式**

```python
class Coffee:
    def cost(self) -> float:
        return 5.0
    
    def description(self) -> str:
        return "Coffee"

class MilkDecorator:
    def __init__(self, coffee: Coffee):
        self.coffee = coffee
    
    def cost(self) -> float:
        return self.coffee.cost() + 2.0
    
    def description(self) -> str:
        return f"{self.coffee.description()} + Milk"

class SugarDecorator:
    def __init__(self, coffee: Coffee):
        self.coffee = coffee
    
    def cost(self) -> float:
        return self.coffee.cost() + 0.5
    
    def description(self) -> str:
        return f"{self.coffee.description()} + Sugar"

# 使用
coffee = Coffee()
coffee = MilkDecorator(coffee)
coffee = SugarDecorator(coffee)
print(coffee.description())  # Coffee + Milk + Sugar
print(coffee.cost())         # 7.5
```

## **4. 行为型设计模式**

### **观察者模式**

```python
from typing import List, Callable

class EventDispatcher:
    def __init__(self):
        self._listeners: List[Callable] = []
    
    def add_listener(self, callback: Callable) -> None:
        self._listeners.append(callback)
    
    def remove_listener(self, callback: Callable) -> None:
        self._listeners.remove(callback)
    
    def dispatch(self, *args, **kwargs) -> None:
        for listener in self._listeners:
            listener(*args, **kwargs)

# 使用
dispatcher = EventDispatcher()

def on_event(data):
    print(f"Listener 1 received: {data}")

def on_event_2(data):
    print(f"Listener 2 received: {data}")

dispatcher.add_listener(on_event)
dispatcher.add_listener(on_event_2)
dispatcher.dispatch("Hello!")
```

### **策略模式**

```python
from abc import ABC, abstractmethod

class SortingStrategy(ABC):
    @abstractmethod
    def sort(self, data: list) -> list:
        ...

class QuickSort(SortingStrategy):
    def sort(self, data: list) -> list:
        return sorted(data)  # 简化实现

class BubbleSort(SortingStrategy):
    def sort(self, data: list) -> list:
        arr = data.copy()
        n = len(arr)
        for i in range(n):
            for j in range(0, n-i-1):
                if arr[j] > arr[j+1]:
                    arr[j], arr[j+1] = arr[j+1], arr[j]
        return arr

class Sorter:
    def __init__(self, strategy: SortingStrategy):
        self.strategy = strategy
    
    def sort(self, data: list) -> list:
        return self.strategy.sort(data)

# 使用
sorter = Sorter(QuickSort())
result = sorter.sort([3, 1, 4, 1, 5])
```

## **5. 架构模式**

### **分层架构**

```python
# presentation_layer.py
class UserController:
    def __init__(self, service: UserService):
        self.service = service
    
    def get_user(self, user_id: int) -> dict:
        user = self.service.get_user(user_id)
        return {"id": user.id, "name": user.name}

# business_layer.py
class UserService:
    def __init__(self, repository: UserRepository):
        self.repository = repository
    
    def get_user(self, user_id: int):
        return self.repository.find_by_id(user_id)

# data_layer.py
class UserRepository:
    def find_by_id(self, user_id: int):
        # 数据库查询
        ...
```

### **依赖注入容器**

```python
class Container:
    def __init__(self):
        self._services = {}
    
    def register(self, interface, implementation):
        self._services[interface] = implementation
    
    def resolve(self, interface):
        if interface not in self._services:
            raise KeyError(f"No service registered for {interface}")
        return self._services[interface]()

# 配置
container = Container()
container.register(Database, MySQLDatabase)
container.register(UserRepository, lambda: UserRepository(container.resolve(Database)))
container.register(UserService, lambda: UserService(container.resolve(UserRepository)))

# 使用
user_service = container.resolve(UserService)
```

---

# **测试工程化**

## **1. pytest 高级用法**

### **Fixtures 与作用域**

```python
import pytest

# conftest.py
@pytest.fixture(scope="session")
def database():
    """会话级别：整个测试会话共享"""
    db = create_test_database()
    yield db
    cleanup_database(db)

@pytest.fixture(scope="module")
def api_client(database):
    """模块级别：每个模块共享"""
    return APIClient(database)

@pytest.fixture
def user(api_client):
    """函数级别：每个测试函数独立"""
    user = api_client.create_user(name="Test User")
    yield user
    api_client.delete_user(user.id)

# test_users.py
def test_get_user(user):
    assert user.name == "Test User"

def test_update_user(user, api_client):
    user.name = "Updated Name"
    updated = api_client.update_user(user)
    assert updated.name == "Updated Name"
```

### **参数化测试**

```python
import pytest

@pytest.mark.parametrize("input,expected", [
    (1, 1),
    (2, 4),
    (3, 9),
    (4, 16),
])
def test_square(input, expected):
    assert input ** 2 == expected

@pytest.mark.parametrize("username,password,expected_status", [
    ("admin", "secret", 200),
    ("user", "wrong", 401),
    ("", "", 400),
])
def test_login(username, password, expected_status):
    response = login_api(username, password)
    assert response.status_code == expected_status
```

### **Mock 与 Stub**

```python
from unittest.mock import Mock, patch, MagicMock
import pytest

# Mock 对象
def test_mock():
    mock_db = Mock()
    mock_db.query.return_value = [{"id": 1, "name": "Alice"}]
    
    result = mock_db.query("SELECT * FROM users")
    assert result == [{"id": 1, "name": "Alice"}]
    mock_db.query.assert_called_once_with("SELECT * FROM users")

# Patch 装饰器
@patch('requests.get')
def test_api_call(mock_get):
    mock_response = Mock()
    mock_response.status_code = 200
    mock_response.json.return_value = {"data": "test"}
    mock_get.return_value = mock_response
    
    response = requests.get("https://api.example.com")
    assert response.status_code == 200
    mock_get.assert_called_once_with("https://api.example.com")

# Patch 上下文管理器
def test_multiple_mocks():
    with patch('module.func1') as mock1, \
         patch('module.func2') as mock2:
        mock1.return_value = 10
        mock2.return_value = 20
        # 测试逻辑
```

## **2. Property-Based Testing（Hypothesis）**

```bash
pip install hypothesis
```

```python
from hypothesis import given, strategies as st

@given(st.integers())
def test_absolute_value_is_non_negative(x):
    assert abs(x) >= 0

@given(st.lists(st.integers(), min_size=1))
def test_sort_preserves_length(lst):
    assert len(sorted(lst)) == len(lst)

@given(st.dictionaries(keys=st.text(), values=st.integers()))
def test_dict_keys_unique(d):
    assert len(d.keys()) == len(set(d.keys()))
```

## **3. 持续集成配置**

```yaml
# .github/workflows/test.yml
name: Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: ['3.9', '3.10', '3.11', '3.12']
    
    steps:
      - uses: actions/checkout@v3
      - name: Set up Python ${{ matrix.python-version }}
        uses: actions/setup-python@v4
        with:
          python-version: ${{ matrix.python-version }}
      - name: Install dependencies
        run: |
          pip install poetry
          poetry install
      - name: Run tests
        run: poetry run pytest --cov=src --cov-report=xml
      - name: Upload coverage
        uses: codecov/codecov-action@v3
```

---

# **项目工程化**

## **1. 依赖管理**

### **Poetry 工作流**

```bash
# 初始化项目
poetry new my-project
cd my-project

# 添加依赖
poetry add requests pydantic
poetry add --dev pytest black mypy

# 虚拟环境管理
poetry shell
poetry env info

# 运行命令
poetry run python main.py
poetry run pytest

# 构建发布
poetry build
poetry publish
```

#### **pyproject.toml 示例**

```toml
[tool.poetry]
name = "my-project"
version = "0.1.0"
description = ""
authors = ["Your Name <you@example.com>"]

[tool.poetry.dependencies]
python = "^3.9"
requests = "^2.31.0"
pydantic = "^2.0.0"

[tool.poetry.group.dev.dependencies]
pytest = "^7.4.0"
black = "^23.7.0"
mypy = "^1.5.0"

[build-system]
requires = ["poetry-core"]
build-backend = "poetry.core.masonry.api"
```

## **2. 代码质量工具**

### **pre-commit 配置**

```yaml
# .pre-commit-config.yaml
repos:
  - repo: https://github.com/psf/black
    rev: 23.7.0
    hooks:
      - id: black
  
  - repo: https://github.com/pycqa/isort
    rev: 5.12.0
    hooks:
      - id: isort
  
  - repo: https://github.com/pycqa/flake8
    rev: 6.1.0
    hooks:
      - id: flake8
  
  - repo: https://github.com/pre-commit/mirrors-mypy
    rev: v1.5.0
    hooks:
      - id: mypy
        additional_dependencies: [types-requests]
```

```bash
pip install pre-commit
pre-commit install
pre-commit run --all-files
```

## **3. 文档生成**

### **Sphinx 快速开始**

```bash
pip install sphinx sphinx-rtd-theme
sphinx-quickstart docs
```

```python
# docstring 规范（Google 风格）
def calculate_area(radius: float) -> float:
    """Calculate the area of a circle.
    
    Args:
        radius: The radius of the circle. Must be non-negative.
    
    Returns:
        The area of the circle.
    
    Raises:
        ValueError: If radius is negative.
    
    Examples:
        >>> calculate_area(5)
        78.53981633974483
    """
    if radius < 0:
        raise ValueError("Radius cannot be negative")
    return math.pi * radius ** 2
```

---

# **安全编程**

## **1. 常见安全漏洞防护**

### **SQL 注入**

```python
# ❌ 不安全：字符串拼接
query = f"SELECT * FROM users WHERE username = '{username}'"
cursor.execute(query)

# ✅ 安全：参数化查询
cursor.execute("SELECT * FROM users WHERE username = %s", (username,))
```

### **命令注入**

```python
import subprocess

# ❌ 不安全：shell=True
subprocess.run(f"ping {user_input}", shell=True)

# ✅ 安全：列表参数
subprocess.run(["ping", user_input], check=True)
```

### **路径遍历**

```python
import os
from pathlib import Path

# ❌ 不安全
file_path = f"/uploads/{filename}"

# ✅ 安全：验证路径
BASE_DIR = Path("/uploads")
file_path = BASE_DIR / filename
file_path = file_path.resolve()
if not file_path.is_relative_to(BASE_DIR):
    raise ValueError("Invalid path")
```

## **2. 密码学最佳实践**

### **密码哈希**

```bash
pip install bcrypt
```

```python
import bcrypt

# 哈希密码
password = b"secure_password"
salt = bcrypt.gensalt(rounds=12)
hashed = bcrypt.hashpw(password, salt)

# 验证密码
if bcrypt.checkpw(password, hashed):
    print("Password matches")
```

### **安全随机数**

```python
import secrets

# ❌ 不安全：伪随机
import random
token = random.randint(100000, 999999)

# ✅ 安全：加密安全随机
token = secrets.token_urlsafe(32)
otp = secrets.randbelow(900000) + 100000
```

## **3. 依赖安全检查**

```bash
# 安装审计工具
pip install pip-audit

# 扫描漏洞
pip-audit

# 定期更新依赖
pip list --outdated
poetry update
```

---

# **生态系统概览**

## **1. Web 框架对比**

| 框架 | 类型 | 特点 | 适用场景 |
|------|------|------|----------|
| Flask | 微框架 | 轻量、灵活、扩展丰富 | 小型应用、API、原型 |
| Django | 全栈 | ORM、Admin、Auth 内置 | 大型应用、CMS、电商 |
| FastAPI | 异步 | 类型安全、自动文档、高性能 | 现代 API、微服务 |
| Starlette | ASGI | 轻量异步基础 | 框架构建、高性能服务 |

### **FastAPI 示例**

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class UserCreate(BaseModel):
    name: str
    email: str

@app.post("/users/")
def create_user(user: UserCreate):
    return {"message": f"User {user.name} created"}

# 自动生成交互式文档：http://localhost:8000/docs
```

## **2. 数据处理生态**

| 库 | 用途 | 优势 |
|----|------|------|
| NumPy | 数值计算 | 高效数组运算 |
| Pandas | 数据分析 | DataFrame API |
| Polars | 高性能数据处理 | Rust 后端、并行 |
| Dask | 分布式计算 | 扩展到大数据 |

### **Polars 示例**

```python
import polars as pl

df = pl.read_csv("data.csv")
result = (
    df.filter(pl.col("age") > 25)
    .groupby("city")
    .agg(pl.col("salary").mean())
)
```

## **3. 任务队列**

| 工具 | 特点 | 适用场景 |
|------|------|----------|
| Celery | 成熟、功能丰富 | 大型分布式系统 |
| RQ | 简单、基于 Redis | 小型项目 |
| Dramatiq | 现代、类型友好 | 新项目 |

### **Celery 示例**

```python
from celery import Celery

app = Celery('tasks', broker='redis://localhost:6379/0')

@app.task
def add(x, y):
    return x + y

# 异步调用
result = add.delay(4, 4)
print(result.get())
```

---

# **项目经验与实战能力**

## **1. 常见场景**

- Web 开发：Flask/Django。
- 数据处理：爬虫（Scrapy/BeautifulSoup）、数据分析。
- 自动化脚本：文件批量处理、任务自动化。
- 机器学习：模型训练与部署。

## **2. 项目展示**

- 描述项目的背景、目标、技术栈和解决方案。
- 强调你在项目中如何使用 Python 的特性解决问题。

---
