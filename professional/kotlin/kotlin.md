# Kotlin 类型

## 1. 基本类型 (Basic Types)

### 1.1 概述
在 Kotlin 中，**一切皆对象**。这意味着任何变量都可以调用成员函数和属性。
- **没有原始类型（Primitive Types）**：不像 Java 有 `int`, `double`等原始类型，Kotlin 中所有数字、字符、布尔值都是对象。
- **智能优化**：虽然它们在概念上是对象，但编译器在大多数情况下会将它们编译为 JVM 的原始类型（如 `int`, `double`），以保留性能优势。只有在需要可空性（Nullable）或作为泛型参数时，才会装箱（Boxing）。

### 1.2 数字 (Numbers)
Kotlin 处理数字的方式与 Java 非常相似，但语法更简洁，且没有隐式 widening conversion（隐式宽化转换，如 int 自动转 long）。

#### 内置数字类型
| 类型 | 位宽 | 说明 |
| :--- | :--- | :--- |
| `Double` | 64 | 双精度浮点数 |
| `Float` | 32 | 单精度浮点数 |
| `Long` | 64 | 长整型 |
| `Int` | 32 | 整型（最常用） |
| `Short` | 16 | 短整型 |
| `Byte` | 8 | 字节型 |

#### 字面量常量
```kotlin
val dec = 123       // 十进制
val hex = 0x0F      // 十六进制
val bin = 0b00001011 // 二进制

val doubleLit = 123.5   // Double
val floatLit = 123.5f   // Float
val longLit = 123L      // Long
```

#### 数字间的转换
Kotlin **不支持** 隐式转换。例如，你不能直接将 `Int` 赋值给 `Long` 变量，必须显式转换。这有助于避免意外的精度丢失或溢出。

```kotlin
val i: Int = 1
// val l: Long = i  // 编译错误！类型不匹配

val l: Long = i.toLong() // 正确：显式转换
val d: Double = i.toDouble()
```

每个数字类型都支持以下转换函数：
`toByte()`, `toShort()`, `toInt()`, `toLong()`, `toFloat()`, `toDouble()`, `toChar()`

#### 运算操作
Kotlin 支持标准的算术运算符：`+`, `-`, `*`, `/`, `%`。
此外，还支持位运算（注意：Kotlin 中没有 `<<`, `>>` 这样的符号运算符用于位运算，而是使用中缀函数）：
- `shl(bits)` – 有符号左移 (Java 的 `<<`)
- `shr(bits)` – 有符号右移 (Java 的 `>>`)
- `ushr(bits)` – 无符号右移 (Java 的 `>>>`)
- `and(bits)` – 位与
- `or(bits)` – 位或
- `xor(bits)` – 位异或
- `inv()` – 位非

```kotlin
val x = (1 shl 2) and 0x000FF000
```

### 1.3 无符号整数 (Unsigned Integers)
*自 Kotlin 1.3 引入实验性支持，1.5+ 稳定。*

在某些底层开发、网络协议解析或高性能场景中，你需要处理无符号数。Kotlin 提供了以下类型：
- `UByte`: 8-bit unsigned integer (0 to 255)
- `UShort`: 16-bit unsigned integer (0 to 65535)
- `UInt`: 32-bit unsigned integer
- `ULong`: 64-bit unsigned integer

**使用示例：**
```kotlin
val uInt: UInt = 10u
val uLong: ULong = 100uL
val uByte: UByte = 255u

// 转换
val regularInt: Int = uInt.toInt()
```
*注意：在无符号数和有符号数之间进行运算时，通常需要显式转换，或者使用特定的扩展函数。*

### 1.4 布尔 (Booleans)
`Boolean` 类型只有两个值：`true` 和 `false`。

- **逻辑运算符**：`||` (短路或), `&&` (短路与), `!` (非)。
- **不可为空**：除非声明为 `Boolean?`。

```kotlin
val isReady: Boolean = true
if (isReady && checkCondition()) {
    // ...
}
```

### 1.5 字符 (Chars)
`Char` 表示单个字符。它不能直接当作数字处理（这与 C/Java 不同）。

- **字面量**：用单引号 `'c'` 表示。
- **特殊字符**：`\t`, `\b`, `\n`, `\r`, `\'`, `\"`, `\\`, `\$`。
- **Unicode**：可以使用 Unicode 转义序列 `'\uFF00'`。

**重要区别：**
在 Kotlin 中，`Char` **不是** 数字。
```kotlin
fun check(c: Char) {
    if (c == 1) { // 编译错误！类型不匹配：Char vs Int
        // ...
    }
}
```
如果需要将 `Char` 转换为数字代码点，必须显式转换：
```kotlin
val code: Int = 'a'.code // 获取 ASCII/Unicode 值
val char: Char = 97.toChar()
```

### 1.6 字符串 (Strings)
`String` 是不可变的（Immutable）。一旦创建，其内容无法更改。

#### 字符串模板 (String Templates)
Kotlin 强大的特性，允许在字符串中直接嵌入表达式。
```kotlin
val name = "Kotlin"
val version = 1.9

// $ 用于变量
println("Hello, $name")

// ${} 用于任意表达式
println("Version: ${version + 0.1}")
println("Length: ${name.length}")
```

#### 原始字符串 (Raw Strings)
由三个引号 `"""` 包裹。
- 可以包含换行符。
- **不处理** 转义字符（如 `\n` 会被视为两个字符 `\` 和 `n`）。
- 常用于编写 SQL 语句、JSON、HTML 或正则表达式。

```kotlin
val text = """
    for (c in "foo")
        print(c)
"""
// 去除前导空格（trimMargin）
val cleanedText = """
    |Hello
    |World
""".trimMargin()
```

#### 字符串比较
- `==`：比较内容（结构相等性），相当于 Java 的 `.equals()`。
- `===`：比较引用（引用相等性），相当于 Java 的 `==`。

```kotlin
val a = "Hello"
val b = "Hello"
println(a == b)   // true (内容相同)
println(a === b)  // true (Kotlin 编译器会优化字符串常量池，通常也相同，但不保证所有情况)
```

### 1.7 数组 (Arrays)
在 Kotlin 中，数组由 `Array<T>` 类表示。

#### 创建数组
```kotlin
// 1. 使用 arrayOf
val arr1 = arrayOf(1, 2, 3) // Array<Int>

// 2. 使用工厂函数 (推荐用于基本类型，避免装箱开销)
val intArr = intArrayOf(1, 2, 3) // IntArray (对应 int[])
val doubleArr = doubleArrayOf(1.0, 2.0) // DoubleArray

// 3. 使用构造函数
val asc = Array(5) { i -> i * i } // [0, 1, 4, 9, 16]
```

#### 访问与修改
```kotlin
val arr = arrayOf(1, 2, 3)
println(arr[0]) // 读取
arr[0] = 10     // 写入
```

#### 基本类型数组的特化
为了性能，Kotlin 为基本类型提供了特化的数组类，它们在 JVM 上对应原始数组，**没有装箱开销**：
- `ByteArray`, `ShortArray`, `IntArray`, `LongArray`
- `FloatArray`, `DoubleArray`
- `CharArray`, `BooleanArray`

*注意：这些特化数组类没有继承自 `Array`，但它们有相同的属性和方法集。*

### 1.8 其他不常用类型

#### Unit
- 相当于 Java 的 `void`。
- 当函数不返回任何有意义的数据时，返回类型为 `Unit`。
- `Unit` 是一个单例对象，只有一个实例 `Unit`。通常可以省略返回值声明。

```kotlin
fun printHello(): Unit {
    println("Hello")
}
// 等价于
fun printHello() {
    println("Hello")
}
```

#### Nothing
- `Nothing` 类型没有实例。
- 用于标记**永不正常返回**的函数（如抛出异常或无限循环）。
- 是任何类型的子类型（Bottom Type）。

```kotlin
fun fail(message: String): Nothing {
    throw IllegalStateException(message)
}

// 编译器知道 fail() 之后的代码不可达
val s: String = fail("Error") // 编译通过，因为 Nothing 是 String 的子类型，但运行时会抛异常
```

#### Any 和 Any?
- `Any` 是所有非空类型的超类（根类）。相当于 Java 的 `Object`。
- `Any?` 是所有类型（包括 null）的超类。
- 默认情况下，变量是非空的。如果需要接受 null，必须显式声明为可空类型（如 `String?`, `Int?`）。

---

## 2. 类型检测与类型转换 (Type Checks and Casts)

由于 Kotlin 强调类型安全，它提供了智能的类型检查机制。

### 2.1 类型检测：`is` 和 `!is`
使用 `is` 运算符检查对象是否符合某种类型。如果检查通过，编译器通常会自动进行智能转换（Smart Casts）。

```kotlin
fun getStringLength(obj: Any): Int? {
    if (obj is String) {
        // 在这里，obj 被自动转换为 String 类型
        return obj.length 
    }
    // 在这里，obj 仍然是 Any 类型
    return null
}
```

`!is` 用于检查对象是否**不**属于某种类型。

### 2.2 智能转换 (Smart Casts)
这是 Kotlin 的一大亮点。在许多情况下，你不需要显式地使用转换运算符，编译器会根据上下文自动转换类型。

**智能转换生效的条件：**
1. 局部变量 (`val`)。
2. 属性（如果是 `private` 或 `internal`，且在同一个模块中访问；或者该属性没有被开放修改器 `open` 修饰且没有自定义 getter）。
3. 在 `is` 检查之后，且变量在检查和使用的中间没有被修改。

```kotlin
fun demo(x: Any) {
    if (x is String) {
        print(x.length) // x 自动转换为 String
    }
}
```

**智能转换失效的情况：**
- 变量是 `var` 且在检查后被修改。
- 变量是开放的属性（可能被其他线程或子类修改）。
- 使用了复杂的逻辑流，编译器无法保证类型不变。

### 2.3 显式转换：Unsafe Cast (`as`)
如果智能转换不适用，你可以使用 `as` 运算符进行显式转换。

```kotlin
val x: String = y as String
```

**风险**：如果 `y` 不是 `String` 类型，这会抛出 `ClassCastException`。

### 2.4 安全转换：Safe Cast (`as?`)
为了避免异常，推荐使用 `as?` 运算符。如果转换失败，它返回 `null` 而不是抛出异常。

```kotlin
val x: String? = y as? String
if (x != null) {
    // 使用 x
}
```

这通常与 Elvis 运算符 `?:` 结合使用：
```kotlin
val length = (y as? String)?.length ?: 0
```

### 2.5 平台类型 (Platform Types)
*针对你关注的 Java/Kotlin 互操作性*

当从 Java 代码调用 Kotlin 时，或者在 Kotlin 中使用 Java 库时，会遇到“平台类型”（表示为 `T!`）。
- Kotlin 编译器不知道 Java 变量是否可为 null。
- 因此，`T!` 既可以当作 `T` 处理，也可以当作 `T?` 处理。
- **责任在你**：你需要根据 Java 文档或源码判断是否可能为 null。如果判断错误（例如将 null 赋值给非空类型），会在运行时抛出 NPE。

```kotlin
// Java: List<String> getList() { return null; }
// Kotlin:
val list: List<String> = javaObj.getList() // 危险！如果 getList 返回 null，这里会崩
val listSafe: List<String>? = javaObj.getList() // 安全
```

---

## 建议

1. **优先使用不可变类型 (`val`)**：这有助于编译器进行智能转换和优化。
2. **利用智能转换**：写出更简洁、可读性更高的代码，减少显式 cast。
3. **注意基本类型数组**：在高性能场景（如图像处理、大量数值计算）下，使用 `IntArray` 等特化数组而非 `Array<Int>` 以避免装箱开销。
4. **谨慎处理平台类型**：在与 Java 交互时，始终假设 Java 返回的对象可能为 null，除非你有十足把握。
5. **无符号数的使用**：仅在确实需要处理位掩码、网络字节流或与 C/C++ 交互时使用 `UInt` 等类型，普通业务逻辑使用 `Int`/`Long` 即可。

# 控制循环
## 1. 条件与循环 (Conditions & Loops)

### 1.1 `if` 表达式
在 Kotlin 中，`if` 是一个**表达式**（expression），而不仅仅是一个语句（statement）。这意味着它可以返回值并赋值给变量。

#### 基本用法
```kotlin
val a = 10
val b = 20

// 传统用法
if (a > b) {
    println("a is greater")
} else {
    println("b is greater")
}

// 作为表达式使用（替代三元运算符 ?:）
// Kotlin 没有三元运算符 (condition ? then : else)，因为 if-else 本身就是表达式
val max = if (a > b) a else b
println("Max value: $max")
```

#### 多分支 `if-else`
```kotlin
val score = 85
val grade = if (score >= 90) "A"
            else if (score >= 80) "B"
            else if (score >= 70) "C"
            else "D"
```

> **注意**：如果 `if` 用作表达式（即有返回值），则必须包含 `else` 分支，否则编译器无法确定当条件为假时返回什么值。

### 1.2 `when` 表达式
`when` 是 Kotlin 中取代 Java `switch-case` 的强大结构。它更灵活、更简洁，并且也是一个表达式。

#### 基本匹配
```kotlin
val x = 2
when (x) {
    1 -> println("x is 1")
    2 -> println("x is 2")
    else -> println("x is neither 1 nor 2")
}
```

#### 合并分支
```kotlin
when (x) {
    0, 1 -> println("x is 0 or 1")
    else -> println("otherwise")
}
```

#### 任意表达式作为分支条件
`when` 的分支条件可以是常量、变量、范围、类型检查等。

```kotlin
val str = "hello"
when (str) {
    "hello" -> println("Greeting")
    in "a".."z" -> println("Lowercase letter") // 范围检查
    !in "0".."9" -> println("Not a digit")      // 非范围检查
    else -> println("Unknown")
}
```

#### 无参数的 `when`（类似 if-else if 链）
如果不提供参数，分支条件必须是布尔表达式。

```kotlin
val number = 15
when {
    number % 2 == 0 -> println("Even")
    number > 10 -> println("Greater than 10")
    else -> println("Other")
}
```

#### 智能转换（Smart Casts）
`when` 经常与 `is` 检查结合使用，Kotlin 会自动进行类型转换。

```kotlin
fun describe(obj: Any): String =
    when (obj) {
        1          -> "One"
        is String  -> obj.length.toString() // obj 自动转换为 String
        is List<*> -> "List of size ${obj.size}" // obj 自动转换为 List
        else       -> "Unknown"
    }
```

### 1.3 循环 (Loops)

#### `for` 循环
Kotlin 的 `for` 循环通过迭代器遍历任何提供了 `iterator()` 方法的对象。

##### 遍历区间（Range）
```kotlin
// 打印 1 到 5
for (i in 1..5) {
    print("$i ")
}
println()

// 打印 5 到 1 (倒序)
for (i in 5 downTo 1) {
    print("$i ")
}
println()

// 步长为 2: 1, 3, 5
for (i in 1..5 step 2) {
    print("$i ")
}
println()

// 不包含上限: 1, 2, 3, 4 (until 排除结束值)
for (i in 1 until 5) {
    print("$i ")
}
```

##### 遍历集合
```kotlin
val items = listOf("apple", "banana", "kiwi")

// 标准遍历
for (item in items) {
    println(item)
}

// 带索引遍历
for ((index, value) in items.withIndex()) {
    println("the element at $index is $value")
}
```

##### 遍历 Map
```kotlin
val map = mapOf("a" to 1, "b" to 2)
for ((key, value) in map) {
    println("$key -> $value")
}
```

#### `while` 和 `do...while` 循环
与 Java 完全一致。

```kotlin
var i = 0
while (i < 5) {
    println(i++)
}

do {
    val code = readLine()
    // 至少执行一次
} while (code != "exit")
```

---

## 2. 返回与跳转 (Returns & Jumps)

Kotlin 支持三个结构化跳转表达式：
*   `return`：默认从最直接包围它的函数或匿名函数返回。
*   `break`：终止最直接包围它的循环。
*   `continue`：跳过当前循环迭代，进入下一次迭代。

### 2.1 标签（Labels）
所有表达式都可以用**标签**标记。标签以标识符后跟 `@` 符号表示，例如 `abc@`、`fooBar@`。

标签主要用于控制嵌套循环或 Lambda 表达式中的跳转行为。

#### 标记循环
```kotlin
loop@ for (i in 1..100) {
    for (j in 1..100) {
        if (i * j > 5000) break@loop // 跳出外层循环 loop
        if (j % 2 == 0) continue@loop // 继续外层循环的下一次迭代
    }
}
```

#### 标记 Lambda 表达式
这是 Kotlin 中最常见的标签用途，用于从 Lambda 中返回到外围函数。

```kotlin
fun foo() {
    listOf(1, 2, 3, 4, 5).forEach lit@{
        if (it == 3) return@lit // 仅从当前 Lambda 返回，继续 forEach 的下一次迭代
        print(it)
    }
    print(" done with explicit label")
}
// 输出: 1245 done with explicit label
```

### 2.2 隐式标签（Implicit Labels）
对于接受 Lambda 作为参数的函数（如 `forEach`, `map`, `filter`），可以使用与函数名相同的标签。

```kotlin
fun foo() {
    listOf(1, 2, 3, 4, 5).forEach {
        if (it == 3) return@forEach // 隐式标签，等同于 return@lit
        print(it)
    }
    print(" done with implicit label")
}
```

### 2.3 从 Lambda 返回到外围函数
如果你希望从 Lambda 中直接返回外围函数（而非仅跳出 Lambda），可以使用**匿名函数**或**限定返回**。

#### 方法一：使用匿名函数
匿名函数中的 `return` 会从匿名函数本身返回，而不是从外围函数返回。但这通常不是我们想要的“跳出外围函数”的效果。若要跳出外围函数，需结合标签。

#### 方法二：限定返回（Qualified Return）
使用标签明确指定返回位置。

```kotlin
fun run() {
    var result = ""
    listOf(1, 2, 3).forEach outer@{
        if (it == 2) return@outer // 只跳过当前元素
        result += it
    }
    println(result) // 13
}
```

**关键区别：**
*   `return`: 从最内层的**函数**返回。如果在 Lambda 中使用，且该 Lambda 是**内联函数**（inline function）的一部分，`return` 可能会从外围函数返回（非局部返回）。
*   `return@label`: 从标记的 Lambda 或循环返回。

#### 非局部返回（Non-local Returns）
只有当 Lambda 传递给**内联函数**（inline function）时，才允许使用不带标签的 `return` 从外围函数返回。

```kotlin
inline fun myInlineFunction(block: () -> Unit) {
    block()
}

fun test() {
    myInlineFunction {
        println("Before return")
        return // 合法！因为 myInlineFunction 是 inline 的，return 直接从 test() 返回
    }
    println("This will not be printed")
}
```

如果函数不是 inline 的，则必须使用 `return@label`。

---

## 3. 异常 (Exceptions)

Kotlin 的异常处理机制与 Java 类似，但有一些重要的简化和安全改进。

### 3.1 抛出异常
使用 `throw` 关键字。异常是对象，通常继承自 `Throwable`。

```kotlin
if (name.isEmpty()) {
    throw IllegalArgumentException("Name cannot be empty")
}
```

Kotlin 标准库提供了一些常用的异常类：
*   `IllegalArgumentException`
*   `IllegalStateException`
*   `NullPointerException` (通常由 `!!` 操作符触发)
*   `IndexOutOfBoundsException`
*   `UnsupportedOperationException`

### 3.2 捕获异常 (`try-catch-finally`)

```kotlin
try {
    val result = 10 / 0
} catch (e: ArithmeticException) {
    println("Arithmetic error: ${e.message}")
} catch (e: Exception) {
    println("General error: ${e.message}")
} finally {
    println("This always executes")
}
```

### 3.3 `try` 作为表达式
与 `if` 和 `when` 一样，`try` 也是一个表达式，可以返回值。

```kotlin
val result: Int = try {
    Integer.parseInt("123")
} catch (e: NumberFormatException) {
    -1 // 默认值
}
println(result) // 123
```

> **注意**：如果 `try` 块正常执行，值是最后一个表达式的值；如果抛出异常并被捕获，值是相应 `catch` 块中最后一个表达式的值。`finally` 块的值不会影响表达式的结果。

### 3.4 受检异常 vs 非受检异常
这是 Kotlin 与 Java 的最大区别之一：

*   **Java**：区分受检异常（Checked Exceptions，如 `IOException`）和非受检异常（Unchecked Exceptions，如 `RuntimeException`）。受检异常必须在方法签名中声明或在代码中捕获。
*   **Kotlin**：**不区分受检异常和非受检异常**。所有异常都是非受检的。
    *   你不需要在函数签名中声明 `throws`。
    *   编译器不强制你捕获任何异常。
    *   这简化了 API 设计，避免了繁琐的 `try-catch` 包裹，但也要求开发者更自觉地处理潜在错误。

```kotlin
// Kotlin 中不需要声明 throws IOException
fun readFile(path: String): String {
    return File(path).readText() // 可能抛出 IOException，但无需声明或强制捕获
}
```

### 3.5 `Nothing` 类型
如果一个函数永远无法正常返回（总是抛出异常），其返回类型是 `Nothing`。

```kotlin
fun fail(message: String): Nothing {
    throw IllegalStateException(message)
}

// 编译器知道 fail() 不会返回，因此后面的代码不可达
val s = fail("Error") 
// println(s) // 编译错误：Unreachable code
```

`Nothing` 是所有类型的子类型，常用于智能转换的场景：

```kotlin
fun handleValue(value: String?) {
    if (value == null) {
        throw IllegalArgumentException("Value must not be null")
        // 此处之后，编译器知道 value 不可能为 null，因为如果为 null 已经抛异常退出了
    }
    println(value.length) // 安全调用，无需 !!
}
```

---

## 对比

| 特性 | Java | Kotlin |
|------|------|--------|
| 三元运算符 | `condition ? a : b` | 无，使用 `if (condition) a else b` |
| Switch | `switch-case` (有限制) | `when` (强大，支持任意表达式、范围、类型) |
| For 循环 | `for (int i=0; i<n; i++)` | `for (i in 0 until n)` 或 `for (item in collection)` |
| 数组/集合遍历 | 需手动获取 Iterator 或索引 | `for ((index, value) in list.withIndex())` |
| 异常声明 | 必须声明 Checked Exceptions | 无 Checked Exceptions，所有异常均为 Unchecked |
| Try 返回值 | 语句，不能直接赋值 | 表达式，可赋值 `val x = try { ... } catch { ... }` |
| Lambda 返回 | 复杂，需借助异常或标志位 | 支持 `return@label` 和内联函数的非局部返回 |

# 包与导入
## 1. 包声明 (Package Declaration)

每个 Kotlin 文件都可以以 `package` 关键字开头来声明所属的包。

### 基本语法
```kotlin
package com.example.myapp

class User {
    // ...
}
```

### 关键特性
1. **目录结构不必完全匹配包名**：
   - 在 Java 中，包名通常严格对应文件系统的目录结构。
   - 在 Kotlin 中，**物理目录结构不需要与包名匹配**。源文件可以放在任意位置，只要编译器知道去哪里找即可。不过，为了项目可维护性，通常建议保持约定俗成的目录结构。

2. **默认包**：
   - 如果文件中没有声明 `package`，则该文件中的内容属于“默认包”（default package）。
   - **注意**：尽量避免使用默认包，尤其是在大型项目中，因为它会导致命名冲突且无法被其他包显式导入。

3. **包的作用域**：
   - 包不仅包含类（Class），还可以包含：
     - 函数（Functions）
     - 属性（Properties/Variables）
     - 类型别名（Type Aliases）
     - 对象声明（Object Declarations）
   - 这意味着你可以在包级别直接定义函数和变量，而不需要包裹在类中（即**顶层声明**）。

---

## 2. 导入 (Imports)

要在当前文件中使用其他包中的类、函数或属性，需要使用 `import` 关键字。

### 基本导入
```kotlin
import com.example.utils.StringUtils
import java.util.ArrayList
```

### 导入所有内容（Wildcard Import）
使用 `*` 可以导入包下的所有可见成员：
```kotlin
import com.example.utils.*
```
- **注意**：Kotlin 编译器非常智能，它只会导入实际使用的成员，不会造成性能损失。但在阅读代码时，显式导入通常更清晰。

### 避免命名冲突：别名导入 (Alias Import)
这是 Kotlin 比 Java 更强大的地方之一。如果两个包中有同名的类，或者你想给长名称起个短别名，可以使用 `as` 关键字。

```kotlin
import java.util.HashMap
import kotlin.collections.HashMap as KHashMap // 解决命名冲突

fun main() {
    val javaMap = HashMap<String, Int>()
    val kotlinMap = KHashMap<String, Int>()
}
```

---

## 3. 默认导入 (Default Imports)

Kotlin 会自动为每个文件导入一些常用的包，因此你无需手动编写这些 import 语句。

默认导入的包包括：
- `kotlin.*`
- `kotlin.annotation.*`
- `kotlin.collections.*`
- `kotlin.comparisons.*` (自 Kotlin 1.1 起)
- `kotlin.io.*`
- `kotlin.ranges.*`
- `kotlin.sequences.*`
- `kotlin.text.*`

此外，根据目标平台不同，还会额外导入：
- **JVM**: `java.lang.*`, `kotlin.jvm.*`
- **JS**: `kotlin.js.*`
- **Native**: `kotlin.native.*`

这就是为什么你可以直接使用 `String`、`List`、`println()` 而无需导入的原因。

---

## 4. 顶层函数与属性 (Top-Level Functions and Properties)

在 Java 中，所有代码必须在类中。而在 Kotlin 中，你可以直接在包里定义函数和变量。

**文件: `com/example/utils/MathUtils.kt`**
```kotlin
package com.example.utils

// 顶层函数
fun add(a: Int, b: Int): Int {
    return a + b
}

// 顶层属性
const val PI = 3.14159
```

**在其他文件中使用：**
```kotlin
package com.example.app

import com.example.utils.add
import com.example.utils.PI

fun main() {
    println(add(1, 2)) // 直接调用，无需类名
    println(PI)
}
```

> **最佳实践**：对于工具函数，优先考虑使用顶层函数，而不是创建只有静态方法的类（如 Java 中的 `Utils` 类）。这更符合 Kotlin 的函数式编程风格。

---

## 5. 可见性修饰符与包 (Visibility Modifiers)

Kotlin 的可见性修饰符与包密切相关：

| 修饰符 | 说明 |
|--------|------|
| `public` (默认) | 任何地方都可见。 |
| `internal` | **模块内可见**。在同一 Module（如 Gradle 模块、Maven 模块）中可见，不同 Module 不可见。这是 Kotlin 特有的，非常适合库开发。 |
| `protected` | 仅用于类和接口内部，子类可见。**不能用于顶层声明**。 |
| `private` | 仅在当前**文件**中可见（如果是顶层声明）；或在当前**类**中可见（如果是类成员）。 |

### 示例：`internal` 的作用
```kotlin
// File: internal_api.kt
package com.example.lib

internal fun helperFunction() {
    // 这个函数只能在同一个 Module 中被调用
    // 其他依赖此 Module 的项目无法看到它
}
```

---

## 6. 包与 JVM 互操作性

由于 Kotlin 运行在 JVM 上，包名最终会映射到 Java 的包结构。

### 1. `@JvmName` 注解
当你在 Kotlin 中定义顶层函数时，编译器会生成一个名为 `FileNameKt` 的 Java 类（例如 `MathUtils.kt` 生成 `MathUtilsKt.java`）。如果你想在 Java 中调用时改变这个类名，可以使用 `@JvmName`。

```kotlin
@file:JvmName("MathHelper") // 更改生成的 Java 类名
package com.example.utils

fun add(a: Int, b: Int) = a + b
```
在 Java 中调用：
```java
import com.example.utils.MathHelper;
MathHelper.add(1, 2);
```

### 2. `@JvmMultifileClass`
如果你有多个 Kotlin 文件想要合并成一个 Java 类，可以使用此注解（较少用，主要用于库设计）。

---

## 7. 常见陷阱与最佳实践

### 最佳实践
1. **使用小写字母作为包名**：遵循 Java 惯例，如 `com.example.project`。
2. **避免深层嵌套**：包层级不要太深，通常 3-4 层足够。
3. **优先使用显式导入**：虽然 `*` 导入方便，但显式导入有助于理解依赖关系。IDE（如 IntelliJ IDEA）可以自动优化导入。
4. **利用 `internal` 隐藏实现细节**：在开发库时，将内部辅助函数标记为 `internal`，只暴露 `public` API。

### 常见错误
1. **命名冲突未处理**：
   ```kotlin
   import java.sql.Date
   import java.util.Date // 编译错误！
   ```
   **解决**：使用别名：
   ```kotlin
   import java.sql.Date as SqlDate
   import java.util.Date as UtilDate
   ```

2. **误以为包名决定物理路径**：
   - 在 Gradle/Maven 项目中，虽然源码通常放在 `src/main/kotlin/com/example/...`，但 Kotlin 编译器并不强制要求这一点。然而，为了构建工具的正确工作，**强烈建议**保持目录结构与包名一致。

3. **在 Android 中混淆包名与应用 ID**：
   - 在 Android 项目中，`package` 在 `AndroidManifest.xml` 或 `build.gradle` 中定义的 `applicationId` 可能不同。Kotlin 源码中的 `package` 仅用于代码组织，不影响 APK 的唯一标识（Application ID）。

---

# 类与对象

## 类（Classes）

### 🔹 核心概念
- **根类 `Any`**：Kotlin 中所有类默认隐式继承自 `Any`（相当于 Java 的 `Object`）。它提供了 `equals()`、`hashCode()`、`toString()` 三个方法。注意：`Any` **不是** `java.lang.Object`，但在 JVM 平台编译后会映射为 `Object`。
- **默认 `final` 语义**：Kotlin 出于**安全性、性能优化（JIT 更易内联）与设计哲学**考虑，类和成员方法默认都是 `final`（不可继承/不可重写）。这强制开发者“显式开放”，避免意外破坏封装。

### 🔹 语法与特性
#### 1. 主构造函数（Primary Constructor）
直接写在类名后，是 Kotlin 类的“第一公民”。
```kotlin
// 自动声明属性，编译器生成 getter/setter 与构造赋值
class User(val id: Int, var name: String) {
    // 若需默认值、校验或复杂逻辑，可配合 init 块
}
```
- 支持参数默认值、命名参数、可见性修饰符。
- 若使用 `val/var`，编译器自动生成字段与访问器；若仅写参数名，则仅为构造函数局部变量。

#### 2. `init` 块
在主构造函数参数赋值后**立即执行**，用于处理无法在签名中表达的初始化逻辑。
```kotlin
class Config(val timeout: Int) {
    init {
        require(timeout > 0) { "超时时间必须大于 0" }
        // 可注册监听器、校验状态、启动轻量级任务等
    }
    // 支持多个 init 块，按声明顺序执行
}
```

#### 3. 次构造函数（Secondary Constructor）
使用 `constructor` 关键字声明，**必须委托给主构造函数**（或另一个次构造函数）：
```kotlin
class Person {
    val name: String
    
    // 次构造函数必须通过 this(...) 委托
    constructor(name: String) : this() {
        this.name = name
    }
    
    // 委托给主构造（若存在）
    constructor(name: String, age: Int) : this(name) {
        // ...
    }
}
```
> 💡 **注意**：若类已有主构造函数，次构造函数**不能**直接调用 `super()`，必须先 `this()`。基类构造调用 `super(...)` 仅在**主构造函数委托**时发生。

#### 4. `this` 与 `super` 作用域
- `this`：指向当前实例。在内部类/嵌套类中可能歧义，需使用**标签化 this**：`this@OuterClass`。
- `super`：调用父类实现。方法重写时必须显式调用 `super.method()`，否则完全覆盖。
- **解析规则**：Kotlin 严格区分“声明类型”与“运行时类型”，所有虚方法调用默认走动态分发（除非标记 `final` 或 `private`）。

### 🔹 最佳实践
1. **优先使用主构造函数**：90% 场景只需主构造 + `val/var` 属性声明。
2. **复杂初始化放 `init`**：避免在构造参数中写表达式副作用；校验、日志、轻量级绑定放在 `init`。
3. **构造期绝不暴露 `this`**：不要在构造函数或 `init` 中将 `this` 注册给回调、线程池、事件总线。此时对象尚未完全初始化，易引发 `NullPointerException` 或状态不一致。
4. 使用**工厂函数/Builder 模式**替代冗长的次构造函数：
   ```kotlin
   // 推荐：顶层工厂函数
   fun createPerson(name: String, age: Int? = null) = Person(name).apply {
       age?.let { this.age = it }
   }
   ```

### 🔹 典型场景
- **数据载体**：配合 `data class`、`value class`（原 `inline class`）
- **配置/上下文对象**：不可变属性 + `init` 校验
- **工具封装**：隐藏实现细节，暴露精简 API

### 🔹 注意事项 / 现代演进
- **无 `static` 关键字**：Kotlin 用以下三种方式替代：
  1. `companion object`：类内部静态作用域，支持接口实现、属性、方法。
  2. **顶层函数/属性**：直接写在 `.kt` 文件顶层，编译后生成 `ClassNameKt` 静态类，**最推荐**。
  3. `@JvmStatic` / `@JvmField`：仅用于 Java 互操作桥接。
- 现代 Kotlin 倾向**减少 `companion object` 滥用**，除非需要访问类内部私有成员或实现接口。

---
## 继承（Inheritance）

### 🔹 核心概念
- **单继承模型**：Kotlin 仅支持单类继承，但支持**多接口实现**。
- **显式 `open` 机制**：基类必须标记 `open` 才能被继承；方法/属性必须标记 `open` 才能被重写。默认 `final` 防止“脆弱基类问题”。

### 🔹 语法与特性
#### 1. 类修饰符
```kotlin
open class Vehicle(val brand: String)        // 可继承
abstract class Engine(val type: String)      // 不可直接实例化，需子类实现
final class Car(brand: String) : Vehicle(brand) // 默认 final，可省略
```

#### 2. `override` 重写规则
- 方法/属性必须显式标记 `override`。
- **可见性不能收窄**：父类 `protected` → 子类可保持 `protected` 或改为 `public`，不可改为 `private`。
- 属性重写可改变可变性：`open val` 可重写为 `override var`，反之不行。
```kotlin
open class Shape {
    open fun draw() { println("Shape") }
    open val color: String get() = "black"
}

class Circle : Shape() {
    override fun draw() {
        super.draw() // 显式调用父类实现
        println("Circle")
    }
    override var color: String = "red" // 允许
}
```

#### 3. 构造链与初始化顺序（关键！）
Kotlin 初始化顺序**严格固定**，与 Java 不同：
1. 基类主构造函数参数赋值
2. 基类属性初始化
3. 基类 `init` 块执行
4. 子类属性初始化
5. 子类 `init` 块执行
```kotlin
open class Base(val x: Int) {
    val y = print("Base.y")
    init { print("Base.init") }
}

class Derived : Base(1) {
    val z = print("Derived.z")
    init { print("Derived.init") }
}
// 输出顺序：Base.y → Base.init → Derived.z → Derived.init
```
> ⚠️ **绝对禁止**在基类构造函数或 `init` 中调用 `open` 方法！此时子类尚未初始化，调用的是子类重写版本，但子类状态为空，极易引发崩溃。

### 🔹 最佳实践
1. **组合优于继承**：用接口委托 `by`、属性持有、策略模式替代深层继承。
2. **按需开放**：仅对明确设计为扩展点的类标记 `open`（如框架生命周期回调、插件 SPI）。
3. **控制继承深度**：建议 ≤ 3 层。过深会导致 `super` 链难以追踪、测试困难、重构成本指数上升。
4. 使用 `sealed class` / `sealed interface` 替代开放继承，实现**封闭类型层次**，编译器可穷举检查。

### 🔹 典型场景
- **UI 组件基类**：Android `View` / `Activity` 生命周期封装
- **策略/模板模式**：抽象基类定义算法骨架，子类实现具体步骤
- **框架扩展点**：如 Ktor 的 `ApplicationCallPipeline`、Room 的 `TypeConverter`

### 🔹 注意事项 / 现代演进
- **`data class` 禁止继承**：`data class` 不能继承非 `Any` 类，也不能被 `open`。因为 `equals()`、`hashCode()`、`copy()` 的自动生成依赖“仅由主构造参数决定状态”的约定，继承会破坏该语义。
- **接口默认实现替代部分继承**：Kotlin 1.1+ 支持接口带实现方法，结合 `by` 委托可大幅减少继承树：
  ```kotlin
  interface Logger {
      fun log(msg: String) = println("[LOG] $msg")
  }
  class Service : Logger by DefaultLoggerImpl() // 委托替代继承
  ```
- **现代趋势**：Kotlin 官方强烈推荐使用 `interface` + 默认实现、`object`（单例）、顶层函数、协程组合子替代传统 OOP 继承。继承仅保留给**语义上真正是 “is-a” 且需状态共享**的场景。

---
这是一份针对你提供大纲的**完整、详细、面向现代 Kotlin（1.9/2.0+）**的深度讲解。内容将严格遵循你的结构，补充原理说明、代码示例、底层机制与工程实践建议，帮助你从“知道语法”走向“写出地道 Kotlin”。

---

## 属性（Properties）

### 核心概念
Kotlin 摒弃了 Java 的 `field` + `get/set` 显式写法，将**字段与访问器统一抽象为“属性”**。声明时自动推断读写能力：
- `val`：只读属性（编译期生成 `get()`，无 `set()`）
- `var`：可变属性（编译期生成 `get()` + `set()`）

> ⚠️ 注意：`val` 仅保证**引用不可变**，若引用的是可变对象（如 `MutableList`），对象内部状态仍可修改。

### 语法与特性

#### 1. 自定义访问器与 `field` 标识符
Kotlin 编译器会为 `var`/`val` 自动生成**幕后字段（backing field）**。在自定义访问器中，通过 `field` 关键字引用它：
```kotlin
class User(var name: String = "") {
    // 自定义 getter：格式化输出
    val displayName: String
        get() = name.trim().replaceFirstChar { it.uppercase() }

    // 自定义 setter：带校验逻辑
    var age: Int = 0
        set(value) {
            require(value >= 0) { "年龄不能为负数" }
            field = value // ⭐ 必须使用 field，不能写 this.age = value（会递归）
        }
}
```
- `field` **仅能在属性的访问器中使用**，且该属性必须拥有幕后字段。
- 若属性只有自定义 getter 且无初始值/委托，则**不会生成幕后字段**（纯计算属性）。

#### 2. `lateinit var` 延迟初始化
用于非空类型，但构造期无法立即赋值的场景：
```kotlin
class AndroidActivity {
    lateinit var viewModel: MainViewModel // 非空，但 onCreate() 前无法初始化

    fun onCreate() {
        viewModel = ViewModelProvider(this).get(MainViewModel::class.java)
    }
}
```
- **限制**：
  - 只能修饰 `var`，不能修饰 `val`、基本类型（Kotlin 1.2 起支持基本类型，但极少用）
  - 不能用在构造函数参数、顶层属性、对象声明中
  - 使用前可通过 `::viewModel.isInitialized` 安全检查

#### 3. 可见性独立控制
属性的可见性默认继承自声明处，但可为 getter/setter 单独降级：
```kotlin
class Config {
    var apiKey: String = "default"
        private set // 外部只读，内部可改

    var debugMode: Boolean = false
        protected get // 子类可读，外部不可见
}
```

### 最佳实践
1. **优先 `val`**：不可变性是函数式编程与线程安全的基石。
2. **访问器保持轻量**：不要在 `get()` 中执行 IO、网络请求或复杂计算，违背“属性访问应快速无副作用”的语言设计哲学。
3. **`lateinit` 仅用于特定场景**：依赖注入（Dagger/Koin）、测试 Mock、Android 生命周期绑定。其他场景优先 `by lazy` 或构造器注入。
4. **状态管理现代化**：UI 状态推荐 `StateFlow`/`MutableState`；领域状态推荐密封类/接口 + 不可变数据类。

### 注意事项 / 现代演进
- **Kotlin 2.0+**：编译器对 `lateinit` 的检查更严格，禁止在值类（value class）、内联类中使用；未初始化访问会生成更精确的 `UninitializedPropertyAccessException` 堆栈。
- **替代方案趋势**：
  - `val data by lazy { computeExpensive() }`（线程安全懒加载）
  - `sealed interface UiState { object Loading : UiState; data class Success(val d: Data) : UiState }`（替代可变状态标志位）

### 典型场景
- DTO/VO 数据载体
- Android `ViewModel` 配置项
- 缓存/连接池的延迟初始化
- 不可变配置类（`val` + `data class`）

---

## 接口（Interfaces）

### 核心概念
接口是**纯行为契约**，不包含实例状态。Kotlin 接口方法默认 `open`，支持默认实现，可声明属性（但无幕后字段）。

### 语法与特性

#### 1. 基础声明与默认实现
```kotlin
interface Repository<T> {
    fun getById(id: String): T
    fun save(item: T) = println("默认保存逻辑: $item") // 默认实现
}
```

#### 2. 接口属性
接口属性**不能有幕后字段**，只能是：
- 抽象属性（实现类必须提供）
- 带 getter 的计算属性（每次调用重新计算）
```kotlin
interface Configurable {
    val version: Int // 抽象
    val isEnabled: Boolean get() = version > 1 // 计算属性，无 field
}
```

#### 3. 多实现冲突解决（菱形问题）
当类实现多个接口且存在同名方法时，需显式指定调用哪个父接口：
```kotlin
interface A { fun print() = println("A") }
interface B { fun print() = println("B") }

class C : A, B {
    override fun print() {
        super<A>.print() // 明确调用 A 的默认实现
        super<B>.print() // 明确调用 B 的默认实现
    }
}
```

### 最佳实践
1. **接口保持轻量**：单一职责，方法数 ≤ 5 为宜。
2. **默认实现仅用于**：向后兼容、工具方法、协议扩展（如 `Iterable` 的 `filter`/`map`）。
3. **优先组合而非继承**：接口表达“能做什么”，类表达“是什么”。
4. **避免在接口中暴露状态**：接口属性应为只读或纯计算，状态由实现类持有。

### 注意事项 / 现代演进
- **Kotlin 1.8+ `sealed interface`**：支持穷举 `when`，用于类型安全的状态机/事件流：
  ```kotlin
  sealed interface NetworkResult<out T> {
      data class Success<T>(val data: T) : NetworkResult<T>
      object Loading : NetworkResult<Nothing>
      data class Error(val msg: String) : NetworkResult<Nothing>
  }
  ```
- **JVM 字节码优化**：Kotlin 2.0 采用全新 IR 后端，接口默认方法生成的桥接方法更少，性能更接近 Java 8+ 原生接口。
- **无状态约束**：接口属性不允许 `var` + 自定义 setter + `field`，编译器会直接报错。

### 典型场景
- 插件/扩展点契约（如 `CoroutineScope`、`LifecycleObserver`）
- 领域驱动设计中的行为抽象（`PaymentStrategy`、`TaxCalculator`）
- 跨模块通信协议（API 定义层）
- 状态机建模（配合 `sealed interface`）

---

## 函数式（SAM）接口

### 核心概念
SAM（Single Abstract Method）接口仅含一个抽象方法。Kotlin 1.4 引入 `fun interface` 关键字，支持 **Lambda 自动转换（SAM Conversion）**。

### 语法与特性

#### 1. `fun interface` 声明
```kotlin
fun interface ErrorHandler {
    fun handle(error: Throwable): Boolean
}
```

#### 2. Lambda 自动转换
```kotlin
fun execute(handler: ErrorHandler) {
    handler.handle(RuntimeException("test"))
}

// 直接传 Lambda，编译器自动转换为 ErrorHandler 实例
execute { error ->
    error is IllegalArgumentException
}
```

#### 3. 与 Java 互操作
- 兼容 Java `@FunctionalInterface`，Kotlin 调用 Java SAM 接口时自动转换：
  ```kotlin
  // Java: public interface OnItemClickListener { void onClick(View v); }
  recyclerView.setOnItemClickListener { v, pos -> println("Clicked: $pos") }
  ```
- Kotlin 定义的 `fun interface` 在 Java 侧同样可被 Lambda 替代（需 Kotlin 1.4+ 编译）。

### 最佳实践
1. **纯 Kotlin 项目优先函数类型**：`(T) -> R` 是 Kotlin 一等公民，性能更好、语法更短。
2. **使用 `fun interface` 的场景**：
   - 调用/暴露给 Java 代码
   - 需要命名语义（`Validator` vs `(String) -> Boolean`）
   - 未来可能扩展为多方法接口（预留演进空间）
3. **避免滥用**：不要为每个回调都建 `fun interface`，函数类型+类型别名通常更优雅：
   ```kotlin
   typealias OnClick = (View) -> Unit
   ```

### 注意事项 / 现代演进
- **性能差异**：函数类型在 Kotlin 2.0 中经过深度优化，内联与逃逸分析更高效。`fun interface` 会生成额外包装类，仅在互操/语义明确时使用。
- **Kotlin 2.0 改进**：SAM 转换的编译器诊断更清晰，错误位置精准；与协程 `suspend` 函数结合时类型推断更稳定。
- **不可与 `suspend` 混用**：`fun interface` 本身不能直接声明为 `suspend`，但方法可以：
  ```kotlin
  fun interface AsyncLoader { suspend fun load(): Data } // ✅ 合法
  ```

### 典型场景
- Android 事件监听器（`OnClickListener`、`TextWatcher`）
- 策略模式/回调封装（替代匿名内部类）
- DSL 构建中的语义化函数包装
- Java 互操作层（Retrofit、OkHttp 拦截器接口）

---

### 📊 快速选型指南

| 需求场景                  | 推荐方案                          | 理由                                     |
|--------------------------|----------------------------------|------------------------------------------|
| 只读配置/常量             | `val`                            | 不可变、线程安全、编译器优化              |
| 延迟加载复杂对象          | `by lazy`                        | 线程安全懒加载、`val` 语义                |
| DI/测试桩/生命周期绑定    | `lateinit var`                   | 明确延迟契约、避免空指针包装              |
| 纯 Kotlin 回调            | `(T) -> R` 函数类型               | 零开销、语法简洁、支持协程 `suspend`      |
| 跨 Java 互操作/命名语义   | `fun interface`                  | 兼容 Java、IDE 提示清晰、易扩展           |
| 行为契约/插件扩展         | `interface`                      | 多实现、默认方法、无状态约束              |
| 状态机/穷举分支           | `sealed interface`               | 编译期穷举检查、类型安全演进              |

---

###  现代 Kotlin 工程建议
1. **属性访问器不是方法**：`get()` 应像访问字段一样快速，耗时操作请命名为 `computeXXX()` 或 `fetchXXX()`。
2. **接口是“能力”不是“数据”**：若发现接口需要大量 `var` 或状态，考虑改为抽象类或组合委托。
3. **Kotlin 2.0 编译器红利**：启用 `-Xir`（默认开启）、使用 `@OptIn` 替代过时实验性 API、关注 `kotlinx.collections.immutable` 库替代可变集合属性。
4. **测试友好性**：`lateinit` 在单元测试中易漏初始化，推荐构造器注入 + `@Test` 显式赋值，或使用 `mockk` 的 `relaxUnitFun`。


## 可见性修饰符（Visibility Modifiers）

### 🔹 核心概念
可见性修饰符是 Kotlin 封装机制的基石，用于控制类、成员、顶层声明的暴露边界。与 Java 的 `package-private` 不同，Kotlin 通过 `internal` 引入了 **模块级可见性**，使多模块架构的 API 治理更加清晰。

### 🔹 语法与特性
| 修饰符 | 作用域 | 说明 |
|--------|--------|------|
| `public`（默认） | 全局可见 | 任何能访问声明位置的作用域均可调用 |
| `private` | 当前文件或当前类/对象内 | 顶级声明仅限同文件；类成员仅限类内部 |
| `protected` | 当前类及其子类 | **不可用于顶层声明**；子类可重写为更宽可见性 |
| `internal` | 同一模块内 | 模块定义：Gradle `module`/`subproject`、Maven `module`、IDE Module 或 Source Set |

**细节特性**：
- 构造函数、属性 setter 可独立指定可见性：
  ```kotlin
  class Config public constructor(val name: String) {
      internal var cache: Map<String, Any> = emptyMap()
          private set // setter 仅类内部可见
  }
  ```
- 顶层函数/属性同样支持 `private`/`internal`，适合做模块内共享工具。

### 🔹 最佳实践
1. **最小暴露原则**：默认不写 `public`，按需开放。实现细节一律 `private`。
2. **库开发分层**：
   - 对外 API：`public`
   - 模块内共享实现：`internal`
   - 仅供 `inline` 函数调用的内部 API：配合 `@PublishedApi internal` 暴露字节码，但编译期仍隐藏。
3. **测试隔离**：使用 `internal` + `@VisibleForTesting`，或在 `testFixtures` 中通过 `friend` 机制隔离，避免污染生产代码。

### 🔹 典型场景
- **多模块架构**：底层 `data` 模块用 `internal` 隐藏实体转换逻辑，仅暴露 `public` 的领域模型。
- **API 稳定化**：将不稳定的实现标记为 `internal`，后续重构不影响下游编译。
- **Android/KMP 组件化**：共享 `internal` 适配器类，防止业务模块直接依赖基础设施细节。

### ⚠️ 注意事项 / 现代演进
- **跨平台差异**：Kotlin/JS 与 Kotlin/Native 中，`internal` 会编译为 `public` 但附加名称混淆（mangling）。若需与 C/JS 互操作，符号仍会暴露，需配合 ABI 约定。
- **反射绕过**：`kotlin.reflect` 可通过 `isAccessible = true` 突破编译期检查，但运行期可能受平台沙盒限制（如 Android R8 混淆后失效）。
- **K2 编译器强化**：K2 对跨模块 `internal` 的误用警告更严格，支持更精准的增量编译可见性追踪。
- **替代方案**：Android 生态常用 `@RestrictTo(Scope.LIBRARY_GROUP)` 配合可见性实现细粒度控制。

---
## 扩展（Extensions）

### 🔹 核心概念
扩展允许在不修改原类、不继承的前提下，为现有类型“附加”函数或属性。**本质是静态解析的语法糖**：编译器将扩展转换为以接收者为第一个参数的静态工具方法，不修改原类字节码。

### 🔹 语法与特性
```kotlin
// 扩展函数
fun String.addExclamation(): String = "$this!"

// 扩展属性（无 backing field）
val String.lastChar: Char
    get() = this[length - 1]

// 可空接收者扩展
fun Int?.safeToString(): String = this?.toString() ?: "null"

// 伴生对象扩展（模拟静态工厂）
class User private constructor(val id: String) {
    companion object {
        fun fromId(id: String) = User(id)
    }
}
// 等价写法（更简洁）：
fun User.Companion.fromId(id: String) = User(id)
```

**关键特性**：
- `this` 始终指向接收者实例。
- **成员优先原则**：若接收者类已存在同名同参成员，扩展函数将被遮蔽（编译期直接绑定到成员）。
- **静态分发**：扩展函数的调用基于**声明时的静态类型**，而非运行时实际类型。
- 无多态特性：扩展不会被子类继承或重写。

### 🔹 最佳实践
1. **适用场景**：工具函数、DSL 构建、第三方库适配（如 Retrofit + Coroutines）。
2. **避免覆盖核心语义**：切勿扩展 `equals`/`hashCode`/`toString` 破坏对象契约。
3. **控制作用域**：通过包/文件可见性限制扩展范围，避免全局污染（如 `kotlin.collections` 内的扩展仅限标准库使用）。
4. **性能敏感场景**：对高频调用的扩展优先使用 `inline`，减少 lambda 分配开销；或直接使用静态工具类。

### 🔹 典型场景
- **Android UI**：`View.onClick { ... }`、`Intent.putExtraBundle`
- **集合操作**：`List<T>.filterIsInstance()`、`Sequence<T>.asyncMap`
- **第三方适配**：`OkHttpClient.newCall().await()`（Coroutines 对 Java 库的 Kotlin 化包装）

### ⚠️ 注意事项 / 现代演进
- **扩展属性无 backing field**：不能声明 `field`，只能定义 `get()`/`set()`，底层必须依赖原对象状态或实时计算。
- **`@OptIn` 的准确用法**：`@OptIn` 本身**不控制可见性**，而是用于“批准使用”被 `@RequiresOptIn` 标记的实验性扩展。真正限制可见性仍依赖 `private/internal` 或平台注解（如 `@RestrictTo`）。
- **静态分发陷阱**：
  ```kotlin
  val any: Any = "hello"
  any.addExclamation() // ❌ 调用 Any 的扩展（若存在），而非 String 的扩展
  ```
  设计 API 时需注意接收者类型推断，必要时使用泛型约束或重载。
- **K2 编译器优化**：K2 显著改进了扩展函数的重载解析与类型推断，减少“歧义调用”编译错误；IDE 提示更精准，支持跨模块扩展的实时索引。
- **现代替代方案**：若扩展需要维护状态，优先考虑 `by lazy` 委托、`value class`（内联类）或组合模式。Kotlin 2.0+ 对扩展的字节码生成进一步瘦身，性能接近原生成员。

---
### 💡 架构级建议
| 维度 | 可见性修饰符 | 扩展 |
|------|--------------|------|
| **设计目标** | 控制暴露边界，保障封装性 | 提升可读性，适配现有类型 |
| **运行时影响** | 仅编译期检查（反射除外） | 静态分发，无多态，零额外对象分配 |
| **库作者必看** | `internal` + `@PublishedApi` 组合控制内联函数暴露 | 避免扩展破坏第三方类契约，明确标注 `@Experimental` 或可见性 |
| **K2/Kotlin 2.0 演进** | 更严格的模块可见性追踪、增量编译优化 | 重载解析增强、IDE 实时类型推断、内联扩展性能提升 |

掌握这两项特性，能显著提升 Kotlin 代码的**可维护性**与**API 设计质量**。在实际项目中，建议结合 `kotlinx` 规范与 Detekt 规则（如 `MaxVisibility`、`UnnecessaryAbstractClass`）进行自动化治理。如需针对特定场景（如 KMP 多模块、Android Jetpack 适配）展开，可提供具体代码片段进一步剖析。
以下基于你提供的提纲，结合 Kotlin 1.9/2.0 的最新特性与工程实践，对三个核心模块进行**原理剖析、代码演示、避坑指南与现代演进**的详细讲解。

---

## 数据类（Data Class）

### 🔍 核心原理
`data class` 本质是 Kotlin 编译器提供的**语法糖**，用于替代 Java 中冗长的 POJO。编译器会根据主构造函数中声明的 `val`/`var` 属性，自动推导并生成：
- `equals()` / `hashCode()`：基于所有主构造参数进行结构相等性比较
- `toString()`：格式为 `ClassName(prop1=value1, prop2=value2)`
- `copy()`：实现**浅拷贝**，允许通过命名参数选择性覆盖字段
- `componentN()`：`N` 从 1 开始，按声明顺序生成，用于解构赋值（Destructuring）

### 💻 典型用法与编译器行为
```kotlin
data class User(
    val id: String,
    val name: String,
    var age: Int,
    val tags: List<String> = emptyList() // 支持默认值
)

fun main() {
    val u1 = User("1", "Alice", 25)
    
    // 1. copy() 浅拷贝 + 命名参数覆盖
    val u2 = u1.copy(name = "Bob") // id/tags 引用不变，仅替换 name
    
    // 2. 解构（依赖 component1(), component2()...）
    val (id, name, age) = u2
    println("$id, $name, $age")
    
    // 3. 结构相等 vs 引用相等
    val u3 = User("1", "Alice", 25)
    println(u1 == u3)  // true (equals 基于属性值)
    println(u1 === u3) // false
}
```

### ⚠️ 避坑指南
| 场景 | 风险 | 正确做法 |
|------|------|----------|
| 将 `data class` 用作 `Map` 的 Key 或放入 `Set` | 若属性含可变集合（如 `var tags: MutableList`），`hashCode()` 会随集合变化，导致 Map 失效 | 属性全声明为 `val`，集合使用只读类型（`List`/`Set`/`Map`） |
| 在 `data class` 中写业务方法 | 破坏单一职责，难以测试与复用 | 拆分为扩展函数或独立的 Service/UseCase 类 |
| 期望 `copy()` 深拷贝 | `copy()` 仅复制引用，嵌套对象会共享状态 | 对嵌套复杂对象手动实现 `deepCopy()`，或改用 `value class`/序列化库 |

### 🚀 现代演进（Kotlin 1.9+）
- **`copy()` 性能优化**：编译器生成更高效的字节码，减少临时对象分配；在高频状态更新（如 Compose/Redux）中收益显著。
- **替代方案建议**：
  - 仅需性能包裹单值 → 使用 `@JvmInline value class`
  - 需类型安全分支 → 升级为 `sealed class/interface`
  - 需不可变深拷贝 → 考虑 `kotlinx.serialization` 或 `AutoValue` 风格代码生成

---

## 密封类与密封接口（Sealed Class / Interface）

### 🔍 核心原理
`sealed` 修饰的类/接口表示**受限的继承树**。编译器在编译期即可获知所有可能的子类，因此：
- `when` 表达式可自动校验是否穷举（Exhaustive），无需 `else` 分支
- 提供类型安全的多态路由，避免传统 `enum` 无法携带状态的问题
- 支持 `object`（单例状态）、`data class`（携带数据）、`class`（含行为）混用

### 💻 典型用法
```kotlin
// Kotlin 1.5+ 支持跨文件，但必须在同一模块内
sealed interface NetworkResult<out T> {
    data class Success<T>(val data: T) : NetworkResult<T>
    data class Error(val code: Int, val message: String) : NetworkResult<Nothing>
    object Loading : NetworkResult<Nothing>
}

fun handleResult(result: NetworkResult<String>) {
    // ✅ 编译器强制穷举检查，漏掉分支会报编译错误
    when (result) {
        is NetworkResult.Loading -> showProgress()
        is NetworkResult.Success -> displayData(result.data)
        is NetworkResult.Error -> showToast(result.message)
    }
}
```

### ⚠️ 避坑指南
| 场景 | 风险 | 正确做法 |
|------|------|----------|
| 子类定义在外部模块或动态加载 | 编译器无法识别，`when` 仍需 `else`，失去穷举优势 | 严格保证同一 Gradle 模块/同一 source set |
| 分支过多（>10个） | `when` 膨胀，维护成本陡增 | 按领域拆分多个 `sealed` 树，或使用状态机库（如 `Orbit`/`MvRx`） |
| 误用 `open` 修饰子类 | 破坏受限继承语义，其他模块可随意继承 | 子类默认 `final`，无需也不应加 `open` |

### 🚀 现代演进（Kotlin 1.5 → 2.0）
- **跨文件支持**：1.5 前要求子类与 `sealed` 同文件；1.5 后放宽至**同模块**，大幅提升架构灵活性。
- `sealed interface`：支持多重实现，可与普通接口组合，避免单继承限制。
- **Kotlin 2.0 编译器增强**：对 `when` 的穷举检查更严格，支持嵌套 `sealed` 的自动推导；生成字节码更紧凑，反射开销降低。
- **替代枚举**：当分支需要携带不同数据或行为时，优先用 `sealed`；仅需固定常量时，仍用 `enum class`（底层 `values()` 数组性能更高）。

---

## 泛型进阶：`in` / `out` / `where` 与类型擦除

### 🔍 核心原理
Kotlin 泛型基于 JVM 实现，受**类型擦除**限制（运行时泛型参数不可见）。为保障类型安全，引入：
- **声明处方差**：`class Producer<out T>` / `class Consumer<in T>`
- **使用处方差**：`List<out Number>` / `MutableList<in Int>`
- **多重约束**：`where T : A, T : B`
- **类型保留**：`inline fun <reified T>` 突破擦除

### 💻 核心语法与场景
#### 1. 协变 `out`（只读/生产者）
```kotlin
// 只能作为返回值（生产者），不能作为参数
interface Repository<out T> {
    fun get(): T          // ✅ 协变位置
    // fun save(t: T)     // ❌ 编译错误：逆变位置不允许 out
}

val strRepo: Repository<String> = object : Repository<String> { override fun get() = "hi" }
val anyRepo: Repository<Any> = strRepo // ✅ 安全向上转型
```

#### 2. 逆变 `in`（只写/消费者）
```kotlin
interface EventHandler<in T> {
    fun handle(event: T)  // ✅ 逆变位置
    // fun get(): T       // ❌ 协变位置不允许 in
}

val anyHandler: EventHandler<Any> = EventHandler { println(it) }
val strHandler: EventHandler<String> = anyHandler // ✅ 安全向下转型
```

#### 3. `where` 多重约束
```kotlin
fun <T> process(item: T) where T : Comparable<T>, T : Cloneable {
    // T 必须同时实现 Comparable 和 Cloneable
    val copy = item.clone() as T
    println(item.compareTo(copy))
}
```

#### 4. `reified` 突破类型擦除
```kotlin
// 必须是 inline 函数，且只能用于参数/局部变量，不能用于类字段
inline fun <reified T> Any.safeCast(): T? = this as? T

inline fun <reified T : View> ViewGroup.find(): T? = findViewById(T::class.java)

// 运行时可获取真实类型
fun <T> printType(value: T) {
    // value is T // ❌ 擦除后等价于 value is Any
}
inline fun <reified T> printReifiedType(value: T) {
    println(value is T) // ✅ 编译器替换为实际类型检查
}
```

### ⚠️ 避坑指南
| 概念 | 常见误区 | 正确实践 |
|------|----------|----------|
| `*` 星投影 | 认为 `List<*>` 等同于 `List<Any>` | 实际是 `List<out Any?>`，**只读不可写**，仅用于安全接收未知类型 |
| 过度使用 `reified` | 在非 `inline` 函数或类中声明 | 仅用于高频类型检查/反射场景；注意 `inline` 会增加字节码体积 |
| 方差声明错误 | 在 `MutableList` 上标 `out` | 可变集合默认**不变**（Invariant），需明确读写边界 |

### 🚀 现代演进（Kotlin 2.0）
- **泛型推断增强**：编译器对嵌套泛型、lambda 类型推断更精准，减少显式类型标注。
- `reified` 编译优化：内联代码生成更智能，避免重复字节码膨胀；结合 `kotlinx.metadata` 可安全实现泛型序列化。
- **工程建议**：
  - 优先使用**声明处方差**（类/接口级别），保持 API 简洁
  - 仅在使用处需要临时放宽类型时，用**使用处方差**
  - 复杂泛型签名用 `typealias` 简化，如 `typealias StringValidator = (String) -> Boolean`

---

### 🧩 跨特性联动最佳实践

| 场景 | 推荐组合 | 理由 |
|------|----------|------|
| 网络请求状态管理 | `sealed interface Result<T>` + `data class Success<T>` + `reified` 扩展 | 类型安全、穷举检查、泛型保留 |
| Compose 状态快照 | `data class UiState(val loading: Boolean, val data: List<Item>)` + `copy()` | 不可变、浅拷贝高效、解构方便 |
| 领域事件总线 | `sealed class DomainEvent` + `where T : Event` + `reified` 订阅者 | 有限事件集、编译期校验、运行时类型分发 |

> 💡 **核心心法**：  
> `data` 负责**承载**，`sealed` 负责**分类**，泛型负责**复用**。三者结合可构建高内聚、低耦合、编译期安全的现代 Kotlin 架构。实际项目中应避免“为了用而用”，始终从**数据流向、状态边界、性能开销**三个维度评估设计。
以下基于你提供的提纲，结合 Kotlin 1.9/2.0 的最新语言规范、JVM 字节码行为与工程实践，对 **嵌套类、枚举类、值类（原内联类）** 进行系统化深度讲解。

---

## 嵌套类（Nested Classes）

### 🔍 核心原理
Kotlin 中的嵌套类默认是**静态的**（等价于 Java 的 `static class`），**不持有外部类实例的隐式引用**。仅当显式添加 `inner` 修饰符时，编译器才会生成一个指向外部类的合成引用字段（`this@Outer`），使其成为**内部类**。

```java
// Kotlin 默认嵌套类编译为 Java 静态类
// class Outer { static class Nested { ... } }

// inner 嵌套类编译为 Java 内部类，携带 Outer 实例引用
// class Outer { class Inner { final Outer outer$; Inner(Outer o) { outer$ = o; } } }
```

### 💻 语法与特性演示
```kotlin
class NetworkClient {
    private val timeout = 5000L
    private var retryCount = 0

    // ✅ 默认静态嵌套：无外部引用，轻量级
    class Config {
        val host = "api.example.com"
        // fun resetRetry() { retryCount = 0 } // ❌ 编译错误：无法访问外部非静态成员
    }

    // ✅ inner 内部类：持有外部引用，可访问私有成员
    inner class RetryStrategy {
        fun shouldRetry(): Boolean {
            retryCount++
            return retryCount < 3
        }
        fun printTimeout() = println(timeout) // ✅ 访问 private 成员
    }

    // ✅ 可见性控制：私有嵌套类仅限外部类使用
    private class AuthInterceptor : Interceptor { ... }
}
```

### ⚠️ 避坑与最佳实践
| 场景 | 风险 | 正确做法 |
|------|------|----------|
| 在 Android `Activity/Fragment` 中使用 `inner class` | 隐式持有生命周期对象，极易引发内存泄漏 | 改用 `static` 嵌套类 + `WeakReference`，或抽离为顶层类 |
| 频繁创建 `inner` 实例 | 每次构造多分配 8~16 字节外部引用 + GC 压力 | 优先使用 `companion object`、顶层函数或扩展函数 |
| 嵌套层级过深 | 作用域污染、可读性骤降 | 超过 2 层应考虑拆包；利用 `package` 级可见性替代 |

### 🚀 现代演进与工程建议
- **Kotlin 2.0 编译器优化**：对 `inner` 类的构造指令进行逃逸分析，若外部引用未实际使用，部分场景可自动降级为静态引用（实验性）。
- **架构替代方案**：
  - 需要“关联上下文”但不强耦合 → 使用 **Context Receivers**（Kotlin 2.0 实验性）或 `with(receiver)` 作用域函数
  - 需要静态工厂/常量 → 使用 `companion object` 或顶层 `object`
  - 需要局部状态隔离 → 抽离为独立文件 + `internal` 可见性

### 🧩 典型场景代码（Builder 模式）
```kotlin
class HttpRequest private constructor(val url: String, val method: String, val headers: Map<String, String>) {
    class Builder {
        var url: String = ""
        var method: String = "GET"
        private val headers = mutableMapOf<String, String>()

        fun header(key: String, value: String) = apply { headers[key] = value }
        fun build() = HttpRequest(url, method, headers.toMap())
    }
    // 无需 inner，Builder 与 HttpRequest 解耦且零引用开销
}
```

---

## 枚举类（Enum Classes）

### 🔍 核心原理
枚举在 JVM 中本质是**继承自 `java.lang.Enum` 的 final 类**。每个枚举常量都是该类的静态单例实例，底层通过静态代码块初始化并缓存至 `$VALUES` 数组。Kotlin 在此基础上提供了类型安全的泛型访问器与接口实现能力。

### 💻 语法与特性演示
```kotlin
// 支持属性、方法、抽象方法覆盖
enum class HttpStatus(val code: Int, val category: String) {
    OK(200, "Success") {
        override fun isClientError() = false
    },
    NOT_FOUND(404, "Client Error") {
        override fun isClientError() = true
    },
    INTERNAL_ERROR(500, "Server Error") {
        override fun isClientError() = false
    };

    abstract fun isClientError(): Boolean

    companion object {
        // Kotlin 1.9+ 推荐：类型安全，避免 Class<T> 反射
        inline fun <reified T : Enum<T>> fromCode(code: Int): T? =
            enumValues<T>().firstOrNull { it.code == code }
    }
}

// 安全遍历
HttpStatus.entries.forEach { println("${it.name}: ${it.code}") } // entries 替代 values()
```

### ⚠️ 避坑与最佳实践
| 场景 | 风险 | 正确做法 |
|------|------|----------|
| 枚举中持有可变状态或复杂对象 | 单例全局共享，引发并发污染 | 枚举仅承载不可变属性；状态管理交由密封类 |
| 频繁调用 `values()` / `ordinal` | 数组拷贝开销；序位依赖导致重构脆弱 | 使用 `entries`（Kotlin 1.9+）；避免硬编码序位 |
| ProGuard/R8 混淆后 `valueOf` 崩溃 | 枚举名称/字段被剥离 | 添加规则：`-keepclassmembers enum * { *; }` |

### 🚀 现代演进与工程建议
- **官方立场**：`enum` 仅用于**编译期固定的、无行为的常量集**；若需分支逻辑、携带不同类型数据或未来可能扩展，**必须迁移到 `sealed class/interface`**。
- **Kotlin 1.9+ 改进**：`enumValues<T>()` 和 `enumEntries<T>()` 替代反射 API，编译期类型推导更精准，零运行时反射开销。
- **性能对比**：
  - `enum`：单例数组缓存，访问 `O(1)`，但内存固定分配
  - `sealed`：按需实例化，支持泛型与携带任意数据，`when` 穷举检查
  - `value class`：零运行时对象，适合单值强类型（如 `enum class Unit(val symbol: String)` → `@JvmInline value class Unit(val symbol: String)`）

### 🧩 典型场景代码（路由权限）
```kotlin
enum class RoutePermission(val path: String, val requiredRole: String) {
    DASHBOARD("/dashboard", "USER"),
    ADMIN("/admin/**", "ADMIN");

    fun matches(requestPath: String): Boolean = 
        if (path.endsWith("**")) requestPath.startsWith(path.dropLast(2))
        else path == requestPath
}
// 行为简单、固定、无状态 → 完美契合 enum
```

---

## 内联类 / 值类（Value Class）

### 🔍 核心原理
值类是 Kotlin 提供的**编译期类型安全包装器**。编译器会在所有使用处**直接内联底层类型**，运行时不生成额外对象实例（零分配开销）。其核心目标是解决“用 `Int`/`String` 裸传导致的语义混淆”，提供领域驱动设计（DDD）中的**强类型标识**。

```kotlin
// 源码
@JvmInline value class UserId(val value: Long)
val id = UserId(123L)
println(id) // 编译期替换为: System.out.println(123L)
```

### 💻 语法与特性演示
```kotlin
// ✅ 基本声明（仅允许一个主构造 val）
@JvmInline value class Currency(val amount: BigDecimal) {
    // 支持扩展属性、方法、接口实现
    val isPositive: Boolean get() = amount > BigDecimal.ZERO
    fun add(other: Currency) = Currency(amount + other.amount)
}

// ✅ 实现接口
interface Loggable { fun log() }
@JvmInline value class SecureToken(val token: String) : Loggable {
    override fun log() = println(token.take(4) + "****") // 脱敏日志
}

// ❌ 非法用法
// @JvmInline value class Invalid(val a: Int, val b: String) // 多字段不支持（Kotlin 2.1+ 实验性开放）
// @JvmInline value class Bad(val value: Int = 0)             // 不支持默认值
```

### ⚠️ 避坑与最佳实践
| 场景 | 风险 | 正确做法 |
|------|------|----------|
| 作为泛型实参传入 Java API | 类型擦除导致接收 `Object` 或编译警告 | Java 侧需声明 `@JvmInline` 参数，或使用原始类型 |
| 反射操作（KClass/`javaClass`） | 自动拆箱为底层类型，丢失包装语义 | 避免反射；若必须，使用 `::class` 获取包装类元数据 |
| 数组/集合大量存储 | 早期版本未优化数组装箱，Kotlin 2.0+ 已修复 | 升级至 2.0+；避免在热点路径频繁 `toArray()` |
| 嵌套过深或包含可变状态 | 破坏不可变语义，内联失败 | 仅包装不可变基础类型/对象；保持轻量 |

### 🚀 现代演进与工程建议
- **Kotlin 1.5**：从 `inline class` 重命名为 `@JvmInline value class`，语义更清晰。
- **Kotlin 2.0**：
  - 数组存储零装箱优化（`Array<ValueClass>` 直接编译为底层类型数组）
  - 与 Java 互操作警告更明确（`@JvmInline` 强制标注）
  - 编译器对 `when`、`equals`、`hashCode` 生成更紧凑字节码
- **Kotlin 2.1+ 实验性**：开放多字段值类（`value class` with multiple properties），底层按固定偏移量布局，接近 C/C++ `struct` 性能。
- **架构定位**：
  - `data class` → 承载多字段业务实体
  - `value class` → 强类型单值标识（ID、金额、密钥、单位）
  - `enum` → 固定常量集
  - `sealed` → 行为/状态分支

### 🧩 典型场景代码（领域强类型）
```kotlin
@JvmInline value class UserId(val value: Long)
@JvmInline value class OrderId(val value: String)

// 编译期拦截错误传参
fun fetchOrder(userId: UserId, orderId: OrderId): Order { ... }

// ✅ 安全
fetchOrder(UserId(1L), OrderId("ORD-999"))
// ❌ 编译错误：Type mismatch. Required: UserId. Found: Long.
fetchOrder(1L, OrderId("ORD-999"))
```

---

### 🧩 三者对比与选型决策树

| 维度 | 嵌套类（Nested） | 枚举类（Enum） | 值类（Value Class） |
|------|------------------|----------------|---------------------|
| **运行时开销** | `inner` 有引用开销；默认静态零开销 | 静态单例数组，固定内存 | **零对象分配**（内联替换） |
| **类型安全** | 普通类继承体系 | 固定实例集，`entries` 遍历安全 | 编译期强类型隔离，防误传 |
| **扩展性** | 可继承、多态 | ❌ 不可扩展 | 仅包装单值，行为有限 |
| **适用场景** | Builder、协议解析、局部状态封装 | 状态码、路由、配置键、权限 | ID、金额、单位、安全令牌 |
| **替代建议** | `companion object` / 顶层函数 | `sealed interface`（需行为/扩展） | `data class`（多字段时） |

> 💡 **核心心法**：  
> - 需要**隔离作用域** → 嵌套类（默认不加 `inner`）  
> - 需要**固定常量集** → 枚举类（行为简单时用 `enum`，复杂时切 `sealed`）  
> - 需要**防误传强类型** → 值类（`@JvmInline value class`，零开销语义隔离）  
> 
> 现代 Kotlin 工程应避免“为封装而封装”。优先使用顶层函数、扩展、上下文接收器与不可变数据流，将嵌套/枚举/值类作为**领域边界显式化**的工具，而非万能结构。

这份大纲已经非常精准地概括了 Kotlin 三大高级特性的核心。下面我将基于你的结构，**逐层展开底层原理、代码实战、陷阱规避与现代 Kotlin（1.9+/2.0）演进细节**，帮助你从“知道语法”跃迁到“工程级掌控”。

---
## 类委托（Class Delegation）

### 🔍 核心概念
类委托是 Kotlin 对 **组合优于继承（Composition over Inheritance）** 原则的语法级支持。通过 `by` 关键字，编译器会在编译期自动生成接口方法的转发代码，使你无需手动编写大量样板代码，即可获得“组合的灵活性 + 接口的多态性”。

### 📝 语法与底层特性
```kotlin
// 1. 基础语法：只能委托给接口（不能是抽象类或具体类）
interface Printer {
    fun print(msg: String)
    fun scan(): Boolean
}

class RealPrinter : Printer {
    override fun print(msg: String) = println("Printing: $msg")
    override fun scan() = true
}

// 编译器自动生成：所有 Printer 方法转发给 printer
class DelegatedPrinter(private val printer: Printer) : Printer by printer
```

**关键特性：**
- **选择性重写**：可显式覆盖特定方法，其余自动转发
  ```kotlin
  class LoggingPrinter(printer: Printer) : Printer by printer {
      override fun print(msg: String) {
          println("[LOG] Before print")
          printer.print(msg) // 显式调用原始实现
          println("[LOG] After print")
      }
      // scan() 自动委托，无需重写
  }
  ```
- **零运行时开销**：Kotlin 编译器直接生成 Java 风格的转发方法，**不使用反射或动态代理**，性能与手写委托完全一致。
- **支持属性委托目标**：Kotlin 1.4+ 起，`by` 右侧可以是 `val/var` 属性（支持热替换/懒初始化代理对象）。

### 🛠 最佳实践
| 场景 | 推荐做法 |
|------|----------|
| 替代多层继承 | 用接口+委托拆分职责，避免 `class A extends B extends C` |
| 装饰器模式 | 委托基类 + 选择性重写增强逻辑（日志、缓存、重试） |
| 接口稳定性 | 委托的接口应保持稳定；若接口频繁变更，委托类需同步维护 |
| 测试 Mock | 编译期委托比 Mockito 更安全（无运行时反射风险，支持 final 类） |

### ⚠️ 注意事项与现代演进
- **不支持部分接口委托**：必须委托整个接口。若只需部分方法，应拆分接口或使用适配器。
- **可见性冲突**：重写的方法**不能降低**原接口的可见性（如接口 `fun foo()` 是 public，重写不能改 protected）。
- **Kotlin 2.0 优化**：K2 编译器对委托链的泛型推断更精准，修复了早期版本中泛型委托类型擦除导致的编译错误；IDE 已支持“一键展开委托方法”查看生成代码。
- **典型陷阱**：委托对象本身持有可变状态时，多线程下可能产生竞态。建议委托对象保持无状态或内部线程安全。

---
## 属性委托（Property Delegation）

### 🔍 核心概念
属性委托将属性的 `get()`/`set()` 逻辑抽离到独立对象中，基于 **操作符约定（Operator Convention）**：
```kotlin
class Delegate {
    operator fun getValue(thisRef: Any?, property: KProperty<*>): T
    operator fun setValue(thisRef: Any?, property: KProperty<*>, value: T)
}
```
Kotlin 编译器在访问委托属性时，会自动转换为对 `getValue`/`setValue` 的调用。

### 📝 标准委托与自定义实现
#### ✅ 标准库委托
| 委托 | 语义 | 适用场景 |
|------|------|----------|
| `lazy { ... }` | 首次访问时初始化，之后缓存 | 耗时对象、DB连接、配置解析 |
| `Delegates.observable(initial) { prop, old, new -> }` | 赋值后触发回调 | UI 状态同步、日志埋点 |
| `Delegates.vetoable(initial) { prop, old, new -> Boolean }` | 赋值前拦截，返回 `false` 则拒绝赋值 | 参数校验、业务规则拦截 |
| `Delegates.notNull()` | 允许延迟赋值，未赋值前访问抛异常 | 替代 `lateinit` 的泛型安全场景 |
| `Map` / `MutableMap` 委托 | 以属性名作为 key 存取 Map | JSON 解析、SharedPreferences 封装 |

```kotlin
// lazy 线程模式选择
val db by lazy(LazyThreadSafetyMode.SYNCHRONIZED) { connectDatabase() } // 默认，线程安全
val uiConfig by lazy(LazyThreadSafetyMode.NONE) { loadConfig() }        // 单线程环境更高效

// vetoable 拦截示例
var age by Delegates.vetoable(0) { _, old, new ->
    new in 0..120 // 返回 false 则拒绝赋值
}
```

#### 🧩 自定义委托（泛型支持）
```kotlin
class SharedPrefDelegate<T>(private val key: String, private val default: T) {
    operator fun getValue(thisRef: Any?, property: KProperty<*>): T {
        val prefs = getPreferences()
        @Suppress("UNCHECKED_CAST")
        return when (default) {
            is String -> prefs.getString(key, default) as T
            is Int -> prefs.getInt(key, default) as T
            else -> default
        }
    }
    operator fun setValue(thisRef: Any?, property: KProperty<*>, value: T) {
        getPreferences().edit().apply {
            when (value) {
                is String -> putString(key, value)
                is Int -> putInt(key, value)
            }.apply()
        }
    }
}

// 使用
var userName by SharedPrefDelegate("name", "")
```

### 🛠 最佳实践
- **优先使用标准委托**，避免重复造轮子。
- **委托对象应保持轻量/无状态**，避免在 `getValue`/`setValue` 中持有 `Context`、`Activity` 等强引用导致内存泄漏。
- `lazy` 的线程安全模式按需选择：`NONE` 性能最高，`SYNCHRONIZED` 最安全，`PUBLICATION` 允许多次初始化但只取第一次结果（适用于无副作用初始化）。
- 自定义委托若用于 Android，建议结合 `Lifecycle` 或 `CoroutineScope` 管理生命周期。

### ⚠️ 注意事项与现代演进
- `lateinit` vs `lazy`：
  | 特性 | `lateinit var` | `val by lazy` |
  |------|----------------|---------------|
  | 可变性 | `var`（可重复赋值） | `val`（仅初始化一次） |
  | 初始化时机 | 任意时机手动赋值 | 首次访问时自动执行 lambda |
  | 类型支持 | 不支持基本类型（Int/Boolean等） | 支持所有类型 |
  | 反射检查 | `::prop.isInitialized` | 无内置 API（需自定义） |
- **Kotlin 2.0 演进**：K2 编译器大幅改进委托属性的泛型类型推断，解决了早期版本中复杂泛型委托编译失败的问题；IDE 对委托属性的导航、重构支持更完善。
- **JVM 字段生成**：委托属性在字节码中仍会生成 backing field，但访问全部走委托逻辑。若需直接暴露字段给 Java，需加 `@JvmField`（此时委托失效）。

---
## 类型别名（Type Aliases）

### 🔍 核心概念
`typealias` 是**纯编译期特性**，仅为现有类型提供更具业务语义的名称，**不创建新类型，零运行时开销**。编译后完全替换为原始类型，Java 端完全感知不到别名存在。

### 📝 语法与特性
```kotlin
// 基础别名
typealias UserId = Long
typealias PasswordHash = String

// 函数类型别名（极大简化高阶函数签名）
typealias OnUserClick = (User, Boolean) -> Unit
typealias AsyncResult<T> = suspend () -> Result<T>

// 泛型与复杂嵌套简化
typealias UserConfig = Map<String, List<Pair<Int, String>>>
typealias Callback<T> = (Result<T>) -> Unit
```

### 🛠 最佳实践
| 场景 | 推荐做法 |
|------|----------|
| 高阶函数签名 | 将 `(T) -> Unit` 命名为 `OnEvent<T>`，提升可读性 |
| 领域术语统一 | `typealias Email = String` 配合 KDoc 约定校验规则 |
| API 过渡期兼容 | 旧别名标记 `@Deprecated` + `@ReplaceWith` 平滑迁移 |
| 避免滥用 | 别名不应改变类型语义；若需类型安全隔离，改用 `@JvmInline value class` |

### ⚠️ 注意事项与现代演进
- **不是新类型**：`typealias A = Long` 与 `Long` 完全等价，编译器不会做类型隔离。若需零成本封装+类型安全，使用 `@JvmInline value class UserId(val value: Long)`。
- **Java 互操作**：Java 代码中只能看到原始类型，别名仅存在于 Kotlin 源码层。
- **可见性与修饰符**：别名不能独立声明访问控制符（继承原类型可见性），不能加 `final`/`open` 等。
- **Kotlin 2.0 支持**：全面支持 `@Deprecated(message = "...", replaceWith = ReplaceWith("NewAlias"))` 实现自动化迁移提示；IDE 已支持别名自动折叠/展开，重构时自动同步所有引用。
- **典型陷阱**：过度使用别名会导致“别名地狱”（如 `typealias A = B`, `B = C`），降低代码可维护性。建议遵循“一个业务概念一个别名”原则。

---
### 总结与选型建议

| 特性 | 核心目的 | 运行时开销 | 适用场景 | 替代方案 |
|------|----------|------------|----------|----------|
| **类委托** | 组合实现多态，避免继承爆炸 | 零（编译器生成转发） | 装饰器、代理、Mock、缓存拦截 | Java 手动转发 / 动态代理（有性能损耗） |
| **属性委托** | 解耦属性访问逻辑 | 极低（方法调用） | 懒加载、配置监听、DI、数据绑定 | 手写 getter/setter / 注解处理器 |
| **类型别名** | 提升可读性，简化复杂签名 | 零（纯编译期） | 高阶函数、领域词汇、API 迁移 | 无直接替代（`value class` 用于类型安全封装） |

### 💡 工程级建议
1. **类委托优先于抽象类继承**：接口+委托更灵活，且天然支持多态组合。
2. **属性委托注意生命周期**：在 Android/Compose 中，委托对象应随作用域销毁，避免隐式持有 Context。
3. **类型别名 vs value class**：
   - 仅求可读性 → `typealias`
   - 需类型安全+零成本 → `@JvmInline value class`
   - 需运行时实例化 → `data class`
---


# 函数与函数式编程

## 1. 函数基础

在 Kotlin 中，函数是一等公民（First-class citizens），但首先我们需要掌握其基本声明和调用方式。Kotlin 的设计哲学是“减少样板代码”，因此在函数定义上提供了许多便利特性。

### 函数声明与调用

#### `fun` 关键字与返回类型推导
Kotlin 使用 `fun` 关键字声明函数。如果函数体包含多个语句或显式返回，通常建议指定返回类型；但如果编译器可以明确推断出返回类型，则可以省略。

```kotlin
// 显式指定返回类型
fun sum(a: Int, b: Int): Int {
    return a + b
}

// 返回类型推导：编译器知道 a + b 是 Int
fun multiply(a: Int, b: Int) = a * b 
// 注意：这种单表达式写法通常配合下面的“单表达式函数”使用
```

> **最佳实践**：对于公共 API 或复杂逻辑，建议始终显式声明返回类型以提高可读性；对于私有辅助函数或简单的计算，可以利用类型推导。

#### 单表达式函数 (Single-expression functions)
当函数体只包含一个表达式时，可以省略花括号 `{}` 和 `return` 关键字，直接使用 `=` 赋值。

```kotlin
fun double(x: Int): Int = x * 2

// 结合类型推导
fun triple(x: Int) = x * 3
```

这种写法不仅简洁，而且强制函数保持纯粹（无副作用），非常适合数学计算或数据转换。

#### 默认参数与命名参数 (Named Arguments)
Kotlin 允许在函数声明中为参数指定默认值。这消除了 Java 中常见的重载函数（Overloading）需求。

```kotlin
fun read(b: Array<Byte>, off: Int = 0, len: Int = b.size) {
    // ...
}

// 调用方式
read(myArray)           // off=0, len=myArray.size
read(myArray, off = 1)  // off=1, len=myArray.size
read(myArray, len = 5)  // off=0, len=5
```

**命名参数**使得调用代码更具自文档性，特别是在参数较多或类型相同容易混淆时（如 `String, String`）。

#### 变长参数 (Varargs)
使用 `vararg` 修饰符允许传递可变数量的参数。在函数内部，这些参数被视为一个数组。

```kotlin
fun printAll(vararg messages: String) {
    for (m in messages) println(m)
}

printAll("Hello", "World", "!")

// 如果已经有一个数组，可以使用展开操作符 * 传入
val args = arrayOf("A", "B")
printAll(*args) 
```

### 函数作用域与嵌套

#### 局部函数 (Local Functions)
Kotlin 支持在函数内部定义函数。局部函数可以访问外部函数的局部变量（即形成闭包），这有助于将大函数拆解为逻辑小块，同时避免污染外部命名空间。

```kotlin
fun dfs(graph: Graph) {
    val visited = HashSet<Vertex>()
    
    // 局部函数，可以直接访问 visited 和 graph
    fun dfs(current: Vertex) {
        if (!visited.add(current)) return
        for (v in current.neighbors)
            dfs(v)
    }

    dfs(graph.vertices[0])
}
```

#### 成员函数与扩展函数初步
*   **成员函数**：定义在类或对象内部的函数。
*   **扩展函数**：定义在类外，但能像成员函数一样被调用的函数。它不会修改类的源码，而是通过静态解析实现。

```kotlin
class User(val name: String)

// 成员函数
fun User.greet() = println("Hi, I'm $name")

// 扩展函数 (在文件顶层定义)
fun String.removeSpaces(): String = this.replace(" ", "")

// 调用
val u = User("Alice")
u.greet()
"Hello World".removeSpaces() // "HelloWorld"
```

### 尾递归优化

递归是函数式编程的核心，但深层递归可能导致栈溢出（StackOverflowError）。如果递归调用是函数执行的**最后一步操作**，Kotlin 编译器可以将其优化为循环。

使用 `tailrec` 修饰符标记此类函数：

```kotlin
tailrec fun findFixPoint(x: Double = 1.0): Double =
    if (x == Math.cos(x)) x else findFixPoint(Math.cos(x))
```

**限制条件**：
1. 递归调用必须是函数体中的最后一个操作。
2. 不能在 `try-catch-finally` 块中进行尾递归调用。
3. 目前仅支持 JVM 和 Native 后端，JS 后端不支持此优化。

---

## 2. Lambda 表达式与高阶函数

Kotlin 对函数式编程的支持主要体现在 Lambda 表达式和高阶函数上。这使得代码更加声明式（Declarative）而非命令式（Imperative）。

### Lambda 基础语法

Lambda 表达式本质上是一个匿名函数块，可以作为参数传递或立即执行。

#### Lambda 表达式的结构
完整语法：`{ 参数列表 -> 函数体 }`

```kotlin
// 完整写法
val sum = { x: Int, y: Int -> x + y }

// 调用
println(sum(1, 2)) // 3
```

#### `it`：单参数的隐式名称
如果 Lambda 只有一个参数，且编译器可以推断出其类型，则可以省略参数声明，并使用默认名称 `it`。这在集合操作中极为常见。

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)

// 完整写法
numbers.filter({ item -> item > 2 })

// 简化写法 (使用 it)
numbers.filter({ it > 2 })

// 进一步简化：如果 Lambda 是最后一个参数，可以移到括号外
numbers.filter { it > 2 } 
```

#### 匿名函数 (Anonymous Functions) vs Lambda
有时你需要显式指定返回类型，或者需要从 Lambda 中非局部返回（见内联函数章节），此时可以使用匿名函数。

```kotlin
// Lambda
val lambda = { x: Int -> x * 2 }

// 匿名函数
val anonFun = fun(x: Int): Int { return x * 2 }

// 区别：匿名函数中 return 只从匿名函数返回，而 Lambda 中的 return 默认从外围函数返回（非局部返回）
```

### 高阶函数 (Higher-Order Functions)

高阶函数是指**接受函数作为参数**或**返回函数**的函数。

#### 函数类型表示法
Kotlin 使用特殊的语法表示函数类型：`(参数类型) -> 返回类型`。

```kotlin
// 定义一个高阶函数，接收一个函数作为参数
fun operate(a: Int, b: Int, operation: (Int, Int) -> Int): Int {
    return operation(a, b)
}

// 调用
val result = operate(10, 5) { x, y -> x + y } // 15
val product = operate(10, 5) { x, y -> x * y } // 50
```

#### 函数作为返回值
函数也可以返回另一个函数，常用于工厂模式或策略模式。

```kotlin
fun createMultiplier(factor: Int): (Int) -> Int {
    return { x -> x * factor }
}

val double = createMultiplier(2)
println(double(5)) // 10
```

### 闭包 (Closures)

Lambda 或匿名函数可以访问其定义所在作用域中的变量，即使这些变量是在外部定义的。这种现象称为**闭包**。

#### 捕获外部变量
Lambda 可以捕获并修改外部变量的值（前提是变量是可变的 `var`）。

```kotlin
var sum = 0
listOf(1, 2, 3).forEach {
    sum += it // 捕获并修改外部变量 sum
}
println(sum) // 6
```

#### 变量修改与线程安全注意事项
*   **JVM 平台**：如果 Lambda 被存储并在不同线程中执行，或者被序列化，捕获的变量可能会引发并发问题。
*   **不可变性推荐**：尽量捕获 `val`（不可变引用）。如果必须捕获 `var`，请确保访问同步，或使用原子类（如 `AtomicInteger`）。
*   **内存泄漏**：在 Android 或长生命周期对象中，如果 Lambda 捕获了 Activity 或 View 的引用，可能会导致内存泄漏。建议使用弱引用或确保 Lambda 的生命周期短于被捕获对象。
以下是针对 **Kotlin 内联函数** 和 **扩展与操作符** 部分的详细讲解。这两部分内容是 Kotlin 实现高效 DSL（领域特定语言）和简洁语法糖的核心机制。

---

## 3. 内联函数 (Inline Functions)

在 JVM 上，Lambda 表达式通常会被编译成匿名内部类对象。如果频繁调用高阶函数（如集合的 `map`, `filter`），会创建大量临时对象，导致内存分配和垃圾回收（GC）的压力。**内联函数**是 Kotlin 解决这一性能问题的关键手段，同时也赋予了 Lambda 特殊的控制流能力。

### 内联机制原理

#### 消除 Lambda 对象创建开销
当使用 `inline` 修饰符标记一个函数时，编译器不会生成该函数的常规调用指令，而是将**函数体代码直接复制（嵌入）**到每一个调用处。同时，传入的 Lambda 表达式代码也会被直接嵌入，而不是创建一个包含 Lambda 逻辑的对象。

**示例对比：**

```kotlin
// 非内联高阶函数
fun locked(lock: Lock, body: () -> Unit) {
    lock.lock()
    try {
        body()
    } finally {
        lock.unlock()
    }
}

// 内联高阶函数
inline fun inlinedLocked(lock: Lock, body: () -> Unit) {
    lock.lock()
    try {
        body()
    } finally {
        lock.unlock()
    }
}

fun main() {
    val lock = ReentrantLock()
    
    // 非内联调用：创建了一个新的 Runnable/Function0 对象
    locked(lock) { println("Body") }

    // 内联调用：编译器生成的字节码大致等价于：
    // lock.lock()
    // try { println("Body") } finally { lock.unlock() }
    // 没有额外的对象创建，也没有函数调用开销
    inlinedLocked(lock) { println("Body") }
}
```

> **注意**：内联会导致字节码体积增大。因此，只应对那些接收 Lambda 参数且被频繁调用的小函数使用 `inline`。不要内联大型函数。

#### 非局部返回 (Non-local returns)
这是内联函数带来的另一个重要特性。在普通的 Lambda 中，`return` 语句只能从 Lambda 本身返回。但在**内联**函数的 Lambda 中，`return` 可以从**包围该 Lambda 的外层函数**返回。

```kotlin
inline fun forEachInline(list: List<Int>, action: (Int) -> Unit) {
    for (item in list) {
        action(item)
    }
}

fun lookForValue(list: List<Int>) {
    forEachInline(list) {
        if (it == 42) {
            return // 非局部返回：直接从 lookForValue 函数返回，而不是仅从 Lambda 返回
        }
        println(it)
    }
    println("Loop finished") // 如果找到 42，这行代码不会执行
}
```

如果函数不是 `inline` 的，上述代码会编译错误，因为 Lambda 中的 `return` 试图跳出非内联的作用域。

### 内联修饰符详解

#### `inline`：标准内联
如上所述，将整个函数体和所有 Lambda 参数内联。

#### `noinline`：禁止特定参数内联
如果一个内联函数接收多个 Lambda 参数，但你希望其中某个参数**不**被内联（例如，你需要将该 Lambda 存储在变量中、传递给其他非内联函数，或作为回调保留），可以使用 `noinline` 修饰该参数。

```kotlin
inline fun mixedInline(
    inlinedBlock: () -> Unit, 
    noinline storedBlock: () -> Unit
) {
    inlinedBlock() // 被内联
    
    // storedBlock 不能被内联，因为它可能被存储或传递
    val runnable = Runnable { storedBlock() } 
    runnable.run()
}
```

#### `crossinline`：禁止非局部返回
有时，你需要将传入的 Lambda 传递给另一个执行上下文（例如另一个线程、协程或嵌套的非内联 Lambda）。在这种情况下，允许“非局部返回”是不安全的，因为外层函数可能已经执行完毕，而 Lambda 稍后才在另一个线程执行。

使用 `crossinline` 标记参数，表示该 Lambda **可以**被内联，但**禁止**在其中使用非局部返回。

```kotlin
inline fun doSomething(crossinline block: () -> Unit) {
    // 假设我们在另一个线程中执行 block
    thread {
        block() // 合法，因为 block 是 crossinline
    }
}

fun test() {
    doSomething {
        // return // 编译错误！不允许非局部返回，因为 block 可能在 test() 结束后才执行
        println("Running in another thread")
    }
}
```

### 具体化类型参数 (Reified Type Parameters)

在 Java/Kotlin 泛型中，由于**类型擦除（Type Erasure）**，运行时无法获取泛型的具体类型信息（例如，你无法判断 `List<String>` 中的元素是否是 `String`，只能知道它是 `List`）。

`inline` 函数结合 `reified` 关键字可以突破这一限制。因为代码被内联到调用处，编译器在编译时就知道具体的类型，从而可以在运行时保留类型信息。

#### `inline` 与 `reified` 的结合使用

```kotlin
// 普通泛型函数：无法使用 is T 检查
fun <T> checkType(obj: Any) {
    // if (obj is T) ... // 编译错误：Cannot check for instance of erased type
}

// 内联 + reified 函数
inline fun <reified T> checkTypeReified(obj: Any) {
    if (obj is T) {
        println("It is a ${T::class.simpleName}")
    }
}

fun main() {
    checkTypeReified<String>("Hello") // 输出: It is a String
    checkTypeReified<Int>(123)        // 输出: It is a Int
}
```

#### 常见应用场景
1.  **启动 Activity (Android)**:
    ```kotlin
    inline fun <reified T : Activity> Context.startActivity() {
        startActivity(Intent(this, T::class.java))
    }
    // 调用: context.startActivity<MainActivity>()
    ```
2.  **JSON 解析**:
    ```kotlin
    inline fun <reified T> parseJson(json: String): T {
        return Gson().fromJson(json, T::class.java)
    }
    ```

---

## 4. 扩展与操作符

Kotlin 通过扩展函数和操作符重载，极大地增强了代码的可读性和表达力，使其更接近自然语言或数学表达。

### 扩展函数与属性 (Extensions)

扩展允许我们为现有的类（包括第三方库或标准库中的类）添加新功能，而无需继承或使用装饰器模式。

#### 定义扩展函数
扩展函数在语法上像是在类内部定义的，但实际上它是**静态解析**的。

```kotlin
// 为 String 类添加一个扩展函数
fun String.lastChar(): Char = this.get(this.length - 1)

fun main() {
    println("Kotlin".lastChar()) // 'n'
}
```
*   **接收者 (Receiver)**: `String` 是接收者类型。
    *   **Dispatch Receiver**: 调用扩展函数的对象实例（上面的 `"Kotlin"`）。
    *   在函数体内，`this` 指向接收者对象。

#### 扩展属性的 Getter/Setter
你也可以为类添加扩展属性，但它们不能有后台字段（backing field），因此必须显式提供 `get()` 和可选的 `set()`。

```kotlin
val <T> List<T>.lastIndex: Int
    get() = this.size - 1

var StringBuilder.isEmpty: Boolean
    get() = this.length == 0
    set(value) {
        if (value) this.clear()
    }
```

#### Companion Object 扩展
你可以为类的伴生对象（Companion Object）定义扩展。这使得你可以像调用静态方法一样调用扩展函数，但具有扩展的灵活性。

```kotlin
class MyClass {
    companion object {
        // 空伴生对象
    }
}

// 为 MyClass 的伴生对象添加扩展
fun MyClass.Companion.create(): MyClass {
    return MyClass()
}

fun main() {
    // 看起来像静态工厂方法
    val instance = MyClass.create() 
}
```

#### 扩展的作用域解析规则 (Dispatch Receiver vs Extension Receiver)
当扩展函数在另一个类的成员函数中定义，或者当存在同名成员函数时，解析规则如下：

1.  **成员函数优先**：如果类中已存在同名同签名的成员函数，扩展函数将被忽略。
2.  **静态解析**：扩展函数是根据**声明类型**而非**运行时类型**来调用的。

```kotlin
open class View
class Button : View()

fun View.click() = println("View clicked")
fun Button.click() = println("Button clicked")

fun main() {
    val view: View = Button()
    view.click() // 输出: "View clicked" 
    // 因为 view 的声明类型是 View，编译器静态绑定了 View.click()
}
```

### 操作符重载 (Operator Overloading)

Kotlin 允许通过特定的命名约定来重载运算符。这使得自定义类可以支持 `+`, `-`, `*`, `/`, `[]`, `()` 等符号。

#### 约定规范 (Conventions)
要实现操作符重载，只需在类中定义带有 `operator` 修饰符的特定名称函数。

| 表达式 | 翻译成的函数调用 | 说明 |
| :--- | :--- | :--- |
| `a + b` | `a.plus(b)` | 加法 |
| `a - b` | `a.minus(b)` | 减法 |
| `a * b` | `a.times(b)` | 乘法 |
| `a / b` | `a.div(b)` | 除法 |
| `a % b` | `a.rem(b)` | 取模 |
| `a++` | `a.inc()` | 自增 |
| `a--` | `a.dec()` | 自减 |
| `+a` | `a.unaryPlus()` |  unary plus |
| `-a` | `a.unaryMinus()` | 取负 |
| `!a` | `a.not()` | 逻辑非 |
| `a == b` | `a?.equals(b) ?: (b === null)` | 相等性 |
| `a > b` | `a.compareTo(b) > 0` | 比较 |
| `a[i]` | `a.get(i)` | 获取元素 |
| `a[i] = b` | `a.set(i, b)` | 设置元素 |
| `a(i)` | `a.invoke(i)` | 调用操作符 |
| `a..b` | `a.rangeTo(b)` | 范围创建 |

**示例：实现一个简单的货币类**

```kotlin
data class Money(val amount: Double, val currency: String) {
    operator fun plus(other: Money): Money {
        require(this.currency == other.currency) { "Currencies must match" }
        return Money(this.amount + other.amount, this.currency)
    }

    operator fun times(factor: Int): Money {
        return Money(this.amount * factor, this.currency)
    }
    
    override fun toString(): String {
        return "$amount $currency"
    }
}

fun main() {
    val fiveDollars = Money(5.0, "USD")
    val tenDollars = Money(10.0, "USD")
    
    println(fiveDollars + tenDollars) // 15.0 USD
    println(fiveDollars * 3)          // 15.0 USD
}
```

#### 中缀调用 (Infix Notation)
对于只有一个参数的函数，可以使用 `infix` 关键字，允许使用中缀语法调用（省略点号和括号）。这常用于构建 DSL。

```kotlin
class MapEntry<K, V>(val key: K, val value: V)

infix fun <K, V> K.to(that: V): MapEntry<K, V> {
    return MapEntry(this, that)
}

fun main() {
    // 标准调用
    val entry1 = "key".to("value")
    
    // 中缀调用 (更自然)
    val entry2 = "name" to "Alice"
    
    // 用于初始化 Map
    val map = mapOf("key1" to 1, "key2" to 2)
}
```

#### 解构声明 (Destructuring Declarations) 与 `componentN()`

解构声明允许将一个对象分解为多个变量。这在处理数据类或返回多个值的函数时非常有用。

**原理**：
编译器会将解构声明转换为对 `component1()`, `component2()`, ..., `componentN()` 函数的调用。这些函数必须标记为 `operator`。

```kotlin
data class User(val name: String, val age: Int)

fun main() {
    val user = User("Alice", 30)
    
    // 解构声明
    val (name, age) = user
    
    // 等价于：
    // val name = user.component1()
    // val age = user.component2()
    
    println("$name is $age years old")
}
```

**自定义解构**：
即使是非数据类，也可以通过定义 `componentN` 函数来支持解构。

```kotlin
class Point(val x: Int, val y: Int) {
    operator fun component1() = x
    operator fun component2() = y
}

fun main() {
    val p = Point(10, 20)
    val (x, y) = p
    println("x=$x, y=$y")
}
```

**忽略某些值**：
如果不需要所有组件，可以使用下划线 `_` 忽略。

```kotlin
val (_, age) = user // 只获取 age
```

---

## 5. 函数引用与组合

在 Kotlin 中，函数是一等公民，这意味着你可以像处理变量一样处理函数：将它们赋值给变量、作为参数传递或从其他函数返回。**函数引用**是实现这一点的语法糖，而**函数组合**则是利用高阶函数构建复杂逻辑的手段。

### 函数引用 (Function References)

当你需要将一个现有的函数传递给高阶函数时，可以使用双冒号 `::` 操作符创建函数引用。

#### `::functionName` 语法
如果编译器可以推断出上下文中的函数类型，你可以直接使用 `::` 引用顶层函数、成员函数或扩展函数。

```kotlin
fun isOdd(x: Int) = x % 2 != 0

fun main() {
    val numbers = listOf(1, 2, 3, 4, 5)
    
    // 使用 Lambda
    // numbers.filter { isOdd(it) }
    
    // 使用函数引用 (更简洁，意图更清晰)
    val odds = numbers.filter(::isOdd)
    println(odds) // [1, 3, 5]
}
```

#### 绑定引用 vs 未绑定引用

*   **绑定引用 (Bound Reference)**：引用特定实例的方法。此时，接收者对象已经确定，函数类型不再包含接收者参数。
    ```kotlin
    class Person(val name: String) {
        fun greet() = println("Hello, $name")
    }

    val alice = Person("Alice")
    val action: () -> Unit = alice::greet // 绑定到 alice 实例
    action() // 输出: Hello, Alice
    ```

*   **未绑定引用 (Unbound Reference)**：引用类的方法，但未指定实例。函数类型的第一个参数将是接收者对象。
    ```kotlin
    val action2: (Person) -> Unit = Person::greet // 未绑定
    val bob = Person("Bob")
    action2(bob) // 输出: Hello, Bob
    ```

#### 属性引用 `::property`
不仅可以引用函数，还可以引用属性。属性引用被视为无参函数，返回属性的值。如果是 `var`，还可以获取 setter 引用。

```kotlin
val x = 10
fun main() {
    // 引用顶层属性
    println(::x.get()) // 10

    // 引用成员属性
    data class Point(val x: Int, val y: Int)
    val p = Point(3, 4)
    
    // 获取 x 属性的值
    val getX = Point::x
    println(getX(p)) // 3
    
    // 在集合操作中非常有用
    val points = listOf(Point(1, 2), Point(3, 4))
    val xCoords = points.map(Point::x) // [1, 3]
}
```

### 函数组合与柯里化

虽然 Kotlin 标准库没有直接提供类似 Haskell 的 `(.)` 组合运算符，但我们可以轻松实现函数组合和部分应用。

#### 部分应用 (Partial Application)
部分应用是指固定函数的某些参数，生成一个新的、参数更少的函数。

```kotlin
// 原始函数
fun multiply(a: Int, b: Int): Int = a * b

// 部分应用：固定第一个参数为 2
val double: (Int) -> Int = { b -> multiply(2, b) }

// 或者使用通用辅助函数
fun <P1, P2, R> partial(f: (P1, P2) -> R, p1: P1): (P2) -> R {
    return { p2 -> f(p1, p2) }
}

val triple = partial(::multiply, 3)
println(triple(5)) // 15
```

#### 函数链式调用设计
通过扩展函数和高阶函数，可以设计出流畅的 API。例如，标准库中的 `let`, `apply`, `run` 本质上就是函数组合的工具，允许你将操作串联起来。

```kotlin
// 自定义组合示例
infix fun <A, B, C> ((A) -> B).then(g: (B) -> C): (A) -> C {
    return { a -> g(this(a)) }
}

fun addOne(x: Int) = x + 1
fun square(x: Int) = x * x

fun main() {
    val addOneThenSquare = ::addOne then ::square
    println(addOneThenSquare(3)) // (3+1)^2 = 16
}
```

---

## 6. 构建器模式与 DSL (Domain Specific Languages)

Kotlin 的 DSL 能力主要依赖于**带接收者的 Lambda (Lambdas with Receivers)**。这种机制允许你在 Lambda 内部直接调用接收者对象的方法，仿佛你就在该对象的上下文中一样。这是 Gradle Kotlin DSL、Ktor routing、Jetpack Compose UI 等框架的核心基础。

### 带接收者的 Lambda (Lambdas with Receivers)

#### `Type.() -> Unit` 类型解析
普通 Lambda 的类型是 `(Args) -> Result`。
带接收者的 Lambda 类型是 `ReceiverType.(Args) -> Result`。

这意味着该 Lambda 有一个隐式的接收者对象，在 Lambda 体内可以通过 `this` 访问，且可以省略 `this.` 前缀直接调用接收者的成员。

```kotlin
class HTML {
    fun body() { println("<body>") }
}

// 定义一个高阶函数，接收带接收者的 Lambda
fun html(init: HTML.() -> Unit): HTML {
    val html = HTML()
    html.init() // 在 HTML 实例上执行 init
    return html
}

fun main() {
    html {
        // 这里 this 是 HTML 实例
        body() // 直接调用 HTML.body()，无需 html.body()
    }
}
```

#### `this` 在 Lambda 中的隐含指向
在带接收者的 Lambda 中，`this` 指向接收者对象。如果存在歧义（例如局部变量与接收者成员同名），可以使用标签限定 `this@label`。

```kotlin
class Config {
    var url: String = ""
}

fun config(init: Config.() -> Unit) {
    val c = Config()
    c.init()
    println(c.url)
}

fun main() {
    val url = "external"
    config {
        // this.url = "http://kotlinlang.org" 
        url = "http://kotlinlang.org" // 省略 this，优先解析为接收者成员
        // 如果想访问外部变量 url，需使用 label 或不同命名
    }
}
```

### 标准库中的作用域函数对比

Kotlin 标准库提供了五个主要的作用域函数，它们的区别在于：**上下文对象如何引用**（`this` 还是 `it`）以及**返回值是什么**。

| 函数 | 上下文对象引用 | 返回值 | 典型用途 |
| :--- | :--- | :--- | :--- |
| **`let`** | `it` | Lambda 结果 | 空安全检查 (`obj?.let {}`)，变量作用域限制 |
| **`run`** | `this` | Lambda 结果 | 对象配置并计算结果，组合多个操作 |
| **`with`** | `this` | Lambda 结果 | 非扩展函数形式，对同一对象执行多组操作 |
| **`apply`** | `this` | 对象本身 (`this`) | 对象配置/初始化 (Builder 模式)，返回对象以便链式调用 |
| **`also`** | `it` | 对象本身 (`this`) | 副作用操作 (如日志记录)，不干扰链式调用 |

**选型指南：**
1.  如果要**配置对象**并返回该对象：用 `apply`。
2.  如果要**配置对象**并返回**计算结果**：用 `run`。
3.  如果要执行**副作用**（如打印日志）并保持链式调用：用 `also`。
4.  如果要进行**空安全转换**或限制变量作用域：用 `let`。
5.  如果对象不是扩展接收者，但你想在其上下文中执行代码：用 `with`。

```kotlin
data class Person(var name: String, var age: Int)

fun main() {
    // apply: 配置对象，返回对象
    val person = Person("Alice", 30).apply {
        name = "Bob"
        age = 25
    }
    
    // let: 空安全处理
    val length = person.name?.let {
        it.length // it 是 name
    }
    
    // run: 配置并返回结果
    val summary = person.run {
        "$name is $age years old" // this 是 person
    }
}
```

### 类型安全的构建器 (Type-Safe Builders)

构建 DSL 时，我们希望确保用户只能在正确的上下文中调用正确的函数（例如，只能在 `<body>` 中放 `<p>`，不能在 `<p>` 中放 `<body>`）。

#### HTML/XML 风格 DSL 实现原理
通过嵌套的带接收者 Lambda 实现层级结构。

```kotlin
class Tag(val name: String) {
    private val children = mutableListOf<Tag>()
    
    fun <T : Tag> child(tag: T, init: T.() -> Unit): T {
        tag.init()
        children.add(tag)
        return tag
    }
    
    override fun toString(): String {
        return "<$name>${children.joinToString("")}</$name>"
    }
}

class Body : Tag("body")
class Paragraph : Tag("p")

fun body(init: Body.() -> Unit): Body {
    val body = Body()
    body.init()
    return body
}

fun Body.p(init: Paragraph.() -> Unit): Paragraph {
    return child(Paragraph(), init)
}

fun main() {
    val html = body {
        p {
            // 这里只能调用 Paragraph 的成员
        }
        // body { } // 错误！Body 中没有 body() 方法，除非显式定义
    }
    println(html)
}
```

#### 标记接口 (Marker Interfaces) 与 `@DslMarker`
在上述例子中，如果 `Body` 继承自 `Tag`，且 `Tag` 中定义了 `body()`，那么在 `p { ... }` 内部仍然可以调用 `body()`，这可能导致非法的 HTML 嵌套。

为了解决这个问题，Kotlin 引入了 `@DslMarker` 注解。

1.  定义一个标记注解：
    ```kotlin
    @DslMarker
    annotation class HtmlTagMarker
    ```
2.  将该注解应用于 DSL 的基类或接口：
    ```kotlin
    @HtmlTagMarker
    open class Tag(val name: String) { ... }
    
    class Body : Tag("body")
    class Paragraph : Tag("p")
    ```
3.  **效果**：当在某个接收者（如 `Paragraph`）的 Lambda 中时，编译器会隐藏所有带有相同 `@DslMarker` 的外部接收者（如 `Body` 或 `HTML`）的成员，除非显式使用 `this@Body`。这强制了作用域的隔离，防止了意外的嵌套调用。

### 构建器的高级技巧

#### 使用带有构建器类型推断的构建器 (Builder Type Inference)
在 Kotlin 1.8+ 中，引入了 `@BuilderInference` 注解，允许编译器根据 Lambda 内部的使用情况来推断泛型参数，而不是仅仅依赖函数调用的参数类型。这对于复杂的 DSL 非常有用。

```kotlin
// 假设我们有一个通用的容器构建器
class Container<T> {
    private val items = mutableListOf<T>()
    fun item(t: T) { items.add(t) }
}

// 使用 @BuilderInference 让编译器根据 item() 的调用推断 T
inline fun <T> buildContainer(@BuilderInference block: Container<T>.() -> Unit): Container<T> {
    val container = Container<T>()
    container.block()
    return container
}

fun main() {
    // 编译器看到 item("hello")，推断 T 为 String
    val stringContainer = buildContainer {
        item("hello")
        item("world")
    }
    
    // 编译器看到 item(1)，推断 T 为 Int
    val intContainer = buildContainer {
        item(1)
        item(2)
    }
}
```
如果没有 `@BuilderInference`，在某些复杂场景下，编译器可能无法推断出 `T`，要求显式指定 `<String>`。

#### 处理可选节点与列表构建
DSL 经常需要处理重复元素（如多个 `<li>`）或可选元素。

*   **列表构建**：通常通过接收 `List` 或变长参数，或者在接收者中提供 `add` 方法来实现。
    ```kotlin
    fun ul(init: UL.() -> Unit): UL { ... }
    class UL : Tag("ul") {
        fun li(text: String) { child(LI(text)) }
    }
    ```
*   **可选节点**：利用 Kotlin 的空安全和默认参数。
    ```kotlin
    fun div(classes: String? = null, init: DIV.() -> Unit) { ... }
    ```

### 实战案例

#### 配置类 DSL 设计 (Gradle Kotlin DSL 风格)
目标是创建如下风格的配置代码：
```kotlin
server {
    port = 8080
    host = "localhost"
    ssl {
        enabled = true
        certPath = "/path/to/cert"
    }
}
```

**实现思路：**
1.  定义 `ServerConfig` 类，包含 `port`, `host` 属性和 `ssl` 方法。
2.  `ssl` 方法接收 `SslConfig.() -> Unit`。
3.  顶层 `server` 函数接收 `ServerConfig.() -> Unit`。

```kotlin
class SslConfig {
    var enabled: Boolean = false
    var certPath: String = ""
}

class ServerConfig {
    var port: Int = 80
    var host: String = "0.0.0.0"
    private var sslConfig: SslConfig? = null

    fun ssl(block: SslConfig.() -> Unit) {
        sslConfig = SslConfig().apply(block)
    }
    
    fun build() {
        println("Server on $host:$port, SSL: ${sslConfig?.enabled ?: false}")
    }
}

fun server(block: ServerConfig.() -> Unit): ServerConfig {
    return ServerConfig().apply(block)
}

fun main() {
    val config = server {
        port = 8080
        host = "localhost"
        ssl {
            enabled = true
            certPath = "/etc/ssl/cert.pem"
        }
    }
    config.build()
}
```

#### UI 布局 DSL 设计思路 (类似 Jetpack Compose)
现代 UI 框架常使用 DSL 描述界面结构。核心思想是**声明式 UI**：函数调用对应 UI 组件，Lambda 对应子组件。

```kotlin
@Composable
fun Column(content: @Composable () -> Unit) { ... }

@Composable
fun Text(text: String) { ... }

@Composable
fun Button(onClick: () -> Unit, content: @Composable () -> Unit) { ... }

// 使用
Column {
    Text("Hello")
    Button(onClick = { /*...*/ }) {
        Text("Click Me")
    }
}
```
这里的关键是 `@Composable` 注解和编译器插件，它们管理状态重组和 UI 树构建，但语法层面依然依赖于带接收者的 Lambda（或无接收者的 Lambda，视具体设计而定，Compose 中 `Column` 的 lambda 接收者实际上是特殊的 Composer 上下文，但对用户透明）。


# 空安全 (Null Safety)

在 Java 中，`NullPointerException` (NPE) 被称为“十亿美元的错误”。Kotlin 通过区分**可空类型**和**非空类型**，强制开发者在编译期处理 null 值，从而极大地减少了运行时崩溃的风险。

## 1. 可空类型与非空类型

### 类型系统基础

Kotlin 的类型系统明确区分了可以持有 `null` 引用的类型和不能持有 `null` 引用的类型。

*   **非空类型 (`String`)**：
    *   默认情况下，Kotlin 中的所有类型都是非空的。
    *   声明 `val name: String = "Alice"` 后，编译器保证 `name` 永远不会是 `null`。
    *   如果你尝试赋值 `name = null`，编译器会直接报错。

*   **可空类型 (`String?`)**：
    *   通过在类型后添加问号 `?` 来声明可空类型。
    *   声明 `val name: String? = "Alice"` 或 `val name: String? = null` 都是合法的。
    *   这意味着该变量可能包含一个 `String` 对象，也可能是 `null`。

```kotlin
var a: String = "abc"
// a = null // 编译错误：Null can not be a value of a non-null type String

var b: String? = "abc"
b = null // 合法
```

**设计哲学**：Kotlin 选择“默认非空”是因为在大多数业务逻辑中，数据不应该为空。显式标记可空类型迫使开发者思考：“这个字段真的可以为空吗？”如果可以为空，我必须处理它。

### 底层表示与 Java 互操作

在 JVM 字节码层面，Kotlin 的可空类型和非空类型通常都编译为相同的 Java 类型（例如 `java.lang.String`）。区别在于：
1.  **编译期检查**：Kotlin 编译器在生成字节码前进行严格的静态分析。
2.  **注解映射**：当 Kotlin 代码被 Java 调用时，Kotlin 编译器会生成 `@NotNull` 或 `@Nullable` 注解（基于 JSR-305 或 JetBrains 注解），以便 Java 工具（如 IDE 或 FindBugs）能理解空性约束。

### 泛型中的可空性

泛型的可空性需要仔细区分，这是初学者容易混淆的地方：

```kotlin
// 1. 列表本身非空，但元素可能为 null
val list1: List<String?> = listOf("A", null, "B") 

// 2. 列表本身可能为 null，但如果存在，其中的元素必须非空
val list2: List<String>? = null 
// val list2: List<String>? = listOf("A", "B") // 合法

// 3. 列表本身可能为 null，且元素也可能为 null
val list3: List<String?>? = null
```

> **最佳实践**：尽量保持集合本身非空（使用空集合 `emptyList()` 代替 `null`），只让元素可空，这样可以简化调用代码，避免大量的 `?.let` 嵌套。

---

## 2. 空安全检查操作符

为了安全地访问可空类型的成员，Kotlin 提供了一系列操作符。

### 安全调用操作符 (`?.`)

这是最常用的操作符。如果接收者不为 null，则调用方法/属性；如果为 null，则整个表达式返回 null。

```kotlin
val length: Int? = b?.length // 如果 b 是 null，length 也是 null，不会抛出 NPE
```

**链式调用**：
它可以串联使用，只要链条中任何一个环节为 null，结果即为 null。

```kotlin
// Bob?.department?.head?.name
// 如果 Bob 为 null，或者 department 为 null，或者 head 为 null，结果均为 null
val managerName = bob?.department?.head?.name
```

### Elvis 操作符 (`?:`)

Elvis 操作符用于处理“如果为 null，则提供替代值”的逻辑。它的名字来源于其形状像猫王埃尔维斯·普雷斯利的发型。

```kotlin
val l: Int = if (b != null) b.length else -1

// 等价于：
val l: Int = b?.length ?: -1
```

**常见模式**：

1.  **提供默认值**：
    ```kotlin
    val name = user.name ?: "Guest"
    ```

2.  **早期返回 (Early Return)**：
    在函数开头检查必要参数，如果为 null 则直接返回。注意 `return` 是一个表达式，其类型为 `Nothing`，可以与任何类型兼容。
    ```kotlin
    fun process(data: String?) {
        val validData = data ?: return // 如果 data 为 null，函数在此结束
        println(validData.length) // 这里 validData 肯定是非空的
    }
    ```

3.  **抛出异常**：
    ```kotlin
    val value = config.getValue() ?: throw IllegalStateException("Config missing")
    ```

### 非空断言操作符 (`!!`)

`!!` 操作符将任何值转换为非空类型，如果值为 null，则抛出 `KotlinNullPointerException`。

```kotlin
val l = b!!.length // 如果 b 是 null，这里会崩溃
```

**使用场景与警告**：
*   **尽量避免使用**：它违背了空安全的初衷。
*   **何时使用**：
    1.  你拥有比编译器更多的上下文信息（例如，你知道某个回调一定会被调用，或者某个值已在其他地方初始化）。
    2.  用于测试目的，故意触发崩溃以验证错误处理路径。
    3.  在遗留代码重构初期，作为临时手段，随后应逐步替换为更安全的写法。

### 安全转换 (`as?`)

普通的 `as` 转换在失败时会抛出 `ClassCastException`。`as?` 在转换失败时返回 `null`，非常适合与 Elvis 操作符结合使用。

```kotlin
val aInt: Int? = a as? Int

// 结合 Elvis：如果转换失败，使用默认值 0
val value: Int = a as? Int ?: 0
```

---

## 3. 智能转换 (Smart Casts)

Kotlin 编译器非常聪明，它能够跟踪代码逻辑。如果你已经检查过变量是否为 null，那么在随后的代码块中，编译器会自动将该变量视为非空类型，无需手动转换或使用 `?.`。

### 原理

```kotlin
fun getStringLength(obj: Any): Int? {
    if (obj is String) {
        // 在这个分支里，obj 自动被智能转换为 String 类型
        return obj.length // 可以直接访问 String 的属性，无需 (obj as String).length
    }
    
    // 在这里，obj 仍然是 Any 类型
    return null
}
```

对于空检查同样有效：

```kotlin
fun printLength(str: String?) {
    if (str != null) {
        // str 在这里被智能转换为 String
        println(str.length) 
    }
}
```

### 限制条件

智能转换并非在所有情况下都可用，主要受限于**变量的可变性**和**可见性**。

1.  **局部 `val` 变量**：最安全，总是支持智能转换。
2.  **局部 `var` 变量**：
    *   如果在检查和使用的中间，变量没有被修改，支持智能转换。
    *   如果变量可能被**局部函数**或**Lambda**修改，编译器无法保证线程安全或执行顺序，因此**不支持**智能转换。
    ```kotlin
    var x: String? = "Hello"
    
    // 错误：Smart cast to 'String' is impossible, because 'x' is a mutable property 
    // that could have been changed by this time
    if (x != null) {
        someFunctionThatMightChangeX() 
        println(x.length) 
    }
    ```
    *   **解决方法**：将值复制到局部的 `val` 中。
    ```kotlin
    val y = x
    if (y != null) {
        println(y.length) // 安全，y 是不可变的
    }
    ```

3.  **成员属性**：
    *   如果属性是 `open` 的，或者有自定义 getter，编译器无法保证每次访问返回相同的值，因此不支持智能转换。
    *   **解决方法**：同样建议使用局部变量缓存，或使用 `lateinit` / `by lazy` 等委托属性（如果适用）。

### 显式转换 (`as`)

当智能转换不可用时，你可以使用显式转换 `as`。
*   `as`：不安全，失败抛异常。
*   `as?`：安全，失败返回 null。

---

## 4. 平台类型 (Platform Types)

当你从 Java 代码调用 Kotlin，或在 Kotlin 中调用 Java 代码时，会遇到**平台类型**。

### 什么是平台类型？

Java 的类型系统没有内置的空安全概念。虽然 Java 8 引入了 `Optional`，但大多数现有 Java 库仍然使用裸引用。
当 Kotlin 看到来自 Java 的类型（例如 `java.lang.String`）时，它不知道这个引用是否可以为 null。因此，Kotlin 将其表示为**平台类型**，记作 `String!`（注意感叹号，但这只是文档表示，代码中不能直接写 `String!`）。

```kotlin
// 假设这是一个 Java 方法: public String getName() { ... }
val name = javaObject.getName() // name 的类型是 String! (平台类型)
```

对于平台类型：
*   Kotlin 编译器**不执行**空安全检查。
*   你可以把它当作 `String` 使用（可能导致运行时 NPE）。
*   你也可以把它当作 `String?` 使用（需要处理 null）。
*   **责任完全在开发者身上**。

### 处理策略

1.  **显式声明类型**：
    不要依赖类型推断来处理来自 Java 的返回值。显式声明它是可空还是非空，表明你的意图。
    ```kotlin
    // 如果你确定 Java 方法不会返回 null
    val name: String = javaObject.getName() 
    
    // 如果可能返回 null
    val name: String? = javaObject.getName()
    ```

2.  **使用注解辅助**：
    现代 Java 库和 Android SDK 广泛使用注解来标记空性：
    *   `@NotNull` / `@Nonnull`：Kotlin 将其视为非空类型 (`String`)。
    *   `@Nullable` / `@CheckForNull`：Kotlin 将其视为可空类型 (`String?`)。
    
    确保你的项目配置了正确的注解处理器（如 IntelliJ 注解、AndroidX 注解或 JSR-305）。

3.  **Android 开发**：
    Android SDK 的大部分 API 都已经添加了空性注解。在 Android Studio 中，调用 Android API 时，Kotlin 通常能正确推断出可空性。如果遇到未标注的 API，务必查阅文档或源码确认。

---

## 5. 可空集合与数组

处理集合时，需要区分“集合为空”和“集合元素为空”。

### 三种状态

1.  **`List<String>`**：列表本身不为 null，且所有元素都不为 null。
2.  **`List<String?>`**：列表本身不为 null，但内部可能包含 null 元素。
    ```kotlin
    val list: List<String?> = listOf("A", null, "B")
    ```
3.  **`List<String>?`**：列表本身可能为 null。如果列表存在，则其中元素非空。
    ```kotlin
    val list: List<String>? = null
    ```

### 过滤与处理 API

Kotlin 标准库提供了强大的扩展函数来处理可空集合：

*   **`filterNotNull()`**：
    从 `List<T?>` 中移除所有 null 元素，返回 `List<T>`。
    ```kotlin
    val mixed: List<String?> = listOf("A", null, "B", null, "C")
    val nonNull: List<String> = mixed.filterNotNull() // ["A", "B", "C"]
    ```

*   **`mapNotNull()`**：
    先映射，然后过滤掉结果为 null 的元素。这比 `map { ... }.filterNotNull()` 更高效，因为它只遍历一次。
    ```kotlin
    val strings = listOf("1", "abc", "2")
    val numbers: List<Int> = strings.mapNotNull { it.toIntOrNull() } // [1, 2]
    ```

*   **安全访问元素**：
    *   `list.firstOrNull()`：如果列表为空，返回 null 而不是抛异常。
    *   `list.getOrNull(index)`：如果索引越界，返回 null。
    *   `map[key]`：对于 Map，如果 key 不存在，直接返回 null（因为 Map 的 get 操作天然支持可空返回值）。

### 最佳实践总结

1.  **优先使用非空类型**：在定义数据模型时，除非业务逻辑允许，否则不要使用 `?`。
2.  **利用 Elvis 操作符**：简洁地处理默认值和早期返回。
3.  **慎用 `!!`**：把它看作最后的 resort。
4.  **注意平台类型**：在与 Java 互操作时，始终显式声明空性预期。
5.  **善用 `filterNotNull` 和 `mapNotNull`**：优雅地清理数据流中的 null 值。

# 相等性 (Equality)

在 Java 中，`==` 用于基本类型比较值，用于对象比较引用，而 `.equals()` 用于比较对象内容。这种双重标准经常导致混淆。Kotlin 通过引入两个不同的操作符 `==` 和 `===` 来清晰地分离这两种概念。

## 1. 结构相等性 vs 引用相等性

### 结构相等性 (`==`)

**定义**：检查两个对象是否具有相同的**内容**或**值**。

*   **底层机制**：
    `a == b` 在编译时会被转换为 `a?.equals(b) ?: (b === null)`。
    这意味着：
    1.  如果 `a` 不为 null，调用 `a.equals(b)`。
    2.  如果 `a` 为 null，则检查 `b` 是否也为 null（使用引用相等 `===`）。
    
    **关键点**：Kotlin 的 `==` 是**空安全**的。你不需要担心 `null == something` 会抛出 NPE。

*   **示例**：
    ```kotlin
    val name1 = String("Hello") // 创建一个新的 String 对象
    val name2 = String("Hello") // 创建另一个新的 String 对象
    
    println(name1 == name2) // true  (内容相同)
    println(name1 === name2) // false (内存地址不同)
    
    val nullStr: String? = null
    println(nullStr == "Hello") // false (安全，不抛异常)
    ```

### 引用相等性 (`===`)

**定义**：检查两个引用是否指向**内存中的同一个对象实例**。

*   **底层机制**：
    对应 Java 中的 `==` 操作符。它比较的是对象的内存地址（引用）。

*   **基本数据类型的特殊情况**：
    在 Kotlin 中，`Int`, `Double`, `Boolean` 等基本类型在运行时通常被映射为 Java 的基本类型（primitive），除非它们被装箱（例如放在 `List<Int>` 中或声明为 `Int?`）。
    *   对于未装箱的基本类型（如局部变量 `val a: Int = 1`），`===` 和 `==` 效果一样，都比较值。
    *   对于**装箱后**的基本类型（`Int?`），`===` 比较的是引用。这就引入了著名的**整数缓存陷阱**（见下文第 3 部分）。

    ```kotlin
    val a: Int = 100
    val b: Int = 100
    println(a === b) // true (在 JVM 上作为 primitive int 比较，或者命中缓存)
    
    val x: Int? = 1000
    val y: Int? = 1000
    println(x === y) // false (两个不同的 Integer 对象)
    println(x == y)  // true  (值相等)
    ```

> **最佳实践**：在比较业务逻辑数据（字符串、数字、自定义对象）时，**始终使用 `==`**。仅在需要判断是否为同一个实例（如单例、缓存键、链表节点检测）时使用 `===`。

---

## 2. `equals()` 与 `hashCode()` 约定

如果你重写 `equals()`，必须同时重写 `hashCode()`。这是 Java/Kotlin 集合框架（HashMap, HashSet）正常工作的基石。

### 通用契约

1.  **自反性**：`x.equals(x)` 必须返回 `true`。
2.  **对称性**：如果 `x.equals(y)` 为 `true`，则 `y.equals(x)` 也必须为 `true`。
3.  **传递性**：如果 `x.equals(y)` 且 `y.equals(z)`，则 `x.equals(z)` 必须为 `true`。
4.  **一致性**：多次调用 `equals` 应返回相同结果（前提是对象状态未变）。
5.  **HashCode 约束**：如果 `x.equals(y)` 为 `true`，那么 `x.hashCode()` 必须等于 `y.hashCode()`。
    *   *注意*：如果 `hashCode` 相同，`equals` 不一定为 true（哈希碰撞），但如果 `equals` 为 true，`hashCode` 必须相同。

### 数据类 (Data Classes) 的自动生成

Kotlin 的 `data class` 是为了解决这个问题而生的。编译器会自动根据**主构造函数**中声明的所有属性生成 `equals()`, `hashCode()`, `toString()`, `copy()` 和 `componentN()`。

```kotlin
data class User(val id: Int, val name: String)

fun main() {
    val u1 = User(1, "Alice")
    val u2 = User(1, "Alice")
    val u3 = User(1, "Bob")
    
    println(u1 == u2) // true  (自动生成的 equals 比较 id 和 name)
    println(u1 == u3) // false
    println(u1.hashCode() == u2.hashCode()) // true
}
```

**关于排除属性**：
`data class` 默认使用所有主构造参数。如果你想让某个属性不参与相等性比较（例如一个临时计算的字段或数据库版本戳），你有两个选择：
1.  **不使用 data class**：使用普通 `class` 并手动编写 `equals/hashCode`。
2.  **将属性移到 body 中**：只有主构造函数中的属性才会被自动包含。
    ```kotlin
    data class User(val id: Int, val name: String) {
        var lastAccessTime: Long = 0 // 这个属性不参与 equals/hashCode
    }
    ```

**`copy()` 与相等性**：
`copy()` 方法创建的对象，除了被修改的属性外，其他属性与原对象相同。因此，如果只修改了非关键属性，`copy` 后的对象可能与原对象 `equals` 为 true；如果修改了参与 equals 的属性，则为 false。

### 手动重写最佳实践

如果必须手动重写（例如在非 data class 中）：

1.  **使用标准库辅助**：
    Kotlin 提供了 `kotlin.jvm.internal.Intrinsics.areEqual` (内部使用) 或更通用的方式。在 Java 互操作或复杂逻辑中，可以使用 `java.util.Objects.equals(a, b)` 来处理 null。
    
2.  **避免可变状态**：
    **千万不要**在 `equals` 或 `hashCode` 中使用可变属性（`var`）。
    *   **原因**：如果一个对象被放入 `HashSet`，它的 `hashCode` 决定了它在哈希表中的桶位置。如果之后你修改了该对象的一个参与 `hashCode` 计算的属性，它的 `hashCode` 会变，但它在 HashSet 中的位置不会变。当你尝试查找或删除它时，HashSet 会用新的 `hashCode` 去错误的桶里找，导致找不到该对象，造成内存泄漏或逻辑错误。
    *   **建议**：用于相等性比较的属性最好是 `val`（不可变）。

---

## 3. 特殊类型的相等性陷阱

### 浮点数比较 (`Float` / `Double`)

浮点数遵循 IEEE 754 标准，这带来了一些反直觉的行为：

1.  **NaN (Not a Number)**：
    *   `NaN != NaN` 总是成立。
    *   在 Kotlin/Java 中，`Double.NaN == Double.NaN` 返回 `false`。
    *   但是，`listOf(Double.NaN).contains(Double.NaN)` 可能返回 `true`，因为某些集合实现有特殊处理。这非常危险。

2.  **-0.0 与 0.0**：
    *   `-0.0 == 0.0` 返回 `true`。
    *   但是 `-0.0` 和 `0.0` 的位表示不同，某些底层操作可能区分它们。

**建议**：
*   不要直接使用 `==` 比较浮点数是否相等，尤其是经过计算后的结果。
*   使用误差范围（Epsilon）比较：
    ```kotlin
    fun Double.isApproximatelyEqual(other: Double, epsilon: Double = 1e-6): Boolean {
        return kotlin.math.abs(this - other) < epsilon
    }
    ```

### 整数装箱缓存 (Integer Cache)

这是 JVM 的特性，但在 Kotlin 中经常坑到初学者。JVM 为了性能，会缓存 `-128` 到 `127` 之间的 `Integer` 对象。

```kotlin
fun main() {
    // 场景 1: 小整数 (在缓存范围内)
    val a: Int? = 100
    val b: Int? = 100
    println(a === b) // true! 因为它们指向缓存中的同一个对象
    
    // 场景 2: 大整数 (超出缓存范围)
    val c: Int? = 200
    val d: Int? = 200
    println(c === d) // false! 它们是两个不同的 Integer 对象
    
    // 场景 3: 无论大小，值比较永远可靠
    println(a == b) // true
    println(c == d) // true
}
```

**结论**：
*   对于 `Int?`, `Long?`, `Boolean?` 等包装类型，**永远使用 `==`** 进行值比较。
*   **永远不要依赖 `===` 的结果来判断数值相等**，除非你明确知道自己在处理单例或特定的引用身份。

---

## 4. 集合中的相等性

Kotlin 标准库中的集合实现了基于内容的相等性。

### List 相等性
*   **顺序敏感**：两个 List 相等，当且仅当它们大小相同，且对应位置的元素相等（`==`）。
    ```kotlin
    println(listOf(1, 2, 3) == listOf(1, 2, 3)) // true
    println(listOf(1, 2, 3) == listOf(3, 2, 1)) // false
    ```

### Set 相等性
*   **顺序无关**：两个 Set 相等，当且仅当它们包含完全相同的元素。
    ```kotlin
    println(setOf(1, 2, 3) == setOf(3, 2, 1)) // true
    println(setOf(1, 2) == setOf(1, 2, 3))     // false
    ```
*   **依赖 hashCode/equals**：Set 的正确行为强烈依赖于元素的 `hashCode` 和 `equals` 实现。如果自定义对象没有正确重写这两个方法，`Set` 将无法去重或正确判断相等性。

### Map 相等性
*   **键值对集合**：两个 Map 相等，当且仅当它们拥有相同的键集，且每个键对应的值也相等。
*   **顺序无关**：对于 `HashMap`，插入顺序不影响相等性。
    ```kotlin
    val map1 = mapOf("a" to 1, "b" to 2)
    val map2 = mapOf("b" to 2, "a" to 1)
    println(map1 == map2) // true
    ```

---

## 5. 身份识别与唯一性

虽然 `==` 是最常用的，但 `===`（引用相等）在特定场景下不可或缺。

### 何时使用引用相等性 (`===`)

1.  **单例模式检查**：
    确保你拿到的是全局唯一的那个实例。
    ```kotlin
    if (config === AppConfig.INSTANCE) { ... }
    ```

2.  **缓存命中判断 (Identity Map)**：
    有些缓存策略希望区分两个内容相同但不同的对象（例如，跟踪对象的生命周期或变更）。

3.  **检测循环引用**：
    在序列化或遍历图结构时，需要判断当前节点是否就是之前访问过的某个节点（内存地址相同），以防止死循环。
    ```kotlin
    fun traverse(node: Node?, visited: MutableSet<Node> = mutableSetOf()) {
        if (node == null) return
        if (visited.any { it === node }) return // 防止循环
        visited.add(node)
        // ... process children
    }
    ```

4.  **优化性能**：
    在某些高频调用场景下，如果已知两个引用指向同一对象，可以直接跳过昂贵的 `equals` 内容比较。
    ```kotlin
    if (this === other) return true // 快速路径
    if (other !is MyClass) return false
    // 接着进行详细的字段比较
    ```

### `Any` 类中的方法

所有 Kotlin 类都继承自 `Any`（类似于 Java 的 `Object`）。它定义了三个核心方法：

1.  **`equals(other: Any?): Boolean`**：
    *   默认实现是比较引用（`===`）。
    *   数据类和普通类通常会重写它以比较内容。

2.  **`hashCode(): Int`**：
    *   默认实现通常基于内存地址转换而来（具体取决于 JVM 实现）。
    *   重写 `equals` 时必须重写此方法。

3.  **`toString(): String`**：
    *   默认实现是 `ClassName@HexHashCode`。
    *   数据类会自动生成包含属性值的友好字符串表示。

---

### 总结

*   **默认使用 `==`**：它安全、直观，比较的是内容。
*   **谨慎使用 `===`**：仅在关心“是否是同一个对象实例”时使用。
*   **Data Class 是好伙伴**：让它们帮你处理 `equals` 和 `hashCode`，但要记住它们只包含主构造函数的属性。
*   **警惕浮点数和装箱整数**：不要假设 `===` 对数字有效，不要直接用 `==` 比较浮点精度。
*   **集合依赖相等性**：确保放入 `Set` 或 `Map` 键的对象正确实现了 `equals/hashCode`，否则集合行为将不可预测。

# this 表达式

## 1. `this` 的基本概念

在大多数面向对象语言中，`this` 指向当前类的实例。Kotlin 也不例外，但引入了更丰富的上下文概念，称为**接收者 (Receiver)**。

### 当前接收者 (Current Receiver)

`this` 总是指向当前执行上下文中可用的**接收者对象**。

*   **在类成员中**：
    `this` 指向当前类的实例。
    ```kotlin
    class User(val name: String) {
        fun greet() {
            println("Hello, I am ${this.name}") // this 指向 User 实例
        }
    }
    ```

*   **在扩展函数中**：
    `this` 指向**被扩展类型的实例**（即调用该扩展函数的对象）。
    ```kotlin
    fun String.addExclamation(): String {
        return this + "!" // this 指向调用该函数的 String 对象
    }
    
    fun main() {
        println("Hi".addExclamation()) // this 是 "Hi"
    }
    ```

### 隐式 vs 显式使用

*   **隐式使用**：
    在大多数情况下，你可以省略 `this`，直接访问成员。这是 Kotlin 推荐的风格，因为它更简洁。
    ```kotlin
    class Person(val name: String) {
        fun intro() {
            println(name) // 隐式访问 this.name
        }
    }
    ```

*   **显式使用**：
    当存在**名称冲突**（例如局部变量与成员变量同名），或者为了**提高代码可读性**（明确表明正在访问成员而非局部变量）时，必须或建议使用 `this`。
    ```kotlin
    class Counter(var count: Int) {
        fun increment(count: Int) { // 参数名与成员名冲突
            this.count += count // this.count 指成员变量，count 指参数
        }
    }
    ```

---

## 2. 限定符 `this` (Qualified `this`)

当代码嵌套多层作用域（如内部类、匿名对象、Lambda）时，简单的 `this` 可能指向最内层的接收者。如果你需要访问**外层作用域**的 `this`，需要使用**限定符 `this`**。

### 语法结构

```kotlin
this@Label
```
其中 `Label` 是你想要访问的那个类、对象或 Lambda 标签的名称。

### 常见应用场景

#### 内部类 (Inner Classes)
在内部类中，`this` 默认指向内部类实例。若要访问外部类实例，需使用 `this@OuterClassName`。

```kotlin
class Outer {
    val x = 10
    
    inner class Inner {
        val x = 20
        
        fun printX() {
            println(x)          // 20 (Inner 的 x)
            println(this.x)     // 20 (Inner 的 x)
            println(this@Outer.x) // 10 (Outer 的 x)
        }
    }
}
```

#### 匿名对象 (Anonymous Objects)
在匿名对象中，`this` 指向匿名对象本身。若需访问外围类，使用 `this@ClassName`。

```kotlin
class MyActivity {
    fun setupListener() {
        view.setOnClickListener(object : View.OnClickListener {
            override fun onClick(v: View?) {
                // this 指向 OnClickListener 匿名对象
                // this@MyActivity 指向 MyActivity 实例
                this@MyActivity.finish() 
            }
        })
    }
}
```

#### Lambda 表达式
*   **非带接收者的 Lambda**：
    普通 Lambda（如传给 `map`, `filter` 的）没有接收者，因此不能在内部使用 `this` 来引用 Lambda 本身（因为没有“本身”的概念，它只是一个函数块）。如果在 Lambda 内部使用 `this`，它指向的是**外围类**的实例（如果是在类方法中定义的）。
    
*   **带接收者的 Lambda (Lambdas with Receivers)**：
    这是 DSL 的核心。在这种 Lambda 中，`this` 指向 Lambda 的**接收者对象**。如果需要访问外围类的 `this`，同样需要使用限定符。

    ```kotlin
    class HTML {
        fun body() { ... }
    }

    fun html(init: HTML.() -> Unit) {
        val html = HTML()
        html.init()
    }

    class Page {
        fun render() {
            html {
                // this 指向 HTML 实例
                this.body() 
                
                // 如果想访问 Page 的方法，需使用限定符
                // this@Page.someMethod()
            }
        }
    }
    ```

---

## 3. `this` 在扩展函数中的行为

这是 Kotlin 中最容易混淆的部分之一，因为扩展函数涉及两个“接收者”。

### 分发接收者 vs 扩展接收者

假设我们在类 `A` 中为类 `B` 定义了一个扩展函数：

```kotlin
class A {
    val value = "A"
    
    // B 是扩展接收者类型
    fun B.printValues() {
        // ...
    }
}
```

在这个扩展函数 `printValues` 内部：
1.  **扩展接收者 (Extension Receiver)**：类型为 `B` 的实例。这是你调用扩展函数时的对象（`bInstance.printValues()`）。在函数体内，它可以通过 `this` 访问。
2.  **分发接收者 (Dispatch Receiver)**：类型为 `A` 的实例。这是定义扩展函数的类的实例。

### 名称冲突处理

如果 `A` 和 `B` 都有名为 `value` 的属性，会发生什么？

```kotlin
class A {
    val value = "From A"
    
    fun B.print() {
        println(value)       // 输出: "From B" (扩展接收者优先)
        println(this.value)  // 输出: "From B" (同上)
        println(this@A.value) // 输出: "From A" (强制访问分发接收者)
    }
}

class B {
    val value = "From B"
}

fun main() {
    A().run { B().print() }
}
```

**规则总结**：
*   默认情况下，`this` 指向**扩展接收者**（被扩展的类型）。
*   如果要访问**分发接收者**（定义扩展的类）的成员，必须使用 `this@ClassName`。
*   这种设计使得扩展函数可以自然地操作被扩展的对象，同时仍能访问定义类的上下文（如果需要）。

---

## 4. `this` 在 DSL 与高阶函数中的应用

Kotlin 的 DSL 能力很大程度上依赖于对 `this` 上下文的灵活控制。

### 带接收者的 Lambda

在 `Type.() -> Unit` 类型的 Lambda 中，`this` 指向传入的 `Type` 实例。这允许你像在类内部一样直接调用其方法。

```kotlin
fun buildString(builderAction: StringBuilder.() -> Unit): String {
    val sb = StringBuilder()
    sb.builderAction() // 在 sb 上执行 lambda，lambda 内的 this 就是 sb
    return sb.toString()
}

val s = buildString {
    this.append("Hello ") // 显式 this
    append("World")       // 隐式 this
}
```

### 作用域函数中的 `this`

回顾之前学过的作用域函数，它们的区别本质上就是 `this` 和 `it` 的区别：

| 函数 | Lambda 中的 `this` 指向 | Lambda 中的 `it` |
| :--- | :--- | :--- |
| **`apply`** | 上下文对象 (Context Object) | 不可用 |
| **`run`** | 上下文对象 (Context Object) | 不可用 |
| **`with`** | 上下文对象 (Context Object) | 不可用 |
| **`let`** | 外围对象的 `this` (如果有) | 上下文对象 |
| **`also`** | 外围对象的 `this` (如果有) | 上下文对象 |

*   **`apply/run/with`**：适合配置对象，因为你可以直接使用 `this` 访问属性，代码像构建器一样流畅。
*   **`let/also`**：适合转换或副作用，因为上下文对象作为参数 `it` 传入，不会遮蔽外围作用域的 `this`。

### 嵌套作用域的 `this` 解析

在多层嵌套的带接收者 Lambda 中，`this` 始终指向**最内层**的接收者。

```kotlin
html {
    body {
        // this 指向 Body 实例
        div {
            // this 指向 Div 实例
            // 如果想访问 Body 的方法，需用 this@body
            // 如果想访问 HTML 的方法，需用 this@html
        }
    }
}
```

如果层级过深导致混淆，可以使用**标签 (Labels)** 来明确指定：

```kotlin
html@ {
    body@ {
        div {
            // this@body 指向 Body
        }
    }
}
```

---

## 5. 特殊场景与陷阱

### 构造函数中的 `this`

*   **初始化块 (`init`)**：
    在 `init` 块中，`this` 指向正在构造的实例。此时对象尚未完全初始化（主构造函数参数已赋值，但属性初始化器和 init 块按顺序执行），因此不能访问尚未初始化的属性。
    
*   **主构造函数参数冲突**：
    ```kotlin
    class User(val name: String) {
        init {
            // name 指的是主构造函数参数
            // this.name 也指的是主构造函数参数（因为它被提升为属性）
        }
    }
    ```
    如果主构造函数参数没有 `val/var`，则它只是局部参数，不是属性，不能用 `this` 访问。

### 伴生对象中的 `this`

伴生对象 (`companion object`) 是一个单例对象。
*   在伴生对象内部，`this` 指向**伴生对象本身**，而不是外围类的实例。
*   伴生对象无法直接访问外围类的实例成员（非 static 成员），因为伴生对象在逻辑上类似于 Java 的 `static` 上下文。

```kotlin
class MyClass {
    val instanceProp = "Instance"
    
    companion object {
        val companionProp = "Companion"
        
        fun print() {
            // println(instanceProp) // 编译错误：无法从静态上下文访问非静态成员
            println(companionProp)  // 正确
            println(this.companionProp) // 正确，this 指向 Companion 对象
        }
    }
}
```

### 顶层函数与文件级属性

*   **没有 `this`**：
    在文件的顶层（不在任何类或对象中）定义的函数和属性，不属于任何实例。因此，在顶层作用域中使用 `this` 会导致编译错误。
    
    ```kotlin
    val globalVar = 10
    
    fun topLevelFunc() {
        // println(this) // 编译错误：'this' is not defined in this context
        println(globalVar) // 正确
    }
    ```

---

### 总结

*   **默认行为**：`this` 指向当前最近的接收者（类实例、扩展对象或 Lambda 接收者）。
*   **消除歧义**：使用 `this@Label` 访问外层作用域的实例，特别是在内部类、匿名对象和嵌套 Lambda 中。
*   **扩展函数**：记住 `this` 默认指向**扩展接收者**（被扩展的对象），用 `this@Class` 访问**分发接收者**（定义扩展的类）。
*   **DSL 核心**：带接收者的 Lambda 利用 `this` 提供流畅的 API 体验，理解 `this` 的指向是掌握 Kotlin DSL 的关键。
*   **避免陷阱**：不要在伴生对象中期望 `this` 指向外围类实例，也不要在顶层使用 `this`。

# Kotlin协程
## 协程基础

### 1. 协程概念

#### 轻量级线程的本质
协程（Coroutines）是 Kotlin 提供的一种轻量级的并发编程解决方案。它们不是操作系统级别的线程，而是运行在用户空间的轻量级执行单元。

**协程的特点：**
- **轻量级**：单个线程可以运行数千个协程，而创建线程通常限制在数百个
- **非阻塞**：协程可以在不阻塞线程的情况下暂停和恢复执行
- **结构化并发**：提供清晰的作用域管理和错误处理机制

```kotlin
import kotlinx.coroutines.*

fun main() = runBlocking {
    // 启动10万个协程
    repeat(100_000) {
        launch {
            delay(1000L) // 每个协程延迟1秒
            print(".")
        }
    }
}
```

#### 挂起与恢复机制
协程的核心机制是挂起（Suspension）和恢复（Resumption）。当协程遇到挂起函数时，它不会阻塞线程，而是将当前执行状态保存起来，让出线程给其他任务使用，稍后可以从挂起点继续执行。

```kotlin
suspend fun fetchData(): String {
    println("开始获取数据...")
    delay(2000L) // 挂起点，线程可以执行其他任务
    println("数据获取完成")
    return "数据内容"
}

suspend fun processData(): String {
    println("开始处理数据...")
    delay(1000L) // 挂起点
    println("数据处理完成")
    return "处理结果"
}

fun main() = runBlocking {
    val data = fetchData()
    val result = processData()
    println("最终结果: $data + $result")
}
```

#### 协程 vs 线程 vs Future/Promise

| 特性 | 协程 | 线程 | Future/Promise |
|------|------|------|----------------|
| 资源开销 | 极低 (~1KB) | 高 (~1MB) | 依赖底层实现 |
| 切换成本 | 几乎为零 | 系统调用 | 异步回调开销 |
| 编程模型 | 顺序代码 | 回调/阻塞 | 回调式 |
| 并发能力 | 高效 | 受限 | 依赖线程池 |

**协程优势示例：**
```kotlin
// 传统的 Future/Promise 风格
fun traditionalAsyncStyle() {
    CompletableFuture.supplyAsync { /* task1 */ }
        .thenCompose { result1 -> 
            CompletableFuture.supplyAsync { /* task2 with result1 */ }
        }
        .thenAccept { result2 ->
            println("Final result: $result2")
        }
}

// 协程风格 - 更直观
suspend fun coroutineStyle() {
    val result1 = async { /* task1 */ }.await()
    val result2 = async { /* task2 with result1 */ }.await()
    println("Final result: $result2")
}
```

### 2. 基本用法

```kotlin
import kotlinx.coroutines.*

fun main() = runBlocking {
    // 1. launch - 启动协程，不返回结果
    val job = launch {
        delay(1000L)
        println("Hello from launch!")
    }
    
    // 2. async - 获取结果，返回 Deferred<T>
    val deferred = async {
        delay(2000L)
        "Hello from async!"
    }
    
    // 3. runBlocking - 阻塞调用，等待所有子协程完成
    println("Before delay")
    delay(500L)
    println("After delay")
    
    // 等待 async 完成并获取结果
    println(deferred.await())
}
```

### 3. 挂起函数 (suspend functions)

#### suspend 关键字的作用
`suspend` 关键字标识一个函数可以被挂起和恢复。挂起函数只能在协程内部或其他挂起函数中调用。

```kotlin
// 挂起函数定义
suspend fun fetchUser(userId: String): User {
    delay(1000L) // 这里会挂起，但不阻塞线程
    return User(userId, "User Name")
}

// 挂起函数只能在协程或另一个挂起函数中调用
suspend fun processUser(userId: String) {
    val user = fetchUser(userId) // 正确调用
    println("Processing user: ${user.name}")
}

// 普通函数不能直接调用挂起函数
fun normalFunction() {
    // fetchUser("123") // 编译错误！
    runBlocking {
        val user = fetchUser("123") // 在协程中调用
    }
}

data class User(val id: String, val name: String)
```

#### 挂起函数的限制和特性
```kotlin
class MyClass {
    // 挂起函数不能是构造函数的一部分
    // suspend constructor() {} // 编译错误
    
    suspend fun mySuspendFunction() {
        // 挂起函数可以访问 this
        println("Accessing instance in suspend function")
        
        // 可以调用其他挂起函数
        delay(100L)
        
        // 可以包含普通的同步代码
        val result = calculateSomething()
    }
    
    private fun calculateSomething(): Int {
        return 42
    }
}

// 挂起函数可以作为高阶函数参数
suspend fun executeWithDelay(action: suspend () -> Unit) {
    delay(1000L)
    action()
}

// 挂起函数可以用作 lambda 表达式
val suspendLambda: suspend () -> String = {
    delay(500L)
    "Result from suspend lambda"
}
```

#### 挂起函数链式调用
```kotlin
suspend fun step1(): String {
    delay(100L)
    println("Step 1 completed")
    return "step1_result"
}

suspend fun step2(input: String): String {
    delay(200L)
    println("Step 2 completed with input: $input")
    return "$input_step2"
}

suspend fun step3(input: String): String {
    delay(300L)
    println("Step 3 completed with input: $input")
    return "$input_step3"
}

suspend fun chainExample() {
    val result = step1()
        .let { step2(it) }
        .let { step3(it) }
    println("Chain result: $result")
}

// 使用协程进行链式调用
fun main() = runBlocking {
    chainExample()
}
```

### 4. 协程构建器

#### `launch` - 启动协程，不返回结果
```kotlin
import kotlinx.coroutines.*

fun launchExamples() = runBlocking {
    // 基本用法
    val job1 = launch {
        delay(1000L)
        println("Task 1 completed")
    }
    
    // 带上下文的 launch
    val job2 = launch(Dispatchers.IO) {
        // 在 IO 线程执行
        println("Running on ${Thread.currentThread().name}")
        delay(500L)
    }
    
    // 异常处理的 launch
    val job3 = launch {
        try {
            delay(200L)
            throw RuntimeException("Error in launch")
        } catch (e: Exception) {
            println("Caught exception: ${e.message}")
        }
    }
    
    // 等待所有任务完成
    joinAll(job1, job2, job3)
    println("All launches completed")
}
```

#### `async` - 异步计算，返回 Deferred
```kotlin
import kotlinx.coroutines.*

fun asyncExamples() = runBlocking {
    // 基本用法
    val deferred1 = async {
        delay(1000L)
        "Result 1"
    }
    
    val deferred2 = async {
        delay(500L)
        "Result 2"
    }
    
    // 并发执行，然后获取结果
    val result1 = deferred1.await()
    val result2 = deferred2.await()
    println("Results: $result1, $result2")
    
    // 立即启动的 async (LAZY 模式)
    val lazyDeferred = async(start = CoroutineStart.LAZY) {
        println("Lazy computation started")
        delay(300L)
        "Lazy result"
    }
    
    println("Before await")
    val lazyResult = lazyDeferred.await() // 此时才开始执行
    println("Lazy result: $lazyResult")
    
    // 错误传播示例
    val errorDeferred = async {
        delay(100L)
        throw RuntimeException("Async error")
    }
    
    try {
        errorDeferred.await()
    } catch (e: Exception) {
        println("Caught async error: ${e.message}")
    }
}
```

#### `runBlocking` - 阻塞当前线程直到完成
```kotlin
import kotlinx.coroutines.*

fun runBlockingExamples() {
    // 最简单的用法
    runBlocking {
        delay(1000L)
        println("Inside runBlocking")
    }
    
    // 返回值
    val result = runBlocking {
        delay(500L)
        "Hello from runBlocking"
    }
    println("Result: $result")
    
    // 与现有协程集成
    runBlocking {
        launch {
            delay(200L)
            println("Background task")
        }
        
        delay(1000L)
        println("Main task")
    }
    
    // 使用指定的上下文
    runBlocking(Dispatchers.IO) {
        println("Running on IO dispatcher: ${Thread.currentThread().name}")
    }
}
```

## 协程与通道介绍

### 1. 协程的基本概念

#### 并发执行的工作单元
```kotlin
import kotlinx.coroutines.*

fun concurrentExecution() = runBlocking {
    val startTime = System.currentTimeMillis()
    
    // 多个协程并发执行
    val jobs = List(10) { i ->
        launch {
            delay((i + 1) * 100L) // 不同的延迟时间
            println("Coroutine $i finished at ${System.currentTimeMillis() - startTime}ms")
        }
    }
    
    // 等待所有协程完成
    jobs.joinAll()
    println("All coroutines finished at ${System.currentTimeMillis() - startTime}ms")
}

// 结构化并发示例
suspend fun structuredConcurrency() {
    coroutineScope {
        // 所有子协程都在这个作用域内
        launch {
            delay(1000L)
            println("Child 1 completed")
        }
        
        launch {
            delay(500L)
            println("Child 2 completed")
        }
        
        // 当所有子协程完成后，这个作用域才会结束
    }
    println("Parent scope completed")
}
```

#### 非阻塞异步编程模型
```kotlin
// 传统的阻塞方式
fun blockingWay() {
    val start = System.currentTimeMillis()
    
    // 这些操作会依次执行，总耗时约 3 秒
    Thread.sleep(1000) // 模拟 I/O 操作
    Thread.sleep(1000) // 模拟另一个 I/O 操作
    Thread.sleep(1000) // 模拟第三个 I/O 操作
    
    println("Blocking way took: ${System.currentTimeMillis() - start}ms")
}

// 协程的非阻塞方式
suspend fun nonBlockingWay() {
    val start = System.currentTimeMillis()
    
    // 这些操作并发执行，总耗时约 1 秒
    coroutineScope {
        launch { delay(1000L); println("Task 1 done") }
        launch { delay(1000L); println("Task 2 done") }
        launch { delay(1000L); println("Task 3 done") }
    }
    
    println("Non-blocking way took: ${System.currentTimeMillis() - start}ms")
}

fun main() = runBlocking {
    println("=== Blocking Way ===")
    blockingWay()
    
    println("\n=== Non-blocking Way ===")
    nonBlockingWay()
}
```

### 2. 通道 (Channels) 概述

#### 生产者-消费者模式
```kotlin
import kotlinx.coroutines.*
import kotlinx.coroutines.channels.*

fun producerConsumerExample() = runBlocking {
    // 创建一个通道
    val channel = Channel<String>()
    
    // 生产者协程
    launch {
        for (i in 1..5) {
            val message = "Message $i"
            channel.send(message)
            println("Sent: $message")
            delay(200L)
        }
        channel.close() // 关闭通道表示没有更多数据
    }
    
    // 消费者协程
    launch {
        for (message in channel) { // 循环直到通道关闭
            println("Received: $message")
            delay(100L) // 模拟处理时间
        }
        println("Channel closed, consumer finished")
    }
    
    delay(2000L) // 等待所有操作完成
}
```

#### 协程间通信机制
```kotlin
// 通过通道进行协程间通信
suspend fun interCoroutineCommunication() {
    val requestChannel = Channel<String>()
    val responseChannel = Channel<String>()
    
    // 服务协程
    launch {
        for (request in requestChannel) {
            println("Processing request: $request")
            delay(500L) // 模拟处理时间
            val response = "Response to: $request"
            responseChannel.send(response)
        }
    }
    
    // 客户端协程
    launch {
        requestChannel.send("Request 1")
        val response1 = responseChannel.receive()
        println("Got response: $response1")
        
        requestChannel.send("Request 2")
        val response2 = responseChannel.receive()
        println("Got response: $response2")
        
        requestChannel.close()
    }
}
```

#### 与传统队列的区别
```kotlin
import java.util.concurrent.ConcurrentLinkedQueue
import kotlinx.coroutines.*

// 传统队列方式（阻塞）
fun traditionalQueueExample() {
    val queue = ConcurrentLinkedQueue<String>()
    var hasData = false
    
    thread {
        // 生产者
        repeat(3) { i ->
            queue.offer("Item $i")
            hasData = true
            Thread.sleep(1000)
        }
    }
    
    thread {
        // 消费者 - 忙等待
        while (true) {
            if (hasData && queue.isNotEmpty()) {
                val item = queue.poll()
                if (item != null) {
                    println("Consumed: $item")
                    hasData = queue.isNotEmpty()
                }
            }
            Thread.sleep(10) // 避免过度消耗 CPU
        }
    }
}

// 通道方式（挂起）
suspend fun channelVsQueueExample() {
    val channel = Channel<String>(Channel.BUFFERED)
    
    // 生产者
    launch {
        repeat(3) { i ->
            channel.send("Item $i")
            delay(1000L)
        }
        channel.close()
    }
    
    // 消费者 - 自动挂起等待
    launch {
        for (item in channel) {
            println("Consumed: $item")
        }
    }
    
    delay(5000L)
}
```

## 取消与超时

### 1. 协程取消

#### 主动取消机制
```kotlin
import kotlinx.coroutines.*

fun activeCancellation() = runBlocking {
    val job = launch {
        repeat(1000) { i ->
            println("Job is running: $i")
            delay(500L)
        }
    }
    
    delay(2000L) // 等待 2 秒
    println("About to cancel job")
    job.cancel() // 主动取消
    job.join()   // 等待取消完成
    println("Job was cancelled and joined")
}

// 可取消的长时间运行任务
suspend fun cancellableLongRunningTask() {
    var nextPrintTime = 0L
    var counter = 0
    
    while (isActive) { // 检查协程是否处于活跃状态
        if (System.currentTimeMillis() >= nextPrintTime) {
            println("Count: $counter")
            nextPrintTime += 1000
            counter++
        }
        // yield() 让出执行权，同时检查取消状态
        yield()
    }
    println("Cancellable task was cancelled")
}
```

#### `cancel()` 和 `join()`
```kotlin
fun cancelAndJoinExample() = runBlocking {
    val job = launch {
        try {
            repeat(1000) { i ->
                println("Working $i ...")
                delay(500L)
            }
        } catch (e: CancellationException) {
            println("Coroutine was cancelled")
            throw e // 重新抛出取消异常
        }
    }
    
    delay(1300L) // 等待一段时间
    println("Cancelling job...")
    job.cancel() // 发送取消请求
    
    println("Joining job...")
    job.join() // 等待协程真正结束
    println("Job joined")
}

// 取消和超时结合使用
suspend fun cancellationWithTimeout() {
    withTimeout(1300L) {
        val job = launch {
            try {
                repeat(1000) {
                    println("Background job: $it")
                    delay(500L)
                }
            } finally {
                println("Finally block in background job")
            }
        }
        delay(2000L) // 这会导致超时
    }
}
```

#### 可取消性检查 (`yield()`, `isActive`)
```kotlin
suspend fun cancellationCheckExample() {
    // 方式1: 使用 isActive 检查
    for (i in 1..100) {
        if (!isActive) {
            println("Coroutine was cancelled")
            return
        }
        println("Processing item $i")
        delay(100L)
    }
    
    // 方式2: 使用 yield() 让出执行权并检查取消状态
    repeat(100) { i ->
        println("Yielding $i")
        yield() // 检查取消状态并可能挂起
        println("After yield $i")
    }
}

// 在密集计算中检查取消状态
suspend fun intensiveComputationWithCancellation() {
    var sum = 0L
    for (i in 1L..1000_000_000L) {
        sum += i
        if (i % 10_000_000 == 0L) {
            yield() // 定期检查取消状态
            println("Progress: ${i / 10_000_000}%")
        }
    }
    println("Sum: $sum")
}
```

#### 不可取消的代码块 (`nonCancellable`)
```kotlin
import kotlinx.coroutines.NonCancellable

fun nonCancellableExample() = runBlocking {
    val job = launch {
        try {
            repeat(100) { i ->
                println("Outer loop $i")
                delay(100L)
                
                // 不可取消的代码块
                withContext(NonCancellable) {
                    println("Starting critical section...")
                    delay(500L) // 即使被取消也会完成
                    println("Critical section completed")
                }
            }
        } finally {
            println("Finally in main coroutine")
        }
    }
    
    delay(300L)
    println("Cancelling job...")
    job.cancel()
    delay(700L) // 等待不可取消部分完成
    println("Done")
}
```

### 2. 超时处理

#### `withTimeout` - 超时抛出异常
```kotlin
import kotlinx.coroutines.*

suspend fun withTimeoutExample() {
    try {
        withTimeout(1000L) {
            println("Starting slow operation")
            delay(1500L) // 这会超时
            println("This won't be printed")
        }
    } catch (e: TimeoutCancellationException) {
        println("Operation timed out: ${e.message}")
    }
}

// 嵌套超时
suspend fun nestedTimeoutExample() {
    withTimeout(2000L) {
        println("Outer timeout: 2 seconds")
        
        withTimeout(500L) {
            println("Inner timeout: 500ms")
            delay(1000L) // 这会在 500ms 后超时
        }
    }
}
```

#### `withTimeoutOrNull` - 超时返回 null
```kotlin
suspend fun withTimeoutOrNullExample() {
    // 成功的情况
    val result1 = withTimeoutOrNull(1000L) {
        delay(500L)
        "Success result"
    }
    println("Result 1: $result1") // 输出: Success result
    
    // 超时的情况
    val result2 = withTimeoutOrNull(500L) {
        delay(1000L) // 这会超时
        "This won't be returned"
    }
    println("Result 2: $result2") // 输出: null
}

// 实际应用：网络请求超时
suspend fun networkCallWithTimeout(): String? {
    return withTimeoutOrNull(3000L) { // 3秒超时
        // 模拟网络请求
        delay(2000L)
        "Network response"
    }
}
```

#### 超时与取消的关系
```kotlin
suspend fun timeoutAndCancellationRelationship() {
    val job = launch {
        try {
            withTimeout(1000L) {
                delay(2000L) // 会发生超时
            }
        } catch (e: TimeoutCancellationException) {
            println("Caught timeout exception")
            // 超时会自动取消协程
            println("Is active after timeout: ${isActive}") // false
        }
    }
    
    delay(500L)
    println("Before job cancellation")
    job.cancel() // 尝试再次取消（实际上已经被超时取消了）
    job.join()
}
```

### 3. 取消费户端模式

#### 结构化并发下的取消传播
```kotlin
suspend fun structuredCancellationPropagation() {
    coroutineScope {
        val outerJob = launch {
            println("Outer job started")
            
            val innerJob = launch {
                try {
                    delay(5000L)
                    println("Inner job completed")
                } finally {
                    println("Inner job cleanup")
                }
            }
            
            delay(2000L)
            println("Outer job cancelling")
            // 当外层作用域结束时，所有子协程都会被取消
        }
        
        delay(1000L)
        println("Coroutine scope ending")
    }
    println("All jobs cancelled")
}

// SupervisorScope 的取消隔离
suspend fun supervisorScopeExample() {
    supervisorScope {
        val failingJob = launch {
            delay(100L)
            throw RuntimeException("Failed job")
        }
        
        val workingJob = launch {
            repeat(5) { i ->
                delay(200L)
                println("Working job: $i")
            }
        }
        
        failingJob.join()
        workingJob.join()
    }
}
```

#### 作用域取消的影响
```kotlin
suspend fun scopeCancellationImpact() {
    // regular scope - 取消传播
    println("=== Regular Scope ===")
    try {
        coroutineScope {
            launch {
                delay(100L)
                println("Should not print - will be cancelled")
            }
            
            launch {
                delay(2000L)
                println("This will also be cancelled")
            }
            
            delay(500L)
            throw RuntimeException("Scope failure")
        }
    } catch (e: Exception) {
        println("Scope failed: ${e.message}")
    }
    
    // supervisor scope - 取消隔离
    println("\n=== Supervisor Scope ===")
    supervisorScope {
        val failingJob = launch {
            delay(100L)
            throw RuntimeException("Failing job")
        }
        
        val workingJob = launch {
            delay(500L)
            println("Working job completed successfully")
        }
        
        failingJob.join()
        workingJob.join()
    }
}
```

## 组合挂起函数

### 1. 并发执行

#### `async` 实现并发
```kotlin
import kotlinx.coroutines.*

// 串行 vs 并行获取数据
suspend fun serialDataFetching() {
    val time = measureTimeMillis {
        val user = fetchUserData("user1")
        val posts = fetchUserPosts("user1")
        val comments = fetchUserComments("user1")
        
        println("Serial - User: ${user.name}, Posts: ${posts.size}, Comments: ${comments.size}")
    }
    println("Serial fetching took: ${time}ms")
}

suspend fun parallelDataFetching() {
    val time = measureTimeMillis {
        // 并发启动所有请求
        val userDeferred = async { fetchUserData("user1") }
        val postsDeferred = async { fetchUserPosts("user1") }
        val commentsDeferred = async { fetchUserComments("user1") }
        
        // 等待所有请求完成
        val user = userDeferred.await()
        val posts = postsDeferred.await()
        val comments = commentsDeferred.await()
        
        println("Parallel - User: ${user.name}, Posts: ${posts.size}, Comments: ${comments.size}")
    }
    println("Parallel fetching took: ${time}ms")
}

// 模拟数据获取函数
suspend fun fetchUserData(userId: String): User {
    delay(500L)
    return User(userId, "User $userId")
}

suspend fun fetchUserPosts(userId: String): List<String> {
    delay(800L)
    return listOf("Post 1", "Post 2", "Post 3")
}

suspend fun fetchUserComments(userId: String): List<String> {
    delay(300L)
    return listOf("Comment 1", "Comment 2")
}
```

#### 结构化并发原则
```kotlin
suspend fun structuredConcurrencyPrinciple() {
    // 正确的方式：使用结构化并发
    val results = coroutineScope {
        val deferred1 = async { heavyComputation1() }
        val deferred2 = async { heavyComputation2() }
        val deferred3 = async { heavyComputation3() }
        
        // 所有计算完成后才返回结果
        listOf(
            deferred1.await(),
            deferred2.await(),
            deferred3.await()
        )
    }
    
    println("Structured results: $results")
}

suspend fun heavyComputation1(): String {
    delay(1000L)
    return "Result 1"
}

suspend fun heavyComputation2(): String {
    delay(800L)
    return "Result 2"
}

suspend fun heavyComputation3(): String {
    delay(1200L)
    return "Result 3"
}
```

#### 异常传播与处理
```kotlin
suspend fun exceptionHandlingInConcurrentExecution() {
    try {
        coroutineScope {
            val successJob = async {
                delay(100L)
                "Success result"
            }
            
            val failureJob = async {
                delay(200L)
                throw RuntimeException("Async failure")
            }
            
            val anotherJob = async {
                delay(300L)
                "Another result" // 这个永远不会执行，因为前面的会先失败
            }
            
            // 当任何一个 async 失败时，整个 coroutineScope 会被取消
            listOf(successJob.await(), failureJob.await(), anotherJob.await())
        }
    } catch (e: Exception) {
        println("Caught exception: ${e.message}")
    }
}

// 使用 supervisorScope 来隔离异常
suspend fun supervisorScopeForExceptionIsolation() {
    supervisorScope {
        val successJob = async {
            delay(100L)
            "Success result"
        }
        
        val failureJob = async {
            delay(200L)
            throw RuntimeException("Async failure - isolated")
        }
        
        val anotherJob = async {
            delay(300L)
            "Another result - will execute"
        }
        
        // 分别处理每个结果
        println("Success: ${successJob.await()}")
        try {
            println("Failure: ${failureJob.await()}")
        } catch (e: Exception) {
            println("Failure caught: ${e.message}")
        }
        println("Another: ${anotherJob.await()}")
    }
}
```

### 2. 顺序执行 vs 并发执行

#### 默认顺序执行特性
```kotlin
suspend fun sequentialExecutionByDefault() {
    val time = measureTimeMillis {
        // 默认是顺序执行的
        val result1 = suspendFunction1()
        val result2 = suspendFunction2()
        val result3 = suspendFunction3()
        
        println("Sequential results: $result1, $result2, $result3")
    }
    println("Sequential execution took: ${time}ms")
}

// 并发执行实现
suspend fun concurrentExecutionImplementation() {
    val time = measureTimeMillis {
        // 使用 async 实现并发
        val deferred1 = async { suspendFunction1() }
        val deferred2 = async { suspendFunction2() }
        val deferred3 = async { suspendFunction3() }
        
        val result1 = deferred1.await()
        val result2 = deferred2.await()
        val result3 = deferred3.await()
        
        println("Concurrent results: $result1, $result2, $result3")
    }
    println("Concurrent execution took: ${time}ms")
}

// 模拟挂起函数
suspend fun suspendFunction1(): String {
    delay(1000L)
    return "Result 1"
}

suspend fun suspendFunction2(): String {
    delay(800L)
    return "Result 2"
}

suspend fun suspendFunction3(): String {
    delay(1200L)
    return "Result 3"
}
```

#### 性能对比分析
```kotlin
suspend fun performanceComparison() {
    println("=== Performance Comparison ===")
    
    // 顺序执行
    val sequentialTime = measureTimeMillis {
        val r1 = expensiveOperation(1)
        val r2 = expensiveOperation(2)
        val r3 = expensiveOperation(3)
        val r4 = expensiveOperation(4)
    }
    
    // 并发执行
    val concurrentTime = measureTimeMillis {
        coroutineScope {
            val d1 = async { expensiveOperation(1) }
            val d2 = async { expensiveOperation(2) }
            val d3 = async { expensiveOperation(3) }
            val d4 = async { expensiveOperation(4) }
            
            d1.await(); d2.await(); d3.await(); d4.await()
        }
    }
    
    println("Sequential time: ${sequentialTime}ms")
    println("Concurrent time: ${concurrentTime}ms")
    println("Speedup: ${sequentialTime.toDouble() / concurrentTime}x")
}

suspend fun expensiveOperation(id: Int): String {
    delay(500L) // 模拟耗时操作
    return "Op$id result"
}
```

### 3. 组合策略

#### `awaitAll()` 批量等待
```kotlin
suspend fun awaitAllExample() {
    val deferredList = listOf(
        async { delay(1000L); "First" },
        async { delay(500L); "Second" },
        async { delay(1500L); "Third" },
        async { delay(800L); "Fourth" }
    )
    
    // 批量等待所有异步操作完成
    val results = awaitAll(*deferredList.toTypedArray())
    println("All results: $results")
}

// 在实际场景中的应用
suspend fun batchProcessingExample() {
    val userIds = listOf("1", "2", "3", "4", "5")
    
    val userFetches = userIds.map { userId ->
        async { fetchUserDetails(userId) }
    }
    
    val users = awaitAll(*userFetches.toTypedArray())
    println("Fetched ${users.size} users")
}

suspend fun fetchUserDetails(userId: String): User {
    delay(200L)
    return User(userId, "User $userId")
}
```

#### 选择表达式 (`select` - 实验性)
```kotlin
// 注意：select 是实验性的，在新版本中可能有变化
import kotlinx.coroutines.selects.*

suspend fun selectExample() {
    val channel1 = Channel<String>()
    val channel2 = Channel<String>()
    
    launch {
        delay(1000L)
        channel1.send("From channel 1")
    }
    
    launch {
        delay(500L)
        channel2.send("From channel 2")
    }
    
    // 选择最先可用的操作
    val result = select<String> {
        channel1.onReceive { value ->
            "Received from channel1: $value"
        }
        channel2.onReceive { value ->
            "Received from channel2: $value"
        }
    }
    
    println(result) // 会收到 channel2 的值，因为它先准备好
}
```

#### 错误处理组合
```kotlin
suspend fun combinedErrorHandling() {
    try {
        coroutineScope {
            val jobs = List(5) { i ->
                async {
                    if (i == 2) {
                        throw RuntimeException("Error in job $i")
                    }
                    delay(i * 200L)
                    "Result from job $i"
                }
            }
            
            // 所有任务要么都成功，要么都失败
            val results = awaitAll(*jobs.toTypedArray())
            println("All results: $results")
        }
    } catch (e: Exception) {
        println("Combined error: ${e.message}")
    }
}

// 带重试的组合
suspend fun retryOnErrorCombination() {
    val results = mutableListOf<String>()
    
    coroutineScope {
        repeat(3) { attempt ->
            try {
                val job = async {
                    if (attempt < 2) {
                        throw RuntimeException("Attempt $attempt failed")
                    }
                    "Success on attempt $attempt"
                }
                results.add(job.await())
                return@coroutineScope
            } catch (e: Exception) {
                println("Attempt $attempt failed: ${e.message}")
                if (attempt == 2) throw e // 最后一次尝试也失败
            }
        }
    }
    
    println("Final results: $results")
}
```

## 协程上下文与调度器

### 1. 协程上下文 (CoroutineContext)

#### 上下文元素组成
```kotlin
import kotlinx.coroutines.*

// 协程上下文包含多个元素
fun contextElementsExample() = runBlocking {
    launch {
        // 获取当前协程的上下文信息
        println("Coroutine Context:")
        println("- Job: ${coroutineContext[Job]}")
        println("- Dispatcher: ${coroutineContext[CoroutineDispatcher]}")
        println("- Name: ${coroutineContext[CoroutineName]}")
        println("- Exception Handler: ${coroutineContext[CoroutineExceptionHandler]}")
    }
}

// 自定义上下文元素
class CustomContextElement : AbstractCoroutineContextElement(CustomContextElement) {
    companion object Key : CoroutineContext.Key<CustomContextElement>
    
    override fun toString(): String = "CustomContextElement"
}

suspend fun customContextElementUsage() {
    withContext(CustomContextElement()) {
        println("Custom element in context: ${coroutineContext[CustomContextElement]}")
    }
}
```

#### `+` 操作符合并上下文
```kotlin
suspend fun contextMergingExample() {
    // 创建不同的上下文
    val dispatcherContext = Dispatchers.IO
    val nameContext = CoroutineName("MyCoroutine")
    val customContext = CustomContextElement()
    
    // 使用 + 操作符合并上下文
    val combinedContext = dispatcherContext + nameContext + customContext
    
    withContext(combinedContext) {
        println("Running with merged context")
        println("Name: ${coroutineContext[CoroutineName]?.name}")
        println("Custom: ${coroutineContext[CustomContextElement]}")
    }
}

// 上下文覆盖规则
suspend fun contextOverrideRules() {
    val ctx1 = Dispatchers.Default + CoroutineName("First")
    val ctx2 = Dispatchers.IO + CoroutineName("Second")
    
    // 第二个上下文会覆盖第一个相同类型的元素
    val merged = ctx1 + ctx2
    
    withContext(merged) {
        println("Dispatcher: ${coroutineContext[CoroutineDispatcher]}") // IO
        println("Name: ${coroutineContext[CoroutineName]?.name}") // Second
    }
}
```

#### 上下文继承机制
```kotlin
suspend fun contextInheritance() {
    withContext(CoroutineName("Parent")) {
        println("Parent context: ${coroutineContext[CoroutineName]?.name}")
        
        // 子协程会继承父协程的上下文
        launch {
            println("Child context: ${coroutineContext[CoroutineName]?.name}")
        }
        
        // 但也可以添加新的上下文元素
        launch(CoroutineName("Child")) {
            println("Overridden child: ${coroutineContext[CoroutineName]?.name}")
        }
    }
}

// 上下文在挂起函数间的传递
suspend fun contextPassingBetweenFunctions() {
    withContext(CoroutineName("Initial")) {
        println("In main: ${coroutineContext[CoroutineName]?.name}")
        callSuspendFunction()
    }
}

suspend fun callSuspendFunction() {
    println("In suspend function: ${coroutineContext[CoroutineName]?.name}")
    anotherSuspendFunction()
}

suspend fun anotherSuspendFunction() {
    println("In another function: ${coroutineContext[CoroutineName]?.name}")
}
```

### 2. 调度器 (Dispatchers)

#### `Dispatchers.Main` - UI 线程
```kotlin
// 注意：在 JVM 环境中需要相应的 UI 框架支持
suspend fun mainDispatcherExample() {
    // 在 Android 或 JavaFX 应用中使用
    withContext(Dispatchers.Main) {
        // 更新 UI 组件
        println("Running on Main thread: ${Thread.currentThread().name}")
        // updateUIComponent()
    }
}

// 模拟 Main 调度器（在测试环境中）
suspend fun simulateMainDispatcher() {
    withContext(SupervisorJob() + Dispatchers.Default.limitedParallelism(1)) {
        println("Simulated main thread: ${Thread.currentThread().name}")
    }
}
```

#### `Dispatchers.IO` - IO 密集型
```kotlin
suspend fun ioDispatcherExample() {
    withContext(Dispatchers.IO) {
        println("IO dispatcher thread: ${Thread.currentThread().name}")
        
        // 适合文件读写、网络请求等 IO 操作
        performIoOperation()
    }
}

suspend fun performIoOperation() {
    // 模拟 IO 操作
    delay(100L)
    println("IO operation completed")
}

// IO 调度器的并发能力
suspend fun ioConcurrencyExample() {
    val time = measureTimeMillis {
        coroutineScope {
            repeat(10) { i ->
                async(Dispatchers.IO) {
                    println("IO task $i starting on ${Thread.currentThread().name}")
                    delay(500L) // 模拟 IO 操作
                    println("IO task $i completed")
                }
            }
        }
    }
    println("IO concurrency took: ${time}ms")
}
```

#### `Dispatchers.Default` - CPU 密集型
```kotlin
suspend fun defaultDispatcherExample() {
    withContext(Dispatchers.Default) {
        println("Default dispatcher thread: ${Thread.currentThread().name}")
        
        // 适合 CPU 密集型计算
        val result = cpuIntensiveCalculation()
        println("CPU calculation result: $result")
    }
}

suspend fun cpuIntensiveCalculation(): Long {
    var sum = 0L
    for (i in 1L..100_000_000L) {
        sum += i
    }
    return sum
}

// Default 调度器的并行计算
suspend fun parallelCalculationExample() {
    val time = measureTimeMillis {
        val result = coroutineScope {
            val part1 = async(Dispatchers.Default) { calculateRange(1L, 25_000_000L) }
            val part2 = async(Dispatchers.Default) { calculateRange(25_000_001L, 50_000_000L) }
            val part3 = async(Dispatchers.Default) { calculateRange(50_000_001L, 75_000_000L) }
            val part4 = async(Dispatchers.Default) { calculateRange(75_000_001L, 100_000_000L) }
            
            part1.await() + part2.await() + part3.await() + part4.await()
        }
        println("Parallel calculation result: $result")
    }
    println("Parallel calculation took: ${time}ms")
}

suspend fun calculateRange(start: Long, end: Long): Long {
    var sum = 0L
    for (i in start..end) {
        sum += i
    }
    return sum
}
```

#### `Dispatchers.Unconfined` - 非受限调度器
```kotlin
suspend fun unconfinedDispatcherExample() {
    println("Before Unconfined - ${Thread.currentThread().name}")
    
    withContext(Dispatchers.Unconfined) {
        println("Unconfined 1 - ${Thread.currentThread().name}")
        delay(100L) // 在 delay 后可能会切换到不同的线程
        println("Unconfined 2 - ${Thread.currentThread().name}")
    }
    
    println("After Unconfined - ${Thread.currentThread().name}")
}

// Unconfined 的使用场景
suspend fun unconfinedUseCase() {
    // 适合快速的非阻塞操作
    withContext(Dispatchers.Unconfined) {
        // 快速的状态更新
        updateStateQuickly()
    }
}

suspend fun updateStateQuickly() {
    // 非阻塞的快速操作
    println("State updated quickly")
}
```

### 3. 上下文控制

#### `withContext` 切换上下文
```kotlin
suspend fun contextSwitchingExample() {
    println("Original context: ${Thread.currentThread().name}")
    
    // 切换到 IO 调度器进行文件操作
    val fileContent = withContext(Dispatchers.IO) {
        println("IO context: ${Thread.currentThread().name}")
        readFileContent()
    }
    
    // 切换到 Default 调度器进行计算
    val processedContent = withContext(Dispatchers.Default) {
        println("Default context: ${Thread.currentThread().name}")
        processFileContent(fileContent)
    }
    
    // 返回原始上下文
    println("Back to original: ${Thread.currentThread().name}")
    println("Final result: $processedContent")
}

suspend fun readFileContent(): String {
    delay(200L) // 模拟文件读取
    return "File content"
}

suspend fun processFileContent(content: String): String {
    delay(300L) // 模拟内容处理
    return "Processed: $content"
}
```

#### 自定义调度器
```kotlin
import java.util.concurrent.Executors

// 创建自定义调度器
val customDispatcher = Executors.newFixedThreadPool(4) { runnable ->
    Thread(runnable, "CustomPoolThread").apply { isDaemon = true }
}.asCoroutineDispatcher()

suspend fun customDispatcherUsage() {
    withContext(customDispatcher) {
        println("Running on custom dispatcher: ${Thread.currentThread().name}")
        delay(100L)
    }
    
    // 使用完后记得关闭
    customDispatcher.close()
}

// 限制并发数的调度器
suspend fun limitedConcurrencyDispatcher() {
    val limitedDispatcher = Dispatchers.Default.limitedParallelism(2)
    
    withContext(limitedDispatcher) {
        coroutineScope {
            repeat(5) { i ->
                launch {
                    println("Task $i running on: ${Thread.currentThread().name}")
                    delay(500L)
                }
            }
        }
    }
}
```

#### 上下文隔离
```kotlin
suspend fun contextIsolationExample() {
    withContext(CoroutineName("Outer")) {
        println("Outer context: ${coroutineContext[CoroutineName]?.name}")
        
        // 创建隔离的上下文
        withContext(Job()) {
            println("Isolated context: ${coroutineContext[CoroutineName]?.name}") // null
            println("Still has Job: ${coroutineContext[Job] != null}")
        }
        
        println("Back to outer: ${coroutineContext[CoroutineName]?.name}")
    }
}
```

### 4. Job 与作用域管理

#### Job 的生命周期
```kotlin
import kotlinx.coroutines.*

fun jobLifecycleExample() = runBlocking {
    val job = launch {
        repeat(1000) { i ->
            println("Job is running: $i")
            delay(500L)
        }
    }
    
    delay(1500L)
    println("Job state before cancel: ${job.state}")
    println("Job isActive: ${job.isActive}")
    println("Job isCompleted: ${job.isCompleted}")
    println("Job isCancelled: ${job.isCancelled}")
    
    job.cancel()
    delay(100L)
    println("Job state after cancel: ${job.state}")
    println("Job isCompleted: ${job.isCompleted}")
    println("Job isCancelled: ${job.isCancelled}")
    
    job.join()
    println("Job joined, final state: ${job.state}")
}
```

#### 父子关系与结构化并发
```kotlin
suspend fun parentChildRelationship() {
    val parentJob = Job()
    
    // 子 Job 会继承父 Job 的取消状态
    val childJob = launch(parentJob + CoroutineName("Child")) {
        try {
            repeat(1000) { i ->
                println("Child job running: $i")
                delay(500L)
            }
        } finally {
            println("Child job cleanup")
        }
    }
    
    delay(1500L)
    println("Cancelling parent job")
    parentJob.cancel() // 取消父 Job 会影响子 Job
    
    childJob.join()
    println("Child job finished after parent cancellation")
}

// 作用域构建器
suspend fun scopeBuildersExample() {
    // coroutineScope - 结构化并发
    try {
        coroutineScope {
            launch {
                delay(100L)
                throw RuntimeException("Scope failure")
            }
            delay(1000L) // 这个不会执行，因为上面会抛出异常
        }
    } catch (e: Exception) {
        println("Caught in coroutineScope: ${e.message}")
    }
    
    // supervisorScope - 异常隔离
    supervisorScope {
        val failingJob = launch {
            delay(100L)
            throw RuntimeException("Supervisor child failure")
        }
        
        val workingJob = launch {
            delay(200L)
            println("Working job completed in supervisor scope")
        }
        
        failingJob.join()
        workingJob.join()
    }
}
```

## 异步流 (Flow)

### 1. Flow 基础

#### 响应式流式数据处理
```kotlin
import kotlinx.coroutines.*
import kotlinx.coroutines.flow.*

// Flow 的基本概念
suspend fun flowBasicsExample() {
    // 创建一个简单的 Flow
    val numbersFlow = flow {
        emit(1)
        emit(2)
        emit(3)
        emit(4)
        emit(5)
    }
    
    // 收集 Flow 中的数据
    numbersFlow.collect { number ->
        println("Collected: $number")
    }
}

// Flow 与序列的对比
suspend fun flowVsSequence() {
    println("=== Flow (Cold Stream) ===")
    val flow = flow {
        println("Flow started")
        emit(1)
        delay(100L)
        emit(2)
        delay(100L)
        emit(3)
    }
    
    println("Flow created, but not started yet")
    delay(200L)
    println("Collecting flow first time:")
    flow.collect { println("First collection: $it") }
    
    println("Collecting flow second time:")
    flow.collect { println("Second collection: $it") }
    
    println("\n=== Sequence (Eager Evaluation) ===")
    val sequence = sequence {
        println("Sequence started")
        yield(1)
        println("After 1")
        yield(2)
        println("After 2")
        yield(3)
        println("After 3")
    }
    
    println("Sequence created")
    println("Iterating sequence first time:")
    sequence.forEach { println("First iteration: $it") }
}
```

#### 冷流特性
```kotlin
// 冷流特性：每次收集都是重新执行
suspend fun coldFlowCharacteristics() {
    val coldFlow = flow {
        println("Flow body executed")
        repeat(3) { i ->
            delay(100L)
            emit("Item $i")
        }
    }
    
    println("Flow created, collecting first time:")
    coldFlow.collect { println("First collection: $it") }
    
    println("\nCollecting second time:")
    coldFlow.collect { println("Second collection: $it") }
}

// 热流 vs 冷流对比
suspend fun hotVsColdFlow() {
    // 冷流 - 每次收集都重新开始
    val coldFlow = flow {
        var counter = 0
        while (true) {
            delay(500L)
            emit(counter++)
        }
    }
    
    // 如果我们想创建热流，需要使用其他机制
    val sharedFlow = MutableSharedFlow<Int>()
    
    // 启动生产者
    launch {
        var counter = 0
        while (true) {
            delay(500L)
            sharedFlow.emit(counter++)
        }
    }
    
    // 两个收集者会收到相同的值（热流）
    launch {
        delay(1000L)
        println("First collector starting")
        sharedFlow.take(5).collect { println("Collector 1: $it") }
    }
    
    launch {
        delay(2000L)
        println("Second collector starting")
        sharedFlow.take(5).collect { println("Collector 2: $it") }
    }
    
    delay(5000L)
}
```

#### Flow vs Sequence vs Observable
```kotlin
// Flow 的优势展示
suspend fun flowAdvantages() {
    // 1. 异步操作
    val asyncFlow = flow {
        repeat(3) { i ->
            delay(1000L) // 异步操作
            emit("Async item $i")
        }
    }
    
    // 2. 背压处理
    val fastFlow = flow {
        repeat(10) { i ->
            emit(i)
        }
    }
    
    fastFlow
        .buffer(2) // 缓冲区大小为2
        .collect { value ->
            delay(300L) // 模拟慢速处理
            println("Collected: $value")
        }
    
    // 3. 错误处理
    val errorHandlingFlow = flow {
        emit(1)
        emit(2)
        throw RuntimeException("Flow error")
        emit(3) // 这个不会发出
    }
    
    try {
        errorHandlingFlow.catch { e ->
            println("Caught error: ${e.message}")
            emit(-1) // 发送错误标记
        }.collect { println("Value: $it") }
    } catch (e: Exception) {
        println("Unhandled error: ${e.message}")
    }
}
```

### 2. Flow 构建

#### `flow { }` 构建器
```kotlin
// 基本的 flow 构建器
suspend fun basicFlowBuilder() {
    val simpleFlow = flow {
        emit("Hello")
        delay(1000L)
        emit("World")
        delay(1000L)
        emit("!")
    }
    
    simpleFlow.collect { println("Basic flow: $it") }
}

// 复杂的 flow 构建器示例
suspend fun complexFlowBuilder() {
    val complexFlow = flow {
        emit("Starting...")
        
        // 模拟多个步骤
        val step1 = async { performStep(1) }
        val step2 = async { performStep(2) }
        val step3 = async { performStep(3) }
        
        emit(step1.await())
        emit(step2.await())
        emit(step3.await())
        
        emit("Completed!")
    }
    
    complexFlow.collect { println("Complex flow: $it") }
}

suspend fun performStep(step: Int): String {
    delay((step * 500).toLong())
    return "Step $step completed"
}
```

#### `flowOf()` 创建简单流
```kotlin
suspend fun flowOfExample() {
    // 创建包含固定值的 Flow
    val simpleFlow = flowOf(1, 2, 3, 4, 5)
    simpleFlow.collect { println("flowOf: $it") }
    
    // 与列表转换
    val listFlow = listOf(10, 20, 30).asFlow()
    listFlow.collect { println("List as flow: $it") }
    
    // 字符串流
    val stringFlow = flowOf("A", "B", "C", "D")
    stringFlow.collect { println("String flow: $it") }
}
```

#### `asFlow()` 转换集合
```kotlin
suspend fun asFlowConversion() {
    // 转换各种集合类型
    val listFlow = listOf(1, 2, 3, 4, 5).asFlow()
    val setFlow = setOf("apple", "banana", "cherry").asFlow()
    val arrayFlow = arrayOf("one", "two", "three").asFlow()
    
    println("List flow:")
    listFlow.collect { println("  $it") }
    
    println("\nSet flow:")
    setFlow.collect { println("  $it") }
    
    println("\nArray flow:")
    arrayFlow.collect { println("  $it") }
}

// Range 转换为 Flow
suspend fun rangeToFlow() {
    (1..5).asFlow()
        .collect { println("Range item: $it") }
    
    // 步长为2的范围
    (0..10 step 2).asFlow()
        .collect { println("Stepped range: $it") }
}
```

### 3. Flow 操作符

#### 中间操作符 (transformations)
```kotlin
suspend fun intermediateOperators() {
    val sourceFlow = (1..10).asFlow()
    
    // map - 转换每个元素
    sourceFlow
        .map { it * 2 }
        .collect { println("Mapped: $it") }
    
    println("\n--- filter ---")
    // filter - 过滤元素
    sourceFlow
        .filter { it % 2 == 0 }
        .collect { println("Filtered: $it") }
    
    println("\n--- take ---")
    // take - 取前几个元素
    sourceFlow
        .take(3)
        .collect { println("Take: $it") }
    
    println("\n--- drop ---")
    // drop - 跳过前几个元素
    sourceFlow
        .drop(7)
        .collect { println("Drop: $it") }
    
    println("\n--- distinct ---")
    // distinct - 去重
    flowOf(1, 1, 2, 2, 3, 3)
        .distinctUntilChanged()
        .collect { println("Distinct: $it") }
    
    println("\n--- transform ---")
    // transform - 通用转换操作符
    sourceFlow
        .transform { value ->
            emit("Before: $value")
            if (value > 5) {
                emit("Large number: $value")
            }
            emit("After: $value")
        }
        .collect { println("Transform: $it") }
}
```

#### 终端操作符 (collections)
```kotlin
suspend fun terminalOperators() {
    val numbersFlow = (1..10).asFlow()
    
    // collect - 收集所有元素
    println("Collect all:")
    numbersFlow.collect { print("$it ") }
    println()
    
    // toList - 转换为列表
    val list = numbersFlow.toList()
    println("To list: $list")
    
    // toSet - 转换为集合
    val set = numbersFlow.filter { it % 2 == 0 }.toSet()
    println("To set: $set")
    
    // reduce - 归约操作
    val sum = numbersFlow.reduce { acc, value -> acc + value }
    println("Sum: $sum")
    
    // fold - 带初始值的归约
    val product = numbersFlow.fold(1) { acc, value -> acc * value }
    println("Product: $product")
    
    // first, last, single
    val first = numbersFlow.first()
    val last = numbersFlow.last()
    println("First: $first, Last: $last")
    
    // count
    val evenCount = numbersFlow.count { it % 2 == 0 }
    println("Even count: $evenCount")
    
    // any, all
    val hasOdd = numbersFlow.any { it % 2 == 1 }
    val allLessThan20 = numbersFlow.all { it < 20 }
    println("Has odd: $hasOdd, All less than 20: $allLessThan20")
}
```

#### 错误处理操作符
```kotlin
suspend fun errorHandlingOperators() {
    // catch - 捕获上游错误
    flowOf(1, 2, 3)
        .map { value ->
            if (value == 2) throw RuntimeException("Error at $value")
            value * 2
        }
        .catch { e ->
            println("Caught error: ${e.message}")
            emit(-1) // 发送错误标记
        }
        .collect { println("Value: $it") }
    
    println("\n--- retry ---")
    // retry - 重试操作
    var attempt = 0
    flow {
        attempt++
        println("Attempt: $attempt")
        if (attempt < 3) {
            throw RuntimeException("Retryable error")
        }
        emit("Success on attempt $attempt")
    }
    .retry(5) { cause ->
        println("Retrying due to: ${cause.message}")
        true
    }
    .collect { println("Final result: $it") }
    
    println("\n--- retryWhen ---")
    // retryWhen - 条件重试
    var retryCount = 0
    flowOf(1, 2, 3)
        .map { value ->
            if (value == 2) throw RuntimeException("Error at $value")
            value
        }
        .retryWhen { cause, attempt ->
            if (attempt < 3 && cause.message?.contains("Error") == true) {
                println("Retrying... (attempt $attempt)")
                delay(100L)
                retryCount++
                true
            } else {
                false
            }
        }
        .catch { e -> println("Final error: ${e.message}") }
        .collect { println("Value: $it") }
}
```

### 4. Flow 配置

#### 背压处理
```kotlin
suspend fun backpressureHandling() {
    // buffer - 缓冲背压
    println("=== Buffer Example ===")
    flow {
        repeat(5) { i ->
            println("Emitting $i")
            emit(i)
            delay(100L)
        }
    }
    .buffer(3) // 缓冲区大小为3
    .collect { value ->
        println("Collecting $value")
        delay(200L) // 模拟慢速处理
    }
    
    println("\n=== Conflate Example ===")
    // conflate - 合并背压（只保留最新值）
    flow {
        repeat(10) { i ->
            emit(i)
            delay(50L)
        }
    }
    .conflate() // 只处理最新的值
    .collect { value ->
        delay(100L) // 模拟慢速处理
        println("Conflated value: $value")
    }
    
    println("\n=== CollectLatest Example ===")
    // collectLatest - 只收集最新的值
    flow {
        repeat(5) { i ->
            emit(i)
            delay(100L)
        }
    }
    .collectLatest { value ->
        println("Started collecting $value")
        delay(300L) // 模拟慢速处理
        println("Finished collecting $value")
    }
}
```

#### 缓冲与收集
```kotlin
suspend fun bufferingAndCollection() {
    val source = flow {
        repeat(8) { i ->
            println("Source emitting $i")
            emit(i)
            delay(100L)
        }
    }
    
    println("=== No buffering ===")
    source.collect { value ->
        println("Collecting $value")
        delay(200L) // 慢速处理
    }
    
    println("\n=== With buffer ===")
    source.buffer(5).collect { value ->
        println("Buffered collecting $value")
        delay(200L) // 慢速处理
    }
    
    println("\n=== With produceIn ===")
    // produceIn - 将 Flow 转换为 Channel
    val channel = source.produceIn(this)
    repeat(8) {
        val value = channel.receive()
        println("Produced: $value")
        delay(150L)
    }
}
```

#### 调度器切换
```kotlin
suspend fun dispatcherSwitchingInFlow() {
    flowOf(1, 2, 3, 4, 5)
        .flowOn(Dispatchers.IO) // 在 IO 线程上发射
        .map { value ->
            println("Mapping on: ${Thread.currentThread().name}, value: $value")
            value * 2
        }
        .flowOn(Dispatchers.Default) // 在 Default 线程上映射
        .collect { value ->
            println("Collecting on: ${Thread.currentThread().name}, value: $value")
        }
}

// Flow 中的上下文控制
suspend fun flowContextControl() {
    flow {
        repeat(3) { i ->
            emit("Item $i")
            delay(200L)
        }
    }
    .flowOn(Dispatchers.IO) // 发射在 IO 线程
    .map { item ->
        withContext(Dispatchers.Default) { // 处理在 Default 线程
            println("Processing $item on ${Thread.currentThread().name}")
            item.uppercase()
        }
    }
    .collect { item ->
        println("Collected $item on ${Thread.currentThread().name}")
    }
}
```

### 5. Flow 特殊操作符

#### `shareIn()` 共享流
```kotlin
import kotlinx.coroutines.flow.SharingStarted

suspend fun shareInExample() {
    // 创建一个热流
    val sharedFlow = flow {
        var counter = 0
        while (true) {
            delay(1000L)
            emit("Shared item ${counter++}")
        }
    }
    .shareIn(
        scope = this,
        started = SharingStarted.WhileSubscribed(0L, 0L) // 订阅时开始，无订阅时停止
    )
    
    // 多个收集者共享同一个流
    launch {
        delay(500L)
        println("First collector starts")
        sharedFlow.take(3).collect { println("Collector 1: $it") }
    }
    
    launch {
        delay(1500L)
        println("Second collector starts")
        sharedFlow.take(3).collect { println("Collector 2: $it") }
    }
    
    delay(5000L)
}
```

#### `stateIn()` 状态流
```kotlin
import kotlinx.coroutines.flow.MutableStateFlow

suspend fun stateInExample() {
    // 创建可变状态流
    val mutableStateFlow = MutableStateFlow("Initial")
    
    // 转换为共享的状态流
    val stateFlow = mutableStateFlow
        .map { it.uppercase() }
        .stateIn(
            scope = this,
            started = SharingStarted.WhileSubscribed(0L),
            initialValue = "Default"
        )
    
    // 收集状态流
    launch {
        stateFlow.collect { value ->
            println("State collected: $value")
        }
    }
    
    // 更新状态
    delay(1000L)
    mutableStateFlow.value = "Updated Value"
    delay(1000L)
    mutableStateFlow.value = "Another Update"
    
    delay(2000L)
}
```

#### `broadcastChannel` (已废弃)
```kotlin
// 注意：BroadcastChannel 已被废弃，推荐使用 SharedFlow
import kotlinx.coroutines.channels.BroadcastChannel
import kotlinx.coroutines.channels.Channel

// 旧版本示例（不推荐使用）
suspend fun broadcastChannelExample() {
    val channel = BroadcastChannel<String>(Channel.BUFFERED)
    
    // 发送者
    launch {
        repeat(3) { i ->
            channel.send("Broadcast $i")
            delay(1000L)
        }
        channel.close()
    }
    
    // 多个接收者
    launch {
        val subscriber = channel.openSubscription()
        repeat(3) {
            val value = subscriber.receive()
            println("Subscriber 1: $value")
        }
    }
    
    launch {
        val subscriber = channel.openSubscription()
        repeat(3) {
            val value = subscriber.receive()
            println("Subscriber 2: $value")
        }
    }
    
    delay(5000L)
}
```

## 通道 (Channels)

### 1. 通道基础

#### 生产者-消费者通信
```kotlin
import kotlinx.coroutines.*
import kotlinx.coroutines.channels.*

suspend fun producerConsumerBasic() {
    val channel = Channel<String>()
    
    // 生产者
    launch {
        repeat(5) { i ->
            val message = "Message $i"
            channel.send(message)
            println("Sent: $message")
            delay(200L)
        }
        channel.close() // 关闭通道
    }
    
    // 消费者
    launch {
        for (message in channel) {
            println("Received: $message")
            delay(100L)
        }
        println("Channel closed, consumer finished")
    }
    
    delay(2000L)
}
```

#### 通道容量与缓冲
```kotlin
suspend fun channelCapacityExample() {
    println("=== Rendezvous Channel (capacity = 0) ===")
    val rendezvousChannel = Channel<String>(Channel.RENDEZVOUS)
    
    launch {
        println("Sending to rendezvous channel")
        rendezvousChannel.send("Rendezvous message")
        println("Message sent")
    }
    
    delay(500L)
    launch {
        delay(1000L)
        val msg = rendezvousChannel.receive()
        println("Received: $msg")
    }
    
    delay(2000L)
    
    println("\n=== Buffered Channel ===")
    val bufferedChannel = Channel<String>(Channel.BUFFERED)
    
    launch {
        repeat(5) {
            bufferedChannel.send("Buffered $it")
            println("Buffered sent: $it")
        }
    }
    
    launch {
        repeat(5) {
            delay(300L)
            val msg = bufferedChannel.receive()
            println("Buffered received: $msg")
        }
    }
    
    delay(2000L)
}

// 自定义容量通道
suspend fun customCapacityChannel() {
    val channel = Channel<String>(3) // 容量为3
    
    launch {
        repeat(5) { i ->
            println("About to send $i")
            channel.send("Item $i") // 前3个立即发送，第4个会挂起
            println("Sent $i")
        }
        channel.close()
    }
    
    launch {
        delay(1000L)
        for (item in channel) {
            println("Received: $item")
            delay(500L) // 慢速消费
        }
    }
    
    delay(3000L)
}
```

#### 通道关闭与完整性
```kotlin
suspend fun channelClosingExample() {
    val channel = Channel<Int>()
    
    launch {
        try {
            repeat(3) { i ->
                channel.send(i)
                println("Sent: $i")
            }
        } finally {
            println("Closing channel")
            channel.close()
        }
    }
    
    launch {
        try {
            for (item in channel) {
                println("Received: $item")
            }
        } finally {
            println("Channel iteration completed")
        }
    }
    
    delay(1000L)
}

// 带异常的通道关闭
suspend fun channelWithErrorClosing() {
    val channel = Channel<String>()
    
    launch {
        try {
            repeat(3) { i ->
                channel.send("Item $i")
            }
            throw RuntimeException("Error in sender")
        } catch (e: Exception) {
            channel.close(e) // 关闭并传递异常
        }
    }
    
    launch {
        try {
            for (item in channel) {
                println("Received: $item")
            }
        } catch (e: Exception) {
            println("Caught in receiver: ${e.message}")
        }
    }
    
    delay(1000L)
}
```

### 2. 通道类型

#### 无缓冲通道
```kotlin
suspend fun rendezvousChannelExample() {
    val channel = Channel<String>(Channel.RENDEZVOUS)
    
    launch {
        println("Sender: About to send")
        channel.send("Synchronous message") // 必须等待接收者
        println("Sender: Message sent")
    }
    
    launch {
        delay(1000L) // 延迟接收
        println("Receiver: About to receive")
        val msg = channel.receive()
        println("Receiver: Received: $msg")
    }
    
    delay(2000L)
}
```

#### 有缓冲通道
```kotlin
suspend fun bufferedChannelTypes() {
    // 默认缓冲
    val defaultBuffered = Channel<String>(Channel.BUFFERED)
    
    // 无缓冲
    val unbuffered = Channel<String>(Channel.RENDEZVOUS)
    
    // 有限缓冲
    val limitedBuffered = Channel<String>(2)
    
    // 演示不同缓冲类型的行为
    println("=== Limited Buffered Channel ===")
    val channel = Channel<String>(2)
    
    launch {
        repeat(5) { i ->
            println("Sending $i...")
            channel.send("Item $i")
            println("Sent $i")
        }
        channel.close()
    }
    
    launch {
        delay(1000L)
        for (item in channel) {
            println("Received: $item")
            delay(300L)
        }
    }
    
    delay(3000L)
}
```

#### BroadcastChannel (已废弃)
```kotlin
// 旧版本的广播通道示例
suspend fun broadcastChannelUsage() {
    val broadcastChannel = BroadcastChannel<String>(Channel.BUFFERED)
    
    // 发送者
    launch {
        repeat(3) { i ->
            broadcastChannel.send("Broadcast $i")
            delay(500L)
        }
        broadcastChannel.close()
    }
    
    // 多个订阅者
    repeat(2) { subscriberId ->
        launch {
            val subscription = broadcastChannel.openSubscription()
            for (item in subscription) {
                println("Subscriber $subscriberId received: $item")
            }
        }
    }
    
    delay(2000L)
}
```

### 3. 通道操作

#### 发送 (`send`, `offer`)
```kotlin
suspend fun channelSendOperations() {
    val channel = Channel<String>(1)
    
    // send - 阻塞发送
    launch {
        channel.send("Blocking send")
        println("Blocking send completed")
    }
    
    // offer - 非阻塞发送
    launch {
        delay(200L)
        val offered = channel.offer("Non-blocking send")
        println("Offer result: $offered")
        
        // 尝试发送到满的通道
        val fullResult = channel.offer("Won't fit")
        println("Full channel offer: $fullResult")
    }
    
    launch {
        delay(500L)
        println("Received: ${channel.receive()}")
    }
    
    delay(1000L)
}
```

#### 接收 (`receive`, `tryReceive`)
```kotlin
suspend fun channelReceiveOperations() {
    val channel = Channel<String>(Channel.BUFFERED)
    
    // 发送一些数据
    launch {
        repeat(3) { i ->
            channel.send("Item $i")
            delay(200L)
        }
    }
    
    launch {
        // receive - 阻塞接收
        val item1 = channel.receive()
        println("Received: $item1")
        
        // tryReceive - 非阻塞接收
        try {
            val item2 = channel.tryReceive().getOrNull()
            println("Try receive: $item2")
            
            // 尝试从空通道接收
            val emptyResult = channel.tryReceive().getOrNull()
            println("Empty channel: $emptyResult")
        } catch (e: Exception) {
            println("Try receive error: ${e.message}")
        }
    }
    
    delay(1000L)
}
```

#### 迭代通道内容
```kotlin
suspend fun iterateChannelContent() {
    val channel = Channel<Int>(Channel.BUFFERED)
    
    // 生产者
    launch {
        repeat(5) { i ->
            channel.send(i)
            delay(100L)
        }
        channel.close()
    }
    
    // 方式1: for 循环
    println("=== For Loop Iteration ===")
    launch {
        for (item in channel) {
            println("For loop: $item")
        }
    }
    
    delay(1000L)
    
    // 方式2: 接收直到关闭
    val channel2 = Channel<String>(Channel.BUFFERED)
    
    launch {
        repeat(3) { i ->
            channel2.send("Msg $i")
            delay(100L)
        }
        channel2.close()
    }
    
    launch {
        while (!channel2.isClosedForReceive) {
            val result = channel2.tryReceive()
            if (result.isSuccess) {
                println("While loop: ${result.getOrNull()}")
            } else {
                delay(50L) // 等待新数据
            }
        }
    }
    
    delay(1000L)
}
```

### 4. 通道管道

#### 数据处理管道
```kotlin
suspend fun dataProcessingPipeline() {
    // 输入通道
    val inputChannel = Channel<Int>(Channel.BUFFERED)
    
    // 处理通道
    val processingChannel = Channel<String>(Channel.BUFFERED)
    
    // 输出通道
    val outputChannel = Channel<String>(Channel.BUFFERED)
    
    // 数据生产者
    launch {
        repeat(5) { i ->
            inputChannel.send(i)
            delay(100L)
        }
        inputChannel.close()
    }
    
    // 数据处理器
    launch {
        for (number in inputChannel) {
            val processed = "Processed: ${number * 2}"
            processingChannel.send(processed)
        }
        processingChannel.close()
    }
    
    // 数据输出器
    launch {
        for (processed in processingChannel) {
            val formatted = "Formatted: [$processed]"
            outputChannel.send(formatted)
        }
        outputChannel.close()
    }
    
    // 最终消费者
    launch {
        for (output in outputChannel) {
            println("Final output: $output")
        }
    }
    
    delay(1000L)
}
```

#### 扇入扇出模式
```kotlin
// 扇出 (Fan-out) - 一个输入多个处理者
suspend fun fanOutPattern() {
    val inputChannel = Channel<Int>(Channel.BUFFERED)
    
    // 启动多个处理器
    repeat(3) { processorId ->
        launch {
            for (item in inputChannel) {
                delay(100L) // 模拟处理时间
                println("Processor $processorId handling: $item")
            }
        }
    }
    
    // 生产数据
    launch {
        repeat(6) { i ->
            inputChannel.send(i)
            delay(50L)
        }
        inputChannel.close()
    }
    
    delay(1000L)
}

// 扇入 (Fan-in) - 多个输入一个汇聚点
suspend fun fanInPattern() {
    val outputChannel = Channel<String>(Channel.BUFFERED)
    
    // 多个生产者
    repeat(3) { producerId ->
        launch {
            repeat(2) { i ->
                val message = "Producer $producerId - Item $i"
                outputChannel.send(message)
                delay(100L)
            }
        }
    }
    
    // 单一消费者
    launch {
        repeat(6) { // 期望接收6个消息
            val message = outputChannel.receive()
            println("Consumer received: $message")
        }
    }
    
    delay(1000L)
}
```

#### 通道与协程结合使用
```kotlin
suspend fun channelsWithCoroutinesIntegration() {
    // 创建一个服务通道
    val serviceChannel = Channel<ServiceRequest>(Channel.BUFFERED)
    
    // 服务协程
    launch {
        for (request in serviceChannel) {
            when (request.type) {
                RequestType.GET_USER -> {
                    val user = getUser(request.id)
                    request.responseChannel.send(ServiceResponse.Success(user))
                }
                RequestType.CREATE_USER -> {
                    val user = createUser(request.data)
                    request.responseChannel.send(ServiceResponse.Success(user))
                }
            }
        }
    }
    
    // 客户端协程
    launch {
        // 发送获取用户请求
        val responseChannel = Channel<ServiceResponse>(Channel.RENDEZVOUS)
        serviceChannel.send(ServiceRequest(RequestType.GET_USER, "123", "", responseChannel))
        val response = responseChannel.receive()
        println("Get user response: $response")
        
        // 发送创建用户请求
        val createResponseChannel = Channel<ServiceResponse>(Channel.RENDEZVOUS)
        serviceChannel.send(ServiceRequest(RequestType.CREATE_USER, "", "New User", createResponseChannel))
        val createResponse = createResponseChannel.receive()
        println("Create user response: $createResponse")
    }
    
    delay(1000L)
}

// 辅助类
enum class RequestType { GET_USER, CREATE_USER }

data class ServiceRequest(
    val type: RequestType,
    val id: String,
    val data: String,
    val responseChannel: Channel<ServiceResponse>
)

sealed class ServiceResponse {
    data class Success(val data: Any) : ServiceResponse()
    data class Error(val message: String) : ServiceResponse()
}

suspend fun getUser(id: String): String {
    delay(200L)
    return "User: $id"
}

suspend fun createUser(data: String): String {
    delay(300L)
    return "Created user: $data"
}
```

## 协程异常处理

### 1. 异常传播

#### 结构化并发下的异常传播
```kotlin
suspend fun structuredExceptionPropagation() {
    try {
        coroutineScope {
            launch {
                delay(100L)
                throw RuntimeException("Child exception")
            }
            
            launch {
                delay(500L)
                println("This should not print") // 不会执行
            }
            
            delay(1000L)
            println("This should also not print") // 不会执行
        }
    } catch (e: Exception) {
        println("Caught in parent: ${e.message}")
    }
}

// 异常传播的详细过程
suspend fun detailedExceptionPropagation() {
    println("=== Starting coroutineScope ===")
    
    try {
        coroutineScope {
            println("Inside coroutineScope")
            
            launch {
                println("Child 1 starting")
                delay(200L)
                println("Child 1 about to fail")
                throw RuntimeException("Child 1 failed")
            }
            
            launch {
                println("Child 2 starting")
                delay(100L)
                println("Child 2 doing work...")
                delay(500L) // 这个不会完成，因为子协程会失败
                println("Child 2 completed") // 不会执行
            }
            
            delay(1000L) // 主作用域不会等到这里，因为子协程失败了
            println("Main scope completed") // 不会执行
        }
    } catch (e: Exception) {
        println("Exception caught: ${e.message}")
        println("Exception in: ${e.stackTrace.firstOrNull()?.methodName}")
    }
    
    println("After coroutineScope - should continue")
}
```

#### SupervisorJob 与异常隔离
```kotlin
suspend fun supervisorJobExceptionIsolation() {
    supervisorScope {
        val failingJob = launch {
            delay(100L)
            println("Failing job starting")
            throw RuntimeException("Supervised failure")
        }
        
        val workingJob = launch {
            repeat(5) { i ->
                delay(200L)
                println("Working job: $i")
            }
        }
        
        failingJob.join()
        workingJob.join()
        println("Both jobs completed (failing one with exception)")
    }
}

// SupervisorJob 详细示例
suspend fun detailedSupervisorJob() {
    val supervisorJob = SupervisorJob()
    
    try {
        withContext(supervisorJob) {
            val job1 = launch {
                delay(100L)
                throw RuntimeException("Job 1 fails")
            }
            
            val job2 = launch {
                delay(200L)
                println("Job 2 succeeds despite job 1 failure")
                delay(200L)
                println("Job 2 completes")
            }
            
            val job3 = launch {
                delay(300L)
                println("Job 3 also succeeds")
            }
            
            joinAll(job1, job2, job3)
        }
    } finally {
        supervisorJob.cancel()
    }
}
```

#### 异常聚合处理
```kotlin
suspend fun exceptionAggregation() {
    try {
        coroutineScope {
            val jobs = List(3) { i ->
                async {
                    delay((i + 1) * 100L)
                    if (i == 1) {
                        throw RuntimeException("Error in job $i")
                    }
                    "Result from job $i"
                }
            }
            
            // 这里会抛出异常，聚合所有子协程的异常
            val results = awaitAll(*jobs.toTypedArray())
            println("Results: $results")
        }
    } catch (e: Exception) {
        println("Aggregated exception: ${e.message}")
        e.printStackTrace()
    }
}

// 处理多个异常
suspend fun multipleExceptionsHandling() {
    val exceptions = mutableListOf<Throwable>()
    
    supervisorScope {
        val jobs = List(3) { i ->
            async {
                delay((i + 1) * 100L)
                if (i in 1..2) {
                    throw RuntimeException("Error in job $i")
                }
                "Success from job $i"
            }
        }
        
        jobs.forEach { job ->
            try {
                job.await()
            } catch (e: Exception) {
                exceptions.add(e)
            }
        }
    }
    
    println("Collected exceptions: ${exceptions.size}")
    exceptions.forEachIndexed { index, exception ->
        println("Exception $index: ${exception.message}")
    }
}
```

### 2. 异常处理策略

#### `try-catch` 在协程中使用
```kotlin
suspend fun tryCatchInCoroutines() {
    // 在协程内部处理异常
    launch {
        try {
            delay(100L)
            throw RuntimeException("Internal error")
        } catch (e: Exception) {
            println("Caught inside coroutine: ${e.message}")
        }
    }
    
    // 在协程外部处理异常
    try {
        async {
            delay(200L)
            throw RuntimeException("Async error")
        }.await()
    } catch (e: Exception) {
        println("Caught outside coroutine: ${e.message}")
    }
    
    delay(500L)
}

// 嵌套异常处理
suspend fun nestedExceptionHandling() {
    coroutineScope {
        launch {
            try {
                async {
                    try {
                        delay(100L)
                        throw RuntimeException("Deep error")
                    } catch (e: Exception) {
                        println("Caught deep: ${e.message}")
                        throw RuntimeException("Re-thrown error", e)
                    }
                }.await()
            } catch (e: Exception) {
                println("Caught outer: ${e.message}")
                if (e.cause != null) {
                    println("Caused by: ${e.cause!!.message}")
                }
            }
        }
    }
}
```

#### `SupervisorScope` 异常隔离
```kotlin
suspend fun supervisorScopeIsolation() {
    supervisorScope {
        // 这个失败不会影响其他协程
        launch {
            delay(100L)
            throw RuntimeException("Supervised failure")
        }
        
        // 这个会正常运行
        launch {
            delay(200L)
            println("This runs despite other failure")
        }
        
        // 这个也会正常运行
        launch {
            delay(300L)
            println("This also runs normally")
        }
    }
}

// SupervisorScope 与 async 的结合
suspend fun supervisorScopeWithAsync() {
    val results = supervisorScope {
        val failingDeferred = async {
            delay(100L)
            throw RuntimeException("Async failure")
        }
        
        val successfulDeferred = async {
            delay(200L)
            "Successful result"
        }
        
        val anotherSuccessful = async {
            delay(300L)
            "Another successful result"
        }
        
        // 分别处理结果
        val results = mutableListOf<String?>()
        
        try {
            results.add(failingDeferred.await())
        } catch (e: Exception) {
            println("Failed async caught: ${e.message}")
            results.add(null)
        }
        
        results.add(successfulDeferred.await())
        results.add(anotherSuccessful.await())
        
        results
    }
    
    println("Results: $results")
}
```

#### `CoroutineExceptionHandler`
```kotlin
// 自定义异常处理器
val customExceptionHandler = CoroutineExceptionHandler { _, exception ->
    println("Custom handler caught: ${exception.message}")
    println("Exception type: ${exception::class.simpleName}")
}

suspend fun coroutineExceptionHandlerUsage() {
    // 在作用域中使用异常处理器
    withContext(customExceptionHandler) {
        launch {
            delay(100L)
            throw RuntimeException("Handled exception")
        }
        
        delay(500L)
        println("Main coroutine continues")
    }
}

// 全局异常处理器
class GlobalExceptionHandler : CoroutineExceptionHandler {
    override val key = CoroutineExceptionHandler
    
    override fun handleException(context: CoroutineContext, exception: Throwable) {
        println("Global handler: ${exception.message}")
        // 记录日志、上报错误等
    }
}

suspend fun globalExceptionHandlerExample() {
    val globalHandler = GlobalExceptionHandler()
    
    withContext(globalHandler) {
        async {
            throw RuntimeException("Global handling test")
        }
        
        delay(200L)
    }
}
```

### 3. 异常处理范围

#### `coroutineScope` vs `supervisorScope`
```kotlin
suspend fun compareScopes() {
    println("=== CoroutineScope (fail-fast) ===")
    try {
        coroutineScope {
            launch {
                delay(100L)
                throw RuntimeException("CoroutineScope failure")
            }
            
            launch {
                delay(200L)
                println("This won't execute")
            }
        }
    } catch (e: Exception) {
        println("CoroutineScope caught: ${e.message}")
    }
    
    println("\n=== SupervisorScope (isolation) ===")
    supervisorScope {
        val failingJob = launch {
            delay(100L)
            throw RuntimeException("SupervisorScope failure")
        }
        
        val workingJob = launch {
            delay(200L)
            println("This executes despite failure")
        }
        
        failingJob.join()
        workingJob.join()
    }
}

// 作用域内的异常处理行为
suspend fun scopeSpecificBehavior() {
    // 在 coroutineScope 中，异常会传播
    println("=== CoroutineScope behavior ===")
    try {
        coroutineScope {
            async {
                delay(100L)
                throw RuntimeException("Scope exception")
            }.await()
            
            println("This won't print") // 不会执行
        }
    } catch (e: Exception) {
        println("Caught in coroutineScope: ${e.message}")
    }
    
    // 在 supervisorScope 中，异常被隔离
    println("\n=== SupervisorScope behavior ===")
    supervisorScope {
        val deferred = async {
            delay(100L)
            throw RuntimeException("Supervisor exception")
        }
        
        // 即使 async 失败，作用域也会继续
        delay(200L)
        println("Supervisor scope continues")
        
        try {
            deferred.await()
        } catch (e: Exception) {
            println("Caught specific: ${e.message}")
        }
    }
}
```

#### 子协程异常对父协程的影响
```kotlin
suspend fun parentChildExceptionRelationship() {
    println("=== Parent affected by child ===")
    try {
        coroutineScope {
            // 父协程
            launch {
                println("Parent started")
                
                // 子协程失败
                launch {
                    delay(100L)
                    throw RuntimeException("Child failure")
                }
                
                // 父协程的后续代码不会执行
                delay(500L)
                println("Parent should not reach here")
            }
        }
    } catch (e: Exception) {
        println("Parent caught: ${e.message}")
    }
    
    println("\n=== Parent unaffected by supervised child ===")
    supervisorScope {
        launch {
            println("Supervised parent started")
            
            launch {
                delay(100L)
                throw RuntimeException("Supervised child failure")
            }
            
            delay(500L)
            println("Supervised parent continues")
        }
    }
}
```

### 4. 异常清理

#### `finally` 块与资源清理
```kotlin
suspend fun finallyBlockCleanup() {
    println("=== Finally block execution ===")
    
    try {
        coroutineScope {
            launch {
                try {
                    delay(100L)
                    throw RuntimeException("Exception in coroutine")
                } finally {
                    println("Finally block executed in coroutine")
                    // 清理资源
                }
            }
        }
    } catch (e: Exception) {
        println("Caught exception: ${e.message}")
    }
    
    println("After exception handling")
}

// 资源管理示例
suspend fun resourceManagementWithFinally() {
    var resource: AutoCloseableResource? = null
    
    try {
        resource = AutoCloseableResource("Test Resource")
        
        coroutineScope {
            launch {
                try {
                    delay(100L)
                    resource.use()
                    delay(200L)
                    throw RuntimeException("Error during resource use")
                } finally {
                    resource?.cleanup()
                }
            }
        }
    } catch (e: Exception) {
        println("Exception handled: ${e.message}")
    } finally {
        resource?.finalCleanup()
    }
}

class AutoCloseableResource(val name: String) {
    var used = false
    
    fun use() {
        used = true
        println("$name is being used")
    }
    
    fun cleanup() {
        if (used) {
            println("$name cleaned up in finally")
        }
    }
    
    fun finalCleanup() {
        println("$name final cleanup")
    }
}
```

#### `ensureActive()` 检查活跃状态
```kotlin
suspend fun ensureActiveExample() {
    val job = launch {
        repeat(1000) { i ->
            ensureActive() // 检查协程是否活跃
            println("Working $i...")
            delay(100L)
        }
    }
    
    delay(500L)
    job.cancel()
    println("Job cancelled, ensureActive will throw CancellationException")
    
    job.join()
}

// 在长时间循环中使用 ensureActive
suspend fun longRunningTaskWithEnsureActive() {
    var counter = 0
    while (true) {
        ensureActive() // 检查是否被取消
        
        // 模拟工作
        delay(10L)
        counter++
        
        if (counter % 100 == 0) {
            println("Processed $counter items")
        }
    }
}
```

#### 协程取消时的清理工作
```kotlin
suspend fun cancellationCleanup() {
    val job = launch {
        try {
            repeat(1000) { i ->
                println("Working: $i")
                delay(100L)
            }
        } finally {
            // 协程被取消时执行清理
            if (!isActive) {
                println("Cleaning up after cancellation")
                performCleanup()
            }
        }
    }
    
    delay(500L)
    job.cancelAndJoin()
    println("Job cancelled and cleaned up")
}

suspend fun performCleanup() {
    delay(100L) // 模拟清理时间
    println("Cleanup completed")
}

// 使用 withContext 进行清理
suspend fun cleanupWithContext() {
    withContext(NonCancellable) {
        try {
            // 可能被取消的操作
            delay(1000L)
        } finally {
            // 不可取消的清理代码
            println("Critical cleanup in NonCancellable context")
        }
    }
}
```

## 共享的可变状态与并发

### 1. 并发问题

#### 竞态条件 (Race Conditions)
```kotlin
// 竞态条件示例
class Counter {
    var count = 0
    
    fun increment() {
        val current = count
        Thread.sleep(1) // 模拟延迟，增加竞态条件概率
        count = current + 1
    }
}

suspend fun raceConditionExample() {
    val counter = Counter()
    val jobs = mutableListOf<Job>()
    
    // 启动多个协程同时修改计数器
    repeat(100) {
        val job = launch {
            repeat(10) {
                counter.increment()
            }
        }
        jobs.add(job)
    }
    
    jobs.joinAll()
    println("Expected: 1000, Actual: ${counter.count}")
    // 结果通常小于 1000，因为存在竞态条件
}

// 使用原子操作修复竞态条件
import java.util.concurrent.atomic.AtomicInteger

class AtomicCounter {
    private val atomicCount = AtomicInteger(0)
    
    fun increment() {
        atomicCount.incrementAndGet()
    }
    
    fun getCount(): Int = atomicCount.get()
}

suspend fun atomicCounterExample() {
    val counter = AtomicCounter()
    val jobs = mutableListOf<Job>()
    
    repeat(100) {
        val job = launch {
            repeat(10) {
                counter.increment()
            }
        }
        jobs.add(job)
    }
    
    jobs.joinAll()
    println("Atomic counter - Expected: 1000, Actual: ${counter.getCount()}")
}
```

#### 数据竞争 (Data Race)
```kotlin
// 数据竞争示例
class UnsafeBankAccount {
    var balance = 1000
    
    suspend fun withdraw(amount: Int) {
        if (balance >= amount) {
            delay(1) // 模拟处理时间
            balance -= amount
        }
    }
    
    suspend fun deposit(amount: Int) {
        if (amount > 0) {
            delay(1) // 模拟处理时间
            balance += amount
        }
    }
    
    fun getBalance(): Int = balance
}

suspend fun dataRaceExample() {
    val account = UnsafeBankAccount()
    val jobs = mutableListOf<Job>()
    
    // 多个协程同时操作账户
    repeat(50) {
        jobs.add(launch { account.withdraw(10) })
        jobs.add(launch { account.deposit(5) })
    }
    
    jobs.joinAll()
    println("Unsafe account balance: ${account.getBalance()}")
    // 由于数据竞争，结果可能不符合预期
}

// 修复数据竞争
class SafeBankAccount {
    private val mutex = Mutex()
    private var balance = 1000
    
    suspend fun withdraw(amount: Int) = mutex.withLock {
        if (balance >= amount) {
            delay(1) // 模拟处理时间
            balance -= amount
        }
    }
    
    suspend fun deposit(amount: Int) = mutex.withLock {
        if (amount > 0) {
            delay(1) // 模拟处理时间
            balance += amount
        }
    }
    
    suspend fun getBalance(): Int = mutex.withLock { balance }
}

suspend fun safeBankAccountExample() {
    val account = SafeBankAccount()
    val jobs = mutableListOf<Job>()
    
    repeat(50) {
        jobs.add(launch { account.withdraw(10) })
        jobs.add(launch { account.deposit(5) })
    }
    
    jobs.joinAll()
    println("Safe account balance: ${account.getBalance()}")
}
```

#### 原子性问题
```kotlin
// 原子性问题示例
class NonAtomicOperations {
    var value1 = 0
    var value2 = 0
    
    suspend fun updateBoth(newValue1: Int, newValue2: Int) {
        value1 = newValue1 // 第一步
        delay(1)          // 模拟中间状态可见
        value2 = newValue2 // 第二步
    }
    
    fun getValues(): Pair<Int, Int> = Pair(value1, value2)
}

suspend fun atomicityProblemExample() {
    val obj = NonAtomicOperations()
    val jobs = mutableListOf<Job>()
    
    // 更新操作
    jobs.add(launch {
        repeat(100) { i ->
            obj.updateBoth(i, i * 2)
        }
    })
    
    // 读取操作
    jobs.add(launch {
        repeat(100) {
            val (v1, v2) = obj.getValues()
            if (v2 != v1 * 2) {
                println("Inconsistent state detected: ($v1, $v2)")
            }
            delay(1)
        }
    })
    
    jobs.joinAll()
}

// 使用锁保证原子性
class AtomicOperations {
    private val mutex = Mutex()
    private var value1 = 0
    private var value2 = 0
    
    suspend fun updateBoth(newValue1: Int, newValue2: Int) = mutex.withLock {
        value1 = newValue1
        value2 = newValue2
    }
    
    suspend fun getValues(): Pair<Int, Int> = mutex.withLock { Pair(value1, value2) }
}
```

### 2. 线程安全解决方案

#### `synchronized` 替代方案
```kotlin
// 传统 synchronized 方式（Java风格）
/*
class SynchronizedCounter {
    @Synchronized
    fun increment() {
        count++
    }
}
*/

// Kotlin 协程中的替代方案：Mutex
import kotlinx.coroutines.sync.Mutex
import kotlinx.coroutines.sync.withLock

class MutexBasedCounter {
    private val mutex = Mutex()
    private var count = 0
    
    suspend fun increment() = mutex.withLock {
        val current = count
        delay(1) // 模拟处理
        count = current + 1
    }
    
    suspend fun getCount(): Int = mutex.withLock { count }
}

suspend fun mutexExample() {
    val counter = MutexBasedCounter()
    val jobs = mutableListOf<Job>()
    
    repeat(100) {
        val job = launch {
            repeat(10) {
                counter.increment()
            }
        }
        jobs.add(job)
    }
    
    jobs.joinAll()
    println("Mutex counter: ${counter.getCount()}")
}
```

#### `Mutex` 互斥锁
```kotlin
// Mutex 详细使用示例
class MutexExample {
    private val mutex = Mutex()
    private val data = mutableListOf<Int>()
    
    suspend fun addItem(item: Int) = mutex.withLock {
        println("Adding $item, current size: ${data.size}")
        data.add(item)
        delay(10) // 模拟处理时间
        println("Added $item, new size: ${data.size}")
    }
    
    suspend fun removeItem(): Int? = mutex.withLock {
        if (data.isNotEmpty()) {
            val item = data.removeAt(0)
            println("Removed $item, new size: ${data.size}")
            item
        } else {
            null
        }
    }
    
    suspend fun getSize(): Int = mutex.withLock { data.size }
}

suspend fun mutexDetailedExample() {
    val example = MutexExample()
    val jobs = mutableListOf<Job>()
    
    // 添加任务
    repeat(5) { i ->
        jobs.add(launch {
            example.addItem(i)
        })
    }
    
    // 移除任务
    repeat(3) { 
        jobs.add(launch {
            example.removeItem()
        })
    }
    
    jobs.joinAll()
    println("Final size: ${example.getSize()}")
}
```

#### `Semaphore` 信号量
```kotlin
import kotlinx.coroutines.sync.Semaphore
import kotlinx.coroutines.sync.withPermit

// 使用信号量控制并发数量
class SemaphoreExample {
    private val semaphore = Semaphore(3) // 最多3个并发
    private val activeTasks = mutableListOf<Int>()
    
    suspend fun performTask(taskId: Int) = semaphore.withPermit {
        activeTasks.add(taskId)
        println("Task $taskId started, active: ${activeTasks.joinToString(", ")}")
        
        delay(1000L) // 模拟任务执行
        
        activeTasks.remove(taskId)
        println("Task $taskId completed, active: ${activeTasks.joinToString(", ")}")
    }
}

suspend fun semaphoreExample() {
    val example = SemaphoreExample()
    val jobs = mutableListOf<Job>()
    
    // 启动10个任务，但只有3个能同时运行
    repeat(10) { i ->
        jobs.add(launch {
            example.performTask(i)
        })
    }
    
    jobs.joinAll()
    println("All tasks completed")
}
```

### 3. 原子变量

#### `AtomicReference`
```kotlin
import java.util.concurrent.atomic.AtomicReference

class AtomicReferenceExample {
    private val dataRef = AtomicReference<String>("Initial")
    
    fun updateData(newValue: String): Boolean {
        var current: String
        do {
            current = dataRef.get()
            val expected = current.uppercase()
            if (expected == newValue) {
                // 模拟 CAS 操作的条件
                if (dataRef.compareAndSet(current, newValue)) {
                    return true
                }
            }
        } while (true)
    }
    
    fun getData(): String = dataRef.get()
    
    // 更实际的例子：计数器
    private val counter = AtomicReference(0)
    
    fun incrementCounter(): Int {
        var current: Int
        var next: Int
        do {
            current = counter.get()
            next = current + 1
        } while (!counter.compareAndSet(current, next))
        return next
    }
    
    fun getCounter(): Int = counter.get()
}

suspend fun atomicReferenceExample() {
    val example = AtomicReferenceExample()
    val jobs = mutableListOf<Job>()
    
    repeat(100) {
        jobs.add(launch {
            example.incrementCounter()
        })
    }
    
    jobs.joinAll()
    println("Atomic counter result: ${example.getCounter()}")
}
```

#### `AtomicBoolean`, `AtomicInteger`
```kotlin
import java.util.concurrent.atomic.AtomicBoolean
import java.util.concurrent.atomic.AtomicInteger

class AtomicVariablesExample {
    private val flag = AtomicBoolean(false)
    private val counter = AtomicInteger(0)
    
    fun setFlag(value: Boolean): Boolean = flag.set(value)
    fun getFlag(): Boolean = flag.get()
    
    fun increment(): Int = counter.incrementAndGet()
    fun decrement(): Int = counter.decrementAndGet()
    fun getCounter(): Int = counter.get()
    
    // 原子复合操作
    fun incrementIfNotSet(): Boolean {
        if (!flag.get()) {
            if (flag.compareAndSet(false, true)) {
                counter.incrementAndGet()
                return true
            }
        }
        return false
    }
}

suspend fun atomicVariablesExample() {
    val example = AtomicVariablesExample()
    val jobs = mutableListOf<Job>()
    
    repeat(50) {
        jobs.add(launch {
            example.incrementIfNotSet()
        })
    }
    
    jobs.joinAll()
    println("Final flag: ${example.getFlag()}, counter: ${example.getCounter()}")
}
```

#### 原子操作 vs 锁性能对比
```kotlin
suspend fun performanceComparison() {
    val atomicCounter = AtomicInteger(0)
    val mutex = Mutex()
    var regularCounter = 0
    
    // 原子操作性能测试
    val atomicTime = measureTimeMillis {
        coroutineScope {
            repeat(10) { 
                launch {
                    repeat(1000) {
                        atomicCounter.incrementAndGet()
                    }
                }
            }
        }
    }
    
    // Mutex 性能测试
    val mutexTime = measureTimeMillis {
        coroutineScope {
            repeat(10) {
                launch {
                    repeat(1000) {
                        mutex.withLock {
                            regularCounter++
                        }
                    }
                }
            }
        }
    }
    
    println("Atomic operations time: ${atomicTime}ms")
    println("Mutex operations time: ${mutexTime}ms")
    println("Atomic counter: ${atomicCounter.get()}")
    println("Regular counter: $regularCounter")
}
```

### 4. Actor 模式

#### 封装状态的协程
```kotlin
// Actor 模式实现
sealed class AccountCommand {
    data class Deposit(val amount: Int) : AccountCommand()
    data class Withdraw(val amount: Int) : AccountCommand()
    data class GetBalance(val responseChannel: Channel<Int>) : AccountCommand()
}

class BankAccountActor {
    private val channel = Channel<AccountCommand>()
    
    init {
        // 启动 actor 协程
        launch(Dispatchers.Default) {
            var balance = 1000
            
            for (command in channel) {
                when (command) {
                    is AccountCommand.Deposit -> {
                        if (command.amount > 0) {
                            balance += command.amount
                        }
                    }
                    is AccountCommand.Withdraw -> {
                        if (command.amount > 0 && balance >= command.amount) {
                            balance -= command.amount
                        }
                    }
                    is AccountCommand.GetBalance -> {
                        command.responseChannel.send(balance)
                    }
                }
            }
        }
    }
    
    suspend fun deposit(amount: Int) {
        channel.send(AccountCommand.Deposit(amount))
    }
    
    suspend fun withdraw(amount: Int) {
        channel.send(AccountCommand.Withdraw(amount))
    }
    
    suspend fun getBalance(): Int {
        val responseChannel = Channel<Int>()
        channel.send(AccountCommand.GetBalance(responseChannel))
        return responseChannel.receive()
    }
}

suspend fun actorPatternExample() {
    val account = BankAccountActor()
    
    // 并发操作
    launch {
        repeat(10) {
            account.deposit(100)
            delay(10L)
        }
    }
    
    launch {
        repeat(5) {
            account.withdraw(50)
            delay(15L)
        }
    }
    
    delay(500L)
    println("Final balance: ${account.getBalance()}")
}
```

#### 状态管理最佳实践
```kotlin
// 更复杂的 Actor 示例：订单处理系统
sealed class OrderCommand {
    data class CreateOrder(val orderId: String, val items: List<String>) : OrderCommand()
    data class CancelOrder(val orderId: String) : OrderCommand()
    data class GetOrderStatus(val orderId: String, val responseChannel: Channel<OrderStatus?>) : OrderCommand()
}

enum class OrderStatus { PENDING, CONFIRMED, SHIPPED, CANCELLED }

class OrderProcessingActor {
    private val channel = Channel<OrderCommand>()
    private val orders = mutableMapOf<String, OrderStatus>()
    
    init {
        launch(Dispatchers.Default) {
            for (command in channel) {
                when (command) {
                    is OrderCommand.CreateOrder -> {
                        if (!orders.containsKey(command.orderId)) {
                            orders[command.orderId] = OrderStatus.PENDING
                            println("Created order: ${command.orderId}")
                        }
                    }
                    is OrderCommand.CancelOrder -> {
                        orders[command.orderId]?.let { currentStatus ->
                            if (currentStatus != OrderStatus.SHIPPED) {
                                orders[command.orderId] = OrderStatus.CANCELLED
                                println("Cancelled order: ${command.orderId}")
                            }
                        }
                    }
                    is OrderCommand.GetOrderStatus -> {
                        val status = orders[command.orderId]
                        command.responseChannel.send(status)
                    }
                }
            }
        }
    }
    
    suspend fun createOrder(orderId: String, items: List<String>) {
        channel.send(OrderCommand.CreateOrder(orderId, items))
    }
    
    suspend fun cancelOrder(orderId: String) {
        channel.send(OrderCommand.CancelOrder(orderId))
    }
    
    suspend fun getOrderStatus(orderId: String): OrderStatus? {
        val responseChannel = Channel<OrderStatus?>()
        channel.send(OrderCommand.GetOrderStatus(orderId, responseChannel))
        return responseChannel.receive()
    }
}

suspend fun orderActorExample() {
    val orderActor = OrderProcessingActor()
    
    // 创建订单
    orderActor.createOrder("ORD001", listOf("Item1", "Item2"))
    orderActor.createOrder("ORD002", listOf("Item3"))
    
    delay(100L)
    
    // 查询状态
    println("Order 1 status: ${orderActor.getOrderStatus("ORD001")}")
    println("Order 2 status: ${orderActor.getOrderStatus("ORD002")}")
    
    // 取消订单
    orderActor.cancelOrder("ORD001")
    println("Order 1 after cancellation: ${orderActor.getOrderStatus("ORD001")}")
}
```

#### 与其他并发模式比较
```kotlin
// 对比：共享状态 vs Actor 模式
class SharedStateCounter {
    private val mutex = Mutex()
    private var count = 0
    
    suspend fun increment() = mutex.withLock { count++ }
    suspend fun getCount(): Int = mutex.withLock { count }
}

// Actor 模式的计数器
sealed class CounterCommand {
    object Increment : CounterCommand()
    data class GetCount(val response: CompletableDeferred<Int>) : CounterCommand()
}

class ActorCounter {
    private val channel = Channel<CounterCommand>()
    
    init {
        launch {
            var count = 0
            for (cmd in channel) {
                when (cmd) {
                    is CounterCommand.Increment -> count++
                    is CounterCommand.GetCount -> cmd.response.complete(count)
                }
            }
        }
    }
    
    suspend fun increment() {
        channel.send(CounterCommand.Increment)
    }
    
    suspend fun getCount(): Int {
        val deferred = CompletableDeferred<Int>()
        channel.send(CounterCommand.GetCount(deferred))
        return deferred.await()
    }
}

suspend fun comparisonExample() {
    println("=== Shared State Approach ===")
    val sharedCounter = SharedStateCounter()
    coroutineScope {
        repeat(10) {
            launch { sharedCounter.increment() }
        }
    }
    println("Shared counter: ${sharedCounter.getCount()}")
    
    println("\n=== Actor Pattern Approach ===")
    val actorCounter = ActorCounter()
    coroutineScope {
        repeat(10) {
            launch { actorCounter.increment() }
        }
    }
    println("Actor counter: ${actorCounter.getCount()}")
}
```

### 5. 线程安全的数据结构

#### 线程安全的集合
```kotlin
// 使用 ConcurrentHashMap
import java.util.concurrent.ConcurrentHashMap

class ThreadSafeCollections {
    private val map = ConcurrentHashMap<String, String>()
    private val set = ConcurrentHashMap.newKeySet<String>()
    
    fun put(key: String, value: String) = map.put(key, value)
    fun get(key: String): String? = map[key]
    fun addSetItem(item: String) = set.add(item)
    fun getSetItems(): Set<String> = set.toSet()
}

// 使用协程友好的数据结构
class CoroutinesFriendlyStructures {
    // 使用 Mutex 保护普通集合
    private val mutex = Mutex()
    private val list = mutableListOf<String>()
    
    suspend fun addItem(item: String) = mutex.withLock {
        list.add(item)
    }
    
    suspend fun getItems(): List<String> = mutex.withLock {
        list.toList() // 返回副本
    }
    
    // 使用 Channel 作为队列
    private val queueChannel = Channel<String>(Channel.BUFFERED)
    
    suspend fun enqueue(item: String) {
        queueChannel.send(item)
    }
    
    suspend fun dequeue(): String? {
        return try {
            queueChannel.receive()
        } catch (e: Exception) {
            null
        }
    }
}
```

#### 并发友好的设计模式
```kotlin
// 不可变数据优先
data class ImmutableUser(
    val id: String,
    val name: String,
    val email: String,
    val roles: List<String> = emptyList()
) {
    fun withName(newName: String) = copy(name = newName)
    fun withEmail(newEmail: String) = copy(email = newEmail)
    fun addRole(role: String) = copy(roles = roles + role)
}

// 使用 StateFlow 管理状态
import kotlinx.coroutines.flow.StateFlow
import kotlinx.coroutines.flow.MutableStateFlow
import kotlinx.coroutines.flow.asStateFlow

class UserManager {
    private val _users = MutableStateFlow<List<ImmutableUser>>(emptyList())
    val users: StateFlow<List<ImmutableUser>> = _users.asStateFlow()
    
    fun addUser(user: ImmutableUser) {
        _users.value = _users.value + user
    }
    
    fun updateUser(updatedUser: ImmutableUser) {
        _users.value = _users.value.map { user ->
            if (user.id == updatedUser.id) updatedUser else user
        }
    }
    
    fun removeUser(userId: String) {
        _users.value = _users.value.filter { it.id != userId }
    }
}

suspend fun immutableDesignExample() {
    val userManager = UserManager()
    
    // 观察用户变化
    launch {
        userManager.users.collect { users ->
            println("Current users: ${users.size}")
        }
    }
    
    // 修改用户
    val user1 = ImmutableUser("1", "Alice", "alice@example.com")
    userManager.addUser(user1)
    
    delay(100L)
    val updatedUser1 = user1.withName("Alice Smith")
    userManager.updateUser(updatedUser1)
    
    delay(100L)
    userManager.removeUser("1")
    
    delay(200L)
}
```

#### 性能考虑因素
```kotlin
suspend fun performanceConsiderations() {
    // 1. 避免过度同步
    class OverSyncExample {
        private val mutex = Mutex()
        private var data = 0
        
        // 不好的做法：读操作也加锁
        suspend fun badGetData(): Int = mutex.withLock { data }
        
        // 好的做法：使用 StateFlow
        private val _state = MutableStateFlow(0)
        val state: StateFlow<Int> = _state.asStateFlow()
        
        suspend fun goodUpdate() {
            _state.value = _state.value + 1
        }
    }
    
    // 2. 减少锁的持有时间
    class ReducedLockTime {
        private val mutex = Mutex()
        private val data = mutableListOf<String>()
        
        // 不好的做法：长时间持有锁
        suspend fun badMethod(items: List<String>) = mutex.withLock {
            // 模拟长时间操作
            delay(1000L)
            data.addAll(items)
        }
        
        // 好的做法：最小化锁持有时间
        suspend fun goodMethod(items: List<String>) {
            val processedItems = processItems(items) // 在锁外处理
            mutex.withLock {
                data.addAll(processedItems)
            }
        }
        
        private suspend fun processItems(items: List<String>): List<String> {
            delay(1000L) // 模拟处理
            return items.map { it.uppercase() }
        }
    }
    
    // 3. 使用无锁数据结构（当适用时）
    class LockFreeStructure {
        private val atomicList = AtomicReference<List<String>>(emptyList())
        
        fun addItem(item: String) {
            var current: List<String>
            var next: List<String>
            do {
                current = atomicList.get()
                next = current + item
            } while (!atomicList.compareAndSet(current, next))
        }
        
        fun getItems(): List<String> = atomicList.get()
    }
}
```

### 6. 实践建议

#### 何时使用共享状态
```kotlin
// 适合使用共享状态的场景
class SuitableForSharedState {
    // 1. 简单的计数器或标志
    private val counter = AtomicInteger(0)
    
    fun increment() = counter.incrementAndGet()
    
    // 2. 缓存（读多写少）
    private val cacheMutex = Mutex()
    private val cache = mutableMapOf<String, String>()
    
    suspend fun getCached(key: String): String? = cacheMutex.withLock {
        cache[key]
    }
    
    suspend fun putCached(key: String, value: String) = cacheMutex.withLock {
        cache[key] = value
    }
    
    // 3. 配置管理（很少修改）
    private val configMutex = Mutex()
    private var config = AppConfiguration()
    
    suspend fun updateConfig(newConfig: AppConfiguration) = configMutex.withLock {
        config = newConfig
    }
    
    suspend fun getConfig(): AppConfiguration = configMutex.withLock {
        config.copy() // 返回副本
    }
}

data class AppConfiguration(
    val timeoutMs: Long = 5000,
    val maxRetries: Int = 3,
    val enabledFeatures: Set<String> = emptySet()
)
```

#### 不可变数据优先原则
```kotlin
// 推荐：不可变数据结构
data class Transaction(
    val id: String,
    val amount: Double,
    val timestamp: Long = System.currentTimeMillis(),
    val status: Status = Status.PENDING
) {
    enum class Status { PENDING, PROCESSING, COMPLETED, FAILED }
    
    fun complete() = copy(status = Status.COMPLETED)
    fun fail() = copy(status = Status.FAILED)
}

// 管理不可变对象的集合
class TransactionManager {
    private val transactions = MutableStateFlow<List<Transaction>>(emptyList())
    
    fun addTransaction(transaction: Transaction) {
        transactions.value = transactions.value + transaction
    }
    
    fun completeTransaction(id: String) {
        transactions.value = transactions.value.map { tx ->
            if (tx.id == id && tx.status == Transaction.Status.PENDING) {
                tx.complete()
            } else {
                tx
            }
        }
    }
    
    fun getTransactions() = transactions.value
}
```

#### 测试并发代码的方法
```kotlin
import kotlinx.coroutines.test.*
import org.junit.Test
import kotlin.test.assertEquals

// 测试并发代码的示例
class ConcurrencyTesting {
    @Test
    fun testConcurrentCounter() = runTest {
        val counter = AtomicCounter()
        
        // 使用 TestScope 进行并发测试
        val jobs = List(10) { 
            async {
                repeat(100) {
                    counter.increment()
                }
            }
        }
        
        jobs.awaitAll()
        assertEquals(1000, counter.getCount())
    }
    
    @Test
    fun testRaceConditionDetection() = runTest {
        val counter = Counter()
        
        // 运行多次来检测竞态条件
        repeat(10) {
            val jobs = List(10) { 
                async {
                    repeat(10) {
                        counter.increment()
                    }
                }
            }
            jobs.awaitAll()
            // 如果存在竞态条件，结果可能不总是 100
            if (counter.count != 100) {
                println("Race condition detected! Count: ${counter.count}")
            }
            counter.count = 0 // 重置用于下次测试
        }
    }
}

// 使用超时来测试死锁
@Test
fun testNoDeadlock() = runTest {
    withTimeout(5000L) { // 5秒超时
        val example = MutexExample()
        
        // 可能导致死锁的操作
        launch {
            example.addItem(1)
        }
        
        launch {
            delay(100L)
            example.removeItem()
        }
        
        delay(1000L) // 等待操作完成
    }
}
```
这是一个为您完善的 Kotlin **注解 (Annotations)** 部分的大纲。考虑到 Kotlin 的特性（如与 Java 的互操作性、编译时处理、反射等），这份大纲从基础语法到高级应用进行了系统化的梳理，适合用于技术文档、教程或内部培训材料。

---
# Kotlin 注解 (Annotations) 
## 1. 基础概念

### 1.1 什么是注解？
**定义**：
注解（Annotation）是一种元数据（Metadata），它嵌入在代码中，为编译器、运行时环境或开发工具提供关于代码的额外信息。

**核心特征**：
1. **非侵入性**：注解本身不包含业务逻辑，不会直接改变程序的执行流程（除非配合反射或编译时处理）。
2. **声明式**：它告诉系统“这是什么”或“这应该被如何处理”，而不是“怎么做”。

**作用场景**：
- **编译器检查**：如 `@Suppress` 抑制警告，`@Deprecated` 标记过时 API。
- **运行时行为**：如 Spring 的 `@Autowired` 进行依赖注入，JUnit 的 `@Test`识别测试方法。
- **代码生成**：如 Room 数据库通过 `@Entity` 生成 DAO 实现类，Moshi/Kotlinx Serialization 通过 `@Serializable` 生成序列化代码。
- **文档生成**：如 `@Since` 或自定义文档标签。

### 1.2 Kotlin 注解 vs Java 注解

虽然 Kotlin 运行在 JVM 上且与 Java 高度互操作，但在注解的定义和使用上有显著差异：

| 特性 | Java | Kotlin |
| :--- | :--- | :--- |
| **定义关键字** | `@interface` | `annotation class` |
| **默认保留策略** | `CLASS` (编译期保留) | `RUNTIME` (注意：Kotlin 早期版本默认不同，但现在通常建议显式指定。实际上 Kotlin 编译器默认将注解保留在字节码中，但若要反射获取需 `RUNTIME`) *更正：Kotlin 中若无 `@Retention`，默认为 `RUNTIME` 吗？不，Kotlin 默认是 `RUNTIME` 仅当用于反射时方便，但标准行为需看具体实现。实际上，Kotlin 注解如果没有指定 `@Retention`，默认是 `RUNTIME` 以便在 Kotlin 反射中使用，但在 Java 反射中可能不可见除非指定。为了安全，始终显式指定。* <br> **准确说法**：Kotlin 中未指定 `@Retention` 时，默认行为取决于上下文，但通常为了兼容性，建议显式声明。Java 默认是 `CLASS`。 |
| **数组语法** | `{ "A", "B" }` | `arrayOf("A", "B")` 或 `["A", "B"]` |
| **属性映射** | 自动映射到字段/方法 | 需要 **Use-site Targets** (`@field:`, `@get:`) 来明确指定目标 |

**互操作性**：
- Kotlin 定义的注解可以在 Java 中使用，Java 定义的注解也可以在 Kotlin 中使用。
- Kotlin 编译器会自动处理大部分桥接问题，例如将 Kotlin 的 `val` 属性生成的 getter 方法暴露给 Java 注解处理器。

---

## 2. 声明注解

### 2.1 基本语法
在 Kotlin 中，注解是一个特殊的类，使用 `annotation class` 关键字声明。

```kotlin
// 最简单的注解，没有任何参数
annotation class Fancy
```

### 2.2 注解构造函数参数
注解可以像普通类一样拥有主构造函数，用于传递配置信息。

**支持的参数类型**：
1. 对应于 Java 基本类型的 Kotlin 类型 (`Int`, `Long`, `Short`, `Float`, `Double`, `Boolean`, `Byte`, `Char`)。
2. `String`
3. `Class` 引用 (如 `String::class`)
4. 枚举 (`enum`)
5. 其他注解
6. 上述类型的数组 (`Array<T>`)

**重要限制**：
- 注解参数不能有默认值以外的复杂逻辑。
- 参数必须是 `val` (不可变)，因为注解实例在编译后是常量。

**示例**：
```kotlin
annotation class ReplaceWith(
    val expression: String, 
    val imports: Array<String> = [] // 支持默认值
)

// 使用枚举
enum class Level { LOW, HIGH }

annotation class Priority(val level: Level)
```

### 2.3 注解目标 (Use-site Targets) —— Kotlin 的核心特性

这是 Kotlin 注解中最容易混淆但也最强大的部分。

**为什么需要它？**
在 Java 中，一个字段通常对应一个成员变量。但在 Kotlin中，一个属性 (`var name: String`) 在编译成字节码时可能对应多个 Java 元素：
1. 一个私有字段 (`private String name`)
2. 一个 getter 方法 (`public String getName()`)
3. 一个 setter 方法 (`public void setName(String)`)

当你写 `@MyAnnotation var name: String` 时，编译器不知道你想把这个注解加在字段上、getter 上还是 setter 上。

**语法**：
`@target:AnnotationName`

**常用目标详解**：

| 目标 | 说明 | 适用场景 |
| :--- | :--- | :--- |
| `@field` | 应用于生成的 Java 字段 | JPA/Hibernate 映射字段，Gson 序列化字段名 |
| `@get` | 应用于 Getter 方法 | Jackson 序列化 Getter，Bean 验证 |
| `@set` | 应用于 Setter 方法 | 权限控制，Setter 验证 |
| `@param` | 应用于构造函数参数 | Spring 构造器注入，Swagger 参数描述 |
| `@property` | 应用于 Kotlin 属性本身 | **仅在 Kotlin 反射中可见**，Java 反射不可见 |
| `@receiver` | 应用于扩展函数的接收者 | 扩展函数文档或特定处理 |
| `@setparam` | 应用于 Setter 的参数 | 较少用，针对 Setter 传入参数的注解 |

**实战示例**：

```kotlin
import com.google.gson.annotations.SerializedName
import javax.persistence.Column

class User {
    // 场景1: Gson 需要注解在字段上才能正确序列化私有字段
    @field:SerializedName("user_name")
    var userName: String = ""

    // 场景2: JPA 需要注解在字段上定义列名
    @field:Column(name = "email_addr")
    var email: String = ""
    
    // 场景3: 如果你想让 Java 代码通过 Getter 看到某个注解
    @get:Deprecated("Use fullName instead")
    val name: String get() = "$userName"
}
```

---

## 3. 注解元数据 (Meta-Annotations)

元注解是用来修饰“注解”的注解。Kotlin 复用了 Java 的元注解体系，但提供了更友好的枚举类型。

### 3.1 `@Target`
限制注解可以使用的位置。如果不指定，默认可以在任何地方使用。

```kotlin
import kotlin.annotation.AnnotationTarget.*

@Target(CLASS, FUNCTION, PROPERTY_GETTER)
annotation class MyRestrictedAnnotation
```
*如果尝试将 `@MyRestrictedAnnotation` 用在局部变量上，编译器会报错。*

### 3.2 `@Retention`
决定注解的生命周期。

```kotlin
import kotlin.annotation.AnnotationRetention.*

@Retention(SOURCE)   // 源码级：编译后丢弃。用于 lint 检查、代码生成提示。
@Retention(BINARY)   // 字节码级：保留在 .class 文件中，但运行时反射不可见。用于编译时检查。
@Retention(RUNTIME)  // 运行时级：保留在 .class 文件中，且可通过反射读取。用于框架动态处理。
```

**关键点**：
- 如果你希望在使用 `kotlin-reflect` 或 Java Reflection 时读到注解，**必须**使用 `RUNTIME`。
- 很多初学者忘了加这个，导致 `findAnnotation` 返回 null。

### 3.3 `@Repeatable`
允许在同一元素上重复使用同一个注解。

**Kotlin 1.6 之前**：
需要创建一个容器注解（Container Annotation），非常麻烦。

**Kotlin 1.6+**：
直接添加 `@Repeatable` 即可。

```kotlin
@Repeatable
annotation class Tag(val name: String)

@Tag("Frontend")
@Tag("Critical")
class HomePage
```
*底层原理：编译器会自动生成一个包含 `Tag` 数组的容器注解，保持对旧版 Java 工具的兼容。*

### 3.4 `@MustBeDocumented`
指示该注解应包含在生成的 KDoc 或 JavaDoc 公共 API 文档中。通常用于库开发者，表明该注解是公开 API 契约的一部分。

---

## 4. 使用注解

### 4.1 基本使用位置
- 类、接口、对象
- 函数、构造函数
- 属性（Val/Var）
- 参数
- 表达式（局部变量、lambda 参数等，需配合 `@Target(EXPRESSION)`）

### 4.2 数组参数传递
Kotlin 提供了两种传递数组参数的语法，推荐使用方括号语法，更简洁。

```kotlin
annotation class Filters(val values: Array<String>)

// 方式1: 传统 arrayOf
@Filters(arrayOf("admin", "user"))

// 方式2: 方括号语法 (Kotlin 1.2+, 推荐)
@Filters(["admin", "user"])
```

### 4.3 注解作为类型 (Type Annotations)
注解可以放在类型前面，而不是声明前面。这主要用于静态分析工具。

```kotlin
// 这里的 NotNull 注解作用于 List 类型本身，而不是变量 myList
val myList: @NotNull List<String> = listOf("a")
```
*这在 Kotlin 中较少手动编写，通常由编译器或工具自动生成，用于增强空安全检查。*

---

## 5. 运行时处理：反射 (Reflection)

### 5.1 环境准备
要在运行时读取注解，你需要：
1. 注解必须标记为 `@Retention(AnnotationRetention.RUNTIME)`。
2. 项目依赖 `kotlin-reflect` 库。
   ```groovy
   implementation "org.jetbrains.kotlin:kotlin-reflect:$kotlin_version"
   ```

### 5.2 核心 API
Kotlin 反射 API (`kotlin.reflect`) 比 Java 反射更强大，因为它能区分 `property`、`getter` 等 Kotlin 特有概念。

- `KClass<T>.annotations`: 获取类上的所有注解。
- `KProperty<T>.annotations`: 获取属性上的注解。
- `KFunction<T>.annotations`: 获取函数上的注解。
- `T::class.findAnnotation<A>()`: 查找特定类型的注解（返回 nullable）。
- `T::class.getAnnotation<A>()`: 查找特定类型的注解（若不存在抛异常）。

### 5.3 实战：自定义验证框架

这是一个模拟 Spring Validation 或 Hibernate Validator 的简单实现。

```kotlin
import kotlin.reflect.full.findAnnotation
import kotlin.reflect.full.memberProperties

// 1. 定义注解
@Retention(AnnotationRetention.RUNTIME)
@Target(AnnotationTarget.PROPERTY)
annotation class NotNull

@Retention(AnnotationRetention.RUNTIME)
@Target(AnnotationTarget.PROPERTY)
annotation class MinLength(val value: Int)

// 2. 定义数据类
data class User(
    @field:NotNull // 注意：这里为了演示反射读取 property，通常用 @property:NotNull 更准确，
                   // 但如果我们要通过 Java 互操作或通用反射，可能需要根据具体情况选择 target。
                   // 在 Kotlin 反射中，@property: 是最直接的。
    @property:NotNull
    val id: String?,

    @property:MinLength(6)
    val password: String
)

// 3. 验证引擎
fun validate(obj: Any) {
    val kClass = obj::class
    val errors = mutableListOf<String>()

    for (prop in kClass.memberProperties) {
        // 检查 NotNull
        if (prop.findAnnotation<NotNull>() != null) {
            prop.isAccessible = true // 允许访问私有属性
            if (prop.get(obj) == null) {
                errors.add("${prop.name} cannot be null")
            }
        }

        // 检查 MinLength
        val minLength = prop.findAnnotation<MinLength>()
        if (minLength != null) {
            prop.isAccessible = true
            val value = prop.get(obj) as? String
            if (value != null && value.length < minLength.value) {
                errors.add("${prop.name} length must be at least ${minLength.value}")
            }
        }
    }

    if (errors.isNotEmpty()) {
        throw IllegalArgumentException("Validation failed:\n${errors.joinToString("\n")}")
    }
}

fun main() {
    try {
        validate(User(null, "123"))
    } catch (e: Exception) {
        println(e.message)
    }
}
```

### 5.4 性能考量
- **反射很慢**：每次调用 `findAnnotation` 或 `getter.call()` 都涉及大量的对象创建和方法查找。
- **优化策略**：
    1. **缓存**：将类的注解信息和属性访问器缓存起来（例如使用 `ConcurrentHashMap`）。
    2. **代码生成**：对于高性能要求的场景（如 JSON 序列化），应避免运行时反射，转而使用 **KSP** 或 **KAPT** 在编译期生成具体的读写代码。

---

## 6. 编译时处理：KSP 与 KAPT

这是现代 Kotlin 开发的分水岭。

### 6.1 KAPT (Kotlin Annotation Processing Tool)
- **原理**：KAPT 是 Java Annotation Processing (JSR 269) 的适配器。它先生成 Java  stubs（桩代码），然后让 Java 注解处理器处理这些 stubs。
- **缺点**：
    - **慢**：生成 stubs 增加了编译时间。
    - **信息丢失**：Stub 是 Java 代码，无法完美表达 Kotlin 特性（如 data class 的 componentN, sealed classes, companion objects 的具体细节）。
    - **增量编译差**：往往导致全量编译。
- **现状**：维护模式。除非你使用的库（如旧版 Dagger 2）只支持 KAPT，否则不建议在新模块中使用。

### 6.2 KSP (Kotlin Symbol Processing)
- **原理**：Google 推出的专为 Kotlin 设计的轻量级 API。它直接读取 Kotlin 编译器的前端符号表，无需生成 Java stubs。
- **优点**：
    - **快**：编译速度显著提升（官方数据称比 KAPT 快 2 倍以上）。
    - **原生支持**：直接理解 Kotlin 的所有语言特性。
    - **增量编译友好**：更好地支持 Gradle 的增量编译。
- **如何工作**：
    1. 开发者编写一个 `SymbolProcessor`。
    2. 在编译过程中，KSP 遍历代码符号。
    3. Processor 根据注解生成新的 Kotlin/Java 文件。
    4. 这些生成的文件参与后续编译。

### 6.3 选择指南

| 场景 | 推荐方案 |
| :--- | :--- |
| 新启动的项目 | **KSP** |
| 需要编写自定义代码生成库 | **KSP** |
| 依赖库仅支持 KAPT (如 Dagger 2 < 2.40) | **KAPT** (被迫) |
| 仅需运行时反射，不生成代码 | **无需处理器** (仅用 Reflection) |
| 简单的编译期检查 (不生成代码) | **KSP** 或 **Compiler Plugin** |

*注：Dagger 2.40+ 和 Hilt 已经支持 KSP。Room 2.5+ 也强烈推荐 KSP。*

---

## 7. 高级主题与最佳实践

### 7.1 注解继承
- **默认行为**：Kotlin 注解**不会**被子类继承。
- **Java 互操作**：如果在 Java 中定义了 `@Inherited` 的注解，Kotlin 子类在通过 Java 反射查看时可能表现出继承性，但在 Kotlin 反射 (`kotlin-reflect`) 中，行为可能不一致。
- **建议**：不要依赖注解继承。如果需要多态行为，建议在运行时递归检查父类或接口上的注解。

### 7.2 文件级注解
有些注解适用于整个文件，而不是单个类。
- **语法**：必须放在文件最顶部，`package` 语句之前。
- **常见用例**：
    - `@file:JvmName("MyUtils")`: 改变生成的 Java 类名。
    - `@file:JvmMultifileClass`: 将多个文件的顶层函数合并到一个 Java 类中。
    - `@file:Suppress("unused")`: 抑制整个文件的警告。

```kotlin
@file:JvmName("StringExtensions")
@file:Suppress("NOTHING_TO_INLINE")

package com.example.utils

fun String.isEmpty(): Boolean { ... }
```

### 7.3 最佳实践总结

1. **显式声明 Retention**：永远不要依赖默认值。问自己：“这个注解需要在运行时被读取吗？”如果是，加 `@Retention(RUNTIME)`；如果只是给编译器看，加 `@Retention(SOURCE)` 或 `BINARY`。
2. **限制 Target**：使用 `@Target` 限制注解的使用范围，防止用户误用（例如把一个只用于类的注解用在了函数上）。
3. **文档化**：为注解类编写清晰的 KDoc，说明每个参数的含义和使用示例。
4. **优先 KSP**：如果你正在构建一个需要生成代码的库（如 ORM、Router、DI），请使用 KSP。它是未来。
5. **避免反射滥用**：在 Android 或高性能服务端应用中，尽量避免在热点路径上使用反射读取注解。考虑在应用启动时一次性扫描并缓存，或者直接使用 KSP 生成静态代码。
6. **Use-site Target 清晰化**：当注解用于属性时，始终明确写出 `@field:` 或 `@get:`，即使编译器能推断，显式写出也能提高代码可读性并避免潜在的互操作 bug。

## 8. 常见内置注解速查
- `@JvmStatic`: 在伴生对象中生成静态方法。
- `@JvmOverloads`: 为带默认参数的函数生成重载方法。
- `@JvmField`: 暴露属性为公共字段，无 getter/setter。
- `@Throws`: 声明函数可能抛出的异常（用于 Java 互操作）。
- `@Suppress`: 抑制编译器警告。
- `@Deprecated`: 标记弃用，可指定替换方案 (`ReplaceWith`)。
- `@Volatile`: 对应 Java 的 `volatile` 关键字。
- `@Synchronized`: 对应 Java 的 `synchronized` 方法。


# Kotlin 解构声明 

## 1. 简介与核心概念

### 什么是解构声明？
解构声明是一种语法糖，允许我们将一个复合对象（如数据类、Pair、Map Entry等）一次性“分解”为多个独立的变量。

*   **直观理解**：就像拆开一个包裹，把里面的东西直接拿出来放在桌面上，而不是抱着整个包裹操作。
*   **代码对比**：
    ```kotlin
    // 传统方式
    val name = person.name
    val age = person.age

    // 解构方式
    val (name, age) = person
    ```

### 为什么使用它？
1.  **简洁性**：大幅减少样板代码，特别是在处理多返回值或遍历 Map 时。
2.  **可读性**：在上下文清晰时，`val (x, y) = point` 比 `point.x` 和 `point.y` 更直观地表达了“提取坐标”的意图。
3.  **函数式风格友好**: 在 Lambda 表达式中解构参数是 Kotlin 函数式编程的一大特色。

---

## 2. 基础语法

###基本形式
```kotlin
data class Person(val name: String, val age: Int)

fun main() {
    val person = Person("Alice", 25)
    
    // 声明两个变量 name 和 age，分别初始化为 person.component1() 和 person.component2()
    val (name, age) = person
    
    println("$name is $age years old")
}
```

### 忽略不需要的变量 (`_`)
如果你只关心对象中的部分属性，可以使用下划线 `_` 跳过其他位置。
```kotlin
val (name, _) = person // 只获取 name，忽略 age
// 注意：被忽略的属性对应的 componentN()方法仍然会被调用，但结果被丢弃。
```

### 类型推断与显式声明
通常编译器可以推断类型，但在需要明确类型或进行类型转换时可以显式声明。
```kotlin
// 显式声明类型
val (name: String, age: Int) = person

// 如果 componentN 返回的是 Any?，可能需要强制转换或智能转换
val (key, value) = mapEntry // key: K, value: V
```

### 在已有变量上赋值
解构不仅可以用于声明新变量，还可以用于给已存在的变量赋值（需配合 `var`）。
```kotlin
var x = 0
var y = 0
val point = Point(10, 20)

(x, y) = point // 更新现有变量
```

---

## 3. 工作原理：`componentN()` 函数

这是解构声明的核心机制。**解构声明不是魔法，而是编译器的转换规则。**

### 编译器转换机制
当你写 `val (a, b) = obj` 时，编译器实际上将其转换为：
```kotlin
val a = obj.component1()
val b = obj.component2()
```
当你写 `val (a, b, c) = obj` 时：
```kotlin
val a = obj.component1()
val b = obj.component2()
val c = obj.component3()
```

### 约定规范 (Convention)
为了让一个类支持解构，它必须提供名为 `componentN()` 的函数，并且这些函数必须标记为 `operator`。
*   `component1()`: 返回第一个分量
*   `component2()`: 返回第二个分量
*   ...以此类推

**限制**：
*   Kotlin 标准库默认支持到 `component5`。
*   如果需要解构更多字段，可以自定义扩展函数 `component6()`, `component7()` 等，但通常建议不要解构超过 5 个变量，这会降低可读性。

---

## 4. 内置支持解构的类型

Kotlin 标准库中许多常用类型已经内置了解构支持。

### 1. Data Classes (数据类)
这是最常见的场景。Kotlin 编译器会自动为数据类主构造函数中声明的所有属性生成 `componentN()` 函数。

```kotlin
data class User(val id: Long, val name: String, val email: String)

// 自动生成了:
// operator fun component1() = id
// operator fun component2() = name
// operator fun component3() = email

val (id, name, email) = User(1L, "Bob", "bob@example.com")
```
*   **注意**：只有**主构造函数**中的属性参与解构。类体中定义的属性不会生成 component 函数。

### 2. Pair 和 Triple
用于函数返回多个值时的轻量级容器。
*   `Pair<A, B>`: 提供 `component1()` (first) 和 `component2()` (second)。
*   `Triple<A, B, C>`: 提供 `component1()`, `component2()`, `component3()`。

```kotlin
fun getCoordinates(): Pair<Double, Double> {
    return Pair(40.7128, -74.0060)
}

val (lat, lon) = getCoordinates()
```

### 3. Maps (映射)
在遍历 Map 时，每个元素是一个 `Map.Entry<K, V>` 对象，它支持解构为 key 和 value。

```kotlin
val map = mapOf("Apple" to 1, "Banana" to 2)

for ((key, value) in map) {
    println("$key costs $value dollars")
}
```

### 4. Arrays 和 Lists (有限支持)
Kotlin 标准库为 `List` 和 `Array` 提供了扩展函数 `component1()` 到 `component5()`，分别对应索引 0 到 4 的元素。

```kotlin
val list = listOf("A", "B", "C", "D", "E")
val (first, second, third) = list // first="A", second="B", third="C"

// 如果列表长度不足，会抛出 IndexOutOfBoundsException
// val (a, b, c, d, e, f) = list // 错误！List 只支持到 component5
```
*   **警告**：对 List/Array 使用解构时要确保集合大小足够，否则运行时崩溃。

---

## 5. 高级用法与自定义解构

### 为非 Data Class 添加解构支持
你可以为任何类（包括第三方库的类、Android SDK 类等）通过**扩展函数**添加解构能力。

**示例：为 Android 的 `Point` 添加解构**
```kotlin
import android.graphics.Point

operator fun Point.component1() = x
operator fun Point.component2() = y

// 使用
val point = Point(100, 200)
val (x, y) = point
```

**示例：为 Java 的 `Map.Entry` 添加额外解构（假设需要）**
虽然 `Map.Entry` 已经支持 `(key, value)`，但如果你想解构出其他计算值，也可以自定义。

### 在 Lambda 表达式中使用解构
这是解构声明最强大的场景之一，特别是在高阶函数中。

**1. Map 遍历**
```kotlin
map.forEach { (key, value) ->
    println("$key -> $value")
}
```

**2. 列表元素解构**
如果列表中包含支持解构的对象（如 Pair 或 Data Class）：
```kotlin
val users = listOf(User(1, "Alice"), User(2, "Bob"))

users.map { (id, name) -> 
    "$id: $name" 
}
```

**3. 复杂 Lambda 参数**
```kotlin
// 假设有一个函数接收 List<Pair<String, Int>>
fun process(data: List<Pair<String, Int>>) {
    data.forEach { (label, count) ->
        println("$label has $count items")
    }
}
```

### 嵌套解构 (Nested Destructuring)
如果对象的属性本身也是可解构的，可以进行嵌套解构。

```kotlin
data class Address(val city: String, val zip: String)
data class Person(val name: String, val address: Address)

val person = Person("Alice", Address("New York", "10001"))

// 嵌套解构
val (name, (city, zip)) = person

println(name)   // Alice
println(city)   // New York
println(zip)    // 10001
```
*   **注意**：嵌套解构要求内部对象也必须支持解构（即有 componentN 函数）。

---

## 6. 常见应用场景

### 1. 函数多返回值
避免创建专门的 DTO 类来返回两个或三个值。
```kotlin
fun divide(a: Int, b: Int): Pair<Int, Int> {
    return Pair(a / b, a % b)
}

val (quotient, remainder) = divide(10, 3)
```

### 2. 状态管理 (State Management)
在 Android Jetpack Compose 或 Redux 架构中，常用来解构状态对象。
```kotlin
data class UiState(val isLoading: Boolean, val data: String?, val error: String?)

@Composable
fun MyScreen(uiState: UiState) {
    val (isLoading, data, error) = uiState
    
    if (isLoading) CircularProgressIndicator()
    else if (error != null) Text(error)
    else Text(data ?: "")
}
```

### 3. 交换变量值
虽然 Kotlin 没有原生的 swap 语法，但可以利用解构和 `also` 或临时 Pair 实现。
```kotlin
var a = 1
var b = 2

// 方法 1: 使用 also (推荐，无额外对象分配)
b = a.also { a = b }

// 方法 2: 使用解构 (创建了一个临时 Pair，略有开销)
val pair = Pair(b, a)
a = pair.first
b = pair.second
// 或者更简洁地：
run {
    val (newA, newB) = Pair(b, a)
    a = newA
    b = newB
}
```
*注：方法 1 更高效，方法 2 展示了解构的概念应用。*

### 4. 解析结构化数据
在处理 JSON 解析后的对象或数据库游标时，快速提取字段。

---

## 7. 最佳实践与注意事项

### ✅ 最佳实践
1.  **可读性优先**：如果解构后的变量名不能清晰表达含义，请使用普通访问器。
    *   好：`val (latitude, longitude) = location`
    *   坏：`val (a, b) = location`
2.  **限制解构数量**：尽量不超过 3-4 个变量。如果超过，考虑是否应该拆分对象或只提取需要的字段。
3.  **使用 `_` 忽略无用值**：这不仅节省命名精力，还向读者表明该值被有意忽略。
4.  **在 Lambda 中广泛使用**：在 `forEach`, `map`, `filter` 等操作符中解构参数是 Kotlin 的惯用写法。

### ⚠️ 注意事项
1.  **性能考量**：
    *   对于 Data Class，`componentN()` 通常是内联的，几乎没有开销。
    *   对于 `Pair`/`Triple`，它们是不可变对象，解构不会创建新对象，只是引用赋值。
    *   对于 `List`/`Array` 的解构，每次调用 `componentN()` 都是一次数组访问，开销极小，但要警惕越界异常。
2.  **空安全 (Null Safety)**：
    *   如果对象本身可能为 null，必须先处理 null。
    ```kotlin
    val person: Person? = getPerson()
    
    // 错误：person 可能为 null
    // val (name, age) = person 
    
    // 正确：使用 let 或 ?:
    person?.let { (name, age) ->
        println(name)
    }
    
    // 或者提供默认值
    val (name, age) = person ?: Person("Unknown", 0)
    ```
3.  **Val vs Var**：
    *   解构声明中的变量可以是 `val`（不可变）或 `var`（可变），根据后续是否需要修改来决定。

---

## 8. 常见陷阱与误区

### ❌ 陷阱 1：Data Class 构造函数顺序变更
这是最大的风险点。
```kotlin
// 版本 1
data class Config(val host: String, val port: Int)
val (host, port) = config

// 版本 2：开发者调整了构造函数顺序
data class Config(val port: Int, val host: String) 
// 此时，原来的解构代码 val (host, port) = config 
// 会导致 host 被赋值为 port 的值，port 被赋值为 host 的值！
// 编译器不会报错，因为类型可能兼容（如都是 String/Int 或都是 String），导致静默 Bug。
```
*   **建议**：在公共 API 库中，谨慎依赖 Data Class 的解构顺序。如果顺序可能变化，建议使用命名参数访问（`config.host`）。

### ❌ 陷阱 2：过度解构导致上下文丢失
```kotlin
// 糟糕的代码
val (a, b, c, d, e) = complexObject
doSomething(a, b, c, d, e)
// 读者不知道 a, b, c, d, e 代表什么，必须跳回去看 complexObject 的定义。
```
*   **建议**：如果变量含义不明显，请使用 `complexObject.propA` 等形式，或者重命名解构变量（如果语言支持别名，但 Kotlin 解构不支持直接别名，只能声明后赋值）。

### ❌ 陷阱 3：混淆解构与 Copy
*   **解构**是**读取**操作：`val (x, y) = point`
*   **Copy**是**写入/创建**操作：`val newPoint = point.copy(x = 10)`
*   不要试图通过解构来修改数据类的属性，因为数据类通常是不可变的（val）。

### ❌ 陷阱 4：List 解构越界
```kotlin
val list = listOf(1, 2)
val (a, b, c) = list // 运行时崩溃：IndexOutOfBoundsException
```
*   **建议**：只对已知大小的集合或使用 `getOrNull` 配合手动赋值，避免对动态大小的 List 使用超过其潜在最小尺寸的解构。

---

# Kotlin 反射

## 1. 基础概念与环境准备

### 1.1 什么是反射？

**定义**：
反射（Reflection）是一种机制，允许程序在**运行时（Runtime）**动态地获取类的信息（如类名、属性、方法、构造函数、注解等），并能够动态地创建对象、调用方法或访问/修改字段，而无需在编译时硬编码这些细节。

**Kotlin 反射 vs Java 反射**：

虽然 Kotlin 运行在 JVM 上，最终字节码与 Java 兼容，但 Kotlin 语言特性（如空安全、默认参数、扩展函数、委托属性）在 Java 反射 API (`java.lang.reflect`) 中无法直接体现或处理起来非常繁琐。因此，Kotlin 提供了自己的反射库 `kotlin-reflect`。

| 特性 | Java 反射 (`java.lang.reflect`) | Kotlin 反射 (`kotlin.reflect`) |
| :--- | :--- | :--- |
| **核心类** | `Class<?>`, `Field`, `Method`, `Constructor` | `KClass<T>`, `KProperty`, `KFunction`, `KConstructor` |
| **空安全** | 无法区分 `String` 和 `String?` | `KType.isMarkedNullable` 明确标识可空性 |
| **默认参数** | 难以处理，需手动计算参数索引 | `callBy(map)` 原生支持命名参数和默认值 |
| **扩展函数** | 视为静态方法，丢失“扩展”语义 | `KFunction` 保留扩展接收者信息 |
| **委托属性** | 只能看到生成的 getter/setter | 可通过 `getDelegate()` 获取委托对象实例 |
| **数据类** | 无特殊标识 | `isData` 属性直接判断 |

**核心优势**：
Kotlin 反射不仅提供了对 JVM 结构的访问，还保留了 **Kotlin 特有的元数据**。这使得编写框架（如序列化、DI、ORM）时，能够更自然地处理 Kotlin 代码逻辑，而不是被迫适配 Java 的视角。

### 1.2 依赖配置

Kotlin 的标准库 `kotlin-stdlib` **不包含**完整的反射支持。你需要额外引入 `kotlin-reflect`。

**为什么分开？**
`kotlin-reflect` 体积较大（约 3MB+），且初始化开销高。许多小型应用或 Android 应用可能不需要反射功能，分离依赖有助于减小包体积。

**Gradle 配置 (Kotlin DSL):**
```kotlin
dependencies {
    implementation("org.jetbrains.kotlin:kotlin-reflect:1.9.0") // 版本需与 kotlin stdlib 一致
}
```

**Maven 配置:**
```xml
<dependency>
    <groupId>org.jetbrains.kotlin</groupId>
    <artifactId>kotlin-reflect</artifactId>
    <version>1.9.0</version>
</dependency>
```

**多平台支持现状：**
*   **JVM**: 完全支持。
*   **JS**: 支持有限。由于 JS 是动态语言，很多反射操作可以通过动态特性实现，但 `kotlin-reflect` 在 JS 目标中通常不可用或行为不同。通常建议使用动态类型 `dynamic`。
*   **Native**: 支持非常有限。由于 AOT 编译和树摇（Tree Shaking）优化，未使用的类可能被裁剪，导致反射找不到类。目前主要用于调试或特定场景，不建议在生产环境重度依赖。

### 1.3 核心 API 概览

所有 Kotlin 反射接口都位于 `kotlin.reflect` 包下。为了简化操作，绝大多数实用扩展函数位于 `kotlin.reflect.full` 包中，建议始终导入此包。

```kotlin
import kotlin.reflect.KClass
import kotlin.reflect.KProperty
import kotlin.reflect.KFunction
import kotlin.reflect.full.* // 重要：包含 memberProperties, callBy 等扩展
```

*   **`KClass<T>`**: 对应 Java 的 `Class<T>`，但提供了更多 Kotlin 视角的信息（如 `isData`, `objectInstance`）。
*   **`KProperty<R>`**: 代表一个属性。如果是 `var`，则是 `KMutableProperty<R>`。它封装了 getter 和 setter。
*   **`KFunction<R>`**: 代表一个函数或方法。包含参数列表、返回类型、是否为 suspend 等信息。
*   **`KType`**: 代表一个具体的类型，包括泛型参数和可空性。例如 `List<String?>` 是一个 `KType`，其 classifier 是 `List`，arguments 包含 `String?`。

---

## 2. 类与对象的操作 (KClass)

### 2.1 获取 KClass 实例

有三种主要方式获取 `KClass`：

1.  **编译时已知类型 (`T::class`)**：
    ```kotlin
    val kClass: KClass<String> = String::class
    ```
    *注意：这返回的是静态类型的 KClass。如果 `T` 是泛型，由于擦除，你可能得不到具体的泛型信息。*

2.  **运行时实例类型 (`obj::class`)**：
    ```kotlin
    val str = "Hello"
    val kClass: KClass<out String> = str::class
    ```
    *这会返回对象实际所属类的 KClass。*

3.  **从 Java Class 转换**：
    ```kotlin
    val javaClass: Class<MyClass> = MyClass::class.java
    val kClass: KClass<MyClass> = javaClass.kotlin
    ```

**对比 `Class.forName()`**:
Java 的 `Class.forName("com.example.MyClass")` 返回 `Class<?>`。若要转为 `KClass`，需调用 `.kotlin` 扩展属性。Kotlin 没有直接的字符串到 `KClass` 的全局查找函数，通常依赖 Java 互操作或自定义类加载器扫描。

### 2.2 类信息查询

```kotlin
data class User(val name: String, val age: Int)

val kClass = User::class

// 名称
println(kClass.simpleName)    // "User"
println(kClass.qualifiedName) // "com.example.User"

// 可见性与特征
println(kClass.isPublic)      // true
println(kClass.isData)        // true
println(kClass.isAbstract)    // false
println(kClass.isFinal)       // true (data classes are final by default)

// 继承体系
println(kClass.superclasses)  // [class kotlin.Any]
```

对于 **Sealed Classes**，这是一个强大的功能：
```kotlin
sealed class Result
class Success(val data: String) : Result()
class Error(val msg: String) : Result()

val sealedKClass = Result::class
// 获取所有直接子类
println(sealedKClass.sealedSubclasses) 
// [class com.example.Success, class com.example.Error]
```

### 2.3 实例化

**无参构造**：
```kotlin
class EmptyClass()
val instance = EmptyClass::class.createInstance()
```
*注意：如果类没有无参构造函数，`createInstance()` 会抛出异常。*

**有参构造**：
这是 Kotlin 反射最强大的地方之一，因为它支持**默认参数**。

```kotlin
class Config(val host: String = "localhost", val port: Int = 8080)

val constructor = Config::class.constructors.first()

// 方式 1: call (位置参数，必须提供所有参数，忽略默认值)
// val obj1 = constructor.call("127.0.0.1", 3000) 

// 方式 2: callBy (映射参数，支持默认值和命名参数) - 推荐
val params = constructor.parameters.associateBy { it.name }
val obj2 = constructor.callBy(mapOf(
    params["host"] to "example.com" 
    // port 未提供，将使用默认值 8080
))
println(obj2.port) // 8080
```

---

## 3. 属性反射 (KProperty)

### 3.1 获取属性

```kotlin
data class Person(val name: String, var age: Int)

val kClass = Person::class

// 获取所有成员属性（包括继承的）
val allProps = kClass.memberProperties

// 仅获取当前类声明的属性
val declaredProps = kClass.declaredMemberProperties

// 按名称查找
val nameProp = kClass.memberProperties.find { it.name == "name" }
```

### 3.2 读取与写入

```kotlin
val person = Person("Alice", 30)
val nameProp = Person::class.memberProperties.find { it.name == "name" } as KProperty1<Person, String>
val ageProp = Person::class.memberProperties.find { it.name == "age" } as KMutableProperty1<Person, Int>

// 读取
val name = nameProp.get(person) // "Alice"
// 或者使用 getter
val name2 = nameProp.getter.call(person)

// 写入 (仅限 KMutableProperty)
ageProp.set(person, 31)
// 或者使用 setter
ageProp.setter.call(person, 32)
```

**类型安全警告**：
`memberProperties` 返回的是 `KProperty<*>`。在实际操作中，通常需要强制转换或检查类型，否则 `get` 返回的是 `Any?`。使用 `KProperty1<Receiver, ReturnType>` 可以提供更好的类型推断。

### 3.3 处理 Kotlin 特有特性

**Nullability**:
```kotlin
class Data(val optional: String?)
val prop = Data::class.memberProperties.first()
println(prop.returnType.isMarkedNullable) // true
```

**Delegated Properties (委托属性)**:
Kotlin 的 `by lazy`, `by observable` 等委托在反射中有特殊支持。

```kotlin
import kotlin.properties.Delegates

class Example {
    var observed: String by Delegates.observable("<init>") { prop, old, new ->
        println("$old -> $new")
    }
}

val ex = Example()
val prop = Example::class.memberProperties.first() as KMutableProperty<*>

// 检查是否委托
if (prop is KProperty.Delegated) {
    // 获取委托对象实例
    val delegate = prop.getDelegate(ex)
    println(delegate::class.simpleName) // "ObservableProperty"
}
```
*应用场景*：在调试工具中，你可能想知道某个属性的值变化监听器是谁；或者在序列化时，需要知道底层存储结构。

**Backing Fields**:
Kotlin 反射**不直接暴露** backing field。你只能通过 getter/setter 访问。如果需要直接操作字段（例如绕过自定义 getter 逻辑），必须回退到 Java 反射：
```kotlin
val javaField = Person::class.java.getDeclaredField("name")
javaField.isAccessible = true
val value = javaField.get(person)
```

---

## 4. 函数与方法反射 (KFunction)

### 4.1 获取函数

```kotlin
class Calculator {
    fun add(a: Int, b: Int) = a + b
    private fun secret() = 42
}

val kClass = Calculator::class

// 获取所有公共成员函数
val functions = kClass.memberFunctions

// 获取特定函数
val addFunc = kClass.memberFunctions.find { it.name == "add" }
```

### 4.2 调用函数

```kotlin
val calc = Calculator()
val addFunc = Calculator::class.memberFunctions.find { it.name == "add" }!!

// 方式 1: call (位置参数)
val result1 = addFunc.call(calc, 10, 20) // 30

// 方式 2: callBy (命名参数 + 默认参数)
// 假设函数定义为: fun greet(name: String = "World") = "Hello $name"
val params = addFunc.parameters.associateBy { it.name }
// 注意：第一个参数通常是实例本身 (instance)，除非是扩展函数或静态方法
val instanceParam = params[null] // 或者 find { it.kind == KParameter.Kind.INSTANCE }
val aParam = params["a"]
val bParam = params["b"]

val result2 = addFunc.callBy(mapOf(
    instanceParam to calc,
    aParam to 5,
    bParam to 15
))
```

**处理重载**：
`memberFunctions` 会返回所有同名函数。你需要通过 `parameters.size` 或 `parameters.map { it.type }` 来区分重载版本。

### 4.3 参数与返回值分析

```kotlin
fun analyze(func: KFunction<*>) {
    println("Return Type: ${func.returnType}")
    println("Is Suspend: ${func.isSuspend}")
    println("Parameters:")
    func.parameters.forEach { param ->
        println("  Name: ${param.name}, Type: ${param.type}, Is Optional: ${param.isOptional}")
    }
}
```
*   `isSuspend`: 判断是否为协程挂起函数。如果是，调用时需要特殊的协程上下文处理（通常不能直接 `call`，需借助 `CoroutineStart` 或包装）。
*   `isOptional`: 对应 Kotlin 的默认参数。

---

## 5. 类型系统与泛型 (KType)

### 5.1 KType 详解

在 Java 中，`List<String>.class` 是不合法的，泛型信息在运行时被擦除。但在 Kotlin 反射中，`KType` 保留了丰富的信息。

```kotlin
class Container<T> {
    lateinit var data: List<T?>
}

val prop = Container::class.memberProperties.first() // data
val type = prop.returnType // KType for List<T?>

println(type.classifier) // interface kotlin.collections.List
println(type.arguments)  // [KTypeProjection(variance=INVARIANT, type=T?)]
println(type.isMarkedNullable) // false (List itself is not nullable)

// 深入泛型参数
val innerType = type.arguments.first().type
println(innerType?.isMarkedNullable) // true (T is nullable)
```

### 5.2 泛型擦除与保留

**JVM 限制**：
尽管 `KType` 看起来保留了泛型，但在 JVM 上，如果泛型类型参数 `T` 没有被具体化（reified），你在运行时仍然无法知道 `T` 具体是 `String` 还是 `Int`，除非该信息来自签名（Signature）且未被擦除。

**`typeOf<T>()` 的威力**：
Kotlin 1.3.50 引入了 `typeOf<T>()`，它利用内联函数和 reified 类型参数，在编译期捕获类型信息并生成常量。这比传统的反射更高效、更准确。

```kotlin
import kotlin.reflect.typeOf

val stringListType = typeOf<List<String>>()
val nullableIntType = typeOf<Int?>()

println(stringListType) // kotlin.collections.List<kotlin.String>
println(nullableIntType.isMarkedNullable) // true
```
*建议*：在新代码中，优先使用 `typeOf` 进行类型比较和检查，而不是手动构建 `KType`。

---

## 6. 高级应用场景

### 6.1 自定义注解处理

注解是反射最常见的用途之一，用于配置行为。

```kotlin
@Target(AnnotationTarget.PROPERTY)
annotation class JsonIgnore

data class User(
    val name: String,
    @JsonIgnore val password: String
)

fun toJson(obj: Any): String {
    val jsonMap = mutableMapOf<String, Any?>()
    val kClass = obj::class
    
    for (prop in kClass.memberProperties) {
        // 检查是否有 JsonIgnore 注解
        if (prop.findAnnotation<JsonIgnore>() != null) {
            continue
        }
        jsonMap[prop.name] = prop.getter.call(obj)
    }
    return jsonMap.toString() // 简易 JSON
}
```

### 6.2 序列化与反序列化框架原理

一个简单的通用序列化器思路：
1.  获取对象的 `KClass`。
2.  遍历 `memberProperties`。
3.  对于每个属性：
    *   如果是基本类型/String，直接取值。
    *   如果是自定义对象，递归调用序列化。
    *   如果是集合，遍历元素。
4.  构建 Map 或 JSON 树。

*注意*：生产环境请使用 `kotlinx.serialization` 或 Jackson/Gson。手动反射序列化性能差且容易出错（循环引用、私有属性等）。

### 6.3 依赖注入 (DI) 容器简易实现

核心逻辑：
1.  **注册**：将类与其对应的 `KClass` 绑定。
2.  **解析**：当请求一个实例时：
    *   获取该类的**主构造函数** (`primaryConstructor`)。
    *   获取构造函数的参数列表 (`parameters`)。
    *   递归地为每个参数类型请求实例（依赖解析）。
    *   使用 `constructor.callBy` 传入解析好的依赖实例。
    *   缓存实例（如果是 Singleton）。

```kotlin
class SimpleContainer {
    private val instances = mutableMapOf<KClass<*>, Any>()

    inline fun <reified T : Any> resolve(): T {
        val kClass = T::class
        if (instances.containsKey(kClass)) {
            return instances[kClass] as T
        }

        val constructor = kClass.primaryConstructor 
            ?: throw IllegalStateException("No primary constructor for $kClass")
        
        val args = mutableMapOf<KParameter, Any?>()
        for (param in constructor.parameters) {
            // 递归解析依赖
            val dependency = resolveDependency(param.type)
            args[param] = dependency
        }

        val instance = constructor.callBy(args)
        instances[kClass] = instance
        return instance as T
    }
    
    private fun resolveDependency(type: KType): Any? {
        val classifier = type.classifier as? KClass<*> ?: return null
        // 这里需要处理泛型、基本类型等复杂情况，简化起见仅演示思路
        return resolve(classifier) 
    }
    
    @Suppress("UNCHECKED_CAST")
    private fun <T : Any> resolve(kClass: KClass<T>): T {
        return resolve() // 实际实现需处理泛型映射
    }
}
```

### 6.4 测试框架支持

*   **Mocking**: Mockito 等库底层大量使用反射来创建代理对象和拦截方法调用。
*   **Fixture Generation**: 可以编写一个工具，根据 `KProperty` 的类型自动生成随机测试数据（例如遇到 `String` 生成随机串，遇到 `Int` 生成随机数）。

---

## 7. 性能考量与最佳实践

### 7.1 性能陷阱

1.  **启动慢**：首次加载 `kotlin-reflect` 和解析类元数据非常耗时。
2.  **调用慢**：`KFunction.call` 比直接调用慢几个数量级，因为它涉及装箱、参数映射和安全检查。
3.  **内存占用**：`KClass` 和相关的反射对象会占用 PermGen/Metaspace 空间。

### 7.2 优化策略

1.  **缓存一切**：
    *   不要每次都用 `::class.memberProperties`。
    *   建立一个 `ConcurrentHashMap<KClass, List<KProperty>>` 缓存属性列表。
    *   缓存 `KFunction` 实例。

2.  **避免在热点路径使用**：
    *   不要在高频循环中进行反射查找或调用。
    *   如果在循环中需要设置属性，考虑生成字节码（ByteBuddy）或使用 Java 反射的 `MethodHandle`（更快）。

3.  **使用 `call` 而非 `callBy`**：
    *   如果不需要默认参数支持，`call(vararg)` 比 `callBy(map)` 快，因为后者需要构建 Map 并匹配参数。

### 7.3 Kotlin 反射 vs Java 反射互操作

有时你需要混合使用：

```kotlin
val kProp = User::class.memberProperties.first()
// 获取对应的 Java Field
val javaField = (kProp as? KProperty1<*, *>)?.javaField
// 获取对应的 Java Getter
val javaGetter = kProp.javaGetter
```

**何时回退到 Java 反射？**
*   需要访问 `private` backing field 且不想破坏封装太严重（虽然两者都需要 `setAccessible(true)`）。
*   性能极度敏感的场景，Java 反射经过多年优化，且没有 Kotlin 层的额外抽象开销。
*   与纯 Java 库交互时。

### 7.4 替代方案：编译时处理

如果反射性能成为瓶颈，现代 Kotlin 开发倾向于**编译时代码生成**：

1.  **KSP (Kotlin Symbol Processing)**: 轻量级，专门用于 Kotlin。可以在编译期读取注解和符号，生成辅助代码（如 JSON 序列化适配器）。
2.  **KAPT**: 基于 Java annotation processing，较重，但生态成熟。
3.  **Compiler Plugins**: 最强大，可以直接修改 AST，但开发难度极高。

*例子*：`kotlinx.serialization` 不使用运行时反射，而是由编译器插件生成序列化代码，因此速度极快且支持 ProGuard/R8 混淆。

---

## 8. 常见误区与调试

1.  **内部类名称**：
    `Outer.Inner` 在 JVM 上的类名是 `Outer$Inner`。使用 `qualifiedName` 时 Kotlin 会显示 `Outer.Inner`，但在使用 `Class.forName` 时需要用 `$`。

2.  **Value Classes (Inline Classes)**：
    ```kotlin
    @JvmInline
    value class UserId(val id: Long)
    ```
    在反射中，`UserId::class` 的行为可能符合预期，但在底层 JVM 表示中，它可能被擦除为 `Long`。在跨边界调用（如传给 Java 方法）时需注意装箱。

3.  **Sealed Classes 的子类扫描**：
    `sealedSubclasses` 只返回**直接**子类。如果子类还有子类，需要递归查找。且确保所有子类都在同一个编译单元或类路径可见范围内。

4.  **异常处理**：
    反射调用抛出的异常通常被包裹在 `InvocationTargetException` 中。真正的异常在 `cause` 里。
    ```kotlin
    try {
        func.call(obj)
    } catch (e: InvocationTargetException) {
        throw e.cause ?: e
    }
    ```

---

## 9. 练习项目代码指引

### 练习 1: Mini JSON Parser (简化版)

```kotlin
import kotlin.reflect.full.memberProperties
import kotlin.reflect.KClass

fun Any.toJson(): String {
    val kClass = this::class
    val props = kClass.memberProperties
    val entries = props.joinToString(", ") { prop ->
        val value = prop.getter.call(this)
        val jsonString = when (value) {
            is String -> "\"$value\""
            null -> "null"
            else -> value.toString() // 简单处理，实际需递归
        }
        "\"${prop.name}\": $jsonString"
    }
    return "{$entries}"
}

// 测试
data class TestUser(val name: String, val age: Int)
fun main() {
    println(TestUser("Bob", 25).toJson()) 
    // 输出: {"name": "Bob", "age": 25}
}
```

### 练习 2: Simple DI Container (核心逻辑)

参考第 6.3 节。关键点在于递归解析 `primaryConstructor` 的参数。

### 练习 3: API Router

```kotlin
@Target(AnnotationTarget.FUNCTION)
annotation class Get(val path: String)

class Router {
    private val routes = mutableMapOf<String, KFunction<*>>()

    fun register(controller: Any) {
        val kClass = controller::class
        for (func in kClass.memberFunctions) {
            val getAnnotation = func.findAnnotation<Get>()
            if (getAnnotation != null) {
                routes[getAnnotation.path] = func
            }
        }
    }

    fun handle(path: String): String? {
        val func = routes[path] ?: return null
        // 假设函数无参且返回 String，实际需处理参数绑定
        return func.callBy(mapOf(func.parameters.firstOrNull { it.kind == KParameter.Kind.INSTANCE } to /* controller instance */)) as? String
    }
}
```

---

这是一份针对你提供的大纲的**详细讲解与代码实现指南**。我将深入每个知识点，提供可运行的代码示例、底层原理解析以及最佳实践建议。

---

# 读取标准输入输出 (Standard I/O in Kotlin)

Kotlin 的标准 I/O 设计哲学是：**简洁、安全、互操作性**。它既保留了 Java `System.in/out` 的强大功能，又通过扩展函数和空安全机制极大地简化了日常开发。

## 1. 基础输出 (Output)

### 1.1 `print()` vs `println()`
这是最基础的输出方式，它们实际上是 `kotlin.io` 包中对 `System.out` 的封装。

*   **`println()`**: 输出内容后自动追加一个换行符 (`\n`)。
*   **`print()`**: 仅输出内容，光标停留在末尾。

```kotlin
fun main() {
    println("Hello, World!") // 输出: Hello, World! [换行]
    print("Kotlin ")         // 输出: Kotlin 
    print("is awesome")      // 输出: is awesome
    // 最终控制台显示:
    // Hello, World!
    // Kotlin is awesome
}
```

### 1.2 字符串模板 (String Templates)
这是 Kotlin 相比 Java `+` 拼接或 `String.format` 最大的优势之一，可读性极高。

*   **简单变量插入**: `$variableName`
*   **复杂表达式插入**: `${expression}`
*   **转义**: 如果需要输出 `$` 符号，使用 `\$`。

```kotlin
fun main() {
    val name = "Alice"
    val age = 30
    
    // 简单插入
    println("Name: $name") 
    
    // 复杂表达式：直接在字符串中进行计算或调用方法
    println("Next year, $name will be ${age + 1} years old.")
    println("Name length: ${name.length}")
    
    // 转义美元符号
    val price = 100
    println("The price is \$${price}") // 输出: The price is $100
}
```

### 1.3 格式化输出
虽然字符串模板很强大，但在处理对齐、小数位数保留等场景时，传统格式化依然必要。

*   **`String.format()`**: 沿用 Java/C 风格。
*   **多行字符串与修剪**: 适合输出大块文本（如 SQL、JSON、HTML）。

```kotlin
fun main() {
    // 1. String.format
    val pi = 3.1415926535
    println(String.format("Pi is approximately %.2f", pi)) // 输出: Pi is approximately 3.14
    
    // 2. 多行字符串与 trimIndent
    // trimIndent 会移除每行共同的缩进前缀，使代码排版整齐且输出干净
    val sqlQuery = """
        SELECT id, name, email
        FROM users
        WHERE active = true
        ORDER BY name
    """.trimIndent()
    
    println(sqlQuery)
    /* 输出:
    SELECT id, name, email
    FROM users
    WHERE active = true
    ORDER BY name
    */
}
```

---

## 2. 基础输入 (Input)

### 2.1 `readLine()` 与 `readln()`
这是从控制台读取一行文本的标准方式。

*   **`readLine()`**: 返回 `String?`。如果到达输入流末尾（EOF），返回 `null`。**必须处理空指针风险**。
*   **`readln()`** (Kotlin 1.6+): 返回 `String`。如果到达 EOF，抛出 `NoSuchElementException`。适合脚本或确定有输入的场景，代码更简洁。

```kotlin
fun main() {
    // 方式 A: 使用 readLine (传统，安全)
    print("Enter your name (readLine): ")
    val name1 = readLine()
    if (name1 != null) {
        println("Hello, $name1")
    } else {
        println("No input provided.")
    }

    // 方式 B: 使用 readln (现代，简洁)
    // 注意：如果在 IDE 中运行且没有输入，可能会抛异常，建议配合 try-catch 或确保有输入
    print("Enter your name (readln): ")
    try {
        val name2 = readln()
        println("Hello, $name2")
    } catch (e: NoSuchElementException) {
        println("Input stream ended.")
    }
}
```

### 2.2 `Scanner` 类 (Java 互操作)
当需要直接读取特定类型（如 `Int`, `Double`）而不想手动解析字符串时，可以使用 Java 的 `Scanner`。

*   **优点**: API 丰富，直接获取类型。
*   **缺点**: 性能较差（正则解析），非 Kotlin 原生风格，需要处理 `InputMismatchException`。

```kotlin
import java.util.Scanner

fun main() {
    val scanner = Scanner(System.`in`)
    
    print("Enter an integer: ")
    if (scanner.hasNextInt()) {
        val number = scanner.nextInt()
        println("You entered: $number")
    } else {
        println("Invalid integer input.")
    }
    
    scanner.close() // 最佳实践：关闭资源
}
```

### 2.3 Kotlin 标准库扩展函数 (推荐)
Kotlin 在 `kotlin.io.ConsoleKt` 中提供了一系列扩展函数，结合了 `readln()` 的简洁和类型转换的便利。这些函数通常在导入 `kotlin.io.*` 后可用，或者在某些环境中默认可用。

*   **常用函数**: `readInt()`, `readLong()`, `readDouble()`, `readBoolean()`, `readLineOrNull()`.
*   **特性**: 内部自动处理 `readln()` 和 `toString().toXxx()`，如果转换失败通常抛出异常或返回 null（取决于具体函数版本和实现，建议查看源码确认，通常 `readInt` 会在解析失败时抛 `NumberFormatException`）。

> **注意**: `readInt()` 等函数并非在所有 Kotlin 平台（如 JS, Native）都一致可用，主要在 JVM 上表现良好。

```kotlin
import kotlin.io.readInt // 显式导入以确保可用性

fun main() {
    print("Enter an integer: ")
    try {
        val num = readInt()
        println("Squared: ${num * num}")
    } catch (e: Exception) {
        println("Please enter a valid integer.")
    }
}
```

**自定义安全扩展函数示例：**
如果你想要一个既安全又方便的 `readIntOrNull`，可以这样写：

```kotlin
fun readIntOrNull(): Int? {
    return readlnOrNull()?.toIntOrNull()
}

fun main() {
    print("Enter a number: ")
    val num = readIntOrNull()
    if (num != null) {
        println("Got: $num")
    } else {
        println("Invalid or empty input.")
    }
}
```

---

## 3. 高级输入处理技巧

### 3.1 批量输入处理 (Split & Map)
在算法竞赛或数据处理中，经常遇到一行包含多个数据的情况，如 `10 20 30`。

```kotlin
fun main() {
    // 假设输入: 10 20 30 40
    print("Enter numbers separated by space: ")
    val line = readln()
    
    // split 默认按空白字符分割，trim 去除首尾空格
    val numbers: List<Int> = line.trim().split("\\s+".toRegex())
                                .map { it.toInt() }
    
    println("Sum: ${numbers.sum()}")
    println("List: $numbers")
}
```

### 3.2 多行输入读取 (GenerateSequence)
当不知道输入有多少行，直到 EOF 结束时，`generateSequence` 是最优雅的 Kotlin 方式。

```kotlin
fun main() {
    println("Enter lines (Ctrl+D/Z to stop):")
    
    // generateSequence 惰性生成序列，每次调用 block 获取下一个元素，直到返回 null
    val lines = generateSequence { readlnOrNull() }
    
    // 转换为列表并处理
    val allLines = lines.toList()
    
    println("Total lines: ${allLines.size}")
    allLines.forEachIndexed { index, line ->
        println("Line $index: $line")
    }
}
```

### 3.3 错误处理与验证循环
健壮的程序必须处理非法输入。

```kotlin
fun readValidAge(): Int {
    while (true) {
        print("Enter your age (1-120): ")
        val input = readlnOrNull() ?: break
        
        try {
            val age = input.toInt()
            if (age in 1..120) {
                return age
            } else {
                println("Age must be between 1 and 120.")
            }
        } catch (e: NumberFormatException) {
            println("Invalid number format. Please try again.")
        }
    }
    throw IllegalStateException("Input stream closed.")
}

fun main() {
    val age = readValidAge()
    println("Valid age entered: $age")
}
```

---

# 选择加入要求 (Opt-in Requirements)

Kotlin 的语言演进非常快，为了在不破坏稳定性的前提下引入新特性，引入了 **Opt-in 机制**。这不仅是注解，更是一种契约。

## 1. 核心概念

*   **实验性 API (Experimental API)**: 标记为 `@RequiresOptIn` 的 API。它们可能随时更改名称、签名或被移除。
*   **选择加入 (Opt-in)**: 开发者必须显式声明“我知道这个 API 不稳定，我同意承担风险”，编译器才会允许编译通过。
*   **目的**:
    1.  **隔离风险**: 防止实验性代码污染整个项目。
    2.  **反馈循环**: 鼓励早期用户试用并反馈 Bug。
    3.  **清晰边界**: 在代码审查中，`@OptIn` 是一个明显的信号，提示审查者注意潜在的不稳定性。

## 2. 核心注解详解

### 2.1 `@RequiresOptIn` (定义者使用)
库作者使用此注解标记自己的 API。

```kotlin
// 库作者代码
@RequiresOptIn(
    level = RequiresOptIn.Level.WARNING, // 或 ERROR
    message = "This API is experimental. It may change in future releases."
)
annotation class MyExperimentalApi

@MyExperimentalApi
fun experimentalFeature() {
    println("This is experimental!")
}
```

### 2.2 `@OptIn` (使用者使用)
应用开发者使用此注解来启用实验性 API。

```kotlin
// 应用开发者代码
import kotlin.OptIn

// 方式 1: 函数级别 (推荐，影响范围最小)
@OptIn(MyExperimentalApi::class)
fun useExperimentalFeature() {
    experimentalFeature()
}

// 方式 2: 类级别
@OptIn(MyExperimentalApi::class)
class MyClass {
    fun doSomething() {
        experimentalFeature()
    }
}

// 方式 3: 文件级别 (影响整个文件)
@file:OptIn(MyExperimentalApi::class)

// 方式 4: 模块级别 (Gradle/Maven 配置，影响整个模块)
```

### 2.3 常见官方实验性 API 示例
*   **`kotlin.time.ExperimentalTime`**: 用于 `Duration` 和 `measureTimeMillis` 等新时间 API（在 Kotlin 1.6+ 中已逐渐稳定，部分不再需要 Opt-in，但旧代码中常见）。
*   **`kotlinx.coroutines.ExperimentalCoroutinesApi`**: 协程中的新操作符或调度器特性。
*   **`kotlin.experimental.ExperimentalNativeApi`**: Kotlin/Native 特定功能。

## 3. 配置与管理实战

### 3.1 Gradle 配置 (Kotlin DSL)
如果你希望在**整个模块**中启用某个实验性 API（例如，你的项目重度依赖某个实验性功能），可以在 `build.gradle.kts` 中配置：

```kotlin
kotlin {
    sourceSets.all {
        languageSettings {
            // 启用特定的实验性 API
            optIn("kotlin.time.ExperimentalTime")
            optIn("kotlinx.coroutines.ExperimentalCoroutinesApi")
            
            // 启用所有实验性 API (不推荐，除非是测试项目)
            // progressiveMode = true 
        }
    }
}
```

### 3.2 Maven 配置
在 `pom.xml` 的 `kotlin-maven-plugin` 配置中：

```xml
<configuration>
    <args>
        <arg>-opt-in=kotlin.time.ExperimentalTime</arg>
        <arg>-opt-in=kotlinx.coroutines.ExperimentalCoroutinesApi</arg>
    </args>
</configuration>
```

### 3.3 IDE 支持
*   **IntelliJ IDEA**: 当你调用一个需要 Opt-in 的 API 时，IDE 会标红或黄色警告。
*   **快速修复**: 将光标放在错误处，按 `Alt+Enter` (Windows/Linux) 或 `Option+Enter` (Mac)，IDE 会自动添加 `@OptIn` 注解或建议修改 Gradle 配置。

## 4. 最佳实践与注意事项

### 4.1 作用域最小化原则
*   **优先函数级**: 只在真正使用实验性 API 的函数上加 `@OptIn`。
*   **避免文件级/模块级**: 除非该实验性 API 已成为项目核心且团队达成一致，否则不要全局启用。全局启用会掩盖其他潜在的实验性 API 使用，降低代码的可维护性。

### 4.2 生产环境风险评估
*   **关键路径慎用**: 不要在核心业务逻辑、高并发服务的关键路径中使用实验性 API，除非你有充分的测试和回滚计划。
*   **替代方案**: 检查是否有稳定的替代方案。例如，早期 `Duration` 是实验性的，现在已稳定，应移除 `@OptIn`。

### 4.3 版本升级与维护
*   **定期清理**: 每次升级 Kotlin 版本后，检查 Release Notes。很多实验性 API 会转为稳定（Stable）。一旦稳定，`@OptIn` 注解就不再需要，应及时移除以保持代码整洁。
*   **Breaking Changes**: 如果实验性 API 被移除或签名大幅变更，编译器会报错。此时需要根据新文档重构代码。

### 4.4 自定义实验性 API (库开发者视角)
如果你是库作者，希望发布一个新功能但不想承诺长期兼容：

```kotlin
@RequiresOptIn(level = RequiresOptIn.Level.ERROR, message = "Deep learning features are experimental.")
annotation class ExperimentalDL

@ExperimentalDL
fun trainModel() { ... }
```
*   **Level.ERROR**: 强制使用者必须显式 Opt-in，否则编译失败。适用于高风险 API。
*   **Level.WARNING**: 仅给出警告，允许编译。适用于低风险或即将稳定的 API。

---

## 总结

*   **I/O 模块**: 掌握 `println`/`print` 的输出技巧，熟练运用 `readln` 结合 `split`/`map` 处理复杂输入，理解 `Scanner` 的适用场景。重点在于**利用 Kotlin 的空安全和集合操作简化输入解析逻辑**。
*   **Opt-in 模块**: 理解这是 Kotlin 平衡**创新**与**稳定**的机制。作为使用者，要遵循**最小作用域原则**；作为库作者，要合理使用 `@RequiresOptIn` 保护用户。随着 Kotlin 版本的迭代，保持对 API 稳定状态的关注是日常维护的一部分。
这是一份经过深度完善和详细讲解的大纲内容。我将原有的要点扩展为**教学级**的详细笔记，增加了底层原理、代码对比、易错点分析以及 2026 年视角下的现代 Kotlin 最佳实践。

---

# 作用域函数 (Scope Functions)

## 1. 核心概念与设计哲学
Kotlin 的作用域函数（`let`, `run`, `with`, `apply`, `also`）本质上是**高阶函数**。它们的共同目的是：**在一个对象的上下文中执行一个代码块（Lambda）**。

它们主要解决两个问题：
1.  **临时作用域**：创建一个局部作用域，避免变量污染外部空间。
2.  **链式调用与空安全**：简化对象初始化和 null 检查后的操作逻辑。

### 关键区分维度
要掌握这五个函数，只需记住两个维度的组合：

| 维度 | 选项 A | 选项 B |
| :--- | :--- | :--- |
| **接收者引用方式** | **`it`** (作为参数传入) | **`this`** (作为接收者) |
| **返回值** | **对象本身** (`T`) | **Lambda 结果** (`R`) |

*   **`it` vs `this`**:
    *   `it`: 当你需要明确区分“当前对象”和“外部类成员”时使用。它更清晰，但访问对象属性时需要加 `it.`。
    *   `this`: 当代码块内部主要是在配置该对象，且不需要频繁访问外部成员时使用。代码更简洁，但容易混淆上下文。
*   **返回 `T` vs `R`**:
    *   返回 `T` (对象本身): 用于**初始化**或**副作用**，目的是保持链式调用继续下去。
    *   返回 `R` (计算结果): 用于**转换**或**提取值”，目的是得到一个新的结果。

---

## 2. 五大函数深度解析

### 2.1 `let` - 空安全与映射转换
*   **签名**: `<T, R> T.let(block: (T) -> R): R`
*   **上下文对象**: `it`
*   **返回值**: Lambda 的最后一行结果 (`R`)
*   **核心场景**:
    1.  **非空执行**: `obj?.let { ... }` 是处理 nullable 对象最 idiomatic（地道）的方式。如果 `obj` 为 null，整个表达式结果为 null，不会执行 block。
    2.  **变量重命名/限制作用域**: 当一个变量名很长或容易冲突时，可以用 `let` 将其映射为 `it` 或自定义名称（通过 `it` 无法改名，但可以通过嵌套 let 模拟，不过通常直接用 `run` 更好）。
    3.  **轻量级 Map**: 对单个对象进行转换。

*   **代码详解**:
    ```kotlin
    val name: String? = getNameFromDb()

    // 传统写法
    if (name != null) {
        println(name.length)
    }

    // let 写法 (推荐)
    // 如果 name 为 null，let 块不执行，result 为 null
    val length = name?.let { 
        println("Processing name: $it")
        it.length 
    } ?: 0 // Elvis 操作符提供默认值
    ```

### 2.2 `apply` - 对象配置器 (Builder)
*   **签名**: `<T> T.apply(block: T.() -> Unit): T`
*   **上下文对象**: `this` (可省略)
*   **返回值**: 对象本身 (`T`)
*   **核心场景**:
    1.  **对象初始化**: 在创建对象后立即设置属性，无需重复写对象名。
    2.  **Android View 配置**: 设置 TextView 颜色、大小等。
    3.  **测试数据构建**: 快速构建复杂的测试对象。

*   **代码详解**:
    ```kotlin
    // 传统写法
    val person = Person()
    person.name = "Alice"
    person.age = 30
    person.city = "New York"

    // apply 写法 (推荐)
    // 返回的是 person 对象本身，所以可以赋值给 val
    val person = Person().apply {
        name = "Alice" // 这里 this 指向 person，所以可以直接访问属性
        age = 30
        city = "New York"
    }
    
    // 链式调用示例
    val textView = TextView(context).apply {
        text = "Hello"
        textSize = 16f
        setTextColor(Color.BLACK)
    }.also { viewGroup.addView(it) } // 结合 also 做副作用
    ```

### 2.3 `run` - 计算与上下文切换
*   **签名**: 
    1.  `<T, R> T.run(block: T.() -> R): R` (扩展函数)
    2.  `<R> run(block: () -> R): R` (顶层函数，无接收者)
*   **上下文对象**: `this`
*   **返回值**: Lambda 结果 (`R`)
*   **核心场景**:
    1.  **需要 `this` 上下文并返回结果**: 比如先配置对象，然后立即基于配置计算一个值。
    2.  **临时作用域**: 使用无接收者的 `run` 将一组变量限制在局部范围内。
    3.  **Nullable 对象的复杂处理**: `obj?.run { ... }`。如果需要在非空块里既访问属性又返回计算结果。

*   **代码详解**:
    ```kotlin
    // 场景1: 配置并计算
    val config = Config().apply { loadDefaults() }
    
    val isValid = config.run {
        // 在这里 this 指向 config
        validateFieldA() && validateFieldB()
    } // 返回 Boolean

    // 场景2: 限制变量作用域 (无接收者 run)
    val result = run {
        val x = computeX()
        val y = computeY()
        x + y // 返回 Int
    }
    // x 和 y 在这里不可见，避免污染外部命名空间
    ```

### 2.4 `with` - 非空对象的工具包
*   **签名**: `<T, R> with(receiver: T, block: T.() -> R): R`
*   **上下文对象**: `this`
*   **返回值**: Lambda 结果 (`R`)
*   **核心场景**:
    1.  **对非空对象执行操作**: 当你有一个确定非 null 的对象，并且想对它调用多个方法，最后返回一个结果时。
    2.  **语义区别**: `with` 不是扩展函数，所以它不能直接处理 null。如果对象可能为 null，必须先用 `?.` 或 `if` 判断，此时用 `let` 或 `run` 更好。因此，看到 `with` 就暗示开发者：“这个对象肯定不为 null”。

*   **代码详解**:
    ```kotlin
    val stringBuilder = StringBuilder()

    // 使用 with 构建字符串
    val result = with(stringBuilder) {
        append("Hello")
        append(" ")
        append("World")
        toString() // 返回 String
    }
    
    // 对比 run:
    // stringBuilder.run { ... } 效果一样，但 with 更强调“在这个对象上操作”
    ```

### 2.5 `also` - 副作用与调试
*   **签名**: `<T> T.also(block: (T) -> Unit): T`
*   **上下文对象**: `it`
*   **返回值**: 对象本身 (`T`)
*   **核心场景**:
    1.  **副作用 (Side Effects)**: 日志记录、断点调试、事件发送。
    2.  **不中断链式调用**: 在 `apply` 或其他链式调用中间插入一个操作，但不改变返回的对象。
    3.  **引用原对象**: 当你在配置对象时，需要将对象本身传递给另一个函数（如注册监听器），用 `it` 比 `this` 更清晰，因为 `this` 可能会被内部 lambda 遮蔽。

*   **代码详解**:
    ```kotlin
    val list = mutableListOf<String>()
    
    // 链式调用中插入日志
    val finalList = list
        .also { println("Initial size: ${it.size}") } // 打印日志，返回 list
        .apply { 
            add("A") 
            add("B") 
        }
        .also { println("After adding: ${it.size}") } // 再次打印
        
    // 注册回调示例
    val button = Button().apply {
        text = "Click Me"
    }.also { 
        it.setOnClickListener { view -> 
            // 这里的 it 是 View，外部的 it 是 Button，互不干扰
            logClick(view) 
        } 
    }
    ```

---

## 3. 决策指南：一图胜千言

在选择函数时，问自己两个问题：

1.  **我想返回什么？**
    *   返回**对象本身** (为了链式调用/初始化) -> 选 `apply` 或 `also`
    *   返回**计算结果** (为了转换/取值) -> 选 `let`, `run`, `with`

2.  **我在 Lambda 里怎么引用对象？**
    *   用 **`it`** (清晰，适合单行或简单操作，或需要区分上下文) -> 选 `let` 或 `also`
    *   用 **`this`** (简洁，适合配置块，或大量访问成员) -> 选 `apply`, `run`, `with`

**综合速查表**:

| 函数 | 引用 | 返回 | 典型用途 | Null-Safe? |
| :--- | :--- | :--- | :--- | :--- |
| **`let`** | `it` | Result | 空安全转换, 局部变量 | ✅ (`?.let`) |
| **`apply`** | `this` | Object | 对象初始化/配置 | ✅ (`?.apply`) |
| **`run`** | `this` | Result | 配置+计算, 临时作用域 | ✅ (`?.run`) |
| **`with`** | `this` | Result | 非空对象的多步操作 | ❌ (需自行判空) |
| **`also`** | `it` | Object | 副作用(日志/调试) | ✅ (`?.also`) |

---

## 4. 高级陷阱与最佳实践 (2026 视角)

1.  **避免“嵌套地狱” (Nested Scope Hell)**:
    *   **错误示范**:
        ```kotlin
        obj?.let { a ->
            a.prop?.let { b ->
                b.doSomething()
            }
        }
        ```
    *   **修正**: 如果嵌套超过两层，代码可读性急剧下降。建议提取函数，或使用标准的 `if-else`，或者使用 Kotlin 的**解构声明**或**Elvis 操作符链**。
    
2.  **`this` 遮蔽 (Shadowing)**:
    *   在类的成员函数中使用 `apply` 或 `run` 时，Lambda 内的 `this` 指向调用者对象，而不是外部类。
    *   **风险**: 如果你想在 Lambda 内访问外部类的成员，必须使用标签引用，如 `this@MyClass.member`。
    *   **建议**: 如果需要频繁访问外部类成员，优先使用 `let` 或 `also` (使用 `it`)，因为它们不会遮蔽 `this`。

3.  **性能真相**:
    *   所有作用域函数都是 `inline` 函数。这意味着在编译后，Lambda 的代码会被直接嵌入调用处，**没有创建匿名类对象的开销**，也没有函数调用的压栈开销。
    *   **结论**: 放心使用，不用担心性能损耗。唯一的性能影响来自代码逻辑本身。

4.  **可读性优先**:
    *   如果 `obj?.let { it.doSomething() }` 比 `if (obj != null) obj.doSomething()` 更难读，那就用 `if`。
    *   作用域函数是为了**表达意图**，而不是为了炫技。

---

# 时间度量 (Time Measurement)

## 1. 为什么 `System.currentTimeMillis()` 不适合测耗时？

*   **墙壁时间 (Wall-Clock Time)**: `currentTimeMillis()` 返回的是自 1970-01-01 UTC 以来的毫秒数。它反映的是“现在几点了”。
*   **不稳定性**:
    *   **NTP 同步**: 操作系统会定期通过网络时间协议校正时钟。如果校正导致时钟回拨，测得的耗时可能是负数！如果时钟向前跳变，耗时会突然变大。
    *   **闰秒**: 虽然罕见，但会影响绝对时间。
    *   **用户修改**: 用户可以手动更改系统时间。
*   **适用场景**: 记录日志时间戳、显示给用户看的时间、持久化存储的时间点。**绝不用于计算两个事件之间的间隔**。

## 2. 黄金标准：`System.nanoTime()`

*   **单调时间 (Monotonic Time)**: `nanoTime()` 返回的是某个固定起点（通常是 JVM 启动或系统启动）之后的纳秒数。
*   **特性**:
    *   **不可逆**: 时间只会增加，不会减少（不受 NTP 影响）。
    *   **高精度**: 纳秒级分辨率（虽然实际硬件精度可能在微秒级，但接口提供纳秒）。
    *   **相对值有意义**: `endTime - startTime` 才是有效的耗时。单独的 `nanoTime()` 值没有任何物理意义。
*   **注意**: 即使 `nanoTime` 也可能受 CPU 频率调整影响（在现代 OS 和 JVM 中已大部分通过硬件计数器解决），但对于应用层性能监控，它是唯一可靠的选择。

## 3. Kotlin 标准库的优雅封装

Kotlin 提供了更语义化的 API，底层均基于 `System.nanoTime()`。

### 3.1 `measureTimeMillis` & `measureNanoTime`
这是最通用的测量工具。

```kotlin
import kotlin.system.measureTimeMillis
import kotlin.system.measureNanoTime

// 场景：监控 API 响应时间
val responseTimeMs = measureTimeMillis {
    val data = apiClient.fetchData()
    process(data)
}
logger.info("API call took $responseTimeMs ms")

// 场景：极高精度算法比对
val diff = measureNanoTime {
    algorithmA(input)
}
```

### 3.2 `kotlin.time.Duration` (类型安全的时间)
从 Kotlin 1.6 开始稳定，推荐使用 `Duration` 替代原始的 `Long` 毫秒/纳秒数，以消除单位混淆。

*   **创建 Duration**:
    ```kotlin
    import kotlin.time.Duration.Companion.seconds
    import kotlin.time.Duration.Companion.milliseconds
    
    val timeout = 5.seconds
    val delay = 500.milliseconds
    val complex = 1.minutes + 30.seconds
    ```

*   **`measureTime`**: 返回 `Duration` 对象，而非 Long。
    ```kotlin
    import kotlin.time.measureTime
    
    val duration: Duration = measureTime {
        heavyTask()
    }
    
    // 丰富的 API
    println(duration.inWholeMilliseconds) // Long
    println(duration.toDouble(DurationUnit.SECONDS)) // Double
    if (duration > 3.seconds) { ... } // 直观的比较
    ```

## 4. 实际应用场景深入

### A. 性能基准测试 (Benchmarking) 的误区
*   **JVM 的 JIT 编译**: Java/Kotlin 代码在运行初期是解释执行的，热点代码会被 JIT 编译为本地机器码。因此，前几次调用通常很慢。
*   **GC 干扰**: 垃圾回收器的随机暂停会影响单次测量。
*   **正确做法**:
    1.  **Warm-up**: 先运行目标代码几千次，让 JIT 完成优化。
    2.  **多次测量**: 运行数千次，取平均值或中位数。
    3.  **使用 JMH**: 对于严肃的性能测试，**不要手写循环**。使用 [JMH (Java Microbenchmark Harness)](https://openjdk.org/projects/code-tools/jmh/)。Kotlin 项目可以轻松集成 JMH。
    
    *Gradle 配置简述*:
    ```groovy
    plugins {
        id 'me.champeau.jmh' version '0.7.2'
    }
    // JMH 会自动处理预热、迭代、 fork 进程等复杂逻辑
    ```

### B. 协程中的超时控制
在异步编程中，时间度量常用于超时切断。

```kotlin
import kotlinx.coroutines.withTimeout
import kotlinx.coroutines.withTimeoutOrNull

suspend fun fetchDataWithTimeout() {
    try {
        // 如果 3 秒内未完成，抛出 TimeoutCancellationException
        val result = withTimeout(3000) {
            api.call()
        }
    } catch (e: TimeoutCancellationException) {
        logger.warn("Request timed out")
    }
    
    // 或者使用OrNull，超时返回 null，不抛异常
    val result = withTimeoutOrNull(3.seconds) {
        api.call()
    }
    if (result == null) handleTimeout()
}
```
*注意*: `withTimeout` 使用的是协程调度器的时钟，通常也是基于单调时间，但在某些自定义 Dispatcher 下需确认其行为。

### C. Android 平台的特殊性
Android 设备会进入深度睡眠（Doze 模式），CPU 可能停止工作。

*   `System.nanoTime()`: 在 Android 上通常基于 `CLOCK_MONOTONIC`，**不包括**深度睡眠时间。如果你测量的是“CPU 处理耗时”，这是对的。但如果你测量的是“用户感知的经过时间”（例如倒计时），它不准。
*   `SystemClock.elapsedRealtime()`: 包括深度睡眠时间。适合测量“从按下按钮到屏幕亮起”的真实物理时间。
*   `SystemClock.uptimeMillis()`: 不包括深度睡眠。适合衡量 CPU 活跃期间的性能。

**建议**:
*   性能分析 (Profiling): 用 `nanoTime` 或 `measureTime`。
*   业务逻辑超时 (如会话过期): 用 `currentTimeMillis` (因为服务器时间也是墙壁时间)。
*   UI 动画/倒计时: 用 `elapsedRealtime`。

## 5. 常见误区总结

1.  **误用 `currentTimeMillis` 做减法**: 这是最常见的 Bug 来源之一，尤其在分布式系统或长时间运行的服务中。
2.  **忽略单位**: 在日志中打印 `100` 而不注明是 ms 还是 ns。使用 `Duration` 类可以强制携带单位信息。
3.  **在生产环境过度打点**: `measureTime` 虽然有 inline 优化，但频繁的日志 I/O 才是性能杀手。建议在开发/测试环境开启详细计时，生产环境仅对关键路径采样。
4.  **认为 `nanoTime` 是绝对时间**: 永远不要将 `nanoTime()` 的值存入数据库或发送给其他机器，因为它在其他 JVM 或重启后毫无意义。

---

# 综合练习

## 练习 1：重构遗留代码
**任务**: 将以下 Java 风格的 Kotlin 代码重构为使用作用域函数。

*原始代码*:
```kotlin
fun createUser(name: String?, age: Int?): User? {
    if (name != null) {
        val user = User()
        user.name = name
        if (age != null) {
            user.age = age
        } else {
            user.age = 0
        }
        user.createdAt = System.currentTimeMillis()
        return user
    }
    return null
}
```

*参考重构*:
```kotlin
fun createUser(name: String?, age: Int?): User? {
    return name?.let { userName ->
        User().apply {
            name = userName
            this.age = age ?: 0
            createdAt = System.currentTimeMillis()
        }
    }
}
```
*解析*: 使用 `let` 处理 `name` 的空安全，使用 `apply` 进行对象初始化，使代码扁平化。

## 练习 2：实现一个带退避重试的网络请求
**任务**: 使用 `kotlin.time.Duration` 和 `measureTime` 实现一个重试机制，每次失败后等待时间加倍，直到达到最大重试次数或总耗时超过限制。

*参考思路*:
```kotlin
import kotlin.time.Duration
import kotlin.time.Duration.Companion.seconds
import kotlin.time.measureTime

suspend fun <T> retryWithBackoff(
    maxRetries: Int = 3,
    maxTotalDuration: Duration = 10.seconds,
    block: suspend () -> T
): T? {
    var attempts = 0
    var waitTime = 1.seconds
    
    while (attempts < maxRetries) {
        val result = runCatching { block() }
        
        if (result.isSuccess) {
            return result.getOrNull()
        }
        
        attempts++
        if (attempts >= maxRetries) break
        
        // 测量等待前的总耗时（可选，用于更精确的控制）
        println("Attempt $attempts failed. Waiting for $waitTime...")
        delay(waitTime)
        waitTime *= 2 // 指数退避
    }
    return null
}
```

## 练习 3：基准测试对比
**任务**: 编写一个简单的 JMH Benchmark 或手动预热循环，对比 `ArrayList` 和 `LinkedList` 在随机访问场景下的性能差异，并使用 `measureNanoTime` 输出结果。观察 JIT 预热前后的巨大差异。

# Gradle (build.gradle.kts)

## 1. 基础结构与初始化

### 1.1 `build.gradle.kts` vs `build.gradle`
*   **本质区别**：
    *   `.gradle` (Groovy): 动态语言，运行时解析。语法灵活但缺乏静态检查，IDE 自动补全较弱，重构困难。
    *   `.kts` (Kotlin): 静态类型语言，编译时解析。**强类型安全**意味着如果在配置中写错属性名或类型，IDE 会立即报错，而不是在构建失败时才暴露。
*   **语法迁移关键点**：
    *   Groovy: `apply plugin: 'java'` -> Kotlin: `plugins { id("java") }`
    *   Groovy: `dependencies { compile 'group:name:version' }` -> Kotlin: `dependencies { implementation("group:name:version") }`
    *   Groovy: 字符串常用单引号 `'` -> Kotlin: 必须使用双引号 `"` 或三引号 `"""`。

### 1.2 项目基本信息配置
这三个属性定义了项目的坐标（Coordinates），在发布到 Maven 仓库时至关重要。

```kotlin
// group: 组织标识，通常反向域名
group = "com.example.myapp"

// version: 项目版本。SNAPSHOT 表示开发中版本，Release 表示稳定版
version = "1.0.0-SNAPSHOT"

// description: 项目描述，会出现在生成的 POM 文件中
description = "A high-performance Kotlin service"
```

> **最佳实践**：在多模块项目中，通常在根目录的 `build.gradle.kts` 中统一设置 `group` 和 `version`，子模块会自动继承，除非子模块显式覆盖。

### 1.3 Java/Kotlin 版本兼容性
确保编译器目标字节码版本与运行环境一致。

**方式一：通过 Java Extension (传统)**
```kotlin
java {
    // 源代码兼容级别
    sourceCompatibility = JavaVersion.VERSION_17
    // 生成的字节码兼容级别
    targetCompatibility = JavaVersion.VERSION_17
}
```

**方式二：通过 JVM Toolchains (推荐 - Gradle 6.7+)**
Toolchains 允许 Gradle 自动下载和管理指定版本的 JDK，即使本地环境变量指向的是其他版本。这解决了“开发者本地 JDK 版本不一致”导致的构建问题。

```kotlin
kotlin {
    // 告诉 Gradle：我需要 JDK 17 来编译和运行这个项目
    jvmToolchain(17)
}
```

---

## 2. 插件管理 (Plugins)

### 2.1 `plugins {}` 块（声明式插件）
这是应用插件的首选方式。Gradle 会在配置阶段早期解析此块，以便正确隔离类路径。

```kotlin
plugins {
    // Kotlin 官方插件快捷写法
    kotlin("jvm") version "1.9.20"
    
    // 社区/第三方插件标准写法
    id("org.springframework.boot") version "3.2.0"
    id("io.spring.dependency-management") version "1.1.4"
}
```

**结合 Version Catalogs (版本目录)**：
为了避免硬编码版本号，现代 Gradle 项目推荐使用 `libs.versions.toml`。

```kotlin
// build.gradle.kts
plugins {
    alias(libs.plugins.kotlin.jvm)
    alias(libs.plugins.spring.boot)
}
```

### 2.2 传统 `apply()` 方法（命令式插件）
仅用于**脚本插件**（Script Plugins）或某些无法在 `plugins {}` 块中应用的旧插件。

```kotlin
// 应用一个本地脚本插件
apply(from = "config/quality.gradle.kts")

// 应用一个 ID（不推荐，除非必要）
apply(plugin = "java-library")
```
> **注意**：`apply()` 应用的插件无法享受 `plugins {}` 块的优化（如配置缓存的部分支持），且容易导致类路径污染。

### 2.3 常用 Kotlin 相关插件详解
*   **`kotlin("jvm")`**: 基础插件，提供 `compileKotlin` 任务。
*   **`kotlin("plugin.serialization")`**: 启用 `@Serializable` 注解支持。需配合依赖 `implementation("org.jetbrains.kotlinx:kotlinx-serialization-json:...")`。
*   **`kotlin("plugin.allopen")`**: **Spring 必备**。Spring AOP 需要类是非 final 的，而 Kotlin 类默认是 `final`。此插件将所有类开放为 non-final，或者仅开放带有特定注解（如 `@Component`）的类。
    ```kotlin
    allOpen {
        annotation("org.springframework.stereotype.Component")
        annotation("org.springframework.transaction.annotation.Transactional")
    }
    ```
*   **`kotlin("plugin.noarg")`**: **JPA/Hibernate 必备**。为带有特定注解的类生成无参构造函数。

---

## 3. 依赖管理 (Dependencies)

### 3.1 依赖配置项 (Configurations) 深度解析
理解依赖范围是解决 `ClassNotFoundException` 和 `NoSuchMethodError` 的关键。

| 配置项 | 编译时可见 | 运行时可见 | 传递给依赖我的项目? | 典型场景 |
| :--- | :---: | :---: | :---: | :--- |
| `implementation` | ✅ | ✅ | ❌ | 内部实现细节，不希望暴露 API |
| `api` | ✅ | ✅ | ✅ | 库项目的公开 API 接口 |
| `compileOnly` | ✅ | ❌ | ❌ | Lombok, Servlet API (由容器提供) |
| `runtimeOnly` | ❌ | ✅ | ❌ | JDBC 驱动, 日志实现 (SLF4J binding) |
| `testImplementation` | ✅ (测试) | ✅ (测试) | ❌ | JUnit, Mockito |

> **核心原则**：优先使用 `implementation`。只有当你希望下游项目直接使用你依赖中的类时，才使用 `api`。这能显著减少重新编译的时间（Gradle 增量编译优势）。

### 3.2 添加依赖的标准写法
```kotlin
dependencies {
    // 1. Kotlin 标准库 (通常由插件自动添加，但可显式声明)
    implementation(kotlin("stdlib"))
    
    // 2. 外部库: "group:name:version"
    implementation("com.google.guava:guava:32.1.3-jre")
    
    // 3. 项目间依赖 (多模块)
    implementation(project(":common-module"))
    
    // 4. 文件依赖 (本地 jar)
    implementation(files("libs/local-lib.jar"))
}
```

### 3.3 版本目录 (Version Catalogs) - 现代最佳实践
在 `gradle/libs.versions.toml` 文件中集中管理依赖。

**`gradle/libs.versions.toml` 示例：**
```toml
[versions]
kotlin = "1.9.20"
coroutines = "1.7.3"
junit = "5.10.0"

[libraries]
kotlin-stdlib = { module = "org.jetbrains.kotlin:kotlin-stdlib", version.ref = "kotlin" }
coroutines-core = { module = "org.jetbrains.kotlinx:kotlinx-coroutines-core", version.ref = "coroutines" }
junit-jupiter = { module = "org.junit.jupiter:junit-jupiter", version.ref = "junit" }

[bundles]
testing = ["junit-jupiter", "mockito-core"] # 组合依赖

[plugins]
kotlin-jvm = { id = "org.jetbrains.kotlin.jvm", version.ref = "kotlin" }
```

**在 `build.gradle.kts` 中使用：**
```kotlin
dependencies {
    implementation(libs.kotlin.stdlib)
    implementation(libs.coroutines.core)
    testImplementation(libs.bundles.testing)
}
```
> **优势**：类型安全访问（IDE 有补全），单一事实来源（Single Source of Truth），易于跨模块共享版本。

### 3.4 平台依赖与 BOM
BOM (Bill of Materials) 是一组协调版本的依赖列表。

```kotlin
dependencies {
    // 导入 Spring Boot 的 BOM
    implementation(platform("org.springframework.boot:spring-boot-dependencies:3.2.0"))
    
    // 现在添加 Spring 组件时，无需指定版本，BOM 会自动管理
    implementation("org.springframework.boot:spring-boot-starter-web")
    implementation("org.springframework.boot:spring-boot-starter-data-jpa")
}
```

---

## 4. 仓库管理 (Repositories)

### 4.1 常见仓库配置
Gradle 按顺序查找依赖。建议将最常用的仓库放在前面以提高解析速度。

```kotlin
repositories {
    mavenCentral() // 首选，全球镜像多
    
    // 如果需要 Google 库 (Android, Firebase 等)
    google()
    
    // 本地 Maven 缓存 (~/.m2/repository)，用于调试本地发布的库
    mavenLocal()
    
    // 私有 Nexus/Artifactory
    maven("https://repo.mycompany.com/releases") {
        name = "MyCompanyRepo"
        credentials {
            username = project.findProperty("nexusUser") as String? ?: ""
            password = project.findProperty("nexusPassword") as String? ?: ""
        }
    }
}
```

### 4.2 敏感信息处理
**永远不要**将密码硬编码在 `build.gradle.kts` 中并提交到 Git。
1.  **环境变量**：`System.getenv("NEXUS_PASSWORD")`
2.  **Gradle Properties**：在 `~/.gradle/gradle.properties` 中定义，或在 CI/CD 环境中注入。
3.  **Credentials Plugin**：使用 Gradle 内置的安全凭证处理。

---

## 5. 任务定制 (Tasks)

### 5.1 注册自定义任务
使用 `tasks.register` 是懒配置（Lazy Configuration）的最佳实践，只有在任务被请求执行时才会配置它，提升构建性能。

```kotlin
// 创建一个复制配置文件的任务
tasks.register<Copy>("copyProdConfig") {
    group = "build" // 在 gradle tasks 中显示的分组
    description = "Copies production config files to build directory"
    
    from("src/main/resources/prod")
    into("$buildDir/config")
    
    // 只有当输入文件变化时才执行
    inputs.dir("src/main/resources/prod")
    outputs.dir("$buildDir/config")
}
```

### 5.2 配置现有任务
使用 `tasks.named` 或 `tasks.withType` 来配置由插件创建的任务。

**配置 Jar 包 Manifest：**
```kotlin
tasks.jar {
    manifest {
        attributes(
            "Implementation-Title" to project.name,
            "Implementation-Version" to project.version,
            "Main-Class" to "com.example.ApplicationKt"
        )
    }
    
    // 打包依赖到一个胖 Jar (Fat Jar) - 简单做法，生产环境建议用 Shadow 插件
    duplicatesStrategy = DuplicatesStrategy.EXCLUDE
    from(configurations.runtimeClasspath.get().map { if (it.isDirectory) it else zipTree(it) })
}
```

**配置测试任务：**
```kotlin
tasks.test {
    useJUnitPlatform() // 启用 JUnit 5
    
    // 传递系统属性给测试进程
    systemProperty("my.config.path", "/tmp/test-config")
    
    // 增加测试堆内存
    maxHeapSize = "2G"
    
    // 显示测试日志
    testLogging {
        events("passed", "skipped", "failed")
        showStandardStreams = true
    }
}
```

### 5.3 任务依赖链
```kotlin
// 在运行 app 之前，先执行 copyProdConfig
tasks.named("run") {
    dependsOn("copyProdConfig")
}

// 在构建完成后，清理一些临时文件
tasks.build {
    finalizedBy("cleanupTempFiles")
}
```

---

## 6. 多模块项目 (Multi-module Projects)

### 6.1 `settings.gradle.kts` 结构
```kotlin
rootProject.name = "microservices-platform"

// 包含子模块
include("api-gateway")
include("user-service")
include("common-lib")
include("integration-tests")

// 可选：重命名项目路径映射
project(":user-service").projectDir = file("services/user")
```

### 6.2 模块间依赖
在 `user-service/build.gradle.kts` 中：
```kotlin
dependencies {
    // 依赖 common-lib 模块
    implementation(project(":common-lib"))
    
    // 如果只需要测试时依赖
    testImplementation(project(":common-test-utils"))
}
```

### 6.3 共享配置 (Convention Plugins)
避免在每个 `build.gradle.kts` 中重复编写相同的 Kotlin 配置、依赖版本等。

**方案 A: `buildSrc` (简单项目)**
在根目录创建 `buildSrc/src/main/kotlin/my-conventions.gradle.kts`。
```kotlin
// buildSrc/src/main/kotlin/my-conventions.gradle.kts
plugins {
    kotlin("jvm")
}

kotlin {
    jvmToolchain(17)
}

dependencies {
    implementation(libs.kotlin.stdlib) // 这里可以使用 libs 吗？需要特殊配置
}
```
然后在子模块中：`plugins { id("my-conventions") }`

**方案 B: 独立的 Convention 插件模块 (大型项目推荐)**
创建一个单独的 Gradle 项目（如 `build-logic`），发布为插件，供主项目引用。这种方式更干净，支持更好的隔离和测试。

---

## 7. Kotlin 特定配置

### 7.1 编译器选项
```kotlin
kotlin {
    compilerOptions {
        // 严格处理 JSR-305 注解 (@Nullable, @Nonnull)
        freeCompilerArgs.add("-Xjsr305=strict")
        
        // 允许使用实验性 API
        freeCompilerArgs.add("-opt-in=kotlinx.coroutines.ExperimentalCoroutinesApi")
        
        // 将警告视为错误 (CI 环境中非常有用)
        allWarningsAsErrors.set(true)
        
        // 启用渐进式模式 (提前体验新特性，可能有风险)
        progressiveMode.set(true)
    }
}
```

### 7.2 源集配置 (Source Sets)
默认源集是 `main` 和 `test`。你可以添加自定义源集，例如用于集成测试。

```kotlin
sourceSets {
    create("integrationTest") {
        kotlin.srcDir("src/integrationTest/kotlin")
        resources.srcDir("src/integrationTest/resources")
        compileClasspath += sourceSets.main.get().output + configurations.testRuntimeClasspath.get()
        runtimeClasspath += output + compileClasspath
    }
}

// 为集成测试添加依赖
dependencies {
    "integrationTestImplementation"(project(":common-test-utils"))
    "integrationTestRuntimeOnly"(libs.h2.database)
}

// 注册集成测试任务
tasks.register<Test>("integrationTest") {
    description = "Runs integration tests."
    group = "verification"
    testClassesDirs = sourceSets["integrationTest"].output.classesDirs
    classpath = sourceSets["integrationTest"].runtimeClasspath
    shouldRunAfter(tasks.test)
}
```

---

## 8. 高级主题与性能优化

### 8.1 构建扫描 (Build Scans)
在 `settings.gradle.kts` 中启用：
```kotlin
plugins {
    id("com.gradle.develocity") version "3.15" // 或旧版 com.gradle.enterprise
}

develocity {
    buildScan {
        termsOfUseUrl = "https://gradle.com/terms-of-service"
        termsOfUseAgree = "yes"
        publishing.onlyIf { it.buildResult.failures.isNotEmpty() } // 仅失败时上传
    }
}
```
运行后，Gradle 会提供一个 URL，展示详细的依赖解析时间、任务执行耗时图谱，是优化构建速度的神器。

### 8.2 配置缓存 (Configuration Cache)
Gradle 7.4+ 稳定特性。跳过配置阶段，直接重用上次构建的任务图。
在 `gradle.properties` 中启用：
```properties
org.gradle.configuration-cache=true
```
**注意**：你的构建脚本必须是“配置缓存兼容”的。这意味着不能在配置阶段执行 I/O 操作、网络请求或访问未声明的项目属性。如果构建失败，Gradle 会明确指出哪个任务破坏了缓存。

### 8.3 并行构建
```properties
# gradle.properties
org.gradle.parallel=true
org.gradle.caching=true
org.gradle.jvmargs=-Xmx4g -XX:MaxMetaspaceSize=1g
```

### 8.4 依赖冲突解决
当不同依赖引入了同一库的不同版本时：
```kotlin
configurations.all {
    resolutionStrategy {
        // 强制使用特定版本
        force("com.google.guava:guava:32.1.3-jre")
        
        // 排除特定模块
        exclude(group = "log4j", module = "log4j")
        
        // 失败策略：如果有冲突则构建失败，而不是悄悄选择最新版本
        failOnVersionConflict()
    }
}
```
使用 `./gradlew dependencies --configuration runtimeClasspath` 查看依赖树，定位冲突。

---

## 9. 常见问题与调试

1.  **IDE 索引慢/红波浪线**：
    *   点击 IntelliJ IDEA 右侧 Gradle 面板的 "Reload All Gradle Projects"。
    *   如果无效：`File` -> `Invalidate Caches / Restart`。
    *   确保 IDE 使用的 Gradle JVM 版本与项目要求的 Toolchain 一致。

2.  **`Could not resolve ...`**：
    *   检查网络连接。
    *   检查 `repositories` 是否包含了该库所在的仓库。
    *   检查版本号是否拼写正确。

3.  **Kotlin DSL 脚本编译错误**：
    *   Kotlin DSL 脚本本身也是 Kotlin 代码，会被编译。如果语法错误，IDE 会提示。
    *   有时 Gradle 守护进程状态异常，运行 `./gradlew --stop` 重启守护进程。

4.  **查看依赖树**：
    ```bash
    ./gradlew dependencies
    ./gradlew :module-name:dependencies --configuration runtimeClasspath
    ```

---

### 标准模板 (`build.gradle.kts`)

```kotlin
import org.jetbrains.kotlin.gradle.tasks.KotlinCompile

plugins {
    kotlin("jvm") version "1.9.20"
    application
    // 如果使用 Spring:
    // id("org.springframework.boot") version "3.2.0"
    // id("io.spring.dependency-management") version "1.1.4"
}

group = "com.example"
version = "1.0.0-SNAPSHOT"

repositories {
    mavenCentral()
}

dependencies {
    // Kotlin Stdlib
    implementation(kotlin("stdlib"))
    
    // Coroutines
    implementation("org.jetbrains.kotlinx:kotlinx-coroutines-core:1.7.3")
    
    // Logging
    implementation("org.slf4j:slf4j-api:2.0.9")
    runtimeOnly("ch.qos.logback:logback-classic:1.4.11")
    
    // Testing
    testImplementation(kotlin("test"))
    testImplementation("org.junit.jupiter:junit-jupiter:5.10.0")
}

// Kotlin 配置
kotlin {
    jvmToolchain(17)
    
    compilerOptions {
        freeCompilerArgs.addAll(
            "-Xjsr305=strict",
            "-opt-in=kotlin.RequiresOptIn"
        )
    }
}

// Application 插件配置
application {
    mainClass.set("com.example.MainKt")
}

// 测试配置
tasks.test {
    useJUnitPlatform()
    testLogging {
        events("passed", "skipped", "failed")
    }
}

// Jar 包配置
tasks.jar {
    manifest {
        attributes["Main-Class"] = application.mainClass.get()
    }
}
```

# Kotlin Multiplatform

## 1. 核心概念与生态概览

### 1.1 什么是 KMP？
Kotlin Multiplatform (KMP) 是 JetBrains 推出的一种跨平台技术，其核心理念是 **“共享逻辑，保留原生体验”**（Share Logic, Keep Native UI），但在 2024-2026 年间，随着 **Compose Multiplatform** 的成熟，这一理念已演变为 **“可选共享 UI”**。

*   **架构哲学对比**：
    *   **KMP (传统模式)**: 共享业务逻辑（网络、数据、算法），UI 层分别使用 Android (Jetpack Compose/XML) 和 iOS (SwiftUI/UIKit)。
    *   **KMP + Compose MP**: 共享业务逻辑 **以及** UI 层。Compose MP 允许你用同一套 Kotlin 代码编写 UI，并在 Android、iOS、Desktop 和 Web 上渲染为原生或接近原生的组件。
    *   **Flutter/React Native**: “Share Everything”。它们通过自己的渲染引擎（Skia/Impeller 或 JS Bridge）绘制 UI。
        *   *差异点*: KMP 在 iOS 上最终编译为原生二进制代码（通过 Kotlin/Native），没有 JS Bridge 的性能损耗，且能直接调用原生 API。Flutter 则是自绘引擎，UI 一致性极高但包体积较大，且非原生控件感。

*   **2024-2026 演进历程**:
    *   **2023**: KMP 宣布稳定，Compose Multiplatform 进入 Beta。
    *   **2024**: Compose Multiplatform 达到 **Stable** 状态，iOS 支持完善。Kotlin/Wasm 成为 Web 开发的主流推荐替代 JS。
    *   **2025-2026**: KMP 成为 Android 开发的默认扩展选项。Google 官方大力推崇 "KMP for Business Logic, Compose for UI"。工具链（IntelliJ/Android Studio）对 KMP 的支持达到原生级别，调试体验大幅提升。

### 1.2 适用场景分析

| 维度 | 选择 KMP ✅ | 不选择 KMP ❌ |
| :--- | :--- | :--- |
| **团队背景** | 团队已有 Kotlin/Android 基础，希望扩展至 iOS/Web。 | 团队纯 Swift 或纯 JS 背景，无 Kotlin 经验。 |
| **业务类型** | 企业应用、内容展示、工具类、需要复杂业务逻辑复用的 App。 | 重度游戏（建议 Unity/Unreal）、极度依赖最新原生硬件特性（如 ARKit 最新功能）。 |
| **UI 需求** | 接受轻微的平台差异，或愿意使用 Compose MP 统一 UI。 | 要求 100% 像素级一致且必须使用原生平台特定动画/交互，且不想学习 Compose。 |
| **维护成本** | 希望减少重复代码，长期维护多端版本。 | 极简原型，一次性项目，或者各端逻辑完全独立。 |

### 1.3 核心组件介绍
*   **Kotlin/Native**: 将 Kotlin 代码编译为 LLVM IR，进而生成原生二进制文件（ARM64/x86_64）。用于 iOS, macOS, Linux, Windows。
*   **Kotlin/JVM**: 编译为字节码，运行在 JVM 上。用于 Android 和后端服务。
*   **Kotlin/JS & Wasm**:
    *   *JS*: 传统 Web 支持。
    *   *Wasm (WebAssembly)*: 2026 年的主流 Web 目标，性能接近原生，启动更快，不再受限于 JS 单线程模型的部分限制。
*   **Compose Multiplatform**: 基于 Jetpack Compose 的 UI 框架，实现了“一次编写，多端运行”。它在 iOS 上通过将 Compose 树映射为 UIKit 视图或直接绘制（取决于配置）来实现高性能渲染。

---

## 2. 环境搭建与项目结构

### 2.1 开发环境准备
*   **IDE**: 推荐使用 **Android Studio Hedgehog (2023.1.1)** 或更高版本（2026 年建议使用最新的 Stable 版，如 Ladybug 或 Meerkat）。IntelliJ IDEA Ultimate 也是极佳选择。
*   **Kotlin Plugin**: 确保 IDE 内置的 Kotlin 插件更新至最新稳定版（支持 K2 Compiler）。
*   **iOS 环境**:
    *   macOS 机器必不可少。
    *   安装最新版的 **Xcode** 和 **Command Line Tools**。
    *   配置 `xcode-select --install`。
*   **JDK**: 推荐 **JDK 17** 或 **JDK 21**（LTS 版本）。Gradle 8.x+ 对 JDK 17+ 支持最好。

### 2.2 创建第一个 KMP 项目
不要手动从头配置 Gradle。使用官方推荐的 **Kotlin Multiplatform Wizard** (web 版或 IDE 插件版)。
*   选择平台：Android, iOS, Desktop, Web (Wasm)。
*   选择 UI 方案：Compose Multiplatform (推荐) 或 No UI (仅逻辑共享)。
*   生成后，直接在 Android Studio 中打开。

### 2.3 深入理解项目结构
KMP 项目的核心在于 **Source Sets (源集)** 的层级结构。

```text
MyKMPProject/
├── shared/               # 核心共享模块
│   ├── src/
│   │   ├── commonMain/   # 【核心】所有平台共享的代码 (Kotlin 标准库 + KMP 兼容库)
│   │   ├── androidMain/  # 仅 Android 可见的代码 (可调用 Android SDK)
│   │   ├── iosMain/      # 仅 iOS 可见的代码 (可调用 UIKit/Foundation)
│   │   ├── jvmMain/      # Desktop/JVM 特定代码
│   │   ├── jsMain/       # Web JS 特定代码
│   │   └── wasmJsMain/   # Web Wasm 特定代码
│   │   └── nativeMain/   # 【中间层】所有 Native 平台 (iOS, macOS, Linux, Windows) 共享
│   │       └── appleMain/# 【中间层】仅 Apple 平台 (iOS, macOS) 共享
│   └── build.gradle.kts
├── androidApp/           # Android 入口模块 (依赖 shared)
├── iosApp/               # iOS 入口模块 (Xcode 项目，依赖 shared framework)
├── desktopApp/           # Desktop 入口模块
└── webApp/               # Web 入口模块
```

*   **继承关系**: `iosMain` 继承自 `appleMain`，`appleMain` 继承自 `nativeMain`，`nativeMain` 继承自 `commonMain`。
*   **作用**: 你可以在 `nativeMain` 中编写适用于所有原生平台的代码（如文件路径处理），而在 `iosMain` 中处理 iOS 特有的权限请求。

---

## 3. Kotlin 语言特性在多平台中的表现

### 3.1 跨平台兼容的子集
*   **kotlin-stdlib**: 绝大部分标准库可用。注意：`java.io.File` 等在 `common` 中不可用，需使用 `kotlinx-io` 或 `expect/actual`。
*   **kotlinx.coroutines**: 完全支持。`Dispatchers.Main` 在各平台自动映射到主线程（Android UI Thread, iOS Main Queue）。
*   **kotlinx.serialization**: 官方推荐的 JSON/ProtoBuf 序列化方案，完美支持多平台。

### 3.2 平台特定 API 的处理：Expect/Actual
这是 KMP 解决平台差异的核心机制。

**步骤 1: 在 `commonMain` 声明接口 (`expect`)**
```kotlin
// commonMain/kotlin/com/example/Platform.kt
package com.example

expect class Platform() {
    val name: String
}
```

**步骤 2: 在平台特定源集实现 (`actual`)**
```kotlin
// androidMain/kotlin/com/example/Platform.kt
package com.example

import android.os.Build

actual class Platform actual constructor() {
    actual val name: String = "Android ${Build.VERSION.SDK_INT}"
}
```

```kotlin
// iosMain/kotlin/com/example/Platform.kt
package com.example

import platform.UIKit.UIDevice

actual class Platform actual constructor() {
    actual val name: String = UIDevice.currentDevice.systemName() + " " + UIDevice.currentDevice.systemVersion
}
```

*   **最佳实践**: 尽量在 `common` 中定义高层抽象（如 `StorageInterface`），而不是暴露底层细节。避免在 `common` 代码中导入任何 `android.*` 或 `UIKit.*` 包。

---

## 4. 共享业务逻辑层 (Shared Module)

### 4.1 网络请求：Ktor Client
Ktor 是 KMP 事实标准的网络库。

```kotlin
// build.gradle.kts (shared)
implementation("io.ktor:ktor-client-core:$ktorVersion")
implementation("io.ktor:ktor-client-content-negotiation:$ktorVersion")
implementation("io.ktor:ktor-serialization-kotlinx-json:$ktorVersion")

// 平台特定引擎依赖
androidImplementation("io.ktor:ktor-client-okhttp:$ktorVersion")
iosImplementation("io.ktor:ktor-client-darwin:$ktorVersion")
jsImplementation("io.ktor:ktor-client-js:$ktorVersion")
```

**配置单例客户端**:
```kotlin
val httpClient = HttpClient {
    install(ContentNegotiation) {
        json(Json { ignoreUnknownKeys = true })
    }
    // 日志拦截器等
}
```

### 4.2 数据存储
*   **轻量级键值对**: 使用 **[Multiplatform Settings](https://github.com/russhwolf/multiplatform-settings)**。它封装了 Android 的 SharedPreferences/DataStore 和 iOS 的 UserDefaults。
*   **关系型数据库**: **SQLDelight** 是首选。它生成类型安全的 Kotlin API，支持 Android (SQLite), iOS (SQLite), Desktop (SQLite/MySQL/PostgreSQL)。
    *   *Room Multiplatform*: 截至 2026 年，Jetpack Room 的多平台支持仍处于 Alpha/Beta 阶段，生产环境建议优先选用 SQLDelight 或 ObjectBox。

### 4.3 依赖注入：Koin
**Koin** 是最流行的 KMP 兼容 DI 框架，因为它基于纯 Kotlin，无需注解处理器（KAPT/KSP），编译速度快。

```kotlin
// commonMain
val appModule = module {
    single { HttpClientProvider().createClient() }
    factory { Repository(get()) }
    viewModel { MainViewModel(get()) } // 如果使用 Compose MP
}
```
*   **初始化**: 在 Android `Application` 和 iOS `AppDelegate` 中分别调用 `startKoin { modules(appModule) }`。

### 4.4 异步编程：Flow
使用 `StateFlow` 和 `SharedFlow` 作为状态管理的核心。
*   **ViewModel**: 在 `commonMain` 中定义 ViewModel，继承自 `ViewModel` (来自 `androidx.lifecycle:lifecycle-viewmodel-compose` 的多平台版本或 KMP 专用库)。
*   **生命周期**: 确保协程在 ViewModel 清除时取消，避免内存泄漏。

---

## 5. UI 层开发策略

### 5.1 策略一：原生 UI + 共享逻辑 (传统模式)
*   **Android**: 使用 Jetpack Compose (Native)。直接从 `shared` 模块获取 ViewModel。
*   **iOS**: 使用 SwiftUI。
    *   需要将 Kotlin 类暴露给 Swift。Kotlin/Native 会自动生成 `.framework`。
    *   **痛点**: 类型转换。Kotlin `List<String>` 变成 Swift `[String]`，但 `Map` 和复杂对象可能需要手动映射或使用辅助函数。
    *   **数据流**: 在 Swift 中观察 Kotlin Flow 需要使用桥接库（如 `KotlinCoroutinesBridge`）将其转换为 Combine `Publisher` 或 Swift `AsyncStream`。

### 5.2 策略二：Compose Multiplatform (2026 主流推荐)
这是目前效率最高的方案。

*   **基础组件**: `Text`, `Button`, `Column`, `Row` 等在所有平台行为一致。
*   **平台特定修饰符**:
    ```kotlin
    Modifier
        .fillMaxWidth()
        .then(if (isIOS) Modifier.iosSafeAreaPadding() else Modifier.padding(16.dp))
    ```
*   **导航**: 使用 **Navigation Compose**。路由字符串在所有平台通用。
*   **iOS 集成细节**:
    *   Compose MP 在 iOS 上通过 `UIViewControllerRepresentable` 嵌入 SwiftUI。
    *   **键盘处理**: 使用 `WindowInsets.ime` 自动处理键盘弹出遮挡问题。
    *   **滚动**: Compose 的 LazyColumn 在 iOS 上模拟了原生滚动效果（包括弹性回弹）。

### 5.3 Web 与桌面端
*   **Web (Wasm)**: Compose for Web (Wasm) 允许将 Compose UI 编译为 Wasm，在浏览器中运行。性能优于旧版 JS Compose。
*   **Desktop**: Compose for Desktop 使用 Skia 进行渲染。可以打包为 `.exe`, `.dmg`, `.deb`。适合内部工具或跨桌面应用。

---

## 6. 平台互操作性 (Interoperability)

### 6.1 Kotlin/Native 与 iOS (Swift/ObjC)
*   **框架生成**: Gradle 任务 `linkDebugFrameworkIosArm64` 会生成 `.framework`。
*   **类型映射**:
    *   Kotlin `String` <-> Swift `String`
    *   Kotlin `Int` <-> Swift `Int32` (注意精度)
    *   Kotlin `List` <-> Swift `NSArray` (通常转换为 `[Any]`)
    *   Kotlin `Sealed Class` <-> Swift `Enum` (有限支持，复杂层级可能退化为 ObjC 协议)
*   **内存管理**:
    *   Kotlin/Native 现在使用 **新的内存管理器 (New MM)**，默认启用。它支持对象在多线程间自由传递，解决了旧版 MM 的严格线程隔离问题。
    *   **循环引用**: 仍需注意 Kotlin 对象持有 Swift 闭包，Swift 闭包又持有 Kotlin 对象的情况。使用 `[weak self]` 或在 Kotlin 侧使用 `WeakReference`。

### 6.2 Kotlin/JVM 与 Android
*   无缝集成。`shared` 模块编译为 AAR。
*   **ProGuard/R8**: 需要在 Android App 的 `proguard-rules.pro` 中保留 Kotlin 反射和序列化相关的类。

### 6.3 Kotlin/JS 与 JavaScript
*   使用 `external` 关键字声明 JS 函数。
*   **npm 依赖**: 可以在 Gradle 中直接引入 npm 包，Kotlin/JS 编译器会处理绑定。

---

## 7. 测试策略

### 7.1 单元测试 (Common Test)
*   在 `commonTest` 中编写测试，使用 `kotlin.test` 断言库。
*   这些测试会在 JVM、Android、iOS 模拟器等多个环境中运行。
*   **Mocking**: 使用 **MockK** (支持多平台) 或手动实现 Fake 接口。

### 7.2 平台特定测试
*   **Android**: 标准的 Instrumented Tests (`androidTest`)。
*   **iOS**: 可以编写 XCTest，调用 Kotlin 生成的 Framework 进行测试。但更常见的做法是在 `iosTest` 源集中使用 Kotlin 编写测试，并由 Gradle 驱动在模拟器上运行。

### 7.3 UI 测试
*   **Compose Multiplatform**: 使用 `compose-ui-test`。它可以针对 Android 和 Desktop 进行截图测试和交互测试。
*   **iOS UI 测试**: 目前主要依赖 Xcode 的原生 UI 测试，或者使用 Detox 等第三方工具。Compose MP 的 iOS UI 测试支持正在不断完善中。

---

## 8. 工程化与 CI/CD

### 8.1 Gradle 构建优化
*   **Configuration Cache**: 务必启用 `org.gradle.configuration-cache=true`，大幅缩短配置阶段时间。
*   **K2 Compiler**: 启用新的 Kotlin K2 编译器 (`languageSettings.useK2 = true`)，提供更快的编译速度和更好的错误提示。
*   **并行构建**: `org.gradle.parallel=true`。

### 8.2 持续集成 (CI)
*   **GitHub Actions / GitLab CI**:
    *   需要 macOS Runner 来构建和测试 iOS 部分。这是成本大头。
    *   **策略**: 仅在 PR 合并到 main 分支或 Release 标签触发时运行完整的 iOS 构建和测试。日常 PR 只运行 Android、JVM 和 Common 测试。
*   **缓存**: 使用 Gradle Build Cache 和 CocoaPods/Swift Package Manager 缓存。

### 8.3 发布管理
*   **Maven Central**: 发布 `shared` 模块的 AAR 和 KLib。
*   **SPM (Swift Package Manager)**: 2026 年的最佳实践是将 Kotlin/Native 框架包装为 SPM 包，方便 iOS 开发者集成。Kotlin 官方插件支持直接生成 SPM 兼容的结构。

---

## 9. 高级主题与性能优化

### 9.1 性能调优
*   **启动时间**: Kotlin/Native 的二进制初始化有开销。使用 `initWith` 延迟初始化非必要模块。
*   **包体积**:
    *   启用 R8/ProGuard 进行 Tree Shaking。
    *   移除未使用的 Ktor 引擎和序列化格式。
    *   iOS Framework 可以使用 Bitcode 压缩。
*   **内存**: 使用 Android Profiler 和 Xcode Instruments 监控内存。注意 Kotlin 协程在后台线程的生命周期。

### 9.2 架构模式：MVI + Clean Architecture
*   **Common Layer**:
    *   `Domain`: UseCases, Entities (纯 Kotlin)。
    *   `Data`: Repositories, DataSources (Ktor, SQLDelight)。
    *   `Presentation`: ViewModels, State/UI States (Flow)。
*   **UI Layer**:
    *   Android/iOS/Desktop 仅负责渲染 State 和发送 Intent。

### 9.3 第三方库生态 (2026 推荐)
*   **Network**: Ktor
*   **DI**: Koin
*   **Database**: SQLDelight
*   **Image Loading**: Coil (Coil 3+ 完美支持 KMP 和 Compose MP)
*   **Navigation**: Voyager (轻量级) 或 Navigation Compose (官方)
*   **Date/Time**: kotlinx-datetime (取代 java.time/threetenbp)

---

## 10. 实战项目案例思路

### 案例：多平台笔记应用 (NoteMaster)
1.  **Shared 模块**:
    *   定义 `Note` 数据类。
    *   `NoteRepository` 接口。
    *   `SqlDelightNoteDataSource` 实现数据库 CRUD。
    *   `NoteViewModel` 暴露 `StateFlow<List<Note>>`。
2.  **Android App**:
    *   Jetpack Compose UI。
    *   订阅 ViewModel，显示列表。
    *   点击添加跳转详情页。
3.  **iOS App**:
    *   SwiftUI List。
    *   通过 `KotlinCoroutinesBridge` 将 Flow 转为 `@Published` 属性。
    *   或者直接采用 **Compose Multiplatform**，共用 UI 代码。
4.  **亮点**:
    *   离线优先：数据先存本地 SQLite，后台同步（模拟）。
    *   深色模式：在 `common` 中定义主题颜色，各平台适配。

---

## 11. 常见陷阱与 FAQ

1.  **线程模型**:
    *   *问题*: 在 iOS 上更新 UI 必须在 Main Thread。
    *   *解决*: Compose MP 和 Ktor 内部已处理大部分情况。手动调用原生 API 时，务必使用 `Dispatchers.Main`。
2.  **日期时间**:
    *   *问题*: `java.util.Date` 不可用。
    *   *解决*: 始终使用 `kotlinx-datetime`。
3.  **浮点数精度**:
    *   *问题*: 不同平台浮点运算可能有微小差异。
    *   *解决*: 金融计算务必使用 `BigDecimal` (需引入特定库) 或以整数（分）为单位存储。
4.  **Gradle 同步慢**:
    *   *解决*: 检查网络代理（下载 Gradle 依赖和 CocoaPods）。使用国内镜像源。启用 Configuration Cache。
5.  **iOS 模拟器 vs 真机**:
    *   *问题*: 架构不同 (x86_64 vs arm64)。
    *   *解决*: Gradle 会自动处理。确保 Xcode Scheme 设置正确。调试时，Xcode 附加到进程即可断点 Kotlin 代码（需配置 dSYM）。

---
# Kotlin 常用库

## 1. Kotlin 标准库 (kotlin-stdlib)
> **定位**：Kotlin 语言的基石。无论你在 JVM、Android、JS 还是 Native 平台开发，这部分 API 都是统一且默认可用的。

### 1.1 集合操作 (Collections)
Kotlin 区分了**只读（Read-only）**和**可变（Mutable）**集合接口，这是防止副作用的关键设计。

*   **不可变 vs 可变**：
    *   `List<T>` / `MutableList<T>`
    *   `Set<T>` / `MutableSet<T>`
    *   `Map<K, V>` / `MutableMap<K, V>`
    *   *最佳实践*：函数参数尽量接收只读接口，仅在内部需要修改时才转换为 mutable 版本。

*   **高阶函数实战**：
    ```kotlin
    val numbers = listOf(1, 2, 3, 4, 5, 6)

    // map: 转换元素
    val doubled = numbers.map { it * 2 } // [2, 4, 6, 8, 10, 12]

    // filter: 过滤元素
    val evens = numbers.filter { it % 2 == 0 } // [2, 4, 6]

    // flatMap: 扁平化映射（常用于嵌套集合）
    val lists = listOf(listOf(1, 2), listOf(3, 4))
    val flat = lists.flatMap { it } // [1, 2, 3, 4]

    // fold/reduce: 聚合操作
    val sum = numbers.fold(0) { acc, i -> acc + i } // 初始值为0的累加
    val product = numbers.reduce { acc, i -> acc * i } // 无初始值，直接用前两个元素开始
    ```

*   **序列 (Sequences)**：
    *   **原理**：`Sequence` 是惰性求值的。中间操作（如 `map`, `filter`）不会立即执行，直到终端操作（如 `toList`, `first`）触发。
    *   **场景**：处理大型数据集或无限流时，避免创建大量中间临时集合，节省内存。
    ```kotlin
    val sequence = sequenceOf(1, 2, 3, 4, 5)
        .map { 
            println("Mapping $it") 
            it * 2 
        }
        .filter { 
            println("Filtering $it") 
            it > 4 
        }
    
    // 此时没有任何打印输出
    val firstResult = sequence.first() 
    // 输出: Mapping 1, Filtering 2, Mapping 2, Filtering 4, Mapping 3, Filtering 6 -> 返回 6
    ```

### 1.2 空安全与类型检查
*   **Elvis 运算符 (`?:`)**：提供默认值。
    ```kotlin
    val name: String? = null
    val displayName = name ?: "Guest" // 如果 name 为 null，则使用 "Guest"
    ```
*   **智能转换 (Smart Casts)**：
    ```kotlin
    fun printLength(obj: Any) {
        if (obj is String) {
            // 编译器自动将 obj 视为 String，无需 obj as String
            println(obj.length) 
        }
    }
    ```
*   **作用域函数选择指南**：
    | 函数 | 上下文对象引用 | 返回值 | 典型用途 |
    | :--- | :---: | :---: | :--- |
    | `let` | `it` | Lambda 结果 | 空安全调用 (`obj?.let {}`)，变量作用域限制 |
    | `run` | `this` | Lambda 结果 | 对象配置并计算结果 |
    | `with` | `this` | Lambda 结果 | 对同一对象执行多个操作（非扩展函数） |
    | `apply` | `this` | 对象本身 | 对象初始化/配置 (Builder 模式) |
    | `also` | `it` | 对象本身 | 副作用操作（如日志打印），不改变对象 |

### 1.3 字符串与文本处理
*   **字符串模板**：支持任意表达式。
    ```kotlin
    val price = 100
    println("The price is \$${price * 1.1}") // The price is $110.0
    ```
*   **Regex**：
    ```kotlin
    val regex = """(\d{4})-(\d{2})-(\d{2})""".toRegex()
    val match = regex.find("2023-10-05")
    if (match != null) {
        println(match.groupValues[1]) // 2023
    }
    ```

### 1.4 协程基础支持 (Stdlib 中的挂起概念)
虽然协程实现在 `kotlinx-coroutines`，但 `suspend` 关键字和基础接口在 stdlib 中定义。
*   **Suspend Function**：可以在不阻塞线程的情况下暂停执行。
*   **注意**：`runBlocking` 仅用于测试或桥接同步/异步代码，严禁在 Android Main 线程或服务器请求处理线程中直接使用，否则会导致卡顿。

---

## 2. 序列化 (kotlinx.serialization)
> **定位**：JetBrains 官方出品，编译期生成代码，性能优于反射方案（Gson/Jackson），且完美支持 Kotlin 特有类型（如 data class, sealed class）。

### 2.1 核心配置
需要在 `build.gradle.kts` 中添加插件：
```kotlin
plugins {
    kotlin("plugin.serialization") version "1.9.0"
}
dependencies {
    implementation("org.jetbrains.kotlinx:kotlinx-serialization-json:1.6.0")
}
```

### 2.2 JSON 处理实战
*   **基本用法**：
    ```kotlin
    @Serializable
    data class User(val name: String, val age: Int)

    val user = User("Alice", 30)
    val json = Json.encodeToString(user) // {"name":"Alice","age":30}
    val decoded = Json.decodeFromString<User>(json)
    ```

*   **关键配置 (`Json` 实例)**：
    ```kotlin
    val format = Json {
        ignoreUnknownKeys = true // 后端多发了字段，前端不会崩溃
        encodeDefaults = false   // 如果字段值等于默认值，序列化时省略该字段，减小体积
        prettyPrint = true       // 格式化输出，便于调试
        isLenient = true         // 允许非严格 JSON（如注释、尾随逗号）
    }
    ```

*   **自定义序列化器**：
    当需要处理非标准格式（如将 Date 存为时间戳字符串）时：
    ```kotlin
    object DateSerializer : KSerializer<Date> {
        override val descriptor = PrimitiveSerialDescriptor("Date", PrimitiveKind.LONG)
        override fun serialize(encoder: Encoder, value: Date) {
            encoder.encodeLong(value.time)
        }
        override fun deserialize(decoder: Decoder): Date {
            return Date(decoder.decodeLong())
        }
    }
    
    @Serializable
    data class Event(@Serializable(with = DateSerializer::class) val timestamp: Date)
    ```

### 2.3 多态序列化
处理继承结构时，必须指定鉴别器（Discriminator）：
```kotlin
@Serializable
sealed class Shape {
    @Serializable
    data class Circle(val radius: Double) : Shape()
    
    @Serializable
    data class Rectangle(val width: Double, val height: Double) : Shape()
}

// 序列化结果: {"type":"Circle","radius":5.0}
val json = Json { classDiscriminator = "type" }.encodeToString(Shape.Circle(5.0))
```

---

## 3. I/O 库 (kotlinx-io)
> **定位**：新一代多平台 I/O。相比 `java.io`，它更安全（自动资源管理）、更高效（Buffer 池）、更统一（跨平台 API 一致）。

### 3.1 核心抽象
*   **Buffer**：内部维护字节数组，支持动态扩容。它是 `Source` 和 `Sink` 背后的存储引擎。
*   **Source**：数据源（类似 InputStream），提供 `readByte`, `readShort`, `readUtf8Line` 等类型安全读取方法。
*   **Sink**：数据目的地（类似 OutputStream），提供 `writeByte`, `writeString` 等方法。

### 3.2 文件操作示例
```kotlin
import kotlinx.io.Files
import kotlinx.io.readString
import kotlinx.io.writeString

// 写入文件
val path = Path("test.txt")
Files.sink(path).buffer().use { sink ->
    sink.writeString("Hello, Kotlin IO!")
}

// 读取文件
val content = Files.source(path).buffer().use { source ->
    source.readString()
}
println(content)
```
*注意：`use` 块确保了流在使用后自动关闭，避免资源泄漏。*

### 3.3 为什么选择 kotlinx-io？
1.  **多平台**：在 iOS (Native) 和 JS 上也能用同样的 API 读写文件/内存。
2.  **结构化**：不再需要手动处理 `byte[]` 数组越界问题。
3.  **协程友好**：虽然核心是阻塞式 API，但设计上易于封装为 suspend 函数，且正在逐步原生支持异步 I/O。

---

## 4. 日期与时间 (kotlinx-datetime)
> **定位**：解决 `java.util.Date` 和 `Calendar` 的设计缺陷（可变性、月份从0开始、时区混乱）。API 风格接近 Java 8 `java.time` 但更简洁，且支持多平台。

### 4.1 核心类型解析
*   **Instant**：精确到纳秒的时间点，始终基于 UTC。适合存储数据库、网络传输。
*   **LocalDateTime**：日历上的“墙钟时间”，不包含时区信息。适合展示给用户看（如“会议在下午3点”）。
*   **TimeZone**：时区规则集合。

### 4.2 常见操作
```kotlin
import kotlinx.datetime.*

// 1. 获取当前时间
val now = Clock.System.now() // Instant

// 2. 转换为本地时间 (例如上海时区)
val shanghaiZone = TimeZone.of("Asia/Shanghai")
val localDt = now.toLocalDateTime(shanghaiZone)

// 3. 构造特定时间
val birthday = LocalDate(1990, Month.MAY, 9)

// 4. 时间运算
val nextWeek = Clock.System.now().plus(7, DateTimeUnit.DAY)

// 5. 计算两个日期的间隔
val period = birthday.periodUntil(LocalDate(2026, Month.MAY, 9), shanghaiZone)
println("${period.years} years") // 36 years
```

### 4.3 格式化
kotlinx-datetime 本身不提供复杂的 `SimpleDateFormat` 式格式化，建议配合 `kotlinx-datetime-serialization` 或使用 ISO 8601 标准字符串交互。如果需要复杂格式化，JVM 上可转回 `java.time` 处理。

---

## 5. 并发与异步 (kotlinx-coroutines)
> **定位**：Kotlin 异步编程的灵魂。通过“挂起”而非“回调”来解决地狱嵌套问题。

### 5.1 结构化并发 (Structured Concurrency)
核心原则：**协程的生命周期与其 Scope 绑定**。父协程取消，子协程自动取消；子协程抛出异常，父协程感知。

*   **Scope 选择**：
    *   `viewModelScope` (Android): 随 ViewModel 销毁而取消。
    *   `lifecycleScope` (Android): 随 Activity/Fragment 生命周期取消。
    *   `CoroutineScope(Dispatchers.IO)`: 后台任务。
    *   `supervisorScope`: 子协程失败不影响其他子协程（适用于并行独立任务）。

### 5.2 Flow：冷数据流
Flow 是响应式流的 Kotlin 实现，支持背压（Backpressure）。

```kotlin
// 定义一个 Flow
fun observeNumbers(): Flow<Int> = flow {
    for (i in 1..5) {
        delay(1000) // 模拟耗时操作
        emit(i)
    }
}

// 收集 Flow
lifecycleScope.launch {
    observeNumbers()
        .filter { it % 2 == 0 }
        .map { "Number: $it" }
        .flowOn(Dispatchers.Default) // 切换上游执行线程
        .collect { text ->
            println(text) // 在主线程更新 UI
        }
}
```

*   **StateFlow vs SharedFlow**:
    *   `StateFlow`: 有初始值，只保留最新值，适合状态管理（UI State）。
    *   `SharedFlow`: 无初始值，可配置回放，适合事件总线（One-time events）。

### 5.3 异常处理
在协程中，未捕获的异常会取消整个 Scope。
```kotlin
supervisorScope {
    launch {
        try {
            doNetworkRequest()
        } catch (e: IOException) {
            // 处理异常，防止 Scope 被取消
        }
    }
    launch {
        doAnotherTask() // 即使上一个失败，这个也会继续运行
    }
}
```

---

## 6. 依赖注入 (Koin / Hilt)

### 6.1 Koin (推荐用于多平台/轻量级项目)
*   **特点**：纯 Kotlin 编写，无代码生成，启动快，DSL 易读。
*   **定义模块**：
    ```kotlin
    val appModule = module {
        single { Repository() } // 单例
        factory { Service(get()) } // 每次注入创建新实例，get() 自动注入 Repository
    }
    ```
*   **注入**：
    ```kotlin
    class MyViewModel : ViewModel() {
        private val repo: Repository by inject()
    }
    ```

### 6.2 Hilt (推荐用于大型 Android 项目)
*   **特点**：基于 Dagger，编译期生成代码，性能极致，强类型检查，但配置稍繁琐。
*   **优势**：与 Android 生命周期组件（Activity, Fragment, Service）无缝集成。

---

## 7. 网络请求 (Ktor Client / Retrofit)

### 7.1 Ktor Client (多平台首选)
*   **异步天然支持**：所有请求函数都是 `suspend`。
*   **插件化架构**：
    ```kotlin
    val client = HttpClient(CIO) {
        install(ContentNegotiation) {
            json(Json { ignoreUnknownKeys = true })
        }
        install(Logging) {
            level = LogLevel.BODY
        }
    }
    
    // 发起请求
    val user: User = client.get("https://api.example.com/user/1").body()
    ```

### 7.2 Retrofit (JVM/Android 传统强者)
*   **优势**：生态极其丰富，注解式定义清晰。
*   **结合 Coroutines**：
    ```kotlin
    interface ApiService {
        @GET("user/{id}")
        suspend fun getUser(@Path("id") userId: String): User
        
        @GET("users")
        fun getUsers(): Flow<List<User>> // 返回 Flow
    }
    ```

---

## 8. 测试库 (kotest / Mockk)

### 8.1 Kotest
比 JUnit 更强大的测试框架，支持多种测试风格。
*   **StringSpec 示例**：
    ```kotlin
    class MyTest : StringSpec({
        "length should return size of string" {
            "hello".length shouldBe 5
        }
        "startswith should match" {
            "hello world" should startWith("hello")
        }
    })
    ```

### 8.2 Mockk
专为 Kotlin 设计的 Mock 库，完美支持协程和扩展函数。
*   **基本用法**：
    ```kotlin
    interface Repo {
        suspend fun fetchUser(id: Int): User
    }

    @Test
    fun testViewModel() = runTest {
        val mockRepo = mockk<Repo>()
        val fakeUser = User("Test", 20)
        
        //  stubbing
        coEvery { mockRepo.fetchUser(1) } returns fakeUser
        
        val vm = MyViewModel(mockRepo)
        vm.loadUser(1)
        
        // verification
        coVerify { mockRepo.fetchUser(1) }
    }
    ```
    *注意：Mock 协程函数时使用 `coEvery` 和 `coVerify`。*

