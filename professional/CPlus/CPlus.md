
# **一、C++ 基础**

## **C++ 概述**

### **1. C++ 的历史与特点**

#### **1.1 历史**

C++ 是由丹麦计算机科学家 Bjarne Stroustrup 在 20 世纪 80 年代初开发的。它最初是作为对 C 语言的扩展，目的是在 C 语言的基础上增加面向对象编程（OOP）的支持，同时保留 C 的高效性和灵活性。

- **1979年**：Bjarne Stroustrup 开始在贝尔实验室工作，他希望将 Simula（一种早期的面向对象语言）的特性引入到 C 中。
- **1983年**：C++ 正式命名为 "C with Classes"，后来更名为 C++（"++" 表示增量操作符，意味着它是 C 的增强版）。
- **1985年**：C++ 第一个商业版本发布，支持类、继承、内联函数、函数重载等特性。
- **1998年**：C++ 标准化委员会发布了第一个国际标准 ISO/IEC 14882:1998，即 C++98。
- **2003年**：C++03 发布，主要是对 C++98 的一些小修正。
- **2011年**：C++11 发布，这是 C++ 的一个重要里程碑，引入了许多现代特性，如智能指针、Lambda 表达式、移动语义等。
- **2014年**：C++14 发布，进一步完善了 C++11 的功能。
- **2017年**：C++17 发布，增加了更多的现代化特性，如结构化绑定、文件系统库等。
- **2020年**：C++20 发布，引入了概念（Concepts）、模块（Modules）、协程（Coroutines）等新特性。

#### **1.2 特点**

C++ 是一种多范式编程语言，支持多种编程风格，包括过程式编程、面向对象编程和泛型编程。以下是 C++ 的主要特点：

1. **高效性**：
   - C++ 提供了对硬件的直接访问能力（如指针操作），使得程序员可以编写高效的代码。
   - 它允许程序员进行底层内存管理，避免了垃圾回收机制带来的性能开销。

2. **面向对象编程（OOP）**：
   - C++ 支持类和对象的概念，允许程序员使用封装、继承和多态等 OOP 特性。
   - 面向对象的设计可以帮助程序员组织复杂的代码结构，提高代码的可维护性和可扩展性。

3. **泛型编程**：
   - C++ 提供了模板（Templates）机制，允许程序员编写与类型无关的通用代码。
   - STL（标准模板库）是 C++ 泛型编程的一个重要组成部分，提供了丰富的容器、算法和迭代器。

4. **兼容性**：
   - C++ 几乎完全兼容 C 语言，这意味着大多数 C 程序可以在 C++ 编译器中编译运行。
   - 这种兼容性使得 C++ 可以轻松地集成到现有的 C 项目中。

5. **丰富的标准库**：
   - C++ 提供了强大的标准库（STL），包括数据结构（如 `vector`, `list`, `map`）、算法（如 `sort`, `find`）、字符串处理、输入输出流等。
   - STL 的设计基于泛型编程，能够处理各种数据类型。

6. **跨平台性**：
   - C++ 是一种跨平台的语言，可以在不同的操作系统（如 Windows、Linux、macOS）上编译和运行。
   - 由于 C++ 的高效性和灵活性，它被广泛应用于嵌入式系统、游戏开发、高性能服务器等领域。

---

### **2. 编译过程：预处理、编译、汇编、链接**

C++ 程序从源代码到可执行文件的生成过程可以分为四个主要阶段：**预处理**、**编译**、**汇编**和**链接**。每个阶段都有其特定的任务，最终生成可执行的二进制文件。

#### **2.1 预处理（Preprocessing）**

预处理是编译过程的第一步，主要负责处理源代码中的预处理指令（如 `#include`, `#define` 等）。预处理器会根据这些指令对源代码进行修改，生成一个新的中间文件。

- **头文件包含**：`#include` 指令会将指定的头文件内容插入到源文件中。例如，`#include <iostream>` 会将标准输入输出库的内容插入到源文件中。
- **宏定义与替换**：`#define` 指令用于定义宏，预处理器会将程序中所有出现的宏名替换为对应的值或表达式。
- **条件编译**：`#ifdef`, `#ifndef`, `#endif` 等指令用于控制代码的编译条件，只有满足条件的代码才会被编译。

**示例**：

```cpp
#include <iostream>
#define PI 3.14159

int main() {
    std::cout << "The value of PI is: " << PI << std::endl;
    return 0;
}
```

在这个例子中，`#include <iostream>` 会将标准输入输出库的内容插入到源文件中，而 `#define PI 3.14159` 会将 `PI` 替换为 `3.14159`。

#### **2.2 编译（Compilation）**

编译是将预处理后的源代码转换为汇编语言的过程。编译器会对源代码进行语法分析、语义分析，并生成与目标平台相关的汇编代码。

- **语法检查**：编译器会检查源代码中的语法错误，如拼写错误、缺少分号等。
- **优化**：编译器会对代码进行优化，以提高程序的执行效率。
- **生成汇编代码**：编译器将高级语言代码转换为低级的汇编语言代码。

**示例**：
假设我们有以下简单的 C++ 程序：

```cpp
int main() {
    int a = 5;
    int b = 10;
    int c = a + b;
    return 0;
}
```

编译器会将这段代码转换为汇编语言，类似于以下形式（具体汇编代码可能因平台而异）：

```asm
mov eax, 5
mov ebx, 10
add eax, ebx
```

#### **2.3 汇编（Assembly）**

汇编是将编译器生成的汇编代码转换为机器代码的过程。汇编器会将汇编语言翻译成目标机器的二进制指令，生成目标文件（通常是 `.o` 或 `.obj` 文件）。

- **目标文件**：目标文件包含了机器代码，但尚未解决外部符号引用（如函数调用、全局变量等）。
- **平台相关性**：汇编器生成的目标文件是与特定硬件架构相关的，例如 x86、ARM 等。

#### **2.4 链接（Linking）**

链接是编译过程的最后一步，负责将多个目标文件和库文件合并成一个可执行文件。链接器会解析目标文件中的外部符号引用，并将它们与相应的定义链接起来。

- **静态链接**：将库文件的代码直接嵌入到可执行文件中。这种方式生成的可执行文件较大，但运行时不需要额外的库文件。
- **动态链接**：只在可执行文件中记录库文件的引用，在运行时动态加载所需的库文件。这种方式生成的可执行文件较小，但需要依赖外部库文件。

**示例**：
假设我们有两个源文件 `main.cpp` 和 `func.cpp`，其中 `func.cpp` 包含一个函数 `int add(int a, int b)`。编译器会分别编译这两个文件为目标文件 `main.o` 和 `func.o`，然后链接器将它们合并成一个可执行文件 `program.exe`。

## **基本语法**

C++ 的基本语法是学习这门语言的基础。它包括程序的结构、数据类型、变量与常量、输入输出等内容。以下将对这些内容进行详细讲解。

---

### **1. 程序结构：`main()` 函数、注释、头文件**

#### **1.1 `main()` 函数**

`main()` 是 C++ 程序的入口点，所有的 C++ 程序都从 `main()` 函数开始执行。`main()` 函数的返回值和参数有以下两种常见形式：

- **无参数版本**：

  ```cpp
  int main() {
      // 程序代码
      return 0;
  }
  ```

  - 返回值为 `int` 类型，通常返回 `0` 表示程序成功执行。
  
- **带参数版本**（用于命令行参数）：

  ```cpp
  int main(int argc, char* argv[]) {
      // argc: 参数个数
      // argv: 参数数组
      return 0;
  }
  ```

  - `argc` 表示命令行参数的数量，`argv` 是一个字符串数组，存储了每个参数的内容。

#### **1.2 注释**

C++ 提供了两种注释方式，用于解释代码或临时禁用某段代码：

- **单行注释**：使用 `//` 开头，注释内容写在同一行。

  ```cpp
  // 这是一个单行注释
  int x = 10; // 这也是注释
  ```

- **多行注释**：使用 `/*` 和 `*/` 包裹注释内容，可以跨越多行。

  ```cpp
  /* 
   * 这是一个多行注释
   * 可以跨越多行书写
   */
  ```

#### **1.3 头文件**

头文件包含了函数声明、类定义和其他必要的信息，通常以 `.h` 或 `.hpp` 结尾。C++ 中常见的头文件包括：

- **标准库头文件**：如 `<iostream>`, `<vector>`, `<string>` 等。
- **自定义头文件**：用户自己编写的头文件，使用 `#include "filename.h"` 引入。

例如：

```cpp
#include <iostream> // 标准输入输出库
#include "myheader.h" // 自定义头文件
```

---

### **2. 数据类型**

#### **2.1 基本数据类型**

C++ 提供了几种基本数据类型，用于存储不同类型的数据：

- **整数类型**：
  - `int`：用于存储整数，默认大小为 4 字节（32 位系统上）。
  - 示例：`int x = 10;`
  
- **浮点数类型**：
  - `float`：单精度浮点数，通常占用 4 字节。
  - `double`：双精度浮点数，通常占用 8 字节。
  - 示例：`float pi = 3.14f; double d = 2.718;`
  
- **字符类型**：
  - `char`：用于存储单个字符，通常占用 1 字节。
  - 示例：`char c = 'A';`
  
- **布尔类型**：
  - `bool`：用于存储逻辑值，只有两个可能的值：`true` 或 `false`。
  - 示例：`bool flag = true;`

#### **2.2 类型修饰符**

类型修饰符用于改变基本数据类型的特性，主要包括以下几种：

- **`signed` 和 `unsigned`**：
  - `signed`：表示有符号数（默认），可以存储正数和负数。
  - `unsigned`：表示无符号数，只能存储非负数。
  - 示例：`unsigned int x = 255; signed int y = -10;`
  
- **`short` 和 `long`**：
  - `short`：短整型，通常占用 2 字节。
  - `long`：长整型，通常占用 4 或 8 字节。
  - 示例：`short s = 32767; long l = 123456789;`

#### **2.3 枚举类型（`enum`）**

枚举类型是一种用户定义的数据类型，用于定义一组命名的整数常量。

- **定义枚举类型**：

  ```cpp
  enum Color { RED, GREEN, BLUE };
  ```

  - 默认情况下，`RED` 的值为 0，`GREEN` 为 1，`BLUE` 为 2。
  
- **指定枚举值**：

  ```cpp
  enum Color { RED = 1, GREEN = 2, BLUE = 3 };
  ```

- **使用枚举类型**：

  ```cpp
  Color c = GREEN;
  if (c == GREEN) {
      std::cout << "The color is green." << std::endl;
  }
  ```

---

### **3. 变量与常量**

#### **3.1 定义与初始化**

- **定义变量**：在 C++ 中，变量必须先定义后使用。

  ```cpp
  int x;        // 定义一个整数变量
  float f = 3.14; // 定义并初始化一个浮点数
  ```

- **自动类型推导（`auto`）**：
  使用 `auto` 关键字可以让编译器自动推导变量的类型。

  ```cpp
  auto a = 10;    // 编译器推导为 int
  auto b = 3.14;  // 编译器推导为 double
  ```

#### **3.2 常量**

- **`const`**：用于定义不可修改的常量。

  ```cpp
  const int MAX_VALUE = 100;
  // MAX_VALUE = 200; // 错误：不能修改 const 常量
  ```

- **`constexpr`**：用于定义编译时常量。

  ```cpp
  constexpr double PI = 3.14159;
  ```

---

### **4. 输入输出**

#### **4.1 `cin` 和 `cout`**

C++ 使用 `cin` 和 `cout` 分别进行输入和输出操作，它们属于 `<iostream>` 头文件。

- **输出**：

  ```cpp
  #include <iostream>
  using namespace std;

  int main() {
      cout << "Hello, World!" << endl; // 输出字符串
      int x = 10;
      cout << "x = " << x << endl;    // 输出变量
      return 0;
  }
  ```

- **输入**：

  ```cpp
  int age;
  cout << "Enter your age: ";
  cin >> age; // 从键盘读取输入
  cout << "Your age is: " << age << endl;
  ```

#### **4.2 格式化输入输出（`iomanip`）**

`<iomanip>` 头文件提供了多种格式化输入输出的功能。

- **设置宽度**：

  ```cpp
  #include <iomanip>
  cout << setw(10) << "Hello" << endl; // 设置输出宽度为 10
  ```

- **设置精度**：

  ```cpp
  double pi = 3.14159;
  cout << setprecision(4) << pi << endl; // 输出保留 4 位小数
  ```

- **设置进制**：

  ```cpp
  int num = 255;
  cout << hex << num << endl; // 输出十六进制
  cout << oct << num << endl; // 输出八进制
  ```

---

### **总结**

C++ 的基本语法涵盖了程序的结构、数据类型、变量与常量、输入输出等核心概念。掌握这些基础知识是进一步学习 C++ 高级特性的前提。以下是关键点回顾：

1. **程序结构**：`main()` 是程序的入口点，注释用于解释代码，头文件包含必要的声明。
2. **数据类型**：C++ 提供了丰富的数据类型，包括整数、浮点数、字符、布尔等，并支持类型修饰符和枚举类型。
3. **变量与常量**：变量需要定义和初始化，`const` 和 `constexpr` 用于定义不可变的常量。
4. **输入输出**：`cin` 和 `cout` 是标准输入输出工具，`iomanip` 提供了格式化功能。

通过熟练掌握这些基础内容，你将能够编写简单的 C++ 程序，并为进一步学习复杂特性打下坚实的基础。

1. **运算符**
   - 算术运算符、关系运算符、逻辑运算符
   - 位运算符（`&`, `|`, `^`, `~`, `<<`, `>>`）
   - 赋值运算符与复合赋值运算符
   - 条件运算符（三元运算符）

2. **控制结构**
   - 条件语句：`if`, `else if`, `switch`
   - 循环语句：`for`, `while`, `do-while`
   - 跳转语句：`break`, `continue`, `goto`, `return`

3. **数组与字符串**
   - 数组定义与访问
   - 多维数组
   - 字符数组与字符串（C 风格字符串 vs `std::string`）

---

# **二、函数**

C++ 中的函数是程序的基本构建块，用于封装代码逻辑并实现代码复用。以下将详细讲解函数的基础知识、重载、默认参数、内联函数以及递归函数。

---

## **1. 函数基础**

### **1.1 函数定义与调用**

函数是执行特定任务的一段代码，它接受输入（称为参数）并返回输出（称为返回值）。函数的定义包括返回类型、函数名、参数列表和函数体。

- **函数定义**：

  ```cpp
  返回类型 函数名(参数列表) {
      // 函数体
      return 返回值;
  }
  ```

  - **返回类型**：函数返回的数据类型，可以是 `void`（表示无返回值）。
  - **函数名**：函数的标识符，遵循变量命名规则。
  - **参数列表**：函数接受的输入参数，可以为空。
  - **函数体**：包含函数的具体实现逻辑。

  示例：

  ```cpp
  int add(int a, int b) {
      return a + b;
  }
  ```

- **函数调用**：
  调用函数时，需要提供实际参数（实参），并根据需要接收返回值。

  ```cpp
  int result = add(3, 5); // 调用 add 函数，传入 3 和 5
  cout << "Result: " << result << endl; // 输出结果
  ```

### **1.2 参数传递**

C++ 支持三种主要的参数传递方式：值传递、指针传递和引用传递。

- **值传递**：
  值传递会复制实参的值到形参中，函数内部对形参的修改不会影响实参。

  ```cpp
  void increment(int x) {
      x++;
  }

  int main() {
      int a = 5;
      increment(a);
      cout << "a: " << a << endl; // 输出仍然是 5
  }
  ```

- **指针传递**：
  指针传递通过传递变量的地址，允许函数直接修改实参的值。

  ```cpp
  void increment(int* x) {
      (*x)++;
  }

  int main() {
      int a = 5;
      increment(&a);
      cout << "a: " << a << endl; // 输出为 6
  }
  ```

- **引用传递**：
  引用传递通过传递变量的别名，允许函数直接修改实参的值。

  ```cpp
  void increment(int& x) {
      x++;
  }

  int main() {
      int a = 5;
      increment(a);
      cout << "a: " << a << endl; // 输出为 6
  }
  ```

### **1.3 返回值与返回类型**

函数可以通过 `return` 语句返回一个值，返回类型必须与声明一致。如果函数不需要返回值，则使用 `void`。

- **有返回值的函数**：

  ```cpp
  double divide(int a, int b) {
      if (b == 0) {
          throw runtime_error("Division by zero");
      }
      return static_cast<double>(a) / b;
  }
  ```

- **无返回值的函数**：

  ```cpp
  void printMessage(const string& message) {
      cout << message << endl;
  }
  ```

---

## **2. 函数重载**

### **2.1 函数签名的概念**

函数签名由函数名和参数列表组成，不包括返回类型。两个函数的签名不同意味着它们可以有不同的参数类型或数量。

- **示例**：

  ```cpp
  void display(int x) {
      cout << "Integer: " << x << endl;
  }

  void display(double x) {
      cout << "Double: " << x << endl;
  }

  void display(const string& s) {
      cout << "String: " << s << endl;
  }
  ```

### **2.2 重载规则与注意事项**

- **重载条件**：
  - 函数名相同。
  - 参数列表不同（数量、类型或顺序不同）。
  
- **注意事项**：
  - 返回类型不能作为区分重载函数的依据。
  - 默认参数可能导致歧义，应避免重载时使用相同的参数数量和类型。

  **错误示例**：

  ```cpp
  int add(int a, int b) { return a + b; }
  double add(int a, int b) { return a + b; } // 错误：仅返回类型不同
  ```

---

## **3. 默认参数与内联函数**

### **3.1 默认参数的使用**

默认参数允许在函数定义时为某些参数指定默认值。如果调用时未提供实参，则使用默认值。

- **语法**：

  ```cpp
  返回类型 函数名(参数1, 参数2 = 默认值) {
      // 函数体
  }
  ```

- **示例**：

  ```cpp
  void greet(const string& name = "Guest") {
      cout << "Hello, " << name << "!" << endl;
  }

  int main() {
      greet();          // 输出：Hello, Guest!
      greet("Alice");   // 输出：Hello, Alice!
  }
  ```

### **3.2 内联函数（`inline` 关键字）**

内联函数是一种优化技术，编译器会尝试将函数调用替换为函数体本身，以减少函数调用的开销。

- **语法**：

  ```cpp
  inline 返回类型 函数名(参数列表) {
      // 函数体
  }
  ```

- **示例**：

  ```cpp
  inline int square(int x) {
      return x * x;
  }

  int main() {
      int result = square(5); // 编译器可能会将 square(5) 替换为 5 * 5
      cout << "Result: " << result << endl;
  }
  ```

- **注意事项**：
  - 内联函数适合短小的函数，复杂函数不适合内联。
  - 内联只是建议，编译器可能忽略。

---

## **4. 递归函数**

### **4.1 递归的基本原理**

递归是指函数直接或间接调用自身的过程。递归函数通常包含两个部分：

- **基准条件（Base Case）**：停止递归的条件。
- **递归步骤（Recursive Step）**：调用自身解决子问题。

- **示例**：
  计算阶乘：

  ```cpp
  int factorial(int n) {
      if (n <= 1) { // 基准条件
          return 1;
      }
      return n * factorial(n - 1); // 递归步骤
  }

  int main() {
      cout << "Factorial of 5: " << factorial(5) << endl; // 输出：120
  }
  ```

### **4.2 经典递归问题**

- **斐波那契数列**：
  斐波那契数列定义为：`F(0) = 0, F(1) = 1, F(n) = F(n-1) + F(n-2)`。

  ```cpp
  int fibonacci(int n) {
      if (n == 0) {
          return 0;
      }
      if (n == 1) {
          return 1;
      }
      return fibonacci(n - 1) + fibonacci(n - 2);
  }

  int main() {
      cout << "Fibonacci of 6: " << fibonacci(6) << endl; // 输出：8
  }
  ```

- **注意事项**：
  - 递归可能导致栈溢出，应避免深度过大的递归。
  - 对于性能要求高的场景，可以使用迭代代替递归。

---

# **三、指针与内存管理**

C++ 中的指针和内存管理是编程的核心概念之一。它们直接影响程序的性能、灵活性以及安全性。以下将详细讲解指针基础、动态内存分配、引用以及智能指针的相关内容。

---

## **1. 指针基础**

### **1.1 指针的概念与声明**

指针是一种特殊的变量，用于存储内存地址。通过指针，可以间接访问和操作内存中的数据。

- **声明指针**：

  ```cpp
  数据类型* 指针名;
  ```

  - `数据类型`：指针所指向的数据类型。
  - `*`：表示这是一个指针变量。

  示例：

  ```cpp
  int x = 10;   // 定义一个整数变量
  int* ptr = &x; // 定义一个指针，指向 x 的地址
  ```

- **指针的初始化**：
  指针必须被初始化为有效地址或 `nullptr`（C++11 引入），否则可能导致未定义行为。

  ```cpp
  int* ptr = nullptr; // 初始化为空指针
  ```

### **1.2 指针的解引用与地址操作**

- **取地址操作符（`&`）**：
  使用 `&` 获取变量的内存地址。

  ```cpp
  int x = 42;
  int* ptr = &x; // ptr 存储了 x 的地址
  ```

- **解引用操作符（`*`）**：
  使用 `*` 访问指针所指向的内存中的值。

  ```cpp
  int value = *ptr; // 解引用 ptr，获取 x 的值（42）
  ```

- **示例**：

  ```cpp
  int main() {
      int a = 5;
      int* p = &a; // p 指向 a 的地址
      cout << "Address of a: " << p << endl; // 输出 a 的地址
      cout << "Value of a: " << *p << endl; // 输出 a 的值
      *p = 10; // 修改 a 的值
      cout << "New value of a: " << a << endl; // 输出 10
  }
  ```

### **1.3 指针与数组的关系**

在 C++ 中，数组名本质上是一个指向数组首元素的指针。

- **数组名作为指针**：

  ```cpp
  int arr[5] = {1, 2, 3, 4, 5};
  int* ptr = arr; // ptr 指向数组的第一个元素
  cout << *ptr << endl; // 输出 1
  cout << *(ptr + 1) << endl; // 输出 2
  ```

- **指针运算**：
  指针支持加减运算，用于遍历数组。

  ```cpp
  for (int i = 0; i < 5; ++i) {
      cout << *(ptr + i) << " "; // 输出数组元素
  }
  ```

---

## **2. 动态内存分配**

### **2.1 `new` 和 `delete` 的使用**

动态内存分配允许在程序运行时分配和释放内存。C++ 提供了 `new` 和 `delete` 操作符来管理堆内存。

- **分配单个对象**：

  ```cpp
  int* ptr = new int; // 分配一个整数
  *ptr = 42;          // 赋值
  delete ptr;         // 释放内存
  ```

- **分配数组**：

  ```cpp
  int* arr = new int[5]; // 分配一个包含 5 个整数的数组
  for (int i = 0; i < 5; ++i) {
      arr[i] = i + 1; // 初始化数组
  }
  delete[] arr; // 释放数组
  ```

- **注意事项**：
  - 必须使用 `delete` 或 `delete[]` 释放动态分配的内存，否则会导致内存泄漏。
  - 不要重复释放同一块内存。

### **2.2 动态数组的分配与释放**

动态数组允许在运行时决定数组的大小。

```cpp
int size;
cout << "Enter array size: ";
cin >> size;

int* dynamicArray = new int[size]; // 动态分配数组
for (int i = 0; i < size; ++i) {
    dynamicArray[i] = i * 2; // 初始化数组
}

// 使用数组...
delete[] dynamicArray; // 释放数组
```

---

## **3. 引用**

### **3.1 引用的定义与使用**

引用是变量的别名，它提供了一种更安全、更直观的方式来操作变量。

- **定义引用**：

  ```cpp
  数据类型& 引用名 = 变量名;
  ```

- **示例**：

  ```cpp
  int x = 10;
  int& ref = x; // ref 是 x 的引用
  ref = 20;     // 修改 ref 实际上修改了 x
  cout << "x: " << x << endl; // 输出 20
  ```

### **3.2 引用与指针的区别**

| 特性            | 引用                       | 指针                       |
|-----------------|----------------------------|----------------------------|
| 初始化         | 必须初始化为一个变量        | 可以初始化为 `nullptr` 或有效地址 |
| 再赋值         | 不能重新绑定到另一个变量    | 可以指向不同的地址          |
| 解引用         | 自动解引用                  | 需要显式解引用（`*`）       |
| 空值           | 不支持空值                 | 支持空值（`nullptr`）       |

---

## **4. 智能指针**

### **4.1 智能指针简介**

智能指针是 C++11 引入的一种资源管理工具，遵循 RAII（Resource Acquisition Is Initialization）原则，自动管理动态分配的内存，避免手动调用 `delete`。

- **常用智能指针**：
  - `std::unique_ptr`：独占所有权的智能指针。
  - `std::shared_ptr`：共享所有权的智能指针。
  - `std::weak_ptr`：辅助 `std::shared_ptr`，避免循环引用。

### **4.2`std::unique_ptr`**

`std::unique_ptr` 是一种独占所有权的智能指针，不能复制，只能移动。

- **示例**：

  ```cpp
  #include <memory>
  std::unique_ptr<int> ptr = std::make_unique<int>(42);
  cout << *ptr << endl; // 输出 42
  // 自动释放内存，无需手动调用 delete
  ```

### **4.3`std::shared_ptr`**

`std::shared_ptr` 允许多个指针共享同一个对象的所有权，引用计数为 0 时自动释放内存。

- **示例**：

  ```cpp
  #include <memory>
  std::shared_ptr<int> ptr1 = std::make_shared<int>(42);
  std::shared_ptr<int> ptr2 = ptr1; // 共享所有权
  cout << *ptr1 << " " << *ptr2 << endl; // 输出 42 42
  ```

### **4.4 `std::weak_ptr`**

`std::weak_ptr` 是一种弱引用智能指针，不增加引用计数，主要用于解决 `std::shared_ptr` 的循环引用问题。

- **示例**：

  ```cpp
  #include <memory>
  std::shared_ptr<int> ptr1 = std::make_shared<int>(42);
  std::weak_ptr<int> weakPtr = ptr1; // 不增加引用计数

  if (auto sharedPtr = weakPtr.lock()) { // 检查是否有效
      cout << *sharedPtr << endl; // 输出 42
  } else {
      cout << "Expired" << endl;
  }
  ```

### **4.5 RAII 原则**

RAII 是一种编程范式，强调资源的获取和释放应与对象的生命周期绑定。智能指针正是 RAII 的典型应用。

- **优点**：
  - 自动管理资源，减少内存泄漏。
  - 提高代码的可读性和安全性。

---

# **四、面向对象编程（OOP）**

面向对象编程（Object-Oriented Programming, OOP）是 C++ 的核心特性之一，它通过类和对象来组织代码，提供了一种更接近现实世界的建模方式。以下将详细介绍 OOP 的关键概念。

---

## **1. 类与对象**

### **1.1 类的定义与成员变量/函数**

- **类的定义**：
  类是一种用户定义的数据类型，用于封装数据和行为。类由成员变量（属性）和成员函数（方法）组成。

  ```cpp
  class 类名 {
      访问控制: // public, private, protected
          成员变量;
          成员函数;
  };
  ```

- **示例**：

  ```cpp
  class Rectangle {
  private:
      int width, height; // 私有成员变量
  public:
      void setDimensions(int w, int h) { // 公有成员函数
          width = w;
          height = h;
      }
      int getArea() const { // 常量成员函数
          return width * height;
      }
  };
  ```

### **1.2 对象的创建与使用**

对象是类的实例，可以通过类名创建对象，并调用其成员函数或访问成员变量。

- **创建对象**：

  ```cpp
  Rectangle rect; // 创建一个 Rectangle 对象
  ```

- **使用对象**：

  ```cpp
  rect.setDimensions(5, 10); // 调用公有成员函数
  cout << "Area: " << rect.getArea() << endl; // 输出面积
  ```

### **1.3 访问控制**

C++ 提供了三种访问控制修饰符，用于限制类成员的访问权限：

- **`public`**：任何地方都可以访问。
- **`private`**：只能在类内部访问。
- **`protected`**：子类可以访问，外部不可访问。

---

## **2. 构造函数与析构函数**

### **2.1 默认构造函数与参数化构造函数**

- **默认构造函数**：
  如果未定义任何构造函数，编译器会生成一个默认构造函数。

  ```cpp
  class Point {
  public:
      int x, y;
      Point() : x(0), y(0) {} // 默认构造函数
  };
  ```

- **参数化构造函数**：
  用于初始化对象时传递参数。

  ```cpp
  class Point {
  public:
      int x, y;
      Point(int a, int b) : x(a), y(b) {} // 参数化构造函数
  };
  ```

### **2.2 拷贝构造函数与赋值操作符**

- **拷贝构造函数**：
  用于通过现有对象初始化新对象。

  ```cpp
  class Point {
  public:
      int x, y;
      Point(const Point& other) : x(other.x), y(other.y) {} // 拷贝构造函数
  };
  ```

- **赋值操作符**：
  用于将一个对象的值赋给另一个对象。

  ```cpp
  Point& operator=(const Point& other) {
      if (this != &other) { // 防止自赋值
          x = other.x;
          y = other.y;
      }
      return *this;
  }
  ```

### **2.3 析构函数的作用**

析构函数在对象销毁时自动调用，用于释放资源。

- **定义析构函数**：

  ```cpp
  class FileHandler {
  public:
      FILE* file;
      FileHandler(const char* filename) {
          file = fopen(filename, "r");
      }
      ~FileHandler() { // 析构函数
          if (file) fclose(file);
      }
  };
  ```

---

## **3. 继承**

### **3.1 单继承与多继承**

- **单继承**：
  子类从一个父类派生。

  ```cpp
  class Animal {
  public:
      void eat() { cout << "Eating..." << endl; }
  };

  class Dog : public Animal {
  public:
      void bark() { cout << "Barking..." << endl; }
  };
  ```

- **多继承**：
  子类从多个父类派生。

  ```cpp
  class A {
  public:
      void funcA() { cout << "A" << endl; }
  };

  class B {
  public:
      void funcB() { cout << "B" << endl; }
  };

  class C : public A, public B {};
  ```

### **3.2 虚继承与虚基类**

虚继承用于解决多继承中的菱形问题，避免重复继承。

- **示例**：

  ```cpp
  class Base {
  public:
      int data;
  };

  class Derived1 : virtual public Base {};
  class Derived2 : virtual public Base {};

  class Final : public Derived1, public Derived2 {};
  ```

### **3.3 子类对父类成员的访问规则**

- 子类可以直接访问父类的 `public` 和 `protected` 成员。
- 子类无法直接访问父类的 `private` 成员。

---

## **4. 多态**

### **4.1 虚函数与纯虚函数**

- **虚函数**：
  使用 `virtual` 关键字声明，允许子类重写父类的方法。

  ```cpp
  class Animal {
  public:
      virtual void sound() { cout << "Animal sound" << endl; }
  };

  class Dog : public Animal {
  public:
      void sound() override { cout << "Woof!" << endl; }
  };
  ```

- **纯虚函数**：
  纯虚函数使类成为抽象类，不能实例化。

  ```cpp
  class Shape {
  public:
      virtual void draw() = 0; // 纯虚函数
  };
  ```

### **4.2 动态绑定与静态绑定**

- **动态绑定**：
  在运行时确定调用哪个函数（通过虚函数实现）。

  ```cpp
  Animal* animal = new Dog();
  animal->sound(); // 输出 "Woof!"
  ```

- **静态绑定**：
  在编译时确定调用哪个函数。

  ```cpp
  Dog dog;
  dog.sound(); // 输出 "Woof!"
  ```

### **4.3 抽象类与接口**

- **抽象类**：
  包含纯虚函数的类称为抽象类，不能实例化。

  ```cpp
  class AbstractClass {
  public:
      virtual void func() = 0;
  };
  ```

- **接口**：
  接口是一个只包含纯虚函数的抽象类。

  ```cpp
  class Interface {
  public:
      virtual void method1() = 0;
      virtual void method2() = 0;
  };
  ```

---

## **5. 其他 OOP 特性**

### **5.1 友元函数与友元类**

- **友元函数**：
  友元函数可以访问类的私有和保护成员。

  ```cpp
  class MyClass {
  private:
      int secret;
  public:
      friend void revealSecret(const MyClass& obj);
  };

  void revealSecret(const MyClass& obj) {
      cout << "Secret: " << obj.secret << endl;
  }
  ```

- **友元类**：
  整个类被声明为另一个类的友元。

  ```cpp
  class A {
  private:
      int data;
  public:
      friend class B;
  };

  class B {
  public:
      void access(A& a) {
          cout << a.data << endl;
      }
  };
  ```

### **5.2 静态成员变量与静态成员函数**

- **静态成员变量**：
  静态成员变量属于类本身，而不是某个对象。

  ```cpp
  class Counter {
  public:
      static int count;
      Counter() { count++; }
  };
  int Counter::count = 0;
  ```

- **静态成员函数**：
  静态成员函数只能访问静态成员变量。

  ```cpp
  class Counter {
  public:
      static int getCount() { return count; }
  };
  ```

### **5.3 运算符重载**

运算符重载允许自定义运算符的行为。

```cpp
class Complex {
public:
    double real, imag;
    Complex(double r = 0, double i = 0) : real(r), imag(i) {}

    Complex operator+(const Complex& other) {
        return Complex(real + other.real, imag + other.imag);
    }
};

int main() {
    Complex c1(1, 2), c2(3, 4);
    Complex c3 = c1 + c2; // 调用重载的 + 运算符
}
```

---

# **五、模板与泛型编程**

## **函数模板**

C++ 中的**函数模板**是一种泛型编程工具，它允许我们编写与类型无关的通用代码。通过模板，我们可以定义一个函数或类，使其可以处理多种数据类型，而无需为每种类型重复编写代码。以下是关于函数模板的详细讲解。

---

### **1. 模板的定义与实例化**

#### **1.1 函数模板的定义**

函数模板是通过 `template` 关键字定义的，它可以接受任意类型的参数。模板的定义包括以下几个部分：

- **`template` 声明**：用于声明模板参数。
- **模板参数列表**：指定模板参数（如类型参数）。
- **函数定义**：使用模板参数作为函数的参数类型或返回类型。

**语法**：

```cpp
template <typename T> // 或者 template <class T>
返回类型 函数名(参数列表) {
    // 函数体
}
```

- **`typename` 和 `class`**：
  - `typename` 和 `class` 是等价的，都可以用于声明模板参数。
  - 示例中通常使用 `typename` 表示更通用的含义。

**示例**：
以下是一个简单的函数模板，用于交换两个变量的值：

```cpp
#include <iostream>
using namespace std;

// 定义函数模板
template <typename T>
void swapValues(T& a, T& b) {
    T temp = a;
    a = b;
    b = temp;
}

int main() {
    int x = 5, y = 10;
    swapValues(x, y); // 调用模板函数
    cout << "x: " << x << ", y: " << y << endl; // 输出：x: 10, y: 5

    double a = 3.14, b = 2.71;
    swapValues(a, b); // 调用模板函数
    cout << "a: " << a << ", b: " << b << endl; // 输出：a: 2.71, b: 3.14
}
```

#### **1.2 模板的实例化**

当调用模板函数时，编译器会根据传递的实际参数类型生成具体的函数实例。这一过程称为**模板实例化**。

- **显式实例化**：
  我们可以手动指定模板参数类型，例如：

  ```cpp
  swapValues<int>(x, y); // 显式指定模板参数类型为 int
  ```

- **隐式实例化**：
  编译器会自动推导模板参数类型，例如：

  ```cpp
  swapValues(x, y); // 编译器推导出 T 为 int
  ```

---

### **2. 泛型函数的使用**

#### **2.1 泛型函数的优势**

泛型函数的核心优势在于其通用性。它们可以处理任意类型的数据，从而减少代码重复，提高代码复用性。

**示例**：
以下是一个泛型函数，用于比较两个值并返回较大的值：

```cpp
#include <iostream>
using namespace std;

// 定义泛型函数模板
template <typename T>
T maxVal(T a, T b) {
    return (a > b) ? a : b;
}

int main() {
    cout << "Max of 5 and 10: " << maxVal(5, 10) << endl; // 输出：10
    cout << "Max of 3.14 and 2.71: " << maxVal(3.14, 2.71) << endl; // 输出：3.14
    cout << "Max of 'a' and 'z': " << maxVal('a', 'z') << endl; // 输出：z
}
```

在这个例子中，`maxVal` 函数可以处理整数、浮点数和字符等多种类型的数据。

#### **2.2 多个模板参数**

函数模板可以有多个模板参数，以支持不同类型的输入。

**示例**：
以下是一个泛型函数，用于将一个类型的值转换为另一个类型的值：

```cpp
#include <iostream>
using namespace std;

// 定义带有两个模板参数的函数模板
template <typename T1, typename T2>
T2 convertType(T1 value) {
    return static_cast<T2>(value);
}

int main() {
    int x = 42;
    double d = convertType<int, double>(x); // 将 int 转换为 double
    cout << "Converted value: " << d << endl; // 输出：42.0
}
```

#### **2.3 默认模板参数**

模板参数可以设置默认值，简化调用。

**示例**：
以下是一个带有默认模板参数的函数模板：

```cpp
#include <iostream>
using namespace std;

// 定义带有默认模板参数的函数模板
template <typename T = int>
T add(T a, T b) {
    return a + b;
}

int main() {
    cout << "Sum: " << add(5, 10) << endl; // 使用默认类型 int
    cout << "Sum: " << add<double>(3.14, 2.71) << endl; // 指定类型 double
}
```

---

### **3. 模板的限制与注意事项**

尽管函数模板非常强大，但在使用时需要注意以下几点：

#### **3.1 类型约束**

模板参数必须支持模板函数中使用的操作。如果某种类型不支持某些操作，会导致编译错误。

**示例**：

```cpp
template <typename T>
void printSize(T value) {
    cout << sizeof(value) << endl;
}

int main() {
    printSize(5);        // 正常工作
    printSize("Hello");  // 错误：无法对字符串字面量使用 sizeof
}
```

#### **3.2 模板的编译期检查**

模板代码在编译时会被实例化，因此所有错误都会在编译阶段被发现。这可能导致复杂的错误信息。

#### **3.3 模板特化**

有时我们需要为特定类型提供特殊的实现，这时可以使用**模板特化**。

**示例**：
以下是对 `printSize` 函数模板的特化实现：

```cpp
template <>
void printSize(const char* value) {
    cout << strlen(value) << endl;
}

int main() {
    printSize(5);         // 输出：4（假设 int 占 4 字节）
    printSize("Hello");   // 输出：5
}
```

---

## **类模板**

类模板是 C++ 中实现泛型编程的另一种重要工具。与函数模板类似，类模板允许我们定义可以处理多种数据类型的通用类。通过类模板，我们可以创建适用于不同数据类型的容器、算法和其他复杂结构。

以下是关于类模板的详细讲解，包括**定义与实例化**、**特化与偏特化**等内容。

---

### **1. 模板类的定义与实例化**

#### **1.1 类模板的定义**

类模板通过 `template` 关键字定义，其语法类似于函数模板。类模板允许我们定义一个通用类，其中的成员变量和成员函数可以使用模板参数作为类型。

**语法**：

```cpp
template <typename T>
class 类名 {
private:
    // 私有成员变量
public:
    // 构造函数、析构函数、成员函数等
};
```

- **模板参数**：`typename T` 或 `class T` 声明模板参数。
- **成员变量和函数**：可以使用模板参数作为类型。

**示例**：
以下是一个简单的类模板，用于表示一个动态数组：

```cpp
#include <iostream>
using namespace std;

// 定义类模板
template <typename T>
class DynamicArray {
private:
    T* data;       // 动态分配的数组
    int size;      // 数组大小

public:
    // 构造函数
    DynamicArray(int s) : size(s) {
        data = new T[size];
    }

    // 析构函数
    ~DynamicArray() {
        delete[] data;
    }

    // 设置元素值
    void setElement(int index, const T& value) {
        if (index >= 0 && index < size) {
            data[index] = value;
        }
    }

    // 获取元素值
    T getElement(int index) const {
        if (index >= 0 && index < size) {
            return data[index];
        }
        return T(); // 返回默认值
    }
};

int main() {
    DynamicArray<int> intArray(5); // 创建一个存储整数的动态数组
    intArray.setElement(0, 10);
    cout << "Element at index 0: " << intArray.getElement(0) << endl;

    DynamicArray<double> doubleArray(3); // 创建一个存储浮点数的动态数组
    doubleArray.setElement(1, 3.14);
    cout << "Element at index 1: " << doubleArray.getElement(1) << endl;
}
```

#### **1.2 模板类的实例化**

类模板的实例化与函数模板类似，分为显式实例化和隐式实例化。

- **显式实例化**：
  我们可以手动指定模板参数类型，例如：

  ```cpp
  DynamicArray<int> intArray(5); // 显式指定模板参数为 int
  ```

- **隐式实例化**：
  编译器会根据传递的实际参数类型推导模板参数。例如：

  ```cpp
  DynamicArray array(5); // 编译器推导出 T 为 int（C++17 起支持自动类型推导）
  ```

---

### **2. 模板类的特化与偏特化**

尽管类模板非常灵活，但在某些情况下，我们需要为特定类型提供特殊的实现。这时可以使用**模板特化**或**偏特化**。

#### **2.1 模板特化**

模板特化是指为某个特定类型提供专门的实现。当模板参数匹配特定类型时，编译器会选择特化的版本。

**语法**：

```cpp
template <>
class 类名<特定类型> {
    // 特化实现
};
```

**示例**：
以下是对 `DynamicArray` 类模板的特化实现，用于处理字符数组：

```cpp
template <>
class DynamicArray<char> {
private:
    char* data;
    int size;

public:
    DynamicArray(int s) : size(s) {
        data = new char[size];
    }

    ~DynamicArray() {
        delete[] data;
    }

    void setElement(int index, char value) {
        if (index >= 0 && index < size) {
            data[index] = value;
        }
    }

    char getElement(int index) const {
        if (index >= 0 && index < size) {
            return data[index];
        }
        return '\0'; // 返回空字符
    }

    void printAll() const {
        for (int i = 0; i < size; ++i) {
            cout << data[i] << " ";
        }
        cout << endl;
    }
};

int main() {
    DynamicArray<char> charArray(3); // 使用特化版本
    charArray.setElement(0, 'A');
    charArray.setElement(1, 'B');
    charArray.printAll(); // 输出：A B \0
}
```

#### **2.2 偏特化**

偏特化是指为部分模板参数提供专门的实现。它允许我们针对某些模板参数的子集进行特化。

**语法**：

```cpp
template <typename T1, typename T2>
class 类名<T1, 特定类型> {
    // 偏特化实现
};
```

**示例**：
以下是一个偏特化的例子，假设我们有一个模板类 `Pair`，并为其第二个参数为 `int` 的情况提供特化：

```cpp
#include <iostream>
using namespace std;

// 通用模板类
template <typename T1, typename T2>
class Pair {
public:
    T1 first;
    T2 second;

    Pair(T1 f, T2 s) : first(f), second(s) {}

    void print() const {
        cout << "Generic Pair: " << first << ", " << second << endl;
    }
};

// 偏特化：第二个参数为 int
template <typename T1>
class Pair<T1, int> {
public:
    T1 first;
    int second;

    Pair(T1 f, int s) : first(f), second(s) {}

    void print() const {
        cout << "Specialized Pair: " << first << ", " << second << endl;
    }
};

int main() {
    Pair<double, double> p1(3.14, 2.71);
    p1.print(); // 输出：Generic Pair: 3.14, 2.71

    Pair<string, int> p2("Hello", 42);
    p2.print(); // 输出：Specialized Pair: Hello, 42
}
```

---

## **STL（标准模板库）**

C++ 标准模板库（Standard Template Library，简称 STL）是 C++ 的核心组件之一，提供了一组高效的工具来处理数据结构和算法。STL 主要由**容器**、**迭代器**和**算法**三部分组成。以下将详细讲解这些内容。

---

### **1. 容器**

容器是 STL 中用于存储和管理数据的类模板。根据数据的组织方式，容器可以分为**序列容器**和**关联容器**。

#### **1.1 序列容器**

序列容器以线性方式存储元素，支持按顺序访问。

- **`vector`**：
  - 动态数组，支持随机访问。
  - 元素在内存中连续存储，插入和删除操作效率较低（O(n)），但访问速度快（O(1)）。
  - **常用操作**：

    ```cpp
    #include <vector>
    vector<int> v = {1, 2, 3};
    v.push_back(4); // 添加元素
    cout << v[0] << endl; // 输出第一个元素
    ```

- **`list`**：
  - 双向链表，支持快速插入和删除（O(1)），但不支持随机访问。
  - **常用操作**：

    ```cpp
    #include <list>
    list<int> l = {1, 2, 3};
    l.push_back(4); // 在末尾添加元素
    l.push_front(0); // 在开头添加元素
    ```

- **`deque`**：
  - 双端队列，支持在两端高效插入和删除（O(1)），同时支持随机访问。
  - **常用操作**：

    ```cpp
    #include <deque>
    deque<int> d = {1, 2, 3};
    d.push_front(0); // 在开头添加元素
    d.push_back(4); // 在末尾添加元素
    ```

#### **1.2 关联容器**

关联容器以键值对的形式存储数据，通常基于平衡二叉树或哈希表实现。

- **`set`**：
  - 集合，存储唯一且有序的元素。
  - 基于红黑树实现，插入、删除和查找操作的时间复杂度为 O(log n)。
  - **常用操作**：

    ```cpp
    #include <set>
    set<int> s = {1, 2, 3};
    s.insert(4); // 插入元素
    s.erase(2); // 删除元素
    ```

- **`map`**：
  - 映射，存储键值对，键唯一且有序。
  - **常用操作**：

    ```cpp
    #include <map>
    map<string, int> m;
    m["Alice"] = 25; // 插入键值对
    cout << m["Alice"] << endl; // 访问值
    ```

- **`unordered_set` 和 `unordered_map`**：
  - 基于哈希表实现，元素无序，插入、删除和查找操作的时间复杂度平均为 O(1)。
  - **常用操作**：

    ```cpp
    #include <unordered_set>
    unordered_set<int> us = {1, 2, 3};
    us.insert(4); // 插入元素

    #include <unordered_map>
    unordered_map<string, int> um;
    um["Bob"] = 30; // 插入键值对
    ```

---

### **2. 迭代器**

迭代器是 STL 中用于遍历容器的工具，类似于指针。它提供了统一的接口来访问容器中的元素。

#### **2.1 迭代器的分类**

根据功能，迭代器可以分为以下几种类型：

- **输入迭代器**：只能单向遍历，支持读取操作。
- **输出迭代器**：只能单向遍历，支持写入操作。
- **前向迭代器**：支持单向遍历，可读可写。
- **双向迭代器**：支持双向遍历（如 `list` 和 `set`）。
- **随机访问迭代器**：支持随机访问（如 `vector` 和 `deque`）。

#### **2.2 迭代器的使用**

迭代器通过容器的成员函数（如 `begin()` 和 `end()`）获取。

- **示例**：

  ```cpp
  #include <vector>
  #include <iostream>
  using namespace std;

  int main() {
      vector<int> v = {1, 2, 3, 4, 5};
      for (auto it = v.begin(); it != v.end(); ++it) {
          cout << *it << " "; // 输出：1 2 3 4 5
      }
      cout << endl;

      // 使用范围 for 循环（C++11 起）
      for (const auto& elem : v) {
          cout << elem << " ";
      }
      cout << endl;
  }
  ```

---

### **3. 算法**

STL 提供了大量通用算法，可以直接应用于容器和迭代器。这些算法定义在 `<algorithm>` 头文件中。

#### **3.1 常用算法**

以下是 STL 中常用的算法及其示例：

- **`sort`**：
  对容器中的元素进行排序。

  ```cpp
  #include <vector>
  #include <algorithm>
  #include <iostream>
  using namespace std;

  int main() {
      vector<int> v = {5, 2, 8, 1, 9};
      sort(v.begin(), v.end()); // 默认升序排序
      for (int x : v) cout << x << " "; // 输出：1 2 5 8 9
      cout << endl;
  }
  ```

- **`find`**：
  查找指定值的元素，返回指向该元素的迭代器。

  ```cpp
  #include <vector>
  #include <algorithm>
  #include <iostream>
  using namespace std;

  int main() {
      vector<int> v = {1, 2, 3, 4, 5};
      auto it = find(v.begin(), v.end(), 3);
      if (it != v.end()) {
          cout << "Found: " << *it << endl; // 输出：Found: 3
      }
  }
  ```

- **`accumulate`**：
  计算容器中元素的累加和。

  ```cpp
  #include <vector>
  #include <numeric>
  #include <iostream>
  using namespace std;

  int main() {
      vector<int> v = {1, 2, 3, 4, 5};
      int sum = accumulate(v.begin(), v.end(), 0); // 初始值为 0
      cout << "Sum: " << sum << endl; // 输出：Sum: 15
  }
  ```

- **`count`**：
  统计容器中某个值出现的次数。

  ```cpp
  #include <vector>
  #include <algorithm>
  #include <iostream>
  using namespace std;

  int main() {
      vector<int> v = {1, 2, 3, 2, 4};
      int cnt = count(v.begin(), v.end(), 2);
      cout << "Count of 2: " << cnt << endl; // 输出：Count of 2: 2
  }
  ```

- **`transform`**：
  对容器中的每个元素应用一个函数，并将结果存储到另一个容器中。

  ```cpp
  #include <vector>
  #include <algorithm>
  #include <iostream>
  using namespace std;

  int square(int x) {
      return x * x;
  }

  int main() {
      vector<int> v1 = {1, 2, 3, 4};
      vector<int> v2(v1.size());
      transform(v1.begin(), v1.end(), v2.begin(), square);
      for (int x : v2) cout << x << " "; // 输出：1 4 9 16
      cout << endl;
  }
  ```

---

# **六、异常处理**

异常处理是 C++ 中用于处理运行时错误的一种机制。通过异常处理，程序可以在遇到错误时优雅地退出或恢复，而不会导致崩溃。以下是关于异常处理的详细讲解。

---

## **1. 异常机制**

### **1.1 `try`, `catch`, `throw`**

C++ 的异常处理机制基于三个关键字：`try`, `catch`, 和 `throw`。

- **`try` 块**：
  - 用于包裹可能抛出异常的代码。
  - 如果在 `try` 块中发生异常，程序会跳转到匹配的 `catch` 块进行处理。

- **`throw` 表达式**：
  - 用于抛出异常，可以抛出任何类型的值（通常是对象）。
  - 抛出异常后，程序会立即跳出当前函数，并寻找最近的匹配 `catch` 块。

- **`catch` 块**：
  - 用于捕获和处理特定类型的异常。
  - 可以有多个 `catch` 块，分别处理不同类型的异常。

**语法**：

```cpp
try {
    // 可能抛出异常的代码
} catch (异常类型1 参数) {
    // 处理异常类型1
} catch (异常类型2 参数) {
    // 处理异常类型2
} catch (...) { // 捕获所有异常
    // 处理未知异常
}
```

**示例**：
以下是一个简单的异常处理示例：

```cpp
#include <iostream>
using namespace std;

void divide(int a, int b) {
    if (b == 0) {
        throw runtime_error("Division by zero"); // 抛出异常
    }
    cout << "Result: " << a / b << endl;
}

int main() {
    try {
        divide(10, 0); // 尝试除以零
    } catch (const exception& e) { // 捕获标准异常
        cout << "Error: " << e.what() << endl; // 输出错误信息
    }
    return 0;
}
```

### **1.2 自定义异常类**

除了使用标准异常类（如 `std::runtime_error`），我们还可以定义自己的异常类来表示特定的错误。

**示例**：
以下是一个自定义异常类的示例：

```cpp
#include <iostream>
#include <string>
using namespace std;

// 定义自定义异常类
class MyException : public exception {
private:
    string message;
public:
    MyException(const string& msg) : message(msg) {}
    const char* what() const noexcept override {
        return message.c_str();
    }
};

void checkAge(int age) {
    if (age < 18) {
        throw MyException("Age must be at least 18");
    }
    cout << "Age is valid" << endl;
}

int main() {
    try {
        checkAge(16); // 尝试传递无效年龄
    } catch (const exception& e) {
        cout << "Error: " << e.what() << endl; // 输出自定义错误信息
    }
    return 0;
}
```

---

## **2. 异常安全**

异常安全是指在发生异常时，程序仍然能够保持一致的状态，避免资源泄漏或其他问题。以下是实现异常安全的关键原则。

### **2.1 异常安全的代码设计**

异常安全的设计通常遵循以下三种级别：

1. **基本保证**：
   - 程序在发生异常后能够保持一致的状态，但可能无法完成预期的操作。
   - 示例：如果文件读取失败，程序应确保文件句柄被正确关闭。

2. **强保证**：
   - 程序在发生异常后能够回滚到操作前的状态。
   - 示例：如果转账失败，账户余额应恢复到初始状态。

3. **无抛出保证**：
   - 程序在某些关键操作中保证不会抛出异常。
   - 示例：析构函数不应抛出异常，否则可能导致未定义行为。

**示例**：
以下是一个实现强保证的示例：

```cpp
#include <iostream>
#include <vector>
#include <stdexcept>
using namespace std;

void appendElements(vector<int>& v, int x, int y) {
    vector<int> temp = v; // 创建临时副本
    temp.push_back(x);
    temp.push_back(y);

    // 如果执行到这里没有抛出异常，则交换数据
    v.swap(temp); // 提供强保证
}

int main() {
    vector<int> v = {1, 2, 3};
    try {
        appendElements(v, 4, 5);
    } catch (const exception& e) {
        cout << "Error: " << e.what() << endl;
    }
    for (int x : v) cout << x << " "; // 输出：1 2 3 4 5
    cout << endl;
    return 0;
}
```

### **2.2 RAII 在异常处理中的作用**

RAII（Resource Acquisition Is Initialization）是一种编程范式，强调资源的获取和释放应与对象的生命周期绑定。通过 RAII，我们可以确保即使发生异常，资源也能被正确释放。

- **智能指针**：
  使用智能指针（如 `std::unique_ptr` 和 `std::shared_ptr`）可以自动管理动态分配的内存，避免内存泄漏。

**示例**：
以下是一个使用 `std::unique_ptr` 的示例：

```cpp
#include <iostream>
#include <memory>
using namespace std;

void allocateMemory() {
    unique_ptr<int> ptr(new int(42)); // 动态分配内存
    if (*ptr != 42) {
        throw runtime_error("Unexpected value");
    }
    // 不需要手动释放内存，智能指针会在离开作用域时自动释放
}

int main() {
    try {
        allocateMemory();
    } catch (const exception& e) {
        cout << "Error: " << e.what() << endl;
    }
    return 0;
}
```

- **锁管理**：
  使用 `std::lock_guard` 或 `std::unique_lock` 可以确保在发生异常时自动释放锁。

**示例**：
以下是一个使用 `std::lock_guard` 的示例：

```cpp
#include <iostream>
#include <thread>
#include <mutex>
using namespace std;

mutex mtx;

void criticalSection() {
    lock_guard<mutex> lock(mtx); // 自动加锁
    cout << "Thread ID: " << this_thread::get_id() << endl;
    // 如果发生异常，锁会自动释放
}

int main() {
    thread t1(criticalSection);
    thread t2(criticalSection);
    t1.join();
    t2.join();
    return 0;
}
```

---

# **七、高级特性**

C++ 的高级特性是现代 C++ 编程的重要组成部分，涵盖了从 Lambda 表达式到多线程编程、移动语义、类型推导以及新标准引入的现代化功能。以下将详细讲解这些内容。

---

## **1. Lambda 表达式**

Lambda 表达式是一种匿名函数，允许我们以简洁的方式定义内联函数对象，常用于 STL 算法中。

### **1.1 Lambda 的定义与捕获列表**
- **语法**：
  ```cpp
  [捕获列表](参数列表) -> 返回类型 {
      函数体
  }
  ```
  - **捕获列表**：指定 Lambda 表达式如何访问外部变量。
    - `[=]`：按值捕获所有外部变量。
    - `[&]`：按引用捕获所有外部变量。
    - `[x, &y]`：按值捕获 `x`，按引用捕获 `y`。
  - **参数列表**：类似于普通函数的参数列表。
  - **返回类型**：可以省略，编译器会自动推导。

**示例**：
```cpp
#include <iostream>
using namespace std;

int main() {
    int x = 10, y = 20;

    // 按值捕获 x 和 y
    auto lambda = [x, y]() { return x + y; };
    cout << "Sum: " << lambda() << endl; // 输出：30

    // 按引用捕获 y
    auto lambdaRef = [&y](int a) { y += a; };
    lambdaRef(5);
    cout << "New y: " << y << endl; // 输出：25
}
```

### **1.2 Lambda 在 STL 中的应用**
Lambda 表达式广泛应用于 STL 算法中，例如 `std::for_each`, `std::sort` 等。

**示例**：
以下是一个使用 Lambda 表达式的例子，对 `vector` 进行排序和遍历：
```cpp
#include <vector>
#include <algorithm>
#include <iostream>
using namespace std;

int main() {
    vector<int> v = {5, 2, 8, 1, 9};

    // 使用 Lambda 表达式进行排序
    sort(v.begin(), v.end(), [](int a, int b) { return a > b; }); // 降序排序
    for (int x : v) cout << x << " "; // 输出：9 8 5 2 1
    cout << endl;

    // 使用 Lambda 表达式遍历
    for_each(v.begin(), v.end(), [](int x) { cout << x * 2 << " "; }); // 输出每个元素的两倍
    cout << endl;
}
```

---

## **2. 多线程与并发**

C++11 引入了 `<thread>` 头文件，支持多线程编程。以下是多线程与并发的核心概念。

### **2.1 线程的创建与管理（`std::thread`）**
- **创建线程**：
  使用 `std::thread` 创建线程，并传递一个可调用对象（如函数或 Lambda 表达式）。
  ```cpp
  #include <iostream>
  #include <thread>
  using namespace std;

  void threadFunction(int id) {
      cout << "Thread ID: " << id << endl;
  }

  int main() {
      thread t1(threadFunction, 1); // 创建线程
      thread t2(threadFunction, 2);

      t1.join(); // 等待线程 t1 完成
      t2.join(); // 等待线程 t2 完成
      return 0;
  }
  ```

### **2.2 同步机制（`std::mutex`, `std::lock_guard`）**
- **`std::mutex`**：
  互斥锁用于保护共享资源，避免多个线程同时访问。
  ```cpp
  #include <iostream>
  #include <thread>
  #include <mutex>
  using namespace std;

  mutex mtx;

  void increment(int& counter) {
      lock_guard<mutex> lock(mtx); // 自动加锁和解锁
      ++counter;
  }

  int main() {
      int counter = 0;
      thread t1(increment, ref(counter));
      thread t2(increment, ref(counter));

      t1.join();
      t2.join();

      cout << "Counter: " << counter << endl; // 输出：2
      return 0;
  }
  ```

### **2.3 条件变量与异步任务**
- **条件变量**：
  使用 `std::condition_variable` 实现线程间的同步。
  ```cpp
  #include <iostream>
  #include <thread>
  #include <mutex>
  #include <condition_variable>
  using namespace std;

  mutex mtx;
  condition_variable cv;
  bool ready = false;

  void worker() {
      unique_lock<mutex> lock(mtx);
      cv.wait(lock, [] { return ready; }); // 等待条件满足
      cout << "Worker thread is running" << endl;
  }

  int main() {
      thread t(worker);

      {
          lock_guard<mutex> lock(mtx);
          ready = true;
      }
      cv.notify_one(); // 唤醒等待的线程

      t.join();
      return 0;
  }
  ```

- **异步任务**：
  使用 `std::async` 执行异步任务并获取结果。
  ```cpp
  #include <iostream>
  #include <future>
  using namespace std;

  int compute() {
      return 42;
  }

  int main() {
      future<int> result = async(compute); // 异步执行 compute
      cout << "Result: " << result.get() << endl; // 获取结果
      return 0;
  }
  ```

---

## **3. 移动语义与右值引用**

### **3.1 左值与右值的概念**
- **左值**：有名字的对象，可以取地址。
- **右值**：临时对象，无法取地址。

### **3.2 移动构造函数与移动赋值操作符**
- **移动构造函数**：
  通过右值引用避免深拷贝，提高性能。
  ```cpp
  class MyClass {
  public:
      int* data;
      MyClass(int size) : data(new int[size]) {}
      ~MyClass() { delete[] data; }

      // 移动构造函数
      MyClass(MyClass&& other) noexcept : data(other.data) {
          other.data = nullptr; // 转移所有权
      }

      // 移动赋值操作符
      MyClass& operator=(MyClass&& other) noexcept {
          if (this != &other) {
              delete[] data;
              data = other.data;
              other.data = nullptr;
          }
          return *this;
      }
  };
  ```

### **3.3 `std::move` 的使用**
`std::move` 将左值转换为右值，触发移动语义。
```cpp
#include <iostream>
#include <vector>
#include <utility>
using namespace std;

int main() {
    vector<int> v1 = {1, 2, 3};
    vector<int> v2 = move(v1); // 转移 v1 的资源到 v2
    cout << "v1 size: " << v1.size() << endl; // 输出：0
    cout << "v2 size: " << v2.size() << endl; // 输出：3
    return 0;
}
```

---

## **4. 类型推导与自动类型**

### **4.1 `auto` 关键字**
`auto` 用于自动推导变量类型。
```cpp
auto x = 10;       // 推导为 int
auto y = 3.14;     // 推导为 double
auto z = "Hello";  // 推导为 const char*
```

### **4.2 `decltype` 的使用**
`decltype` 用于获取表达式的类型。
```cpp
int x = 5;
decltype(x) y = 10; // y 的类型为 int
```

---

## **5. 现代 C++ 特性**

### **5.1 C++11, C++14, C++17, C++20 新特性概述**
- **C++11**：
  - Lambda 表达式、智能指针、右值引用、`auto`。
- **C++14**：
  - 泛型 Lambda、返回类型后置语法。
- **C++17**：
  - 结构化绑定、`std::optional`, `std::variant`。
- **C++20**：
  - 概念（Concepts）、范围（Ranges）、协程（Coroutines）。

### **5.2 示例：结构化绑定与范围 for 循环**
- **结构化绑定**：
  ```cpp
  pair<int, string> p = {42, "Hello"};
  auto [id, name] = p; // 结构化绑定
  cout << "ID: " << id << ", Name: " << name << endl;
  ```

- **范围 for 循环**：
  ```cpp
  vector<int> v = {1, 2, 3};
  for (const auto& x : v) {
      cout << x << " ";
  }
  ```


---

# **八、实践与项目**

1. **常见算法与数据结构**
   - 排序算法（冒泡排序、快速排序等）
   - 查找算法（二分查找、哈希查找等）
   - 常见数据结构（链表、栈、队列、树、图）

2. **小型项目练习**
   - 设计一个简单的管理系统（如学生管理系统）
   - 实现一个游戏（如贪吃蛇、井字棋）
   - 使用 STL 容器实现复杂功能（如模拟银行排队系统）

3. **调试与优化**
   - 使用调试工具（如 GDB 或 IDE 调试器）
   - 性能优化技巧（如减少拷贝、使用高效算法）

---

# **九、补充知识**

1. **C++ 标准与规范**
   - 不同版本的 C++ 标准（C++98, C++11, C++14, C++17, C++20）
   - 标准的变化与新增特性

2. **编码风格与最佳实践**
   - 命名规范
   - 代码可读性与维护性
   - 避免常见错误（如内存泄漏、野指针）

3. **参考资料**
   - 《C++ Primer》
   - 《Effective C++》
   - 《The C++ Programming Language》
   - 官方文档与社区资源

---

# **十、C++算法应用**


## 🧰 1、常用 STL 容器 & 函数速查表

| 类型 | 用途 | 常见操作 |
|------|------|----------|
| `vector` | 可变数组 | `push_back`, `size`, `resize` |
| `string` | 字符串 | `substr`, `size`, `find` |
| `map` / `unordered_map` | 键值对映射 | `[]`, `find`, `insert` |
| `set` / `unordered_set` | 去重集合 | `insert`, `find`, `count` |
| `queue` | 队列 | `push`, `pop`, `front`, `size` |
| `stack` | 栈 | `push`, `pop`, `top` |
| `priority_queue` | 优先队列（堆） | `push`, `top`, `pop` |
| `deque` | 双端队列 | 支持两端插入删除 |
| `pair` / `tuple` | 多元组 | `make_pair`, `tie` |

---

## 📌 2、常见数据结构写法对比（Python vs C++）

| 功能 | Python | C++ |
|------|--------|-----|
| 动态数组 | `list = []` | `vector<int> v;` |
| 字符串 | `s = "abc"` | `string s = "abc";` |
| 字典 | `d = {}` | `unordered_map<string, int> m;` |
| 集合 | `s = set()` | `unordered_set<int> st;` |
| 队列 | `from collections import deque` | `queue<int> q;` |
| 栈 | `stack = []` | `stack<int> st;` |
| 最大堆 | `heapq`（取负数模拟） | `priority_queue<int> pq;` |
| 最小堆 | `heapq` | `priority_queue<int, vector<int>, greater<>> pq;` |
| 双端队列 | `deque` | `deque<int> dq;` |
| 排序 | `sorted(list)` | `sort(vec.begin(), vec.end());` |
| 查找 | `in` 运算符 | `find(st.begin(), st.end(), x) != st.end()` |
| 拷贝子串 | `s[1:3]` | `s.substr(1, 2)` |

---

## 🧱 3、C++ 刷题常用模板 & 技巧

### ✅ 1. 输入输出模板（LeetCode/牛客风格）

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

class Solution {
public:
    // 示例：最长公共子串
    string LCS(string str1, string str2) {
        // 实现逻辑
    }
};

int main() {
    string s1, s2;
    cin >> s1 >> s2;
    Solution sol;
    cout << sol.LCS(s1, s2) << endl;
    return 0;
}
```

---

### ✅ 2. 常用容器初始化与使用方式

#### 🧩 vector 初始化

```cpp
vector<int> v1;               // 空数组
vector<int> v2(5);            // 5个0
vector<int> v3{1, 2, 3};      // 初始化列表
vector<int> v4(v3);           // 拷贝构造
vector<int> v5(v3.begin(), v3.end()); // 从迭代器构造
```

#### 🧩 map 使用

```cpp
unordered_map<string, int> mp;
mp["a"] = 1;
if (mp.count("a")) { /* 存在 */ }
for (auto& p : mp) {
    cout << p.first << " " << p.second << endl;
}
```

#### 🧩 set 使用

```cpp
unordered_set<int> st;
st.insert(1);
if (st.find(1) != st.end()) {
    // 找到了
}
```

#### 🧩 queue / stack / priority_queue

```cpp
queue<int> q;
q.push(1);
cout << q.front(); q.pop();

stack<int> st;
st.push(1);
cout << st.top();

priority_queue<int> max_heap;       // 最大堆
priority_queue<int, vector<int>, greater<>> min_heap;  // 最小堆
```

---

### ✅ 3. 常用函数库

| 作用 | Python | C++ |
|------|--------|-----|
| 排序 | `sorted()` / `.sort()` | `sort(arr.begin(), arr.end())` |
| 二分查找 | `bisect` | `lower_bound`, `upper_bound` |
| 数组拷贝 | `arr[:]` | `vector<int> copy(arr.begin(), arr.end())` |
| 字符串转数字 | `int(s)` | `stoi(s)` |
| 数字转字符串 | `str(x)` | `to_string(x)` |
| 最大最小 | `max(a, b)` | `max(a, b)` |
| 绝对值 | `abs(x)` | `abs(x)` |
| 数组长度 | `len(arr)` | `arr.size()` |
| 字符串长度 | `len(s)` | `s.size()` |
| 打印调试 | `print()` | `cout << ... << endl;` |

---

### ✅ 4. 常用算法函数（头文件 `<algorithm>`）

```cpp
#include <algorithm>

sort(vec.begin(), vec.end());         // 升序排序
reverse(vec.begin(), vec.end());       // 反转
int sum = accumulate(vec.begin(), vec.end(), 0); // 求和
int cnt = count(vec.begin(), vec.end(), x);       // 统计x出现次数
auto it = find(vec.begin(), vec.end(), x);        // 查找x的位置
min_element(vec.begin(), vec.end());             // 最小值指针
max_element(vec.begin(), vec.end());             // 最大值指针
```

---

### ✅ 5. 字符串常用操作

```cpp
string s = "hello world";
int pos = s.find("world");     // 返回索引
string sub = s.substr(6, 5);   // 截取 "world"
replace(s.begin(), s.end(), ' ', '_');  // 替换空格为下划线
stringstream ss(s);
string word;
while (ss >> word) {  // 分割单词
    cout << word << endl;
}
```

---

### ✅ 6. C++11 新特性简化代码

```cpp
// 范围 for 循环
for (int num : nums) {
    cout << num << " ";
}

// auto 自动推导类型
auto it = mp.find(key);
auto res = to_string(123);

// lambda 表达式 + sort 自定义排序
sort(vec.begin(), vec.end(), [](int a, int b) {
    return abs(a) < abs(b);
});
```

---

## 🎁 四、C++ 刷题高频技巧汇总

| 场景 | 写法 |
|------|------|
| 构造二维数组 | `vector<vector<int>> dp(n, vector<int>(m, 0))` |
| 构造哈希表 | `unordered_map<string, int> mp;` |
| 遍历字符串 | `for (char c : s)` |
| 遍历 vector | `for (int x : vec)` |
| 打印调试 | `cout << x << endl;` |
| 快速读入 | `cin >> s;` |
| 快速读入多行 | `while (cin >> s)` |
| 去重 | `unordered_set<int> st(vec.begin(), vec.end())` |

---
