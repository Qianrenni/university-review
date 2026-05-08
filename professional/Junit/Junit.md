
# 🧪 一、JUnit 简介

JUnit 是一个开源的单元测试框架，广泛用于 Java 应用程序中。它支持：

- 自动化测试
- 测试驱动开发 (TDD)
- 持续集成环境中的测试执行

## ✅ 当前主流版本：JUnit 5（也叫 Jupiter）

JUnit 5 = JUnit Platform + JUnit Jupiter + JUnit Vintage  

- **JUnit Platform**：在 JVM 上启动测试框架的基础层。
- **JUnit Jupiter**：新的编程模型和扩展模型。
- **JUnit Vintage**：兼容旧版 JUnit 3 和 JUnit 4 的测试引擎。

---

# 📦 二、Maven 配置

如果你使用 Maven 构建项目，在 `pom.xml` 中添加如下依赖：

```xml
<dependencies>
    <!-- JUnit Jupiter API -->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.11.0</version>
        <scope>test</scope>
    </dependency>

    <!-- JUnit Jupiter Engine -->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-engine</artifactId>
        <version>5.11.0</version>
        <scope>test</scope>
    </dependency>

    <!-- 可选：JUnit Platform Launcher -->
    <dependency>
        <groupId>org.junit.platform</groupId>
        <artifactId>junit-platform-launcher</artifactId>
        <version>1.11.0</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

---

# 🧱 三、基本测试结构

创建一个测试类，并使用 JUnit 提供的注解来定义测试方法。

```java
import org.junit.jupiter.api.*;

import static org.junit.jupiter.api.Assertions.*;

class CalculatorTest {

    @BeforeAll
    static void setUpAll() {
        System.out.println("Before all tests");
    }

    @BeforeEach
    void setUp() {
        System.out.println("Before each test");
    }

    @AfterEach
    void tearDown() {
        System.out.println("After each test");
    }

    @AfterAll
    static void tearDownAll() {
        System.out.println("After all tests");
    }

    @Test
    void testAdd() {
        Calculator calculator = new Calculator();
        int result = calculator.add(2, 3);
        assertEquals(5, result, "2 + 3 should equal 5");
    }
}
```

---

# 🔖 四、常用注解说明

| 注解 | 作用 |
|------|------|
| `@Test` | 标记一个方法为测试方法 |
| `@BeforeEach` | 每个测试方法执行前调用 |
| `@AfterEach` | 每个测试方法执行后调用 |
| `@BeforeAll` | 所有测试方法之前执行一次（必须是静态方法） |
| `@AfterAll` | 所有测试方法之后执行一次（必须是静态方法） |
| `@DisplayName` | 给测试类或方法设置自定义显示名称 |
| `@Disabled` | 禁用某个测试方法或类 |
| `@RepeatedTest(n)` | 重复执行测试 n 次 |
| `@ParameterizedTest` | 参数化测试 |
| `@Tag("xxx")` | 给测试打标签，可用于分组过滤 |

---

# 🧠 五、断言（Assertions）

JUnit 提供了丰富的断言方法，位于 `org.junit.jupiter.api.Assertions.*`。

常见断言方法：

| 方法 | 用途 |
|------|------|
| `assertEquals(expected, actual)` | 判断两个值是否相等 |
| `assertNotEquals(unexpected, actual)` | 判断两个值不相等 |
| `assertTrue(condition)` | 判断条件为 true |
| `assertFalse(condition)` | 判断条件为 false |
| `assertNull(object)` | 判断对象为 null |
| `assertNotNull(object)` | 判断对象不为 null |
| `assertSame(expected, actual)` | 判断引用是否相同 |
| `assertNotSame(expected, actual)` | 判断引用不同 |
| `assertThrows(exceptionClass, executable)` | 判断是否会抛出异常 |
| `assertTimeout(duration, executable)` | 判断执行是否超时 |

示例：

```java
@Test
void testDivideByZero() {
    Calculator calculator = new Calculator();
    assertThrows(ArithmeticException.class, () -> calculator.divide(10, 0));
}
```

---

# 🔄 六、参数化测试（Parameterized Tests）

可以使用不同的输入数据多次运行同一个测试逻辑。

引入依赖（如果需要从 CSV 文件读取）：

```xml
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-params</artifactId>
    <version>5.11.0</version>
    <scope>test</scope>
</dependency>
```

示例：

```java
@ParameterizedTest
@ValueSource(ints = {2, 4, 6})
void isEven(int number) {
    assertTrue(number % 2 == 0);
}
```

或者从 CSV 文件加载数据：

```java
@ParameterizedTest
@CsvSource({"1, 1", "2, 4", "3, 9"})
void square(int input, int expected) {
    assertEquals(expected, input * input);
}
```

---

# 🧪 七、嵌套测试（Nested Tests）

允许将多个相关测试组织在一个内部类中，提高可读性和结构清晰度。

```java
@DisplayName("Calculator Tests")
class CalculatorTest {

    @Nested
    @DisplayName("Addition Tests")
    class AdditionTests {
        @Test
        void addPositiveNumbers() {
            // ...
        }

        @Test
        void addNegativeNumbers() {
            // ...
        }
    }
}
```

---

# 🚫 八、异常测试

测试方法是否抛出预期的异常：

```java
@Test
void testDivideByZeroThrowsException() {
    Calculator calculator = new Calculator();
    assertThrows(ArithmeticException.class, () -> calculator.divide(10, 0));
}
```

---

# ⏱️ 九、超时测试

确保某个操作在指定时间内完成：

```java
@Test
void testFastOperation() {
    assertTimeout(Duration.ofMillis(100), () -> {
        // some operation
    });
}
```

---

# 🧩 十、测试生命周期回调方法

| 生命周期阶段 | 注解 |
|--------------|------|
| 所有测试开始前 | `@BeforeAll` |
| 每个测试开始前 | `@BeforeEach` |
| 每个测试结束后 | `@AfterEach` |
| 所有测试结束后 | `@AfterAll` |

---

# 📁 十一、目录结构建议

标准 Maven 项目结构：

```
src/
├── main/
│   └── java/
│       └── com.example.demo/  # 主代码
└── test/
    └── java/
        └── com.example.demo/  # 测试代码
```

---

# 🧪 十二、IDE 支持

主流 IDE 均支持 JUnit 5：

- IntelliJ IDEA
- Eclipse
- VS Code（配合 Java 插件）
- NetBeans

右键点击类或方法 → Run Test / Debug Test 即可运行测试。

---

# 🧪 十三、构建工具集成

## Maven

```bash
mvn test
```

## Gradle

```bash
gradle test
```

---

# 📚 推荐阅读

- [JUnit 官方文档](https://junit.org/junit5/docs/current/user-guide/)
- [JUnit 5 GitHub 示例](https://github.com/junit-team/junit5)
