# 1. 基础概念

## TypeScript 简介

### 什么是 TypeScript
TypeScript 是由微软开发的开源编程语言，它是 JavaScript 的超集，为 JavaScript 添加了静态类型系统。

### 核心特性
- **静态类型检查**：在编译时检测类型错误
- **类型推断**：自动推断变量类型
- **接口和类**：面向对象编程支持
- **泛型**：创建可重用的类型安全组件
- **装饰器**：元编程支持
- **模块系统**：代码组织和复用

### 优势
- 提高代码质量和可维护性
- 增强开发工具支持（智能提示、重构）
- 早期错误检测
- 更好的团队协作
- 渐进式采用（可逐步迁移现有 JS 代码）

## 与 JavaScript 的关系

### 超集关系
```
TypeScript ⊃ JavaScript
```
所有有效的 JavaScript 代码都是有效的 TypeScript 代码。

### 语法兼容性
```javascript
// 这是有效的 JavaScript 和 TypeScript
function greet(name) {
    return "Hello, " + name;
}
```

```typescript
// 这是 TypeScript 特有语法
function greet(name: string): string {
    return "Hello, " + name;
}
```

### 编译转换
```
TypeScript (.ts) → TypeScript Compiler → JavaScript (.js)
```

### 版本对应关系
| TypeScript 版本 | 支持的 ECMAScript 版本 |
|----------------|----------------------|
| TS 1.0         | ES3, ES5             |
| TS 2.0         | ES3, ES5, ES2015     |
| TS 3.0         | ES3, ES5, ES2015+    |
| TS 4.0+        | ES3, ES5, ES2015+    |

## 环境搭建与配置

### 安装 Node.js
```bash
 检查 Node.js 是否已安装
node --version
npm --version

 如果未安装，从官网下载或使用包管理器
 Windows: https://nodejs.org/
 macOS: brew install node
 Ubuntu: sudo apt install nodejs npm
```

### 安装 TypeScript
```bash
 全局安装
npm install -g typescript

 检查安装
tsc --version

 本地安装（推荐用于项目）
npm install typescript --save-dev
```

### 初始化项目
```bash
 创建项目目录
mkdir my-typescript-project
cd my-typescript-project

 初始化 npm 项目
npm init -y

 初始化 TypeScript 配置
tsc --init
```

### 编辑器配置
#### VS Code（推荐）
- 自动支持 TypeScript
- 安装官方 TypeScript 插件
- 配置工作区设置

#### 其他编辑器
- WebStorm：内置 TypeScript 支持
- Sublime Text：安装 TypeScript 插件
- Vim：安装相关插件

### 基本项目结构
```
my-typescript-project/
├── package.json
├── tsconfig.json
├── src/
│   └── index.ts
├── dist/
└── node_modules/
```

## 编译流程

### 编译命令
```bash
 编译单个文件
tsc hello.ts

 编译整个项目
tsc

 监听模式
tsc --watch

 指定输出目录
tsc --outDir ./dist

 指定目标版本
tsc --target ES2017
```

### 编译过程详解

#### 1. 词法分析（Lexical Analysis）
将源代码分解为标记（Tokens）
```typescript
// 源代码
let message: string = "Hello";

// 标记化结果
[LET, IDENTIFIER(message), COLON, STRING, EQUALS, STRING_LITERAL(Hello), SEMICOLON]
```

#### 2. 语法分析（Syntax Analysis）
构建抽象语法树（AST）
```typescript
// AST 结构示例
VariableDeclaration {
    kind: "let",
    name: "message",
    type: "string",
    initializer: StringLiteral("Hello")
}
```

#### 3. 类型检查（Type Checking）
验证类型安全性和一致性
```typescript
// 正确的类型使用
let count: number = 42;        // ✓
count = "hello";               // ✗ 编译错误

// 函数类型检查
function add(a: number, b: number): number {
    return a + b;
}
add(1, 2);                     // ✓
add("1", "2");                 // ✗ 编译错误
```

#### 4. 代码生成（Code Generation）
将 TypeScript 转换为 JavaScript
```typescript
// TypeScript 源码
class Greeter {
    greeting: string;
    
    constructor(message: string) {
        this.greeting = message;
    }
    
    greet(): string {
        return "Hello, " + this.greeting;
    }
}
```

```javascript
// 编译后的 JavaScript (ES5)
var Greeter = /** @class */ (function () {
    function Greeter(message) {
        this.greeting = message;
    }
    Greeter.prototype.greet = function () {
        return "Hello, " + this.greeting;
    };
    return Greeter;
}());
```

### 编译器架构

#### 主要组件
1. **Scanner（扫描器）**：词法分析
2. **Parser（解析器）**：语法分析
3. **Binder（绑定器）**：符号绑定
4. **Checker（检查器）**：类型检查
5. **Emitter（发射器）**：代码生成

#### 编译阶段
```
Source Code → Scanner → Parser → Binder → Checker → Emitter → JavaScript
```

### tsconfig.json 配置详解

#### 基本配置
```json
{
  "compilerOptions": {
    "target": "ES2017",
    "module": "commonjs",
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "**/*.spec.ts"]
}
```

#### 重要编译选项
```json
{
  "compilerOptions": {
    // 基础选项
    "target": "ES2017",           // 编译目标
    "module": "commonjs",         // 模块系统
    "lib": ["ES2017", "DOM"],     // 库定义文件
    
    // 严格类型检查
    "strict": true,               // 启用所有严格检查
    "noImplicitAny": true,        // 不允许隐式 any
    "strictNullChecks": true,     // 严格的 null 检查
    "strictFunctionTypes": true,  // 严格的函数类型检查
    
    // 模块解析
    "moduleResolution": "node",   // 模块解析策略
    "baseUrl": "./",              // 基础目录
    "paths": {},                  // 路径映射
    
    // 输出选项
    "outDir": "./dist",           // 输出目录
    "rootDir": "./src",           // 源码根目录
    "removeComments": true,       // 移除注释
    "sourceMap": true,            // 生成 source map
    
    // 其他选项
    "esModuleInterop": true,      // ES 模块互操作
    "skipLibCheck": true,         // 跳过库文件检查
    "forceConsistentCasingInFileNames": true  // 强制文件名大小写一致
  }
}
```

### 编译器 API 使用

#### 程序化编译
```typescript
import * as ts from "typescript";

const source = "let x: string = 'hello world';";

// 创建源文件
const sourceFile = ts.createSourceFile(
    "test.ts",
    source,
    ts.ScriptTarget.ES2015,
    true
);

// 编译选项
const options: ts.CompilerOptions = {
    target: ts.ScriptTarget.ES2015,
    module: ts.ModuleKind.CommonJS
};

// 编译
const result = ts.transpile(source, options);
console.log(result);
```

### 构建工具集成

#### Webpack 配置
```javascript
// webpack.config.js
module.exports = {
    entry: "./src/index.ts",
    module: {
        rules: [
            {
                test: /\.tsx?$/,
                use: 'ts-loader',
                exclude: /node_modules/,
            }
        ]
    },
    resolve: {
        extensions: ['.tsx', '.ts', '.js']
    },
    output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
    }
};
```

#### Gulp 配置
```javascript
const gulp = require('gulp');
const ts = require('gulp-typescript');

const tsProject = ts.createProject('tsconfig.json');

gulp.task('compile', () => {
    return tsProject.src()
        .pipe(tsProject())
        .js.pipe(gulp.dest('dist'));
});
```

### 调试支持

#### Source Maps
```json
{
  "compilerOptions": {
    "sourceMap": true,
    "inlineSourceMap": false,
    "inlineSources": true
  }
}
```

#### 调试配置（VS Code）
```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "Debug TypeScript",
            "program": "${workspaceFolder}/src/index.ts",
            "outFiles": ["${workspaceFolder}/dist/**/*.js"],
            "preLaunchTask": "tsc: build"
        }
    ]
}
```

# 2. 基本类型系统

## 原始类型（Primitive Types）

### boolean 类型
表示逻辑值：true 或 false

```typescript
// 基本声明
let isDone: boolean = false;
let isCompleted: boolean = true;

// 从表达式推断
let hasPermission = true; // 类型推断为 boolean

// 在条件语句中使用
if (isDone) {
    console.log("Task completed");
}

// 逻辑运算
let canAccess = isDone && hasPermission; // boolean
let shouldRetry = !isDone || !hasPermission; // boolean
```

### number 类型
表示所有数字类型（整数和浮点数）

```typescript
// 整数
let decimal: number = 42;
let hex: number = 0xf00d;        // 十六进制
let binary: number = 0b1010;     // 二进制
let octal: number = 0o744;       // 八进制

// 浮点数
let float: number = 3.14;
let scientific: number = 1.23e5; // 科学计数法

// 特殊数值
let infinity: number = Infinity;
let notANumber: number = NaN;

// 从表达式推断
let count = 10; // number
let result = 10 / 3; // number

// 数学运算
let sum = decimal + float; // number
let product = decimal * 2; // number
```

### string 类型
表示文本数据

```typescript
// 字符串字面量
let color: string = "blue";
let fullName: string = 'Bob Smith';

// 模板字符串
let firstName: string = "John";
let lastName: string = "Doe";
let fullName2: string = `${firstName} ${lastName}`;
let greeting: string = `Hello, ${fullName2}!`;

// 多行字符串
let multiline: string = `
    This is a
    multiline
    string
`;

// 字符串方法
let message: string = "Hello World";
let upperCase = message.toUpperCase(); // string
let length = message.length; // number
let substring = message.substring(0, 5); // string

// 从表达式推断
let text = "Hello"; // string
let template = `Count: ${count}`; // string
```

### bigint 类型
表示任意精度的整数（ES2020）

```typescript
// BigInt 字面量
let bigNumber: bigint = 123n;
let anotherBig: bigint = BigInt(456);

// BigInt 运算
let sumBig = bigNumber + anotherBig; // bigint
let productBig = bigNumber * 2n; // 注意：必须使用 n 后缀

// 与 number 的区别
let regularNumber: number = 123;
// let invalid = bigNumber + regularNumber; // 错误：不能混合使用

// BigInt 方法
let parsedBig = BigInt("9007199254740991");
let maxSafe = BigInt(Number.MAX_SAFE_INTEGER);

// 注意事项
// BigInt 不能与 Math 对象一起使用
// BigInt 不能序列化为 JSON
```

### symbol 类型
表示唯一的标识符（ES2015）

```typescript
// 创建 Symbol
let sym1: symbol = Symbol();
let sym2: symbol = Symbol("key"); // 可选描述
let sym3: symbol = Symbol("key");

// Symbol 是唯一的
console.log(sym2 === sym3); // false

// Symbol 作为对象属性键
let obj = {
    [sym1]: "value1",
    [sym2]: "value2"
};

// 获取 Symbol 属性
console.log(obj[sym1]); // "value1"

// 全局 Symbol 注册表
let globalSym = Symbol.for("globalKey");
let sameGlobalSym = Symbol.for("globalKey");
console.log(globalSym === sameGlobalSym); // true

// 获取 Symbol 描述
console.log(sym2.description); // "key"

// 内置 Symbol
let iteratorSymbol = Symbol.iterator;
let toStringSymbol = Symbol.toStringTag;
```

## 特殊类型（Special Types）

### any 类型
禁用类型检查，可以赋值给任何类型

```typescript
// any 类型变量
let notSure: any = 4;
notSure = "maybe a string";
notSure = false; // 也可以是 boolean

// any 数组
let list: any[] = [1, true, "free"];
list[1] = 100;

// any 对象属性
let looselyTyped: any = 4;
looselyTyped.ifItExists(); // 不会报错
looselyTyped.toFixed(); // 不会报错

// 与 unknown 的区别
let anyValue: any = "hello";
let stringValue: string = anyValue; // 允许，但不安全

// 注意：过度使用 any 会失去类型安全
```

### unknown 类型
类型安全的 any，需要类型检查后才能使用

```typescript
// unknown 基本使用
let value: unknown = 4;
value = "hello";
value = true;

// 不能直接赋值给其他类型
// let stringValue: string = value; // 错误！

// 需要类型检查或断言
if (typeof value === "string") {
    let stringValue: string = value; // 正确
    console.log(value.toUpperCase());
}

// 类型断言
let strValue = value as string; // 类型断言
// 或者
let strValue2 = <string>value; // 另一种断言语法

// 使用类型保护函数
function isString(value: unknown): value is string {
    return typeof value === "string";
}

if (isString(value)) {
    console.log(value.toUpperCase()); // 安全使用
}
```

### void 类型
表示没有返回值的函数

```typescript
// 函数没有返回值
function warnUser(): void {
    console.log("This is my warning message");
}

// void 变量通常只能是 undefined 或 null
let unusable: void = undefined;
// unusable = null; // 在 strictNullChecks 下会报错

// 箭头函数的 void 返回
const logMessage = (): void => {
    console.log("Logging...");
};

// 实际上很少需要显式声明 void
function implicitVoid() {
    console.log("No return statement");
} // 推断为 void
```

### null 和 undefined 类型
表示空值和未定义值

```typescript
// 基本声明
let u: undefined = undefined;
let n: null = null;

// 在 strictNullChecks 模式下
let num: number = 42;
// num = null; // 错误！
// num = undefined; // 错误！

// 联合类型与 null/undefined
let nullableNum: number | null = 42;
nullableNum = null; // 正确

let optionalStr: string | undefined = "hello";
optionalStr = undefined; // 正确

// 可选参数和属性
function greet(name?: string) { // name: string | undefined
    console.log(`Hello, ${name || "Guest"}`);
}

interface User {
    name: string;
    email?: string; // email: string | undefined
}

// null 和 undefined 的比较
console.log(null == undefined); // true
console.log(null === undefined); // false
```

### never 类型
表示永远不会发生的值的类型

```typescript
// 永远不会返回的函数
function error(message: string): never {
    throw new Error(message);
}

// 永远不会结束的函数
function infiniteLoop(): never {
    while (true) {
        // 死循环
    }
}

// 类型守卫的 never 分支
function assertNever(x: never): never {
    throw new Error("Unexpected object: " + x);
}

// 在类型收窄中的应用
type Shape = "circle" | "square" | "triangle";

function getArea(shape: Shape): number {
    switch (shape) {
        case "circle":
            return Math.PI * 1 * 1;
        case "square":
            return 1 * 1;
        case "triangle":
            return 0.5 * 1 * 1;
        default:
            return assertNever(shape); // 如果有未处理的情况，这里会报错
    }
}

// never 是所有类型的子类型
let neverValue: never;
let stringValue: string = neverValue; // 正确，never 可以赋值给任何类型
```

## 数组类型（Array Types）

### 基本数组声明
```typescript
// 方式一：类型[]
let list1: number[] = [1, 2, 3];
let list2: string[] = ["a", "b", "c"];
let list3: boolean[] = [true, false, true];

// 方式二：Array<类型>
let list4: Array<number> = [1, 2, 3];
let list5: Array<string> = ["a", "b", "c"];

// 从数组字面量推断
let inferredList = [1, 2, 3]; // number[]
let mixedList = [1, "hello", true]; // (string | number | boolean)[]
```

### 数组操作
```typescript
let numbers: number[] = [1, 2, 3, 4, 5];

// 访问元素
let first = numbers[0]; // number
let last = numbers[numbers.length - 1]; // number

// 修改数组
numbers[0] = 10;
numbers.push(6); // 添加到末尾
numbers.unshift(0); // 添加到开头
let removed = numbers.pop(); // 移除最后一个元素

// 数组方法
let doubled = numbers.map(x => x * 2); // number[]
let evens = numbers.filter(x => x % 2 === 0); // number[]
let sum = numbers.reduce((acc, x) => acc + x, 0); // number

// 数组解构
let [firstElement, secondElement] = numbers;
let [head, ...tail] = numbers; // head: number, tail: number[]
```

### 多维数组
```typescript
// 二维数组
let matrix: number[][] = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
];

let firstRow = matrix[0]; // number[]
let firstElement = matrix[0][0]; // number

// 三维数组
let cube: string[][][] = [[["a"]]];
```

### 只读数组
```typescript
// 只读数组类型
let readonlyArray: readonly number[] = [1, 2, 3];
// readonlyArray[0] = 10; // 错误！只读数组不能修改

// ReadonlyArray 类型
let readonlyNumbers: ReadonlyArray<number> = [1, 2, 3];
// readonlyNumbers.push(4); // 错误！

// 数组转只读数组
let mutableArray: number[] = [1, 2, 3];
let readOnlyView: readonly number[] = mutableArray;
// readOnlyView[0] = 10; // 错误！
mutableArray[0] = 10; // 正确
```

## 元组类型（Tuple Types）

### 基本元组
```typescript
// 基本元组声明
let tuple: [string, number] = ["hello", 10];
let person: [string, number, boolean] = ["John", 30, true];

// 访问元组元素
let name = tuple[0]; // string
let age = tuple[1]; // number

// 元组长度是固定的
// tuple[2] = "extra"; // 错误！索引超出范围

// 元组解构
let [str, num] = tuple;
let [firstName, personAge, isMarried] = person;
```

### 可选元素元组
```typescript
// 可选元素（TypeScript 3.0+）
let optionalTuple: [string, number?] = ["hello"];
optionalTuple = ["hello", 42]; // 也可以有两个元素

let [str1, num1] = optionalTuple; // num1: number | undefined
```

### 剩余元素元组
```typescript
// 剩余元素（TypeScript 3.0+）
let restTuple: [number, ...string[]] = [1];
restTuple = [1, "a"];
restTuple = [1, "a", "b", "c"];

// 混合使用
let mixedTuple: [string, ...number[], boolean] = ["start", true];
mixedTuple = ["start", 1, 2, 3, true];
```

### 元组标签
```typescript
// 带标签的元组（TypeScript 4.0+）
let labeledTuple: [name: string, age: number] = ["John", 30];

// 访问带标签的元素
let personName = labeledTuple[0]; // string
let personAge = labeledTuple[1]; // number
```

### 元组方法
```typescript
let tupleData: [string, number] = ["hello", 42];

// concat 方法返回数组
let newArray = tupleData.concat(["world", 100]); // (string | number)[]

// slice 方法
let sliced = tupleData.slice(0, 1); // [string]

// 注意：push/pop 等修改方法会改变类型
tupleData.push("extra"); // 现在 tupleData 变成了 (string | number)[]
```

## 枚举类型（Enum Types）

### 数字枚举
```typescript
// 基本数字枚举
enum Direction {
    Up,    // 0
    Down,  // 1
    Left,  // 2
    Right  // 3
}

let dir: Direction = Direction.Up;
console.log(dir); // 0
console.log(Direction[0]); // "Up"

// 手动赋值
enum StatusCode {
    OK = 200,
    NotFound = 404,
    ServerError = 500
}

// 部分初始化
enum MixedEnum {
    First,      // 0
    Second,     // 1
    Third = 10, // 10
    Fourth      // 11
}
```

### 字符串枚举
```typescript
// 字符串枚举
enum DirectionStr {
    Up = "UP",
    Down = "DOWN",
    Left = "LEFT",
    Right = "RIGHT"
}

let strDir: DirectionStr = DirectionStr.Up;
console.log(strDir); // "UP"

// 字符串枚举的优势
// 1. 运行时有意义的值
// 2. 更好的调试体验
// 3. 序列化友好
```

### 异构枚举
```typescript
// 混合数字和字符串
enum BooleanLikeHeterogeneousEnum {
    No = 0,
    Yes = "YES"
}

// 注意：不推荐使用异构枚举
// 因为它们容易引起混淆
```

### 常量枚举
```typescript
// 常量枚举（编译时求值）
const enum DirectionConst {
    Up,
    Down,
    Left,
    Right
}

let directions = [
    DirectionConst.Up,
    DirectionConst.Down,
    DirectionConst.Left,
    DirectionConst.Right
];

// 编译后会被完全内联，不生成运行时代码
```

### 计算枚举
```typescript
// 使用表达式初始化
enum FileAccess {
    None = 0,
    Read = 1 << 1,    // 2
    Write = 1 << 2,   // 4
    ReadWrite = Read | Write, // 6
}

// 使用函数计算
function getEnumValue(): number {
    return Math.floor(Math.random() * 100);
}

enum ComputedEnum {
    First = 1,
    Second = getEnumValue(), // 运行时计算
    Third = 2
}
```

### 枚举成员类型
```typescript
// 字面量枚举成员
enum ShapeKind {
    Circle,    // 字面量枚举成员
    Square = 1, // 字面量枚举成员
    Rectangle = ShapeKind.Circle + 1 // 非字面量枚举成员
}

// 联合枚举
enum E { A, B }
let e: E = E.A;

// 反向映射
enum Enum {
    A
}
let a = Enum.A; // 0
let nameOfA = Enum[a]; // "A"
```

## 类型推断（Type Inference）

### 基本类型推断
```typescript
// 从初始化值推断
let num = 42;        // number
let str = "hello";   // string
let bool = true;     // boolean
let arr = [1, 2, 3]; // number[]

// 从函数返回值推断
function getGreeting() {
    return "Hello, World!";
} // 推断为 () => string

// 从函数参数推断
function logMessage(message = "default") {
    console.log(message);
} // message 推断为 string
```

### 上下文类型推断
```typescript
// 事件处理器
window.onmousedown = function(mouseEvent) {
    // mouseEvent 被推断为 MouseEvent
    console.log(mouseEvent.button);
};

// 数组方法
let numbers = [1, 2, 3];
let doubled = numbers.map(x => x * 2); // x 被推断为 number

// 对象字面量
let person = {
    name: "John",
    age: 30
}; // 推断为 { name: string; age: number; }
```

### 最佳通用类型推断
```typescript
// 从多个候选类型中选择最佳通用类型
let arr1 = [1, 2, null]; // (number | null)[]
let arr2 = [1, "hello", true]; // (string | number | boolean)[]

// 类继承关系
class Animal {}
class Dog extends Animal {}
class Cat extends Animal {}

let animals = [new Dog(), new Cat()]; // Animal[]
```

### 类型断言与类型推断
```typescript
// 类型断言会覆盖推断
let someValue: any = "this is a string";
let strLength: number = (someValue as string).length;

// 双重推断
function createSquare(config: { color?: string; width?: number; }) {
    // ...
}

let squareOptions = { colour: "red", width: 100 }; // 注意拼写错误
// createSquare(squareOptions); // 错误！colour 不匹配

// 解决方案：类型断言
createSquare(squareOptions as { color: string; width: number; });

// 或者添加索引签名
interface SquareConfig {
    color?: string;
    width?: number;
    [propName: string]: any; // 索引签名
}
```

### 控制流类型推断
```typescript
// 条件分支中的类型收窄
function padLeft(value: string, padding: string | number) {
    if (typeof padding === "number") {
        // 在这个分支中，padding 被推断为 number
        return Array(padding + 1).join(" ") + value;
    }
    // 在这个分支中，padding 被推断为 string
    return padding + value;
}

// instanceof 类型保护
class Bird {
    fly() {}
    layEggs() {}
}

class Fish {
    swim() {}
    layEggs() {}
}

function move(animal: Bird | Fish) {
    if (animal instanceof Bird) {
        // animal 被推断为 Bird
        animal.fly();
    } else {
        // animal 被推断为 Fish
        animal.swim();
    }
}
```

### 泛型类型推断
```typescript
// 从函数参数推断泛型类型
function identity<T>(arg: T): T {
    return arg;
}

let output = identity("myString"); // T 被推断为 string

// 从多个参数推断
function map<T, U>(array: T[], func: (x: T) => U): U[] {
    return array.map(func);
}

let lengths = map(["hello", "world"], x => x.length); // T: string, U: number

// 约束类型推断
function longest<T extends { length: number }>(a: T, b: T) {
    if (a.length >= b.length) {
        return a;
    } else {
        return b;
    }
}

let result = longest("alice", "bob"); // T 推断为 string
```


# 3. 函数类型

## 函数声明与表达式

### 函数声明（Function Declarations）
```typescript
// 基本函数声明
function add(x: number, y: number): number {
    return x + y;
}

// 函数声明提升
console.log(multiply(2, 3)); // 正常工作，因为函数声明会被提升

function multiply(x: number, y: number): number {
    return x * y;
}

// 带类型注解的函数声明
function greet(name: string): string {
    return `Hello, ${name}!`;
}

// 无返回值的函数声明
function logMessage(message: string): void {
    console.log(message);
}
```

### 函数表达式（Function Expressions）
```typescript
// 基本函数表达式
let myAdd = function(x: number, y: number): number {
    return x + y;
};

// 带类型注解的函数表达式
let myAdd2: (x: number, y: number) => number = 
    function(x: number, y: number): number {
        return x + y;
    };

// 简化写法（类型推断）
let myAdd3: (baseValue: number, increment: number) => number = 
    function(x, y) {  // TypeScript 可以推断参数类型
        return x + y;
    };

// 匿名函数表达式
const calculate = function(operation: string, a: number, b: number): number {
    switch(operation) {
        case "add": return a + b;
        case "subtract": return a - b;
        default: return 0;
    }
};
```

### 函数类型注解
```typescript
// 完整的函数类型
let myFunc: (a: number, b: number) => number;

// 函数类型别名
type MathOperation = (x: number, y: number) => number;
let addOperation: MathOperation = (a, b) => a + b;

// 接口定义函数类型
interface StringFormatter {
    (input: string): string;
}

let uppercase: StringFormatter = (str) => str.toUpperCase();
```

## 参数类型注解

### 基本参数类型
```typescript
// 单一类型参数
function sayHello(name: string): void {
    console.log(`Hello, ${name}`);
}

// 多参数类型
function createUser(name: string, age: number, isActive: boolean): void {
    console.log(`User: ${name}, Age: ${age}, Active: ${isActive}`);
}

// 联合类型参数
function formatValue(value: string | number): string {
    return value.toString();
}

// 对象参数
function printUser(user: { name: string; age: number }): void {
    console.log(`Name: ${user.name}, Age: ${user.age}`);
}

// 数组参数
function sumArray(numbers: number[]): number {
    return numbers.reduce((sum, num) => sum + num, 0);
}
```

### 复杂参数类型
```typescript
// 接口参数
interface Product {
    id: number;
    name: string;
    price: number;
}

function displayProduct(product: Product): string {
    return `${product.name}: $${product.price}`;
}

// 泛型参数
function identity<T>(arg: T): T {
    return arg;
}

// 可调用接口参数
interface Processor {
    (data: string): string;
}

function processData(input: string, processor: Processor): string {
    return processor(input);
}
```

## 返回值类型

### 基本返回类型
```typescript
// 原始类型返回
function getPi(): number {
    return 3.14159;
}

function getGreeting(): string {
    return "Hello, World!";
}

function isEven(num: number): boolean {
    return num % 2 === 0;
}

// 对象返回类型
function createUserObject(name: string, age: number): { name: string; age: number } {
    return { name, age };
}

// 数组返回类型
function getNumbers(): number[] {
    return [1, 2, 3, 4, 5];
}

// Promise 返回类型
async function fetchData(): Promise<string> {
    return "data";
}
```

### 复杂返回类型
```typescript
// 联合返回类型
function getValue(key: string): string | number | null {
    // 根据 key 返回不同类型的值
    if (key === "name") return "John";
    if (key === "age") return 30;
    return null;
}

// 泛型返回类型
function createArray<T>(item: T, count: number): T[] {
    return Array(count).fill(item);
}

// 条件返回类型
function processInput<T extends string | number>(
    input: T
): T extends string ? string : number {
    if (typeof input === "string") {
        return input.toUpperCase() as any;
    } else {
        return (input * 2) as any;
    }
}
```

### void 和 never 返回类型
```typescript
// void 返回类型
function logMessage(message: string): void {
    console.log(message);
    // 不需要 return 语句
}

// never 返回类型
function throwError(message: string): never {
    throw new Error(message);
}

function infiniteLoop(): never {
    while (true) {
        // 永远不会返回
    }
}
```

## 可选参数与默认参数

### 可选参数
```typescript
// 可选参数（使用 ?）
function buildName(firstName: string, lastName?: string): string {
    if (lastName) {
        return firstName + " " + lastName;
    } else {
        return firstName;
    }
}

// 使用可选参数
let result1 = buildName("Bob");        // 正确
let result2 = buildName("Bob", "Adams"); // 正确
// let result3 = buildName("Bob", "Adams", "Sr."); // 错误，参数过多

// 可选参数必须在必需参数之后
// function invalid(name?: string, age: number): void {} // 错误！
```

### 默认参数
```typescript
// 默认参数值
function buildName2(firstName: string, lastName = "Smith"): string {
    return firstName + " " + lastName;
}

// 使用默认参数
let result3 = buildName2("Bob");        // "Bob Smith"
let result4 = buildName2("Bob", "Adams"); // "Bob Adams"

// 默认参数可以是表达式
function calculateTax(amount: number, taxRate = 0.1 + 0.05): number {
    return amount * taxRate;
}

// 默认参数可以引用其他参数
function applyDiscount(price: number, discount = price * 0.1): number {
    return price - discount;
}
```

### 可选与默认参数组合
```typescript
// 复杂参数组合
function createPerson(
    firstName: string,
    lastName?: string,
    age = 18,
    isActive = true
): { name: string; age: number; isActive: boolean } {
    const name = lastName ? `${firstName} ${lastName}` : firstName;
    return { name, age, isActive };
}

// 调用示例
let person1 = createPerson("John");                    // John, 18, true
let person2 = createPerson("John", "Doe");             // John Doe, 18, true
let person3 = createPerson("John", "Doe", 25);         // John Doe, 25, true
let person4 = createPerson("John", "Doe", 25, false);  // John Doe, 25, false
```

## 剩余参数

### 基本剩余参数
```typescript
// 剩余参数（使用 ...）
function buildName3(firstName: string, ...restOfName: string[]): string {
    return firstName + " " + restOfName.join(" ");
}

// 使用剩余参数
let employeeName = buildName3("Joseph", "Samuel", "Lucas", "MacKinzie");
// 结果: "Joseph Samuel Lucas MacKinzie"

// 剩余参数类型推断
function sum(...numbers: number[]): number {
    return numbers.reduce((total, num) => total + num, 0);
}

let total = sum(1, 2, 3, 4, 5); // 15
```

### 复杂剩余参数
```typescript
// 联合类型的剩余参数
function formatItems(...items: (string | number)[]): string {
    return items.map(item => item.toString()).join(", ");
}

let formatted = formatItems("apple", 42, "banana", 100);

// 对象类型的剩余参数
interface Config {
    name: string;
    value: any;
}

function applyConfigs(...configs: Config[]): void {
    configs.forEach(config => {
        console.log(`${config.name}: ${config.value}`);
    });
}

applyConfigs(
    { name: "theme", value: "dark" },
    { name: "language", value: "en" }
);
```

### 剩余参数与泛型
```typescript
// 泛型剩余参数
function mergeArrays<T>(...arrays: T[][]): T[] {
    return ([] as T[]).concat(...arrays);
}

let merged = mergeArrays([1, 2], [3, 4], [5, 6]); // number[]

// 带约束的泛型剩余参数
function createObjects<T extends object>(...objects: T[]): T[] {
    return objects.map(obj => ({ ...obj }));
}
```

## 函数重载

### 基本函数重载
```typescript
// 函数重载声明
function pickCard(x: {suit: string; card: number; }[]): number;
function pickCard(x: number): {suit: string; card: number; };

// 函数实现
function pickCard(x): any {
    if (typeof x === "object") {
        let pickedCard = Math.floor(Math.random() * x.length);
        return pickedCard;
    } else if (typeof x === "number") {
        let pickedSuit = Math.floor(x / 13);
        return { suit: suits[pickedSuit], card: x % 13 };
    }
}

// 使用重载
let myDeck = [{ suit: "diamonds", card: 2 }, { suit: "spades", card: 10 }];
let pickedCard1 = myDeck[pickCard(myDeck)];
let pickedCard2 = pickCard(15);
```

### 复杂函数重载
```typescript
// 多个重载签名
function makeDate(timestamp: number): Date;
function makeDate(m: number, d: number, y: number): Date;
function makeDate(mOrTimestamp: number, d?: number, y?: number): Date {
    if (d !== undefined && y !== undefined) {
        return new Date(y, mOrTimestamp, d);
    } else {
        return new Date(mOrTimestamp);
    }
}

// 使用重载
const d1 = makeDate(12345678);           // 使用时间戳
const d2 = makeDate(5, 5, 2022);         // 使用月日年
// const d3 = makeDate(1, 3);            // 错误！没有匹配的重载
```

### 重载与联合类型
```typescript
// 重载 vs 联合类型
// 重载方式
function len(s: string): number;
function len(arr: any[]): number;
function len(x: any): number {
    return x.length;
}

// 联合类型方式
function len2(x: string | any[]): number {
    return x.length;
}

// 重载提供了更精确的类型信息
len("hello");     // 返回 number
len([1, 2, 3]);   // 返回 number

len2("hello");    // 返回 number
len2([1, 2, 3]);  // 返回 number
```

## 箭头函数

### 基本箭头函数
```typescript
// 基本语法
let add = (x: number, y: number): number => x + y;

// 带大括号的箭头函数
let multiply = (x: number, y: number): number => {
    return x * y;
};

// 无参数箭头函数
let getCurrentDate = (): Date => new Date();

// 单参数箭头函数（可以省略括号）
let double = (x: number): number => x * 2;
let square = x => x * x; // 类型推断
```

### 箭头函数与 this
```typescript
// 箭头函数不绑定自己的 this
class Counter {
    count: number = 0;
    
    // 普通方法
    increment() {
        this.count++;
    }
    
    // 箭头函数方法
    incrementArrow = () => {
        this.count++; // this 指向类实例
    }
    
    // 在回调中使用箭头函数
    delayedIncrement() {
        setTimeout(() => {
            this.count++; // this 正确指向类实例
        }, 1000);
    }
}
```

### 箭头函数类型注解
```typescript
// 箭头函数类型
let myFunc: (a: number, b: number) => number = (x, y) => x + y;

// 复杂箭头函数类型
type EventHandler<T> = (event: T) => void;

let clickHandler: EventHandler<MouseEvent> = (event) => {
    console.log("Clicked at", event.clientX, event.clientY);
};

// 泛型箭头函数
let identity = <T>(arg: T): T => arg;

// 注意：在 .tsx 文件中需要不同的语法
// let identity = <T,>(arg: T): T => arg; // 需要逗号来区分 JSX 标签
```

### 箭头函数与高阶函数
```typescript
// 数组方法中的箭头函数
let numbers = [1, 2, 3, 4, 5];
let doubled = numbers.map(x => x * 2); // number[]
let evens = numbers.filter(x => x % 2 === 0); // number[]

// 链式调用
let result = numbers
    .filter(x => x > 2)
    .map(x => x * 2)
    .reduce((acc, x) => acc + x, 0);

// 柯里化箭头函数
let adder = (x: number) => (y: number) => x + y;
let add5 = adder(5);
let result2 = add5(3); // 8
```

## this 类型

### 显式 this 参数
```typescript
// 显式指定 this 类型
interface UIElement {
    addClickListener(onclick: (this: void, e: Event) => void): void;
}

class Handler {
    info: string;
    
    onClickBad(this: Handler, e: Event) {
        // 这里 this 的类型是 Handler
        this.info = e.type;
    }
    
    onClickGood(this: void, e: Event) {
        // 这里不能使用 this.info
        console.log('clicked!');
    }
}

let h = new Handler();
let uiElement: UIElement = {
    addClickListener(onclick) {
        // ...
    }
};

// uiElement.addClickListener(h.onClickBad); // 错误！
uiElement.addClickListener(h.onClickGood); // 正确
```

### 类中的 this 类型
```typescript
class MyClass {
    name: string = "MyClass";
    
    // 普通方法
    getName(): string {
        return this.name;
    }
    
    // 箭头函数属性
    getNameArrow = (): string => {
        return this.name;
    }
    
    // 返回 this 类型的方法（用于链式调用）
    setName(name: string): this {
        this.name = name;
        return this;
    }
    
    doSomething(): this {
        console.log("Doing something...");
        return this;
    }
}

// 链式调用
let instance = new MyClass();
instance.setName("New Name").doSomething();
```

### this 类型推断
```typescript
// 在类方法中，this 的类型会被自动推断
class Calculator {
    private result: number = 0;
    
    add(num: number): this {
        this.result += num;
        return this;
    }
    
    multiply(num: number): this {
        this.result *= num;
        return this;
    }
    
    getResult(): number {
        return this.result;
    }
}

let calc = new Calculator();
let finalResult = calc.add(5).multiply(2).getResult(); // 10
```

### this 在回调函数中的使用
```typescript
class Container {
    private items: string[] = [];
    
    addItem(item: string): void {
        this.items.push(item);
    }
    
    // 使用箭头函数保持 this 绑定
    processItems(callback: (item: string) => void): void {
        this.items.forEach(item => {
            callback(item); // this 绑定正确
        });
    }
    
    // 或者显式绑定 this
    processItems2(callback: (this: void, item: string) => void): void {
        this.items.forEach(item => {
            callback(item);
        });
    }
}
```

### 多态 this 类型
```typescript
// 多态 this 类型用于链式调用
class BasicCalculator {
    public constructor(protected value: number = 0) {}
    
    public currentValue(): number {
        return this.value;
    }
    
    public add(operand: number): this {
        this.value += operand;
        return this;
    }
    
    public multiply(operand: number): this {
        this.value *= operand;
        return this;
    }
}

class ScientificCalculator extends BasicCalculator {
    public constructor(value = 0) {
        super(value);
    }
    
    public sin(): this {
        this.value = Math.sin(this.value);
        return this;
    }
}

// 多态 this 允许链式调用继承的方法
let calc = new ScientificCalculator(10)
    .add(5)        // 返回 ScientificCalculator
    .multiply(2)   // 返回 ScientificCalculator
    .sin()         // 返回 ScientificCalculator
    .currentValue(); // 返回 number
```
# 4. 对象类型

## 接口定义

### 基本接口定义
```typescript
// 基本接口
interface Person {
    name: string;
    age: number;
}

// 使用接口
let user: Person = {
    name: "Alice",
    age: 30
};

// 函数参数使用接口
function greet(person: Person) {
    console.log(`Hello, ${person.name}! You are ${person.age} years old.`);
}

greet(user);
```

### 接口与对象字面量
```typescript
// 对象字面量必须完全匹配接口
interface Point {
    x: number;
    y: number;
}

let point1: Point = { x: 10, y: 20 }; // 正确

// 额外属性会报错
// let point2: Point = { x: 10, y: 20, z: 30 }; // 错误！

// 变量赋值时的额外属性检查
let point3 = { x: 10, y: 20, z: 30 }; // 多余属性不会报错
let point4: Point = point3; // 正确，因为 point3 是变量

// 绕过额外属性检查的方式
// 1. 类型断言
let point5: Point = { x: 10, y: 20, z: 30 } as Point;

// 2. 索引签名
interface PointWithExtra {
    x: number;
    y: number;
    [propName: string]: any;
}

let point6: PointWithExtra = { x: 10, y: 20, z: 30 }; // 正确
```

### 接口的可选属性
```typescript
// 可选属性使用 ? 标记
interface SquareConfig {
    color?: string;
    width?: number;
}

function createSquare(config: SquareConfig): { color: string; area: number } {
    let newSquare = { color: "white", area: 100 };
    
    if (config.color) {
        newSquare.color = config.color;
    }
    
    if (config.width) {
        newSquare.area = config.width * config.width;
    }
    
    return newSquare;
}

// 使用可选属性
let mySquare = createSquare({ color: "black" });
let mySquare2 = createSquare({ width: 100 });
let mySquare3 = createSquare({ color: "red", width: 50 });
```

## 可选属性

### 基本可选属性
```typescript
// 可选属性示例
interface UserProfile {
    username: string;
    email?: string;
    age?: number;
    isActive?: boolean;
}

// 创建用户配置
let user1: UserProfile = {
    username: "john_doe"
};

let user2: UserProfile = {
    username: "jane_smith",
    email: "jane@example.com",
    age: 25
};

// 访问可选属性
function displayUser(user: UserProfile) {
    console.log(`Username: ${user.username}`);
    
    if (user.email) {
        console.log(`Email: ${user.email}`);
    }
    
    if (user.age !== undefined) {
        console.log(`Age: ${user.age}`);
    }
    
    // 可选属性的默认值处理
    const isActive = user.isActive ?? true;
    console.log(`Active: ${isActive}`);
}
```

### 可选属性与类型守卫
```typescript
// 类型守卫检查可选属性
interface ApiResponse {
    success: boolean;
    data?: any;
    error?: string;
}

function handleResponse(response: ApiResponse) {
    if (response.success) {
        // data 可能存在
        if (response.data) {
            console.log("Data:", response.data);
        }
    } else {
        // error 可能存在
        if (response.error) {
            console.error("Error:", response.error);
        }
    }
}

// 使用 in 操作符检查可选属性
function processResponse(response: ApiResponse) {
    if ("data" in response) {
        console.log("Has data:", response.data);
    }
    
    if ("error" in response) {
        console.log("Has error:", response.error);
    }
}
```

## 只读属性

### 基本只读属性
```typescript
// 使用 readonly 关键字
interface Point {
    readonly x: number;
    readonly y: number;
}

let point: Point = { x: 10, y: 20 };
// point.x = 5; // 错误！不能修改只读属性

// 数组的只读版本
interface ReadOnlyArray {
    readonly items: readonly string[];
}

let readOnlyData: ReadOnlyArray = {
    items: ["a", "b", "c"] as const
};

// readOnlyData.items[0] = "x"; // 错误！
// readOnlyData.items.push("d"); // 错误！
```

### Readonly<T> 工具类型
```typescript
// 使用 Readonly 工具类型
interface Todo {
    title: string;
    description: string;
}

let todo1: Readonly<Todo> = {
    title: "Learn TypeScript",
    description: "Study interfaces and types"
};

// todo1.title = "Updated"; // 错误！

// 创建只读数组
let readOnlyNumbers: ReadonlyArray<number> = [1, 2, 3, 4];
// readOnlyNumbers[0] = 12; // 错误！
// readOnlyNumbers.push(5); // 错误！
// readOnlyNumbers.length = 100; // 错误！

// 只读元组
let readOnlyTuple: readonly [string, number] = ["hello", 42];
// readOnlyTuple[0] = "world"; // 错误！
```

### 函数参数的只读属性
```typescript
// 函数参数使用只读属性
function printPoint(point: Readonly<Point>) {
    console.log(`Point: (${point.x}, ${point.y})`);
    // point.x = 10; // 错误！参数是只读的
}

// 只读数组参数
function sumArray(numbers: readonly number[]): number {
    return numbers.reduce((sum, num) => sum + num, 0);
    // numbers.push(1); // 错误！
}

// 只读对象参数
interface Config {
    readonly apiUrl: string;
    readonly timeout: number;
}

function makeRequest(config: Readonly<Config>) {
    fetch(config.apiUrl, { timeout: config.timeout });
    // config.apiUrl = "new-url"; // 错误！
}
```

## 索引签名

### 基本索引签名
```typescript
// 数字索引签名
interface StringArray {
    [index: number]: string;
}

let myArray: StringArray = ["Bob", "Fred"];
let myStr: string = myArray[0];

// 字符串索引签名
interface StringDictionary {
    [key: string]: string;
}

let dictionary: StringDictionary = {
    "name": "John",
    "age": "30"  // 注意：所有值都必须是 string
};

let name = dictionary["name"];
dictionary["city"] = "New York";

// 混合索引签名
interface HybridDictionary {
    [index: number]: string;  // 数字索引返回 string
    [key: string]: string;    // 字符串索引返回 string
    length: number;           // 可以有其他属性
}

let hybrid: HybridDictionary = {
    0: "first",
    1: "second",
    "name": "John",
    length: 2
};
```

### 索引签名与已知属性
```typescript
// 索引签名与具体属性的兼容性
interface NumberDictionary {
    [index: string]: number;
    length: number;      // 正确，number 可以赋值给 number
    // name: string;     // 错误，string 不能赋值给 number
}

// 使用联合类型解决兼容性问题
interface ConflictingDictionary {
    [index: string]: string | number;
    length: number;    // 正确
    name: string;      // 正确
}

// 只读索引签名
interface ReadOnlyStringArray {
    readonly [index: number]: string;
}

let readOnlyArray: ReadOnlyStringArray = ["a", "b", "c"];
let item = readOnlyArray[0]; // 正确
// readOnlyArray[0] = "x"; // 错误！
```

### 索引签名的实际应用
```typescript
// 动态属性对象
interface FlexibleObject {
    [key: string]: any;
    id: string;  // 必需的已知属性
}

let obj: FlexibleObject = {
    id: "123",
    name: "John",
    age: 30,
    isActive: true
};

// 配置对象
interface ConfigOptions {
    [key: string]: string | number | boolean;
}

function configure(options: ConfigOptions) {
    for (let key in options) {
        console.log(`${key}: ${options[key]}`);
    }
}

configure({
    theme: "dark",
    fontSize: 14,
    enableAnimations: true
});
```

## 扩展接口

### 基本接口扩展
```typescript
// 基础接口
interface Shape {
    color: string;
}

// 扩展接口
interface Square extends Shape {
    sideLength: number;
}

let square: Square = {
    color: "blue",
    sideLength: 10
};

// 多重扩展
interface PenStroke {
    penWidth: number;
}

interface ColoredSquare extends Shape, PenStroke {
    sideLength: number;
}

let coloredSquare: ColoredSquare = {
    color: "red",
    penWidth: 2,
    sideLength: 15
};
```

### 扩展与重写属性
```typescript
// 扩展时重写属性类型（必须更具体）
interface BasicUser {
    name: string;
    email: string | null;
}

interface PremiumUser extends BasicUser {
    name: "Premium User";  // 更具体的字符串字面量类型
    email: string;         // 从 string | null 收窄为 string
    subscriptionLevel: "basic" | "premium" | "enterprise";
}

let premiumUser: PremiumUser = {
    name: "Premium User",
    email: "user@example.com",
    subscriptionLevel: "premium"
};
```

### 扩展索引签名
```typescript
// 扩展带有索引签名的接口
interface BaseDictionary {
    [key: string]: any;
    id: string;
}

interface TypedDictionary extends BaseDictionary {
    [key: string]: string | number;  // 更严格的索引签名
    name: string;
    age: number;
}

let dict: TypedDictionary = {
    id: "123",
    name: "John",
    age: 30,
    city: "New York"  // string 类型
    // score: true;   // 错误！boolean 不在索引签名类型中
};
```

## 混合类型

### 函数与对象的混合
```typescript
// 混合类型：既是函数又有属性
interface Counter {
    (start: number): string;
    interval: number;
    reset(): void;
}

function getCounter(): Counter {
    let counter = <Counter>function (start: number) {
        return `Count: ${start}`;
    };
    
    counter.interval = 123;
    counter.reset = function () {
        console.log("Counter reset");
    };
    
    return counter;
}

let c = getCounter();
c(10);
c.reset();
c.interval = 5.0;
```

### 复杂混合类型
```typescript
// 更复杂的混合类型
interface MathLibrary {
    // 函数调用签名
    (x: number, y: number): number;
    
    // 属性
    version: string;
    constants: {
        PI: number;
        E: number;
    };
    
    // 方法
    add(x: number, y: number): number;
    multiply(x: number, y: number): number;
    
    // 索引签名
    [key: string]: any;
}

// 实现混合类型
let mathLib: MathLibrary = <MathLibrary>function(x: number, y: number): number {
    return x + y;
};

mathLib.version = "1.0.0";
mathLib.constants = {
    PI: 3.14159,
    E: 2.71828
};

mathLib.add = (x, y) => x + y;
mathLib.multiply = (x, y) => x * y;
```

## 接口继承

### 基本继承
```typescript
// 父接口
interface Animal {
    name: string;
    age: number;
    move(): void;
}

// 子接口
interface Dog extends Animal {
    breed: string;
    bark(): void;
}

// 实现子接口
class GoldenRetriever implements Dog {
    name: string = "Buddy";
    age: number = 3;
    breed: string = "Golden Retriever";
    
    move(): void {
        console.log("Dog is running");
    }
    
    bark(): void {
        console.log("Woof!");
    }
}
```

### 多重继承
```typescript
// 多个父接口
interface Flyable {
    fly(): void;
    maxAltitude: number;
}

interface Swimmable {
    swim(): void;
    maxDepth: number;
}

// 继承多个接口
interface Duck extends Animal, Flyable, Swimmable {
    species: string;
}

// 实现多重继承的接口
class MallardDuck implements Duck {
    name: string = "Mallard";
    age: number = 2;
    species: string = "Anas platyrhynchos";
    maxAltitude: number = 1000;
    maxDepth: number = 5;
    
    move(): void {
        console.log("Duck is moving");
    }
    
    fly(): void {
        console.log("Duck is flying");
    }
    
    swim(): void {
        console.log("Duck is swimming");
    }
}
```

### 继承层次结构
```typescript
// 建立继承层次
interface Vehicle {
    brand: string;
    start(): void;
}

interface MotorVehicle extends Vehicle {
    engineType: string;
    fuelCapacity: number;
}

interface Car extends MotorVehicle {
    doors: number;
    trunkCapacity: number;
    honk(): void;
}

interface ElectricCar extends Car {
    batteryCapacity: number;
    charge(): void;
}

// 实现最底层接口
class TeslaModel3 implements ElectricCar {
    brand: string = "Tesla";
    engineType: string = "Electric";
    fuelCapacity: number = 0;
    doors: number = 4;
    trunkCapacity: number = 400;
    batteryCapacity: number = 75;
    
    start(): void {
        console.log("Tesla starting silently");
    }
    
    honk(): void {
        console.log("Beep beep!");
    }
    
    charge(): void {
        console.log("Charging battery...");
    }
}
```

## 类类型接口

### 基本类类型接口
```typescript
// 定义构造函数类型接口
interface ClockConstructor {
    new (hour: number, minute: number): ClockInterface;
}

// 定义实例类型接口
interface ClockInterface {
    tick(): void;
}

// 实现类
function createClock(
    ctor: ClockConstructor,
    hour: number,
    minute: number
): ClockInterface {
    return new ctor(hour, minute);
}

class DigitalClock implements ClockInterface {
    constructor(h: number, m: number) {}
    tick() {
        console.log("beep beep");
    }
}

class AnalogClock implements ClockInterface {
    constructor(h: number, m: number) {}
    tick() {
        console.log("tick tock");
    }
}

let digital = createClock(DigitalClock, 12, 17);
let analog = createClock(AnalogClock, 7, 32);
```

### 静态部分与实例部分
```typescript
// 分离静态部分和实例部分
interface ShapeConstructor {
    new (): Shape;
    displayName: string;
    defaultColor: string;
}

interface Shape {
    color: string;
    area(): number;
}

// 实现类
class Circle implements Shape {
    static displayName = "Circle";
    static defaultColor = "red";
    
    color: string;
    radius: number;
    
    constructor(radius: number = 1) {
        this.radius = radius;
        this.color = Circle.defaultColor;
    }
    
    area(): number {
        return Math.PI * this.radius * this.radius;
    }
}

// 创建形状工厂
function createShape<T extends Shape>(
    ctor: new () => T
): T {
    return new ctor();
}

let circle = createShape(Circle);
console.log(circle.area());
```

### 类的公共接口
```typescript
// 定义类的公共接口
interface Logger {
    log(message: string): void;
    warn(message: string): void;
    error(message: string): void;
}

// 实现类
class ConsoleLogger implements Logger {
    log(message: string): void {
        console.log(`LOG: ${message}`);
    }
    
    warn(message: string): void {
        console.warn(`WARN: ${message}`);
    }
    
    error(message: string): void {
        console.error(`ERROR: ${message}`);
    }
}

// 使用接口作为类型
let logger: Logger = new ConsoleLogger();
logger.log("Application started");
```

## 函数类型接口

### 基本函数类型接口
```typescript
// 定义函数类型接口
interface SearchFunc {
    (source: string, subString: string): boolean;
}

// 实现函数类型接口
let mySearch: SearchFunc = function(source: string, subString: string) {
    let result = source.search(subString);
    return result > -1;
};

// 简化实现（类型推断）
let mySearch2: SearchFunc = (src, sub) => {
    return src.includes(sub);
};

// 使用函数类型接口
function findString(searchFunc: SearchFunc, text: string, query: string): boolean {
    return searchFunc(text, query);
}

let found = findString(mySearch, "Hello world", "world");
```

### 复杂函数类型接口
```typescript
// 带有属性的函数类型接口
interface EventHandler {
    (event: Event): void;
    eventType: string;
    priority: number;
}

// 实现复杂函数类型接口
let clickHandler: EventHandler = <EventHandler>function(event: Event) {
    console.log("Click event handled");
};

clickHandler.eventType = "click";
clickHandler.priority = 1;

// 泛型函数类型接口
interface MapFunction<T, U> {
    (item: T, index: number, array: T[]): U;
}

// 使用泛型函数类型接口
let mapStringToNumber: MapFunction<string, number> = (str, index) => {
    return str.length + index;
};

let lengths = ["hello", "world", "typescript"].map(mapStringToNumber);
```

### 可调用接口
```typescript
// 可调用接口定义
interface StringProcessor {
    (input: string): string;
    version: string;
    process(input: string): string;
}

// 实现可调用接口
let processor: StringProcessor = <StringProcessor>function(input: string): string {
    return input.toUpperCase();
};

processor.version = "1.0.0";
processor.process = (input: string) => input.toLowerCase();

// 使用可调用接口
console.log(processor("Hello")); // "HELLO"
console.log(processor.process("Hello")); // "hello"
console.log(processor.version); // "1.0.0"
```

### 函数重载接口
```typescript
// 函数重载接口
interface OverloadedFunction {
    (x: number): number;
    (x: string): string;
    (x: boolean): boolean;
}

// 实现重载函数
let overloaded: OverloadedFunction = <OverloadedFunction>function(x: any): any {
    if (typeof x === "number") {
        return x * 2;
    } else if (typeof x === "string") {
        return x.toUpperCase();
    } else {
        return !x;
    }
};

// 使用重载函数
let numResult = overloaded(42);        // number
let strResult = overloaded("hello");   // string
let boolResult = overloaded(true);     // boolean
```

# 5. 类型别名

## 基本类型别名

### 简单类型别名
```typescript
// 基本类型别名
type Name = string;
type Age = number;
type IsActive = boolean;

// 使用类型别名
let userName: Name = "Alice";
let userAge: Age = 30;
let userActive: IsActive = true;

// 复杂类型的简化
type UserID = string;
type UserEmail = string;
type UserPassword = string;

// 函数类型别名
type GreetingFunction = (name: string) => string;

let greet: GreetingFunction = (name) => `Hello, ${name}!`;

// 对象类型别名
type User = {
    id: UserID;
    name: Name;
    email: UserEmail;
    age: Age;
    isActive: IsActive;
};

let user: User = {
    id: "123",
    name: "Alice",
    email: "alice@example.com",
    age: 30,
    isActive: true
};
```

### 泛型类型别名
```typescript
// 泛型类型别名
type Container<T> = { value: T };

let stringContainer: Container<string> = { value: "hello" };
let numberContainer: Container<number> = { value: 42 };

// 多泛型参数
type Pair<T, U> = {
    first: T;
    second: U;
};

let nameAgePair: Pair<string, number> = {
    first: "Alice",
    second: 30
};

// 带约束的泛型类型别名
type StringContainer<T extends string> = {
    value: T;
    length: number;
};

let greetingContainer: StringContainer<"Hello"> = {
    value: "Hello",
    length: 5
};
```

### 递归类型别名
```typescript
// 递归类型别名（需要交叉类型）
type JsonValue = 
    | string
    | number
    | boolean
    | null
    | JsonObject
    | JsonArray;

type JsonObject = { [key: string]: JsonValue };
interface JsonArray extends Array<JsonValue> {}

// 使用递归类型
let jsonData: JsonValue = {
    name: "Alice",
    age: 30,
    hobbies: ["reading", "swimming"],
    address: {
        street: "123 Main St",
        city: "New York"
    }
};
```

## 联合类型

### 基本联合类型
```typescript
// 简单联合类型
type StringOrNumber = string | number;
type BooleanOrNull = boolean | null;
type Primitive = string | number | boolean | null | undefined;

// 使用联合类型
let value: StringOrNumber = "hello";
value = 42; // 也可以是数字

// 联合类型的实际应用
type HttpStatus = 200 | 404 | 500;
type Direction = "up" | "down" | "left" | "right";
type Size = "small" | "medium" | "large";

function handleStatus(status: HttpStatus) {
    switch (status) {
        case 200:
            console.log("OK");
            break;
        case 404:
            console.log("Not Found");
            break;
        case 500:
            console.log("Internal Server Error");
            break;
    }
}

function move(direction: Direction) {
    console.log(`Moving ${direction}`);
}

let currentStatus: HttpStatus = 200;
let currentDirection: Direction = "up";
```

### 联合类型与类型守卫
```typescript
// 联合类型中的类型收窄
type Padding = number | string;

function padLeft(value: string, padding: Padding) {
    if (typeof padding === "number") {
        // padding 在这里是 number 类型
        return " ".repeat(padding) + value;
    }
    
    // padding 在这里是 string 类型
    return padding + value;
}

// 对象联合类型
interface Bird {
    type: "bird";
    flyingSpeed: number;
}

interface Horse {
    type: "horse";
    runningSpeed: number;
}

type Animal = Bird | Horse;

function moveAnimal(animal: Animal) {
    switch (animal.type) {
        case "bird":
            console.log(`Flying at ${animal.flyingSpeed} km/h`);
            break;
        case "horse":
            console.log(`Running at ${animal.runningSpeed} km/h`);
            break;
    }
}

let bird: Animal = {
    type: "bird",
    flyingSpeed: 100
};

moveAnimal(bird);
```

### 联合类型与属性访问
```typescript
// 联合类型中的公共属性
interface Admin {
    name: string;
    privileges: string[];
}

interface Employee {
    name: string;
    startDate: Date;
}

type UnknownEmployee = Employee | Admin;

function printEmployeeInformation(emp: UnknownEmployee) {
    console.log("Name: " + emp.name); // 公共属性可以直接访问
    
    // 需要类型检查才能访问特定属性
    if ("privileges" in emp) {
        console.log("Privileges: " + emp.privileges);
    }
    
    if ("startDate" in emp) {
        console.log("Start Date: " + emp.startDate);
    }
}

// 使用 instanceof 检查
class Car {
    drive() {
        console.log("Driving...");
    }
}

class Truck {
    drive() {
        console.log("Driving a truck...");
    }
    
    loadCargo(amount: number) {
        console.log(`Loading cargo: ${amount}`);
    }
}

type Vehicle = Car | Truck;

function useVehicle(vehicle: Vehicle) {
    vehicle.drive();
    
    if (vehicle instanceof Truck) {
        vehicle.loadCargo(1000);
    }
}
```

## 交叉类型

### 基本交叉类型
```typescript
// 简单交叉类型
interface Identifiable {
    id: string;
}

interface Timestamped {
    createdAt: Date;
    updatedAt: Date;
}

type Model = Identifiable & Timestamped;

let model: Model = {
    id: "123",
    createdAt: new Date(),
    updatedAt: new Date()
};

// 交叉类型与对象合并
interface Person {
    name: string;
    age: number;
}

interface Employee {
    employeeId: string;
    department: string;
}

interface Manager {
    teamSize: number;
    reports: string[];
}

type ManagerEmployee = Person & Employee & Manager;

let manager: ManagerEmployee = {
    name: "Alice",
    age: 35,
    employeeId: "E123",
    department: "Engineering",
    teamSize: 10,
    reports: ["Bob", "Charlie"]
};
```

### 交叉类型与冲突处理
```typescript
// 交叉类型中的类型冲突
interface A {
    prop: string;
}

interface B {
    prop: number;
}

// type C = A & B; // prop 的类型变为 never
// let c: C = { prop: "hello" }; // 错误！
// let c2: C = { prop: 42 }; // 错误！

// 解决冲突的方法
interface A2 {
    name: string;
    age: number;
}

interface B2 {
    name: "specific"; // 字面量类型
    email: string;
}

type C2 = A2 & B2;

let c2: C2 = {
    name: "specific", // 必须是 "specific"
    age: 30,
    email: "test@example.com"
};
```

### 复杂交叉类型
```typescript
// 嵌套交叉类型
interface BaseConfig {
    debug: boolean;
}

interface DatabaseConfig {
    host: string;
    port: number;
}

interface ApiConfig {
    baseUrl: string;
    timeout: number;
}

type AppConfig = BaseConfig & {
    database: DatabaseConfig;
    api: ApiConfig;
};

let config: AppConfig = {
    debug: true,
    database: {
        host: "localhost",
        port: 5432
    },
    api: {
        baseUrl: "https://api.example.com",
        timeout: 5000
    }
};

// 交叉类型与泛型
type Merge<T, U> = T & U;

type User = {
    id: string;
    name: string;
};

type UserWithPermissions = Merge<User, {
    permissions: string[];
}>;

let userWithPerms: UserWithPermissions = {
    id: "123",
    name: "Alice",
    permissions: ["read", "write"]
};
```

## 字面量类型

### 字符串字面量类型
```typescript
// 字符串字面量类型
type RequestMethod = "GET" | "POST" | "PUT" | "DELETE";
type Theme = "light" | "dark" | "auto";
type UserRole = "admin" | "user" | "guest";

// 使用字面量类型
function makeRequest(url: string, method: RequestMethod) {
    console.log(`Making ${method} request to ${url}`);
}

makeRequest("/api/users", "GET"); // 正确
// makeRequest("/api/users", "get"); // 错误！类型不匹配

// 字面量类型与对象
interface Config {
    theme: Theme;
    language: "en" | "zh" | "es";
    notifications: boolean;
}

let appConfig: Config = {
    theme: "dark",
    language: "en",
    notifications: true
};
```

### 数字字面量类型
```typescript
// 数字字面量类型
type DiceValue = 1 | 2 | 3 | 4 | 5 | 6;
type HttpStatusCode = 200 | 201 | 400 | 404 | 500;
type Priority = 1 | 2 | 3 | 4 | 5;

function rollDice(): DiceValue {
    return (Math.floor(Math.random() * 6) + 1) as DiceValue;
}

function handleResponse(status: HttpStatusCode) {
    switch (status) {
        case 200:
            console.log("Success");
            break;
        case 404:
            console.log("Not Found");
            break;
        case 500:
            console.log("Server Error");
            break;
    }
}

// 数字字面量与计算
type PowerOfTwo = 1 | 2 | 4 | 8 | 16 | 32 | 64 | 128 | 256 | 512 | 1024;
```

### 布尔字面量类型
```typescript
// 布尔字面量类型
type Success = true;
type Failure = false;
type StrictBoolean = true | false; // 等同于 boolean

// 使用布尔字面量类型
interface ApiResponse<T> {
    success: true;
    data: T;
}

interface ApiError {
    success: false;
    error: string;
}

type ApiResponseOrError<T> = ApiResponse<T> | ApiError;

function handleApiResponse<T>(response: ApiResponseOrError<T>) {
    if (response.success) {
        // TypeScript 知道这是 ApiResponse<T>
        console.log("Data:", response.data);
    } else {
        // TypeScript 知道这是 ApiError
        console.error("Error:", response.error);
    }
}
```

### 模板字面量类型（TypeScript 4.1+）
```typescript
// 模板字面量类型
type World = "world";
type Greeting = `hello ${World}`; // "hello world"

// 与联合类型结合
type EmailLocaleIDs = "welcome_email" | "email_heading";
type FooterLocaleIDs = "footer_title" | "footer_sendoff";

type AllLocaleIDs = `${EmailLocaleIDs | FooterLocaleIDs}_id`;

// 大小写转换类型
type PropEventSource<T> = {
    on<Key extends keyof T & string>(
        eventName: `${Key}Changed`,
        callback: (newValue: T[Key]) => void
    ): void;
};

declare function makeWatchedObject<T>(obj: T): T & PropEventSource<T>;

let person = makeWatchedObject({
    firstName: "Alice",
    lastName: "Johnson",
    age: 30
});

// 触发类型检查的事件名
person.on("firstNameChanged", newName => {
    // newName 的类型是 string
    console.log(`new name is ${newName.toUpperCase()}`);
});

// person.on("firstNamechanged", () => {}); // 错误！大小写不匹配
```

## 类型别名与接口的区别

### 声明语法
```typescript
// 类型别名使用 type 关键字
type Point = {
    x: number;
    y: number;
};

// 接口使用 interface 关键字
interface PointInterface {
    x: number;
    y: number;
}

// 使用方式相同
let point1: Point = { x: 10, y: 20 };
let point2: PointInterface = { x: 10, y: 20 };
```

### 扩展能力
```typescript
// 接口可以扩展其他接口
interface Animal {
    name: string;
}

interface Dog extends Animal {
    breed: string;
}

// 类型别名可以通过交叉类型扩展
type AnimalType = {
    name: string;
};

type DogType = AnimalType & {
    breed: string;
};

// 接口可以被多次声明（声明合并）
interface Window {
    customProperty: string;
}

interface Window {
    anotherProperty: number;
}

// 现在 Window 接口有所有声明的属性
// 类型别名不能这样做
// type Window = { customProperty: string; };
// type Window = { anotherProperty: number; }; // 错误！重复声明
```

### 实现类的能力
```typescript
// 接口可以被类实现
interface Drawable {
    draw(): void;
}

class Circle implements Drawable {
    draw() {
        console.log("Drawing circle");
    }
}

// 类型别名也可以被类实现（如果它是对象类型）
type DrawableType = {
    draw(): void;
};

class Square implements DrawableType {
    draw() {
        console.log("Drawing square");
    }
}
```

### 联合类型和交叉类型
```typescript
// 类型别名更适合联合类型和交叉类型
type StringOrNumber = string | number;
type Point3D = Point & { z: number };

// 接口不能直接表示联合类型
// interface StringOrNumber = string | number; // 错误！

// 但接口可以通过继承实现类似交叉类型的效果
interface Point2D {
    x: number;
    y: number;
}

interface Point3D extends Point2D {
    z: number;
}
```

### 函数类型定义
```typescript
// 类型别名定义函数类型更简洁
type GreetFunction = (name: string) => string;

// 接口定义函数类型
interface GreetInterface {
    (name: string): string;
}

// 可调用接口
interface Callable {
    (x: number): number;
    version: string;
}

// 类型别名实现可调用接口比较复杂
type CallableType = ((x: number) => number) & {
    version: string;
};
```

### 性能考虑
```typescript
// 接口在编译器处理时通常性能更好
// 因为它们支持声明合并和增量编译

// 类型别名在复杂情况下可能会有性能影响
// 特别是递归类型和复杂联合类型

// 但在大多数情况下，性能差异可以忽略不计
```

### 使用建议
```typescript
// 何时使用接口：
// 1. 定义对象的形状
// 2. 需要扩展或继承
// 3. 需要声明合并
// 4. 定义类的公共契约

interface User {
    name: string;
    email: string;
}

interface AdminUser extends User {
    permissions: string[];
}

// 何时使用类型别名：
// 1. 联合类型
// 2. 交叉类型
// 3. 原始类型的别名
// 4. 复杂的类型操作

type Status = "pending" | "approved" | "rejected";
type ApiResponse<T> = SuccessResponse<T> | ErrorResponse;
type ID = string | number;
```

### 实际应用示例
```typescript
// 复杂业务场景：API 响应处理

// 使用接口定义数据结构
interface User {
    id: string;
    name: string;
    email: string;
}

interface Pagination {
    page: number;
    limit: number;
    total: number;
}

// 使用类型别名处理联合类型
type ApiSuccess<T> = {
    success: true;
    data: T;
    message?: string;
};

type ApiError = {
    success: false;
    error: string;
    code: number;
};

type ApiResponse<T> = ApiSuccess<T> | ApiError;

// 使用交叉类型组合接口
type PaginatedResponse<T> = ApiResponse<T[]> & {
    pagination: Pagination;
};

// 实际使用
function handleUserResponse(response: ApiResponse<User>) {
    if (response.success) {
        console.log("User:", response.data.name);
    } else {
        console.error("Error:", response.error);
    }
}

function handleUsersResponse(response: PaginatedResponse<User>) {
    if (response.success) {
        console.log("Users count:", response.data.length);
        console.log("Page:", response.pagination.page);
    }
}
```


# 6. 类和面向对象

## 类的基本语法

### 基本类定义
```typescript
// 基本类定义
class Person {
    // 属性声明
    name: string;
    age: number;
    
    // 构造函数
    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
    
    // 方法定义
    greet(): string {
        return `Hello, my name is ${this.name}`;
    }
    
    // 带参数的方法
    haveBirthday(): void {
        this.age++;
        console.log(`Happy birthday! Now I'm ${this.age} years old.`);
    }
}

// 创建类实例
let person1 = new Person("Alice", 30);
let person2 = new Person("Bob", 25);

console.log(person1.greet()); // "Hello, my name is Alice"
person1.haveBirthday(); // "Happy birthday! Now I'm 31 years old."
```

### 属性初始化
```typescript
// 属性初始化的不同方式
class Product {
    // 直接初始化
    category: string = "General";
    
    // 构造函数中初始化
    name: string;
    price: number;
    
    // 可选属性
    description?: string;
    
    // 只读属性（稍后详述）
    readonly id: string;
    
    constructor(name: string, price: number, description?: string) {
        this.name = name;
        this.price = price;
        this.description = description;
        this.id = Math.random().toString(36);
    }
    
    // getter 方法
    getDisplayPrice(): string {
        return `$${this.price.toFixed(2)}`;
    }
}

let product = new Product("Laptop", 999.99, "High-performance laptop");
console.log(product.getDisplayPrice()); // "$999.99"
```

### 字段初始化器
```typescript
// 使用字段初始化器简化构造函数
class Rectangle {
    // 直接初始化属性
    width: number = 0;
    height: number = 0;
    color: string = "white";
    
    constructor(width?: number, height?: number, color?: string) {
        if (width !== undefined) this.width = width;
        if (height !== undefined) this.height = height;
        if (color !== undefined) this.color = color;
    }
    
    getArea(): number {
        return this.width * this.height;
    }
}

// 使用参数属性简化构造函数（稍后详述）
class Circle {
    constructor(
        public radius: number,
        private color: string = "red",
        readonly id: string = Math.random().toString(36)
    ) {}
    
    getArea(): number {
        return Math.PI * this.radius * this.radius;
    }
}
```

## 构造函数

### 基本构造函数
```typescript
// 构造函数的基本用法
class Book {
    title: string;
    author: string;
    pages: number;
    published: Date;
    
    // 基本构造函数
    constructor(title: string, author: string, pages: number) {
        this.title = title;
        this.author = author;
        this.pages = pages;
        this.published = new Date();
    }
}

// 带默认参数的构造函数
class Article {
    title: string;
    author: string;
    views: number = 0; // 默认值
    published: Date;
    
    constructor(title: string, author: string, published?: Date) {
        this.title = title;
        this.author = author;
        this.published = published || new Date();
    }
}

// 重载构造函数
class User {
    name: string;
    email: string;
    role: string;
    
    // 构造函数重载
    constructor(name: string, email: string, role?: string);
    constructor(userData: { name: string; email: string; role?: string });
    
    // 实际实现
    constructor(
        nameOrData: string | { name: string; email: string; role?: string },
        email?: string,
        role: string = "user"
    ) {
        if (typeof nameOrData === "string") {
            this.name = nameOrData;
            this.email = email!;
            this.role = role;
        } else {
            this.name = nameOrData.name;
            this.email = nameOrData.email;
            this.role = nameOrData.role || "user";
        }
    }
}
```

### 参数属性
```typescript
// 参数属性（Parameter Properties）
class Student {
    // 使用参数属性简化构造函数
    constructor(
        public name: string,           // public 属性
        private age: number,           // private 属性
        protected grade: string,       // protected 属性
        readonly studentId: string     // readonly 属性
    ) {
        // 不需要手动赋值，TypeScript 会自动处理
    }
    
    getInfo(): string {
        // 可以访问 public 和 protected 属性
        return `${this.name} (${this.grade})`;
        // this.age; // 错误！private 属性不能在类外部访问
    }
}

let student = new Student("Alice", 20, "A", "S12345");
console.log(student.name); // "Alice"
console.log(student.studentId); // "S12345"
// student.age; // 错误！private 属性
```

### 构造函数链
```typescript
// 构造函数中的初始化逻辑
class DatabaseConnection {
    private connectionString: string;
    private timeout: number;
    private isConnected: boolean = false;
    
    constructor(connectionString: string, timeout: number = 5000) {
        this.connectionString = connectionString;
        this.timeout = timeout;
        this.validateConnectionString();
    }
    
    private validateConnectionString(): void {
        if (!this.connectionString.startsWith("db://")) {
            throw new Error("Invalid connection string format");
        }
    }
    
    connect(): Promise<void> {
        return new Promise((resolve) => {
            setTimeout(() => {
                this.isConnected = true;
                resolve();
            }, this.timeout);
        });
    }
}
```

## 继承与多态

### 基本继承
```typescript
// 父类（基类）
class Animal {
    name: string;
    age: number;
    
    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
    
    move(distance: number = 0): void {
        console.log(`${this.name} moved ${distance}m.`);
    }
    
    makeSound(): void {
        console.log(`${this.name} makes a sound.`);
    }
}

// 子类（派生类）
class Dog extends Animal {
    breed: string;
    
    constructor(name: string, age: number, breed: string) {
        super(name, age); // 调用父类构造函数
        this.breed = breed;
    }
    
    // 重写父类方法
    move(distance: number = 5): void {
        console.log("Dog is running...");
        super.move(distance); // 调用父类方法
    }
    
    // 新增方法
    bark(): void {
        console.log("Woof! Woof!");
    }
    
    // 重写父类方法
    makeSound(): void {
        this.bark();
    }
}

let dog = new Dog("Buddy", 3, "Golden Retriever");
dog.move(); // "Dog is running...\nBuddy moved 5m."
dog.makeSound(); // "Woof! Woof!"
```

### 多层继承
```typescript
// 多层继承
class Mammal extends Animal {
    furColor: string;
    
    constructor(name: string, age: number, furColor: string) {
        super(name, age);
        this.furColor = furColor;
    }
    
    nurse(): void {
        console.log(`${this.name} is nursing its young.`);
    }
}

class Cat extends Mammal {
    isIndoor: boolean;
    
    constructor(
        name: string, 
        age: number, 
        furColor: string, 
        isIndoor: boolean = true
    ) {
        super(name, age, furColor);
        this.isIndoor = isIndoor;
    }
    
    move(distance: number = 1): void {
        console.log("Cat is sneaking...");
        super.move(distance);
    }
    
    meow(): void {
        console.log("Meow!");
    }
    
    makeSound(): void {
        this.meow();
    }
}

let cat = new Cat("Whiskers", 2, "orange", true);
cat.move(); // "Cat is sneaking...\nWhiskers moved 1m."
cat.nurse(); // "Whiskers is nursing its young."
```

### 多态性
```typescript
// 多态性的应用
class Bird extends Animal {
    wingSpan: number;
    
    constructor(name: string, age: number, wingSpan: number) {
        super(name, age);
        this.wingSpan = wingSpan;
    }
    
    move(distance: number = 10): void {
        console.log("Bird is flying...");
        super.move(distance);
    }
    
    makeSound(): void {
        console.log("Tweet! Tweet!");
    }
}

// 多态函数 - 接受父类类型，但运行时调用子类方法
function makeAnimalMove(animal: Animal): void {
    animal.move(); // 运行时多态
    animal.makeSound(); // 运行时多态
}

let animals: Animal[] = [
    new Dog("Buddy", 3, "Golden Retriever"),
    new Cat("Whiskers", 2, "orange", true),
    new Bird("Tweety", 1, 0.5)
];

animals.forEach(animal => makeAnimalMove(animal));
// 输出不同动物的移动和声音行为
```

### 方法重写与 super 关键字
```typescript
// 方法重写和 super 的使用
class Vehicle {
    protected speed: number = 0;
    
    constructor(protected brand: string) {}
    
    start(): void {
        console.log(`${this.brand} vehicle started`);
    }
    
    accelerate(increment: number): void {
        this.speed += increment;
        console.log(`Speed: ${this.speed} km/h`);
    }
    
    getInfo(): string {
        return `${this.brand} - Speed: ${this.speed} km/h`;
    }
}

class Car extends Vehicle {
    private doors: number;
    
    constructor(brand: string, doors: number) {
        super(brand); // 必须首先调用 super()
        this.doors = doors;
    }
    
    // 重写父类方法
    start(): void {
        super.start(); // 调用父类方法
        console.log("Car engine running");
    }
    
    // 重写并扩展父类方法
    accelerate(increment: number): void {
        console.log("Car accelerating...");
        super.accelerate(increment); // 调用父类方法
        if (this.speed > 120) {
            console.log("Warning: Speed limit exceeded!");
        }
    }
    
    // 新增方法
    honk(): void {
        console.log("Beep beep!");
    }
    
    // 重写父类方法
    getInfo(): string {
        return `${super.getInfo()} - Doors: ${this.doors}`;
    }
}

let car = new Car("Toyota", 4);
car.start(); // "Toyota vehicle started\nCar engine running"
car.accelerate(50); // "Car accelerating...\nSpeed: 50 km/h"
console.log(car.getInfo()); // "Toyota - Speed: 50 km/h - Doors: 4"
```

## 访问修饰符（public, private, protected）

### public 修饰符
```typescript
// public 修饰符（默认）
class PublicExample {
    public name: string;        // 明确声明为 public
    age: number;                // 默认为 public
    
    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
    
    public greet(): string {    // 明确声明为 public
        return `Hello, I'm ${this.name}`;
    }
    
    introduce(): string {       // 默认为 public
        return `I'm ${this.age} years old`;
    }
}

let publicObj = new PublicExample("Alice", 30);
console.log(publicObj.name);    // "Alice" - 可以访问
console.log(publicObj.age);     // 30 - 可以访问
console.log(publicObj.greet()); // "Hello, I'm Alice" - 可以调用
console.log(publicObj.introduce()); // "I'm 30 years old" - 可以调用
```

### private 修饰符
```typescript
// private 修饰符
class PrivateExample {
    private secret: string;
    private password: string;
    
    constructor(secret: string, password: string) {
        this.secret = secret;
        this.password = password;
    }
    
    private validatePassword(input: string): boolean {
        return input === this.password;
    }
    
    public revealSecret(inputPassword: string): string | null {
        if (this.validatePassword(inputPassword)) {
            return this.secret;
        }
        return null;
    }
    
    // private 构造函数（用于单例模式）
    private constructor(secret: string) {
        this.secret = secret;
    }
    
    private static instance: PrivateExample;
    
    public static getInstance(secret: string): PrivateExample {
        if (!PrivateExample.instance) {
            PrivateExample.instance = new PrivateExample(secret);
        }
        return PrivateExample.instance;
    }
}

let privateObj = new PrivateExample("Top Secret", "123456");
// privateObj.secret; // 错误！private 属性不能在类外部访问
// privateObj.validatePassword("123"); // 错误！private 方法不能在类外部调用

let secret = privateObj.revealSecret("123456"); // 通过 public 方法访问
console.log(secret); // "Top Secret"

// 单例模式示例
let instance1 = PrivateExample.getInstance("Secret1");
let instance2 = PrivateExample.getInstance("Secret2");
console.log(instance1 === instance2); // true - 同一个实例
```

### protected 修饰符
```typescript
// protected 修饰符
class ProtectedExample {
    protected name: string;
    protected internalId: string;
    
    constructor(name: string) {
        this.name = name;
        this.internalId = Math.random().toString(36);
    }
    
    protected generateReport(): string {
        return `Report for ${this.name} (${this.internalId})`;
    }
    
    public getPublicInfo(): string {
        return this.name; // 可以访问 protected 属性
    }
}

class ExtendedExample extends ProtectedExample {
    private department: string;
    
    constructor(name: string, department: string) {
        super(name);
        this.department = department;
    }
    
    public getFullInfo(): string {
        // 可以访问父类的 protected 属性和方法
        return `${this.name} - ${this.department} - ${this.generateReport()}`;
    }
    
    public tryAccess(): void {
        console.log(this.name);        // 可以访问
        console.log(this.internalId);  // 可以访问
        console.log(this.generateReport()); // 可以调用
    }
}

let protectedObj = new ProtectedExample("Base");
// protectedObj.name; // 错误！protected 属性不能在类外部访问

let extendedObj = new ExtendedExample("Extended", "IT");
console.log(extendedObj.getPublicInfo()); // "Extended" - 可以访问
console.log(extendedObj.getFullInfo());   // 可以访问 protected 成员
extendedObj.tryAccess(); // 可以访问所有 protected 成员
```

### 访问修饰符的实际应用
```typescript
// 实际应用示例：银行账户系统
class BankAccount {
    protected accountNumber: string;
    private balance: number;
    private pin: string;
    
    constructor(accountNumber: string, initialBalance: number, pin: string) {
        this.accountNumber = accountNumber;
        this.balance = initialBalance;
        this.pin = pin;
    }
    
    protected validatePin(inputPin: string): boolean {
        return inputPin === this.pin;
    }
    
    public getAccountNumber(): string {
        return this.accountNumber; // protected 属性可以被 public 方法访问
    }
    
    public getBalance(pin: string): number | null {
        if (this.validatePin(pin)) {
            return this.balance;
        }
        return null;
    }
    
    protected updateBalance(amount: number): void {
        this.balance += amount;
    }
}

class SavingsAccount extends BankAccount {
    private interestRate: number;
    
    constructor(
        accountNumber: string, 
        initialBalance: number, 
        pin: string, 
        interestRate: number
    ) {
        super(accountNumber, initialBalance, pin);
        this.interestRate = interestRate;
    }
    
    public addInterest(): void {
        // 可以访问父类的 protected 方法
        const interest = this.getBalance("dummy")! * this.interestRate;
        this.updateBalance(interest); // 访问 protected 方法
    }
    
    public deposit(pin: string, amount: number): boolean {
        if (this.validatePin(pin)) { // 访问 protected 方法
            this.updateBalance(amount); // 访问 protected 方法
            return true;
        }
        return false;
    }
}

let account = new SavingsAccount("123456789", 1000, "1234", 0.05);
console.log(account.getAccountNumber()); // "123456789"
console.log(account.getBalance("1234")); // 1000
// account.balance; // 错误！private 属性
// account.pin; // 错误！private 属性
```

## 只读修饰符

### 基本只读属性
```typescript
// 只读属性
class ReadOnlyExample {
    readonly id: string;
    readonly createdAt: Date;
    readonly name: string;
    
    constructor(name: string) {
        this.name = name;
        this.id = Math.random().toString(36);
        this.createdAt = new Date();
        
        // 只能在构造函数中修改 readonly 属性
        // this.id = "new-id"; // 错误！构造函数外不能修改
    }
    
    public getInfo(): string {
        return `ID: ${this.id}, Name: ${this.name}, Created: ${this.createdAt}`;
    }
    
    // private readonly 属性
    private readonly secretKey: string = "secret123";
    
    public getSecretLength(): number {
        return this.secretKey.length; // 可以读取
        // this.secretKey = "new-secret"; // 错误！不能修改
    }
}

let readOnlyObj = new ReadOnlyExample("Test");
console.log(readOnlyObj.getInfo());
// readOnlyObj.id = "new-id"; // 错误！不能修改 readonly 属性
// readOnlyObj.createdAt = new Date(); // 错误！不能修改 readonly 属性
```

### 参数属性中的只读
```typescript
// 参数属性中的 readonly
class Product {
    constructor(
        public readonly name: string,
        public readonly price: number,
        private readonly category: string,
        protected readonly sku: string
    ) {
        // readonly 属性在构造函数参数中自动初始化
    }
    
    public getProductInfo(): string {
        return `${this.name} - $${this.price}`;
        // this.category; // 可以访问 private readonly
        // this.sku; // 可以访问 protected readonly
    }
    
    public tryModify(): void {
        // this.name = "New Name"; // 错误！readonly 不能修改
        // this.price = 999; // 错误！readonly 不能修改
    }
}

let product = new Product("Laptop", 999.99, "Electronics", "SKU123");
console.log(product.name); // "Laptop" - 可以读取
console.log(product.price); // 999.99 - 可以读取
// product.name = "Desktop"; // 错误！readonly 不能修改
```

### 只读数组和对象
```typescript
// 只读数组和对象属性
class DataContainer {
    public readonly items: readonly string[];
    public readonly config: Readonly<{ 
        apiUrl: string; 
        timeout: number 
    }>;
    
    constructor() {
        // 初始化只读数组和对象
        this.items = ["item1", "item2", "item3"] as const;
        this.config = {
            apiUrl: "https://api.example.com",
            timeout: 5000
        } as const;
    }
    
    public getItems(): readonly string[] {
        return this.items;
    }
    
    public tryModify(): void {
        // this.items.push("new-item"); // 错误！只读数组
        // this.items[0] = "modified"; // 错误！只读数组元素
        // this.config.apiUrl = "new-url"; // 错误！只读对象属性
    }
}

let container = new DataContainer();
let items = container.getItems();
// items.push("test"); // 错误！返回的也是只读数组
```

## 静态属性和方法

### 基本静态成员
```typescript
// 静态属性和方法
class MathUtils {
    // 静态属性
    static readonly PI: number = 3.14159;
    static version: string = "1.0.0";
    
    // 静态方法
    static add(a: number, b: number): number {
        return a + b;
    }
    
    static multiply(a: number, b: number): number {
        return a * b;
    }
    
    // 静态方法访问静态属性
    static getCircleArea(radius: number): number {
        return MathUtils.PI * radius * radius;
    }
    
    // 静态方法访问其他静态方法
    static getCircleCircumference(radius: number): number {
        return MathUtils.multiply(2, MathUtils.PI * radius);
    }
}

// 使用静态成员
console.log(MathUtils.PI); // 3.14159
console.log(MathUtils.version); // "1.0.0"
console.log(MathUtils.add(5, 3)); // 8
console.log(MathUtils.getCircleArea(5)); // 78.53975

// 修改静态属性
MathUtils.version = "1.1.0";
console.log(MathUtils.version); // "1.1.0"
```

### 静态成员与实例成员
```typescript
// 静态成员与实例成员的区别
class Counter {
    // 实例属性
    private count: number = 0;
    
    // 静态属性
    private static totalInstances: number = 0;
    public static globalCount: number = 0;
    
    constructor() {
        Counter.totalInstances++; // 访问静态属性
    }
    
    // 实例方法
    public increment(): void {
        this.count++;
        Counter.globalCount++; // 实例方法可以访问静态属性
    }
    
    public getCount(): number {
        return this.count;
    }
    
    // 静态方法
    public static getTotalInstances(): number {
        return Counter.totalInstances;
    }
    
    public static getGlobalCount(): number {
        return Counter.globalCount;
        // return this.count; // 错误！静态方法不能访问实例属性
    }
    
    // 静态方法不能访问实例方法
    public static createCounter(): Counter {
        return new Counter();
        // this.increment(); // 错误！静态方法不能调用实例方法
    }
}

let counter1 = new Counter();
let counter2 = new Counter();

counter1.increment();
counter2.increment();
counter2.increment();

console.log(counter1.getCount()); // 1
console.log(counter2.getCount()); // 2
console.log(Counter.getTotalInstances()); // 2
console.log(Counter.getGlobalCount()); // 3
```

### 静态块（TypeScript 4.4+）
```typescript
// 静态块
class DatabaseConfig {
    static host: string;
    static port: number;
    static database: string;
    
    // 静态块用于复杂初始化
    static {
        // 从环境变量读取配置
        this.host = process.env.DB_HOST || "localhost";
        this.port = parseInt(process.env.DB_PORT || "5432");
        this.database = process.env.DB_NAME || "myapp";
        
        // 执行一些初始化逻辑
        console.log("Database configuration loaded");
    }
    
    static getConnectionUrl(): string {
        return `postgresql://${this.host}:${this.port}/${this.database}`;
    }
}

// 静态块中的错误处理
class AppConfig {
    static debug: boolean;
    static environment: string;
    
    static {
        try {
            this.environment = process.env.NODE_ENV || "development";
            this.debug = this.environment === "development";
        } catch (error) {
            console.error("Failed to load app config:", error);
            this.environment = "unknown";
            this.debug = false;
        }
    }
}
```

### 工厂模式与静态方法
```typescript
// 使用静态方法实现工厂模式
class ShapeFactory {
    static createShape(type: string, ...args: any[]): Shape {
        switch (type) {
            case "circle":
                return new Circle(args[0]);
            case "rectangle":
                return new Rectangle(args[0], args[1]);
            case "triangle":
                return new Triangle(args[0], args[1], args[2]);
            default:
                throw new Error(`Unknown shape type: ${type}`);
        }
    }
    
    static createRandomShape(): Shape {
        const shapes = ["circle", "rectangle", "triangle"];
        const randomType = shapes[Math.floor(Math.random() * shapes.length)];
        return this.createShape(randomType, 10, 20, 30);
    }
}

interface Shape {
    getArea(): number;
}

class Circle implements Shape {
    constructor(private radius: number) {}
    getArea(): number {
        return Math.PI * this.radius * this.radius;
    }
}

class Rectangle implements Shape {
    constructor(private width: number, private height: number) {}
    getArea(): number {
        return this.width * this.height;
    }
}

// 使用工厂
let circle = ShapeFactory.createShape("circle", 5);
let rectangle = ShapeFactory.createShape("rectangle", 10, 20);
let randomShape = ShapeFactory.createRandomShape();

console.log(circle.getArea());
console.log(rectangle.getArea());
```

## 抽象类

### 基本抽象类
```typescript
// 抽象类定义
abstract class Animal {
    protected name: string;
    protected age: number;
    
    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
    
    // 具体方法
    public getInfo(): string {
        return `${this.name} is ${this.age} years old`;
    }
    
    // 抽象方法 - 必须在子类中实现
    abstract makeSound(): void;
    
    // 抽象方法
    abstract move(distance: number): void;
    
    // 可以有抽象 getter/setter
    abstract get species(): string;
}

// 继承抽象类
class Dog extends Animal {
    private breed: string;
    
    constructor(name: string, age: number, breed: string) {
        super(name, age);
        this.breed = breed;
    }
    
    // 实现抽象方法
    makeSound(): void {
        console.log("Woof! Woof!");
    }
    
    // 实现抽象方法
    move(distance: number): void {
        console.log(`${this.name} runs ${distance} meters`);
    }
    
    // 实现抽象属性
    get species(): string {
        return "Canine";
    }
    
    // 新增方法
    getBreed(): string {
        return this.breed;
    }
}

// 不能直接实例化抽象类
// let animal = new Animal("Generic", 5); // 错误！

// 可以实例化具体子类
let dog = new Dog("Buddy", 3, "Golden Retriever");
dog.makeSound(); // "Woof! Woof!"
dog.move(10); // "Buddy runs 10 meters"
console.log(dog.species); // "Canine"
```

### 复杂抽象类示例
```typescript
// 复杂的抽象类示例
abstract class DatabaseConnection {
    protected connectionString: string;
    protected isConnected: boolean = false;
    
    constructor(connectionString: string) {
        this.connectionString = connectionString;
    }
    
    // 模板方法模式
    public async connect(): Promise<void> {
        if (this.isConnected) {
            console.log("Already connected");
            return;
        }
        
        console.log("Connecting to database...");
        await this.openConnection();
        this.isConnected = true;
        console.log("Connected successfully");
    }
    
    public async disconnect(): Promise<void> {
        if (!this.isConnected) {
            console.log("Not connected");
            return;
        }
        
        console.log("Disconnecting from database...");
        await this.closeConnection();
        this.isConnected = false;
        console.log("Disconnected successfully");
    }
    
    // 抽象方法 - 子类必须实现
    protected abstract openConnection(): Promise<void>;
    protected abstract closeConnection(): Promise<void>;
    public abstract executeQuery(query: string): Promise<any>;
    
    // 具体方法
    public isConnectedStatus(): boolean {
        return this.isConnected;
    }
    
    // 抽象 getter
    public abstract get databaseType(): string;
}

// 具体实现
class PostgreSQLConnection extends DatabaseConnection {
    constructor(connectionString: string) {
        super(connectionString);
    }
    
    protected async openConnection(): Promise<void> {
        // PostgreSQL 连接逻辑
        await new Promise(resolve => setTimeout(resolve, 1000));
        console.log("PostgreSQL connection established");
    }
    
    protected async closeConnection(): Promise<void> {
        // PostgreSQL 断开连接逻辑
        await new Promise(resolve => setTimeout(resolve, 500));
        console.log("PostgreSQL connection closed");
    }
    
    public async executeQuery(query: string): Promise<any> {
        if (!this.isConnected) {
            throw new Error("Not connected to database");
        }
        
        console.log(`Executing PostgreSQL query: ${query}`);
        // 模拟查询执行
        return { rows: [], rowCount: 0 };
    }
    
    public get databaseType(): string {
        return "PostgreSQL";
    }
}

class MySQLConnection extends DatabaseConnection {
    constructor(connectionString: string) {
        super(connectionString);
    }
    
    protected async openConnection(): Promise<void> {
        // MySQL 连接逻辑
        await new Promise(resolve => setTimeout(resolve, 800));
        console.log("MySQL connection established");
    }
    
    protected async closeConnection(): Promise<void> {
        // MySQL 断开连接逻辑
        await new Promise(resolve => setTimeout(resolve, 300));
        console.log("MySQL connection closed");
    }
    
    public async executeQuery(query: string): Promise<any> {
        if (!this.isConnected) {
            throw new Error("Not connected to database");
        }
        
        console.log(`Executing MySQL query: ${query}`);
        // 模拟查询执行
        return { results: [], affectedRows: 0 };
    }
    
    public get databaseType(): string {
        return "MySQL";
    }
}

// 使用抽象类
async function useDatabase(connection: DatabaseConnection) {
    console.log(`Database type: ${connection.databaseType}`);
    
    await connection.connect();
    await connection.executeQuery("SELECT * FROM users");
    await connection.disconnect();
}

// let db = new DatabaseConnection("connection-string"); // 错误！抽象类不能实例化

let postgresDB = new PostgreSQLConnection("postgresql://localhost:5432/mydb");
let mysqlDB = new MySQLConnection("mysql://localhost:3306/mydb");

useDatabase(postgresDB);
useDatabase(mysqlDB);
```

### 抽象类与接口的结合
```typescript
// 接口定义契约
interface Logger {
    log(message: string): void;
    error(message: string): void;
}

// 抽象类提供部分实现
abstract class BaseLogger implements Logger {
    protected abstract getTimestamp(): string;
    
    log(message: string): void {
        console.log(`[${this.getTimestamp()}] LOG: ${message}`);
    }
    
    error(message: string): void {
        console.error(`[${this.getTimestamp()}] ERROR: ${message}`);
    }
    
    // 可以有具体方法
    public logWithLevel(level: string, message: string): void {
        console.log(`[${this.getTimestamp()}] ${level.toUpperCase()}: ${message}`);
    }
}

// 具体实现
class ConsoleLogger extends BaseLogger {
    protected getTimestamp(): string {
        return new Date().toISOString();
    }
}

class FileLogger extends BaseLogger {
    private fileName: string;
    
    constructor(fileName: string) {
        super();
        this.fileName = fileName;
    }
    
    protected getTimestamp(): string {
        return new Date().toLocaleString();
    }
    
    log(message: string): void {
        super.log(message);
        // 额外的文件写入逻辑
        console.log(`Writing to file: ${this.fileName}`);
    }
}

let consoleLogger = new ConsoleLogger();
let fileLogger = new FileLogger("app.log");

consoleLogger.log("Application started");
fileLogger.error("Database connection failed");
```

## 存取器（Getters and Setters）

### 基本存取器
```typescript
// 基本存取器
class Employee {
    private _firstName: string;
    private _lastName: string;
    private _salary: number;
    
    constructor(firstName: string, lastName: string, salary: number) {
        this._firstName = firstName;
        this._lastName = lastName;
        this._salary = salary;
    }
    
    // Getter
    get firstName(): string {
        return this._firstName;
    }
    
    // Setter
    set firstName(value: string) {
        if (value.length === 0) {
            throw new Error("First name cannot be empty");
        }
        this._firstName = value;
    }
    
    // 只读 getter
    get fullName(): string {
        return `${this._firstName} ${this._lastName}`;
    }
    
    // Getter 和 Setter 配对
    get salary(): number {
        return this._salary;
    }
    
    set salary(value: number) {
        if (value < 0) {
            throw new Error("Salary cannot be negative");
        }
        this._salary = value;
    }
    
    // 计算属性
    get annualSalary(): number {
        return this._salary * 12;
    }
}

let employee = new Employee("John", "Doe", 5000);
console.log(employee.firstName); // "John"
console.log(employee.fullName); // "John Doe"
console.log(employee.annualSalary); // 60000

employee.firstName = "Jane";
employee.salary = 6000;
console.log(employee.fullName); // "Jane Doe"
console.log(employee.annualSalary); // 72000

// employee.firstName = ""; // 抛出错误
// employee.salary = -1000; // 抛出错误
```

### 复杂存取器示例
```typescript
// 复杂存取器示例
class Temperature {
    private _celsius: number;
    
    constructor(celsius: number) {
        this._celsius = celsius;
    }
    
    // 摄氏度存取器
    get celsius(): number {
        return this._celsius;
    }
    
    set celsius(value: number) {
        if (value < -273.15) {
            throw new Error("Temperature cannot be below absolute zero");
        }
        this._celsius = value;
    }
    
    // 华氏度存取器
    get fahrenheit(): number {
        return (this._celsius * 9/5) + 32;
    }
    
    set fahrenheit(value: number) {
        if (value < -459.67) {
            throw new Error("Temperature cannot be below absolute zero");
        }
        this._celsius = (value - 32) * 5/9;
    }
    
    // 开尔文存取器
    get kelvin(): number {
        return this._celsius + 273.15;
    }
    
    set kelvin(value: number) {
        if (value < 0) {
            throw new Error("Temperature cannot be below absolute zero");
        }
        this._celsius = value - 273.15;
    }
    
    // 格式化显示
    get formatted(): string {
        return `${this._celsius}°C (${this.fahrenheit.toFixed(1)}°F)`;
    }
}

let temp = new Temperature(25);
console.log(temp.formatted); // "25°C (77.0°F)"

temp.fahrenheit = 100;
console.log(temp.celsius); // 37.777...
console.log(temp.formatted); // "37.8°C (100.0°F)"

temp.kelvin = 0;
console.log(temp.celsius); // -273.15
// temp.celsius = -300; // 抛出错误
```

### 存取器与验证
```typescript
// 存取器与数据验证
class User {
    private _email: string = "";
    private _age: number = 0;
    private _password: string = "";
    
    // Email 验证存取器
    get email(): string {
        return this._email;
    }
    
    set email(value: string) {
        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        if (!emailRegex.test(value)) {
            throw new Error("Invalid email format");
        }
        this._email = value.toLowerCase();
    }
    
    // 年龄验证存取器
    get age(): number {
        return this._age;
    }
    
    set age(value: number) {
        if (value < 0 || value > 150) {
            throw new Error("Age must be between 0 and 150");
        }
        this._age = value;
    }
    
    // 密码安全存取器
    get password(): string {
        return "*".repeat(this._password.length);
    }
    
    set password(value: string) {
        if (value.length < 8) {
            throw new Error("Password must be at least 8 characters long");
        }
        if (!/[A-Z]/.test(value)) {
            throw new Error("Password must contain at least one uppercase letter");
        }
        if (!/[0-9]/.test(value)) {
            throw new Error("Password must contain at least one digit");
        }
        this._password = value;
    }
    
    // 只读属性
    get isAdult(): boolean {
        return this._age >= 18;
    }
    
    // 计算属性
    get securityScore(): number {
        let score = 0;
        if (this._password.length >= 12) score += 30;
        if (/[!@#$%^&*(),.?":{}|<>]/.test(this._password)) score += 20;
        if (/[a-z]/.test(this._password) && /[A-Z]/.test(this._password)) score += 20;
        return Math.min(score, 100);
    }
}

let user = new User();
try {
    user.email = "user@example.com";
    user.age = 25;
    user.password = "MySecurePass123!";
    
    console.log(user.email); // "user@example.com"
    console.log(user.password); // "*************"
    console.log(user.isAdult); // true
    console.log(user.securityScore); // 70
} catch (error) {
    console.error(error.message);
}
```

### 存取器与惰性初始化
```typescript
// 存取器与惰性初始化
class ExpensiveObject {
    private _data: string[] | null = null;
    private _computedValue: number | null = null;
    
    // 惰性初始化数据
    get data(): string[] {
        if (this._data === null) {
            console.log("Initializing expensive data...");
            // 模拟昂贵的计算或数据获取
            this._data = Array.from({ length: 1000 }, (_, i) => `Item ${i}`);
        }
        return this._data;
    }
    
    // 惰性计算属性
    get computedValue(): number {
        if (this._computedValue === null) {
            console.log("Computing expensive value...");
            // 模拟复杂的计算
            this._computedValue = this.data.length * Math.random();
        }
        return this._computedValue;
    }
    
    // 重置缓存
    public resetCache(): void {
        this._data = null;
        this._computedValue = null;
    }
    
    get dataCount(): number {
        return this.data.length; // 触发惰性初始化
    }
}

let obj = new ExpensiveObject();
console.log("Object created");

// 第一次访问触发初始化
console.log(obj.dataCount); // "Initializing expensive data..." 然后输出 1000

// 后续访问使用缓存
console.log(obj.computedValue); // "Computing expensive value..." 然后输出计算结果
console.log(obj.computedValue); // 直接返回缓存结果，无额外输出

obj.resetCache(); // 重置缓存
console.log(obj.dataCount); // 再次触发初始化
```

## 类表达式

### 基本类表达式
```typescript
// 基本类表达式
let MyClass = class {
    name: string;
    
    constructor(name: string) {
        this.name = name;
    }
    
    greet(): string {
        return `Hello, ${this.name}!`;
    }
};

let instance = new MyClass("Alice");
console.log(instance.greet()); // "Hello, Alice!"

// 命名类表达式
let NamedClass = class Person {
    constructor(public name: string) {}
    
    introduce(): string {
        return `I'm ${this.name}`;
    }
};

let person = new NamedClass("Bob");
console.log(person.introduce()); // "I'm Bob"

// 在类表达式内部可以引用类名
let SelfReferencingClass = class Node {
    children: Node[] = [];
    
    constructor(public value: string) {}
    
    addChild(value: string): Node {
        let child = new Node(value);
        this.children.push(child);
        return child;
    }
    
    // 可以使用类名进行类型检查
    findChild(value: string): Node | null {
        if (this.value === value) return this;
        
        for (let child of this.children) {
            let found = child.findChild(value);
            if (found) return found;
        }
        
        return null;
    }
};
```

### 动态类创建
```typescript
// 动态创建类
function createClass(name: string, methods: any) {
    return class DynamicClass {
        constructor() {
            // 动态添加属性
            (this as any).className = name;
        }
        
        // 动态添加方法
        [key: string]: any;
    };
}

// 为动态类添加方法
let DynamicPerson = createClass("Person", {});
(DynamicPerson.prototype as any).greet = function() {
    return `Hello from ${this.className}`;
};

let dynamicInstance = new DynamicPerson();
console.log(dynamicInstance.greet()); // "Hello from Person"
```

### 类表达式与工厂函数
```typescript
// 使用类表达式实现工厂函数
function createLogger(type: "console" | "file"): any {
    if (type === "console") {
        return class ConsoleLogger {
            log(message: string): void {
                console.log(`[CONSOLE] ${message}`);
            }
        };
    } else {
        return class FileLogger {
            log(message: string): void {
                console.log(`[FILE] ${message}`);
            }
        };
    }
}

let ConsoleLogger = createLogger("console");
let FileLogger = createLogger("file");

let consoleLogger = new ConsoleLogger();
let fileLogger = new FileLogger();

consoleLogger.log("Console message");
fileLogger.log("File message");
```

### 类表达式与装饰器
```typescript
// 类表达式与装饰器结合
function addMethod(methodName: string, method: Function) {
    return function<T extends { new (...args: any[]): {} }>(constructor: T) {
        return class extends constructor {
            [key: string]: any;
        };
    };
}

// 使用类表达式添加方法
let EnhancedClass = addMethod("extraMethod", function() {
    return "Extra functionality";
})(class BaseClass {
    baseMethod(): string {
        return "Base functionality";
    }
});

// 动态添加方法到类表达式
(EnhancedClass.prototype as any).extraMethod = function() {
    return "Extra functionality";
};

let enhancedInstance = new EnhancedClass();
console.log(enhancedInstance.baseMethod()); // "Base functionality"
console.log((enhancedInstance as any).extraMethod()); // "Extra functionality"
```

### 类表达式的实际应用
```typescript
// 实际应用：策略模式
interface PaymentStrategy {
    pay(amount: number): string;
}

let CreditCardStrategy = class implements PaymentStrategy {
    pay(amount: number): string {
        return `Paid $${amount} using Credit Card`;
    }
};

let PayPalStrategy = class implements PaymentStrategy {
    pay(amount: number): string {
        return `Paid $${amount} using PayPal`;
    }
};

let BitcoinStrategy = class implements PaymentStrategy {
    pay(amount: number): string {
        return `Paid $${amount} using Bitcoin`;
    }
};

// 支付上下文
class PaymentContext {
    private strategy: PaymentStrategy;
    
    constructor(strategy: PaymentStrategy) {
        this.strategy = strategy;
    }
    
    setStrategy(strategy: PaymentStrategy): void {
        this.strategy = strategy;
    }
    
    executePayment(amount: number): string {
        return this.strategy.pay(amount);
    }
}

// 使用不同的支付策略
let context = new PaymentContext(new CreditCardStrategy());
console.log(context.executePayment(100));

context.setStrategy(new PayPalStrategy());
console.log(context.executePayment(50));

context.setStrategy(new BitcoinStrategy());
console.log(context.executePayment(200));
```

# 7. 泛型

## 泛型函数

### 基本泛型函数
```typescript
// 不使用泛型的问题
function identityAny(arg: any): any {
    return arg;
}
// 问题：丢失了类型信息，返回值可能是任何类型

// 使用泛型解决
function identity<T>(arg: T): T {
    return arg;
}

// 使用泛型函数
let output1 = identity<string>("myString"); // 明确指定类型参数
let output2 = identity("myString");         // 类型推断
let output3 = identity<number>(42);
let output4 = identity(42);                 // 类型推断

// 泛型函数的实际应用
function firstElement<T>(arr: T[]): T | undefined {
    return arr[0];
}

let firstString = firstElement(["a", "b", "c"]); // string | undefined
let firstNumber = firstElement([1, 2, 3]);       // number | undefined
```

### 多个类型参数
```typescript
// 多个类型参数的泛型函数
function swap<T, U>(tuple: [T, U]): [U, T] {
    return [tuple[1], tuple[0]];
}

let swapped = swap(["hello", 42]); // [number, string]

// 复杂的多类型参数函数
function mapObject<T, U>(
    obj: T,
    mapper: (value: T[keyof T]) => U
): { [K in keyof T]: U } {
    let result = {} as { [K in keyof T]: U };
    for (let key in obj) {
        result[key] = mapper(obj[key]);
    }
    return result;
}

let obj = { a: 1, b: 2, c: 3 };
let mapped = mapObject(obj, x => x * 2); // { a: number, b: number, c: number }
```

### 泛型函数约束
```typescript
// 泛型函数中的类型约束
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
    return obj[key];
}

let person = { name: "Alice", age: 30 };
let name = getProperty(person, "name"); // string
let age = getProperty(person, "age");   // number
// let invalid = getProperty(person, "invalid"); // 编译错误

// 数组操作的泛型函数
function filterArray<T>(arr: T[], predicate: (item: T) => boolean): T[] {
    return arr.filter(predicate);
}

let numbers = [1, 2, 3, 4, 5];
let evens = filterArray(numbers, x => x % 2 === 0); // number[]

let strings = ["hello", "world", "typescript"];
let longStrings = filterArray(strings, s => s.length > 5); // string[]
```

### 泛型函数的高级用法
```typescript
// 条件类型与泛型函数结合
type NonNullable<T> = T extends null | undefined ? never : T;

function compact<T>(arr: T[]): NonNullable<T>[] {
    return arr.filter((item): item is NonNullable<T> => 
        item !== null && item !== undefined
    ) as NonNullable<T>[];
}

let mixedArray = [1, null, "hello", undefined, 42];
let compacted = compact(mixedArray); // (string | number)[]

// 泛型函数与 Promise
async function fetchAndProcess<T>(
    url: string,
    processor: (data: any) => T
): Promise<T> {
    const response = await fetch(url);
    const data = await response.json();
    return processor(data);
}

// 使用示例
interface User {
    id: number;
    name: string;
}

let user = await fetchAndProcess<User>(
    "/api/user/1",
    (data: any) => ({ id: data.id, name: data.name })
);
```

## 泛型接口

### 基本泛型接口
```typescript
// 基本泛型接口
interface GenericIdentityFn<T> {
    (arg: T): T;
}

let myIdentity: GenericIdentityFn<number> = function(arg) {
    return arg;
};

// 泛型接口的实际应用
interface Repository<T> {
    findById(id: string): T | null;
    findAll(): T[];
    save(entity: T): T;
    delete(id: string): boolean;
}

// 实现泛型接口
class User {
    constructor(public id: string, public name: string) {}
}

class UserRepository implements Repository<User> {
    private users: Map<string, User> = new Map();
    
    findById(id: string): User | null {
        return this.users.get(id) || null;
    }
    
    findAll(): User[] {
        return Array.from(this.users.values());
    }
    
    save(entity: User): User {
        this.users.set(entity.id, entity);
        return entity;
    }
    
    delete(id: string): boolean {
        return this.users.delete(id);
    }
}
```

### 复杂泛型接口
```typescript
// 复杂的泛型接口
interface ApiResponse<T> {
    success: boolean;
    data?: T;
    error?: string;
    timestamp: Date;
}

interface PaginatedResponse<T> extends ApiResponse<T[]> {
    pagination: {
        page: number;
        limit: number;
        total: number;
        hasNext: boolean;
        hasPrev: boolean;
    };
}

// 使用泛型接口
let userResponse: ApiResponse<User> = {
    success: true,
    data: new User("1", "Alice"),
    timestamp: new Date()
};

let usersResponse: PaginatedResponse<User> = {
    success: true,
    data: [new User("1", "Alice"), new User("2", "Bob")],
    timestamp: new Date(),
    pagination: {
        page: 1,
        limit: 10,
        total: 2,
        hasNext: false,
        hasPrev: false
    }
};
```

### 泛型接口与函数类型
```typescript
// 泛型函数类型接口
interface MapFunction<T, U> {
    (item: T, index: number, array: T[]): U;
}

interface FilterFunction<T> {
    (item: T, index: number, array: T[]): boolean;
}

interface ReduceFunction<T, U> {
    (accumulator: U, currentValue: T, currentIndex: number, array: T[]): U;
}

// 使用泛型函数类型接口
let mapStringToLength: MapFunction<string, number> = 
    (str, index) => str.length + index;

let filterEvenNumbers: FilterFunction<number> = 
    (num, index) => num % 2 === 0;

let sumReducer: ReduceFunction<number, number> = 
    (acc, curr) => acc + curr;

let strings = ["hello", "world", "typescript"];
let lengths = strings.map(mapStringToLength); // number[]

let numbers = [1, 2, 3, 4, 5];
let evens = numbers.filter(filterEvenNumbers); // number[]
let sum = numbers.reduce(sumReducer, 0); // number
```

### 泛型接口与索引签名
```typescript
// 泛型接口与索引签名
interface Dictionary<T> {
    [key: string]: T;
    length: number; // 可以有已知属性
}

interface NumericDictionary<T> {
    [index: number]: T;
    length: number;
}

// 使用泛型字典接口
let stringDict: Dictionary<string> = {
    "name": "Alice",
    "city": "New York",
    length: 2
};

let numberDict: NumericDictionary<number> = {
    0: 10,
    1: 20,
    2: 30,
    length: 3
};

// 泛型接口与方法
interface Collection<T> {
    add(item: T): void;
    remove(item: T): boolean;
    contains(item: T): boolean;
    [index: number]: T;
    length: number;
}

class StringCollection implements Collection<string> {
    private items: string[] = [];
    
    add(item: string): void {
        this.items.push(item);
    }
    
    remove(item: string): boolean {
        const index = this.items.indexOf(item);
        if (index > -1) {
            this.items.splice(index, 1);
            return true;
        }
        return false;
    }
    
    contains(item: string): boolean {
        return this.items.includes(item);
    }
    
    get length(): number {
        return this.items.length;
    }
    
    get [index: number](): string {
        return this.items[index];
    }
}
```

## 泛型类

### 基本泛型类
```typescript
// 基本泛型类
class GenericNumber<T> {
    zeroValue: T;
    add: (x: T, y: T) => T;
    
    constructor(zeroValue: T, addFn: (x: T, y: T) => T) {
        this.zeroValue = zeroValue;
        this.add = addFn;
    }
}

// 使用泛型类
let myGenericNumber = new GenericNumber<number>(0, (x, y) => x + y);
console.log(myGenericNumber.add(myGenericNumber.zeroValue, 42)); // 42

let stringNumeric = new GenericNumber<string>("", (x, y) => x + y);
console.log(stringNumeric.add(stringNumeric.zeroValue, "test")); // "test"
```

### 泛型类的实际应用
```typescript
// 泛型栈类
class Stack<T> {
    private items: T[] = [];
    
    push(item: T): void {
        this.items.push(item);
    }
    
    pop(): T | undefined {
        return this.items.pop();
    }
    
    peek(): T | undefined {
        return this.items[this.items.length - 1];
    }
    
    isEmpty(): boolean {
        return this.items.length === 0;
    }
    
    size(): number {
        return this.items.length;
    }
    
    clear(): void {
        this.items = [];
    }
}

// 使用泛型栈
let numberStack = new Stack<number>();
numberStack.push(1);
numberStack.push(2);
numberStack.push(3);
console.log(numberStack.pop()); // 3

let stringStack = new Stack<string>();
stringStack.push("hello");
stringStack.push("world");
console.log(stringStack.peek()); // "world"
```

### 泛型类与继承
```typescript
// 泛型基类
class BaseRepository<T> {
    protected items: Map<string, T> = new Map();
    
    findById(id: string): T | null {
        return this.items.get(id) || null;
    }
    
    findAll(): T[] {
        return Array.from(this.items.values());
    }
    
    save(id: string, entity: T): void {
        this.items.set(id, entity);
    }
    
    delete(id: string): boolean {
        return this.items.delete(id);
    }
}

// 继承泛型类
class UserRepository2 extends BaseRepository<User> {
    findByEmail(email: string): User | null {
        for (let user of this.items.values()) {
            // 假设 User 有 email 属性
            if ((user as any).email === email) {
                return user;
            }
        }
        return null;
    }
}

// 泛型子类
class GenericService<T> {
    private repository: BaseRepository<T>;
    
    constructor(repository: BaseRepository<T>) {
        this.repository = repository;
    }
    
    get(id: string): T | null {
        return this.repository.findById(id);
    }
    
    getAll(): T[] {
        return this.repository.findAll();
    }
}

let userRepo = new UserRepository2();
let userService = new GenericService<User>(userRepo);
```

### 泛型类与静态成员
```typescript
// 泛型类的静态成员
class Factory<T> {
    static create<T>(constructor: new () => T): T {
        return new constructor();
    }
    
    static createWithArgs<T>(constructor: new (...args: any[]) => T, ...args: any[]): T {
        return new constructor(...args);
    }
    
    // 实例方法
    createInstance(constructor: new () => T): T {
        return new constructor();
    }
}

// 使用静态泛型方法
class Person {
    constructor(public name: string = "Anonymous") {}
}

let person1 = Factory.create(Person);
let person2 = Factory.createWithArgs(Person, "Alice");
```

## 泛型约束

### 基本泛型约束
```typescript
// 使用 extends 关键字进行约束
interface Lengthwise {
    length: number;
}

function loggingIdentity<T extends Lengthwise>(arg: T): T {
    console.log(arg.length); // 现在我们知道它有 .length 属性
    return arg;
}

// 使用约束函数
loggingIdentity("hello"); // string 有 length 属性
loggingIdentity([1, 2, 3]); // 数组有 length 属性
loggingIdentity({ length: 10, value: "hi" }); // 对象有 length 属性

// loggingIdentity(42); // 错误！number 没有 length 属性

// 多重约束
interface HasName {
    name: string;
}

interface HasAge {
    age: number;
}

function greetPerson<T extends HasName & HasAge>(person: T): string {
    return `Hello, ${person.name}! You are ${person.age} years old.`;
}

let person = { name: "Alice", age: 30, email: "alice@example.com" };
console.log(greetPerson(person)); // 额外属性不影响
```

### 属性约束
```typescript
// 约束特定属性存在
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
    return obj[key];
}

// 约束属性类型
function pluck<T, K extends keyof T>(array: T[], key: K): T[K][] {
    return array.map(x => x[key]);
}

let persons = [
    { name: "Alice", age: 30 },
    { name: "Bob", age: 25 },
    { name: "Charlie", age: 35 }
];

let names = pluck(persons, "name"); // string[]
let ages = pluck(persons, "age");   // number[]
```

### 构造函数约束
```typescript
// 约束类型必须有构造函数
function createInstance<T extends new (...args: any[]) => any>(
    ctor: T,
    ...args: ConstructorParameters<T>
): InstanceType<T> {
    return new ctor(...args);
}

class MyClass {
    constructor(public name: string, public value: number) {}
}

let instance = createInstance(MyClass, "test", 42);
console.log(instance.name); // "test"
console.log(instance.value); // 42
```

### 类型参数约束
```typescript
// 约束类型参数之间的关系
function assign<T extends object, U extends keyof T>(
    obj: T,
    key: U,
    value: T[U]
): void {
    obj[key] = value;
}

let obj = { name: "Alice", age: 30 };
assign(obj, "name", "Bob"); // 正确
assign(obj, "age", 25);     // 正确
// assign(obj, "name", 42); // 错误！类型不匹配

// 复杂约束示例
interface Configurable {
    configure(config: any): void;
}

function configureObject<T extends Configurable>(
    obj: T,
    config: Parameters<T['configure']>[0]
): T {
    obj.configure(config);
    return obj;
}
```

## 泛型参数默认值

### 基本默认值
```typescript
// 泛型参数默认值
class Container<T = string> {
    private value: T;
    
    constructor(value: T) {
        this.value = value;
    }
    
    getValue(): T {
        return this.value;
    }
}

// 使用默认值
let stringContainer = new Container("hello"); // T 默认为 string
let numberContainer = new Container<number>(42); // 显式指定 T 为 number

// 函数泛型默认值
function createArray<T = string>(length: number, value: T): T[] {
    return Array(length).fill(value);
}

let strings = createArray(3, "hello"); // string[]
let numbers = createArray<number>(3, 42); // number[]
```

### 多个默认值
```typescript
// 多个泛型参数的默认值
class Pair<T = string, U = number> {
    constructor(public first: T, public second: U) {}
}

// 使用默认值的不同方式
let pair1 = new Pair("hello", 42);           // string, number
let pair2 = new Pair<string>("hello", 42);   // string, number (第二个参数默认)
let pair3 = new Pair<boolean, string>(true, "yes"); // boolean, string
let pair4 = new Pair();                      // 错误！需要构造函数参数

// 函数多个默认值
function mergeObjects<T extends object = {}, U extends object = {}>(
    obj1: T,
    obj2: U
): T & U {
    return { ...obj1, ...obj2 };
}

let merged1 = mergeObjects({ a: 1 }, { b: 2 }); // { a: number } & { b: number }
let merged2 = mergeObjects<{ x: string }>({ x: "hello" }, { y: 42 });
```

### 复杂默认值
```typescript
// 基于其他参数的默认值
type ResponseType<T = any> = {
    success: boolean;
    data?: T;
    error?: string;
    timestamp: Date;
};

// 使用默认响应类型
let defaultResponse: ResponseType = {
    success: true,
    timestamp: new Date()
};

let userResponse: ResponseType<User> = {
    success: true,
    data: new User("1", "Alice"),
    timestamp: new Date()
};

// 条件默认值
type Maybe<T> = T | null | undefined;
type StrictMaybe<T = never> = T extends never ? null | undefined : T | null | undefined;

// 实际应用
class Cache<T = string> {
    private storage: Map<string, T> = new Map();
    
    set(key: string, value: T): void {
        this.storage.set(key, value);
    }
    
    get(key: string): T | undefined {
        return this.storage.get(key);
    }
    
    has(key: string): boolean {
        return this.storage.has(key);
    }
}

let stringCache = new Cache(); // T 默认为 string
let userCache = new Cache<User>(); // T 为 User
```

### 默认值与约束结合
```typescript
// 默认值与约束结合
interface Identifiable {
    id: string;
}

class Repository<T extends Identifiable = User> {
    private items: Map<string, T> = new Map();
    
    add(item: T): void {
        this.items.set(item.id, item);
    }
    
    getById(id: string): T | undefined {
        return this.items.get(id);
    }
    
    getAll(): T[] {
        return Array.from(this.items.values());
    }
}

// 使用默认类型
let defaultRepo = new Repository(); // T 默认为 User
let userRepo3 = new Repository<User>();
let productRepo = new Repository<Product>();

// 函数默认值与约束
function processItems<T extends string[] = string[]>(
    items: T
): { [K in keyof T]: string } {
    return items.map(item => item.toString()) as any;
}

let processed = processItems(["a", "b", "c"]); // string[]
```

## 条件类型与泛型

### 基本条件类型
```typescript
// 基本条件类型语法：T extends U ? X : Y
type NonNullable<T> = T extends null | undefined ? never : T;

type A = NonNullable<string | null>;        // string
type B = NonNullable<number | undefined>;   // number
type C = NonNullable<string | number>;      // string | number
type D = NonNullable<null | undefined>;     // never

// 条件类型的实际应用
type MessageOf<T> = T extends { message: unknown } ? T['message'] : never;

interface Email {
    message: string;
}

interface SMS {
    message: string;
    phoneNumber: string;
}

interface VoiceCall {
    duration: number;
}

type EmailMessage = MessageOf<Email>;  // string
type SMSMessage = MessageOf<SMS>;      // string
type VoiceMessage = MessageOf<VoiceCall>; // never
```

### 分布式条件类型
```typescript
// 分布式条件类型
type ToArray<T> = T extends any ? T[] : never;

type A1 = ToArray<string>;              // string[]
type A2 = ToArray<string | number>;     // string[] | number[]
type A3 = ToArray<string | number | boolean>; // string[] | number[] | boolean[]

// 与泛型函数结合
type Flatten<T> = T extends any[] ? T[number] : T;

type B1 = Flatten<string[]>;            // string
type B2 = Flatten<number[][]>;          // number[]
type B3 = Flatten<string>;              // string

// 实用工具类型
type StringKeys<T> = {
    [K in keyof T]: T[K] extends string ? K : never
}[keyof T];

interface Person2 {
    name: string;
    age: number;
    email: string;
    isActive: boolean;
}

type StringKey = StringKeys<Person2>; // "name" | "email"
```

### 条件类型与 infer
```typescript
// 使用 infer 关键字
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : any;

type C1 = ReturnType<() => string>;           // string
type C2 = ReturnType<(x: number) => number[]>; // number[]
type C3 = ReturnType<string>;                 // any

// 获取函数参数类型
type Parameters<T> = T extends (...args: infer P) => any ? P : never;

type D1 = Parameters<(name: string, age: number) => void>; // [string, number]
type D2 = Parameters<() => boolean>;                       // []
type D3 = Parameters<string>;                              // never

// 获取构造函数参数
type ConstructorParameters<T> = T extends new (...args: infer P) => any ? P : never;

type E1 = ConstructorParameters<typeof Person>; // [string] (假设构造函数参数)

// 获取实例类型
type InstanceType<T> = T extends new (...args: any[]) => infer R ? R : any;

type F1 = InstanceType<typeof Person>; // Person
```

### 复杂条件类型
```typescript
// 复杂条件类型示例
type DeepReadonly<T> = T extends any[] 
    ? DeepReadonlyArray<T[number]> 
    : T extends object 
    ? DeepReadonlyObject<T> 
    : T;

interface DeepReadonlyArray<T> extends ReadonlyArray<DeepReadonly<T>> {}

type DeepReadonlyObject<T> = {
    readonly [P in keyof T]: DeepReadonly<T[P]>;
};

// 使用深度只读
interface NestedObject {
    name: string;
    details: {
        age: number;
        hobbies: string[];
        address: {
            street: string;
            city: string;
        };
    };
}

type ReadonlyNested = DeepReadonly<NestedObject>;

let readonlyObj: ReadonlyNested = {
    name: "Alice",
    details: {
        age: 30,
        hobbies: ["reading", "swimming"],
        address: {
            street: "123 Main St",
            city: "New York"
        }
    }
};

// readonlyObj.name = "Bob"; // 错误！
// readonlyObj.details.age = 31; // 错误！
// readonlyObj.details.hobbies[0] = "coding"; // 错误！
```

## 映射类型与泛型

### 基本映射类型
```typescript
// 基本映射类型语法：{ [P in keyof T]: X }
type Readonly<T> = {
    readonly [P in keyof T]: T[P];
};

type Partial<T> = {
    [P in keyof T]?: T[P];
};

type Required<T> = {
    [P in keyof T]-?: T[P];
};

// 使用映射类型
interface User2 {
    name: string;
    age: number;
    email?: string;
}

type ReadonlyUser = Readonly<User2>;
type PartialUser = Partial<User2>;
type RequiredUser = Required<User2>;

let readonlyUser: ReadonlyUser = {
    name: "Alice",
    age: 30,
    email: "alice@example.com"
};

// readonlyUser.name = "Bob"; // 错误！只读属性

let partialUser: PartialUser = {
    name: "Bob" // 可以只提供部分属性
};

let requiredUser: RequiredUser = {
    name: "Charlie",
    age: 25,
    email: "charlie@example.com" // email 变为必需
};
```

### 映射类型修饰符
```typescript
// 映射类型修饰符
// +? 可选，-? 必需，+readonly 只读，-readonly 可写

type Mutable<T> = {
    -readonly [P in keyof T]: T[P];
};

type Complete<T> = {
    [P in keyof T]-?: T[P];
};

interface OptionalUser {
    name?: string;
    age?: number;
    email?: string;
}

type CompleteUser = Complete<OptionalUser>;

let completeUser: CompleteUser = {
    name: "Alice",
    age: 30,
    email: "alice@example.com" // 所有属性都必需
};

// 移除只读修饰符
interface ReadOnlyPoint {
    readonly x: number;
    readonly y: number;
}

type MutablePoint = Mutable<ReadOnlyPoint>;

let mutablePoint: MutablePoint = { x: 10, y: 20 };
mutablePoint.x = 15; // 正确！现在是可变的
```

### 键重映射
```typescript
// 键重映射（TypeScript 4.1+）
type Getters<T> = {
    [K in keyof T as `get${Capitalize<string & K>}`]: () => T[K]
};

interface Person3 {
    name: string;
    age: number;
    email: string;
}

type PersonGetters = Getters<Person3>;

// 结果类型：
// {
//     getName: () => string;
//     getAge: () => number;
//     getEmail: () => string;
// }

// 移除特定属性
type RemoveKindField<T> = {
    [K in keyof T as Exclude<K, "kind">]: T[K]
};

interface Circle2 {
    kind: "circle";
    radius: number;
}

interface Square2 {
    kind: "square";
    sideLength: number;
}

type CircleWithoutKind = RemoveKindField<Circle2>; // { radius: number }
type SquareWithoutKind = RemoveKindField<Square2>; // { sideLength: number }
```

### 模板字面量类型与映射
```typescript
// 模板字面量类型与映射类型结合
type EventHandlers<T> = {
    [K in keyof T as `on${Capitalize<string & K>}Change`]?: (value: T[K]) => void
};

interface FormState {
    name: string;
    age: number;
    isActive: boolean;
}

type FormEventHandlers = EventHandlers<FormState>;

// 结果类型：
// {
//     onNameChange?: (value: string) => void;
//     onAgeChange?: (value: number) => void;
//     onIsActiveChange?: (value: boolean) => void;
// }

// 实际使用
class FormManager {
    private state: FormState = {
        name: "",
        age: 0,
        isActive: false
    };
    
    private handlers: FormEventHandlers = {};
    
    setState<K extends keyof FormState>(key: K, value: FormState[K]): void {
        this.state[key] = value;
        const handlerKey = `on${key.charAt(0).toUpperCase() + key.slice(1)}Change` as 
            keyof FormEventHandlers;
        this.handlers[handlerKey]?.(value);
    }
    
    onChange<K extends keyof FormState>(
        key: K, 
        handler: (value: FormState[K]) => void
    ): void {
        const handlerKey = `on${key.charAt(0).toUpperCase() + key.slice(1)}Change` as 
            keyof FormEventHandlers;
        this.handlers[handlerKey] = handler;
    }
}
```

### 高级映射类型
```typescript
// 高级映射类型示例
type FunctionPropertyNames<T> = {
    [K in keyof T]: T[K] extends Function ? K : never
}[keyof T];

type FunctionProperties<T> = Pick<T, FunctionPropertyNames<T>>;

type NonFunctionPropertyNames<T> = {
    [K in keyof T]: T[K] extends Function ? never : K
}[keyof T];

type NonFunctionProperties<T> = Pick<T, NonFunctionPropertyNames<T>>;

interface SampleObject {
    name: string;
    age: number;
    greet(): string;
    calculate(x: number, y: number): number;
}

type FuncNames = FunctionPropertyNames<SampleObject>; // "greet" | "calculate"
type FuncProps = FunctionProperties<SampleObject>;     // { greet(): string; calculate(x: number, y: number): number; }
type NonFuncNames = NonFunctionPropertyNames<SampleObject>; // "name" | "age"
type NonFuncProps = NonFunctionProperties<SampleObject>;   // { name: string; age: number; }

// 条件映射类型
type Diff<T, U> = T extends U ? never : T;
type Filter<T, U> = {
    [K in keyof T]: T[K] extends U ? K : never
}[keyof T];

type StringKeysOnly<T> = {
    [K in Filter<T, string>]: T[K]
};

interface MixedObject {
    name: string;
    age: number;
    email: string;
    isActive: boolean;
}

type StringProperties = StringKeysOnly<MixedObject>; // { name: string; email: string; }
```


# 8. 高级类型

## 联合类型

### 基本联合类型
```typescript
// 基本联合类型定义
type StringOrNumber = string | number;
type BooleanOrNull = boolean | null;
type Primitive = string | number | boolean | null | undefined;

// 使用联合类型
let value: StringOrNumber = "hello";
value = 42; // 也可以是数字

// 函数参数使用联合类型
function padLeft(value: string, padding: string | number) {
    if (typeof padding === "number") {
        return " ".repeat(padding) + value;
    }
    return padding + value;
}

console.log(padLeft("Hello world", 4));        // "    Hello world"
console.log(padLeft("Hello world", ">>> "));   // ">>> Hello world"
```

### 联合类型与对象
```typescript
// 对象联合类型
interface Bird {
    type: "bird";
    flyingSpeed: number;
}

interface Horse {
    type: "horse";
    runningSpeed: number;
}

interface Fish {
    type: "fish";
    swimmingSpeed: number;
}

type Animal = Bird | Horse | Fish;

// 使用联合类型对象
function moveAnimal(animal: Animal) {
    switch (animal.type) {
        case "bird":
            console.log(`Flying at ${animal.flyingSpeed} km/h`);
            break;
        case "horse":
            console.log(`Running at ${animal.runningSpeed} km/h`);
            break;
        case "fish":
            console.log(`Swimming at ${animal.swimmingSpeed} km/h`);
            break;
        default:
            // 穷尽检查
            const _exhaustive: never = animal;
            return _exhaustive;
    }
}

let bird: Animal = {
    type: "bird",
    flyingSpeed: 100
};

moveAnimal(bird);
```

### 联合类型与数组
```typescript
// 联合类型数组
type MixedArray = (string | number | boolean)[];

let mixedData: MixedArray = ["hello", 42, true, "world", 100];

// 处理联合类型数组元素
function processMixedArray(items: MixedArray): void {
    items.forEach(item => {
        if (typeof item === "string") {
            console.log(`String: ${item.toUpperCase()}`);
        } else if (typeof item === "number") {
            console.log(`Number: ${item * 2}`);
        } else {
            console.log(`Boolean: ${item ? "Yes" : "No"}`);
        }
    });
}

processMixedArray(mixedData);
```

### 联合类型的类型收窄
```typescript
// 联合类型收窄
type Admin = {
    name: string;
    privileges: string[];
};

type Employee = {
    name: string;
    startDate: Date;
};

type UnknownEmployee = Employee | Admin;

function printEmployeeInformation(emp: UnknownEmployee) {
    console.log("Name: " + emp.name);
    
    // 类型收窄 - 使用 in 操作符
    if ("privileges" in emp) {
        console.log("Privileges: " + emp.privileges);
    }
    
    if ("startDate" in emp) {
        console.log("Start Date: " + emp.startDate);
    }
    
    // 类型收窄 - 使用 instanceof
    if (emp instanceof Date) {
        // 这个检查不会工作，因为 emp 不是 Date
    }
}

// 联合类型与可选属性
interface Car {
    engine: string;
    wheels?: number;
}

interface Boat {
    engine: string;
    hasSail: boolean;
}

type Vehicle = Car | Boat;

function checkVehicle(vehicle: Vehicle) {
    // 可选属性检查
    if ("wheels" in vehicle) {
        console.log(`Car with ${vehicle.wheels} wheels`);
    }
    
    if ("hasSail" in vehicle) {
        console.log(`Boat with sail: ${vehicle.hasSail}`);
    }
}
```

## 交叉类型

### 基本交叉类型
```typescript
// 基本交叉类型
interface Identifiable {
    id: string;
}

interface Timestamped {
    createdAt: Date;
    updatedAt: Date;
}

type Model = Identifiable & Timestamped;

let model: Model = {
    id: "123",
    createdAt: new Date(),
    updatedAt: new Date()
};

// 交叉类型合并属性
interface Person {
    name: string;
    age: number;
}

interface Employee {
    employeeId: string;
    department: string;
}

interface Manager {
    teamSize: number;
    reports: string[];
}

type ManagerEmployee = Person & Employee & Manager;

let manager: ManagerEmployee = {
    name: "Alice",
    age: 35,
    employeeId: "E123",
    department: "Engineering",
    teamSize: 10,
    reports: ["Bob", "Charlie"]
};
```

### 交叉类型与函数
```typescript
// 交叉类型与函数类型
type Callable = {
    (x: number): number;
    description: string;
};

let double: Callable = Object.assign(
    (x: number) => x * 2,
    { description: "Doubles the input" }
);

console.log(double(5)); // 10
console.log(double.description); // "Doubles the input"

// 交叉类型与方法
interface Flyable {
    fly(): void;
}

interface Swimmable {
    swim(): void;
}

interface Duck extends Flyable, Swimmable {
    quack(): void;
}

// 等价于使用交叉类型
type DuckType = Flyable & Swimmable & {
    quack(): void;
};
```

### 交叉类型冲突处理
```typescript
// 交叉类型中的类型冲突
interface A {
    prop: string;
}

interface B {
    prop: number;
}

// type C = A & B; // prop 的类型变为 never
// let c: C = { prop: "hello" }; // 错误！
// let c2: C = { prop: 42 }; // 错误！

// 解决冲突 - 使用字面量类型
interface A2 {
    name: string;
    age: number;
}

interface B2 {
    name: "specific"; // 字面量类型
    email: string;
}

type C2 = A2 & B2;

let c2: C2 = {
    name: "specific", // 必须是 "specific"
    age: 30,
    email: "test@example.com"
};

// 函数交叉类型
type AddFunction = (a: number, b: number) => number;
type MultiplyFunction = (a: number, b: number) => number;

type MathFunction = AddFunction & MultiplyFunction & {
    description: string;
};

let mathFunc: MathFunction = Object.assign(
    (a: number, b: number) => a + b,
    { description: "Mathematical operations" }
);

mathFunc.description = "Addition function";
```

## 类型保护

### typeof 类型保护
```typescript
// typeof 类型保护
function isString(test: any): test is string {
    return typeof test === "string";
}

function isNumber(test: any): test is number {
    return typeof test === "number";
}

function example(x: string | number | boolean) {
    if (typeof x === "string") {
        // x 在这里是 string 类型
        console.log(x.charAt(0));
    } else if (typeof x === "number") {
        // x 在这里是 number 类型
        console.log(x.toFixed(2));
    } else {
        // x 在这里是 boolean 类型
        console.log(x ? "true" : "false");
    }
}

// 实际应用
function formatValue(value: string | number): string {
    if (typeof value === "string") {
        return value.toUpperCase();
    } else {
        return value.toFixed(2);
    }
}

console.log(formatValue("hello")); // "HELLO"
console.log(formatValue(42.567)); // "42.57"
```

### instanceof 类型保护
```typescript
// instanceof 类型保护
class Dog {
    breed: string;
    constructor(breed: string) {
        this.breed = breed;
    }
    bark() {
        console.log("Woof!");
    }
}

class Cat {
    color: string;
    constructor(color: string) {
        this.color = color;
    }
    meow() {
        console.log("Meow!");
    }
}

function handlePet(pet: Dog | Cat) {
    if (pet instanceof Dog) {
        // pet 在这里是 Dog 类型
        console.log(`Dog breed: ${pet.breed}`);
        pet.bark();
    } else {
        // pet 在这里是 Cat 类型
        console.log(`Cat color: ${pet.color}`);
        pet.meow();
    }
}

let dog = new Dog("Golden Retriever");
let cat = new Cat("Orange");

handlePet(dog);
handlePet(cat);
```

### in 操作符类型保护
```typescript
// in 操作符类型保护
interface AdminUser {
    name: string;
    privileges: string[];
}

interface RegularUser {
    name: string;
    email: string;
}

type User = AdminUser | RegularUser;

function printUserInfo(user: User) {
    console.log(`Name: ${user.name}`);
    
    if ("privileges" in user) {
        // user 在这里是 AdminUser 类型
        console.log(`Privileges: ${user.privileges.join(", ")}`);
    }
    
    if ("email" in user) {
        // user 在这里是 RegularUser 类型
        console.log(`Email: ${user.email}`);
    }
}

let admin: User = {
    name: "Alice",
    privileges: ["read", "write", "delete"]
};

let regular: User = {
    name: "Bob",
    email: "bob@example.com"
};

printUserInfo(admin);
printUserInfo(regular);
```

## 类型谓词

### 基本类型谓词
```typescript
// 基本类型谓词
function isString(value: any): value is string {
    return typeof value === "string";
}

function isNumber(value: any): value is number {
    return typeof value === "number";
}

function isBoolean(value: any): value is boolean {
    return typeof value === "boolean";
}

// 使用类型谓词
function processValue(value: any) {
    if (isString(value)) {
        // value 在这里是 string 类型
        console.log(value.toUpperCase());
    } else if (isNumber(value)) {
        // value 在这里是 number 类型
        console.log(value.toFixed(2));
    } else if (isBoolean(value)) {
        // value 在这里是 boolean 类型
        console.log(value ? "Yes" : "No");
    }
}

processValue("hello"); // "HELLO"
processValue(42.567);  // "42.57"
processValue(true);    // "Yes"
```

### 复杂类型谓词
```typescript
// 复杂类型谓词
interface Circle {
    kind: "circle";
    radius: number;
}

interface Square {
    kind: "square";
    sideLength: number;
}

interface Triangle {
    kind: "triangle";
    base: number;
    height: number;
}

type Shape = Circle | Square | Triangle;

function isCircle(shape: Shape): shape is Circle {
    return shape.kind === "circle";
}

function isSquare(shape: Shape): shape is Square {
    return shape.kind === "square";
}

function isTriangle(shape: Shape): shape is Triangle {
    return shape.kind === "triangle";
}

// 使用复杂类型谓词
function calculateArea(shape: Shape): number {
    if (isCircle(shape)) {
        // shape 在这里是 Circle 类型
        return Math.PI * shape.radius * shape.radius;
    } else if (isSquare(shape)) {
        // shape 在这里是 Square 类型
        return shape.sideLength * shape.sideLength;
    } else {
        // shape 在这里是 Triangle 类型
        return 0.5 * shape.base * shape.height;
    }
}

let circle: Shape = { kind: "circle", radius: 5 };
let square: Shape = { kind: "square", sideLength: 4 };

console.log(calculateArea(circle)); // 78.539...
console.log(calculateArea(square)); // 16
```

### 数组类型谓词
```typescript
// 数组类型谓词
function isStringArray(arr: any[]): arr is string[] {
    return arr.every(item => typeof item === "string");
}

function isNumberArray(arr: any[]): arr is number[] {
    return arr.every(item => typeof item === "number");
}

function processArray(items: any[]) {
    if (isStringArray(items)) {
        // items 在这里是 string[] 类型
        items.forEach(str => console.log(str.toUpperCase()));
    } else if (isNumberArray(items)) {
        // items 在这里是 number[] 类型
        items.forEach(num => console.log(num * 2));
    } else {
        // items 在这里是 any[] 类型
        console.log("Mixed array");
    }
}

processArray(["hello", "world"]);     // "HELLO", "WORLD"
processArray([1, 2, 3]);             // 2, 4, 6
processArray(["hello", 42, true]);    // "Mixed array"
```

### 自定义类型谓词库
```typescript
// 自定义类型谓词库
class TypeGuards {
    static isString(value: any): value is string {
        return typeof value === "string";
    }
    
    static isNumber(value: any): value is number {
        return typeof value === "number";
    }
    
    static isArray<T>(value: any): value is T[] {
        return Array.isArray(value);
    }
    
    static isObject(value: any): value is object {
        return typeof value === "object" && value !== null && !Array.isArray(value);
    }
    
    static hasProperty<T extends object, K extends string>(
        obj: T,
        key: K
    ): obj is T & Record<K, any> {
        return key in obj;
    }
    
    static isDefined<T>(value: T | null | undefined): value is T {
        return value !== null && value !== undefined;
    }
}

// 使用自定义类型谓词
function processData(data: any) {
    if (TypeGuards.isString(data)) {
        console.log(data.toUpperCase());
    } else if (TypeGuards.isNumber(data)) {
        console.log(data.toFixed(2));
    } else if (TypeGuards.isArray(data)) {
        console.log(`Array with ${data.length} items`);
    } else if (TypeGuards.isObject(data)) {
        console.log("Object with keys:", Object.keys(data));
    } else {
        console.log("Undefined or null value");
    }
}
```

## 类型断言

### 基本类型断言
```typescript
// 基本类型断言语法
let someValue: any = "this is a string";

// 方式一：尖括号语法
let strLength1: number = (<string>someValue).length;

// 方式二：as 语法（推荐）
let strLength2: number = (someValue as string).length;

console.log(strLength1); // 16
console.log(strLength2); // 16

// 在 JSX 中只能使用 as 语法
// let strLength3: number = (<string>someValue).length; // 错误在 .tsx 文件中
```

### 复杂类型断言
```typescript
// 复杂类型断言
interface Person {
    name: string;
    age: number;
}

interface Employee extends Person {
    employeeId: string;
    department: string;
}

let personData: any = {
    name: "Alice",
    age: 30,
    employeeId: "E123",
    department: "Engineering"
};

// 断言为更具体的类型
let employee = personData as Employee;
console.log(employee.employeeId); // "E123"

// 双重断言
let value: any = "hello";
let numValue = value as unknown as number; // 先断言为 unknown，再断言为 number
// 注意：双重断言要谨慎使用
```

### 非空断言操作符
```typescript
// 非空断言操作符 (!)
function fixedLength(str: string | null): number {
    // 告诉 TypeScript str 不会是 null
    return str!.length;
}

let str: string | null = "hello";
console.log(fixedLength(str)); // 5

// 在严格模式下的应用
class UserComponent {
    user!: User; // 非空断言 - 告诉 TypeScript 这个属性会在使用前被初始化
    
    constructor() {
        this.initializeUser();
    }
    
    private initializeUser() {
        this.user = new User("1", "Alice");
    }
    
    getName(): string {
        return this.user.name; // 不需要额外检查
    }
}
```

### 类型断言的实际应用
```typescript
// 类型断言的实际应用场景
// 1. DOM 操作
let element = document.getElementById("myElement") as HTMLDivElement;
element.style.color = "red";

// 2. JSON 解析
let jsonData: any = JSON.parse('{"name": "Alice", "age": 30}');
let user = jsonData as User;

// 3. 第三方库集成
declare const $: any;
let jQueryElement = $("#myId") as JQuery;

// 4. 事件处理
function handleClick(event: Event) {
    let mouseEvent = event as MouseEvent;
    console.log(`Clicked at (${mouseEvent.clientX}, ${mouseEvent.clientY})`);
}

// 5. 数组类型转换
let mixedArray: any[] = ["hello", 42, true];
let stringArray = mixedArray as string[];
// 注意：这种转换在运行时可能不安全
```

## 类型守卫

### 自定义类型守卫
```typescript
// 自定义类型守卫函数
function isUser(obj: any): obj is User {
    return obj && typeof obj.name === "string" && typeof obj.age === "number";
}

function isEmployee(obj: any): obj is Employee {
    return isUser(obj) && typeof obj.employeeId === "string" && typeof obj.department === "string";
}

// 使用自定义类型守卫
function processObject(obj: any) {
    if (isUser(obj)) {
        // obj 在这里是 User 类型
        console.log(`User: ${obj.name}, Age: ${obj.age}`);
    }
    
    if (isEmployee(obj)) {
        // obj 在这里是 Employee 类型
        console.log(`Employee ID: ${obj.employeeId}, Department: ${obj.department}`);
    }
}

let userData = {
    name: "Alice",
    age: 30,
    employeeId: "E123",
    department: "Engineering"
};

processObject(userData);
```

### 类型守卫与联合类型
```typescript
// 类型守卫与联合类型结合
type ApiResponse<T> = 
    | { success: true; data: T }
    | { success: false; error: string };

function handleResponse<T>(response: ApiResponse<T>): void {
    if (response.success) {
        // response 在这里是 { success: true; data: T }
        console.log("Data:", response.data);
    } else {
        // response 在这里是 { success: false; error: string }
        console.error("Error:", response.error);
    }
}

let successResponse: ApiResponse<User> = {
    success: true,
     new User("1", "Alice")
};

let errorResponse: ApiResponse<User> = {
    success: false,
    error: "User not found"
};

handleResponse(successResponse);
handleResponse(errorResponse);
```

### 类型守卫工厂函数
```typescript
// 类型守卫工厂函数
function createTypeGuard<T>(
    validator: (obj: any) => boolean
): (obj: any) => obj is T {
    return (obj: any): obj is T => validator(obj);
}

// 使用类型守卫工厂
const isStringGuard = createTypeGuard<string>(
    (obj: any) => typeof obj === "string"
);

const isNumberGuard = createTypeGuard<number>(
    (obj: any) => typeof obj === "number"
);

function processData2(value: any) {
    if (isStringGuard(value)) {
        console.log(value.toUpperCase());
    } else if (isNumberGuard(value)) {
        console.log(value.toFixed(2));
    }
}

// 更复杂的类型守卫工厂
function hasProperties<T extends Record<string, any>>(
    ...requiredProps: (keyof T)[]
): (obj: any) => obj is T {
    return (obj: any): obj is T => {
        if (!obj || typeof obj !== "object") return false;
        return requiredProps.every(prop => prop in obj);
    };
}

const hasNameAndAge = hasProperties<User>("name", "age");

let obj: any = { name: "Alice", age: 30 };
if (hasNameAndAge(obj)) {
    console.log(`Name: ${obj.name}, Age: ${obj.age}`);
}
```

### 类型守卫与泛型
```typescript
// 泛型类型守卫
function isArrayOf<T>(guard: (item: any) => item is T): (arr: any) => arr is T[] {
    return (arr: any): arr is T[] => {
        return Array.isArray(arr) && arr.every(guard);
    };
}

// 创建具体的数组类型守卫
const isStringArrayGuard = isArrayOf<string>(
    (item: any): item is string => typeof item === "string"
);

const isNumberArrayGuard = isArrayOf<number>(
    (item: any): item is number => typeof item === "number"
);

// 使用泛型类型守卫
function processArray2(data: any) {
    if (isStringArrayGuard(data)) {
        console.log("String array:", data.map(s => s.toUpperCase()));
    } else if (isNumberArrayGuard(data)) {
        console.log("Number array:", data.map(n => n * 2));
    } else {
        console.log("Not a recognized array type");
    }
}

processArray2(["hello", "world"]); // String array: ["HELLO", "WORLD"]
processArray2([1, 2, 3]);          // Number array: [2, 4, 6]
```

## 辨别联合类型

### 基本辨别联合
```typescript
// 基本辨别联合类型
interface LoadingState {
    type: "loading";
}

interface SuccessState<T> {
    type: "success";
    data: T;
}

interface ErrorState {
    type: "error";
    error: string;
}

type AsyncState<T> = LoadingState | SuccessState<T> | ErrorState;

// 使用辨别联合
function renderState<T>(state: AsyncState<T>): string {
    switch (state.type) {
        case "loading":
            return "Loading...";
        case "success":
            return `Success: ${JSON.stringify(state.data)}`;
        case "error":
            return `Error: ${state.error}`;
        default:
            // 穷尽检查
            const _exhaustive: never = state;
            return _exhaustive;
    }
}

let loading: AsyncState<User> = { type: "loading" };
let success: AsyncState<User> = { type: "success", data: new User("1", "Alice") };
let error: AsyncState<User> = { type: "error", error: "Network error" };

console.log(renderState(loading));  // "Loading..."
console.log(renderState(success));  // "Success: {"id":"1","name":"Alice"}"
console.log(renderState(error));    // "Error: Network error"
```

### 复杂辨别联合
```typescript
// 复杂辨别联合类型
type NetworkRequest =
    | { type: "GET"; url: string; headers?: Record<string, string> }
    | { type: "POST"; url: string; body: any; headers?: Record<string, string> }
    | { type: "PUT"; url: string; body: any; headers?: Record<string, string> }
    | { type: "DELETE"; url: string; headers?: Record<string, string> };

// 处理复杂辨别联合
function processRequest(request: NetworkRequest): void {
    switch (request.type) {
        case "GET":
            console.log(`GET request to ${request.url}`);
            break;
        case "POST":
            console.log(`POST request to ${request.url} with body:`, request.body);
            break;
        case "PUT":
            console.log(`PUT request to ${request.url} with body:`, request.body);
            break;
        case "DELETE":
            console.log(`DELETE request to ${request.url}`);
            break;
        default:
            // 穷尽检查确保处理所有情况
            const _exhaustive: never = request;
            throw new Error(`Unhandled request type: ${_exhaustive}`);
    }
}

let getRequest: NetworkRequest = {
    type: "GET",
    url: "/api/users"
};

let postRequest: NetworkRequest = {
    type: "POST",
    url: "/api/users",
    body: { name: "Alice", age: 30 }
};

processRequest(getRequest);
processRequest(postRequest);
```

### 辨别联合与状态机
```typescript
// 辨别联合实现状态机
type PlayerState =
    | { type: "idle" }
    | { type: "playing"; song: string; progress: number }
    | { type: "paused"; song: string; progress: number }
    | { type: "stopped"; lastSong: string }
    | { type: "error"; message: string };

class MusicPlayer {
    private state: PlayerState = { type: "idle" };
    
    play(song: string): void {
        switch (this.state.type) {
            case "idle":
            case "stopped":
            case "error":
                this.state = { type: "playing", song, progress: 0 };
                console.log(`Now playing: ${song}`);
                break;
            case "paused":
                this.state = { type: "playing", song: this.state.song, progress: this.state.progress };
                console.log(`Resuming: ${this.state.song}`);
                break;
            case "playing":
                console.log(`Already playing: ${this.state.song}`);
                break;
        }
    }
    
    pause(): void {
        if (this.state.type === "playing") {
            this.state = { type: "paused", song: this.state.song, progress: this.state.progress };
            console.log(`Paused: ${this.state.song}`);
        }
    }
    
    stop(): void {
        if (this.state.type === "playing" || this.state.type === "paused") {
            this.state = { type: "stopped", lastSong: this.state.song };
            console.log("Playback stopped");
        }
    }
    
    getStatus(): string {
        switch (this.state.type) {
            case "idle":
                return "Player is idle";
            case "playing":
                return `Playing: ${this.state.song} (${this.state.progress}%)`;
            case "paused":
                return `Paused: ${this.state.song} (${this.state.progress}%)`;
            case "stopped":
                return `Stopped. Last played: ${this.state.lastSong}`;
            case "error":
                return `Error: ${this.state.message}`;
        }
    }
}

let player = new MusicPlayer();
console.log(player.getStatus()); // "Player is idle"
player.play("Song 1");
console.log(player.getStatus()); // "Playing: Song 1 (0%)"
player.pause();
console.log(player.getStatus()); // "Paused: Song 1 (0%)"
```

## 索引类型

### 基本索引类型
```typescript
// 基本索引类型操作
interface Person {
    name: string;
    age: number;
    email: string;
}

// keyof 操作符
type PersonKeys = keyof Person; // "name" | "age" | "email"

// 索引访问类型
type PersonName = Person["name"]; // string
type PersonAge = Person["age"];   // number
type PersonEmail = Person["email"]; // string

// 联合索引访问
type PersonNameOrAge = Person["name" | "age"]; // string | number

// 使用索引类型
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
    return obj[key];
}

let person: Person = {
    name: "Alice",
    age: 30,
    email: "alice@example.com"
};

let name = getProperty(person, "name"); // string
let age = getProperty(person, "age");   // number
// let invalid = getProperty(person, "invalid"); // 编译错误
```

### 索引类型与泛型
```typescript
// 索引类型与泛型结合
function pluck<T, K extends keyof T>(array: T[], key: K): T[K][] {
    return array.map(x => x[key]);
}

let persons = [
    { name: "Alice", age: 30, email: "alice@example.com" },
    { name: "Bob", age: 25, email: "bob@example.com" },
    { name: "Charlie", age: 35, email: "charlie@example.com" }
];

let names = pluck(persons, "name"); // string[]
let ages = pluck(persons, "age");   // number[]
let emails = pluck(persons, "email"); // string[]

// 多个属性的 pluck
function pluckMultiple<T, K extends keyof T>(array: T[], ...keys: K[]): { [P in K]: T[P] }[] {
    return array.map(item => {
        const result = {} as { [P in K]: T[P] };
        keys.forEach(key => {
            result[key] = item[key];
        });
        return result;
    });
}

let nameAgePairs = pluckMultiple(persons, "name", "age");
// { name: string; age: number; }[]
```

### 索引类型约束
```typescript
// 索引类型约束
function getValues<T, K extends keyof T>(obj: T, keys: K[]): T[K][] {
    return keys.map(key => obj[key]);
}

let user = {
    id: "123",
    name: "Alice",
    age: 30,
    email: "alice@example.com",
    isActive: true
};

let values = getValues(user, ["name", "age", "email"]);
// (string | number)[]

// 类型安全的对象映射
function mapObject<T extends Record<string, any>, U>(
    obj: T,
    mapper: <K extends keyof T>(value: T[K], key: K) => U
): { [K in keyof T]: U } {
    const result = {} as { [K in keyof T]: U };
    for (const key in obj) {
        result[key] = mapper(obj[key], key);
    }
    return result;
}

let numbers = { a: 1, b: 2, c: 3 };
let doubled = mapObject(numbers, (value, key) => value * 2);
// { a: number, b: number, c: number }
```

### 索引签名与索引类型
```typescript
// 索引签名与索引类型
interface Dictionary<T> {
    [key: string]: T;
}

type DictionaryKeys<T> = keyof Dictionary<T>; // string | number

// 从索引签名提取值类型
type DictionaryValue<T> = T extends Dictionary<infer U> ? U : never;

type StringDict = Dictionary<string>;
type StringDictValue = DictionaryValue<StringDict>; // string

// 实际应用：类型安全的字典操作
function getValue<T>(dict: Dictionary<T>, key: string): T | undefined {
    return dict[key];
}

function setValue<T>(dict: Dictionary<T>, key: string, value: T): void {
    dict[key] = value;
}

let stringDict: Dictionary<string> = {
    "name": "Alice",
    "city": "New York"
};

console.log(getValue(stringDict, "name")); // "Alice"
setValue(stringDict, "age", "30"); // 错误！类型不匹配
```

## 映射类型

### 基本映射类型
```typescript
// 基本映射类型
type Readonly<T> = {
    readonly [P in keyof T]: T[P];
};

type Partial<T> = {
    [P in keyof T]?: T[P];
};

type Required<T> = {
    [P in keyof T]-?: T[P];
};

type Pick<T, K extends keyof T> = {
    [P in K]: T[P];
};

type Omit<T, K extends keyof T> = Pick<T, Exclude<keyof T, K>>;

// 使用内置映射类型
interface User {
    id: string;
    name: string;
    age: number;
    email?: string;
}

type ReadonlyUser = Readonly<User>;
type PartialUser = Partial<User>;
type RequiredUser = Required<User>;
type UserBasicInfo = Pick<User, "id" | "name">;
type UserWithoutEmail = Omit<User, "email">;

let readonlyUser: ReadonlyUser = {
    id: "123",
    name: "Alice",
    age: 30,
    email: "alice@example.com"
};

// readonlyUser.name = "Bob"; // 错误！只读属性

let partialUser: PartialUser = {
    name: "Bob" // 只需要部分属性
};

let requiredUser: RequiredUser = {
    id: "456",
    name: "Charlie",
    age: 25,
    email: "charlie@example.com" // email 变为必需
};
```

### 映射类型修饰符
```typescript
// 映射类型修饰符
// +? 可选，-? 必需，+readonly 只读，-readonly 可写

type Mutable<T> = {
    -readonly [P in keyof T]: T[P];
};

type Complete<T> = {
    [P in keyof T]-?: T[P];
};

interface OptionalUser {
    name?: string;
    age?: number;
    email?: string;
}

type CompleteUser = Complete<OptionalUser>;

let completeUser: CompleteUser = {
    name: "Alice",
    age: 30,
    email: "alice@example.com" // 所有属性都必需
};

// 移除只读修饰符
interface ReadOnlyPoint {
    readonly x: number;
    readonly y: number;
}

type MutablePoint = Mutable<ReadOnlyPoint>;

let mutablePoint: MutablePoint = { x: 10, y: 20 };
mutablePoint.x = 15; // 正确！现在是可变的
```

### 自定义映射类型
```typescript
// 自定义映射类型
type Nullable<T> = {
    [P in keyof T]: T[P] | null;
};

type Stringify<T> = {
    [P in keyof T]: string;
};

type DeepPartial<T> = {
    [P in keyof T]?: T[P] extends object ? DeepPartial<T[P]> : T[P];
};

// 使用自定义映射类型
interface Address {
    street: string;
    city: string;
    zipCode: number;
}

interface UserWithAddress {
    name: string;
    age: number;
    address: Address;
}

type NullableUser = Nullable<UserWithAddress>;
type StringifiedUser = Stringify<UserWithAddress>;
type DeepPartialUser = DeepPartial<UserWithAddress>;

let nullableUser: NullableUser = {
    name: "Alice",
    age: null,
    address: null
};

let stringifiedUser: StringifiedUser = {
    name: "Alice",
    age: "30",
    address: "[object Object]" // 所有属性都变成字符串
};

let deepPartialUser: DeepPartialUser = {
    name: "Bob",
    address: {
        street: "123 Main St"
        // city 和 zipCode 是可选的
    }
};
```

### 条件映射类型
```typescript
// 条件映射类型
type FunctionPropertyNames<T> = {
    [K in keyof T]: T[K] extends Function ? K : never
}[keyof T];

type FunctionProperties<T> = Pick<T, FunctionPropertyNames<T>>;

type NonFunctionPropertyNames<T> = {
    [K in keyof T]: T[K] extends Function ? never : K
}[keyof T];

type NonFunctionProperties<T> = Pick<T, NonFunctionPropertyNames<T>>;

interface SampleObject {
    name: string;
    age: number;
    greet(): string;
    calculate(x: number, y: number): number;
}

type FuncNames = FunctionPropertyNames<SampleObject>; // "greet" | "calculate"
type FuncProps = FunctionProperties<SampleObject>;     // { greet(): string; calculate(x: number, y: number): number; }
type NonFuncNames = NonFunctionPropertyNames<SampleObject>; // "name" | "age"
type NonFuncProps = NonFunctionProperties<SampleObject>;   // { name: string; age: number; }
```

## 条件类型

### 基本条件类型
```typescript
// 基本条件类型语法：T extends U ? X : Y
type NonNullable<T> = T extends null | undefined ? never : T;

type A = NonNullable<string | null>;        // string
type B = NonNullable<number | undefined>;   // number
type C = NonNullable<string | number>;      // string | number
type D = NonNullable<null | undefined>;     // never

// 条件类型的实际应用
type MessageOf<T> = T extends { message: unknown } ? T['message'] : never;

interface Email {
    message: string;
}

interface SMS {
    message: string;
    phoneNumber: string;
}

interface VoiceCall {
    duration: number;
}

type EmailMessage = MessageOf<Email>;  // string
type SMSMessage = MessageOf<SMS>;      // string
type VoiceMessage = MessageOf<VoiceCall>; // never
```

### 分布式条件类型
```typescript
// 分布式条件类型
type ToArray<T> = T extends any ? T[] : never;

type A1 = ToArray<string>;              // string[]
type A2 = ToArray<string | number>;     // string[] | number[]
type A3 = ToArray<string | number | boolean>; // string[] | number[] | boolean[]

// 与泛型函数结合
type Flatten<T> = T extends any[] ? T[number] : T;

type B1 = Flatten<string[]>;            // string
type B2 = Flatten<number[][]>;          // number[]
type B3 = Flatten<string>;              // string

// 实用工具类型
type StringKeys<T> = {
    [K in keyof T]: T[K] extends string ? K : never
}[keyof T];

interface Person2 {
    name: string;
    age: number;
    email: string;
    isActive: boolean;
}

type StringKey = StringKeys<Person2>; // "name" | "email"
```

### 条件类型与类型推断
```typescript
// 条件类型与类型推断
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : any;

type C1 = ReturnType<() => string>;           // string
type C2 = ReturnType<(x: number) => number[]>; // number[]
type C3 = ReturnType<string>;                 // any

// 获取函数参数类型
type Parameters<T> = T extends (...args: infer P) => any ? P : never;

type D1 = Parameters<(name: string, age: number) => void>; // [string, number]
type D2 = Parameters<() => boolean>;                       // []
type D3 = Parameters<string>;                              // never

// 获取构造函数参数
type ConstructorParameters<T> = T extends new (...args: infer P) => any ? P : never;

type E1 = ConstructorParameters<typeof Person>; // [string] (假设构造函数参数)
```

### 复杂条件类型
```typescript
// 复杂条件类型示例
type DeepReadonly<T> = T extends any[] 
    ? DeepReadonlyArray<T[number]> 
    : T extends object 
    ? DeepReadonlyObject<T> 
    : T;

interface DeepReadonlyArray<T> extends ReadonlyArray<DeepReadonly<T>> {}

type DeepReadonlyObject<T> = {
    readonly [P in keyof T]: DeepReadonly<T[P]>;
};

// 使用深度只读
interface NestedObject {
    name: string;
    details: {
        age: number;
        hobbies: string[];
        address: {
            street: string;
            city: string;
        };
    };
}

type ReadonlyNested = DeepReadonly<NestedObject>;

let readonlyObj: ReadonlyNested = {
    name: "Alice",
    details: {
        age: 30,
        hobbies: ["reading", "swimming"],
        address: {
            street: "123 Main St",
            city: "New York"
        }
    }
};

// readonlyObj.name = "Bob"; // 错误！
// readonlyObj.details.age = 31; // 错误！
// readonlyObj.details.hobbies[0] = "coding"; // 错误！
```

## infer 关键字

### 基本 infer 用法
```typescript
// 基本 infer 用法
type GetReturnType<T> = T extends (...args: any[]) => infer R ? R : never;

type A = GetReturnType<() => string>;        // string
type B = GetReturnType<(x: number) => number[]>; // number[]
type C = GetReturnType<string>;              // never

// 获取函数参数类型
type GetParameters<T> = T extends (...args: infer P) => any ? P : never;

type D = GetParameters<(name: string, age: number) => void>; // [string, number]
type E = GetParameters<() => boolean>;                       // []

// 获取数组元素类型
type GetElementType<T> = T extends (infer U)[] ? U : T;

type F = GetElementType<number[]>;    // number
type G = GetElementType<string[]>;    // string
type H = GetElementType<boolean>;     // boolean
```

### infer 与泛型约束
```typescript
// infer 与泛型约束结合
type GetPromiseType<T> = T extends Promise<infer U> ? U : T;

type A1 = GetPromiseType<Promise<string>>;        // string
type B1 = GetPromiseType<Promise<number[]>>;      // number[]
type C1 = GetPromiseType<string>;                 // string

// 处理嵌套 Promise
type UnwrapPromise<T> = T extends Promise<infer U> ? UnwrapPromise<U> : T;

type D1 = UnwrapPromise<Promise<string>>;                    // string
type E1 = UnwrapPromise<Promise<Promise<number>>>;           // number
type F1 = UnwrapPromise<Promise<Promise<Promise<boolean>>>>; // boolean

// 获取对象属性类型
type GetPropType<T, K extends keyof T> = T extends { [P in K]: infer U } ? U : never;

interface User {
    name: string;
    age: number;
    email: string;
}

type UserNameType = GetPropType<User, "name">; // string
type UserAgeType = GetPropType<User, "age">;   // number
```

### infer 与条件类型组合
```typescript
// infer 与条件类型组合
type GetLast<T extends any[]> = T extends [...any[], infer U] ? U : never;

type A = GetLast<[1, 2, 3]>;        // 3
type B = GetLast<[string, number]>;  // number
type C = GetLast<[]>;               // never

// 获取数组第一个元素
type GetFirst<T extends any[]> = T extends [infer U, ...any[]] ? U : never;

type D = GetFirst<[1, 2, 3]>;       // 1
type E = GetFirst<[string, number]>; // string

// 获取数组长度
type GetLength<T extends any[]> = T extends { length: infer U } ? U : never;

type F = GetLength<[1, 2, 3]>;      // 3
type G = GetLength<[]>;             // 0

// 条件类型中的多个 infer
type Split<T extends string, U extends string> = 
    T extends `${infer L}${U}${infer R}` ? [L, R] : [T, ""];

type H = Split<"hello world", " ">;  // ["hello", "world"]
type I = Split<"hello", "-">;        // ["hello", ""]
```

### infer 的高级应用
```typescript
// infer 的高级应用
// 提取函数的 this 类型
type GetThisParameterType<T> = T extends (this: infer U, ...args: any[]) => any ? U : unknown;

class MyClass {
    value: number = 42;
    method() {
        return this.value;
    }
}

type ThisType = GetThisParameterType<MyClass['method']>; // MyClass

// 提取字符串字面量类型
type GetStringLength<T extends string> = T extends { length: infer U } ? U : never;

type Length = GetStringLength<"hello">; // 5

// 类型级别的字符串操作
type CapitalizeString<T extends string> = T extends `${infer First}${infer Rest}` 
    ? `${Uppercase<First>}${Rest}` 
    : T;

type Capitalized = CapitalizeString<"hello">; // "Hello"

// 提取联合类型的元素
type UnionToIntersection<U> = 
    (U extends any ? (k: U) => void : never) extends ((k: infer I) => void) ? I : never;

type A2 = UnionToIntersection<string | number>; // string & number (never)
type B2 = UnionToIntersection<{ a: string } | { b: number }>; // { a: string } & { b: number }
```

# 9. 模块系统

## 模块导出

### 基本导出语法
```typescript
// 命名导出 - 导出声明
export interface User {
    id: string;
    name: string;
    age: number;
}

export class UserService {
    getUser(id: string): User {
        return { id, name: "Default User", age: 0 };
    }
}

export const MAX_USERS = 1000;

export function validateUser(user: User): boolean {
    return user.name.length > 0 && user.age >= 0;
}

export type UserRole = "admin" | "user" | "guest";

// 导出时重命名
export { UserService as Service, validateUser as isValidUser };

// 导出值
export const config = {
    apiUrl: "https://api.example.com",
    timeout: 5000
};
```

### 导出列表
```typescript
// 先声明，后导出
interface Product {
    id: string;
    name: string;
    price: number;
}

class ProductManager {
    private products: Product[] = [];
    
    addProduct(product: Product): void {
        this.products.push(product);
    }
    
    getProducts(): Product[] {
        return this.products;
    }
}

const DEFAULT_CATEGORY = "general";

function formatPrice(price: number): string {
    return `$${price.toFixed(2)}`;
}

// 在文件末尾统一导出
export { 
    Product, 
    ProductManager, 
    DEFAULT_CATEGORY, 
    formatPrice,
    ProductManager as Manager  // 重命名导出
};
```

### 默认导出
```typescript
// 默认导出类
export default class DatabaseConnection {
    constructor(private connectionString: string) {}
    
    connect(): Promise<void> {
        // 连接逻辑
        return Promise.resolve();
    }
    
    disconnect(): Promise<void> {
        // 断开连接逻辑
        return Promise.resolve();
    }
}

// 默认导出函数
export default function calculateTotal(items: number[]): number {
    return items.reduce((sum, item) => sum + item, 0);
}

// 默认导出值
const DEFAULT_CONFIG = {
    host: "localhost",
    port: 3000,
    debug: false
};

export default DEFAULT_CONFIG;

// 默认导出接口（需要先声明）
interface AppConfig {
    host: string;
    port: number;
    debug: boolean;
}

export default interface AppConfig; // 错误！不能直接默认导出接口

// 正确方式
interface AppConfig2 {
    host: string;
    port: number;
    debug: boolean;
}

const AppConfigType: AppConfig2 = {
    host: "localhost",
    port: 3000,
    debug: false
};

export default AppConfigType;
```

### 导出类型
```typescript
// 导出类型（TypeScript 3.8+）
export type { User, UserRole } from "./user";
export type { Product } from "./product";

// 或者在导出时指定类型
interface ApiResponse<T> {
    success: boolean;
     T;
    message?: string;
}

export type { ApiResponse };

// 导出类型别名
type Status = "pending" | "approved" | "rejected";
export type { Status };

// 混合导出值和类型
export { 
    UserService,  // 值
    type User,    // 类型
    type UserRole // 类型
};
```

## 模块导入

### 基本导入语法
```typescript
// 导入所有命名导出
import * as UserModule from "./user";
const user: UserModule.User = { id: "1", name: "Alice", age: 30 };

// 导入特定命名导出
import { User, UserService, MAX_USERS, validateUser } from "./user";

// 导入时重命名
import { UserService as Service, validateUser as isValidUser } from "./user";

// 导入类型（TypeScript 3.8+）
import type { User, UserRole } from "./user";
import { type Product, ProductManager } from "./product";

// 混合导入
import DatabaseConnection, { 
    User, 
    UserService,
    type UserRole 
} from "./module";
```

### 导入默认导出
```typescript
// 导入默认导出
import DatabaseConnection from "./database";

// 导入默认导出和命名导出
import DatabaseConnection, { User, UserService } from "./module";

// 导入默认导出并重命名
import Connection from "./database";
import calcTotal from "./calculator";

// 导入默认导出为不同名称
import { default as DBConnection } from "./database";
```

### 动态导入类型
```typescript
// 动态导入的类型处理
async function loadModule() {
    const module = await import("./dynamic-module");
    // module 的类型是 Promise<typeof import("./dynamic-module")>
    
    return module;
}

// 使用动态导入
async function useDynamicModule() {
    const { User, UserService } = await import("./user");
    const user = new UserService();
    // ...
}

// 条件导入
async function conditionalImport(condition: boolean) {
    if (condition) {
        const { AdminService } = await import("./admin");
        return new AdminService();
    } else {
        const { UserService } = await import("./user");
        return new UserService();
    }
}
```

### 导入副作用
```typescript
// 仅导入副作用（不导入任何值）
import "./polyfills";
import "./styles.css";
import "@babel/polyfill";

// 实际应用示例
// polyfills.ts
console.log("Polyfills loaded");
// 注册全局变量或修改原型

// main.ts
import "./polyfills"; // 确保在使用前加载
import { App } from "./app";

const app = new App();
```

## 默认导出与导入

### 默认导出的特点
```typescript
// 默认导出的灵活性
// math.ts
export default function add(a: number, b: number): number {
    return a + b;
}

// 可以导入为任何名称
import myAddFunction from "./math";
import calculateSum from "./math";
import addNumbers from "./math";

// 默认导出类
// user-service.ts
export default class UserService {
    getUsers(): string[] {
        return ["Alice", "Bob", "Charlie"];
    }
}

// 导入默认导出的类
import UserService from "./user-service";
const service = new UserService();

// 默认导出对象
// config.ts
export default {
    apiUrl: "https://api.example.com",
    timeout: 5000,
    retries: 3
};

// 导入配置对象
import config from "./config";
console.log(config.apiUrl);
```

### 默认导出与命名导出的组合
```typescript
// 组合导出
// api.ts
export interface ApiResponse<T> {
    success: boolean;
     T;
}

export class ApiClient {
    // ...
}

// 默认导出
export default class DefaultApiClient extends ApiClient {
    // 默认实现
}

// utils.ts
export function formatDate(date: Date): string {
    return date.toISOString();
}

export function parseDate(dateString: string): Date {
    return new Date(dateString);
}

// 默认导出
const DateUtils = {
    formatDate,
    parseDate
};

export default DateUtils;

// 使用组合导出
// main.ts
import DefaultApiClient, { ApiClient, ApiResponse } from "./api";
import DateUtils, { formatDate, parseDate } from "./utils";

const client = new DefaultApiClient();
const formattedDate = DateUtils.formatDate(new Date());
```

### 默认导出的最佳实践
```typescript
// 推荐：每个文件只有一个默认导出
// logger.ts
export interface LogOptions {
    level: "debug" | "info" | "warn" | "error";
    timestamp: boolean;
}

export default class Logger {
    constructor(private options: LogOptions) {}
    
    log(message: string): void {
        if (this.options.timestamp) {
            console.log(`[${new Date().toISOString()}] ${message}`);
        } else {
            console.log(message);
        }
    }
}

// 不推荐：多个默认导出
// bad-example.ts
export default class Logger { /* ... */ }
export default function helper() { /* ... */ } // 错误！

// 推荐：明确的默认导出意图
// good-example.ts
class Logger { /* ... */ }

// 明确导出主要功能作为默认
export default Logger;

// 同时导出辅助功能作为命名导出
export { LogOptions } from "./logger";
```

## 重新导出

### 基本重新导出
```typescript
// 重新导出其他模块的内容
// utils/index.ts
export { formatDate, parseDate } from "./date-utils";
export { validateEmail, validatePhone } from "./validation";
export { Logger } from "./logger";

// 重新导出并重命名
export { 
    formatDate as format, 
    parseDate as parse 
} from "./date-utils";

// 重新导出默认导出
export { default as Logger } from "./logger";
export { default as Config } from "./config";

// 重新导出所有内容
export * from "./helpers";
export * as Validators from "./validation";
```

### 包装重新导出
```typescript
// 包装重新导出 - 添加额外功能
// enhanced-utils.ts
import { formatDate as originalFormatDate } from "./date-utils";
import { Logger as BaseLogger } from "./logger";

// 增强功能
export function formatDate(date: Date, includeTime: boolean = true): string {
    const baseFormat = originalFormatDate(date);
    if (includeTime) {
        return `${baseFormat} ${date.toLocaleTimeString()}`;
    }
    return baseFormat;
}

// 扩展类
export class Logger extends BaseLogger {
    logWithLevel(level: string, message: string): void {
        super.log(`[${level.toUpperCase()}] ${message}`);
    }
}

// 重新导出其他内容
export { parseDate } from "./date-utils";
export { validateEmail } from "./validation";
```

### 模块聚合
```typescript
// 模块聚合模式
// api/index.ts
// 重新导出所有 API 相关模块
export * from "./user-api";
export * from "./product-api";
export * from "./order-api";

// 重新导出类型
export type { User, Product, Order } from "./types";

// 重新导出默认导出
export { default as ApiClient } from "./api-client";

// 有条件地重新导出
import * as UserApi from "./user-api";

// 只在开发环境重新导出调试工具
if (process.env.NODE_ENV === "development") {
    export * from "./debug-api";
}

// 使用聚合模块
// main.ts
import { getUser, Product, ApiClient } from "./api";
import type { User, Order } from "./api";
```

### 重新导出的实际应用
```typescript
// 实际应用：创建库的入口点
// my-library/index.ts

// 核心功能
export { default as HttpClient } from "./http-client";
export { default as Database } from "./database";

// 工具函数
export * from "./utils/string-utils";
export * from "./utils/array-utils";
export * from "./utils/object-utils";

// 类型定义
export type { 
    HttpRequest, 
    HttpResponse,
    DatabaseConfig 
} from "./types";

// 错误类
export { 
    NetworkError, 
    DatabaseError,
    ValidationError 
} from "./errors";

// 配置
export { default as config } from "./config";

// 使用库
// app.ts
import { HttpClient, Database, config } from "my-library";
import type { HttpRequest, DatabaseConfig } from "my-library";
import { capitalize, chunk } from "my-library/utils/array-utils";
```

## 动态导入

### 基本动态导入
```typescript
// 基本动态导入
async function loadUserModule() {
    const userModule = await import("./user");
    
    // 访问导出的内容
    const { User, UserService } = userModule;
    const userService = new UserService();
    
    return userService;
}

// 动态导入的返回类型
async function getModuleInfo() {
    const module = await import("./math");
    
    // module 的类型是 Promise<typeof import("./math")>
    console.log(typeof module.add); // "function"
    console.log(typeof module.PI);  // "number"
}
```

### 条件动态导入
```typescript
// 条件动态导入
async function loadModuleByCondition(condition: string) {
    switch (condition) {
        case "user":
            const { UserService } = await import("./user");
            return new UserService();
            
        case "product":
            const { ProductManager } = await import("./product");
            return new ProductManager();
            
        case "admin":
            const { AdminService } = await import("./admin");
            return new AdminService();
            
        default:
            throw new Error("Unknown module");
    }
}

// 基于环境的动态导入
async function loadEnvironmentSpecificModule() {
    if (process.env.NODE_ENV === "development") {
        const { DebugService } = await import("./debug");
        return new DebugService();
    } else {
        const { ProductionService } = await import("./production");
        return new ProductionService();
    }
}
```

### 动态导入与错误处理
```typescript
// 动态导入的错误处理
async function safeImport(modulePath: string) {
    try {
        const module = await import(modulePath);
        return { success: true, module };
    } catch (error) {
        console.error(`Failed to import ${modulePath}:`, error);
        return { success: false, error };
    }
}

// 使用示例
async function useModule() {
    const result = await safeImport("./optional-module");
    
    if (result.success) {
        const { SomeClass } = result.module;
        const instance = new SomeClass();
        // 使用模块
    } else {
        // 处理加载失败的情况
        console.log("Using fallback implementation");
    }
}

// 重试机制
async function importWithRetry(modulePath: string, maxRetries: number = 3) {
    for (let i = 0; i < maxRetries; i++) {
        try {
            return await import(modulePath);
        } catch (error) {
            if (i === maxRetries - 1) throw error;
            console.log(`Retry ${i + 1} for ${modulePath}`);
            await new Promise(resolve => setTimeout(resolve, 1000));
        }
    }
}
```

### 动态导入与代码分割
```typescript
// 代码分割的实际应用
// 路由组件懒加载
class Router {
    private routes: Map<string, () => Promise<any>> = new Map();
    
    addRoute(path: string, loader: () => Promise<any>) {
        this.routes.set(path, loader);
    }
    
    async navigate(path: string) {
        const loader = this.routes.get(path);
        if (loader) {
            try {
                const module = await loader();
                const { default: Component } = module;
                // 渲染组件
                return new Component();
            } catch (error) {
                console.error("Failed to load route:", error);
            }
        }
    }
}

// 使用示例
const router = new Router();
router.addRoute("/users", () => import("./components/UserList"));
router.addRoute("/products", () => import("./components/ProductList"));

// 功能模块按需加载
class FeatureManager {
    private loadedFeatures: Map<string, any> = new Map();
    
    async loadFeature(name: string) {
        if (this.loadedFeatures.has(name)) {
            return this.loadedFeatures.get(name);
        }
        
        try {
            const module = await import(`./features/${name}`);
            this.loadedFeatures.set(name, module);
            return module;
        } catch (error) {
            throw new Error(`Failed to load feature ${name}: ${error}`);
        }
    }
    
    async useFeature(name: string) {
        const feature = await this.loadFeature(name);
        return feature.default || feature;
    }
}
```

## 模块解析策略

### 模块解析基础
```typescript
// 模块解析路径
// 相对导入
import { User } from "./models/user";
import { Logger } from "../utils/logger";
import { Config } from "../../config";

// 绝对导入
import { Database } from "database";
import { ApiClient } from "@services/api-client";
import lodash from "lodash";

// TypeScript 配置影响解析
// tsconfig.json
{
  "compilerOptions": {
    "baseUrl": "./src",
    "paths": {
      "@/*": ["*"],
      "@models/*": ["models/*"],
      "@services/*": ["services/*"],
      "@utils/*": ["utils/*"]
    }
  }
}

// 使用路径映射
import { User } from "@models/user";
import { Logger } from "@utils/logger";
import { ApiService } from "@services/api";
```

### 解析策略配置
```typescript
// 模块解析策略配置
// tsconfig.json
{
  "compilerOptions": {
    "moduleResolution": "node",  // 或 "classic"
    "baseUrl": "./src",
    "paths": {
      // 路径别名
      "@app/*": ["app/*"],
      "@components/*": ["components/*"],
      "@utils/*": ["utils/*"],
      "@types/*": ["types/*"],
      
      // 多个候选项
      "shared/*": ["../shared/*", "./src/shared/*"],
      
      // 具体文件映射
      "config": ["config/index"],
      "logger": ["utils/logger"]
    },
    
    // 模块后缀
    "moduleSuffixes": [".ios", ".android", ""],
    
    // 类型根目录
    "typeRoots": ["./node_modules/@types", "./src/types"],
    
    // 允许的模块类型
    "allowSyntheticDefaultImports": true,
    "esModuleInterop": true
  },
  
  // 包含和排除文件
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

### 自定义模块解析
```typescript
// 自定义模块解析示例
// webpack.config.js 中的 resolve 配置
module.exports = {
  resolve: {
    alias: {
      '@': path.resolve(__dirname, 'src'),
      'components': path.resolve(__dirname, 'src/components'),
      'utils': path.resolve(__dirname, 'src/utils'),
      'assets': path.resolve(__dirname, 'src/assets')
    },
    
    extensions: ['.ts', '.tsx', '.js', '.jsx', '.json'],
    
    modules: [
      path.resolve(__dirname, 'src'),
      'node_modules'
    ]
  }
};

// 使用自定义解析
import Button from 'components/Button';
import { formatDate } from 'utils/date';
import logo from 'assets/logo.png';
```

### 模块解析调试
```typescript
// 模块解析调试技巧
// 1. 使用 tsc --traceResolution 查看解析过程
// tsc --traceResolution --noEmit

// 2. 检查模块解析结果
// 在代码中添加类型检查
import type { User } from "./models/user"; // 仅导入类型

// 3. 使用模块声明文件
// types/modules.d.ts
declare module "my-custom-module" {
  export interface CustomConfig {
    apiUrl: string;
    timeout: number;
  }
  
  export function initialize(config: CustomConfig): void;
  export default function createInstance(): any;
}

// 4. 处理解析错误
try {
  // 动态导入用于处理解析错误
  const module = await import("some-module");
} catch (error) {
  if (error.code === "MODULE_NOT_FOUND") {
    console.log("Module not found, using fallback");
  }
}
```

## 命名空间

### 命名空间基础
```typescript
// 基本命名空间
namespace Validation {
    export interface StringValidator {
        isAcceptable(s: string): boolean;
    }
    
    const lettersRegexp = /^[A-Za-z]+$/;
    const numberRegexp = /^[0-9]+$/;
    
    export class LettersOnlyValidator implements StringValidator {
        isAcceptable(s: string) {
            return lettersRegexp.test(s);
        }
    }
    
    export class ZipCodeValidator implements StringValidator {
        isAcceptable(s: string) {
            return s.length === 5 && numberRegexp.test(s);
        }
    }
}

// 使用命名空间
let validators: { [s: string]: Validation.StringValidator; } = {};
validators["ZIP code"] = new Validation.ZipCodeValidator();
validators["Letters only"] = new Validation.LettersOnlyValidator();

// 测试每个验证器
let strings = ["Hello", "98052", "101"];
strings.forEach(s => {
    for (let name in validators) {
        console.log(`"${s}" - ${validators[name].isAcceptable(s) ? "matches" : "does not match"} ${name}`);
    }
});
```

### 命名空间分割
```typescript
// 将命名空间分割到多个文件
// Validation.ts
namespace Validation {
    export interface StringValidator {
        isAcceptable(s: string): boolean;
    }
}

// LettersOnlyValidator.ts
/// <reference path="Validation.ts" />
namespace Validation {
    const lettersRegexp = /^[A-Za-z]+$/;
    
    export class LettersOnlyValidator implements StringValidator {
        isAcceptable(s: string) {
            return lettersRegexp.test(s);
        }
    }
}

// ZipCodeValidator.ts
/// <reference path="Validation.ts" />
namespace Validation {
    const numberRegexp = /^[0-9]+$/;
    
    export class ZipCodeValidator implements StringValidator {
        isAcceptable(s: string) {
            return s.length === 5 && numberRegexp.test(s);
        }
    }
}

// Test.ts
/// <reference path="Validation.ts" />
/// <reference path="LettersOnlyValidator.ts" />
/// <reference path="ZipCodeValidator.ts" />

// 现在可以使用命名空间中的所有类型
let validators: { [s: string]: Validation.StringValidator; } = {};
validators["ZIP code"] = new Validation.ZipCodeValidator();
validators["Letters only"] = new Validation.LettersOnlyValidator();
```

### 命名空间别名
```typescript
// 命名空间别名
namespace Shapes {
    export namespace Polygons {
        export class Triangle {
            constructor(public sideLength: number) {}
            
            getArea(): number {
                return (Math.sqrt(3) / 4) * Math.pow(this.sideLength, 2);
            }
        }
        
        export class Square {
            constructor(public sideLength: number) {}
            
            getArea(): number {
                return Math.pow(this.sideLength, 2);
            }
        }
    }
}

// 创建命名空间别名
import polygons = Shapes.Polygons;
let sq = new polygons.Square(10);
console.log(sq.getArea()); // 100

// 嵌套命名空间别名
namespace A {
    export namespace B {
        export namespace C {
            export function doSomething() {
                console.log("Doing something in A.B.C");
            }
        }
    }
}

import doIt = A.B.C.doSomething;
doIt(); // "Doing something in A.B.C"
```

### 命名空间与模块的互操作
```typescript
// 命名空间与模块的互操作
// legacy.ts - 使用命名空间的旧代码
namespace Legacy {
    export class OldService {
        doWork(): string {
            return "Legacy work done";
        }
    }
    
    export const VERSION = "1.0.0";
}

// modern.ts - 使用模块的新代码
import { NewService } from "./new-service";

// 可以混合使用
class ModernAdapter {
    private legacyService = new Legacy.OldService();
    private newService = new NewService();
    
    doWork(): string {
        return `${this.legacyService.doWork()} and ${this.newService.doWork()}`;
    }
}

// 将命名空间导出为模块
// legacy-adapter.ts
import "./legacy"; // 导入命名空间

export const LegacyService = Legacy.OldService;
export const LEGACY_VERSION = Legacy.VERSION;
```

## 声明合并

### 接口合并
```typescript
// 接口合并基础
interface Box {
    height: number;
    width: number;
}

interface Box {
    scale: number;
}

// 结果接口
// interface Box {
//     height: number;
//     width: number;
//     scale: number;
// }

let box: Box = { height: 5, width: 6, scale: 10 };

// 函数合并
interface Cloner {
    clone(animal: Animal): Animal;
}

interface Cloner {
    clone(animal: Sheep): Sheep;
}

interface Cloner {
    clone(animal: Dog): Dog;
    clone(animal: Cat): Cat;
}

// 结果接口
// interface Cloner {
//     clone(animal: Dog): Dog;
//     clone(animal: Cat): Cat;
//     clone(animal: Sheep): Sheep;
//     clone(animal: Animal): Animal;
// }
```

### 命名空间合并
```typescript
// 命名空间合并
namespace Animals {
    export class Zebra { }
}

namespace Animals {
    export interface Legged { numberOfLegs: number; }
    export class Dog { }
}

// 结果命名空间
// namespace Animals {
//     export class Zebra { }
//     export interface Legged { numberOfLegs: number; }
//     export class Dog { }
// }

// 使用合并后的命名空间
let zebra = new Animals.Zebra();
let dog = new Animals.Dog();
```

### 命名空间与类合并
```typescript
// 命名空间与类合并
class Album {
    label: Album.AlbumLabel;
}

namespace Album {
    export interface AlbumLabel {
        name: string;
        year: number;
    }
    
    export function createLabel(name: string, year: number): AlbumLabel {
        return { name, year };
    }
}

// 使用合并结果
let album = new Album();
album.label = Album.createLabel("Greatest Hits", 2020);

// 函数与命名空间合并
function buildName(firstName: string, lastName?: string) {
    if (lastName) {
        return firstName + " " + lastName;
    } else {
        return firstName;
    }
}

namespace buildName {
    export function reallyFancyName(firstName: string, lastName?: string) {
        return "The Honorable " + buildName(firstName, lastName);
    }
}

// 使用合并结果
console.log(buildName("Bob")); // "Bob"
console.log(buildName.reallyFancyName("Bob", "Smith")); // "The Honorable Bob Smith"
```

### 枚举与命名空间合并
```typescript
// 枚举与命名空间合并
enum Color {
    red,
    green,
    blue
}

namespace Color {
    export function mixColor(colorName: string) {
        if (colorName === "yellow") {
            return Color.red + Color.green;
        } else if (colorName === "white") {
            return Color.red + Color.green + Color.blue;
        } else if (colorName === "magenta") {
            return Color.red + Color.blue;
        } else if (colorName === "cyan") {
            return Color.green + Color.blue;
        }
    }
}

// 使用合并结果
console.log(Color.mixColor("yellow")); // 1 (red + green)
console.log(Color[Color.red]); // "red"
```

### 声明合并的实际应用
```typescript
// 实际应用：扩展第三方库
// 为第三方库添加类型定义
declare namespace $ {
    interface JQuery {
        myPlugin(options?: MyPluginOptions): JQuery;
    }
    
    interface MyPluginOptions {
        color?: string;
        duration?: number;
    }
}

// 扩展全局对象
declare global {
    interface Window {
        myCustomProperty: string;
        myCustomFunction(): void;
    }
}

// 在代码中使用扩展
window.myCustomProperty = "Hello";
window.myCustomFunction = () => {
    console.log("Custom function called");
};

// 扩展内置类型
interface Array<T> {
    groupBy<U>(keySelector: (item: T) => U): Map<U, T[]>;
}

// 实现扩展方法
Array.prototype.groupBy = function<T, U>(keySelector: (item: T) => U): Map<U, T[]> {
    const map = new Map<U, T[]>();
    this.forEach(item => {
        const key = keySelector(item);
        if (!map.has(key)) {
            map.set(key, []);
        }
        map.get(key)!.push(item);
    });
    return map;
};

// 使用扩展方法
let users = [
    { name: "Alice", department: "IT" },
    { name: "Bob", department: "HR" },
    { name: "Charlie", department: "IT" }
];

let grouped = users.groupBy(user => user.department);
console.log(grouped.get("IT")); // [{ name: "Alice", ... }, { name: "Charlie", ... }]
```

# 10. 装饰器

## 类装饰器

### 基本类装饰器
```typescript
// 基本类装饰器
function sealed(constructor: Function) {
    Object.seal(constructor);
    Object.seal(constructor.prototype);
}

@sealed
class Greeter {
    greeting: string;
    
    constructor(message: string) {
        this.greeting = message;
    }
    
    greet() {
        return "Hello, " + this.greeting;
    }
}

// 类装饰器可以返回新的构造函数
function classDecorator<T extends { new (...args: any[]): {} }>(constructor: T) {
    return class extends constructor {
        newProperty = "new property";
        hello = "override";
    };
}

@classDecorator
class Myclass {
    property = "property";
    hello: string;
    
    constructor(m: string) {
        this.hello = m;
    }
}

console.log(new Myclass("world")); // { property: "property", hello: "override", newProperty: "new property" }
```

### 类装饰器的实际应用
```typescript
// 日志记录装饰器
function logClass(target: Function) {
    console.log(`Class ${target.name} is being created`);
}

@logClass
class UserService {
    constructor() {
        console.log("UserService constructor called");
    }
    
    getUsers() {
        return ["Alice", "Bob", "Charlie"];
    }
}

// 单例装饰器
function singleton<T extends { new (...args: any[]): {} }>(constructor: T) {
    let instance: T;
    return class extends constructor {
        constructor(...args: any[]) {
            if (!instance) {
                super(...args);
                instance = this as any;
            }
            return instance;
        }
    };
}

@singleton
class DatabaseConnection {
    private connectionString: string;
    
    constructor(connectionString: string) {
        this.connectionString = connectionString;
        console.log(`Creating database connection to ${connectionString}`);
    }
    
    connect() {
        console.log("Connected to database");
    }
}

let db1 = new DatabaseConnection("localhost:5432");
let db2 = new DatabaseConnection("localhost:5432");
console.log(db1 === db2); // true - 同一个实例
```

### 类装饰器与元数据
```typescript
// 类装饰器添加元数据
function version(version: string) {
    return function (constructor: Function) {
        constructor.prototype.version = version;
        constructor.prototype.getVersion = function() {
            return version;
        };
    };
}

@version("1.0.0")
class ApiClient {
    constructor() {}
    
    makeRequest() {
        console.log(`Making request with version ${this.getVersion()}`);
    }
}

let client = new ApiClient();
client.makeRequest(); // "Making request with version 1.0.0"
console.log(client.version); // "1.0.0"
```

## 方法装饰器

### 基本方法装饰器
```typescript
// 基本方法装饰器
function enumerable(value: boolean) {
    return function (target: any, propertyKey: string, descriptor: PropertyDescriptor) {
        descriptor.enumerable = value;
    };
}

class Greeter2 {
    greeting: string;
    
    constructor(message: string) {
        this.greeting = message;
    }
    
    @enumerable(false)
    greet() {
        return "Hello, " + this.greeting;
    }
}

// 方法装饰器可以修改方法行为
function log(target: any, propertyName: string, descriptor: PropertyDescriptor) {
    const method = descriptor.value;
    
    descriptor.value = function (...args: any[]) {
        console.log(`Calling ${propertyName} with arguments:`, args);
        const result = method.apply(this, args);
        console.log(`Method ${propertyName} returned:`, result);
        return result;
    };
}

class Calculator {
    @log
    add(a: number, b: number): number {
        return a + b;
    }
    
    @log
    multiply(a: number, b: number): number {
        return a * b;
    }
}

let calc = new Calculator();
calc.add(2, 3); // 日志输出和结果
calc.multiply(4, 5); // 日志输出和结果
```

### 方法装饰器的实际应用
```typescript
// 缓存装饰器
function cache(target: any, propertyName: string, descriptor: PropertyDescriptor) {
    const method = descriptor.value;
    const cache = new Map<string, any>();
    
    descriptor.value = function (...args: any[]) {
        const key = JSON.stringify(args);
        
        if (cache.has(key)) {
            console.log(`Returning cached result for ${propertyName}`);
            return cache.get(key);
        }
        
        const result = method.apply(this, args);
        cache.set(key, result);
        console.log(`Caching result for ${propertyName}`);
        return result;
    };
}

class ExpensiveService {
    @cache
    calculateFibonacci(n: number): number {
        if (n <= 1) return n;
        return this.calculateFibonacci(n - 1) + this.calculateFibonacci(n - 2);
    }
    
    @cache
    fetchUserData(id: string): any {
        console.log(`Fetching user data for ${id} from database`);
        return { id, name: `User ${id}` };
    }
}

let service = new ExpensiveService();
console.log(service.calculateFibonacci(10)); // 计算并缓存
console.log(service.calculateFibonacci(10)); // 从缓存返回
```

### 方法装饰器与错误处理
```typescript
// 错误处理装饰器
function catchError(fallbackValue?: any) {
    return function (target: any, propertyName: string, descriptor: PropertyDescriptor) {
        const method = descriptor.value;
        
        descriptor.value = function (...args: any[]) {
            try {
                return method.apply(this, args);
            } catch (error) {
                console.error(`Error in ${propertyName}:`, error);
                return fallbackValue;
            }
        };
    };
}

class RiskyService {
    @catchError(0)
    divide(a: number, b: number): number {
        if (b === 0) throw new Error("Division by zero");
        return a / b;
    }
    
    @catchError("Error occurred")
    riskyOperation(data: any): string {
        if (!data) throw new Error("Invalid data");
        return JSON.stringify(data);
    }
}

let service2 = new RiskyService();
console.log(service2.divide(10, 2)); // 5
console.log(service2.divide(10, 0)); // 0 (fallback value)
console.log(service2.riskyOperation(null)); // "Error occurred"
```

## 访问器装饰器

### 基本访问器装饰器
```typescript
// 基本访问器装饰器
function configurable(value: boolean) {
    return function (target: any, propertyKey: string, descriptor: PropertyDescriptor) {
        descriptor.configurable = value;
    };
}

class Point {
    private _x: number;
    private _y: number;
    
    constructor(x: number, y: number) {
        this._x = x;
        this._y = y;
    }
    
    @configurable(false)
    get x() {
        return this._x;
    }
    
    @configurable(false)
    get y() {
        return this._y;
    }
}

// 验证装饰器
function validate(validateFn: (value: any) => boolean, errorMessage: string) {
    return function (target: any, propertyKey: string, descriptor: PropertyDescriptor) {
        const originalSet = descriptor.set;
        
        descriptor.set = function (value: any) {
            if (!validateFn(value)) {
                throw new Error(errorMessage);
            }
            if (originalSet) {
                originalSet.call(this, value);
            }
        };
    };
}

class User {
    private _email: string = "";
    
    @validate(
        (value: string) => typeof value === "string" && value.includes("@"),
        "Invalid email format"
    )
    set email(value: string) {
        this._email = value;
    }
    
    get email(): string {
        return this._email;
    }
}

let user = new User();
try {
    user.email = "invalid-email"; // 抛出错误
} catch (error) {
    console.error(error.message); // "Invalid email format"
}

user.email = "valid@example.com"; // 正确设置
console.log(user.email); // "valid@example.com"
```

### 访问器装饰器的实际应用
```typescript
// 日志访问器装饰器
function logAccess(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
    const originalGet = descriptor.get;
    const originalSet = descriptor.set;
    
    if (originalGet) {
        descriptor.get = function () {
            console.log(`Getting ${propertyKey}`);
            return originalGet.call(this);
        };
    }
    
    if (originalSet) {
        descriptor.set = function (value: any) {
            console.log(`Setting ${propertyKey} to ${value}`);
            return originalSet.call(this, value);
        };
    }
}

class Temperature {
    private _celsius: number = 0;
    
    @logAccess
    get celsius(): number {
        return this._celsius;
    }
    
    set celsius(value: number) {
        if (value < -273.15) {
            throw new Error("Temperature cannot be below absolute zero");
        }
        this._celsius = value;
    }
    
    @logAccess
    get fahrenheit(): number {
        return (this._celsius * 9/5) + 32;
    }
    
    set fahrenheit(value: number) {
        this.celsius = (value - 32) * 5/9;
    }
}

let temp = new Temperature();
temp.celsius = 25; // "Setting celsius to 25"
console.log(temp.celsius); // "Getting celsius" 然后输出 25
console.log(temp.fahrenheit); // "Getting fahrenheit" 然后输出 77
```

## 属性装饰器

### 基本属性装饰器
```typescript
// 基本属性装饰器
function format(formatString: string) {
    return function (target: any, propertyKey: string) {
        let value: string;
        
        const getter = function () {
            return value;
        };
        
        const setter = function (newVal: string) {
            value = newVal ? `${formatString}${newVal}` : newVal;
        };
        
        Object.defineProperty(target, propertyKey, {
            get: getter,
            set: setter,
            enumerable: true,
            configurable: true
        });
    };
}

class Product {
    @format("SKU-")
    sku: string;
    
    constructor(sku: string) {
        this.sku = sku;
    }
}

let product = new Product("12345");
console.log(product.sku); // "SKU-12345"
```

### 属性装饰器与元数据
```typescript
// 属性装饰器添加元数据
const requiredMetadataKey = Symbol("required");

function required(target: any, propertyKey: string | symbol) {
    const existingRequiredProperties: string[] = Reflect.getMetadata(requiredMetadataKey, target) || [];
    existingRequiredProperties.push(propertyKey as string);
    Reflect.defineMetadata(requiredMetadataKey, existingRequiredProperties, target);
}

function validateRequired(target: any, propertyName: string, descriptor: PropertyDescriptor) {
    const method = descriptor.value;
    
    descriptor.value = function (...args: any[]) {
        const requiredProperties = Reflect.getMetadata(requiredMetadataKey, target) || [];
        
        for (const property of requiredProperties) {
            if (!this[property]) {
                throw new Error(`Property ${property} is required`);
            }
        }
        
        return method.apply(this, args);
    };
}

class UserForm {
    @required
    name: string;
    
    @required
    email: string;
    
    constructor(name: string, email: string) {
        this.name = name;
        this.email = email;
    }
    
    @validateRequired
    submit() {
        console.log("Form submitted successfully");
        return { name: this.name, email: this.email };
    }
}

let form = new UserForm("", "user@example.com");
try {
    form.submit(); // 抛出错误：Property name is required
} catch (error) {
    console.error(error.message);
}

let validForm = new UserForm("Alice", "alice@example.com");
console.log(validForm.submit()); // "Form submitted successfully"
```

### 属性装饰器的实际应用
```typescript
// 验证属性装饰器
function minLength(length: number) {
    return function (target: any, propertyKey: string) {
        let value: string;
        
        const getter = function () {
            return value;
        };
        
        const setter = function (newVal: string) {
            if (newVal && newVal.length < length) {
                throw new Error(`Property ${propertyKey} must be at least ${length} characters long`);
            }
            value = newVal;
        };
        
        Object.defineProperty(target, propertyKey, {
            get: getter,
            set: setter,
            enumerable: true,
            configurable: true
        });
    };
}

function maxLength(length: number) {
    return function (target: any, propertyKey: string) {
        let value: string;
        
        const getter = function () {
            return value;
        };
        
        const setter = function (newVal: string) {
            if (newVal && newVal.length > length) {
                throw new Error(`Property ${propertyKey} must be no more than ${length} characters long`);
            }
            value = newVal;
        };
        
        Object.defineProperty(target, propertyKey, {
            get: getter,
            set: setter,
            enumerable: true,
            configurable: true
        });
    };
}

class UserRegistration {
    @minLength(3)
    @maxLength(20)
    username: string;
    
    @minLength(6)
    password: string;
    
    constructor(username: string, password: string) {
        this.username = username;
        this.password = password;
    }
}

try {
    let user1 = new UserRegistration("ab", "password123"); // 用户名太短
} catch (error) {
    console.error(error.message);
}

try {
    let user2 = new UserRegistration("alice", "123"); // 密码太短
} catch (error) {
    console.error(error.message);
}

let validUser = new UserRegistration("alice", "password123"); // 正确
console.log(validUser.username); // "alice"
```

## 参数装饰器

### 基本参数装饰器
```typescript
// 基本参数装饰器
function logParameter(target: Object, propertyKey: string | symbol, parameterIndex: number) {
    const existingRequiredParameters: number[] = Reflect.getMetadata("logParameters", target, propertyKey) || [];
    existingRequiredParameters.push(parameterIndex);
    Reflect.defineMetadata("logParameters", existingRequiredParameters, target, propertyKey);
}

function logMethod(target: any, propertyName: string, descriptor: PropertyDescriptor) {
    const method = descriptor.value;
    
    descriptor.value = function (...args: any[]) {
        const logParameters: number[] = Reflect.getMetadata("logParameters", target, propertyName) || [];
        
        logParameters.forEach(index => {
            console.log(`Parameter ${index} of method ${propertyName}: ${args[index]}`);
        });
        
        return method.apply(this, args);
    };
}

class Calculator2 {
    @logMethod
    add(@logParameter a: number, @logParameter b: number): number {
        return a + b;
    }
    
    @logMethod
    multiply(a: number, @logParameter b: number, @logParameter c: number): number {
        return a * b * c;
    }
}

let calc2 = new Calculator2();
calc2.add(2, 3); // 输出参数日志和结果
calc2.multiply(2, 3, 4); // 输出指定参数的日志和结果
```

### 参数装饰器与验证
```typescript
// 参数验证装饰器
const validationMetadataKey = Symbol("validation");

interface ValidationRule {
    index: number;
    validator: (value: any) => boolean;
    message: string;
}

function validate(validator: (value: any) => boolean, message: string) {
    return function (target: Object, propertyKey: string | symbol, parameterIndex: number) {
        const existingValidations: ValidationRule[] = 
            Reflect.getMetadata(validationMetadataKey, target, propertyKey) || [];
        
        existingValidations.push({
            index: parameterIndex,
            validator,
            message
        });
        
        Reflect.defineMetadata(validationMetadataKey, existingValidations, target, propertyKey);
    };
}

function validateParameters(target: any, propertyName: string, descriptor: PropertyDescriptor) {
    const method = descriptor.value;
    
    descriptor.value = function (...args: any[]) {
        const validations: ValidationRule[] = 
            Reflect.getMetadata(validationMetadataKey, target, propertyName) || [];
        
        for (const validation of validations) {
            const value = args[validation.index];
            if (!validation.validator(value)) {
                throw new Error(`Parameter validation failed: ${validation.message}`);
            }
        }
        
        return method.apply(this, args);
    };
}

class UserService2 {
    @validateParameters
    createUser(
        @validate((name: string) => name.length > 0, "Name cannot be empty")
        @validate((name: string) => name.length <= 50, "Name too long")
        name: string,
        
        @validate((email: string) => /\S+@\S+\.\S+/.test(email), "Invalid email format")
        email: string,
        
        @validate((age: number) => age >= 0 && age <= 150, "Invalid age")
        age: number
    ): any {
        return { name, email, age, id: Math.random().toString(36) };
    }
}

let service3 = new UserService2();

try {
    service3.createUser("", "user@example.com", 25); // 名字为空
} catch (error) {
    console.error(error.message); // "Parameter validation failed: Name cannot be empty"
}

try {
    service3.createUser("Alice", "invalid-email", 25); // 邮箱格式错误
} catch (error) {
    console.error(error.message); // "Parameter validation failed: Invalid email format"
}

let user = service3.createUser("Alice", "alice@example.com", 25); // 正确
console.log(user);
```

## 装饰器工厂

### 基本装饰器工厂
```typescript
// 基本装饰器工厂
function color(value: string) {
    return function (target: any) {
        target.prototype.color = value;
    };
}

function logPrefix(prefix: string) {
    return function (target: any, propertyName: string, descriptor: PropertyDescriptor) {
        const method = descriptor.value;
        
        descriptor.value = function (...args: any[]) {
            console.log(`[${prefix}] Calling ${propertyName}`);
            return method.apply(this, args);
        };
    };
}

@color("blue")
class Widget {
    @logPrefix("DEBUG")
    doSomething() {
        console.log("Doing something...");
    }
    
    @logPrefix("INFO")
    doAnotherThing() {
        console.log("Doing another thing...");
    }
}

let widget = new Widget();
widget.doSomething(); // "[DEBUG] Calling doSomething" 然后 "Doing something..."
widget.doAnotherThing(); // "[INFO] Calling doAnotherThing" 然后 "Doing another thing..."
console.log((widget as any).color); // "blue"
```

### 复杂装饰器工厂
```typescript
// 复杂装饰器工厂
interface RetryOptions {
    maxRetries?: number;
    delay?: number;
    exponentialBackoff?: boolean;
}

function retry(options: RetryOptions = {}) {
    const { maxRetries = 3, delay = 1000, exponentialBackoff = false } = options;
    
    return function (target: any, propertyName: string, descriptor: PropertyDescriptor) {
        const method = descriptor.value;
        
        descriptor.value = async function (...args: any[]) {
            let lastError: Error;
            
            for (let i = 0; i <= maxRetries; i++) {
                try {
                    return await method.apply(this, args);
                } catch (error) {
                    lastError = error;
                    
                    if (i < maxRetries) {
                        const waitTime = exponentialBackoff ? delay * Math.pow(2, i) : delay;
                        console.log(`Attempt ${i + 1} failed, retrying in ${waitTime}ms...`);
                        await new Promise(resolve => setTimeout(resolve, waitTime));
                    }
                }
            }
            
            throw lastError;
        };
    };
}

class ApiService {
    @retry({ maxRetries: 3, delay: 1000, exponentialBackoff: true })
    async fetchUserData(id: string): Promise<any> {
        // 模拟网络请求，可能失败
        if (Math.random() < 0.7) {
            throw new Error("Network error");
        }
        return { id, name: `User ${id}` };
    }
    
    @retry({ maxRetries: 2, delay: 500 })
    async saveUserData(data: any): Promise<boolean> {
        // 模拟保存操作
        if (Math.random() < 0.5) {
            throw new Error("Database error");
        }
        return true;
    }
}

// 使用示例
async function useApiService() {
    const service = new ApiService();
    
    try {
        const user = await service.fetchUserData("123");
        console.log("User fetched:", user);
    } catch (error) {
        console.error("Failed to fetch user:", error.message);
    }
}
```

### 装饰器工厂组合
```typescript
// 装饰器工厂组合
function withLogging(prefix: string) {
    return function (target: any, propertyName: string, descriptor: PropertyDescriptor) {
        const originalMethod = descriptor.value;
        
        descriptor.value = function (...args: any[]) {
            console.log(`[${prefix}] ${propertyName} called with:`, args);
            const result = originalMethod.apply(this, args);
            console.log(`[${prefix}] ${propertyName} returned:`, result);
            return result;
        };
    };
}

function withTiming(target: any, propertyName: string, descriptor: PropertyDescriptor) {
    const originalMethod = descriptor.value;
    
    descriptor.value = function (...args: any[]) {
        const start = Date.now();
        const result = originalMethod.apply(this, args);
        const end = Date.now();
        console.log(`${propertyName} took ${end - start}ms`);
        return result;
    };
}

function withCache(ttl: number = 60000) { // 默认1分钟
    return function (target: any, propertyName: string, descriptor: PropertyDescriptor) {
        const cache = new Map<string, { value: any; timestamp: number }>();
        const originalMethod = descriptor.value;
        
        descriptor.value = function (...args: any[]) {
            const key = JSON.stringify(args);
            const cached = cache.get(key);
            
            if (cached && Date.now() - cached.timestamp < ttl) {
                console.log(`[${propertyName}] Returning cached result`);
                return cached.value;
            }
            
            const result = originalMethod.apply(this, args);
            cache.set(key, { value: result, timestamp: Date.now() });
            console.log(`[${propertyName}] Caching new result`);
            return result;
        };
    };
}

class DataProcessor {
    @withLogging("PROCESSOR")
    @withTiming
    @withCache(30000) // 30秒缓存
    processData(data: any[]): any[] {
        // 模拟耗时操作
        const start = Date.now();
        while (Date.now() - start < 100) {
            // 模拟处理时间
        }
        return data.map(item => ({ ...item, processed: true }));
    }
}

let processor = new DataProcessor();
let data = [{ id: 1, name: "item1" }, { id: 2, name: "item2" }];

processor.processData(data); // 第一次调用
processor.processData(data); // 第二次调用（从缓存返回）
```

## 装饰器执行顺序

### 装饰器应用顺序
```typescript
// 装饰器应用顺序演示
function first() {
    console.log("first(): factory evaluated");
    return function (target: any, propertyKey: string, descriptor: PropertyDescriptor) {
        console.log("first(): called");
    };
}

function second() {
    console.log("second(): factory evaluated");
    return function (target: any, propertyKey: string, descriptor: PropertyDescriptor) {
        console.log("second(): called");
    };
}

class Example {
    @first()
    @second()
    method() {}
}

// 输出顺序：
// first(): factory evaluated
// second(): factory evaluated
// second(): called
// first(): called
```

### 不同类成员装饰器的执行顺序
```typescript
// 不同类成员装饰器的执行顺序
function classDecorator() {
    console.log("Class decorator factory evaluated");
    return function (constructor: Function) {
        console.log("Class decorator called");
    };
}

function propertyDecorator() {
    console.log("Property decorator factory evaluated");
    return function (target: any, propertyKey: string) {
        console.log(`Property decorator called for ${propertyKey}`);
    };
}

function methodDecorator() {
    console.log("Method decorator factory evaluated");
    return function (target: any, propertyKey: string, descriptor: PropertyDescriptor) {
        console.log(`Method decorator called for ${propertyKey}`);
    };
}

function parameterDecorator() {
    console.log("Parameter decorator factory evaluated");
    return function (target: Object, propertyKey: string | symbol, parameterIndex: number) {
        console.log(`Parameter decorator called for parameter ${parameterIndex} of ${propertyKey}`);
    };
}

@classDecorator()
class Order {
    @propertyDecorator()
    productName: string;
    
    constructor(
        @parameterDecorator() productName: string
    ) {
        this.productName = productName;
    }
    
    @methodDecorator()
    calculateTotal(
        @parameterDecorator() quantity: number,
        @parameterDecorator() price: number
    ): number {
        return quantity * price;
    }
}

// 输出顺序：
// Property decorator factory evaluated
// Parameter decorator factory evaluated
// Method decorator factory evaluated
// Parameter decorator factory evaluated
// Parameter decorator factory evaluated
// Class decorator factory evaluated
// Property decorator called for productName
// Parameter decorator called for parameter 0 of calculateTotal
// Parameter decorator called for parameter 1 of calculateTotal
// Method decorator called for calculateTotal
// Parameter decorator called for parameter 0 of constructor
// Class decorator called
```

### 实际执行顺序示例
```typescript
// 实际执行顺序示例
let counter = 0;

function logDecorator(name: string) {
    const id = ++counter;
    console.log(`${id}. ${name} factory evaluated`);
    
    return function (target: any, propertyKey?: string, descriptor?: PropertyDescriptor) {
        console.log(`${id}. ${name} decorator called`);
    };
}

function logClassDecorator(name: string) {
    const id = ++counter;
    console.log(`${id}. ${name} factory evaluated`);
    
    return function (constructor: Function) {
        console.log(`${id}. ${name} decorator called`);
    };
}

function logParameterDecorator(name: string) {
    const id = ++counter;
    console.log(`${id}. ${name} factory evaluated`);
    
    return function (target: Object, propertyKey: string | symbol, parameterIndex: number) {
        console.log(`${id}. ${name} decorator called for parameter ${parameterIndex}`);
    };
}

@logClassDecorator("ClassA")
@logClassDecorator("ClassB")
class TestClass {
    @logDecorator("PropertyA")
    @logDecorator("PropertyB")
    prop1: string;
    
    @logDecorator("PropertyC")
    prop2: number;
    
    constructor(
        @logParameterDecorator("ParamA")
        @logParameterDecorator("ParamB")
        param1: string,
        
        @logParameterDecorator("ParamC")
        param2: number
    ) {
        this.prop1 = param1;
        this.prop2 = param2;
    }
    
    @logDecorator("MethodA")
    @logDecorator("MethodB")
    method1(
        @logParameterDecorator("MethodParamA")
        @logParameterDecorator("MethodParamB")
        arg1: string
    ) {
        console.log("method1 called");
    }
    
    @logDecorator("MethodC")
    method2() {
        console.log("method2 called");
    }
}
```

## 元数据反射

### 基本元数据反射
```typescript
// 需要安装 reflect-metadata 包
// npm install reflect-metadata
// import "reflect-metadata";

// 基本元数据反射
function metadata(key: string, value: any) {
    return function (target: any, propertyKey?: string) {
        if (propertyKey) {
            Reflect.defineMetadata(key, value, target, propertyKey);
        } else {
            Reflect.defineMetadata(key, value, target);
        }
    };
}

function getMetadata(key: string, target: any, propertyKey?: string) {
    if (propertyKey) {
        return Reflect.getMetadata(key, target, propertyKey);
    } else {
        return Reflect.getMetadata(key, target);
    }
}

@metadata("version", "1.0.0")
@metadata("author", "John Doe")
class ApiClient2 {
    @metadata("type", "string")
    @metadata("required", true)
    apiKey: string;
    
    @metadata("type", "number")
    @metadata("min", 1)
    @metadata("max", 100)
    timeout: number;
    
    constructor(apiKey: string, timeout: number) {
        this.apiKey = apiKey;
        this.timeout = timeout;
    }
    
    @metadata("returns", "Promise<any>")
    @metadata("throws", ["NetworkError", "TimeoutError"])
    async makeRequest(endpoint: string): Promise<any> {
        // 实现
        return {};
    }
}

// 读取元数据
console.log(getMetadata("version", ApiClient2)); // "1.0.0"
console.log(getMetadata("author", ApiClient2)); // "John Doe"
console.log(getMetadata("type", ApiClient2.prototype, "apiKey")); // "string"
console.log(getMetadata("required", ApiClient2.prototype, "apiKey")); // true
console.log(getMetadata("returns", ApiClient2.prototype, "makeRequest")); // "Promise<any>"
```

### 设计时类型元数据
```typescript
// 设计时类型元数据
function logType(target: any, propertyKey: string) {
    const type = Reflect.getMetadata("design:type", target, propertyKey);
    console.log(`${propertyKey} type: ${type.name}`);
}

function logParamTypes(target: any, propertyKey: string) {
    const types = Reflect.getMetadata("design:paramtypes", target, propertyKey);
    console.log(`${propertyKey} parameter types:`, types?.map((t: any) => t.name));
}

function logReturnType(target: any, propertyKey: string) {
    const type = Reflect.getMetadata("design:returntype", target, propertyKey);
    console.log(`${propertyKey} return type: ${type?.name}`);
}

class UserService3 {
    @logType
    name: string;
    
    @logType
    age: number;
    
    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
    
    @logParamTypes
    @logReturnType
    getUser(id: string): Promise<any> {
        return Promise.resolve({ id, name: this.name, age: this.age });
    }
    
    @logParamTypes
    updateUser(id: string, data: { name: string; age: number }): void {
        // 实现
    }
}

let userService = new UserService3("Alice", 30);
// 输出：
// name type: String
// age type: Number
// getUser parameter types: [String]
// getUser return type: Promise
// updateUser parameter types: [String, Object]
```

### 元数据反射的实际应用
```typescript
// 元数据反射的实际应用：依赖注入
interface Injectable {
    new (...args: any[]): any;
}

const INJECTABLE_KEY = Symbol("injectable");
const INJECTIONS_KEY = Symbol("injections");

function Injectable() {
    return function (constructor: Injectable) {
        Reflect.defineMetadata(INJECTABLE_KEY, true, constructor);
        
        // 获取构造函数参数类型
        const tokens = Reflect.getMetadata("design:paramtypes", constructor) || [];
        Reflect.defineMetadata(INJECTIONS_KEY, tokens, constructor);
    };
}

function Inject(token: any) {
    return function (target: any, propertyKey: string | symbol, parameterIndex: number) {
        const existingInjections = Reflect.getMetadata(INJECTIONS_KEY, target) || [];
        existingInjections[parameterIndex] = token;
        Reflect.defineMetadata(INJECTIONS_KEY, existingInjections, target);
    };
}

class Container {
    private services = new Map<any, any>();
    
    register<T>(token: any, implementation: Injectable): void {
        this.services.set(token, implementation);
    }
    
    resolve<T>(token: any): T {
        const Service = this.services.get(token);
        if (!Service) {
            throw new Error(`No service registered for ${token.name}`);
        }
        
        // 获取需要注入的依赖
        const tokens = Reflect.getMetadata(INJECTIONS_KEY, Service) || [];
        const injections = tokens.map((token: any) => this.resolve(token));
        
        return new Service(...injections);
    }
}

// 服务定义
@Injectable()
class DatabaseService {
    connect() {
        console.log("Database connected");
    }
}

@Injectable()
class LoggerService {
    log(message: string) {
        console.log(`[LOG] ${message}`);
    }
}

@Injectable()
class UserService4 {
    constructor(
        private database: DatabaseService,
        private logger: LoggerService
    ) {}
    
    getUsers() {
        this.logger.log("Fetching users");
        this.database.connect();
        return ["Alice", "Bob", "Charlie"];
    }
}

// 使用依赖注入
const container = new Container();
container.register(DatabaseService, DatabaseService);
container.register(LoggerService, LoggerService);
container.register(UserService4, UserService4);

const userService4 = container.resolve<UserService4>(UserService4);
console.log(userService4.getUsers());
```

### 高级元数据应用
```typescript
// 高级元数据应用：ORM 映射
interface ColumnOptions {
    name?: string;
    type?: string;
    primaryKey?: boolean;
    nullable?: boolean;
}

const TABLE_KEY = Symbol("table");
const COLUMNS_KEY = Symbol("columns");

function Entity(tableName: string) {
    return function (constructor: Function) {
        Reflect.defineMetadata(TABLE_KEY, tableName, constructor);
    };
}

function Column(options: ColumnOptions = {}) {
    return function (target: any, propertyKey: string) {
        const columns = Reflect.getMetadata(COLUMNS_KEY, target.constructor) || {};
        columns[propertyKey] = {
            name: options.name || propertyKey,
            type: options.type,
            primaryKey: options.primaryKey || false,
            nullable: options.nullable !== undefined ? options.nullable : true
        };
        Reflect.defineMetadata(COLUMNS_KEY, columns, target.constructor);
    };
}

@Entity("users")
class UserEntity {
    @Column({ primaryKey: true, type: "integer" })
    id: number;
    
    @Column({ name: "user_name", type: "varchar", nullable: false })
    name: string;
    
    @Column({ type: "integer" })
    age: number;
    
    @Column({ type: "varchar", nullable: true })
    email: string;
}

// 读取 ORM 元数据
function getTableMetadata(target: any) {
    const tableName = Reflect.getMetadata(TABLE_KEY, target);
    const columns = Reflect.getMetadata(COLUMNS_KEY, target) || {};
    
    return {
        table: tableName,
        columns
    };
}

const metadata = getTableMetadata(UserEntity);
console.log("Table:", metadata.table);
console.log("Columns:", metadata.columns);

// 生成 SQL
function generateCreateTableSQL(target: any): string {
    const { table, columns } = getTableMetadata(target);
    
    const columnDefinitions = Object.entries(columns).map(([property, column]: [string, any]) => {
        let definition = `"${column.name}" ${column.type || 'TEXT'}`;
        if (column.primaryKey) {
            definition += " PRIMARY KEY";
        }
        if (!column.nullable) {
            definition += " NOT NULL";
        }
        return definition;
    });
    
    return `CREATE TABLE "${table}" (\n  ${columnDefinitions.join(',\n  ')}\n);`;
}

console.log(generateCreateTableSQL(UserEntity));
// CREATE TABLE "users" (
//   "id" integer PRIMARY KEY,
//   "user_name" varchar NOT NULL,
//   "age" integer,
//   "email" varchar
// );
```


# 11. 配置选项

## tsconfig.json 结构

### 基本结构
```json
{
  "compilerOptions": {
    // 编译器选项
  },
  "files": [
    // 指定要编译的文件列表
  ],
  "include": [
    // 包含的文件模式
  ],
  "exclude": [
    // 排除的文件模式
  ],
  "references": [
    // 项目引用
  ],
  "compileOnSave": true,
  "extends": "./base-tsconfig.json",
  "watchOptions": {
    // 监视选项
  }
}
```

### 完整的 tsconfig.json 示例
```json
{
  "compilerOptions": {
    // 基础选项
    "target": "ES2020",
    "module": "commonjs",
    "lib": ["ES2020", "DOM"],
    "outDir": "./dist",
    "rootDir": "./src",
    
    // 严格类型检查
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "strictFunctionTypes": true,
    "strictBindCallApply": true,
    "strictPropertyInitialization": true,
    "noImplicitThis": true,
    "alwaysStrict": true,
    
    // 模块解析
    "moduleResolution": "node",
    "baseUrl": "./",
    "paths": {
      "@/*": ["src/*"],
      "@components/*": ["src/components/*"]
    },
    
    // 装饰器支持
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true,
    
    // 其他选项
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "resolveJsonModule": true,
    "sourceMap": true,
    "declaration": true,
    "removeComments": true
  },
  
  "include": [
    "src/**/*"
  ],
  
  "exclude": [
    "node_modules",
    "dist",
    "**/*.spec.ts"
  ],
  
  "references": [
    { "path": "../shared" }
  ],
  
  "compileOnSave": true
}
```

### files、include 和 exclude 配置
```json
{
  "compilerOptions": {
    "target": "ES2020",
    "outDir": "./dist"
  },
  
  // 方式一：明确指定文件
  "files": [
    "src/index.ts",
    "src/utils.ts",
    "src/models/user.ts"
  ],
  
  // 方式二：包含文件模式（更常用）
  "include": [
    "src/**/*",           // src 目录下所有文件
    "tests/**/*.ts",      // tests 目录下所有 .ts 文件
    "typings/**/*.d.ts"   // 类型定义文件
  ],
  
  // 排除文件模式
  "exclude": [
    "node_modules",       // 排除 node_modules
    "dist",              // 排除输出目录
    "**/*.spec.ts",      // 排除测试文件
    "src/test-files"     // 排除特定目录
  ],
  
  // 通配符说明
  // * 匹配零个或多个字符（不包括目录分隔符）
  // ? 匹配一个字符
  // ** 递归匹配任意层级目录
}
```

## 编译器选项详解

### 基础编译选项
```json
{
  "compilerOptions": {
    // 目标 JavaScript 版本
    "target": "ES2020",  // ES3, ES5, ES2015, ES2016, ES2017, ES2018, ES2019, ES2020, ESNext
    
    // 模块系统
    "module": "commonjs", // none, commonjs, amd, system, umd, es2015, esnext
    
    // 标准库
    "lib": [
      "ES2020",          // JavaScript 标准库
      "DOM",             // DOM API
      "DOM.Iterable",    // DOM 可迭代接口
      "WebWorker"        // Web Worker API
    ],
    
    // 输出目录
    "outDir": "./dist",
    
    // 源码根目录
    "rootDir": "./src",
    
    // 复合项目
    "composite": true,
    
    // 增量编译
    "incremental": true,
    "tsBuildInfoFile": "./dist/.tsbuildinfo"
  }
}
```

### 严格类型检查选项
```json
{
  "compilerOptions": {
    // 启用所有严格类型检查选项
    "strict": true,
    
    // 具体的严格检查选项
    "noImplicitAny": true,              // 不允许隐式的 any 类型
    "strictNullChecks": true,           // 严格的 null 检查
    "strictFunctionTypes": true,        // 严格的函数类型检查
    "strictBindCallApply": true,        // 严格的 bind/call/apply 检查
    "strictPropertyInitialization": true, // 类属性必须初始化
    "noImplicitThis": true,             // 不允许隐式的 this
    "alwaysStrict": true,               // 始终使用严格模式
    
    // 其他类型检查选项
    "noUnusedLocals": true,             // 检查未使用的局部变量
    "noUnusedParameters": true,         // 检查未使用的参数
    "noImplicitReturns": true,          // 函数所有路径都必须有返回值
    "noFallthroughCasesInSwitch": true, // switch 语句不允许贯穿
    "noUncheckedIndexedAccess": true,   // 索引访问可能返回 undefined
    "exactOptionalPropertyTypes": true  // 可选属性不允许 undefined
  }
}
```

### 模块解析选项
```json
{
  "compilerOptions": {
    // 模块解析策略
    "moduleResolution": "node",  // node, classic
    
    // 基础目录
    "baseUrl": "./",
    
    // 路径映射
    "paths": {
      "@/*": ["src/*"],
      "@components/*": ["src/components/*"],
      "@utils/*": ["src/utils/*"],
      "shared/*": ["../shared/src/*"]
    },
    
    // 根目录
    "rootDirs": ["src", "generated"],
    
    // 类型根目录
    "typeRoots": [
      "./node_modules/@types",
      "./src/types"
    ],
    
    // 具体类型定义
    "types": ["node", "jest"],
    
    // 允许默认导入
    "allowSyntheticDefaultImports": true,
    
    // ES 模块互操作
    "esModuleInterop": true,
    
    // 保留 const 枚举
    "preserveConstEnums": true
  }
}
```

### 装饰器和实验性选项
```json
{
  "compilerOptions": {
    // 装饰器支持
    "experimentalDecorators": true,
    
    // 发射装饰器元数据
    "emitDecoratorMetadata": true,
    
    // JSX 支持
    "jsx": "react",  // preserve, react, react-native, react-jsx, react-jsxdev
    
    // 装饰器元数据的实验性选项
    "useDefineForClassFields": true
  }
}
```

### 输出和调试选项
```json
{
  "compilerOptions": {
    // 源码映射
    "sourceMap": true,
    "inlineSourceMap": false,
    "inlineSources": true,
    
    // 声明文件
    "declaration": true,
    "declarationMap": true,
    "emitDeclarationOnly": false,
    
    // 移除注释
    "removeComments": true,
    
    // 不输出文件
    "noEmit": false,
    "noEmitOnError": true,
    "noEmitHelpers": false,
    
    // 导入辅助函数
    "importHelpers": true,
    
    // 下载定义文件
    "downlevelIteration": true
  }
}
```

### JavaScript 支持选项
```json
{
  "compilerOptions": {
    // 允许 JavaScript 文件
    "allowJs": true,
    
    // 检查 JavaScript 文件
    "checkJs": true,
    
    // 最大节点模块 JS 深度
    "maxNodeModuleJsDepth": 2
  },
  
  "include": [
    "src/**/*",
    "lib/**/*.js"
  ]
}
```

## 项目引用

### 基本项目引用配置
```json
// 主项目 tsconfig.json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "outDir": "./dist",
    "rootDir": "./src",
    "composite": true,
    "declaration": true
  },
  "include": ["src/**/*"],
  "references": [
    { "path": "../shared" },
    { "path": "../utils" }
  ]
}

// 共享库 tsconfig.json (shared/tsconfig.json)
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "outDir": "./dist",
    "rootDir": "./src",
    "composite": true,
    "declaration": true
  },
  "include": ["src/**/*"]
}

// 工具库 tsconfig.json (utils/tsconfig.json)
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "outDir": "./dist",
    "rootDir": "./src",
    "composite": true,
    "declaration": true
  },
  "include": ["src/**/*"],
  "references": [
    { "path": "../shared" }
  ]
}
```

### 项目引用的实际应用
```typescript
// shared/src/models/user.ts
export interface User {
    id: string;
    name: string;
    email: string;
}

export class UserService {
    private users: User[] = [];
    
    addUser(user: User): void {
        this.users.push(user);
    }
    
    getUserById(id: string): User | undefined {
        return this.users.find(u => u.id === id);
    }
}

// utils/src/formatters.ts
import { User } from "shared/models/user";

export function formatUserName(user: User): string {
    return `${user.name} <${user.email}>`;
}

export function formatUserList(users: User[]): string {
    return users.map(u => formatUserName(u)).join('\n');
}

// main/src/app.ts
import { UserService } from "shared/models/user";
import { formatUserName } from "utils/formatters";

const userService = new UserService();
userService.addUser({ id: "1", name: "Alice", email: "alice@example.com" });

const user = userService.getUserById("1");
if (user) {
    console.log(formatUserName(user));
}
```

### 构建脚本配置
```json
// package.json
{
  "scripts": {
    "build": "tsc --build",
    "build:watch": "tsc --build --watch",
    "clean": "tsc --build --clean",
    "build:shared": "tsc --build shared",
    "build:utils": "tsc --build utils"
  }
}
```

### 项目引用的高级配置
```json
// 主项目 tsconfig.json（复杂引用）
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "outDir": "./dist",
    "rootDir": "./src",
    "composite": true,
    "declaration": true,
    "declarationMap": true
  },
  "include": ["src/**/*"],
  "references": [
    { 
      "path": "../shared",
      "prepend": false  // 是否前置编译输出
    },
    { 
      "path": "../utils" 
    },
    { 
      "path": "../legacy",
      "outputs": ["../legacy/dist/index.js"]  // 指定输出文件
    }
  ]
}
```

## 增量编译

### 增量编译基础配置
```json
// 启用增量编译
{
  "compilerOptions": {
    "incremental": true,
    "tsBuildInfoFile": "./dist/.tsbuildinfo",
    "composite": true,  // 增量编译通常与复合项目一起使用
    "outDir": "./dist",
    "rootDir": "./src"
  },
  "include": ["src/**/*"]
}
```

### 增量编译的工作原理
```typescript
// 增量编译跟踪文件依赖关系
// .tsbuildinfo 文件包含：
// 1. 文件哈希值
// 2. 依赖关系图
// 3. 编译选项
// 4. 类型检查结果

// 示例项目结构
// src/
//   ├── models/
//   │   ├── user.ts
//   │   └── product.ts
//   ├── services/
//   │   ├── user-service.ts
//   │   └── product-service.ts
//   └── index.ts

// src/models/user.ts
export interface User {
    id: string;
    name: string;
    email: string;
}

// src/services/user-service.ts
import { User } from "../models/user";

export class UserService {
    private users: User[] = [];
    
    addUser(user: User): void {
        this.users.push(user);
    }
    
    getUsers(): User[] {
        return this.users;
    }
}

// 当只修改 user-service.ts 时，增量编译只会重新编译该文件
// 而不会重新编译 user.ts（如果没有变化）
```

### 增量编译优化
```json
// 增量编译优化配置
{
  "compilerOptions": {
    "incremental": true,
    "tsBuildInfoFile": "./build-cache/.tsbuildinfo",
    "composite": true,
    "outDir": "./dist",
    "rootDir": "./src",
    
    // 性能优化选项
    "skipLibCheck": true,           // 跳过库文件检查
    "assumeChangesOnlyAffectDirectDependencies": true, // 假设更改只影响直接依赖
    
    // 并行编译
    "maxNodeModuleJsDepth": 0
  },
  
  "include": ["src/**/*"],
  
  "watchOptions": {
    "watchFile": "useFsEvents",     // 文件监视策略
    "watchDirectory": "useFsEvents", // 目录监视策略
    "fallbackPolling": "dynamicPriority",
    "synchronousWatchDirectory": true,
    "excludeDirectories": ["**/node_modules", "_build"]
  }
}
```

### 增量编译与 CI/CD
```bash
 CI/CD 中的增量编译
 1. 缓存 .tsbuildinfo 文件
 2. 只在源码改变时重新编译

 GitHub Actions 示例
name: Build
on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      
      - name: Cache build info
        uses: actions/cache@v2
        with:
          path: |
            **/dist/.tsbuildinfo
            **/.tsbuildinfo
          key: ${{ runner.os }}-ts-${{ hashFiles('**/tsconfig.json') }}
          
      - name: Install dependencies
        run: npm ci
        
      - name: Build with incremental compilation
        run: npx tsc --build --verbose
```

## 构建模式

### 基本构建模式配置
```json
// 开发环境配置 (tsconfig.dev.json)
{
  "extends": "./tsconfig.json",
  "compilerOptions": {
    "sourceMap": true,
    "inlineSourceMap": false,
    "noEmitOnError": false,
    "watch": true
  }
}

// 生产环境配置 (tsconfig.prod.json)
{
  "extends": "./tsconfig.json",
  "compilerOptions": {
    "sourceMap": false,
    "removeComments": true,
    "noEmitOnError": true,
    "outDir": "./dist/prod"
  }
}

// 测试环境配置 (tsconfig.test.json)
{
  "extends": "./tsconfig.json",
  "compilerOptions": {
    "sourceMap": true,
    "inlineSourceMap": true,
    "noEmitOnError": false,
    "types": ["jest", "node"]
  },
  "include": [
    "src/**/*",
    "tests/**/*"
  ]
}
```

### 多环境构建脚本
```json
{
  "scripts": {
    "build": "tsc --build",
    "build:dev": "tsc --build tsconfig.dev.json",
    "build:prod": "tsc --build tsconfig.prod.json",
    "build:test": "tsc --build tsconfig.test.json",
    "watch": "tsc --build --watch",
    "watch:dev": "tsc --build tsconfig.dev.json --watch",
    "clean": "tsc --build --clean"
  }
}
```

### 条件编译配置
```json
// 库开发配置 (tsconfig.lib.json)
{
  "compilerOptions": {
    "target": "ES2015",
    "module": "ES2015",
    "outDir": "./dist/lib",
    "declaration": true,
    "declarationMap": true,
    "sourceMap": true
  },
  "include": ["src/lib/**/*"]
}

// 应用配置 (tsconfig.app.json)
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "outDir": "./dist/app",
    "sourceMap": true
  },
  "include": ["src/app/**/*"],
  "references": [
    { "path": "./tsconfig.lib.json" }
  ]
}
```

### 构建性能优化
```json
// 高性能构建配置
{
  "compilerOptions": {
    "incremental": true,
    "composite": true,
    "tsBuildInfoFile": "./build-cache/.tsbuildinfo",
    
    // 并行编译
    "maxNodeModuleJsDepth": 0,
    
    // 类型检查优化
    "skipLibCheck": true,
    "skipDefaultLibCheck": true,
    
    // 内存优化
    "disableSizeLimit": false,
    "maxFileSize": 4194304,  // 4MB
    
    // 输出优化
    "importHelpers": true,
    "noEmitHelpers": false
  },
  
  "watchOptions": {
    "watchFile": "useFsEventsOnParentDirectory",
    "watchDirectory": "useFsEvents",
    "fallbackPolling": "dynamicPriority",
    "synchronousWatchDirectory": true
  }
}
```

## 路径映射

### 基本路径映射
```json
{
  "compilerOptions": {
    "baseUrl": "./src",
    "paths": {
      // 基本路径映射
      "@/*": ["./*"],
      "@components/*": ["./components/*"],
      "@utils/*": ["./utils/*"],
      "@models/*": ["./models/*"],
      "@services/*": ["./services/*"],
      
      // 多候选项路径映射
      "@shared/*": [
        "../shared/src/*",
        "./shared/*"
      ],
      
      // 具体文件映射
      "@config": ["./config/index"],
      "@logger": ["./utils/logger"],
      
      // 相对路径映射
      "shared/*": ["../shared/src/*"],
      "common/*": ["../../common/src/*"]
    }
  }
}
```

### 路径映射的实际应用
```typescript
// 项目结构
// src/
//   ├── components/
//   │   ├── Button.tsx
//   │   └── Header.tsx
//   ├── utils/
//   │   ├── helpers.ts
//   │   └── validators.ts
//   ├── models/
//   │   ├── User.ts
//   │   └── Product.ts
//   ├── services/
//   │   ├── UserService.ts
//   │   └── ProductService.ts
//   └── index.ts

// 使用路径映射导入
// src/components/Header.tsx
import { User } from '@models/User';
import { UserService } from '@services/UserService';
import { formatUserName } from '@utils/helpers';

// src/services/UserService.ts
import { User } from '@models/User';
import { validateEmail } from '@utils/validators';

// src/utils/helpers.ts
import { User } from '@models/User';

export function formatUserName(user: User): string {
    return `${user.name} (${user.email})`;
}
```

### 复杂路径映射配置
```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      // 多个项目路径映射
      "@app/*": ["src/app/*"],
      "@shared/*": ["src/shared/*"],
      "@ui/*": ["src/components/ui/*"],
      "@features/*": ["src/features/*"],
      
      // 第三方库别名
      "lodash": ["node_modules/lodash-es"],
      "react": ["node_modules/preact/compat"],
      
      // 版本控制路径
      "@api/v1/*": ["src/api/v1/*"],
      "@api/v2/*": ["src/api/v2/*"],
      
      // 环境特定路径
      "@env/config": [
        "src/config/production",
        "src/config/development"
      ],
      
      // 备用路径
      "@legacy/*": [
        "src/legacy/*",
        "../legacy/src/*"
      ]
    }
  }
}
```

### 路径映射与构建工具集成
```javascript
// webpack.config.js
const path = require('path');

module.exports = {
  resolve: {
    alias: {
      '@': path.resolve(__dirname, 'src'),
      '@components': path.resolve(__dirname, 'src/components'),
      '@utils': path.resolve(__dirname, 'src/utils'),
      '@models': path.resolve(__dirname, 'src/models'),
      '@services': path.resolve(__dirname, 'src/services')
    },
    extensions: ['.ts', '.tsx', '.js', '.jsx']
  }
};

// jest.config.js
module.exports = {
  moduleNameMapper: {
    '^@/(.*)$': '<rootDir>/src/$1',
    '^@components/(.*)$': '<rootDir>/src/components/$1',
    '^@utils/(.*)$': '<rootDir>/src/utils/$1',
    '^@models/(.*)$': '<rootDir>/src/models/$1',
    '^@services/(.*)$': '<rootDir>/src/services/$1'
  }
};
```

## 类型根目录

### 基本类型根目录配置
```json
{
  "compilerOptions": {
    "typeRoots": [
      "./node_modules/@types",    // 默认类型定义目录
      "./src/types",              // 自定义类型定义目录
      "./typings"                 // 另一个类型定义目录
    ],
    
    // 指定包含的具体类型包
    "types": [
      "node",
      "jest",
      "express",
      "webpack-env"
    ]
  }
}
```

### 自定义类型定义
```typescript
// src/types/custom.d.ts
// 全局类型声明
declare global {
    interface Window {
        myCustomProperty: string;
        myCustomFunction(): void;
    }
    
    interface Array<T> {
        groupBy<U>(keySelector: (item: T) => U): Map<U, T[]>;
    }
}

// 模块类型声明
declare module "my-custom-module" {
    export interface CustomConfig {
        apiUrl: string;
        timeout: number;
    }
    
    export function initialize(config: CustomConfig): void;
    export default function createInstance(): any;
}

// 环境变量类型声明
declare module "process" {
    global {
        namespace NodeJS {
            interface ProcessEnv {
                NODE_ENV: 'development' | 'production' | 'test';
                API_URL: string;
                DATABASE_URL: string;
            }
        }
    }
}
```

### 第三方库类型定义
```typescript
// src/types/third-party.d.ts
// 为没有类型定义的库添加声明
declare module "untyped-library" {
    export function doSomething(input: string): number;
    export class SomeClass {
        constructor(name: string);
        getName(): string;
    }
}

// 扩展现有类型
declare module "express" {
    interface Request {
        userId?: string;
        userRole?: string;
    }
}

// CSS 模块类型声明
declare module "*.css" {
    const content: { [className: string]: string };
    export default content;
}

declare module "*.scss" {
    const content: { [className: string]: string };
    export default content;
}

// 图片文件类型声明
declare module "*.png" {
    const value: string;
    export default value;
}

declare module "*.jpg" {
    const value: string;
    export default value;
}

declare module "*.svg" {
    const value: string;
    export default value;
}
```

### 类型根目录的最佳实践
```json
// 推荐的类型根目录结构
{
  "compilerOptions": {
    "typeRoots": [
      "./node_modules/@types",
      "./src/types/global",
      "./src/types/modules",
      "./src/types/custom"
    ],
    
    "types": [
      "node",
      "jest"
    ]
  }
}

// 目录结构
// src/
//   └── types/
//       ├── global/           // 全局类型声明
//       │   ├── index.d.ts
//       │   └── window.d.ts
//       ├── modules/          // 模块类型声明
//       │   ├── express.d.ts
//       │   └── custom-lib.d.ts
//       └── custom/           // 自定义类型
//           ├── api.d.ts
//           └── models.d.ts
```

### 类型定义文件组织
```typescript
// src/types/global/window.d.ts
declare global {
    interface Window {
        // 应用程序全局属性
        APP_VERSION: string;
        APP_CONFIG: {
            apiUrl: string;
            debug: boolean;
        };
        
        // 第三方库全局对象
        ga: Function;  // Google Analytics
        fbq: Function; // Facebook Pixel
    }
}

export {}; // 确保这是一个模块

// src/types/modules/express.d.ts
import { Request } from 'express';

declare module 'express' {
    interface Request {
        // 扩展 Express Request 对象
        userId?: string;
        userRole?: 'admin' | 'user' | 'guest';
        correlationId: string;
    }
}

// src/types/custom/api.d.ts
// 自定义 API 响应类型
declare namespace API {
    interface SuccessResponse<T> {
        success: true;
         T;
        timestamp: string;
    }
    
    interface ErrorResponse {
        success: false;
        error: string;
        code: number;
        timestamp: string;
    }
    
    type ApiResponse<T> = SuccessResponse<T> | ErrorResponse;
}

// 使用自定义类型
// src/services/user-service.ts
async function fetchUser(id: string): Promise<API.ApiResponse<User>> {
    try {
        const response = await fetch(`/api/users/${id}`);
        const data = await response.json();
        return {
            success: true,
             data,
            timestamp: new Date().toISOString()
        };
    } catch (error) {
        return {
            success: false,
            error: error.message,
            code: 500,
            timestamp: new Date().toISOString()
        };
    }
}
```


# 12. 实用工具类型

## Partial<T>

### 基本用法
```typescript
// Partial<T> 将类型 T 的所有属性变为可选
interface User {
    id: string;
    name: string;
    email: string;
    age: number;
}

// 使用 Partial 创建可选属性的类型
type PartialUser = Partial<User>;

// 等价于：
// interface PartialUser {
//     id?: string;
//     name?: string;
//     email?: string;
//     age?: number;
// }

// 实际应用
function updateUser(id: string, updates: PartialUser): void {
    console.log(`Updating user ${id} with:`, updates);
}

// 可以只提供部分属性
updateUser("123", { name: "Alice" }); // 只更新名字
updateUser("123", { email: "alice@example.com", age: 30 }); // 更新邮箱和年龄
```

### 高级用法
```typescript
// 深度 Partial（递归可选）
type DeepPartial<T> = {
    [P in keyof T]?: T[P] extends object ? DeepPartial<T[P]> : T[P];
};

interface Address {
    street: string;
    city: string;
    zipCode: number;
}

interface UserWithAddress {
    id: string;
    name: string;
    address: Address;
}

type DeepPartialUser = DeepPartial<UserWithAddress>;

// 使用深度 Partial
let partialUser: DeepPartialUser = {
    name: "Alice",
    address: {
        city: "New York" // 只需要部分地址信息
    }
};

// 嵌套 Partial
type NestedPartial<T> = T extends object ? {
    [P in keyof T]?: NestedPartial<T[P]>;
} : T;

// 实际应用：配置对象
interface AppConfig {
    apiUrl: string;
    timeout: number;
    retries: number;
    debug: boolean;
}

function createApp(config: Partial<AppConfig> = {}): AppConfig {
    return {
        apiUrl: config.apiUrl || "https://api.example.com",
        timeout: config.timeout || 5000,
        retries: config.retries || 3,
        debug: config.debug || false
    };
}

let app1 = createApp(); // 使用默认配置
let app2 = createApp({ debug: true, timeout: 10000 }); // 自定义部分配置
```

## Required<T>

### 基本用法
```typescript
// Required<T> 将类型 T 的所有属性变为必需
interface UserOptional {
    id?: string;
    name?: string;
    email?: string;
    age?: number;
}

// 使用 Required 创建必需属性的类型
type RequiredUser = Required<UserOptional>;

// 等价于：
// interface RequiredUser {
//     id: string;
//     name: string;
//     email: string;
//     age: number;
// }

// 实际应用
function validateUser(user: RequiredUser): boolean {
    return user.id.length > 0 && 
           user.name.length > 0 && 
           user.email.length > 0 && 
           user.age > 0;
}

// 从可选对象创建必需对象
let optionalUser: UserOptional = {
    id: "123",
    name: "Alice"
    // email 和 age 是可选的
};

// 需要确保所有属性都存在
let requiredUser: RequiredUser = {
    id: optionalUser.id!,
    name: optionalUser.name!,
    email: optionalUser.email || "",
    age: optionalUser.age || 0
};
```

### 高级用法
```typescript
// 深度 Required（递归必需）
type DeepRequired<T> = {
    [P in keyof T]-?: T[P] extends object ? DeepRequired<T[P]> : T[P];
};

interface OptionalUserWithAddress {
    id?: string;
    name?: string;
    address?: {
        street?: string;
        city?: string;
        zipCode?: number;
    };
}

type DeepRequiredUser = DeepRequired<OptionalUserWithAddress>;

// 使用深度 Required
let requiredUserWithAddress: DeepRequiredUser = {
    id: "123",
    name: "Alice",
    address: {
        street: "123 Main St",
        city: "New York",
        zipCode: 10001
    }
};

// 条件 Required
type ConditionalRequired<T, K extends keyof T> = T & Required<Pick<T, K>>;

interface PartialConfig {
    host?: string;
    port?: number;
    username?: string;
    password?: string;
}

// 要求 host 和 port 必需
type RequiredHostPort = ConditionalRequired<PartialConfig, "host" | "port">;

let config: RequiredHostPort = {
    host: "localhost",  // 必需
    port: 3000,         // 必需
    username: "admin",  // 可选
    password: "secret"  // 可选
};
```

## Readonly<T>

### 基本用法
```typescript
// Readonly<T> 将类型 T 的所有属性变为只读
interface UserMutable {
    id: string;
    name: string;
    email: string;
    age: number;
}

// 使用 Readonly 创建只读类型
type ReadonlyUser = Readonly<UserMutable>;

// 等价于：
// interface ReadonlyUser {
//     readonly id: string;
//     readonly name: string;
//     readonly email: string;
//     readonly age: number;
// }

// 实际应用
function processUser(user: ReadonlyUser): string {
    // 可以读取属性
    console.log(`Processing user: ${user.name}`);
    
    // 不能修改属性
    // user.name = "New Name"; // 错误！
    
    return `Processed: ${user.name} (${user.email})`;
}

let user: UserMutable = {
    id: "123",
    name: "Alice",
    email: "alice@example.com",
    age: 30
};

let readonlyUser: ReadonlyUser = user; // 可以赋值
console.log(processUser(readonlyUser));
```

### 高级用法
```typescript
// 深度 Readonly（递归只读）
type DeepReadonly<T> = {
    readonly [P in keyof T]: T[P] extends object ? DeepReadonly<T[P]> : T[P];
};

interface UserWithNestedData {
    id: string;
    name: string;
    preferences: {
        theme: string;
        language: string;
        notifications: {
            email: boolean;
            push: boolean;
        };
    };
}

type DeepReadonlyUser = DeepReadonly<UserWithNestedData>;

// 使用深度 Readonly
let readonlyUserWithNested: DeepReadonlyUser = {
    id: "123",
    name: "Alice",
    preferences: {
        theme: "dark",
        language: "en",
        notifications: {
            email: true,
            push: false
        }
    }
};

// 不能修改任何属性
// readonlyUserWithNested.id = "456"; // 错误！
// readonlyUserWithNested.preferences.theme = "light"; // 错误！
// readonlyUserWithNested.preferences.notifications.email = false; // 错误！
```

## Record<K,T>

### 基本用法
```typescript
// Record<K,T> 创建一个对象类型，其键为 K，值为 T
type UserRoles = "admin" | "user" | "guest";
type UserRolePermissions = Record<UserRoles, string[]>;

// 等价于：
// type UserRolePermissions = {
//     admin: string[];
//     user: string[];
//     guest: string[];
// }

// 实际应用
const permissions: UserRolePermissions = {
    admin: ["read", "write", "delete", "manage_users"],
    user: ["read", "write"],
    guest: ["read"]
};

// 字符串键的 Record
type StringRecord = Record<string, number>;
let scores: StringRecord = {
    "Alice": 95,
    "Bob": 87,
    "Charlie": 92
};

// 数字键的 Record
type NumberRecord = Record<number, string>;
let monthNames: NumberRecord = {
    1: "January",
    2: "February",
    3: "March"
    // ...
};
```

### 高级用法
```typescript
// Record 与映射类型结合
type ApiResponse<T> = Record<"success" | "data" | "error" | "timestamp", any> & {
    success: boolean;
     T;
    error?: string;
    timestamp: Date;
};

// 动态 Record
type DynamicRecord<T> = Record<string, T>;

function createRecord<T>(keys: string[], value: T): DynamicRecord<T> {
    const record: DynamicRecord<T> = {};
    keys.forEach(key => {
        record[key] = value;
    });
    return record;
}

let booleanFlags = createRecord(["debug", "verbose", "silent"], false);
// { debug: false, verbose: false, silent: false }

// 类型安全的配置对象
type ConfigKeys = "host" | "port" | "database" | "username";
type ConfigValues = string | number;
type AppConfig = Record<ConfigKeys, ConfigValues>;

let config: AppConfig = {
    host: "localhost",
    port: 5432,
    database: "myapp",
    username: "admin"
};

// 嵌套 Record
type NestedRecord<K extends string | number | symbol, T> = Record<K, Record<string, T>>;

type UserPreferences = NestedRecord<"theme" | "layout", string | boolean>;

let preferences: UserPreferences = {
    theme: {
        color: "dark",
        fontSize: "medium"
    },
    layout: {
        sidebar: true,
        navbar: false
    }
};
```

## Pick<T,K>

### 基本用法
```typescript
// Pick<T,K> 从类型 T 中选择属性 K
interface UserFull {
    id: string;
    name: string;
    email: string;
    age: number;
    password: string;
    createdAt: Date;
    updatedAt: Date;
}

// 选择特定属性
type UserPublicInfo = Pick<UserFull, "id" | "name" | "email">;

// 等价于：
// interface UserPublicInfo {
//     id: string;
//     name: string;
//     email: string;
// }

// 实际应用
function getUserPublicInfo(user: UserFull): UserPublicInfo {
    return {
        id: user.id,
        name: user.name,
        email: user.email
    };
}

// 选择方法属性
interface ApiClient {
    get(url: string): Promise<any>;
    post(url: string, data: any): Promise<any>;
    put(url: string, data: any): Promise<any>;
    delete(url: string): Promise<any>;
    authenticate(token: string): void;
    logout(): void;
}

type ReadOperations = Pick<ApiClient, "get">;
type WriteOperations = Pick<ApiClient, "post" | "put" | "delete">;
type AuthOperations = Pick<ApiClient, "authenticate" | "logout">;
```

### 高级用法
```typescript
// 动态 Pick
type PickByType<T, U> = {
    [K in keyof T as T[K] extends U ? K : never]: T[K]
};

interface MixedTypes {
    name: string;
    age: number;
    isActive: boolean;
    score: number;
    email: string;
}

type StringProperties = PickByType<MixedTypes, string>;
// { name: string; email: string; }

type NumberProperties = PickByType<MixedTypes, number>;
// { age: number; score: number; }

type BooleanProperties = PickByType<MixedTypes, boolean>;
// { isActive: boolean; }

// 条件 Pick
type ConditionalPick<T, U> = Pick<T, {
    [K in keyof T]: T[K] extends U ? K : never
}[keyof T]>;

// 从对象数组中 Pick
interface Product {
    id: string;
    name: string;
    price: number;
    category: string;
    inStock: boolean;
}

type ProductSummary = Pick<Product, "id" | "name" | "price">;

function getProductSummaries(products: Product[]): ProductSummary[] {
    return products.map(product => ({
        id: product.id,
        name: product.name,
        price: product.price
    }));
}

// Pick 与泛型结合
function pickProperties<T, K extends keyof T>(obj: T, keys: K[]): Pick<T, K> {
    const result = {} as Pick<T, K>;
    keys.forEach(key => {
        result[key] = obj[key];
    });
    return result;
}

let user: UserFull = {
    id: "123",
    name: "Alice",
    email: "alice@example.com",
    age: 30,
    password: "secret",
    createdAt: new Date(),
    updatedAt: new Date()
};

let publicInfo = pickProperties(user, ["id", "name", "email"]);
// 类型为 Pick<UserFull, "id" | "name" | "email">
```

## Omit<T,K>

### 基本用法
```typescript
// Omit<T,K> 从类型 T 中排除属性 K
interface UserComplete {
    id: string;
    name: string;
    email: string;
    password: string;
    ssn: string;
    creditCard: string;
    createdAt: Date;
    updatedAt: Date;
}

// 排除敏感信息
type UserSafe = Omit<UserComplete, "password" | "ssn" | "creditCard">;

// 等价于：
// interface UserSafe {
//     id: string;
//     name: string;
//     email: string;
//     createdAt: Date;
//     updatedAt: Date;
// }

// 实际应用
function sanitizeUser(user: UserComplete): UserSafe {
    const { password, ssn, creditCard, ...safeUser } = user;
    return safeUser;
}

// 排除方法
interface DatabaseConnection {
    connect(): Promise<void>;
    disconnect(): Promise<void>;
    query(sql: string): Promise<any>;
    execute(sql: string): Promise<any>;
    getConnectionInfo(): string;
    getPassword(): string; // 敏感方法
    setPassword(password: string): void; // 敏感方法
}

type SafeDatabaseConnection = Omit<DatabaseConnection, "getPassword" | "setPassword">;

// 排除多个属性
type UserWithoutTimestamps = Omit<UserComplete, "createdAt" | "updatedAt">;
type UserBasicInfo = Omit<UserComplete, "password" | "ssn" | "creditCard" | "createdAt" | "updatedAt">;
```

### 高级用法
```typescript
// 动态 Omit
type OmitByType<T, U> = {
    [K in keyof T as T[K] extends U ? never : K]: T[K]
};

interface MixedData {
    name: string;
    age: number;
    email: string;
    password: string;
    callback: () => void;
    data: any;
}

type WithoutFunctions = OmitByType<MixedData, Function>;
// { name: string; age: number; email: string; password: string; data: any; }

type WithoutStrings = OmitByType<MixedData, string>;
// { age: number; callback: () => void; data: any; }

// 条件 Omit
type ConditionalOmit<T, U> = Omit<T, {
    [K in keyof T]: T[K] extends U ? K : never
}[keyof T]>;

// 递归 Omit
type DeepOmit<T, K extends string> = {
    [P in keyof T as P extends K ? never : P]: T[P] extends object ? DeepOmit<T[P], K> : T[P];
};

interface NestedUser {
    id: string;
    name: string;
    profile: {
        email: string;
        password: string;
        settings: {
            theme: string;
            password: string; // 嵌套的敏感信息
        };
    };
}

type SafeNestedUser = DeepOmit<NestedUser, "password">;
// 递归移除所有 password 属性

// Omit 与 Pick 组合
type UserPublicProfile = Pick<Omit<UserComplete, "password" | "ssn" | "creditCard">, "id" | "name" | "email">;
```

## Exclude<T,U>

### 基本用法
```typescript
// Exclude<T,U> 从类型 T 中排除可分配给 U 的类型
type Status = "pending" | "approved" | "rejected" | "draft";
type ActiveStatus = Exclude<Status, "draft">;

// ActiveStatus = "pending" | "approved" | "rejected"

// 排除数字类型
type Numbers = 1 | 2 | 3 | 4 | 5;
type EvenNumbers = Exclude<Numbers, 1 | 3 | 5>;

// EvenNumbers = 2 | 4

// 排除字符串类型
type Colors = "red" | "green" | "blue" | "yellow" | "purple";
type PrimaryColors = Exclude<Colors, "yellow" | "purple">;

// PrimaryColors = "red" | "green" | "blue"

// 实际应用
interface Task {
    id: string;
    title: string;
    status: Status;
    assignee?: string;
}

function updateTaskStatus(task: Task, newStatus: Exclude<Status, "draft">): void {
    task.status = newStatus;
}

let task: Task = {
    id: "123",
    title: "Implement feature",
    status: "pending"
};

// updateTaskStatus(task, "draft"); // 错误！"draft" 被排除了
updateTaskStatus(task, "approved"); // 正确
```

### 高级用法
```typescript
// Exclude 与联合类型
type Primitive = string | number | boolean | null | undefined;
type NonNullablePrimitive = Exclude<Primitive, null | undefined>;

// NonNullablePrimitive = string | number | boolean

// Exclude 与字符串字面量类型
type HttpMethod = "GET" | "POST" | "PUT" | "DELETE" | "PATCH" | "HEAD" | "OPTIONS";
type MutatingMethods = Exclude<HttpMethod, "GET" | "HEAD" | "OPTIONS">;

// MutatingMethods = "POST" | "PUT" | "DELETE" | "PATCH"

// 实际应用：API 客户端
class ApiClient {
    async request<T>(
        method: Exclude<HttpMethod, "HEAD" | "OPTIONS">,
        url: string,
        data?: any
    ): Promise<T> {
        // 实现请求逻辑
        return {} as T;
    }
}

// Exclude 与泛型
type Diff<T, U> = T extends U ? never : T;

type Letters = "a" | "b" | "c" | "d" | "e";
type Vowels = "a" | "e";
type Consonants = Diff<Letters, Vowels>;

// Consonants = "b" | "c" | "d"

// 条件 Exclude
type ConditionalExclude<T, U> = T extends U ? never : T;

// 排除特定模式的字符串
type RoutePaths = "/users" | "/users/:id" | "/admin" | "/admin/settings" | "/api/*";
type PublicRoutes = Exclude<RoutePaths, "/admin" | "/admin/settings">;

// PublicRoutes = "/users" | "/users/:id" | "/api/*"
```

## Extract<T,U>

### 基本用法
```typescript
// Extract<T,U> 从类型 T 中提取可分配给 U 的类型
type Status2 = "pending" | "approved" | "rejected" | "draft";
type CompletedStatus = Extract<Status2, "approved" | "rejected">;

// CompletedStatus = "approved" | "rejected"

// 提取数字类型
type Numbers2 = 1 | 2 | 3 | 4 | 5;
type OddNumbers = Extract<Numbers2, 1 | 3 | 5>;

// OddNumbers = 1 | 3 | 5

// 提取字符串类型
type Colors2 = "red" | "green" | "blue" | "yellow" | "purple";
type WarmColors = Extract<Colors2, "red" | "yellow" | "orange">;

// WarmColors = "red" | "yellow" (orange 不在原联合类型中)

// 实际应用
interface Order {
    id: string;
    status: Status2;
    total: number;
}

function processCompletedOrders(orders: Order[]): Order[] {
    return orders.filter(order => 
        Extract<Status2, "approved" | "rejected">(order.status as any)
    );
}

// 更好的实现方式
function isCompletedStatus(status: Status2): status is Extract<Status2, "approved" | "rejected"> {
    return status === "approved" || status === "rejected";
}

function processCompletedOrders2(orders: Order[]): Order[] {
    return orders.filter(order => isCompletedStatus(order.status));
}
```

### 高级用法
```typescript
// Extract 与字符串操作
type FileExtensions = ".js" | ".ts" | ".jsx" | ".tsx" | ".css" | ".scss";
type TypeScriptExtensions = Extract<FileExtensions, ".ts" | ".tsx">;

// TypeScriptExtensions = ".ts" | ".tsx"

// 提取函数类型
type MixedTypes2 = string | number | (() => void) | ((x: number) => string);
type FunctionTypes = Extract<MixedTypes2, Function>;

// FunctionTypes = (() => void) | ((x: number) => string)

// 实际应用：类型守卫
function isFunctionType<T>(value: T): value is Extract<T, Function> {
    return typeof value === "function";
}

// Extract 与条件类型
type Filter<T, U> = T extends U ? T : never;

type StringOrNumber = string | number | boolean;
type StringTypes = Filter<StringOrNumber, string>;

// StringTypes = string

// 提取特定属性名
type StringKeys<T> = Extract<keyof T, string>;

interface MixedKeys {
    name: string;
    0: number;
    [Symbol.iterator]: () => Iterator<any>;
}

type StringKeyNames = StringKeys<MixedKeys>;
// StringKeyNames = "name"
```

## NonNullable<T>

### 基本用法
```typescript
// NonNullable<T> 从类型 T 中排除 null 和 undefined
type NullableString = string | null | undefined;
type NonNullString = NonNullable<NullableString>;

// NonNullString = string

type MixedNullable = string | number | null | undefined;
type NonNullMixed = NonNullable<MixedNullable>;

// NonNullMixed = string | number

// 实际应用
function processString(value: NullableString): string {
    // 需要类型守卫
    if (value === null || value === undefined) {
        return "default";
    }
    
    // 现在 value 是 string 类型
    return value.toUpperCase();
}

// 使用 NonNullable 简化类型
function processString2(value: NonNullable<NullableString>): string {
    // value 已经是非空的
    return value.toUpperCase();
}

// 处理数组中的可空值
type NullableArray = (string | null | undefined)[];
type NonNullArray = NonNullable<NullableArray>[number][];

// NonNullArray = string[]

function filterNonNull(array: NullableArray): string[] {
    return array.filter((item): item is NonNullable<typeof item> => 
        item !== null && item !== undefined
    ) as string[];
}
```

### 高级用法
```typescript
// NonNullable 与泛型
function compact<T>(array: T[]): NonNullable<T>[] {
    return array.filter((item): item is NonNullable<T> => 
        item !== null && item !== undefined
    ) as NonNullable<T>[];
}

let mixedArray = ["hello", null, "world", undefined, 42, null];
let compacted = compact(mixedArray); // (string | number)[]

// NonNullable 与对象属性
interface UserWithOptionalFields {
    id: string;
    name: string;
    email: string | null;
    phone: string | undefined;
    address: string | null | undefined;
}

type RequiredUserFields = {
    [K in keyof UserWithOptionalFields]: NonNullable<UserWithOptionalFields[K]>
};

// RequiredUserFields = {
//     id: string;
//     name: string;
//     email: string;
//     phone: string;
//     address: string;
// }

// 实际应用：数据库查询结果处理
interface DatabaseResult {
    id: number;
    name: string | null;
    email: string | null;
    created_at: string;
}

function sanitizeDatabaseResult(result: DatabaseResult): NonNullable<DatabaseResult> {
    return {
        id: result.id,
        name: result.name || "Unknown",
        email: result.email || "no-email@example.com",
        created_at: result.created_at
    };
}
```

## Parameters<T>

### 基本用法
```typescript
// Parameters<T> 获取函数类型 T 的参数类型
type Func = (name: string, age: number, isActive: boolean) => void;
type FuncParams = Parameters<Func>;

// FuncParams = [string, number, boolean]

// 实际应用
function createUser(name: string, age: number, email: string): { id: string; name: string; age: number; email: string } {
    return {
        id: Math.random().toString(36),
        name,
        age,
        email
    };
}

type CreateUserParams = Parameters<typeof createUser>;
// CreateUserParams = [string, number, string]

function callWithParams<T extends (...args: any[]) => any>(
    func: T,
    params: Parameters<T>
): ReturnType<T> {
    return func(...params);
}

let user = callWithParams(createUser, ["Alice", 30, "alice@example.com"]);

// 获取特定参数类型
type FirstParam<T> = Parameters<T>[0];
type SecondParam<T> = Parameters<T>[1];

type CreateUserFirstParam = FirstParam<typeof createUser>; // string
type CreateUserSecondParam = SecondParam<typeof createUser>; // number
```

### 高级用法
```typescript
// Parameters 与构造函数
class UserClass {
    constructor(
        public name: string,
        public age: number,
        public email?: string
    ) {}
}

type UserConstructorParams = Parameters<typeof UserClass>;
// UserConstructorParams = [string, number, (string | undefined)?]

// Parameters 与泛型函数
function genericFunc<T>(value: T, transform: (val: T) => string): string {
    return transform(value);
}

type GenericFuncParams = Parameters<typeof genericFunc>;
// GenericFuncParams = [unknown, (val: unknown) => string]

// 实际应用：函数参数验证
function validateFunctionParams<T extends (...args: any[]) => any>(
    func: T,
    ...args: Parameters<T>
): boolean {
    // 参数验证逻辑
    console.log(`Function called with ${args.length} arguments`);
    return args.length === func.length;
}

// Parameters 与重载函数
interface OverloadedFunc {
    (x: number): number;
    (x: string): string;
    (x: boolean): boolean;
}

// 注意：Parameters 只能获取最后一个重载签名的参数
type OverloadedParams = Parameters<OverloadedFunc>;
// OverloadedParams = [boolean]
```

## ConstructorParameters<T>

### 基本用法
```typescript
// ConstructorParameters<T> 获取构造函数类型 T 的参数类型
class DatabaseConnection {
    constructor(
        public host: string,
        public port: number,
        public username: string,
        public password?: string
    ) {}
}

type ConnectionParams = ConstructorParameters<typeof DatabaseConnection>;
// ConnectionParams = [string, number, string, (string | undefined)?]

// 实际应用
function createConnection(
    ...args: ConstructorParameters<typeof DatabaseConnection>
): DatabaseConnection {
    return new DatabaseConnection(...args);
}

let connection1 = createConnection("localhost", 5432, "admin", "secret");
let connection2 = createConnection("localhost", 5432, "admin"); // 可选参数

// 与类工厂函数结合
class User {
    constructor(
        public id: string,
        public name: string,
        public email: string
    ) {}
}

function createUserFactory<T extends new (...args: any[]) => any>(
    Constructor: T,
    ...args: ConstructorParameters<T>
): InstanceType<T> {
    return new Constructor(...args);
}

let user = createUserFactory(User, "123", "Alice", "alice@example.com");
```

### 高级用法
```typescript
// ConstructorParameters 与抽象类
abstract class BaseRepository<T> {
    constructor(
        protected tableName: string,
        protected primaryKey: string = "id"
    ) {}
}

class UserRepository extends BaseRepository<User> {
    constructor(tableName: string = "users") {
        super(tableName);
    }
}

type BaseRepoParams = ConstructorParameters<typeof BaseRepository>;
// BaseRepoParams = [string, string?]

type UserRepoParams = ConstructorParameters<typeof UserRepository>;
// UserRepoParams = [string?] (因为有默认参数)

// ConstructorParameters 与泛型类
class GenericRepository<T> {
    constructor(
        private entityType: new () => T,
        private tableName: string
    ) {}
}

type GenericRepoParams = ConstructorParameters<typeof GenericRepository>;
// GenericRepoParams = [new () => unknown, string]

// 实际应用：依赖注入容器
interface Injectable {
    new (...args: any[]): any;
}

class Container {
    private services = new Map<any, any>();
    
    register<T extends Injectable>(
        token: T,
        ...args: ConstructorParameters<T>
    ): void {
        this.services.set(token, args);
    }
    
    resolve<T extends Injectable>(token: T): InstanceType<T> {
        const args = this.services.get(token) || [];
        return new token(...args);
    }
}

// 使用示例
class Logger {
    constructor(private level: string = "info") {}
}

class Database {
    constructor(private connectionString: string) {}
}

let container = new Container();
container.register(Logger, "debug");
container.register(Database, "postgresql://localhost:5432/mydb");
```

## ReturnType<T>

### 基本用法
```typescript
// ReturnType<T> 获取函数类型 T 的返回类型
function getUser(id: string): { id: string; name: string; email: string } {
    return {
        id,
        name: "Default User",
        email: "default@example.com"
    };
}

type GetUserReturnType = ReturnType<typeof getUser>;
// GetUserReturnType = { id: string; name: string; email: string }

// 实际应用
async function fetchUserData(id: string): Promise<{ id: string; name: string; email: string }> {
    // 模拟 API 调用
    return {
        id,
        name: "Fetched User",
        email: "fetched@example.com"
    };
}

type FetchUserReturnType = ReturnType<typeof fetchUserData>;
// FetchUserReturnType = Promise<{ id: string; name: string; email: string }>

type FetchUserResolvedType = Awaited<FetchUserReturnType>;
// FetchUserResolvedType = { id: string; name: string; email: string }

// 与泛型函数结合
function identity<T>(value: T): T {
    return value;
}

type IdentityReturnType = ReturnType<typeof identity>;
// IdentityReturnType = unknown (因为 T 是泛型参数)

// 实际应用：API 响应处理
interface ApiResponse<T> {
    success: boolean;
     T;
    message?: string;
}

async function apiCall<T>(endpoint: string): Promise<ApiResponse<T>> {
    // 实现 API 调用
    return {
        success: true,
         data: {} as T
    };
}

type ApiCallReturnType<T> = ReturnType<typeof apiCall<T>>;
// ApiCallReturnType<T> = Promise<ApiResponse<T>>
```

### 高级用法
```typescript
// ReturnType 与重载函数
function processValue(value: string): string;
function processValue(value: number): number;
function processValue(value: boolean): boolean;
function processValue(value: string | number | boolean): string | number | boolean {
    return value;
}

type ProcessValueReturnType = ReturnType<typeof processValue>;
// ProcessValueReturnType = boolean (最后一个重载签名的返回类型)

// ReturnType 与条件类型结合
type Unpromisify<T> = T extends Promise<infer U> ? U : T;

function asyncFunction(): Promise<string> {
    return Promise.resolve("hello");
}

type AsyncFunctionReturnType = ReturnType<typeof asyncFunction>;
// AsyncFunctionReturnType = Promise<string>

type UnpromisifiedReturnType = Unpromisify<ReturnType<typeof asyncFunction>>;
// UnpromisifiedReturnType = string

// 实际应用：函数结果缓存
class ResultCache {
    private cache = new Map<string, any>();
    
    getCachedResult<T extends (...args: any[]) => any>(
        key: string,
        func: T,
        ...args: Parameters<T>
    ): ReturnType<T> {
        if (this.cache.has(key)) {
            return this.cache.get(key);
        }
        
        const result = func(...args);
        this.cache.set(key, result);
        return result;
    }
}

let cache = new ResultCache();
let result = cache.getCachedResult("user-123", getUser, "123");
// result 的类型是 ReturnType<typeof getUser>
```

## InstanceType<T>

### 基本用法
```typescript
// InstanceType<T> 获取构造函数类型 T 的实例类型
class User2 {
    constructor(
        public id: string,
        public name: string,
        public email: string
    ) {}
    
    greet(): string {
        return `Hello, ${this.name}!`;
    }
}

type UserInstance = InstanceType<typeof User2>;
// UserInstance = User2

// 实际应用
function createInstance<T extends new (...args: any[]) => any>(
    Constructor: T,
    ...args: ConstructorParameters<T>
): InstanceType<T> {
    return new Constructor(...args);
}

let user = createInstance(User2, "123", "Alice", "alice@example.com");
// user 的类型是 User2

// 与抽象类结合
abstract class BaseRepository2<T> {
    abstract findById(id: string): T | null;
    abstract save(entity: T): void;
}

class UserRepository2 extends BaseRepository2<User2> {
    findById(id: string): User2 | null {
        return new User2(id, "Default", "default@example.com");
    }
    
    save(entity: User2): void {
        console.log(`Saving user ${entity.id}`);
    }
}

type RepositoryInstance<T extends typeof BaseRepository2> = InstanceType<T>;

// 实际应用：工厂模式
interface IProduct {
    name: string;
    price: number;
}

class Book implements IProduct {
    constructor(public name: string, public price: number, public author: string) {}
}

class Electronics implements IProduct {
    constructor(public name: string, public price: number, public brand: string) {}
}

type ProductConstructors = typeof Book | typeof Electronics;
type ProductInstance = InstanceType<ProductConstructors>;

function createProduct<T extends ProductConstructors>(
    Constructor: T,
    ...args: ConstructorParameters<T>
): InstanceType<T> {
    return new Constructor(...args);
}

let book = createProduct(Book, "TypeScript Guide", 29.99, "John Doe");
let electronics = createProduct(Electronics, "Laptop", 999.99, "TechCorp");
```

### 高级用法
```typescript
// InstanceType 与泛型类
class GenericService<T> {
    constructor(private data: T[]) {}
    
    find(predicate: (item: T) => boolean): T | undefined {
        return this.data.find(predicate);
    }
    
    add(item: T): void {
        this.data.push(item);
    }
}

type ServiceInstance<T> = InstanceType<typeof GenericService<T>>;
// 注意：这种方式在实际使用中有限制

// 实际应用：依赖注入容器改进版
class DIContainer {
    private services = new Map<any, { constructor: any; args: any[] }>();
    
    register<T extends new (...args: any[]) => any>(
        token: T,
        ...args: ConstructorParameters<T>
    ): void {
        this.services.set(token, { constructor: token, args });
    }
    
    resolve<T extends new (...args: any[]) => any>(token: T): InstanceType<T> {
        const serviceInfo = this.services.get(token);
        if (!serviceInfo) {
            throw new Error(`Service ${token.name} not registered`);
        }
        
        return new serviceInfo.constructor(...serviceInfo.args);
    }
    
    // 批量解析
    resolveAll<T extends (new (...args: any[]) => any)[]>(
        tokens: [...T]
    ): { [K in keyof T]: InstanceType<T[K]> } {
        return tokens.map(token => this.resolve(token)) as any;
    }
}

// 使用示例
class Logger2 {
    constructor(private level: string = "info") {}
    log(message: string) { console.log(`[${this.level}] ${message}`); }
}

class Database2 {
    constructor(private connectionString: string) {}
    connect() { console.log(`Connecting to ${this.connectionString}`); }
}

let container = new DIContainer();
container.register(Logger2, "debug");
container.register(Database2, "postgresql://localhost:5432/mydb");

let logger = container.resolve(Logger2);
let database = container.resolve(Database2);

// 批量解析
let [logger2, database2] = container.resolveAll([Logger2, Database2]);
```

## ThisParameterType<T>

### 基本用法
```typescript
// ThisParameterType<T> 提取函数类型 T 的 this 参数类型
interface User3 {
    id: string;
    name: string;
}

function getUserInfo(this: User3): string {
    return `${this.name} (${this.id})`;
}

type UserInfoThisType = ThisParameterType<typeof getUserInfo>;
// UserInfoThisType = User3

// 实际应用
class UserService3 {
    private users: User3[] = [];
    
    addUser(this: UserService3, user: User3): void {
        this.users.push(user);
    }
    
    findUser(this: UserService3, id: string): User3 | undefined {
        return this.users.find(u => u.id === id);
    }
}

type AddUserThisType = ThisParameterType<UserService3['addUser']>;
// AddUserThisType = UserService3

type FindUserThisType = ThisParameterType<UserService3['findUser']>;
// FindUserThisType = UserService3

// 与 bind 结合使用
let service = new UserService3();
let boundAddUser = service.addUser.bind(service);

type BoundAddUserThisType = ThisParameterType<typeof boundAddUser>;
// BoundAddUserThisType = UserService3
```

### 高级用法
```typescript
// ThisParameterType 与方法装饰器
function logMethodCalls<T>(
    target: T,
    methodName: string,
    descriptor: TypedPropertyDescriptor<(...args: any[]) => any>
): void {
    const originalMethod = descriptor.value;
    
    if (originalMethod) {
        descriptor.value = function (...args: any[]) {
            const thisType = ThisParameterType<typeof originalMethod>;
            console.log(`Calling ${methodName} on ${target.constructor.name}`);
            return originalMethod.apply(this, args);
        };
    }
}

// ThisParameterType 与事件处理器
interface Component {
    state: any;
    update(): void;
}

function handleClick(this: Component, event: MouseEvent): void {
    console.log('Component clicked');
    this.update();
}

type ComponentClickHandler = ThisParameterType<typeof handleClick>;
// ComponentClickHandler = Component

// 实际应用：类型安全的事件绑定
class EventManager {
    bind<T extends (this: any, ...args: any[]) => any>(
        element: HTMLElement,
        event: string,
        handler: T,
        context: ThisParameterType<T>
    ): void {
        element.addEventListener(event, handler.bind(context));
    }
}

let manager = new EventManager();
let component: Component = {
    state: {},
    update() { console.log('Component updated'); }
};

// manager.bind(button, 'click', handleClick, component);
```

## OmitThisParameter<T>

### 基本用法
```typescript
// OmitThisParameter<T> 移除函数类型 T 的 this 参数
interface User4 {
    id: string;
    name: string;
}

function getUserDetails(this: User4): { id: string; name: string; greeting: string } {
    return {
        id: this.id,
        name: this.name,
        greeting: `Hello, ${this.name}!`
    };
}

type UserDetailsFunction = OmitThisParameter<typeof getUserDetails>;
// UserDetailsFunction = () => { id: string; name: string; greeting: string }

// 实际应用
class UserProfile {
    constructor(public user: User4) {}
    
    // 移除 this 参数的方法
    getDetails = (): ReturnType<typeof getUserDetails> => {
        return getUserDetails.call(this.user);
    }
}

// 使用 bind 移除 this 参数
let user: User4 = { id: "123", name: "Alice" };
let boundGetUserDetails = getUserDetails.bind(user) as UserDetailsFunction;

let details = boundGetUserDetails(); // 不需要 this 参数
console.log(details); // { id: "123", name: "Alice", greeting: "Hello, Alice!" }

// 与箭头函数结合
class UserService4 {
    private currentUser: User4;
    
    constructor(user: User4) {
        this.currentUser = user;
    }
    
    // 创建不依赖 this 的函数
    createPublicProfile(): OmitThisParameter<typeof this.formatUser> {
        return this.formatUser.bind(this.currentUser) as OmitThisParameter<typeof this.formatUser>;
    }
    
    private formatUser(this: User4): string {
        return `${this.name} (${this.id})`;
    }
}
```

### 高级用法
```typescript
// OmitThisParameter 与高阶函数
function withUserContext<T extends (this: User4, ...args: any[]) => any>(
    fn: T
): (...args: Parameters<OmitThisParameter<T>>) => ReturnType<T> {
    return function (...args: Parameters<OmitThisParameter<T>>): ReturnType<T> {
        // 这里需要提供 this 上下文
        throw new Error('This context required');
    };
}

// 实际应用：函数组合
class DataProcessor {
    private context: any;
    
    constructor(context: any) {
        this.context = context;
    }
    
    pipe<T extends (this: any, ...args: any[]) => any>(
        ...functions: T[]
    ): (...args: Parameters<OmitThisParameter<T>>) => ReturnType<T> {
        return (...args: any[]) => {
            return functions.reduce((result, fn) => {
                const boundFn = fn.bind(this.context) as OmitThisParameter<T>;
                return (boundFn as any)(result);
            }, args[0]);
        };
    }
}

// OmitThisParameter 与事件系统
interface EventHandler<T> {
    (this: T, event: Event): void;
}

type EventListener<T> = OmitThisParameter<EventHandler<T>>;

class EventSystem<T> {
    private handlers: EventListener<T>[] = [];
    
    addHandler(handler: EventHandler<T>): void {
        const listener = handler.bind(null) as EventListener<T>; // 需要实际的上下文
        this.handlers.push(listener);
    }
    
    trigger(event: Event): void {
        this.handlers.forEach(handler => handler(event));
    }
}
```

## ThisType<T>

### 基本用法
```typescript
// ThisType<T> 为对象字面量提供 this 类型
// 需要在 tsconfig.json 中设置 "noImplicitThis": true

interface User5 {
    name: string;
    age: number;
}

interface UserMethods {
    getName(): string;
    getAge(): number;
    greet(): string;
}

let userObject: User5 & ThisType<User5 & UserMethods> = {
    name: "Alice",
    age: 30,
    
    getName() {
        return this.name; // this 的类型是 User5 & UserMethods
    },
    
    getAge() {
        return this.age; // this 的类型是 User5 & UserMethods
    },
    
    greet() {
        return `Hello, ${this.getName()}! You are ${this.getAge()} years old.`;
    }
};

console.log(userObject.greet()); // "Hello, Alice! You are 30 years old."
```

### 高级用法
```typescript
// ThisType 与 fluent API
interface Calculator {
    value: number;
    add(x: number): this;
    multiply(x: number): this;
    subtract(x: number): this;
    divide(x: number): this;
    result(): number;
}

let calculator: Calculator & ThisType<Calculator> = {
    value: 0,
    
    add(x: number) {
        this.value += x;
        return this; // this 的类型是 Calculator
    },
    
    multiply(x: number) {
        this.value *= x;
        return this;
    },
    
    subtract(x: number) {
        this.value -= x;
        return this;
    },
    
    divide(x: number) {
        this.value /= x;
        return this;
    },
    
    result() {
        return this.value;
    }
};

let result = calculator.add(5).multiply(2).subtract(3).divide(2).result();
console.log(result); // 3.5

// ThisType 与配置对象
interface ConfigBuilder<T> {
    set<K extends keyof T>(key: K, value: T[K]): this;
    get<K extends keyof T>(key: K): T[K];
    build(): T;
}

interface AppConfig {
    host: string;
    port: number;
    debug: boolean;
}

let configBuilder: ConfigBuilder<AppConfig> & ThisType<ConfigBuilder<AppConfig>> = {
    host: "localhost",
    port: 3000,
    debug: false,
    
    set(key, value) {
        this[key] = value;
        return this;
    },
    
    get(key) {
        return this[key];
    },
    
    build() {
        return {
            host: this.host,
            port: this.port,
            debug: this.debug
        };
    }
};

let config = configBuilder.set("host", "0.0.0.0").set("port", 8080).build();
console.log(config); // { host: "0.0.0.0", port: 8080, debug: false }

// ThisType 与插件系统
interface PluginAPI {
    register(name: string, handler: Function): void;
    execute(name: string, ...args: any[]): any;
}

interface PluginContext {
    api: PluginAPI;
    config: any;
    utils: {
        log(message: string): void;
        error(error: string): void;
    };
}

let pluginContext: PluginContext & ThisType<PluginContext> = {
    api: {
        register(name: string, handler: Function) { /* ... */ },
        execute(name: string, ...args: any[]) { /* ... */ }
    },
    
    config: {},
    
    utils: {
        log(message: string) {
            console.log(`[LOG] ${message}`);
        },
        
        error(error: string) {
            console.error(`[ERROR] ${error}`);
        }
    },
    
    // 插件方法可以访问 this
    initialize() {
        this.utils.log("Plugin initialized");
        this.api.register("test", () => "Hello from plugin");
    }
};
```


# 13. 类型操作

## keyof 操作符

### 基本用法
```typescript
// keyof 操作符获取对象类型的所有键名
interface User {
    id: string;
    name: string;
    email: string;
    age: number;
}

// 获取所有键名的联合类型
type UserKeys = keyof User;
// UserKeys = "id" | "name" | "email" | "age"

// 实际应用
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
    return obj[key];
}

let user: User = {
    id: "123",
    name: "Alice",
    email: "alice@example.com",
    age: 30
};

let userName = getProperty(user, "name"); // string 类型
let userAge = getProperty(user, "age");   // number 类型
// let invalid = getProperty(user, "invalid"); // 编译错误

// keyof 与索引签名
interface Dictionary {
    [key: string]: any;
}

type DictKeys = keyof Dictionary;
// DictKeys = string | number (因为数字键会转换为字符串)

// keyof 与数字索引
interface NumericArray {
    [index: number]: string;
}

type NumericKeys = keyof NumericArray;
// NumericKeys = number | "length" | "toString" | "toLocaleString" | "push" | ...
```

### 高级用法
```typescript
// keyof 与泛型约束
function pluck<T, K extends keyof T>(array: T[], key: K): T[K][] {
    return array.map(item => item[key]);
}

let users: User[] = [
    { id: "1", name: "Alice", email: "alice@example.com", age: 30 },
    { id: "2", name: "Bob", email: "bob@example.com", age: 25 }
];

let names = pluck(users, "name"); // string[]
let ages = pluck(users, "age");   // number[]

// keyof 与条件类型
type FunctionPropertyNames<T> = {
    [K in keyof T]: T[K] extends Function ? K : never
}[keyof T];

type NonFunctionPropertyNames<T> = {
    [K in keyof T]: T[K] extends Function ? never : K
}[keyof T];

interface SampleObject {
    name: string;
    age: number;
    greet(): string;
    calculate(x: number, y: number): number;
}

type FuncProps = FunctionPropertyNames<SampleObject>;     // "greet" | "calculate"
type NonFuncProps = NonFunctionPropertyNames<SampleObject>; // "name" | "age"

// keyof 与映射类型
type Partial<T> = {
    [P in keyof T]?: T[P];
};

type Required<T> = {
    [P in keyof T]-?: T[P];
};

type Readonly<T> = {
    readonly [P in keyof T]: T[P];
};

// 实际应用：类型安全的对象操作
class ObjectUtils {
    static hasKey<T extends object>(obj: T, key: keyof any): key is keyof T {
        return key in obj;
    }
    
    static getKeys<T extends object>(obj: T): (keyof T)[] {
        return Object.keys(obj) as (keyof T)[];
    }
    
    static pick<T extends object, K extends keyof T>(obj: T, keys: K[]): Pick<T, K> {
        const result = {} as Pick<T, K>;
        keys.forEach(key => {
            if (key in obj) {
                result[key] = obj[key];
            }
        });
        return result;
    }
}
```

## typeof 操作符

### 基本用法
```typescript
// typeof 操作符获取值的类型
let str = "hello";
let num = 42;
let bool = true;
let arr = [1, 2, 3];
let obj = { name: "Alice", age: 30 };

type StrType = typeof str;    // string
type NumType = typeof num;    // number
type BoolType = typeof bool;  // boolean
type ArrType = typeof arr;    // number[]
type ObjType = typeof obj;    // { name: string; age: number }

// typeof 与函数
function greet(name: string): string {
    return `Hello, ${name}!`;
}

type GreetType = typeof greet; // (name: string) => string

// typeof 与类
class Person {
    constructor(public name: string, public age: number) {}
    
    greet(): string {
        return `Hello, I'm ${this.name}`;
    }
}

type PersonType = typeof Person; // new (name: string, age: number) => Person
type PersonInstanceType = InstanceType<typeof Person>; // Person

// typeof 与枚举
enum Direction {
    Up,
    Down,
    Left,
    Right
}

type DirectionType = typeof Direction;
// DirectionType = {
//     Up: Direction.Up;
//     Down: Direction.Down;
//     Left: Direction.Left;
//     Right: Direction.Right;
//     0: "Up";
//     1: "Down";
//     2: "Left";
//     3: "Right";
// }
```

### 高级用法
```typescript
// typeof 与模块
import * as fs from "fs";

type FsType = typeof fs;
// 包含 fs 模块的所有导出类型

// typeof 与命名空间
namespace MathUtils {
    export function add(a: number, b: number): number {
        return a + b;
    }
    
    export const PI = 3.14159;
}

type MathUtilsType = typeof MathUtils;
// {
//     add: (a: number, b: number) => number;
//     PI: number;
// }

// typeof 与条件类型
type NonUndefined<T> = T extends undefined ? never : T;

function getValue<T>(obj: T): typeof obj extends undefined ? never : T {
    if (obj === undefined) {
        throw new Error("Value is undefined");
    }
    return obj;
}

// typeof 与类型推断
function createPerson(name: string, age: number) {
    return {
        name,
        age,
        greet() {
            return `Hello, I'm ${this.name}`;
        }
    };
}

type PersonReturnType = typeof createPerson;
// (name: string, age: number) => { name: string; age: number; greet(): string }

type PersonObjectType = ReturnType<typeof createPerson>;
// { name: string; age: number; greet(): string }

// 实际应用：运行时类型检查
const VALID_STATUS = ["pending", "approved", "rejected"] as const;
type Status = typeof VALID_STATUS[number]; // "pending" | "approved" | "rejected"

function isValidStatus(status: string): status is Status {
    return (VALID_STATUS as readonly string[]).includes(status);
}

// typeof 与配置对象
const APP_CONFIG = {
    apiUrl: "https://api.example.com",
    timeout: 5000,
    retries: 3,
    debug: false
} as const;

type AppConfig = typeof APP_CONFIG;
// {
//     readonly apiUrl: "https://api.example.com";
//     readonly timeout: 5000;
//     readonly retries: 3;
//     readonly debug: false;
// }

// 使用配置类型
function createApiClient(config: typeof APP_CONFIG) {
    // config 的类型是精确的字面量类型
    console.log(`API URL: ${config.apiUrl}`);
    console.log(`Timeout: ${config.timeout}ms`);
}
```

## 索引访问类型

### 基本用法
```typescript
// 索引访问类型 T[K] 获取对象类型 T 中键 K 对应的类型
interface User {
    id: string;
    name: string;
    email: string;
    age: number;
}

type UserIdType = User["id"];     // string
type UserNameType = User["name"]; // string
type UserAgeType = User["age"];   // number

// 联合索引访问
type UserStringFields = User["name" | "email"]; // string
type UserPrimitiveFields = User["id" | "name" | "age"]; // string | number

// 索引访问与 keyof 结合
type AllUserFieldTypes = User[keyof User]; // string | number

// 索引访问与数组
type ArrayElementType<T> = T extends (infer U)[] ? U : T;

let numbers = [1, 2, 3, 4, 5];
type NumberArrayType = typeof numbers;        // number[]
type NumberType = NumberArrayType[number];    // number
type NumberType2 = typeof numbers[number];    // number

// 索引访问与元组
let tuple = ["hello", 42, true] as const;
type TupleType = typeof tuple;                // readonly ["hello", 42, true]
type FirstElementType = TupleType[0];         // "hello"
type SecondElementType = TupleType[1];        // 42
type ThirdElementType = TupleType[2];         // true
```

### 高级用法
```typescript
// 索引访问与泛型
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
    return obj[key];
}

// 索引访问与条件类型
type Flatten<T> = T extends any[] ? T[number] : T;

type StringArray = string[];
type FlattenedString = Flatten<StringArray>; // string

type NumberOrString = number | string;
type FlattenedUnion = Flatten<NumberOrString>; // number | string

// 索引访问与映射类型
type Getters<T> = {
    [K in keyof T as `get${Capitalize<string & K>}`]: () => T[K]
};

interface Person {
    name: string;
    age: number;
}

type PersonGetters = Getters<Person>;
// {
//     getName: () => string;
//     getAge: () => number;
// }

// 索引访问与递归类型
type DeepIndex<T, K extends string> = 
    K extends `${infer Head}.${infer Tail}` 
        ? Head extends keyof T 
            ? T[Head] extends object 
                ? DeepIndex<T[Head], Tail>
                : never
            : never
        : K extends keyof T 
            ? T[K]
            : never;

interface NestedObject {
    user: {
        profile: {
            name: string;
            age: number;
        };
        settings: {
            theme: string;
        };
    };
}

type UserName = DeepIndex<NestedObject, "user.profile.name">; // string
type UserTheme = DeepIndex<NestedObject, "user.settings.theme">; // string

// 实际应用：类型安全的状态管理
interface AppState {
    user: {
        id: string;
        name: string;
        preferences: {
            theme: "light" | "dark";
            language: string;
        };
    };
    ui: {
        loading: boolean;
        error: string | null;
    };
}

// 创建类型安全的选择器
function createSelector<T, K extends string>(
    state: T,
    path: K
): DeepIndex<T, K> {
    // 实现略
    return null as any;
}

// 使用示例
// let userName = createSelector(appState, "user.name"); // string
// let theme = createSelector(appState, "user.preferences.theme"); // "light" | "dark"
```

## 映射类型修饰符

### 基本修饰符
```typescript
// 映射类型修饰符
// +? 可选，-? 必需，+readonly 只读，-readonly 可写

// 可选修饰符
type Partial<T> = {
    [P in keyof T]+?: T[P]; // +? 是默认行为
};

type Required<T> = {
    [P in keyof T]-?: T[P]; // -? 移除可选性
};

interface UserOptional {
    id?: string;
    name?: string;
    email?: string;
    age?: number;
}

type UserRequired = Required<UserOptional>;
// {
//     id: string;
//     name: string;
//     email: string;
//     age: number;
// }

// 只读修饰符
type Readonly<T> = {
    +readonly [P in keyof T]: T[P]; // +readonly 是默认行为
};

type Mutable<T> = {
    -readonly [P in keyof T]: T[P]; // -readonly 移除只读性
};

interface ReadOnlyUser {
    readonly id: string;
    readonly name: string;
    readonly email: string;
}

type MutableUser = Mutable<ReadOnlyUser>;
// {
//     id: string;
//     name: string;
//     email: string;
// }
```

### 高级修饰符用法
```typescript
// 组合修饰符
type Complete<T> = {
    [P in keyof T]-?: T[P]; // 移除可选性
};

type DeepReadonly<T> = T extends object
    ? { readonly [P in keyof T]: DeepReadonly<T[P]> }
    : T;

type DeepMutable<T> = T extends object
    ? { -readonly [P in keyof T]: DeepMutable<T[P]> }
    : T;

interface NestedObject {
    name: string;
    details: {
        age: number;
        address: {
            street: string;
            city: string;
        };
    };
}

type ReadonlyNested = DeepReadonly<NestedObject>;
// 所有层级都是只读的

type MutableNested = DeepMutable<ReadonlyNested>;
// 所有层级都是可变的

// 条件修饰符
type ConditionalReadonly<T, K extends keyof T> = {
    readonly [P in K]: T[P];
} & {
    [P in Exclude<keyof T, K>]: T[P];
};

interface Config {
    host: string;
    port: number;
    debug: boolean;
    apiKey: string;
}

type SecureConfig = ConditionalReadonly<Config, "apiKey">;
// apiKey 是只读的，其他属性是可变的

// 映射类型与模板字面量结合
type Getters<T> = {
    [K in keyof T as `get${Capitalize<string & K>}`]: () => T[K];
};

type Setters<T> = {
    [K in keyof T as `set${Capitalize<string & K>}`]: (value: T[K]) => void;
};

interface Person2 {
    name: string;
    age: number;
}

type PersonAccessors = Getters<Person2> & Setters<Person2>;
// {
//     getName: () => string;
//     getAge: () => number;
//     setName: (value: string) => void;
//     setAge: (value: number) => void;
// }
```

### 实际应用
```typescript
// 实际应用：创建配置对象的只读版本
type DeepPartial<T> = {
    [P in keyof T]?: T[P] extends object ? DeepPartial<T[P]> : T[P];
};

type DeepRequired<T> = {
    [P in keyof T]-?: T[P] extends object ? DeepRequired<T[P]> : T[P];
};

interface AppConfig {
    server: {
        host: string;
        port: number;
        ssl?: {
            enabled: boolean;
            certPath?: string;
        };
    };
    database: {
        host: string;
        port: number;
        name: string;
    };
}

type PartialConfig = DeepPartial<AppConfig>;
type RequiredConfig = DeepRequired<AppConfig>;

// 创建配置工厂
function createConfig(partial: PartialConfig): RequiredConfig {
    return {
        server: {
            host: partial.server?.host || "localhost",
            port: partial.server?.port || 3000,
            ssl: {
                enabled: partial.server?.ssl?.enabled || false,
                certPath: partial.server?.ssl?.certPath || ""
            }
        },
        database: {
            host: partial.database?.host || "localhost",
            port: partial.database?.port || 5432,
            name: partial.database?.name || "myapp"
        }
    };
}

// 实际应用：创建响应式对象
type Reactive<T> = {
    [P in keyof T]: {
        value: T[P];
        subscribe(callback: (newValue: T[P]) => void): void;
        unsubscribe(callback: (newValue: T[P]) => void): void;
    }
};

interface UserFormData {
    name: string;
    email: string;
    age: number;
}

type ReactiveUserForm = Reactive<UserFormData>;
// 每个属性都变成了响应式对象
```

## 模板字面量类型

### 基本用法
```typescript
// 模板字面量类型（TypeScript 4.1+）
type World = "world";
type Greeting = `hello ${World}`; // "hello world"

// 与联合类型结合
type EmailLocaleIDs = "welcome_email" | "email_heading";
type FooterLocaleIDs = "footer_title" | "footer_sendoff";

type AllLocaleIDs = `${EmailLocaleIDs | FooterLocaleIDs}_id`;
// "welcome_email_id" | "email_heading_id" | "footer_title_id" | "footer_sendoff_id"

// 实际应用：生成事件名称
type EventName = "click" | "hover" | "focus";
type EventHandlerName = `on${Capitalize<EventName>}`;
// "onClick" | "onHover" | "onFocus"

// 与字符串操作类型结合
type Capitalize<S extends string> = S extends `${infer First}${infer Rest}` 
    ? `${Uppercase<First>}${Rest}` 
    : S;

type Uncapitalize<S extends string> = S extends `${infer First}${infer Rest}` 
    ? `${Lowercase<First>}${Rest}` 
    : S;

type HelloWorld = Capitalize<"hello world">; // "Hello world"
type HelloWorld2 = Uncapitalize<"Hello World">; // "hello World"
```

### 高级用法
```typescript
// 字符串操作类型
type Uppercase<S extends string> = intrinsic; // 内置类型
type Lowercase<S extends string> = intrinsic;
type Capitalize<S extends string> = intrinsic;
type Uncapitalize<S extends string> = intrinsic;

// 实际应用：生成 CSS 类名
type Size = "small" | "medium" | "large";
type Variant = "primary" | "secondary" | "danger";
type ClassName = `btn-${Size}-${Variant}`;
// "btn-small-primary" | "btn-small-secondary" | "btn-small-danger" | ...

// 实际应用：生成 API 端点
type Resource = "users" | "posts" | "comments";
type Action = "get" | "create" | "update" | "delete";
type ApiEndpoint = `/${Resource}/${Action}`;
// "/users/get" | "/users/create" | "/users/update" | "/users/delete" | ...

// 实际应用：生成状态类型
type Status = "pending" | "fulfilled" | "rejected";
type AsyncStatus<T> = `${T}_${Status}`;
type UserStatus = AsyncStatus<"user">;
// "user_pending" | "user_fulfilled" | "user_rejected"

// 与泛型结合
type Prefixed<T extends string, Prefix extends string> = `${Prefix}${Capitalize<T>}`;

type UserFields = "name" | "email" | "age";
type UserGetters = Prefixed<UserFields, "get">;
// "getName" | "getEmail" | "getAge"

type UserSetters = Prefixed<UserFields, "set">;
// "setName" | "setEmail" | "setAge"
```

### 复杂模板字面量类型
```typescript
// 复杂模板字面量类型
type Join<T extends string[], D extends string> = 
    T extends [infer F extends string, ...infer R extends string[]]
        ? R extends []
            ? F
            : `${F}${D}${Join<R, D>}`
        : "";

type Path = Join<["users", "123", "posts"], "/">; // "users/123/posts"

// 实际应用：生成文件路径
type FileExtension = ".js" | ".ts" | ".jsx" | ".tsx";
type FileName<T extends string> = `${T}${FileExtension}`;

type ComponentName = "Button" | "Header" | "Footer";
type ComponentFiles = FileName<ComponentName>;
// "Button.js" | "Button.ts" | "Button.jsx" | "Button.tsx" | ...

// 实际应用：生成环境变量名称
type EnvPrefix = "REACT_APP_" | "NEXT_PUBLIC_";
type EnvName<T extends string> = `${EnvPrefix}${Uppercase<T>}`;

type ConfigKeys = "apiUrl" | "apiKey" | "debug";
type EnvVariables = EnvName<ConfigKeys>;
// "REACT_APP_APIURL" | "REACT_APP_APIKEY" | "REACT_APP_DEBUG" | ...

// 实际应用：生成 CSS 变量名
type CSSVarName<T extends string> = `--${KebabCase<T>}`;

type KebabCase<S extends string> = S extends `${infer T}${infer U}`
    ? U extends Uncapitalize<U>
        ? `${Lowercase<T>}${KebabCase<U>}`
        : `${Lowercase<T>}-${KebabCase<U>}`
    : S;

type ThemeKeys = "primaryColor" | "secondaryColor" | "fontSize";
type CSSVariables = CSSVarName<ThemeKeys>;
// "--primary-color" | "--secondary-color" | "--font-size"
```

## 字符串字面量类型操作

### 基本字符串操作
```typescript
// 字符串字面量类型操作
// 分割字符串
type Split<S extends string, D extends string> = 
    S extends `${infer T}${D}${infer U}` ? [T, ...Split<U, D>] : [S];

type PathSegments = Split<"users/123/posts/456", "/">;
// ["users", "123", "posts", "456"]

type CommaSeparated = Split<"a,b,c,d", ",">;
// ["a", "b", "c", "d"]

// 替换字符串
type Replace<S extends string, From extends string, To extends string> = 
    S extends `${infer Before}${From}${infer After}`
        ? `${Before}${To}${After}`
        : S;

type Replaced = Replace<"hello world", "world", "TypeScript">;
// "hello TypeScript"

// 重复字符串
type Repeat<S extends string, N extends number, Acc extends string = ""> = 
    N extends 0 ? Acc : Repeat<S, MinusOne<N>, `${Acc}${S}`>;

type MinusOne<N extends number> = 
    N extends 0 ? 0 : 
    N extends 1 ? 0 :
    N extends 2 ? 1 :
    // ... 实际实现更复杂
    any;

type Repeated = Repeat<"a", 3>; // "aaa"

// 字符串长度
type StringLength<S extends string> = 
    S extends `${infer First}${infer Rest}` 
        ? Add<StringLength<Rest>, 1>
        : 0;

type Add<A extends number, B extends number> = any; // 内置实现

type Length = StringLength<"hello">; // 5
```

### 高级字符串操作
```typescript
// 高级字符串操作
// 驼峰命名转换
type CamelCase<S extends string> = 
    S extends `${infer First}-${infer Rest}`
        ? `${First}${Capitalize<CamelCase<Rest>>}`
        : S;

type CamelCased = CamelCase<"hello-world-example">;
// "helloWorldExample"

// 帕斯卡命名转换
type PascalCase<S extends string> = Capitalize<CamelCase<S>>;

type PascalCased = PascalCase<"hello-world-example">;
// "HelloWorldExample"

// 蛇形命名转换
type SnakeCase<S extends string> = 
    S extends `${infer T}${infer U}`
        ? U extends Uncapitalize<U>
            ? `${Lowercase<T>}${SnakeCase<U>}`
            : `${Lowercase<T>}_${SnakeCase<U>}`
        : S;

type Snaked = SnakeCase<"helloWorldExample">;
// "hello_world_example"

// 实际应用：生成类型安全的路由参数
type RoutePath = "/users/:id/posts/:postId";
type RouteParams<T extends string> = 
    T extends `${infer Before}:${infer Param}/${infer After}`
        ? Param | RouteParams<`/${After}`>
        : T extends `${infer Before}:${infer Param}`
            ? Param
            : never;

type UserPostParams = RouteParams<"/users/:id/posts/:postId">;
// "id" | "postId"

// 实际应用：生成表单验证规则
type FormField<T extends string> = 
    T extends `${infer Name}Required` 
        ? { [K in Name]: string }
        : T extends `${infer Name}Optional`
            ? { [K in Name]?: string }
            : never;

type RequiredField = FormField<"emailRequired">;
// { email: string }

type OptionalField = FormField<"phoneOptional">;
// { phone?: string }
```

### 实际应用场景
```typescript
// 实际应用：类型安全的 CSS 类名生成器
type Size = "small" | "medium" | "large";
type Variant = "primary" | "secondary" | "danger";
type State = "normal" | "hover" | "active" | "disabled";

type ButtonClass = `btn-${Size}-${Variant}${State extends "normal" ? "" : `-${State}`}`;

// 更智能的类名生成
type ButtonClassBuilder<
    S extends Size = "medium",
    V extends Variant = "primary",
    ST extends State = "normal"
> = `btn-${S}-${V}${ST extends "normal" ? "" : `-${ST}`}`;

// 实际应用：API 端点类型安全
type HttpMethod = "GET" | "POST" | "PUT" | "DELETE";
type ApiEndpoint<
    Method extends HttpMethod,
    Path extends string
> = `${Method} ${Path}`;

type UserEndpoints = 
    | ApiEndpoint<"GET", "/users">
    | ApiEndpoint<"GET", "/users/:id">
    | ApiEndpoint<"POST", "/users">
    | ApiEndpoint<"PUT", "/users/:id">
    | ApiEndpoint<"DELETE", "/users/:id">;

// 实际应用：环境变量类型安全
type EnvVar<T extends string> = `REACT_APP_${Uppercase<T>}`;

type ConfigKey = "apiUrl" | "apiKey" | "debugMode";
type EnvVars = {
    [K in ConfigKey as EnvVar<K>]: string;
};

// EnvVars = {
//     "REACT_APP_APIURL": string;
//     "REACT_APP_APIKEY": string;
//     "REACT_APP_DEBUGMODE": string;
// }

// 实际应用：生成类型安全的事件处理器名称
type EventName = "click" | "hover" | "focus" | "blur";
type EventHandlerName<T extends EventName> = `on${Capitalize<T>}`;

type ComponentEvents = {
    [K in EventName as EventHandlerName<K>]?: (event: any) => void;
};

// ComponentEvents = {
//     onClick?: (event: any) => void;
//     onHover?: (event: any) => void;
//     onFocus?: (event: any) => void;
//     onBlur?: (event: any) => void;
// }

// 实际应用：数据库表名和字段名生成
type TableName<T extends string> = `${Lowercase<T>}Table`;
type ColumnName<T extends string> = `${SnakeCase<T>}_column`;

type UserTable = TableName<"User">; // "userTable"
type UserNameColumn = ColumnName<"userName">; // "user_name_column"

// 实际应用：生成类型安全的 Redux action 类型
type ActionType<Entity extends string, Operation extends string> = 
    `@@app/${Lowercase<Entity>}/${Lowercase<Operation>}`;

type UserActionTypes = 
    | ActionType<"User", "FETCH">
    | ActionType<"User", "CREATE">
    | ActionType<"User", "UPDATE">
    | ActionType<"User", "DELETE">;

// "@@app/user/fetch" | "@@app/user/create" | "@@app/user/update" | "@@app/user/delete"
```


# 14. 声明文件

## .d.ts 文件

### 基本概念
```typescript
// .d.ts 文件是 TypeScript 声明文件
// 它们包含类型信息但不包含实际的实现代码
// 用于为 JavaScript 库提供类型定义

// 命名约定
// my-library.d.ts - 为 my-library 提供类型定义
// index.d.ts - 包含目录的类型定义
// global.d.ts - 全局类型声明

// 基本 .d.ts 文件结构
// my-library.d.ts
declare module "my-library" {
    export interface User {
        id: string;
        name: string;
        email: string;
    }
    
    export class UserService {
        static getUser(id: string): User;
        static createUser(user: Omit<User, 'id'>): User;
    }
    
    export default UserService;
}

// 使用声明文件
// 在 TypeScript 代码中
import UserService, { User } from "my-library";

const user: User = UserService.getUser("123");
```

### 编写声明文件
```typescript
// 为现有 JavaScript 库编写声明文件
// example-library.js
/*
export function add(a, b) {
    return a + b;
}

export class Calculator {
    constructor(initialValue = 0) {
        this.value = initialValue;
    }
    
    add(x) {
        this.value += x;
        return this;
    }
    
    getValue() {
        return this.value;
    }
}
*/

// example-library.d.ts
declare module "example-library" {
    // 函数声明
    export function add(a: number, b: number): number;
    
    // 类声明
    export class Calculator {
        constructor(initialValue?: number);
        value: number;
        add(x: number): this;
        getValue(): number;
    }
    
    // 默认导出
    export default Calculator;
}

// 复杂声明文件示例
// complex-library.d.ts
declare module "complex-library" {
    // 命名空间
    export namespace Utils {
        export function formatDate(date: Date): string;
        export function parseDate(dateString: string): Date;
    }
    
    // 接口
    export interface Config {
        apiUrl: string;
        timeout: number;
        retries: number;
        debug?: boolean;
    }
    
    // 类型别名
    export type Status = "pending" | "fulfilled" | "rejected";
    
    // 泛型函数
    export function fetch<T>(url: string, config?: Partial<Config>): Promise<T>;
    
    // 枚举
    export enum LogLevel {
        DEBUG = 0,
        INFO = 1,
        WARN = 2,
        ERROR = 3
    }
    
    // 类
    export class Logger {
        constructor(level: LogLevel);
        log(message: string, level?: LogLevel): void;
        debug(message: string): void;
        info(message: string): void;
        warn(message: string): void;
        error(message: string): void;
    }
    
    // 默认导出
    export default Logger;
}
```

### 发布声明文件
```typescript
// package.json 配置
{
    "name": "my-awesome-library",
    "version": "1.0.0",
    "main": "dist/index.js",
    "types": "dist/index.d.ts",  // 指定声明文件位置
    "files": [
        "dist/**/*"
    ],
    "devDependencies": {
        "typescript": "^4.0.0"
    },
    "scripts": {
        "build": "tsc",
        "prepublishOnly": "npm run build"
    }
}

// tsconfig.json 配置
{
    "compilerOptions": {
        "target": "ES2015",
        "module": "commonjs",
        "declaration": true,        // 生成 .d.ts 文件
        "declarationMap": true,     // 生成 .d.ts.map 文件
        "outDir": "./dist",
        "rootDir": "./src"
    },
    "include": ["src/**/*"]
}

// 目录结构
// my-awesome-library/
// ├── src/
// │   ├── index.ts
// │   ├── user.ts
// │   └── utils.ts
// ├── dist/
// │   ├── index.js
// │   ├── index.d.ts
// │   ├── user.js
// │   ├── user.d.ts
// │   ├── utils.js
// │   └── utils.d.ts
// ├── package.json
// └── tsconfig.json
```

## 全局声明

### 基本全局声明
```typescript
// global.d.ts - 全局类型声明文件
// 全局变量声明
declare var GLOBAL_CONFIG: {
    apiUrl: string;
    version: string;
    debug: boolean;
};

// 全局函数声明
declare function log(message: string): void;
declare function alert(message: string): void;

// 全局类声明
declare class GlobalLogger {
    static log(message: string): void;
    static error(error: string): void;
}

// 全局接口声明
interface Window {
    myCustomProperty: string;
    myCustomFunction(): void;
}

// 使用全局声明
console.log(GLOBAL_CONFIG.apiUrl);
log("Hello world");
GlobalLogger.log("Global message");

// 在代码中扩展全局对象
window.myCustomProperty = "Hello";
window.myCustomFunction = () => {
    console.log("Custom function called");
};
```

### 扩展内置类型
```typescript
// 扩展全局类型
// global-extensions.d.ts
declare global {
    // 扩展 Array 接口
    interface Array<T> {
        groupBy<K>(keySelector: (item: T) => K): Map<K, T[]>;
        distinct(): T[];
        shuffle(): T[];
    }
    
    // 扩展 String 接口
    interface String {
        capitalize(): string;
        kebabCase(): string;
        camelCase(): string;
    }
    
    // 扩展 Number 接口
    interface Number {
        toCurrency(currency?: string): string;
        format(digits?: number): string;
    }
    
    // 扩展 Window 接口
    interface Window {
        $: any;  // jQuery
        ga: Function;  // Google Analytics
        fbq: Function; // Facebook Pixel
    }
    
    // 全局类型别名
    type JSONObject = { [key: string]: any };
    type JSONArray = JSONObject[];
    type JSONValue = string | number | boolean | null | JSONObject | JSONArray;
}

// 实现扩展方法（在实际的 .ts 文件中）
// array-extensions.ts
Array.prototype.groupBy = function<T, K>(keySelector: (item: T) => K): Map<K, T[]> {
    const map = new Map<K, T[]>();
    this.forEach(item => {
        const key = keySelector(item);
        if (!map.has(key)) {
            map.set(key, []);
        }
        map.get(key)!.push(item);
    });
    return map;
};

Array.prototype.distinct = function<T>(): T[] {
    return [...new Set(this)];
};

// string-extensions.ts
String.prototype.capitalize = function(): string {
    return this.charAt(0).toUpperCase() + this.slice(1);
};

String.prototype.kebabCase = function(): string {
    return this.replace(/([a-z])([A-Z])/g, '$1-$2').toLowerCase();
};
```

### 环境特定的全局声明
```typescript
// 开发环境全局声明
// global.dev.d.ts
declare global {
    interface Window {
        __DEV__: boolean;
        __REDUX_DEVTOOLS_EXTENSION__: any;
        __REACT_DEVTOOLS_GLOBAL_HOOK__: any;
    }
}

// 生产环境全局声明
// global.prod.d.ts
declare global {
    interface Window {
        __DEV__: undefined;
        // 生产环境不包含开发工具
    }
}

// Node.js 环境全局声明
// node-global.d.ts
declare global {
    namespace NodeJS {
        interface ProcessEnv {
            NODE_ENV: 'development' | 'production' | 'test';
            PORT?: string;
            DATABASE_URL: string;
            API_KEY: string;
        }
        
        interface Global {
            myGlobalVar: any;
        }
    }
}

// 浏览器环境全局声明
// browser-global.d.ts
declare global {
    interface Navigator {
        readonly connection?: NetworkInformation;
        readonly battery?: BatteryManager;
    }
    
    interface NetworkInformation {
        readonly effectiveType: 'slow-2g' | '2g' | '3g' | '4g';
        readonly downlink: number;
        readonly rtt: number;
    }
}
```

## 模块声明

### 基本模块声明
```typescript
// 模块声明语法
// module-declarations.d.ts
declare module "my-module" {
    export interface User {
        id: string;
        name: string;
        email: string;
    }
    
    export function getUser(id: string): User;
    export function createUser(user: Omit<User, 'id'>): User;
    
    const VERSION: string;
    export { VERSION };
    
    export default function main(): void;
}

// 声明带有通配符的模块
declare module "*.css" {
    const content: { [className: string]: string };
    export default content;
}

declare module "*.scss" {
    const content: { [className: string]: string };
    export default content;
}

declare module "*.png" {
    const value: string;
    export default value;
}

declare module "*.jpg" {
    const value: string;
    export default value;
}

declare module "*.svg" {
    const value: string;
    export default value;
}

declare module "*.json" {
    const value: any;
    export default value;
}

// 使用模块声明
// app.ts
import styles from "./App.module.css";
import logo from "./logo.png";
import data from "./data.json";

console.log(styles.container);
console.log(logo);
console.log(data);
```

### 复杂模块声明
```typescript
// 复杂模块声明示例
// react-component.d.ts
declare module "react-component-library" {
    import * as React from "react";
    
    // 组件 Props
    export interface ButtonProps {
        children: React.ReactNode;
        variant?: "primary" | "secondary" | "danger";
        size?: "small" | "medium" | "large";
        disabled?: boolean;
        onClick?: (event: React.MouseEvent<HTMLButtonElement>) => void;
    }
    
    // 组件声明
    export class Button extends React.Component<ButtonProps> {}
    
    // 函数组件
    export const IconButton: React.FC<{
        icon: string;
        onClick?: (event: React.MouseEvent<HTMLButtonElement>) => void;
    }>;
    
    // Hook
    export function useCounter(initialValue?: number): [number, {
        increment: () => void;
        decrement: () => void;
        reset: () => void;
    }];
    
    // 高阶组件
    export function withLoading<P>(
        WrappedComponent: React.ComponentType<P>
    ): React.ComponentType<P & { loading: boolean }>;
    
    // 默认导出
    export default Button;
}

// 声明命名空间模块
declare module "my-namespace-module" {
    namespace MyNamespace {
        export interface Config {
            host: string;
            port: number;
        }
        
        export class Client {
            constructor(config: Config);
            connect(): Promise<void>;
            disconnect(): Promise<void>;
        }
    }
    
    export = MyNamespace;
}

// 使用命名空间模块
// import MyNamespace = require("my-namespace-module");
// const client = new MyNamespace.Client({ host: "localhost", port: 3000 });
```

### 模块增强声明
```typescript
// 模块增强声明
// 为现有模块添加额外的类型定义
// react-router-dom-augmentation.d.ts
declare module "react-router-dom" {
    // 添加新的导出
    export interface RouteComponentProps<T = {}> {
        isAuthenticated?: boolean;
        userRole?: string;
    }
    
    // 扩展现有接口
    interface BrowserRouterProps {
        basename?: string;
        getUserConfirmation?: (message: string, callback: (result: boolean) => void) => void;
        forceRefresh?: boolean;
        keyLength?: number;
    }
}

// 为第三方库添加自定义类型
// express-session-augmentation.d.ts
declare module "express-session" {
    interface SessionData {
        userId?: string;
        userRole?: string;
        lastActivity?: number;
    }
}

// 在 Express 应用中使用
// import { Request } from "express";
// declare module "express" {
//     interface Request {
//         session: Session & Partial<SessionData>;
//     }
// }
```

## 声明合并

### 接口合并
```typescript
// 接口合并示例
// 基本接口合并
interface Box {
    height: number;
    width: number;
}

interface Box {
    scale: number;
}

// 结果接口
// interface Box {
//     height: number;
//     width: number;
//     scale: number;
// }

let box: Box = { height: 5, width: 6, scale: 10 };

// 函数合并
interface Cloner {
    clone(animal: Animal): Animal;
}

interface Cloner {
    clone(animal: Sheep): Sheep;
}

interface Cloner {
    clone(animal: Dog): Dog;
    clone(animal: Cat): Cat;
}

// 结果接口
// interface Cloner {
//     clone(animal: Dog): Dog;
//     clone(animal: Cat): Cat;
//     clone(animal: Sheep): Sheep;
//     clone(animal: Animal): Animal;
// }

// 声明合并的实际应用
// 为第三方库扩展接口
// express-extensions.d.ts
declare module "express" {
    interface Request {
        userId?: string;
        userRole?: string;
        correlationId: string;
    }
    
    interface Response {
        success<T>(data: T): this;
        error(message: string, code?: number): this;
    }
}

// 在实际代码中使用扩展的类型
// app.ts
import { Request, Response } from "express";

app.use((req: Request, res: Response, next) => {
    req.correlationId = Math.random().toString(36);
    req.userId = "123";
    req.userRole = "admin";
    next();
});

app.get("/api/users", (req: Request, res: Response) => {
    // 现在可以安全地访问扩展的属性
    console.log(`User ${req.userId} with role ${req.userRole} requested users`);
    res.success([{ id: "1", name: "Alice" }]);
});
```

### 命名空间合并
```typescript
// 命名空间合并
// 基本命名空间合并
namespace Validation {
    export interface StringValidator {
        isAcceptable(s: string): boolean;
    }
}

namespace Validation {
    const lettersRegexp = /^[A-Za-z]+$/;
    
    export class LettersOnlyValidator implements StringValidator {
        isAcceptable(s: string) {
            return lettersRegexp.test(s);
        }
    }
}

namespace Validation {
    const numberRegexp = /^[0-9]+$/;
    
    export class ZipCodeValidator implements StringValidator {
        isAcceptable(s: string) {
            return s.length === 5 && numberRegexp.test(s);
        }
    }
}

// 结果命名空间
// namespace Validation {
//     export interface StringValidator { ... }
//     export class LettersOnlyValidator { ... }
//     export class ZipCodeValidator { ... }
// }

// 命名空间与类合并
class Album {
    label: Album.AlbumLabel;
}

namespace Album {
    export interface AlbumLabel {
        name: string;
        year: number;
    }
    
    export function createLabel(name: string, year: number): AlbumLabel {
        return { name, year };
    }
}

// 使用合并结果
let album = new Album();
album.label = Album.createLabel("Greatest Hits", 2020);

// 函数与命名空间合并
function buildName(firstName: string, lastName?: string) {
    if (lastName) {
        return firstName + " " + lastName;
    } else {
        return firstName;
    }
}

namespace buildName {
    export function reallyFancyName(firstName: string, lastName?: string) {
        return "The Honorable " + buildName(firstName, lastName);
    }
}

// 使用合并结果
console.log(buildName("Bob")); // "Bob"
console.log(buildName.reallyFancyName("Bob", "Smith")); // "The Honorable Bob Smith"
```

### 枚举合并
```typescript
// 枚举合并
// 基本枚举合并
enum Color {
    red = 1,
    green = 2,
    blue = 4
}

enum Color {
    yellow = 8,
    orange = 16,
    purple = 32
}

// 结果枚举
// enum Color {
//     red = 1,
//     green = 2,
//     blue = 4,
//     yellow = 8,
//     orange = 16,
//     purple = 32
// }

// 枚举与命名空间合并
enum Animal {
    Dog,
    Cat,
    Bird
}

namespace Animal {
    export function getSound(animal: Animal): string {
        switch (animal) {
            case Animal.Dog: return "Woof";
            case Animal.Cat: return "Meow";
            case Animal.Bird: return "Tweet";
            default: return "Unknown";
        }
    }
    
    export const descriptions = {
        [Animal.Dog]: "Man's best friend",
        [Animal.Cat]: "Independent companion",
        [Animal.Bird]: "Feathered friend"
    };
}

// 使用合并结果
console.log(Animal.getSound(Animal.Dog)); // "Woof"
console.log(Animal.descriptions[Animal.Cat]); // "Independent companion"
```

## 环境声明

### 基本环境声明
```typescript
// 环境声明用于描述运行时环境
// browser-env.d.ts
declare const __DEV__: boolean;
declare const __VERSION__: string;
declare const process: {
    env: {
        NODE_ENV: 'development' | 'production' | 'test';
        [key: string]: string | undefined;
    };
};

// 浏览器 API 声明
interface Navigator {
    readonly clipboard: Clipboard;
}

interface Clipboard {
    writeText(text: string): Promise<void>;
    readText(): Promise<string>;
}

// DOM 扩展声明
interface HTMLElement {
    scrollIntoViewIfNeeded?: (centerIfNeeded?: boolean) => void;
}

// Web Workers 声明
interface WorkerGlobalScope {
    importScripts(...urls: string[]): void;
    postMessage(message: any, transfer?: Transferable[]): void;
    onmessage: ((this: WorkerGlobalScope, ev: MessageEvent) => any) | null;
}

// Service Workers 声明
interface ServiceWorkerRegistration {
    readonly active: ServiceWorker | null;
    readonly installing: ServiceWorker | null;
    readonly waiting: ServiceWorker | null;
    update(): Promise<void>;
}
```

### Node.js 环境声明
```typescript
// node-env.d.ts
// Node.js 全局对象
declare const global: NodeJS.Global & typeof globalThis;

// Node.js 进程对象
declare const process: NodeJS.Process;

// Node.js 模块系统
declare const require: NodeRequire;
declare const module: NodeModule;
declare const exports: any;

// Buffer 声明
interface Buffer extends Uint8Array {
    write(string: string, offset?: number, length?: number, encoding?: string): number;
    toString(encoding?: string, start?: number, end?: number): string;
    // ... 其他方法
}

// Node.js 核心模块声明
declare module "fs" {
    export function readFile(
        path: string | Buffer | URL,
        options: { encoding: BufferEncoding; flag?: string; } | BufferEncoding,
        callback: (err: NodeJS.ErrnoException | null, data: string) => void
    ): void;
    
    export function writeFile(
        path: string | Buffer | URL,
        data: string | Uint8Array,
        options: { encoding?: string; mode?: number; flag?: string; } | string,
        callback: (err: NodeJS.ErrnoException | null) => void
    ): void;
    
    // ... 其他导出
}

declare module "path" {
    export function join(...paths: string[]): string;
    export function resolve(...pathSegments: string[]): string;
    export function basename(path: string, ext?: string): string;
    export function dirname(path: string): string;
    export function extname(path: string): string;
    // ... 其他导出
}

declare module "http" {
    import * as stream from "stream";
    import { URL } from "url";
    
    export interface IncomingMessage extends stream.Readable {
        url?: string;
        method?: string;
        headers: IncomingHttpHeaders;
        // ... 其他属性
    }
    
    export interface ServerResponse extends stream.Writable {
        statusCode: number;
        statusMessage: string;
        setHeader(name: string, value: number | string | string[]): void;
        end(callback?: () => void): void;
        end(data: string | Uint8Array, callback?: () => void): void;
        // ... 其他方法
    }
    
    export function createServer(
        requestListener?: (request: IncomingMessage, response: ServerResponse) => void
    ): Server;
    
    // ... 其他导出
}
```

### 现代 Web API 声明
```typescript
// web-apis.d.ts
// Fetch API
declare function fetch(
    input: RequestInfo,
    init?: RequestInit
): Promise<Response>;

interface RequestInit {
    method?: string;
    headers?: HeadersInit;
    body?: BodyInit | null;
    mode?: RequestMode;
    credentials?: RequestCredentials;
    cache?: RequestCache;
    redirect?: RequestRedirect;
    referrer?: string;
    referrerPolicy?: ReferrerPolicy;
    integrity?: string;
    keepalive?: boolean;
    signal?: AbortSignal | null;
}

// Web Storage API
interface Storage {
    readonly length: number;
    clear(): void;
    getItem(key: string): string | null;
    key(index: number): string | null;
    removeItem(key: string): void;
    setItem(key: string, value: string): void;
}

// Geolocation API
interface Geolocation {
    getCurrentPosition(
        successCallback: PositionCallback,
        errorCallback?: PositionErrorCallback,
        options?: PositionOptions
    ): void;
    
    watchPosition(
        successCallback: PositionCallback,
        errorCallback?: PositionErrorCallback,
        options?: PositionOptions
    ): number;
    
    clearWatch(watchId: number): void;
}

// Notification API
interface NotificationOptions {
    body?: string;
    icon?: string;
    badge?: string;
    image?: string;
    data?: any;
    tag?: string;
    renotify?: boolean;
    silent?: boolean;
    requireInteraction?: boolean;
    actions?: NotificationAction[];
}

interface Notification extends EventTarget {
    readonly title: string;
    readonly body: string;
    readonly icon: string;
    // ... 其他属性
}

// WebSocket API
interface WebSocket extends EventTarget {
    readonly url: string;
    readonly readyState: number;
    readonly bufferedAmount: number;
    onopen: ((this: WebSocket, ev: Event) => any) | null;
    onerror: ((this: WebSocket, ev: Event) => any) | null;
    onclose: ((this: WebSocket, ev: CloseEvent) => any) | null;
    close(code?: number, reason?: string): void;
    // ... 其他方法
}

declare var WebSocket: {
    prototype: WebSocket;
    new(url: string | URL, protocols?: string | string[]): WebSocket;
    readonly CLOSED: number;
    readonly CLOSING: number;
    readonly CONNECTING: number;
    readonly OPEN: number;
};
```

## 第三方库声明

### 使用 DefinitelyTyped
```typescript
// DefinitelyTyped 是官方的 TypeScript 类型定义仓库
// https://github.com/DefinitelyTyped/DefinitelyTyped

// 安装第三方库的类型定义
// npm install --save-dev @types/lodash
// npm install --save-dev @types/express
// npm install --save-dev @types/react
// npm install --save-dev @types/node

// 使用类型定义
import * as _ from "lodash";
import express from "express";
import * as React from "react";

// lodash 使用示例
const numbers = [1, 2, 3, 4, 5];
const doubled = _.map(numbers, n => n * 2);
const sum = _.sum(numbers);

// express 使用示例
const app = express();
app.get("/api/users", (req, res) => {
    res.json({ users: [] });
});

// react 使用示例
const MyComponent: React.FC<{ name: string }> = ({ name }) => {
    return <div>Hello, {name}!</div>;
};
```

### 创建自定义类型定义
```typescript
// 为没有类型定义的库创建自定义类型定义
// types/untyped-library/index.d.ts
declare module "untyped-library" {
    export interface Config {
        host: string;
        port: number;
        timeout?: number;
    }
    
    export class Client {
        constructor(config: Config);
        connect(): Promise<void>;
        disconnect(): Promise<void>;
        request<T>(endpoint: string, data?: any): Promise<T>;
    }
    
    export function createClient(config: Config): Client;
    export function setGlobalConfig(config: Partial<Config>): void;
    
    export default createClient;
}

// 为库添加额外的类型定义
// types/untyped-library/additional.d.ts
declare module "untyped-library" {
    // 添加新的导出
    export interface AdvancedConfig extends Config {
        retries: number;
        backoff: boolean;
    }
    
    export class AdvancedClient extends Client {
        constructor(config: AdvancedConfig);
        retryRequest<T>(endpoint: string, data?: any, maxRetries?: number): Promise<T>;
    }
    
    // 扩展现有接口
    interface Client {
        healthCheck(): Promise<boolean>;
    }
}

// 使用自定义类型定义
// tsconfig.json
{
    "compilerOptions": {
        "typeRoots": ["./node_modules/@types", "./types"]
    }
}

// app.ts
import createClient, { Client, Config } from "untyped-library";

const config: Config = {
    host: "localhost",
    port: 3000
};

const client = createClient(config);
client.connect().then(() => {
    console.log("Connected!");
});
```

### 维护类型定义
```typescript
// 为自己的库维护类型定义
// my-library/package.json
{
    "name": "my-awesome-library",
    "version": "1.0.0",
    "main": "dist/index.js",
    "types": "dist/index.d.ts",
    "files": [
        "dist/**/*"
    ]
}

// my-library/src/index.ts
export interface User {
    id: string;
    name: string;
    email: string;
}

export class UserService {
    private users: User[] = [];
    
    getUser(id: string): User | undefined {
        return this.users.find(u => u.id === id);
    }
    
    createUser(user: Omit<User, 'id'>): User {
        const newUser = { ...user, id: Math.random().toString(36) };
        this.users.push(newUser);
        return newUser;
    }
}

export default UserService;

// 生成的声明文件 my-library/dist/index.d.ts
export interface User {
    id: string;
    name: string;
    email: string;
}

export class UserService {
    private users: User[];
    getUser(id: string): User | undefined;
    createUser(user: Omit<User, 'id'>): User;
}

export default UserService;

// 为库创建额外的类型定义文件
// my-library/types/enhanced.d.ts
declare module "my-awesome-library" {
    export interface EnhancedUser extends User {
        createdAt: Date;
        updatedAt: Date;
    }
    
    export class EnhancedUserService extends UserService {
        getRecentUsers(hours: number): EnhancedUser[];
        getUserStats(): { total: number; active: number };
    }
}
```

### 类型定义最佳实践
```typescript
// 类型定义最佳实践

// 1. 使用命名空间组织相关类型
declare module "my-library" {
    namespace MyLibrary {
        export interface Config {
            host: string;
            port: number;
        }
        
        export class Client {
            constructor(config: Config);
        }
    }
    
    export = MyLibrary;
}

// 2. 提供默认导出和命名导出
declare module "my-library" {
    export interface User {
        id: string;
        name: string;
    }
    
    export class UserService {
        getUser(id: string): User;
    }
    
    // 默认导出
    export default UserService;
    
    // 命名导出
    export { UserService, User };
}

// 3. 使用泛型提高灵活性
declare module "generic-library" {
    export function map<T, U>(array: T[], fn: (item: T) => U): U[];
    export function filter<T>(array: T[], predicate: (item: T) => boolean): T[];
    export class Repository<T> {
        findById(id: string): T | null;
        save(entity: T): T;
    }
}

// 4. 提供详细的 JSDoc 注释
declare module "documented-library" {
    /**
     * 用户服务类
     * 提供用户相关的操作方法
     */
    export class UserService {
        /**
         * 根据 ID 获取用户
         * @param id 用户 ID
         * @returns 用户对象或 undefined
         */
        getUser(id: string): User | undefined;
        
        /**
         * 创建新用户
         * @param userData 用户数据（不包含 ID）
         * @returns 创建的用户对象
         */
        createUser(userData: Omit<User, 'id'>): User;
    }
}

// 5. 处理可选依赖
declare module "conditional-library" {
    export interface BaseConfig {
        host: string;
        port: number;
    }
    
    // 条件导出类型
    export type Config<T extends boolean = false> = T extends true 
        ? BaseConfig & { ssl: boolean; certPath: string }
        : BaseConfig;
    
    export class Client<T extends boolean = false> {
        constructor(config: Config<T>);
    }
}
```


# 15. JSX 支持

## 基本 JSX 语法

### JSX 基础配置
```typescript
// tsconfig.json 配置 JSX
{
  "compilerOptions": {
    "jsx": "react",           // react, preserve, react-native, react-jsx, react-jsxdev
    "jsxFactory": "React.createElement",
    "jsxFragmentFactory": "React.Fragment"
  }
}

// React 17+ 新的 JSX 转换
{
  "compilerOptions": {
    "jsx": "react-jsx",       // 自动导入 jsx 和 jsxs
    "module": "esnext",
    "moduleResolution": "node"
  }
}
```

### 基本 JSX 语法
```typescript
// 基本 JSX 元素
const element = <div>Hello, World!</div>;

// 带属性的 JSX 元素
const elementWithProps = <div className="container" id="main">Content</div>;

// 自闭合标签
const selfClosing = <img src="image.jpg" alt="Description" />;

// 嵌套 JSX 元素
const nestedElements = (
  <div className="card">
    <h1>Title</h1>
    <p>Description</p>
    <button onClick={() => console.log('Clicked!')}>Click me</button>
  </div>
);

// JSX 表达式
const name = "Alice";
const greeting = <h1>Hello, {name}!</h1>;

// 条件渲染
const isLoggedIn = true;
const conditionalElement = (
  <div>
    {isLoggedIn ? <p>Welcome back!</p> : <p>Please log in.</p>}
  </div>
);

// 列表渲染
const items = ['Apple', 'Banana', 'Orange'];
const listItems = (
  <ul>
    {items.map((item, index) => (
      <li key={index}>{item}</li>
    ))}
  </ul>
);

// Fragment 使用
const fragmentElement = (
  <>
    <h1>Title</h1>
    <p>Content</p>
  </>
);

// React Fragment
const reactFragment = (
  <React.Fragment>
    <h1>Title</h1>
    <p>Content</p>
  </React.Fragment>
);
```

### JSX 与 TypeScript 集成
```typescript
// JSX 与 TypeScript 类型
// 定义组件 Props 接口
interface UserCardProps {
  name: string;
  age: number;
  email: string;
  isActive?: boolean;
}

// 函数组件使用 JSX
const UserCard: React.FC<UserCardProps> = ({ name, age, email, isActive = true }) => {
  return (
    <div className={`user-card ${isActive ? 'active' : 'inactive'}`}>
      <h2>{name}</h2>
      <p>Age: {age}</p>
      <p>Email: {email}</p>
      <span>Status: {isActive ? 'Active' : 'Inactive'}</span>
    </div>
  );
};

// 使用组件
const App = () => {
  return (
    <div>
      <UserCard 
        name="Alice" 
        age={30} 
        email="alice@example.com" 
        isActive={true} 
      />
      <UserCard 
        name="Bob" 
        age={25} 
        email="bob@example.com" 
      />
    </div>
  );
};
```

## 类型检查

### JSX 类型检查基础
```typescript
// JSX 类型检查配置
// tsconfig.json
{
  "compilerOptions": {
    "jsx": "react",
    "strict": true,                    // 启用严格类型检查
    "noImplicitAny": true,             // 不允许隐式的 any
    "strictNullChecks": true,          // 严格的 null 检查
    "strictFunctionTypes": true        // 严格的函数类型检查
  }
}

// 基本类型检查示例
interface ButtonProps {
  label: string;
  onClick: () => void;
  disabled?: boolean;
}

const Button: React.FC<ButtonProps> = ({ label, onClick, disabled = false }) => {
  return (
    <button 
      onClick={onClick} 
      disabled={disabled}
      className={disabled ? 'disabled' : 'enabled'}
    >
      {label}
    </button>
  );
};

// 正确使用
const CorrectUsage = () => {
  return (
    <Button 
      label="Click me" 
      onClick={() => console.log('Clicked!')} 
    />
  );
};

// 错误使用（编译时错误）
const WrongUsage = () => {
  return (
    // <Button label={123} onClick="not a function" /> // 编译错误
    <Button 
      label="Click me" 
      // onClick={() => console.log('Clicked!')} 
      missingRequiredProp={true} // 编译错误
    />
  );
};
```

### 复杂类型检查
```typescript
// 联合类型 Props
interface SuccessProps {
  status: 'success';
  message: string;
}

interface ErrorProps {
  status: 'error';
  error: string;
}

interface LoadingProps {
  status: 'loading';
}

type StatusProps = SuccessProps | ErrorProps | LoadingProps;

const StatusComponent: React.FC<StatusProps> = (props) => {
  switch (props.status) {
    case 'success':
      return <div className="success">{props.message}</div>;
    case 'error':
      return <div className="error">{props.error}</div>;
    case 'loading':
      return <div className="loading">Loading...</div>;
    default:
      // 穷尽检查
      const _exhaustive: never = props;
      return _exhaustive;
  }
};

// 泛型组件
interface ListProps<T> {
  items: T[];
  renderItem: (item: T, index: number) => React.ReactNode;
  keyExtractor: (item: T) => string | number;
}

const List = <T,>({ items, renderItem, keyExtractor }: ListProps<T>) => {
  return (
    <ul>
      {items.map((item, index) => (
        <li key={keyExtractor(item)}>
          {renderItem(item, index)}
        </li>
      ))}
    </ul>
  );
};

// 使用泛型组件
interface User {
  id: string;
  name: string;
  email: string;
}

const UserList = () => {
  const users: User[] = [
    { id: '1', name: 'Alice', email: 'alice@example.com' },
    { id: '2', name: 'Bob', email: 'bob@example.com' }
  ];

  return (
    <List<User>
      items={users}
      renderItem={(user) => (
        <div>
          <h3>{user.name}</h3>
          <p>{user.email}</p>
        </div>
      )}
      keyExtractor={(user) => user.id}
    />
  );
};
```

### 条件类型检查
```typescript
// 条件类型与 JSX
type IsString<T> = T extends string ? true : false;

interface ConditionalProps<T> {
  value: T;
  isString: IsString<T>;
  onStringChange?: (value: string) => void;
  onNumberChange?: (value: number) => void;
}

const ConditionalComponent = <T,>({ 
  value, 
  isString, 
  onStringChange, 
  onNumberChange 
}: ConditionalProps<T>) => {
  if (isString) {
    return (
      <input 
        type="text" 
        value={value as string}
        onChange={(e) => onStringChange?.(e.target.value)}
      />
    );
  } else {
    return (
      <input 
        type="number" 
        value={value as number}
        onChange={(e) => onNumberChange?.(Number(e.target.value))}
      />
    );
  }
};

// 实用工具类型在 JSX 中的应用
type Optionalize<T extends K, K> = Omit<T, keyof K>;

interface BaseButtonProps {
  label: string;
  onClick: () => void;
  disabled?: boolean;
  className?: string;
}

interface PrimaryButtonProps extends BaseButtonProps {
  variant: 'primary';
  primaryColor: string;
}

interface SecondaryButtonProps extends BaseButtonProps {
  variant: 'secondary';
  secondaryColor: string;
}

type ButtonProps = PrimaryButtonProps | SecondaryButtonProps;

const Button: React.FC<ButtonProps> = (props) => {
  const baseProps: BaseButtonProps = {
    label: props.label,
    onClick: props.onClick,
    disabled: props.disabled,
    className: props.className
  };

  switch (props.variant) {
    case 'primary':
      return (
        <button 
          {...baseProps}
          style={{ backgroundColor: props.primaryColor }}
        >
          {props.label}
        </button>
      );
    case 'secondary':
      return (
        <button 
          {...baseProps}
          style={{ backgroundColor: props.secondaryColor }}
        >
          {props.label}
        </button>
      );
    default:
      const _exhaustive: never = props;
      return _exhaustive;
  }
};
```

## 固有元素

### HTML 元素类型检查
```typescript
// React 内置的 HTML 元素类型定义
// 这些类型定义在 @types/react 中

// 基本 HTML 元素
const divElement: JSX.IntrinsicElements['div'] = {
  className: "container",
  id: "main",
  children: "Content"
};

const inputElement: JSX.IntrinsicElements['input'] = {
  type: "text",
  placeholder: "Enter text",
  value: "initial value",
  onChange: (e) => console.log(e.target.value)
};

// 常用 HTML 元素类型
interface DivProps extends React.HTMLAttributes<HTMLDivElement> {}
interface InputProps extends React.InputHTMLAttributes<HTMLInputElement> {}
interface ButtonProps extends React.ButtonHTMLAttributes<HTMLButtonElement> {}
interface AnchorProps extends React.AnchorHTMLAttributes<HTMLAnchorElement> {}

// 自定义 HTML 元素组件
const CustomDiv: React.FC<DivProps> = ({ children, ...props }) => {
  return <div {...props}>{children}</div>;
};

const CustomInput: React.FC<InputProps> = (props) => {
  return <input {...props} />;
};

// 使用自定义 HTML 元素组件
const FormComponent = () => {
  const [value, setValue] = React.useState("");

  return (
    <CustomDiv className="form-container">
      <CustomInput
        type="text"
        value={value}
        onChange={(e) => setValue(e.target.value)}
        placeholder="Enter your name"
        required
      />
      <button type="submit">Submit</button>
    </CustomDiv>
  );
};
```

### DOM 属性类型检查
```typescript
// DOM 属性类型检查
interface CustomInputProps extends React.InputHTMLAttributes<HTMLInputElement> {
  // 添加自定义属性
  customValidation?: (value: string) => boolean;
  onCustomValidation?: (isValid: boolean) => void;
}

const ValidatedInput: React.FC<CustomInputProps> = ({ 
  customValidation, 
  onCustomValidation,
  ...props 
}) => {
  const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
    if (customValidation && onCustomValidation) {
      const isValid = customValidation(e.target.value);
      onCustomValidation(isValid);
    }
    props.onChange?.(e);
  };

  return <input {...props} onChange={handleChange} />;
};

// 使用带验证的输入框
const EmailInput = () => {
  const [isValid, setIsValid] = React.useState(true);

  const validateEmail = (email: string): boolean => {
    return /\S+@\S+\.\S+/.test(email);
  };

  return (
    <div>
      <ValidatedInput
        type="email"
        placeholder="Enter email"
        customValidation={validateEmail}
        onCustomValidation={setIsValid}
        style={{ borderColor: isValid ? 'green' : 'red' }}
      />
      {!isValid && <span style={{ color: 'red' }}>Invalid email format</span>}
    </div>
  );
};

// 事件处理程序类型
interface InteractiveDivProps extends React.HTMLAttributes<HTMLDivElement> {
  onDoubleClick?: React.MouseEventHandler<HTMLDivElement>;
  onContextMenu?: React.MouseEventHandler<HTMLDivElement>;
  onWheel?: React.WheelEventHandler<HTMLDivElement>;
}

const InteractiveDiv: React.FC<InteractiveDivProps> = (props) => {
  return <div {...props} />;
};

// 使用交互式 div
const InteractiveComponent = () => {
  const handleDoubleClick = (e: React.MouseEvent<HTMLDivElement>) => {
    console.log('Double clicked at:', e.clientX, e.clientY);
  };

  const handleContextMenu = (e: React.MouseEvent<HTMLDivElement>) => {
    e.preventDefault();
    console.log('Context menu opened');
  };

  const handleWheel = (e: React.WheelEvent<HTMLDivElement>) => {
    console.log('Wheel scrolled:', e.deltaY);
  };

  return (
    <InteractiveDiv
      onDoubleClick={handleDoubleClick}
      onContextMenu={handleContextMenu}
      onWheel={handleWheel}
      style={{ width: '200px', height: '200px', backgroundColor: 'lightblue' }}
    >
      Double click or scroll me!
    </InteractiveDiv>
  );
};
```

### SVG 元素支持
```typescript
// SVG 元素类型检查
interface CustomSVGProps extends React.SVGProps<SVGSVGElement> {
  title?: string;
}

const CustomSVG: React.FC<CustomSVGProps> = ({ title, children, ...props }) => {
  return (
    <svg {...props}>
      {title && <title>{title}</title>}
      {children}
    </svg>
  );
};

// 使用 SVG 元素
const IconComponent = () => {
  return (
    <CustomSVG 
      width="24" 
      height="24" 
      viewBox="0 0 24 24"
      title="User Icon"
    >
      <circle cx="12" cy="8" r="4" fill="currentColor" />
      <path 
        d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2" 
        stroke="currentColor" 
        strokeWidth="2" 
        fill="none" 
      />
    </CustomSVG>
  );
};

// SVG 元素属性类型
interface CircleProps extends React.SVGProps<SVGCircleElement> {}
interface PathProps extends React.SVGProps<SVGPathElement> {}
interface RectProps extends React.SVGProps<SVGRectElement> {}

const CustomCircle: React.FC<CircleProps> = (props) => {
  return <circle {...props} />;
};

const CustomPath: React.FC<PathProps> = (props) => {
  return <path {...props} />;
};

// 组合 SVG 组件
const CustomIcon = () => {
  return (
    <svg width="32" height="32" viewBox="0 0 32 32">
      <CustomCircle cx="16" cy="10" r="6" fill="#007acc" />
      <CustomPath 
        d="M26 30v-3a5 5 0 0 0-5-5H11a5 5 0 0 0-5 5v3" 
        stroke="#007acc" 
        strokeWidth="2" 
        fill="none" 
      />
    </svg>
  );
};
```

## 基于值的元素

### 组件引用类型检查
```typescript
// 基于值的元素 - 组件引用
// 函数组件
const Welcome: React.FC<{ name: string }> = ({ name }) => {
  return <h1>Hello, {name}!</h1>;
};

// 类组件
class Goodbye extends React.Component<{ name: string }> {
  render() {
    return <h1>Goodbye, {this.props.name}!</h1>;
  }
}

// 使用基于值的元素
const App = () => {
  const Component = Math.random() > 0.5 ? Welcome : Goodbye;
  
  return (
    <div>
      <Component name="Alice" />
    </div>
  );
};

// 组件类型推断
type WelcomeComponentType = typeof Welcome; // React.FC<{ name: string }>
type GoodbyeComponentType = typeof Goodbye; // React.ComponentClass<{ name: string }>

// 动态组件选择
interface ComponentMap {
  welcome: React.FC<{ name: string }>;
  goodbye: React.ComponentClass<{ name: string }>;
}

const componentMap: ComponentMap = {
  welcome: Welcome,
  goodbye: Goodbye
};

const DynamicComponent = ({ type, name }: { type: keyof ComponentMap; name: string }) => {
  const Component = componentMap[type];
  return <Component name={name} />;
};
```

### 高阶组件类型检查
```typescript
// 高阶组件 (HOC) 类型检查
interface WithLoadingProps {
  loading: boolean;
}

// HOC 工厂函数
function withLoading<P extends WithLoadingProps>(
  WrappedComponent: React.ComponentType<P>
) {
  return class WithLoading extends React.Component<Omit<P, 'loading'>> {
    render() {
      return (
        <div>
          <p>Loading...</p>
          <WrappedComponent {...(this.props as P)} loading={false} />
        </div>
      );
    }
  };
}

// 更好的 HOC 类型定义
function withLoading2<P>(
  WrappedComponent: React.ComponentType<P & WithLoadingProps>
) {
  return (props: P) => (
    <div>
      <p>Loading...</p>
      <WrappedComponent {...props} loading={true} />
    </div>
  );
}

// 使用 HOC
interface UserProfileProps {
  name: string;
  email: string;
  loading: boolean;
}

const UserProfile: React.FC<UserProfileProps> = ({ name, email, loading }) => {
  if (loading) return <p>Loading user profile...</p>;
  
  return (
    <div>
      <h2>{name}</h2>
      <p>{email}</p>
    </div>
  );
};

const LoadingUserProfile = withLoading2(UserProfile);

// 使用增强组件
const AppWithHOC = () => {
  return <LoadingUserProfile name="Alice" email="alice@example.com" />;
};
```

### 组件组合类型检查
```typescript
// 组件组合类型检查
interface LayoutProps {
  children: React.ReactNode;
  title: string;
}

const Layout: React.FC<LayoutProps> = ({ children, title }) => {
  return (
    <div className="layout">
      <header>
        <h1>{title}</h1>
      </header>
      <main>{children}</main>
      <footer>© 2023</footer>
    </div>
  );
};

// 子组件
const Header: React.FC<{ title: string }> = ({ title }) => {
  return <h1>{title}</h1>;
};

const Content: React.FC<{ content: string }> = ({ content }) => {
  return <p>{content}</p>;
};

const Sidebar: React.FC<{ items: string[] }> = ({ items }) => {
  return (
    <ul>
      {items.map((item, index) => (
        <li key={index}>{item}</li>
      ))}
    </ul>
  );
};

// 组合使用组件
const ComplexApp = () => {
  return (
    <Layout title="My App">
      <Header title="Welcome" />
      <Content content="This is the main content." />
      <Sidebar items={['Home', 'About', 'Contact']} />
    </Layout>
  );
};

// 条件渲染组件
interface ConditionalWrapperProps {
  condition: boolean;
  wrapper: (children: React.ReactNode) => React.ReactNode;
  children: React.ReactNode;
}

const ConditionalWrapper: React.FC<ConditionalWrapperProps> = ({ 
  condition, 
  wrapper, 
  children 
}) => {
  return condition ? wrapper(children) : <>{children}</>;
};

// 使用条件包装器
const ConditionalApp = () => {
  const [showBorder, setShowBorder] = React.useState(true);

  return (
    <ConditionalWrapper
      condition={showBorder}
      wrapper={(children) => <div style={{ border: '1px solid red' }}>{children}</div>}
    >
      <p>This content may or may not have a border.</p>
      <button onClick={() => setShowBorder(!showBorder)}>
        Toggle Border
      </button>
    </ConditionalWrapper>
  );
};
```

## 函数组件

### 基本函数组件
```typescript
// 基本函数组件定义
interface ButtonProps {
  label: string;
  onClick: () => void;
  variant?: 'primary' | 'secondary' | 'danger';
  size?: 'small' | 'medium' | 'large';
  disabled?: boolean;
}

// 使用 React.FC
const Button: React.FC<ButtonProps> = ({ 
  label, 
  onClick, 
  variant = 'primary', 
  size = 'medium', 
  disabled = false 
}) => {
  return (
    <button
      className={`btn btn-${variant} btn-${size} ${disabled ? 'disabled' : ''}`}
      onClick={onClick}
      disabled={disabled}
    >
      {label}
    </button>
  );
};

// 不使用 React.FC（推荐方式）
const Button2 = ({ 
  label, 
  onClick, 
  variant = 'primary', 
  size = 'medium', 
  disabled = false 
}: ButtonProps) => {
  return (
    <button
      className={`btn btn-${variant} btn-${size} ${disabled ? 'disabled' : ''}`}
      onClick={onClick}
      disabled={disabled}
    >
      {label}
    </button>
  );
};

// 使用组件
const App = () => {
  return (
    <div>
      <Button label="Primary" onClick={() => console.log('Primary clicked')} />
      <Button 
        label="Secondary Large" 
        onClick={() => console.log('Secondary clicked')} 
        variant="secondary"
        size="large"
      />
      <Button 
        label="Disabled" 
        onClick={() => console.log('Should not fire')} 
        disabled
      />
    </div>
  );
};
```

### 带状态的函数组件
```typescript
// 使用 useState Hook
interface CounterProps {
  initialValue?: number;
  step?: number;
}

const Counter: React.FC<CounterProps> = ({ 
  initialValue = 0, 
  step = 1 
}) => {
  const [count, setCount] = React.useState(initialValue);

  const increment = () => setCount(count + step);
  const decrement = () => setCount(count - step);
  const reset = () => setCount(initialValue);

  return (
    <div className="counter">
      <span>Count: {count}</span>
      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
};

// 使用 useEffect Hook
interface TimerProps {
  initialSeconds?: number;
}

const Timer: React.FC<TimerProps> = ({ initialSeconds = 0 }) => {
  const [seconds, setSeconds] = React.useState(initialSeconds);
  const [isActive, setIsActive] = React.useState(false);

  React.useEffect(() => {
    let interval: NodeJS.Timeout | null = null;

    if (isActive) {
      interval = setInterval(() => {
        setSeconds(s => s + 1);
      }, 1000);
    }

    return () => {
      if (interval) clearInterval(interval);
    };
  }, [isActive]);

  const toggleTimer = () => setIsActive(!isActive);
  const resetTimer = () => {
    setSeconds(initialSeconds);
    setIsActive(false);
  };

  return (
    <div className="timer">
      <div>Time: {seconds}s</div>
      <button onClick={toggleTimer}>
        {isActive ? 'Pause' : 'Start'}
      </button>
      <button onClick={resetTimer}>Reset</button>
    </div>
  );
};
```

### 自定义 Hook 类型检查
```typescript
// 自定义 Hook
interface UseCounterReturn {
  count: number;
  increment: () => void;
  decrement: () => void;
  reset: () => void;
}

function useCounter(initialValue: number = 0, step: number = 1): UseCounterReturn {
  const [count, setCount] = React.useState(initialValue);

  const increment = React.useCallback(() => setCount(c => c + step), [step]);
  const decrement = React.useCallback(() => setCount(c => c - step), [step]);
  const reset = React.useCallback(() => setCount(initialValue), [initialValue]);

  return { count, increment, decrement, reset };
}

// 使用自定义 Hook
const CounterWithHook: React.FC<{ initialValue?: number; step?: number }> = ({ 
  initialValue = 0, 
  step = 1 
}) => {
  const { count, increment, decrement, reset } = useCounter(initialValue, step);

  return (
    <div>
      <span>Count: {count}</span>
      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
};

// 复杂自定义 Hook
interface UseApiReturn<T> {
  data: T | null;
  loading: boolean;
  error: string | null;
  refetch: () => void;
}

async function fetchData<T>(url: string): Promise<T> {
  const response = await fetch(url);
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }
  return response.json();
}

function useApi<T>(url: string): UseApiReturn<T> {
  const [data, setData] = React.useState<T | null>(null);
  const [loading, setLoading] = React.useState(true);
  const [error, setError] = React.useState<string | null>(null);

  const fetchDataCallback = React.useCallback(async () => {
    setLoading(true);
    setError(null);
    try {
      const result = await fetchData<T>(url);
      setData(result);
    } catch (err) {
      setError(err instanceof Error ? err.message : 'An error occurred');
    } finally {
      setLoading(false);
    }
  }, [url]);

  React.useEffect(() => {
    fetchDataCallback();
  }, [fetchDataCallback]);

  return { data, loading, error, refetch: fetchDataCallback };
}

// 使用 API Hook
interface User {
  id: string;
  name: string;
  email: string;
}

const UserList: React.FC = () => {
  const { data: users, loading, error, refetch } = useApi<User[]>('/api/users');

  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error}</div>;
  if (!users) return <div>No users found</div>;

  return (
    <div>
      <button onClick={refetch}>Refresh</button>
      <ul>
        {users.map(user => (
          <li key={user.id}>
            {user.name} - {user.email}
          </li>
        ))}
      </ul>
    </div>
  );
};
```

## 类组件

### 基本类组件
```typescript
// 基本类组件定义
interface UserCardProps {
  user: {
    id: string;
    name: string;
    email: string;
    age: number;
  };
  onEdit?: (user: UserCardProps['user']) => void;
  onDelete?: (id: string) => void;
}

interface UserCardState {
  isEditing: boolean;
  editedName: string;
  editedEmail: string;
}

class UserCard extends React.Component<UserCardProps, UserCardState> {
  constructor(props: UserCardProps) {
    super(props);
    
    this.state = {
      isEditing: false,
      editedName: props.user.name,
      editedEmail: props.user.email
    };
  }

  handleEdit = () => {
    this.setState({ isEditing: true });
  };

  handleCancel = () => {
    this.setState({
      isEditing: false,
      editedName: this.props.user.name,
      editedEmail: this.props.user.email
    });
  };

  handleSave = () => {
    const { user, onEdit } = this.props;
    const { editedName, editedEmail } = this.state;
    
    if (onEdit) {
      onEdit({
        ...user,
        name: editedName,
        email: editedEmail
      });
    }
    
    this.setState({ isEditing: false });
  };

  handleNameChange = (e: React.ChangeEvent<HTMLInputElement>) => {
    this.setState({ editedName: e.target.value });
  };

  handleEmailChange = (e: React.ChangeEvent<HTMLInputElement>) => {
    this.setState({ editedEmail: e.target.value });
  };

  render() {
    const { user, onDelete } = this.props;
    const { isEditing, editedName, editedEmail } = this.state;

    return (
      <div className="user-card">
        {isEditing ? (
          <div>
            <input
              type="text"
              value={editedName}
              onChange={this.handleNameChange}
            />
            <input
              type="email"
              value={editedEmail}
              onChange={this.handleEmailChange}
            />
            <button onClick={this.handleSave}>Save</button>
            <button onClick={this.handleCancel}>Cancel</button>
          </div>
        ) : (
          <div>
            <h3>{user.name}</h3>
            <p>Email: {user.email}</p>
            <p>Age: {user.age}</p>
            <button onClick={this.handleEdit}>Edit</button>
            {onDelete && (
              <button onClick={() => onDelete(user.id)}>Delete</button>
            )}
          </div>
        )}
      </div>
    );
  }
}
```

### 带生命周期的类组件
```typescript
// 带生命周期方法的类组件
interface UserProfileProps {
  userId: string;
}

interface UserProfileState {
  user: {
    id: string;
    name: string;
    email: string;
    createdAt: string;
  } | null;
  loading: boolean;
  error: string | null;
}

class UserProfile extends React.Component<UserProfileProps, UserProfileState> {
  private abortController: AbortController | null = null;

  constructor(props: UserProfileProps) {
    super(props);
    this.state = {
      user: null,
      loading: true,
      error: null
    };
  }

  componentDidMount() {
    this.fetchUser();
  }

  componentDidUpdate(prevProps: UserProfileProps) {
    if (prevProps.userId !== this.props.userId) {
      this.fetchUser();
    }
  }

  componentWillUnmount() {
    if (this.abortController) {
      this.abortController.abort();
    }
  }

  private fetchUser = async () => {
    this.setState({ loading: true, error: null });
    
    this.abortController = new AbortController();
    
    try {
      const response = await fetch(`/api/users/${this.props.userId}`, {
        signal: this.abortController.signal
      });
      
      if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`);
      }
      
      const user = await response.json();
      this.setState({ user, loading: false });
    } catch (error) {
      if (error instanceof Error && error.name !== 'AbortError') {
        this.setState({ 
          error: error.message, 
          loading: false 
        });
      }
    }
  };

  render() {
    const { user, loading, error } = this.state;

    if (loading) return <div>Loading...</div>;
    if (error) return <div>Error: {error}</div>;
    if (!user) return <div>User not found</div>;

    return (
      <div className="user-profile">
        <h2>{user.name}</h2>
        <p>Email: {user.email}</p>
        <p>Member since: {new Date(user.createdAt).toLocaleDateString()}</p>
      </div>
    );
  }
}
```

### 带 Refs 的类组件
```typescript
// 带 Refs 的类组件
interface FocusableInputProps {
  initialValue?: string;
  placeholder?: string;
  onEnter?: (value: string) => void;
}

class FocusableInput extends React.Component<FocusableInputProps> {
  private inputRef: React.RefObject<HTMLInputElement>;
  private containerRef: React.RefObject<HTMLDivElement>;

  constructor(props: FocusableInputProps) {
    super(props);
    this.inputRef = React.createRef();
    this.containerRef = React.createRef();
  }

  componentDidMount() {
    // 组件挂载后自动聚焦
    this.focusInput();
    
    // 添加键盘事件监听
    if (this.containerRef.current) {
      this.containerRef.current.addEventListener('keydown', this.handleKeyDown);
    }
  }

  componentWillUnmount() {
    // 清理事件监听
    if (this.containerRef.current) {
      this.containerRef.current.removeEventListener('keydown', this.handleKeyDown);
    }
  }

  focusInput = () => {
    if (this.inputRef.current) {
      this.inputRef.current.focus();
    }
  };

  blurInput = () => {
    if (this.inputRef.current) {
      this.inputRef.current.blur();
    }
  };

  selectAll = () => {
    if (this.inputRef.current) {
      this.inputRef.current.select();
    }
  };

  private handleKeyDown = (event: KeyboardEvent) => {
    if (event.key === 'Escape') {
      this.blurInput();
    } else if (event.key === 'Enter' && this.inputRef.current) {
      this.props.onEnter?.(this.inputRef.current.value);
    }
  };

  render() {
    const { initialValue = '', placeholder = '' } = this.props;

    return (
      <div ref={this.containerRef} className="focusable-input-container">
        <input
          ref={this.inputRef}
          type="text"
          defaultValue={initialValue}
          placeholder={placeholder}
          className="focusable-input"
        />
        <div className="input-actions">
          <button onClick={this.focusInput}>Focus</button>
          <button onClick={this.selectAll}>Select All</button>
          <button onClick={this.blurInput}>Blur</button>
        </div>
      </div>
    );
  }
}

// 使用带 Refs 的组件
const AppWithRefs = () => {
  const handleEnter = (value: string) => {
    console.log('Enter pressed with value:', value);
  };

  return (
    <div>
      <h1>Focusable Input Demo</h1>
      <FocusableInput 
        placeholder="Type something and press Enter"
        onEnter={handleEnter}
      />
    </div>
  );
};
```

## 属性类型检查

### 基本属性类型检查
```typescript
// 基本属性类型定义
interface ButtonProps {
  // 必需属性
  label: string;
  onClick: () => void;
  
  // 可选属性
  variant?: 'primary' | 'secondary' | 'danger';
  size?: 'small' | 'medium' | 'large';
  disabled?: boolean;
  
  // 联合类型属性
  icon?: string | React.ReactNode;
  
  // 函数属性
  onMouseEnter?: (event: React.MouseEvent<HTMLButtonElement>) => void;
  onMouseLeave?: (event: React.MouseEvent<HTMLButtonElement>) => void;
  
  // 任意属性
  [key: string]: any; // 不推荐，但有时需要
}

const Button: React.FC<ButtonProps> = ({ 
  label, 
  onClick, 
  variant = 'primary', 
  size = 'medium', 
  disabled = false,
  icon,
  ...restProps 
}) => {
  return (
    <button
      className={`btn btn-${variant} btn-${size} ${disabled ? 'disabled' : ''}`}
      onClick={onClick}
      disabled={disabled}
      {...restProps}
    >
      {icon && <span className="btn-icon">{icon}</span>}
      <span className="btn-label">{label}</span>
    </button>
  );
};

// 使用带类型检查的按钮
const ButtonDemo = () => {
  return (
    <div>
      <Button 
        label="Primary" 
        onClick={() => console.log('Primary clicked')}
      />
      <Button 
        label="Secondary with Icon" 
        onClick={() => console.log('Secondary clicked')}
        variant="secondary"
        icon="★"
      />
      <Button 
        label="Disabled Danger" 
        onClick={() => console.log('Should not fire')}
        variant="danger"
        disabled
      />
    </div>
  );
};
```

### 复杂属性类型检查
```typescript
// 复杂属性类型定义
interface FormFieldProps<T> {
  // 泛型属性
  value: T;
  onChange: (value: T) => void;
  
  // 条件属性
  required?: boolean;
  validation?: (value: T) => string | null;
  
  // 联合类型属性
  type: 'text' | 'number' | 'email' | 'password' | 'select';
  
  // 对象属性
  config?: {
    placeholder?: string;
    minLength?: number;
    maxLength?: number;
    min?: number;
    max?: number;
    options?: Array<{ value: string; label: string }>;
  };
  
  // 样式属性
  className?: string;
  style?: React.CSSProperties;
}

const FormField = <T,>({ 
  value, 
  onChange, 
  required = false, 
  validation,
  type,
  config = {},
  className = '',
  style = {}
}: FormFieldProps<T>) => {
  const [error, setError] = React.useState<string | null>(null);
  
  const handleChange = (newValue: T) => {
    if (validation) {
      const validationError = validation(newValue);
      setError(validationError);
    }
    onChange(newValue);
  };

  const renderInput = () => {
    switch (type) {
      case 'text':
      case 'email':
      case 'password':
        return (
          <input
            type={type}
            value={value as unknown as string}
            onChange={(e) => handleChange(e.target.value as unknown as T)}
            placeholder={config.placeholder}
            minLength={config.minLength}
            maxLength={config.maxLength}
            required={required}
            className={className}
            style={style}
          />
        );
      
      case 'number':
        return (
          <input
            type="number"
            value={value as unknown as number}
            onChange={(e) => handleChange(Number(e.target.value) as unknown as T)}
            min={config.min}
            max={config.max}
            required={required}
            className={className}
            style={style}
          />
        );
      
      case 'select':
        return (
          <select
            value={value as unknown as string}
            onChange={(e) => handleChange(e.target.value as unknown as T)}
            required={required}
            className={className}
            style={style}
          >
            {config.options?.map(option => (
              <option key={option.value} value={option.value}>
                {option.label}
              </option>
            ))}
          </select>
        );
      
      default:
        return null;
    }
  };

  return (
    <div className="form-field">
      {renderInput()}
      {error && <span className="error-message">{error}</span>}
    </div>
  );
};

// 使用复杂属性的表单字段
const FormDemo = () => {
  const [name, setName] = React.useState('');
  const [email, setEmail] = React.useState('');
  const [age, setAge] = React.useState(18);

  const validateEmail = (email: string): string | null => {
    return /\S+@\S+\.\S+/.test(email) ? null : 'Invalid email format';
  };

  return (
    <form>
      <FormField
        label="Name"
        value={name}
        onChange={setName}
        type="text"
        config={{ placeholder: "Enter your name", minLength: 2 }}
        required
      />
      
      <FormField
        label="Email"
        value={email}
        onChange={setEmail}
        type="email"
        config={{ placeholder: "Enter your email" }}
        validation={validateEmail}
        required
      />
      
      <FormField
        label="Age"
        value={age}
        onChange={setAge}
        type="number"
        config={{ min: 18, max: 120 }}
        required
      />
    </form>
  );
};
```

### 属性默认值和解构
```typescript
// 属性默认值和解构
interface CardProps {
  title: string;
  children: React.ReactNode;
  variant?: 'default' | 'success' | 'warning' | 'error';
  shadow?: boolean;
  rounded?: boolean;
  className?: string;
  style?: React.CSSProperties;
}

// 使用默认参数
const Card = ({
  title,
  children,
  variant = 'default',
  shadow = true,
  rounded = true,
  className = '',
  style = {}
}: CardProps) => {
  const cardClassName = [
    'card',
    `card-${variant}`,
    shadow ? 'card-shadow' : '',
    rounded ? 'card-rounded' : '',
    className
  ].filter(Boolean).join(' ');

  return (
    <div className={cardClassName} style={style}>
      <div className="card-header">
        <h3>{title}</h3>
      </div>
      <div className="card-body">
        {children}
      </div>
    </div>
  );
};

// 使用 defaultProps（不推荐，但有时会遇到）
class OldStyleCard extends React.Component<CardProps> {
  static defaultProps: Partial<CardProps> = {
    variant: 'default',
    shadow: true,
    rounded: true,
    className: '',
    style: {}
  };

  render() {
    const { title, children, variant, shadow, rounded, className, style } = this.props;
    
    const cardClassName = [
      'card',
      `card-${variant}`,
      shadow ? 'card-shadow' : '',
      rounded ? 'card-rounded' : '',
      className
    ].filter(Boolean).join(' ');

    return (
      <div className={cardClassName} style={style}>
        <div className="card-header">
          <h3>{title}</h3>
        </div>
        <div className="card-body">
          {children}
        </div>
      </div>
    );
  }
}

// 条件属性类型
interface ConditionalProps {
  type: 'input' | 'select' | 'textarea';
  value: string;
  onChange: (value: string) => void;
  // 条件属性 - 只在特定 type 下存在
  placeholder?: string;  // input 和 textarea
  options?: Array<{ value: string; label: string }>; // select
  rows?: number;  // textarea
  multiple?: boolean; // select
}

const ConditionalInput: React.FC<ConditionalProps> = (props) => {
  const { type, value, onChange, ...rest } = props;

  switch (type) {
    case 'input':
      return (
        <input
          type="text"
          value={value}
          onChange={(e) => onChange(e.target.value)}
          placeholder={rest.placeholder}
        />
      );
    
    case 'select':
      return (
        <select
          value={value}
          onChange={(e) => onChange(e.target.value)}
          multiple={rest.multiple}
        >
          {rest.options?.map(option => (
            <option key={option.value} value={option.value}>
              {option.label}
            </option>
          ))}
        </select>
      );
    
    case 'textarea':
      return (
        <textarea
          value={value}
          onChange={(e) => onChange(e.target.value)}
          placeholder={rest.placeholder}
          rows={rest.rows}
        />
      );
    
    default:
      return null;
  }
};
```

## Children 类型

### 基本 Children 类型
```typescript
// React.Children 类型
// React.ReactNode - 所有可以作为 children 的类型
type ReactNode = 
  | ReactChild
  | ReactFragment
  | ReactPortal
  | boolean
  | null
  | undefined;

type ReactChild = ReactElement | ReactText;
type ReactText = string | number;
type ReactFragment = {} | ReactNodeArray;
interface ReactNodeArray extends Array<ReactNode> {}

// 基本 Children 使用
interface ContainerProps {
  children: React.ReactNode;
  title?: string;
}

const Container: React.FC<ContainerProps> = ({ children, title }) => {
  return (
    <div className="container">
      {title && <h2>{title}</h2>}
      <div className="container-content">
        {children}
      </div>
    </div>
  );
};

// 使用 Container 组件
const ContainerDemo = () => {
  return (
    <Container title="My Container">
      <p>This is some content.</p>
      <button>Click me</button>
      {true && <span>Conditional content</span>}
      {null}
      {undefined}
      Simple text
      {42}
    </Container>
  );
};
```

### Children 操作和验证
```typescript
// 使用 React.Children API
interface ChildrenProcessorProps {
  children: React.ReactNode;
  separator?: React.ReactNode;
}

const ChildrenProcessor: React.FC<ChildrenProcessorProps> = ({ 
  children, 
  separator = ', ' 
}) => {
  // 过滤掉 null 和 undefined
  const validChildren = React.Children.toArray(children).filter(
    child => child !== null && child !== undefined
  );

  // 在每个子元素之间添加分隔符
  const childrenWithSeparators = validChildren.reduce<React.ReactNode[]>(
    (acc, child, index) => {
      if (index > 0) {
        acc.push(React.cloneElement(separator as React.ReactElement, { key: `sep-${index}` }));
      }
      acc.push(React.cloneElement(child as React.ReactElement, { key: `child-${index}` }));
      return acc;
    },
    []
  );

  return <div>{childrenWithSeparators}</div>;
};

// 使用 ChildrenProcessor
const ChildrenDemo = () => {
  return (
    <ChildrenProcessor separator=" | ">
      <span>First</span>
      <span>Second</span>
      {null}
      <span>Third</span>
      {undefined}
      <span>Fourth</span>
    </ChildrenProcessor>
  );
};

// Children 映射和转换
interface ChildrenMapperProps {
  children: React.ReactNode;
  mapFunction: (child: React.ReactNode, index: number) => React.ReactNode;
}

const ChildrenMapper: React.FC<ChildrenMapperProps> = ({ 
  children, 
  mapFunction 
}) => {
  return (
    <div>
      {React.Children.map(children, (child, index) => {
        if (React.isValidElement(child)) {
          return mapFunction(child, index);
        }
        return child;
      })}
    </div>
  );
};

// 使用 ChildrenMapper
const MapperDemo = () => {
  const addWrapper = (child: React.ReactNode, index: number) => {
    return (
      <div key={index} className="wrapped-item">
        {child}
      </div>
    );
  };

  return (
    <ChildrenMapper mapFunction={addWrapper}>
      <button>Button 1</button>
      <button>Button 2</button>
      <button>Button 3</button>
    </ChildrenMapper>
  );
};
```

### 复杂 Children 类型
```typescript
// 复杂 Children 类型检查
interface LayoutProps {
  header?: React.ReactNode;
  sidebar?: React.ReactNode;
  main: React.ReactNode;
  footer?: React.ReactNode;
}

const Layout: React.FC<LayoutProps> = ({ header, sidebar, main, footer }) => {
  return (
    <div className="layout">
      {header && <header className="layout-header">{header}</header>}
      <div className="layout-body">
        {sidebar && <aside className="layout-sidebar">{sidebar}</aside>}
        <main className="layout-main">{main}</main>
      </div>
      {footer && <footer className="layout-footer">{footer}</footer>}
    </div>
  );
};

// 使用复杂布局
const ComplexLayoutDemo = () => {
  return (
    <Layout
      header={<h1>Website Header</h1>}
      sidebar={
        <nav>
          <ul>
            <li><a href="#home">Home</a></li>
            <li><a href="#about">About</a></li>
            <li><a href="#contact">Contact</a></li>
          </ul>
        </nav>
      }
      main={
        <div>
          <h2>Main Content</h2>
          <p>This is the main content area.</p>
        </div>
      }
      footer={<p>© 2023 My Website</p>}
    />
  );
};

// Children 类型约束
interface StrictChildrenProps {
  children: React.ReactElement | React.ReactElement[];
}

const StrictContainer: React.FC<StrictChildrenProps> = ({ children }) => {
  // 只接受 ReactElement，不接受字符串、数字等
  return (
    <div className="strict-container">
      {React.Children.map(children, (child, index) => 
        React.cloneElement(child, { key: index })
      )}
    </div>
  );
};

// 使用严格 Children
const StrictDemo = () => {
  return (
    <StrictContainer>
      <div>First element</div>
      <div>Second element</div>
      <span>Third element</span>
    </StrictContainer>
  );
};

// 函数作为 Children
interface RenderPropsComponentProps {
  children: (data: { count: number; increment: () => void }) => React.ReactNode;
}

const RenderPropsComponent: React.FC<RenderPropsComponentProps> = ({ children }) => {
  const [count, setCount] = React.useState(0);
  
  const increment = () => setCount(c => c + 1);
  
  return <>{children({ count, increment })}</>;
};

// 使用 Render Props
const RenderPropsDemo = () => {
  return (
    <RenderPropsComponent>
      {({ count, increment }) => (
        <div>
          <p>Count: {count}</p>
          <button onClick={increment}>Increment</button>
        </div>
      )}
    </RenderPropsComponent>
  );
};
```

### Children 工具类型
```typescript
// 自定义 Children 工具类型
type ReactChildElement<T extends React.ElementType = React.ElementType> = 
  React.ReactElement<any, T>;

type ReactChildComponent<P = any> = 
  | ReactChildElement<React.ComponentType<P>>
  | React.FunctionComponentElement<P>;

// Children 类型守卫
interface ChildrenUtils {
  isElement: (child: React.ReactNode) => child is React.ReactElement;
  isDOMElement: (child: React.ReactNode) => child is React.DOMElement<any, Element>;
  isCompositeElement: (child: React.ReactNode) => child is React.ReactElement;
  isText: (child: React.ReactNode) => child is string | number;
}

const ChildrenUtils: ChildrenUtils = {
  isElement: React.isValidElement,
  isDOMElement: (child): child is React.DOMElement<any, Element> => 
    React.isValidElement(child) && typeof child.type === 'string',
  isCompositeElement: (child): child is React.ReactElement => 
    React.isValidElement(child) && typeof child.type !== 'string',
  isText: (child): child is string | number => 
    typeof child === 'string' || typeof child === 'number'
};

// 使用 Children 工具
interface SmartContainerProps {
  children: React.ReactNode;
  className?: string;
}

const SmartContainer: React.FC<SmartContainerProps> = ({ children, className = '' }) => {
  const processedChildren = React.Children.map(children, child => {
    if (ChildrenUtils.isDOMElement(child)) {
      // 为 DOM 元素添加默认类名
      return React.cloneElement(child, {
        className: `${child.props.className || ''} default-style`.trim()
      });
    } else if (ChildrenUtils.isCompositeElement(child)) {
      // 传递额外属性给组件元素
      return React.cloneElement(child, {
        containerClass: className
      });
    } else if (ChildrenUtils.isText(child)) {
      // 包装文本内容
      return <span className="text-wrapper">{child}</span>;
    }
    return child;
  });

  return (
    <div className={`smart-container ${className}`.trim()}>
      {processedChildren}
    </div>
  );
};

// 使用智能容器
const SmartContainerDemo = () => {
  return (
    <SmartContainer className="my-container">
      <div>Regular div</div>
      <p>Regular paragraph</p>
      Plain text content
      {42}
      <CustomComponent>Custom component</CustomComponent>
    </SmartContainer>
  );
};

// 自定义组件用于演示
const CustomComponent: React.FC<{ children: React.ReactNode; containerClass?: string }> = 
({ children, containerClass }) => {
  return (
    <div className={`custom-component ${containerClass || ''}`.trim()}>
      {children}
    </div>
  );
};
```


# 16. 迭代器和生成器

## 可迭代接口

### 基本可迭代接口
```typescript
// 可迭代接口定义
interface Iterable<T> {
    [Symbol.iterator](): Iterator<T>;
}

interface Iterator<T> {
    next(value?: any): IteratorResult<T>;
    return?(value?: any): IteratorResult<T>;
    throw?(e?: any): IteratorResult<T>;
}

interface IteratorResult<T> {
    done: boolean;
    value: T;
}

// 实现基本可迭代接口
class NumberSequence implements Iterable<number> {
    constructor(private start: number, private end: number) {}
    
    [Symbol.iterator](): Iterator<number> {
        let current = this.start;
        return {
            next: (): IteratorResult<number> => {
                if (current <= this.end) {
                    return { done: false, value: current++ };
                } else {
                    return { done: true, value: undefined as any };
                }
            }
        };
    }
}

// 使用可迭代对象
let sequence = new NumberSequence(1, 5);
for (let num of sequence) {
    console.log(num); // 1, 2, 3, 4, 5
}

// 将可迭代对象转换为数组
let numbers = Array.from(sequence); // [1, 2, 3, 4, 5]
```

### 内置可迭代对象
```typescript
// 数组是可迭代的
let arr: number[] = [1, 2, 3, 4, 5];
for (let item of arr) {
    console.log(item);
}

// 字符串是可迭代的
let str: string = "hello";
for (let char of str) {
    console.log(char); // h, e, l, l, o
}

// Map 是可迭代的
let map = new Map<string, number>([
    ["a", 1],
    ["b", 2],
    ["c", 3]
]);

for (let [key, value] of map) {
    console.log(`${key}: ${value}`);
}

// Set 是可迭代的
let set = new Set<number>([1, 2, 3, 4, 5]);
for (let item of set) {
    console.log(item);
}

// NodeList 是可迭代的（在现代浏览器中）
// for (let node of document.querySelectorAll('div')) {
//     console.log(node);
// }
```

### 自定义可迭代对象
```typescript
// 自定义可迭代对象示例
class FibonacciSequence implements Iterable<number> {
    constructor(private maxCount: number) {}
    
    [Symbol.iterator](): Iterator<number> {
        let count = 0;
        let prev = 0;
        let curr = 1;
        
        return {
            next: (): IteratorResult<number> => {
                if (count < this.maxCount) {
                    let result = prev;
                    [prev, curr] = [curr, prev + curr];
                    count++;
                    return { done: false, value: result };
                } else {
                    return { done: true, value: undefined as any };
                }
            }
        };
    }
}

// 使用斐波那契序列
let fib = new FibonacciSequence(10);
for (let num of fib) {
    console.log(num); // 0, 1, 1, 2, 3, 5, 8, 13, 21, 34
}

// 转换为数组
let fibArray = Array.from(new FibonacciSequence(8));
console.log(fibArray); // [0, 1, 1, 2, 3, 5, 8, 13]

// 可迭代对象的解构
let [first, second, third] = new FibonacciSequence(10);
console.log(first, second, third); // 0, 1, 1

// 扩展运算符与可迭代对象
let moreNumbers = [0, ...new FibonacciSequence(5), 100];
console.log(moreNumbers); // [0, 0, 1, 1, 2, 3, 100]
```

### 可迭代接口的高级用法
```typescript
// 带参数的可迭代对象
class Range implements Iterable<number> {
    constructor(
        private start: number, 
        private end: number, 
        private step: number = 1
    ) {}
    
    [Symbol.iterator](): Iterator<number> {
        let current = this.start;
        return {
            next: (): IteratorResult<number> => {
                if (current <= this.end) {
                    let value = current;
                    current += this.step;
                    return { done: false, value };
                } else {
                    return { done: true, value: undefined as any };
                }
            }
        };
    }
}

// 使用范围迭代器
let range = new Range(0, 10, 2);
for (let num of range) {
    console.log(num); // 0, 2, 4, 6, 8, 10
}

// 可迭代对象的组合
class CombinedIterable<T> implements Iterable<T> {
    constructor(private iterables: Iterable<T>[]) {}
    
    [Symbol.iterator](): Iterator<T> {
        let iterators = this.iterables.map(iter => iter[Symbol.iterator]());
        let currentIndex = 0;
        
        return {
            next: (): IteratorResult<T> => {
                while (currentIndex < iterators.length) {
                    let result = iterators[currentIndex].next();
                    if (!result.done) {
                        return result;
                    }
                    currentIndex++;
                }
                return { done: true, value: undefined as any };
            }
        };
    }
}

// 组合多个可迭代对象
let combined = new CombinedIterable([
    [1, 2, 3],
    new Range(4, 6),
    new Set([7, 8, 9])
]);

for (let item of combined) {
    console.log(item); // 1, 2, 3, 4, 5, 6, 7, 8, 9
}
```

## 生成器函数

### 基本生成器函数
```typescript
// 基本生成器函数
function* simpleGenerator(): Generator<number> {
    yield 1;
    yield 2;
    yield 3;
}

// 使用生成器函数
let gen = simpleGenerator();
console.log(gen.next()); // { value: 1, done: false }
console.log(gen.next()); // { value: 2, done: false }
console.log(gen.next()); // { value: 3, done: false }
console.log(gen.next()); // { value: undefined, done: true }

// 生成器函数的类型定义
type SimpleGenerator = Generator<number, void, unknown>;

function* typedGenerator(): SimpleGenerator {
    yield 1;
    yield 2;
    yield 3;
}

// 带返回值的生成器
function* generatorWithReturn(): Generator<number, string, unknown> {
    yield 1;
    yield 2;
    return "finished";
}

let genWithReturn = generatorWithReturn();
console.log(genWithReturn.next()); // { value: 1, done: false }
console.log(genWithReturn.next()); // { value: 2, done: false }
console.log(genWithReturn.next()); // { value: "finished", done: true }
```

### 生成器函数的实际应用
```typescript
// 生成器实现斐波那契数列
function* fibonacciGenerator(maxCount: number): Generator<number> {
    let count = 0;
    let prev = 0;
    let curr = 1;
    
    while (count < maxCount) {
        yield prev;
        [prev, curr] = [curr, prev + curr];
        count++;
    }
}

// 使用斐波那契生成器
for (let num of fibonacciGenerator(10)) {
    console.log(num); // 0, 1, 1, 2, 3, 5, 8, 13, 21, 34
}

// 生成器实现范围
function* rangeGenerator(start: number, end: number, step: number = 1): Generator<number> {
    for (let i = start; i <= end; i += step) {
        yield i;
    }
}

// 使用范围生成器
let rangeArray = Array.from(rangeGenerator(0, 10, 2));
console.log(rangeArray); // [0, 2, 4, 6, 8, 10]

// 生成器处理异步操作
async function* asyncNumberGenerator(): AsyncGenerator<number> {
    for (let i = 1; i <= 5; i++) {
        await new Promise(resolve => setTimeout(resolve, 1000));
        yield i;
    }
}

// 使用异步生成器
async function useAsyncGenerator() {
    for await (let num of asyncNumberGenerator()) {
        console.log(num); // 1, 2, 3, 4, 5 (每秒输出一个)
    }
}

// 生成器实现数据管道
function* numberGenerator(): Generator<number> {
    yield 1;
    yield 2;
    yield 3;
    yield 4;
    yield 5;
}

function* filterEven(iterable: Iterable<number>): Generator<number> {
    for (let item of iterable) {
        if (item % 2 === 0) {
            yield item;
        }
    }
}

function* multiply(iterable: Iterable<number>, factor: number): Generator<number> {
    for (let item of iterable) {
        yield item * factor;
    }
}

// 组合生成器
let pipeline = multiply(filterEven(numberGenerator()), 10);
for (let item of pipeline) {
    console.log(item); // 20, 40
}
```

### 生成器函数的高级特性
```typescript
// 生成器函数接收参数
function* parameterizedGenerator(): Generator<number, void, number> {
    let input = yield 1;
    console.log(`Received: ${input}`);
    yield input! * 2;
    let secondInput = yield input! * 3;
    console.log(`Second received: ${secondInput}`);
    return secondInput! * 4;
}

let paramGen = parameterizedGenerator();
console.log(paramGen.next());           // { value: 1, done: false }
console.log(paramGen.next(10));        // Received: 10, { value: 20, done: false }
console.log(paramGen.next(5));         // Second received: 5, { value: 20, done: true }

// 生成器抛出异常
function* errorGenerator(): Generator<number> {
    try {
        yield 1;
        yield 2;
        yield 3;
    } catch (error) {
        console.log(`Caught error: ${error}`);
        yield 4;
    }
}

let errorGen = errorGenerator();
console.log(errorGen.next()); // { value: 1, done: false }
console.log(errorGen.next()); // { value: 2, done: false }
console.log(errorGen.throw(new Error("Something went wrong"))); // Caught error: Error: Something went wrong, { value: 4, done: false }
console.log(errorGen.next()); // { value: undefined, done: true }

// 生成器提前返回
function* earlyReturnGenerator(): Generator<number> {
    yield 1;
    yield 2;
    yield 3;
    yield 4;
    yield 5;
}

let earlyGen = earlyReturnGenerator();
console.log(earlyGen.next()); // { value: 1, done: false }
console.log(earlyGen.return("early exit")); // { value: "early exit", done: true }
console.log(earlyGen.next()); // { value: undefined, done: true }
```

### 生成器与类结合
```typescript
// 生成器方法
class DataProcessor {
    private data: number[] = [1, 2, 3, 4, 5];
    
    *processData(): Generator<number> {
        for (let item of this.data) {
            yield item * 2;
        }
    }
    
    *filterData(condition: (item: number) => boolean): Generator<number> {
        for (let item of this.data) {
            if (condition(item)) {
                yield item;
            }
        }
    }
    
    *transformData(transformer: (item: number) => number): Generator<number> {
        for (let item of this.data) {
            yield transformer(item);
        }
    }
}

// 使用类生成器方法
let processor = new DataProcessor();

for (let item of processor.processData()) {
    console.log(item); // 2, 4, 6, 8, 10
}

for (let item of processor.filterData(x => x > 3)) {
    console.log(item); // 4, 5
}

for (let item of processor.transformData(x => x ** 2)) {
    console.log(item); // 1, 4, 9, 16, 25
}

// 静态生成器方法
class MathUtils {
    static *range(start: number, end: number, step: number = 1): Generator<number> {
        for (let i = start; i <= end; i += step) {
            yield i;
        }
    }
    
    static *fibonacci(count: number): Generator<number> {
        let [prev, curr] = [0, 1];
        for (let i = 0; i < count; i++) {
            yield prev;
            [prev, curr] = [curr, prev + curr];
        }
    }
}

// 使用静态生成器方法
console.log(Array.from(MathUtils.range(1, 10, 2))); // [1, 3, 5, 7, 9]
console.log(Array.from(MathUtils.fibonacci(8))); // [0, 1, 1, 2, 3, 5, 8, 13]
```

## for..of 语句

### 基本 for..of 用法
```typescript
// for..of 与数组
let numbers: number[] = [1, 2, 3, 4, 5];
for (let num of numbers) {
    console.log(num);
}

// for..of 与字符串
let text: string = "hello";
for (let char of text) {
    console.log(char); // h, e, l, l, o
}

// for..of 与 Map
let map = new Map<string, number>([
    ["a", 1],
    ["b", 2],
    ["c", 3]
]);

for (let [key, value] of map) {
    console.log(`${key}: ${value}`);
}

// for..of 与 Set
let set = new Set<string>(["apple", "banana", "orange"]);
for (let fruit of set) {
    console.log(fruit);
}

// for..of 与生成器
function* colorGenerator(): Generator<string> {
    yield "red";
    yield "green";
    yield "blue";
}

for (let color of colorGenerator()) {
    console.log(color); // red, green, blue
}
```

### for..of 与解构
```typescript
// for..of 与数组解构
let pairs: [string, number][] = [
    ["a", 1],
    ["b", 2],
    ["c", 3]
];

for (let [key, value] of pairs) {
    console.log(`${key}: ${value}`);
}

// for..of 与对象解构（需要自定义迭代器）
interface Person {
    name: string;
    age: number;
}

class PeopleCollection implements Iterable<Person> {
    constructor(private people: Person[]) {}
    
    *[Symbol.iterator](): Iterator<Person> {
        for (let person of this.people) {
            yield person;
        }
    }
}

let people = new PeopleCollection([
    { name: "Alice", age: 30 },
    { name: "Bob", age: 25 },
    { name: "Charlie", age: 35 }
]);

for (let { name, age } of people) {
    console.log(`${name} is ${age} years old`);
}

// for..of 与嵌套解构
let matrix: [number, number][][] = [
    [[1, 2], [3, 4]],
    [[5, 6], [7, 8]]
];

for (let [row1, row2] of matrix) {
    console.log(`Row 1: [${row1}], Row 2: [${row2}]`);
}

for (let [[a, b], [c, d]] of matrix) {
    console.log(`a=${a}, b=${b}, c=${c}, d=${d}`);
}
```

### for..of 与类型安全
```typescript
// for..of 的类型推断
let items: (string | number)[] = ["hello", 42, "world", 100];

for (let item of items) {
    // item 的类型是 string | number
    if (typeof item === "string") {
        console.log(item.toUpperCase()); // 类型安全
    } else {
        console.log(item.toFixed(2)); // 类型安全
    }
}

// for..of 与泛型
function processIterable<T>(iterable: Iterable<T>): T[] {
    let result: T[] = [];
    for (let item of iterable) {
        result.push(item);
    }
    return result;
}

let stringArray = processIterable(["a", "b", "c"]); // string[]
let numberArray = processIterable(new Set([1, 2, 3])); // number[]

// for..of 与联合类型
type DataItem = { type: "string"; value: string } | { type: "number"; value: number };

function* dataGenerator(): Generator<DataItem> {
    yield { type: "string", value: "hello" };
    yield { type: "number", value: 42 };
    yield { type: "string", value: "world" };
}

for (let item of dataGenerator()) {
    // TypeScript 可以正确推断 item 的类型
    if (item.type === "string") {
        console.log(item.value.toUpperCase()); // 安全访问 string 方法
    } else {
        console.log(item.value.toFixed(2)); // 安全访问 number 方法
    }
}
```

### for..of 的性能考虑
```typescript
// for..of 与传统循环的性能比较
let largeArray = Array.from({ length: 1000000 }, (_, i) => i);

// for..of 循环
console.time("for..of");
let sum1 = 0;
for (let item of largeArray) {
    sum1 += item;
}
console.timeEnd("for..of");

// 传统 for 循环
console.time("traditional for");
let sum2 = 0;
for (let i = 0; i < largeArray.length; i++) {
    sum2 += largeArray[i];
}
console.timeEnd("traditional for");

// forEach 循环
console.time("forEach");
let sum3 = 0;
largeArray.forEach(item => {
    sum3 += item;
});
console.timeEnd("forEach");

// 注意：实际性能可能因 JavaScript 引擎而异
```

## Iterator 和 Generator 类型

### Iterator 类型详解
```typescript
// Iterator 类型定义
interface Iterator<T, TReturn = any, TNext = undefined> {
    // TReturn: next() 方法返回值中的 value 类型（当 done 为 true 时）
    // TNext: next() 方法接收的参数类型
    next(...args: [] | [TNext]): IteratorResult<T, TReturn>;
    return?(value?: TReturn): IteratorResult<T, TReturn>;
    throw?(e?: any): IteratorResult<T, TReturn>;
}

interface IteratorResult<T, TReturn = any> {
    done: false;
    value: T;
} | {
    done: true;
    value: TReturn;
}

// 基本 Iterator 类型使用
type NumberIterator = Iterator<number>;
type StringIterator = Iterator<string, string>; // 返回字符串
type BooleanIterator = Iterator<boolean, void, number>; // 接收数字参数

// 实现自定义 Iterator
class CustomIterator implements Iterator<string> {
    private index = 0;
    private items = ["first", "second", "third"];
    
    next(): IteratorResult<string> {
        if (this.index < this.items.length) {
            return {
                done: false,
                value: this.items[this.index++]
            };
        } else {
            return {
                done: true,
                value: undefined as any
            };
        }
    }
}

// 使用自定义 Iterator
let customIter = new CustomIterator();
console.log(customIter.next()); // { done: false, value: "first" }
console.log(customIter.next()); // { done: false, value: "second" }
console.log(customIter.next()); // { done: false, value: "third" }
console.log(customIter.next()); // { done: true, value: undefined }
```

### Generator 类型详解
```typescript
// Generator 类型定义
interface Generator<T = unknown, TReturn = any, TNext = unknown> 
    extends Iterator<T, TReturn, TNext> {
    // Generator 继承自 Iterator，添加了额外的方法
    next(...args: [] | [TNext]): IteratorResult<T, TReturn>;
    return(value: TReturn): IteratorResult<T, TReturn>;
    throw(e: any): IteratorResult<T, TReturn>;
    
    // Symbol.iterator 使 Generator 本身也是可迭代的
    [Symbol.iterator](): Generator<T, TReturn, TNext>;
}

// Generator 类型参数
// T: 生成的值的类型
// TReturn: return() 方法的返回值类型
// TNext: next() 方法接收的参数类型

type SimpleGenerator = Generator<number>;
type GeneratorWithReturn = Generator<number, string>;
type GeneratorWithNext = Generator<number, void, string>;
type FullGenerator = Generator<number, string, boolean>;

// 基本 Generator 类型使用
function* basicGenerator(): Generator<number> {
    yield 1;
    yield 2;
    yield 3;
}

// 带返回值的 Generator
function* generatorWithReturnType(): Generator<number, string> {
    yield 1;
    yield 2;
    return "finished";
}

// 接收参数的 Generator
function* generatorWithNextType(): Generator<number, void, string> {
    let input = yield 1;
    console.log(`Received: ${input}`);
    yield 2;
}

// 完整类型的 Generator
function* fullGenerator(): Generator<number, string, boolean> {
    let shouldContinue = yield 1;
    if (shouldContinue) {
        yield 2;
        return "completed";
    } else {
        return "aborted";
    }
}
```

### AsyncIterator 和 AsyncGenerator 类型
```typescript
// AsyncIterator 类型
interface AsyncIterator<T, TReturn = any, TNext = undefined> {
    next(...args: [] | [TNext]): Promise<IteratorResult<T, TReturn>>;
    return?(value?: TReturn): Promise<IteratorResult<T, TReturn>>;
    throw?(e?: any): Promise<IteratorResult<T, TReturn>>;
}

// AsyncGenerator 类型
interface AsyncGenerator<T = unknown, TReturn = any, TNext = unknown> 
    extends AsyncIterator<T, TReturn, TNext> {
    next(...args: [] | [TNext]): Promise<IteratorResult<T, TReturn>>;
    return(value: TReturn): Promise<IteratorResult<T, TReturn>>;
    throw(e: any): Promise<IteratorResult<T, TReturn>>;
    [Symbol.asyncIterator](): AsyncGenerator<T, TReturn, TNext>;
}

// 异步生成器函数
async function* asyncGenerator(): AsyncGenerator<number> {
    for (let i = 1; i <= 5; i++) {
        await new Promise(resolve => setTimeout(resolve, 100));
        yield i;
    }
}

// 使用异步生成器
async function useAsyncGenerator() {
    for await (let num of asyncGenerator()) {
        console.log(num); // 1, 2, 3, 4, 5 (每 100ms 输出一个)
    }
}

// 异步生成器的完整类型
async function* fullAsyncGenerator(): AsyncGenerator<string, number, boolean> {
    let shouldContinue = yield "first";
    if (shouldContinue) {
        yield "second";
        return 42;
    } else {
        return 0;
    }
}

// 使用完整的异步生成器
async function useFullAsyncGenerator() {
    let gen = fullAsyncGenerator();
    
    let first = await gen.next(); // { value: "first", done: false }
    console.log(first);
    
    let second = await gen.next(true); // { value: "second", done: false }
    console.log(second);
    
    let result = await gen.next(); // { value: 42, done: true }
    console.log(result);
}
```

### 实用工具类型
```typescript
// 自定义 Iterator 工具类型
type IteratorElementType<T> = T extends Iterator<infer U> ? U : never;
type GeneratorElementType<T> = T extends Generator<infer U> ? U : never;
type AsyncIteratorElementType<T> = T extends AsyncIterator<infer U> ? U : never;

// 使用工具类型
type MyIterator = Iterator<string>;
type MyIteratorElement = IteratorElementType<MyIterator>; // string

type MyGenerator = Generator<number>;
type MyGeneratorElement = GeneratorElementType<MyGenerator>; // number

type MyAsyncIterator = AsyncIterator<boolean>;
type MyAsyncIteratorElement = AsyncIteratorElementType<MyAsyncIterator>; // boolean

// 创建可迭代的工具函数
function createIterable<T>(items: T[]): Iterable<T> {
    return {
        *[Symbol.iterator]() {
            for (let item of items) {
                yield item;
            }
        }
    };
}

// 创建异步可迭代的工具函数
async function* createAsyncIterable<T>(
    items: T[],
    delay: number = 0
): AsyncGenerator<T> {
    for (let item of items) {
        if (delay > 0) {
            await new Promise(resolve => setTimeout(resolve, delay));
        }
        yield item;
    }
}

// 使用工具函数
let iterable = createIterable([1, 2, 3, 4, 5]);
for (let item of iterable) {
    console.log(item);
}

async function useAsyncIterable() {
    for await (let item of createAsyncIterable(["a", "b", "c"], 1000)) {
        console.log(item); // 每秒输出一个
    }
}

// 类型安全的迭代器包装器
class IteratorWrapper<T> implements Iterable<T> {
    constructor(private iterator: Iterator<T>) {}
    
    *[Symbol.iterator](): Iterator<T> {
        let result = this.iterator.next();
        while (!result.done) {
            yield result.value;
            result = this.iterator.next();
        }
    }
}

// 使用迭代器包装器
let wrapper = new IteratorWrapper(basicGenerator());
for (let item of wrapper) {
    console.log(item); // 1, 2, 3
}
```


# 17. 模块解析

## 相对与非相对模块导入

### 相对模块导入
```typescript
// 相对导入使用 ./ 或 ../ 开头
// 文件结构：
// src/
//   ├── components/
//   │   ├── Button.ts
//   │   └── Header.ts
//   ├── utils/
//   │   ├── helpers.ts
//   │   └── validators.ts
//   └── index.ts

// 在 src/components/Header.ts 中
import { Button } from './Button';           // 同级文件
import { validateEmail } from '../utils/validators';  // 上级目录
import { formatDate } from '../utils/helpers';        // 上级目录

// 相对导入的特点：
// 1. 相对于当前文件位置解析
// 2. 必须包含文件扩展名（TypeScript 编译时会自动添加）
// 3. 通常用于项目内部模块

// 相对导入的实际示例
// src/models/User.ts
export interface User {
    id: string;
    name: string;
    email: string;
}

export class UserService {
    static createUser(userData: Omit<User, 'id'>): User {
        return {
            ...userData,
            id: Math.random().toString(36)
        };
    }
}

// src/components/UserForm.ts
import { User, UserService } from '../models/User';
import { validateEmail } from '../utils/validation';

export class UserForm {
    private user: User | null = null;
    
    submit(formData: { name: string; email: string }) {
        if (validateEmail(formData.email)) {
            this.user = UserService.createUser(formData);
            return this.user;
        }
        throw new Error('Invalid email');
    }
}
```

### 非相对模块导入
```typescript
// 非相对导入不以 ./ 或 ../ 开头
// 通常用于导入外部库或通过配置映射的模块

// 导入外部库
import React from 'react';
import lodash from 'lodash';
import express from 'express';

// 导入通过路径映射的模块
import { User } from '@models/User';
import { Button } from '@components/Button';
import { Logger } from '@utils/logger';

// 导入通过 baseUrl 配置的模块
import { Database } from 'database';
import { ApiClient } from 'services/api-client';

// 非相对导入的特点：
// 1. 在 node_modules 中查找
// 2. 通过 tsconfig.json 配置查找
// 3. 通常用于第三方库或项目根目录模块

// 非相对导入的实际示例
// src/services/UserService.ts
import { User } from '@models/User';  // 通过路径映射
import { Logger } from '@utils/Logger';  // 通过路径映射
import axios from 'axios';  // 第三方库

export class UserService {
    constructor(private logger: Logger) {}
    
    async fetchUser(id: string): Promise<User> {
        try {
            const response = await axios.get(`/api/users/${id}`);
            return response.data;
        } catch (error) {
            this.logger.error(`Failed to fetch user ${id}`, error);
            throw error;
        }
    }
}

// src/utils/Logger.ts
export class Logger {
    log(message: string): void {
        console.log(`[LOG] ${new Date().toISOString()} - ${message}`);
    }
    
    error(message: string, error?: any): void {
        console.error(`[ERROR] ${new Date().toISOString()} - ${message}`, error);
    }
}
```

### 混合导入示例
```typescript
// 项目结构示例：
// my-project/
//   ├── src/
//   │   ├── components/
//   │   │   ├── Button.ts
//   │   │   └── Form.ts
//   │   ├── models/
//   │   │   └── User.ts
//   │   ├── services/
//   │   │   └── ApiService.ts
//   │   ├── utils/
//   │   │   └── helpers.ts
//   │   └── index.ts
//   ├── node_modules/
//   │   └── lodash/
//   └── tsconfig.json

// src/components/Form.ts
// 相对导入 - 同级文件
import { Button } from './Button';

// 相对导入 - 上级目录
import { User } from '../models/User';

// 非相对导入 - 第三方库
import _ from 'lodash';

// 非相对导入 - 通过路径映射（需要 tsconfig.json 配置）
import { ApiService } from '@services/ApiService';
import { formatDate } from '@utils/helpers';

export class Form {
    constructor(private apiService: ApiService) {}
    
    handleSubmit(userData: Partial<User>) {
        // 使用 lodash
        const cleanData = _.omitBy(userData, _.isNil);
        
        // 使用工具函数
        console.log(`Submitted at: ${formatDate(new Date())}`);
        
        // 使用 API 服务
        return this.apiService.createUser(cleanData as User);
    }
}
```

## 模块解析策略

### Node 模块解析策略
```typescript
// tsconfig.json 配置
{
  "compilerOptions": {
    "moduleResolution": "node",  // 默认策略
    "target": "ES2020",
    "module": "commonjs"
  }
}

// Node 模块解析规则：

// 1. 相对导入解析
// import { helper } from './utils/helpers';
// 解析顺序：
// - ./utils/helpers.ts
// - ./utils/helpers.tsx
// - ./utils/helpers.d.ts
// - ./utils/helpers/package.json (如果包含 "types" 字段)
// - ./utils/helpers/index.ts
// - ./utils/helpers/index.tsx
// - ./utils/helpers/index.d.ts

// 2. 非相对导入解析
// import lodash from 'lodash';
// 解析顺序：
// - ./node_modules/lodash/package.json (检查 "types" 字段)
// - ./node_modules/lodash/index.d.ts
// - ./node_modules/lodash/lodash.d.ts
// - ../node_modules/lodash/package.json (向上级目录查找)
// - ../../node_modules/lodash/package.json (继续向上查找)

// 实际示例：
// 项目结构：
// project/
//   ├── src/
//   │   └── index.ts
//   ├── node_modules/
//   │   └── my-library/
//   │       ├── package.json
//   │       ├── index.js
//   │       └── index.d.ts
//   └── tsconfig.json

// my-library/package.json
{
  "name": "my-library",
  "version": "1.0.0",
  "main": "index.js",
  "types": "index.d.ts"  // TypeScript 会查找这个字段
}

// src/index.ts
import myLibrary from 'my-library';  // 解析到 node_modules/my-library/index.d.ts
```

### Classic 模块解析策略
```typescript
// tsconfig.json 配置
{
  "compilerOptions": {
    "moduleResolution": "classic",  // 仅用于 AMD | System | ES2015 模块
    "target": "ES2020",
    "module": "ES2015"
  }
}

// Classic 模块解析规则（较少使用）：

// 1. 相对导入解析
// import { helper } from './utils/helpers';
// 解析顺序：
// - ./utils/helpers.ts
// - ./utils/helpers.d.ts
// - ./utils/helpers.tsx

// 2. 非相对导入解析
// import lodash from 'lodash';
// 解析顺序：
// - / lodash.ts
// - / lodash.d.ts
// - / lodash.tsx

// 注意：Classic 策略已被弃用，建议使用 Node 策略
```

### 模块解析的高级配置
```typescript
// 复杂的模块解析配置
{
  "compilerOptions": {
    "moduleResolution": "node",
    "target": "ES2020",
    "module": "commonjs",
    
    // 允许合成默认导入
    "allowSyntheticDefaultImports": true,
    
    // ES 模块互操作
    "esModuleInterop": true,
    
    // 跳过库检查（提高编译速度）
    "skipLibCheck": true,
    
    // 解析 JSON 模块
    "resolveJsonModule": true,
    
    // 最大节点模块 JS 深度
    "maxNodeModuleJsDepth": 2
  },
  
  // 包含文件
  "include": [
    "src/**/*"
  ],
  
  // 排除文件
  "exclude": [
    "node_modules",
    "dist"
  ]
}

// 实际应用示例：
// src/config/app.json
{
  "appName": "My Application",
  "version": "1.0.0",
  "apiUrl": "https://api.example.com"
}

// src/services/ConfigService.ts
import appConfig from '../config/app.json';  // 需要 resolveJsonModule: true

export class ConfigService {
    static getConfig() {
        return appConfig;
    }
    
    static getApiUrl(): string {
        return appConfig.apiUrl;
    }
}

// src/index.ts
import React from 'react';  // 需要 esModuleInterop: true
import * as _ from 'lodash';  // 需要 allowSyntheticDefaultImports: true
import { ConfigService } from './services/ConfigService';

console.log(ConfigService.getConfig());
```

## 路径映射配置

### 基本路径映射
```typescript
// tsconfig.json 路径映射配置
{
  "compilerOptions": {
    "baseUrl": "./src",  // 基础目录
    "paths": {
      // 基本路径映射
      "@/*": ["./*"],
      "@components/*": ["./components/*"],
      "@models/*": ["./models/*"],
      "@services/*": ["./services/*"],
      "@utils/*": ["./utils/*"],
      
      // 具体文件映射
      "@config": ["./config/index"],
      "@logger": ["./utils/Logger"],
      
      // 多候选项映射
      "@shared/*": [
        "../shared/src/*",
        "./shared/*"
      ]
    }
  }
}

// 项目结构：
// project/
//   ├── src/
//   │   ├── components/
//   │   │   └── Button.ts
//   │   ├── models/
//   │   │   └── User.ts
//   │   ├── services/
//   │   │   └── ApiService.ts
//   │   ├── utils/
//   │   │   └── Logger.ts
//   │   ├── config/
//   │   │   └── index.ts
//   │   └── index.ts
//   └── tsconfig.json

// 使用路径映射的导入示例：
// src/index.ts
import { Button } from '@components/Button';
import { User } from '@models/User';
import { ApiService } from '@services/ApiService';
import { Logger } from '@logger';
import config from '@config';

// 不使用路径映射的等效导入：
// import { Button } from './components/Button';
// import { User } from './models/User';
// import { ApiService } from './services/ApiService';
// import { Logger } from './utils/Logger';
// import config from './config/index';
```

### 复杂路径映射
```typescript
// 复杂的路径映射配置
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      // 多级目录映射
      "@app/*": ["src/app/*"],
      "@shared/*": ["src/shared/*"],
      "@ui/*": ["src/components/ui/*"],
      "@features/*": ["src/features/*"],
      
      // 版本控制映射
      "@api/v1/*": ["src/api/v1/*"],
      "@api/v2/*": ["src/api/v2/*"],
      
      // 环境特定映射
      "@env/config": [
        "src/config/production",
        "src/config/development"
      ],
      
      // 备用路径映射
      "@legacy/*": [
        "src/legacy/*",
        "../legacy/src/*"
      ],
      
      // 别名映射
      "@utils": ["src/utils/index"],
      "@helpers": ["src/utils/helpers"],
      "@validators": ["src/utils/validators"],
      
      // 第三方库别名
      "lodash": ["node_modules/lodash-es"],
      "react": ["node_modules/preact/compat"],
      
      // 通配符映射
      "@assets/*": ["src/assets/*"],
      "@styles/*": ["src/styles/*"]
    }
  }
}

// 实际应用示例：
// src/features/user/UserService.ts
import { User } from '@models/User';  // 映射到 src/models/User.ts
import { Logger } from '@utils/Logger';  // 映射到 src/utils/Logger.ts
import { validateEmail } from '@validators';  // 映射到 src/utils/validators.ts

export class UserService {
    constructor(private logger: Logger) {}
    
    createUser(userData: Omit<User, 'id'>): User {
        if (!validateEmail(userData.email)) {
            throw new Error('Invalid email');
        }
        
        const user: User = {
            ...userData,
            id: Math.random().toString(36)
        };
        
        this.logger.log(`Created user: ${user.name}`);
        return user;
    }
}

// src/app/main.ts
import { UserService } from '@features/user/UserService';
import { Logger } from '@utils';
import config from '@env/config';

const logger = new Logger();
const userService = new UserService(logger);

// 使用配置
console.log(`App version: ${config.version}`);
```

### 路径映射与构建工具集成
```typescript
// webpack.config.js 集成路径映射
const path = require('path');

module.exports = {
  resolve: {
    alias: {
      '@': path.resolve(__dirname, 'src'),
      '@components': path.resolve(__dirname, 'src/components'),
      '@models': path.resolve(__dirname, 'src/models'),
      '@services': path.resolve(__dirname, 'src/services'),
      '@utils': path.resolve(__dirname, 'src/utils'),
      '@assets': path.resolve(__dirname, 'src/assets')
    },
    extensions: ['.ts', '.tsx', '.js', '.jsx']
  }
};

// jest.config.js 集成路径映射
module.exports = {
  moduleNameMapper: {
    '^@/(.*)$': '<rootDir>/src/$1',
    '^@components/(.*)$': '<rootDir>/src/components/$1',
    '^@models/(.*)$': '<rootDir>/src/models/$1',
    '^@services/(.*)$': '<rootDir>/src/services/$1',
    '^@utils/(.*)$': '<rootDir>/src/utils/$1',
    '^@assets/(.*)$': '<rootDir>/src/assets/$1'
  }
};

// 使用示例：
// src/components/UserProfile.tsx
import React from 'react';
import { User } from '@models/User';
import { Button } from '@components/Button';
import { formatDate } from '@utils/helpers';

interface UserProfileProps {
    user: User;
}

export const UserProfile: React.FC<UserProfileProps> = ({ user }) => {
    return (
        <div className="user-profile">
            <h2>{user.name}</h2>
            <p>Email: {user.email}</p>
            <p>Joined: {formatDate(user.createdAt)}</p>
            <Button onClick={() => console.log('Edit clicked')}>
                Edit Profile
            </Button>
        </div>
    );
};
```

## baseUrl 配置

### baseUrl 基础配置
```typescript
// baseUrl 配置示例
{
  "compilerOptions": {
    "baseUrl": "./src",  // 设置基础目录为 src
    "target": "ES2020",
    "module": "commonjs"
  }
}

// 项目结构：
// project/
//   ├── src/
//   │   ├── components/
//   │   │   └── Button.ts
//   │   ├── models/
//   │   │   └── User.ts
//   │   ├── services/
//   │   │   └── ApiService.ts
//   │   └── index.ts
//   └── tsconfig.json

// 使用 baseUrl 的导入示例：
// src/index.ts
import { Button } from 'components/Button';  // 解析到 src/components/Button.ts
import { User } from 'models/User';          // 解析到 src/models/User.ts
import { ApiService } from 'services/ApiService';  // 解析到 src/services/ApiService.ts

// 不使用 baseUrl 的等效导入：
// import { Button } from './components/Button';
// import { User } from './models/User';
// import { ApiService } from './services/ApiService';
```

### baseUrl 与路径映射结合
```typescript
// baseUrl 与路径映射结合使用
{
  "compilerOptions": {
    "baseUrl": "./src",  // baseUrl 作为路径映射的基础
    "paths": {
      // 相对于 baseUrl 的路径
      "@/*": ["./*"],                    // @/component/Button -> src/component/Button
      "@components/*": ["./components/*"],  // @components/Button -> src/components/Button
      "@models/*": ["./models/*"],          // @models/User -> src/models/User
      "@services/*": ["./services/*"],      // @services/ApiService -> src/services/ApiService
      
      // 绝对路径映射（相对于项目根目录）
      "shared/*": ["../shared/src/*"],      // shared/module -> ../shared/src/module
      
      // 多候选项
      "utils/*": [
        "./utils/*",           // src/utils/*
        "../shared/utils/*"    // ../shared/utils/*
      ]
    }
  }
}

// 实际应用示例：
// src/services/UserService.ts
import { User } from '@models/User';        // baseUrl + paths 映射
import { Logger } from 'utils/Logger';      // baseUrl 直接解析
import { validateEmail } from 'utils/validators';  // baseUrl 直接解析

export class UserService {
    private users: User[] = [];
    
    constructor(private logger: Logger) {}
    
    addUser(userData: Omit<User, 'id'>): User {
        if (!validateEmail(userData.email)) {
            throw new Error('Invalid email');
        }
        
        const user: User = {
            ...userData,
            id: Math.random().toString(36)
        };
        
        this.users.push(user);
        this.logger.log(`Added user: ${user.name}`);
        return user;
    }
}
```

### baseUrl 的高级用法
```typescript
// 复杂的 baseUrl 配置
{
  "compilerOptions": {
    "baseUrl": ".",  // 项目根目录
    "paths": {
      // 项目内部模块
      "@app/*": ["src/app/*"],
      "@shared/*": ["src/shared/*"],
      "@ui/*": ["src/components/ui/*"],
      
      // 第三方库重定向
      "react": ["node_modules/preact/compat"],
      "react-dom": ["node_modules/preact/compat"],
      
      // 别名简化
      "@config": ["src/config/index"],
      "@logger": ["src/utils/Logger"],
      "@types": ["src/types/index"],
      
      // 多项目共享
      "common/*": ["../common/src/*"],
      "shared/*": ["../shared/src/*"]
    }
  }
}

// 项目结构：
// workspace/
//   ├── project-a/
//   │   ├── src/
//   │   │   ├── app/
//   │   │   ├── components/
//   │   │   └── utils/
//   │   └── tsconfig.json
//   ├── common/
//   │   └── src/
//   │       ├── types/
//   │       └── utils/
//   └── shared/
//       └── src/
//           ├── models/
//           └── services/

// 使用示例：
// src/app/main.ts
import { AppComponent } from '@app/AppComponent';  // project-a/src/app/AppComponent
import { User } from 'shared/models/User';         // ../shared/src/models/User
import { Logger } from '@logger';                  // project-a/src/utils/Logger
import { AppConfig } from '@config';               // project-a/src/config/index
import { CommonUtils } from 'common/utils';        // ../common/src/utils

// 类型定义共享
// src/types/index.ts
export interface ApiResponse<T> {
    success: boolean;
     T;
    message?: string;
}

export type UserRole = 'admin' | 'user' | 'guest';

// 使用共享类型
// src/app/UserManager.ts
import { ApiResponse, UserRole } from '@types';
import { User } from 'shared/models/User';

export class UserManager {
    async getUsers(): Promise<ApiResponse<User[]>> {
        // 实现获取用户逻辑
        return {
            success: true,
             []
        };
    }
    
    checkUserRole(role: UserRole): boolean {
        return role === 'admin' || role === 'user';
    }
}
```

## rootDirs 配置

### rootDirs 基础概念
```typescript
// rootDirs 配置允许将多个目录视为一个虚拟目录结构
{
  "compilerOptions": {
    "rootDirs": [
      "src/views",
      "generated/templates"
    ],
    "outDir": "dist"
  }
}

// 项目结构：
// project/
//   ├── src/
//   │   └── views/
//   │       └── user-view.ts
//   ├── generated/
//   │   └── templates/
//   │       └── user-template.ts
//   └── tsconfig.json

// rootDirs 的作用：
// 1. 允许模块在不同的目录中"合并"
// 2. 编译时将这些目录视为一个虚拟目录
// 3. 便于代码生成和模板系统

// src/views/user-view.ts
import { UserTemplate } from './user-template';  // 可以导入 generated/templates 中的文件

// generated/templates/user-template.ts
export class UserTemplate {
    render(user: any): string {
        return `<div>${user.name}</div>`;
    }
}
```

### rootDirs 实际应用
```typescript
// 实际的 rootDirs 配置示例
{
  "compilerOptions": {
    "rootDirs": [
      "src",
      "generated",
      "shared"
    ],
    "outDir": "dist",
    "baseUrl": ".",
    "paths": {
      "@generated/*": ["generated/*"],
      "@shared/*": ["shared/*"]
    }
  }
}

// 项目结构：
// project/
//   ├── src/
//   │   ├── components/
//   │   │   └── UserComponent.ts
//   │   └── services/
//   │       └── UserService.ts
//   ├── generated/
//   │   ├── models/
//   │   │   └── GeneratedModels.ts
//   │   └── api/
//   │       └── GeneratedApi.ts
//   ├── shared/
//   │   ├── types/
//   │   │   └── SharedTypes.ts
//   │   └── utils/
//   │       └── SharedUtils.ts
//   └── tsconfig.json

// src/components/UserComponent.ts
import { UserService } from 'services/UserService';           // 来自 src
import { GeneratedUser } from 'models/GeneratedModels';       // 来自 generated
import { SharedType } from 'types/SharedTypes';               // 来自 shared
import { apiCall } from 'api/GeneratedApi';                   // 来自 generated

export class UserComponent {
    constructor(private userService: UserService) {}
    
    async renderUser(userId: string): Promise<string> {
        const user = await this.userService.getUser(userId);
        const generatedUser: GeneratedUser = {
            id: user.id,
            name: user.name,
            email: user.email
        };
        
        return apiCall('renderUser', generatedUser);
    }
}
```

### rootDirs 与代码生成
```typescript
// 代码生成场景的 rootDirs 配置
{
  "compilerOptions": {
    "rootDirs": [
      "src",
      "generated/client",
      "generated/server"
    ],
    "outDir": "dist",
    "declaration": true,
    "declarationDir": "types"
  }
}

// 项目结构：
// project/
//   ├── src/
//   │   ├── client/
//   │   │   └── App.ts
//   │   └── server/
//   │       └── Server.ts
//   ├── generated/
//   │   ├── client/
//   │   │   ├── api-client.ts
//   │   │   └── models.ts
//   │   └── server/
//   │       ├── database.ts
//   │       └── routes.ts
//   └── tsconfig.json

// 代码生成示例：
// 生成的客户端 API
// generated/client/api-client.ts
export interface User {
    id: string;
    name: string;
    email: string;
}

export async function fetchUser(id: string): Promise<User> {
    const response = await fetch(`/api/users/${id}`);
    return response.json();
}

// 生成的服务端路由
// generated/server/routes.ts
import { Request, Response } from 'express';

export function getUserRoute(req: Request, res: Response) {
    // 处理获取用户请求
    res.json({ id: '1', name: 'John', email: 'john@example.com' });
}

// src/client/App.ts
import { fetchUser } from 'api-client';  // 从 generated/client 导入
import { User } from 'models';           // 从 generated/client 导入

export class App {
    async loadUser(userId: string) {
        try {
            const user: User = await fetchUser(userId);
            console.log('Loaded user:', user);
        } catch (error) {
            console.error('Failed to load user:', error);
        }
    }
}

// src/server/Server.ts
import express from 'express';
import { getUserRoute } from 'routes';  // 从 generated/server 导入

export class Server {
    private app = express();
    
    constructor() {
        this.setupRoutes();
    }
    
    private setupRoutes() {
        this.app.get('/api/users/:id', getUserRoute);
    }
    
    start(port: number) {
        this.app.listen(port, () => {
            console.log(`Server running on port ${port}`);
        });
    }
}
```

### rootDirs 与构建系统集成
```typescript
// 复杂的构建系统配置
{
  "compilerOptions": {
    "rootDirs": [
      "src",
      "generated/types",
      "generated/api",
      "shared"
    ],
    "baseUrl": ".",
    "paths": {
      "@app/*": ["src/app/*"],
      "@generated/*": ["generated/*"],
      "@shared/*": ["shared/*"],
      "@types": ["generated/types/index"]
    },
    "outDir": "dist",
    "declaration": true,
    "composite": true
  },
  "references": [
    { "path": "./tsconfig.shared.json" }
  ]
}

// 构建脚本示例：
// package.json
{
  "scripts": {
    "prebuild": "npm run generate",
    "generate": "node scripts/generate-code.js",
    "build": "tsc --build",
    "watch": "tsc --build --watch",
    "clean": "tsc --build --clean"
  }
}

// 代码生成脚本示例：
// scripts/generate-code.js
const fs = require('fs');
const path = require('path');

// 生成 API 客户端
function generateApiClient() {
    const apiContent = `
export interface User {
    id: string;
    name: string;
    email: string;
}

export async function fetchUser(id: string): Promise<User> {
    // 实现 API 调用
    return { id, name: 'Generated User', email: 'generated@example.com' };
}
    `;
    
    fs.writeFileSync(
        path.join(__dirname, '../generated/api/client.ts'),
        apiContent.trim()
    );
}

// 生成类型定义
function generateTypes() {
    const typesContent = `
export type Status = 'pending' | 'approved' | 'rejected';
export type Priority = 'low' | 'medium' | 'high';

export interface ApiResponse<T> {
    success: boolean;
     T;
    message?: string;
}
    `;
    
    fs.writeFileSync(
        path.join(__dirname, '../generated/types/index.ts'),
        typesContent.trim()
    );
}

// 执行生成
generateApiClient();
generateTypes();
console.log('Code generation completed');

// 使用生成的代码：
// src/app/UserManager.ts
import { fetchUser } from '@generated/api/client';  // 生成的 API 客户端
import { Status, ApiResponse } from '@types';       // 生成的类型

export class UserManager {
    async loadUser(id: string): Promise<ApiResponse<User>> {
        try {
            const user = await fetchUser(id);
            return {
                success: true,
                 user
            };
        } catch (error) {
            return {
                success: false,
                message: error.message
            };
        }
    }
    
    checkStatus(status: Status): boolean {
        return status === 'approved';
    }
}
```


# 18. 命名空间 (Namespaces)

## 1. 命名空间语法

命名空间是 TypeScript 中组织代码的一种方式，用于避免命名冲突。

### 基本语法

```typescript
// 定义命名空间
namespace MyNamespace {
    export interface User {
        name: string;
        age: number;
    }
    
    export class UserService {
        static getUsers(): User[] {
            return [];
        }
    }
    
    // 内部成员（不导出）
    const secretKey = "secret";
    
    // 导出函数
    export function greet(name: string): string {
        return `Hello, ${name}!`;
    }
}

// 使用命名空间中的成员
const users = MyNamespace.UserService.getUsers();
console.log(MyNamespace.greet("Alice"));
```

### 嵌套命名空间

```typescript
namespace OuterNamespace {
    export namespace InnerNamespace {
        export class MyClass {
            constructor(public value: string) {}
        }
    }
    
    export function outerFunction(): void {
        console.log("Outer function called");
    }
}

// 使用嵌套命名空间
const instance = new OuterNamespace.InnerNamespace.MyClass("test");
OuterNamespace.outerFunction();
```

## 2. 多文件命名空间

可以将同一个命名空间分布在多个文件中。

### 文件1: Validation.ts
```typescript
namespace Validation {
    export interface StringValidator {
        isAcceptable(s: string): boolean;
    }
    
    const lettersRegexp = /^[A-Za-z]+$/;
    
    export class LettersOnlyValidator implements StringValidator {
        isAcceptable(s: string): boolean {
            return lettersRegexp.test(s);
        }
    }
}
```

### 文件2: ZipCodeValidator.ts
```typescript
/// <reference path="Validation.ts" />

namespace Validation {
    const numberRegexp = /^[0-9]+$/;
    
    export class ZipCodeValidator implements StringValidator {
        isAcceptable(s: string): boolean {
            return s.length === 5 && numberRegexp.test(s);
        }
    }
}
```

### 文件3: Test.ts
```typescript
/// <reference path="Validation.ts" />
/// <reference path="ZipCodeValidator.ts" />

// 现在可以使用来自两个文件的验证器
let validators: { [s: string]: Validation.StringValidator; } = {};
validators["ZIP code"] = new Validation.ZipCodeValidator();
validators["Letters only"] = new Validation.LettersOnlyValidator();

// 测试
let strings = ["Hello", "98052", "101"];
strings.forEach(s => {
    for (let name in validators) {
        console.log(`"${s}" - ${validators[name].isAcceptable(s) ? "matches" : "does not match"} ${name}`);
    }
});
```

### 编译多文件命名空间

```bash
# 编译所有文件到一个输出文件
tsc --outFile sample.js Validation.ts ZipCodeValidator.ts Test.ts

# 或者分别编译，然后在HTML中按顺序引用
tsc Validation.ts ZipCodeValidator.ts Test.ts
```

## 3. 别名

可以为命名空间或命名空间中的成员创建别名。

### 基本别名

```typescript
namespace Shapes {
    export namespace Polygons {
        export class Triangle {
            constructor(public base: number, public height: number) {}
            
            getArea(): number {
                return 0.5 * this.base * this.height;
            }
        }
        
        export class Square {
            constructor(public side: number) {}
            
            getArea(): number {
                return this.side * this.side;
            }
        }
    }
}

// 创建别名
import polygons = Shapes.Polygons;
import Triangle = Shapes.Polygons.Triangle;

// 使用别名
const triangle = new Triangle(10, 5);
const square = new polygons.Square(4);

console.log(triangle.getArea()); // 25
console.log(square.getArea());   // 16
```

### 函数别名

```typescript
namespace Utilities {
    export function formatDate(date: Date): string {
        return date.toISOString().split('T')[0];
    }
    
    export namespace MathUtils {
        export function add(a: number, b: number): number {
            return a + b;
        }
    }
}

// 为函数创建别名
import format = Utilities.formatDate;
import add = Utilities.MathUtils.add;

console.log(format(new Date())); // 2023-12-07
console.log(add(5, 3)); // 8
```

## 4. 与模块的区别

### 命名空间 vs 模块的主要区别

| 特性 | 命名空间 | 模块 |
|------|----------|------|
| 组织代码方式 | 内部模块 | 外部模块 |
| 依赖管理 | 通过引用标签 | 通过导入/导出 |
| 编译输出 | 全局作用域 | 封装的作用域 |
| 文件结构 | 多个文件可合并 | 每个文件独立 |

### 命名空间示例

```typescript
// namespace-example.ts
namespace MyLibrary {
    export interface Config {
        apiUrl: string;
        timeout: number;
    }
    
    export class ApiClient {
        constructor(private config: Config) {}
        
        fetchData(): Promise<any> {
            // 实现
            return Promise.resolve({});
        }
    }
    
    export function createClient(config: Config): ApiClient {
        return new ApiClient(config);
    }
}

// 使用命名空间
const client = MyLibrary.createClient({
    apiUrl: "https://api.example.com",
    timeout: 5000
});
```

### 模块示例

```typescript
// api-client.ts
export interface Config {
    apiUrl: string;
    timeout: number;
}

export class ApiClient {
    constructor(private config: Config) {}
    
    fetchData(): Promise<any> {
        // 实现
        return Promise.resolve({});
    }
}

export function createClient(config: Config): ApiClient {
    return new ApiClient(config);
}

// main.ts
import { ApiClient, Config, createClient } from './api-client';

const client = createClient({
    apiUrl: "https://api.example.com",
    timeout: 5000
});
```

### 混合使用示例

```typescript
// 有时可以在模块中使用命名空间来组织相关功能
export namespace Validation {
    export namespace Email {
        export function isValid(email: string): boolean {
            return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
        }
        
        export function normalize(email: string): string {
            return email.toLowerCase().trim();
        }
    }
    
    export namespace Phone {
        export function isValid(phone: string): boolean {
            return /^\d{10,11}$/.test(phone.replace(/[-\s]/g, ''));
        }
    }
}

// 使用方式
import { Validation } from './validation';

const email = "USER@EXAMPLE.COM";
if (Validation.Email.isValid(email)) {
    console.log(Validation.Email.normalize(email)); // user@example.com
}
```

### 何时使用命名空间

```typescript
// 1. 当需要扩展全局作用域时
declare global {
    namespace Express {
        interface Request {
            userId?: string;
        }
    }
}

// 2. 当需要组织大型应用的内部代码时
namespace GameEngine {
    export namespace Graphics {
        export class Renderer {}
        export class Texture {}
    }
    
    export namespace Audio {
        export class SoundManager {}
        export class MusicPlayer {}
    }
    
    export namespace Physics {
        export class CollisionDetector {}
        export class Rigidbody {}
    }
}

// 3. 当需要向后兼容或与旧代码集成时
namespace Legacy {
    export function oldFunction(): void {
        // 旧的实现
    }
}
```

## 最佳实践

### 1. 命名规范
```typescript
// 好的做法：清晰的命名
namespace MyCompany {
    export namespace Utilities {
        export namespace StringHelpers {
            export function capitalize(str: string): string {
                return str.charAt(0).toUpperCase() + str.slice(1);
            }
        }
    }
}

// 避免：过长或不清晰的命名
namespace MC_U {
    export namespace SH {
        export function cap(s: string): string { /* ... */ }
    }
}
```

### 2. 合理的组织结构
```typescript
// 按功能组织
namespace MyApp {
    export namespace Models {
        export interface User { /* ... */ }
        export interface Product { /* ... */ }
    }
    
    export namespace Services {
        export class UserService { /* ... */ }
        export class ProductService { /* ... */ }
    }
    
    export namespace Components {
        export class UserComponent { /* ... */ }
        export class ProductComponent { /* ... */ }
    }
    
    export namespace Utils {
        export function formatDate(date: Date): string { /* ... */ }
        export function formatCurrency(amount: number): string { /* ... */ }
    }
}
```

### 3. 避免过度嵌套
```typescript
// 避免：过深的嵌套
namespace A {
    namespace B {
        namespace C {
            namespace D {
                export function doSomething(): void { /* ... */ }
            }
        }
    }
}

// 更好的方式：适度的嵌套
namespace MyApp {
    export namespace API {
        export function fetchData(): Promise<any> { /* ... */ }
    }
    
    export namespace UI {
        export function render(): void { /* ... */ }
    }
}
```


# 19. 三斜线指令 (Triple-Slash Directives)

三斜线指令是 TypeScript 中的特殊注释语法，用于向编译器提供指令。这些指令必须放在文件的顶部，在任何声明之前。

## 1. /// <reference path="..." />

这是最常见的三斜线指令，用于告诉编译器包含另一个文件。

### 基本用法

```typescript
// file1.ts
namespace MyNamespace {
    export interface User {
        name: string;
        age: number;
    }
    
    export function greet(user: User): string {
        return `Hello, ${user.name}!`;
    }
}

// file2.ts
/// <reference path="./file1.ts" />

// 现在可以使用 file1.ts 中的定义
const user: MyNamespace.User = {
    name: "Alice",
    age: 30
};

console.log(MyNamespace.greet(user));
```

### 编译示例

```bash
# 编译包含引用的文件
tsc file2.ts

# 或者编译到单个文件
tsc --outFile bundle.js file2.ts
```

### 实际应用示例

```typescript
// validation.ts
namespace Validation {
    export interface StringValidator {
        isAcceptable(s: string): boolean;
    }
}

// lettersOnlyValidator.ts
/// <reference path="./validation.ts" />

namespace Validation {
    const lettersRegexp = /^[A-Za-z]+$/;
    
    export class LettersOnlyValidator implements StringValidator {
        isAcceptable(s: string): boolean {
            return lettersRegexp.test(s);
        }
    }
}

// zipCodeValidator.ts
/// <reference path="./validation.ts" />

namespace Validation {
    const numberRegexp = /^[0-9]+$/;
    
    export class ZipCodeValidator implements StringValidator {
        isAcceptable(s: string): boolean {
            return s.length === 5 && numberRegexp.test(s);
        }
    }
}

// test.ts
/// <reference path="./validation.ts" />
/// <reference path="./lettersOnlyValidator.ts" />
/// <reference path="./zipCodeValidator.ts" />

let validators: { [s: string]: Validation.StringValidator; } = {};
validators["ZIP code"] = new Validation.ZipCodeValidator();
validators["Letters only"] = new Validation.LettersOnlyValidator();
```

### 路径解析规则

```typescript
// 相对路径
/// <reference path="./utils.ts" />
/// <reference path="../shared/types.ts" />
/// <reference path="./components/button.ts" />

// 绝对路径（相对于项目根目录）
/// <reference path="/src/core/interfaces.ts" />
```

## 2. /// <reference types="..." />

用于声明对特定类型定义包的依赖，通常用于声明全局类型。

### 基本用法

```typescript
// main.ts
/// <reference types="node" />
/// <reference types="jquery" />
/// <reference types="lodash" />

// 现在可以使用这些库的全局类型
import * as fs from 'fs'; // Node.js 类型可用
const $ = require('jquery'); // jQuery 类型可用

// 使用 Node.js 的全局变量
console.log(__dirname);
process.exit(0);
```

### 在声明文件中使用

```typescript
// mylib.d.ts
/// <reference types="react" />

declare namespace MyLib {
    interface ComponentProps {
        children: React.ReactNode;
    }
    
    class MyComponent extends React.Component<ComponentProps> {
        render(): JSX.Element;
    }
}
```

### 配合 DefinitelyTyped

```typescript
// custom.d.ts
/// <reference types="@types/express" />
/// <reference types="@types/mongoose" />

declare global {
    namespace Express {
        interface Request {
            userId?: string;
        }
    }
}

// server.ts
/// <reference path="./custom.d.ts" />

import express from 'express';
const app = express();

app.use((req, res, next) => {
    req.userId = "123"; // 类型安全
    next();
});
```

## 3. /// <reference lib="..." />

用于显式包含内置的 TypeScript 库定义文件。

### 常用库引用

```typescript
// ES2015 特性
/// <reference lib="es2015" />

// DOM API
/// <reference lib="dom" />

// Web Workers
/// <reference lib="webworker" />

// ESNext
/// <reference lib="esnext" />
```

### 实际应用示例

```typescript
// webworker.ts
/// <reference lib="webworker" />

// 现在可以使用 Web Worker 的全局变量和类型
self.addEventListener('message', (event: MessageEvent) => {
    const data = event.data;
    // 处理数据
    self.postMessage({ result: 'processed' });
});

// service-worker.ts
/// <reference lib="webworker" />
/// <reference lib="scripthost" />

self.addEventListener('fetch', (event: FetchEvent) => {
    event.respondWith(
        caches.match(event.request)
            .then(response => response || fetch(event.request))
    );
});
```

### 组合使用多个库

```typescript
// modern-browser.ts
/// <reference lib="es2020" />
/// <reference lib="dom" />
/// <reference lib="dom.iterable" />

// 现在可以使用现代 JavaScript 和 DOM API
const array = [1, 2, 3, 4, 5];
const iterator = array[Symbol.iterator]();

// 使用 DOM API
const element = document.querySelector('.my-class');
if (element) {
    element.classList.add('active');
}
```

### TypeScript 内置库列表

```typescript
// ES 标准库
/// <reference lib="es5" />
/// <reference lib="es2015" />
/// <reference lib="es2016" />
/// <reference lib="es2017" />
/// <reference lib="es2018" />
/// <reference lib="es2019" />
/// <reference lib="es2020" />
/// <reference lib="es2021" />
/// <reference lib="es2022" />
/// <reference lib="esnext" />

// DOM 相关
/// <reference lib="dom" />
/// <reference lib="dom.iterable" />
/// <reference lib="dom.asynciterable" />

// Web APIs
/// <reference lib="webworker" />
/// <reference lib="webworker.importscripts" />
/// <reference lib="webworker.iterable" />
/// <reference lib="scripthost" />
/// <reference lib="es2020.sharedmemory" />
```

## 4. /// <reference no-default-lib="true"/>

这是一个特殊的指令，用于告诉编译器不要包含默认的库文件。

### 基本用法

```typescript
// custom-lib.ts
/// <reference no-default-lib="true"/>
/// <reference lib="es5" />

// 只包含 ES5 库，不包含其他默认库
// 这样可以创建自定义的最小环境

interface Array<T> {
    forEach(callbackfn: (value: T, index: number, array: T[]) => void): void;
    // 只定义需要的方法
}
```

### 创建自定义运行环境

```typescript
// minimal-runtime.d.ts
/// <reference no-default-lib="true"/>
/// <reference lib="es2020" />

// 为特定运行环境定义全局变量
declare const __VERSION__: string;
declare const __ENV__: 'development' | 'production';

// 自定义全局函数
declare function log(message: string): void;
declare function assert(condition: boolean, message?: string): asserts condition;
```

### 与编译器选项配合

```json
// tsconfig.json
{
  "compilerOptions": {
    "lib": ["es2020", "dom"],
    "noLib": false
  }
}
```

```typescript
// 在这种配置下使用 no-default-lib
/// <reference no-default-lib="true"/>
/// <reference lib="es5" />
/// <reference lib="es2015.promise" />

// 只有明确引用的库才可用
Promise.resolve("hello").then(console.log);
// Array, Object 等基本类型可能不可用，除非明确引用
```

## 综合应用示例

### 大型项目结构

```typescript
// globals.d.ts
/// <reference no-default-lib="true"/>
/// <reference lib="es2020" />
/// <reference lib="dom" />

// 项目全局类型定义
declare global {
    interface Window {
        MyApp: {
            version: string;
            config: any;
        };
    }
}

// core.ts
/// <reference path="./globals.d.ts" />

namespace MyApp {
    export interface Config {
        apiUrl: string;
        debug: boolean;
    }
    
    export class Core {
        constructor(private config: Config) {}
        
        init(): void {
            window.MyApp = {
                version: "1.0.0",
                config: this.config
            };
        }
    }
}

// utils.ts
/// <reference path="./core.ts" />

namespace MyApp {
    export namespace Utils {
        export function formatDate(date: Date): string {
            return date.toISOString();
        }
        
        export function debounce<T extends (...args: any[]) => any>(
            func: T, 
            wait: number
        ): (...args: Parameters<T>) => void {
            let timeout: number;
            return function executedFunction(...args: Parameters<T>) {
                const later = () => {
                    clearTimeout(timeout);
                    func(...args);
                };
                clearTimeout(timeout);
                timeout = setTimeout(later, wait);
            };
        }
    }
}
```

### 库开发示例

```typescript
// mylib.d.ts
/// <reference no-default-lib="true"/>
/// <reference lib="es2018" />
/// <reference types="node" />

declare namespace MyLib {
    interface Options {
        timeout?: number;
        retries?: number;
    }
    
    class Client {
        constructor(options?: Options);
        request(url: string): Promise<any>;
    }
    
    function createClient(options?: Options): Client;
}

// mylib-implementation.ts
/// <reference path="./mylib.d.ts" />

namespace MyLib {
    export class Client {
        private options: Required<Options>;
        
        constructor(options: Options = {}) {
            this.options = {
                timeout: options.timeout || 5000,
                retries: options.retries || 3
            };
        }
        
        async request(url: string): Promise<any> {
            // 实现
            return fetch(url, { 
                signal: AbortSignal.timeout(this.options.timeout) 
            });
        }
    }
    
    export function createClient(options?: Options): Client {
        return new Client(options);
    }
}
```

## 编译器行为

### 顺序处理

```typescript
// file1.ts
/// <reference path="./file2.ts" />
/// <reference path="./file3.ts" />

// 引用的文件会按顺序处理
// file2.ts 中的内容先被处理
// 然后是 file3.ts
// 最后是 file1.ts
```

### 循环引用检测

```typescript
// a.ts
/// <reference path="./b.ts" />

// b.ts  
/// <reference path="./a.ts" /> // 编译器会检测到循环引用并警告
```

## 最佳实践

### 1. 合理使用场景

```typescript
// ✅ 适合使用的情况：声明文件、库定义
// mylib.d.ts
/// <reference lib="es2020" />
/// <reference types="node" />

// ❌ 不推荐：现代项目中过度使用 path 引用
// main.ts
/// <reference path="./utils.ts" /> // 更推荐使用 ES 模块导入
```

### 2. 清晰的依赖管理

```typescript
// 推荐：明确声明依赖
/// <reference types="node" />
/// <reference lib="es2020" />

// 而不是依赖 tsconfig.json 的全局配置
```

### 3. 避免冲突

```typescript
// 当使用 no-default-lib 时要小心
/// <reference no-default-lib="true"/>
/// <reference lib="es5" /> // 确保包含必要的库
```


# 20. 与主流框架集成
- React + TypeScript
- Vue + TypeScript
- Angular + TypeScript
- Node.js + TypeScript
- Express + TypeScript
- NestJS + TypeScript

# 21. 性能优化

TypeScript 性能优化是一个重要的主题，特别是在大型项目中。合理的优化可以显著提升开发体验和构建速度。

## 1. 编译性能优化

### tsconfig.json 配置优化

```json
{
  "compilerOptions": {
    // 启用增量编译
    "incremental": true,
    "tsBuildInfoFile": "./dist/.tsbuildinfo",
    
    // 跳过类型检查的库文件
    "skipLibCheck": true,
    
    // 跳过声明文件的检查
    "skipDefaultLibCheck": true,
    
    // 不生成声明文件（如果不需要的话）
    "declaration": false,
    "declarationMap": false,
    
    // 不生成 source map（生产环境）
    "sourceMap": false,
    "inlineSourceMap": false,
    
    // 不检查 js 文件（如果不需要的话）
    "checkJs": false,
    
    // 使用更快的模块解析
    "moduleResolution": "node",
    
    // 限制包含的文件
    "include": [
      "src/**/*"
    ],
    "exclude": [
      "node_modules",
      "dist",
      "**/*.spec.ts"
    ]
  }
}
```

### 优化编译选项

```json
{
  "compilerOptions": {
    // 针对特定目标优化
    "target": "ES2020", // 避免过多的 polyfill
    
    // 合理的模块设置
    "module": "ES2020",
    
    // 不需要的装饰器支持
    "experimentalDecorators": false,
    "emitDecoratorMetadata": false,
    
    // 不生成辅助函数
    "importHelpers": true,
    "noEmitHelpers": false,
    
    // 严格模式（虽然严格，但有助于性能）
    "strict": true,
    
    // 移除注释
    "removeComments": true
  }
}
```

### 文件结构优化

```typescript
// ❌ 避免：巨大的单一文件
// utils.ts - 包含所有工具函数
export function formatDate(date: Date): string { /* ... */ }
export function validateEmail(email: string): boolean { /* ... */ }
export function calculateTax(amount: number): number { /* ... */ }
// ... 100+ 个函数

// ✅ 推荐：模块化组织
// utils/date.ts
export function formatDate(date: Date): string { /* ... */ }

// utils/validation.ts
export function validateEmail(email: string): boolean { /* ... */ }

// utils/finance.ts
export function calculateTax(amount: number): number { /* ... */ }
```

## 2. 类型检查性能

### 避免复杂的类型推断

```typescript
// ❌ 避免：复杂的泛型推断
function processComplex<T extends Record<string, any>>(
  data: T,
  processor: <K extends keyof T>(value: T[K], key: K) => any
): any {
  // 复杂的类型推断会影响性能
}

// ✅ 推荐：明确类型或简化泛型
interface Processable {
  [key: string]: any;
}

function processSimple(
  data: Processable,
  processor: (value: any, key: string) => any
): any {
  // 更快的类型检查
}
```

### 优化联合类型

```typescript
// ❌ 避免：过长的联合类型
type Status = 
  | 'pending' | 'processing' | 'completed' | 'failed' 
  | 'cancelled' | 'refunded' | 'disputed' | 'resolved'
  | 'archived' | 'deleted' | 'suspended' | 'active'
  | 'inactive' | 'locked' | 'unlocked' | 'verified';

// ✅ 推荐：使用枚举或常量
const Statuses = {
  PENDING: 'pending',
  PROCESSING: 'processing',
  COMPLETED: 'completed',
  FAILED: 'failed',
  // ... 其他状态
} as const;

type Status = typeof Statuses[keyof typeof Statuses];
```

### 避免深层嵌套对象类型

```typescript
// ❌ 避免：深层嵌套
interface DeepNested {
  level1: {
    level2: {
      level3: {
        level4: {
          level5: {
            value: string;
          };
        };
      };
    };
  };
}

// ✅ 推荐：扁平化结构
interface Level1 {
  level2: Level2;
}

interface Level2 {
  level3: Level3;
}

interface Level3 {
  level4: Level4;
}

interface Level4 {
  level5: Level5;
}

interface Level5 {
  value: string;
}
```

### 使用类型断言优化

```typescript
// ❌ 避免：频繁的类型守卫
function processResponse(response: unknown): string {
  if (response && typeof response === 'object') {
    if ('data' in response && response.data) {
      if (typeof response.data === 'object') {
        if ('message' in response.data && typeof response.data.message === 'string') {
          return response.data.message;
        }
      }
    }
  }
  return '';
}

// ✅ 推荐：合理使用类型断言
interface ApiResponse {
  data: {
    message: string;
  };
}

function processResponse(response: unknown): string {
  const apiResponse = response as ApiResponse;
  return apiResponse?.data?.message || '';
}
```

## 3. 增量编译

### 基本增量编译配置

```json
{
  "compilerOptions": {
    "incremental": true,
    "tsBuildInfoFile": "./dist/tsconfig.tsbuildinfo"
  }
}
```

### 增量编译工作原理

```bash
# 第一次编译（较慢）
tsc --incremental

# 第二次编译（快速，只编译更改的文件）
tsc --incremental

# 查看生成的构建信息文件
cat dist/tsconfig.tsbuildinfo
```

### 增量编译最佳实践

```typescript
// src/components/Button.tsx
export interface ButtonProps {
  text: string;
  onClick: () => void;
}

export function Button({ text, onClick }: ButtonProps) {
  return <button onClick={onClick}>{text}</button>;
}

// src/components/Input.tsx
export interface InputProps {
  value: string;
  onChange: (value: string) => void;
}

export function Input({ value, onChange }: InputProps) {
  return (
    <input 
      value={value} 
      onChange={(e) => onChange(e.target.value)} 
    />
  );
}

// 只修改 Button.tsx 时，Input.tsx 不会被重新编译
```

### 监视模式下的增量编译

```bash
# 启用监视模式和增量编译
tsc --watch --incremental

# 或者使用配置文件
tsc --build --watch
```

## 4. 项目引用优化

### 项目引用基本配置

```json
// tsconfig.base.json
{
  "compilerOptions": {
    "composite": true,
    "declaration": true,
    "declarationMap": true,
    "sourceMap": true
  }
}
```

```json
// packages/shared/tsconfig.json
{
  "extends": "../../tsconfig.base.json",
  "compilerOptions": {
    "outDir": "../../dist/shared",
    "rootDir": "."
  },
  "include": ["src/**/*"]
}
```

```json
// packages/core/tsconfig.json
{
  "extends": "../../tsconfig.base.json",
  "compilerOptions": {
    "outDir": "../../dist/core",
    "rootDir": "."
  },
  "references": [
    { "path": "../shared" }
  ],
  "include": ["src/**/*"]
}
```

```json
// packages/app/tsconfig.json
{
  "extends": "../../tsconfig.base.json",
  "compilerOptions": {
    "outDir": "../../dist/app",
    "rootDir": "."
  },
  "references": [
    { "path": "../core" },
    { "path": "../shared" }
  ],
  "include": ["src/**/*"]
}
```

### 项目引用的优势

```bash
# 构建整个项目（智能增量构建）
tsc --build

# 清理构建
tsc --build --clean

# 强制重新构建
tsc --build --force

# 监视模式
tsc --build --watch
```

### 项目引用的实际示例

```typescript
// packages/shared/src/types.ts
export interface User {
  id: string;
  name: string;
  email: string;
}

export interface ApiResponse<T> {
  data: T;
  status: number;
  message?: string;
}

// packages/shared/src/utils.ts
export function isValidEmail(email: string): boolean {
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
}

// packages/core/src/api.ts
import { User, ApiResponse } from '@myproject/shared';
import { isValidEmail } from '@myproject/shared/utils';

export class UserApi {
  async getUser(id: string): Promise<ApiResponse<User>> {
    // 实现
    return {
      data: { id, name: '', email: '' },
      status: 200
    };
  }
}

// packages/app/src/main.ts
import { UserApi } from '@myproject/core';

const api = new UserApi();
api.getUser('123').then(response => {
  console.log(response.data);
});
```

### 项目引用的构建脚本

```json
{
  "scripts": {
    "build": "tsc --build",
    "build:clean": "tsc --build --clean",
    "build:watch": "tsc --build --watch",
    "build:force": "tsc --build --force"
  }
}
```

## 5. 构建工具集成

### Webpack 集成优化

```javascript
// webpack.config.js
const path = require('path');

module.exports = {
  entry: './src/index.ts',
  module: {
    rules: [
      {
        test: /\.tsx?$/,
        use: [
          {
            loader: 'ts-loader',
            options: {
              // 启用转译模式（跳过类型检查）
              transpileOnly: true,
              // 使用缓存提高性能
              compilerOptions: {
                module: 'es2015'
              }
            }
          }
        ],
        exclude: /node_modules/
      }
    ]
  },
  resolve: {
    extensions: ['.tsx', '.ts', '.js']
  },
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  },
  // 启用缓存
  cache: {
    type: 'filesystem'
  }
};
```

### 使用 ForkTsCheckerWebpackPlugin

```javascript
// webpack.config.js
const ForkTsCheckerWebpackPlugin = require('fork-ts-checker-webpack-plugin');

module.exports = {
  // ... 其他配置
  plugins: [
    new ForkTsCheckerWebpackPlugin({
      typescript: {
        configFile: path.resolve(__dirname, 'tsconfig.json'),
        memoryLimit: 4096,
        mode: 'write-references'
      },
      issue: {
        include: [
          { file: '**/src/**/*.{ts,tsx}' }
        ]
      }
    })
  ]
};
```

### Rollup 集成

```javascript
// rollup.config.js
import typescript from '@rollup/plugin-typescript';
import { terser } from 'rollup-plugin-terser';

export default {
  input: 'src/index.ts',
  output: {
    dir: 'dist',
    format: 'es'
  },
  plugins: [
    typescript({
      // 优化配置
      tsconfig: './tsconfig.build.json',
      declaration: true,
      declarationDir: 'dist/types',
      // 跳过类型检查以提高构建速度
      transpileOnly: true
    }),
    terser({
      compress: {
        drop_console: true,
        drop_debugger: true
      }
    })
  ]
};
```

### Vite 集成

```typescript
// vite.config.ts
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';

export default defineConfig({
  plugins: [react()],
  build: {
    // 启用 CSS 代码分割
    cssCodeSplit: true,
    // 启用 rollup 选项
    rollupOptions: {
      output: {
        manualChunks: {
          vendor: ['react', 'react-dom'],
          utils: ['lodash', 'moment']
        }
      }
    },
    // 启用 brotli 压缩
    brotliSize: true
  },
  // 开发服务器优化
  server: {
    // 预转换依赖
    preTransformRequests: true
  }
});
```

### 并行构建优化

```json
{
  "scripts": {
    "build": "concurrently \"npm run build:types\" \"npm run build:js\"",
    "build:types": "tsc --emitDeclarationOnly",
    "build:js": "babel src --out-dir dist --extensions .ts,.tsx"
  },
  "devDependencies": {
    "concurrently": "^7.0.0",
    "babel-cli": "^6.26.0",
    "@babel/preset-typescript": "^7.0.0"
  }
}
```

### 缓存优化

```json
// tsconfig.build.json
{
  "extends": "./tsconfig.json",
  "compilerOptions": {
    "incremental": true,
    "tsBuildInfoFile": "./dist/.tsbuildinfo",
    "composite": true
  },
  "exclude": [
    "node_modules",
    "**/*.test.ts",
    "**/*.spec.ts"
  ]
}
```

### 监视模式优化

```bash
# 使用更快的监视模式
tsc --watch --incremental

# 或者使用 nodemon
nodemon --exec "tsc && node dist/index.js" --watch src --ext ts

# 或者使用 concurrently 同时运行多个监视进程
concurrently "tsc --watch" "nodemon dist/index.js"
```

## 性能监控和分析

### 使用 TypeScript 性能标志

```bash
# 启用详细的性能报告
tsc --extendedDiagnostics

# 生成性能追踪文件
tsc --generateTrace ./trace

# 分析追踪文件
# 在 Chrome 中打开 chrome://tracing，然后加载生成的 trace 文件
```

### 构建时间分析

```javascript
// build-time-analyzer.js
const { performance } = require('perf_hooks');

const start = performance.now();

// 执行构建命令
require('child_process').execSync('tsc', { stdio: 'inherit' });

const end = performance.now();
console.log(`Build completed in ${end - start} milliseconds`);
```

### 内存使用优化

```json
{
  "scripts": {
    "build": "node --max-old-space-size=4096 ./node_modules/.bin/tsc"
  }
}
```

## 最佳实践总结

### 1. 配置优化清单

```json
{
  "compilerOptions": {
    // 必须的优化选项
    "incremental": true,
    "composite": true,
    "skipLibCheck": true,
    
    // 可选的优化选项
    "declaration": false,
    "sourceMap": false,
    "removeComments": true,
    
    // 项目结构优化
    "include": ["src/**/*"],
    "exclude": ["node_modules", "dist", "**/*.test.ts"]
  }
}
```

### 2. 开发环境 vs 生产环境

```json
// tsconfig.dev.json
{
  "extends": "./tsconfig.json",
  "compilerOptions": {
    "sourceMap": true,
    "declaration": true,
    "incremental": true
  }
}

// tsconfig.prod.json
{
  "extends": "./tsconfig.json",
  "compilerOptions": {
    "sourceMap": false,
    "declaration": false,
    "removeComments": true
  }
}
```

### 3. 持续优化

```bash
# 定期检查性能
npm run build -- --extendedDiagnostics

# 分析构建时间
time npm run build

# 监控内存使用
node --inspect-brk ./node_modules/.bin/tsc
```


# 22. 调试技巧

调试是开发过程中不可或缺的技能，TypeScript 提供了丰富的调试工具和技巧来帮助开发者快速定位和解决问题。

## 1. Source Maps 配置

Source Maps 是调试 TypeScript 代码的关键，它将编译后的 JavaScript 代码映射回原始的 TypeScript 源代码。

### 基本 Source Maps 配置

```json
// tsconfig.json
{
  "compilerOptions": {
    // 启用 source map 生成
    "sourceMap": true,
    
    // 或者使用内联 source map
    "inlineSourceMap": false,
    
    // 包含源代码在 source map 中
    "inlineSources": true,
    
    // 指定 source map 文件的位置
    "mapRoot": "./sourcemaps",
    
    // 指定源文件根目录
    "sourceRoot": "./src"
  }
}
```

### 详细的 Source Maps 配置

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "outDir": "./dist",
    "rootDir": "./src",
    
    // 基本 source map 配置
    "sourceMap": true,
    "inlineSources": true,
    
    // 调试优化配置
    "removeComments": false, // 保留注释有助于调试
    "declaration": true,     // 生成声明文件
    
    // 严格模式有助于调试时发现问题
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true
  },
  "include": [
    "src/**/*"
  ]
}
```

### Webpack 中的 Source Maps 配置

```javascript
// webpack.config.js
const path = require('path');

module.exports = {
  mode: 'development',
  entry: './src/index.ts',
  devtool: 'source-map', // 或 'inline-source-map', 'eval-source-map'
  
  module: {
    rules: [
      {
        test: /\.tsx?$/,
        use: 'ts-loader',
        exclude: /node_modules/
      }
    ]
  },
  
  resolve: {
    extensions: ['.tsx', '.ts', '.js']
  },
  
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  },
  
  // 开发服务器配置
  devServer: {
    contentBase: './dist',
    hot: true
  }
};
```

### 不同环境的 Source Maps 策略

```javascript
// webpack.config.js
const isDevelopment = process.env.NODE_ENV === 'development';

module.exports = {
  // ... 其他配置
  
  devtool: isDevelopment ? 'eval-source-map' : 'source-map',
  
  optimization: {
    minimize: !isDevelopment
  }
};
```

### 自定义 Source Maps 路径

```json
{
  "compilerOptions": {
    "sourceMap": true,
    "inlineSources": true,
    "mapRoot": "https://myapp.com/sourcemaps/",
    "sourceRoot": "src/"
  }
}
```

## 2. 调试器配置

### VS Code 调试配置

```json
// .vscode/launch.json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Debug TypeScript",
      "type": "node",
      "request": "launch",
      "program": "${workspaceFolder}/src/index.ts",
      "preLaunchTask": "tsc: build - tsconfig.json",
      "outFiles": ["${workspaceFolder}/dist/**/*.js"],
      "sourceMaps": true,
      "smartStep": true,
      "internalConsoleOptions": "openOnSessionStart"
    },
    {
      "name": "Debug with ts-node",
      "type": "node",
      "request": "launch",
      "runtimeArgs": ["-r", "ts-node/register"],
      "args": ["${workspaceFolder}/src/index.ts"],
      "cwd": "${workspaceFolder}",
      "protocol": "inspector",
      "console": "integratedTerminal",
      "internalConsoleOptions": "neverOpen"
    },
    {
      "name": "Attach to Process",
      "type": "node",
      "request": "attach",
      "port": 9229,
      "restart": true,
      "sourceMaps": true,
      "outFiles": ["${workspaceFolder}/dist/**/*.js"]
    }
  ]
}
```

### Chrome DevTools 调试配置

```typescript
// src/debug-example.ts
class Calculator {
  private history: string[] = [];
  
  add(a: number, b: number): number {
    const result = a + b;
    this.history.push(`${a} + ${b} = ${result}`);
    return result;
  }
  
  multiply(a: number, b: number): number {
    const result = a * b;
    this.history.push(`${a} * ${b} = ${result}`);
    return result;
  }
  
  getHistory(): string[] {
    return this.history;
  }
}

// 添加断点标记
function main() {
  const calc = new Calculator();
  
  // 在这里设置断点
  const sum = calc.add(5, 3);
  const product = calc.multiply(sum, 2);
  
  console.log('Results:', { sum, product });
  console.log('History:', calc.getHistory());
}

main();
```

### Node.js 调试配置

```bash
# 使用 ts-node 直接调试
ts-node --inspect-brk src/index.ts

# 或者使用 nodemon 监视模式调试
nodemon --exec "node --inspect-brk -r ts-node/register" src/index.ts

# 使用 tsc 编译后调试
tsc && node --inspect-brk dist/index.js
```

### 浏览器调试配置

```html
<!-- index.html -->
<!DOCTYPE html>
<html>
<head>
    <title>TypeScript Debug Demo</title>
</head>
<body>
    <script src="dist/bundle.js"></script>
</body>
</html>
```

```typescript
// src/browser-debug.ts
interface User {
  id: number;
  name: string;
  email: string;
}

class UserService {
  private users: User[] = [];
  
  addUser(user: User): void {
    debugger; // 浏览器中会在此处暂停
    this.users.push(user);
  }
  
  findUser(id: number): User | undefined {
    return this.users.find(user => user.id === id);
  }
  
  getAllUsers(): User[] {
    return [...this.users]; // 返回副本
  }
}

// 使用示例
const userService = new UserService();

userService.addUser({
  id: 1,
  name: "Alice",
  email: "alice@example.com"
});

console.log(userService.getAllUsers());
```

## 3. 类型错误诊断

### 详细错误信息配置

```json
{
  "compilerOptions": {
    // 启用详细的错误报告
    "noErrorTruncation": true,
    
    // 显示诊断信息
    "diagnostics": true,
    "extendedDiagnostics": true,
    
    // 严格类型检查
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "strictFunctionTypes": true,
    "strictBindCallApply": true,
    "strictPropertyInitialization": true,
    "noImplicitThis": true,
    "alwaysStrict": true
  }
}
```

### 常见类型错误示例

```typescript
// 1. 类型不匹配错误
function calculateTotal(items: number[]): number {
  return items.reduce((sum, item) => sum + item, 0);
}

// 错误：传递了错误的类型
// calculateTotal(["1", "2", "3"]); // Error: Type 'string' is not assignable to type 'number'

// 2. 可能为 undefined 的错误
interface User {
  name: string;
  email?: string; // 可选属性
}

function sendEmail(user: User): void {
  // 错误：email 可能为 undefined
  // console.log(user.email.toUpperCase()); // Error: Object is possibly 'undefined'
  
  // 正确的方式
  if (user.email) {
    console.log(user.email.toUpperCase());
  }
}

// 3. 函数参数类型错误
function processData(data: { id: number; name: string }): void {
  console.log(`Processing ${data.name} (${data.id})`);
}

// 错误：缺少必需属性
// processData({ name: "Test" }); // Error: Property 'id' is missing

// 4. 泛型类型错误
function identity<T>(arg: T): T {
  return arg;
}

// 错误：类型参数推断失败
// const result: number = identity("hello"); // Error: Type 'string' is not assignable to type 'number'
```

### 类型错误诊断工具

```typescript
// 使用类型守卫进行诊断
function isString(value: unknown): value is string {
  return typeof value === 'string';
}

function processValue(value: unknown): void {
  if (isString(value)) {
    // TypeScript 知道这里 value 是 string 类型
    console.log(value.toUpperCase());
  } else {
    // TypeScript 知道这里 value 不是 string 类型
    console.log('Not a string');
  }
}

// 使用条件类型进行诊断
type NonNullable<T> = T extends null | undefined ? never : T;

function removeNullable<T>(value: T): NonNullable<T> {
  if (value === null || value === undefined) {
    throw new Error('Value cannot be null or undefined');
  }
  return value as NonNullable<T>;
}

// 类型断言的正确使用
interface ApiResponse {
  data: any;
  status: number;
}

function handleResponse(response: unknown): ApiResponse {
  // 断言前进行验证
  if (response && typeof response === 'object' && 'data' in response && 'status' in response) {
    return response as ApiResponse;
  }
  throw new Error('Invalid response format');
}
```

### 自定义类型错误消息

```typescript
// 使用 never 类型创建编译时错误
type AssertNever<T> = T extends never ? T : never;

function exhaustiveCheck(value: never): never {
  throw new Error(`Unhandled case: ${value}`);
}

// 使用示例
type Status = 'pending' | 'completed' | 'failed';

function handleStatus(status: Status): string {
  switch (status) {
    case 'pending':
      return 'Processing...';
    case 'completed':
      return 'Done!';
    case 'failed':
      return 'Error occurred';
    default:
      // 如果添加新的状态但忘记处理，这里会报错
      return exhaustiveCheck(status);
  }
}
```

## 4. 编译错误处理

### 编译错误配置

```json
{
  "compilerOptions": {
    // 错误处理选项
    "noEmitOnError": true, // 有错误时不生成输出
    "noEmit": false,       // 仍然生成输出（即使有错误）
    
    // 严格模式
    "strict": true,
    
    // 特定的错误检查
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    
    // 实验性功能
    "strictPropertyInitialization": true
  },
  "watchOptions": {
    "watchFile": "useFsEvents",
    "watchDirectory": "useFsEvents",
    "fallbackPolling": "dynamicPriority",
    "synchronousWatchDirectory": true,
    "excludeDirectories": ["**/node_modules", "_build"]
  }
}
```

### 编译错误处理脚本

```json
{
  "scripts": {
    "build": "tsc",
    "build:watch": "tsc --watch",
    "build:strict": "tsc --noEmitOnError",
    "build:ci": "tsc --noEmit --noErrorTruncation",
    "lint": "tsc --noEmit --pretty false"
  }
}
```

### 编译错误监控

```bash
# 基本编译
tsc

# 监视模式编译
tsc --watch

# 详细诊断信息
tsc --extendedDiagnostics

# 生成性能追踪
tsc --generateTrace ./trace

# 只检查不编译
tsc --noEmit
```

### 编译错误处理示例

```typescript
// src/error-handling.ts
// 模拟编译错误的场景

// 1. 语法错误
// function missingBracket() { // Error: '{' expected
//   console.log("Missing bracket"

// 2. 类型错误
interface User {
  id: number;
  name: string;
}

// const user: User = { // Error: Property 'id' is missing
//   name: "Alice"
// };

// 3. 导入错误
// import { nonExistent } from './non-existent-file'; // Error: Cannot find module

// 4. 变量未声明
// console.log(undeclaredVariable); // Error: Cannot find name

// 正确的代码示例
class ErrorHandler {
  static handleAsync<T>(promise: Promise<T>): Promise<[T | null, Error | null]> {
    return promise
      .then(data => [data, null] as [T, null])
      .catch(error => [null, error] as [null, Error]);
  }
  
  static validateInput(input: unknown): input is string {
    return typeof input === 'string' && input.length > 0;
  }
}

// 使用示例
async function example() {
  const [result, error] = await ErrorHandler.handleAsync(
    fetch('/api/data').then(res => res.json())
  );
  
  if (error) {
    console.error('API Error:', error);
    return;
  }
  
  console.log('Data:', result);
}

example();
```

### 构建管道中的错误处理

```javascript
// build.js
const { execSync } = require('child_process');
const fs = require('fs');

function runBuild() {
  try {
    console.log('Running TypeScript compilation...');
    
    // 执行编译
    const output = execSync('tsc --noEmitOnError', { 
      stdio: 'pipe',
      encoding: 'utf-8'
    });
    
    console.log('Compilation successful!');
    return true;
    
  } catch (error) {
    console.error('Compilation failed:');
    console.error(error.stdout);
    console.error(error.stderr);
    return false;
  }
}

// 条件编译
function conditionalBuild() {
  const isProduction = process.env.NODE_ENV === 'production';
  
  try {
    if (isProduction) {
      execSync('tsc --noEmitOnError --strict', { stdio: 'inherit' });
    } else {
      execSync('tsc --watch', { stdio: 'inherit' });
    }
  } catch (error) {
    console.error('Build failed:', error.message);
    process.exit(1);
  }
}

// 运行构建
if (require.main === module) {
  conditionalBuild();
}
```

### 错误报告和日志

```typescript
// src/error-reporting.ts
interface ErrorReport {
  timestamp: Date;
  fileName: string;
  lineNumber: number;
  errorMessage: string;
  stackTrace?: string;
}

class ErrorReporter {
  static report(error: Error, fileName: string, lineNumber: number): void {
    const report: ErrorReport = {
      timestamp: new Date(),
      fileName,
      lineNumber,
      errorMessage: error.message,
      stackTrace: error.stack
    };
    
    console.error('Error Report:', JSON.stringify(report, null, 2));
    
    // 可以发送到错误监控服务
    // this.sendToMonitoringService(report);
  }
  
  static createCustomError(message: string, code: string): Error {
    const error = new Error(message);
    (error as any).code = code;
    return error;
  }
}

// 使用示例
try {
  throw ErrorReporter.createCustomError('Something went wrong', 'CUSTOM_001');
} catch (error) {
  ErrorReporter.report(error, 'example.ts', 42);
}
```

## 调试最佳实践

### 1. 调试配置模板

```json
// tsconfig.debug.json
{
  "extends": "./tsconfig.json",
  "compilerOptions": {
    "sourceMap": true,
    "inlineSources": true,
    "removeComments": false,
    "noEmitOnError": false,
    "diagnostics": true
  }
}
```

### 2. 调试工具链

```bash
# 安装调试工具
npm install --save-dev ts-node nodemon

# package.json 脚本
{
  "scripts": {
    "debug": "node --inspect-brk -r ts-node/register src/index.ts",
    "debug:watch": "nodemon --exec 'node --inspect-brk -r ts-node/register' src/index.ts",
    "build:debug": "tsc --project tsconfig.debug.json"
  }
}
```

### 3. 调试技巧

```typescript
// 使用 console.trace() 进行堆栈跟踪
function debugFunction() {
  console.trace('Debug point reached');
  // ... 函数逻辑
}

// 使用条件断点
for (let i = 0; i < 100; i++) {
  if (i === 50) {
    debugger; // 只在 i=50 时暂停
  }
  // ... 循环逻辑
}

// 使用 console.table() 显示对象数组
const users = [
  { id: 1, name: 'Alice', age: 30 },
  { id: 2, name: 'Bob', age: 25 }
];
console.table(users);
```


# 23. 测试策略

测试是保证代码质量和可靠性的关键环节。TypeScript 提供了强大的类型系统，但仍然需要各种类型的测试来确保运行时的正确性。

## 1. 单元测试配置

### Jest 配置

```json
// jest.config.js
module.exports = {
  preset: 'ts-jest',
  testEnvironment: 'node',
  roots: ['<rootDir>/src'],
  testMatch: [
    '**/__tests__/**/*.+(ts|tsx|js)',
    '**/?(*.)+(spec|test).+(ts|tsx|js)'
  ],
  transform: {
    '^.+\\.(ts|tsx)$': 'ts-jest'
  },
  collectCoverageFrom: [
    'src/**/*.{ts,tsx}',
    '!src/**/*.d.ts'
  ],
  coverageDirectory: 'coverage',
  coverageReporters: ['text', 'lcov', 'html']
};
```

```json
// tsconfig.json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "lib": ["ES2020"],
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "declaration": true,
    "sourceMap": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "**/*.test.ts", "**/*.spec.ts"]
}
```

```json
// tsconfig.test.json
{
  "extends": "./tsconfig.json",
  "compilerOptions": {
    "types": ["jest", "node"]
  },
  "include": [
    "src/**/*",
    "**/*.test.ts",
    "**/*.spec.ts"
  ]
}
```

### 基础单元测试示例

```typescript
// src/calculator.ts
export class Calculator {
  add(a: number, b: number): number {
    return a + b;
  }
  
  subtract(a: number, b: number): number {
    return a - b;
  }
  
  multiply(a: number, b: number): number {
    return a * b;
  }
  
  divide(a: number, b: number): number {
    if (b === 0) {
      throw new Error('Division by zero');
    }
    return a / b;
  }
  
  factorial(n: number): number {
    if (n < 0) {
      throw new Error('Factorial of negative number is not defined');
    }
    if (n === 0 || n === 1) {
      return 1;
    }
    return n * this.factorial(n - 1);
  }
}
```

```typescript
// src/calculator.test.ts
import { Calculator } from './calculator';

describe('Calculator', () => {
  let calculator: Calculator;
  
  beforeEach(() => {
    calculator = new Calculator();
  });
  
  describe('add', () => {
    test('should add two positive numbers correctly', () => {
      expect(calculator.add(2, 3)).toBe(5);
    });
    
    test('should add negative numbers correctly', () => {
      expect(calculator.add(-2, -3)).toBe(-5);
    });
    
    test('should handle zero correctly', () => {
      expect(calculator.add(5, 0)).toBe(5);
      expect(calculator.add(0, 0)).toBe(0);
    });
  });
  
  describe('subtract', () => {
    test('should subtract correctly', () => {
      expect(calculator.subtract(5, 3)).toBe(2);
      expect(calculator.subtract(3, 5)).toBe(-2);
    });
  });
  
  describe('multiply', () => {
    test('should multiply correctly', () => {
      expect(calculator.multiply(3, 4)).toBe(12);
      expect(calculator.multiply(-2, 3)).toBe(-6);
      expect(calculator.multiply(0, 5)).toBe(0);
    });
  });
  
  describe('divide', () => {
    test('should divide correctly', () => {
      expect(calculator.divide(10, 2)).toBe(5);
      expect(calculator.divide(7, 2)).toBeCloseTo(3.5);
    });
    
    test('should throw error when dividing by zero', () => {
      expect(() => calculator.divide(5, 0)).toThrow('Division by zero');
    });
  });
  
  describe('factorial', () => {
    test('should calculate factorial correctly', () => {
      expect(calculator.factorial(0)).toBe(1);
      expect(calculator.factorial(1)).toBe(1);
      expect(calculator.factorial(5)).toBe(120);
    });
    
    test('should throw error for negative numbers', () => {
      expect(() => calculator.factorial(-1)).toThrow('Factorial of negative number is not defined');
    });
  });
});
```

### 异步测试示例

```typescript
// src/api-client.ts
export interface User {
  id: number;
  name: string;
  email: string;
}

export class ApiClient {
  private baseUrl: string;
  
  constructor(baseUrl: string) {
    this.baseUrl = baseUrl;
  }
  
  async getUser(id: number): Promise<User> {
    const response = await fetch(`${this.baseUrl}/users/${id}`);
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    return response.json();
  }
  
  async createUser(userData: Omit<User, 'id'>): Promise<User> {
    const response = await fetch(`${this.baseUrl}/users`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(userData)
    });
    
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    
    return response.json();
  }
}
```

```typescript
// src/api-client.test.ts
import { ApiClient, User } from './api-client';

// Mock fetch globally
global.fetch = jest.fn();

describe('ApiClient', () => {
  let apiClient: ApiClient;
  const baseUrl = 'https://api.example.com';
  
  beforeEach(() => {
    apiClient = new ApiClient(baseUrl);
    (global.fetch as jest.Mock).mockClear();
  });
  
  describe('getUser', () => {
    test('should fetch user successfully', async () => {
      const mockUser: User = {
        id: 1,
        name: 'John Doe',
        email: 'john@example.com'
      };
      
      (global.fetch as jest.Mock).mockResolvedValue({
        ok: true,
        json: () => Promise.resolve(mockUser)
      });
      
      const user = await apiClient.getUser(1);
      
      expect(user).toEqual(mockUser);
      expect(global.fetch).toHaveBeenCalledWith(`${baseUrl}/users/1`);
    });
    
    test('should throw error when HTTP request fails', async () => {
      (global.fetch as jest.Mock).mockResolvedValue({
        ok: false,
        status: 404
      });
      
      await expect(apiClient.getUser(999)).rejects.toThrow('HTTP error! status: 404');
    });
  });
  
  describe('createUser', () => {
    test('should create user successfully', async () => {
      const userData = {
        name: 'Jane Doe',
        email: 'jane@example.com'
      };
      
      const mockCreatedUser: User = {
        id: 2,
        ...userData
      };
      
      (global.fetch as jest.Mock).mockResolvedValue({
        ok: true,
        json: () => Promise.resolve(mockCreatedUser)
      });
      
      const createdUser = await apiClient.createUser(userData);
      
      expect(createdUser).toEqual(mockCreatedUser);
      expect(global.fetch).toHaveBeenCalledWith(`${baseUrl}/users`, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(userData)
      });
    });
  });
});
```

## 2. 类型测试

### 使用 tsd 进行类型测试

```bash
# 安装类型测试工具
npm install --save-dev tsd
```

```typescript
// src/user-service.ts
export interface User {
  id: number;
  name: string;
  email: string;
  age?: number;
}

export class UserService {
  private users: Map<number, User> = new Map();
  
  addUser(user: Omit<User, 'id'>): User {
    const id = this.generateId();
    const newUser: User = { id, ...user };
    this.users.set(id, newUser);
    return newUser;
  }
  
  getUser(id: number): User | undefined {
    return this.users.get(id);
  }
  
  updateUser(id: number, updates: Partial<User>): User | undefined {
    const user = this.users.get(id);
    if (user) {
      const updatedUser = { ...user, ...updates };
      this.users.set(id, updatedUser);
      return updatedUser;
    }
    return undefined;
  }
  
  deleteUser(id: number): boolean {
    return this.users.delete(id);
  }
  
  private generateId(): number {
    return Math.floor(Math.random() * 1000000);
  }
}
```

```typescript
// src/user-service.test-d.ts
import { expectType, expectError } from 'tsd';
import { User, UserService } from './user-service';

// 测试正确的类型使用
expectType<UserService>(new UserService());

const userService = new UserService();

// 测试 addUser 返回类型
expectType<User>(userService.addUser({
  name: 'John',
  email: 'john@example.com'
}));

// 测试 getUser 返回类型
expectType<User | undefined>(userService.getUser(1));

// 测试 updateUser 返回类型
expectType<User | undefined>(userService.updateUser(1, { name: 'Jane' }));

// 测试类型错误 - 不能传递 id 给 addUser
expectError(userService.addUser({
  id: 1, // 这应该报错
  name: 'John',
  email: 'john@example.com'
}));

// 测试类型错误 - updateUser 的部分更新应该是安全的
const partialUpdate = userService.updateUser(1, { age: 30 });
expectType<User | undefined>(partialUpdate);
```

### 使用 dtslint 进行类型测试

```bash
# 安装 dtslint
npm install --save-dev dtslint
```

```typescript
// src/array-utils.ts
export function first<T>(array: T[]): T | undefined {
  return array[0];
}

export function last<T>(array: T[]): T | undefined {
  return array[array.length - 1];
}

export function compact<T>(array: (T | null | undefined)[]): T[] {
  return array.filter((item): item is T => item !== null && item !== undefined);
}

export function chunk<T>(array: T[], size: number): T[][] {
  const chunks: T[][] = [];
  for (let i = 0; i < array.length; i += size) {
    chunks.push(array.slice(i, i + size));
  }
  return chunks;
}
```

```typescript
// src/array-utils.test-d.ts
import { expectType } from 'tsd';
import { first, last, compact, chunk } from './array-utils';

// first function tests
const numbers = [1, 2, 3];
const strings = ['a', 'b', 'c'];
const empty: number[] = [];

expectType<number | undefined>(first(numbers));
expectType<string | undefined>(first(strings));
expectType<number | undefined>(first(empty));

// last function tests
expectType<number | undefined>(last(numbers));
expectType<string | undefined>(last(strings));
expectType<number | undefined>(last(empty));

// compact function tests
const mixedArray = [1, null, 2, undefined, 3, null];
expectType<number[]>(compact(mixedArray));

const stringArray = ['a', null, 'b', undefined, 'c'];
expectType<string[]>(compact(stringArray));

// chunk function tests
expectType<number[][]>(chunk(numbers, 2));
expectType<string[][]>(chunk(strings, 1));
```

### 复杂类型测试

```typescript
// src/advanced-types.ts
export type DeepPartial<T> = {
  [P in keyof T]?: T[P] extends object ? DeepPartial<T[P]> : T[P];
};

export type RequiredKeys<T> = {
  [K in keyof T]-?: {} extends Pick<T, K> ? never : K;
}[keyof T];

export type OptionalKeys<T> = {
  [K in keyof T]-?: {} extends Pick<T, K> ? K : never;
}[keyof T];

export interface User {
  id: number;
  name: string;
  email: string;
  profile?: {
    avatar?: string;
    bio?: string;
    preferences?: {
      theme: 'light' | 'dark';
      notifications: boolean;
    };
  };
}

export function updateUser<T extends User>(
  user: T,
  updates: DeepPartial<T>
): T {
  return { ...user, ...updates };
}
```

```typescript
// src/advanced-types.test-d.ts
import { expectType, expectError } from 'tsd';
import { DeepPartial, RequiredKeys, OptionalKeys, User, updateUser } from './advanced-types';

// 测试 DeepPartial 类型
type UserDeepPartial = DeepPartial<User>;

const partialUser: UserDeepPartial = {
  name: 'John',
  profile: {
    bio: 'Developer',
    preferences: {
      theme: 'dark'
    }
  }
};

expectType<UserDeepPartial>(partialUser);

// 测试 RequiredKeys 和 OptionalKeys
expectType<'id' | 'name' | 'email'>({} as RequiredKeys<User>);
expectType<'profile'>({} as OptionalKeys<User>);

// 测试 updateUser 函数
const user: User = {
  id: 1,
  name: 'John',
  email: 'john@example.com'
};

// 正确的更新
const updatedUser = updateUser(user, {
  name: 'Jane',
  profile: {
    bio: 'Updated bio'
  }
});

expectType<User>(updatedUser);

// 错误的更新应该被拒绝
expectError(updateUser(user, {
  id: 'not-a-number' // 类型错误
}));
```

## 3. 集成测试

### 数据库集成测试

```typescript
// src/database.ts
export interface DatabaseConfig {
  host: string;
  port: number;
  username: string;
  password: string;
  database: string;
}

export interface User {
  id: number;
  name: string;
  email: string;
  createdAt: Date;
}

export class Database {
  private config: DatabaseConfig;
  private connected: boolean = false;
  
  constructor(config: DatabaseConfig) {
    this.config = config;
  }
  
  async connect(): Promise<void> {
    // 模拟数据库连接
    await new Promise(resolve => setTimeout(resolve, 100));
    this.connected = true;
  }
  
  async disconnect(): Promise<void> {
    this.connected = false;
  }
  
  async createUser(userData: Omit<User, 'id' | 'createdAt'>): Promise<User> {
    if (!this.connected) {
      throw new Error('Database not connected');
    }
    
    const newUser: User = {
      id: Math.floor(Math.random() * 1000),
      ...userData,
      createdAt: new Date()
    };
    
    // 模拟数据库插入操作
    await new Promise(resolve => setTimeout(resolve, 50));
    return newUser;
  }
  
  async getUserById(id: number): Promise<User | null> {
    if (!this.connected) {
      throw new Error('Database not connected');
    }
    
    // 模拟数据库查询
    await new Promise(resolve => setTimeout(resolve, 30));
    return null; // 模拟未找到
  }
  
  async getAllUsers(): Promise<User[]> {
    if (!this.connected) {
      throw new Error('Database not connected');
    }
    
    // 模拟数据库查询
    await new Promise(resolve => setTimeout(resolve, 50));
    return [];
  }
}
```

```typescript
// src/database.integration.test.ts
import { Database, DatabaseConfig, User } from './database';

describe('Database Integration', () => {
  let database: Database;
  let config: DatabaseConfig;
  
  beforeAll(() => {
    config = {
      host: 'localhost',
      port: 5432,
      username: 'test',
      password: 'test',
      database: 'test_db'
    };
    database = new Database(config);
  });
  
  describe('Connection', () => {
    test('should connect to database successfully', async () => {
      await expect(database.connect()).resolves.toBeUndefined();
      // 这里可以添加连接状态检查
    });
    
    test('should disconnect from database successfully', async () => {
      await database.connect();
      await expect(database.disconnect()).resolves.toBeUndefined();
    });
  });
  
  describe('User Operations', () => {
    beforeAll(async () => {
      await database.connect();
    });
    
    afterAll(async () => {
      await database.disconnect();
    });
    
    test('should create user successfully', async () => {
      const userData = {
        name: 'John Doe',
        email: 'john@example.com'
      };
      
      const user = await database.createUser(userData);
      
      expect(user).toMatchObject({
        name: userData.name,
        email: userData.email
      });
      expect(user.id).toBeDefined();
      expect(user.createdAt).toBeInstanceOf(Date);
    });
    
    test('should retrieve user by id', async () => {
      const userData = {
        name: 'Jane Doe',
        email: 'jane@example.com'
      };
      
      const createdUser = await database.createUser(userData);
      const retrievedUser = await database.getUserById(createdUser.id);
      
      // 注意：在实际测试中，这里应该返回创建的用户
      // 但由于是模拟实现，返回 null
      expect(retrievedUser).toBeNull();
    });
    
    test('should throw error when database not connected', async () => {
      const disconnectedDb = new Database(config);
      
      await expect(disconnectedDb.createUser({
        name: 'Test',
        email: 'test@example.com'
      })).rejects.toThrow('Database not connected');
    });
    
    test('should get all users', async () => {
      const users = await database.getAllUsers();
      expect(Array.isArray(users)).toBe(true);
    });
  });
});
```

### API 集成测试

```typescript
// src/server.ts
import express, { Application, Request, Response } from 'express';
import { User } from './database';

export class Server {
  private app: Application;
  private port: number;
  
  constructor(port: number = 3000) {
    this.app = express();
    this.port = port;
    this.setupMiddleware();
    this.setupRoutes();
  }
  
  private setupMiddleware(): void {
    this.app.use(express.json());
  }
  
  private setupRoutes(): void {
    this.app.get('/health', (req: Request, res: Response) => {
      res.json({ status: 'OK', timestamp: new Date().toISOString() });
    });
    
    this.app.get('/users', (req: Request, res: Response) => {
      // 模拟获取用户列表
      const users: User[] = [];
      res.json(users);
    });
    
    this.app.post('/users', (req: Request, res: Response) => {
      const { name, email } = req.body;
      
      if (!name || !email) {
        return res.status(400).json({ error: 'Name and email are required' });
      }
      
      // 模拟创建用户
      const user: User = {
        id: Math.floor(Math.random() * 1000),
        name,
        email,
        createdAt: new Date()
      };
      
      res.status(201).json(user);
    });
    
    this.app.use((req: Request, res: Response) => {
      res.status(404).json({ error: 'Not found' });
    });
  }
  
  start(): Promise<void> {
    return new Promise((resolve) => {
      this.app.listen(this.port, () => {
        console.log(`Server running on port ${this.port}`);
        resolve();
      });
    });
  }
  
  getApp(): Application {
    return this.app;
  }
}
```

```typescript
// src/server.integration.test.ts
import request from 'supertest';
import { Server } from './server';

describe('Server Integration', () => {
  let server: Server;
  
  beforeAll(() => {
    server = new Server(0); // 0 表示随机端口
  });
  
  describe('Health Check', () => {
    test('should return health status', async () => {
      const app = server.getApp();
      
      const response = await request(app)
        .get('/health')
        .expect(200);
      
      expect(response.body).toMatchObject({
        status: 'OK'
      });
      expect(response.body.timestamp).toBeDefined();
    });
  });
  
  describe('User API', () => {
    test('should get empty users list', async () => {
      const app = server.getApp();
      
      const response = await request(app)
        .get('/users')
        .expect(200);
      
      expect(Array.isArray(response.body)).toBe(true);
      expect(response.body).toHaveLength(0);
    });
    
    test('should create user successfully', async () => {
      const app = server.getApp();
      const userData = {
        name: 'John Doe',
        email: 'john@example.com'
      };
      
      const response = await request(app)
        .post('/users')
        .send(userData)
        .expect(201);
      
      expect(response.body).toMatchObject({
        name: userData.name,
        email: userData.email
      });
      expect(response.body.id).toBeDefined();
      expect(response.body.createdAt).toBeDefined();
    });
    
    test('should return 400 for invalid user data', async () => {
      const app = server.getApp();
      const invalidData = {
        name: 'John Doe'
        // 缺少 email
      };
      
      await request(app)
        .post('/users')
        .send(invalidData)
        .expect(400);
    });
    
    test('should return 404 for non-existent routes', async () => {
      const app = server.getApp();
      
      await request(app)
        .get('/non-existent')
        .expect(404);
    });
  });
});
```

## 4. 端到端测试

### Cypress 配置

```json
// cypress.json
{
  "baseUrl": "http://localhost:3000",
  "viewportWidth": 1280,
  "viewportHeight": 720,
  "defaultCommandTimeout": 10000,
  "pageLoadTimeout": 60000,
  "video": false,
  "screenshotsFolder": "cypress/screenshots",
  "videosFolder": "cypress/videos"
}
```

```typescript
// cypress/tsconfig.json
{
  "compilerOptions": {
    "target": "ES2020",
    "lib": ["ES2020", "dom"],
    "types": ["cypress", "node"],
    "moduleResolution": "node",
    "strict": true,
    "esModuleInterop": true
  },
  "include": [
    "**/*.ts"
  ]
}
```

```typescript
// cypress/support/commands.ts
/// <reference types="cypress" />

Cypress.Commands.add('login', (email: string, password: string) => {
  cy.visit('/login');
  cy.get('[data-testid="email-input"]').type(email);
  cy.get('[data-testid="password-input"]').type(password);
  cy.get('[data-testid="login-button"]').click();
});

Cypress.Commands.add('createUser', (userData: { name: string; email: string }) => {
  cy.visit('/admin/users');
  cy.get('[data-testid="add-user-button"]').click();
  cy.get('[data-testid="name-input"]').type(userData.name);
  cy.get('[data-testid="email-input"]').type(userData.email);
  cy.get('[data-testid="save-user-button"]').click();
});

declare global {
  namespace Cypress {
    interface Chainable {
      login(email: string, password: string): Chainable<void>;
      createUser(userData: { name: string; email: string }): Chainable<void>;
    }
  }
}
```

```typescript
// cypress/integration/user-management.spec.ts
describe('User Management', () => {
  beforeEach(() => {
    // 登录管理员账户
    cy.login('admin@example.com', 'password123');
  });
  
  it('should display user list', () => {
    cy.visit('/admin/users');
    cy.get('[data-testid="user-table"]').should('be.visible');
    cy.get('[data-testid="user-row"]').should('have.length.gte', 0);
  });
  
  it('should create new user', () => {
    const newUser = {
      name: 'John Doe',
      email: 'john.doe@example.com'
    };
    
    cy.createUser(newUser);
    
    // 验证用户已创建
    cy.get('[data-testid="user-table"]').within(() => {
      cy.contains(newUser.name).should('be.visible');
      cy.contains(newUser.email).should('be.visible');
    });
  });
  
  it('should edit existing user', () => {
    cy.visit('/admin/users');
    
    // 找到第一个用户并编辑
    cy.get('[data-testid="edit-user-button"]').first().click();
    
    const updatedName = 'Updated Name';
    cy.get('[data-testid="name-input"]').clear().type(updatedName);
    cy.get('[data-testid="save-user-button"]').click();
    
    // 验证更新成功
    cy.contains(updatedName).should('be.visible');
  });
  
  it('should delete user', () => {
    cy.visit('/admin/users');
    
    // 记录删除前的用户数量
    cy.get('[data-testid="user-row"]').then(($rows) => {
      const initialCount = $rows.length;
      
      // 删除第一个用户
      cy.get('[data-testid="delete-user-button"]').first().click();
      cy.get('[data-testid="confirm-delete-button"]').click();
      
      // 验证用户数量减少
      cy.get('[data-testid="user-row"]').should('have.length', initialCount - 1);
    });
  });
});
```

### Playwright 配置

```typescript
// playwright.config.ts
import { PlaywrightTestConfig } from '@playwright/test';

const config: PlaywrightTestConfig = {
  use: {
    baseURL: 'http://localhost:3000',
    headless: true,
    viewport: { width: 1280, height: 720 },
    ignoreHTTPSErrors: true,
    video: 'retain-on-failure',
    screenshot: 'only-on-failure',
  },
  projects: [
    {
      name: 'chromium',
      use: { browserName: 'chromium' },
    },
    {
      name: 'firefox',
      use: { browserName: 'firefox' },
    },
    {
      name: 'webkit',
      use: { browserName: 'webkit' },
    },
  ],
  reporter: [
    ['list'],
    ['html', { outputFolder: 'playwright-report' }]
  ],
  timeout: 30000,
  retries: process.env.CI ? 2 : 0,
};

export default config;
```

```typescript
// tests/e2e/auth.spec.ts
import { test, expect } from '@playwright/test';

test.describe('Authentication', () => {
  test('should login successfully with valid credentials', async ({ page }) => {
    await page.goto('/login');
    
    await page.fill('[data-testid="email-input"]', 'user@example.com');
    await page.fill('[data-testid="password-input"]', 'password123');
    await page.click('[data-testid="login-button"]');
    
    await expect(page).toHaveURL('/dashboard');
    await expect(page.locator('[data-testid="welcome-message"]')).toBeVisible();
  });
  
  test('should show error for invalid credentials', async ({ page }) => {
    await page.goto('/login');
    
    await page.fill('[data-testid="email-input"]', 'invalid@example.com');
    await page.fill('[data-testid="password-input"]', 'wrongpassword');
    await page.click('[data-testid="login-button"]');
    
    await expect(page.locator('[data-testid="error-message"]')).toBeVisible();
    await expect(page.locator('[data-testid="error-message"]')).toContainText('Invalid credentials');
  });
  
  test('should logout successfully', async ({ page }) => {
    // 先登录
    await page.goto('/login');
    await page.fill('[data-testid="email-input"]', 'user@example.com');
    await page.fill('[data-testid="password-input"]', 'password123');
    await page.click('[data-testid="login-button"]');
    
    // 然后登出
    await page.click('[data-testid="user-menu"]');
    await page.click('[data-testid="logout-button"]');
    
    await expect(page).toHaveURL('/login');
  });
});
```

```typescript
// tests/e2e/navigation.spec.ts
import { test, expect } from '@playwright/test';

test.describe('Navigation', () => {
  test.beforeEach(async ({ page }) => {
    // 登录以访问受保护的页面
    await page.goto('/login');
    await page.fill('[data-testid="email-input"]', 'user@example.com');
    await page.fill('[data-testid="password-input"]', 'password123');
    await page.click('[data-testid="login-button"]');
  });
  
  test('should navigate between main pages', async ({ page }) => {
    // 导航到仪表板
    await page.click('[data-testid="dashboard-link"]');
    await expect(page).toHaveURL('/dashboard');
    await expect(page.locator('h1')).toContainText('Dashboard');
    
    // 导航到用户管理
    await page.click('[data-testid="users-link"]');
    await expect(page).toHaveURL('/users');
    await expect(page.locator('h1')).toContainText('Users');
    
    // 导航到设置
    await page.click('[data-testid="settings-link"]');
    await expect(page).toHaveURL('/settings');
    await expect(page.locator('h1')).toContainText('Settings');
  });
  
  test('should maintain navigation state', async ({ page }) => {
    await page.goto('/users');
    
    // 添加一些过滤器
    await page.fill('[data-testid="search-input"]', 'john');
    await page.click('[data-testid="apply-filters-button"]');
    
    // 导航到其他页面再返回
    await page.click('[data-testid="dashboard-link"]');
    await page.click('[data-testid="users-link"]');
    
    // 验证过滤器状态保持
    await expect(page.locator('[data-testid="search-input"]')).toHaveValue('john');
  });
});
```

## 测试最佳实践

### 1. 测试配置模板

```json
// package.json
{
  "scripts": {
    "test": "jest",
    "test:watch": "jest --watch",
    "test:coverage": "jest --coverage",
    "test:types": "tsd",
    "test:integration": "jest --config jest.integration.config.js",
    "test:e2e": "playwright test",
    "test:e2e:ui": "playwright test --headed",
    "test:all": "npm run test && npm run test:types && npm run test:integration"
  },
  "devDependencies": {
    "@types/jest": "^29.0.0",
    "jest": "^29.0.0",
    "ts-jest": "^29.0.0",
    "tsd": "^0.28.0",
    "supertest": "^6.0.0",
    "@playwright/test": "^1.30.0",
    "cypress": "^12.0.0"
  }
}
```

### 2. 测试工具链

```typescript
// src/test-utils.ts
import { jest } from '@jest/globals';

// 创建模拟数据
export function createMockUser(overrides: Partial<User> = {}): User {
  return {
    id: Math.floor(Math.random() * 1000),
    name: 'Test User',
    email: 'test@example.com',
    createdAt: new Date(),
    ...overrides
  };
}

// 等待异步操作
export async function waitFor(condition: () => boolean, timeout = 5000): Promise<void> {
  const startTime = Date.now();
  
  while (!condition() && Date.now() - startTime < timeout) {
    await new Promise(resolve => setTimeout(resolve, 100));
  }
  
  if (!condition()) {
    throw new Error(`Condition not met within ${timeout}ms`);
  }
}

// 模拟延迟
export function delay(ms: number): Promise<void> {
  return new Promise(resolve => setTimeout(resolve, ms));
}

// 重置所有模拟
export function resetAllMocks(): void {
  jest.clearAllMocks();
  jest.resetAllMocks();
}
```

### 3. 测试覆盖率配置

```javascript
// jest.config.js
module.exports = {
  // ... 其他配置
  collectCoverage: true,
  collectCoverageFrom: [
    'src/**/*.{ts,tsx}',
    '!src/**/*.d.ts',
    '!src/**/index.ts',
    '!src/types/**'
  ],
  coverageThreshold: {
    global: {
      branches: 80,
      functions: 80,
      lines: 80,
      statements: 80
    }
  },
  coverageReporters: ['text', 'lcov', 'html', 'json-summary']
};
```


# 24. 最佳实践

TypeScript 最佳实践是编写高质量、可维护代码的关键。遵循这些实践可以显著提升开发效率和代码质量。

## 1. 类型设计原则

### 明确性和可读性优先

```typescript
// ❌ 避免：模糊的类型定义
type Data = any;
type Callback = Function;
type Config = object;

// ✅ 推荐：明确的类型定义
interface UserData {
  id: number;
  name: string;
  email: string;
  createdAt: Date;
}

type ApiResponse<T> = {
  success: boolean;
  data: T;
  message?: string;
  timestamp: number;
};

type EventHandler<T> = (event: T) => void;
```

### 使用联合类型而非 any

```typescript
// ❌ 避免：使用 any
function processValue(value: any): string {
  return value.toString();
}

// ✅ 推荐：使用联合类型
function processValue(value: string | number | boolean): string {
  return String(value);
}

// ✅ 更好：使用泛型
function processValue<T>(value: T): string {
  return String(value);
}
```

### 类型守卫和类型谓词

```typescript
// 类型守卫函数
function isString(value: unknown): value is string {
  return typeof value === 'string';
}

function isNumber(value: unknown): value is number {
  return typeof value === 'number';
}

function isArray<T>(value: unknown): value is T[] {
  return Array.isArray(value);
}

// 复杂类型守卫
interface User {
  type: 'user';
  id: number;
  name: string;
}

interface Admin {
  type: 'admin';
  id: number;
  name: string;
  permissions: string[];
}

type Account = User | Admin;

function isAdmin(account: Account): account is Admin {
  return account.type === 'admin';
}

function processAccount(account: Account): void {
  if (isAdmin(account)) {
    // TypeScript 知道这里是 Admin 类型
    console.log(account.permissions);
  } else {
    // TypeScript 知道这里是 User 类型
    console.log(account.name);
  }
}
```

### 条件类型和映射类型

```typescript
// 条件类型示例
type NonNullable<T> = T extends null | undefined ? never : T;

type MyType = NonNullable<string | null>; // string
type MyType2 = NonNullable<number | undefined>; // number

// 映射类型示例
type Partial<T> = {
  [P in keyof T]?: T[P];
};

type Required<T> = {
  [P in keyof T]-?: T[P];
};

type Readonly<T> = {
  readonly [P in keyof T]: T[P];
};

// 自定义映射类型
type Mutable<T> = {
  -readonly [P in keyof T]: T[P];
};

type Nullable<T> = {
  [P in keyof T]: T[P] | null;
};

// 使用示例
interface User {
  readonly id: number;
  name: string;
  email: string;
}

type MutableUser = Mutable<User>;
type NullableUser = Nullable<User>;
type PartialUser = Partial<User>;
```

## 2. 项目结构规范

### 标准项目结构

```
my-project/
├── src/
│   ├── components/          # UI 组件
│   │   ├── Button/
│   │   │   ├── Button.tsx
│   │   │   ├── Button.types.ts
│   │   │   └── Button.styles.ts
│   │   └── index.ts
│   ├── hooks/               # 自定义 Hook
│   │   ├── useApi.ts
│   │   ├── useLocalStorage.ts
│   │   └── index.ts
│   ├── services/            # 业务服务
│   │   ├── api/
│   │   │   ├── user.service.ts
│   │   │   └── auth.service.ts
│   │   └── index.ts
│   ├── utils/               # 工具函数
│   │   ├── date.utils.ts
│   │   ├── string.utils.ts
│   │   └── index.ts
│   ├── types/               # 全局类型定义
│   │   ├── user.types.ts
│   │   ├── api.types.ts
│   │   └── index.ts
│   ├── constants/           # 常量定义
│   │   ├── app.constants.ts
│   │   └── index.ts
│   ├── store/               # 状态管理
│   │   ├── user/
│   │   │   ├── user.slice.ts
│   │   │   └── user.selectors.ts
│   │   └── index.ts
│   └── index.ts
├── tests/
│   ├── unit/
│   ├── integration/
│   └── e2e/
├── docs/
├── config/
├── scripts/
├── public/
└── package.json
```

### 按功能模块化组织

```typescript
// src/features/user/
// src/features/user/types.ts
export interface User {
  id: number;
  name: string;
  email: string;
  createdAt: Date;
}

export interface UserState {
  users: User[];
  loading: boolean;
  error: string | null;
}

// src/features/user/api.ts
import { User } from './types';

export class UserApi {
  static async getUsers(): Promise<User[]> {
    const response = await fetch('/api/users');
    return response.json();
  }
  
  static async getUserById(id: number): Promise<User> {
    const response = await fetch(`/api/users/${id}`);
    return response.json();
  }
}

// src/features/user/hooks.ts
import { useState, useEffect } from 'react';
import { UserApi } from './api';
import { User } from './types';

export function useUsers() {
  const [users, setUsers] = useState<User[]>([]);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState<string | null>(null);
  
  useEffect(() => {
    const fetchUsers = async () => {
      try {
        setLoading(true);
        const data = await UserApi.getUsers();
        setUsers(data);
      } catch (err) {
        setError(err instanceof Error ? err.message : 'Unknown error');
      } finally {
        setLoading(false);
      }
    };
    
    fetchUsers();
  }, []);
  
  return { users, loading, error };
}

// src/features/user/index.ts
export * from './types';
export * from './api';
export * from './hooks';
```

### 共享库结构

```
shared-lib/
├── packages/
│   ├── core/
│   │   ├── src/
│   │   │   ├── utils/
│   │   │   ├── types/
│   │   │   └── index.ts
│   │   ├── package.json
│   │   └── tsconfig.json
│   ├── ui/
│   │   ├── src/
│   │   │   ├── components/
│   │   │   ├── hooks/
│   │   │   └── index.ts
│   │   ├── package.json
│   │   └── tsconfig.json
│   └── api/
│       ├── src/
│       │   ├── client/
│       │   ├── types/
│       │   └── index.ts
│       ├── package.json
│       └── tsconfig.json
├── package.json
├── tsconfig.json
└── lerna.json
```

## 3. 命名约定

### 接口和类型命名

```typescript
// ✅ 接口使用 PascalCase
interface User {
  id: number;
  name: string;
  email: string;
}

interface ApiResponse<T> {
  data: T;
  status: number;
  message?: string;
}

// ✅ 类型别名使用 PascalCase
type UserRole = 'admin' | 'user' | 'guest';
type UserId = number | string;

// ✅ 泛型参数使用单个大写字母或 PascalCase
function processItems<T>(items: T[]): T[] {
  return items;
}

function createUser<U extends User>(userData: U): U {
  return userData;
}
```

### 函数和变量命名

```typescript
// ✅ 函数使用 camelCase
function getUserById(id: number): User | undefined {
  // 实现
}

function calculateTotal(items: number[]): number {
  return items.reduce((sum, item) => sum + item, 0);
}

// ✅ 变量使用 camelCase
const currentUser: User = {
  id: 1,
  name: 'John Doe',
  email: 'john@example.com'
};

const isActive = true;
const userList: User[] = [];

// ✅ 布尔值变量使用 is/has/can 等前缀
const isLoading = false;
const hasPermission = true;
const canEdit = false;
const isVisible = true;
```

### 常量命名

```typescript
// ✅ 常量使用 UPPER_SNAKE_CASE
const MAX_RETRY_ATTEMPTS = 3;
const DEFAULT_PAGE_SIZE = 20;
const API_BASE_URL = 'https://api.example.com';

// ✅ 枚举使用 PascalCase
enum HttpStatus {
  OK = 200,
  NOT_FOUND = 404,
  INTERNAL_SERVER_ERROR = 500
}

// ✅ 对象常量使用 PascalCase
const AppConstants = {
  VERSION: '1.0.0',
  NAME: 'MyApp',
  SUPPORTED_LANGUAGES: ['en', 'zh', 'es']
} as const;
```

### 文件命名

```typescript
// ✅ 组件文件使用 PascalCase
// Button.tsx
// UserProfile.tsx
// DataTable.tsx

// ✅ 工具文件使用 camelCase
// stringUtils.ts
// dateHelpers.ts
// apiClient.ts

// ✅ 类型文件使用 .types.ts 后缀
// user.types.ts
// api.types.ts
// form.types.ts

// ✅ 测试文件使用 .test.ts 或 .spec.ts 后缀
// user.service.test.ts
// button.component.spec.ts
```

## 4. 错误处理模式

### 统一错误处理

```typescript
// src/types/error.types.ts
export interface AppError {
  code: string;
  message: string;
  details?: Record<string, any>;
  timestamp: number;
}

export class CustomError extends Error {
  constructor(
    public code: string,
    message: string,
    public details?: Record<string, any>
  ) {
    super(message);
    this.name = 'CustomError';
  }
}

// src/utils/error.utils.ts
export function createError(code: string, message: string, details?: Record<string, any>): CustomError {
  return new CustomError(code, message, details);
}

export function isCustomError(error: unknown): error is CustomError {
  return error instanceof CustomError;
}

export function handleError(error: unknown): AppError {
  if (isCustomError(error)) {
    return {
      code: error.code,
      message: error.message,
      details: error.details,
      timestamp: Date.now()
    };
  }
  
  return {
    code: 'UNKNOWN_ERROR',
    message: error instanceof Error ? error.message : 'An unknown error occurred',
    timestamp: Date.now()
  };
}

// src/services/api.service.ts
import { AppError, handleError, createError } from '../utils/error.utils';

export class ApiService {
  static async request<T>(url: string, options?: RequestInit): Promise<T> {
    try {
      const response = await fetch(url, options);
      
      if (!response.ok) {
        throw createError(
          `HTTP_${response.status}`,
          `HTTP Error: ${response.status} ${response.statusText}`,
          { status: response.status, url }
        );
      }
      
      return await response.json();
    } catch (error) {
      const appError = handleError(error);
      console.error('API Error:', appError);
      throw appError;
    }
  }
}
```

### 异步操作错误处理

```typescript
// src/utils/async.utils.ts
export type Result<T, E = AppError> = {
  success: true;
  data: T;
} | {
  success: false;
  error: E;
};

export async function safeExecute<T>(
  asyncFn: () => Promise<T>
): Promise<Result<T>> {
  try {
    const data = await asyncFn();
    return { success: true, data };
  } catch (error) {
    return { success: false, error: handleError(error) };
  }
}

// 使用示例
async function fetchUserData(userId: number) {
  const result = await safeExecute(() => 
    ApiService.request<User>(`/api/users/${userId}`)
  );
  
  if (result.success) {
    return result.data;
  } else {
    console.error('Failed to fetch user:', result.error);
    return null;
  }
}
```

### 验证和断言

```typescript
// src/utils/validation.utils.ts
export function assert(condition: unknown, message: string): asserts condition {
  if (!condition) {
    throw new Error(message);
  }
}

export function assertNotNull<T>(value: T | null | undefined, message: string): T {
  assert(value != null, message);
  return value;
}

export function validateEmail(email: string): boolean {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return emailRegex.test(email);
}

// 使用示例
function processUser(user: User | null) {
  // 使用断言确保值存在
  assertNotNull(user, 'User cannot be null');
  
  // 现在 TypeScript 知道 user 不为 null
  console.log(user.name);
  
  // 验证邮箱
  if (!validateEmail(user.email)) {
    throw createError('INVALID_EMAIL', 'Invalid email format');
  }
}
```

## 5. 代码组织

### 模块化设计

```typescript
// src/modules/auth/types.ts
export interface LoginCredentials {
  email: string;
  password: string;
}

export interface AuthTokens {
  accessToken: string;
  refreshToken: string;
}

export interface AuthState {
  isAuthenticated: boolean;
  tokens: AuthTokens | null;
  user: User | null;
}

// src/modules/auth/service.ts
export class AuthService {
  static async login(credentials: LoginCredentials): Promise<AuthTokens> {
    const response = await fetch('/api/auth/login', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(credentials)
    });
    
    if (!response.ok) {
      throw new Error('Login failed');
    }
    
    return response.json();
  }
  
  static logout(): void {
    localStorage.removeItem('authTokens');
  }
}

// src/modules/auth/hooks.ts
import { useState, useEffect } from 'react';
import { AuthService } from './service';
import { AuthState, LoginCredentials } from './types';

export function useAuth() {
  const [authState, setAuthState] = useState<AuthState>({
    isAuthenticated: false,
    tokens: null,
    user: null
  });
  
  const login = async (credentials: LoginCredentials) => {
    try {
      const tokens = await AuthService.login(credentials);
      setAuthState({
        isAuthenticated: true,
        tokens,
        user: null // 可以进一步获取用户信息
      });
      return { success: true };
    } catch (error) {
      return { success: false, error };
    }
  };
  
  const logout = () => {
    AuthService.logout();
    setAuthState({
      isAuthenticated: false,
      tokens: null,
      user: null
    });
  };
  
  return { ...authState, login, logout };
}
```

### 工厂模式和策略模式

```typescript
// src/factories/component.factory.ts
export interface ComponentConfig {
  type: string;
  props: Record<string, any>;
}

export class ComponentFactory {
  private static components: Map<string, React.ComponentType<any>> = new Map();
  
  static register(type: string, component: React.ComponentType<any>): void {
    this.components.set(type, component);
  }
  
  static create(config: ComponentConfig): React.ReactElement | null {
    const Component = this.components.get(config.type);
    if (!Component) {
      console.warn(`Component type '${config.type}' not found`);
      return null;
    }
    
    return React.createElement(Component, config.props);
  }
}

// src/strategies/payment.strategy.ts
export interface PaymentStrategy {
  pay(amount: number): Promise<boolean>;
  getFee(amount: number): number;
}

export class CreditCardStrategy implements PaymentStrategy {
  async pay(amount: number): Promise<boolean> {
    // 信用卡支付逻辑
    return true;
  }
  
  getFee(amount: number): number {
    return amount * 0.029; // 2.9% 手续费
  }
}

export class PayPalStrategy implements PaymentStrategy {
  async pay(amount: number): Promise<boolean> {
    // PayPal 支付逻辑
    return true;
  }
  
  getFee(amount: number): number {
    return amount * 0.034 + 0.30; // 3.4% + $0.30
  }
}

export class PaymentProcessor {
  private strategy: PaymentStrategy;
  
  constructor(strategy: PaymentStrategy) {
    this.strategy = strategy;
  }
  
  setStrategy(strategy: PaymentStrategy): void {
    this.strategy = strategy;
  }
  
  async processPayment(amount: number): Promise<boolean> {
    const fee = this.strategy.getFee(amount);
    console.log(`Processing payment of $${amount} with fee $${fee.toFixed(2)}`);
    return await this.strategy.pay(amount);
  }
}
```

## 6. 文档编写

### JSDoc 注释规范

```typescript
/**
 * 用户服务类，提供用户相关的操作方法
 * @author John Doe
 * @version 1.0.0
 */
export class UserService {
  private users: Map<number, User> = new Map();
  
  /**
   * 根据 ID 获取用户信息
   * @param id - 用户 ID
   * @returns 用户对象，如果未找到则返回 undefined
   * @throws {CustomError} 当 ID 无效时抛出错误
   * @example
   * ```typescript
   * const user = userService.getUserById(1);
   * if (user) {
   *   console.log(user.name);
   * }
   * ```
   */
  getUserById(id: number): User | undefined {
    if (id <= 0) {
      throw createError('INVALID_ID', 'User ID must be positive');
    }
    return this.users.get(id);
  }
  
  /**
   * 创建新用户
   * @param userData - 用户数据，不包含 ID
   * @returns 创建的用户对象
   * @since 1.0.0
   * @see {@link User} 用户接口定义
   */
  createUser(userData: Omit<User, 'id'>): User {
    const id = this.generateId();
    const user: User = { id, ...userData, createdAt: new Date() };
    this.users.set(id, user);
    return user;
  }
  
  /**
   * 更新用户信息
   * @param id - 要更新的用户 ID
   * @param updates - 更新的数据
   * @returns 更新后的用户对象，如果用户不存在则返回 undefined
   * @deprecated 使用 updateUserV2 替代
   */
  updateUser(id: number, updates: Partial<User>): User | undefined {
    const user = this.users.get(id);
    if (user) {
      const updatedUser = { ...user, ...updates };
      this.users.set(id, updatedUser);
      return updatedUser;
    }
    return undefined;
  }
  
  private generateId(): number {
    return Math.floor(Math.random() * 1000000);
  }
}
```

### README 文档模板

```markdown
# 项目名称

简短的项目描述

## 🚀 快速开始

### 安装依赖
```bash
npm install
```

### 开发模式
```bash
npm run dev
```

### 构建项目
```bash
npm run build
```

## 📁 项目结构

```
src/
├── components/     # React 组件
├── hooks/         # 自定义 Hook
├── services/      # 业务服务
├── utils/         # 工具函数
├── types/         # 类型定义
└── index.ts       # 入口文件
```

## 🛠️ 技术栈

- TypeScript
- React
- Redux Toolkit
- Styled Components
- Jest
- ESLint
- Prettier

## 📖 API 文档

### 用户相关接口

#### 获取用户列表
```
GET /api/users
```

响应示例：
```json
{
  "data": [
    {
      "id": 1,
      "name": "John Doe",
      "email": "john@example.com"
    }
  ]
}
```

## 🧪 测试

### 单元测试
```bash
npm run test:unit
```

### 集成测试
```bash
npm run test:integration
```

### 端到端测试
```bash
npm run test:e2e
```

## 📈 性能优化

- 使用 React.memo 优化组件渲染
- 实现虚拟滚动处理大量数据
- 使用 Web Workers 处理复杂计算
- 启用代码分割和懒加载

## 🤝 贡献指南

1. Fork 项目
2. 创建功能分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

## 📄 许可证

MIT License - 查看 [LICENSE](LICENSE) 文件了解详情
```

## 7. 版本兼容性

### TypeScript 版本管理

```json
// package.json
{
  "engines": {
    "node": ">=16.0.0",
    "npm": ">=8.0.0"
  },
  "dependencies": {
    "typescript": "^5.0.0"
  },
  "devDependencies": {
    "@types/node": "^18.0.0",
    "@types/react": "^18.0.0",
    "@types/jest": "^29.0.0"
  }
}
```

### 浏览器兼容性配置

```json
// tsconfig.json
{
  "compilerOptions": {
    "target": "ES2020", // 根据目标浏览器选择合适的版本
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "module": "ES2020",
    "moduleResolution": "node"
  }
}
```

### Polyfill 管理

```typescript
// src/polyfills.ts
// 根据需要导入 polyfill
import 'core-js/es/array/includes';
import 'core-js/es/object/assign';
import 'core-js/es/promise';
import 'whatwg-fetch';

// 条件导入 polyfill
if (!window.Intl) {
  import('intl').then(() => {
    // Intl 已加载
  });
}

// 自定义 polyfill
if (!Array.prototype.flat) {
  Array.prototype.flat = function(depth = 1) {
    return this.reduce(function (flat: any[], toFlatten: any[]) {
      return flat.concat((Array.isArray(toFlatten) && (depth > 1)) ? toFlatten.flat(depth - 1) : toFlatten);
    }, []);
  };
}
```

### 向后兼容性检查

```typescript
// src/compatibility/utils.ts
export function isModernBrowser(): boolean {
  return 'serviceWorker' in navigator &&
         'fetch' in window &&
         'Promise' in window &&
         'Map' in window &&
         'Set' in window;
}

export function checkFeatureSupport(): {
  webAssembly: boolean;
  serviceWorker: boolean;
  pushNotifications: boolean;
  offlineSupport: boolean;
} {
  return {
    webAssembly: typeof WebAssembly !== 'undefined',
    serviceWorker: 'serviceWorker' in navigator,
    pushNotifications: 'PushManager' in window,
    offlineSupport: 'caches' in window
  };
}

// 使用示例
const support = checkFeatureSupport();
if (!support.webAssembly) {
  console.warn('WebAssembly not supported, using fallback implementation');
}
```

### 渐进式增强

```typescript
// src/progressive-enhancement.ts
export class ProgressiveEnhancement {
  static async loadModernFeatures() {
    // 动态导入现代功能
    if ('IntersectionObserver' in window) {
      const { LazyLoad } = await import('./features/lazy-load');
      LazyLoad.init();
    }
    
    if ('serviceWorker' in navigator) {
      const { ServiceWorkerManager } = await import('./features/service-worker');
      ServiceWorkerManager.register();
    }
    
    // 特性检测
    if (window.CSS && CSS.supports('display', 'grid')) {
      const { GridLayout } = await import('./features/grid-layout');
      GridLayout.enable();
    } else {
      const { FlexLayout } = await import('./features/flex-layout');
      FlexLayout.enable();
    }
  }
}

// 在应用启动时调用
ProgressiveEnhancement.loadModernFeatures();
```

## 综合最佳实践示例

```typescript
// src/app.ts - 完整的应用示例
import { UserService } from './services/user.service';
import { Logger } from './utils/logger';
import { ErrorHandler } from './utils/error-handler';
import { ProgressiveEnhancement } from './progressive-enhancement';

/**
 * 应用主类
 * 管理应用的初始化和生命周期
 */
export class App {
  private userService: UserService;
  private logger: Logger;
  
  constructor() {
    this.userService = new UserService();
    this.logger = new Logger('App');
    this.handleError = this.handleError.bind(this);
  }
  
  /**
   * 初始化应用
   */
  async init(): Promise<void> {
    try {
      this.logger.info('Initializing application');
      
      // 加载现代功能
      await ProgressiveEnhancement.loadModernFeatures();
      
      // 初始化服务
      await this.userService.init();
      
      // 绑定事件
      this.bindEvents();
      
      this.logger.info('Application initialized successfully');
    } catch (error) {
      this.handleError(error);
    }
  }
  
  /**
   * 绑定全局事件
   * @private
   */
  private bindEvents(): void {
    window.addEventListener('error', this.handleError);
    window.addEventListener('unhandledrejection', (event) => {
      this.handleError(event.reason);
    });
  }
  
  /**
   * 统一错误处理
   * @param error - 错误对象
   * @private
   */
  private handleError(error: unknown): void {
    const appError = ErrorHandler.handle(error);
    this.logger.error('Application error', appError);
    
    // 显示用户友好的错误信息
    // this.showErrorMessage(appError.message);
  }
  
  /**
   * 销毁应用
   */
  destroy(): void {
    window.removeEventListener('error', this.handleError);
    window.removeEventListener('unhandledrejection', (event) => {
      this.handleError(event.reason);
    });
    this.logger.info('Application destroyed');
  }
}

// 启动应用
const app = new App();
app.init().catch(console.error);

// 优雅关闭
window.addEventListener('beforeunload', () => {
  app.destroy();
});
```

# 25. 生态系统
- DefinitelyTyped
- TypeScript Definition Manager
- 第三方类型定义
- 开发工具支持
- IDE 集成

# 26. 高级特性

TypeScript 的高级特性为开发者提供了强大的类型系统能力，可以创建更加灵活和精确的类型定义。

## 1. 混入（Mixins）

混入是一种在不使用继承的情况下向类添加功能的模式。

### 基础混入实现

```typescript
// 定义混入函数的类型
type Constructor<T = {}> = new (...args: any[]) => T;

// 混入示例：时间戳功能
function Timestamped<TBase extends Constructor>(Base: TBase) {
  return class extends Base {
    timestamp = Date.now();
    
    getTimestamp(): number {
      return this.timestamp;
    }
    
    updateTimestamp(): void {
      this.timestamp = Date.now();
    }
  };
}

// 混入示例：激活状态功能
function Activatable<TBase extends Constructor>(Base: TBase) {
  return class extends Base {
    isActive = false;
    
    activate(): void {
      this.isActive = true;
    }
    
    deactivate(): void {
      this.isActive = false;
    }
  };
}

// 混入示例：可验证功能
function Validatable<TBase extends Constructor>(Base: TBase) {
  return class extends Base {
    errors: string[] = [];
    
    addError(error: string): void {
      this.errors.push(error);
    }
    
    clearErrors(): void {
      this.errors = [];
    }
    
    isValid(): boolean {
      return this.errors.length === 0;
    }
    
    getErrors(): string[] {
      return [...this.errors];
    }
  };
}

// 使用混入创建类
class User {
  constructor(
    public name: string,
    public email: string
  ) {}
  
  getName(): string {
    return this.name;
  }
}

// 应用多个混入
const TimestampedUser = Timestamped(User);
const ActivatableTimestampedUser = Activatable(TimestampedUser);
const FullyFeaturedUser = Validatable(ActivatableTimestampedUser);

// 创建实例
const user = new FullyFeaturedUser("Alice", "alice@example.com");

// 使用混入的功能
console.log(user.getName()); // Alice
console.log(user.getTimestamp()); // 时间戳
user.activate();
console.log(user.isActive); // true
user.addError("Invalid email format");
console.log(user.isValid()); // false
console.log(user.getErrors()); // ["Invalid email format"]
```

### 复杂混入示例

```typescript
// 通用混入工厂
function createMixin<T extends Record<string, any>>(mixin: T) {
  return <TBase extends Constructor>(Base: TBase) => {
    return class extends Base {
      constructor(...args: any[]) {
        super(...args);
        Object.assign(this, mixin);
      }
    } as Constructor<T & InstanceType<TBase>>;
  };
}

// 数据持久化混入
interface Persistence {
  save(): Promise<void>;
  load(): Promise<void>;
  delete(): Promise<void>;
}

function Persistable<TBase extends Constructor>(Base: TBase) {
  return class extends Base implements Persistence {
    private storageKey: string;
    
    constructor(...args: any[]) {
      super(...args);
      this.storageKey = this.constructor.name + '_' + Date.now();
    }
    
    async save(): Promise<void> {
      if (typeof localStorage !== 'undefined') {
        localStorage.setItem(this.storageKey, JSON.stringify(this));
      }
    }
    
    async load(): Promise<void> {
      if (typeof localStorage !== 'undefined') {
        const data = localStorage.getItem(this.storageKey);
        if (data) {
          Object.assign(this, JSON.parse(data));
        }
      }
    }
    
    async delete(): Promise<void> {
      if (typeof localStorage !== 'undefined') {
        localStorage.removeItem(this.storageKey);
      }
    }
  };
}

// 日志记录混入
function Loggable<TBase extends Constructor>(Base: TBase) {
  return class extends Base {
    private logHistory: string[] = [];
    
    protected log(message: string): void {
      const logEntry = `[${new Date().toISOString()}] ${message}`;
      this.logHistory.push(logEntry);
      console.log(logEntry);
    }
    
    getLogHistory(): string[] {
      return [...this.logHistory];
    }
  };
}

// 使用多个混入
class Product {
  constructor(
    public id: number,
    public name: string,
    public price: number
  ) {}
  
  getFormattedPrice(): string {
    return `$${this.price.toFixed(2)}`;
  }
}

// 应用混入
const EnhancedProduct = Loggable(Persistable(Product));

const product = new EnhancedProduct(1, "Laptop", 999.99);
product.log(`Product created: ${product.name}`);
await product.save();

console.log(product.getLogHistory());
```

### 混入类型约束

```typescript
// 带类型约束的混入
function WithId<TBase extends Constructor<{ id: number }>>(Base: TBase) {
  return class extends Base {
    getId(): number {
      return this.id;
    }
    
    setId(id: number): void {
      this.id = id;
    }
  };
}

// 带泛型参数的混入
function WithCollection<T, TBase extends Constructor>(Base: TBase) {
  return class extends Base {
    private items: T[] = [];
    
    addItem(item: T): void {
      this.items.push(item);
    }
    
    removeItem(item: T): void {
      const index = this.items.indexOf(item);
      if (index > -1) {
        this.items.splice(index, 1);
      }
    }
    
    getItems(): T[] {
      return [...this.items];
    }
    
    getItemCount(): number {
      return this.items.length;
    }
  };
}

// 使用泛型混入
class Container {
  name: string;
  
  constructor(name: string) {
    this.name = name;
  }
}

const CollectionContainer = WithCollection<string>(Container);
const container = new CollectionContainer("My Container");
container.addItem("item1");
container.addItem("item2");
console.log(container.getItems()); // ["item1", "item2"]
```

## 2. 模块增强

模块增强允许你为现有的模块添加新的类型声明。

### 基本模块增强

```typescript
// src/types/express.d.ts
// 为 Express 模块添加类型增强
import { User } from './user';

declare module 'express' {
  interface Request {
    user?: User;
    sessionId?: string;
    isAuthenticated(): boolean;
  }
  
  interface Response {
    success<T>(data: T, message?: string): this;
    error(message: string, status?: number): this;
    jsonSuccess<T>(data: T, message?: string): this;
  }
}

// src/middleware/auth.middleware.ts
import { Request, Response, NextFunction } from 'express';

export function authMiddleware(req: Request, res: Response, next: NextFunction) {
  // 现在可以安全地访问增强的属性
  if (req.user) {
    req.isAuthenticated = () => true;
  } else {
    req.isAuthenticated = () => false;
  }
  
  next();
}

// src/utils/response.utils.ts
import { Response } from 'express';

// 实现增强的方法
Response.prototype.success = function<T>(data: T, message?: string): Response {
  return this.status(200).json({
    success: true,
    data,
    message
  });
};

Response.prototype.error = function(message: string, status: number = 400): Response {
  return this.status(status).json({
    success: false,
    message
  });
};
```

### 第三方库增强

```typescript
// src/types/lodash.d.ts
// 为 Lodash 添加自定义方法类型
declare module 'lodash' {
  interface LoDashStatic {
    // 添加自定义方法
    deepClone<T>(value: T): T;
    isPlainObject(value: any): value is Record<string, any>;
    omitDeep<T extends object>(object: T, paths: string[]): Partial<T>;
  }
  
  interface LoDashExplicitWrapper<TValue> {
    deepClone(): this;
    omitDeep(paths: string[]): this;
  }
}

// src/types/react.d.ts
// 为 React 添加自定义属性
declare module 'react' {
  interface HTMLAttributes<T> extends DOMAttributes<T> {
    // 添加自定义 HTML 属性
    'data-testid'?: string;
    'data-cy'?: string;
  }
}

// src/types/styled-components.d.ts
// 为 styled-components 添加主题类型
import 'styled-components';

declare module 'styled-components' {
  export interface DefaultTheme {
    colors: {
      primary: string;
      secondary: string;
      background: string;
      text: string;
      border: string;
    };
    spacing: {
      xs: string;
      sm: string;
      md: string;
      lg: string;
      xl: string;
    };
    breakpoints: {
      mobile: string;
      tablet: string;
      desktop: string;
    };
  }
}
```

### 自定义模块增强

```typescript
// src/my-module.ts
export class MyClass {
  constructor(public name: string) {}
  
  greet(): string {
    return `Hello, ${this.name}!`;
  }
}

// src/types/my-module.d.ts
declare module './my-module' {
  interface MyClass {
    // 添加新的方法
    farewell(): string;
    // 添加新的属性
    createdAt: Date;
  }
}

// src/my-module-extensions.ts
import { MyClass } from './my-module';

// 实现增强的方法
MyClass.prototype.farewell = function(): string {
  return `Goodbye, ${this.name}!`;
};

// 添加增强的属性
Object.defineProperty(MyClass.prototype, 'createdAt', {
  value: new Date(),
  writable: true,
  enumerable: true,
  configurable: true
});
```

## 3. 全局增强

全局增强允许你扩展全局作用域中的类型。

### 基本全局增强

```typescript
// src/types/global.d.ts
// 扩展全局 Window 接口
declare global {
  interface Window {
    MyApp: {
      version: string;
      config: AppConfig;
      utils: {
        formatDate: (date: Date) => string;
        generateId: () => string;
      };
    };
  }
  
  // 扩展全局 Console 接口
  interface Console {
    debugInfo(message: string, ...optionalParams: any[]): void;
    debugError(message: string, ...optionalParams: any[]): void;
  }
  
  // 添加全局类型
  type UUID = string & { readonly brand: unique symbol };
  type Email = string & { readonly brand: unique symbol };
  
  // 扩展全局变量
  var __VERSION__: string;
  var __ENV__: 'development' | 'production' | 'test';
  
  // 扩展全局函数
  function uuid(): UUID;
  function isValidEmail(email: string): email is Email;
}

// src/utils/global-utils.ts
// 实现全局函数
window.MyApp = {
  version: '1.0.0',
  config: {
    apiUrl: 'https://api.example.com',
    debug: true
  },
  utils: {
    formatDate: (date: Date) => date.toISOString(),
    generateId: () => Math.random().toString(36).substr(2, 9)
  }
};

// 实现全局函数
function uuid(): UUID {
  return crypto.randomUUID() as UUID;
}

function isValidEmail(email: string): email is Email {
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
}

// 扩展 Console
console.debugInfo = function(message: string, ...optionalParams: any[]): void {
  if (__ENV__ === 'development') {
    console.log(`[DEBUG] ${message}`, ...optionalParams);
  }
};

console.debugError = function(message: string, ...optionalParams: any[]): void {
  if (__ENV__ === 'development') {
    console.error(`[DEBUG ERROR] ${message}`, ...optionalParams);
  }
};
```

### Node.js 全局增强

```typescript
// src/types/node.d.ts
declare global {
  namespace NodeJS {
    interface ProcessEnv {
      NODE_ENV: 'development' | 'production' | 'test';
      PORT?: string;
      DATABASE_URL: string;
      JWT_SECRET: string;
      API_BASE_URL: string;
    }
    
    interface Global {
      __TESTING__: boolean;
      __MOCK_DATA__: Record<string, any>;
    }
  }
  
  // 扩展全局模块
  interface NodeModule {
    hot?: {
      accept: (callback?: () => void) => void;
      dispose: (callback: (data: any) => void) => void;
    };
  }
}

// 使用增强的类型
const port = process.env.PORT ? parseInt(process.env.PORT) : 3000;
const isDev = process.env.NODE_ENV === 'development';
```

## 4. 条件类型分布式

分布式条件类型是条件类型的一个重要特性，当条件类型作用于联合类型时会分布式地应用。

### 基础分布式条件类型

```typescript
// 基本分布式条件类型
type Exclude<T, U> = T extends U ? never : T;

// 示例：从联合类型中排除某些类型
type Status = 'pending' | 'loading' | 'success' | 'error';
type LoadingStatus = Exclude<Status, 'success' | 'error'>; // 'pending' | 'loading'

type Primitive = string | number | boolean | null | undefined;
type NonNullablePrimitive = Exclude<Primitive, null | undefined>; // string | number | boolean

// Extract 类型
type Extract<T, U> = T extends U ? T : never;

type StringOrNumber = string | number | boolean;
type OnlyStringNumber = Extract<StringOrNumber, string | number>; // string | number

// NonNullable 类型
type NonNullable<T> = T extends null | undefined ? never : T;

type MaybeString = string | null | undefined;
type DefinitelyString = NonNullable<MaybeString>; // string
```

### 高级分布式条件类型

```typescript
// 提取函数参数类型
type Parameters<T> = T extends (...args: infer P) => any ? P : never;

type MyFunction = (a: string, b: number) => boolean;
type MyFunctionParams = Parameters<MyFunction>; // [string, number]

// 提取函数返回类型
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : any;

type MyFunctionReturn = ReturnType<MyFunction>; // boolean

// 提取构造函数参数
type ConstructorParameters<T> = T extends new (...args: infer P) => any ? P : never;

class MyClass {
  constructor(public name: string, public age: number) {}
}

type MyClassParams = ConstructorParameters<typeof MyClass>; // [string, number]

// 提取实例类型
type InstanceType<T> = T extends new (...args: any[]) => infer R ? R : any;

type MyClassInstance = InstanceType<typeof MyClass>; // MyClass

// 自定义分布式条件类型
type Flatten<T> = T extends any[] ? T[number] : T;

type NestedArray = number[][];
type Flattened = Flatten<NestedArray>; // number[]

type MixedType = string | number[] | boolean[][];
type FlattenedMixed = Flatten<MixedType>; // string | number | boolean[]

// 条件类型的实际应用
type FunctionPropertyNames<T> = {
  [K in keyof T]: T[K] extends Function ? K : never;
}[keyof T];

type FunctionProperties<T> = Pick<T, FunctionPropertyNames<T>>;

type NonFunctionPropertyNames<T> = {
  [K in keyof T]: T[K] extends Function ? never : K;
}[keyof T];

type NonFunctionProperties<T> = Pick<T, NonFunctionPropertyNames<T>>;

// 使用示例
interface Person {
  name: string;
  age: number;
  greet(): string;
  sayGoodbye(): void;
}

type PersonMethods = FunctionProperties<Person>; // { greet(): string; sayGoodbye(): void; }
type PersonProperties = NonFunctionProperties<Person>; // { name: string; age: number; }
```

### 复杂分布式条件类型

```typescript
// 递归条件类型
type DeepReadonly<T> = T extends Function 
  ? T 
  : T extends object 
    ? { readonly [P in keyof T]: DeepReadonly<T[P]> } 
    : T;

interface NestedObject {
  name: string;
  config: {
    debug: boolean;
    settings: {
      theme: string;
      notifications: boolean;
    };
  };
  callback: () => void;
}

type ReadonlyNested = DeepReadonly<NestedObject>;
// 所有属性都变为 readonly，但函数保持不变

// 条件类型与映射类型的结合
type MutableKeys<T> = {
  [K in keyof T]-?: T[K] extends Function 
    ? never 
    : (<U>() => U extends { [P in K]: T[K] } ? 1 : 2) extends <U>() => U extends { -readonly [P in K]: T[K] } ? 1 : 2 
      ? K 
      : never;
}[keyof T];

type ImmutableKeys<T> = {
  [K in keyof T]-?: T[K] extends Function 
    ? never 
    : (<U>() => U extends { [P in K]: T[K] } ? 1 : 2) extends <U>() => U extends { -readonly [P in K]: T[K] } ? 1 : 2 
      ? never 
      : K;
}[keyof T];

// 实用的条件类型组合
type RequiredKeys<T> = {
  [K in keyof T]-?: {} extends Pick<T, K> ? never : K;
}[keyof T];

type OptionalKeys<T> = {
  [K in keyof T]-?: {} extends Pick<T, K> ? K : never;
}[keyof T];

interface User {
  id: number;
  name: string;
  email?: string;
  age?: number;
}

type UserRequiredKeys = RequiredKeys<User>; // "id" | "name"
type UserOptionalKeys = OptionalKeys<User>; // "email" | "age"
```

## 5. 映射类型高级用法

### 基础映射类型回顾

```typescript
// TypeScript 内置映射类型
type Partial<T> = {
  [P in keyof T]?: T[P];
};

type Required<T> = {
  [P in keyof T]-?: T[P];
};

type Readonly<T> = {
  readonly [P in keyof T]: T[P];
};

type Pick<T, K extends keyof T> = {
  [P in K]: T[P];
};

type Omit<T, K extends keyof any> = Pick<T, Exclude<keyof T, K>>;

// 使用示例
interface User {
  id: number;
  name: string;
  email: string;
  age?: number;
}

type PartialUser = Partial<User>;
type RequiredUser = Required<User>;
type ReadonlyUser = Readonly<User>;
type UserBasicInfo = Pick<User, 'id' | 'name'>;
type UserWithoutId = Omit<User, 'id'>;
```

### 高级映射类型

```typescript
// 条件映射类型
type ConditionalPick<T, U> = {
  [K in keyof T as T[K] extends U ? K : never]: T[K];
};

interface ApiResponse {
  data: any[];
  status: number;
  message: string;
  timestamp: Date;
  metadata: Record<string, any>;
}

type StringProperties = ConditionalPick<ApiResponse, string>;
// { message: string }

type NumberProperties = ConditionalPick<ApiResponse, number>;
// { status: number }

type ObjectProperties = ConditionalPick<ApiResponse, object>;
// { data: any[]; metadata: Record<string, any> }

// 键重映射
type Getters<T> = {
  [K in keyof T as `get${Capitalize<string & K>}`]: () => T[K];
};

type Setters<T> = {
  [K in keyof T as `set${Capitalize<string & K>}`]: (value: T[K]) => void;
};

interface Person {
  name: string;
  age: number;
  email: string;
}

type PersonGetters = Getters<Person>;
// {
//   getName: () => string;
//   getAge: () => number;
//   getEmail: () => string;
// }

type PersonSetters = Setters<Person>;
// {
//   setName: (value: string) => void;
//   setAge: (value: number) => void;
//   setEmail: (value: string) => void;
// }

// 实现 Getter/Setter
class PersonWithAccessors implements PersonGetters, PersonSetters {
  constructor(
    public name: string,
    public age: number,
    public email: string
  ) {}
  
  getName(): string { return this.name; }
  getAge(): number { return this.age; }
  getEmail(): string { return this.email; }
  
  setName(value: string): void { this.name = value; }
  setAge(value: number): void { this.age = value; }
  setEmail(value: string): void { this.email = value; }
}
```

### 复杂映射类型

```typescript
// 递归映射类型
type DeepPartial<T> = T extends object 
  ? { [P in keyof T]?: DeepPartial<T[P]> } 
  : T;

interface NestedConfig {
  server: {
    port: number;
    host: string;
    ssl: {
      enabled: boolean;
      cert: string;
      key: string;
    };
  };
  database: {
    host: string;
    port: number;
    credentials: {
      username: string;
      password: string;
    };
  };
}

type PartialConfig = DeepPartial<NestedConfig>;
// 所有嵌套属性都变为可选

// 条件映射类型与模板字面量结合
type CamelToSnakeCase<S extends string> = S extends `${infer T}${infer U}`
  ? U extends Uncapitalize<U>
    ? `${Uncapitalize<T>}${CamelToSnakeCase<U>}`
    : `${Uncapitalize<T>}_${CamelToSnakeCase<U>}`
  : S;

type SnakeCaseKeys<T> = {
  [K in keyof T as CamelToSnakeCase<string & K>]: T[K];
};

interface ApiRequest {
  userId: number;
  firstName: string;
  lastName: string;
  emailAddress: string;
  createdAt: Date;
}

type SnakeCaseRequest = SnakeCaseKeys<ApiRequest>;
// {
//   user_id: number;
//   first_name: string;
//   last_name: string;
//   email_address: string;
//   created_at: Date;
// }

// 反向映射：SnakeCase 到 CamelCase
type SnakeToCamelCase<S extends string> = S extends `${infer T}_${infer U}`
  ? `${T}${Capitalize<SnakeToCamelCase<U>>}`
  : S;

type CamelCaseKeys<T> = {
  [K in keyof T as SnakeToCamelCase<string & K>]: T[K];
};

// 组合多种映射操作
type StrictOmit<T, K extends keyof any> = Pick<T, Exclude<keyof T, K>>;

type StrictPick<T, K extends keyof T> = Pick<T, K>;

type TransformProperties<T, Transform extends (value: any) => any> = {
  [K in keyof T]: Transform<T[K]>;
};

// 实用的映射类型工具
type Mutable<T> = {
  -readonly [P in keyof T]: T[P];
};

type Writable<T> = {
  -readonly [P in keyof T]: T[P];
};

type Nullable<T> = {
  [P in keyof T]: T[P] | null;
};

type Undefinedable<T> = {
  [P in keyof T]: T[P] | undefined;
};

// 使用示例
interface StrictUser {
  readonly id: number;
  readonly name: string;
  readonly email: string;
}

type MutableUser = Mutable<StrictUser>;
type NullableUser = Nullable<StrictUser>;
type UndefinedableUser = Undefinedable<StrictUser>;
```

## 6. 模板字面量类型高级用法

### 基础模板字面量类型

```typescript
// 基本模板字面量类型
type Greeting = `Hello, ${string}!`;
const greeting: Greeting = "Hello, World!";

type StatusMessage = `Status: ${'success' | 'error' | 'pending'}`;
const successMessage: StatusMessage = "Status: success";
const errorMessage: StatusMessage = "Status: error";

// 与联合类型结合
type HttpMethod = 'GET' | 'POST' | 'PUT' | 'DELETE';
type ApiEndpoint = `api/${string}`;
type ApiRoute = `${HttpMethod} ${ApiEndpoint}`;

const userRoute: ApiRoute = "GET api/users";
const createUserRoute: ApiRoute = "POST api/users";

// 字符串操作类型
type Capitalize<S extends string> = intrinsic;
type Uncapitalize<S extends string> = intrinsic;
type Uppercase<S extends string> = intrinsic;
type Lowercase<S extends string> = intrinsic;
```

### 高级模板字面量类型

```typescript
// 动态生成类型
type EventName<T extends string> = `on${Capitalize<T>}`;

type ClickEvent = EventName<'click'>; // "onClick"
type HoverEvent = EventName<'hover'>; // "onHover"
type SubmitEvent = EventName<'submit'>; // "onSubmit"

// 事件处理器类型
type EventHandler<T extends string> = {
  [K in EventName<T>]?: (event: any) => void;
};

interface ButtonProps extends EventHandler<'click' | 'hover' | 'focus'> {
  text: string;
  disabled?: boolean;
}

const buttonProps: ButtonProps = {
  text: "Click me",
  onClick: (event) => console.log("Button clicked"),
  onHover: (event) => console.log("Button hovered")
};

// 路径参数类型
type PathParam<T extends string> = T extends `:${infer Param}`
  ? Param
  : never;

type RouteParams<T extends string> = T extends `${infer Start}/${infer Rest}`
  ? PathParam<Start> | RouteParams<Rest>
  : PathParam<T>;

type UserRoute = "/users/:id/posts/:postId";
type UserRouteParams = RouteParams<UserRoute>; // "id" | "postId"

// 查询参数类型
type QueryParam<T extends string> = T extends `${infer Key}=${infer Value}`
  ? { [K in Key]: Value }
  : { [K in T]: string };

type QueryString<T extends string> = T extends `${infer Param}&${infer Rest}`
  ? QueryParam<Param> & QueryString<Rest>
  : QueryParam<T>;

type SearchQuery = "q=search&page=1&limit=10";
type SearchParams = QueryString<SearchQuery>;
// { q: "search"; page: "1"; limit: "10" }
```

### 复杂模板字面量类型

```typescript
// CSS 类名生成
type Size = 'small' | 'medium' | 'large';
type Variant = 'primary' | 'secondary' | 'danger';
type State = 'normal' | 'hover' | 'active' | 'disabled';

type ClassName<T extends string> = `btn-${T}`;

type ButtonSizeClass = ClassName<Size>; // "btn-small" | "btn-medium" | "btn-large"
type ButtonVariantClass = ClassName<Variant>; // "btn-primary" | "btn-secondary" | "btn-danger"
type ButtonStateClass = ClassName<State>; // "btn-normal" | "btn-hover" | "btn-active" | "btn-disabled"

type ButtonClass = `${ButtonSizeClass} ${ButtonVariantClass}${'' | ` ${ButtonStateClass}`}`;

const buttonClass: ButtonClass = "btn-medium btn-primary btn-hover";

// 环境变量类型
type EnvPrefix = 'REACT_APP_' | 'NEXT_PUBLIC_' | 'VUE_APP_';
type EnvVar<T extends string> = `${EnvPrefix}${Uppercase<T>}`;

type ApiUrlVar = EnvVar<'api_url'>; // "REACT_APP_API_URL" | "NEXT_PUBLIC_API_URL" | "VUE_APP_API_URL"
type DebugVar = EnvVar<'debug'>; // "REACT_APP_DEBUG" | "NEXT_PUBLIC_DEBUG" | "VUE_APP_DEBUG"

// 文件路径类型
type FileExtension = '.ts' | '.tsx' | '.js' | '.jsx' | '.json';
type FilePath<T extends string> = `${T}${FileExtension}`;

type ConfigFile = FilePath<'config'>; // "config.ts" | "config.tsx" | "config.js" | "config.jsx" | "config.json"
type IndexFile = FilePath<'index'>; // "index.ts" | "index.tsx" | "index.js" | "index.jsx" | "index.json"

// 版本号类型
type VersionNumber = `${number}.${number}.${number}`;
type VersionWithPrefix = `v${VersionNumber}`;

const version: VersionWithPrefix = "v1.2.3";
const version2: VersionNumber = "2.0.0";

// HTTP 状态码消息
type HttpStatusCode = 200 | 201 | 400 | 404 | 500;
type HttpStatusMessage<T extends HttpStatusCode> = 
  T extends 200 ? 'OK' :
  T extends 201 ? 'Created' :
  T extends 400 ? 'Bad Request' :
  T extends 404 ? 'Not Found' :
  T extends 500 ? 'Internal Server Error' :
  'Unknown Status';

type ApiResponseMessage = HttpStatusMessage<200>; // "OK"
type NotFoundMessage = HttpStatusMessage<404>; // "Not Found"
```

### 模板字面量类型与条件类型结合

```typescript
// 动态接口生成
type ApiEndpoints = {
  'users': { id: number; name: string };
  'posts': { id: number; title: string; content: string };
  'comments': { id: number; postId: number; text: string };
};

type ApiPath<T extends keyof ApiEndpoints> = `/api/${T}`;
type ApiPathWithId<T extends keyof ApiEndpoints> = `/api/${T}/${number}`;

type UserPath = ApiPath<'users'>; // "/api/users"
type UserPathWithId = ApiPathWithId<'users'>; // "/api/users/123"

// HTTP 方法与路径组合
type HttpMethod = 'GET' | 'POST' | 'PUT' | 'DELETE';
type HttpRoute<T extends HttpMethod, P extends string> = `${T} ${P}`;

type GetUserRoute = HttpRoute<'GET', '/api/users'>; // "GET /api/users"
type CreateUserRoute = HttpRoute<'POST', '/api/users'>; // "POST /api/users"

// 基于模板的类型安全
type RouteHandler<T extends string> = T extends `${infer Method} ${infer Path}`
  ? {
      method: Method;
      path: Path;
      handler: (req: any, res: any) => void;
    }
  : never;

const routeHandler: RouteHandler<'GET /api/users'> = {
  method: 'GET',
  path: '/api/users',
  handler: (req, res) => {
    // 处理请求
  }
};

// 复杂的模板类型操作
type Split<S extends string, D extends string> = 
  S extends `${infer T}${D}${infer U}` ? [T, ...Split<U, D>] : [S];

type PathParts = Split<'users/123/posts/456', '/'>; // ["users", "123", "posts", "456"]

type Join<T extends string[], D extends string> = 
  T extends [infer F extends string, ...infer R extends string[]]
    ? R extends []
      ? F
      : `${F}${D}${Join<R, D>}`
    : '';

type JoinedPath = Join<['api', 'users', '123'], '/'>; // "api/users/123"
```

### 实际应用场景

```typescript
// 类型安全的配置对象
type ConfigKey<T extends string> = T extends `${infer Prefix}_${infer Suffix}`
  ? `${Uppercase<Prefix>}_${Uppercase<Suffix>}`
  : Uppercase<T>;

type AppConfig = {
  [K in ConfigKey<'api_url' | 'debug_mode' | 'max_retries'>]: string;
};

const config: AppConfig = {
  API_URL: 'https://api.example.com',
  DEBUG_MODE: 'true',
  MAX_RETRIES: '3'
};

// 类型安全的事件系统
type EventType = 'click' | 'hover' | 'focus' | 'blur';
type EventCallback<E extends EventType> = (event: E) => void;

type EventMap = {
  [K in EventType as `on${Capitalize<K>}`]: EventCallback<K>;
};

interface ComponentProps extends Partial<EventMap> {
  children?: any;
}

const buttonProps: ComponentProps = {
  onClick: (event) => console.log('Clicked'),
  onFocus: (event) => console.log('Focused')
};

// 类型安全的国际化
type Locale = 'en' | 'zh' | 'es' | 'fr';
type TranslationKey = 'welcome' | 'goodbye' | 'error';

type TranslationPath<T extends TranslationKey> = `${Locale}.${T}`;

type Translations = {
  [K in TranslationPath<TranslationKey>]: string;
};

const translations: Translations = {
  'en.welcome': 'Welcome',
  'zh.welcome': '欢迎',
  'es.welcome': 'Bienvenido',
  'fr.welcome': 'Bienvenue',
  'en.goodbye': 'Goodbye',
  'zh.goodbye': '再见',
  // ... 其他翻译
};
```


# 27. 版本特性演进

TypeScript 自 2012 年发布以来，经历了多个重要版本的演进，每个版本都带来了新的特性和改进。了解这些演进历程有助于更好地使用 TypeScript。

## 1. TypeScript 1.x 特性

### TypeScript 1.0 (2014年4月)

#### 核心特性

```typescript
// 基础类型系统
interface User {
  name: string;
  age: number;
}

class UserService {
  private users: User[] = [];
  
  addUser(user: User): void {
    this.users.push(user);
  }
  
  getUser(name: string): User {
    return this.users.filter(user => user.name === name)[0];
  }
}

// 泛型支持
interface Repository<T> {
  save(item: T): void;
  findById(id: number): T;
  findAll(): T[];
}

class UserRepository implements Repository<User> {
  save(item: User): void {
    // 实现保存逻辑
  }
  
  findById(id: number): User {
    // 实现查找逻辑
    return { name: "Default", age: 0 };
  }
  
  findAll(): User[] {
    return [];
  }
}

// 函数重载
function padding(value: number): string;
function padding(value: string): string;
function padding(value: any): string {
  if (typeof value === "number") {
    return Array(value + 1).join(" ");
  }
  return value;
}

// 联合类型
type Primitive = string | number | boolean;

function processValue(value: Primitive): string {
  return value.toString();
}

// 可选参数和属性
interface Config {
  apiUrl?: string;
  timeout?: number;
  debug?: boolean;
}

function createConfig(config?: Config): Config {
  return {
    apiUrl: "http://localhost:3000",
    timeout: 5000,
    debug: false,
    ...config
  };
}
```

### TypeScript 1.3 (2014年10月)

#### 保护性（Protected）修饰符

```typescript
class Animal {
  protected name: string;
  
  constructor(name: string) {
    this.name = name;
  }
  
  move(distance: number = 0): void {
    console.log(`${this.name} moved ${distance}m.`);
  }
}

class Dog extends Animal {
  bark(): void {
    console.log(`${this.name} barks.`);
  }
  
  move(distance: number = 5): void {
    console.log(`${this.name} runs...`);
    super.move(distance);
  }
}

const dog = new Dog("Buddy");
dog.bark(); // 可以访问
dog.move(); // 可以访问
// dog.name; // 错误：不能在类外部访问 protected 成员
```

### TypeScript 1.4 (2014年10月)

#### 联合类型增强

```typescript
// 字符串字面量类型
type Easing = "ease-in" | "ease-out" | "ease-in-out";

class UIElement {
  animate(dx: number, dy: number, easing: Easing) {
    if (easing === "ease-in") {
      // ...
    } else if (easing === "ease-out") {
      // ...
    } else if (easing === "ease-in-out") {
      // ...
    }
  }
}

// 模板字符串
let greeting = `Hello, ${name}!`;

// 类型保护
function isFish(pet: Fish | Bird): pet is Fish {
  return (<Fish>pet).swim !== undefined;
}
```

### TypeScript 1.5 (2015年7月)

#### ES6 模块支持

```typescript
// math.ts
export function add(x: number, y: number): number {
  return x + y;
}

export function subtract(x: number, y: number): number {
  return x - y;
}

export default function multiply(x: number, y: number): number {
  return x * y;
}

// main.ts
import multiply, { add, subtract } from "./math";
import * as math from "./math";

console.log(add(1, 2)); // 3
console.log(multiply(3, 4)); // 12
console.log(math.subtract(5, 2)); // 3
```

#### 装饰器（实验性）

```typescript
// 装饰器示例（需要启用 experimentalDecorators）
function readonly(target: any, key: string, descriptor: PropertyDescriptor) {
  descriptor.writable = false;
  return descriptor;
}

class Greeter {
  greeting: string;
  
  constructor(message: string) {
    this.greeting = message;
  }
  
  @readonly
  greet() {
    return "Hello, " + this.greeting;
  }
}
```

## 2. TypeScript 2.x 特性

### TypeScript 2.0 (2016年9月)

#### Null 检查

```typescript
// 启用 strictNullChecks 后
let x: number; // Error: 变量未初始化
let y: number | undefined = undefined; // 正确
let z: number | null = null; // 正确

function validateEntity(e?: Entity) {
  // e 的类型是 Entity | undefined
  if (e) {
    // e 的类型是 Entity
    return e.name;
  }
}

// 非空断言操作符
function processEntity(e: Entity | null) {
  return e!.name; // 告诉编译器 e 不为 null
}
```

#### 控制流分析

```typescript
function example(x: string | number | boolean) {
  if (typeof x === "string") {
    // x 的类型是 string
    x; // string
    x = x + " World";
  } else if (typeof x === "number") {
    // x 的类型是 number
    x; // number
    x = x + 1;
  } else {
    // x 的类型是 boolean
    x; // boolean
    x = x === true;
  }
}
```

#### Never 类型

```typescript
// never 类型表示永远不会返回的函数
function error(message: string): never {
  throw new Error(message);
}

function fail() {
  return error("Something failed");
}

function infiniteLoop(): never {
  while (true) {
    // ...
  }
}

// never 在类型保护中的应用
type Foo = string | number;

function check(x: Foo) {
  if (typeof x === "string") {
    return true;
  } else if (typeof x === "number") {
    return false;
  }
  // 这里 x 的类型是 never
  return fail();
}
```

### TypeScript 2.1 (2016年12月)

#### keyof 和查找类型

```typescript
interface Person {
  name: string;
  age: number;
  location: string;
}

// keyof 操作符
type K1 = keyof Person; // "name" | "age" | "location"
type K2 = keyof Person[]; // "length" | "push" | "pop" | ...
type K3 = keyof { [x: string]: Person }; // string

// 查找类型
type P1 = Person["name"]; // string
type P2 = Person["name" | "age"]; // string | number
type P3 = string["charAt"]; // (pos: number) => string
type P4 = string[]["push"]; // (...items: string[]) => number
```

#### 映射类型

```typescript
// Partial 映射类型
type Partial<T> = {
  [P in keyof T]?: T[P];
};

interface User {
  id: number;
  name: string;
  email: string;
}

type PartialUser = Partial<User>;
// 等价于：
// {
//   id?: number;
//   name?: string;
//   email?: string;
// }

// Readonly 映射类型
type Readonly<T> = {
  readonly [P in keyof T]: T[P];
};

type ReadonlyUser = Readonly<User>;
// 等价于：
// {
//   readonly id: number;
//   readonly name: string;
//   readonly email: string;
// }
```

### TypeScript 2.2 (2017年2月)

#### 对象类型和混合类型

```typescript
// object 类型
function create(o: object | null): void {
  // ...
}

create({ prop: 0 }); // OK
create(null); // OK
// create(42); // Error
// create("string"); // Error
// create(false); // Error
// create(undefined); // Error

// 支持混合类型
type Constructor<T> = new (...args: any[]) => T;

function createInstance<T>(ctor: Constructor<T>): T {
  return new ctor();
}
```

### TypeScript 2.3 (2017年4月)

#### 生成器和 Async/Await

```typescript
// 生成器支持
function* fibonacci(): IterableIterator<number> {
  let [prev, curr] = [0, 1];
  for (;;) {
    yield curr;
    [prev, curr] = [curr, prev + curr];
  }
}

// Async/Await
async function fetchUser(id: number): Promise<User> {
  const response = await fetch(`/api/users/${id}`);
  return response.json();
}
```

## 3. TypeScript 3.x 特性

### TypeScript 3.0 (2018年7月)

#### 元组中的剩余元素

```typescript
// 带标签的元组
type Foo = [number, string, boolean];

// 剩余元素
type Arr = readonly any[];

// 剩余元素在元组中的使用
type Bar = [boolean, ...string[]]; // [boolean, string, string, ...]

function foo(...args: [number, string, boolean]) {
  // ...
}

function bar(...args: [number, ...string[]]) {
  // 第一个参数必须是 number，其余参数是 string
  const [first, ...rest] = args;
  // first: number
  // rest: string[]
}
```

#### 项目引用

```json
// tsconfig.base.json
{
  "compilerOptions": {
    "composite": true,
    "declaration": true,
    "declarationMap": true
  }
}

// packages/core/tsconfig.json
{
  "extends": "../../tsconfig.base.json",
  "compilerOptions": {
    "outDir": "../../lib/core"
  },
  "references": [
    { "path": "../shared" }
  ]
}
```

### TypeScript 3.1 (2018年9月)

#### 映射类型中的属性

```typescript
// 映射类型现在可以处理属性
function homomorphic<T>(arg: T): T {
  return arg;
}

// 支持对数组和元组的映射
type MapToPromise<T> = { [K in keyof T]: Promise<T[K]> };

type Coordinate = [number, number];
type PromiseCoordinate = MapToPromise<Coordinate>; // [Promise<number>, Promise<number>]

type Foo = { a: string; b: number; c: boolean };
type PromiseFoo = MapToPromise<Foo>; // { a: Promise<string>; b: Promise<number>; c: Promise<boolean> }
```

### TypeScript 3.2 (2018年11月)

#### BigInt 支持

```typescript
// BigInt 类型支持
const big: bigint = BigInt(100);
const anotherBig: bigint = 100n;

// BigInt 运算
const result = big + anotherBig;
const comparison = big > anotherBig;
```

#### 严格函数类型

```typescript
// 启用 strictFunctionTypes 后，函数参数类型检查更严格
interface Animal {
  name: string;
}

interface Dog extends Animal {
  breed: string;
}

// 在严格模式下，这会报错
interface Comparer<T> {
  compare: (a: T, b: T) => number;
}

declare let animalComparer: Comparer<Animal>;
declare let dogComparer: Comparer<Dog>;

// 在严格模式下，这会报错
// animalComparer = dogComparer; // Error
```

### TypeScript 3.4 (2019年3月)

#### const 断言

```typescript
// const 断言
const config = {
  apiUrl: "https://api.example.com",
  timeout: 5000,
  debug: true
} as const;

// apiUrl 的类型是 "https://api.example.com" 而不是 string
// timeout 的类型是 5000 而不是 number
// debug 的类型是 true 而不是 boolean

// 数组 const 断言
const colors = ["red", "green", "blue"] as const;
// 类型是 readonly ["red", "green", "blue"]

// 单个值 const 断言
const PI = 3.14159 as const; // 类型是 3.14159 而不是 number
```

#### 更智能的类型推断

```typescript
// 更好的数组类型推断
function getArray() {
  return [1, 2, 3]; // 推断为 number[]
}

function getTuple() {
  return [1, "hello", true] as const; // 推断为 [1, "hello", true]
}
```

## 4. TypeScript 4.x 特性

### TypeScript 4.0 (2020年8月)

#### 可变参数元组类型

```typescript
// 可变参数元组类型
type Arr = readonly any[];

function concat<T extends Arr, U extends Arr>(arr1: T, arr2: U): [...T, ...U] {
  return [...arr1, ...arr2];
}

const result = concat([1, 2, 3], ["hello"]); // [number, number, number, string]

// 剩余参数和展开
type Unshift<T extends any[], U> = [U, ...T];
type Push<T extends any[], U> = [...T, U];

type Test1 = Unshift<[number, string], boolean>; // [boolean, number, string]
type Test2 = Push<[number, string], boolean>; // [number, string, boolean]
```

#### 标签模板字符串类型

```typescript
// 更好的标签模板字符串类型推断
function tag<T extends string>(strings: TemplateStringsArray, ...values: T[]) {
  // ...
}

const result = tag`Hello ${"world"}!`; // T 被推断为 "world"
```

### TypeScript 4.1 (2020年11月)

#### 模板字面量类型

```typescript
// 模板字面量类型
type World = "world";
type Greeting = `hello ${World}`; // "hello world"

// 与联合类型结合
type VerticalAlignment = "top" | "middle" | "bottom";
type HorizontalAlignment = "left" | "center" | "right";

// 获取所有可能的对齐组合
type Alignment = `${VerticalAlignment}-${HorizontalAlignment}`;
// "top-left" | "top-center" | "top-right" | "middle-left" | ...

// 字符串操作类型
type Getter<T extends string> = `get${Capitalize<T>}`;
type Setter<T extends string> = `set${Capitalize<T>}`;

type FirstNameGetter = Getter<"firstName">; // "getFirstName"
type LastNameSetter = Setter<"lastName">; // "setLastName"
```

#### Key Remapping in Mapped Types

```typescript
// 映射类型中的键重映射
type Getters<T> = {
  [K in keyof T as `get${Capitalize<string & K>}`]: () => T[K];
};

type Setters<T> = {
  [K in keyof T as `set${Capitalize<string & K>}`]: (value: T[K]) => void;
};

interface Person {
  name: string;
  age: number;
  email: string;
}

type PersonAccessors = Getters<Person> & Setters<Person>;
// {
//   getName: () => string;
//   getAge: () => number;
//   getEmail: () => string;
//   setName: (value: string) => void;
//   setAge: (value: number) => void;
//   setEmail: (value: string) => void;
// }
```

### TypeScript 4.2 (2021年2月)

#### 剩余参数的类型推断改进

```typescript
// 更好的剩余参数类型推断
function call<T extends any[], R>(fn: (...args: T) => R, ...args: T): R {
  return fn(...args);
}

function add(a: number, b: number): number {
  return a + b;
}

const result = call(add, 1, 2); // 正确推断为 number
```

#### 元组中的前导/尾随逗号

```typescript
// 支持前导/尾随逗号
type Foo = [
  string,
  number,
  boolean,
];

const foo: Foo = [
  "hello",
  42,
  true,
];
```

### TypeScript 4.3 (2021年5月)

#### Separate Write Types on Properties

```typescript
// 属性的读写类型分离
class Thing {
  #size = 0;
  
  get size(): number {
    return this.#size;
  }
  
  set size(value: string | number | boolean) {
    let num = Number(value);
    if (!Number.isFinite(num)) {
      this.#size = 0;
      return;
    }
    this.#size = num;
  }
}
```

### TypeScript 4.4 (2021年8月)

#### 控制流分析改进

```typescript
// 更智能的控制流分析
function foo(param: unknown) {
  if (param && typeof param === "object" && "name" in param) {
    // 在 TypeScript 4.4 之前，这可能不会正确推断
    // 现在可以正确推断 param 的类型
    console.log(param.name); // OK
  }
}
```

#### Symbol 和模板字符串索引签名

```typescript
// Symbol 索引签名
const strKey = Symbol();
const numKey = Symbol();
const boolKey = Symbol();

type Key = typeof strKey | typeof numKey | typeof boolKey;

interface Foo {
  [strKey]: string;
  [numKey]: number;
  [boolKey]: boolean;
}

const foo: Foo = {
  [strKey]: "hello",
  [numKey]: 42,
  [boolKey]: true
};
```

### TypeScript 4.5 (2021年11月)

#### Awaited 类型

```typescript
// Awaited 类型用于递归解包 Promise
type A = Awaited<Promise<string>>; // string
type B = Awaited<Promise<Promise<number>>>; // number
type C = Awaited<boolean | Promise<number>>; // boolean | number

// 在 lib.es2015.promise.d.ts 中的定义
// type Awaited<T> = T extends null | undefined ? T : 
//   T extends object & { then(onfulfilled: infer F): any } ? 
//     F extends ((value: infer V, ...args: any) => any) ? 
//       Awaited<V> : 
//       never : 
//   T;
```

#### Import Assertions

```typescript
// 导入断言
import obj from "./something.json" assert { type: "json" };

// 动态导入断言
const obj = await import("./something.json", { 
  assert: { type: "json" } 
});
```

## 5. TypeScript 5.x 特性

### TypeScript 5.0 (2023年3月)

#### 装饰器标准化

```typescript
// 新的装饰器语法（符合 TC39 提案）
function loggedMethod<This, Args extends any[], Return>(
  target: (this: This, ...args: Args) => Return,
  context: ClassMethodDecoratorContext<This, (this: This, ...args: Args) => Return>
) {
  const methodName = String(context.name);
  
  function replacementMethod(this: This, ...args: Args): Return {
    console.log(`LOG: Entering method '${methodName}'.`);
    const result = target.call(this, ...args);
    console.log(`LOG: Exiting method '${methodName}'.`);
    return result;
  }
  
  return replacementMethod;
}

class Person {
  name: string;
  
  constructor(name: string) {
    this.name = name;
  }
  
  @loggedMethod
  greet() {
    console.log(`Hello, my name is ${this.name}.`);
  }
}
```

#### const 类型参数

```typescript
// const 类型参数
function f<const T>(x: T) {
  // ...
}

// 在映射类型中使用 const
type MappedType<const T> = {
  [K in keyof T]: T[K];
};
```

#### 多个配置文件扩展

```json
// tsconfig.json
{
  "extends": [
    "@tsconfig/strictest/tsconfig.json",
    "@tsconfig/node18/tsconfig.json"
  ],
  "compilerOptions": {
    "outDir": "./dist"
  }
}
```

### TypeScript 5.1 (2023年5月)

#### 未解析的 JSX 元素类型

```typescript
// 更好的 JSX 元素类型推断
const MyComponent = (props: { name: string }) => {
  return <div>Hello, {props.name}!</div>;
};

// 在 TypeScript 5.1 中，未解析的 JSX 元素有更好的类型推断
```

#### undefined 在可选属性中更准确

```typescript
// 可选属性现在更准确地反映 undefined
interface Person {
  name: string;
  age?: number;
}

function processPerson(person: Person) {
  // 在 TypeScript 5.1 中，age 的类型是 number | undefined
  if (person.age !== undefined) {
    // age 现在被正确缩小为 number
    console.log(person.age.toFixed(2));
  }
}
```

### TypeScript 5.2 (2023年9月)

#### using 声明和显式资源管理

```typescript
// using 声明（需要 Symbol.dispose）
{
  using file = new TempFile("example.txt");
  // file 在块结束时自动清理
}

// await using 声明（需要 Symbol.asyncDispose）
{
  await using connection = await connectToDatabase();
  // connection 在块结束时自动异步清理
}

// 实现显式资源管理
class TempFile implements Disposable {
  #path: string;
  
  constructor(path: string) {
    this.#path = path;
    console.log(`Created temp file: ${path}`);
  }
  
  [Symbol.dispose]() {
    console.log(`Cleaning up temp file: ${this.#path}`);
    // 清理逻辑
  }
}
```

#### 命名和匿名元组元素

```typescript
// 命名元组元素
type PersonTuple = [name: string, age: number, email: string];

function createPerson(...args: PersonTuple) {
  const [name, age, email] = args;
  return { name, age, email };
}

// 在解构时有更好的提示
const person: PersonTuple = ["Alice", 30, "alice@example.com"];
const [name, age, email] = person; // IDE 会显示名称提示
```

### TypeScript 5.3 (2023年11月)

#### Import Attributes

```typescript
// Import Attributes（替代 Import Assertions）
import obj from "./something.json" with { type: "json" };

// 动态导入
const obj = await import("./something.json", { 
  with: { type: "json" } 
});
```

#### 更好的 JSX 属性类型检查

```typescript
// 改进的 JSX 属性类型检查
interface ButtonProps {
  onClick: () => void;
  children: React.ReactNode;
  disabled?: boolean;
}

const Button = (props: ButtonProps) => {
  // 更好的类型检查和自动完成
  return <button {...props} />;
};
```

## 6. 未来发展方向

### 即将到来的特性

#### 更强大的模式匹配

```typescript
// 未来的模式匹配（提案阶段）
// function processValue(value: unknown) {
//   return match(value) {
//     when (x is string) => x.toUpperCase(),
//     when (x is number) => x.toFixed(2),
//     when ({ name, age } is { name: string, age: number }) => `${name} is ${age}`,
//     when (_) => "Unknown type"
//   };
// }
```

#### 更好的泛型推断

```typescript
// 未来的泛型推断改进
// function pipe<T>(...fns: [(arg: T) => any, ...((arg: any) => any)[]]) {
//   return (value: T) => fns.reduce((acc, fn) => fn(acc), value);
// }
//
// const result = pipe(
//   (x: number) => x + 1,
//   (x) => x * 2,  // x 的类型可以被正确推断
//   (x) => x.toString()  // 返回类型也可以被推断
// )(5);
```

#### 增量类型检查

```typescript
// 未来的增量类型检查优化
// 通过更好的增量编译和缓存机制提高大型项目的编译速度
```

### 性能优化方向

#### 更快的编译速度

```bash
# 未来的性能优化特性
# - 更智能的增量编译
# - 更好的并行处理
# - 更高效的类型检查算法
# - 更好的缓存机制
```

#### 更好的开发体验

```typescript
// 未来的开发体验改进
// - 更快的编辑器响应
// - 更准确的错误提示
// - 更好的重构支持
// - 更智能的自动完成
```

### 生态系统发展

#### 更好的工具集成

```json
// 未来的工具集成改进
{
  "compilerOptions": {
    // 更好的构建工具集成
    // 更智能的包管理器支持
    // 更好的测试工具集成
    // 更好的调试工具支持
  }
}
```

### 最佳实践演进

```typescript
// 随着 TypeScript 的发展，最佳实践也在演进

// TypeScript 1.x: 基础类型系统
// TypeScript 2.x: 严格的 null 检查
// TypeScript 3.x: 更好的类型推断
// TypeScript 4.x: 模板字面量类型
// TypeScript 5.x: 装饰器标准化和资源管理

// 未来趋势：
// - 更强大的类型系统
// - 更好的开发体验
// - 更快的编译速度
// - 更好的生态系统集成
```


# 28. 常见问题解决

在使用 TypeScript 的过程中，开发者经常会遇到各种问题。了解这些问题的解决方案对于提高开发效率至关重要。

## 1. 类型兼容性问题

### 基本类型兼容性

```typescript
// 问题：类型不兼容错误
interface User {
  id: number;
  name: string;
  email: string;
}

interface Admin {
  id: number;
  name: string;
  email: string;
  role: string;
}

// 错误：Admin 不能赋值给 User（多出 role 属性）
// const user: User = adminUser; // Error

// 解决方案 1：类型断言
const adminUser: Admin = {
  id: 1,
  name: "Admin",
  email: "admin@example.com",
  role: "admin"
};

const user1: User = adminUser as User; // 类型断言

// 解决方案 2：使用 Pick
type UserFromAdmin = Pick<Admin, 'id' | 'name' | 'email'>;
const user2: UserFromAdmin = adminUser; // 正确

// 解决方案 3：使用对象展开
const user3: User = {
  id: adminUser.id,
  name: adminUser.name,
  email: adminUser.email
};
```

### 函数类型兼容性

```typescript
// 问题：函数参数类型不兼容
type Handler1 = (event: MouseEvent) => void;
type Handler2 = (event: Event) => void;

// MouseEvent 继承自 Event，所以 Handler1 可以赋值给 Handler2
const handler1: Handler1 = (event) => console.log(event.clientX);
const handler2: Handler2 = handler1; // 正确

// 但是反过来不行
// const handler3: Handler1 = handler2; // Error

// 解决方案：使用类型守卫
function isMouseEvent(event: Event): event is MouseEvent {
  return event instanceof MouseEvent;
}

const safeHandler: Handler2 = (event) => {
  if (isMouseEvent(event)) {
    console.log(event.clientX); // 现在可以安全访问 MouseEvent 特有的属性
  }
};
```

### 泛型类型兼容性

```typescript
// 问题：泛型类型不兼容
interface Box<T> {
  value: T;
}

// 不同的泛型参数导致类型不兼容
const stringBox: Box<string> = { value: "hello" };
const numberBox: Box<number> = { value: 42 };

// 错误：类型不兼容
// const boxes: Box<string | number>[] = [stringBox, numberBox]; // Error

// 解决方案 1：使用联合类型
const boxes1: Box<string | number>[] = [stringBox, numberBox]; // 正确

// 解决方案 2：使用类型断言
const boxes2: Box<any>[] = [stringBox, numberBox]; // 不推荐

// 解决方案 3：创建通用接口
interface GenericBox {
  value: unknown;
}

const genericBoxes: GenericBox[] = [stringBox, numberBox];

// 解决方案 4：使用条件类型
type CompatibleBox<T> = T extends Box<infer U> ? Box<U> : never;
```

### 联合类型和交叉类型兼容性

```typescript
// 问题：联合类型和交叉类型的混淆
type Status = 'pending' | 'loading' | 'success' | 'error';
type LoadingStatus = 'pending' | 'loading';

// LoadingStatus 是 Status 的子集
const loadingStatus: LoadingStatus = 'pending';
const status: Status = loadingStatus; // 正确

// 但是反过来不行
// const anyStatus: Status = 'success';
// const loading: LoadingStatus = anyStatus; // Error

// 交叉类型示例
interface Nameable {
  name: string;
}

interface Ageable {
  age: number;
}

type Person = Nameable & Ageable;

const person: Person = {
  name: "Alice",
  age: 30
};

// 交叉类型可以赋值给各个接口
const nameable: Nameable = person; // 正确
const ageable: Ageable = person; // 正确
```

## 2. 循环引用问题

### 模块循环引用

```typescript
// ❌ 错误示例：循环引用
// user.ts
import { Post } from './post';

export interface User {
  id: number;
  name: string;
  posts: Post[];
}

export function createUser(name: string): User {
  return {
    id: Math.random(),
    name,
    posts: []
  };
}

// post.ts
import { User } from './user'; // 循环引用！

export interface Post {
  id: number;
  title: string;
  author: User;
}

export function createPost(title: string, author: User): Post {
  return {
    id: Math.random(),
    title,
    author
  };
}
```

### 解决方案 1：创建共享类型文件

```typescript
// types.ts
export interface User {
  id: number;
  name: string;
  posts: Post[];
}

export interface Post {
  id: number;
  title: string;
  author: User;
}

// user.ts
import { User, Post } from './types';

export function createUser(name: string): User {
  return {
    id: Math.random(),
    name,
    posts: []
  };
}

// post.ts
import { User, Post } from './types';

export function createPost(title: string, author: User): Post {
  return {
    id: Math.random(),
    title,
    author
  };
}
```

### 解决方案 2：使用延迟类型引用

```typescript
// types.ts
export interface User {
  id: number;
  name: string;
  posts: Post[]; // 直接引用
}

export interface Post {
  id: number;
  title: string;
  author: User; // 直接引用
}

// 或者使用字符串字面量类型（不推荐）
export interface PostAlternative {
  id: number;
  title: string;
  author: 'User'; // 这样做会失去类型安全
}
```

### 解决方案 3：使用接口合并

```typescript
// base-types.ts
export interface BaseEntity {
  id: number;
}

// user.ts
import { BaseEntity } from './base-types';
import type { Post } from './post'; // 使用 import type 避免运行时循环引用

export interface User extends BaseEntity {
  name: string;
  posts: Post[];
}

// post.ts
import { BaseEntity } from './base-types';
import type { User } from './user'; // 使用 import type

export interface Post extends BaseEntity {
  title: string;
  author: User;
}
```

### 解决方案 4：动态导入

```typescript
// user.ts
import { BaseEntity } from './base-types';

export interface User extends BaseEntity {
  name: string;
  posts: any[]; // 暂时使用 any
}

export async function getUserPosts(userId: number) {
  // 动态导入避免循环引用
  const { getPostsByUserId } = await import('./post');
  return getPostsByUserId(userId);
}

// post.ts
import { BaseEntity } from './base-types';
import type { User } from './user';

export interface Post extends BaseEntity {
  title: string;
  author: User;
}

export function getPostsByUserId(userId: number) {
  // 实现逻辑
  return [];
}
```

## 3. 模块解析问题

### 路径映射问题

```json
// tsconfig.json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"],
      "@components/*": ["src/components/*"],
      "@utils/*": ["src/utils/*"],
      "@types/*": ["src/types/*"]
    }
  }
}
```

```typescript
// ❌ 错误的导入路径
// import { Button } from '../../../components/Button';

// ✅ 正确的导入路径
import { Button } from '@components/Button';
import { formatDate } from '@utils/date';
import type { User } from '@types/user';
```

### 模块解析错误解决

```typescript
// 问题：找不到模块错误
// Error: Cannot find module './utils' or its corresponding type declarations.

// 解决方案 1：检查文件扩展名
// ❌ 错误
// import { helper } from './utils';

// ✅ 正确
import { helper } from './utils.ts';
// 或者
import { helper } from './utils/index';

// 解决方案 2：配置 moduleResolution
{
  "compilerOptions": {
    "moduleResolution": "node", // 或 "node16", "nodenext"
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true
  }
}

// 解决方案 3：处理 CommonJS 和 ES Modules 混合
// 对于 CommonJS 模块
import * as fs from 'fs';
import fs2 = require('fs');

// 对于 ES Modules
import { readFile } from 'fs/promises';
```

### 类型声明文件问题

```typescript
// 问题：缺少类型声明
// Error: Could not find a declaration file for module 'lodash'

// 解决方案 1：安装类型声明
// npm install --save-dev @types/lodash

// 解决方案 2：创建自己的类型声明
// src/types/lodash.d.ts
declare module 'lodash' {
  export function chunk<T>(array: T[], size: number): T[][];
  export function debounce<T extends (...args: any[]) => any>(
    func: T, 
    wait?: number
  ): T & { cancel(): void; flush(): void };
}

// 解决方案 3：使用 any（不推荐）
// declare module 'some-untyped-module' {
//   const content: any;
//   export default content;
// }
```

## 4. 性能问题诊断

### 编译性能问题

```bash
# 诊断编译性能
tsc --extendedDiagnostics

# 生成性能追踪
tsc --generateTrace ./trace

# 分析追踪文件
# 在 Chrome 中打开 chrome://tracing，然后加载生成的 trace 文件
```

### 大型项目优化

```json
// tsconfig.json - 性能优化配置
{
  "compilerOptions": {
    // 启用增量编译
    "incremental": true,
    "tsBuildInfoFile": "./dist/.tsbuildinfo",
    
    // 跳过不必要的检查
    "skipLibCheck": true,
    "skipDefaultLibCheck": true,
    
    // 限制包含的文件
    "include": ["src/**/*"],
    "exclude": ["node_modules", "dist", "**/*.test.ts"],
    
    // 不生成不必要的文件
    "declaration": false,
    "sourceMap": false,
    "inlineSourceMap": false
  }
}
```

### 类型推断性能优化

```typescript
// ❌ 避免：复杂的类型推断
function processComplex<T extends Record<string, any>>(
   T,
  processor: <K extends keyof T>(value: T[K], key: K) => any
): any {
  // 复杂的类型推断会影响性能
}

// ✅ 推荐：明确类型
interface Processable {
  [key: string]: any;
}

function processSimple(
   Processable,
  processor: (value: any, key: string) => any
): any {
  // 更快的类型检查
}
```

### 大型联合类型优化

```typescript
// ❌ 避免：过长的联合类型
type Status = 
  | 'pending' | 'processing' | 'completed' | 'failed' 
  | 'cancelled' | 'refunded' | 'disputed' | 'resolved'
  | 'archived' | 'deleted' | 'suspended' | 'active'
  | 'inactive' | 'locked' | 'unlocked' | 'verified';

// ✅ 推荐：使用枚举或常量
const Statuses = {
  PENDING: 'pending',
  PROCESSING: 'processing',
  COMPLETED: 'completed',
  FAILED: 'failed'
} as const;

type Status = typeof Statuses[keyof typeof Statuses];
```

## 5. 编译错误处理

### 常见编译错误及解决

```typescript
// 1. 类型不匹配错误
// Error: Type 'string' is not assignable to type 'number'
let count: number = "5"; // 错误

// 解决方案
let count1: number = 5; // 正确
let count2: number = parseInt("5"); // 正确
let count3 = "5" as unknown as number; // 类型断言（谨慎使用）

// 2. 属性不存在错误
// Error: Property 'toUpperCase' does not exist on type 'string | null'
const maybeString: string | null = getString();
// maybeString.toUpperCase(); // 错误

// 解决方案
if (maybeString) {
  maybeString.toUpperCase(); // 正确
}

// 或者使用可选链
maybeString?.toUpperCase();

// 3. 函数参数错误
// Error: Expected 2 arguments, but got 1
function add(a: number, b: number): number {
  return a + b;
}

// add(5); // 错误

// 解决方案
add(5, 3); // 正确

// 或者使用可选参数
function addOptional(a: number, b: number = 0): number {
  return a + b;
}

addOptional(5); // 正确

// 4. 泛型错误
// Error: Generic type 'Array<T>' requires 1 type argument(s)
// const arr: Array = [1, 2, 3]; // 错误

// 解决方案
const arr1: Array<number> = [1, 2, 3]; // 正确
const arr2: number[] = [1, 2, 3]; // 正确
```

### 错误抑制和处理

```typescript
// 1. 使用 any（谨慎使用）
// @ts-ignore - 忽略下一行的错误
const result: any = someUntypedFunction();

// @ts-expect-error - 期望下一行有错误
// @ts-expect-error
const wrong: number = "string";

// 2. 类型断言
const element = document.getElementById('myElement') as HTMLElement;

// 3. 非空断言操作符
const user = getUserById(1)!; // 告诉编译器 user 不为 null

// 4. 自定义错误处理
function safeParseJSON(json: string): unknown {
  try {
    return JSON.parse(json);
  } catch (error) {
    console.error('Failed to parse JSON:', error);
    return null;
  }
}
```

### 构建脚本中的错误处理

```json
{
  "scripts": {
    "build": "tsc --noEmitOnError",
    "build:strict": "tsc --noEmit --noErrorTruncation",
    "build:ci": "tsc --noEmit --pretty false",
    "lint": "tsc --noEmit --pretty false | grep -v 'TS1005\\|TS1006'"
  }
}
```

```javascript
// build.js
const { execSync } = require('child_process');

function build() {
  try {
    console.log('Running TypeScript compilation...');
    execSync('tsc --noEmitOnError', { stdio: 'inherit' });
    console.log('Build successful!');
  } catch (error) {
    console.error('Build failed:', error.message);
    process.exit(1);
  }
}
```

## 6. 运行时类型检查

### TypeScript 与运行时类型检查

```typescript
// TypeScript 只在编译时进行类型检查，运行时没有类型信息
interface User {
  id: number;
  name: string;
  email: string;
}

// 这在运行时会失败，因为接口在运行时不存在
function processUser(user: User) {
  // if (user instanceof User) // Error: 'User' only refers to a type
  if (typeof user === 'object' && user !== null) {
    // 手动检查属性
    if ('id' in user && 'name' in user && 'email' in user) {
      // 处理用户对象
    }
  }
}
```

### 运行时类型检查库

```typescript
// 使用 io-ts 进行运行时类型检查
import * as t from 'io-ts';
import { isLeft } from 'fp-ts/lib/Either';

// 定义运行时类型
const User = t.interface({
  id: t.number,
  name: t.string,
  email: t.string
});

type User = t.TypeOf<typeof User>;

// 验证数据
function validateUser(data: unknown): User | null {
  const result = User.decode(data);
  if (isLeft(result)) {
    console.error('Validation failed:', result.left);
    return null;
  }
  return result.right;
}

const userData = { id: 1, name: "Alice", email: "alice@example.com" };
const user = validateUser(userData);
if (user) {
  console.log('Valid user:', user);
}
```

### 自定义类型守卫

```typescript
// 创建类型守卫函数
interface User {
  id: number;
  name: string;
  email: string;
}

interface Admin extends User {
  role: string;
  permissions: string[];
}

// 基本类型守卫
function isUser(obj: any): obj is User {
  return (
    obj &&
    typeof obj === 'object' &&
    typeof obj.id === 'number' &&
    typeof obj.name === 'string' &&
    typeof obj.email === 'string'
  );
}

// 扩展类型守卫
function isAdmin(obj: any): obj is Admin {
  return (
    isUser(obj) &&
    typeof obj.role === 'string' &&
    Array.isArray(obj.permissions) &&
    obj.permissions.every((perm: any) => typeof perm === 'string')
  );
}

// 使用类型守卫
function processUserData(data: any) {
  if (isUser(data)) {
    console.log(`User: ${data.name}`);
    if (isAdmin(data)) {
      console.log(`Admin role: ${data.role}`);
    }
  } else {
    console.error('Invalid user data');
  }
}
```

### Zod 类型验证

```typescript
// 使用 Zod 进行类型验证
import { z } from 'zod';

// 定义 schema
const UserSchema = z.object({
  id: z.number(),
  name: z.string().min(1),
  email: z.string().email(),
  age: z.number().optional()
});

type User = z.infer<typeof UserSchema>;

// 验证数据
function validateAndParseUser(data: unknown): User | null {
  try {
    return UserSchema.parse(data);
  } catch (error) {
    if (error instanceof z.ZodError) {
      console.error('Validation errors:', error.errors);
    }
    return null;
  }
}

// 安全解析
function safeParseUser(data: unknown) {
  const result = UserSchema.safeParse(data);
  if (result.success) {
    return result.data;
  } else {
    console.error('Validation failed:', result.error.errors);
    return null;
  }
}

// 使用示例
const userData = { id: 1, name: "Alice", email: "alice@example.com" };
const user = validateAndParseUser(userData);
if (user) {
  console.log('Valid user:', user);
}
```

### 运行时类型检查最佳实践

```typescript
// 1. API 响应验证
interface ApiResponse<T> {
  success: boolean;
   T;
  message?: string;
}

function validateApiResponse<T>(
  data: any, 
  validator: (data: any) => data is T
): data is ApiResponse<T> {
  return (
    data &&
    typeof data === 'object' &&
    typeof data.success === 'boolean' &&
    (data.success ? validator(data.data) : true) &&
    (data.message === undefined || typeof data.message === 'string')
  );
}

// 2. 环境变量验证
const EnvSchema = z.object({
  NODE_ENV: z.enum(['development', 'production', 'test']),
  PORT: z.string().regex(/^\d+$/).transform(Number),
  DATABASE_URL: z.string().url(),
  JWT_SECRET: z.string().min(32)
});

type Env = z.infer<typeof EnvSchema>;

function validateEnv(env: Record<string, any>): Env | never {
  const result = EnvSchema.safeParse(env);
  if (!result.success) {
    throw new Error(
      `Environment validation failed: ${result.error.errors.map(e => e.message).join(', ')}`
    );
  }
  return result.data;
}

// 3. 配置文件验证
const ConfigSchema = z.object({
  server: z.object({
    port: z.number().min(1).max(65535),
    host: z.string()
  }),
  database: z.object({
    url: z.string().url(),
    pool: z.object({
      min: z.number().nonnegative(),
      max: z.number().positive()
    }).optional()
  })
});

type Config = z.infer<typeof ConfigSchema>;

function loadConfig(): Config {
  const config = require('./config.json');
  const result = ConfigSchema.safeParse(config);
  if (!result.success) {
    throw new Error(`Config validation failed: ${result.error.errors[0].message}`);
  }
  return result.data;
}
```
