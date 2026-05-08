
# **一、Java 基础知识**

## **1. Java 简介**

### **Java 的历史与特点**

Java 是一种广泛使用的面向对象的编程语言，由 Sun Microsystems 公司于1995年发布。它的设计初衷是让程序员能够“编写一次，到处运行”（Write Once, Run Anywhere），这意味着编译后的Java代码可以在所有支持Java的平台上运行，无需重新编译。这种跨平台能力是通过Java虚拟机（JVM）实现的。

#### **Java的主要特点**

- **面向对象**：Java的设计理念基于面向对象编程（OOP），它几乎所有的概念都围绕着类和对象展开。
- **跨平台性**：由于Java程序是在JVM上运行，而JVM可以在任何操作系统上运行，这使得Java具有良好的跨平台特性。
- **健壮性和安全性**：Java提供了自动垃圾收集机制来管理内存，减少了内存泄漏的可能性；同时，Java的安全模型帮助防止了许多安全漏洞。
- **多线程处理**：Java内置了对多线程的支持，允许并发执行多个任务，提高了程序的效率。
- **动态性**：Java可以适应不断发展的环境，库中可以自由添加新方法和实例变量而不会影响现有的代码。

- JDK、JRE 和 JVM 的区别

- **JDK (Java Development Kit)**：是Java开发工具包，包含了开发Java应用程序所需的一切：JRE（Java运行时环境）、编译器（javac）和其他工具（如用于打包Java应用程序的jar工具）。简单来说，如果你想要开发Java应用程序，你需要安装JDK。

- **JRE (Java Runtime Environment)**：是Java运行时环境，它是运行Java应用程序所需的最小设置。JRE包含了Java虚拟机（JVM）、核心类库和其他文件，但不包含开发工具（如编译器或调试器）。如果你仅需要运行Java程序而不是开发它们，那么只需要安装JRE即可。

- **JVM (Java Virtual Machine)**：是Java虚拟机，它是一个抽象的计算机，在实际的计算机上模拟运行字节码的机器。JVM是Java实现跨平台的关键部分，因为编译后的Java代码是一组字节码，这些字节码可以在任何实现了JVM的平台上运行。JVM负责加载、验证、执行字节码，并提供运行时环境。

#### **基本语法**

- 数据类型与变量
  - 基本数据类型（`int`, `double`, `char`, `boolean` 等）
  - 引用数据类型（类、数组、接口等）
- 运算符
  - 算术运算符、关系运算符、逻辑运算符、位运算符等
- 流程控制语句
  - 条件语句（`if`, `switch`）
  - 循环语句（`for`, `while`, `do-while`）
  - 跳转语句（`break`, `continue`, `return`）

### **数组**

#### **一维数组和多维数组的定义与使用**

- **一维数组**：最简单的数组形式，用于存储一组相同类型的元素。在Java中定义一个一维数组的基本语法如下：

  ```java
  数据类型[] 数组名 = new 数据类型[数组长度];
  // 或者直接初始化
  数据类型[] 数组名 = {值1, 值2, ...};
  ```

  例如，定义并初始化一个整数型的一维数组：

  ```java
  int[] numbers = {1, 2, 3, 4, 5};
  ```

- **多维数组**：可以看作是“数组的数组”，其中二维数组是最常用的多维数组。定义一个二维数组的方式如下：

  ```java
  数据类型[][] 数组名 = new 数据类型[行数][列数];
  // 或者直接初始化
  数据类型[][] 数组名 = {{值1, 值2}, {值3, 值4}};
  ```

  例如，定义并初始化一个二维整数数组：

  ```java
  int[][] matrix = {{1, 2, 3}, {4, 5, 6}};
  ```

#### **数组的遍历与常见操作（排序、查找等）**

- **数组的遍历**：可以通过for循环或增强型for循环来遍历数组中的元素。

  - 对于一维数组：

    ```java
    for(int i = 0; i < numbers.length; i++) {
        System.out.println(numbers[i]);
    }
    // 使用增强型for循环
    for(int num : numbers) {
        System.out.println(num);
    }
    ```
  
  - 对于二维数组：

    ```java
    for(int i = 0; i < matrix.length; i++) {
        for(int j = 0; j < matrix[i].length; j++) {
            System.out.print(matrix[i][j] + " ");
        }
        System.out.println();
    }
    ```

- **排序**：Java提供了`Arrays.sort()`方法对数组进行排序。它可以直接对一维数组进行升序排列，对于对象数组，则需要实现`Comparable`接口或提供`Comparator`。

  ```java
  import java.util.Arrays;
  
  Arrays.sort(numbers); // 对一维数组numbers进行排序
  ```

- **查找**：对于基本数据类型的数组，可以使用线性搜索或者二分搜索（如果数组已经排序）。Java提供的`Arrays.binarySearch()`方法可用于已排序数组的快速查找。

  ```java
  int index = Arrays.binarySearch(numbers, 3); // 查找数字3的位置
  ```

### **字符串**

在 Java 中，字符串是通过 `String` 类实现的。字符串是不可变的对象，同时提供了许多实用的方法来操作和处理文本数据。此外，Java 还提供了 `StringBuilder` 和 `StringBuffer` 用于高效地处理可变字符串。

---

#### **`String` 类的不可变性**

- **不可变性**：  
  在 Java 中，`String` 对象一旦被创建，其内容就不能被修改。任何对字符串的操作（如拼接、截取等）都会生成一个新的 `String` 对象，而不是修改原有的对象。这种设计有助于提高安全性、线程安全性和性能优化。

  ```java
  String str = "Hello";
  str.concat(" World"); // 不会改变原字符串
  System.out.println(str); // 输出 "Hello"
  ```

  如果需要保存修改后的结果，可以将新字符串赋值给一个变量：

  ```java
  String newStr = str.concat(" World");
  System.out.println(newStr); // 输出 "Hello World"
  ```

---

#### **常用方法**

`String` 类提供了许多常用的方法，以下是一些常见的操作：

1. **`substring(int beginIndex, int endIndex)`**  
   返回从 `beginIndex` 到 `endIndex-1` 的子字符串。

   ```java
   String str = "HelloWorld";
   String sub = str.substring(0, 5); // "Hello"
   ```

2. **`concat(String str)`**  
   将指定的字符串连接到当前字符串的末尾。

   ```java
   String str1 = "Hello";
   String str2 = str1.concat(" World"); // "Hello World"
   ```

3. **`equals(Object obj)`**  
   比较两个字符串的内容是否相等（区分大小写）。

   ```java
   String str1 = "hello";
   String str2 = "HELLO";
   System.out.println(str1.equals(str2)); // false
   ```

4. **`equalsIgnoreCase(String anotherString)`**  
   比较两个字符串的内容是否相等（忽略大小写）。

   ```java
   System.out.println(str1.equalsIgnoreCase(str2)); // true
   ```

5. **`indexOf(String str)`**  
   返回指定子字符串第一次出现的位置索引，如果不存在则返回 -1。

   ```java
   String str = "Hello World";
   int index = str.indexOf("World"); // 6
   ```

6. **`length()`**  
   返回字符串的长度（字符数）。

   ```java
   String str = "Hello";
   System.out.println(str.length()); // 5
   ```

7. **`replace(CharSequence target, CharSequence replacement)`**  
   将字符串中的某个子串替换为另一个子串。

   ```java
   String str = "Hello World";
   String replaced = str.replace("World", "Java"); // "Hello Java"
   ```

8. **`toLowerCase()` 和 `toUpperCase()`**  
   将字符串转换为小写或大写。

   ```java
   String str = "Hello World";
   System.out.println(str.toLowerCase()); // "hello world"
   System.out.println(str.toUpperCase()); // "HELLO WORLD"
   ```

9. **`trim()`**  
   去除字符串两端的空白字符（空格、制表符等）。

   ```java
   String str = "   Hello World   ";
   System.out.println(str.trim()); // "Hello World"
   ```

---

#### **`StringBuilder` 和 `StringBuffer` 的区别与使用**

由于 `String` 是不可变的，频繁地进行字符串拼接会导致大量临时对象的创建，影响性能。为此，Java 提供了 `StringBuilder` 和 `StringBuffer` 两种可变字符串类。

- **`StringBuilder`**  
  - **特点**：非线程安全，但性能更高。
  - **适用场景**：适用于单线程环境下的字符串操作。
  - **示例**：

    ```java
    StringBuilder sb = new StringBuilder();
    sb.append("Hello");
    sb.append(" ");
    sb.append("World");
    System.out.println(sb.toString()); // "Hello World"
    ```

- **`StringBuffer`**  
  - **特点**：线程安全，性能略低于 `StringBuilder`。
  - **适用场景**：适用于多线程环境下的字符串操作。
  - **示例**：

    ```java
    StringBuffer sb = new StringBuffer();
    sb.append("Hello");
    sb.append(" ");
    sb.append("World");
    System.out.println(sb.toString()); // "Hello World"
    ```

##### **两者的区别**

| 特性               | `StringBuilder`          | `StringBuffer`           |
|--------------------|--------------------------|--------------------------|
| 线程安全性         | 非线程安全               | 线程安全                 |
| 性能               | 更高                     | 略低                     |
| 适用场景           | 单线程环境               | 多线程环境               |

---

# **二、面向对象编程（OOP）**

以下是关于 **面向对象编程（OOP）** 各部分内容的详细介绍，涵盖了 Java 中的核心概念和实现方法。

---

## **1. 类与对象**

### **1.1 类的定义与实例化**

- **类的定义**：
  - 类是面向对象编程的基本单元，用于描述具有相同属性和行为的对象。
  - 定义格式：

    ```java
    public class ClassName {
        // 成员变量
        private String name;
        private int age;

        // 构造方法
        public ClassName(String name, int age) {
            this.name = name;
            this.age = age;
        }

        // 成员方法
        public void display() {
            System.out.println("Name: " + name + ", Age: " + age);
        }
    }
    ```

- **实例化**：
  - 创建类的对象称为实例化，使用 `new` 关键字完成。

    ```java
    ClassName obj = new ClassName("Alice", 25);
    obj.display(); // 输出：Name: Alice, Age: 25
    ```

### **1.2 构造方法与重载**

- **构造方法**：
  - 构造方法用于初始化对象，方法名与类名相同，没有返回值。
  - 如果未定义构造方法，编译器会提供一个默认的无参构造方法。

    ```java
    public class Person {
        private String name;

        // 无参构造方法
        public Person() {}

        // 带参构造方法
        public Person(String name) {
            this.name = name;
        }
    }
    ```

- **构造方法重载**：
  - 可以定义多个构造方法，参数列表不同。

    ```java
    public class Person {
        private String name;
        private int age;

        public Person() {}
        public Person(String name) { this.name = name; }
        public Person(String name, int age) {
            this.name = name;
            this.age = age;
        }
    }
    ```

### **1.3 成员变量与局部变量的区别**

| 特性               | 成员变量                         | 局部变量                        |
|--------------------|----------------------------------|---------------------------------|
| **作用范围**       | 整个类                          | 方法或代码块中                 |
| **存储位置**       | 堆内存                          | 栈内存                         |
| **生命周期**       | 随对象创建而存在，随对象销毁而消失 | 随方法调用而存在，随方法结束而消失 |
| **默认值**         | 有默认值（如 `int` 默认为 0）   | 必须显式初始化，否则无法使用   |

---

## **2. 封装**

### **2.1 访问修饰符**

Java 提供了四种访问修饰符，用于控制类、成员变量和方法的访问权限：

- `private`：仅在当前类内可访问。
- `protected`：在同一包内或子类中可访问。
- `public`：任何地方都可访问。
- **默认**（无修饰符）：同一包内可访问。

示例：

```java
public class Person {
    private String name; // 私有变量

    public String getName() { // Getter 方法
        return name;
    }

    public void setName(String name) { // Setter 方法
        this.name = name;
    }
}
```

### **2.2 Getter 和 Setter 方法**

- **Getter 方法**：用于获取私有成员变量的值。
- **Setter 方法**：用于设置私有成员变量的值。
- 封装的好处：
  - 保护数据，避免直接修改。
  - 提供统一的访问接口。

---

## **3. 继承**

### **3.1 继承的概念与实现**

- **继承**是一种机制，允许一个类（子类）继承另一个类（父类）的属性和方法。
- 使用 `extends` 关键字实现继承。
- 示例：

    ```java
    public class Animal {
        protected String name;

        public void eat() {
            System.out.println(name + " is eating.");
        }
    }

    public class Dog extends Animal {
        public void bark() {
            System.out.println(name + " is barking.");
        }
    }
    ```

### **3.2 方法重写（@Override）**

- 子类可以重写父类的方法，以实现不同的行为。
- 使用 `@Override` 注解标记重写的方法。

    ```java
    public class Dog extends Animal {
        @Override
        public void eat() {
            System.out.println(name + " is eating bones.");
        }
    }
    ```

### **3.3 super 关键字的使用**

- `super` 用于引用父类的成员（变量、方法或构造方法）。
- 示例：

    ```java
    public class Dog extends Animal {
        public Dog(String name) {
            super(); // 调用父类构造方法
            this.name = name;
        }

        @Override
        public void eat() {
            super.eat(); // 调用父类方法
            System.out.println(name + " is eating bones.");
        }
    }
    ```

---

## **4. 多态**

### **4.1 编译时多态（方法重载）**

- 方法重载是指在同一个类中定义多个同名方法，但参数列表不同。
- 示例：

    ```java
    public class Calculator {
        public int add(int a, int b) {
            return a + b;
        }

        public double add(double a, double b) {
            return a + b;
        }
    }
    ```

### **4.2 运行时多态（方法重写）**

- 运行时多态通过继承和方法重写实现。
- 父类引用指向子类对象时，调用的方法由实际对象决定。

    ```java
    Animal animal = new Dog("Tom");
    animal.eat(); // 输出：Tom is eating bones.
    ```

### **4.3 向上转型与向下转型**

- **向上转型**：将子类对象赋值给父类引用（自动完成）。

    ```java
    Animal animal = new Dog("Tom"); // 向上转型
    ```

- **向下转型**：将父类引用强制转换为子类类型（需确保实际对象类型匹配）。

    ```java
    Dog dog = (Dog) animal; // 向下转型
    ```

---

## **5. 抽象类与接口**

### **5.1 抽象类的定义与使用**

- 抽象类使用 `abstract` 关键字定义，不能实例化。
- 包含抽象方法（无实现）和普通方法（有实现）。

    ```java
    public abstract class Shape {
        public abstract void draw(); // 抽象方法

        public void print() { // 普通方法
            System.out.println("This is a shape.");
        }
    }
    ```

### **5.2 接口的定义与实现**

- 接口使用 `interface` 关键字定义，包含抽象方法和默认方法。
- 类通过 `implements` 实现接口。

    ```java
    public interface Drawable {
        void draw(); // 抽象方法
    }

    public class Circle implements Drawable {
        @Override
        public void draw() {
            System.out.println("Drawing a circle.");
        }
    }
    ```

### **5.3 抽象类与接口的区别**

| 特性               | 抽象类                           | 接口                           |
|--------------------|----------------------------------|--------------------------------|
| **关键字**         | `abstract`                      | `interface`                   |
| **成员变量**       | 可以有普通变量                  | 只能有常量（`final`）         |
| **方法**           | 可以有普通方法和抽象方法         | 默认只有抽象方法（Java 8+ 支持默认方法） |
| **继承方式**       | 单继承（只能继承一个抽象类）     | 多继承（可以实现多个接口）    |

---

## **6. 内部类**

### **6.1 静态内部类**

- 静态内部类属于外部类本身，不依赖外部类实例。

    ```java
    public class OuterClass {
        static class StaticInnerClass {
            public void display() {
                System.out.println("Static Inner Class");
            }
        }
    }
    ```

### **6.2 成员内部类**

- 成员内部类属于外部类的实例，必须通过外部类实例访问。

    ```java
    public class OuterClass {
        class MemberInnerClass {
            public void display() {
                System.out.println("Member Inner Class");
            }
        }
    }
    ```

### **6.3 局部内部类**

- 局部内部类定义在方法或代码块中，仅在该范围内有效。

    ```java
    public class OuterClass {
        public void method() {
            class LocalInnerClass {
                public void display() {
                    System.out.println("Local Inner Class");
                }
            }
        }
    }
    ```

### **6.4 匿名内部类**

- 匿名内部类是没有名字的类，通常用于简化代码。

    ```java
    Runnable r = new Runnable() {
        @Override
        public void run() {
            System.out.println("Anonymous Inner Class");
        }
    };
    ```

---

## **7. 枚举**

### **7.1 枚举类型的定义与使用**

- 枚举使用 `enum` 关键字定义，表示一组固定的常量。

    ```java
    public enum Day {
        MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
    }
    ```

### **7.2 枚举与 `switch` 的结合**

- 枚举可以与 `switch` 结合使用，增强代码的可读性。

    ```java
    public void printDay(Day day) {
        switch (day) {
            case MONDAY:
                System.out.println("Start of the week");
                break;
            case FRIDAY:
                System.out.println("End of the week");
                break;
            default:
                System.out.println("Other day");
        }
    }
    ```

---

# **三、异常处理**

## **1. 异常体系**

### **1.1 异常分类**

Java 中的异常分为两大类：`Checked Exception` 和 `Unchecked Exception`。

#### **1.1.1 Checked Exception（受检异常）**

- **定义**：
  - 必须在编译时显式处理的异常。
  - 如果方法可能抛出受检异常，则必须通过 `try-catch` 或 `throws` 声明进行处理。
- **特点**：
  - 继承自 `Exception` 类，但不包括 `RuntimeException` 及其子类。
  - 通常表示可恢复的错误或外部资源问题（如文件读取失败、网络连接中断等）。
- **常见类型**：
  - `IOException`
  - `SQLException`
  - `FileNotFoundException`

#### **1.1.2 Unchecked Exception（非受检异常）**

- **定义**：
  - 不需要在编译时显式处理的异常。
  - 包括运行时异常（`RuntimeException`）和错误（`Error`）。
- **特点**：
  - 运行时异常通常由程序逻辑错误引起，难以预测。
  - 错误（`Error`）是严重的系统级问题，一般无法恢复。
- **常见类型**：
  - **运行时异常**：
    - `NullPointerException`：尝试访问空对象的方法或属性。
    - `ArrayIndexOutOfBoundsException`：数组索引越界。
    - `ArithmeticException`：除以零等算术错误。
  - **错误**：
    - `OutOfMemoryError`：内存不足。
    - `StackOverflowError`：栈溢出。

#### **1.1.3 异常层次结构**

```plaintext
Throwable
├── Error (严重错误，不可恢复)
│   ├── OutOfMemoryError
│   ├── StackOverflowError
├── Exception (可恢复的异常)
│   ├── RuntimeException (非受检异常)
│   │   ├── NullPointerException
│   │   ├── ArrayIndexOutOfBoundsException
│   │   ├── ArithmeticException
│   ├── IOException (受检异常)
│   │   ├── FileNotFoundException
│   │   ├── SocketException
```

---

## **2. 异常处理机制**

### **2.1 try-catch-finally**

- **作用**：
  - 捕获并处理异常，防止程序崩溃。
- **语法**：

  ```java
  try {
      // 可能抛出异常的代码
  } catch (ExceptionType e) {
      // 处理异常
  } finally {
      // 无论是否发生异常都会执行的代码
  }
  ```

- **特点**：
  - `try` 块用于包裹可能抛出异常的代码。
  - `catch` 块用于捕获并处理特定类型的异常。
  - `finally` 块用于释放资源（如关闭文件流、数据库连接等），即使发生异常也会执行。

#### **示例**

```java
public class ExceptionHandlingExample {
    public static void main(String[] args) {
        try {
            int result = 10 / 0; // 抛出 ArithmeticException
        } catch (ArithmeticException e) {
            System.out.println("Caught exception: " + e.getMessage());
        } finally {
            System.out.println("Finally block executed.");
        }
    }
}
```

输出：

```
Caught exception: / by zero
Finally block executed.
```

---

### **2.2 throw 和 throws**

#### **2.2.1 throw**

- **作用**：
  - 用于手动抛出异常。
- **语法**：

  ```java
  throw new ExceptionType("Message");
  ```

- **示例**：

  ```java
  public void validateAge(int age) {
      if (age < 18) {
          throw new IllegalArgumentException("Age must be at least 18.");
      }
  }
  ```

#### **2.2.2 throws**

- **作用**：
  - 声明方法可能抛出的异常，将异常处理的责任交给调用者。
- **语法**：

  ```java
  public void readFile() throws IOException {
      FileReader file = new FileReader("test.txt");
      // 文件操作
  }
  ```

- **示例**：

  ```java
  public void processFile() throws IOException {
      readFile();
  }

  public void readFile() throws IOException {
      FileReader file = new FileReader("test.txt");
      // 文件操作
  }
  ```

---

### **2.3 自定义异常**

- **定义**：
  - 创建自己的异常类，继承自 `Exception` 或 `RuntimeException`。
- **语法**：

  ```java
  public class CustomException extends Exception {
      public CustomException(String message) {
          super(message);
      }
  }
  ```

- **示例**：

  ```java
  public class CustomExceptionExample {
      public static void main(String[] args) {
          try {
              validateAge(15);
          } catch (CustomException e) {
              System.out.println(e.getMessage());
          }
      }

      public static void validateAge(int age) throws CustomException {
          if (age < 18) {
              throw new CustomException("Age must be at least 18.");
          }
      }
  }
  ```

---

## **3. 异常的最佳实践**

### **3.1 不要吞掉异常**

- **问题**：
  - 捕获异常后不做任何处理（即“吞掉”异常），会导致问题被隐藏，难以排查。
- **错误示例**：

  ```java
  try {
      int result = 10 / 0;
  } catch (ArithmeticException e) {
      // 啥也不做，吞掉异常
  }
  ```

- **正确做法**：
  - 至少记录异常信息或采取补救措施。
  - 示例：

    ```java
    try {
        int result = 10 / 0;
    } catch (ArithmeticException e) {
        System.err.println("An error occurred: " + e.getMessage());
    }
    ```

---

### **3.2 使用日志记录异常信息**

- **推荐工具**：
  - 使用专业的日志框架（如 Log4j、SLF4J）记录异常信息。
- **优点**：
  - 提供详细的上下文信息，便于问题定位。
  - 避免直接将异常信息打印到控制台。
- **示例**：

  ```java
  import org.slf4j.Logger;
  import org.slf4j.LoggerFactory;

  public class LoggingExample {
      private static final Logger logger = LoggerFactory.getLogger(LoggingExample.class);

      public static void main(String[] args) {
          try {
              int result = 10 / 0;
          } catch (ArithmeticException e) {
              logger.error("An arithmetic error occurred.", e);
          }
      }
  }
  ```

---

### **3.3 其他最佳实践**

1. **避免滥用异常**：
   - 异常应该用于处理异常情况，而不是作为流程控制的手段。
2. **区分受检异常和非受检异常**：
   - 对于可以预见并恢复的错误，使用受检异常。
   - 对于不可预见或无法恢复的错误，使用非受检异常。
3. **保持异常链**：
   - 在重新抛出异常时，保留原始异常信息。
   - 示例：

     ```java
     try {
         someMethod();
     } catch (Exception e) {
         throw new CustomException("Wrapped exception", e);
     }
     ```

---

# **四、集合框架**

以下是关于 **Java 集合框架** 的详细讲解，涵盖集合概述、具体实现类、工具类以及泛型的使用。

---

## **1. 集合概述**

### **1.1 集合框架的层次结构**

Java 集合框架（Collection Framework）提供了一组接口和类，用于存储和操作对象的集合。它的主要接口包括 `Collection` 和 `Map`，其层次结构如下：

#### **1.1.1 Collection 接口**

- **定义**：
  - 是集合的根接口，表示一组对象（称为元素）。
- **子接口**：
  - `List`：有序集合，允许重复元素。
  - `Set`：无序集合，不允许重复元素。
  - `Queue`：队列，用于按特定顺序处理元素。
- **实现类**：
  - `ArrayList`, `LinkedList`（实现 `List`）
  - `HashSet`, `TreeSet`, `LinkedHashSet`（实现 `Set`）

#### **1.1.2 Map 接口**

- **定义**：
  - 表示键值对的集合，每个键最多对应一个值。
- **实现类**：
  - `HashMap`：基于哈希表实现，无序。
  - `TreeMap`：基于红黑树实现，按键排序。
  - `LinkedHashMap`：基于哈希表和链表实现，保持插入顺序。

---

### **1.2 Collection 接口与 Map 接口的区别**

| 特性                   | Collection                          | Map                              |
|------------------------|-------------------------------------|----------------------------------|
| **数据结构**            | 存储单个元素                       | 存储键值对                      |
| **是否允许重复**        | 允许（`List`）或不允许（`Set`）     | 键不允许重复，值可以重复        |
| **遍历方式**            | 使用迭代器或增强型 for 循环         | 遍历键、值或键值对              |
| **典型实现**            | `ArrayList`, `HashSet`             | `HashMap`, `TreeMap`            |

---

## **2. List**

### **2.1 ArrayList 与 LinkedList 的区别与使用场景**

#### **2.1.1 ArrayList**

- **特点**：
  - 基于动态数组实现。
  - 查询快（通过索引访问），增删慢（需要移动元素）。
- **适用场景**：
  - 需要频繁随机访问元素时。
- **示例**：

  ```java
  List<String> list = new ArrayList<>();
  list.add("A");
  list.add("B");
  System.out.println(list.get(0)); // 输出：A
  ```

#### **2.1.2 LinkedList**

- **特点**：
  - 基于双向链表实现。
  - 插入和删除快（只需调整指针），查询慢（需要从头或尾遍历）。
- **适用场景**：
  - 需要频繁插入或删除元素时。
- **示例**：

  ```java
  List<String> list = new LinkedList<>();
  list.add("A");
  list.add("B");
  list.remove(0); // 删除第一个元素
  ```

---

### **2.2 遍历方式**

#### **2.2.1 for 循环**

```java
List<String> list = Arrays.asList("A", "B", "C");
for (int i = 0; i < list.size(); i++) {
    System.out.println(list.get(i));
}
```

#### **2.2.2 foreach 循环**

```java
List<String> list = Arrays.asList("A", "B", "C");
for (String item : list) {
    System.out.println(item);
}
```

#### **2.2.3 Iterator**

```java
List<String> list = Arrays.asList("A", "B", "C");
Iterator<String> iterator = list.iterator();
while (iterator.hasNext()) {
    System.out.println(iterator.next());
}
```

---

## **3. Set**

### **3.1 HashSet**

- **特点**：
  - 基于哈希表实现。
  - 无序且不允许重复元素。
- **适用场景**：
  - 需要快速查找元素时。
- **示例**：

  ```java
  Set<String> set = new HashSet<>();
  set.add("A");
  set.add("B");
  set.add("A"); // 不会添加重复元素
  System.out.println(set); // 输出：[A, B]
  ```

### **3.2 TreeSet**

- **特点**：
  - 基于红黑树实现。
  - 按自然顺序或自定义顺序排序。
- **适用场景**：
  - 需要有序存储且不重复的元素时。
- **示例**：

  ```java
  Set<Integer> set = new TreeSet<>();
  set.add(3);
  set.add(1);
  set.add(2);
  System.out.println(set); // 输出：[1, 2, 3]
  ```

### **3.3 LinkedHashSet**

- **特点**：
  - 基于哈希表和链表实现。
  - 保持插入顺序且不允许重复元素。
- **适用场景**：
  - 需要保持插入顺序时。
- **示例**：

  ```java
  Set<String> set = new LinkedHashSet<>();
  set.add("A");
  set.add("B");
  set.add("C");
  System.out.println(set); // 输出：[A, B, C]
  ```

---

## **4. Map**

### **4.1 HashMap**

- **特点**：
  - 基于哈希表实现。
  - 无序且允许一个 `null` 键和多个 `null` 值。
- **适用场景**：
  - 需要快速查找键值对时。
- **示例**：

  ```java
  Map<String, Integer> map = new HashMap<>();
  map.put("A", 1);
  map.put("B", 2);
  System.out.println(map.get("A")); // 输出：1
  ```

### **4.2 TreeMap**

- **特点**：
  - 基于红黑树实现。
  - 按键排序（自然顺序或自定义顺序）。
- **适用场景**：
  - 需要按键排序的键值对时。
- **示例**：

  ```java
  Map<String, Integer> map = new TreeMap<>();
  map.put("C", 3);
  map.put("A", 1);
  map.put("B", 2);
  System.out.println(map); // 输出：{A=1, B=2, C=3}
  ```

### **4.3 LinkedHashMap**

- **特点**：
  - 基于哈希表和链表实现。
  - 保持插入顺序。
- **适用场景**：
  - 需要保持插入顺序的键值对时。
- **示例**：

  ```java
  Map<String, Integer> map = new LinkedHashMap<>();
  map.put("A", 1);
  map.put("B", 2);
  map.put("C", 3);
  System.out.println(map); // 输出：{A=1, B=2, C=3}
  ```

---

## **5. 工具类**

### **5.1 Collections 工具类**

- **常用方法**：
  - `sort(List<T> list)`：对列表进行排序。
  - `reverse(List<T> list)`：反转列表。
  - `shuffle(List<T> list)`：随机打乱列表。
  - `synchronizedList(List<T> list)`：返回线程安全的列表。
- **示例**：

  ```java
  List<Integer> list = new ArrayList<>(Arrays.asList(3, 1, 2));
  Collections.sort(list); // 排序
  System.out.println(list); // 输出：[1, 2, 3]

  Collections.reverse(list); // 反转
  System.out.println(list); // 输出：[3, 2, 1]
  ```

### **5.2 Arrays 工具类**

- **常用方法**：
  - `sort(T[] array)`：对数组进行排序。
  - `binarySearch(T[] array, T key)`：在已排序数组中查找元素。
  - `asList(T... a)`：将数组转换为列表。
- **示例**：

  ```java
  int[] array = {3, 1, 2};
  Arrays.sort(array); // 排序
  System.out.println(Arrays.toString(array)); // 输出：[1, 2, 3]

  int index = Arrays.binarySearch(array, 2); // 查找
  System.out.println(index); // 输出：1
  ```

---

## **6. 泛型**

### **6.1 泛型的基本概念**

- **定义**：
  - 泛型允许在编译时指定类型参数，从而提高代码的安全性和复用性。
- **语法**：
  - `<T>` 表示类型参数。
- **示例**：

  ```java
  List<String> list = new ArrayList<>();
  list.add("A");
  String value = list.get(0); // 不需要强制类型转换
  ```

---

### **6.2 泛型类、泛型方法、通配符的使用**

#### **6.2.1 泛型类**

- **定义**：
  - 类中定义类型参数。
- **示例**：

  ```java
  public class Box<T> {
      private T item;

      public void setItem(T item) {
          this.item = item;
      }

      public T getItem() {
          return item;
      }
  }

  Box<String> box = new Box<>();
  box.setItem("Hello");
  System.out.println(box.getItem()); // 输出：Hello
  ```

#### **6.2.2 泛型方法**

- **定义**：
  - 方法中定义类型参数。
- **示例**：

  ```java
  public <T> void printArray(T[] array) {
      for (T element : array) {
          System.out.println(element);
      }
  }

  String[] array = {"A", "B", "C"};
  printArray(array);
  ```

#### **6.2.3 通配符**

- **定义**：
  - `?` 表示未知类型。
  - `? extends T`：上限，表示类型必须是 `T` 或其子类。
  - `? super T`：下限，表示类型必须是 `T` 或其父类。
- **示例**：

  ```java
  public static void processElements(List<? extends Number> list) {
      for (Number num : list) {
          System.out.println(num);
      }
  }

  List<Integer> integers = Arrays.asList(1, 2, 3);
  processElements(integers);
  ```

---

### **6.3 泛型的限制**

- 不能实例化泛型类型的数组：

  ```java
  T[] array = new T[10]; // 编译错误
  ```

- 不能使用基本类型作为泛型参数：

  ```java
  List<int> list = new ArrayList<>(); // 编译错误
  ```

---

## **总结**

- **集合框架** 提供了丰富的接口和实现类，用于存储和操作对象集合。
- **List** 强调有序性，`Set` 强调唯一性，`Map` 强调键值对。
- **工具类** 如 `Collections` 和 `Arrays` 提供了便捷的操作方法。
- **泛型** 提高了代码的类型安全性和复用性。

---

# **五、I/O 流**

以下是关于 **Java I/O 流** 的详细讲解，涵盖文件操作、字节流与字符流、序列化与反序列化以及 NIO 的核心内容。

---

## **1. 文件操作**

### **1.1 文件的创建、删除、读取与写入**

Java 中通过 `File` 类可以对文件和目录进行操作。以下是一些常见的文件操作：

#### **1.1.1 创建文件**

```java
import java.io.File;
import java.io.IOException;

public class FileExample {
    public static void main(String[] args) throws IOException {
        File file = new File("example.txt");
        if (file.createNewFile()) {
            System.out.println("File created: " + file.getName());
        } else {
            System.out.println("File already exists.");
        }
    }
}
```

#### **1.1.2 删除文件**

```java
File file = new File("example.txt");
if (file.delete()) {
    System.out.println("File deleted: " + file.getName());
} else {
    System.out.println("Failed to delete the file.");
}
```

#### **1.1.3 读取文件**

使用 `FileInputStream` 或 `BufferedReader` 读取文件内容：

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class FileReadExample {
    public static void main(String[] args) throws IOException {
        BufferedReader reader = new BufferedReader(new FileReader("example.txt"));
        String line;
        while ((line = reader.readLine()) != null) {
            System.out.println(line);
        }
        reader.close();
    }
}
```

#### **1.1.4 写入文件**

使用 `FileOutputStream` 或 `BufferedWriter` 写入文件内容：

```java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;

public class FileWriteExample {
    public static void main(String[] args) throws IOException {
        BufferedWriter writer = new BufferedWriter(new FileWriter("example.txt"));
        writer.write("Hello, World!");
        writer.close();
    }
}
```

---

### **1.2 File 类的常用方法**

| 方法名                      | 描述                                   |
|-----------------------------|---------------------------------------|
| `createNewFile()`           | 创建新文件                           |
| `delete()`                  | 删除文件或目录                       |
| `exists()`                  | 检查文件或目录是否存在               |
| `isFile()`                  | 判断是否为文件                       |
| `isDirectory()`             | 判断是否为目录                       |
| `getName()`                 | 获取文件或目录的名称                 |
| `getPath()`                 | 获取文件或目录的路径                 |
| `length()`                  | 获取文件的大小（以字节为单位）       |
| `listFiles()`               | 获取目录中的文件和子目录列表         |

---

## **2. 字节流与字符流**

### **2.1 字节流（InputStream 和 OutputStream）**

- **定义**：
  - 字节流用于处理二进制数据（如图片、音频等），基于字节（8 位）操作。
- **常用类**：
  - `InputStream`：输入流的基类。
  - `OutputStream`：输出流的基类。
  - 具体实现类：
    - `FileInputStream` 和 `FileOutputStream`
    - `BufferedInputStream` 和 `BufferedOutputStream`

#### **示例：复制文件（使用字节流）**

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class CopyFileExample {
    public static void main(String[] args) throws IOException {
        FileInputStream in = new FileInputStream("source.txt");
        FileOutputStream out = new FileOutputStream("target.txt");

        byte[] buffer = new byte[1024];
        int bytesRead;
        while ((bytesRead = in.read(buffer)) != -1) {
            out.write(buffer, 0, bytesRead);
        }

        in.close();
        out.close();
    }
}
```

---

### **2.2 字符流（Reader 和 Writer）**

- **定义**：
  - 字符流用于处理文本数据，基于字符（16 位 Unicode）操作。
- **常用类**：
  - `Reader`：输入流的基类。
  - `Writer`：输出流的基类。
  - 具体实现类：
    - `FileReader` 和 `FileWriter`
    - `BufferedReader` 和 `BufferedWriter`

#### **示例：读取和写入文本文件（使用字符流）**

```java
import java.io.*;

public class TextFileExample {
    public static void main(String[] args) throws IOException {
        // 写入文件
        BufferedWriter writer = new BufferedWriter(new FileWriter("output.txt"));
        writer.write("Hello, Java I/O!");
        writer.close();

        // 读取文件
        BufferedReader reader = new BufferedReader(new FileReader("output.txt"));
        String line;
        while ((line = reader.readLine()) != null) {
            System.out.println(line);
        }
        reader.close();
    }
}
```

---

## **3. 序列化与反序列化**

### **3.1 Serializable 接口的作用**

- **定义**：
  - `Serializable` 是一个标记接口，表示对象可以被序列化（转换为字节流）。
- **用途**：
  - 主要用于将对象保存到文件或通过网络传输。

#### **示例：序列化与反序列化**

```java
import java.io.*;

class Person implements Serializable {
    private static final long serialVersionUID = 1L;
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + "}";
    }
}

public class SerializationExample {
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        // 序列化
        Person person = new Person("Alice", 25);
        ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("person.ser"));
        out.writeObject(person);
        out.close();

        // 反序列化
        ObjectInputStream in = new ObjectInputStream(new FileInputStream("person.ser"));
        Person deserializedPerson = (Person) in.readObject();
        in.close();

        System.out.println(deserializedPerson); // 输出：Person{name='Alice', age=25}
    }
}
```

---

### **3.2 注意事项**

1. **serialVersionUID**：
   - 建议显式声明 `serialVersionUID`，以确保序列化和反序列化的兼容性。
2. **静态成员**：
   - 静态字段不会被序列化，因为它们属于类而不是对象。
3. **瞬态字段**：
   - 使用 `transient` 关键字修饰的字段不会被序列化。

---

## **4. NIO（New I/O）**

### **4.1 缓冲区（Buffer）**

- **定义**：
  - 缓冲区是 NIO 的核心组件，用于存储数据。
  - 常见类型：`ByteBuffer`, `CharBuffer`, `IntBuffer` 等。
- **基本操作**：
  - `put()`：向缓冲区写入数据。
  - `get()`：从缓冲区读取数据。
  - `flip()`：切换到读模式。
  - `clear()`：清空缓冲区，切换到写模式。

#### **示例：使用 ByteBuffer**

```java
import java.nio.ByteBuffer;

public class BufferExample {
    public static void main(String[] args) {
        ByteBuffer buffer = ByteBuffer.allocate(10);

        // 写入数据
        buffer.put((byte) 1);
        buffer.put((byte) 2);

        // 切换到读模式
        buffer.flip();

        // 读取数据
        while (buffer.hasRemaining()) {
            System.out.println(buffer.get());
        }

        // 清空缓冲区
        buffer.clear();
    }
}
```

---

### **4.2 通道（Channel）**

- **定义**：
  - 通道是数据传输的载体，支持双向读写。
- **常用类**：
  - `FileChannel`：用于文件操作。
  - `SocketChannel` 和 `ServerSocketChannel`：用于网络通信。

#### **示例：使用 FileChannel 复制文件**

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.nio.channels.FileChannel;

public class FileChannelExample {
    public static void main(String[] args) throws Exception {
        FileInputStream in = new FileInputStream("source.txt");
        FileOutputStream out = new FileOutputStream("target.txt");

        FileChannel inChannel = in.getChannel();
        FileChannel outChannel = out.getChannel();

        outChannel.transferFrom(inChannel, 0, inChannel.size());

        inChannel.close();
        outChannel.close();
        in.close();
        out.close();
    }
}
```

---

### **4.3 文件锁与内存映射文件**

#### **文件锁**

- **作用**：
  - 防止多个进程同时修改同一文件。
- **示例**：

  ```java
  import java.io.RandomAccessFile;
  import java.nio.channels.FileChannel;
  import java.nio.channels.FileLock;

  public class FileLockExample {
      public static void main(String[] args) throws Exception {
          RandomAccessFile file = new RandomAccessFile("test.txt", "rw");
          FileChannel channel = file.getChannel();

          FileLock lock = channel.lock(); // 加锁
          System.out.println("File is locked.");

          lock.release(); // 解锁
          System.out.println("File is unlocked.");

          channel.close();
          file.close();
      }
  }
  ```

#### **内存映射文件**

- **定义**：
  - 将文件直接映射到内存中，提高文件读写效率。
- **示例**：

  ```java
  import java.io.RandomAccessFile;
  import java.nio.MappedByteBuffer;
  import java.nio.channels.FileChannel;

  public class MappedFileExample {
      public static void main(String[] args) throws Exception {
          RandomAccessFile file = new RandomAccessFile("test.txt", "rw");
          FileChannel channel = file.getChannel();

          MappedByteBuffer buffer = channel.map(FileChannel.MapMode.READ_WRITE, 0, channel.size());
          buffer.put(0, (byte) 'H');
          buffer.put(1, (byte) 'i');

          channel.close();
          file.close();
      }
  }
  ```

---

## **总结**

- **文件操作** 提供了对文件和目录的基本操作。
- **字节流** 和 **字符流** 分别用于处理二进制数据和文本数据。
- **序列化** 和 **反序列化** 使得对象可以在不同环境中传递和存储。
- **NIO** 提供了更高效的 I/O 操作方式，包括缓冲区、通道、文件锁和内存映射文件。

---

# **六、多线程与并发**

在现代软件开发中，多线程和并发编程是提高程序性能的重要手段。通过合理利用多线程技术，可以充分利用多核CPU的优势，提升程序的响应速度和吞吐量。以下是对多线程与并发相关知识点的详细讲解。

---

## **1. 线程基础**

### **1.1 线程的概念与生命周期**

- **线程的概念**：  
  线程是操作系统能够独立调度的基本单位，是进程中的一个执行路径。一个进程可以包含多个线程，所有线程共享进程的内存空间（如堆、方法区等），但每个线程有自己的栈。
  
- **线程的生命周期**：  
  Java线程有以下几种状态：
  1. **新建 (New)**：线程对象被创建，但尚未启动。
  2. **就绪 (Runnable)**：线程已启动，等待CPU调度执行。
  3. **运行 (Running)**：线程正在CPU上执行。
  4. **阻塞 (Blocked)**：线程因等待资源（如I/O操作、锁）而暂停。
  5. **等待 (Waiting)**：线程进入无限期等待，直到其他线程显式唤醒（如调用`wait()`）。
  6. **超时等待 (Timed Waiting)**：线程进入有限期等待（如调用`sleep()`或带超时参数的`wait()`）。
  7. **终止 (Terminated)**：线程执行完毕或因异常退出。

---

### **1.2 创建线程的方式**

Java中有多种方式创建线程：

#### **1.2.1 继承 `Thread` 类**

```java
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Thread is running");
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread thread = new MyThread();
        thread.start(); // 启动线程
    }
}
```

- **优点**：简单直观。
- **缺点**：由于Java不支持多继承，如果类已经继承了其他类，则无法使用该方式。

---

#### **1.2.2 实现 `Runnable` 接口**

```java
class MyRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("Runnable is running");
    }
}

public class Main {
    public static void main(String[] args) {
        Thread thread = new Thread(new MyRunnable());
        thread.start();
    }
}
```

- **优点**：避免单继承限制，更灵活。
- **缺点**：需要额外创建`Thread`对象。

---

#### **1.2.3 使用线程池**

线程池是一种管理线程的高级方式，通过复用线程减少频繁创建和销毁线程的开销。

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class Main {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(2); // 创建固定大小的线程池
        for (int i = 0; i < 5; i++) {
            executor.submit(() -> System.out.println("Task executed by " + Thread.currentThread().getName()));
        }
        executor.shutdown(); // 关闭线程池
    }
}
```

- **优点**：高效、可控性强。
- **常见实现**：
  - `Executors.newFixedThreadPool(int nThreads)`：创建固定大小的线程池。
  - `Executors.newCachedThreadPool()`：根据需要动态调整线程数量。
  - `Executors.newSingleThreadExecutor()`：单线程的线程池。

---

## **2. 线程同步**

### **2.1 `synchronized` 关键字**

`synchronized` 是Java提供的内置锁机制，用于保证多线程环境下的数据一致性。

#### **2.1.1 方法级同步**

```java
public synchronized void method() {
    // 同步代码块
}
```

#### **2.1.2 块级同步**

```java
public void method() {
    synchronized (this) {
        // 同步代码块
    }
}
```

#### **2.1.3 锁的对象**

- `synchronized` 可以作用于实例方法、静态方法或指定对象。
- 静态方法的锁是类对象（`Class` 对象）。

---

### **2.2 死锁的概念与避免**

- **死锁定义**：多个线程相互持有对方所需的资源，导致彼此永久阻塞。
- **死锁条件**（必要条件）：
  1. **互斥**：资源只能被一个线程占用。
  2. **占有且等待**：线程持有资源的同时等待其他资源。
  3. **不可剥夺**：资源不能被强行抢占。
  4. **循环等待**：存在一个线程等待环路。

- **避免死锁的方法**：
  - 按顺序获取锁。
  - 使用定时锁（`tryLock`）。
  - 减少锁的粒度。

---

### **2.3 `volatile` 关键字**

- **作用**：确保变量的可见性，即每次读取时都从主内存加载最新值。
- **适用场景**：适用于简单的标志位变量。
- **注意**：`volatile` 不保证原子性，不能替代锁。

```java
private volatile boolean flag = true;

public void stop() {
    flag = false;
}
```

---

## **3. 高级并发工具**

### **3.1 `Lock` 接口与 `ReentrantLock`**

`Lock` 提供比 `synchronized` 更灵活的锁机制。

```java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class Main {
    private final Lock lock = new ReentrantLock();

    public void method() {
        lock.lock();
        try {
            // 临界区代码
        } finally {
            lock.unlock();
        }
    }
}
```

- **优点**：
  - 支持公平锁和非公平锁。
  - 提供可中断锁（`lockInterruptibly`）。
  - 支持尝试获取锁（`tryLock`）。

---

### **3.2 并发集合**

Java提供了多种线程安全的集合类。

- **`ConcurrentHashMap`**：分段锁机制，支持高并发读写。
- **`CopyOnWriteArrayList`**：写时复制，适合读多写少的场景。

```java
import java.util.concurrent.ConcurrentHashMap;

ConcurrentHashMap<String, Integer> map = new ConcurrentHashMap<>();
map.put("key", 1);
```

---

### **3.3 线程池**

线程池的核心类是 `ThreadPoolExecutor`，它允许开发者自定义线程池。

```java
import java.util.concurrent.*;

public class Main {
    public static void main(String[] args) {
        ThreadPoolExecutor executor = new ThreadPoolExecutor(
            2, // 核心线程数
            4, // 最大线程数
            10, // 空闲线程存活时间
            TimeUnit.SECONDS,
            new LinkedBlockingQueue<>()
        );
        executor.submit(() -> System.out.println("Task executed"));
        executor.shutdown();
    }
}
```

---

### **3.4 原子类**

原子类提供无锁的线程安全操作。

- **常用原子类**：
  - `AtomicInteger`
  - `AtomicBoolean`
  - `AtomicReference`

```java
import java.util.concurrent.atomic.AtomicInteger;

AtomicInteger counter = new AtomicInteger(0);
counter.incrementAndGet(); // 原子操作
```

---

## **4. 线程间通信**

### **4.1 `wait()`, `notify()`, `notifyAll()`**

这些方法用于线程间的协作，必须在同步块中使用。

```java
synchronized (obj) {
    while (conditionNotMet) {
        obj.wait(); // 当前线程等待
    }
    // 执行逻辑
    obj.notify(); // 唤醒一个等待线程
    obj.notifyAll(); // 唤醒所有等待线程
}
```

---

### **4.2 生产者-消费者模式**

生产者-消费者模式是一种经典的线程间通信模型。

```java
import java.util.LinkedList;
import java.util.Queue;

public class ProducerConsumer {
    private final Queue<Integer> queue = new LinkedList<>();
    private final int CAPACITY = 5;
    private final Object lock = new Object();

    public void produce() throws InterruptedException {
        int value = 0;
        while (true) {
            synchronized (lock) {
                while (queue.size() == CAPACITY) {
                    lock.wait();
                }
                queue.add(value++);
                lock.notify();
            }
        }
    }

    public void consume() throws InterruptedException {
        while (true) {
            synchronized (lock) {
                while (queue.isEmpty()) {
                    lock.wait();
                }
                int value = queue.poll();
                System.out.println("Consumed: " + value);
                lock.notify();
            }
        }
    }
}
```

---

# **七、Java 新特性**

## **一、Java 8 及以后的新特性**

### **1. Lambda 表达式**

Lambda 表达式是 Java 8 中最重要的特性之一，它简化了匿名类的使用，使代码更加简洁和易读。Lambda 表达式用于实现函数式接口（只有一个抽象方法的接口）。

#### **语法：**

```java
(parameters) -> expression
```

#### **示例：**

```java
// 使用匿名类实现 Runnable 接口
Runnable r1 = new Runnable() {
    @Override
    public void run() {
        System.out.println("Hello, World!");
    }
};

// 使用 Lambda 表达式实现
Runnable r2 = () -> System.out.println("Hello, World!");

// 调用
r1.run(); // 输出: Hello, World!
r2.run(); // 输出: Hello, World!
```

#### **优势：**

- 减少样板代码。
- 提高代码可读性。
- 支持函数式编程风格。

---

### **2. 函数式接口（`@FunctionalInterface`）**

函数式接口是指仅包含一个抽象方法的接口。可以使用 `@FunctionalInterface` 注解来标记这样的接口。Lambda 表达式只能用于实现函数式接口。

#### **示例：**

```java
@FunctionalInterface
interface MyFunction {
    int apply(int a, int b);
}

public class Main {
    public static void main(String[] args) {
        // 使用 Lambda 表达式实现函数式接口
        MyFunction add = (a, b) -> a + b;
        System.out.println(add.apply(3, 5)); // 输出: 8
    }
}
```

#### **常见函数式接口：**

- `java.util.function.Function<T, R>`：将输入 T 转换为输出 R。
- `java.util.function.Consumer<T>`：对输入 T 执行操作，无返回值。
- `java.util.function.Predicate<T>`：判断条件是否满足，返回布尔值。
- `java.util.function.Supplier<T>`：提供一个 T 类型的结果。

---

### **3. Stream API**

Stream API 是 Java 8 引入的一个强大的工具，用于处理集合数据。它可以进行过滤、映射、归约等操作，并支持链式调用。

#### **核心概念：**

- **流（Stream）**：表示一系列元素的序列，支持聚合操作。
- **中间操作**：如 `filter`、`map`、`sorted`，返回新的流。
- **终端操作**：如 `forEach`、`collect`、`reduce`，触发实际计算并结束流。

#### **示例：**

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

// 过滤名字长度大于 3 的元素，并转换为大写
List<String> result = names.stream()
        .filter(name -> name.length() > 3)
        .map(String::toUpperCase)
        .collect(Collectors.toList());

System.out.println(result); // 输出: [ALICE, CHARLIE]
```

#### **优势：**

- 提供声明式编程风格。
- 支持并行流（`parallelStream`），提高性能。
- 简化集合操作。

---

### **4. 默认方法与静态方法在接口中的使用**

Java 8 允许在接口中定义默认方法和静态方法，避免修改现有实现类时破坏代码。

#### **默认方法：**

```java
interface MyInterface {
    default void sayHello() {
        System.out.println("Hello from default method!");
    }
}

class MyClass implements MyInterface {}

public class Main {
    public static void main(String[] args) {
        MyClass obj = new MyClass();
        obj.sayHello(); // 输出: Hello from default method!
    }
}
```

#### **静态方法：**

```java
interface MyInterface {
    static void sayHi() {
        System.out.println("Hi from static method!");
    }
}

public class Main {
    public static void main(String[] args) {
        MyInterface.sayHi(); // 输出: Hi from static method!
    }
}
```

#### **用途：**

- 向后兼容：在不破坏现有实现的情况下扩展接口功能。
- 提供通用方法实现。

---

### **5. Optional 类的使用**

`Optional` 是一个容器类，用于避免空指针异常（`NullPointerException`）。它表示一个值可能存在或不存在。

#### **常用方法：**

- `Optional.of(T value)`：创建非空的 Optional。
- `Optional.empty()`：创建空的 Optional。
- `isPresent()`：检查是否有值。
- `orElse(T other)`：如果为空，则返回指定值。
- `ifPresent(Consumer<? super T> consumer)`：如果存在值，则执行操作。

#### **示例：**

```java
Optional<String> optional = Optional.of("Hello");
optional.ifPresent(System.out::println); // 输出: Hello

Optional<String> empty = Optional.empty();
System.out.println(empty.orElse("Default Value")); // 输出: Default Value
```

#### **优势：**

- 明确表达可能为空的场景。
- 减少空指针异常的风险。

---

## **二、Java 9-17 的新特性**

### **1. 模块化系统（JPMS）**

Java 9 引入了模块化系统（Java Platform Module System, JPMS），通过 `module-info.java` 文件定义模块及其依赖关系，增强了项目的可维护性和安全性。

#### **示例：**

```java
// module-info.java
module com.example.myapp {
    requires java.sql; // 声明依赖
    exports com.example.myapp.api; // 导出包
}
```

#### **优势：**

- 提高封装性：模块间明确依赖关系。
- 减少运行时依赖冲突。
- 支持更小的运行时镜像。

---

### **2. var 关键字（局部变量类型推断）**

Java 10 引入了 `var` 关键字，允许编译器根据赋值自动推断局部变量的类型。

#### **示例：**

```java
var list = new ArrayList<String>(); // 编译器推断为 ArrayList<String>
list.add("Java");
System.out.println(list); // 输出: [Java]
```

#### **限制：**

- 仅适用于局部变量。
- 不适用于方法参数、字段或返回值。

#### **优势：**

- 简化代码，减少冗长的类型声明。

---

### **3. 新增的集合工厂方法**

Java 9 引入了 `List.of`、`Set.of` 和 `Map.of` 等工厂方法，用于快速创建不可变集合。

#### **示例：**

```java
List<String> list = List.of("A", "B", "C");
Set<Integer> set = Set.of(1, 2, 3);
Map<String, Integer> map = Map.of("Alice", 25, "Bob", 30);

System.out.println(list); // 输出: [A, B, C]
System.out.println(set);  // 输出: [1, 2, 3]
System.out.println(map);  // 输出: {Alice=25, Bob=30}
```

#### **特点：**

- 创建的集合是不可变的。
- 避免空指针异常（不允许包含 `null` 值）。

---

### **4. 文本块（Text Blocks）**

Java 15 引入了文本块（Text Blocks），用于简化多行字符串的书写。

#### **语法：**

```java
String json = """
{
    "name": "Alice",
    "age": 25
}
""";
System.out.println(json);
```

#### **优势：**

- 自动处理换行符和缩进。
- 提高代码可读性。

---

## **总结**

从 Java 8 到 Java 17，每个版本都引入了许多实用的新特性，极大地提升了开发效率和代码质量。以下是关键特性的总结：

- **Java 8**：Lambda 表达式、Stream API、Optional 类。
- **Java 9**：模块化系统、集合工厂方法。
- **Java 10**：`var` 关键字。
- **Java 15**：文本块。

这些新特性不仅使 Java 更加现代化，还为开发者提供了更多的灵活性和便利性。

---

# **八、数据库与网络编程**

## **1. JDBC**

JDBC（Java Database Connectivity）是 Java 提供的一组 API，用于与关系型数据库进行交互。它通过标准接口屏蔽了底层数据库的实现细节，使得开发者可以使用统一的方式操作不同的数据库。

---

### **1.1 JDBC 的基本使用**

JDBC 操作数据库的基本步骤如下：

1. **加载驱动程序**
   - 使用 `Class.forName()` 方法加载数据库驱动程序。
   - 现代 JDBC 驱动程序通常支持自动加载，因此在某些情况下可以省略这一步。

   ```java
   Class.forName("com.mysql.cj.jdbc.Driver");
   ```

2. **建立连接**
   - 使用 `DriverManager.getConnection()` 方法创建数据库连接。
   - URL 格式因数据库而异，例如 MySQL 的连接 URL 是：

     ```
     jdbc:mysql://[host]:[port]/[database]?user=[username]&password=[password]
     ```

   ```java
   String url = "jdbc:mysql://localhost:3306/testdb";
   String user = "root";
   String password = "password";
   Connection conn = DriverManager.getConnection(url, user, password);
   ```

3. **执行 SQL**
   - 创建 `Statement` 或 `PreparedStatement` 对象来执行 SQL 查询。
   - 使用 `executeQuery()` 执行查询语句，返回 `ResultSet`。
   - 使用 `executeUpdate()` 执行更新、插入或删除语句，返回受影响的行数。

   ```java
   // 查询示例
   Statement stmt = conn.createStatement();
   ResultSet rs = stmt.executeQuery("SELECT * FROM users");

   while (rs.next()) {
       System.out.println(rs.getString("name"));
   }

   // 插入示例
   PreparedStatement pstmt = conn.prepareStatement("INSERT INTO users(name, age) VALUES(?, ?)");
   pstmt.setString(1, "Alice");
   pstmt.setInt(2, 25);
   int rowsAffected = pstmt.executeUpdate();
   ```

4. **关闭资源**
   - 按照打开顺序的逆序关闭资源（`ResultSet` -> `Statement` -> `Connection`）。
   - 使用 try-with-resources 自动关闭资源。

   ```java
   try (Connection conn = DriverManager.getConnection(url, user, password);
        Statement stmt = conn.createStatement();
        ResultSet rs = stmt.executeQuery("SELECT * FROM users")) {

       while (rs.next()) {
           System.out.println(rs.getString("name"));
       }
   } catch (SQLException e) {
       e.printStackTrace();
   }
   ```

---

### **1.2 事务管理**

事务是一组逻辑操作单元，要么全部成功提交，要么全部回滚。JDBC 支持事务管理，主要通过以下方法实现：

1. **设置自动提交模式**
   - 默认情况下，JDBC 连接处于自动提交模式（`autoCommit=true`），即每条 SQL 语句都会立即生效。
   - 可以通过 `conn.setAutoCommit(false)` 关闭自动提交模式，手动控制事务。

   ```java
   conn.setAutoCommit(false); // 关闭自动提交
   ```

2. **提交事务**
   - 在所有操作完成后调用 `conn.commit()` 提交事务。

   ```java
   conn.commit(); // 提交事务
   ```

3. **回滚事务**
   - 如果发生异常，调用 `conn.rollback()` 回滚事务。

   ```java
   try {
       conn.setAutoCommit(false);
       // 执行多个 SQL 操作
       conn.commit();
   } catch (SQLException e) {
       conn.rollback(); // 发生异常时回滚
       e.printStackTrace();
   } finally {
       conn.setAutoCommit(true); // 恢复默认的自动提交模式
   }
   ```

---

### **1.3 连接池**

频繁地创建和关闭数据库连接会导致性能开销，因此引入了连接池技术。连接池预先创建一组数据库连接，并在需要时分配给应用程序使用，使用完毕后归还到池中。

常见的连接池实现包括 HikariCP、C3P0 和 DBCP。

#### **HikariCP 示例**

```java
import com.zaxxer.hikari.HikariConfig;
import com.zaxxer.hikari.HikariDataSource;

public class HikariExample {
    public static void main(String[] args) throws Exception {
        HikariConfig config = new HikariConfig();
        config.setJdbcUrl("jdbc:mysql://localhost:3306/testdb");
        config.setUsername("root");
        config.setPassword("password");
        config.setMaximumPoolSize(10);

        try (HikariDataSource ds = new HikariDataSource(config);
             Connection conn = ds.getConnection()) {

            Statement stmt = conn.createStatement();
            ResultSet rs = stmt.executeQuery("SELECT * FROM users");

            while (rs.next()) {
                System.out.println(rs.getString("name"));
            }
        }
    }
}
```

## **2.网络编程**

网络编程是指通过计算机网络实现不同设备之间的通信。Java 提供了丰富的网络编程 API，主要包括 TCP/IP 和 UDP 协议的支持。

---

### **2.1 TCP/IP 协议与 UDP 协议**

- **TCP/IP**
  - 面向连接的协议，提供可靠的、有序的数据传输。
  - 常用于需要高可靠性的场景，如文件传输、电子邮件等。
  - 基于三次握手建立连接。

- **UDP**
  - 面向无连接的协议，不保证数据包的可靠性，但效率更高。
  - 常用于实时性要求较高的场景，如视频会议、在线游戏等。

---

### **2.2 Socket 编程**

Socket 是网络通信的基础，Java 提供了 `java.net.Socket` 和 `java.net.ServerSocket` 类分别用于客户端和服务器端的通信。

#### **服务器端实现**

```java
import java.io.*;
import java.net.*;

public class Server {
    public static void main(String[] args) throws IOException {
        ServerSocket serverSocket = new ServerSocket(8080);
        System.out.println("Server is listening on port 8080...");

        while (true) {
            Socket clientSocket = serverSocket.accept(); // 接受客户端连接
            System.out.println("Client connected: " + clientSocket.getInetAddress());

            BufferedReader in = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
            PrintWriter out = new PrintWriter(clientSocket.getOutputStream(), true);

            String inputLine;
            while ((inputLine = in.readLine()) != null) {
                System.out.println("Received: " + inputLine);
                out.println("Echo: " + inputLine); // 返回响应
            }

            clientSocket.close();
        }
    }
}
```

#### **客户端实现**

```java
import java.io.*;
import java.net.*;

public class Client {
    public static void main(String[] args) throws IOException {
        Socket socket = new Socket("localhost", 8080);
        PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
        BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));

        BufferedReader stdIn = new BufferedReader(new InputStreamReader(System.in));
        String userInput;

        while ((userInput = stdIn.readLine()) != null) {
            out.println(userInput); // 发送数据到服务器
            System.out.println("Server response: " + in.readLine()); // 接收服务器响应
        }

        socket.close();
    }
}
```

---

### **2.3 NIO 在网络编程中的应用**

NIO（New I/O）是 Java 提供的一种高效 I/O 模型，基于缓冲区和通道，可以实现非阻塞式网络通信。

#### **NIO 示例：非阻塞服务器**

```java
import java.io.IOException;
import java.net.InetSocketAddress;
import java.nio.ByteBuffer;
import java.nio.channels.SelectionKey;
import java.nio.channels.Selector;
import java.nio.channels.ServerSocketChannel;
import java.nio.channels.SocketChannel;
import java.util.Iterator;

public class NIOServer {
    public static void main(String[] args) throws IOException {
        Selector selector = Selector.open();
        ServerSocketChannel serverSocket = ServerSocketChannel.open();
        serverSocket.bind(new InetSocketAddress(8080));
        serverSocket.configureBlocking(false);
        serverSocket.register(selector, SelectionKey.OP_ACCEPT);

        ByteBuffer buffer = ByteBuffer.allocate(256);

        while (true) {
            selector.select();
            Iterator<SelectionKey> keys = selector.selectedKeys().iterator();

            while (keys.hasNext()) {
                SelectionKey key = keys.next();
                keys.remove();

                if (key.isAcceptable()) {
                    ServerSocketChannel server = (ServerSocketChannel) key.channel();
                    SocketChannel client = server.accept();
                    client.configureBlocking(false);
                    client.register(selector, SelectionKey.OP_READ);
                    System.out.println("Client connected: " + client.getRemoteAddress());
                } else if (key.isReadable()) {
                    SocketChannel client = (SocketChannel) key.channel();
                    buffer.clear();
                    int read = client.read(buffer);
                    if (read == -1) {
                        client.close();
                    } else {
                        buffer.flip();
                        byte[] data = new byte[buffer.remaining()];
                        buffer.get(data);
                        System.out.println("Received: " + new String(data));
                        client.write(ByteBuffer.wrap(("Echo: " + new String(data)).getBytes()));
                    }
                }
            }
        }
    }
}
```

---

# **九、Java 反射**

反射（Reflection）是 Java 提供的一种强大的机制，允许程序在运行时动态地获取类的信息（如类名、方法、字段等），并操作对象的属性和方法。反射使得程序可以在编译时不知道类的具体信息的情况下，仍然能够进行操作。它在框架开发、动态代理、注解处理等场景中非常常见。

## **1. 反射的基本概念**

反射的核心是 `java.lang.reflect` 包，其中包含以下关键类：

- **Class**：表示类或接口的元数据。
- **Field**：表示类中的字段（成员变量）。
- **Method**：表示类中的方法。
- **Constructor**：表示类的构造方法。

通过反射，我们可以在运行时动态地加载类、创建对象、调用方法以及访问字段。

---

## **2. 获取 Class 对象**

要使用反射，首先需要获取目标类的 `Class` 对象。以下是几种常见的获取方式：

### **2.1 通过 `Class.forName()`**

```java
Class<?> clazz = Class.forName("java.util.ArrayList");
System.out.println(clazz.getName()); // 输出：java.util.ArrayList
```

### **2.2 通过 `.class` 属性**

```java
Class<?> clazz = ArrayList.class;
System.out.println(clazz.getName()); // 输出：java.util.ArrayList
```

### **2.3 通过对象的 `getClass()` 方法**

```java
ArrayList<String> list = new ArrayList<>();
Class<?> clazz = list.getClass();
System.out.println(clazz.getName()); // 输出：java.util.ArrayList
```

---

## **3. 创建对象**

通过反射可以动态创建对象，主要有两种方式：

### **3.1 使用无参构造方法**

```java
Class<?> clazz = Class.forName("java.util.Date");
Object obj = clazz.getDeclaredConstructor().newInstance();
System.out.println(obj); // 输出当前时间
```

### **3.2 使用带参构造方法**

```java
Class<?> clazz = Class.forName("java.lang.String");
Constructor<?> constructor = clazz.getConstructor(String.class);
Object obj = constructor.newInstance("Hello, Reflection!");
System.out.println(obj); // 输出：Hello, Reflection!
```

---

## **4. 访问字段**

反射可以访问类的私有字段，并对其进行读写操作。

### **4.1 获取字段**

```java
Class<?> clazz = Person.class;
Field field = clazz.getDeclaredField("name"); // 获取名为 "name" 的字段
field.setAccessible(true); // 绕过私有访问限制
```

### **4.2 设置和获取字段值**

```java
Person person = new Person();
Field field = Person.class.getDeclaredField("name");
field.setAccessible(true);

field.set(person, "Alice"); // 设置字段值
System.out.println(field.get(person)); // 输出：Alice
```

---

## **5. 调用方法**

反射可以动态调用类的方法。

### **5.1 获取方法**

```java
Class<?> clazz = Person.class;
Method method = clazz.getDeclaredMethod("sayHello", String.class); // 获取方法
method.setAccessible(true); // 如果方法是私有的
```

### **5.2 调用方法**

```java
Person person = new Person();
Method method = Person.class.getDeclaredMethod("sayHello", String.class);
method.setAccessible(true);

Object result = method.invoke(person, "Alice"); // 调用 sayHello 方法
System.out.println(result); // 输出：Hello, Alice
```

---

## **6. 处理注解**

反射可以用于读取类、方法或字段上的注解信息。

### **6.1 定义注解**

```java
import java.lang.annotation.*;

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface MyAnnotation {
    String value();
}
```

### **6.2 使用注解**

```java
public class Person {
    @MyAnnotation("Hello")
    public void sayHello() {
        System.out.println("Hello!");
    }
}
```

### **6.3 获取注解信息**

```java
Class<?> clazz = Person.class;
Method method = clazz.getMethod("sayHello");
if (method.isAnnotationPresent(MyAnnotation.class)) {
    MyAnnotation annotation = method.getAnnotation(MyAnnotation.class);
    System.out.println(annotation.value()); // 输出：Hello
}
```

---

## **7. 动态代理**

动态代理是反射的一个重要应用场景，它允许我们为接口动态生成代理对象，并在调用方法时插入额外的逻辑。

### **7.1 定义接口和实现类**

```java
public interface Greeting {
    void sayHello(String name);
}

public class GreetingImpl implements Greeting {
    @Override
    public void sayHello(String name) {
        System.out.println("Hello, " + name);
    }
}
```

### **7.2 创建动态代理**

```java
import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

public class ProxyExample {
    public static void main(String[] args) {
        Greeting greeting = new GreetingImpl();

        Greeting proxy = (Greeting) Proxy.newProxyInstance(
            greeting.getClass().getClassLoader(),
            greeting.getClass().getInterfaces(),
            new InvocationHandler() {
                @Override
                public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                    System.out.println("Before method call");
                    Object result = method.invoke(greeting, args);
                    System.out.println("After method call");
                    return result;
                }
            }
        );

        proxy.sayHello("Alice");
    }
}
```

输出结果：

```
Before method call
Hello, Alice
After method call
```

---

## **8. 反射的优缺点**

### **优点**

1. **灵活性高**：可以在运行时动态加载类、创建对象、调用方法。
2. **框架支持**：许多框架（如 Spring、Hibernate）依赖反射实现核心功能。
3. **扩展性强**：可以通过配置文件动态加载类，而无需修改代码。

### **缺点**

1. **性能开销**：反射操作比直接调用方法或访问字段慢。
2. **安全性问题**：反射可以绕过访问控制修饰符（如 private），可能导致安全隐患。
3. **可读性差**：反射代码通常较复杂，不易理解和维护。

## **总结**

- **反射的核心** 是 `java.lang.reflect` 包，包括 `Class`、`Field`、`Method` 和 `Constructor` 等类。
- **基本操作** 包括获取类信息、创建对象、访问字段、调用方法和处理注解。
- **动态代理** 是反射的重要应用，广泛用于 AOP（面向切面编程）。
- **优缺点分析** 表明反射虽然强大，但需要权衡性能和安全性。

---

# **十、Java 动态代理 （Dynamic Proxy）详解**

Java 动态代理是一种**运行时动态生成代理类的技术**，它是 Java 反射机制的一部分。通过动态代理，我们可以在不修改目标对象的前提下，对目标对象的方法进行增强或拦截，是 AOP（面向切面编程）的基础。

## **📌 1、什么是动态代理？**

### 定义

动态代理是指在程序运行过程中，根据传入的真实对象（被代理对象），**动态创建一个代理对象**，并用这个代理对象来代替真实对象完成操作。

### 核心作用

- **在不修改目标对象的前提下，对方法进行功能增强**
- **实现解耦，提高代码的可扩展性和灵活性**
- **AOP（如 Spring AOP）底层实现原理**

---

## **🧱 2、核心 API 和类**

| 类/接口 | 说明 |
|--------|------|
| `java.lang.reflect.Proxy` | 核心类，用于生成代理对象 |
| `java.lang.reflect.InvocationHandler` | 接口，用于定义代理逻辑 |
| `java.lang.reflect.Method` | 表示被调用的方法对象 |

---

## **🛠️ 3、动态代理的使用步骤**

### ✅ 步骤 1：定义接口（必须）

```java
public interface UserService {
    void addUser();
    void deleteUser();
}
```

> ⚠️ 注意：Java 动态代理只能对接口进行代理！

---

### ✅ 步骤 2：实现接口类（真实对象）

```java
public class UserServiceImpl implements UserService {
    @Override
    public void addUser() {
        System.out.println("添加用户");
    }

    @Override
    public void deleteUser() {
        System.out.println("删除用户");
    }
}
```

---

### ✅ 步骤 3：实现 InvocationHandler 接口（定义代理逻辑）

```java
import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;

public class MyInvocationHandler implements InvocationHandler {

    private Object target; // 被代理的对象

    public MyInvocationHandler(Object target) {
        this.target = target;
    }

    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("【前置增强】方法执行前：" + method.getName());

        // 执行真实对象的方法
        Object result = method.invoke(target, args);

        System.out.println("【后置增强】方法执行后：" + method.getName());
        return result;
    }
}
```

---

### ✅ 步骤 4：生成代理对象并调用

```java
import java.lang.reflect.Proxy;

public class TestProxy {
    public static void main(String[] args) {
        // 创建真实对象
        UserService userService = new UserServiceImpl();

        // 创建代理处理器
        MyInvocationHandler handler = new MyInvocationHandler(userService);

        // 生成代理对象
        UserService proxy = (UserService) Proxy.newProxyInstance(
                userService.getClass().getClassLoader(),   // 类加载器
                userService.getClass().getInterfaces(),   // 被代理对象实现的接口
                handler                                   // 代理逻辑处理器
        );

        // 调用代理对象的方法
        proxy.addUser();
        proxy.deleteUser();
    }
}
```

---

## 📈 4、输出结果

```
【前置增强】方法执行前：addUser
添加用户
【后置增强】方法执行后：addUser

【前置增强】方法执行前：deleteUser
删除用户
【后置增强】方法执行后：deleteUser
```

---

## 🔄 5、与静态代理的区别

| 特点 | 静态代理 | 动态代理 |
|------|----------|-----------|
| 代理类是否手动编写 | 是 | 否 |
| 是否支持多个接口 | 否 | 是 |
| 是否灵活 | 不灵活 | 灵活 |
| 实现复杂度 | 简单 | 复杂 |
| 性能 | 略高 | 略低（但差距不大） |

---

## 🔐 6、应用场景

| 应用场景 | 说明 |
|----------|------|
| 日志记录 | 在方法执行前后记录日志 |
| 权限控制 | 控制某些方法是否可以被调用 |
| 性能监控 | 统计方法执行时间 |
| 事务管理 | 在方法执行前后开启和提交事务 |
| AOP 编程 | Spring 框架中大量使用动态代理做切面处理 |

---

## 🧩 7、Spring 中的 AOP 与动态代理的关系

Spring AOP 默认使用 JDK 动态代理（基于接口），但如果目标类没有实现接口，则会使用 **CGLIB**（继承方式实现代理）。

> ✅ 如果你希望强制使用 CGLIB 代理，可以在配置中设置：

```xml
<aop:config proxy-target-class="true"/>
```

---

## 📎 8、动态代理的局限性

- **只能代理接口方法**（JDK 原生动态代理）
- **不能代理类方法**（除非使用 CGLIB 或 Javassist 等第三方库）
- **性能略低于直接调用**（但一般影响不大）
- **调试较困难**（因为代理类是运行时生成的）

---

## 🧪 9、完整代码汇总

### 1. 接口定义

```java
public interface UserService {
    void addUser();
    void deleteUser();
}
```

### 2. 实现类

```java
public class UserServiceImpl implements UserService {
    @Override
    public void addUser() {
        System.out.println("添加用户");
    }

    @Override
    public void deleteUser() {
        System.out.println("删除用户");
    }
}
```

### 3. 代理处理器

```java
import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;

public class MyInvocationHandler implements InvocationHandler {
    private Object target;

    public MyInvocationHandler(Object target) {
        this.target = target;
    }

    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("【前置增强】方法执行前：" + method.getName());
        Object result = method.invoke(target, args);
        System.out.println("【后置增强】方法执行后：" + method.getName());
        return result;
    }
}
```

### 4. 测试类

```java
import java.lang.reflect.Proxy;

public class TestProxy {
    public static void main(String[] args) {
        UserService userService = new UserServiceImpl();
        MyInvocationHandler handler = new MyInvocationHandler(userService);
        UserService proxy = (UserService) Proxy.newProxyInstance(
            userService.getClass().getClassLoader(),
            userService.getClass().getInterfaces(),
            handler
        );
        proxy.addUser();
        proxy.deleteUser();
    }
}
```

---

## 🧠 10、总结

| 项目 | 内容 |
|------|------|
| 动态代理 | 运行时生成代理类，用于增强方法 |
| 核心类 | `Proxy`, `InvocationHandler` |
| 必须条件 | 被代理类必须实现接口 |
| 使用场景 | 日志、权限、事务、AOP |
| 优点 | 解耦、灵活、易于扩展 |
| 缺点 | 只能代理接口方法，调试困难 |

# **十一、Java 数据安全**

数据安全是软件开发中的核心问题之一，尤其是在涉及敏感信息（如用户密码、支付信息）的场景中。Java 提供了多种机制和工具来保护数据的安全性。本节将从以下几个方面详细讲解 Java 数据安全的核心内容：

---

## **1. 数据加密**

加密是保护数据安全的重要手段，通过将明文数据转换为密文，确保只有拥有正确密钥的人才能解密并读取数据。

### **1.1 对称加密**

对称加密使用同一个密钥进行加密和解密，适合快速加密大量数据。常见的对称加密算法包括 AES 和 DES。

#### **AES 加密示例**

```java
import javax.crypto.Cipher;
import javax.crypto.KeyGenerator;
import javax.crypto.SecretKey;

public class AESExample {
    public static void main(String[] args) throws Exception {
        // 生成密钥
        KeyGenerator keyGen = KeyGenerator.getInstance("AES");
        keyGen.init(128); // 密钥长度
        SecretKey secretKey = keyGen.generateKey();

        // 加密
        Cipher cipher = Cipher.getInstance("AES");
        cipher.init(Cipher.ENCRYPT_MODE, secretKey);
        byte[] encryptedData = cipher.doFinal("Sensitive Data".getBytes());
        System.out.println("Encrypted: " + new String(encryptedData));

        // 解密
        cipher.init(Cipher.DECRYPT_MODE, secretKey);
        byte[] decryptedData = cipher.doFinal(encryptedData);
        System.out.println("Decrypted: " + new String(decryptedData));
    }
}
```

### **1.2 非对称加密**

非对称加密使用一对密钥（公钥和私钥），其中一个用于加密，另一个用于解密。常见的非对称加密算法包括 RSA。

#### **RSA 加密示例**

```java
import java.security.*;
import javax.crypto.Cipher;

public class RSAExample {
    public static void main(String[] args) throws Exception {
        // 生成密钥对
        KeyPairGenerator keyGen = KeyPairGenerator.getInstance("RSA");
        keyGen.initialize(2048);
        KeyPair keyPair = keyGen.generateKeyPair();
        PublicKey publicKey = keyPair.getPublic();
        PrivateKey privateKey = keyPair.getPrivate();

        // 加密
        Cipher cipher = Cipher.getInstance("RSA");
        cipher.init(Cipher.ENCRYPT_MODE, publicKey);
        byte[] encryptedData = cipher.doFinal("Sensitive Data".getBytes());
        System.out.println("Encrypted: " + new String(encryptedData));

        // 解密
        cipher.init(Cipher.DECRYPT_MODE, privateKey);
        byte[] decryptedData = cipher.doFinal(encryptedData);
        System.out.println("Decrypted: " + new String(decryptedData));
    }
}
```

---

## **2. 数据完整性**

数据完整性确保数据在传输或存储过程中未被篡改。常用的方法是使用哈希函数和数字签名。

### **2.1 哈希函数**

哈希函数将任意长度的数据映射为固定长度的值，且不可逆。常见的哈希算法包括 MD5 和 SHA 系列。

#### **SHA-256 示例**

```java
import java.security.MessageDigest;

public class HashExample {
    public static void main(String[] args) throws Exception {
        String data = "Sensitive Data";
        MessageDigest digest = MessageDigest.getInstance("SHA-256");
        byte[] hash = digest.digest(data.getBytes());
        System.out.println("Hash: " + bytesToHex(hash));
    }

    private static String bytesToHex(byte[] hash) {
        StringBuilder hexString = new StringBuilder();
        for (byte b : hash) {
            String hex = Integer.toHexString(0xff & b);
            if (hex.length() == 1) hexString.append('0');
            hexString.append(hex);
        }
        return hexString.toString();
    }
}
```

### **2.2 数字签名**

数字签名结合了哈希函数和非对称加密，用于验证数据的来源和完整性。

#### **数字签名示例**

```java
import java.security.*;
import java.util.Base64;

public class SignatureExample {
    public static void main(String[] args) throws Exception {
        // 生成密钥对
        KeyPairGenerator keyGen = KeyPairGenerator.getInstance("RSA");
        keyGen.initialize(2048);
        KeyPair keyPair = keyGen.generateKeyPair();
        PrivateKey privateKey = keyPair.getPrivate();
        PublicKey publicKey = keyPair.getPublic();

        // 签名
        Signature signature = Signature.getInstance("SHA256withRSA");
        signature.initSign(privateKey);
        signature.update("Sensitive Data".getBytes());
        byte[] digitalSignature = signature.sign();
        System.out.println("Signature: " + Base64.getEncoder().encodeToString(digitalSignature));

        // 验证签名
        signature.initVerify(publicKey);
        signature.update("Sensitive Data".getBytes());
        boolean isVerified = signature.verify(digitalSignature);
        System.out.println("Verified: " + isVerified);
    }
}
```

---

## **3. 数据存储安全**

在存储敏感数据时，必须采取措施防止数据泄露。

### **3.1 密码存储**

密码不应以明文形式存储，而应使用加盐哈希的方式存储。

#### **加盐哈希示例**

```java
import java.security.MessageDigest;
import java.security.SecureRandom;

public class PasswordStorageExample {
    public static void main(String[] args) throws Exception {
        String password = "userPassword";

        // 生成随机盐
        SecureRandom random = new SecureRandom();
        byte[] salt = new byte[16];
        random.nextBytes(salt);

        // 加盐哈希
        MessageDigest digest = MessageDigest.getInstance("SHA-256");
        digest.update(salt);
        byte[] hash = digest.digest(password.getBytes());

        System.out.println("Salt: " + bytesToHex(salt));
        System.out.println("Hashed Password: " + bytesToHex(hash));
    }

    private static String bytesToHex(byte[] bytes) {
        StringBuilder hexString = new StringBuilder();
        for (byte b : bytes) {
            String hex = Integer.toHexString(0xff & b);
            if (hex.length() == 1) hexString.append('0');
            hexString.append(hex);
        }
        return hexString.toString();
    }
}
```

### **3.2 数据库加密**

敏感数据在存储到数据库之前可以加密，例如使用 JPA 的 `@Convert` 注解实现字段级加密。

---

## **4. 数据传输安全**

在网络传输中，必须确保数据不被窃听或篡改。SSL/TLS 是最常见的解决方案。

### **4.1 使用 HTTPS**

HTTPS 是基于 SSL/TLS 的安全协议，用于保护客户端与服务器之间的通信。

#### **启用 HTTPS 示例**

1. 在服务器端配置 SSL 证书。
2. 客户端使用 `HttpsURLConnection` 进行安全连接：

```java
import javax.net.ssl.HttpsURLConnection;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.URL;

public class HttpsExample {
    public static void main(String[] args) throws Exception {
        URL url = new URL("https://example.com");
        HttpsURLConnection connection = (HttpsURLConnection) url.openConnection();
        connection.setRequestMethod("GET");

        BufferedReader reader = new BufferedReader(new InputStreamReader(connection.getInputStream()));
        String line;
        while ((line = reader.readLine()) != null) {
            System.out.println(line);
        }
        reader.close();
    }
}
```

---

## **5. 安全编码实践**

除了上述技术手段，还需要遵循安全编码的最佳实践：

- **输入验证**：防止 SQL 注入、XSS 攻击等。
- **最小权限原则**：程序只请求必要的权限。
- **日志管理**：避免记录敏感信息。
- **依赖更新**：定期更新第三方库以修复已知漏洞。

---

## **总结**

- **数据加密** 是保护数据安全的核心，包括对称加密（AES）、非对称加密（RSA）和哈希函数（SHA）。
- **数据完整性** 通过哈希函数和数字签名确保数据未被篡改。
- **数据存储安全** 需要使用加盐哈希存储密码，并考虑数据库加密。
- **数据传输安全** 通常依赖于 HTTPS 和 SSL/TLS。
- **安全编码实践** 是防范攻击的基础。

---

# **十二、Java 性能优化**

性能优化是软件开发中至关重要的环节，尤其是在高并发、大数据量的场景下。Java 提供了丰富的工具和方法来帮助开发者优化程序性能。本节将从代码层面优化、JVM 调优以及性能监控工具三个方面进行详细讲解。

## **1. 代码层面优化**

代码层面的优化是从程序设计和实现的角度入手，通过改进代码逻辑和结构来提升性能。以下是常见的优化策略：

### **1.1 避免不必要的对象创建**

频繁的对象创建会增加垃圾回收（GC）的压力，从而影响程序性能。以下是一些避免不必要对象创建的技巧：

- **重用对象**：对于可复用的对象，尽量使用单例模式或对象池技术。

  ```java
  // 使用对象池避免频繁创建对象
  public class ObjectPool {
      private static final int POOL_SIZE = 10;
      private static final List<MyObject> pool = new ArrayList<>();

      static {
          for (int i = 0; i < POOL_SIZE; i++) {
              pool.add(new MyObject());
          }
      }

      public static MyObject getObject() {
          return pool.isEmpty() ? new MyObject() : pool.remove(0);
      }

      public static void returnObject(MyObject obj) {
          pool.add(obj);
      }
  }
  ```

- **避免自动装箱/拆箱**：在性能敏感的场景中，避免使用 `Integer` 等包装类代替基本类型。

  ```java
  // 错误示例：频繁装箱/拆箱
  Integer sum = 0;
  for (int i = 0; i < 1000000; i++) {
      sum += i; // 自动装箱/拆箱
  }

  // 正确示例：使用基本类型
  int sum = 0;
  for (int i = 0; i < 1000000; i++) {
      sum += i;
  }
  ```

### **1.2 使用高效的数据结构**

选择合适的数据结构可以显著提升程序性能。例如：

- **ArrayList vs LinkedList**：`ArrayList` 在随机访问时更快，而 `LinkedList` 在插入和删除操作时更高效。
- **HashMap vs TreeMap**：`HashMap` 提供常数时间复杂度的查找效率，而 `TreeMap` 提供有序存储但查找效率稍低。

```java
// 示例：优先使用 HashMap 而非 TreeMap
Map<String, String> map = new HashMap<>();
map.put("key1", "value1");
map.put("key2", "value2");

// 查找效率更高
String value = map.get("key1");
```

### **1.3 减少锁的粒度**

在多线程环境中，锁的粒度过大会导致线程竞争加剧，从而降低性能。以下是一些优化锁使用的建议：

- **细粒度锁**：将锁作用范围限制在最小范围内。

  ```java
  // 错误示例：粗粒度锁
  synchronized (this) {
      // 复杂逻辑
  }

  // 正确示例：细粒度锁
  synchronized (lockObject) {
      // 最小范围逻辑
  }
  ```

- **使用读写锁**：当读操作远多于写操作时，使用 `ReentrantReadWriteLock` 可以提高并发性能。

  ```java
  ReentrantReadWriteLock lock = new ReentrantReadWriteLock();
  lock.readLock().lock();
  try {
      // 读操作
  } finally {
      lock.readLock().unlock();
  }
  ```

- **无锁编程**：在某些场景下，可以使用 `Atomic` 类（如 `AtomicInteger`）实现无锁操作。

  ```java
  AtomicInteger counter = new AtomicInteger(0);
  counter.incrementAndGet(); // 原子操作
  ```

---

## **2. JVM 调优**

JVM 是 Java 程序运行的核心环境，其性能直接影响到程序的运行效率。以下是 JVM 调优的关键点：

### **2.1 内存模型**

JVM 的内存分为以下几个区域：

- **堆（Heap）**：存放对象实例和数组，是 GC 的主要工作区域。
- **栈（Stack）**：存放方法调用的局部变量和操作数栈。
- **方法区（Method Area）**：存放类信息、常量池和静态变量。
- **本地方法栈（Native Method Stack）**：支持 JNI（Java Native Interface）调用。
- **程序计数器（PC Register）**：记录当前线程执行的字节码指令地址。

### **2.2 GC（垃圾回收）机制**

GC 是 JVM 自动管理内存的重要机制，主要包括以下几种算法：

- **标记-清除（Mark-Sweep）**：标记需要回收的对象并清除。
- **复制（Copying）**：将存活对象复制到新的内存区域。
- **标记-整理（Mark-Compact）**：标记后整理内存，避免碎片化。
- **分代收集（Generational Collection）**：将堆划分为新生代（Young Generation）和老年代（Old Generation），分别采用不同的 GC 算法。

### **2.3 常见的 JVM 参数调优**

JVM 提供了大量参数用于调优，以下是一些常用的参数：

- **堆内存设置**：
  - `-Xms<size>`：设置初始堆大小。
  - `-Xmx<size>`：设置最大堆大小。
  - 示例：`-Xms512m -Xmx2g`
- **新生代设置**：
  - `-XX:NewRatio=<ratio>`：设置老年代与新生代的比例。
  - `-XX:SurvivorRatio=<ratio>`：设置 Eden 区与 Survivor 区的比例。
- **GC 算法选择**：
  - `-XX:+UseG1GC`：使用 G1 垃圾回收器。
  - `-XX:+UseParallelGC`：使用并行垃圾回收器。
  - 示例：`-XX:+UseG1GC -XX:MaxGCPauseMillis=200`

---

## **3. 性能监控工具**

性能监控工具可以帮助开发者分析程序的运行状态，定位性能瓶颈。以下是常用的工具及其功能：

### **3.1 VisualVM**

VisualVM 是一个轻量级的性能监控工具，集成了多种功能：

- **CPU 分析**：查看方法调用的耗时。
- **内存分析**：监控堆内存使用情况。
- **线程分析**：查看线程的状态和调用栈。
- **快照分析**：生成堆转储文件（Heap Dump）进行离线分析。

使用方法：

1. 启动 VisualVM：`jvisualvm`。
2. 连接到目标 JVM 进程。
3. 查看 CPU、内存、线程等指标。

### **3.2 JProfiler**

JProfiler 是一款商业化的性能分析工具，功能强大，适合复杂的性能调优场景：

- **CPU 分析**：支持方法级别的性能分析。
- **内存分析**：查看对象分配和引用关系。
- **线程分析**：检测死锁和线程阻塞。
- **数据库分析**：监控 SQL 查询性能。

### **3.3 MAT（Memory Analyzer Tool）**

MAT 是一款专门用于分析堆转储文件的工具，适合排查内存泄漏问题：

- **内存泄漏检测**：分析对象的引用链，找出未释放的对象。
- **大对象分析**：查看占用内存最多的对象。
- **DOM 树视图**：以图形化方式展示对象之间的引用关系。

使用方法：

1. 生成堆转储文件：`jmap -dump:live,format=b,file=heap.hprof <pid>`。
2. 打开 MAT 并加载堆转储文件。
3. 使用 Histogram 和 Dominator Tree 功能分析内存使用情况。

---

# **十三、综合实战**

1. **项目开发**
   - 分析需求与设计架构
   - 使用 MVC 模式进行项目开发
   - 数据库设计与优化

2. **单元测试**
   - JUnit 的使用
   - 测试驱动开发（TDD）

3. **部署与运维**
   - 打包与发布（Maven/Gradle）
   - Docker 容器化部署

---

以上大纲涵盖了 Java 开发的核心知识点，建议根据自己的学习目标和实际需求逐步深入学习。如果需要更详细的某一部分内容，请随时告诉我！
