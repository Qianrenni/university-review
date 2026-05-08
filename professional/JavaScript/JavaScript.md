# 一、JavaScript 基础理论

## 1.1 JavaScript 语言概述

### JavaScript 的定义和特点

**定义：**
JavaScript 是一种高级、解释型的编程语言，最初由 Netscape 公司的 Brendan Eich 在 1995 年创建。它是一种多范式的编程语言，支持面向对象编程、函数式编程和命令式编程。

**主要特点：**

- **动态类型：** 变量在运行时确定类型，无需预先声明
- **弱类型：** 允许不同类型之间的自动转换
- **基于原型：** 对象继承通过原型链实现，而非传统的类继承
- **单线程：** JavaScript 引擎使用单线程执行代码
- **事件驱动：** 通过事件循环机制处理异步操作
- **解释执行：** 代码在运行时被解释执行，而非编译执行
- **跨平台：** 可以在多种环境中运行（浏览器、服务器、移动端等）

### JavaScript 在前端和后端的应用

**前端应用：**

- **DOM 操作：** 动态修改网页内容、结构和样式
- **用户交互：** 处理点击、输入、滚动等用户事件
- **表单验证：** 客户端数据验证，提升用户体验
- **动画效果：** 创建丰富的用户界面动画和过渡效果
- **AJAX 请求：** 异步与服务器通信，实现无刷新更新
- **前端框架：** React、Vue、Angular 等现代框架的基础

**后端应用：**

- **服务器开发：** 使用 Node.js 构建 Web 服务器
- **API 开发：** 创建 RESTful API 和 GraphQL 接口
- **数据库操作：** 连接和操作各种数据库系统
- **实时应用：** 聊天应用、实时通知等
- **命令行工具：** 开发自动化脚本和 CLI 工具
- **微服务架构：** 构建轻量级、可扩展的微服务

### JavaScript 与 ECMAScript 的关系

**ECMAScript：**

- ECMAScript 是 JavaScript 的标准化规范，由 ECMA 国际组织制定
- 它定义了语言的核心语法、数据类型、内置对象等标准
- JavaScript 是 ECMAScript 规范的具体实现之一

**关系说明：**

- **标准化过程：** ECMAScript 提供语言标准，JavaScript 遵循这些标准
- **版本对应：** ES5、ES6(ES2015)、ES7(ES2016) 等版本号对应不同的 ECMAScript 标准
- **扩展功能：** JavaScript 在 ECMAScript 基础上添加了浏览器 API（如 DOM、BOM）
- **其他实现：** ActionScript、JScript 等也是 ECMAScript 的其他实现

### JavaScript 引擎工作原理

**引擎组成：**

- **解析器（Parser）：** 将源代码转换为抽象语法树（AST）
- **解释器（Interpreter）：** 将 AST 转换为字节码并执行
- **编译器（Compiler）：** 将热点代码编译为优化的机器码
- **垃圾回收器（Garbage Collector）：** 自动管理内存分配和回收

**执行流程：**

1. **词法分析：** 将源代码分解为标记（tokens）
2. **语法分析：** 构建抽象语法树（AST）
3. **编译优化：** 识别热点代码并进行优化编译
4. **代码执行：** 执行编译后的机器码或解释执行字节码
5. **内存管理：** 自动回收不再使用的内存

**主流引擎：**

- **V8（Chrome/Node.js）：** Google 开发，性能优异
- **SpiderMonkey（Firefox）：** Mozilla 开发的首个 JavaScript 引擎
- **JavaScriptCore（Safari）：** Apple 开发的引擎
- **Chakra（Edge）：** Microsoft 开发的引擎

## 1.2 JavaScript 发展历史

### ECMAScript 版本演进历程

**早期版本（1997-2009）：**

- **ES1（1997）：** 第一个正式标准，奠定了语言基础
- **ES2（1998）：** 小幅修订，主要是编辑性修改
- **ES3（1999）：** 重要版本，添加了正则表达式、异常处理等特性
- **ES4（2008）：** 由于分歧较大被废弃，但为后续版本奠定基础

**现代版本（2009至今）：**

- **ES5（2009）：** 添加严格模式、JSON 支持、数组方法等
- **ES6/ES2015（2015）：** 重大更新，引入类、模块、箭头函数等
- **ES2016：** 添加 Array.prototype.includes、指数运算符
- **ES2017：** 引入 async/await、共享内存等特性
- **ES2018：** 异步迭代器、Promise.finally 等
- **ES2019：** 可选 catch 绑定、JSON 超集等
- **ES2020：** 可选链、空值合并、BigInt 等
- **ES2021：** 逻辑赋值运算符、Promise.any 等
- **ES2022：** 顶层 await、私有字段等

### 各版本主要特性对比

**ES5 核心特性：**

- 严格模式（"use strict"）
- JSON 对象支持
- 数组新方法（forEach、map、filter 等）
- Object.create、Object.defineProperty 等

**ES6 核心特性：**

- let/const 变量声明
- 箭头函数
- 模板字符串
- 解构赋值
- 默认参数和剩余参数
- 类（Class）语法
- 模块系统
- Promise
- 生成器函数

**ES2017+ 现代特性：**

- async/await 异步语法
- 可选链操作符（?.）
- 空值合并操作符（??）
- 私有字段（#field）
- 顶层 await
- BigInt 大整数类型

### 浏览器兼容性问题

**兼容性挑战：**

- 不同浏览器对新特性的支持程度不同
- 旧版本浏览器缺乏对现代语法的支持
- 移动端浏览器兼容性更加复杂
- 企业环境中仍需支持老旧浏览器

**解决方案：**

- **转译工具：** Babel 将新语法转换为兼容代码
- **Polyfill：** 为旧环境提供缺失的 API 实现
- **特性检测：** 运行时检测浏览器支持情况
- **渐进增强：** 基础功能优先，增强功能可选

**最佳实践：**

- 使用 Babel 进行代码转译
- 配置 browserslist 指定目标浏览器
- 利用 polyfill-service 按需加载补丁
- 建立完善的测试和兼容性检查流程

### 现代 JavaScript 生态系统

**开发工具：**

- **包管理器：** npm、yarn、pnpm
- **构建工具：** Webpack、Rollup、Vite
- **代码检查：** ESLint、JSHint
- **代码格式化：** Prettier
- **测试框架：** Jest、Mocha、Cypress

**框架和库：**

- **前端框架：** React、Vue、Angular
- **状态管理：** Redux、Vuex、MobX
- **路由管理：** React Router、Vue Router
- **UI 组件库：** Ant Design、Element UI、Material-UI

**运行环境：**

- **浏览器环境：** Chrome、Firefox、Safari、Edge
- **服务器环境：** Node.js 及其各种版本
- **移动开发：** React Native、Ionic
- **桌面应用：** Electron、NW.js

**发展趋势：**

- **模块化：** ES6 模块成为标准
- **类型安全：** TypeScript 越来越受欢迎
- **函数式编程：** 更多函数式编程特性的引入
- **性能优化：** 持续的引擎优化和新特性
- **生态完善：** 丰富的工具链和社区支持

# 二、JavaScript 核心语法

## 2.1 变量声明和作用域

### var、let、const 的区别和使用场景

```javascript
// var - 函数作用域
function varExample() {
    if (true) {
        var x = 1;
    }
    console.log(x); // 1 - 可以访问，不受块级限制
}

// var - 变量提升
console.log(a); // undefined (不是报错)
var a = 5;

// var - 重复声明
var b = 1;
var b = 2; // 允许重复声明

// let - 块级作用域
function letExample() {
    if (true) {
        let y = 1;
    }
    // console.log(y); // ReferenceError: y is not defined
}

// let - 暂时性死区
// console.log(c); // ReferenceError: Cannot access 'c' before initialization
let c = 5;

// let - 禁止重复声明
let d = 1;
// let d = 2; // SyntaxError: Identifier 'd' has already been declared

// const - 块级作用域 + 禁止重新赋值
const PI = 3.14159;
// PI = 3.14; // TypeError: Assignment to constant variable

// const - 必须初始化
// const name; // SyntaxError: Missing initializer in const declaration

// const - 对象和数组可以修改内容
const obj = { name: "张三" };
obj.name = "李四"; // 可以修改属性
obj.age = 25; // 可以添加属性

const arr = [1, 2, 3];
arr.push(4); // 可以修改数组内容
// arr = [5, 6, 7]; // TypeError: Assignment to constant variable
```

### 变量提升机制

```javascript
// var 提升示例
console.log(name); // undefined
var name = "张三";
console.log(name); // "张三"

// 等价于：
// var name;
// console.log(name); // undefined
// name = "张三";
// console.log(name); // "张三"

// let/const 暂时性死区
function temporalDeadZone() {
    // console.log(x); // ReferenceError
    let x = 1;
}

// 函数提升
sayHello(); // "Hello!" - 函数声明被完全提升

function sayHello() {
    console.log("Hello!");
}

// 函数表达式只提升变量声明
// sayHi(); // TypeError: sayHi is not a function
var sayHi = function() {
    console.log("Hi!");
};

// 提升顺序示例
function hoistingOrder() {
    console.log(typeof foo); // "function"
    var foo = "变量";
    function foo() {
        return "函数";
    }
    console.log(typeof foo); // "string"
}
```

### 作用域链概念

```javascript
// 全局作用域
var globalVar = "全局变量";

function outer() {
    // 函数作用域
    var outerVar = "外层变量";
    
    function inner() {
        // 内层函数作用域
        var innerVar = "内层变量";
        
        // 作用域链查找：inner -> outer -> global
        console.log(innerVar);  // "内层变量"
        console.log(outerVar);  // "外层变量"
        console.log(globalVar); // "全局变量"
    }
    
    inner();
    // console.log(innerVar); // ReferenceError: innerVar is not defined
}

outer();
// console.log(outerVar); // ReferenceError: outerVar is not defined

// 闭包中的作用域链
function createCounter() {
    let count = 0; // 私有变量
    
    return function() {
        count++; // 保持对外层变量的引用
        return count;
    };
}

const counter = createCounter();
console.log(counter()); // 1
console.log(counter()); // 2
console.log(counter()); // 3
```

### 块级作用域和函数作用域

```javascript
// 函数作用域示例
function functionScope() {
    var i = 0;
    if (true) {
        var i = 1; // 同一个变量
        console.log(i); // 1
    }
    console.log(i); // 1 - 变量被覆盖
}

// 块级作用域示例
function blockScope() {
    let j = 0;
    if (true) {
        let j = 1; // 新的变量
        console.log(j); // 1
    }
    console.log(j); // 0 - 原变量未被影响
}

// 循环中的变量声明
// 使用 var 的问题
for (var k = 0; k < 3; k++) {
    setTimeout(() => {
        console.log(k); // 输出 3, 3, 3
    }, 100);
}

// 使用 let 的正确方式
for (let l = 0; l < 3; l++) {
    setTimeout(() => {
        console.log(l); // 输出 0, 1, 2
    }, 100);
}
```

## 2.2 数据类型系统

### 基本数据类型（原始类型）

```javascript
// Number 类型
let num1 = 42;           // 整数
let num2 = 3.14;         // 浮点数
let num3 = 0xFF;         // 十六进制: 255
let num4 = 0b1010;       // 二进制: 10
let num5 = 0o755;        // 八进制: 493
let nan = NaN;           // 非数字
let infinity = Infinity; // 无穷大
let negativeInfinity = -Infinity; // 负无穷大

// String 类型
let str1 = "双引号字符串";
let str2 = '单引号字符串';
let str3 = `模板字符串`;
let str4 = "包含\"引号\"的字符串";
let str5 = `多行
字符串`;

// Boolean 类型
let bool1 = true;
let bool2 = false;

// falsy 值
console.log(Boolean(false));     // false
console.log(Boolean(0));         // false
console.log(Boolean(""));        // false
console.log(Boolean(null));      // false
console.log(Boolean(undefined)); // false
console.log(Boolean(NaN));       // false

// Undefined 类型
let undefinedVar;
console.log(undefinedVar); // undefined
console.log(typeof undefinedVar); // "undefined"

// Null 类型
let nullVar = null;
console.log(typeof nullVar); // "object" (历史遗留问题)

// Symbol 类型
let sym1 = Symbol('description');
let sym2 = Symbol('description');
console.log(sym1 === sym2); // false - 每个 Symbol 都是唯一的

// 对象属性的唯一标识
let obj = {
    [sym1]: "symbol 属性值"
};

// BigInt 类型
let bigInt1 = 123456789012345678901234567890n;
let bigInt2 = BigInt("123456789012345678901234567890");
```

### 引用数据类型

```javascript
// Object 类型
let person = {
    name: "张三",
    age: 25,
    hobbies: ["读书", "游泳"],
    address: {
        city: "北京",
        street: "长安街"
    }
};

// 动态添加属性
person.job = "程序员";
person["salary"] = 10000;

// Array 类型
let arr1 = [1, 2, 3];
let arr2 = new Array(1, 2, 3);
let arr3 = Array.of(1, 2, 3);
let arr4 = Array.from("hello"); // ['h', 'e', 'l', 'l', 'o']

// Function 类型
function normalFunction(a, b) {
    return a + b;
}

let arrowFunction = (a, b) => a + b;

let anonymousFunction = function(a, b) {
    return a + b;
};

// Date 类型
let now = new Date();
let specificDate = new Date("2023-01-01");
let timestampDate = new Date(1672531200000);

// RegExp 类型
let regex1 = /pattern/flags;
let regex2 = new RegExp("pattern", "flags");
let emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
```

### 类型检测方法和区别

```javascript
// typeof 操作符
console.log(typeof 42);              // "number"
console.log(typeof "hello");         // "string"
console.log(typeof true);            // "boolean"
console.log(typeof undefined);       // "undefined"
console.log(typeof null);            // "object" (历史遗留问题)
console.log(typeof {});              // "object"
console.log(typeof []);              // "object"
console.log(typeof function(){});    // "function"
console.log(typeof Symbol());        // "symbol"
console.log(typeof BigInt(123));     // "bigint"

// instanceof 操作符
let arr = [1, 2, 3];
let obj = { name: "张三" };
let date = new Date();

console.log(arr instanceof Array);   // true
console.log(obj instanceof Object);  // true
console.log(date instanceof Date);   // true
console.log(arr instanceof Object);  // true (Array 继承自 Object)

// constructor 属性
console.log([].constructor === Array);           // true
console.log({}.constructor === Object);          // true
console.log(new Date().constructor === Date);    // true

// Object.prototype.toString.call() - 最准确的方法
console.log(Object.prototype.toString.call([]));           // "[object Array]"
console.log(Object.prototype.toString.call({}));           // "[object Object]"
console.log(Object.prototype.toString.call(null));         // "[object Null]"
console.log(Object.prototype.toString.call(undefined));    // "[object Undefined]"
console.log(Object.prototype.toString.call(function(){})); // "[object Function]"

// Array.isArray()
console.log(Array.isArray([]));      // true
console.log(Array.isArray({}));      // false
console.log(Array.isArray("array")); // false
```

### 类型转换规则和隐式转换

```javascript
// 显式类型转换
let num = Number("123");        // 123
let str = String(123);          // "123"
let bool = Boolean(123);        // true

let int = parseInt("123.45");   // 123
let float = parseFloat("123.45"); // 123.45

// 隐式类型转换场景
// 算术运算中的转换
console.log("5" - 3);           // 2 (字符串转数字)
console.log("5" + 3);           // "53" (数字转字符串)
console.log(true + 1);          // 2 (布尔转数字)
console.log(null + 5);          // 5 (null转数字)

// 比较运算中的转换
console.log("10" == 10);        // true (字符串转数字)
console.log(true == 1);         // true (布尔转数字)
console.log(null == undefined); // true (特殊规则)
console.log("" == 0);           // true (空字符串转数字)

// 布尔运算中的转换
if ("hello") { /* 执行 */ }     // 非空字符串为 true
if (0) { /* 不执行 */ }         // 0 为 false
if ({}) { /* 执行 */ }          // 对象为 true

// 字符串拼接中的转换
console.log("结果: " + 42);     // "结果: 42"
console.log(1 + 2 + "3");       // "33" (左到右计算)
console.log("1" + 2 + 3);       // "123" (左到右计算)

// 特殊情况
console.log(NaN == NaN);        // false
console.log(NaN === NaN);       // false
console.log(Object.is(NaN, NaN)); // true

console.log(0 == -0);           // true
console.log(0 === -0);          // true
console.log(Object.is(0, -0));  // false

console.log(null == undefined); // true
console.log(null === undefined); // false
console.log(Object.is(null, undefined)); // false
```

## 2.3 运算符体系

### 算术运算符和优先级

```javascript
// 基本算术运算符
let a = 10, b = 3;
console.log(a + b);  // 13 - 加法
console.log(a - b);  // 7 - 减法
console.log(a * b);  // 30 - 乘法
console.log(a / b);  // 3.333... - 除法
console.log(a % b);  // 1 - 取模
console.log(a ** b); // 1000 - 幂运算 (10的3次方)

// 一元运算符
let x = 5;
console.log(++x);    // 6 - 前置递增
console.log(x++);    // 6 - 后置递增，返回递增前的值
console.log(x);      // 7

let y = 5;
console.log(--y);    // 4 - 前置递减
console.log(y--);    // 4 - 后置递减，返回递减前的值
console.log(y);      // 3

console.log(+x);     // 7 - 转换为数字
console.log(-x);     // -7 - 转换为数字并取反

// 运算符优先级
let result1 = 2 + 3 * 4;        // 14 (乘法优先)
let result2 = (2 + 3) * 4;      // 20 (括号优先)
let result3 = 2 ** 3 * 4;       // 32 (幂运算优先级高于乘法)
let result4 = 2 + 3 - 1;        // 4 (同级从左到右)

// 特殊运算规则
console.log(0 / 0);             // NaN
console.log(1 / 0);             // Infinity
console.log(-1 / 0);            // -Infinity
console.log(Infinity + 1);      // Infinity
console.log(Infinity - Infinity); // NaN
```

### 比较运算符和相等性判断

```javascript
// 比较运算符
console.log(5 > 3);             // true
console.log(5 < 3);             // false
console.log(5 >= 5);            // true
console.log(5 <= 4);            // false

// 相等性判断
console.log(5 == "5");          // true (抽象相等，类型转换)
console.log(5 === "5");         // false (严格相等，不转换)
console.log(5 != "6");          // true (抽象不等)
console.log(5 !== "5");         // true (严格不等)

// Object.is() 方法
console.log(Object.is(5, 5));           // true
console.log(Object.is(0, -0));          // false
console.log(Object.is(NaN, NaN));       // true
console.log(Object.is(null, undefined)); // false

// 类型转换规则示例
console.log("10" > 9);          // true (字符串转数字)
console.log(true > 0);          // true (布尔转数字)
console.log(false == 0);        // true (布尔转数字)
console.log("" == 0);           // true (空字符串转数字)
console.log(" " == 0);          // true (空白字符串转数字)
console.log("0" == false);      // true (复杂转换链)

// 比较特殊情况
console.log(NaN == NaN);        // false
console.log(NaN === NaN);       // false
console.log(NaN != NaN);        // true
console.log(NaN !== NaN);       // true

console.log(null == undefined); // true
console.log(null === undefined); // false

console.log(0 == false);        // true
console.log(0 === false);       // false

console.log("" == false);       // true
console.log("" === false);      // false
```

### 逻辑运算符和短路求值

```javascript
// 基本逻辑运算符
console.log(true && true);      // true
console.log(true && false);     // false
console.log(false && true);     // false
console.log(false && false);    // false

console.log(true || true);      // true
console.log(true || false);     // true
console.log(false || true);     // true
console.log(false || false);    // false

console.log(!true);             // false
console.log(!false);            // true

// 短路求值特性
let obj = null;
// console.log(obj.name);       // TypeError
console.log(obj && obj.name);  // null (短路，不执行 obj.name)

let user = { name: "张三" };
console.log(user && user.name); // "张三" (不短路，执行 user.name)

let defaultName = "默认用户";
let userName = "" || defaultName; // "默认用户" (空字符串为 falsy)

// 返回值特点
console.log("hello" && "world"); // "world" (最后一个真值)
console.log("hello" && 0 && "world"); // 0 (第一个假值)
console.log("hello" || "world"); // "hello" (第一个真值)
console.log("" || 0 || "default"); // "default" (最后一个假值)

// 实际应用
function greet(name) {
    name = name || "访客"; // 设置默认值
    console.log("你好, " + name);
}

greet();        // "你好, 访客"
greet("张三");   // "你好, 张三"

// 新增逻辑运算符
// 空值合并运算符 ??
let value1 = null ?? "默认值";    // "默认值"
let value2 = undefined ?? "默认值"; // "默认值"
let value3 = "" ?? "默认值";      // "" (空字符串不是 null/undefined)
let value4 = 0 ?? "默认值";       // 0 (0 不是 null/undefined)

// 逻辑赋值运算符
let obj1 = { x: 1, y: 0 };
obj1.x &&= 2;   // obj1.x = 2 (因为 x 为真)
obj1.y &&= 3;   // obj1.y = 0 (因为 y 为假，不执行赋值)
obj1.z ||= 10;  // obj1.z = 10 (因为 z 为 undefined，为假)
obj1.x ||= 20;  // obj1.x = 2 (因为 x 为真，不执行赋值)

let obj2 = { a: null, b: 0 };
obj2.a ??= "默认"; // obj2.a = "默认" (因为 a 为 null)
obj2.b ??= "默认"; // obj2.b = 0 (因为 b 不是 null/undefined)
```

### 赋值运算符和复合赋值

```javascript
// 基本赋值运算符
let a = 10;
let b = 20;
let c = 30;

// 链式赋值
let x = y = z = 5; // x=5, y=5, z=5

// 解构赋值
// 数组解构
let [first, second, third] = [1, 2, 3];
console.log(first);  // 1
console.log(second); // 2
console.log(third);  // 3

// 带默认值的数组解构
let [p, q = 10, r = 20] = [1, 2];
console.log(p); // 1
console.log(q); // 2
console.log(r); // 20

// 剩余元素
let [head, ...tail] = [1, 2, 3, 4, 5];
console.log(head); // 1
console.log(tail); // [2, 3, 4, 5]

// 对象解构
let person = { name: "张三", age: 25, city: "北京" };
let { name, age } = person;
console.log(name); // "张三"
console.log(age);  // 25

// 重命名属性
let { name: fullName, age: userAge } = person;
console.log(fullName); // "张三"
console.log(userAge);  // 25

// 带默认值的对象解构
let { job = "程序员", salary = 8000 } = person;
console.log(job);    // "程序员" (person中没有job属性)
console.log(salary); // 8000

// 嵌套解构
let company = {
    name: "科技公司",
    address: {
        city: "深圳",
        district: "南山区"
    },
    employees: ["张三", "李四"]
};

let { 
    name: companyName,
    address: { city, district },
    employees: [emp1, emp2]
} = company;

console.log(companyName); // "科技公司"
console.log(city);        // "深圳"
console.log(district);    // "南山区"
console.log(emp1);        // "张三"
console.log(emp2);        // "李四"

// 复合赋值运算符
let num = 10;
num += 5;   // num = num + 5 = 15
num -= 3;   // num = num - 3 = 12
num *= 2;   // num = num * 2 = 24
num /= 4;   // num = num / 4 = 6
num %= 4;   // num = num % 4 = 2
num **= 3;  // num = num ** 3 = 8

// 位运算赋值
let flag = 5; // 二进制: 101
flag <<= 1;   // 左移一位: 1010 (10)
flag >>= 1;   // 右移一位: 101 (5)
flag &= 3;    // 按位与: 101 & 011 = 001 (1)
flag |= 2;    // 按位或: 001 | 010 = 011 (3)
flag ^= 1;    // 按位异或: 011 ^ 001 = 010 (2)

// 赋值运算特点
let result = (a = 5); // 赋值表达式的返回值是赋值的值
console.log(result);  // 5
console.log(a);       // 5

// 解构赋值的实际应用
// 交换变量值
let m = 1, n = 2;
[m, n] = [n, m];
console.log(m); // 2
console.log(n); // 1

// 函数参数解构
function printUser({ name, age, city = "未知" }) {
    console.log(`${name}, ${age}岁, 来自${city}`);
}

printUser({ name: "张三", age: 25 }); // "张三, 25岁, 来自未知"

// 返回多个值
function getCoordinates() {
    return [100, 200];
}

let [x, y] = getCoordinates();
console.log(`坐标: (${x}, ${y})`); // "坐标: (100, 200)"
```

# 三、程序控制结构

程序控制结构是编程语言中控制程序执行流程的基本机制，主要包括条件控制和循环控制两大类。掌握这些结构对于编写高效、可读性强的代码至关重要。

## 3.1 条件控制语句

### if...else 语句的嵌套使用

#### 基本语法结构

```javascript
// 单层if语句
if (条件) {
    // 执行语句
}

// if...else语句
if (条件) {
    // 条件为真时执行
} else {
    // 条件为假时执行
}

// 多重if...else嵌套
if (条件1) {
    // 执行语句1
} else if (条件2) {
    // 执行语句2
} else if (条件3) {
    // 执行语句3
} else {
    // 所有条件都不满足时执行
}
```

#### 实际应用示例

```javascript
// 成绩等级判断
function getGrade(score) {
    if (score >= 90) {
        return 'A';
    } else if (score >= 80) {
        return 'B';
    } else if (score >= 70) {
        return 'C';
    } else if (score >= 60) {
        return 'D';
    } else {
        return 'F';
    }
}

// 复杂条件判断
function checkUserAccess(user) {
    if (user.isLoggedIn) {
        if (user.role === 'admin') {
            if (user.permissions.includes('manage_users')) {
                return 'full_access';
            } else {
                return 'limited_admin_access';
            }
        } else {
            return 'user_access';
        }
    } else {
        return 'no_access';
    }
}
```

#### 最佳实践

1. **避免深层嵌套**：使用早期返回减少嵌套层级

```javascript
// 不推荐的深层嵌套
function processData(data) {
    if (data) {
        if (data.isValid) {
            if (data.items.length > 0) {
                // 处理数据
                return processItems(data.items);
            }
        }
    }
    return null;
}

// 推荐的早期返回
function processData(data) {
    if (!data || !data.isValid || data.items.length === 0) {
        return null;
    }
    return processItems(data.items);
}
```

### switch 语句的匹配机制

#### 基本语法

```javascript
switch (表达式) {
    case 值1:
        // 执行语句1
        break;
    case 值2:
        // 执行语句2
        break;
    case 值3:
    case 值4:
        // 值3或值4时执行
        break;
    default:
        // 默认执行语句
}
```

#### 匹配机制详解

```javascript
// 基本匹配
function getDayName(dayNumber) {
    switch (dayNumber) {
        case 1:
            return 'Monday';
        case 2:
            return 'Tuesday';
        case 3:
            return 'Wednesday';
        case 4:
            return 'Thursday';
        case 5:
            return 'Friday';
        case 6:
            return 'Saturday';
        case 7:
            return 'Sunday';
        default:
            return 'Invalid day';
    }
}

// 贯穿执行（fall-through）
function getSeason(month) {
    switch (month) {
        case 12:
        case 1:
        case 2:
            return 'Winter';
        case 3:
        case 4:
        case 5:
            return 'Spring';
        case 6:
        case 7:
        case 8:
            return 'Summer';
        case 9:
        case 10:
        case 11:
            return 'Autumn';
        default:
            return 'Invalid month';
    }
}
```

#### 高级用法

```javascript
// 使用表达式
function calculate(operation, a, b) {
    switch (operation) {
        case 'add':
            return a + b;
        case 'subtract':
            return a - b;
        case 'multiply':
            return a * b;
        case 'divide':
            return b !== 0 ? a / b : 'Cannot divide by zero';
        default:
            return 'Invalid operation';
    }
}

// 使用对象替代switch（更现代的方式）
const operations = {
    add: (a, b) => a + b,
    subtract: (a, b) => a - b,
    multiply: (a, b) => a * b,
    divide: (a, b) => b !== 0 ? a / b : 'Cannot divide by zero'
};

function calculateModern(operation, a, b) {
    return operations[operation] ? operations[operation](a, b) : 'Invalid operation';
}
```

### 三元运算符的应用场景

#### 基本语法

```javascript
条件 ? 值1 : 值2
```

#### 简单应用

```javascript
// 基本用法
const isAdult = age >= 18 ? true : false;
const message = isLoggedIn ? 'Welcome back!' : 'Please log in';

// 在函数中使用
function getStatus(isActive) {
    return isActive ? 'Active' : 'Inactive';
}

// 在JSX中的应用（React）
const UserComponent = ({ isLoggedIn }) => (
    <div>
        {isLoggedIn ? <Dashboard /> : <Login />}
    </div>
);
```

#### 复杂应用

```javascript
// 嵌套三元运算符
const userStatus = user.isLoggedIn 
    ? user.isPremium 
        ? 'Premium User' 
        : 'Regular User' 
    : 'Guest';

// 在数组操作中的应用
const numbers = [1, 2, 3, 4, 5];
const processedNumbers = numbers.map(num => 
    num % 2 === 0 ? num * 2 : num * 3
);

// 条件赋值
const theme = userPreference || (systemPreference === 'dark' ? 'dark' : 'light');
```

#### 注意事项

```javascript
// 避免过度嵌套
// 不推荐
const result = condition1 
    ? (condition2 ? (condition3 ? 'deep' : 'nested') : 'complex') 
    : 'structure';

// 推荐使用if...else
if (condition1) {
    if (condition2) {
        if (condition3) {
            return 'deep';
        } else {
            return 'nested';
        }
    } else {
        return 'complex';
    }
} else {
    return 'structure';
}
```

### 条件表达式的最佳实践

#### 1. 真值检查

```javascript
// 推荐的真值检查方式
function isValid(value) {
    // 检查null、undefined、空字符串、0、false、NaN
    return !!value;
}

// 检查数组是否为空
function hasItems(array) {
    return Array.isArray(array) && array.length > 0;
}

// 检查对象是否为空
function hasProperties(obj) {
    return obj && typeof obj === 'object' && Object.keys(obj).length > 0;
}
```

#### 2. 类型安全比较

```javascript
// 严格相等比较
if (value === true) { /* ... */ }
if (count === 0) { /* ... */ }
if (name === '') { /* ... */ }

// 避免隐式类型转换
// 不推荐
if (value == 1) { /* 可能匹配 "1", true 等 */ }

// 推荐
if (value === 1) { /* 只匹配数字1 */ }
```

#### 3. 组合条件

```javascript
// 使用逻辑运算符
const canAccess = user.isLoggedIn && user.hasPermission && !user.isBlocked;

// 复杂条件的可读性
const isValidUser = user.isLoggedIn 
    && user.emailVerified 
    && user.accountActive 
    && user.subscriptionValid;

// 提取复杂条件为变量
const meetsAgeRequirement = user.age >= 18;
const hasValidId = user.idCard && user.idCard.isValid;
const isVerified = user.emailVerified && user.phoneVerified;

if (meetsAgeRequirement && hasValidId && isVerified) {
    // 处理验证通过的用户
}
```

## 3.2 循环控制语句

### for 循环的各种变体

#### 传统for循环

```javascript
// 基本语法
for (初始化; 条件; 迭代) {
    // 循环体
}

// 实际应用
for (let i = 0; i < 10; i++) {
    console.log(i);
}

// 数组遍历
const items = ['apple', 'banana', 'orange'];
for (let i = 0; i < items.length; i++) {
    console.log(`${i}: ${items[i]}`);
}
```

#### 倒序循环

```javascript
// 倒序遍历数组
for (let i = items.length - 1; i >= 0; i--) {
    console.log(items[i]);
}

// 倒序计数
for (let i = 10; i > 0; i--) {
    console.log(i);
}
```

#### 步长控制

```javascript
// 每次增加2
for (let i = 0; i < 20; i += 2) {
    console.log(i); // 0, 2, 4, 6, 8, 10, 12, 14, 16, 18
}

// 每次减少3
for (let i = 30; i > 0; i -= 3) {
    console.log(i); // 30, 27, 24, 21, 18, 15, 12, 9, 6, 3
}
```

### while 和 do...while 循环

#### while循环

```javascript
// 基本语法
while (条件) {
    // 循环体
    // 必须有改变条件的语句
}

// 实际应用
let count = 0;
while (count < 5) {
    console.log(count);
    count++;
}

// 用户输入验证
let userInput;
while (!userInput || userInput.trim() === '') {
    userInput = prompt('请输入有效内容:');
}
```

#### do...while循环

```javascript
// 基本语法
do {
    // 循环体
    // 至少执行一次
} while (条件);

// 实际应用
let password;
do {
    password = prompt('请输入密码:');
} while (password !== 'secret123');

// 菜单系统
let choice;
do {
    choice = prompt('选择操作: 1-添加 2-删除 3-退出');
    switch (choice) {
        case '1':
            addItem();
            break;
        case '2':
            removeItem();
            break;
        case '3':
            console.log('退出程序');
            break;
        default:
            console.log('无效选择');
    }
} while (choice !== '3');
```

#### 两种循环的区别

```javascript
// while循环 - 条件先判断
let i = 5;
while (i < 3) {
    console.log('这不会执行'); // 条件一开始就不满足
    i++;
}

// do...while循环 - 至少执行一次
let j = 5;
do {
    console.log('这会执行一次'); // 先执行，再判断条件
    j++;
} while (j < 3);
```

### for...in 和 for...of 循环的区别

#### for...in 循环

```javascript
// 用于遍历对象的可枚举属性
const person = {
    name: 'Alice',
    age: 30,
    city: 'New York'
};

for (let key in person) {
    console.log(`${key}: ${person[key]}`);
}
// 输出: name: Alice, age: 30, city: New York

// 遍历数组（不推荐）
const colors = ['red', 'green', 'blue'];
for (let index in colors) {
    console.log(`${index}: ${colors[index]}`);
}
// 输出: 0: red, 1: green, 2: blue
```

#### for...of 循环

```javascript
// 用于遍历可迭代对象（数组、字符串、Map、Set等）
const fruits = ['apple', 'banana', 'orange'];

// 遍历数组元素
for (let fruit of fruits) {
    console.log(fruit);
}
// 输出: apple, banana, orange

// 遍历字符串
const message = 'Hello';
for (let char of message) {
    console.log(char);
}
// 输出: H, e, l, l, o

// 遍历Set
const uniqueNumbers = new Set([1, 2, 3, 4]);
for (let num of uniqueNumbers) {
    console.log(num);
}

// 遍历Map
const userRoles = new Map([
    ['alice', 'admin'],
    ['bob', 'user'],
    ['charlie', 'moderator']
]);

for (let [user, role] of userRoles) {
    console.log(`${user}: ${role}`);
}
```

#### 关键区别对比

```javascript
const arr = [10, 20, 30];
arr.customProperty = 'test'; // 添加自定义属性

// for...in 遍历所有可枚举属性（包括自定义属性）
for (let key in arr) {
    console.log(key, arr[key]);
}
// 输出: 0 10, 1 20, 2 30, customProperty test

// for...of 只遍历值
for (let value of arr) {
    console.log(value);
}
// 输出: 10, 20, 30
```

### 循环控制语句 break 和 continue

#### break语句

```javascript
// 基本用法 - 跳出循环
for (let i = 0; i < 10; i++) {
    if (i === 5) {
        break; // 当i等于5时跳出循环
    }
    console.log(i);
}
// 输出: 0, 1, 2, 3, 4

// 在嵌套循环中使用
outer: for (let i = 0; i < 3; i++) {
    for (let j = 0; j < 3; j++) {
        if (i === 1 && j === 1) {
            break outer; // 跳出外层循环
        }
        console.log(`i: ${i}, j: ${j}`);
    }
}
// 输出: i: 0, j: 0; i: 0, j: 1; i: 0, j: 2; i: 1, j: 0
```

#### continue语句

```javascript
// 基本用法 - 跳过当前迭代
for (let i = 0; i < 10; i++) {
    if (i % 2 === 0) {
        continue; // 跳过偶数
    }
    console.log(i);
}
// 输出: 1, 3, 5, 7, 9

// 在while循环中使用
let count = 0;
while (count < 10) {
    count++;
    if (count % 3 === 0) {
        continue; // 跳过3的倍数
    }
    console.log(count);
}
// 输出: 1, 2, 4, 5, 7, 8, 10
```

#### 实际应用场景

```javascript
// 查找特定元素
function findUser(users, targetId) {
    for (let user of users) {
        if (user.id === targetId) {
            return user;
        }
    }
    return null;
}

// 数据过滤和处理
function processNumbers(numbers) {
    const result = [];
    for (let num of numbers) {
        if (num < 0) {
            continue; // 跳过负数
        }
        if (num > 100) {
            break; // 遇到大于100的数就停止
        }
        result.push(num * 2);
    }
    return result;
}

// 错误处理
function validateData(dataList) {
    const errors = [];
    for (let data of dataList) {
        if (!data.requiredField) {
            errors.push('Missing required field');
            continue;
        }
        if (data.value < 0) {
            errors.push('Negative value not allowed');
            continue;
        }
        // 处理有效数据
        processData(data);
    }
    return errors;
}
```

### 循环性能优化建议

#### 1. 缓存数组长度

```javascript
// 不推荐
for (let i = 0; i < array.length; i++) {
    // 每次都计算array.length
}

// 推荐
for (let i = 0, len = array.length; i < len; i++) {
    // 只计算一次长度
}
```

#### 2. 选择合适的循环方式

```javascript
const numbers = [1, 2, 3, 4, 5];

// 对于简单遍历，for...of通常最快
for (let num of numbers) {
    console.log(num);
}

// 对于需要索引的情况，传统for循环
for (let i = 0; i < numbers.length; i++) {
    console.log(`${i}: ${numbers[i]}`);
}

// 对于函数式编程，使用数组方法
numbers.forEach(num => console.log(num));
```

# 四、函数编程概念

## 4.1 函数定义和调用

### 函数声明和函数表达式的区别

#### 函数声明（Function Declaration）

```javascript
// 函数声明
function greet(name) {
    return `Hello, ${name}!`;
}

// 函数声明具有提升（hoisting）特性
console.log(greet("Alice")); // 正常工作，输出: Hello, Alice!

function greet(name) {
    return `Hello, ${name}!`;
}
```

#### 函数表达式（Function Expression）

```javascript
// 函数表达式
const greet = function(name) {
    return `Hello, ${name}!`;
};

// 函数表达式没有提升
console.log(greet("Bob")); // TypeError: Cannot access 'greet' before initialization

const greet = function(name) {
    return `Hello, ${name}!`;
};

// 命名函数表达式
const factorial = function fact(n) {
    if (n <= 1) return 1;
    return n * fact(n - 1); // 可以在函数内部调用自身
};

console.log(factorial(5)); // 120
console.log(fact(5)); // ReferenceError: fact is not defined
```

#### 主要区别对比

```javascript
// 1. 提升行为
// 函数声明会被完全提升
console.log(declaredFunction()); // "I'm declared"

function declaredFunction() {
    return "I'm declared";
}

// 函数表达式只有变量被提升，值为undefined
console.log(expressFunction); // undefined
console.log(expressFunction()); // TypeError: expressFunction is not a function

var expressFunction = function() {
    return "I'm expressed";
};

// 2. 调试友好性
// 函数声明在调试器中显示函数名
function debugFunction() {
    console.trace(); // 显示 "debugFunction"
}

// 匿名函数表达式显示为 "anonymous"
const debugExpression = function() {
    console.trace(); // 显示 "anonymous"
};
```

### 箭头函数的特性和限制

#### 基本语法

```javascript
// 基本箭头函数
const add = (a, b) => a + b;

// 单参数可以省略括号
const square = x => x * x;

// 多参数需要括号
const multiply = (a, b) => a * b;

// 无参数需要空括号
const getRandom = () => Math.random();

// 函数体多行需要大括号和return
const complexCalculation = (x, y) => {
    const result = x * y + x - y;
    return result > 0 ? result : 0;
};

// 返回对象字面量需要括号
const createUser = (name, age) => ({
    name: name,
    age: age,
    id: Math.random()
});
```

#### 箭头函数的关键特性

##### 1. this绑定

```javascript
// 普通函数 - this取决于调用方式
const person = {
    name: 'Alice',
    greet: function() {
        console.log(`Hello, I'm ${this.name}`);
        
        // 普通函数中的this指向全局对象
        setTimeout(function() {
            console.log(`Delayed greeting from ${this.name}`); // undefined
        }, 1000);
    }
};

// 箭头函数 - this继承自外层作用域
const person2 = {
    name: 'Bob',
    greet: function() {
        console.log(`Hello, I'm ${this.name}`);
        
        // 箭头函数中的this指向person2对象
        setTimeout(() => {
            console.log(`Delayed greeting from ${this.name}`); // Bob
        }, 1000);
    }
};

person.greet();
person2.greet();
```

##### 2. 不能用作构造函数

```javascript
// 普通函数可以作为构造函数
function Person(name) {
    this.name = name;
}

const alice = new Person('Alice');
console.log(alice.name); // Alice

// 箭头函数不能作为构造函数
const ArrowPerson = (name) => {
    this.name = name;
};

// const bob = new ArrowPerson('Bob'); // TypeError: ArrowPerson is not a constructor
```

##### 3. 没有arguments对象

```javascript
// 普通函数有arguments对象
function normalFunction() {
    console.log(arguments); // Arguments对象
    return Array.from(arguments).reduce((sum, num) => sum + num, 0);
}

console.log(normalFunction(1, 2, 3, 4)); // 10

// 箭头函数没有arguments，使用剩余参数
const arrowFunction = (...args) => {
    console.log(args); // 数组
    return args.reduce((sum, num) => sum + num, 0);
};

console.log(arrowFunction(1, 2, 3, 4)); // 10
```

#### 箭头函数的限制

```javascript
// 1. 不能使用yield（不能作为生成器函数）
// const generator = *() => {}; // SyntaxError

// 2. 不能使用await（除非在async箭头函数中）
// const asyncFn = () => await fetch('/api'); // SyntaxError

// 3. 不能绑定this、arguments、super或new.target
const obj = {
    method: () => {
        // this不指向obj
        console.log(this); // 全局对象或undefined（严格模式）
    }
};
```

### 立即执行函数表达式（IIFE）

#### 基本语法

```javascript
// 基本形式1：函数表达式后立即调用
(function() {
    console.log('IIFE executed');
})();

// 基本形式2：使用箭头函数
(() => {
    console.log('Arrow IIFE executed');
})();

// 带参数的IIFE
(function(name, age) {
    console.log(`Hello, ${name}! You are ${age} years old.`);
})('Alice', 25);

// 返回值的IIFE
const result = (function(a, b) {
    return a + b;
})(3, 4);
console.log(result); // 7
```

#### 实际应用场景

##### 1. 创建私有作用域

```javascript
// 避免全局变量污染
(function() {
    const privateVariable = 'This is private';
    const privateFunction = function() {
        return 'Private function result';
    };
    
    // 暴露公共接口
    window.MyModule = {
        publicMethod: function() {
            return privateFunction() + ' - ' + privateVariable;
        }
    };
})();

console.log(MyModule.publicMethod()); // Private function result - This is private
// console.log(privateVariable); // ReferenceError: privateVariable is not defined
```

##### 2. 模块模式

```javascript
const Calculator = (function() {
    let result = 0;
    
    return {
        add: function(x) {
            result += x;
            return this;
        },
        subtract: function(x) {
            result -= x;
            return this;
        },
        multiply: function(x) {
            result *= x;
            return this;
        },
        getResult: function() {
            return result;
        },
        reset: function() {
            result = 0;
            return this;
        }
    };
})();

// 链式调用
const finalResult = Calculator.add(10).subtract(3).multiply(2).getResult();
console.log(finalResult); // 14
```

##### 3. 避免闭包问题

```javascript
// 问题代码：所有回调函数都引用同一个i
for (var i = 0; i < 3; i++) {
    setTimeout(function() {
        console.log(i); // 输出: 3, 3, 3
    }, 100);
}

// 使用IIFE解决闭包问题
for (var i = 0; i < 3; i++) {
    (function(index) {
        setTimeout(function() {
            console.log(index); // 输出: 0, 1, 2
        }, 100);
    })(i);
}

// 现代解决方案：使用let
for (let i = 0; i < 3; i++) {
    setTimeout(function() {
        console.log(i); // 输出: 0, 1, 2
    }, 100);
}
```

### 高阶函数的概念和应用

#### 高阶函数定义

高阶函数是满足以下条件之一的函数：

1. 接受一个或多个函数作为参数
2. 返回一个函数作为结果

#### 接受函数作为参数

```javascript
// 数组方法都是高阶函数
const numbers = [1, 2, 3, 4, 5];

// map接受函数作为参数
const doubled = numbers.map(x => x * 2);
console.log(doubled); // [2, 4, 6, 8, 10]

// filter接受函数作为参数
const evens = numbers.filter(x => x % 2 === 0);
console.log(evens); // [2, 4]

// reduce接受函数作为参数
const sum = numbers.reduce((acc, x) => acc + x, 0);
console.log(sum); // 15

// 自定义高阶函数
function createValidator(validatorFn, errorMessage) {
    return function(value) {
        if (!validatorFn(value)) {
            throw new Error(errorMessage);
        }
        return true;
    };
}

const emailValidator = createValidator(
    email => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email),
    'Invalid email format'
);

const minLengthValidator = createValidator(
    value => value.length >= 6,
    'Value must be at least 6 characters long'
);

try {
    emailValidator('test@example.com'); // 验证通过
    minLengthValidator('password123'); // 验证通过
} catch (error) {
    console.log(error.message);
}
```

#### 返回函数作为结果

```javascript
// 创建特定功能的函数
function createMultiplier(multiplier) {
    return function(number) {
        return number * multiplier;
    };
}

const double = createMultiplier(2);
const triple = createMultiplier(3);

console.log(double(5)); // 10
console.log(triple(4)); // 12

// 创建配置化的函数
function createGreeter(greeting) {
    return function(name) {
        return `${greeting}, ${name}!`;
    };
}

const sayHello = createGreeter('Hello');
const sayHi = createGreeter('Hi');

console.log(sayHello('Alice')); // Hello, Alice!
console.log(sayHi('Bob')); // Hi, Bob!
```

#### 实际应用示例

##### 1. 函数组合

```javascript
// 函数组合工具
function compose(...functions) {
    return function(value) {
        return functions.reduceRight((acc, fn) => fn(acc), value);
    };
}

const addOne = x => x + 1;
const double = x => x * 2;
const square = x => x * x;

const addOneThenDoubleThenSquare = compose(square, double, addOne);
console.log(addOneThenDoubleThenSquare(3)); // ((3+1)*2)^2 = 64
```

##### 2. 函数柯里化

```javascript
// 柯里化函数
function curry(fn) {
    return function curried(...args) {
        if (args.length >= fn.length) {
            return fn.apply(this, args);
        }
        return function(...nextArgs) {
            return curried(...args, ...nextArgs);
        };
    };
}

function add(a, b, c) {
    return a + b + c;
}

const curriedAdd = curry(add);
console.log(curriedAdd(1)(2)(3)); // 6
console.log(curriedAdd(1, 2)(3)); // 6
console.log(curriedAdd(1)(2, 3)); // 6
```

##### 3. 装饰器模式

```javascript
// 日志装饰器
function withLogging(fn) {
    return function(...args) {
        console.log(`Calling ${fn.name} with arguments:`, args);
        const result = fn.apply(this, args);
        console.log(`${fn.name} returned:`, result);
        return result;
    };
}

function calculate(a, b) {
    return a * b + a - b;
}

const loggedCalculate = withLogging(calculate);
loggedCalculate(5, 3);
// 输出:
// Calling calculate with arguments: [5, 3]
// calculate returned: 17
```

## 4.2 函数参数处理

### 参数传递机制

#### 值传递 vs 引用传递

```javascript
// 基本类型 - 值传递
function modifyPrimitive(value) {
    value = value * 2;
    console.log('Inside function:', value); // 20
}

let num = 10;
modifyPrimitive(num);
console.log('Outside function:', num); // 10 (未改变)

// 对象类型 - 引用传递（传递引用的副本）
function modifyObject(obj) {
    obj.name = 'Modified';
    obj.newProperty = 'Added';
    console.log('Inside function:', obj); // { name: 'Modified', age: 25, newProperty: 'Added' }
}

let person = { name: 'Alice', age: 25 };
modifyObject(person);
console.log('Outside function:', person); // { name: 'Modified', age: 25, newProperty: 'Added' }

// 重新赋值对象引用不会影响原对象
function reassignObject(obj) {
    obj = { completely: 'new object' };
    console.log('Inside function:', obj); // { completely: 'new object' }
}

let originalObj = { name: 'Original' };
reassignObject(originalObj);
console.log('Outside function:', originalObj); // { name: 'Original' }
```

#### 深拷贝 vs 浅拷贝

```javascript
// 浅拷贝示例
function shallowModify(obj) {
    obj.name = 'Modified';
    obj.address.city = 'Modified City'; // 嵌套对象会被修改
}

const user = {
    name: 'Alice',
    address: {
        city: 'New York',
        country: 'USA'
    }
};

shallowModify(user);
console.log(user); // { name: 'Modified', address: { city: 'Modified City', country: 'USA' } }

// 深拷贝示例
function deepModify(originalObj) {
    // 简单深拷贝（实际项目中建议使用lodash.cloneDeep等库）
    const obj = JSON.parse(JSON.stringify(originalObj));
    obj.name = 'Modified';
    obj.address.city = 'Modified City';
    return obj;
}

const user2 = {
    name: 'Bob',
    address: {
        city: 'London',
        country: 'UK'
    }
};

const modifiedUser = deepModify(user2);
console.log(user2); // 原对象未改变
console.log(modifiedUser); // 修改后的对象
```

### 默认参数设置

#### ES6默认参数

```javascript
// 基本默认参数
function greet(name = 'Guest', greeting = 'Hello') {
    return `${greeting}, ${name}!`;
}

console.log(greet()); // Hello, Guest!
console.log(greet('Alice')); // Hello, Alice!
console.log(greet('Bob', 'Hi')); // Hi, Bob!

// 复杂默认值
function createUser(name, options = {}) {
    const defaults = {
        age: 18,
        active: true,
        role: 'user'
    };
    
    const config = { ...defaults, ...options };
    
    return {
        name,
        ...config
    };
}

console.log(createUser('Alice'));
// { name: 'Alice', age: 18, active: true, role: 'user' }

console.log(createUser('Bob', { age: 25, role: 'admin' }));
// { name: 'Bob', age: 25, active: true, role: 'admin' }
```

#### 默认参数表达式

```javascript
// 默认参数可以是表达式
function generateId(prefix = 'user_' + Date.now()) {
    return prefix + Math.random().toString(36).substr(2, 9);
}

console.log(generateId()); // user_1640995200000 + random
console.log(generateId('admin_')); // admin_ + random

// 默认参数可以引用前面的参数
function calculateTax(amount, taxRate = amount * 0.1) {
    return amount + taxRate;
}

console.log(calculateTax(100)); // 110 (默认税率10%)
console.log(calculateTax(100, 15)); // 115 (指定税率15)
```

#### 与arguments对象的关系

```javascript
// ES6默认参数不会影响arguments对象
function testDefaults(a = 1, b = 2) {
    console.log('Parameters:', a, b);
    console.log('Arguments length:', arguments.length);
    console.log('Arguments:', arguments);
}

testDefaults(); // Parameters: 1 2, Arguments length: 0, Arguments: []
testDefaults(5); // Parameters: 5 2, Arguments length: 1, Arguments: [5]
```

### 剩余参数和扩展运算符

#### 剩余参数（Rest Parameters）

```javascript
// 基本语法
function sum(...numbers) {
    return numbers.reduce((total, num) => total + num, 0);
}

console.log(sum(1, 2, 3, 4, 5)); // 15
console.log(sum()); // 0

// 与其他参数结合使用
function introduce(greeting, ...names) {
    return `${greeting} ${names.join(', ')}!`;
}

console.log(introduce('Hello', 'Alice', 'Bob', 'Charlie'));
// Hello Alice, Bob, Charlie!

// 剩余参数必须是最后一个参数
// function invalid(a, ...rest, b) {} // SyntaxError

// 剩余参数与数组方法结合
function findMax(...numbers) {
    return Math.max(...numbers);
}

console.log(findMax(1, 5, 3, 9, 2)); // 9
```

#### 扩展运算符（Spread Operator）

```javascript
// 数组扩展
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const combined = [...arr1, ...arr2, 7, 8];
console.log(combined); // [1, 2, 3, 4, 5, 6, 7, 8]

// 数组复制
const original = [1, 2, 3];
const copy = [...original];
copy.push(4);
console.log(original); // [1, 2, 3] (未改变)
console.log(copy); // [1, 2, 3, 4]

// 字符串扩展
const str = 'hello';
const chars = [...str];
console.log(chars); // ['h', 'e', 'l', 'l', 'o']

// 对象扩展
const obj1 = { a: 1, b: 2 };
const obj2 = { c: 3, d: 4 };
const merged = { ...obj1, ...obj2, e: 5 };
console.log(merged); // { a: 1, b: 2, c: 3, d: 4, e: 5 }

// 对象复制和更新
const user = { name: 'Alice', age: 25 };
const updatedUser = { ...user, age: 26, city: 'New York' };
console.log(updatedUser); // { name: 'Alice', age: 26, city: 'New York' }
```

#### 实际应用场景

```javascript
// 函数重载模拟
function formatMessage(template, ...values) {
    return template.replace(/{(\d+)}/g, (match, index) => {
        return values[index] !== undefined ? values[index] : match;
    });
}

console.log(formatMessage('Hello {0}, you have {1} messages', 'Alice', 5));
// Hello Alice, you have 5 messages

// 数组去重
function uniqueArray(...items) {
    return [...new Set(items)];
}

console.log(uniqueArray(1, 2, 2, 3, 3, 4)); // [1, 2, 3, 4]

// 数学运算
function calculate(operation, ...numbers) {
    switch (operation) {
        case 'sum':
            return numbers.reduce((a, b) => a + b, 0);
        case 'product':
            return numbers.reduce((a, b) => a * b, 1);
        case 'max':
            return Math.max(...numbers);
        case 'min':
            return Math.min(...numbers);
        default:
            throw new Error('Unknown operation');
    }
}

console.log(calculate('sum', 1, 2, 3, 4)); // 10
console.log(calculate('max', 5, 2, 8, 1)); // 8
```

### arguments 对象的使用

#### arguments对象特性

```javascript
// arguments对象是类数组对象
function showArguments() {
    console.log('Arguments object:', arguments);
    console.log('Length:', arguments.length);
    console.log('First argument:', arguments[0]);
    
    // 转换为真正的数组
    const argsArray = Array.from(arguments);
    // 或者使用扩展运算符
    const argsArray2 = [...arguments];
    // 或者使用slice
    const argsArray3 = Array.prototype.slice.call(arguments);
    
    return argsArray;
}

showArguments('a', 'b', 'c');
// Arguments object: Arguments(3) ['a', 'b', 'c']
// Length: 3
// First argument: a
```

#### 与剩余参数的区别

```javascript
// arguments对象（ES5方式）
function oldStyle() {
    console.log('Arguments length:', arguments.length);
    for (let i = 0; i < arguments.length; i++) {
        console.log(`Argument ${i}:`, arguments[i]);
    }
}

// 剩余参数（ES6方式）
function newStyle(...args) {
    console.log('Args length:', args.length);
    args.forEach((arg, index) => {
        console.log(`Arg ${index}:`, arg);
    });
}

oldStyle(1, 2, 3);
newStyle(1, 2, 3);
```

#### 实际应用

```javascript
// 函数代理
function createProxy(targetFunction) {
    return function() {
        console.log('Before calling target function');
        const result = targetFunction.apply(this, arguments);
        console.log('After calling target function');
        return result;
    };
}

function originalFunction(a, b) {
    return a + b;
}

const proxiedFunction = createProxy(originalFunction);
console.log(proxiedFunction(3, 4)); // 7

// 参数验证
function validateArguments(...validators) {
    return function(targetFunction) {
        return function() {
            for (let i = 0; i < validators.length; i++) {
                if (i < arguments.length && !validators[i](arguments[i])) {
                    throw new Error(`Argument ${i} failed validation`);
                }
            }
            return targetFunction.apply(this, arguments);
        };
    };
}

const numberValidator = value => typeof value === 'number';
const stringValidator = value => typeof value === 'string';

const validatedFunction = validateArguments(numberValidator, stringValidator)(
    function processData(num, str) {
        return `${str}: ${num}`;
    }
);

console.log(validatedFunction(42, 'Answer')); // Answer: 42
// validatedFunction('not a number', 'test'); // Error: Argument 0 failed validation
```

## 4.3 作用域和闭包

### 词法作用域原理

#### 作用域链

```javascript
// 全局作用域
const globalVar = 'I am global';

function outerFunction() {
    // outerFunction的作用域
    const outerVar = 'I am outer';
    
    function innerFunction() {
        // innerFunction的作用域
        const innerVar = 'I am inner';
        
        // 可以访问所有外层作用域的变量
        console.log(globalVar); // I am global
        console.log(outerVar);   // I am outer
        console.log(innerVar);   // I am inner
    }
    
    innerFunction();
    
    // 不能访问内层作用域的变量
    // console.log(innerVar); // ReferenceError
}

outerFunction();

// 不能访问函数内部的变量
// console.log(outerVar); // ReferenceError
```

#### 作用域查找规则

```javascript
const x = 1;

function function1() {
    const x = 2;
    
    function function2() {
        const x = 3;
        
        function function3() {
            // 从最近的作用域开始查找
            console.log(x); // 3 (function3作用域)
        }
        
        function3();
    }
    
    function2();
}

function1();

// 变量遮蔽
const name = 'Global';

function showName() {
    const name = 'Local';
    console.log(name); // Local (局部变量遮蔽全局变量)
}

showName();
console.log(name); // Global
```

#### 块级作用域

```javascript
// var没有块级作用域
if (true) {
    var blockVar = 'I am not block scoped';
}
console.log(blockVar); // I am not block scoped

// let和const有块级作用域
if (true) {
    let blockLet = 'I am block scoped';
    const blockConst = 'I am also block scoped';
    console.log(blockLet); // I am block scoped
    console.log(blockConst); // I am also block scoped
}
// console.log(blockLet); // ReferenceError
// console.log(blockConst); // ReferenceError

// 循环中的块级作用域
for (let i = 0; i < 3; i++) {
    setTimeout(() => {
        console.log(i); // 0, 1, 2 (每次循环都有独立的i)
    }, 100);
}

// 使用var会有问题
for (var j = 0; j < 3; j++) {
    setTimeout(() => {
        console.log(j); // 3, 3, 3 (所有回调共享同一个j)
    }, 100);
}
```

### 闭包的形成和应用

#### 闭包基本概念

```javascript
// 闭包：内部函数可以访问外部函数的变量
function outerFunction(outerVariable) {
    return function innerFunction(innerVariable) {
        console.log('Outer:', outerVariable);
        console.log('Inner:', innerVariable);
    };
}

const closure = outerFunction('outside');
closure('inside');
// Outer: outside
// Inner: inside

// 闭包保持对外部变量的引用
function createCounter() {
    let count = 0;
    
    return function() {
        count++;
        return count;
    };
}

const counter1 = createCounter();
const counter2 = createCounter();

console.log(counter1()); // 1
console.log(counter1()); // 2
console.log(counter2()); // 1 (独立的闭包环境)
console.log(counter1()); // 3
```

#### 闭包的实际应用

##### 1. 数据私有化

```javascript
function createBankAccount(initialBalance) {
    let balance = initialBalance;
    
    return {
        deposit: function(amount) {
            if (amount > 0) {
                balance += amount;
                return balance;
            }
            throw new Error('Deposit amount must be positive');
        },
        withdraw: function(amount) {
            if (amount > 0 && amount <= balance) {
                balance -= amount;
                return balance;
            }
            throw new Error('Invalid withdrawal amount');
        },
        getBalance: function() {
            return balance;
        }
    };
}

const account = createBankAccount(1000);
console.log(account.deposit(500)); // 1500
console.log(account.withdraw(200)); // 1300
console.log(account.getBalance()); // 1300
// console.log(account.balance); // undefined (私有变量)
```

##### 2. 函数工厂

```javascript
function createValidator(type) {
    switch (type) {
        case 'email':
            return function(value) {
                return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(value);
            };
        case 'phone':
            return function(value) {
                return /^\d{10,11}$/.test(value.replace(/[-\s]/g, ''));
            };
        case 'password':
            return function(value) {
                return value.length >= 8 && /[A-Z]/.test(value) && /[0-9]/.test(value);
            };
        default:
            return function() {
                return true;
            };
    }
}

const emailValidator = createValidator('email');
const phoneValidator = createValidator('phone');

console.log(emailValidator('test@example.com')); // true
console.log(phoneValidator('123-456-7890')); // true
```

##### 3. 事件处理

```javascript
// 为多个元素添加事件监听器
function attachListeners() {
    const buttons = document.querySelectorAll('.button');
    
    buttons.forEach((button, index) => {
        // 闭包保存每个按钮的索引
        button.addEventListener('click', function() {
            console.log(`Button ${index} clicked`);
        });
    });
}

// 防抖函数
function debounce(func, delay) {
    let timeoutId;
    
    return function(...args) {
        // 清除之前的定时器
        clearTimeout(timeoutId);
        // 设置新的定时器
        timeoutId = setTimeout(() => func.apply(this, args), delay);
    };
}

const debouncedSearch = debounce(function(query) {
    console.log('Searching for:', query);
}, 300);
```

##### 4. 柯里化和偏函数应用

```javascript
// 柯里化函数利用闭包保存参数
function curry(fn) {
    return function curried(...args) {
        if (args.length >= fn.length) {
            return fn.apply(this, args);
        }
        return function(...nextArgs) {
            return curried(...args, ...nextArgs);
        };
    };
}

function multiply(a, b, c) {
    return a * b * c;
}

const curriedMultiply = curry(multiply);
console.log(curriedMultiply(2)(3)(4)); // 24
console.log(curriedMultiply(2, 3)(4)); // 24

// 偏函数应用
function partial(fn, ...fixedArgs) {
    return function(...remainingArgs) {
        const args = [...fixedArgs];
        let argIndex = 0;
        
        for (let i = 0; i < args.length; i++) {
            if (args[i] === undefined) {
                args[i] = remainingArgs[argIndex++];
            }
        }
        
        return fn.apply(this, args);
    };
}

function greet(greeting, name, punctuation) {
    return `${greeting}, ${name}${punctuation}`;
}

const sayHello = partial(greet, 'Hello', undefined, '!');
console.log(sayHello('Alice')); // Hello, Alice!
```

### 内存泄漏风险和防范

#### 常见内存泄漏场景

##### 1. 意外的全局变量

```javascript
// 错误示例
function leakingFunction() {
    // 忘记使用var/let/const
    globalVar = 'This becomes a global variable';
}

// 正确示例
function nonLeakingFunction() {
    const localVar = 'This stays local';
}
```

##### 2. 被遗忘的定时器

```javascript
// 可能导致内存泄漏
function startTimer() {
    const largeData = new Array(1000000).fill('data');
    
    setInterval(() => {
        console.log(largeData[0]); // 保持对largeData的引用
    }, 1000);
}

// 改进版本
function startTimerImproved() {
    const largeData = new Array(1000000).fill('data');
    let timerId;
    
    timerId = setInterval(() => {
        console.log(largeData[0]);
    }, 1000);
    
    // 提供清理方法
    return function cleanup() {
        clearInterval(timerId);
    };
}

const cleanup = startTimerImproved();
// 在适当时候调用cleanup()
```

##### 3. 闭包中的循环引用

```javascript
// 可能导致内存泄漏
function createCircularReference() {
    const obj = {};
    obj.self = obj; // 循环引用
    
    return function() {
        return obj;
    };
}

// DOM事件监听器泄漏
function attachEventListeners() {
    const button = document.getElementById('myButton');
    
    // 每次调用都会添加新的监听器
    button.addEventListener('click', function() {
        console.log('Button clicked');
    });
}

// 改进版本
function attachEventListenersImproved() {
    const button = document.getElementById('myButton');
    const handler = function() {
        console.log('Button clicked');
    };
    
    // 移除旧的监听器
    button.removeEventListener('click', handler);
    // 添加新的监听器
    button.addEventListener('click', handler);
    
    // 返回清理函数
    return function cleanup() {
        button.removeEventListener('click', handler);
    };
}
```

#### 内存泄漏防范策略

##### 1. 及时清理资源

```javascript
// 使用WeakMap避免内存泄漏
const privateData = new WeakMap();

function createSecureObject(data) {
    const obj = {};
    privateData.set(obj, data);
    
    obj.getData = function() {
        return privateData.get(obj);
    };
    
    return obj;
}

// 当obj被垃圾回收时，WeakMap中的对应条目也会被自动清理
```

##### 2. 合理使用闭包

```javascript
// 避免不必要的闭包
function createManyFunctions() {
    const functions = [];
    
    // 不好的做法：每个函数都创建闭包
    for (let i = 0; i < 1000; i++) {
        functions.push(function() {
            return i; // 每个函数都保持对i的引用
        });
    }
    
    return functions;
}

// 更好的做法
function createManyFunctionsImproved() {
    const functions = [];
    
    for (let i = 0; i < 1000; i++) {
        functions.push(createFunction(i));
    }
    
    return functions;
}

function createFunction(value) {
    return function() {
        return value;
    };
}
```

##### 3. 监控内存使用

```javascript
// 内存使用监控工具
function monitorMemory() {
    if (performance.memory) {
        console.log('Used:', performance.memory.usedJSHeapSize);
        console.log('Total:', performance.memory.totalJSHeapSize);
        console.log('Limit:', performance.memory.jsHeapSizeLimit);
    }
}

// 定期检查内存使用情况
setInterval(monitorMemory, 5000);
```

### 模块模式的实现

#### 基本模块模式

```javascript
// 基本模块模式
const MyModule = (function() {
    // 私有变量和函数
    let privateVariable = 0;
    
    function privateFunction() {
        return 'This is private';
    }
    
    // 返回公共接口
    return {
        publicVariable: 'This is public',
        
        publicMethod: function() {
            privateVariable++;
            return privateFunction() + ' - Counter: ' + privateVariable;
        },
        
        getPrivateVariable: function() {
            return privateVariable;
        }
    };
})();

console.log(MyModule.publicVariable); // This is public
console.log(MyModule.publicMethod()); // This is private - Counter: 1
console.log(MyModule.getPrivateVariable()); // 1
// MyModule.privateFunction(); // TypeError: MyModule.privateFunction is not a function
```

#### 增强模块模式

```javascript
// 增强模块模式 - 支持继承
const EnhancedModule = (function() {
    // 私有变量
    let instance;
    
    // 构造函数
    function Constructor(name) {
        this.name = name;
    }
    
    // 原型方法
    Constructor.prototype.getName = function() {
        return this.name;
    };
    
    // 工厂方法
    return function(name) {
        if (!instance) {
            instance = new Constructor(name);
        }
        return instance;
    };
})();

const module1 = EnhancedModule('First');
const module2 = EnhancedModule('Second');
console.log(module1.getName()); // First
console.log(module2.getName()); // First (单例)
console.log(module1 === module2); // true
```

#### 现代模块模式

```javascript
// ES6模块模式
const ModulePattern = (function() {
    // 私有状态
    const privateState = new Map();
    
    class Module {
        constructor(id) {
            this.id = id;
            privateState.set(this, {
                counter: 0,
                data: []
            });
        }
        
        increment() {
            const state = privateState.get(this);
            state.counter++;
            return state.counter;
        }
        
        addData(item) {
            const state = privateState.get(this);
            state.data.push(item);
            return state.data.length;
        }
        
        getData() {
            const state = privateState.get(this);
            return [...state.data]; // 返回副本
        }
    }
    
    // 静态方法
    Module.create = function(id) {
        return new Module(id);
    };
    
    return Module;
})();

const myModule = ModulePattern.create('test');
console.log(myModule.increment()); // 1
console.log(myModule.addData('item1')); // 1
console.log(myModule.getData()); // ['item1']
```

#### 实际应用示例

```javascript
// 配置管理模块
const ConfigManager = (function() {
    // 私有配置存储
    let config = {};
    let observers = [];
    
    // 私有方法
    function notifyObservers(key, oldValue, newValue) {
        observers.forEach(observer => {
            observer(key, oldValue, newValue);
        });
    }
    
    function validateConfig(newConfig) {
        // 配置验证逻辑
        return typeof newConfig === 'object' && newConfig !== null;
    }
    
    // 公共接口
    return {
        // 获取配置值
        get: function(key) {
            return key ? config[key] : { ...config };
        },
        
        // 设置配置值
        set: function(key, value) {
            if (typeof key === 'object') {
                // 批量设置
                const oldConfig = { ...config };
                Object.assign(config, key);
                notifyObservers('*', oldConfig, config);
            } else {
                // 单个设置
                const oldValue = config[key];
                config[key] = value;
                notifyObservers(key, oldValue, value);
            }
        },
        
        // 重置配置
        reset: function() {
            const oldConfig = { ...config };
            config = {};
            notifyObservers('*', oldConfig, {});
        },
        
        // 订阅配置变化
        subscribe: function(observer) {
            if (typeof observer === 'function') {
                observers.push(observer);
                return function unsubscribe() {
                    const index = observers.indexOf(observer);
                    if (index > -1) {
                        observers.splice(index, 1);
                    }
                };
            }
        },
        
        // 验证配置
        validate: function(newConfig) {
            return validateConfig(newConfig);
        }
    };
})();

// 使用示例
const unsubscribe = ConfigManager.subscribe((key, oldValue, newValue) => {
    console.log(`Config changed: ${key}`, oldValue, newValue);
});

ConfigManager.set('apiUrl', 'https://api.example.com');
ConfigManager.set('timeout', 5000);
console.log(ConfigManager.get()); // { apiUrl: 'https://api.example.com', timeout: 5000 }
```

# 五、面向对象编程

## 5.1 对象创建方式

### 1. 对象字面量语法

最简单直接的创建对象方式：

```javascript
// 对象字面量
const person = {
    name: 'Alice',
    age: 25,
    greet() {
        console.log(`Hello, I'm ${this.name}`);
    }
};

// 动态添加属性
person.city = 'Beijing';
person['email'] = 'alice@example.com';

console.log(person); // {name: "Alice", age: 25, greet: ƒ, city: "Beijing", email: "alice@example.com"}
```

### 2. 构造函数模式

使用函数作为构造器创建对象：

```javascript
// 构造函数
function Person(name, age) {
    this.name = name;
    this.age = age;
    this.greet = function() {
        console.log(`Hello, I'm ${this.name}`);
    };
}

// 使用 new 关键字创建实例
const person1 = new Person('Bob', 30);
const person2 = new Person('Charlie', 28);

console.log(person1 instanceof Person); // true
console.log(person1.greet === person2.greet); // false (每个实例都有自己的方法副本)
```

### 3. Object.create() 方法

通过指定原型对象创建新对象：

```javascript
// 创建原型对象
const personProto = {
    greet() {
        console.log(`Hello, I'm ${this.name}`);
    },
    introduce() {
        console.log(`I'm ${this.age} years old`);
    }
};

// 使用 Object.create() 创建对象
const student = Object.create(personProto);
student.name = 'David';
student.age = 22;
student.major = 'Computer Science';

student.greet(); // Hello, I'm David
student.introduce(); // I'm 22 years old

// 指定属性描述符
const teacher = Object.create(personProto, {
    name: {
        value: 'Eva',
        writable: true,
        enumerable: true,
        configurable: true
    },
    subject: {
        value: 'Math',
        writable: true,
        enumerable: true,
        configurable: true
    }
});
```

### 4. ES6 Class 语法糖

更现代的面向对象语法：

```javascript
// ES6 类定义
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
    
    // 实例方法
    greet() {
        console.log(`Hello, I'm ${this.name}`);
    }
    
    // 静态方法
    static getSpecies() {
        return 'Homo sapiens';
    }
    
    // Getter
    get info() {
        return `${this.name}, ${this.age} years old`;
    }
    
    // Setter
    set nickname(value) {
        this._nickname = value;
    }
}

const person = new Person('Frank', 35);
person.greet(); // Hello, I'm Frank
console.log(Person.getSpecies()); // Homo sapiens
console.log(person.info); // Frank, 35 years old
person.nickname = 'Frankie';
```

## 5.2 原型和原型链

### 1. prototype 属性机制

每个函数都有一个 prototype 属性：

```javascript
function Animal(name) {
    this.name = name;
}

// 在原型上添加方法
Animal.prototype.speak = function() {
    console.log(`${this.name} makes a sound`);
};

Animal.prototype.type = 'Animal';

const dog = new Animal('Dog');
dog.speak(); // Dog makes a sound
console.log(dog.type); // Animal

// 查看原型关系
console.log(dog.__proto__ === Animal.prototype); // true
console.log(Animal.prototype.constructor === Animal); // true
```

### 2. 原型链继承原理

对象属性查找机制：

```javascript
function Parent() {
    this.parentProp = 'parent property';
}

Parent.prototype.parentMethod = function() {
    return 'parent method';
};

function Child() {
    this.childProp = 'child property';
}

// 建立原型链
Child.prototype = Object.create(Parent.prototype);
Child.prototype.constructor = Child;

Child.prototype.childMethod = function() {
    return 'child method';
};

const child = new Child();

// 属性查找顺序：实例 -> Child.prototype -> Parent.prototype -> Object.prototype -> null
console.log(child.childProp); // child property
console.log(child.parentProp); // undefined (在Parent构造函数中定义)
console.log(child.childMethod()); // child method
console.log(child.parentMethod()); // parent method
console.log(child.toString()); // [object Object] (来自Object.prototype)
```

### 3. instanceof 运算符

检查对象是否是某个构造函数的实例：

```javascript
function A() {}
function B() {}

B.prototype = Object.create(A.prototype);

const b = new B();

console.log(b instanceof B); // true
console.log(b instanceof A); // true (通过原型链)
console.log(B instanceof A); // false
console.log(B instanceof Function); // true
console.log(b instanceof Object); // true

// 自定义 instanceof 实现
function myInstanceof(obj, constructor) {
    let proto = Object.getPrototypeOf(obj);
    
    while (proto !== null) {
        if (proto === constructor.prototype) {
            return true;
        }
        proto = Object.getPrototypeOf(proto);
    }
    
    return false;
}

console.log(myInstanceof(b, B)); // true
console.log(myInstanceof(b, A)); // true
```

### 4. 原型污染安全问题

恶意修改原型对象可能导致安全问题：

```javascript
// 危险示例：原型污染
function processUserInput(input) {
    const user = {};
    
    // 不安全的属性设置
    for (let key in input) {
        user[key] = input[key]; // 如果 key 是 '__proto__'，可能污染原型
    }
    
    return user;
}

// 恶意输入
const maliciousInput = {
    name: 'Alice',
    __proto__: {
        isAdmin: true // 污染 Object.prototype
    }
};

const user = processUserInput(maliciousInput);

// 所有对象都可能受到影响
const anotherObject = {};
console.log(anotherObject.isAdmin); // true (被污染了！)

// 安全的处理方式
function safeProcessUserInput(input) {
    const user = {};
    
    for (let key in input) {
        // 防止原型污染
        if (key !== '__proto__' && key !== 'constructor' && key !== 'prototype') {
            user[key] = input[key];
        }
    }
    
    return user;
}
```

## 5.3 继承机制

### 1. 原型链继承

通过原型链实现继承：

```javascript
// 父类
function Animal(name) {
    this.name = name;
    this.colors = ['red', 'blue'];
}

Animal.prototype.speak = function() {
    console.log(`${this.name} makes a sound`);
};

// 子类
function Dog(name, breed) {
    this.name = name;
    this.breed = breed;
}

// 继承
Dog.prototype = new Animal();
Dog.prototype.constructor = Dog;

Dog.prototype.bark = function() {
    console.log(`${this.name} barks`);
};

const dog1 = new Dog('Buddy', 'Golden Retriever');
const dog2 = new Dog('Max', 'Labrador');

dog1.colors.push('green');
console.log(dog2.colors); // ['red', 'blue', 'green'] - 问题：引用类型属性被共享
```

### 2. 构造函数继承

使用 call/apply 调用父构造函数：

```javascript
function Animal(name) {
    this.name = name;
    this.colors = ['red', 'blue'];
}

Animal.prototype.speak = function() {
    console.log(`${this.name} makes a sound`);
};

function Dog(name, breed) {
    // 继承实例属性
    Animal.call(this, name);
    this.breed = breed;
}

const dog1 = new Dog('Buddy', 'Golden Retriever');
const dog2 = new Dog('Max', 'Labrador');

dog1.colors.push('green');
console.log(dog1.colors); // ['red', 'blue', 'green']
console.log(dog2.colors); // ['red', 'blue'] - 解决了引用类型属性共享问题

// 问题：无法继承原型方法
// dog1.speak(); // TypeError: dog1.speak is not a function
```

### 3. 组合继承模式

结合原型链继承和构造函数继承：

```javascript
function Animal(name) {
    this.name = name;
    this.colors = ['red', 'blue'];
}

Animal.prototype.speak = function() {
    console.log(`${this.name} makes a sound`);
};

function Dog(name, breed) {
    // 继承实例属性（构造函数继承）
    Animal.call(this, name);
    this.breed = breed;
}

// 继承原型方法（原型链继承）
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;

Dog.prototype.bark = function() {
    console.log(`${this.name} barks`);
};

const dog1 = new Dog('Buddy', 'Golden Retriever');
const dog2 = new Dog('Max', 'Labrador');

dog1.colors.push('green');
console.log(dog1.colors); // ['red', 'blue', 'green']
console.log(dog2.colors); // ['red', 'blue']

dog1.speak(); // Buddy makes a sound
dog1.bark(); // Buddy barks

// 问题：调用了两次父构造函数
```

### 4. ES6 类继承语法

现代的继承方式：

```javascript
// 父类
class Animal {
    constructor(name) {
        this.name = name;
        this.colors = ['red', 'blue'];
    }
    
    speak() {
        console.log(`${this.name} makes a sound`);
    }
    
    static getKingdom() {
        return 'Animalia';
    }
}

// 子类
class Dog extends Animal {
    constructor(name, breed) {
        super(name); // 调用父类构造函数
        this.breed = breed;
    }
    
    speak() {
        super.speak(); // 调用父类方法
        console.log(`${this.name} barks`);
    }
    
    bark() {
        console.log(`${this.name} barks loudly`);
    }
}

const dog = new Dog('Buddy', 'Golden Retriever');
dog.speak(); // Buddy makes a sound \n Buddy barks
dog.bark(); // Buddy barks loudly

console.log(Animal.getKingdom()); // Animalia
console.log(Dog.getKingdom()); // Animalia (继承静态方法)

// 检查继承关系
console.log(dog instanceof Dog); // true
console.log(dog instanceof Animal); // true
console.log(Dog instanceof Animal); // false
console.log(Dog.prototype instanceof Animal); // true
```

### 高级继承示例

```javascript
// 复杂继承示例
class Shape {
    constructor(color) {
        this.color = color;
    }
    
    getColor() {
        return this.color;
    }
    
    // 抽象方法
    getArea() {
        throw new Error('getArea method must be implemented');
    }
}

class Rectangle extends Shape {
    constructor(color, width, height) {
        super(color);
        this.width = width;
        this.height = height;
    }
    
    getArea() {
        return this.width * this.height;
    }
    
    getPerimeter() {
        return 2 * (this.width + this.height);
    }
}

class Square extends Rectangle {
    constructor(color, side) {
        super(color, side, side);
        this.side = side;
    }
    
    // 重写方法
    getPerimeter() {
        return 4 * this.side;
    }
}

const rect = new Rectangle('red', 5, 3);
const square = new Square('blue', 4);

console.log(rect.getArea()); // 15
console.log(square.getArea()); // 16
console.log(rect.getPerimeter()); // 16
console.log(square.getPerimeter()); // 16

// Mixin 模式
const Flyable = {
    fly() {
        console.log(`${this.name} is flying`);
    }
};

const Swimmable = {
    swim() {
        console.log(`${this.name} is swimming`);
    }
};

class Bird extends Animal {
    constructor(name) {
        super(name);
    }
}

// 添加 mixin
Object.assign(Bird.prototype, Flyable);

class Duck extends Bird {
    constructor(name) {
        super(name);
    }
}

Object.assign(Duck.prototype, Swimmable);

const duck = new Duck('Donald');
duck.fly(); // Donald is flying
duck.swim(); // Donald is swimming
```

# 六、数组和字符串处理

## 6.1 数组操作方法

### 1. 数组创建和初始化

```javascript
// 数组字面量
const arr1 = [1, 2, 3, 4, 5];
const arr2 = ['apple', 'banana', 'orange'];
const arr3 = [1, 'hello', true, null, {name: 'John'}]; // 混合类型数组

// Array 构造函数
const arr4 = new Array(5); // 创建长度为5的空数组 [empty × 5]
const arr5 = new Array(1, 2, 3, 4, 5); // [1, 2, 3, 4, 5]
const arr6 = Array(1, 2, 3); // 不使用 new 也可以

// Array.of() - 创建指定元素的数组
const arr7 = Array.of(1); // [1]
const arr8 = Array.of(1, 2, 3); // [1, 2, 3]
const arr9 = Array.of(undefined); // [undefined]

// Array.from() - 从类数组对象或可迭代对象创建数组
const arr10 = Array.from('hello'); // ['h', 'e', 'l', 'l', 'o']
const arr11 = Array.from([1, 2, 3], x => x * 2); // [2, 4, 6]

// 类数组对象转换
function example() {
    const args = Array.from(arguments);
    console.log(args); // 转换 arguments 为真正的数组
}
example(1, 2, 3); // [1, 2, 3]

// NodeList 转数组
const divs = Array.from(document.querySelectorAll('div'));

// 设置长度和填充
const arr12 = new Array(10).fill(0); // [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
const arr13 = new Array(5).fill('default'); // ['default', 'default', 'default', 'default', 'default']
```

### 2. 变异方法和非变异方法

#### 变异方法（修改原数组）

```javascript
const fruits = ['apple', 'banana', 'orange'];

// push() - 在末尾添加元素，返回新长度
const newLength = fruits.push('grape', 'kiwi');
console.log(fruits); // ['apple', 'banana', 'orange', 'grape', 'kiwi']
console.log(newLength); // 5

// pop() - 删除末尾元素，返回删除的元素
const lastFruit = fruits.pop();
console.log(fruits); // ['apple', 'banana', 'orange', 'grape']
console.log(lastFruit); // 'kiwi'

// shift() - 删除首元素，返回删除的元素
const firstFruit = fruits.shift();
console.log(fruits); // ['banana', 'orange', 'grape']
console.log(firstFruit); // 'apple'

// unshift() - 在开头添加元素，返回新长度
const newLength2 = fruits.unshift('mango', 'pear');
console.log(fruits); // ['mango', 'pear', 'banana', 'orange', 'grape']
console.log(newLength2); // 5

// splice() - 添加/删除元素，返回删除的元素数组
const removed = fruits.splice(1, 2, 'lemon', 'lime'); // 从索引1开始删除2个元素，并添加新元素
console.log(fruits); // ['mango', 'lemon', 'lime', 'orange', 'grape']
console.log(removed); // ['pear', 'banana']

// sort() - 排序
const numbers = [3, 1, 4, 1, 5, 9];
numbers.sort(); // 字典序排序（字符串比较）
console.log(numbers); // [1, 1, 3, 4, 5, 9]

// 数字排序需要比较函数
numbers.sort((a, b) => a - b); // 升序
numbers.sort((a, b) => b - a); // 降序

// reverse() - 反转数组
numbers.reverse();
console.log(numbers); // [9, 5, 4, 3, 1, 1]

// fill() - 填充数组
const arr = new Array(5);
arr.fill('x');
console.log(arr); // ['x', 'x', 'x', 'x', 'x']

arr.fill('y', 1, 3); // 从索引1到3（不包括3）填充'y'
console.log(arr); // ['x', 'y', 'y', 'x', 'x']

// copyWithin() - 浅复制数组的一部分到同一数组的另一位置
const arr2 = [1, 2, 3, 4, 5];
arr2.copyWithin(0, 3); // 从索引3开始复制到索引0
console.log(arr2); // [4, 5, 3, 4, 5]
```

#### 非变异方法（不修改原数组）

```javascript
const original = [1, 2, 3, 4, 5];

// concat() - 合并数组
const combined = original.concat([6, 7], [8, 9]);
console.log(combined); // [1, 2, 3, 4, 5, 6, 7, 8, 9]
console.log(original); // [1, 2, 3, 4, 5] - 原数组不变

// slice() - 提取部分数组
const part1 = original.slice(1, 4); // 从索引1到4（不包括4）
console.log(part1); // [2, 3, 4]
const part2 = original.slice(2); // 从索引2到末尾
console.log(part2); // [3, 4, 5]
const part3 = original.slice(-2); // 倒数两个元素
console.log(part3); // [4, 5]

// join() - 数组转字符串
const str1 = original.join(); // 默认用逗号分隔
console.log(str1); // '1,2,3,4,5'
const str2 = original.join(' - ');
console.log(str2); // '1 - 2 - 3 - 4 - 5'

// toString() 和 toLocaleString()
console.log(original.toString()); // '1,2,3,4,5'
console.log(original.toLocaleString()); // '1,2,3,4,5'

// indexOf() 和 lastIndexOf()
const arr = [1, 2, 3, 2, 4];
console.log(arr.indexOf(2)); // 1 - 第一次出现的索引
console.log(arr.lastIndexOf(2)); // 3 - 最后一次出现的索引
console.log(arr.indexOf(10)); // -1 - 未找到返回-1

// includes() - 检查是否包含元素
console.log(arr.includes(2)); // true
console.log(arr.includes(10)); // false
console.log(arr.includes(2, 2)); // false - 从索引2开始查找

// find() 和 findIndex()
const people = [
    {name: 'Alice', age: 25},
    {name: 'Bob', age: 30},
    {name: 'Charlie', age: 35}
];

const found = people.find(person => person.age > 28);
console.log(found); // {name: 'Bob', age: 30}

const foundIndex = people.findIndex(person => person.name === 'Charlie');
console.log(foundIndex); // 2

// filter() - 过滤数组
const adults = people.filter(person => person.age >= 30);
console.log(adults); // [{name: 'Bob', age: 30}, {name: 'Charlie', age: 35}]

// map() - 转换数组元素
const names = people.map(person => person.name);
console.log(names); // ['Alice', 'Bob', 'Charlie']

const agesPlusTen = people.map(person => ({...person, age: person.age + 10}));
console.log(agesPlusTen); // [{name: 'Alice', age: 35}, ...]

// reduce() 和 reduceRight()
const numbers = [1, 2, 3, 4, 5];

// 求和
const sum = numbers.reduce((accumulator, currentValue) => accumulator + currentValue, 0);
console.log(sum); // 15

// 求最大值
const max = numbers.reduce((max, current) => current > max ? current : max);
console.log(max); // 5

// 数组扁平化
const nested = [1, [2, 3], [4, [5, 6]]];
const flattened = nested.reduce((acc, val) => acc.concat(val), []);
console.log(flattened); // [1, 2, 3, 4, [5, 6]]
```

### 3. 数组迭代和遍历方法

```javascript
const numbers = [1, 2, 3, 4, 5];

// forEach() - 遍历数组
numbers.forEach((value, index, array) => {
    console.log(`Index ${index}: ${value}`);
});

// for...of 循环
for (const value of numbers) {
    console.log(value);
}

// entries(), keys(), values()
for (const [index, value] of numbers.entries()) {
    console.log(`${index}: ${value}`);
}

for (const index of numbers.keys()) {
    console.log(index);
}

for (const value of numbers.values()) {
    console.log(value);
}

// every() - 检查所有元素是否满足条件
const allPositive = numbers.every(num => num > 0);
console.log(allPositive); // true

// some() - 检查是否有元素满足条件
const hasEven = numbers.some(num => num % 2 === 0);
console.log(hasEven); // true

// 实际应用示例
const products = [
    {name: 'Laptop', price: 1000, category: 'Electronics'},
    {name: 'Book', price: 20, category: 'Education'},
    {name: 'Phone', price: 800, category: 'Electronics'},
    {name: 'Desk', price: 300, category: 'Furniture'}
];

// 过滤电子产品
const electronics = products.filter(product => product.category === 'Electronics');

// 获取产品名称
const productNames = products.map(product => product.name);

// 计算总价
const totalPrice = products.reduce((sum, product) => sum + product.price, 0);

// 检查是否有昂贵商品
const hasExpensive = products.some(product => product.price > 500);

// 检查所有商品都有价格
const allHavePrice = products.every(product => product.price > 0);
```

### 4. 数组扁平化和转换

```javascript
// 数组扁平化方法

// flat() - 扁平化数组
const nestedArray = [1, [2, 3], [4, [5, 6]]];
console.log(nestedArray.flat()); // [1, 2, 3, 4, [5, 6]] - 默认扁平化一层
console.log(nestedArray.flat(2)); // [1, 2, 3, 4, 5, 6] - 指定扁平化深度

// 深度扁平化
const deepNested = [1, [2, [3, [4, [5]]]]];
console.log(deepNested.flat(Infinity)); // [1, 2, 3, 4, 5]

// flatMap() - 先映射再扁平化一层
const arr = [1, 2, 3];
const result = arr.flatMap(x => [x, x * 2]);
console.log(result); // [1, 2, 2, 4, 3, 6]

// 等价于
const result2 = arr.map(x => [x, x * 2]).flat();
console.log(result2); // [1, 2, 2, 4, 3, 6]

// 实际应用：处理嵌套数据
const sentences = ['Hello world', 'JavaScript is awesome', 'Arrays are useful'];
const words = sentences.flatMap(sentence => sentence.split(' '));
console.log(words); // ['Hello', 'world', 'JavaScript', 'is', 'awesome', 'Arrays', 'are', 'useful']

// 数组转换技巧

// 数组去重
const duplicates = [1, 2, 2, 3, 3, 4, 5, 5];
const unique = [...new Set(duplicates)];
console.log(unique); // [1, 2, 3, 4, 5]

// 数组分组
function groupBy(array, key) {
    return array.reduce((groups, item) => {
        const group = item[key];
        if (!groups[group]) {
            groups[group] = [];
        }
        groups[group].push(item);
        return groups;
    }, {});
}

const people = [
    {name: 'Alice', department: 'IT'},
    {name: 'Bob', department: 'HR'},
    {name: 'Charlie', department: 'IT'},
    {name: 'David', department: 'Finance'}
];

const grouped = groupBy(people, 'department');
console.log(grouped);
// {
//   IT: [{name: 'Alice', department: 'IT'}, {name: 'Charlie', department: 'IT'}],
//   HR: [{name: 'Bob', department: 'HR'}],
//   Finance: [{name: 'David', department: 'Finance'}]
// }

// 数组分块
function chunk(array, size) {
    const chunks = [];
    for (let i = 0; i < array.length; i += size) {
        chunks.push(array.slice(i, i + size));
    }
    return chunks;
}

const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9];
const chunked = chunk(numbers, 3);
console.log(chunked); // [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

// 数组交集、并集、差集
const arr1 = [1, 2, 3, 4];
const arr2 = [3, 4, 5, 6];

// 交集
const intersection = arr1.filter(x => arr2.includes(x));
console.log(intersection); // [3, 4]

// 并集
const union = [...new Set([...arr1, ...arr2])];
console.log(union); // [1, 2, 3, 4, 5, 6]

// 差集 (arr1 - arr2)
const difference = arr1.filter(x => !arr2.includes(x));
console.log(difference); // [1, 2]
```

## 6.2 字符串处理技术

### 1. 字符串基本操作

```javascript
// 字符串创建
const str1 = 'Hello';
const str2 = "World";
const str3 = `Template`;
const str4 = new String('Object'); // 不推荐，创建的是String对象

// 字符串长度
const text = 'JavaScript';
console.log(text.length); // 10

// 访问字符
console.log(text[0]); // 'J'
console.log(text.charAt(0)); // 'J'
console.log(text.charCodeAt(0)); // 74 (Unicode值)
console.log(text.codePointAt(0)); // 74 (ES6，支持Unicode码点)

// 字符串不可变性
let greeting = 'Hello';
greeting[0] = 'h'; // 无效操作
console.log(greeting); // 'Hello' - 原字符串不变

// 字符串连接
const firstName = 'John';
const lastName = 'Doe';
const fullName = firstName + ' ' + lastName; // 'John Doe'
const fullName2 = `${firstName} ${lastName}`; // 模板字符串
const fullName3 = firstName.concat(' ', lastName); // 'John Doe'

// 字符串比较
console.log('a' < 'b'); // true
console.log('A' < 'a'); // true (ASCII码比较)
console.log('10' < '2'); // true (字符串比较，不是数值比较)

// localeCompare() - 本地化字符串比较
console.log('ä'.localeCompare('z', 'de')); // -1 (德语中 ä 排在 z 前面)
```

### 2. 字符串搜索和替换

```javascript
const text = 'The quick brown fox jumps over the lazy dog';

// 搜索方法
console.log(text.indexOf('the')); // 32 - 第一次出现的位置（区分大小写）
console.log(text.indexOf('the', 10)); // 32 - 从索引10开始搜索
console.log(text.lastIndexOf('the')); // 32 - 最后一次出现的位置

console.log(text.search('brown')); // 10 - 支持正则表达式
console.log(text.search(/fox/i)); // 16 - 忽略大小写

// 包含检查
console.log(text.includes('quick')); // true
console.log(text.includes('Quick')); // false
console.log(text.includes('quick', 5)); // true - 从索引5开始检查

// 开头和结尾检查
console.log(text.startsWith('The')); // true
console.log(text.startsWith('quick', 4)); // true - 从索引4开始检查
console.log(text.endsWith('dog')); // true
console.log(text.endsWith('lazy', text.length - 4)); // true - 检查前(length-4)个字符

// 正则表达式搜索
const email = 'contact@example.com';
const emailRegex = /\w+@\w+\.\w+/;
console.log(emailRegex.test(email)); // true
console.log(email.match(emailRegex)); // ['contact@example.com']

// matchAll() - ES2020
const text2 = 'Phone: 123-456-7890, Fax: 987-654-3210';
const phoneRegex = /(\d{3})-(\d{3})-(\d{4})/g;
const matches = [...text2.matchAll(phoneRegex)];
console.log(matches[0]); // ['123-456-7890', '123', '456', '7890']

// 替换方法
const sentence = 'The cat sat on the mat';

// 基本替换
console.log(sentence.replace('cat', 'dog')); // 'The dog sat on the mat'
console.log(sentence.replace(/the/gi, 'a')); // 'a cat sat on a mat' (全局替换，忽略大小写)

// 使用函数进行替换
const prices = 'Price: $29.99, Discount: $5.00';
const updatedPrices = prices.replace(/\$(\d+\.\d+)/g, (match, price) => {
    return `$${(parseFloat(price) * 0.9).toFixed(2)}`;
});
console.log(updatedPrices); // 'Price: $26.99, Discount: $4.50'

// replaceAll() - ES2021
const text3 = 'cat and cat and cat';
console.log(text3.replaceAll('cat', 'dog')); // 'dog and dog and dog'

// 提取子字符串
const longText = 'JavaScript is awesome';

console.log(longText.substring(0, 10)); // 'JavaScript'
console.log(longText.substring(11)); // 'is awesome'

console.log(longText.slice(0, 10)); // 'JavaScript'
console.log(longText.slice(-7)); // 'awesome' - 负数表示从末尾开始
console.log(longText.slice(-7, -1)); // 'awesom'

// substr() - 已废弃，但仍可用
console.log(longText.substr(0, 10)); // 'JavaScript'
console.log(longText.substr(11, 2)); // 'is'
```

### 3. 字符串格式化方法

```javascript
// 大小写转换
const text = 'Hello World';

console.log(text.toUpperCase()); // 'HELLO WORLD'
console.log(text.toLowerCase()); // 'hello world'

// ES2015 新增方法
console.log(text.toLocaleUpperCase()); // 'HELLO WORLD' (考虑本地化)
console.log(text.toLocaleLowerCase()); // 'hello world' (考虑本地化)

// 首字母大写函数
function capitalize(str) {
    return str.charAt(0).toUpperCase() + str.slice(1).toLowerCase();
}
console.log(capitalize('hello')); // 'Hello'

// 去除空白字符
const spacedText = '  Hello World  ';
console.log(spacedText.trim()); // 'Hello World'
console.log(spacedText.trimStart()); // 'Hello World  '
console.log(spacedText.trimEnd()); // '  Hello World'

// padStart() 和 padEnd() - ES2017
const number = '5';
console.log(number.padStart(3, '0')); // '005'
console.log(number.padEnd(3, '0')); // '500'

// 时间格式化示例
function formatTime(hours, minutes, seconds) {
    return `${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
}
console.log(formatTime(9, 5, 7)); // '09:05:07'

// repeat() - 重复字符串
const dash = '-'.repeat(10);
console.log(dash); // '----------'

const separator = '='.repeat(20);
console.log(separator);

// 字符串分割
const csv = 'apple,banana,orange,grape';
const fruits = csv.split(',');
console.log(fruits); // ['apple', 'banana', 'orange', 'grape']

const sentence = 'The quick brown fox';
const words = sentence.split(' ');
console.log(words); // ['The', 'quick', 'brown', 'fox']

const chars = sentence.split('');
console.log(chars); // ['T', 'h', 'e', ' ', 'q', 'u', 'i', 'c', 'k', ...]

// 限制分割数量
const limited = csv.split(',', 2);
console.log(limited); // ['apple', 'banana']

// 使用正则表达式分割
const text = 'apple123banana456orange';
const parts = text.split(/\d+/);
console.log(parts); // ['apple', 'banana', 'orange']

// 字符串反转
function reverseString(str) {
    return str.split('').reverse().join('');
}
console.log(reverseString('hello')); // 'olleh'

// 字符串统计
function countChar(str, char) {
    return str.split(char).length - 1;
}
console.log(countChar('hello world', 'l')); // 3
```

### 4. 模板字符串特性

```javascript
// 基本模板字符串
const name = 'Alice';
const age = 25;
const greeting = `Hello, ${name}! You are ${age} years old.`;
console.log(greeting); // 'Hello, Alice! You are 25 years old.'

// 表达式插值
const a = 5;
const b = 10;
console.log(`The sum of ${a} and ${b} is ${a + b}.`); // 'The sum of 5 and 10 is 15.'

// 多行字符串
const multiline = `
This is a
multiline
string
`;
console.log(multiline);

// HTML 模板示例
function createUserCard(user) {
    return `
        <div class="user-card">
            <h2>${user.name}</h2>
            <p>Age: ${user.age}</p>
            <p>Email: ${user.email}</p>
        </div>
    `;
}

const user = {
    name: 'John Doe',
    age: 30,
    email: 'john@example.com'
};

console.log(createUserCard(user));

// 嵌套模板字符串
const classes = ['btn', 'btn-primary'];
const button = `
    <button class="${classes.join(' ')}" 
            data-action="${'submit'}">
        ${'Click me'}
    </button>
`;

// 带标签的模板字符串
function highlight(strings, ...values) {
    let result = '';
    strings.forEach((string, i) => {
        result += string;
        if (values[i]) {
            result += `<mark>${values[i]}</mark>`;
        }
    });
    return result;
}

const name2 = 'JavaScript';
const feature = 'template strings';
const message = highlight`Learn ${name2} ${feature} today!`;
console.log(message); // 'Learn <mark>JavaScript</mark> <mark>template strings</mark> today!'

// 实用的标签函数示例
function currency(strings, ...values) {
    let result = '';
    strings.forEach((string, i) => {
        result += string;
        if (values[i] !== undefined) {
            result += `$${values[i].toFixed(2)}`;
        }
    });
    return result;
}

const price1 = 19.99;
const price2 = 5.50;
const total = price1 + price2;
console.log(currency`Item 1: ${price1}, Item 2: ${price2}, Total: ${total}`);
// 'Item 1: $19.99, Item 2: $5.50, Total: $25.49'

// 原始字符串访问
function raw(strings, ...values) {
    console.log('Raw strings:', strings.raw);
    console.log('Cooked strings:', strings);
}

raw`Hello\nWorld`; 
// Raw strings: ['Hello\\nWorld']
// Cooked strings: ['Hello\nWorld']

// 实际应用：SQL 查询构建
function sql(strings, ...values) {
    let query = '';
    strings.forEach((string, i) => {
        query += string;
        if (values[i] !== undefined) {
            // 简单的 SQL 注入防护（实际项目中需要更完善的方案）
            query += `'${values[i].toString().replace(/'/g, "''")}'`;
        }
    });
    return query;
}

const tableName = 'users';
const userId = "1'; DROP TABLE users; --";
const query = sql`SELECT * FROM ${tableName} WHERE id = ${userId}`;
console.log(query); // "SELECT * FROM 'users' WHERE id = '1''; DROP TABLE users; --'"

// 模板字符串性能优化
// 对于重复使用的模板，可以预编译
function createTemplate(template) {
    return function(data) {
        return template.replace(/\${(\w+)}/g, (match, key) => data[key] || match);
    };
}

const userTemplate = createTemplate('Hello, ${name}! You are ${age} years old.');
console.log(userTemplate({name: 'Bob', age: 30})); // 'Hello, Bob! You are 30 years old.'
```

# 七、正则表达式

## 7.1 正则表达式基础

### 1. 正则表达式语法和模式

```javascript
// 正则表达式基本语法
// 字面量形式
const regex1 = /pattern/flags;
const regex2 = /hello/i; // 不区分大小写

// 构造函数形式
const regex3 = new RegExp('pattern', 'flags');
const regex4 = new RegExp('hello', 'i');

// 基本字符匹配
const text = 'Hello World';
console.log(/Hello/.test(text)); // true
console.log(/hello/.test(text)); // false (区分大小写)
console.log(/hello/i.test(text)); // true (不区分大小写)

// 特殊字符
// . 匹配除换行符外的任意字符
console.log(/h.llo/.test('hello')); // true
console.log(/h.llo/.test('hallo')); // true
console.log(/h.llo/.test('h\nllo')); // false

// ^ 匹配行首
console.log(/^Hello/.test('Hello World')); // true
console.log(/^World/.test('Hello World')); // false

// $ 匹配行尾
console.log(/World$/.test('Hello World')); // true
console.log(/Hello$/.test('Hello World')); // false

// \b 匹配单词边界
console.log(/\bWorld\b/.test('Hello World')); // true
console.log(/\bWorld\b/.test('Hello Worldwide')); // false

// \B 匹配非单词边界
console.log(/\Borld\B/.test('Worldwide')); // true

// 转义特殊字符
const specialChars = /\.\^\$\*\+\?\(\)\[\]\{\}\|\\/;
console.log(specialChars.test('.^$*+?()[]{}|\\')); // true
```

### 2. 字面量和构造函数创建方式

```javascript
// 字面量形式 - 编译时确定
const literalRegex = /hello \d+/i;
console.log(literalRegex.test('Hello 123')); // true

// 构造函数形式 - 运行时确定
const pattern = 'hello \\d+';
const constructorRegex = new RegExp(pattern, 'i');
console.log(constructorRegex.test('Hello 123')); // true

// 动态创建正则表达式
function createEmailRegex(domains) {
    const domainPattern = domains.join('|');
    return new RegExp(`^[\\w.-]+@(${domainPattern})$`, 'i');
}

const emailRegex = createEmailRegex(['gmail.com', 'yahoo.com', 'outlook.com']);
console.log(emailRegex.test('user@gmail.com')); // true
console.log(emailRegex.test('user@hotmail.com')); // false

// 转义注意事项
// 字面量中的反斜杠需要双重转义
const literalPattern = /\d+\.\d+/; // 匹配数字.数字

// 构造函数中的反斜杠需要四重转义
const constructorPattern = new RegExp('\\d+\\.\\d+');

// 实际应用：动态验证规则
function createValidator(pattern, flags = '') {
    if (typeof pattern === 'string') {
        return new RegExp(pattern, flags);
    }
    return pattern;
}

const phoneValidator = createValidator('^\\d{3}-\\d{3}-\\d{4}$');
const emailValidator = createValidator('^[\\w.-]+@[\\w.-]+\\.[\\w]+$');

console.log(phoneValidator.test('123-456-7890')); // true
console.log(emailValidator.test('user@example.com')); // true
```

### 3. 标志位的含义和作用

```javascript
// 正则表达式标志位

// i - 不区分大小写 (ignore case)
const caseInsensitive = /hello/i;
console.log(caseInsensitive.test('Hello')); // true
console.log(caseInsensitive.test('HELLO')); // true
console.log(caseInsensitive.test('HeLLo')); // true

// g - 全局匹配 (global)
const globalRegex = /hello/g;
const text = 'Hello hello HELLO';
console.log(text.match(globalRegex)); // ['hello'] (不区分大小写的情况下)
const caseSensitiveGlobal = /hello/g;
console.log(text.match(caseSensitiveGlobal)); // ['hello'] (只匹配第一个)

// m - 多行模式 (multiline)
const multilineText = `Line 1
Line 2
Line 3`;

const withoutM = /^Line/g;
console.log(multilineText.match(withoutM)); // ['Line'] - 只匹配第一行

const withM = /^Line/mg;
console.log(multilineText.match(withM)); // ['Line', 'Line', 'Line'] - 匹配每行开头

// s - dotAll 模式 (ES2018) - 让 . 匹配换行符
const dotAllRegex = /hello.world/s;
const textWithNewline = 'hello\nworld';
console.log(dotAllRegex.test(textWithNewline)); // true (with s flag)
console.log(/hello.world/.test(textWithNewline)); // false (without s flag)

// u - Unicode 模式
const unicodeRegex = /\u{1F600}/u; // 匹配笑脸表情符号
console.log(unicodeRegex.test('😀')); // true

// y - 粘性匹配 (sticky)
const stickyRegex = /hello/y;
const text2 = 'hello world hello';
console.log(stickyRegex.test(text2)); // true
stickyRegex.lastIndex = 6; // 设置匹配位置
console.log(stickyRegex.test(text2)); // false (位置6不是'hello')

// 标志位组合使用
const complexRegex = /hello world/gim;
// g - 全局匹配
// i - 不区分大小写  
// m - 多行模式

// 检查和修改标志位
const regex = /hello/gi;
console.log(regex.flags); // 'gi'
console.log(regex.global); // true
console.log(regex.ignoreCase); // true
console.log(regex.multiline); // false

// 注意：标志位在创建后不能修改
// regex.global = false; // 无效
```

### 4. 字符类和量词使用

```javascript
// 字符类 (Character Classes)

// [abc] - 匹配方括号内任意字符
const vowelRegex = /[aeiou]/g;
const text = 'hello world';
console.log(text.match(vowelRegex)); // ['e', 'o', 'o']

// [a-z] - 匹配范围内的字符
const lowercaseRegex = /[a-z]/g;
console.log('Hello123'.match(lowercaseRegex)); // ['e', 'l', 'l', 'o']

// [^abc] - 匹配除了方括号内字符以外的任意字符
const nonVowelRegex = /[^aeiou\s]/g; // 非元音字母且非空白字符
console.log('hello world'.match(nonVowelRegex)); // ['h', 'l', 'l', 'w', 'r', 'l', 'd']

// 预定义字符类
console.log(/\d/.test('123')); // true - 数字 [0-9]
console.log(/\D/.test('abc')); // true - 非数字 [^0-9]
console.log(/\w/.test('a1_')); // true - 单词字符 [a-zA-Z0-9_]
console.log(/\W/.test(' @')); // true - 非单词字符 [^a-zA-Z0-9_]
console.log(/\s/.test(' \t\n')); // true - 空白字符
console.log(/\S/.test('abc')); // true - 非空白字符

// 量词 (Quantifiers)

// * - 匹配0次或多次
const zeroOrMore = /go*l/; // g + 0个或多个o + l
console.log(zeroOrMore.test('gl')); // true
console.log(zeroOrMore.test('gol')); // true
console.log(zeroOrMore.test('gooool')); // true

// + - 匹配1次或多次
const oneOrMore = /go+l/; // g + 1个或多个o + l
console.log(oneOrMore.test('gl')); // false
console.log(oneOrMore.test('gol')); // true
console.log(oneOrMore.test('gooool')); // true

// ? - 匹配0次或1次
const zeroOrOne = /go?l/; // g + 0个或1个o + l
console.log(zeroOrOne.test('gl')); // true
console.log(zeroOrOne.test('gol')); // true
console.log(zeroOrOne.test('gooool')); // false

// {n} - 匹配恰好n次
const exactlyThree = /a{3}/; // 恰好3个a
console.log(exactlyThree.test('aa')); // false
console.log(exactlyThree.test('aaa')); // true
console.log(exactlyThree.test('aaaa')); // true (匹配前3个)

// {n,} - 匹配至少n次
const atLeastTwo = /a{2,}/; // 至少2个a
console.log(atLeastTwo.test('a')); // false
console.log(atLeastTwo.test('aa')); // true
console.log(atLeastTwo.test('aaaaa')); // true

// {n,m} - 匹配n到m次
const twoToFour = /a{2,4}/; // 2到4个a
console.log(twoToFour.test('a')); // false
console.log(twoToFour.test('aa')); // true
console.log(twoToFour.test('aaaaa')); // true (匹配前4个)

// 贪婪与非贪婪匹配
const text2 = '<div>Hello</div><div>World</div>';

// 贪婪匹配 (默认) - 匹配尽可能多的字符
const greedy = /<div>.*<\/div>/;
console.log(text2.match(greedy)[0]); // '<div>Hello</div><div>World</div>'

// 非贪婪匹配 - 匹配尽可能少的字符
const nonGreedy = /<div>.*?<\/div>/g;
console.log(text2.match(nonGreedy)); // ['<div>Hello</div>', '<div>World</div>']

// 分组和捕获
const dateRegex = /(\d{4})-(\d{2})-(\d{2})/;
const date = '2023-12-25';
const match = date.match(dateRegex);
console.log(match); // ['2023-12-25', '2023', '12', '25']
console.log(match[1]); // '2023' (年)
console.log(match[2]); // '12' (月)
console.log(match[3]); // '25' (日)

// 非捕获分组
const nonCapturing = /(?:https?):\/\/(\w+)/;
const url = 'https://example.com';
const urlMatch = url.match(nonCapturing);
console.log(urlMatch); // ['https://example', 'example'] (没有捕获协议部分)

// 命名捕获组 (ES2018)
const namedGroups = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/;
const namedMatch = '2023-12-25'.match(namedGroups);
console.log(namedMatch.groups.year); // '2023'
console.log(namedMatch.groups.month); // '12'
console.log(namedMatch.groups.day); // '25'
```

## 7.2 正则表达式应用

### 1. 字符串匹配和验证

```javascript
// 常用验证正则表达式

// 邮箱验证
function validateEmail(email) {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return emailRegex.test(email);
}

console.log(validateEmail('user@example.com')); // true
console.log(validateEmail('invalid.email')); // false

// 更严格的邮箱验证
function validateEmailStrict(email) {
    const strictEmailRegex = /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?(?:\.[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?)*$/;
    return strictEmailRegex.test(email);
}

// 手机号验证 (中国)
function validatePhone(phone) {
    const phoneRegex = /^1[3-9]\d{9}$/;
    return phoneRegex.test(phone);
}

console.log(validatePhone('13812345678')); // true
console.log(validatePhone('12345678901')); // false

// 身份证验证 (中国18位)
function validateIDCard(id) {
    const idRegex = /^[1-9]\d{5}(18|19|20)\d{2}((0[1-9])|(1[0-2]))(([0-2][1-9])|10|20|30|31)\d{3}[0-9Xx]$/;
    return idRegex.test(id);
}

// 密码强度验证
function validatePassword(password) {
    // 至少8位，包含大小写字母、数字和特殊字符
    const passwordRegex = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$/;
    return passwordRegex.test(password);
}

console.log(validatePassword('Password123!')); // true
console.log(validatePassword('password')); // false

// URL验证
function validateURL(url) {
    const urlRegex = /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/;
    return urlRegex.test(url);
}

// IP地址验证
function validateIP(ip) {
    const ipRegex = /^((25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$/;
    return ipRegex.test(ip);
}

console.log(validateIP('192.168.1.1')); // true
console.log(validateIP('999.999.999.999')); // false

// 综合验证器
class Validator {
    static patterns = {
        email: /^[^\s@]+@[^\s@]+\.[^\s@]+$/,
        phone: /^1[3-9]\d{9}$/,
        url: /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/,
        ip: /^((25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$/,
        hexColor: /^#?([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$/
    };
    
    static validate(type, value) {
        const pattern = this.patterns[type];
        return pattern ? pattern.test(value) : false;
    }
}

console.log(Validator.validate('email', 'test@example.com')); // true
console.log(Validator.validate('hexColor', '#ff0000')); // true
```

### 2. 文本搜索和替换

```javascript
// 文本搜索应用

// 搜索所有匹配项
const text = 'The quick brown fox jumps over the lazy dog. The fox is quick.';
const foxRegex = /fox/gi; // 全局、不区分大小写
const matches = text.match(foxRegex);
console.log(matches); // ['fox', 'fox']

// 搜索匹配位置
const positions = [];
let match;
while ((match = foxRegex.exec(text)) !== null) {
    positions.push({
        match: match[0],
        index: match.index
    });
}
console.log(positions); // [{match: 'fox', index: 16}, {match: 'fox', index: 44}]

// 搜索和替换应用

// 基本替换
const newText = text.replace(/fox/gi, 'cat');
console.log(newText); // 'The quick brown cat jumps over the lazy dog. The cat is quick.'

// 使用捕获组进行替换
const dateText = '2023-12-25 is Christmas';
const formattedDate = dateText.replace(/(\d{4})-(\d{2})-(\d{2})/, '$2/$3/$1');
console.log(formattedDate); // '12/25/2023 is Christmas'

// 使用函数进行复杂替换
const prices = 'Price: $29.99, Discount: $5.00, Tax: $2.70';
const updatedPrices = prices.replace(/\$(\d+\.\d+)/g, (match, price) => {
    const newPrice = (parseFloat(price) * 1.1).toFixed(2);
    return `$${newPrice}`;
});
console.log(updatedPrices); // 'Price: $32.99, Discount: $5.50, Tax: $2.97'

// 文本高亮
function highlightText(text, searchTerm) {
    const regex = new RegExp(`(${searchTerm})`, 'gi');
    return text.replace(regex, '<mark>$1</mark>');
}

const content = 'JavaScript is a programming language. JavaScript is versatile.';
const highlighted = highlightText(content, 'javascript');
console.log(highlighted); // '<mark>JavaScript</mark> is a programming language. <mark>JavaScript</mark> is versatile.'

// 敏感词过滤
function filterSensitiveWords(text, sensitiveWords) {
    const pattern = sensitiveWords.map(word => word.replace(/[.*+?^${}()|[\]\\]/g, '\\$&')).join('|');
    const regex = new RegExp(`(${pattern})`, 'gi');
    return text.replace(regex, '***');
}

const sensitiveWords = ['badword', 'spam', 'scam'];
const filtered = filterSensitiveWords('This is a badword and spam message', sensitiveWords);
console.log(filtered); // 'This is a *** and *** message'

// 批量替换
function batchReplace(text, replacements) {
    let result = text;
    for (const [pattern, replacement] of Object.entries(replacements)) {
        const regex = new RegExp(pattern, 'g');
        result = result.replace(regex, replacement);
    }
    return result;
}

const replacements = {
    'hello': 'hi',
    'world': 'universe',
    '\\d+': 'NUMBER'
};

const originalText = 'Hello world! I have 5 apples and 3 oranges.';
const replacedText = batchReplace(originalText, replacements);
console.log(replacedText); // 'hi universe! I have NUMBER apples and NUMBER oranges.'
```

### 3. 数据提取和解析

```javascript
// 数据提取应用

// 从文本中提取邮箱地址
function extractEmails(text) {
    const emailRegex = /[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}/g;
    return text.match(emailRegex) || [];
}

const textWithEmails = 'Contact us at support@example.com or sales@company.org';
console.log(extractEmails(textWithEmails)); // ['support@example.com', 'sales@company.org']

// 从HTML中提取链接
function extractLinks(html) {
    const linkRegex = /<a\s+(?:[^>]*?\s+)?href=(["'])(.*?)\1/g;
    const links = [];
    let match;
    while ((match = linkRegex.exec(html)) !== null) {
        links.push(match[2]);
    }
    return links;
}

const html = '<a href="https://example.com">Example</a><a href="mailto:test@example.com">Email</a>';
console.log(extractLinks(html)); // ['https://example.com', 'mailto:test@example.com']

// 解析CSV数据
function parseCSV(csv) {
    const lines = csv.trim().split('\n');
    const headers = lines[0].split(',').map(header => header.trim());
    const data = [];
    
    for (let i = 1; i < lines.length; i++) {
        const values = lines[i].split(',');
        const row = {};
        headers.forEach((header, index) => {
            row[header] = values[index] ? values[index].trim() : '';
        });
        data.push(row);
    }
    
    return data;
}

const csvData = `name,age,city
John,25,New York
Jane,30,Los Angeles
Bob,35,Chicago`;

console.log(parseCSV(csvData));

// 从日志中提取信息
function parseLog(logLine) {
    const logRegex = /^(\d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2}) \[(\w+)\] (.+)$/;
    const match = logLine.match(logRegex);
    
    if (match) {
        return {
            timestamp: match[1],
            level: match[2],
            message: match[3]
        };
    }
    return null;
}

const logLine = '2023-12-25 14:30:45 [ERROR] Database connection failed';
console.log(parseLog(logLine));
// {timestamp: '2023-12-25 14:30:45', level: 'ERROR', message: 'Database connection failed'}

// 解析URL参数
function parseURLParams(url) {
    const params = {};
    const queryString = url.split('?')[1];
    
    if (queryString) {
        const pairs = queryString.split('&');
        pairs.forEach(pair => {
            const [key, value] = pair.split('=');
            params[decodeURIComponent(key)] = decodeURIComponent(value || '');
        });
    }
    
    return params;
}

const url = 'https://example.com/search?q=javascript&category=tutorial&page=1';
console.log(parseURLParams(url)); // {q: 'javascript', category: 'tutorial', page: '1'}

// 使用正则表达式解析复杂数据
function parseStructuredData(text) {
    // 解析类似 "Name: John, Age: 25, Email: john@example.com" 的数据
    const dataRegex = /(\w+):\s*([^,]+)/g;
    const data = {};
    let match;
    
    while ((match = dataRegex.exec(text)) !== null) {
        const key = match[1].toLowerCase();
        const value = match[2].trim();
        data[key] = value;
    }
    
    return data;
}

const structuredText = 'Name: John Doe, Age: 25, Email: john@example.com, City: New York';
console.log(parseStructuredData(structuredText));
// {name: 'John Doe', age: '25', email: 'john@example.com', city: 'New York'}

// 提取电话号码
function extractPhoneNumbers(text) {
    const phoneRegex = /(\+?1[-.\s]?)?\(?([0-9]{3})\)?[-.\s]?([0-9]{3})[-.\s]?([0-9]{4})/g;
    const phones = [];
    let match;
    
    while ((match = phoneRegex.exec(text)) !== null) {
        const fullNumber = match[0];
        const areaCode = match[2];
        const exchange = match[3];
        const number = match[4];
        phones.push({
            full: fullNumber,
            formatted: `(${areaCode}) ${exchange}-${number}`,
            areaCode: areaCode
        });
    }
    
    return phones;
}

const textWithPhones = 'Call me at 123-456-7890 or (987) 654-3210';
console.log(extractPhoneNumbers(textWithPhones));
```

### 4. 性能优化技巧

```javascript
// 正则表达式性能优化

// 1. 避免回溯灾难
// 危险示例：可能导致指数级时间复杂度
const dangerousRegex = /^(a+)+$/;
// dangerousRegex.test('aaaaaaaaaaaaaaaaaaaaaaaaaaaaaab'); // 可能导致浏览器卡死

// 安全替代方案
const safeRegex = /^a+$/;
safeRegex.test('aaaaaaaaaaaaaaaaaaaaaaaaaaaaaab'); // 快速返回 false

// 2. 使用具体字符而非通配符
// 慢：使用 .*
const slowRegex = /<div>.*<\/div>/;

// 快：使用具体字符类
const fastRegex = /<div>[^]*?<\/div>/; // [^]* 匹配包括换行符的所有字符

// 3. 预编译正则表达式
// 避免在循环中重复创建
function processData(items) {
    // 不好的做法
    // items.forEach(item => {
    //     const regex = /pattern/g; // 每次循环都创建
    //     // ...
    // });
    
    // 好的做法
    const regex = /pattern/g; // 预先创建
    items.forEach(item => {
        // 使用预编译的正则表达式
        regex.lastIndex = 0; // 重置 lastIndex
        // ...
    });
}

// 4. 使用 lastIndex 优化连续匹配
function findWords(text) {
    const wordRegex = /\w+/g;
    const words = [];
    let match;
    
    while ((match = wordRegex.exec(text)) !== null) {
        words.push(match[0]);
    }
    
    return words;
}

// 5. 缓存正则表达式
class RegexCache {
    constructor() {
        this.cache = new Map();
    }
    
    get(pattern, flags = '') {
        const key = `${pattern}_${flags}`;
        if (!this.cache.has(key)) {
            this.cache.set(key, new RegExp(pattern, flags));
        }
        return this.cache.get(key);
    }
}

const regexCache = new RegexCache();
const emailRegex = regexCache.get('^[^\\s@]+@[^\\s@]+\\.[^\\s@]+$');

// 6. 使用非捕获分组减少内存使用
// 不需要捕获时使用 (?:...)
const nonCapturing = /(?:https?):\/\/(\w+)/; // 只捕获域名
const capturing = /(https?):\/\/(\w+)/; // 捕获协议和域名

// 7. 避免不必要的全局标志
// 只需要检查是否存在时，不需要全局标志
const hasEmail = /[^\s@]+@[^\s@]+\.[^\s@]+/.test(text); // 比 /g 更快

// 8. 使用字符类而非选择符
// 慢：使用选择符
const slowCharClass = /(a|b|c)/;

// 快：使用字符类
const fastCharClass = /[abc]/;

// 9. 实际性能测试示例
function performanceTest() {
    const text = 'a'.repeat(1000) + 'b';
    
    // 测试不同正则表达式的性能
    const tests = [
        { name: '贪婪匹配', regex: /a+b/ },
        { name: '非贪婪匹配', regex: /a+?b/ },
        { name: 'possessive匹配', regex: /a++b/ } // 注意：JavaScript不支持possessive量词
    ];
    
    tests.forEach(test => {
        const start = performance.now();
        test.regex.test(text);
        const end = performance.now();
        console.log(`${test.name}: ${end - start}ms`);
    });
}

// 10. 正则表达式调试工具
function debugRegex(pattern, text) {
    const regex = new RegExp(pattern, 'g');
    const matches = [];
    let match;
    let iterations = 0;
    
    console.log(`Testing pattern: ${pattern}`);
    console.log(`Against text: ${text.substring(0, 50)}${text.length > 50 ? '...' : ''}`);
    
    while ((match = regex.exec(text)) !== null && iterations < 1000) {
        matches.push({
            match: match[0],
            index: match.index,
            groups: match.slice(1)
        });
        iterations++;
    }
    
    console.log(`Found ${matches.length} matches in ${iterations} iterations`);
    console.log('Matches:', matches);
    
    return matches;
}

// 11. 避免在循环中使用复杂的正则表达式
// 不好的做法
function badPractice(items) {
    return items.map(item => {
        return item.replace(/复杂的正则表达式/g, 'replacement');
    });
}

// 好的做法：预编译
function goodPractice(items) {
    const regex = /复杂的正则表达式/g;
    return items.map(item => {
        regex.lastIndex = 0; // 重置
        return item.replace(regex, 'replacement');
    });
}

// 12. 使用正则表达式进行预过滤
function efficientSearch(text, searchTerm) {
    // 先用简单检查快速排除
    if (!text.includes(searchTerm)) {
        return [];
    }
    
    // 再用正则表达式进行精确匹配
    const regex = new RegExp(searchTerm.replace(/[.*+?^${}()|[\]\\]/g, '\\$&'), 'gi');
    return text.match(regex) || [];
}
```

# 八、异步编程模型

## 8.1 异步编程基础

### 1. 同步和异步的区别

```javascript
// 同步编程 - 阻塞执行
console.log('1. 开始执行');

function syncOperation() {
    console.log('2. 同步操作开始');
    // 模拟耗时操作
    for (let i = 0; i < 1000000000; i++) {
        // 耗时计算
    }
    console.log('3. 同步操作结束');
    return '同步结果';
}

console.log('4. 调用同步函数');
const result = syncOperation();
console.log('5. 同步结果:', result);
console.log('6. 结束执行');

// 输出顺序：
// 1. 开始执行
// 4. 调用同步函数
// 2. 同步操作开始
// 3. 同步操作结束
// 5. 同步结果: 同步结果
// 6. 结束执行

// 异步编程 - 非阻塞执行
console.log('1. 开始执行');

function asyncOperation(callback) {
    console.log('2. 异步操作开始');
    
    // 使用 setTimeout 模拟异步操作
    setTimeout(() => {
        console.log('3. 异步操作结束');
        callback('异步结果');
    }, 1000);
    
    console.log('4. 异步操作已启动');
}

console.log('5. 调用异步函数');
asyncOperation((result) => {
    console.log('6. 异步回调执行:', result);
});
console.log('7. 异步函数调用结束');
console.log('8. 结束执行');

// 输出顺序：
// 1. 开始执行
// 5. 调用异步函数
// 2. 异步操作开始
// 4. 异步操作已启动
// 7. 异步函数调用结束
// 8. 结束执行
// (1秒后)
// 3. 异步操作结束
// 6. 异步回调执行: 异步结果

// 实际应用示例：文件读取对比
// 同步读取（阻塞）
const fs = require('fs');
console.log('开始同步读取');
try {
    const data = fs.readFileSync('large-file.txt', 'utf8');
    console.log('同步读取完成:', data.length);
} catch (error) {
    console.error('同步读取失败:', error);
}
console.log('继续执行');

// 异步读取（非阻塞）
console.log('开始异步读取');
fs.readFile('large-file.txt', 'utf8', (err, data) => {
    if (err) {
        console.error('异步读取失败:', err);
    } else {
        console.log('异步读取完成:', data.length);
    }
});
console.log('继续执行，不等待文件读取');
```

### 2. 回调函数模式

```javascript
// 基本回调函数
function fetchData(callback) {
    setTimeout(() => {
        const data = { id: 1, name: 'John' };
        callback(null, data); // Node.js 风格：error-first callback
    }, 1000);
}

fetchData((error, data) => {
    if (error) {
        console.error('获取数据失败:', error);
    } else {
        console.log('获取数据成功:', data);
    }
});

// 回调地狱示例
function getUser(userId, callback) {
    setTimeout(() => {
        callback(null, { id: userId, name: `User${userId}` });
    }, 100);
}

function getPosts(userId, callback) {
    setTimeout(() => {
        callback(null, [`Post1 by User${userId}`, `Post2 by User${userId}`]);
    }, 200);
}

function getComments(postId, callback) {
    setTimeout(() => {
        callback(null, [`Comment1 on ${postId}`, `Comment2 on ${postId}`]);
    }, 150);
}

// 回调地狱 - 嵌套过多，难以维护
getUser(1, (error, user) => {
    if (error) {
        console.error('获取用户失败:', error);
        return;
    }
    
    console.log('用户:', user);
    
    getPosts(user.id, (error, posts) => {
        if (error) {
            console.error('获取帖子失败:', error);
            return;
        }
        
        console.log('帖子:', posts);
        
        if (posts.length > 0) {
            getComments(posts[0], (error, comments) => {
                if (error) {
                    console.error('获取评论失败:', error);
                    return;
                }
                
                console.log('评论:', comments);
            });
        }
    });
});

// 回调函数错误处理
function riskyOperation(callback) {
    setTimeout(() => {
        try {
            // 模拟可能出错的操作
            const random = Math.random();
            if (random < 0.5) {
                throw new Error('随机错误');
            }
            callback(null, '操作成功');
        } catch (error) {
            callback(error, null);
        }
    }, 500);
}

riskyOperation((error, result) => {
    if (error) {
        console.error('操作失败:', error.message);
    } else {
        console.log('操作成功:', result);
    }
});

// 回调函数工具函数
class CallbackUtils {
    // 并行执行多个异步操作
    static parallel(tasks, callback) {
        const results = [];
        let completed = 0;
        let hasError = false;
        
        if (tasks.length === 0) {
            callback(null, []);
            return;
        }
        
        tasks.forEach((task, index) => {
            task((error, result) => {
                if (hasError) return;
                
                if (error) {
                    hasError = true;
                    callback(error, null);
                    return;
                }
                
                results[index] = result;
                completed++;
                
                if (completed === tasks.length) {
                    callback(null, results);
                }
            });
        });
    }
    
    // 串行执行多个异步操作
    static series(tasks, callback) {
        const results = [];
        
        function executeTask(index) {
            if (index >= tasks.length) {
                callback(null, results);
                return;
            }
            
            tasks[index]((error, result) => {
                if (error) {
                    callback(error, null);
                    return;
                }
                
                results.push(result);
                executeTask(index + 1);
            });
        }
        
        executeTask(0);
    }
    
    // 限制并发数量
    static parallelLimit(tasks, limit, callback) {
        const results = [];
        let running = 0;
        let completed = 0;
        let index = 0;
        
        function runNext() {
            if (index >= tasks.length && running === 0) {
                callback(null, results);
                return;
            }
            
            while (running < limit && index < tasks.length) {
                const currentIndex = index++;
                const task = tasks[currentIndex];
                
                running++;
                task((error, result) => {
                    running--;
                    completed++;
                    
                    if (error) {
                        callback(error, null);
                        return;
                    }
                    
                    results[currentIndex] = result;
                    runNext();
                });
            }
        }
        
        runNext();
    }
}

// 使用示例
const tasks = [
    (cb) => setTimeout(() => cb(null, 'Task 1'), 100),
    (cb) => setTimeout(() => cb(null, 'Task 2'), 200),
    (cb) => setTimeout(() => cb(null, 'Task 3'), 150)
];

CallbackUtils.parallel(tasks, (error, results) => {
    console.log('并行执行结果:', results);
});

CallbackUtils.series(tasks, (error, results) => {
    console.log('串行执行结果:', results);
});

CallbackUtils.parallelLimit(tasks, 2, (error, results) => {
    console.log('限制并发执行结果:', results);
});
```

### 3. 事件循环机制

```javascript
// 事件循环详解
console.log('1. 同步代码');

setTimeout(() => {
    console.log('2. setTimeout 0ms');
}, 0);

setImmediate(() => {
    console.log('3. setImmediate');
});

process.nextTick(() => {
    console.log('4. process.nextTick');
});

Promise.resolve().then(() => {
    console.log('5. Promise then');
});

console.log('6. 同步代码结束');

// 输出顺序：
// 1. 同步代码
// 6. 同步代码结束
// 4. process.nextTick
// 5. Promise then
// 2. setTimeout 0ms
// 3. setImmediate

// 事件循环阶段详解
// 1. timers: 执行 setTimeout, setInterval 回调
// 2. pending callbacks: 执行系统操作回调
// 3. idle, prepare: 内部使用
// 4. poll: 检索新的 I/O 事件，执行 I/O 回调
// 5. check: 执行 setImmediate 回调
// 6. close callbacks: 执行 close 事件回调

// 详细示例
console.log('同步代码开始');

// timers 阶段
setTimeout(() => {
    console.log('timer1');
}, 0);

setTimeout(() => {
    console.log('timer2');
}, 0);

// check 阶段
setImmediate(() => {
    console.log('immediate1');
});

setImmediate(() => {
    console.log('immediate2');
});

// microtask 队列
process.nextTick(() => {
    console.log('nextTick1');
});

Promise.resolve().then(() => {
    console.log('promise1');
});

Promise.resolve().then(() => {
    console.log('promise2');
});

process.nextTick(() => {
    console.log('nextTick2');
});

console.log('同步代码结束');

// 执行顺序分析：
// 1. 同步代码执行
// 2. nextTick 队列清空
// 3. Promise 微任务队列清空
// 4. timers 阶段
// 5. check 阶段

// 事件循环实际应用
class EventLoopDemo {
    constructor() {
        this.queue = [];
        this.running = false;
    }
    
    // 模拟事件循环
    addTask(task) {
        this.queue.push(task);
        if (!this.running) {
            this.run();
        }
    }
    
    run() {
        this.running = true;
        
        const execute = () => {
            if (this.queue.length > 0) {
                const task = this.queue.shift();
                try {
                    task();
                } catch (error) {
                    console.error('任务执行错误:', error);
                }
                
                // 使用 setImmediate 确保非阻塞
                setImmediate(execute);
            } else {
                this.running = false;
            }
        };
        
        setImmediate(execute);
    }
}

const demo = new EventLoopDemo();
demo.addTask(() => console.log('任务1'));
demo.addTask(() => console.log('任务2'));
demo.addTask(() => console.log('任务3'));
```

### 4. 宏任务和微任务

```javascript
// 宏任务 (Macro Task) 和微任务 (Micro Task)

// 宏任务包括：
// - setTimeout, setInterval
// - setImmediate (Node.js)
// - I/O 操作
// - UI 渲染 (浏览器)

// 微任务包括：
// - Promise.then/catch/finally
// - process.nextTick (Node.js)
// - queueMicrotask
// - MutationObserver (浏览器)

console.log('1. 同步代码');

// 宏任务
setTimeout(() => {
    console.log('2. setTimeout');
}, 0);

// 微任务
Promise.resolve().then(() => {
    console.log('3. Promise then');
});

Promise.resolve().then(() => {
    console.log('4. Promise then 2');
});

// 宏任务
setTimeout(() => {
    console.log('5. setTimeout 2');
}, 0);

console.log('6. 同步代码结束');

// 输出顺序：
// 1. 同步代码
// 6. 同步代码结束
// 3. Promise then
// 4. Promise then 2
// 2. setTimeout
// 5. setTimeout 2

// 复杂示例：宏任务和微任务的嵌套
console.log('Start');

setTimeout(() => {
    console.log('setTimeout 1');
    Promise.resolve().then(() => {
        console.log('Promise in setTimeout 1');
    });
}, 0);

Promise.resolve().then(() => {
    console.log('Promise 1');
    setTimeout(() => {
        console.log('setTimeout in Promise 1');
    }, 0);
});

Promise.resolve().then(() => {
    console.log('Promise 2');
});

setTimeout(() => {
    console.log('setTimeout 2');
}, 0);

console.log('End');

// 输出顺序：
// Start
// End
// Promise 1
// Promise 2
// setTimeout 1
// Promise in setTimeout 1
// setTimeout 2
// setTimeout in Promise 1

// process.nextTick 的特殊性 (Node.js)
console.log('1. Start');

setTimeout(() => {
    console.log('2. setTimeout');
}, 0);

process.nextTick(() => {
    console.log('3. nextTick 1');
});

Promise.resolve().then(() => {
    console.log('4. Promise');
});

process.nextTick(() => {
    console.log('5. nextTick 2');
});

console.log('6. End');

// 输出顺序：
// 1. Start
// 6. End
// 3. nextTick 1
// 5. nextTick 2
// 4. Promise
// 2. setTimeout

// 实际应用：任务调度器
class TaskScheduler {
    constructor() {
        this.microTasks = [];
        this.macroTasks = [];
    }
    
    // 添加微任务
    addMicroTask(task) {
        this.microTasks.push(task);
        if (this.microTasks.length === 1) {
            this.flushMicroTasks();
        }
    }
    
    // 添加宏任务
    addMacroTask(task) {
        this.macroTasks.push(task);
        if (this.macroTasks.length === 1) {
            this.scheduleMacroTask();
        }
    }
    
    // 执行微任务
    flushMicroTasks() {
        Promise.resolve().then(() => {
            while (this.microTasks.length > 0) {
                const task = this.microTasks.shift();
                try {
                    task();
                } catch (error) {
                    console.error('微任务执行错误:', error);
                }
            }
        });
    }
    
    // 调度宏任务
    scheduleMacroTask() {
        setTimeout(() => {
            while (this.macroTasks.length > 0) {
                const task = this.macroTasks.shift();
                try {
                    task();
                } catch (error) {
                    console.error('宏任务执行错误:', error);
                }
            }
        }, 0);
    }
}

const scheduler = new TaskScheduler();

scheduler.addMacroTask(() => console.log('宏任务1'));
scheduler.addMicroTask(() => console.log('微任务1'));
scheduler.addMacroTask(() => console.log('宏任务2'));
scheduler.addMicroTask(() => console.log('微任务2'));
```

## 8.2 Promise 编程

### 1. Promise 状态和生命周期

```javascript
// Promise 的三种状态
// 1. pending (待定) - 初始状态
// 2. fulfilled (已成功) - 操作成功完成
// 3. rejected (已失败) - 操作失败

// 创建 Promise
const promise1 = new Promise((resolve, reject) => {
    console.log('Promise 执行器立即执行');
    resolve('成功');
});

const promise2 = new Promise((resolve, reject) => {
    setTimeout(() => {
        reject(new Error('失败'));
    }, 1000);
});

const promise3 = new Promise((resolve, reject) => {
    // 永远不会改变状态
});

console.log('Promise 创建完成');

// Promise 状态不可逆
const stateDemo = new Promise((resolve, reject) => {
    resolve('第一次调用 resolve');
    reject('第二次调用 reject'); // 无效
    resolve('第三次调用 resolve'); // 无效
});

stateDemo.then(result => {
    console.log('结果:', result); // '第一次调用 resolve'
});

// Promise 状态检查
function checkPromiseState(promise) {
    // 注意：Promise 没有直接的状态检查方法
    // 可以通过 then/catch 来观察状态
    promise.then(
        result => console.log('Promise 成功:', result),
        error => console.log('Promise 失败:', error)
    );
}

// 创建不同状态的 Promise
const resolvedPromise = Promise.resolve('已解决的值');
const rejectedPromise = Promise.reject(new Error('已拒绝的原因'));

checkPromiseState(resolvedPromise); // Promise 成功: 已解决的值
checkPromiseState(rejectedPromise); // Promise 失败: Error: 已拒绝的原因

// Promise 构造函数的实用模式
function createPromiseFromCallback(asyncFunction) {
    return new Promise((resolve, reject) => {
        asyncFunction((error, result) => {
            if (error) {
                reject(error);
            } else {
                resolve(result);
            }
        });
    });
}

// 模拟异步操作
function fakeAsyncOperation(success, delay = 1000) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if (success) {
                resolve(`操作成功，耗时 ${delay}ms`);
            } else {
                reject(new Error('操作失败'));
            }
        }, delay);
    });
}

// 使用示例
fakeAsyncOperation(true)
    .then(result => console.log(result))
    .catch(error => console.error(error));

// Promise 状态转换的详细示例
class PromiseLifecycle {
    static demonstrate() {
        console.log('=== Promise 生命周期演示 ===');
        
        const promise = new Promise((resolve, reject) => {
            console.log('1. 执行器执行 (pending)');
            
            setTimeout(() => {
                const random = Math.random();
                if (random > 0.5) {
                    console.log('2. 调用 resolve (fulfilled)');
                    resolve('成功结果');
                } else {
                    console.log('2. 调用 reject (rejected)');
                    reject(new Error('失败原因'));
                }
            }, 1000);
        });
        
        console.log('3. Promise 对象已创建');
        
        promise
            .then(result => {
                console.log('4. then 处理器执行:', result);
            })
            .catch(error => {
                console.log('4. catch 处理器执行:', error.message);
            })
            .finally(() => {
                console.log('5. finally 处理器总是执行');
            });
        
        return promise;
    }
}

PromiseLifecycle.demonstrate();
```

### 2. Promise 链式调用

```javascript
// Promise 链式调用基础
function step1() {
    console.log('执行步骤1');
    return Promise.resolve('步骤1完成');
}

function step2(data) {
    console.log('执行步骤2，接收到:', data);
    return Promise.resolve(`${data} -> 步骤2完成`);
}

function step3(data) {
    console.log('执行步骤3，接收到:', data);
    return Promise.resolve(`${data} -> 步骤3完成`);
}

// 链式调用
step1()
    .then(step2)
    .then(step3)
    .then(result => {
        console.log('最终结果:', result);
    })
    .catch(error => {
        console.error('错误处理:', error);
    });

// 链式调用中的值传递
Promise.resolve(1)
    .then(value => {
        console.log('第一个 then:', value); // 1
        return value + 1;
    })
    .then(value => {
        console.log('第二个 then:', value); // 2
        return value * 2;
    })
    .then(value => {
        console.log('第三个 then:', value); // 4
        // 不返回值，相当于返回 undefined
    })
    .then(value => {
        console.log('第四个 then:', value); // undefined
        return Promise.resolve('Promise 值');
    })
    .then(value => {
        console.log('第五个 then:', value); // 'Promise 值'
    });

// 链式调用中的错误处理
Promise.resolve('开始')
    .then(value => {
        console.log(value);
        throw new Error('中间步骤出错');
    })
    .then(value => {
        console.log('这不会执行');
        return '正常流程';
    })
    .catch(error => {
        console.log('捕获错误:', error.message);
        return '错误恢复后的值';
    })
    .then(value => {
        console.log('恢复后继续执行:', value);
        return '最终结果';
    })
    .then(value => {
        console.log('最后结果:', value);
    });

// 链式调用中的异步操作
function fetchUserData(userId) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if (userId > 0) {
                resolve({ id: userId, name: `User${userId}` });
            } else {
                reject(new Error('无效用户ID'));
            }
        }, 100);
    });
}

function fetchUserPosts(userId) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve([`Post1 by User${userId}`, `Post2 by User${userId}`]);
        }, 200);
    });
}

function fetchPostComments(post) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve([`Comment1 on ${post}`, `Comment2 on ${post}`]);
        }, 150);
    });
}

// 链式调用解决回调地狱
fetchUserData(1)
    .then(user => {
        console.log('获取用户:', user);
        return fetchUserPosts(user.id);
    })
    .then(posts => {
        console.log('获取帖子:', posts);
        return fetchPostComments(posts[0]);
    })
    .then(comments => {
        console.log('获取评论:', comments);
    })
    .catch(error => {
        console.error('处理过程中出错:', error.message);
    });

// 链式调用中的返回值处理
Promise.resolve('初始值')
    .then(value => {
        // 返回普通值
        return value + ' -> 处理1';
    })
    .then(value => {
        // 返回 Promise
        return Promise.resolve(value + ' -> 处理2');
    })
    .then(value => {
        // 返回新的 Promise
        return new Promise(resolve => {
            setTimeout(() => {
                resolve(value + ' -> 处理3');
            }, 100);
        });
    })
    .then(value => {
        // 抛出错误
        if (value.includes('处理3')) {
            throw new Error('模拟错误');
        }
        return value;
    })
    .then(value => {
        console.log('这不会执行');
    })
    .catch(error => {
        console.log('捕获错误:', error.message);
        // 返回值继续链式调用
        return '错误处理完成';
    })
    .then(value => {
        console.log('最终结果:', value);
    });

// 高级链式调用示例
class DataProcessor {
    static process(data) {
        return Promise.resolve(data)
            .then(this.validate)
            .then(this.transform)
            .then(this.enrich)
            .catch(this.handleError);
    }
    
    static validate(data) {
        console.log('验证数据:', data);
        if (!data || typeof data !== 'object') {
            throw new Error('数据格式无效');
        }
        return data;
    }
    
    static transform(data) {
        console.log('转换数据:', data);
        return {
            ...data,
            processed: true,
            timestamp: new Date().toISOString()
        };
    }
    
    static enrich(data) {
        console.log('丰富数据:', data);
        return new Promise(resolve => {
            setTimeout(() => {
                resolve({
                    ...data,
                    enriched: true,
                    version: '1.0'
                });
            }, 100);
        });
    }
    
    static handleError(error) {
        console.error('处理错误:', error.message);
        return {
            error: error.message,
            fallback: true
        };
    }
}

// 使用示例
DataProcessor.process({ id: 1, name: 'Test' })
    .then(result => {
        console.log('处理结果:', result);
    });

DataProcessor.process(null)
    .then(result => {
        console.log('错误处理结果:', result);
    });
```

### 3. Promise 组合方法

```javascript
// Promise 组合方法

// Promise.all() - 所有 Promise 都成功才成功
const promises = [
    Promise.resolve('结果1'),
    Promise.resolve('结果2'),
    Promise.resolve('结果3')
];

Promise.all(promises)
    .then(results => {
        console.log('所有结果:', results); // ['结果1', '结果2', '结果3']
    })
    .catch(error => {
        console.error('其中一个失败:', error);
    });

// Promise.all() 失败示例
const mixedPromises = [
    Promise.resolve('成功1'),
    Promise.reject(new Error('失败')),
    Promise.resolve('成功2')
];

Promise.all(mixedPromises)
    .then(results => {
        console.log('这不会执行');
    })
    .catch(error => {
        console.log('捕获到错误:', error.message); // '失败'
    });

// Promise.allSettled() - 等待所有 Promise 完成（无论成功或失败）
const mixedPromises2 = [
    Promise.resolve('成功1'),
    Promise.reject(new Error('失败1')),
    Promise.resolve('成功2'),
    Promise.reject(new Error('失败2'))
];

Promise.allSettled(mixedPromises2)
    .then(results => {
        console.log('所有 Promise 状态:');
        results.forEach((result, index) => {
            if (result.status === 'fulfilled') {
                console.log(`Promise ${index}: 成功 - ${result.value}`);
            } else {
                console.log(`Promise ${index}: 失败 - ${result.reason.message}`);
            }
        });
    });

// Promise.race() - 返回第一个完成的 Promise
const fastPromise = new Promise(resolve => {
    setTimeout(() => resolve('快速完成'), 100);
});

const slowPromise = new Promise(resolve => {
    setTimeout(() => resolve('慢速完成'), 1000);
});

Promise.race([fastPromise, slowPromise])
    .then(result => {
        console.log('最先完成:', result); // '快速完成'
    });

// Promise.race() 超时控制
function withTimeout(promise, timeout) {
    const timeoutPromise = new Promise((_, reject) => {
        setTimeout(() => reject(new Error('操作超时')), timeout);
    });
    
    return Promise.race([promise, timeoutPromise]);
}

// 使用示例
const slowOperation = new Promise(resolve => {
    setTimeout(() => resolve('慢操作完成'), 2000);
});

withTimeout(slowOperation, 1000)
    .then(result => {
        console.log('操作完成:', result);
    })
    .catch(error => {
        console.log('操作失败:', error.message); // '操作超时'
    });

// Promise.any() - 返回第一个成功的 Promise (ES2021)
const promisesWithErrors = [
    Promise.reject(new Error('错误1')),
    Promise.reject(new Error('错误2')),
    Promise.resolve('第一个成功'),
    Promise.resolve('第二个成功')
];

Promise.any(promisesWithErrors)
    .then(result => {
        console.log('第一个成功的结果:', result); // '第一个成功'
    })
    .catch(error => {
        console.log('所有都失败:', error.errors);
    });

// Promise.any() 全部失败示例
const allFailures = [
    Promise.reject(new Error('错误1')),
    Promise.reject(new Error('错误2'))
];

Promise.any(allFailures)
    .then(result => {
        console.log('这不会执行');
    })
    .catch(error => {
        console.log('所有都失败:', error.errors); // [Error: 错误1, Error: 错误2]
    });

// 实际应用：并发请求处理
class ConcurrentRequestHandler {
    static async fetchMultipleUrls(urls) {
        const fetchPromises = urls.map(url => 
            fetch(url).catch(error => ({ error, url }))
        );
        
        const results = await Promise.allSettled(fetchPromises);
        
        return results.map((result, index) => ({
            url: urls[index],
            status: result.status,
            ...(result.status === 'fulfilled' 
                ? { data: result.value } 
                : { error: result.reason })
        }));
    }
    
    static async fetchWithTimeout(urls, timeout = 5000) {
        const fetchPromises = urls.map(url => 
            Promise.race([
                fetch(url),
                new Promise((_, reject) => 
                    setTimeout(() => reject(new Error(`请求超时: ${url}`)), timeout)
                )
            ]).catch(error => ({ error, url }))
        );
        
        return Promise.all(fetchPromises);
    }
    
    static async fetchFastest(urls) {
        const fetchPromises = urls.map(url => fetch(url));
        return Promise.race(fetchPromises);
    }
}

// 使用示例
const urls = [
    'https://api.github.com/users/octocat',
    'https://api.github.com/users/torvalds',
    'https://api.github.com/users/gvanrossum'
];

// ConcurrentRequestHandler.fetchMultipleUrls(urls)
//     .then(results => {
//         results.forEach(result => {
//             console.log(`${result.url}: ${result.status}`);
//         });
//     });

// 实用的 Promise 组合工具
class PromiseCombinators {
    // 限制并发数量的 Promise.all
    static async allLimit(promises, limit) {
        const results = [];
        const executing = [];
        
        for (const [index, promise] of promises.entries()) {
            const p = Promise.resolve(promise).then(result => {
                results[index] = result;
            });
            
            executing.push(p);
            
            if (executing.length >= limit) {
                await Promise.race(executing);
                executing.splice(executing.findIndex(p => p === Promise.race(executing)), 1);
            }
        }
        
        await Promise.all(executing);
        return results;
    }
    
    // 重试机制
    static retry(promiseFunction, retries = 3) {
        return new Promise((resolve, reject) => {
            const attempt = (n) => {
                promiseFunction()
                    .then(resolve)
                    .catch(error => {
                        if (n === 1) {
                            reject(error);
                        } else {
                            console.log(`重试 ${retries - n + 1}/${retries}`);
                            setTimeout(() => attempt(n - 1), 1000);
                        }
                    });
            };
            
            attempt(retries);
        });
    }
    
    // 超时控制
    static timeout(promise, ms) {
        return Promise.race([
            promise,
            new Promise((_, reject) => 
                setTimeout(() => reject(new Error('操作超时')), ms)
            )
        ]);
    }
    
    // 批量处理
    static batch(processFunction, items, batchSize = 10) {
        const batches = [];
        for (let i = 0; i < items.length; i += batchSize) {
            batches.push(items.slice(i, i + batchSize));
        }
        
        return batches.reduce(async (chain, batch) => {
            const results = await chain;
            const batchResults = await Promise.all(
                batch.map(item => processFunction(item))
            );
            return [...results, ...batchResults];
        }, Promise.resolve([]));
    }
}

// 使用示例
const flakyOperation = () => {
    return new Promise((resolve, reject) => {
        if (Math.random() > 0.7) {
            resolve('成功');
        } else {
            reject(new Error('随机失败'));
        }
    });
};

PromiseCombinators.retry(flakyOperation, 3)
    .then(result => console.log('重试成功:', result))
    .catch(error => console.log('重试失败:', error.message));

const slowOperation = new Promise(resolve => {
    setTimeout(() => resolve('慢操作'), 2000);
});

PromiseCombinators.timeout(slowOperation, 1000)
    .then(result => console.log('操作完成:', result))
    .catch(error => console.log('操作超时:', error.message));
```

### 4. 错误处理机制

```javascript
// Promise 错误处理机制

// 基本错误处理
Promise.reject(new Error('测试错误'))
    .then(result => {
        console.log('这不会执行');
    })
    .catch(error => {
        console.log('捕获错误:', error.message); // '测试错误'
    })
    .finally(() => {
        console.log('清理工作');
    });

// 链式调用中的错误处理
Promise.resolve('开始')
    .then(value => {
        console.log(value);
        throw new Error('中间错误');
    })
    .then(value => {
        console.log('这不会执行');
    })
    .catch(error => {
        console.log('捕获错误:', error.message);
        // 可以返回值继续链式调用
        return '错误恢复';
    })
    .then(value => {
        console.log('恢复后继续:', value); // '错误恢复'
    });

// 多层错误处理
Promise.resolve('开始')
    .then(value => {
        console.log(value);
        throw new Error('第一层错误');
    })
    .catch(error => {
        console.log('第一层捕获:', error.message);
        // 可以重新抛出错误
        throw new Error('第二层错误');
    })
    .catch(error => {
        console.log('第二层捕获:', error.message);
        // 返回正常值
        return '恢复正常';
    })
    .then(value => {
        console.log('最终结果:', value);
    });

// Promise.all 中的错误处理
const promises = [
    Promise.resolve('成功1'),
    Promise.reject(new Error('失败1')),
    Promise.resolve('成功2'),
    Promise.reject(new Error('失败2'))
];

Promise.all(promises)
    .then(results => {
        console.log('这不会执行');
    })
    .catch(error => {
        console.log('Promise.all 错误:', error.message); // '失败1' (第一个错误)
    });

// Promise.allSettled 的错误处理
Promise.allSettled(promises)
    .then(results => {
        const errors = results
            .filter(result => result.status === 'rejected')
            .map(result => result.reason.message);
        
        if (errors.length > 0) {
            console.log('部分操作失败:', errors);
        }
        
        const successes = results
            .filter(result => result.status === 'fulfilled')
            .map(result => result.value);
        
        console.log('成功的结果:', successes);
    });

// 异步函数中的错误处理
async function asyncWithErrorHandling() {
    try {
        const result = await Promise.reject(new Error('异步错误'));
        console.log('这不会执行');
    } catch (error) {
        console.log('异步捕获错误:', error.message);
        return '错误处理完成';
    }
}

asyncWithErrorHandling().then(result => {
    console.log('异步函数结果:', result);
});

// 未处理的 Promise 错误
// Node.js 会发出警告
Promise.reject(new Error('未处理的错误'));
// (node:1234) UnhandledPromiseRejectionWarning: Error: 未处理的错误

// 正确处理未处理的错误
process.on('unhandledRejection', (reason, promise) => {
    console.log('未处理的 Promise 拒绝:', reason);
    // 可以在这里进行错误记录或清理工作
});

// 实际应用：API 错误处理
class APIError extends Error {
    constructor(message, status, url) {
        super(message);
        this.status = status;
        this.url = url;
        this.name = 'APIError';
    }
}

class APIClient {
    static async fetchWithErrorHandling(url) {
        try {
            const response = await fetch(url);
            
            if (!response.ok) {
                throw new APIError(
                    `HTTP ${response.status}: ${response.statusText}`,
                    response.status,
                    url
                );
            }
            
            const data = await response.json();
            return data;
        } catch (error) {
            if (error instanceof APIError) {
                throw error; // 重新抛出 API 错误
            } else {
                // 网络错误或其他错误
                throw new APIError(
                    `网络错误: ${error.message}`,
                    0,
                    url
                );
            }
        }
    }
    
    static async fetchWithRetry(url, retries = 3) {
        for (let i = 0; i < retries; i++) {
            try {
                return await this.fetchWithErrorHandling(url);
            } catch (error) {
                console.log(`请求失败 (${i + 1}/${retries}):`, error.message);
                
                if (i === retries - 1) {
                    throw error; // 最后一次重试仍然失败
                }
                
                // 等待后重试
                await new Promise(resolve => setTimeout(resolve, 1000 * (i + 1)));
            }
        }
    }
}

// 错误处理最佳实践
class ErrorHandler {
    // 统一错误处理
    static async handleAsync(asyncFunction, fallbackValue = null) {
        try {
            return await asyncFunction();
        } catch (error) {
            console.error('操作失败:', error);
            
            // 记录错误日志
            this.logError(error);
            
            // 返回默认值而不是抛出错误
            return fallbackValue;
        }
    }
    
    // 错误日志记录
    static logError(error) {
        const errorInfo = {
            message: error.message,
            stack: error.stack,
            timestamp: new Date().toISOString(),
            type: error.constructor.name
        };
        
        // 在实际应用中，这里可以发送到错误监控服务
        console.error('错误日志:', JSON.stringify(errorInfo, null, 2));
    }
    
    // 优雅降级
    static async withFallback(primaryFunction, fallbackFunction) {
        try {
            return await primaryFunction();
        } catch (error) {
            console.warn('主操作失败，使用备用方案:', error.message);
            return await fallbackFunction();
        }
    }
    
    // 错误分类处理
    static categorizeAndHandle(error) {
        if (error instanceof TypeError) {
            console.error('类型错误:', error.message);
        } else if (error instanceof ReferenceError) {
            console.error('引用错误:', error.message);
        } else if (error.message.includes('timeout')) {
            console.error('超时错误:', error.message);
        } else {
            console.error('未知错误:', error.message);
        }
    }
}

// 使用示例
ErrorHandler.handleAsync(
    () => Promise.reject(new Error('测试错误')),
    '默认值'
).then(result => {
    console.log('处理结果:', result); // '默认值'
});

// 错误边界模式（模拟）
class ErrorBoundary {
    constructor() {
        this.errors = [];
    }
    
    async executeWithErrorBoundary(asyncFunction) {
        try {
            return await asyncFunction();
        } catch (error) {
            this.errors.push(error);
            
            // 根据错误类型决定是否继续执行
            if (this.isRecoverable(error)) {
                console.log('可恢复错误，继续执行');
                return null;
            } else {
                console.log('不可恢复错误，停止执行');
                throw error;
            }
        }
    }
    
    isRecoverable(error) {
        // 简单的错误分类逻辑
        const recoverableErrors = ['timeout', 'network', 'temporary'];
        return recoverableErrors.some(keyword => 
            error.message.toLowerCase().includes(keyword)
        );
    }
    
    getErrorCount() {
        return this.errors.length;
    }
    
    clearErrors() {
        this.errors = [];
    }
}

const errorBoundary = new ErrorBoundary();

// 测试可恢复错误
errorBoundary.executeWithErrorBoundary(() => 
    Promise.reject(new Error('temporary network error'))
).then(result => {
    console.log('可恢复操作结果:', result);
});

// 测试不可恢复错误
errorBoundary.executeWithErrorBoundary(() => 
    Promise.reject(new Error('critical database error'))
).catch(error => {
    console.log('不可恢复错误:', error.message);
});
```

## 8.3 现代异步语法

### 1. async/await 语法糖

```javascript
// async/await 基础语法

// async 函数声明
async function fetchData() {
    try {
        console.log('开始获取数据');
        const response = await fetch('https://api.github.com/users/octocat');
        const data = await response.json();
        console.log('数据获取完成');
        return data;
    } catch (error) {
        console.error('获取数据失败:', error);
        throw error;
    }
}

// async 函数表达式
const fetchDataExpression = async function() {
    const response = await fetch('https://api.github.com/users/octocat');
    return response.json();
};

// async 箭头函数
const fetchDataArrow = async () => {
    const response = await fetch('https://api.github.com/users/octocat');
    return response.json();
};

// async 方法
class DataFetcher {
    async fetchUser(username) {
        const response = await fetch(`https://api.github.com/users/${username}`);
        return response.json();
    }
    
    async fetchMultipleUsers(usernames) {
        const users = [];
        for (const username of usernames) {
            const user = await this.fetchUser(username);
            users.push(user);
        }
        return users;
    }
}

// async 函数总是返回 Promise
async function asyncFunction() {
    return 'async result';
}

console.log(asyncFunction() instanceof Promise); // true
asyncFunction().then(result => {
    console.log(result); // 'async result'
});

// await 只能在 async 函数内部使用
// 错误示例（会报语法错误）
// const result = await Promise.resolve('outside async');

// 正确示例
async function useAwait() {
    const result = await Promise.resolve('inside async');
    console.log(result);
}

// async/await 与 Promise 的转换
// 使用 Promise
function withPromise() {
    return fetch('https://api.github.com/users/octocat')
        .then(response => response.json())
        .then(data => {
            console.log(data);
            return data;
        })
        .catch(error => {
            console.error(error);
            throw error;
        });
}

// 使用 async/await
async function withAsyncAwait() {
    try {
        const response = await fetch('https://api.github.com/users/octocat');
        const data = await response.json();
        console.log(data);
        return data;
    } catch (error) {
        console.error(error);
        throw error;
    }
}

// 实际应用：用户数据处理
class UserService {
    async getUser(userId) {
        console.log(`获取用户 ${userId}`);
        const response = await fetch(`/api/users/${userId}`);
        if (!response.ok) {
            throw new Error(`获取用户失败: ${response.status}`);
        }
        return response.json();
    }
    
    async updateUser(userId, userData) {
        console.log(`更新用户 ${userId}`);
        const response = await fetch(`/api/users/${userId}`, {
            method: 'PUT',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(userData)
        });
        
        if (!response.ok) {
            throw new Error(`更新用户失败: ${response.status}`);
        }
        
        return response.json();
    }
    
    async processUser(userId) {
        try {
            const user = await this.getUser(userId);
            console.log('用户信息:', user);
            
            const updatedUser = await this.updateUser(userId, {
                ...user,
                lastUpdated: new Date().toISOString()
            });
            
            console.log('更新后的用户:', updatedUser);
            return updatedUser;
        } catch (error) {
            console.error('处理用户失败:', error);
            throw error;
        }
    }
}

// 使用示例
const userService = new UserService();
// userService.processUser(123);

// async/await 错误处理对比
// Promise 方式
function handleWithPromise() {
    return fetch('/api/data')
        .then(response => {
            if (!response.ok) {
                throw new Error('网络错误');
            }
            return response.json();
        })
        .then(data => {
            return processData(data);
        })
        .catch(error => {
            console.error('处理失败:', error);
            return { error: error.message };
        });
}

// async/await 方式
async function handleWithAsyncAwait() {
    try {
        const response = await fetch('/api/data');
        if (!response.ok) {
            throw new Error('网络错误');
        }
        
        const data = await response.json();
        return await processData(data);
    } catch (error) {
        console.error('处理失败:', error);
        return { error: error.message };
    }
}

// 模拟数据处理
async function processData(data) {
    // 模拟异步处理
    await new Promise(resolve => setTimeout(resolve, 100));
    return { ...data, processed: true };
}
```

### 2. 异步函数错误处理

```javascript
// 异步函数错误处理

// try/catch 基本用法
async function basicErrorHandling() {
    try {
        const result = await Promise.reject(new Error('测试错误'));
        console.log('这不会执行');
    } catch (error) {
        console.log('捕获错误:', error.message);
    }
}

// 多层 try/catch
async function nestedErrorHandling() {
    try {
        await firstOperation();
    } catch (error) {
        console.log('第一层错误处理:', error.message);
        try {
            await fallbackOperation();
        } catch (fallbackError) {
            console.log('备用操作也失败:', fallbackError.message);
            throw new Error('所有操作都失败');
        }
    }
}

async function firstOperation() {
    throw new Error('主要操作失败');
}

async function fallbackOperation() {
    throw new Error('备用操作失败');
}

// 错误类型检查
async function typeSpecificErrorHandling() {
    try {
        const result = await riskyOperation();
        return result;
    } catch (error) {
        if (error instanceof TypeError) {
            console.error('类型错误:', error.message);
        } else if (error instanceof ReferenceError) {
            console.error('引用错误:', error.message);
        } else if (error.message.includes('network')) {
            console.error('网络错误:', error.message);
            // 可以进行重试
            return await retryOperation();
        } else {
            console.error('未知错误:', error.message);
            throw error; // 重新抛出未知错误
        }
    }
}

async function riskyOperation() {
    const random = Math.random();
    if (random < 0.3) {
        throw new TypeError('类型错误示例');
    } else if (random < 0.6) {
        throw new Error('network timeout');
    } else {
        throw new Error('其他错误');
    }
}

async function retryOperation() {
    console.log('重试操作');
    return '重试成功';
}

// finally 块的使用
async function withFinally() {
    try {
        console.log('开始操作');
        const result = await Promise.resolve('成功结果');
        console.log('操作成功');
        return result;
    } catch (error) {
        console.log('操作失败:', error.message);
        throw error;
    } finally {
        console.log('清理资源');
        // 这里的代码总是会执行
    }
}

// 错误传播
async function errorPropagation() {
    const result = await level1();
    console.log('最终结果:', result);
}

async function level1() {
    return await level2();
}

async function level2() {
    return await level3();
}

async function level3() {
    throw new Error('深层错误');
}

// 错误边界模式
class AsyncErrorBoundary {
    constructor() {
        this.errorCount = 0;
    }
    
    async execute(asyncFunction, retries = 3) {
        for (let i = 0; i < retries; i++) {
            try {
                return await asyncFunction();
            } catch (error) {
                this.errorCount++;
                console.log(`尝试 ${i + 1} 失败:`, error.message);
                
                if (i === retries - 1) {
                    console.log('所有重试都失败');
                    throw error;
                }
                
                // 等待后重试
                await this.delay(1000 * (i + 1));
            }
        }
    }
    
    async delay(ms) {
        return new Promise(resolve => setTimeout(resolve, ms));
    }
    
    getErrorCount() {
        return this.errorCount;
    }
}

// 使用示例
const errorBoundary = new AsyncErrorBoundary();

async function flakyOperation() {
    if (Math.random() < 0.7) {
        throw new Error('随机失败');
    }
    return '成功';
}

// errorBoundary.execute(flakyOperation)
//     .then(result => console.log('最终结果:', result))
//     .catch(error => console.log('最终失败:', error.message));

// 统一错误处理装饰器模式
function withErrorHandling(target, propertyName, descriptor) {
    const method = descriptor.value;
    
    descriptor.value = async function(...args) {
        try {
            return await method.apply(this, args);
        } catch (error) {
            console.error(`方法 ${propertyName} 执行失败:`, error.message);
            
            // 可以在这里添加统一的错误处理逻辑
            this.handleError?.(error);
            
            throw error;
        }
    };
    
    return descriptor;
}

class ServiceWithLogging {
    @withErrorHandling
    async fetchData() {
        throw new Error('服务错误');
    }
    
    handleError(error) {
        console.log('统一错误处理:', error.message);
    }
}

// 实际应用：API 客户端错误处理
class APIClient {
    constructor(baseURL) {
        this.baseURL = baseURL;
    }
    
    async request(endpoint, options = {}) {
        const url = `${this.baseURL}${endpoint}`;
        
        try {
            console.log(`请求: ${url}`);
            const response = await fetch(url, options);
            
            if (!response.ok) {
                const errorData = await response.json().catch(() => ({}));
                throw new Error(`HTTP ${response.status}: ${errorData.message || response.statusText}`);
            }
            
            const data = await response.json();
            console.log(`响应: ${url}`, data);
            return data;
        } catch (error) {
            console.error(`请求失败: ${url}`, error);
            
            // 根据错误类型进行不同处理
            if (error.name === 'TypeError' && error.message.includes('fetch')) {
                throw new Error('网络连接失败，请检查网络');
            }
            
            throw error;
        }
    }
    
    async get(endpoint) {
        return this.request(endpoint, { method: 'GET' });
    }
    
    async post(endpoint, data) {
        return this.request(endpoint, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(data)
        });
    }
    
    async withRetry(asyncFunction, maxRetries = 3) {
        for (let i = 0; i < maxRetries; i++) {
            try {
                return await asyncFunction();
            } catch (error) {
                console.log(`重试 ${i + 1}/${maxRetries}:`, error.message);
                
                if (i === maxRetries - 1) {
                    throw error;
                }
                
                await this.delay(1000 * Math.pow(2, i)); // 指数退避
            }
        }
    }
    
    delay(ms) {
        return new Promise(resolve => setTimeout(resolve, ms));
    }
}

// 使用示例
const apiClient = new APIClient('https://api.example.com');

async function fetchUserData() {
    try {
        const user = await apiClient.withRetry(() => 
            apiClient.get('/users/123')
        );
        console.log('用户数据:', user);
    } catch (error) {
        console.error('获取用户数据失败:', error.message);
    }
}
```

### 3. 并行和串行执行

```javascript
// 并行和串行执行

// 串行执行 - 一个接一个执行
async function serialExecution() {
    console.log('开始串行执行');
    
    const result1 = await operation1();
    console.log('操作1完成:', result1);
    
    const result2 = await operation2();
    console.log('操作2完成:', result2);
    
    const result3 = await operation3();
    console.log('操作3完成:', result3);
    
    return [result1, result2, result3];
}

// 并行执行 - 同时执行多个操作
async function parallelExecution() {
    console.log('开始并行执行');
    
    // 同时启动所有操作
    const [result1, result2, result3] = await Promise.all([
        operation1(),
        operation2(),
        operation3()
    ]);
    
    console.log('所有操作完成');
    console.log('结果1:', result1);
    console.log('结果2:', result2);
    console.log('结果3:', result3);
    
    return [result1, result2, result3];
}

// 模拟异步操作
function operation1() {
    return new Promise(resolve => {
        setTimeout(() => resolve('操作1结果'), 1000);
    });
}

function operation2() {
    return new Promise(resolve => {
        setTimeout(() => resolve('操作2结果'), 1500);
    });
}

function operation3() {
    return new Promise(resolve => {
        setTimeout(() => resolve('操作3结果'), 800);
    });
}

// 性能对比
async function performanceComparison() {
    console.log('=== 性能对比 ===');
    
    // 串行执行
    console.time('串行执行');
    await serialExecution();
    console.timeEnd('串行执行'); // 约 3300ms
    
    // 并行执行
    console.time('并行执行');
    await parallelExecution();
    console.timeEnd('并行执行'); // 约 1500ms
}

// 限制并发数量
async function limitedParallelExecution(tasks, limit = 3) {
    const results = [];
    
    for (let i = 0; i < tasks.length; i += limit) {
        const batch = tasks.slice(i, i + limit);
        const batchResults = await Promise.all(
            batch.map(task => task())
        );
        results.push(...batchResults);
        console.log(`批次 ${Math.floor(i/limit) + 1} 完成`);
    }
    
    return results;
}

// 使用示例
const tasks = [
    () => operation1(),
    () => operation2(),
    () => operation3(),
    () => operation1(),
    () => operation2()
];

// limitedParallelExecution(tasks, 2);

// 混合执行模式 - 部分并行，部分串行
async function mixedExecution() {
    console.log('开始混合执行');
    
    // 先并行执行一组操作
    const [user, permissions] = await Promise.all([
        fetchUser(),
        fetchPermissions()
    ]);
    
    console.log('用户和权限获取完成');
    
    // 基于前面的结果串行执行后续操作
    const profile = await fetchProfile(user.id);
    const preferences = await fetchPreferences(user.id);
    
    console.log('详细信息获取完成');
    
    return {
        user,
        permissions,
        profile,
        preferences
    };
}

async function fetchUser() {
    await delay(500);
    return { id: 1, name: 'John' };
}

async function fetchPermissions() {
    await delay(300);
    return ['read', 'write'];
}

async function fetchProfile(userId) {
    await delay(400);
    return { avatar: 'avatar.jpg', bio: 'Developer' };
}

async function fetchPreferences(userId) {
    await delay(200);
    return { theme: 'dark', language: 'en' };
}

async function delay(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

// 实际应用：批量数据处理
class BatchProcessor {
    constructor() {
        this.processedCount = 0;
        this.errorCount = 0;
    }
    
    // 串行处理
    async processSerial(items, processor) {
        const results = [];
        
        for (const item of items) {
            try {
                const result = await processor(item);
                results.push(result);
                this.processedCount++;
            } catch (error) {
                console.error(`处理项目失败:`, error);
                this.errorCount++;
                results.push(null); // 或者抛出错误
            }
        }
        
        return results;
    }
    
    // 并行处理
    async processParallel(items, processor, concurrency = 5) {
        const results = new Array(items.length);
        
        // 分批处理
        for (let i = 0; i < items.length; i += concurrency) {
            const batch = items.slice(i, i + concurrency);
            const batchPromises = batch.map((item, index) => 
                processor(item).then(
                    result => ({ success: true, result, originalIndex: i + index }),
                    error => ({ success: false, error, originalIndex: i + index })
                )
            );
            
            const batchResults = await Promise.all(batchPromises);
            
            batchResults.forEach(({ success, result, error, originalIndex }) => {
                if (success) {
                    results[originalIndex] = result;
                    this.processedCount++;
                } else {
                    console.error(`处理项目失败:`, error);
                    results[originalIndex] = null;
                    this.errorCount++;
                }
            });
        }
        
        return results;
    }
    
    // 流水线处理 - 保持最大并发数
    async processPipeline(items, processor, concurrency = 5) {
        const results = [];
        const executing = [];
        
        for (const item of items) {
            const promise = processor(item)
                .then(result => {
                    results.push({ success: true, result, item });
                    this.processedCount++;
                })
                .catch(error => {
                    results.push({ success: false, error, item });
                    this.errorCount++;
                })
                .finally(() => {
                    const index = executing.indexOf(promise);
                    if (index > -1) {
                        executing.splice(index, 1);
                    }
                });
            
            executing.push(promise);
            
            if (executing.length >= concurrency) {
                await Promise.race(executing);
            }
        }
        
        await Promise.all(executing);
        return results;
    }
    
    getStats() {
        return {
            processed: this.processedCount,
            errors: this.errorCount,
            successRate: this.processedCount > 0 
                ? ((this.processedCount - this.errorCount) / this.processedCount * 100).toFixed(2) + '%'
                : '0%'
        };
    }
    
    resetStats() {
        this.processedCount = 0;
        this.errorCount = 0;
    }
}

// 使用示例
const processor = new BatchProcessor();

// 模拟处理函数
async function processItem(item) {
    // 模拟随机处理时间
    await delay(Math.random() * 1000);
    
    // 模拟随机失败
    if (Math.random() < 0.1) {
        throw new Error(`处理 ${item} 失败`);
    }
    
    return `处理完成: ${item}`;
}

const items = Array.from({ length: 20 }, (_, i) => `项目${i + 1}`);

// 串行处理
console.log('=== 串行处理 ===');
processor.resetStats();
// const serialResults = await processor.processSerial(items, processItem);
// console.log('串行结果:', processor.getStats());

// 并行处理
console.log('=== 并行处理 ===');
processor.resetStats();
// const parallelResults = await processor.processParallel(items, processItem, 5);
// console.log('并行结果:', processor.getStats());

// 流水线处理
console.log('=== 流水线处理 ===');
processor.resetStats();
// const pipelineResults = await processor.processPipeline(items, processItem, 5);
// console.log('流水线结果:', processor.getStats());

// 高级并行控制：依赖图执行
class DependencyExecutor {
    constructor() {
        this.results = new Map();
        this.executing = new Set();
    }
    
    async execute(tasks) {
        const results = {};
        
        // 找到没有依赖的任务
        const readyTasks = Object.keys(tasks).filter(
            name => !tasks[name].dependencies || tasks[name].dependencies.length === 0
        );
        
        // 并行执行没有依赖的任务
        await Promise.all(
            readyTasks.map(name => this.executeTask(name, tasks, results))
        );
        
        return results;
    }
    
    async executeTask(name, tasks, results) {
        if (this.results.has(name)) {
            return this.results.get(name);
        }
        
        if (this.executing.has(name)) {
            // 等待正在执行的任务
            return new Promise(resolve => {
                const check = () => {
                    if (this.results.has(name)) {
                        resolve(this.results.get(name));
                    } else {
                        setTimeout(check, 10);
                    }
                };
                check();
            });
        }
        
        this.executing.add(name);
        
        try {
            const task = tasks[name];
            
            // 等待依赖任务完成
            if (task.dependencies && task.dependencies.length > 0) {
                await Promise.all(
                    task.dependencies.map(dep => 
                        this.executeTask(dep, tasks, results)
                    )
                );
            }
            
            // 执行当前任务
            const result = await task.fn();
            this.results.set(name, result);
            results[name] = result;
            
            return result;
        } finally {
            this.executing.delete(name);
        }
    }
}

// 使用示例
const dependencyExecutor = new DependencyExecutor();

const tasks = {
    'fetchUser': {
        fn: () => delay(500).then(() => ({ id: 1, name: 'John' })),
        dependencies: []
    },
    'fetchPermissions': {
        fn: () => delay(300).then(() => ['read', 'write']),
        dependencies: []
    },
    'fetchProfile': {
        fn: () => delay(400).then(() => ({ avatar: 'avatar.jpg' })),
        dependencies: ['fetchUser']
    },
    'generateReport': {
        fn: () => delay(600).then(() => '报告生成完成'),
        dependencies: ['fetchUser', 'fetchPermissions', 'fetchProfile']
    }
};

// dependencyExecutor.execute(tasks).then(results => {
//     console.log('依赖执行结果:', results);
// });
```

### 4. 异步迭代器

```javascript
// 异步迭代器 (Async Iterator) 和异步生成器 (Async Generator)

// 异步迭代器基础
class AsyncCounter {
    constructor(max) {
        this.max = max;
        this.current = 0;
    }
    
    [Symbol.asyncIterator]() {
        return {
            next: async () => {
                await this.delay(100); // 模拟异步操作
                
                if (this.current < this.max) {
                    return {
                        value: this.current++,
                        done: false
                    };
                } else {
                    return {
                        value: undefined,
                        done: true
                    };
                }
            }
        };
    }
    
    delay(ms) {
        return new Promise(resolve => setTimeout(resolve, ms));
    }
}

// 使用 for-await-of 循环
async function useAsyncCounter() {
    console.log('开始异步计数');
    
    const counter = new AsyncCounter(5);
    
    for await (const value of counter) {
        console.log('计数值:', value);
    }
    
    console.log('计数完成');
}

// useAsyncCounter();

// 异步生成器函数
async function* asyncNumberGenerator(max) {
    for (let i = 0; i < max; i++) {
        await delay(100); // 模拟异步操作
        yield i;
    }
}

async function useAsyncGenerator() {
    console.log('使用异步生成器');
    
    for await (const value of asyncNumberGenerator(5)) {
        console.log('生成值:', value);
    }
    
    console.log('生成完成');
}

function delay(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

// useAsyncGenerator();

// 实际应用：异步数据流处理
async function* fetchPaginatedData(url, maxPages = 10) {
    let page = 1;
    let hasMore = true;
    
    while (hasMore && page <= maxPages) {
        try {
            console.log(`获取第 ${page} 页数据`);
            
            // 模拟 API 调用
            const response = await fetch(`${url}?page=${page}`);
            const data = await response.json();
            
            // 检查是否还有更多数据
            hasMore = data.hasMore;
            page++;
            
            yield data.items;
            
            // 添加延迟避免过于频繁的请求
            await delay(100);
        } catch (error) {
            console.error(`获取第 ${page} 页失败:`, error);
            break;
        }
    }
}

// 使用异步生成器处理分页数据
async function processPaginatedData() {
    console.log('开始处理分页数据');
    
    let totalCount = 0;
    
    for await (const items of fetchPaginatedData('/api/data')) {
        console.log(`处理 ${items.length} 个项目`);
        totalCount += items.length;
        
        // 处理每个项目
        for (const item of items) {
            await processItem(item);
        }
    }
    
    console.log(`总共处理了 ${totalCount} 个项目`);
}

async function processItem(item) {
    // 模拟项目处理
    await delay(10);
    // console.log('处理项目:', item);
}

// 异步生成器的实际应用：文件读取
const fs = require('fs').promises;
const { createReadStream } = require('fs');
const { createInterface } = require('readline');

async function* readLines(filename) {
    const fileStream = createReadStream(filename);
    const rl = createInterface({
        input: fileStream,
        crlfDelay: Infinity
    });
    
    for await (const line of rl) {
        yield line;
    }
}

// 使用示例
async function processFile() {
    try {
        for await (const line of readLines('large-file.txt')) {
            // 处理每一行
            console.log('处理行:', line.substring(0, 50));
        }
    } catch (error) {
        console.error('文件处理失败:', error);
    }
}

// 异步迭代器组合和转换
async function* mapAsync(asyncIterable, mapper) {
    for await (const item of asyncIterable) {
        yield await mapper(item);
    }
}

async function* filterAsync(asyncIterable, predicate) {
    for await (const item of asyncIterable) {
        if (await predicate(item)) {
            yield item;
        }
    }
}

async function* takeAsync(asyncIterable, count) {
    let taken = 0;
    for await (const item of asyncIterable) {
        if (taken >= count) break;
        yield item;
        taken++;
    }
}

// 使用组合函数
async function processDataPipeline() {
    const numbers = asyncNumberGenerator(20);
    
    const pipeline = takeAsync(
        filterAsync(
            mapAsync(numbers, async x => x * 2),
            async x => x > 10
        ),
        5
    );
    
    console.log('处理管道结果:');
    for await (const value of pipeline) {
        console.log('管道值:', value);
    }
}

// processDataPipeline();

// 异步迭代器工具类
class AsyncIterableUtils {
    // 将普通数组转换为异步可迭代对象
    static async* fromArray(array) {
        for (const item of array) {
            yield item;
        }
    }
    
    // 将 Promise 数组转换为异步可迭代对象
    static async* fromPromises(promises) {
        for (const promise of promises) {
            yield await promise;
        }
    }
    
    // 异步扁平化
    static async* flatten(asyncIterable) {
        for await (const item of asyncIterable) {
            if (item && typeof item[Symbol.asyncIterator] === 'function') {
                yield* item;
            } else if (item && typeof item[Symbol.iterator] === 'function') {
                yield* item;
            } else {
                yield item;
            }
        }
    }
    
    // 异步归约
    static async reduce(asyncIterable, reducer, initialValue) {
        let accumulator = initialValue;
        for await (const item of asyncIterable) {
            accumulator = await reducer(accumulator, item);
        }
        return accumulator;
    }
    
    // 转换为数组
    static async toArray(asyncIterable) {
        const results = [];
        for await (const item of asyncIterable) {
            results.push(item);
        }
        return results;
    }
}

// 使用工具类
async function useAsyncIterableUtils() {
    // 从数组创建
    const arrayIterable = AsyncIterableUtils.fromArray([1, 2, 3, 4, 5]);
    
    // 映射和过滤
    const mapped = mapAsync(arrayIterable, async x => x * 2);
    const filtered = filterAsync(mapped, async x => x > 4);
    
    const result = await AsyncIterableUtils.toArray(filtered);
    console.log('结果:', result); // [6, 8, 10]
    
    // 异步归约
    const sum = await AsyncIterableUtils.reduce(
        AsyncIterableUtils.fromArray([1, 2, 3, 4, 5]),
        async (acc, val) => acc + val,
        0
    );
    console.log('求和结果:', sum); // 15
}

// useAsyncIterableUtils();

// 实际应用：实时数据处理
class RealTimeDataProcessor {
    constructor() {
        this.processing = false;
    }
    
    async* dataStream() {
        while (this.processing) {
            // 模拟实时数据
            yield {
                id: Date.now(),
                value: Math.random(),
                timestamp: new Date()
            };
            
            await delay(1000); // 每秒产生一个数据点
        }
    }
    
    async* processData() {
        for await (const data of this.dataStream()) {
            // 处理数据
            const processed = {
                ...data,
                processedValue: data.value * 100,
                category: data.value > 0.5 ? 'high' : 'low'
            };
            
            yield processed;
        }
    }
    
    async startProcessing(callback) {
        this.processing = true;
        console.log('开始实时数据处理');
        
        try {
            for await (const processedData of this.processData()) {
                await callback(processedData);
            }
        } finally {
            this.processing = false;
        }
    }
    
    stopProcessing() {
        this.processing = false;
        console.log('停止实时数据处理');
    }
}

// 使用示例
const processor = new RealTimeDataProcessor();

// 启动处理（5秒后停止）
// setTimeout(() => processor.stopProcessing(), 5000);

// processor.startProcessing(async (data) => {
//     console.log('处理数据:', data);
// });

// 异步迭代器错误处理
async function* errorHandlingGenerator() {
    try {
        yield 1;
        yield 2;
        throw new Error('生成器中的错误');
        yield 3; // 这不会执行
    } catch (error) {
        console.log('生成器内部捕获错误:', error.message);
        yield 'error-recovery';
    }
}

async function useErrorHandlingGenerator() {
    try {
        for await (const value of errorHandlingGenerator()) {
            console.log('值:', value);
        }
    } catch (error) {
        console.log('外部捕获错误:', error.message);
    }
}

// useErrorHandlingGenerator();

// 异步迭代器的并发控制
class ConcurrentAsyncProcessor {
    constructor(concurrency = 3) {
        this.concurrency = concurrency;
    }
    
    async* processWithConcurrency(asyncIterable, processor) {
        const queue = [];
        let active = 0;
        
        for await (const item of asyncIterable) {
            if (active >= this.concurrency) {
                // 等待队列中有完成的项目
                const completed = await Promise.race(queue);
                const index = queue.indexOf(completed);
                if (index > -1) {
                    queue.splice(index, 1);
                }
                active--;
            }
            
            const promise = processor(item)
                .then(result => ({ success: true, result, item }))
                .catch(error => ({ success: false, error, item }));
            
            queue.push(promise);
            active++;
            
            // 如果队列未满，继续添加项目
            if (active < this.concurrency) {
                continue;
            }
            
            // 等待一个项目完成
            const completed = await Promise.race(queue);
            const index = queue.indexOf(completed);
            if (index > -1) {
                queue.splice(index, 1);
            }
            active--;
            
            if (completed.success) {
                yield completed.result;
            } else {
                console.error('处理失败:', completed.error);
                yield null;
            }
        }
        
        // 处理剩余的项目
        while (queue.length > 0) {
            const completed = await Promise.race(queue);
            const index = queue.indexOf(completed);
            if (index > -1) {
                queue.splice(index, 1);
            }
            
            if (completed.success) {
                yield completed.result;
            } else {
                console.error('处理失败:', completed.error);
                yield null;
            }
        }
    }
}

// 使用并发控制
async function useConcurrentProcessor() {
    const processor = new ConcurrentAsyncProcessor(3);
    
    const numbers = asyncNumberGenerator(10);
    
    const processItem = async (item) => {
        await delay(Math.random() * 1000); // 随机处理时间
        return item * 2;
    };
    
    console.log('开始并发处理');
    for await (const result of processor.processWithConcurrency(numbers, processItem)) {
        console.log('处理结果:', result);
    }
    console.log('并发处理完成');
}

// useConcurrentProcessor();
```

# 九、Web API 操作

## 9.1 DOM 操作技术

### 1. DOM 节点选择和遍历

```javascript
// DOM 节点选择方法

// 基本选择方法
// getElementById - 通过 ID 选择单个元素
const elementById = document.getElementById('myId');

// getElementsByClassName - 通过类名选择元素集合
const elementsByClass = document.getElementsByClassName('myClass');

// getElementsByTagName - 通过标签名选择元素集合
const elementsByTag = document.getElementsByTagName('div');

// getElementsByName - 通过 name 属性选择元素集合
const elementsByName = document.getElementsByName('myName');

// 现代选择器方法 (返回 NodeList 或单个元素)
// querySelector - 选择第一个匹配的元素
const firstElement = document.querySelector('.myClass'); // CSS 选择器
const specificElement = document.querySelector('#myId .childClass');

// querySelectorAll - 选择所有匹配的元素
const allElements = document.querySelectorAll('.myClass');
const complexSelection = document.querySelectorAll('div[data-role="button"]');

// NodeList 和 HTMLCollection 的区别
const nodeList = document.querySelectorAll('.item'); // 静态 NodeList
const htmlCollection = document.getElementsByClassName('item'); // 动态 HTMLCollection

// NodeList 遍历
nodeList.forEach(element => {
    console.log(element.textContent);
});

// HTMLCollection 遍历
for (let i = 0; i < htmlCollection.length; i++) {
    console.log(htmlCollection[i].textContent);
}

// 转换为数组以便使用数组方法
const elementsArray = Array.from(nodeList);
const filteredElements = elementsArray.filter(el => el.classList.contains('active'));

// 高级选择器示例
const advancedSelectors = {
    // 属性选择器
    attributeSelectors: [
        document.querySelector('[data-id]'), // 有 data-id 属性
        document.querySelector('[data-role="admin"]'), // data-role 等于 "admin"
        document.querySelector('[class*="btn"]'), // class 包含 "btn"
        document.querySelector('[id^="user"]'), // id 以 "user" 开头
        document.querySelector('[href$=".pdf"]') // href 以 ".pdf" 结尾
    ],
    
    // 伪类选择器
    pseudoSelectors: [
        document.querySelector('li:first-child'), // 第一个 li
        document.querySelector('li:last-child'), // 最后一个 li
        document.querySelector('li:nth-child(2n)'), // 偶数位置的 li
        document.querySelector('input:focus'), // 获得焦点的 input
        document.querySelector('a:hover') // 鼠标悬停的 a (实际中很少使用)
    ],
    
    // 组合选择器
    combinedSelectors: [
        document.querySelector('div.container > p'), // 直接子元素
        document.querySelector('ul ~ p'), // 兄弟元素
        document.querySelector('form input[type="text"]'), // 后代元素
        document.querySelectorAll('h1, h2, h3') // 多个选择器
    ]
};

// DOM 遍历方法

// 父节点遍历
function traverseParents(element) {
    const parents = [];
    let current = element.parentElement;
    
    while (current) {
        parents.push(current);
        current = current.parentElement;
    }
    
    return parents;
}

// 子节点遍历
function traverseChildren(element) {
    const children = [];
    
    // 所有子节点（包括文本节点）
    element.childNodes.forEach(node => {
        if (node.nodeType === Node.ELEMENT_NODE) {
            children.push(node);
        }
    });
    
    // 只获取元素节点
    const elementChildren = Array.from(element.children);
    
    return { allChildren: children, elementChildren };
}

// 兄弟节点遍历
function traverseSiblings(element) {
    const siblings = [];
    let sibling = element.previousElementSibling;
    
    // 获取前面的兄弟节点
    while (sibling) {
        siblings.unshift(sibling); // 添加到数组开头
        sibling = sibling.previousElementSibling;
    }
    
    sibling = element.nextElementSibling;
    
    // 获取后面的兄弟节点
    while (sibling) {
        siblings.push(sibling);
        sibling = sibling.nextElementSibling;
    }
    
    return siblings;
}

// 深度遍历 DOM 树
function traverseDOMTree(root, callback) {
    callback(root);
    
    for (let child = root.firstElementChild; child; child = child.nextElementSibling) {
        traverseDOMTree(child, callback);
    }
}

// 广度遍历 DOM 树
function traverseDOMBreadth(root, callback) {
    const queue = [root];
    
    while (queue.length > 0) {
        const current = queue.shift();
        callback(current);
        
        for (let child = current.firstElementChild; child; child = child.nextElementSibling) {
            queue.push(child);
        }
    }
}

// 实际应用：查找特定元素
function findElementsByText(root, searchText) {
    const results = [];
    
    traverseDOMTree(root || document.body, element => {
        if (element.nodeType === Node.TEXT_NODE && 
            element.textContent.includes(searchText)) {
            results.push(element.parentElement);
        }
    });
    
    return results;
}

// 实际应用：构建 DOM 结构树
function buildDOMStructure(root) {
    const structure = {
        tag: root.tagName.toLowerCase(),
        id: root.id,
        classes: Array.from(root.classList),
        children: []
    };
    
    for (let child = root.firstElementChild; child; child = child.nextElementSibling) {
        structure.children.push(buildDOMStructure(child));
    }
    
    return structure;
}

// 性能优化的选择器使用
class OptimizedSelector {
    constructor() {
        this.cache = new Map();
    }
    
    // 缓存选择器结果
    select(selector, context = document) {
        const key = `${selector}_${context.tagName || 'document'}`;
        
        if (!this.cache.has(key)) {
            const result = context.querySelector(selector);
            this.cache.set(key, result);
        }
        
        return this.cache.get(key);
    }
    
    selectAll(selector, context = document) {
        const key = `all_${selector}_${context.tagName || 'document'}`;
        
        if (!this.cache.has(key)) {
            const result = context.querySelectorAll(selector);
            this.cache.set(key, result);
        }
        
        return this.cache.get(key);
    }
    
    clearCache() {
        this.cache.clear();
    }
}

// 使用示例
const selector = new OptimizedSelector();
const element = selector.select('#myId .child');
const elements = selector.selectAll('.myClass');
```

### 2. DOM 节点创建和修改

```javascript
// DOM 节点创建

// 创建元素节点
const newDiv = document.createElement('div');
const newSpan = document.createElement('span');
const newInput = document.createElement('input');

// 创建文本节点
const textNode = document.createTextNode('Hello World');

// 创建注释节点
const commentNode = document.createComment('This is a comment');

// 创建文档片段 (DocumentFragment)
const fragment = document.createDocumentFragment();

// 设置元素属性和内容
newDiv.id = 'myDiv';
newDiv.className = 'container';
newDiv.setAttribute('data-role', 'content');
newDiv.textContent = '这是内容';
newDiv.innerHTML = '<strong>这是 HTML 内容</strong>';

// 设置样式
newDiv.style.color = 'red';
newDiv.style.fontSize = '16px';
newDiv.style.backgroundColor = '#f0f0f0';

// 批量设置样式
Object.assign(newDiv.style, {
    padding: '10px',
    margin: '5px',
    border: '1px solid #ccc'
});

// DOM 节点插入

// 插入到父节点的末尾
const parent = document.getElementById('container');
parent.appendChild(newDiv);

// 插入到指定位置
const referenceNode = document.getElementById('reference');
parent.insertBefore(newDiv, referenceNode);

// 使用 insertAdjacentHTML 插入 HTML
parent.insertAdjacentHTML('beforeend', '<p>插入的段落</p>');
parent.insertAdjacentHTML('afterbegin', '<h2>插入的标题</h2>');

// insertAdjacentElement 和 insertAdjacentText
const newElement = document.createElement('strong');
newElement.textContent = '重要文本';
parent.insertAdjacentElement('beforeend', newElement);

// DOM 节点修改

// 修改文本内容
const element = document.getElementById('myElement');
element.textContent = '新文本内容'; // 安全，会转义 HTML
element.innerText = '新文本内容'; // 考虑样式，会触发重排
element.innerHTML = '<strong>新 HTML 内容</strong>'; // 可能存在 XSS 风险

// 修改属性
element.setAttribute('data-value', '123');
element.removeAttribute('data-value');
const value = element.getAttribute('data-value');

// 修改类名
element.className = 'newClass';
element.classList.add('active', 'highlight');
element.classList.remove('inactive');
element.classList.toggle('visible');
element.classList.contains('active'); // 检查是否包含类

// 修改样式
element.style.setProperty('color', 'blue');
element.style.removeProperty('background-color');

// 批量样式修改
element.style.cssText = 'color: red; font-size: 18px;';

// DOM 节点删除和替换

// 删除节点
const nodeToRemove = document.getElementById('toRemove');
nodeToRemove.remove(); // 现代方法

// 传统方法
if (nodeToRemove.parentNode) {
    nodeToRemove.parentNode.removeChild(nodeToRemove);
}

// 替换节点
const oldNode = document.getElementById('old');
const newNode = document.createElement('div');
newNode.textContent = '新节点';
oldNode.replaceWith(newNode); // 现代方法

// 传统方法
oldNode.parentNode.replaceChild(newNode, oldNode);

// 克隆节点
const original = document.getElementById('original');
const clone = original.cloneNode(true); // true 表示深克隆
const shallowClone = original.cloneNode(false); // false 表示浅克隆

// 高级 DOM 操作

// 创建复杂元素结构
function createCard(data) {
    const card = document.createElement('div');
    card.className = 'card';
    
    const header = document.createElement('div');
    header.className = 'card-header';
    header.textContent = data.title;
    
    const body = document.createElement('div');
    body.className = 'card-body';
    
    const content = document.createElement('p');
    content.textContent = data.content;
    
    const footer = document.createElement('div');
    footer.className = 'card-footer';
    
    const button = document.createElement('button');
    button.textContent = '查看详情';
    button.addEventListener('click', () => {
        console.log('查看详情:', data.id);
    });
    
    body.appendChild(content);
    footer.appendChild(button);
    card.appendChild(header);
    card.appendChild(body);
    card.appendChild(footer);
    
    return card;
}

// 使用模板字符串创建 HTML
function createHTMLCard(data) {
    const html = `
        <div class="card" data-id="${data.id}">
            <div class="card-header">${data.title}</div>
            <div class="card-body">
                <p>${data.content}</p>
            </div>
            <div class="card-footer">
                <button onclick="viewDetails(${data.id})">查看详情</button>
            </div>
        </div>
    `;
    
    const temp = document.createElement('div');
    temp.innerHTML = html.trim();
    return temp.firstChild;
}

// 批量 DOM 操作优化
class BatchDOMOperations {
    constructor() {
        this.fragment = document.createDocumentFragment();
    }
    
    // 批量添加元素
    addElements(elements) {
        elements.forEach(element => {
            this.fragment.appendChild(element);
        });
    }
    
    // 应用到 DOM
    applyTo(parent) {
        parent.appendChild(this.fragment);
    }
    
    // 清空片段
    clear() {
        while (this.fragment.firstChild) {
            this.fragment.removeChild(this.fragment.firstChild);
        }
    }
}

// 使用示例
const batchOps = new BatchDOMOperations();
const elements = [];

for (let i = 0; i < 100; i++) {
    const div = document.createElement('div');
    div.textContent = `Item ${i}`;
    elements.push(div);
}

batchOps.addElements(elements);
// batchOps.applyTo(document.getElementById('container'));

// DOM 操作工具类
class DOMUtils {
    // 创建元素的便捷方法
    static createElement(tag, attributes = {}, content = '') {
        const element = document.createElement(tag);
        
        // 设置属性
        Object.keys(attributes).forEach(key => {
            if (key === 'className') {
                element.className = attributes[key];
            } else if (key === 'textContent') {
                element.textContent = attributes[key];
            } else if (key === 'innerHTML') {
                element.innerHTML = attributes[key];
            } else {
                element.setAttribute(key, attributes[key]);
            }
        });
        
        // 设置内容
        if (content && !attributes.textContent && !attributes.innerHTML) {
            element.textContent = content;
        }
        
        return element;
    }
    
    // 批量设置样式
    static setStyles(element, styles) {
        Object.assign(element.style, styles);
    }
    
    // 批量添加类
    static addClasses(element, ...classes) {
        element.classList.add(...classes);
    }
    
    // 批量移除类
    static removeClasses(element, ...classes) {
        element.classList.remove(...classes);
    }
    
    // 切换类（支持条件）
    static toggleClass(element, className, condition) {
        if (condition !== undefined) {
            element.classList.toggle(className, condition);
        } else {
            element.classList.toggle(className);
        }
    }
    
    // 安全的 HTML 设置
    static setHTML(element, html) {
        // 简单的 XSS 防护（实际项目中需要更完善的方案）
        const sanitized = html.replace(/<script\b[^<]*(?:(?!<\/script>)<[^<]*)*<\/script>/gi, '');
        element.innerHTML = sanitized;
    }
}

// 使用示例
const button = DOMUtils.createElement('button', {
    className: 'btn btn-primary',
    'data-action': 'submit'
}, '提交');

DOMUtils.setStyles(button, {
    padding: '10px 20px',
    backgroundColor: '#007bff',
    color: 'white',
    border: 'none',
    borderRadius: '4px'
});

DOMUtils.addClasses(button, 'active', 'hover-effect');
```

### 3. DOM 事件处理机制

```javascript
// DOM 事件处理基础

// 添加事件监听器
const button = document.getElementById('myButton');

// 传统方法
button.onclick = function(event) {
    console.log('按钮被点击');
};

// 现代方法 - addEventListener
button.addEventListener('click', function(event) {
    console.log('按钮被点击 - 现代方法');
});

// 使用箭头函数
button.addEventListener('click', (event) => {
    console.log('按钮被点击 - 箭头函数');
});

// 事件对象属性
button.addEventListener('click', (event) => {
    console.log('事件类型:', event.type);
    console.log('目标元素:', event.target);
    console.log('当前目标:', event.currentTarget);
    console.log('事件时间戳:', event.timeStamp);
    console.log('鼠标坐标:', event.clientX, event.clientY);
});

// 移除事件监听器
function handleClick(event) {
    console.log('处理点击事件');
}

button.addEventListener('click', handleClick);
// 移除监听器
button.removeEventListener('click', handleClick);

// 事件监听器选项
button.addEventListener('click', handleClick, {
    once: true, // 只执行一次
    passive: true, // 被动监听器，不会调用 preventDefault
    capture: false // 是否在捕获阶段执行
});

// 事件冒泡和捕获
const container = document.getElementById('container');
const child = document.getElementById('child');

// 捕获阶段
container.addEventListener('click', (event) => {
    console.log('容器 - 捕获阶段');
}, true); // true 表示捕获阶段

// 冒泡阶段
container.addEventListener('click', (event) => {
    console.log('容器 - 冒泡阶段');
}, false); // false 表示冒泡阶段

child.addEventListener('click', (event) => {
    console.log('子元素 - 冒泡阶段');
});

// 阻止事件传播
child.addEventListener('click', (event) => {
    console.log('子元素点击');
    event.stopPropagation(); // 阻止事件继续传播
    // event.stopImmediatePropagation(); // 阻止同级监听器执行
});

// 阻止默认行为
const link = document.getElementById('myLink');
link.addEventListener('click', (event) => {
    event.preventDefault(); // 阻止链接跳转
    console.log('链接点击被阻止');
});

// 键盘事件处理
document.addEventListener('keydown', (event) => {
    console.log('按键:', event.key);
    console.log('键码:', event.keyCode); // 已废弃，使用 event.key
    console.log('是否按下 Ctrl:', event.ctrlKey);
    console.log('是否按下 Alt:', event.altKey);
    console.log('是否按下 Shift:', event.shiftKey);
    
    // 特殊按键处理
    if (event.key === 'Escape') {
        console.log('按下 ESC 键');
    }
    
    if (event.ctrlKey && event.key === 's') {
        event.preventDefault(); // 阻止保存页面
        console.log('Ctrl+S 被按下');
    }
});

// 鼠标事件处理
const mouseArea = document.getElementById('mouseArea');

mouseArea.addEventListener('mousedown', (event) => {
    console.log('鼠标按下:', event.button); // 0: 左键, 1: 中键, 2: 右键
});

mouseArea.addEventListener('mouseup', (event) => {
    console.log('鼠标释放');
});

mouseArea.addEventListener('mousemove', (event) => {
    console.log('鼠标移动:', event.clientX, event.clientY);
});

mouseArea.addEventListener('mouseenter', (event) => {
    console.log('鼠标进入');
});

mouseArea.addEventListener('mouseleave', (event) => {
    console.log('鼠标离开');
});

// 表单事件处理
const form = document.getElementById('myForm');
const input = document.getElementById('myInput');

// 输入事件
input.addEventListener('input', (event) => {
    console.log('输入内容:', event.target.value);
});

// 变化事件
input.addEventListener('change', (event) => {
    console.log('值发生变化:', event.target.value);
});

// 焦点事件
input.addEventListener('focus', (event) => {
    console.log('获得焦点');
});

input.addEventListener('blur', (event) => {
    console.log('失去焦点');
});

// 表单提交
form.addEventListener('submit', (event) => {
    event.preventDefault(); // 阻止表单默认提交
    console.log('表单提交');
    
    // 表单验证
    const formData = new FormData(form);
    for (const [key, value] of formData.entries()) {
        console.log(`${key}: ${value}`);
    }
});

// 窗口事件
window.addEventListener('load', (event) => {
    console.log('页面加载完成');
});

window.addEventListener('resize', (event) => {
    console.log('窗口大小改变:', window.innerWidth, window.innerHeight);
});

window.addEventListener('scroll', (event) => {
    console.log('页面滚动:', window.scrollY);
});

// 自定义事件
const customEvent = new CustomEvent('myCustomEvent', {
    detail: { message: '自定义事件数据' },
    bubbles: true,
    cancelable: true
});

document.addEventListener('myCustomEvent', (event) => {
    console.log('自定义事件触发:', event.detail.message);
});

// 触发自定义事件
document.dispatchEvent(customEvent);

// 事件委托
class EventDelegation {
    constructor(container) {
        this.container = container;
        this.setupDelegation();
    }
    
    setupDelegation() {
        this.container.addEventListener('click', (event) => {
            const target = event.target;
            
            // 委托给按钮
            if (target.matches('.btn')) {
                this.handleButtonClick(target, event);
            }
            
            // 委托给链接
            if (target.matches('a[data-action]')) {
                this.handleLinkClick(target, event);
            }
            
            // 委托给列表项
            if (target.matches('li')) {
                this.handleListItemClick(target, event);
            }
        });
    }
    
    handleButtonClick(button, event) {
        const action = button.dataset.action;
        console.log('按钮点击:', action);
        
        switch (action) {
            case 'delete':
                this.deleteItem(button);
                break;
            case 'edit':
                this.editItem(button);
                break;
            default:
                console.log('未知操作:', action);
        }
    }
    
    handleLinkClick(link, event) {
        event.preventDefault();
        const action = link.dataset.action;
        console.log('链接点击:', action);
    }
    
    handleListItemClick(item, event) {
        console.log('列表项点击:', item.textContent);
    }
    
    deleteItem(button) {
        const item = button.closest('.item');
        if (item) {
            item.remove();
        }
    }
    
    editItem(button) {
        const item = button.closest('.item');
        if (item) {
            const text = item.querySelector('.text');
            if (text) {
                text.contentEditable = true;
                text.focus();
            }
        }
    }
}

// 使用事件委托
// const delegation = new EventDelegation(document.getElementById('container'));

// 事件管理器
class EventManager {
    constructor() {
        this.events = new Map();
    }
    
    // 添加事件监听器
    on(element, eventType, handler, options = {}) {
        const key = this.getEventKey(element, eventType, handler);
        
        if (!this.events.has(key)) {
            element.addEventListener(eventType, handler, options);
            this.events.set(key, { element, eventType, handler, options });
        }
    }
    
    // 移除事件监听器
    off(element, eventType, handler) {
        const key = this.getEventKey(element, eventType, handler);
        
        if (this.events.has(key)) {
            element.removeEventListener(eventType, handler);
            this.events.delete(key);
        }
    }
    
    // 一次性事件
    once(element, eventType, handler, options = {}) {
        const onceHandler = (event) => {
            handler(event);
            this.off(element, eventType, onceHandler);
        };
        
        this.on(element, eventType, onceHandler, options);
    }
    
    // 触发事件
    trigger(element, eventType, detail = {}) {
        const event = new CustomEvent(eventType, { detail });
        element.dispatchEvent(event);
    }
    
    // 移除所有事件监听器
    removeAll() {
        this.events.forEach(({ element, eventType, handler }) => {
            element.removeEventListener(eventType, handler);
        });
        this.events.clear();
    }
    
    // 获取事件键
    getEventKey(element, eventType, handler) {
        return `${element.tagName}_${eventType}_${handler.name}`;
    }
}

// 使用事件管理器
const eventManager = new EventManager();
const button = document.getElementById('myButton');

eventManager.on(button, 'click', (event) => {
    console.log('按钮点击');
});

eventManager.once(button, 'click', (event) => {
    console.log('只会执行一次');
});

// 事件节流和防抖
class EventUtils {
    // 防抖 - 限制函数执行频率
    static debounce(func, delay) {
        let timeoutId;
        return function(...args) {
            clearTimeout(timeoutId);
            timeoutId = setTimeout(() => func.apply(this, args), delay);
        };
    }
    
    // 节流 - 固定时间间隔内只执行一次
    static throttle(func, limit) {
        let inThrottle;
        return function(...args) {
            if (!inThrottle) {
                func.apply(this, args);
                inThrottle = true;
                setTimeout(() => inThrottle = false, limit);
            }
        };
    }
    
    // 事件节流应用
    static setupThrottledScroll(callback, delay = 100) {
        const throttledCallback = this.throttle(callback, delay);
        window.addEventListener('scroll', throttledCallback);
        return throttledCallback;
    }
    
    // 事件防抖应用
    static setupDebouncedResize(callback, delay = 300) {
        const debouncedCallback = this.debounce(callback, delay);
        window.addEventListener('resize', debouncedCallback);
        return debouncedCallback;
    }
}

// 使用示例
const searchInput = document.getElementById('search');

// 防抖搜索
const debouncedSearch = EventUtils.debounce((event) => {
    console.log('执行搜索:', event.target.value);
}, 300);

searchInput.addEventListener('input', debouncedSearch);

// 节流滚动处理
const throttledScroll = EventUtils.throttle(() => {
    console.log('滚动位置:', window.scrollY);
}, 100);

window.addEventListener('scroll', throttledScroll);
```

### 4. DOM 性能优化

```javascript
// DOM 性能优化技术

// 1. 减少 DOM 操作次数

// 不好的做法 - 多次 DOM 操作
function badDOMUpdate() {
    const list = document.getElementById('list');
    for (let i = 0; i < 1000; i++) {
        const item = document.createElement('li');
        item.textContent = `Item ${i}`;
        list.appendChild(item); // 每次都触发重排
    }
}

// 好的做法 - 使用文档片段
function goodDOMUpdate() {
    const list = document.getElementById('list');
    const fragment = document.createDocumentFragment();
    
    for (let i = 0; i < 1000; i++) {
        const item = document.createElement('li');
        item.textContent = `Item ${i}`;
        fragment.appendChild(item);
    }
    
    list.appendChild(fragment); // 只触发一次重排
}

// 2. 批量样式修改

// 不好的做法 - 多次修改样式
function badStyleUpdate(element) {
    element.style.color = 'red';
    element.style.fontSize = '16px';
    element.style.backgroundColor = 'yellow';
    // 每次修改都可能触发重排和重绘
}

// 好的做法 - 批量修改
function goodStyleUpdate(element) {
    // 方法1: 使用 cssText
    element.style.cssText = 'color: red; font-size: 16px; background-color: yellow;';
    
    // 方法2: 修改 class
    element.className = 'updated-style';
    
    // 方法3: 使用 CSS 类切换
    element.classList.add('highlight', 'large-text');
}

// 3. 虚拟滚动优化

class VirtualScroller {
    constructor(container, items, itemHeight = 50) {
        this.container = container;
        this.items = items;
        this.itemHeight = itemHeight;
        this.visibleCount = Math.ceil(container.clientHeight / itemHeight) + 2;
        this.startIndex = 0;
        
        this.setupContainer();
        this.render();
        this.setupScrollListener();
    }
    
    setupContainer() {
        this.container.style.height = `${this.items.length * this.itemHeight}px`;
        this.container.style.position = 'relative';
        this.container.style.overflow = 'auto';
    }
    
    render() {
        // 清空容器
        this.container.innerHTML = '';
        
        // 创建可见项
        const fragment = document.createDocumentFragment();
        
        for (let i = this.startIndex; i < Math.min(this.startIndex + this.visibleCount, this.items.length); i++) {
            const item = this.createItem(this.items[i], i);
            fragment.appendChild(item);
        }
        
        this.container.appendChild(fragment);
    }
    
    createItem(data, index) {
        const item = document.createElement('div');
        item.style.position = 'absolute';
        item.style.top = `${index * this.itemHeight}px`;
        item.style.height = `${this.itemHeight}px`;
        item.style.width = '100%';
        item.textContent = data;
        return item;
    }
    
    setupScrollListener() {
        this.container.addEventListener('scroll', () => {
            const scrollTop = this.container.scrollTop;
            const newStartIndex = Math.floor(scrollTop / this.itemHeight);
            
            if (newStartIndex !== this.startIndex) {
                this.startIndex = newStartIndex;
                this.render();
            }
        });
    }
}

// 4. DOM 查询优化

class OptimizedDOMQuery {
    constructor() {
        this.cache = new Map();
    }
    
    // 缓存查询结果
    query(selector, context = document) {
        const key = `${selector}_${context.tagName || 'document'}`;
        
        if (!this.cache.has(key)) {
            const result = context.querySelector(selector);
            this.cache.set(key, result);
        }
        
        return this.cache.get(key);
    }
    
    queryAll(selector, context = document) {
        const key = `all_${selector}_${context.tagName || 'document'}`;
        
        if (!this.cache.has(key)) {
            const result = context.querySelectorAll(selector);
            this.cache.set(key, result);
        }
        
        return this.cache.get(key);
    }
    
    // 预查询常用元素
    preloadSelectors(selectors) {
        selectors.forEach(selector => {
            this.query(selector);
        });
    }
    
    clearCache() {
        this.cache.clear();
    }
}

// 5. 事件处理优化

class OptimizedEventManager {
    constructor() {
        this.delegates = new Map();
    }
    
    // 事件委托优化
    delegate(container, eventType, selector, handler) {
        const key = `${container.tagName}_${eventType}_${selector}`;
        
        if (!this.delegates.has(key)) {
            container.addEventListener(eventType, (event) => {
                const target = event.target;
                if (target.matches && target.matches(selector)) {
                    handler.call(target, event);
                }
            });
            
            this.delegates.set(key, true);
        }
    }
    
    // 事件节流
    throttle(handler, delay) {
        let lastExecTime = 0;
        return function(...args) {
            const now = Date.now();
            if (now - lastExecTime >= delay) {
                handler.apply(this, args);
                lastExecTime = now;
            }
        };
    }
    
    // 事件防抖
    debounce(handler, delay) {
        let timeoutId;
        return function(...args) {
            clearTimeout(timeoutId);
            timeoutId = setTimeout(() => handler.apply(this, args), delay);
        };
    }
}

// 6. 内存泄漏预防

class MemorySafeDOM {
    constructor() {
        this.eventListeners = new WeakMap();
    }
    
    // 安全添加事件监听器
    addEventListener(element, eventType, handler, options = {}) {
        element.addEventListener(eventType, handler, options);
        
        if (!this.eventListeners.has(element)) {
            this.eventListeners.set(element, []);
        }
        
        this.eventListeners.get(element).push({
            eventType,
            handler,
            options
        });
    }
    
    // 移除元素及其所有事件监听器
    removeElement(element) {
        if (this.eventListeners.has(element)) {
            const listeners = this.eventListeners.get(element);
            listeners.forEach(({ eventType, handler }) => {
                element.removeEventListener(eventType, handler);
            });
            this.eventListeners.delete(element);
        }
        
        if (element.parentNode) {
            element.parentNode.removeChild(element);
        }
    }
    
    // 清理所有监听器
    cleanup() {
        this.eventListeners.forEach((listeners, element) => {
            listeners.forEach(({ eventType, handler }) => {
                element.removeEventListener(eventType, handler);
            });
        });
        this.eventListeners.clear();
    }
}

// 7. 性能监控工具

class PerformanceMonitor {
    constructor() {
        this.measurements = [];
    }
    
    // 测量函数执行时间
    measure(name, fn) {
        const start = performance.now();
        const result = fn();
        const end = performance.now();
        
        const duration = end - start;
        this.measurements.push({ name, duration });
        
        console.log(`${name}: ${duration.toFixed(2)}ms`);
        return result;
    }
    
    // DOM 操作性能测试
    testDOMOperations() {
        // 测试创建元素性能
        this.measure('创建1000个元素', () => {
            const fragment = document.createDocumentFragment();
            for (let i = 0; i < 1000; i++) {
                const div = document.createElement('div');
                div.textContent = `Item ${i}`;
                fragment.appendChild(div);
            }
            return fragment;
        });
        
        // 测试查询性能
        this.measure('查询100次元素', () => {
            for (let i = 0; i < 100; i++) {
                document.querySelector('.test-class');
            }
        });
        
        // 测试样式修改性能
        this.measure('修改100个元素样式', () => {
            const elements = document.querySelectorAll('.test-item');
            elements.forEach(el => {
                el.style.color = 'red';
            });
        });
    }
    
    // 获取性能报告
    getReport() {
        return this.measurements.map(m => ({
            operation: m.name,
            time: `${m.duration.toFixed(2)}ms`
        }));
    }
    
    // 清空测量数据
    clear() {
        this.measurements = [];
    }
}

// 8. 实际应用：高性能列表渲染

class HighPerformanceList {
    constructor(container, options = {}) {
        this.container = container;
        this.items = [];
        this.visibleItems = [];
        this.itemHeight = options.itemHeight || 50;
        this.buffer = options.buffer || 5;
        this.renderFunction = options.render || this.defaultRender;
        
        this.setupContainer();
        this.setupScrollHandler();
    }
    
    setupContainer() {
        this.container.style.overflow = 'auto';
        this.container.style.position = 'relative';
    }
    
    addItem(item) {
        this.items.push(item);
        this.updateContainerHeight();
        this.updateVisibleItems();
    }
    
    addItems(items) {
        this.items.push(...items);
        this.updateContainerHeight();
        this.updateVisibleItems();
    }
    
    updateContainerHeight() {
        this.container.style.height = `${this.items.length * this.itemHeight}px`;
    }
    
    setupScrollHandler() {
        let ticking = false;
        
        this.container.addEventListener('scroll', () => {
            if (!ticking) {
                requestAnimationFrame(() => {
                    this.updateVisibleItems();
                    ticking = false;
                });
                ticking = true;
            }
        });
    }
    
    updateVisibleItems() {
        const scrollTop = this.container.scrollTop;
        const containerHeight = this.container.clientHeight;
        
        const startIndex = Math.max(0, Math.floor(scrollTop / this.itemHeight) - this.buffer);
        const endIndex = Math.min(
            this.items.length,
            Math.ceil((scrollTop + containerHeight) / this.itemHeight) + this.buffer
        );
        
        this.renderVisibleItems(startIndex, endIndex);
    }
    
    renderVisibleItems(startIndex, endIndex) {
        // 清空容器
        this.container.innerHTML = '';
        
        const fragment = document.createDocumentFragment();
        
        for (let i = startIndex; i < endIndex; i++) {
            const itemElement = this.renderFunction(this.items[i], i);
            itemElement.style.position = 'absolute';
            itemElement.style.top = `${i * this.itemHeight}px`;
            itemElement.style.height = `${this.itemHeight}px`;
            itemElement.style.width = '100%';
            
            fragment.appendChild(itemElement);
        }
        
        this.container.appendChild(fragment);
    }
    
    defaultRender(item, index) {
        const element = document.createElement('div');
        element.textContent = typeof item === 'object' ? JSON.stringify(item) : String(item);
        return element;
    }
    
    // 更新特定项目
    updateItem(index, newItem) {
        this.items[index] = newItem;
        // 如果该项目当前可见，重新渲染
        this.updateVisibleItems();
    }
    
    // 移除项目
    removeItem(index) {
        this.items.splice(index, 1);
        this.updateContainerHeight();
        this.updateVisibleItems();
    }
}

// 使用示例
// const container = document.getElementById('list-container');
// const list = new HighPerformanceList(container, {
//     itemHeight: 60,
//     render: (item, index) => {
//         const div = document.createElement('div');
//         div.innerHTML = `<strong>${item.name}</strong><br>${item.description}`;
//         return div;
//     }
// });
//
// // 添加大量数据
// const data = Array.from({ length: 10000 }, (_, i) => ({
//     name: `Item ${i}`,
//     description: `Description for item ${i}`
// }));
// list.addItems(data);

// 9. CSS 动画优化

class OptimizedAnimations {
    // 使用 transform 和 opacity 进行动画（触发合成层）
    static animateWithTransform(element, animationProps, duration = 300) {
        element.style.transition = `transform ${duration}ms ease, opacity ${duration}ms ease`;
        
        Object.keys(animationProps).forEach(prop => {
            if (prop === 'x' || prop === 'y' || prop === 'scale') {
                const currentTransform = element.style.transform || '';
                let newTransform = currentTransform;
                
                if (prop === 'x') {
                    newTransform += ` translateX(${animationProps[prop]}px)`;
                } else if (prop === 'y') {
                    newTransform += ` translateY(${animationProps[prop]}px)`;
                } else if (prop === 'scale') {
                    newTransform += ` scale(${animationProps[prop]})`;
                }
                
                element.style.transform = newTransform;
            } else if (prop === 'opacity') {
                element.style.opacity = animationProps[prop];
            }
        });
    }
    
    // 使用 requestAnimationFrame 优化动画
    static smoothAnimation(element, from, to, duration, property) {
        const startTime = performance.now();
        
        const animate = (currentTime) => {
            const elapsed = currentTime - startTime;
            const progress = Math.min(elapsed / duration, 1);
            
            // 缓动函数
            const easeProgress = 1 - Math.pow(1 - progress, 3);
            const currentValue = from + (to - from) * easeProgress;
            
            element.style[property] = `${currentValue}px`;
            
            if (progress < 1) {
                requestAnimationFrame(animate);
            }
        };
        
        requestAnimationFrame(animate);
    }
    
    // 硬件加速提示
    static enableHardwareAcceleration(element) {
        element.style.transform = 'translateZ(0)';
        // 或者
        // element.style.willChange = 'transform';
    }
}

// 10. 性能测试工具

class DOMPerformanceTester {
    static testCreateElements(count) {
        console.time('创建元素');
        const fragment = document.createDocumentFragment();
        for (let i = 0; i < count; i++) {
            const div = document.createElement('div');
            div.textContent = `Item ${i}`;
            fragment.appendChild(div);
        }
        console.timeEnd('创建元素');
        return fragment;
    }
    
    static testQuerySelectors(count, selector) {
        console.time('查询元素');
        for (let i = 0; i < count; i++) {
            document.querySelector(selector);
        }
        console.timeEnd('查询元素');
    }
    
    static testStyleUpdates(elements) {
        console.time('样式更新');
        elements.forEach(el => {
            el.style.color = 'red';
            el.style.fontSize = '16px';
        });
        console.timeEnd('样式更新');
    }
    
    static testEventHandling(elements, eventType) {
        console.time('事件处理');
        elements.forEach(el => {
            el.addEventListener(eventType, () => {});
        });
        console.timeEnd('事件处理');
    }
}

// 使用性能测试
// const testElements = Array.from({ length: 1000 }, (_, i) => {
//     const div = document.createElement('div');
//     div.className = 'test-item';
//     div.textContent = `Test ${i}`;
//     return div;
// });
//
// DOMPerformanceTester.testCreateElements(1000);
// DOMPerformanceTester.testQuerySelectors(100, '.test-item');
// DOMPerformanceTester.testStyleUpdates(testElements);
```

## 9.2 BOM 对象操作

### 1. window 对象功能

```javascript
// window 对象核心功能

// 窗口尺寸和位置
console.log('窗口尺寸:', {
    width: window.innerWidth,
    height: window.innerHeight,
    outerWidth: window.outerWidth,
    outerHeight: window.outerHeight
});

console.log('窗口位置:', {
    screenX: window.screenX,
    screenY: window.screenY,
    pageXOffset: window.pageXOffset,
    pageYOffset: window.pageYOffset
});

// 窗口操作
function windowOperations() {
    // 打开新窗口
    const newWindow = window.open(
        'https://example.com',
        'example',
        'width=800,height=600,scrollbars=yes'
    );
    
    // 调整窗口大小
    window.resizeTo(1024, 768);
    window.resizeBy(100, 50); // 相对调整
    
    // 移动窗口
    window.moveTo(100, 100);
    window.moveBy(50, 50); // 相对移动
    
    // 滚动窗口
    window.scrollTo(0, 100);
    window.scrollBy(0, 50);
    window.scroll({ top: 100, left: 0, behavior: 'smooth' });
}

// 窗口焦点和可见性
window.addEventListener('focus', () => {
    console.log('窗口获得焦点');
});

window.addEventListener('blur', () => {
    console.log('窗口失去焦点');
});

// Page Visibility API
document.addEventListener('visibilitychange', () => {
    if (document.hidden) {
        console.log('页面隐藏');
    } else {
        console.log('页面可见');
    }
});

// 窗口关闭和刷新
function windowControl() {
    // 关闭窗口
    // window.close(); // 只能关闭通过 window.open 打开的窗口
    
    // 刷新页面
    // window.location.reload();
    
    // 前进后退
    window.history.back();
    window.history.forward();
    window.history.go(-2); // 后退两步
}

// 窗口对话框
function showDialogs() {
    // 警告对话框
    alert('这是一个警告');
    
    // 确认对话框
    const confirmed = confirm('确定要执行此操作吗？');
    if (confirmed) {
        console.log('用户确认');
    }
    
    // 输入对话框
    const userInput = prompt('请输入您的姓名：', '默认值');
    if (userInput !== null) {
        console.log('用户输入:', userInput);
    }
}

// 自定义对话框
class CustomDialog {
    constructor() {
        this.dialog = null;
    }
    
    show(message, options = {}) {
        return new Promise((resolve, reject) => {
            // 创建对话框元素
            this.dialog = document.createElement('div');
            this.dialog.className = 'custom-dialog';
            this.dialog.innerHTML = `
                <div class="dialog-overlay">
                    <div class="dialog-content">
                        <div class="dialog-message">${message}</div>
                        <div class="dialog-buttons">
                            <button class="btn-cancel">取消</button>
                            <button class="btn-confirm">确定</button>
                        </div>
                    </div>
                </div>
            `;
            
            // 添加样式
            this.addStyles();
            
            // 添加到页面
            document.body.appendChild(this.dialog);
            
            // 绑定事件
            this.dialog.querySelector('.btn-confirm').addEventListener('click', () => {
                this.close();
                resolve(true);
            });
            
            this.dialog.querySelector('.btn-cancel').addEventListener('click', () => {
                this.close();
                resolve(false);
            });
            
            // ESC 键关闭
            const handleEsc = (event) => {
                if (event.key === 'Escape') {
                    this.close();
                    resolve(false);
                    document.removeEventListener('keydown', handleEsc);
                }
            };
            
            document.addEventListener('keydown', handleEsc);
        });
    }
    
    close() {
        if (this.dialog) {
            this.dialog.remove();
            this.dialog = null;
        }
    }
    
    addStyles() {
        if (!document.getElementById('custom-dialog-styles')) {
            const style = document.createElement('style');
            style.id = 'custom-dialog-styles';
            style.textContent = `
                .custom-dialog {
                    position: fixed;
                    top: 0;
                    left: 0;
                    width: 100%;
                    height: 100%;
                    z-index: 10000;
                }
                .dialog-overlay {
                    position: absolute;
                    top: 0;
                    left: 0;
                    width: 100%;
                    height: 100%;
                    background: rgba(0, 0, 0, 0.5);
                    display: flex;
                    justify-content: center;
                    align-items: center;
                }
                .dialog-content {
                    background: white;
                    padding: 20px;
                    border-radius: 8px;
                    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
                    min-width: 300px;
                }
                .dialog-message {
                    margin-bottom: 20px;
                }
                .dialog-buttons {
                    display: flex;
                    justify-content: flex-end;
                    gap: 10px;
                }
                .dialog-buttons button {
                    padding: 8px 16px;
                    border: none;
                    border-radius: 4px;
                    cursor: pointer;
                }
                .btn-confirm {
                    background: #007bff;
                    color: white;
                }
                .btn-cancel {
                    background: #6c757d;
                    color: white;
                }
            `;
            document.head.appendChild(style);
        }
    }
}

// 使用自定义对话框
// const dialog = new CustomDialog();
// dialog.show('确定要删除这个项目吗？').then(result => {
//     if (result) {
//         console.log('用户确认删除');
//     } else {
//         console.log('用户取消删除');
//     }
// });

// 窗口存储
function windowStorage() {
    // localStorage - 持久存储
    localStorage.setItem('username', 'john');
    const username = localStorage.getItem('username');
    localStorage.removeItem('username');
    
    // sessionStorage - 会话存储
    sessionStorage.setItem('sessionData', 'temp');
    const sessionData = sessionStorage.getItem('sessionData');
    
    // 存储复杂对象
    const user = { name: 'John', age: 30 };
    localStorage.setItem('user', JSON.stringify(user));
    const storedUser = JSON.parse(localStorage.getItem('user') || '{}');
}

// 窗口通信
function windowCommunication() {
    // PostMessage API
    const newWindow = window.open('https://example.com', 'target');
    
    // 发送消息
    newWindow.postMessage({
        type: 'greeting',
        message: 'Hello from parent window'
    }, 'https://example.com');
    
    // 接收消息
    window.addEventListener('message', (event) => {
        // 安全检查
        if (event.origin !== 'https://example.com') {
            return;
        }
        
        console.log('收到消息:', event.data);
    });
}

// 窗口错误处理
window.addEventListener('error', (event) => {
    console.error('全局错误:', event.error);
    // 可以发送错误报告到服务器
});

window.addEventListener('unhandledrejection', (event) => {
    console.error('未处理的 Promise 拒绝:', event.reason);
    event.preventDefault(); // 阻止默认的错误处理
});

// 窗口性能监控
class WindowPerformance {
    static getMetrics() {
        return {
            // 导航时间
            navigation: performance.getEntriesByType('navigation')[0],
            // 资源加载时间
            resources: performance.getEntriesByType('resource'),
            // 内存使用情况
            memory: performance.memory || {},
            // 用户计时
            measures: performance.getEntriesByType('measure')
        };
    }
    
    static mark(name) {
        performance.mark(name);
    }
    
    static measure(name, startMark, endMark) {
        performance.measure(name, startMark, endMark);
    }
    
    static getTiming() {
        return performance.timing;
    }
}

// 窗口实用工具类
class WindowUtils {
    // 获取视口尺寸
    static getViewportSize() {
        return {
            width: window.innerWidth || document.documentElement.clientWidth,
            height: window.innerHeight || document.documentElement.clientHeight
        };
    }
    
    // 检查是否为移动设备
    static isMobile() {
        return /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent);
    }
    
    // 滚动到顶部
    static scrollToTop() {
        window.scrollTo({
            top: 0,
            behavior: 'smooth'
        });
    }
    
    // 滚动到元素
    static scrollToElement(element, offset = 0) {
        const rect = element.getBoundingClientRect();
        const scrollTop = window.pageYOffset || document.documentElement.scrollTop;
        const targetPosition = rect.top + scrollTop - offset;
        
        window.scrollTo({
            top: targetPosition,
            behavior: 'smooth'
        });
    }
    
    // 防抖 resize 事件
    static onResize(callback, delay = 300) {
        let timeoutId;
        return window.addEventListener('resize', () => {
            clearTimeout(timeoutId);
            timeoutId = setTimeout(callback, delay);
        });
    }
    
    // 节流 scroll 事件
    static onScroll(callback, delay = 100) {
        let ticking = false;
        return window.addEventListener('scroll', () => {
            if (!ticking) {
                requestAnimationFrame(() => {
                    callback();
                    ticking = false;
                });
                ticking = true;
            }
        });
    }
    
    // 检测网络状态
    static isOnline() {
        return navigator.onLine;
    }
    
    // 监听网络状态变化
    static onNetworkChange(callback) {
        window.addEventListener('online', () => callback(true));
        window.addEventListener('offline', () => callback(false));
    }
}

// 使用示例
console.log('视口尺寸:', WindowUtils.getViewportSize());
console.log('是否为移动设备:', WindowUtils.isMobile());

WindowUtils.onResize(() => {
    console.log('窗口大小改变:', WindowUtils.getViewportSize());
});

WindowUtils.onScroll(() => {
    console.log('滚动位置:', window.scrollY);
});

WindowUtils.onNetworkChange((isOnline) => {
    console.log('网络状态:', isOnline ? '在线' : '离线');
});
```

### 2. location 和 history 对象

```javascript
// location 对象操作

// location 对象属性
console.log('Location 信息:', {
    href: location.href, // 完整 URL
    protocol: location.protocol, // 协议 (http:, https:)
    host: location.host, // 主机名和端口
    hostname: location.hostname, // 主机名
    port: location.port, // 端口
    pathname: location.pathname, // 路径
    search: location.search, // 查询字符串
    hash: location.hash, // 锚点
    origin: location.origin // 源 (协议 + 主机名 + 端口)
});

// URL 操作
function urlOperations() {
    // 修改 URL
    location.assign('https://example.com'); // 导航到新页面
    location.replace('https://example.com'); // 替换当前页面
    location.reload(); // 重新加载页面
    
    // 修改部分 URL
    location.hash = '#section1'; // 修改锚点
    location.search = '?param=value'; // 修改查询参数
}

// 查询参数处理
class URLParams {
    // 获取查询参数
    static get(name) {
        const urlParams = new URLSearchParams(location.search);
        return urlParams.get(name);
    }
    
    // 设置查询参数
    static set(name, value) {
        const urlParams = new URLSearchParams(location.search);
        urlParams.set(name, value);
        location.search = urlParams.toString();
    }
    
    // 删除查询参数
    static remove(name) {
        const urlParams = new URLSearchParams(location.search);
        urlParams.delete(name);
        location.search = urlParams.toString();
    }
    
    // 获取所有查询参数
    static getAll() {
        const urlParams = new URLSearchParams(location.search);
        const params = {};
        for (const [key, value] of urlParams.entries()) {
            params[key] = value;
        }
        return params;
    }
    
    // 构建带参数的 URL
    static build(baseUrl, params) {
        const url = new URL(baseUrl);
        Object.keys(params).forEach(key => {
            url.searchParams.set(key, params[key]);
        });
        return url.toString();
    }
}

// 使用示例
console.log('查询参数:', URLParams.getAll());
URLParams.set('page', '2');
URLParams.set('filter', 'active');

// URLSearchParams 实用方法
class URLSearchParamsUtils {
    // 解析查询字符串
    static parse(searchString) {
        const params = new URLSearchParams(searchString);
        const result = {};
        for (const [key, value] of params.entries()) {
            if (result[key]) {
                // 处理多个同名参数
                if (Array.isArray(result[key])) {
                    result[key].push(value);
                } else {
                    result[key] = [result[key], value];
                }
            } else {
                result[key] = value;
            }
        }
        return result;
    }
    
    // 序列化对象为查询字符串
    static stringify(obj) {
        const params = new URLSearchParams();
        Object.keys(obj).forEach(key => {
            const value = obj[key];
            if (Array.isArray(value)) {
                value.forEach(v => params.append(key, v));
            } else {
                params.set(key, value);
            }
        });
        return params.toString();
    }
    
    // 合并查询参数
    static merge(base, additional) {
        const params = new URLSearchParams(base);
        Object.keys(additional).forEach(key => {
            params.set(key, additional[key]);
        });
        return params.toString();
    }
}

// history 对象操作

// history 对象属性
console.log('History 信息:', {
    length: history.length, // 历史记录长度
    state: history.state // 当前状态
});

// history 导航操作
function historyNavigation() {
    history.back(); // 后退
    history.forward(); // 前进
    history.go(-2); // 后退两步
    history.go(1); // 前进一步
}

// HTML5 History API
class HistoryManager {
    // 推入新状态
    static pushState(state, title, url) {
        history.pushState(state, title, url);
    }
    
    // 替换当前状态
    static replaceState(state, title, url) {
        history.replaceState(state, title, url);
    }
    
    // 监听历史记录变化
    static onPopState(callback) {
        window.addEventListener('popstate', (event) => {
            callback(event.state, event);
        });
    }
    
    // 创建 SPA 路由
    static createRouter(routes) {
        const router = {
            routes,
            currentRoute: null,
            
            init() {
                this.handleCurrentRoute();
                this.setupPopStateListener();
            },
            
            handleCurrentRoute() {
                const path = location.pathname;
                const route = this.routes.find(r => r.path === path);
                
                if (route) {
                    this.currentRoute = route;
                    route.handler();
                } else {
                    // 处理 404
                    console.log('路由未找到:', path);
                }
            },
            
            navigate(path, state = {}) {
                const route = this.routes.find(r => r.path === path);
                if (route) {
                    history.pushState(state, route.title || '', path);
                    this.currentRoute = route;
                    route.handler(state);
                }
            },
            
            setupPopStateListener() {
                window.addEventListener('popstate', (event) => {
                    this.handleCurrentRoute();
                });
            }
        };
        
        return router;
    }
}

// 使用 History API 创建 SPA 路由
const router = HistoryManager.createRouter([
    {
        path: '/',
        title: '首页',
        handler: () => {
            console.log('显示首页');
            document.body.innerHTML = '<h1>首页</h1>';
        }
    },
    {
        path: '/about',
        title: '关于我们',
        handler: () => {
            console.log('显示关于我们');
            document.body.innerHTML = '<h1>关于我们</h1>';
        }
    },
    {
        path: '/contact',
        title: '联系我们',
        handler: () => {
            console.log('显示联系我们');
            document.body.innerHTML = '<h1>联系我们</h1>';
        }
    }
]);

// 初始化路由
// router.init();

// 导航到不同页面
// router.navigate('/about', { from: 'home' });

// SPA 路由管理器
class SPARouter {
    constructor() {
        this.routes = new Map();
        this.currentRoute = null;
        this.init();
    }
    
    // 添加路由
    addRoute(path, handler, title = '') {
        this.routes.set(path, { handler, title });
        return this;
    }
    
    // 初始化路由
    init() {
        this.handleRoute();
        window.addEventListener('popstate', () => {
            this.handleRoute();
        });
    }
    
    // 处理当前路由
    handleRoute() {
        const path = this.normalizePath(location.pathname);
        const route = this.routes.get(path);
        
        if (route) {
            this.currentRoute = path;
            document.title = route.title || document.title;
            route.handler();
        } else {
            this.handleNotFound();
        }
    }
    
    // 导航到指定路径
    navigate(path, state = {}, title = '') {
        const normalizedPath = this.normalizePath(path);
        
        if (this.routes.has(normalizedPath)) {
            history.pushState(state, title, normalizedPath);
            this.handleRoute();
        } else {
            console.warn('路由未找到:', normalizedPath);
        }
    }
    
    // 替换当前路由
    replace(path, state = {}, title = '') {
        const normalizedPath = this.normalizePath(path);
        history.replaceState(state, title, normalizedPath);
        this.handleRoute();
    }
    
    // 处理 404
    handleNotFound() {
        console.log('404 - 页面未找到');
        // 可以显示 404 页面
    }
    
    // 标准化路径
    normalizePath(path) {
        return path.replace(/\/+$/, '') || '/';
    }
    
    // 获取当前路由参数
    getParams() {
        return URLSearchParamsUtils.parse(location.search);
    }
    
    // 构建带参数的路由
    buildRoute(path, params = {}) {
        if (Object.keys(params).length === 0) {
            return path;
        }
        const queryString = URLSearchParamsUtils.stringify(params);
        return `${path}?${queryString}`;
    }
}

// 使用 SPA 路由
const spaRouter = new SPARouter();

spaRouter
    .addRoute('/', () => {
        console.log('首页');
    }, '首页')
    .addRoute('/users', () => {
        console.log('用户列表');
    }, '用户列表')
    .addRoute('/users/:id', (params) => {
        console.log('用户详情:', params.id);
    }, '用户详情');

// 页面切换函数
function goToPage(page, params = {}) {
    const route = spaRouter.buildRoute(page, params);
    spaRouter.navigate(route);
}

// URL 工具类
class URLUtils {
    // 解析完整 URL
    static parse(url) {
        const urlObj = new URL(url);
        return {
            protocol: urlObj.protocol,
            hostname: urlObj.hostname,
            port: urlObj.port,
            pathname: urlObj.pathname,
            search: urlObj.search,
            hash: urlObj.hash,
            origin: urlObj.origin,
            params: URLSearchParamsUtils.parse(urlObj.search)
        };
    }
    
    // 构建 URL
    static build(base, path = '', params = {}, hash = '') {
        const url = new URL(base);
        url.pathname = path;
        
        Object.keys(params).forEach(key => {
            url.searchParams.set(key, params[key]);
        });
        
        url.hash = hash;
        return url.toString();
    }
    
    // 检查 URL 是否有效
    static isValid(url) {
        try {
            new URL(url);
            return true;
        } catch {
            return false;
        }
    }
    
    // 获取 URL 的文件扩展名
    static getExtension(url) {
        const path = new URL(url).pathname;
        const match = path.match(/\.([^.]+)$/);
        return match ? match[1] : '';
    }
    
    // 移除 URL 的查询参数
    static removeParams(url) {
        const urlObj = new URL(url);
        urlObj.search = '';
        return urlObj.toString();
    }
    
    // 移除 URL 的锚点
    static removeHash(url) {
        const urlObj = new URL(url);
        urlObj.hash = '';
        return urlObj.toString();
    }
}

// 使用 URL 工具
console.log('解析 URL:', URLUtils.parse('https://example.com/path?param=value#section'));
console.log('构建 URL:', URLUtils.build('https://example.com', '/api/users', { page: 1, limit: 10 }));
console.log('URL 有效性:', URLUtils.isValid('https://example.com'));
```

### 3. navigator 对象信息

```javascript
// navigator 对象 - 浏览器信息和功能检测

// 基本浏览器信息
console.log('浏览器信息:', {
    userAgent: navigator.userAgent,
    appName: navigator.appName,
    appVersion: navigator.appVersion,
    platform: navigator.platform,
    language: navigator.language,
    languages: navigator.languages,
    onLine: navigator.onLine,
    cookieEnabled: navigator.cookieEnabled
});

// 设备和屏幕信息
console.log('设备信息:', {
    userAgent: navigator.userAgent,
    platform: navigator.platform,
    hardwareConcurrency: navigator.hardwareConcurrency, // CPU 核心数
    deviceMemory: navigator.deviceMemory, // 设备内存 (GB)
    maxTouchPoints: navigator.maxTouchPoints // 触摸点数量
});

// 地理位置 API
class GeolocationAPI {
    // 获取当前位置
    static getCurrentPosition(options = {}) {
        return new Promise((resolve, reject) => {
            if (!navigator.geolocation) {
                reject(new Error('浏览器不支持地理位置'));
                return;
            }
            
            navigator.geolocation.getCurrentPosition(
                (position) => {
                    resolve({
                        latitude: position.coords.latitude,
                        longitude: position.coords.longitude,
                        accuracy: position.coords.accuracy,
                        altitude: position.coords.altitude,
                        altitudeAccuracy: position.coords.altitudeAccuracy,
                        heading: position.coords.heading,
                        speed: position.coords.speed,
                        timestamp: position.timestamp
                    });
                },
                (error) => {
                    reject(new Error(this.getErrorMessage(error)));
                },
                {
                    enableHighAccuracy: options.highAccuracy || false,
                    timeout: options.timeout || 10000,
                    maximumAge: options.maximumAge || 0
                }
            );
        });
    }
    
    // 监听位置变化
    static watchPosition(callback, options = {}) {
        if (!navigator.geolocation) {
            throw new Error('浏览器不支持地理位置');
        }
        
        return navigator.geolocation.watchPosition(
            (position) => {
                callback({
                    latitude: position.coords.latitude,
                    longitude: position.coords.longitude,
                    accuracy: position.coords.accuracy,
                    timestamp: position.timestamp
                });
            },
            (error) => {
                console.error('位置获取失败:', this.getErrorMessage(error));
            },
            {
                enableHighAccuracy: options.highAccuracy || false,
                timeout: options.timeout || 10000,
                maximumAge: options.maximumAge || 0
            }
        );
    }
    
    // 停止监听位置
    static clearWatch(watchId) {
        if (navigator.geolocation) {
            navigator.geolocation.clearWatch(watchId);
        }
    }
    
    // 获取错误信息
    static getErrorMessage(error) {
        const errorMessages = {
            1: '用户拒绝了位置请求',
            2: '位置信息不可用',
            3: '获取位置信息超时'
        };
        return errorMessages[error.code] || '未知错误';
    }
}

// 使用地理位置 API
// GeolocationAPI.getCurrentPosition({ highAccuracy: true, timeout: 5000 })
//     .then(position => {
//         console.log('当前位置:', position);
//     })
//     .catch(error => {
//         console.error('获取位置失败:', error.message);
//     });

// 媒体设备 API
class MediaDevicesAPI {
    // 获取媒体设备列表
    static async getDevices() {
        if (!navigator.mediaDevices || !navigator.mediaDevices.enumerateDevices) {
            throw new Error('浏览器不支持媒体设备枚举');
        }
        
        try {
            const devices = await navigator.mediaDevices.enumerateDevices();
            return {
                audioinput: devices.filter(device => device.kind === 'audioinput'),
                audiooutput: devices.filter(device => device.kind === 'audiooutput'),
                videoinput: devices.filter(device => device.kind === 'videoinput')
            };
        } catch (error) {
            throw new Error(`获取设备列表失败: ${error.message}`);
        }
    }
    
    // 获取用户媒体 (摄像头/麦克风)
    static async getUserMedia(constraints = { video: true, audio: true }) {
        if (!navigator.mediaDevices || !navigator.mediaDevices.getUserMedia) {
            throw new Error('浏览器不支持 getUserMedia');
        }
        
        try {
            const stream = await navigator.mediaDevices.getUserMedia(constraints);
            return stream;
        } catch (error) {
            throw new Error(`获取媒体流失败: ${error.message}`);
        }
    }
    
    // 检查媒体设备支持
    static isSupported() {
        return !!(navigator.mediaDevices && navigator.mediaDevices.getUserMedia);
    }
    
    // 获取显示媒体 (屏幕共享)
    static async getDisplayMedia(constraints = { video: true }) {
        if (!navigator.mediaDevices || !navigator.mediaDevices.getDisplayMedia) {
            throw new Error('浏览器不支持屏幕共享');
        }
        
        try {
            const stream = await navigator.mediaDevices.getDisplayMedia(constraints);
            return stream;
        } catch (error) {
            throw new Error(`获取显示媒体失败: ${error.message}`);
        }
    }
}

// 使用媒体设备 API
// MediaDevicesAPI.getDevices()
//     .then(devices => {
//         console.log('音频输入设备:', devices.audioinput);
//         console.log('视频输入设备:', devices.videoinput);
//     })
//     .catch(error => {
//         console.error('获取设备失败:', error.message);
//     });

// 网络信息 API
class NetworkInformation {
    // 获取网络连接信息
    static getConnectionInfo() {
        const connection = navigator.connection || 
                          navigator.mozConnection || 
                          navigator.webkitConnection;
        
        if (!connection) {
            return null;
        }
        
        return {
            effectiveType: connection.effectiveType, // 网络类型 (4g, 3g, 2g, slow-2g)
            downlink: connection.downlink, // 下行速度 (Mbps)
            downlinkMax: connection.downlinkMax, // 最大下行速度
            rtt: connection.rtt, // 往返时间 (ms)
            saveData: connection.saveData, // 是否启用数据保存模式
            type: connection.type // 连接类型
        };
    }
    
    // 监听网络变化
    static onConnectionChange(callback) {
        const connection = navigator.connection || 
                          navigator.mozConnection || 
                          navigator.webkitConnection;
        
        if (connection) {
            connection.addEventListener('change', () => {
                callback(this.getConnectionInfo());
            });
        }
    }
    
    // 检查是否为慢速网络
    static isSlowNetwork() {
        const info = this.getConnectionInfo();
        if (!info) return false;
        
        return info.effectiveType === 'slow-2g' || 
               info.effectiveType === '2g' ||
               (info.downlink && info.downlink < 0.5);
    }
}

// 使用网络信息 API
const networkInfo = NetworkInformation.getConnectionInfo();
console.log('网络信息:', networkInfo);

NetworkInformation.onConnectionChange((info) => {
    console.log('网络连接变化:', info);
});

// 剪贴板 API
class ClipboardAPI {
    // 读取文本
    static async readText() {
        if (!navigator.clipboard || !navigator.clipboard.readText) {
            throw new Error('浏览器不支持剪贴板读取');
        }
        
        try {
            const text = await navigator.clipboard.readText();
            return text;
        } catch (error) {
            throw new Error(`读取剪贴板失败: ${error.message}`);
        }
    }
    
    // 写入文本
    static async writeText(text) {
        if (!navigator.clipboard || !navigator.clipboard.writeText) {
            throw new Error('浏览器不支持剪贴板写入');
        }
        
        try {
            await navigator.clipboard.writeText(text);
            return true;
        } catch (error) {
            throw new Error(`写入剪贴板失败: ${error.message}`);
        }
    }
    
    // 检查权限
    static async checkPermission() {
        if (!navigator.permissions) {
            return 'unknown';
        }
        
        try {
            const permission = await navigator.permissions.query({ name: 'clipboard-read' });
            return permission.state;
        } catch {
            return 'denied';
        }
    }
}

// 使用剪贴板 API
// ClipboardAPI.writeText('Hello, World!')
//     .then(() => {
//         console.log('文本已复制到剪贴板');
//     })
//     .catch(error => {
//         console.error('复制失败:', error.message);
//     });

// 通知 API
class NotificationAPI {
    // 请求通知权限
    static async requestPermission() {
        if (!('Notification' in window)) {
            throw new Error('浏览器不支持通知');
        }
        
        if (Notification.permission === 'granted') {
            return 'granted';
        }
        
        try {
            const permission = await Notification.requestPermission();
            return permission;
        } catch (error) {
            throw new Error(`请求通知权限失败: ${error.message}`);
        }
    }
    
    // 显示通知
    static showNotification(title, options = {}) {
        if (!('Notification' in window)) {
            throw new Error('浏览器不支持通知');
        }
        
        if (Notification.permission === 'granted') {
            return new Notification(title, options);
        } else {
            throw new Error('通知权限未授予');
        }
    }
    
    // 检查权限状态
    static getPermission() {
        if (!('Notification' in window)) {
            return 'unsupported';
        }
        return Notification.permission;
    }
}

// 使用通知 API
// NotificationAPI.requestPermission()
//     .then(permission => {
//         if (permission === 'granted') {
//             NotificationAPI.showNotification('Hello!', {
//                 body: '这是通知内容',
//                 icon: '/icon.png'
//             });
//         }
//     })
//     .catch(error => {
//         console.error('请求通知权限失败:', error.message);
//     });

// 电池状态 API (已废弃，但仍有浏览器支持)
class BatteryAPI {
    // 获取电池信息
    static async getBatteryInfo() {
        if (!navigator.getBattery) {
            throw new Error('浏览器不支持电池状态 API');
        }
        
        try {
            const battery = await navigator.getBattery();
            return {
                charging: battery.charging,
                chargingTime: battery.chargingTime,
                dischargingTime: battery.dischargingTime,
                level: battery.level,
                addEventListener: (event, callback) => {
                    battery.addEventListener(event, callback);
                }
            };
        } catch (error) {
            throw new Error(`获取电池信息失败: ${error.message}`);
        }
    }
}

// 浏览器功能检测工具
class FeatureDetector {
    // 检测 Web Storage 支持
    static supportsWebStorage() {
        try {
            const test = '__storage_test__';
            localStorage.setItem(test, test);
            localStorage.removeItem(test);
            return true;
        } catch {
            return false;
        }
    }
    
    // 检测 IndexedDB 支持
    static supportsIndexedDB() {
        return !!window.indexedDB;
    }
    
    // 检测 Service Worker 支持
    static supportsServiceWorker() {
        return 'serviceWorker' in navigator;
    }
    
    // 检测 WebGL 支持
    static supportsWebGL() {
        try {
            const canvas = document.createElement('canvas');
            return !!(canvas.getContext && canvas.getContext('webgl'));
        } catch {
            return false;
        }
    }
    
    // 检测 Web Workers 支持
    static supportsWebWorkers() {
        return !!window.Worker;
    }
    
    // 检测 Fetch API 支持
    static supportsFetch() {
        return !!window.fetch;
    }
    
    // 检测 Promise 支持
    static supportsPromise() {
        return !!window.Promise;
    }
    
    // 综合功能检测
    static getSupportedFeatures() {
        return {
            webStorage: this.supportsWebStorage(),
            indexedDB: this.supportsIndexedDB(),
            serviceWorker: this.supportsServiceWorker(),
            webGL: this.supportsWebGL(),
            webWorkers: this.supportsWebWorkers(),
            fetch: this.supportsFetch(),
            promise: this.supportsPromise(),
            geolocation: !!navigator.geolocation,
            mediaDevices: !!(navigator.mediaDevices && navigator.mediaDevices.getUserMedia),
            notifications: 'Notification' in window,
            clipboard: !!(navigator.clipboard && navigator.clipboard.writeText),
            battery: !!navigator.getBattery,
            vibration: 'vibrate' in navigator,
            online: 'onLine' in navigator
        };
    }
}

// 使用功能检测
console.log('浏览器支持的功能:', FeatureDetector.getSupportedFeatures());

// 浏览器识别和兼容性处理
class BrowserDetector {
    constructor() {
        this.userAgent = navigator.userAgent;
    }
    
    // 检测浏览器类型
    getBrowser() {
        const browsers = [
            { name: 'Chrome', pattern: /Chrome\/(\d+)/ },
            { name: 'Firefox', pattern: /Firefox\/(\d+)/ },
            { name: 'Safari', pattern: /Safari\/(\d+)/ },
            { name: 'Edge', pattern: /Edge\/(\d+)/ },
            { name: 'IE', pattern: /MSIE (\d+)|Trident.*rv:(\d+)/ }
        ];
        
        for (const browser of browsers) {
            const match = this.userAgent.match(browser.pattern);
            if (match) {
                return {
                    name: browser.name,
                    version: parseInt(match[1] || match[2])
                };
            }
        }
        
        return { name: 'Unknown', version: 0 };
    }
    
    // 检测是否为移动浏览器
    isMobile() {
        return /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(this.userAgent);
    }
    
    // 检测操作系统
    getOS() {
        const osPatterns = [
            { name: 'Windows', pattern: /Windows NT (\d+\.\d+)/ },
            { name: 'macOS', pattern: /Mac OS X (\d+[._]\d+)/ },
            { name: 'Linux', pattern: /Linux/ },
            { name: 'Android', pattern: /Android (\d+\.\d+)/ },
            { name: 'iOS', pattern: /OS (\d+)_(\d+)/ }
        ];
        
        for (const os of osPatterns) {
            const match = this.userAgent.match(os.pattern);
            if (match) {
                return {
                    name: os.name,
                    version: match[1] ? parseFloat(match[1].replace('_', '.')) : null
                };
            }
        }
        
        return { name: 'Unknown', version: null };
    }
    
    // 检测触摸支持
    supportsTouch() {
        return 'ontouchstart' in window || navigator.maxTouchPoints > 0;
    }
    
    // 获取设备信息
    getDeviceInfo() {
        return {
            browser: this.getBrowser(),
            os: this.getOS(),
            isMobile: this.isMobile(),
            supportsTouch: this.supportsTouch(),
            userAgent: this.userAgent,
            language: navigator.language,
            languages: navigator.languages,
            cookiesEnabled: navigator.cookieEnabled,
            onLine: navigator.onLine
        };
    }
}

// 使用浏览器检测
const detector = new BrowserDetector();
console.log('设备信息:', detector.getDeviceInfo());

// 根据浏览器特性提供降级方案
class CompatibilityManager {
    constructor() {
        this.features = FeatureDetector.getSupportedFeatures();
        this.browser = new BrowserDetector().getBrowser();
    }
    
    // 选择合适的存储方案
    getStorage() {
        if (this.features.webStorage) {
            return {
                set: (key, value) => localStorage.setItem(key, value),
                get: (key) => localStorage.getItem(key),
                remove: (key) => localStorage.removeItem(key)
            };
        } else {
            // 降级到 cookie
            return {
                set: (key, value) => this.setCookie(key, value),
                get: (key) => this.getCookie(key),
                remove: (key) => this.removeCookie(key)
            };
        }
    }
    
    // Cookie 操作方法
    setCookie(name, value, days = 7) {
        const expires = new Date();
        expires.setTime(expires.getTime() + (days * 24 * 60 * 60 * 1000));
        document.cookie = `${name}=${value};expires=${expires.toUTCString()};path=/`;
    }
    
    getCookie(name) {
        const nameEQ = name + "=";
        const ca = document.cookie.split(';');
        for (let i = 0; i < ca.length; i++) {
            let c = ca[i];
            while (c.charAt(0) === ' ') c = c.substring(1, c.length);
            if (c.indexOf(nameEQ) === 0) return c.substring(nameEQ.length, c.length);
        }
        return null;
    }
    
    removeCookie(name) {
        this.setCookie(name, "", -1);
    }
    
    // 选择合适的请求方法
    getRequestMethod() {
        if (this.features.fetch) {
            return this.fetchRequest.bind(this);
        } else {
            return this.xhrRequest.bind(this);
        }
    }
    
    async fetchRequest(url, options = {}) {
        const response = await fetch(url, options);
        return response.json();
    }
    
    xhrRequest(url, options = {}) {
        return new Promise((resolve, reject) => {
            const xhr = new XMLHttpRequest();
            xhr.open(options.method || 'GET', url);
            
            xhr.onload = () => {
                if (xhr.status >= 200 && xhr.status < 300) {
                    resolve(JSON.parse(xhr.responseText));
                } else {
                    reject(new Error(`HTTP ${xhr.status}: ${xhr.statusText}`));
                }
            };
            
            xhr.onerror = () => reject(new Error('网络错误'));
            xhr.send(options.body);
        });
    }
}

// 使用兼容性管理器
const compatManager = new CompatibilityManager();
const storage = compatManager.getStorage();
const request = compatManager.getRequestMethod();

// 存储数据
storage.set('user', 'John Doe');

// 发起请求
// request('/api/data')
//     .then(data => console.log(data))
//     .catch(error => console.error(error));
```

### 4. 定时器和动画控制

```javascript
// 定时器和动画控制

// 基本定时器
// setTimeout - 延迟执行
const timeoutId = setTimeout(() => {
    console.log('延迟执行的代码');
}, 1000);

// setInterval - 重复执行
const intervalId = setInterval(() => {
    console.log('重复执行的代码');
}, 2000);

// 清除定时器
clearTimeout(timeoutId);
clearInterval(intervalId);

// 定时器管理类
class TimerManager {
    constructor() {
        this.timeouts = new Map();
        this.intervals = new Map();
        this.counter = 0;
    }
    
    // 设置带标签的 timeout
    setTimeout(label, callback, delay, ...args) {
        const id = ++this.counter;
        const timeoutId = setTimeout(() => {
            callback(...args);
            this.timeouts.delete(label);
        }, delay);
        
        this.timeouts.set(label, { id: timeoutId, label });
        return id;
    }
    
    // 设置带标签的 interval
    setInterval(label, callback, delay, ...args) {
        const id = ++this.counter;
        const intervalId = setInterval(() => {
            callback(...args);
        }, delay);
        
        this.intervals.set(label, { id: intervalId, label });
        return id;
    }
    
    // 清除特定标签的定时器
    clearTimeout(label) {
        const timer = this.timeouts.get(label);
        if (timer) {
            clearTimeout(timer.id);
            this.timeouts.delete(label);
        }
    }
    
    // 清除特定标签的间隔
    clearInterval(label) {
        const timer = this.intervals.get(label);
        if (timer) {
            clearInterval(timer.id);
            this.intervals.delete(label);
        }
    }
    
    // 清除所有定时器
    clearAll() {
        this.timeouts.forEach(timer => clearTimeout(timer.id));
        this.intervals.forEach(timer => clearInterval(timer.id));
        this.timeouts.clear();
        this.intervals.clear();
    }
    
    // 获取定时器数量
    getCount() {
        return {
            timeouts: this.timeouts.size,
            intervals: this.intervals.size
        };
    }
}

// 使用定时器管理器
const timerManager = new TimerManager();

timerManager.setTimeout('userNotification', () => {
    console.log('用户通知');
}, 3000);

timerManager.setInterval('heartbeat', () => {
    console.log('心跳检测');
}, 5000);

// requestAnimationFrame - 动画帧
class AnimationFrameManager {
    constructor() {
        this.animations = new Map();
        this.frameId = null;
        this.running = false;
    }
    
    // 添加动画
    addAnimation(id, callback) {
        this.animations.set(id, callback);
        if (!this.running) {
            this.start();
        }
    }
    
    // 移除动画
    removeAnimation(id) {
        this.animations.delete(id);
        if (this.animations.size === 0) {
            this.stop();
        }
    }
    
    // 开始动画循环
    start() {
        if (this.running) return;
        
        this.running = true;
        const animate = (timestamp) => {
            if (this.animations.size > 0) {
                this.animations.forEach(callback => {
                    callback(timestamp);
                });
                this.frameId = requestAnimationFrame(animate);
            } else {
                this.running = false;
            }
        };
        
        this.frameId = requestAnimationFrame(animate);
    }
    
    // 停止动画循环
    stop() {
        if (this.frameId) {
            cancelAnimationFrame(this.frameId);
            this.frameId = null;
        }
        this.running = false;
    }
    
    // 清除所有动画
    clear() {
        this.animations.clear();
        this.stop();
    }
}

// 使用动画帧管理器
const animationManager = new AnimationFrameManager();

// 创建平滑动画
class SmoothAnimation {
    constructor(element, duration = 1000) {
        this.element = element;
        this.duration = duration;
        this.startTime = null;
        this.startValue = 0;
        this.endValue = 100;
    }
    
    animate() {
        const animate = (timestamp) => {
            if (!this.startTime) this.startTime = timestamp;
            
            const elapsed = timestamp - this.startTime;
            const progress = Math.min(elapsed / this.duration, 1);
            
            // 缓动函数
            const easeProgress = this.easeOutCubic(progress);
            const currentValue = this.startValue + (this.endValue - this.startValue) * easeProgress;
            
            this.element.style.transform = `translateX(${currentValue}px)`;
            
            if (progress < 1) {
                requestAnimationFrame(animate);
            }
        };
        
        requestAnimationFrame(animate);
    }
    
    // 缓动函数
    easeOutCubic(t) {
        return 1 - Math.pow(1 - t, 3);
    }
    
    easeInOutQuad(t) {
        return t < 0.5 ? 2 * t * t : -1 + (4 - 2 * t) * t;
    }
}

// 高级动画控制类
class AdvancedAnimator {
    constructor() {
        this.animations = new Map();
        this.globalId = 0;
    }
    
    // 创建补间动画
    tween(element, properties, duration, options = {}) {
        const id = ++this.globalId;
        const startTime = performance.now();
        const startValues = {};
        const endValues = properties;
        
        // 获取起始值
        Object.keys(properties).forEach(prop => {
            if (prop === 'x' || prop === 'y' || prop === 'translateX' || prop === 'translateY') {
                const transform = getComputedStyle(element).transform;
                // 简化的变换值获取
                startValues[prop] = 0;
            } else if (prop === 'opacity') {
                startValues[prop] = parseFloat(getComputedStyle(element).opacity) || 1;
            } else {
                startValues[prop] = parseFloat(getComputedStyle(element)[prop]) || 0;
            }
        });
        
        const animate = (currentTime) => {
            const elapsed = currentTime - startTime;
            const progress = Math.min(elapsed / duration, 1);
            
            // 应用缓动函数
            const easedProgress = this.applyEasing(progress, options.easing || 'linear');
            
            // 更新属性
            Object.keys(properties).forEach(prop => {
                const startValue = startValues[prop];
                const endValue = endValues[prop];
                const currentValue = startValue + (endValue - startValue) * easedProgress;
                
                if (prop === 'x' || prop === 'translateX') {
                    this.updateTransform(element, 'translateX', currentValue);
                } else if (prop === 'y' || prop === 'translateY') {
                    this.updateTransform(element, 'translateY', currentValue);
                } else if (prop === 'scale') {
                    this.updateTransform(element, 'scale', currentValue);
                } else {
                    element.style[prop] = this.formatValue(prop, currentValue);
                }
            });
            
            if (progress < 1) {
                requestAnimationFrame(animate);
            } else {
                // 动画完成回调
                if (options.onComplete) {
                    options.onComplete();
                }
            }
        };
        
        requestAnimationFrame(animate);
        return id;
    }
    
    // 更新变换属性
    updateTransform(element, property, value) {
        const currentTransform = element.style.transform || '';
        const regex = new RegExp(`${property}\\([^)]*\\)`, 'g');
        const newValue = `${property}(${this.formatValue(property, value)})`;
        
        if (regex.test(currentTransform)) {
            element.style.transform = currentTransform.replace(regex, newValue);
        } else {
            element.style.transform = `${currentTransform} ${newValue}`.trim();
        }
    }
    
    // 格式化值
    formatValue(property, value) {
        if (property.includes('translate') || property === 'x' || property === 'y') {
            return `${value}px`;
        } else if (property === 'scale' || property === 'opacity') {
            return value;
        } else {
            return `${value}px`;
        }
    }
    
    // 应用缓动函数
    applyEasing(progress, easing) {
        const easingFunctions = {
            linear: t => t,
            easeInQuad: t => t * t,
            easeOutQuad: t => t * (2 - t),
            easeInOutQuad: t => t < 0.5 ? 2 * t * t : -1 + (4 - 2 * t) * t,
            easeInCubic: t => t * t * t,
            easeOutCubic: t => (--t) * t * t + 1,
            easeInOutCubic: t => t < 0.5 ? 4 * t * t * t : (t - 1) * (2 * t - 2) * (2 * t - 2) + 1
        };
        
        return easingFunctions[easing] ? easingFunctions[easing](progress) : progress;
    }
    
    // 串行动画
    sequence(animations) {
        let index = 0;
        
        const runNext = () => {
            if (index < animations.length) {
                const animation = animations[index];
                const options = {
                    ...animation.options,
                    onComplete: () => {
                        if (animation.options && animation.options.onComplete) {
                            animation.options.onComplete();
                        }
                        index++;
                        runNext();
                    }
                };
                
                this.tween(animation.element, animation.properties, animation.duration, options);
            }
        };
        
        runNext();
    }
    
    // 并行动画
    parallel(animations) {
        animations.forEach(animation => {
            this.tween(animation.element, animation.properties, animation.duration, animation.options);
        });
    }
}

// 使用高级动画器
const animator = new AdvancedAnimator();

// 创建动画元素
const animatedElement = document.createElement('div');
animatedElement.style.width = '50px';
animatedElement.style.height = '50px';
animatedElement.style.backgroundColor = 'red';
animatedElement.style.position = 'absolute';
animatedElement.style.left = '0px';
animatedElement.style.top = '0px';

document.body.appendChild(animatedElement);

// 执行补间动画
// animator.tween(animatedElement, {
//     x: 200,
//     y: 100,
//     scale: 1.5,
//     opacity: 0.5
// }, 2000, {
//     easing: 'easeOutCubic',
//     onComplete: () => console.log('动画完成')
// });

// 定时器工具类
class TimerUtils {
    // 防抖函数
    static debounce(func, delay) {
        let timeoutId;
        return function(...args) {
            clearTimeout(timeoutId);
            timeoutId = setTimeout(() => func.apply(this, args), delay);
        };
    }
    
    // 节流函数
    static throttle(func, limit) {
        let inThrottle;
        return function(...args) {
            if (!inThrottle) {
                func.apply(this, args);
                inThrottle = true;
                setTimeout(() => inThrottle = false, limit);
            }
        };
    }
    
    // 精确定时器
    static preciseInterval(callback, interval) {
        let startTime = performance.now();
        let expectedTime = startTime + interval;
        
        const tick = () => {
            const currentTime = performance.now();
            const drift = currentTime - expectedTime;
            
            callback();
            
            expectedTime += interval;
            const nextDelay = Math.max(0, interval - drift);
            
            setTimeout(tick, nextDelay);
        };
        
        setTimeout(tick, interval);
    }
    
    // 延迟执行直到条件满足
    static waitUntil(condition, callback, interval = 100, timeout = 5000) {
        const startTime = Date.now();
        
        const check = () => {
            if (condition()) {
                callback();
            } else if (Date.now() - startTime < timeout) {
                setTimeout(check, interval);
            } else {
                console.warn('等待超时');
            }
        };
        
        check();
    }
    
    // 批量延迟执行
    static batchDelay(tasks, delayBetween = 100) {
        let index = 0;
        
        const executeNext = () => {
            if (index < tasks.length) {
                tasks[index]();
                index++;
                setTimeout(executeNext, delayBetween);
            }
        };
        
        executeNext();
    }
}

// 使用定时器工具
const debouncedSearch = TimerUtils.debounce((query) => {
    console.log('执行搜索:', query);
}, 300);

const throttledScroll = TimerUtils.throttle(() => {
    console.log('处理滚动事件');
}, 100);

// 动画性能优化
class OptimizedAnimation {
    constructor() {
        this.animations = new Map();
        this.rafId = null;
        this.isRunning = false;
    }
    
    // 添加高性能动画
    addAnimation(id, element, updateFunction) {
        this.animations.set(id, {
            element,
            update: updateFunction,
            lastUpdate: 0
        });
        
        if (!this.isRunning) {
            this.start();
        }
    }
    
    // 启动动画循环
    start() {
        if (this.isRunning) return;
        
        this.isRunning = true;
        
        const animate = (timestamp) => {
            if (this.animations.size > 0) {
                this.animations.forEach((animation, id) => {
                    // 可以添加帧率控制
                    animation.update(timestamp);
                    animation.lastUpdate = timestamp;
                });
                
                this.rafId = requestAnimationFrame(animate);
            } else {
                this.isRunning = false;
            }
        };
        
        this.rafId = requestAnimationFrame(animate);
    }
    
    // 移除动画
    removeAnimation(id) {
        this.animations.delete(id);
        if (this.animations.size === 0) {
            this.stop();
        }
    }
    
    // 停止所有动画
    stop() {
        if (this.rafId) {
            cancelAnimationFrame(this.rafId);
            this.rafId = null;
        }
        this.isRunning = false;
    }
    
    // 动画暂停和恢复
    pause() {
        this.stop();
    }
    
    resume() {
        if (this.animations.size > 0) {
            this.start();
        }
    }
}

// 实际应用：进度条动画
class ProgressBar {
    constructor(element, options = {}) {
        this.element = element;
        this.options = {
            duration: options.duration || 1000,
            easing: options.easing || 'easeOutCubic',
            ...options
        };
        this.currentProgress = 0;
    }
    
    setProgress(progress, animate = true) {
        const targetProgress = Math.max(0, Math.min(100, progress));
        
        if (!animate) {
            this.updateProgress(targetProgress);
            return;
        }
        
        const startTime = performance.now();
        const startProgress = this.currentProgress;
        const duration = this.options.duration;
        
        const animateProgress = (currentTime) => {
            const elapsed = currentTime - startTime;
            const progressRatio = Math.min(elapsed / duration, 1);
            
            // 应用缓动
            const easedProgress = this.applyEasing(progressRatio, this.options.easing);
            const currentProgress = startProgress + (targetProgress - startProgress) * easedProgress;
            
            this.updateProgress(currentProgress);
            
            if (progressRatio < 1) {
                requestAnimationFrame(animateProgress);
            }
        };
        
        requestAnimationFrame(animateProgress);
    }
    
    updateProgress(progress) {
        this.currentProgress = progress;
        this.element.style.width = `${progress}%`;
        
        // 可选：更新文本
        const textElement = this.element.querySelector('.progress-text');
        if (textElement) {
            textElement.textContent = `${Math.round(progress)}%`;
        }
    }
    
    applyEasing(t, easing) {
        const functions = {
            linear: t => t,
            easeOutCubic: t => 1 - Math.pow(1 - t, 3),
            easeInOutQuad: t => t < 0.5 ? 2 * t * t : -1 + (4 - 2 * t) * t
        };
        
        return functions[easing] ? functions[easing](t) : t;
    }
    
    // 重置进度条
    reset() {
        this.setProgress(0, false);
    }
    
    // 完成进度条
    complete(callback) {
        this.setProgress(100, true);
        if (callback) {
            setTimeout(callback, this.options.duration);
        }
    }
}

// 创建进度条元素
function createProgressBar() {
    const container = document.createElement('div');
    container.className = 'progress-container';
    container.style.width = '100%';
    container.style.height = '20px';
    container.style.backgroundColor = '#f0f0f0';
    container.style.borderRadius = '10px';
    container.style.overflow = 'hidden';
    
    const bar = document.createElement('div');
    bar.className = 'progress-bar';
    bar.style.height = '100%';
    bar.style.width = '0%';
    bar.style.backgroundColor = '#007bff';
    bar.style.transition = 'width 0.3s ease';
    bar.style.borderRadius = '10px';
    
    container.appendChild(bar);
    return container;
}

// 使用进度条
// const progressBarElement = createProgressBar();
// document.body.appendChild(progressBarElement);
// const progressBar = new ProgressBar(progressBarElement.querySelector('.progress-bar'));
// progressBar.setProgress(50);

// 动画性能监控
class AnimationPerformance {
    constructor() {
        this.metrics = [];
        this.frameCount = 0;
        this.lastTime = performance.now();
    }
    
    // 监控帧率
    monitorFPS(callback) {
        const measureFPS = (timestamp) => {
            this.frameCount++;
            
            if (timestamp >= this.lastTime + 1000) {
                const fps = Math.round((this.frameCount * 1000) / (timestamp - this.lastTime));
                this.metrics.push({ timestamp, fps });
                
                if (callback) callback(fps);
                
                this.frameCount = 0;
                this.lastTime = timestamp;
            }
            
            requestAnimationFrame(measureFPS);
        };
        
        requestAnimationFrame(measureFPS);
    }
    
    // 获取性能报告
    getReport() {
        if (this.metrics.length === 0) return null;
        
        const fpsValues = this.metrics.map(m => m.fps);
        const averageFPS = fpsValues.reduce((a, b) => a + b, 0) / fpsValues.length;
        const minFPS = Math.min(...fpsValues);
        const maxFPS = Math.max(...fpsValues);
        
        return {
            average: Math.round(averageFPS),
            min: minFPS,
            max: maxFPS,
            samples: this.metrics.length
        };
    }
    
    // 检查性能问题
    checkPerformance() {
        const report = this.getReport();
        if (!report) return null;
        
        const issues = [];
        
        if (report.average < 30) {
            issues.push('平均帧率过低');
        }
        
        if (report.min < 15) {
            issues.push('最低帧率过低');
        }
        
        return issues.length > 0 ? issues : null;
    }
}

// 使用性能监控
const perfMonitor = new AnimationPerformance();
// perfMonitor.monitorFPS((fps) => {
//     console.log(`当前 FPS: ${fps}`);
// });
```

## 9.3 事件处理系统

### 1. 事件流和事件冒泡

```javascript
// 事件流和事件冒泡

// 事件流的三个阶段
// 1. 捕获阶段 (Capture Phase) - 从 document 到目标元素
// 2. 目标阶段 (Target Phase) - 到达目标元素
// 3. 冒泡阶段 (Bubbling Phase) - 从目标元素到 document

// 事件流示例
document.addEventListener('click', (event) => {
    console.log('Document - 捕获阶段', event.eventPhase); // 1
}, true); // true 表示捕获阶段

document.addEventListener('click', (event) => {
    console.log('Document - 冒泡阶段', event.eventPhase); // 3
}, false); // false 表示冒泡阶段

const container = document.getElementById('container');
container.addEventListener('click', (event) => {
    console.log('Container - 捕获阶段', event.eventPhase); // 1
}, true);

container.addEventListener('click', (event) => {
    console.log('Container - 冒泡阶段', event.eventPhase); // 3
}, false);

const button = document.getElementById('button');
button.addEventListener('click', (event) => {
    console.log('Button - 目标阶段', event.eventPhase); // 2
});

// 事件冒泡示例
const outer = document.getElementById('outer');
const middle = document.getElementById('middle');
const inner = document.getElementById('inner');

outer.addEventListener('click', (event) => {
    console.log('Outer clicked');
});

middle.addEventListener('click', (event) => {
    console.log('Middle clicked');
    // event.stopPropagation(); // 阻止事件继续冒泡
    // event.stopImmediatePropagation(); // 阻止同级监听器执行
});

inner.addEventListener('click', (event) => {
    console.log('Inner clicked');
    // event.stopPropagation(); // 阻止事件继续冒泡
});

// 事件捕获示例
outer.addEventListener('click', (event) => {
    console.log('Outer capture');
}, true);

middle.addEventListener('click', (event) => {
    console.log('Middle capture');
}, true);

inner.addEventListener('click', (event) => {
    console.log('Inner capture');
    // event.stopPropagation(); // 阻止事件继续捕获
}, true);

// 事件对象属性详解
function eventObjectDemo(event) {
    console.log('=== 事件对象属性 ===');
    console.log('type:', event.type); // 事件类型
    console.log('target:', event.target); // 实际触发事件的元素
    console.log('currentTarget:', event.currentTarget); // 当前处理事件的元素
    console.log('eventPhase:', event.eventPhase); // 事件阶段 (1:捕获, 2:目标, 3:冒泡)
    console.log('bubbles:', event.bubbles); // 是否冒泡
    console.log('cancelable:', event.cancelable); // 是否可取消默认行为
    console.log('defaultPrevented:', event.defaultPrevented); // 是否已阻止默认行为
    console.log('timeStamp:', event.timeStamp); // 事件时间戳
    console.log('isTrusted:', event.isTrusted); // 是否是用户触发的事件
}

// 阻止事件传播
function stopEventPropagation() {
    const button = document.getElementById('myButton');
    
    button.addEventListener('click', (event) => {
        console.log('按钮点击');
        
        // 阻止事件冒泡
        event.stopPropagation();
        
        // 阻止同级监听器执行
        // event.stopImmediatePropagation();
        
        // 阻止默认行为
        event.preventDefault();
    });
}

// 事件委托原理
class EventDelegationDemo {
    constructor() {
        this.setupDelegation();
    }
    
    setupDelegation() {
        // 在父容器上监听事件
        const container = document.getElementById('container');
        
        container.addEventListener('click', (event) => {
            const target = event.target;
            
            // 根据目标元素的特性处理不同事件
            if (target.matches('.button-delete')) {
                this.handleDelete(target, event);
            } else if (target.matches('.button-edit')) {
                this.handleEdit(target, event);
            } else if (target.matches('li')) {
                this.handleListItemClick(target, event);
            }
        });
    }
    
    handleDelete(button, event) {
        console.log('删除按钮点击');
        const item = button.closest('.item');
        if (item) {
            item.remove();
        }
    }
    
    handleEdit(button, event) {
        console.log('编辑按钮点击');
        const item = button.closest('.item');
        if (item) {
            const text = item.querySelector('.text');
            if (text) {
                text.contentEditable = true;
                text.focus();
            }
        }
    }
    
    handleListItemClick(item, event) {
        console.log('列表项点击:', item.textContent);
    }
}

// 事件流控制工具
class EventFlowController {
    // 在捕获阶段处理事件
    static capture(element, eventType, handler) {
        element.addEventListener(eventType, handler, true);
    }
    
    // 在冒泡阶段处理事件
    static bubble(element, eventType, handler) {
        element.addEventListener(eventType, handler, false);
    }
    
    // 一次性事件处理
    static once(element, eventType, handler, useCapture = false) {
        const onceHandler = (event) => {
            handler(event);
            element.removeEventListener(eventType, onceHandler, useCapture);
        };
        
        element.addEventListener(eventType, onceHandler, useCapture);
    }
    
    // 条件事件处理
    static conditional(element, eventType, condition, handler, useCapture = false) {
        const conditionalHandler = (event) => {
            if (condition(event)) {
                handler(event);
            }
        };
        
        element.addEventListener(eventType, conditionalHandler, useCapture);
    }
    
    // 委托事件处理
    static delegate(container, eventType, selector, handler) {
        container.addEventListener(eventType, (event) => {
            const target = event.target;
            if (target.matches && target.matches(selector)) {
                handler.call(target, event);
            }
        });
    }
}

// 使用事件流控制
// EventFlowController.capture(document, 'click', (event) => {
//     console.log('捕获阶段处理');
// });

// EventFlowController.once(button, 'click', (event) => {
//     console.log('只执行一次');
// });

// EventFlowController.conditional(button, 'click', 
//     (event) => event.ctrlKey, 
//     (event) => {
//         console.log('按住 Ctrl 点击');
//     }
// );

// 事件流可视化工具
class EventFlowVisualizer {
    constructor() {
        this.events = [];
    }
    
    logEvent(event, phase) {
        this.events.push({
            type: event.type,
            target: event.target.tagName,
            currentTarget: event.currentTarget.tagName,
            phase: phase,
            timestamp: Date.now()
        });
    }
    
    visualize() {
        console.table(this.events);
        return this.events;
    }
    
    clear() {
        this.events = [];
    }
}

// 使用可视化工具
const visualizer = new EventFlowVisualizer();

document.addEventListener('click', (event) => {
    visualizer.logEvent(event, '捕获');
}, true);

document.addEventListener('click', (event) => {
    visualizer.logEvent(event, '冒泡');
}, false);

// 高级事件流控制
class AdvancedEventFlow {
    constructor() {
        this.middleware = [];
    }
    
    // 添加中间件
    use(middleware) {
        this.middleware.push(middleware);
    }
    
    // 处理事件
    handleEvent(event) {
        let index = 0;
        const next = () => {
            if (index < this.middleware.length) {
                const middleware = this.middleware[index++];
                middleware(event, next);
            }
        };
        
        next();
    }
    
    // 在元素上应用中间件
    applyMiddleware(element, eventType) {
        element.addEventListener(eventType, (event) => {
            this.handleEvent(event);
        });
    }
}

// 使用中间件处理事件
const eventFlow = new AdvancedEventFlow();

// 日志中间件
eventFlow.use((event, next) => {
    console.log(`事件 ${event.type} 开始处理`);
    next();
    console.log(`事件 ${event.type} 处理完成`);
});

// 权限检查中间件
eventFlow.use((event, next) => {
    if (event.type === 'click' && event.target.hasAttribute('data-require-auth')) {
        console.log('需要权限验证');
        // 模拟权限检查
        setTimeout(() => {
            console.log('权限验证通过');
            next();
        }, 100);
    } else {
        next();
    }
});

// 性能监控中间件
eventFlow.use((event, next) => {
    const start = performance.now();
    next();
    const end = performance.now();
    console.log(`事件处理耗时: ${end - start}ms`);
});

// 事件流调试工具
class EventFlowDebugger {
    constructor() {
        this.breakpoints = new Set();
        this.logs = [];
    }
    
    // 设置断点
    setBreakpoint(element, eventType) {
        const key = `${element.tagName}_${eventType}`;
        this.breakpoints.add(key);
    }
    
    // 移除断点
    removeBreakpoint(element, eventType) {
        const key = `${element.tagName}_${eventType}`;
        this.breakpoints.delete(key);
    }
    
    // 监听事件
    watch(element, eventType, handler) {
        const originalHandler = handler;
        const debugHandler = (event) => {
            const key = `${event.currentTarget.tagName}_${event.type}`;
            
            if (this.breakpoints.has(key)) {
                debugger; // 触发断点
            }
            
            this.logEvent(event);
            originalHandler(event);
        };
        
        element.addEventListener(eventType, debugHandler);
    }
    
    // 记录事件
    logEvent(event) {
        this.logs.push({
            timestamp: Date.now(),
            type: event.type,
            target: event.target.tagName,
            currentTarget: event.currentTarget.tagName,
            phase: ['捕获', '目标', '冒泡'][event.eventPhase - 1]
        });
    }
    
    // 获取事件日志
    getLogs() {
        return this.logs;
    }
    
    // 清空日志
    clearLogs() {
        this.logs = [];
    }
}
```

### 2. 事件监听器管理

```javascript
// 事件监听器管理

// 基础事件管理器
class EventManager {
    constructor() {
        this.listeners = new Map(); // 存储监听器
        this.listenerId = 0; // 监听器 ID 计数器
    }
    
    // 添加事件监听器
    addListener(element, eventType, handler, options = {}) {
        const id = ++this.listenerId;
        const key = this.getElementKey(element);
        
        if (!this.listeners.has(key)) {
            this.listeners.set(key, new Map());
        }
        
        const elementListeners = this.listeners.get(key);
        
        if (!elementListeners.has(eventType)) {
            elementListeners.set(eventType, new Map());
        }
        
        const typeListeners = elementListeners.get(eventType);
        typeListeners.set(id, { handler, options });
        
        // 实际添加监听器
        element.addEventListener(eventType, handler, options);
        
        return id;
    }
    
    // 移除事件监听器
    removeListener(element, eventType, id) {
        const key = this.getElementKey(element);
        const elementListeners = this.listeners.get(key);
        
        if (!elementListeners) return false;
        
        const typeListeners = elementListeners.get(eventType);
        if (!typeListeners) return false;
        
        const listener = typeListeners.get(id);
        if (!listener) return false;
        
        // 实际移除监听器
        element.removeEventListener(eventType, listener.handler, listener.options);
        
        // 从管理器中移除
        typeListeners.delete(id);
        
        // 清理空的映射
        if (typeListeners.size === 0) {
            elementListeners.delete(eventType);
        }
        
        if (elementListeners.size === 0) {
            this.listeners.delete(key);
        }
        
        return true;
    }
    
    // 移除元素的所有监听器
    removeAllListeners(element) {
        const key = this.getElementKey(element);
        const elementListeners = this.listeners.get(key);
        
        if (!elementListeners) return false;
        
        elementListeners.forEach((typeListeners, eventType) => {
            typeListeners.forEach((listener) => {
                element.removeEventListener(eventType, listener.handler, listener.options);
            });
        });
        
        this.listeners.delete(key);
        return true;
    }
    
    // 获取元素的监听器数量
    getListenerCount(element) {
        const key = this.getElementKey(element);
        const elementListeners = this.listeners.get(key);
        
        if (!elementListeners) return 0;
        
        let count = 0;
        elementListeners.forEach(typeListeners => {
            count += typeListeners.size;
        });
        
        return count;
    }
    
    // 获取所有监听器信息
    getAllListeners() {
        const result = [];
        
        this.listeners.forEach((elementListeners, elementKey) => {
            elementListeners.forEach((typeListeners, eventType) => {
                typeListeners.forEach((listener, id) => {
                    result.push({
                        id,
                        element: elementKey,
                        eventType,
                        handler: listener.handler,
                        options: listener.options
                    });
                });
            });
        });
        
        return result;
    }
    
    // 生成元素键
    getElementKey(element) {
        return element.tagName + '_' + (element.id || element.className || element.innerHTML.substring(0, 20));
    }
}

// 使用事件管理器
const eventManager = new EventManager();

const button = document.getElementById('myButton');
const clickHandler = (event) => {
    console.log('按钮点击');
};

// 添加监听器
const listenerId = eventManager.addListener(button, 'click', clickHandler);

// 移除监听器
// eventManager.removeListener(button, 'click', listenerId);

// 高级事件管理器
class AdvancedEventManager {
    constructor() {
        this.events = new Map();
        this.groups = new Map();
        this.contexts = new Map();
    }
    
    // 添加带组的事件监听器
    addListener(element, eventType, handler, options = {}, group = 'default') {
        const eventId = this.generateId();
        
        const eventInfo = {
            id: eventId,
            element,
            eventType,
            handler,
            options,
            group
        };
        
        // 存储事件信息
        this.events.set(eventId, eventInfo);
        
        // 添加到组
        if (!this.groups.has(group)) {
            this.groups.set(group, new Set());
        }
        this.groups.get(group).add(eventId);
        
        // 实际添加监听器
        element.addEventListener(eventType, handler, options);
        
        return eventId;
    }
    
    // 移除特定事件监听器
    removeListener(eventId) {
        const eventInfo = this.events.get(eventId);
        if (!eventInfo) return false;
        
        const { element, eventType, handler, options, group } = eventInfo;
        
        // 实际移除监听器
        element.removeEventListener(eventType, handler, options);
        
        // 从管理器中移除
        this.events.delete(eventId);
        
        // 从组中移除
        if (this.groups.has(group)) {
            this.groups.get(group).delete(eventId);
            if (this.groups.get(group).size === 0) {
                this.groups.delete(group);
            }
        }
        
        return true;
    }
    
    // 按组移除事件监听器
    removeGroup(group) {
        const groupEvents = this.groups.get(group);
        if (!groupEvents) return false;
        
        const removed = [];
        groupEvents.forEach(eventId => {
            if (this.removeListener(eventId)) {
                removed.push(eventId);
            }
        });
        
        return removed;
    }
    
    // 按元素移除事件监听器
    removeByElement(element) {
        const removed = [];
        
        this.events.forEach((eventInfo, eventId) => {
            if (eventInfo.element === element) {
                if (this.removeListener(eventId)) {
                    removed.push(eventId);
                }
            }
        });
        
        return removed;
    }
    
    // 按事件类型移除监听器
    removeByType(eventType) {
        const removed = [];
        
        this.events.forEach((eventInfo, eventId) => {
            if (eventInfo.eventType === eventType) {
                if (this.removeListener(eventId)) {
                    removed.push(eventId);
                }
            }
        });
        
        return removed;
    }
    
    // 临时事件监听器（自动移除）
    once(element, eventType, handler, options = {}) {
        const onceHandler = (event) => {
            handler(event);
            // 自动移除
            this.events.forEach((eventInfo, eventId) => {
                if (eventInfo.handler === onceHandler) {
                    this.removeListener(eventId);
                }
            });
        };
        
        return this.addListener(element, eventType, onceHandler, options);
    }
    
    // 上下文绑定事件监听器
    bindContext(element, eventType, handler, context, options = {}) {
        const boundHandler = handler.bind(context);
        
        const eventId = this.addListener(element, eventType, boundHandler, options);
        
        // 存储上下文信息
        if (!this.contexts.has(context)) {
            this.contexts.set(context, new Set());
        }
        this.contexts.get(context).add(eventId);
        
        return eventId;
    }
    
    // 移除上下文的所有监听器
    removeContext(context) {
        const contextEvents = this.contexts.get(context);
        if (!contextEvents) return false;
        
        const removed = [];
        contextEvents.forEach(eventId => {
            if (this.removeListener(eventId)) {
                removed.push(eventId);
            }
        });
        
        this.contexts.delete(context);
        return removed;
    }
    
    // 获取事件统计信息
    getStats() {
        return {
            totalEvents: this.events.size,
            groups: Array.from(this.groups.keys()),
            contexts: this.contexts.size
        };
    }
    
    // 生成唯一 ID
    generateId() {
        return Date.now() + '_' + Math.random().toString(36).substr(2, 9);
    }
}

// 使用高级事件管理器
const advancedEventManager = new AdvancedEventManager();

const button1 = document.getElementById('button1');
const button2 = document.getElementById('button2');

// 添加监听器到不同组
advancedEventManager.addListener(button1, 'click', () => {
    console.log('按钮1点击 - 组A');
}, {}, 'groupA');

advancedEventManager.addListener(button2, 'click', () => {
    console.log('按钮2点击 - 组B');
}, {}, 'groupB');

// 移除特定组的所有监听器
// advancedEventManager.removeGroup('groupA');

// 事件监听器池
class EventListenerPool {
    constructor(maxSize = 100) {
        this.pool = [];
        this.active = new Map();
        this.maxSize = maxSize;
    }
    
    // 获取事件监听器
    getListener(handler, context = null) {
        // 查找可用的监听器
        for (let i = 0; i < this.pool.length; i++) {
            const listener = this.pool[i];
            if (listener.handler === handler && listener.context === context) {
                this.pool.splice(i, 1);
                this.active.set(listener.id, listener);
                return listener.boundHandler;
            }
        }
        
        // 创建新的监听器
        const id = this.generateId();
        const boundHandler = context ? handler.bind(context) : handler;
        const listener = {
            id,
            handler,
            context,
            boundHandler
        };
        
        this.active.set(id, listener);
        return boundHandler;
    }
    
    // 释放事件监听器
    releaseListener(boundHandler) {
        this.active.forEach((listener, id) => {
            if (listener.boundHandler === boundHandler) {
                this.active.delete(id);
                
                // 如果池未满，将监听器放回池中
                if (this.pool.length < this.maxSize) {
                    this.pool.push(listener);
                }
            }
        });
    }
    
    // 清空池
    clear() {
        this.pool = [];
        this.active.clear();
    }
    
    // 生成唯一 ID
    generateId() {
        return 'listener_' + Date.now() + '_' + Math.random().toString(36).substr(2, 9);
    }
}

// 事件监听器装饰器
class EventDecorator {
    // 防抖装饰器
    static debounce(delay) {
        return function(target, propertyName, descriptor) {
            const method = descriptor.value;
            let timeoutId;
            
            descriptor.value = function(...args) {
                clearTimeout(timeoutId);
                timeoutId = setTimeout(() => method.apply(this, args), delay);
            };
            
            return descriptor;
        };
    }
    
    // 节流装饰器
    static throttle(limit) {
        return function(target, propertyName, descriptor) {
            const method = descriptor.value;
            let inThrottle;
            
            descriptor.value = function(...args) {
                if (!inThrottle) {
                    method.apply(this, args);
                    inThrottle = true;
                    setTimeout(() => inThrottle = false, limit);
                }
            };
            
            return descriptor;
        };
    }
    
    // 一次性执行装饰器
    static once() {
        return function(target, propertyName, descriptor) {
            const method = descriptor.value;
            let executed = false;
            
            descriptor.value = function(...args) {
                if (!executed) {
                    executed = true;
                    return method.apply(this, args);
                }
            };
            
            return descriptor;
        };
    }
    
    // 条件执行装饰器
    static condition(conditionFunction) {
        return function(target, propertyName, descriptor) {
            const method = descriptor.value;
            
            descriptor.value = function(...args) {
                if (conditionFunction.apply(this, args)) {
                    return method.apply(this, args);
                }
            };
            
            return descriptor;
        };
    }
}

// 使用事件装饰器
class ButtonHandler {
    @EventDecorator.debounce(300)
    handleButtonClick(event) {
        console.log('按钮点击（防抖）');
    }
    
    @EventDecorator.throttle(1000)
    handleScroll(event) {
        console.log('滚动事件（节流）');
    }
    
    @EventDecorator.once()
    handleFirstClick(event) {
        console.log('只执行一次');
    }
    
    @EventDecorator.condition((event) => event.ctrlKey)
    handleCtrlClick(event) {
        console.log('按住 Ctrl 点击');
    }
}

// 事件监听器性能监控
class EventPerformanceMonitor {
    constructor() {
        this.metrics = new Map();
        this.activeListeners = new Map();
    }
    
    // 监控事件监听器性能
    monitorListener(element, eventType, handler, options = {}) {
        const listenerId = this.generateId();
        const startTime = performance.now();
        
        const monitoredHandler = (event) => {
            const handlerStart = performance.now();
            try {
                handler(event);
            } finally {
                const handlerEnd = performance.now();
                const duration = handlerEnd - handlerStart;
                
                // 记录性能指标
                if (!this.metrics.has(listenerId)) {
                    this.metrics.set(listenerId, {
                        element: element.tagName,
                        eventType,
                        callCount: 0,
                        totalTime: 0,
                        maxTime: 0,
                        minTime: Infinity
                    });
                }
                
                const metric = this.metrics.get(listenerId);
                metric.callCount++;
                metric.totalTime += duration;
                metric.maxTime = Math.max(metric.maxTime, duration);
                metric.minTime = Math.min(metric.minTime, duration);
            }
        };
        
        // 实际添加监听器
        element.addEventListener(eventType, monitoredHandler, options);
        
        // 记录活动监听器
        this.activeListeners.set(listenerId, {
            element,
            eventType,
            handler: monitoredHandler,
            originalHandler: handler,
            options
        });
        
        return listenerId;
    }
    
    // 移除监控的监听器
    removeMonitoredListener(listenerId) {
        const listenerInfo = this.activeListeners.get(listenerId);
        if (!listenerInfo) return false;
        
        const { element, eventType, handler } = listenerInfo;
        element.removeEventListener(eventType, handler);
        this.activeListeners.delete(listenerId);
        
        return true;
    }
    
    // 获取性能报告
    getPerformanceReport() {
        const report = [];
        
        this.metrics.forEach((metric, id) => {
            report.push({
                ...metric,
                averageTime: metric.totalTime / metric.callCount,
                listenerId: id
            });
        });
        
        return report.sort((a, b) => b.averageTime - a.averageTime);
    }
    
    // 获取慢监听器
    getSlowListeners(threshold = 16) { // 16ms = 60fps
        return this.getPerformanceReport()
            .filter(metric => metric.averageTime > threshold);
    }
    
    // 清空性能数据
    clearMetrics() {
        this.metrics.clear();
    }
    
    // 生成唯一 ID
    generateId() {
        return 'perf_' + Date.now() + '_' + Math.random().toString(36).substr(2, 9);
    }
}

// 使用性能监控
const perfMonitor = new EventPerformanceMonitor();

const button = document.getElementById('perfButton');
const slowHandler = (event) => {
    // 模拟慢操作
    for (let i = 0; i < 1000000; i++) {
        // 空循环
    }
    console.log('慢操作完成');
};

// perfMonitor.monitorListener(button, 'click', slowHandler);

// 事件监听器工具类
class EventUtils {
    // 批量添加事件监听器
    static addListeners(element, events, handler, options = {}) {
        const listenerIds = [];
        events.forEach(eventType => {
            const id = eventManager.addListener(element, eventType, handler, options);
            listenerIds.push(id);
        });
        return listenerIds;
    }
    
    // 批量移除事件监听器
    static removeListeners(listenerIds) {
        listenerIds.forEach(id => {
            eventManager.removeListener(null, null, id); // 需要改进
        });
    }
    
    // 事件委托
    static delegate(container, eventType, selector, handler) {
        return eventManager.addListener(container, eventType, (event) => {
            const target = event.target;
            if (target.matches && target.matches(selector)) {
                handler.call(target, event);
            }
        });
    }
    
    // 创建自定义事件
    static createCustomEvent(eventName, detail = {}) {
        return new CustomEvent(eventName, {
            detail,
            bubbles: true,
            cancelable: true
        });
    }
    
    // 触发自定义事件
    static dispatchEvent(element, eventName, detail = {}) {
        const event = this.createCustomEvent(eventName, detail);
        return element.dispatchEvent(event);
    }
    
    // 等待事件
    static waitForEvent(element, eventType, timeout = 5000) {
        return new Promise((resolve, reject) => {
            const handler = (event) => {
                element.removeEventListener(eventType, handler);
                resolve(event);
            };
            
            element.addEventListener(eventType, handler);
            
            if (timeout > 0) {
                setTimeout(() => {
                    element.removeEventListener(eventType, handler);
                    reject(new Error(`等待事件 ${eventType} 超时`));
                }, timeout);
            }
        });
    }
    
    // 事件组合器
    static combineEvents(element, eventTypes, handler) {
        let eventStates = {};
        eventTypes.forEach(type => eventStates[type] = false);
        
        eventTypes.forEach(type => {
            element.addEventListener(type, (event) => {
                eventStates[type] = true;
                
                const allFired = Object.values(eventStates).every(state => state);
                if (allFired) {
                    handler(eventStates);
                    // 重置状态
                    eventTypes.forEach(type => eventStates[type] = false);
                }
            });
        });
    }
}

// 使用事件工具
// EventUtils.addListeners(button, ['click', 'touchstart'], (event) => {
//     console.log('多事件处理:', event.type);
// });

// EventUtils.delegate(document, 'click', '.dynamic-button', (event) => {
//     console.log('委托事件处理');
// });

// EventUtils.waitForEvent(button, 'click', 3000)
//     .then(event => {
//         console.log('等待到点击事件');
//     })
//     .catch(error => {
//         console.log('等待超时:', error.message);
//     });
```

### 3. 自定义事件创建

```javascript
// 自定义事件创建

// 基础自定义事件
class CustomEventBasics {
    // 创建自定义事件
    static createEvent(eventName, detail = {}) {
        return new CustomEvent(eventName, {
            detail, // 传递的自定义数据
            bubbles: true, // 是否冒泡
            cancelable: true // 是否可以取消默认行为
        });
    }
    
    // 触发自定义事件
    static dispatchEvent(element, eventName, detail = {}) {
        const event = this.createEvent(eventName, detail);
        return element.dispatchEvent(event);
    }
    
    // 监听自定义事件
    static listenEvent(element, eventName, handler) {
        element.addEventListener(eventName, handler);
    }
    
    // 移除自定义事件监听器
    static removeEvent(element, eventName, handler) {
        element.removeEventListener(eventName, handler);
    }
}

// 使用基础自定义事件
const button = document.getElementById('customEventButton');

// 创建和触发自定义事件
CustomEventBasics.listenEvent(button, 'customClick', (event) => {
    console.log('自定义点击事件:', event.detail);
});

// 触发自定义事件
CustomEventBasics.dispatchEvent(button, 'customClick', {
    message: 'Hello Custom Event',
    timestamp: Date.now()
});

// 高级自定义事件系统
class AdvancedCustomEventSystem {
    constructor() {
        this.events = new Map();
        this.eventQueue = [];
        this.isProcessing = false;
    }
    
    // 创建自定义事件类
    createEventClass(eventName, options = {}) {
        class CustomEventClass extends Event {
            constructor(detail = {}, eventOptions = {}) {
                super(eventName, {
                    bubbles: options.bubbles !== false, // 默认冒泡
                    cancelable: options.cancelable !== false, // 默认可取消
                    composed: options.composed || false,
                    ...eventOptions
                });
                
                this.detail = detail;
                this.timestamp = Date.now();
                this.eventId = this.generateId();
            }
            
            generateId() {
                return `${eventName}_${Date.now()}_${Math.random().toString(36).substr(2, 9)}`;
            }
        }
        
        this.events.set(eventName, CustomEventClass);
        return CustomEventClass;
    }
    
    // 触发自定义事件
    emit(element, eventName, detail = {}, options = {}) {
        const EventClass = this.events.get(eventName);
        
        if (!EventClass) {
            console.warn(`事件 ${eventName} 未定义`);
            return false;
        }
        
        const event = new EventClass(detail, options);
        return element.dispatchEvent(event);
    }
    
    // 异步触发事件
    async emitAsync(element, eventName, detail = {}, options = {}) {
        return new Promise((resolve) => {
            this.eventQueue.push({
                element,
                eventName,
                detail,
                options,
                resolve
            });
            
            if (!this.isProcessing) {
                this.processQueue();
            }
        });
    }
    
    // 处理事件队列
    async processQueue() {
        this.isProcessing = true;
        
        while (this.eventQueue.length > 0) {
            const { element, eventName, detail, options, resolve } = this.eventQueue.shift();
            
            try {
                const result = this.emit(element, eventName, detail, options);
                resolve(result);
            } catch (error) {
                console.error('事件触发失败:', error);
                resolve(false);
            }
            
            // 让出控制权，避免阻塞
            await this.yield();
        }
        
        this.isProcessing = false;
    }
    
    // 让出控制权
    yield() {
        return new Promise(resolve => setTimeout(resolve, 0));
    }
    
    // 批量触发事件
    emitBatch(events) {
        const results = [];
        
        events.forEach(({ element, eventName, detail, options }) => {
            const result = this.emit(element, eventName, detail, options);
            results.push({ eventName, result });
        });
        
        return results;
    }
    
    // 延迟触发事件
    emitDelayed(element, eventName, detail = {}, delay = 0, options = {}) {
        return new Promise((resolve) => {
            setTimeout(() => {
                const result = this.emit(element, eventName, detail, options);
                resolve(result);
            }, delay);
        });
    }
    
    // 条件触发事件
    emitConditional(condition, element, eventName, detail = {}, options = {}) {
        if (condition) {
            return this.emit(element, eventName, detail, options);
        }
        return false;
    }
}

// 使用高级自定义事件系统
const eventSystem = new AdvancedCustomEventSystem();

// 创建自定义事件类
const UserLoginEvent = eventSystem.createEventClass('userLogin', {
    bubbles: true,
    cancelable: true
});

const DataUpdateEvent = eventSystem.createEventClass('dataUpdate', {
    bubbles: false,
    cancelable: false
});

// 监听自定义事件
document.addEventListener('userLogin', (event) => {
    console.log('用户登录事件:', event.detail);
    console.log('事件ID:', event.eventId);
});

// 触发自定义事件
eventSystem.emit(document, 'userLogin', {
    userId: 123,
    username: 'john_doe',
    loginTime: new Date()
});

// 自定义事件管理器
class CustomEventManager {
    constructor() {
        this.listeners = new Map();
        this.eventHistory = [];
        this.maxHistory = 100;
    }
    
    // 添加事件监听器
    on(eventName, handler, context = null) {
        if (!this.listeners.has(eventName)) {
            this.listeners.set(eventName, []);
        }
        
        const boundHandler = context ? handler.bind(context) : handler;
        this.listeners.get(eventName).push({
            handler: boundHandler,
            context,
            originalHandler: handler
        });
        
        return this;
    }
    
    // 移除事件监听器
    off(eventName, handler = null) {
        if (!this.listeners.has(eventName)) {
            return this;
        }
        
        if (!handler) {
            // 移除所有该事件的监听器
            this.listeners.delete(eventName);
        } else {
            // 移除特定监听器
            const listeners = this.listeners.get(eventName);
            const index = listeners.findIndex(l => l.originalHandler === handler);
            if (index > -1) {
                listeners.splice(index, 1);
            }
            
            if (listeners.length === 0) {
                this.listeners.delete(eventName);
            }
        }
        
        return this;
    }
    
    // 触发事件
    trigger(eventName, data = {}) {
        if (!this.listeners.has(eventName)) {
            return false;
        }
        
        const event = {
            name: eventName,
            data,
            timestamp: Date.now(),
            preventDefault: false
        };
        
        // 记录事件历史
        this.recordEvent(event);
        
        // 触发所有监听器
        const listeners = this.listeners.get(eventName);
        listeners.forEach(({ handler }) => {
            try {
                handler.call(null, event);
            } catch (error) {
                console.error(`事件处理错误 ${eventName}:`, error);
            }
        });
        
        return !event.preventDefault;
    }
    
    // 一次性事件监听器
    once(eventName, handler, context = null) {
        const onceHandler = (event) => {
            handler.call(context, event);
            this.off(eventName, onceHandler);
        };
        
        return this.on(eventName, onceHandler, context);
    }
    
    // 等待事件
    waitFor(eventName, timeout = 5000) {
        return new Promise((resolve, reject) => {
            let timeoutId;
            
            const handler = (event) => {
                if (timeoutId) {
                    clearTimeout(timeoutId);
                }
                resolve(event);
            };
            
            this.once(eventName, handler);
            
            if (timeout > 0) {
                timeoutId = setTimeout(() => {
                    this.off(eventName, handler);
                    reject(new Error(`等待事件 ${eventName} 超时`));
                }, timeout);
            }
        });
    }
    
    // 记录事件历史
    recordEvent(event) {
        this.eventHistory.push(event);
        
        if (this.eventHistory.length > this.maxHistory) {
            this.eventHistory.shift();
        }
    }
    
    // 获取事件历史
    getEventHistory(eventName = null) {
        if (eventName) {
            return this.eventHistory.filter(event => event.name === eventName);
        }
        return [...this.eventHistory];
    }
    
    // 清空事件历史
    clearEventHistory() {
        this.eventHistory = [];
    }
    
    // 获取所有事件类型
    getEventTypes() {
        return Array.from(this.listeners.keys());
    }
    
    // 获取事件监听器数量
    getListenerCount(eventName = null) {
        if (eventName) {
            return this.listeners.has(eventName) ? this.listeners.get(eventName).length : 0;
        }
        
        let count = 0;
        this.listeners.forEach(listeners => {
            count += listeners.length;
        });
        return count;
    }
}

// 使用自定义事件管理器
const customEventManager = new CustomEventManager();

// 添加事件监听器
customEventManager.on('userAction', (event) => {
    console.log('用户操作:', event.data);
});

customEventManager.once('pageLoad', (event) => {
    console.log('页面加载完成:', event.data);
});

// 触发事件
customEventManager.trigger('userAction', {
    action: 'click',
    element: 'button',
    timestamp: Date.now()
});

customEventManager.trigger('pageLoad', {
    url: window.location.href,
    loadTime: performance.now()
});

// 等待事件
// customEventManager.waitFor('dataReady', 3000)
//     .then(event => {
//         console.log('数据准备就绪:', event.data);
//     })
//     .catch(error => {
//         console.log('等待超时:', error.message);
//     });

// 自定义事件装饰器
class EventDecorator {
    // 事件发布装饰器
    static emit(eventName, eventManager) {
        return function(target, propertyName, descriptor) {
            const method = descriptor.value;
            
            descriptor.value = function(...args) {
                const result = method.apply(this, args);
                
                // 触发事件
                eventManager.trigger(eventName, {
                    args,
                    result,
                    context: this
                });
                
                return result;
            };
            
            return descriptor;
        };
    }
    
    // 事件订阅装饰器
    static listen(eventName, eventManager) {
        return function(target, propertyName, descriptor) {
            const method = descriptor.value;
            
            // 在类实例化时自动订阅事件
            const originalConstructor = target.constructor;
            const originalConnectedCallback = target.connectedCallback;
            
            target.connectedCallback = function() {
                if (originalConnectedCallback) {
                    originalConnectedCallback.call(this);
                }
                
                eventManager.on(eventName, method.bind(this));
            };
            
            return descriptor;
        };
    }
}

// 使用事件装饰器
const decoratorEventManager = new CustomEventManager();

class UserService {
    @EventDecorator.emit('userCreated', decoratorEventManager)
    createUser(userData) {
        console.log('创建用户:', userData);
        return { id: Date.now(), ...userData };
    }
    
    @EventDecorator.emit('userUpdated', decoratorEventManager)
    updateUser(userId, userData) {
        console.log('更新用户:', userId, userData);
        return { id: userId, ...userData };
    }
}

// 监听用户事件
decoratorEventManager.on('userCreated', (event) => {
    console.log('用户创建事件:', event.data);
});

decoratorEventManager.on('userUpdated', (event) => {
    console.log('用户更新事件:', event.data);
});

// 使用服务
const userService = new UserService();
const newUser = userService.createUser({ name: 'John', email: 'john@example.com' });
userService.updateUser(newUser.id, { name: 'John Doe' });

// 自定义事件总线
class EventBus {
    constructor() {
        this.channels = new Map();
        this.middlewares = [];
    }
    
    // 订阅频道
    subscribe(channel, handler) {
        if (!this.channels.has(channel)) {
            this.channels.set(channel, new Set());
        }
        
        this.channels.get(channel).add(handler);
        return () => this.unsubscribe(channel, handler); // 返回取消订阅函数
    }
    
    // 取消订阅
    unsubscribe(channel, handler) {
        if (this.channels.has(channel)) {
            this.channels.get(channel).delete(handler);
            
            if (this.channels.get(channel).size === 0) {
                this.channels.delete(channel);
            }
        }
    }
    
    // 发布消息
    publish(channel, message) {
        // 应用中间件
        let processedMessage = message;
        for (const middleware of this.middlewares) {
            processedMessage = middleware(channel, processedMessage);
            if (processedMessage === null) {
                return; // 中间件阻止了消息传递
            }
        }
        
        // 发送消息到订阅者
        if (this.channels.has(channel)) {
            this.channels.get(channel).forEach(handler => {
                try {
                    handler(processedMessage);
                } catch (error) {
                    console.error(`频道 ${channel} 处理错误:`, error);
                }
            });
        }
    }
    
    // 添加中间件
    use(middleware) {
        this.middlewares.push(middleware);
    }
    
    // 创建带命名空间的子总线
    createNamespace(namespace) {
        const namespacedBus = new EventBus();
        
        // 重写 publish 方法以支持命名空间
        const originalPublish = namespacedBus.publish;
        namespacedBus.publish = (channel, message) => {
            originalPublish.call(namespacedBus, `${namespace}.${channel}`, message);
        };
        
        // 重写 subscribe 方法以支持命名空间
        const originalSubscribe = namespacedBus.subscribe;
        namespacedBus.subscribe = (channel, handler) => {
            return originalSubscribe.call(namespacedBus, `${namespace}.${channel}`, handler);
        };
        
        return namespacedBus;
    }
    
    // 获取频道统计信息
    getStats() {
        const stats = {};
        this.channels.forEach((handlers, channel) => {
            stats[channel] = handlers.size;
        });
        return stats;
    }
    
    // 清空所有订阅
    clear() {
        this.channels.clear();
        this.middlewares = [];
    }
}

// 使用事件总线
const eventBus = new EventBus();

// 添加日志中间件
eventBus.use((channel, message) => {
    console.log(`[${new Date().toISOString()}] ${channel}:`, message);
    return message;
});

// 添加验证中间件
eventBus.use((channel, message) => {
    if (!message || typeof message !== 'object') {
        console.warn(`无效的消息格式在频道 ${channel}`);
        return null; // 阻止消息传递
    }
    return message;
});

// 订阅频道
const unsubscribeUser = eventBus.subscribe('user', (message) => {
    console.log('用户频道消息:', message);
});

const unsubscribeOrder = eventBus.subscribe('order', (message) => {
    console.log('订单频道消息:', message);
});

// 发布消息
eventBus.publish('user', { type: 'login', userId: 123 });
eventBus.publish('order', { type: 'created', orderId: 456 });

// 创建命名空间
const userBus = eventBus.createNamespace('user');
userBus.subscribe('profile', (message) => {
    console.log('用户配置文件消息:', message);
});

userBus.publish('profile', { action: 'updated', profile: { name: 'John' } });

// 自定义事件工具类
class CustomEventUtils {
    // 创建事件工厂
    static createEventFactory(eventDefinitions) {
        const factory = {};
        
        Object.keys(eventDefinitions).forEach(eventName => {
            const definition = eventDefinitions[eventName];
            
            factory[eventName] = (detail = {}, options = {}) => {
                return new CustomEvent(eventName, {
                    detail,
                    bubbles: definition.bubbles !== false,
                    cancelable: definition.cancelable !== false,
                    composed: definition.composed || false,
                    ...options
                });
            };
        });
        
        return factory;
    }
    
    // 批量监听事件
    static listenMultiple(element, eventMap) {
        const unsubscribers = [];
        
        Object.keys(eventMap).forEach(eventName => {
            const handler = eventMap[eventName];
            element.addEventListener(eventName, handler);
            
            unsubscribers.push(() => {
                element.removeEventListener(eventName, handler);
            });
        });
        
        return () => {
            unsubscribers.forEach(unsubscribe => unsubscribe());
        };
    }
    
    // 事件管道
    static pipeEvents(sourceElement, sourceEvent, targetElement, targetEvent, transformer = null) {
        const handler = (event) => {
            let data = event;
            
            if (transformer) {
                data = transformer(event);
            }
            
            const newEvent = new CustomEvent(targetEvent, {
                detail: data,
                bubbles: true,
                cancelable: true
            });
            
            targetElement.dispatchEvent(newEvent);
        };
        
        sourceElement.addEventListener(sourceEvent, handler);
        
        return () => {
            sourceElement.removeEventListener(sourceEvent, handler);
        };
    }
    
    // 事件节流
    static throttleEvent(element, eventName, handler, limit) {
        let inThrottle;
        
        const throttledHandler = (event) => {
            if (!inThrottle) {
                handler(event);
                inThrottle = true;
                setTimeout(() => inThrottle = false, limit);
            }
        };
        
        element.addEventListener(eventName, throttledHandler);
        
        return () => {
            element.removeEventListener(eventName, throttledHandler);
        };
    }
    
    // 事件防抖
    static debounceEvent(element, eventName, handler, delay) {
        let timeoutId;
        
        const debouncedHandler = (event) => {
            clearTimeout(timeoutId);
            timeoutId = setTimeout(() => handler(event), delay);
        };
        
        element.addEventListener(eventName, debouncedHandler);
        
        return () => {
            clearTimeout(timeoutId);
            element.removeEventListener(eventName, debouncedHandler);
        };
    }
}

// 使用自定义事件工具
const eventDefinitions = {
    userLogin: { bubbles: true, cancelable: true },
    dataUpdate: { bubbles: false, cancelable: false },
    error: { bubbles: true, cancelable: false }
};

const eventFactory = CustomEventUtils.createEventFactory(eventDefinitions);

// 批量监听
const unlisten = CustomEventUtils.listenMultiple(document, {
    'userLogin': (event) => console.log('用户登录:', event.detail),
    'dataUpdate': (event) => console.log('数据更新:', event.detail),
    'error': (event) => console.log('错误:', event.detail)
});

// 触发事件
document.dispatchEvent(eventFactory.userLogin({ userId: 123 }));
document.dispatchEvent(eventFactory.dataUpdate({ data: 'new data' }));

// 管道事件
const input = document.getElementById('textInput');
const output = document.getElementById('textOutput');

CustomEventUtils.pipeEvents(
    input,
    'input',
    output,
    'textChanged',
    (event) => event.target.value
);
```

### 4. 事件委托模式

```javascript
// 事件委托模式

// 基础事件委托
class BasicEventDelegation {
    constructor(container) {
        this.container = container;
        this.delegates = new Map();
    }
    
    // 添加委托监听器
    delegate(eventType, selector, handler) {
        const key = `${eventType}_${selector}`;
        
        if (!this.delegates.has(key)) {
            this.container.addEventListener(eventType, (event) => {
                this.handleDelegatedEvent(event, eventType, selector, handler);
            });
            
            this.delegates.set(key, {
                eventType,
                selector,
                handler
            });
        }
    }
    
    // 处理委托事件
    handleDelegatedEvent(event, eventType, selector, handler) {
        const target = event.target;
        
        // 检查目标元素是否匹配选择器
        if (target.matches && target.matches(selector)) {
            handler.call(target, event);
        }
        
        // 检查祖先元素是否匹配选择器
        let parent = target.parentElement;
        while (parent && parent !== this.container) {
            if (parent.matches && parent.matches(selector)) {
                handler.call(parent, event);
                break;
            }
            parent = parent.parentElement;
        }
    }
    
    // 移除委托监听器
    undelegate(eventType, selector) {
        const key = `${eventType}_${selector}`;
        this.delegates.delete(key);
        // 注意：实际的事件监听器仍然存在，但不会处理该委托
    }
}

// 使用基础事件委托
const container = document.getElementById('eventContainer');
const delegation = new BasicEventDelegation(container);

delegation.delegate('click', '.button-delete', function(event) {
    console.log('删除按钮点击:', this);
    this.parentElement.remove();
});

delegation.delegate('click', '.button-edit', function(event) {
    console.log('编辑按钮点击:', this);
    const text = this.parentElement.querySelector('.text');
    if (text) {
        text.contentEditable = true;
        text.focus();
    }
});

// 高级事件委托系统
class AdvancedEventDelegation {
    constructor(container) {
        this.container = container;
        this.delegates = new Map();
        this.delegateId = 0;
    }
    
    // 添加委托监听器
    on(eventType, selector, handler, options = {}) {
        const id = ++this.delegateId;
        const key = `${eventType}_${selector}_${id}`;
        
        const delegate = {
            id,
            eventType,
            selector,
            handler,
            options,
            active: true
        };
        
        if (!this.delegates.has(eventType)) {
            this.delegates.set(eventType, new Map());
            this.setupEventListener(eventType);
        }
        
        this.delegates.get(eventType).set(key, delegate);
        
        return id;
    }
    
    // 设置事件监听器
    setupEventListener(eventType) {
        this.container.addEventListener(eventType, (event) => {
            this.processEvent(event);
        }, false);
    }
    
    // 处理事件
    processEvent(event) {
        const eventType = event.type;
        const delegates = this.delegates.get(eventType);
        
        if (!delegates) return;
        
        // 按照事件流顺序处理委托
        const matchedDelegates = [];
        
        let target = event.target;
        while (target && target !== this.container) {
            delegates.forEach((delegate, key) => {
                if (delegate.active && target.matches(delegate.selector)) {
                    matchedDelegates.push({
                        delegate,
                        target,
                        key
                    });
                }
            });
            target = target.parentElement;
        }
        
        // 按照添加顺序执行处理函数
        matchedDelegates.forEach(({ delegate, target }) => {
            if (delegate.active) {
                const result = delegate.handler.call(target, event);
                
                // 处理选项
                if (delegate.options.once && result !== false) {
                    delegate.active = false;
                }
                
                if (delegate.options.stopPropagation && result !== false) {
                    event.stopPropagation();
                }
                
                if (delegate.options.preventDefault && result !== false) {
                    event.preventDefault();
                }
                
                if (result === false) {
                    event.preventDefault();
                    event.stopPropagation();
                }
            }
        });
    }
    
    // 移除委托监听器
    off(id) {
        this.delegates.forEach((delegatesByType) => {
            delegatesByType.forEach((delegate, key) => {
                if (delegate.id === id) {
                    delegate.active = false;
                    delegatesByType.delete(key);
                }
            });
        });
    }
    
    // 移除特定事件类型的委托
    offByType(eventType) {
        if (this.delegates.has(eventType)) {
            this.delegates.get(eventType).forEach(delegate => {
                delegate.active = false;
            });
            this.delegates.delete(eventType);
        }
    }
    
    // 移除特定选择器的委托
    offBySelector(selector) {
        this.delegates.forEach((delegatesByType) => {
            delegatesByType.forEach((delegate, key) => {
                if (delegate.selector === selector) {
                    delegate.active = false;
                    delegatesByType.delete(key);
                }
            });
        });
    }
    
    // 一次性委托
    once(eventType, selector, handler, options = {}) {
        return this.on(eventType, selector, handler, { ...options, once: true });
    }
    
    // 条件委托
    conditional(eventType, selector, condition, handler, options = {}) {
        const conditionalHandler = (event) => {
            if (condition(event)) {
                return handler(event);
            }
        };
        
        return this.on(eventType, selector, conditionalHandler, options);
    }
}

// 使用高级事件委托
const advancedContainer = document.getElementById('advancedContainer');
const advancedDelegation = new AdvancedEventDelegation(advancedContainer);

// 基本委托
const deleteId = advancedDelegation.on('click', '.delete-btn', function(event) {
    console.log('删除按钮点击');
    this.closest('.item').remove();
});

// 一次性委托
const onceId = advancedDelegation.once('click', '.once-btn', function(event) {
    console.log('这只执行一次');
});

// 条件委托
const conditionalId = advancedDelegation.conditional(
    'click',
    '.conditional-btn',
    (event) => event.ctrlKey, // 只有按住 Ctrl 时才触发
    function(event) {
        console.log('按住 Ctrl 点击条件按钮');
    }
);

// 智能事件委托
class SmartEventDelegation {
    constructor(container) {
        this.container = container;
        this.delegates = new Map();
        this.delegateId = 0;
        this.eventCache = new Map();
    }
    
    // 智能委托
    delegate(config) {
        const id = ++this.delegateId;
        const delegate = {
            id,
            ...config,
            active: true,
            stats: {
                calls: 0,
                lastCall: 0
            }
        };
        
        // 处理多个事件类型
        const eventTypes = Array.isArray(config.event) ? config.event : [config.event];
        
        eventTypes.forEach(eventType => {
            if (!this.delegates.has(eventType)) {
                this.delegates.set(eventType, new Map());
                this.setupSmartListener(eventType);
            }
            
            const key = `${config.selector}_${id}`;
            this.delegates.get(eventType).set(key, delegate);
        });
        
        return id;
    }
    
    // 设置智能监听器
    setupSmartListener(eventType) {
        this.container.addEventListener(eventType, (event) => {
            this.processSmartEvent(event);
        }, false);
    }
    
    // 处理智能事件
    processSmartEvent(event) {
        const eventType = event.type;
        const delegates = this.delegates.get(eventType);
        
        if (!delegates) return;
        
        const matchedDelegates = this.findMatchingDelegates(event, delegates);
        
        // 按优先级排序
        matchedDelegates.sort((a, b) => {
            const priorityA = a.delegate.priority || 0;
            const priorityB = b.delegate.priority || 0;
            return priorityB - priorityA; // 高优先级先执行
        });
        
        // 执行匹配的委托
        matchedDelegates.forEach(({ delegate, target }) => {
            if (delegate.active && this.shouldExecute(delegate, event)) {
                this.executeDelegate(delegate, target, event);
            }
        });
    }
    
    // 查找匹配的委托
    findMatchingDelegates(event, delegates) {
        const matched = [];
        let target = event.target;
        
        while (target && target !== this.container) {
            delegates.forEach((delegate, key) => {
                if (delegate.active && this.matchesSelector(target, delegate.selector)) {
                    matched.push({ delegate, target, key });
                }
            });
            target = target.parentElement;
        }
        
        return matched;
    }
    
    // 检查选择器匹配
    matchesSelector(element, selector) {
        try {
            return element.matches(selector);
        } catch (error) {
            console.warn('无效的选择器:', selector);
            return false;
        }
    }
    
    // 检查是否应该执行委托
    shouldExecute(delegate, event) {
        // 检查条件
        if (delegate.condition && !delegate.condition(event)) {
            return false;
        }
        
        // 检查节流
        if (delegate.throttle) {
            const now = Date.now();
            if (now - delegate.stats.lastCall < delegate.throttle) {
                return false;
            }
        }
        
        // 检查防抖
        if (delegate.debounce) {
            if (delegate._debounceTimer) {
                clearTimeout(delegate._debounceTimer);
            }
            
            delegate._debounceTimer = setTimeout(() => {
                this.executeDelegate(delegate, event.target, event);
            }, delegate.debounce);
            
            return false;
        }
        
        return true;
    }
    
    // 执行委托
    executeDelegate(delegate, target, event) {
        try {
            // 更新统计信息
            delegate.stats.calls++;
            delegate.stats.lastCall = Date.now();
            
            // 执行处理函数
            const result = delegate.handler.call(target, event, delegate);
            
            // 处理选项
            this.handleOptions(delegate, event, result);
            
        } catch (error) {
            console.error('委托执行错误:', error);
            if (delegate.onError) {
                delegate.onError(error, event, delegate);
            }
        }
    }
    
    // 处理选项
    handleOptions(delegate, event, result) {
        // 一次性执行
        if (delegate.once) {
            delegate.active = false;
        }
        
        // 阻止冒泡
        if (delegate.stopPropagation) {
            event.stopPropagation();
        }
        
        // 阻止默认行为
        if (delegate.preventDefault) {
            event.preventDefault();
        }
        
        // 返回 false 时阻止默认行为和冒泡
        if (result === false) {
            event.preventDefault();
            event.stopPropagation();
        }
    }
    
    // 移除委托
    undelegate(id) {
        this.delegates.forEach((delegatesByType) => {
            delegatesByType.forEach((delegate, key) => {
                if (delegate.id === id) {
                    delegate.active = false;
                    delegatesByType.delete(key);
                    
                    // 清理防抖定时器
                    if (delegate._debounceTimer) {
                        clearTimeout(delegate._debounceTimer);
                    }
                }
            });
        });
    }
    
    // 获取委托统计信息
    getStats() {
        const stats = [];
        this.delegates.forEach((delegatesByType, eventType) => {
            delegatesByType.forEach((delegate) => {
                stats.push({
                    id: delegate.id,
                    eventType,
                    selector: delegate.selector,
                    calls: delegate.stats.calls,
                    lastCall: delegate.stats.lastCall
                });
            });
        });
        return stats;
    }
    
    // 清空所有委托
    clear() {
        this.delegates.forEach((delegatesByType) => {
            delegatesByType.forEach((delegate) => {
                delegate.active = false;
                if (delegate._debounceTimer) {
                    clearTimeout(delegate._debounceTimer);
                }
            });
        });
        this.delegates.clear();
        this.eventCache.clear();
    }
}

// 使用智能事件委托
const smartContainer = document.getElementById('smartContainer');
const smartDelegation = new SmartEventDelegation(smartContainer);

// 基本委托
smartDelegation.delegate({
    event: 'click',
    selector: '.btn-primary',
    handler: function(event, delegate) {
        console.log('主要按钮点击');
    }
});

// 带优先级的委托
smartDelegation.delegate({
    event: 'click',
    selector: '.btn-danger',
    handler: function(event, delegate) {
        console.log('危险按钮点击（高优先级）');
    },
    priority: 10
});

// 带节流的委托
smartDelegation.delegate({
    event: 'scroll',
    selector: '.scroll-container',
    handler: function(event, delegate) {
        console.log('滚动事件（节流）');
    },
    throttle: 100 // 100ms 内最多执行一次
});

// 带防抖的委托
smartDelegation.delegate({
    event: 'input',
    selector: '.search-input',
    handler: function(event, delegate) {
        console.log('搜索输入（防抖）:', event.target.value);
    },
    debounce: 300 // 300ms 后执行
});

// 带条件的委托
smartDelegation.delegate({
    event: 'click',
    selector: '.conditional-btn',
    handler: function(event, delegate) {
        console.log('条件按钮点击');
    },
    condition: (event) => event.ctrlKey // 只有按住 Ctrl 时才执行
});

// 一次性委托
smartDelegation.delegate({
    event: 'click',
    selector: '.once-btn',
    handler: function(event, delegate) {
        console.log('这只执行一次');
    },
    once: true
});

// 带错误处理的委托
smartDelegation.delegate({
    event: 'click',
    selector: '.error-btn',
    handler: function(event, delegate) {
        throw new Error('模拟错误');
    },
    onError: (error, event, delegate) => {
        console.log('处理错误:', error.message);
    }
});

// 事件委托工具类
class EventDelegationUtils {
    // 创建委托配置
    static createDelegate(event, selector, handler, options = {}) {
        return {
            event: Array.isArray(event) ? event : [event],
            selector,
            handler,
            ...options
        };
    }
    
    // 批量委托
    static batchDelegate(container, delegates) {
        const delegation = new SmartEventDelegation(container);
        const ids = [];
        
        delegates.forEach(delegate => {
            const id = delegation.delegate(delegate);
            ids.push(id);
        });
        
        return {
            delegation,
            ids,
            destroy: () => ids.forEach(id => delegation.undelegate(id))
        };
    }
    
    // 委托事件映射
    static mapEvents(container, eventMap) {
        const delegation = new SmartEventDelegation(container);
        const ids = [];
        
        Object.keys(eventMap).forEach(key => {
            const [eventType, selector] = key.split(' ');
            const handler = eventMap[key];
            
            const id = delegation.delegate({
                event: eventType,
                selector: selector,
                handler: handler
            });
            
            ids.push(id);
        });
        
        return {
            delegation,
            ids,
            destroy: () => ids.forEach(id => delegation.undelegate(id))
        };
    }
    
    // 动态委托
    static dynamicDelegate(container, getDelegateConfig) {
        const delegation = new SmartEventDelegation(container);
        
        return (event) => {
            const config = getDelegateConfig(event);
            if (config) {
                return delegation.delegate(config);
            }
            return null;
        };
    }
    
    // 委托链
    static chainDelegates(container, ...delegates) {
        const delegation = new SmartEventDelegation(container);
        const chain = [];
        
        delegates.forEach((delegate, index) => {
            const id = delegation.delegate({
                ...delegate,
                priority: delegates.length - index, // 后面的优先级更高
                handler: function(event, delegateInfo) {
                    const result = delegate.handler.call(this, event, delegateInfo);
                    if (result !== false && chain[index + 1]) {
                        // 继续执行下一个委托
                        return chain[index + 1].handler.call(this, event, chain[index + 1]);
                    }
                    return result;
                }
            });
            
            chain.push({ ...delegate, id });
        });
        
        return {
            delegation,
            chain,
            destroy: () => chain.forEach(item => delegation.undelegate(item.id))
        };
    }
}

// 使用事件委托工具
// 批量委托
const batchResult = EventDelegationUtils.batchDelegate(document, [
    {
        event: 'click',
        selector: '.btn-save',
        handler: function() { console.log('保存按钮'); }
    },
    {
        event: 'click',
        selector: '.btn-cancel',
        handler: function() { console.log('取消按钮'); }
    }
]);

// 事件映射
const mapResult = EventDelegationUtils.mapEvents(document, {
    'click .btn-submit': function() { console.log('提交按钮'); },
    'click .btn-reset': function() { console.log('重置按钮'); },
    'input .form-input': function() { console.log('表单输入'); }
});

// 动态委托
const dynamicHandler = EventDelegationUtils.dynamicDelegate(document, (event) => {
    if (event.target.classList.contains('dynamic-btn')) {
        return {
            event: 'click',
            selector: '.dynamic-btn',
            handler: function() { console.log('动态按钮'); }
        };
    }
    return null;
});

// 委托链
const chainResult = EventDelegationUtils.chainDelegates(document,
    {
        event: 'click',
        selector: '.chain-btn',
        handler: function() { 
            console.log('链式委托1'); 
            return true; // 继续执行下一个
        }
    },
    {
        event: 'click',
        selector: '.chain-btn',
        handler: function() { 
            console.log('链式委托2'); 
            return false; // 停止执行
        }
    }
);

// 事件委托性能优化
class OptimizedEventDelegation {
    constructor(container) {
        this.container = container;
        this.delegates = new Map();
        this.selectorCache = new Map();
        this.eventCache = new Map();
    }
    
    // 优化的选择器匹配
    matchesSelector(element, selector) {
        // 缓存选择器函数
        if (!this.selectorCache.has(selector)) {
            try {
                // 预编译选择器
                const testElement = document.createElement('div');
                testElement.matches(selector); // 测试选择器有效性
                this.selectorCache.set(selector, (el) => el.matches(selector));
            } catch (error) {
                console.warn('无效的选择器:', selector);
                this.selectorCache.set(selector, () => false);
            }
        }
        
        return this.selectorCache.get(selector)(element);
    }
    
    // 事件委托性能监控
    delegate(eventType, selector, handler, options = {}) {
        const startTime = performance.now();
        
        // 实际委托逻辑
        const result = this.addDelegate(eventType, selector, handler, options);
        
        const endTime = performance.now();
        console.log(`委托添加耗时: ${endTime - startTime}ms`);
        
        return result;
    }
    
    addDelegate(eventType, selector, handler, options) {
        // 实现委托逻辑
        return Math.random(); // 返回模拟的 ID
    }
    
    // 懒加载委托
    lazyDelegate(eventType, selector, handlerFactory, options = {}) {
        let handler;
        
        return this.delegate(eventType, selector, (event) => {
            if (!handler) {
                handler = handlerFactory();
            }
            return handler(event);
        }, options);
    }
    
    // 委托池
    delegatePool(maxSize = 100) {
        const pool = [];
        const active = new Set();
        
        return {
            get: (eventType, selector, handler) => {
                // 从池中获取或创建委托
                const delegate = pool.pop() || this.createDelegate(eventType, selector, handler);
                active.add(delegate);
                return delegate;
            },
            
            release: (delegate) => {
                if (active.has(delegate)) {
                    active.delete(delegate);
                    if (pool.length < maxSize) {
                        pool.push(delegate);
                    }
                }
            }
        };
    }
}

// 使用优化的事件委托
const optimizedContainer = document.getElementById('optimizedContainer');
const optimizedDelegation = new OptimizedEventDelegation(optimizedContainer);

// 懒加载委托
const lazyId = optimizedDelegation.lazyDelegate('click', '.heavy-btn', () => {
    // 懒加载重型处理函数
    return function(event) {
        console.log('重型处理函数执行');
    };
});

// 委托池
const pool = optimizedDelegation.delegatePool();
```
# 十、ES6+ 新特性详解

## 10.1 现代语法特性

### 解构赋值语法

解构赋值是一种从数组或对象中提取值并赋给变量的语法。

#### 数组解构
```javascript
// 基本用法
const [a, b, c] = [1, 2, 3];
console.log(a, b, c); // 1 2 3

// 跳过某些元素
const [first, , third] = [1, 2, 3, 4];
console.log(first, third); // 1 3

// 默认值
const [x = 10, y = 20] = [5];
console.log(x, y); // 5 20

// 嵌套数组解构
const [head, ...tail] = [1, 2, 3, 4];
console.log(head, tail); // 1 [2, 3, 4]

// 交换变量
let x = 1, y = 2;
[x, y] = [y, x];
console.log(x, y); // 2 1
```

#### 对象解构
```javascript
// 基本用法
const person = { name: 'Alice', age: 25, city: 'Beijing' };
const { name, age } = person;
console.log(name, age); // Alice 25

// 重命名变量
const { name: fullName, age: years } = person;
console.log(fullName, years); // Alice 25

// 默认值
const { name, gender = 'unknown' } = person;
console.log(gender); // unknown

// 嵌套对象解构
const user = {
  name: 'Bob',
  address: {
    street: 'Main St',
    city: 'Shanghai'
  }
};
const { address: { city } } = user;
console.log(city); // Shanghai

// 函数参数解构
function printUser({ name, age, city = 'Unknown' }) {
  console.log(`${name}, ${age}, ${city}`);
}
printUser(person); // Alice, 25, Beijing
```

### 模板字符串扩展

模板字符串使用反引号(``)包围，支持多行字符串和表达式插值。

```javascript
// 基本语法
const name = 'Alice';
const greeting = `Hello, ${name}!`;
console.log(greeting); // Hello, Alice!

// 多行字符串
const multiline = `
  这是第一行
  这是第二行
  这是第三行
`;

// 表达式插值
const a = 5, b = 10;
console.log(`a + b = ${a + b}`); // a + b = 15

// 嵌套模板字符串
const classes = 'header';
const className = `item ${classes ? `class-${classes}` : ''}`;
console.log(className); // item class-header

// 带标签的模板字符串
function highlight(strings, ...values) {
  let result = '';
  strings.forEach((string, i) => {
    result += string + (values[i] ? `<mark>${values[i]}</mark>` : '');
  });
  return result;
}

const name = 'Alice';
const age = 25;
const message = highlight`Hello, ${name}! You are ${age} years old.`;
console.log(message); // Hello, <mark>Alice</mark>! You are <mark>25</mark> years old.
```

### 展开运算符应用

展开运算符(...)可以展开数组、对象或可迭代对象。

```javascript
// 数组展开
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const combined = [...arr1, ...arr2];
console.log(combined); // [1, 2, 3, 4, 5, 6]

// 复制数组
const original = [1, 2, 3];
const copy = [...original];
console.log(copy); // [1, 2, 3]

// 字符串展开
const str = 'hello';
const chars = [...str];
console.log(chars); // ['h', 'e', 'l', 'l', 'o']

// 对象展开
const obj1 = { a: 1, b: 2 };
const obj2 = { c: 3, d: 4 };
const merged = { ...obj1, ...obj2 };
console.log(merged); // { a: 1, b: 2, c: 3, d: 4 }

// 浅拷贝对象
const originalObj = { name: 'Alice', hobbies: ['reading', 'coding'] };
const copyObj = { ...originalObj };
console.log(copyObj); // { name: 'Alice', hobbies: ['reading', 'coding'] }

// 函数调用时展开参数
const numbers = [1, 2, 3, 4, 5];
console.log(Math.max(...numbers)); // 5

// 函数定义时收集参数（剩余参数）
function sum(...numbers) {
  return numbers.reduce((total, num) => total + num, 0);
}
console.log(sum(1, 2, 3, 4, 5)); // 15
```

### 默认参数和剩余参数

```javascript
// 默认参数
function greet(name = 'Guest', greeting = 'Hello') {
  return `${greeting}, ${name}!`;
}
console.log(greet()); // Hello, Guest!
console.log(greet('Alice')); // Hello, Alice!
console.log(greet('Bob', 'Hi')); // Hi, Bob!

// 默认参数可以是表达式
function add(x, y = x * 2) {
  return x + y;
}
console.log(add(5)); // 15

// 剩余参数
function multiply(multiplier, ...numbers) {
  return numbers.map(number => multiplier * number);
}
console.log(multiply(2, 1, 2, 3)); // [2, 4, 6]

// 结合解构使用
function createUser({ name = 'Anonymous', age = 0, ...otherProps } = {}) {
  return {
    name,
    age,
    ...otherProps
  };
}
console.log(createUser({ name: 'Alice', city: 'Beijing' }));
// { name: 'Alice', age: 0, city: 'Beijing' }
```

## 10.2 模块化系统

### 模块导入导出语法

```javascript
// math.js - 命名导出
export const PI = 3.14159;
export function add(a, b) {
  return a + b;
}
export function subtract(a, b) {
  return a - b;
}

// 另一种命名导出方式
const multiply = (a, b) => a * b;
const divide = (a, b) => a / b;
export { multiply, divide };

// 默认导出
export default function calculator(a, b) {
  return {
    add: add(a, b),
    subtract: subtract(a, b),
    multiply: multiply(a, b),
    divide: divide(a, b)
  };
}

// main.js - 导入语法
// 导入命名导出
import { PI, add, subtract } from './math.js';
import { multiply as mul, divide } from './math.js';

// 导入默认导出
import calc from './math.js';

// 导入所有内容
import * as math from './math.js';

console.log(PI); // 3.14159
console.log(add(5, 3)); // 8
console.log(mul(5, 3)); // 15
console.log(calc(10, 2)); // { add: 12, subtract: 8, multiply: 20, divide: 5 }
console.log(math.PI); // 3.14159
```

### 模块加载机制

```javascript
// 动态导入
async function loadModule() {
  try {
    const module = await import('./math.js');
    console.log(module.add(5, 3)); // 8
  } catch (error) {
    console.error('模块加载失败:', error);
  }
}

// 条件导入
if (process.env.NODE_ENV === 'development') {
  import('./dev-tools.js').then(module => {
    module.enableDebug();
  });
}

// 按需加载
document.getElementById('loadButton').addEventListener('click', async () => {
  const { heavyFunction } = await import('./heavy-module.js');
  heavyFunction();
});
```

### 循环依赖处理

```javascript
// a.js
import { functionB } from './b.js';

export function functionA() {
  console.log('Function A');
  // 避免在模块初始化时调用可能造成循环依赖的函数
}

export function callB() {
  functionB(); // 运行时调用是安全的
}

// b.js
import { functionA } from './a.js';

export function functionB() {
  console.log('Function B');
}

export function callA() {
  functionA();
}

// main.js
import { callA } from './a.js';
import { callB } from './b.js';

callA(); // Function A
callB(); // Function B
```

### 动态导入特性

```javascript
// 基本动态导入
async function loadLodash() {
  const { default: _ } = await import('lodash');
  return _;
}

// 条件动态导入
async function loadChartLibrary(chartType) {
  switch (chartType) {
    case 'bar':
      return await import('./bar-chart.js');
    case 'line':
      return await import('./line-chart.js');
    case 'pie':
      return await import('./pie-chart.js');
    default:
      throw new Error('Unsupported chart type');
  }
}

// 错误处理
async function safeImport(modulePath) {
  try {
    return await import(modulePath);
  } catch (error) {
    console.warn(`Failed to load module ${modulePath}:`, error);
    return null;
  }
}

// 并行动态导入
async function loadMultipleModules() {
  const [moduleA, moduleB, moduleC] = await Promise.all([
    import('./module-a.js'),
    import('./module-b.js'),
    import('./module-c.js')
  ]);
  
  return { moduleA, moduleB, moduleC };
}
```

## 10.3 新数据结构

### Set 集合特性

Set 是一个存储唯一值的集合。

```javascript
// 基本用法
const set = new Set([1, 2, 3, 4, 4, 5]);
console.log(set); // Set { 1, 2, 3, 4, 5 }

// 添加和删除元素
set.add(6);
set.add(1); // 重复值不会被添加
console.log(set.has(1)); // true
set.delete(1);
console.log(set.size); // 5

// 遍历 Set
for (const item of set) {
  console.log(item);
}

set.forEach(item => {
  console.log(item);
});

// 转换为数组
const array = [...set];
console.log(array); // [2, 3, 4, 5, 6]

// 实际应用：数组去重
const numbers = [1, 2, 2, 3, 3, 4, 5, 5];
const uniqueNumbers = [...new Set(numbers)];
console.log(uniqueNumbers); // [1, 2, 3, 4, 5]

// 实际应用：求交集、并集、差集
const setA = new Set([1, 2, 3, 4]);
const setB = new Set([3, 4, 5, 6]);

// 并集
const union = new Set([...setA, ...setB]);
console.log(union); // Set { 1, 2, 3, 4, 5, 6 }

// 交集
const intersection = new Set([...setA].filter(x => setB.has(x)));
console.log(intersection); // Set { 3, 4 }

// 差集
const difference = new Set([...setA].filter(x => !setB.has(x)));
console.log(difference); // Set { 1, 2 }
```

### Map 映射结构

Map 是键值对的集合，键可以是任意类型。

```javascript
// 基本用法
const map = new Map();
map.set('name', 'Alice');
map.set(1, 'number one');
map.set(true, 'boolean key');

console.log(map.get('name')); // Alice
console.log(map.has(1)); // true
console.log(map.size); // 3

// 使用对象作为键
const user1 = { id: 1, name: 'Alice' };
const user2 = { id: 2, name: 'Bob' };
const userMap = new Map();
userMap.set(user1, 'Active');
userMap.set(user2, 'Inactive');

console.log(userMap.get(user1)); // Active

// 初始化时传入数组
const map2 = new Map([
  ['key1', 'value1'],
  ['key2', 'value2'],
  [1, 'number key']
]);

// 遍历 Map
for (const [key, value] of map2) {
  console.log(key, value);
}

map2.forEach((value, key) => {
  console.log(key, value);
});

// 转换为数组
const entries = [...map2];
console.log(entries); // [['key1', 'value1'], ['key2', 'value2'], [1, 'number key']]

// 实际应用：缓存
class SimpleCache {
  constructor() {
    this.cache = new Map();
  }
  
  get(key) {
    return this.cache.get(key);
  }
  
  set(key, value) {
    this.cache.set(key, value);
  }
  
  has(key) {
    return this.cache.has(key);
  }
  
  clear() {
    this.cache.clear();
  }
}

const cache = new SimpleCache();
cache.set('user:1', { name: 'Alice', age: 25 });
console.log(cache.get('user:1')); // { name: 'Alice', age: 25 }
```

### WeakSet 和 WeakMap

WeakSet 和 WeakMap 只能存储对象的弱引用，不会阻止垃圾回收。

```javascript
// WeakSet
const weakSet = new WeakSet();
const obj1 = {};
const obj2 = {};

weakSet.add(obj1);
weakSet.add(obj2);

console.log(weakSet.has(obj1)); // true

// WeakSet 不能遍历，也不能获取大小
// console.log(weakSet.size); // undefined
// for (const item of weakSet) // TypeError

// 实际应用：标记对象
const processedObjects = new WeakSet();

function processObject(obj) {
  if (processedObjects.has(obj)) {
    console.log('Object already processed');
    return;
  }
  
  // 处理对象
  console.log('Processing object');
  processedObjects.add(obj);
}

const obj = {};
processObject(obj); // Processing object
processObject(obj); // Object already processed

// WeakMap
const weakMap = new WeakMap();
const domElement = document.createElement('div');
const data = { clickCount: 0 };

weakMap.set(domElement, data);

console.log(weakMap.get(domElement)); // { clickCount: 0 }

// 实际应用：私有数据
const privateData = new WeakMap();

class User {
  constructor(name) {
    privateData.set(this, { name });
  }
  
  getName() {
    return privateData.get(this).name;
  }
  
  setName(name) {
    privateData.get(this).name = name;
  }
}

const user = new User('Alice');
console.log(user.getName()); // Alice
// 无法直接访问 privateData
```

### 数据结构应用场景

```javascript
// 1. 使用 Set 进行快速查找和去重
class UniqueIdGenerator {
  constructor() {
    this.usedIds = new Set();
  }
  
  generateId() {
    let id;
    do {
      id = Math.random().toString(36).substr(2, 9);
    } while (this.usedIds.has(id));
    
    this.usedIds.add(id);
    return id;
  }
  
  isUsed(id) {
    return this.usedIds.has(id);
  }
}

// 2. 使用 Map 进行复杂键的映射
class Graph {
  constructor() {
    this.adjacencyList = new Map();
  }
  
  addVertex(vertex) {
    if (!this.adjacencyList.has(vertex)) {
      this.adjacencyList.set(vertex, new Set());
    }
  }
  
  addEdge(vertex1, vertex2) {
    this.addVertex(vertex1);
    this.addVertex(vertex2);
    this.adjacencyList.get(vertex1).add(vertex2);
    this.adjacencyList.get(vertex2).add(vertex1);
  }
  
  getNeighbors(vertex) {
    return this.adjacencyList.get(vertex) || new Set();
  }
}

// 3. 使用 WeakMap 实现 DOM 元素数据绑定
const elementData = new WeakMap();

function bindData(element, data) {
  elementData.set(element, data);
}

function getData(element) {
  return elementData.get(element);
}

function removeData(element) {
  elementData.delete(element);
}

// 4. 综合应用：缓存系统
class LRUCache {
  constructor(maxSize = 100) {
    this.maxSize = maxSize;
    this.cache = new Map();
  }
  
  get(key) {
    if (!this.cache.has(key)) {
      return undefined;
    }
    
    // 移动到最近使用位置
    const value = this.cache.get(key);
    this.cache.delete(key);
    this.cache.set(key, value);
    return value;
  }
  
  set(key, value) {
    // 如果已存在，先删除
    if (this.cache.has(key)) {
      this.cache.delete(key);
    } else if (this.cache.size >= this.maxSize) {
      // 删除最久未使用的项
      const firstKey = this.cache.keys().next().value;
      this.cache.delete(firstKey);
    }
    
    this.cache.set(key, value);
  }
  
  has(key) {
    return this.cache.has(key);
  }
  
  delete(key) {
    return this.cache.delete(key);
  }
  
  clear() {
    this.cache.clear();
  }
}

// 使用示例
const cache = new LRUCache(3);
cache.set('a', 1);
cache.set('b', 2);
cache.set('c', 3);
console.log(cache.get('a')); // 1
cache.set('d', 4); // 会移除 'b'
console.log(cache.has('b')); // false
```

# 十一、JavaScript 错误处理机制详解

## 11.1 错误类型识别

### 1. JavaScript 内置错误类型

JavaScript 提供了多种内置的错误类型（Error 类型），它们都继承自 `Error` 构造函数。了解这些错误类型有助于我们识别错误来源并进行针对性处理。

#### 常见内置错误类型：

| 错误类型 | 触发场景 | 示例 |
|--------|--------|------|
| `Error` | 通用错误类型，通常用于自定义错误 | `throw new Error("出错了")` |
| `SyntaxError` | 语法错误，代码解析阶段出错 | `eval('var a = ')` |
| `ReferenceError` | 引用未声明的变量 | `console.log(x)`（x 未定义） |
| `TypeError` | 类型错误，调用值的方法或属性时类型不匹配 | `null.toString()` |
| `RangeError` | 数值超出允许范围 | `new Array(-1)` |
| `URIError` | URI 相关函数使用错误 | `decodeURIComponent('%')` |
| `EvalError` | `eval()` 使用错误（已废弃） | — |
| `InternalError` | 引擎内部错误（非标准） | 递归太深导致栈溢出 |

> 💡 注意：`SyntaxError` 通常在代码解析阶段发生，**无法被 `try...catch` 捕获**，因为代码根本没执行。

#### 示例：识别不同错误类型

```js
try {
    JSON.parse("{ bad json }");
} catch (err) {
    if (err instanceof SyntaxError) {
        console.error("JSON 语法错误:", err.message);
    } else {
        console.error("其他错误:", err.message);
    }
}
```

---

### 2. 自定义错误类创建

为了更清晰地表达业务逻辑中的异常情况，我们可以继承 `Error` 类创建自定义错误类型。

#### 创建自定义错误类

```js
class ValidationError extends Error {
    constructor(message) {
        super(message); // 调用父类构造函数
        this.name = "ValidationError"; // 设置错误名称
        this.code = "VALIDATION_ERROR"; // 可扩展字段
    }
}

// 使用
function validateEmail(email) {
    if (!email.includes("@")) {
        throw new ValidationError("邮箱格式不正确");
    }
}

try {
    validateEmail("not-an-email");
} catch (err) {
    if (err instanceof ValidationError) {
        console.error("验证失败:", err.message);
    }
}
```

#### 高级自定义错误（带额外信息）

```js
class ApiError extends Error {
    constructor(status, message, url) {
        super(`${status} ${message} - ${url}`);
        this.name = "ApiError";
        this.status = status;
        this.url = url;
    }
}

// 使用
throw new ApiError(404, "Not Found", "https://api.example.com/user");
```

> ✅ 最佳实践：
> - 继承 `Error`
> - 设置 `this.name`
> - 保留堆栈信息（现代 JS 引擎自动处理）
> - 添加业务相关属性（如 code、status 等）

---

### 3. 错误堆栈跟踪（Stack Trace）

错误对象通常包含 `.stack` 属性，提供错误发生的调用堆栈信息，对调试至关重要。

#### 示例：查看堆栈

```js
function inner() {
    throw new Error("出错了！");
}

function outer() {
    inner();
}

try {
    outer();
} catch (err) {
    console.log(err.stack);
}
```

输出示例：

```
Error: 出错了！
    at inner (script.js:2:11)
    at outer (script.js:5:5)
    at script.js:8:5
```

#### 堆栈的作用：

- 定位错误发生的具体文件和行号
- 查看函数调用链
- 在开发和生产环境中辅助调试

> ⚠️ 注意：
> - `stack` 属性是非标准但广泛支持的。
> - 生产环境中可考虑隐藏详细堆栈以防信息泄露。

---

### 4. 错误信息格式化

为了统一错误输出，提升可读性，我们可以对错误信息进行格式化处理。

#### 方法一：封装错误处理函数

```js
function formatError(err) {
    return {
        name: err.name,
        message: err.message,
        stack: err.stack?.split('\n').slice(0, 5), // 只保留前5行
        timestamp: new Date().toISOString(),
        ...(err.code && { code: err.code }),
        ...(err.status && { status: err.status })
    };
}

try {
    throw new ValidationError("用户名不能为空");
} catch (err) {
    console.error("格式化错误:", formatError(err));
}
```

#### 方法二：使用 `console.error` 配合自定义格式

```js
console.error(`[${new Date().toLocaleString()}] ${err.name}: ${err.message}`);
```

#### 方法三：日志系统集成（如 Winston、Pino）

```js
// 使用 Winston 示例
const logger = require('winston');
logger.error({
    level: 'error',
    message: err.message,
    stack: err.stack,
    meta: { userId: 123 }
});
```

---

## 11.2 异常处理策略

### 1. `try...catch` 语句使用

`try...catch` 是 JavaScript 中最基本的同步异常捕获机制。

#### 基本语法：

```js
try {
    // 可能出错的代码
    riskyOperation();
} catch (err) {
    // 处理错误
    console.error("捕获到错误:", err.message);
} finally {
    // 可选，无论是否出错都会执行
}
```

#### 注意事项：

- `catch` 块中的 `err` 是错误对象
- 推荐使用 `err` 而不是 `error` 保持一致性
- 不要忽略错误（避免空 `catch {}`）

#### 捕获特定错误类型

```js
try {
    someOperation();
} catch (err) {
    if (err instanceof TypeError) {
        console.log("类型错误");
    } else if (err instanceof ReferenceError) {
        console.log("引用错误");
    } else {
        console.log("未知错误");
        throw err; // 重新抛出不处理的错误
    }
}
```

> ✅ 最佳实践：
> - 尽量只捕获你能处理的错误
> - 处理不了的错误应重新抛出
> - 避免使用 `catch (e)` 捕获所有异常而不做判断

---

### 2. `finally` 块执行机制

`finally` 块用于执行**无论是否发生异常都必须执行的清理操作**。

#### 基本行为：

```js
try {
    console.log("进入 try");
    throw new Error("出错了");
} catch (err) {
    console.log("进入 catch");
} finally {
    console.log("进入 finally");
}
// 输出：进入 try → 进入 catch → 进入 finally
```

#### `finally` 的执行优先级

即使 `try` 或 `catch` 中有 `return`，`finally` 也会执行：

```js
function test() {
    try {
        return "try";
    } catch (err) {
        return "catch";
    } finally {
        console.log("finally always runs");
    }
}
test(); // 输出: "finally always runs"，然后返回 "try"
```

#### 特殊情况：`finally` 中的 `return` 会覆盖前面的返回值

```js
function test() {
    try {
        return "try";
    } finally {
        return "finally"; // 覆盖前面的 return
    }
}
test(); // 返回 "finally"
```

> ⚠️ 警告：避免在 `finally` 中使用 `return`、`throw` 或改变控制流，容易造成逻辑混乱。

#### 典型应用场景：

- 关闭文件或连接
- 清理定时器
- 恢复状态
- 加载状态关闭（如 UI loading 动画）

```js
let loading = true;
try {
    showLoading();
    await fetchData();
} catch (err) {
    showError(err.message);
} finally {
    hideLoading(); // 无论成功失败都要关闭 loading
}
```

---

### 3. 异步错误处理

异步操作中的错误不能用普通的 `try...catch` 直接捕获，需特殊处理。

#### (1) Promise 错误处理

```js
// 方法一：.catch()
fetch('/api/data')
    .then(res => res.json())
    .then(data => console.log(data))
    .catch(err => console.error("请求失败:", err));

// 方法二：then 的第二个参数
promise.then(
    value => { /* 成功 */ },
    err => { /* 失败 */ }
);
```

#### (2) `async/await` 中使用 `try...catch`

```js
async function fetchData() {
    try {
        const res = await fetch('/api/data');
        if (!res.ok) throw new Error(`HTTP ${res.status}`);
        const data = await res.json();
        return data;
    } catch (err) {
        console.error("获取数据失败:", err.message);
        // 可选择重新抛出
        throw err;
    }
}
```

#### (3) 并行异步任务的错误处理

```js
// Promise.all()：任一失败则整体失败
try {
    const [a, b] = await Promise.all([
        fetchA(),
        fetchB()
    ]);
} catch (err) {
    console.error("其中一个请求失败");
}

// Promise.allSettled()：始终成功，返回结果数组
const results = await Promise.allSettled([fetchA(), fetchB()]);
results.forEach((result, i) => {
    if (result.status === 'rejected') {
        console.error(`任务 ${i} 失败:`, result.reason);
    }
});
```

#### (4) 错误传播

```js
async function service() {
    try {
        return await apiCall();
    } catch (err) {
        throw new ServiceError("服务调用失败", { cause: err });
    }
}
```

---

### 4. 全局错误捕获

用于捕获未被处理的异常，防止程序崩溃，并收集错误日志。

#### (1) `window.onerror`（浏览器）

捕获全局同步错误、资源加载错误等。

```js
window.onerror = function(message, source, lineno, colno, error) {
    console.error("全局错误:", {
        message,
        source, // 错误文件
        lineno, // 行号
        colno,  // 列号
        error   // 错误对象
    });

    // 上报错误日志
    reportErrorToServer({ message, source, lineno, colno, stack: error?.stack });

    return true; // 阻止默认错误弹窗（可选）
};
```

> ⚠️ 注意：跨域脚本错误会显示为 `"Script error."`，需设置 CORS 和 `crossorigin` 属性。

#### (2) `window.addEventListener('error')`

更现代的方式，可捕获更多类型的错误（如资源加载失败）。

```js
window.addEventListener('error', (event) => {
    if (event.error) {
        console.error("JavaScript 错误:", event.error);
    } else {
        console.error("资源加载失败:", event.target.src || event.target.href);
    }
});
```

#### (3) `unhandledrejection`（未处理的 Promise 错误）

非常重要！未被 `.catch()` 的 Promise 会触发此事件。

```js
window.addEventListener('unhandledrejection', (event) => {
    console.error("未处理的 Promise 拒绝:", event.reason);
    event.preventDefault(); // 阻止控制台警告（谨慎使用）
});
```

#### (4) Node.js 中的全局错误处理

```js
// 未捕获异常
process.on('uncaughtException', (err) => {
    console.error('未捕获的异常:', err);
    // 通常建议记录日志后退出进程
    process.exit(1);
});

// 未处理的 Promise 拒绝
process.on('unhandledRejection', (reason, promise) => {
    console.error('未处理的 Promise 拒绝:', reason);
});
```

> ⚠️ 警告：`uncaughtException` 后程序处于不稳定状态，**不建议继续运行**，应记录日志后退出。

---

## 总结：错误处理最佳实践

| 实践 | 说明 |
|------|------|
| ✅ 使用 `try...catch` 处理可预期的同步错误 | 如 JSON 解析、用户输入验证 |
| ✅ `async/await` 配合 `try...catch` | 处理异步错误最清晰的方式 |
| ✅ 创建自定义错误类 | 提高错误语义化和可维护性 |
| ✅ 使用 `finally` 进行资源清理 | 如关闭连接、取消 loading |
| ✅ 捕获未处理的 Promise 错误 | 避免静默失败 |
| ✅ 全局错误监听用于日志上报 | 但不要阻止所有错误 |
| ❌ 避免空 `catch` 块 | 至少要记录日志 |
| ❌ 不要忽略 `unhandledRejection` | 会导致内存泄漏或逻辑错误 |
| 📊 生产环境格式化并上报错误 | 结合 Sentry、LogRocket 等工具 |

---

## 附：常见错误处理模式

### 模式 1：重试机制

```js
async function fetchWithRetry(url, retries = 3) {
    for (let i = 0; i < retries; i++) {
        try {
            return await fetch(url);
        } catch (err) {
            if (i === retries - 1) throw err;
            await new Promise(r => setTimeout(r, 1000 * (i + 1)));
        }
    }
}
```

### 模式 2：错误包装（Error Wrapping）

```js
class BusinessError extends Error {
    constructor(message, { cause, code } = {}) {
        super(message);
        this.name = "BusinessError";
        this.code = code;
        this.cause = cause;
    }
}
```

---
# 十二、JavaScript 性能优化技术详解

在现代 Web 应用中，性能直接影响用户体验、SEO 排名和用户留存。JavaScript 作为浏览器端的核心语言，其性能表现尤为关键。本章将从 **内存管理优化** 和 **代码性能优化** 两大维度，系统深入地讲解 JavaScript 的性能调优策略。

---

## 12.1 内存管理优化

### 1. 垃圾回收机制原理（Garbage Collection, GC）

JavaScript 是一门自动内存管理的语言，开发者无需手动分配或释放内存。引擎通过 **垃圾回收机制** 自动清理不再使用的对象。

#### 主要垃圾回收算法：

##### （1）**引用计数（Reference Counting）**
- 每个对象维护一个“被引用次数”的计数器。
- 当引用数为 0 时，对象被立即回收。
- ❌ 缺陷：无法处理**循环引用**。

```js
let obj1 = {};
let obj2 = {};
obj1.ref = obj2;
obj2.ref = obj1; // 循环引用，引用数始终 ≥1，无法回收
```

> 现代 JS 引擎已不再单独使用引用计数。

##### （2）**标记-清除（Mark-and-Sweep）** ✅ 主流算法
- 从根对象（如 `window`、`global`）开始遍历所有可达对象，进行“标记”。
- 扫描所有对象，未被标记的对象视为“不可达”，即垃圾，进行清除。
- ✅ 能正确处理循环引用。

```js
let obj = { data: "large" };
obj = null; // 原对象不再可达，下次 GC 时会被回收
```

#### 垃圾回收过程（以 V8 为例）：

V8 引擎采用 **分代回收（Generational Collection）** 策略：

| 代际 | 特点 | 回收频率 |
|------|------|----------|
| 新生代（Young Generation） | 存放短期存活对象（如局部变量） | 高频（Scavenge 算法） |
| 老生代（Old Generation） | 存放长期存活对象 | 低频（Mark-Sweep + Mark-Compact） |

> ✅ 优势：提高 GC 效率，减少停顿时间。

#### GC 对性能的影响：
- **Stop-The-World**：GC 执行时会暂停 JavaScript 执行，造成卡顿。
- 频繁 GC 会导致页面卡顿，应尽量减少对象创建。

---

### 2. 内存泄漏识别和预防

内存泄漏指“本应被释放的内存未被释放”，长期积累会导致页面变慢甚至崩溃。

#### 常见内存泄漏场景：

##### （1）意外的全局变量

```js
function leak() {
    leakVar = "I'm global!"; // 忘记 var/let/const → 成为 window.leakVar
}
```

✅ 预防：使用严格模式 `"use strict"`，会报错。

##### （2）未清理的定时器或事件监听

```js
setInterval(() => {
    const hugeData = fetchData();
    // hugeData 一直被闭包引用，无法释放
}, 1000);

// 事件监听未移除
element.addEventListener('click', handler);
// 忘记 element.removeEventListener(...)
```

✅ 预防：组件销毁时清理定时器和事件。

```js
let timer = setInterval(...);
// 销毁时
clearInterval(timer);
element.removeEventListener('click', handler);
```

##### （3）闭包引用大型对象

```js
function outer() {
    const bigData = new Array(1000000).fill('*');
    return function inner() {
        console.log("Still referencing bigData");
    };
}
const fn = outer(); // bigData 无法被回收
```

✅ 预防：避免闭包中长期持有大对象，使用完后置为 `null`。

##### （4）DOM 引用未释放

```js
const element = document.getElementById('myDiv');
const map = new Map();
map.set(element, someData);

// 即使 DOM 被移除，map 仍持有引用，无法回收
document.body.removeChild(element);
```

✅ 预防：使用 `WeakMap` 或手动清理。

```js
const weakMap = new WeakMap(); // 键是弱引用，DOM 删除后自动清理
weakMap.set(element, someData);
```

#### 识别内存泄漏工具：

- **Chrome DevTools → Memory 面板**
  - Heap Snapshot（堆快照）：查看当前内存对象
  - Record Allocation Timeline：记录内存分配过程
- **Performance 面板**：查看 GC 活动和内存增长趋势

> 🔍 技巧：操作前后拍两张堆快照，对比找出未释放的对象。

---

### 3. 对象池模式应用（Object Pool Pattern）

频繁创建和销毁对象会加重 GC 负担。对象池通过**复用对象**减少内存分配。

#### 适用场景：
- 频繁创建/销毁的短生命周期对象（如粒子、子弹、DOM 元素）
- 创建成本高的对象（如复杂配置对象）

#### 实现一个简单的对象池：

```js
class ObjectPool {
    constructor(createFn, resetFn, initialSize = 5) {
        this.createFn = createFn;  // 创建对象的函数
        this.resetFn = resetFn;    // 重置对象状态的函数
        this.pool = [];
        // 预创建一些对象
        for (let i = 0; i < initialSize; i++) {
            this.pool.push(createFn());
        }
    }

    acquire() {
        if (this.pool.length > 0) {
            return this.pool.pop();
        }
        return this.createFn(); // 池空时新建
    }

    release(obj) {
        this.resetFn(obj); // 重置状态
        this.pool.push(obj); // 放回池中
    }
}

// 使用示例：复用 DOM 元素
const divPool = new ObjectPool(
    () => document.createElement('div'),
    (div) => {
        div.textContent = '';
        div.className = '';
        if (div.parentNode) div.remove();
    }
);

// 获取
const div = divPool.acquire();
div.textContent = "Hello";
document.body.appendChild(div);

// 使用完放回
divPool.release(div);
```

✅ 优势：
- 减少 GC 压力
- 提升性能（避免重复创建开销）

⚠️ 注意：
- 不是所有场景都适用（如对象状态复杂难重置）
- 池过大也会浪费内存

---

### 4. 内存使用监控

主动监控内存使用情况，及时发现异常。

#### （1）浏览器中使用 Performance API

```js
// 获取内存信息（仅 Chrome 支持）
if (performance.memory) {
    console.log({
        used: performance.memory.usedJSHeapSize,
        total: performance.memory.totalJSHeapSize,
        limit: performance.memory.jsHeapSizeLimit
    });
}
```

> ⚠️ 非标准 API，仅用于开发调试。

#### （2）Node.js 中使用 `process.memoryUsage()`

```js
setInterval(() => {
    const mem = process.memoryUsage();
    console.log({
        rss: (mem.rss / 1024 / 1024).toFixed(2) + ' MB', // 物理内存
        heapTotal: (mem.heapTotal / 1024 / 1024).toFixed(2) + ' MB',
        heapUsed: (mem.heapUsed / 1024 / 1024).toFixed(2) + ' MB',
    });
}, 5000);
```

#### （3）监控内存增长趋势

```js
let lastHeap = 0;
function checkMemoryLeak() {
    if (performance.memory) {
        const current = performance.memory.usedJSHeapSize;
        if (current - lastHeap > 10 * 1024 * 1024) { // 增长超过 10MB
            console.warn("内存增长过快，可能存在泄漏");
        }
        lastHeap = current;
    }
}
```

#### （4）集成监控工具

- **Sentry**：捕获错误并附带内存上下文
- **Datadog / New Relic**：监控 Node.js 内存指标
- **Lighthouse**：自动化性能审计

---

## 12.2 代码性能优化

### 1. 算法复杂度分析

选择高效的算法是性能优化的根基。常用复杂度：

| 复杂度 | 名称 | 示例 |
|--------|------|------|
| O(1) | 常数时间 | 数组索引、哈希表查找 |
| O(log n) | 对数时间 | 二分查找 |
| O(n) | 线性时间 | 遍历数组 |
| O(n log n) | 线性对数 | 快速排序、归并排序 |
| O(n²) | 平方时间 | 双重循环、冒泡排序 |
| O(2ⁿ) | 指数时间 | 递归斐波那契（无缓存） |

#### 优化示例：从 O(n²) 到 O(n)

```js
// ❌ O(n²)：查找数组中是否有重复元素
function hasDuplicate(arr) {
    for (let i = 0; i < arr.length; i++) {
        for (let j = i + 1; j < arr.length; j++) {
            if (arr[i] === arr[j]) return true;
        }
    }
    return false;
}

// ✅ O(n)：使用 Set
function hasDuplicate(arr) {
    const seen = new Set();
    for (const item of arr) {
        if (seen.has(item)) return true;
        seen.add(item);
    }
    return false;
}
```

✅ 建议：
- 尽量避免嵌套循环
- 优先使用哈希结构（`Object`、`Map`、`Set`）提升查找效率

---

### 2. DOM 操作优化

DOM 操作是性能瓶颈之一，因其涉及 **重排（reflow）** 和 **重绘（repaint）**。

#### 重排 vs 重绘：
- **重排**：元素几何属性改变（宽高、位置），触发布局重新计算（昂贵）
- **重绘**：元素样式改变但不影响布局（如颜色），只需重绘（较轻）

#### 优化策略：

##### （1）批量 DOM 操作

```js
// ❌ 每次都触发重排
for (let i = 0; i < items.length; i++) {
    const el = document.createElement('li');
    el.textContent = items[i];
    list.appendChild(el); // 每次都修改 DOM
}

// ✅ 使用 DocumentFragment 批量插入
const fragment = document.createDocumentFragment();
for (let i = 0; i < items.length; i++) {
    const el = document.createElement('li');
    el.textContent = items[i];
    fragment.appendChild(el);
}
list.appendChild(fragment); // 仅一次 DOM 修改
```

##### （2）离线操作 DOM

```js
// 隐藏元素 → 修改 → 显示
list.style.display = 'none';
// 大量修改...
list.style.display = 'block';
```

##### （3）使用 `requestAnimationFrame` 批量更新

```js
let updates = [];
function updateDOM(prop, value) {
    updates.push([prop, value]);
    requestAnimationFrame(applyUpdates);
}

function applyUpdates() {
    updates.forEach(([prop, value]) => {
        element[prop] = value;
    });
    updates = [];
}
```

##### （4）避免强制同步布局（Forced Synchronous Layout）

```js
// ❌ 强制同步布局：读写交替，导致多次重排
el.style.height = el.scrollHeight + 'px';
el.style.width = el.scrollWidth + 'px';

// ✅ 先读后写
const height = el.scrollHeight;
const width = el.scrollWidth;
el.style.height = height + 'px';
el.style.width = width + 'px';
```

---

### 3. 事件处理优化

事件处理不当会导致内存泄漏或卡顿。

#### 优化策略：

##### （1）事件委托（Event Delegation）

避免为每个子元素绑定事件。

```js
// ❌ 为每个按钮绑定
buttons.forEach(btn => btn.addEventListener('click', handler));

// ✅ 委托给父容器
container.addEventListener('click', (e) => {
    if (e.target.matches('.btn')) {
        handler(e);
    }
});
```

✅ 优势：
- 减少事件监听器数量
- 动态添加的元素也能响应

##### （2）节流（Throttle）与防抖（Debounce）

适用于高频事件：`scroll`、`resize`、`input` 等。

```js
// 防抖：最后一次触发后执行
function debounce(fn, delay) {
    let timer;
    return function (...args) {
        clearTimeout(timer);
        timer = setTimeout(() => fn.apply(this, args), delay);
    };
}

// 节流：固定时间间隔执行一次
function throttle(fn, delay) {
    let last = 0;
    return function (...args) {
        const now = Date.now();
        if (now - last > delay) {
            fn.apply(this, args);
            last = now;
        }
    };
}

// 使用
window.addEventListener('scroll', throttle(handleScroll, 100));
input.addEventListener('input', debounce(search, 300));
```

---

### 4. 网络请求优化

减少请求数量和数据体积，提升加载速度。

#### 优化策略：

##### （1）减少请求数量
- 合并 CSS/JS 文件（使用 Webpack、Vite 等构建工具）
- 使用 CSS Sprites 合并小图标
- 使用 HTTP/2 多路复用

##### （2）压缩资源
- 启用 Gzip/Brotli 压缩
- 图片使用 WebP 格式
- JS 使用 Terser 压缩

##### （3）缓存策略
- 设置 `Cache-Control`、`ETag`
- 使用 Service Worker 实现离线缓存

##### （4）懒加载（Lazy Loading）

```js
// 图片懒加载
const img = document.querySelector('img[data-src]');
const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            entry.target.src = entry.target.dataset.src;
            observer.unobserve(entry.target);
        }
    });
});
observer.observe(img);
```

##### （5）预加载与预连接

```html
<!-- 预加载关键资源 -->
<link rel="preload" href="critical.js" as="script">

<!-- 预连接第三方域名 -->
<link rel="preconnect" href="https://api.example.com">
```

##### （6）使用 Web Workers 处理耗时任务

避免阻塞主线程：

```js
// worker.js
self.onmessage = function(e) {
    const result = heavyComputation(e.data);
    self.postMessage(result);
};

// main.js
const worker = new Worker('worker.js');
worker.postMessage(data);
worker.onmessage = (e) => {
    console.log('结果:', e.data);
};
```

---

## 总结：性能优化 checklist

| 类别 | 优化措施 |
|------|----------|
| **内存管理** | 减少对象创建、清理引用、使用 WeakMap、对象池 |
| **算法** | 避免 O(n²)，优先使用哈希结构 |
| **DOM** | 批量操作、离线更新、避免强制同步布局 |
| **事件** | 事件委托、节流防抖 |
| **网络** | 合并资源、压缩、缓存、懒加载 |
| **监控** | 使用 DevTools、Performance API、错误上报 |

---

## 附：性能测试工具推荐

- **Lighthouse**：综合性能评分（Chrome 内置）
- **WebPageTest**：多地点加载测试
- **Chrome DevTools Performance 面板**：分析运行时性能
- **BundlePhobia**：查看 npm 包体积影响
- **Sentry / LogRocket**：生产环境性能监控

---

# 十三、JavaScript 调试与测试详解

在现代软件开发中，**调试**是定位和修复问题的过程，**测试**是预防问题、保证质量的手段。两者相辅相成，是构建高质量、可维护 JavaScript 应用的核心环节。

本章将从 **调试技术** 和 **测试策略** 两个维度，系统深入地讲解如何高效排查问题并建立可靠的代码质量保障体系。

---

## 13.1 调试技术

### 1. 浏览器开发者工具（DevTools）

浏览器开发者工具是前端调试的“瑞士军刀”，以 Chrome DevTools 为例，核心功能包括：

#### 主要面板介绍：

| 面板 | 功能 |
|------|------|
| **Elements** | 查看和修改 DOM 结构、CSS 样式 |
| **Console** | 执行 JS、输出日志、捕获错误 |
| **Sources** | 设置断点、单步执行、查看调用栈 |
| **Network** | 监控 HTTP 请求、响应时间、资源大小 |
| **Performance** | 记录运行时性能，分析 FPS、CPU、内存 |
| **Memory** | 拍摄堆快照、记录内存分配，检测内存泄漏 |
| **Application** | 查看 Storage、Cookies、Service Workers、Cache |
| **Security** | 检查 HTTPS、证书、混合内容等安全问题 |

#### 高效使用技巧：

- `Ctrl+P`（或 `Cmd+P`）快速打开文件
- `console.log()` 可以传多个参数：`console.log("User:", user, "Count:", count)`
- 使用 `console.table()` 查看数组或对象表格化输出
- `console.time('label')` / `console.timeEnd('label')` 测量执行时间
- `$0` 表示当前选中的 DOM 元素（在 Elements 面板中右键选择）

```js
console.table([{name: "Alice", age: 25}, {name: "Bob", age: 30}]);
console.time("fetch");
await fetch('/api/data');
console.timeEnd("fetch");
```

---

### 2. 断点调试技巧

断点是调试的核心，允许你在代码执行到某一行时暂停，检查变量状态。

#### 设置断点的方式：

1. **行断点（Line Breakpoint）**
   - 在 Sources 面板点击行号左侧
   - 程序执行到该行时暂停

2. **条件断点（Conditional Breakpoint）**
   - 右键行号 → "Add conditional breakpoint"
   - 仅当条件为 `true` 时触发
   - 示例：`userId === 123`

3. **DOM 断点**
   - 在 Elements 面板右键 DOM 节点
   - 选择 "Break on" → "subtree modifications" 等
   - 当 DOM 被修改时暂停

4. **XHR/Fetch 断点**
   - 在 Sources 面板 → XHR Breakpoints
   - 输入 URL 关键字，当请求匹配时暂停

5. **事件监听器断点**
   - 在 Sources 面板 → Event Listener Breakpoints
   - 勾选 `click`、`scroll` 等事件，触发时暂停

#### 调试控制按钮：

- ▶️ **Resume**：继续执行（F8）
- ⏩ **Step over**：跳过当前函数调用（F10）
- ⏭️ **Step into**：进入函数内部（F11）
- ⏭️▶️ **Step out**：跳出当前函数（Shift+F11）
- ⏯️ **Deactivate breakpoints**：临时禁用所有断点（Ctrl+F8）

#### 调用栈（Call Stack）分析

- 查看函数调用链，定位错误源头
- 点击任意栈帧可跳转到对应代码位置
- 异步代码会显示 `async` 标记

#### 作用域（Scope）查看

- 查看当前执行上下文中的变量（Local、Closure、Global）
- 可直接修改变量值进行测试

---

### 3. 性能分析工具

用于识别性能瓶颈，如卡顿、加载慢、CPU 占用高等。

#### 使用 Performance 面板：

1. 打开 **Performance** 面板
2. 点击 ▶️ 开始记录
3. 执行目标操作（如页面加载、点击按钮）
4. 点击 ■ 停止记录

#### 分析关键指标：

- **FPS（Frames Per Second）**：绿色条越高越好，红色表示掉帧
- **CPU 使用率**：高 CPU 可能导致卡顿
- **Main 线程**：查看 JS 执行、渲染、合成等任务
- **火焰图（Flame Chart）**：自上而下显示函数调用栈和耗时

#### 常见性能问题识别：

- **长任务（Long Task）**：>50ms 的任务会阻塞主线程
- **频繁的重排/重绘**：Layout、Paint 任务过多
- **过多的垃圾回收（GC）**：频繁的内存分配

#### 示例：优化一个慢函数

```js
// ❌ 慢函数
function slowCalc(arr) {
    for (let i = 0; i < arr.length; i++) {
        for (let j = 0; j < arr.length; j++) {
            // O(n²) 算法
        }
    }
}
```

通过 Performance 面板发现该函数耗时 800ms，可优化为哈希查找（O(n)）。

---

### 4. 内存分析方法

内存泄漏是隐蔽但致命的问题，会导致页面越来越卡，最终崩溃。

#### 使用 Memory 面板：

##### （1）堆快照（Heap Snapshot）

- 拍摄当前内存对象的快照
- 可对比多个快照，找出未释放的对象

**操作步骤：**
1. 打开 Memory 面板
2. 选择 "Heap snapshot"
3. 点击 "Take snapshot"
4. 执行操作（如打开关闭组件）
5. 再拍一张快照
6. 使用 "Objects allocated between GCs" 对比

**关键列：**
- **Distance**：到根对象的距离
- **Shallow Size**：对象自身占用内存
- **Retained Size**：该对象被回收后能释放的总内存

##### （2）记录内存分配时间线（Record Allocation Timeline）

- 实时记录对象分配和回收
- 红色柱子表示新分配的对象
- 如果红色不消失，说明未被回收 → 内存泄漏

##### （3）识别常见泄漏模式：

- `Detached DOM trees`：已从 DOM 移除但仍被 JS 引用
- `Closure`：闭包引用大型对象
- `Event listeners`：未移除的事件监听器

#### 示例：使用 `WeakMap` 避免泄漏

```js
// ❌ 普通 Map 持有强引用
const cache = new Map();
cache.set(domElement, data);

// ✅ WeakMap 键是弱引用，DOM 删除后自动清理
const weakCache = new WeakMap();
weakCache.set(domElement, data);
```

---

## 13.2 测试策略

### 1. 单元测试概念（Unit Testing）

单元测试是针对**最小可测试单元**（通常是函数或类）的测试，目的是验证其行为是否符合预期。

#### 核心原则：

- **独立性**：每个测试用例独立，不依赖外部状态
- **可重复性**：相同输入总是得到相同结果
- **自动化**：可由 CI/CD 自动执行

#### 常用工具：

- **Jest**：最流行的 JS 测试框架，内置断言、Mock、覆盖率
- **Mocha + Chai**：经典组合，灵活但需搭配更多工具
- **Vitest**：Vite 生态的现代测试框架，速度快

#### 示例：Jest 测试一个函数

```js
// math.js
export function add(a, b) {
    return a + b;
}

// math.test.js
import { add } from './math';

test('adds 1 + 2 to equal 3', () => {
    expect(add(1, 2)).toBe(3);
});

test('handles negative numbers', () => {
    expect(add(-1, 1)).toBe(0);
});
```

#### 断言（Assertions）常用方法：

| 方法 | 说明 |
|------|------|
| `expect(value).toBe(expected)` | 严格相等（===） |
| `expect(value).toEqual(object)` | 深度相等 |
| `expect(fn).toThrow()` | 函数抛出错误 |
| `expect(value).toBeDefined()` | 不是 undefined |
| `expect(value).toContain(item)` | 数组包含某元素 |

#### Mocking（模拟）

用于隔离外部依赖，如 API 调用、定时器。

```js
// 模拟 API
jest.spyOn(global, 'fetch').mockResolvedValue({
    json: () => Promise.resolve({ data: 'mock' })
});

// 模拟 setTimeout
jest.useFakeTimers();
setTimeout(callback, 1000);
jest.runAllTimers();
```

---

### 2. 集成测试方法（Integration Testing）

集成测试验证**多个模块协同工作**是否正常，介于单元测试和端到端测试之间。

#### 适用场景：

- 多个函数组合调用
- 组件间通信（React/Vue 组件）
- 服务层与数据层交互

#### 示例：测试 React 组件交互

```jsx
// LoginForm.jsx
function LoginForm({ onLogin }) {
    const [user, setUser] = useState('');
    return (
        <div>
            <input value={user} onChange={e => setUser(e.target.value)} />
            <button onClick={() => onLogin(user)}>登录</button>
        </div>
    );
}

// LoginForm.test.jsx
import { render, screen, fireEvent } from '@testing-library/react';
import '@testing-library/jest-dom';

test('calls onLogin with username', () => {
    const mockLogin = jest.fn();
    render(<LoginForm onLogin={mockLogin} />);
    
    fireEvent.change(screen.getByRole('textbox'), { target: { value: 'alice' } });
    fireEvent.click(screen.getByRole('button'));
    
    expect(mockLogin).toHaveBeenCalledWith('alice');
});
```

✅ 优势：
- 比单元测试更贴近真实使用场景
- 比 E2E 更快、更稳定

---

### 3. 端到端测试（End-to-End Testing, E2E）

E2E 测试模拟真实用户操作，从用户角度验证整个应用流程。

#### 常用工具：

- **Cypress**：语法简洁，自带 UI，适合中小型项目
- **Playwright**：支持多浏览器（Chromium、Firefox、WebKit），功能强大
- **Puppeteer**：底层控制 Chrome，适合爬虫和复杂自动化

#### 示例：Cypress 测试登录流程

```js
// cypress/e2e/login.cy.js
describe('Login Flow', () => {
    it('should login successfully', () => {
        cy.visit('/login');
        cy.get('input[name="username"]').type('testuser');
        cy.get('input[name="password"]').type('password123');
        cy.get('button[type="submit"]').click();
        cy.url().should('include', '/dashboard');
        cy.contains('欢迎回来');
    });
});
```

#### E2E 测试特点：

| 优点 | 缺点 |
|------|------|
| 最接近真实用户行为 | 执行慢（秒级） |
| 覆盖完整业务流程 | 容易受网络、环境影响 |
| 发现集成问题 | 维护成本高 |

✅ 建议：
- 用 E2E 测试核心路径（如注册、支付）
- 不要测试所有分支逻辑

---

### 4. 测试驱动开发（Test-Driven Development, TDD）

TDD 是一种开发方法论，遵循 **“红-绿-重构”** 循环：

1. **Red（红）**：先写一个失败的测试
2. **Green（绿）**：编写最简代码让测试通过
3. **Refactor（重构）**：优化代码结构，保持测试通过

#### TDD 流程示例：

```js
// 1. 写测试（红）
test('should validate email format', () => {
    expect(validateEmail('not-email')).toBe(false);
    expect(validateEmail('user@example.com')).toBe(true);
});

// 2. 写实现（绿）
function validateEmail(email) {
    return email.includes('@');
}

// 3. 重构（如增加更严格的正则）
function validateEmail(email) {
    const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return re.test(email);
}
```

#### TDD 的优势：

- 确保代码可测试
- 避免过度设计
- 提供即时反馈
- 形成完整的测试套件

#### 挑战：

- 学习曲线陡峭
- 初期开发速度变慢
- 不适合探索性开发

✅ 适用场景：
- 核心业务逻辑
- 工具库、SDK 开发
- 团队协作项目

---

## 总结：调试与测试最佳实践

| 类别 | 推荐做法 |
|------|----------|
| **调试** | 善用 DevTools、设置条件断点、分析性能和内存 |
| **单元测试** | 覆盖核心函数，使用 Jest + Mock |
| **集成测试** | 测试组件交互，使用 Testing Library |
| **E2E 测试** | 覆盖关键用户路径，使用 Playwright/Cypress |
| **TDD** | 在稳定需求中推行，形成自动化测试文化 |

---

## 附：完整测试金字塔

```
        E2E 测试（少量）
          ↑
    集成测试（中等）
          ↑
    单元测试（大量）
```

- **底层多，顶层少**：单元测试应占 70% 以上
- **越往上越慢越不稳定**
- **每层都不可或缺**

---

## 工具链推荐

| 用途 | 推荐工具 |
|------|----------|
| 调试 | Chrome DevTools、VS Code Debugger |
| 单元测试 | Jest、Vitest |
| 集成测试 | React Testing Library、Vue Test Utils |
| E2E 测试 | Playwright、Cypress |
| CI/CD | GitHub Actions、GitLab CI |
| 覆盖率 | `jest --coverage` |
| 错误监控 | Sentry、LogRocket |

---
# 十四、JavaScript 安全防护措施详解

在现代 Web 应用开发中，**安全**是不可忽视的核心要素。JavaScript 作为前端和后端（Node.js）的重要组成部分，既是攻击的入口，也是防御的关键环节。本章将从 **常见安全威胁** 和 **安全编码实践** 两个维度，系统深入地讲解如何构建安全的 JavaScript 应用。

---

## 14.1 常见安全威胁

### 1. XSS 攻击防护（跨站脚本攻击，Cross-Site Scripting）

#### 什么是 XSS？

XSS 是指攻击者将恶意脚本注入网页，当其他用户浏览时，脚本在他们的浏览器中执行，从而窃取 Cookie、会话令牌、篡改页面内容等。

#### XSS 类型：

| 类型 | 描述 | 示例 |
|------|------|------|
| **存储型 XSS** | 恶意脚本被永久存储在服务器（如评论、用户资料） | `<script>stealCookies()</script>` 存入数据库 |
| **反射型 XSS** | 恶意脚本通过 URL 参数反射回页面 | `https://example.com?search=<script>...</script>` |
| **DOM 型 XSS** | 通过 JavaScript 操作 DOM 注入脚本（纯前端） | `el.innerHTML = location.hash.slice(1)` |

#### 防护措施：

##### （1）输出编码（Output Encoding）

在将用户输入插入 HTML 前，进行 HTML 实体编码：

```js
function escapeHtml(text) {
    const div = document.createElement('div');
    div.textContent = text;
    return div.innerHTML;
}

// 使用
const userInput = '<script>alert("xss")</script>';
el.innerHTML = escapeHtml(userInput); // 显示为纯文本
```

##### （2）避免使用危险的 API

| 危险 API | 安全替代 |
|---------|----------|
| `innerHTML` | `textContent` |
| `document.write()` | `appendChild()` / `insertAdjacentHTML()` |
| `eval()` | 避免使用，改用 JSON.parse 等 |
| `setTimeout(string)` | 传函数而非字符串 |

✅ 推荐使用现代框架（React、Vue）的默认防护：
- React 使用 `{}` 插值自动转义
- Vue 使用 `{{ }}` 插值自动转义

##### （3）使用 CSP（内容安全策略）

通过 HTTP 头限制可执行的脚本来源：

```http
Content-Security-Policy: default-src 'self'; script-src 'self' https://trusted.cdn.com; object-src 'none';
```

- `'self'`：只允许同源脚本
- 禁止内联脚本（如 `<script>...</script>`）
- 禁止 `eval()`

> ✅ 强烈建议在生产环境中启用 CSP。

##### （4）使用 sanitizer 库

```js
import { sanitize } from 'dompurify';

const clean = sanitize(dirtyHTML); // 清理恶意标签
el.innerHTML = clean;
```

---

### 2. CSRF 攻击防范（跨站请求伪造，Cross-Site Request Forgery）

#### 什么是 CSRF？

攻击者诱导用户在已登录的状态下，向目标网站发送非预期的请求（如转账、修改密码），利用用户的认证状态执行操作。

#### 示例：

用户登录 `bank.com`，Cookie 被浏览器保存。  
攻击者诱导用户访问 `evil.com`，其中包含：

```html
<img src="https://bank.com/transfer?to=attacker&amount=1000" />
```

浏览器自动携带 `bank.com` 的 Cookie，完成转账。

#### 防护措施：

##### （1）使用 CSRF Token

- 服务器生成一次性 token，嵌入表单或响应头
- 前端在请求时携带 token（如 `X-CSRF-Token` 头）
- 服务器验证 token 有效性

```html
<!-- 表单中 -->
<input type="hidden" name="csrfToken" value="abc123" />
```

```js
// AJAX 请求
fetch('/api/action', {
    method: 'POST',
    headers: {
        'X-CSRF-Token': getToken(),
        'Content-Type': 'application/json'
    },
    body: JSON.stringify(data)
});
```

##### （2）SameSite Cookie 属性

设置 Cookie 的 `SameSite` 属性，防止跨站请求携带 Cookie：

```http
Set-Cookie: session=abc123; Path=/; Secure; HttpOnly; SameSite=Strict
```

- `Strict`：完全禁止跨站携带
- `Lax`：允许安全的跨站 GET 请求（推荐）
- `None`：允许跨站，但必须配合 `Secure`

✅ 建议设置为 `SameSite=Lax` 或 `Strict`。

##### （3）验证 `Origin` 或 `Referer` 头

服务器检查请求来源：

```js
// Node.js 示例
if (req.headers.origin !== 'https://yourdomain.com') {
    return res.status(403).send('Forbidden');
}
```

⚠️ 注意：`Referer` 可能被客户端屏蔽，不能作为唯一依据。

---

### 3. 数据注入攻击

#### （1）SQL 注入（Node.js 后端常见）

攻击者通过输入构造恶意 SQL 语句。

```js
// ❌ 危险：字符串拼接
const query = `SELECT * FROM users WHERE name = '${name}'`;

// ✅ 安全：使用参数化查询
db.query('SELECT * FROM users WHERE name = ?', [name]);
```

✅ 使用 ORM（如 Sequelize、TypeORM）或预处理语句。

#### （2）NoSQL 注入（MongoDB）

```js
// ❌ 危险
db.users.find({ username: req.body.username });

// 如果输入: { "$ne": "" } → 匹配所有用户

// ✅ 安全：验证和过滤输入
if (!/^[a-zA-Z0-9_]+$/.test(username)) {
    throw new Error('Invalid username');
}
```

#### （3）命令注入（Node.js）

```js
// ❌ 危险：执行系统命令
const { exec } = require('child_process');
exec(`ping ${ip}`, callback);

// 攻击输入: `127.0.0.1; rm -rf /`

// ✅ 安全：使用参数化或白名单
const ping = require('ping');
ping.promise.probe(ip);
```

---

### 4. 安全头设置（HTTP Security Headers）

通过 HTTP 响应头增强应用安全性。

#### 关键安全头：

| 头部 | 作用 | 示例 |
|------|------|------|
| `Content-Security-Policy` | 防止 XSS | `default-src 'self'; script-src 'self'` |
| `X-Content-Type-Options` | 禁止 MIME 类型嗅探 | `nosniff` |
| `X-Frame-Options` | 防止点击劫持 | `DENY` 或 `SAMEORIGIN` |
| `X-XSS-Protection` | 启用浏览器 XSS 过滤器（已过时） | `1; mode=block` |
| `Strict-Transport-Security` | 强制 HTTPS | `max-age=31536000; includeSubDomains` |
| `Referrer-Policy` | 控制 Referer 信息泄露 | `strict-origin-when-cross-origin` |

#### Node.js 中设置安全头（Express 示例）：

```js
const helmet = require('helmet');

app.use(helmet({
    contentSecurityPolicy: {
        directives: {
            defaultSrc: ["'self'"],
            scriptSrc: ["'self'", "https://trusted.cdn.com"],
            objectSrc: ["'none'"],
        }
    },
    hsts: { maxAge: 31536000, includeSubDomains: true },
    frameguard: { action: 'deny' }
}));
```

✅ 推荐使用 `helmet` 库一键启用多种安全头。

---

## 14.2 安全编码实践

### 1. 输入验证和过滤

所有用户输入都应视为**不可信**，必须验证和过滤。

#### 验证策略：

- **白名单验证**：只允许已知安全的字符或格式
- **类型检查**：确保输入是预期类型
- **长度限制**：防止超长输入导致缓冲区问题

```js
function validateEmail(email) {
    const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return re.test(email);
}

function sanitizeInput(str) {
    return str.trim().slice(0, 100); // 去空格 + 截断
}
```

#### 使用验证库：

- `joi`（Node.js）
- `yup`（前端/后端）
- `validator.js`

```js
const schema = require('yup').object({
    email: yup.string().email().required(),
    age: yup.number().integer().min(18).max(120)
});

try {
    await schema.validate(userData);
} catch (err) {
    console.error(err.errors);
}
```

---

### 2. 输出编码处理

在将数据插入不同上下文时，必须进行相应编码。

#### 编码类型：

| 上下文 | 编码方式 |
|--------|----------|
| HTML 内容 | HTML 实体编码（`&`, `<`, `>`, `"`, `'`） |
| HTML 属性 | 同上，且属性值用引号包围 |
| JavaScript 字符串 | JavaScript 转义（`\n`, `\u2028` 等） |
| URL 参数 | `encodeURIComponent()` |
| CSS | CSS 转义 |

```js
// 安全插入 JavaScript 字符串
const userContent = 'Hello "world" <script>';
const safe = `<script>show("${userContent.replace(/"/g, '\\"')}")</script>`;
// ❌ 仍有风险，应避免内联脚本

// 安全 URL
const url = `https://api.com/search?q=${encodeURIComponent(query)}`;
```

✅ 最佳实践：尽量避免动态生成脚本或样式，使用数据驱动方式（如 React state）。

---

### 3. 权限控制机制

确保用户只能访问其被授权的资源。

#### 常见问题：

- **水平越权**：用户 A 访问用户 B 的数据（如 `/api/user/2`）
- **垂直越权**：普通用户访问管理员接口（如 `/admin/delete`）

#### 防护措施：

##### （1）服务端权限验证

```js
// Node.js 示例
app.get('/api/user/:id', auth, async (req, res) => {
    const userId = req.params.id;
    if (req.user.id !== userId && !req.user.isAdmin) {
        return res.status(403).send('Forbidden');
    }
    const user = await User.findById(userId);
    res.json(user);
});
```

##### （2）最小权限原则

- 用户只拥有完成任务所需的最小权限
- 管理员功能应二次验证（如输入密码）

##### （3）敏感操作日志

记录关键操作（如删除、修改密码），便于审计。

```js
logAction(req.user.id, 'DELETE_USER', targetUserId);
```

---

### 4. 安全审计流程

建立系统化的安全审查机制，持续发现和修复漏洞。

#### 审计内容：

| 项目 | 说明 |
|------|------|
| **代码审查** | 检查是否存在 XSS、SQL 注入、硬编码密钥等 |
| **依赖扫描** | 使用 `npm audit` 或 `snyk` 检查第三方库漏洞 |
| **渗透测试** | 模拟攻击，发现潜在漏洞 |
| **安全配置检查** | 验证 CSP、HTTPS、Cookie 属性等 |
| **日志监控** | 监控异常登录、频繁失败请求等 |

#### 自动化工具：

- `npm audit`：检查依赖漏洞
- `snyk`：持续监控依赖安全
- `Retire.js`：检测已知漏洞库
- `OWASP ZAP`：自动化渗透测试工具
- `SonarQube`：代码质量与安全分析

#### 安全发布流程（Security Release Process）：

1. 开发阶段：遵循安全编码规范
2. 代码审查：团队成员交叉审查
3. 自动化扫描：CI 中集成 `npm audit`、`snyk`
4. 安全测试：定期进行渗透测试
5. 上线前审计：检查生产配置
6. 监控响应：上线后监控异常行为

---

## 总结：JavaScript 安全防护 checklist

| 风险 | 防护措施 |
|------|----------|
| **XSS** | 输出编码、CSP、避免 `innerHTML`、使用 sanitizer |
| **CSRF** | CSRF Token、SameSite Cookie、验证 Origin |
| **注入攻击** | 参数化查询、输入验证、避免 `eval` |
| **安全头** | 设置 CSP、HSTS、X-Frame-Options 等 |
| **输入安全** | 白名单验证、长度限制、类型检查 |
| **权限控制** | 服务端验证、最小权限、操作日志 |
| **依赖安全** | 定期 `npm audit`、使用 Snyk 监控 |
| **审计流程** | 代码审查、渗透测试、自动化扫描 |

---

## 附：安全开发原则（Secure by Design）

1. **默认安全**：新功能默认启用安全配置
2. **纵深防御**：多层防护，不依赖单一机制
3. **最小暴露**：只暴露必要的接口和数据
4. **失败安全**：异常情况下默认拒绝访问
5. **持续监控**：实时发现异常行为

---
# 十五、Node.js 基础知识

## 15.1 Node.js 概述

### Node.js 架构和特点

**架构概述：**
Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境，采用单线程事件循环架构。

```javascript
// Node.js 架构层次
┌──────────────────────────────────┐
│           应用程序层              │
├──────────────────────────────────┤
│        Node.js 标准库            │
├──────────────────────────────────┤
│        V8 引擎 + libuv           │
├──────────────────────────────────┤
│         操作系统 API             │
└──────────────────────────────────┘
```

**主要特点：**
- **单线程**：避免多线程的复杂性
- **非阻塞 I/O**：提高并发处理能力
- **事件驱动**：基于事件循环机制
- **跨平台**：支持 Windows、Linux、macOS

### V8 引擎工作机制

**V8 引擎组成：**
```javascript
// V8 引擎内部结构
┌─────────────┐    ┌─────────────┐
│   Parser    │    │  Ignition   │
│  (解析器)    │───▶│ (解释器)     │
└─────────────┘    └─────────────┘
                          │
                   ┌─────────────┐
                   │   TurboFan  │
                   │  (编译器)    │
                   └─────────────┘
```

**性能优化机制：**
```javascript
// 1. JIT 编译
function add(a, b) {
    return a + b; // 首次解释执行，后续优化编译
}

// 2. 内联缓存
const obj = { name: 'Node.js' };
console.log(obj.name); // 快速属性访问

// 3. 垃圾回收
// 新生代和老生代分代回收
```

### 事件驱动和非阻塞 I/O

**事件循环机制：**
```javascript
// 事件循环阶段
┌─────────────────────────────────────┐
│               timers                │
│    ┌─────────────────────────────┐  │
│    │ setTimeout(), setInterval() │  │
│    └─────────────────────────────┘  │
└─────────────────────────────────────┘
                    │
┌─────────────────────────────────────┐
│         pending callbacks           │
│    ┌─────────────────────────────┐  │
│    │  TCP errors, etc.          │  │
│    └─────────────────────────────┘  │
└─────────────────────────────────────┘
                    │
┌─────────────────────────────────────┐
│        idle, prepare                │
│    ┌─────────────────────────────┐  │
│    │   only used internally      │  │
│    └─────────────────────────────┘  │
└─────────────────────────────────────┘
                    │
┌─────────────────────────────────────┐
│              poll                   │
│    ┌─────────────────────────────┐  │
│    │ I/O callbacks, incoming     │  │
│    │ connections, data, etc.     │  │
│    └─────────────────────────────┘  │
└─────────────────────────────────────┘
                    │
┌─────────────────────────────────────┐
│              check                  │
│    ┌─────────────────────────────┐  │
│    │      setImmediate()         │  │
│    └─────────────────────────────┘  │
└─────────────────────────────────────┘
                    │
┌─────────────────────────────────────┐
│         close callbacks             │
│    ┌─────────────────────────────┐  │
│    │   socket.on('close', ...)   │  │
│    └─────────────────────────────┘  │
└─────────────────────────────────────┘
```

**非阻塞 I/O 示例：**
```javascript
const fs = require('fs');

// 阻塞方式（不推荐）
// const data = fs.readFileSync('file.txt');
// console.log(data.toString());

// 非阻塞方式（推荐）
fs.readFile('file.txt', (err, data) => {
    if (err) throw err;
    console.log(data.toString());
});

console.log('读取文件中...'); // 先执行
```

### Node.js 应用场景

**适用场景：**
```javascript
// 1. Web 服务器
const http = require('http');

const server = http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Hello Node.js!');
});

server.listen(3000);

// 2. API 服务
const express = require('express');
const app = express();

app.get('/api/users', (req, res) => {
    res.json({ users: [] });
});

// 3. 实时应用
const WebSocket = require('ws');
const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', (ws) => {
    ws.on('message', (message) => {
        console.log('received:', message);
    });
});

// 4. 命令行工具
#!/usr/bin/env node
const program = require('commander');

program
    .version('1.0.0')
    .command('init')
    .action(() => {
        console.log('初始化项目');
    });
```

## 15.2 Node.js 核心模块

### fs 模块文件操作

**基本文件操作：**
```javascript
const fs = require('fs');
const path = require('path');

// 同步操作
try {
    const data = fs.readFileSync('example.txt', 'utf8');
    console.log(data);
} catch (err) {
    console.error(err);
}

// 异步操作
fs.readFile('example.txt', 'utf8', (err, data) => {
    if (err) throw err;
    console.log(data);
});

// Promise 方式
const fsPromises = require('fs').promises;

async function readFileAsync() {
    try {
        const data = await fsPromises.readFile('example.txt', 'utf8');
        console.log(data);
    } catch (err) {
        console.error(err);
    }
}
```

**文件系统操作：**
```javascript
// 文件写入
fs.writeFile('output.txt', 'Hello World', (err) => {
    if (err) throw err;
    console.log('文件写入成功');
});

// 文件追加
fs.appendFile('log.txt', '新日志内容\n', (err) => {
    if (err) throw err;
});

// 文件信息
fs.stat('example.txt', (err, stats) => {
    if (err) throw err;
    console.log(`文件大小: ${stats.size} bytes`);
    console.log(`是否为文件: ${stats.isFile()}`);
    console.log(`修改时间: ${stats.mtime}`);
});

// 目录操作
fs.readdir('./', (err, files) => {
    if (err) throw err;
    console.log('目录内容:', files);
});

// 创建目录
fs.mkdir('./newDir', { recursive: true }, (err) => {
    if (err) throw err;
});
```

### path 模路径处理

**路径操作：**
```javascript
const path = require('path');

// 路径拼接
const fullPath = path.join(__dirname, 'public', 'index.html');
console.log(fullPath);

// 路径解析
const parsedPath = path.parse('/users/node/app.js');
console.log(parsedPath);
// {
//   root: '/',
//   dir: '/users/node',
//   base: 'app.js',
//   ext: '.js',
//   name: 'app'
// }

// 路径规范化
console.log(path.normalize('/users//node/../node/app.js'));
// 输出: /users/node/app.js

// 相对路径
console.log(path.relative('/users/node', '/users/admin'));
// 输出: ../admin

// 路径分隔符
console.log(path.sep); // Windows: \, Unix: /
```

### http/https 网络模块

**HTTP 服务器：**
```javascript
const http = require('http');
const url = require('url');

const server = http.createServer((req, res) => {
    const parsedUrl = url.parse(req.url, true);
    const path = parsedUrl.pathname;
    const query = parsedUrl.query;
    
    // 设置响应头
    res.writeHead(200, {
        'Content-Type': 'application/json',
        'Access-Control-Allow-Origin': '*'
    });
    
    // 路由处理
    if (path === '/api/users' && req.method === 'GET') {
        res.end(JSON.stringify({ users: [] }));
    } else if (path === '/api/users' && req.method === 'POST') {
        let body = '';
        req.on('data', chunk => {
            body += chunk.toString();
        });
        req.on('end', () => {
            const userData = JSON.parse(body);
            res.end(JSON.stringify({ id: 1, ...userData }));
        });
    } else {
        res.writeHead(404);
        res.end('Not Found');
    }
});

server.listen(3000, () => {
    console.log('服务器运行在 http://localhost:3000');
});
```

**HTTP 客户端：**
```javascript
const http = require('http');

// 发送 GET 请求
const options = {
    hostname: 'jsonplaceholder.typicode.com',
    port: 80,
    path: '/posts/1',
    method: 'GET'
};

const req = http.request(options, (res) => {
    let data = '';
    
    res.on('data', (chunk) => {
        data += chunk;
    });
    
    res.on('end', () => {
        console.log(JSON.parse(data));
    });
});

req.on('error', (error) => {
    console.error(error);
});

req.end();
```

### events 事件系统

**事件发射器：**
```javascript
const EventEmitter = require('events');

class MyEmitter extends EventEmitter {}

const myEmitter = new MyEmitter();

// 监听事件
myEmitter.on('event', (data) => {
    console.log('事件触发:', data);
});

// 监听一次
myEmitter.once('startup', () => {
    console.log('应用启动');
});

// 发射事件
myEmitter.emit('event', { message: 'Hello World' });
myEmitter.emit('startup');
myEmitter.emit('startup'); // 不会再次触发

// 移除监听器
const listener = (data) => console.log('监听器:', data);
myEmitter.on('test', listener);
myEmitter.removeListener('test', listener);

// 错误处理
myEmitter.on('error', (err) => {
    console.error('发生错误:', err.message);
});
```

### stream 流处理

**可读流：**
```javascript
const fs = require('fs');

// 创建可读流
const readableStream = fs.createReadStream('large-file.txt');

readableStream.on('data', (chunk) => {
    console.log(`接收到 ${chunk.length} 字节的数据`);
});

readableStream.on('end', () => {
    console.log('数据读取完成');
});

readableStream.on('error', (err) => {
    console.error('读取错误:', err);
});
```

**可写流：**
```javascript
const fs = require('fs');

// 创建可写流
const writableStream = fs.createWriteStream('output.txt');

writableStream.write('第一行数据\n');
writableStream.write('第二行数据\n');
writableStream.end('最后一行数据');

writableStream.on('finish', () => {
    console.log('写入完成');
});
```

**管道流：**
```javascript
const fs = require('fs');
const zlib = require('zlib');

// 文件压缩
const readStream = fs.createReadStream('input.txt');
const writeStream = fs.createWriteStream('input.txt.gz');
const gzip = zlib.createGzip();

readStream.pipe(gzip).pipe(writeStream);

// 链式处理
readStream
    .pipe(zlib.createGzip())
    .pipe(fs.createWriteStream('output.txt.gz'));
```

### buffer 缓冲区操作

**Buffer 基本操作：**
```javascript
// 创建 Buffer
const buf1 = Buffer.alloc(10); // 创建长度为10的零填充Buffer
const buf2 = Buffer.allocUnsafe(10); // 创建未初始化的Buffer
const buf3 = Buffer.from([1, 2, 3, 4]); // 从数组创建
const buf4 = Buffer.from('Hello World', 'utf8'); // 从字符串创建

// Buffer 操作
console.log(buf4.length); // 11
console.log(buf4.toString()); // 'Hello World'
console.log(buf4.toString('hex')); // 十六进制表示

// Buffer 拼接
const bufA = Buffer.from('Hello ');
const bufB = Buffer.from('World');
const bufC = Buffer.concat([bufA, bufB]);
console.log(bufC.toString()); // 'Hello World'

// Buffer 比较
const buf1 = Buffer.from('ABC');
const buf2 = Buffer.from('ABCD');
console.log(buf1.compare(buf2)); // -1
```

## 15.3 模块系统

### CommonJS 规范

**模块定义和导出：**
```javascript
// math.js - 模块定义
function add(a, b) {
    return a + b;
}

function subtract(a, b) {
    return a - b;
}

// 方式1: 对象导出
module.exports = {
    add,
    subtract
};

// 方式2: 单个导出
module.exports.add = add;
module.exports.subtract = subtract;

// 方式3: exports 简写
exports.add = add;
exports.subtract = subtract;

// 方式4: 默认导出
module.exports = add; // 默认导出 add 函数
```

**模块导入：**
```javascript
// app.js - 模块使用
const math = require('./math'); // 导入整个模块
const { add, subtract } = require('./math'); // 解构导入
const addFunction = require('./math'); // 导入默认导出

console.log(math.add(1, 2)); // 3
console.log(add(1, 2)); // 3
console.log(addFunction(1, 2)); // 3
```

### 模块加载机制

**模块解析过程：**
```javascript
// 模块加载顺序
// 1. 核心模块
const fs = require('fs');

// 2. 相对路径文件模块
const myModule = require('./myModule');

// 3. 绝对路径文件模块
const absoluteModule = require('/absolute/path/to/module');

// 4. node_modules 中的模块
const express = require('express');

// 模块缓存机制
console.log(require.cache); // 查看模块缓存

// 清除模块缓存
delete require.cache[require.resolve('./myModule')];
```

**模块包装：**
```javascript
// Node.js 实际上将模块包装成函数
(function(exports, require, module, __filename, __dirname) {
    // 模块代码在这里执行
    const fs = require('fs');
    
    function myFunction() {
        console.log(__filename); // 当前文件路径
        console.log(__dirname);  // 当前目录路径
    }
    
    module.exports = myFunction;
});
```

### 内置模块和第三方模块

**内置模块使用：**
```javascript
// 常用内置模块
const os = require('os');
const path = require('path');
const fs = require('fs');
const http = require('http');
const crypto = require('crypto');

// 系统信息
console.log(os.platform()); // 操作系统平台
console.log(os.cpus()); // CPU 信息
console.log(os.totalmem()); // 总内存

// 加密
const hash = crypto.createHash('sha256');
hash.update('password');
console.log(hash.digest('hex'));
```

**第三方模块管理：**
```json
// package.json
{
  "name": "my-app",
  "version": "1.0.0",
  "dependencies": {
    "express": "^4.18.0",
    "lodash": "^4.17.21"
  },
  "devDependencies": {
    "nodemon": "^2.0.20"
  },
  "scripts": {
    "start": "node app.js",
    "dev": "nodemon app.js"
  }
}
```

```javascript
// 使用第三方模块
const express = require('express');
const _ = require('lodash');

const app = express();

// lodash 使用示例
const users = [
    { name: 'Alice', age: 25 },
    { name: 'Bob', age: 30 }
];

const youngUsers = _.filter(users, user => user.age < 30);
console.log(youngUsers);
```

### 模块缓存机制

**缓存演示：**
```javascript
// counter.js
let count = 0;

function increment() {
    return ++count;
}

module.exports = {
    increment,
    getCount: () => count
};

// app.js
const counter1 = require('./counter');
const counter2 = require('./counter'); // 同一个模块

console.log(counter1.increment()); // 1
console.log(counter2.increment()); // 2
console.log(counter1 === counter2); // true - 同一个实例

// 查看缓存
console.log(Object.keys(require.cache));

// 清除缓存（开发环境调试用）
delete require.cache[require.resolve('./counter')];
```

**循环依赖处理：**
```javascript
// a.js
console.log('a 开始');
exports.done = false;
const b = require('./b.js');
console.log('在 a 中, b.done = %j', b.done);
exports.done = true;
console.log('a 结束');

// b.js
console.log('b 开始');
exports.done = false;
const a = require('./a.js'); // 循环依赖
console.log('在 b 中, a.done = %j', a.done);
exports.done = true;
console.log('b 结束');

// main.js
console.log('main 开始');
const a = require('./a.js');
const b = require('./b.js');
console.log('在 main 中, a.done=%j, b.done=%j', a.done, b.done);
```

# 十六、Node.js 进阶特性

## 16.1 异步编程

### 回调函数模式

**错误优先回调约定：**
```javascript
// Node.js 标准回调模式：(error, data) => {}
const fs = require('fs');

// 正确的回调函数模式
function readFile(filename, callback) {
    fs.readFile(filename, 'utf8', (err, data) => {
        if (err) {
            // 错误优先返回
            return callback(err, null);
        }
        callback(null, data);
    });
}

// 使用回调函数
readFile('example.txt', (err, data) => {
    if (err) {
        console.error('读取文件失败:', err.message);
        return;
    }
    console.log('文件内容:', data);
});

// 回调地狱示例
fs.readFile('file1.txt', 'utf8', (err, data1) => {
    if (err) throw err;
    fs.readFile('file2.txt', 'utf8', (err, data2) => {
        if (err) throw err;
        fs.readFile('file3.txt', 'utf8', (err, data3) => {
            if (err) throw err;
            console.log(data1, data2, data3);
        });
    });
});
```

**自定义回调函数实现：**
```javascript
// 模拟异步操作
function asyncOperation(data, callback) {
    setTimeout(() => {
        if (Math.random() > 0.5) {
            callback(null, `处理完成: ${data}`);
        } else {
            callback(new Error('处理失败'));
        }
    }, 1000);
}

// 并行执行
function parallelExecution(tasks, callback) {
    let completed = 0;
    let results = [];
    let hasError = false;

    if (tasks.length === 0) {
        return callback(null, []);
    }

    tasks.forEach((task, index) => {
        task((err, result) => {
            if (hasError) return;
            
            if (err) {
                hasError = true;
                return callback(err);
            }

            results[index] = result;
            completed++;

            if (completed === tasks.length) {
                callback(null, results);
            }
        });
    });
}

// 串行执行
function serialExecution(tasks, callback) {
    let results = [];

    function executeTask(index) {
        if (index >= tasks.length) {
            return callback(null, results);
        }

        tasks[index]((err, result) => {
            if (err) return callback(err);
            results.push(result);
            executeTask(index + 1);
        });
    }

    executeTask(0);
}
```

### Promise 在 Node.js 中的应用

**Promise 基本使用：**
```javascript
const fs = require('fs').promises;

// 将回调转换为 Promise
function promisify(fn) {
    return function(...args) {
        return new Promise((resolve, reject) => {
            fn.call(this, ...args, (err, result) => {
                if (err) reject(err);
                else resolve(result);
            });
        });
    };
}

// 使用 promisify
const readFile = promisify(fs.readFile);
const writeFile = promisify(fs.writeFile);

// Promise 链式调用
readFile('input.txt', 'utf8')
    .then(data => {
        console.log('读取数据:', data);
        return data.toUpperCase();
    })
    .then(upperData => {
        return writeFile('output.txt', upperData);
    })
    .then(() => {
        console.log('文件写入完成');
    })
    .catch(err => {
        console.error('操作失败:', err.message);
    });
```

**Promise 组合操作：**
```javascript
// 并行执行
Promise.all([
    fs.readFile('file1.txt', 'utf8'),
    fs.readFile('file2.txt', 'utf8'),
    fs.readFile('file3.txt', 'utf8')
]).then(results => {
    console.log('所有文件读取完成:', results);
}).catch(err => {
    console.error('读取失败:', err);
});

// 竞争执行
Promise.race([
    fetch('http://api1.com/data'),
    fetch('http://api2.com/data')
]).then(response => {
    console.log('最快的响应:', response);
});

// 全部完成（包括失败）
Promise.allSettled([
    fs.readFile('file1.txt', 'utf8'),
    fs.readFile('file2.txt', 'utf8')
]).then(results => {
    results.forEach((result, index) => {
        if (result.status === 'fulfilled') {
            console.log(`文件${index + 1}读取成功:`, result.value);
        } else {
            console.log(`文件${index + 1}读取失败:`, result.reason);
        }
    });
});
```

### async/await 语法支持

**基本 async/await 使用：**
```javascript
const fs = require('fs').promises;

// async 函数
async function processFiles() {
    try {
        // 串行执行
        const data1 = await fs.readFile('file1.txt', 'utf8');
        const data2 = await fs.readFile('file2.txt', 'utf8');
        console.log('串行读取:', data1, data2);

        // 并行执行
        const [content1, content2] = await Promise.all([
            fs.readFile('file1.txt', 'utf8'),
            fs.readFile('file2.txt', 'utf8')
        ]);
        console.log('并行读取:', content1, content2);

        // 处理数据
        const processedData = await processData(content1, content2);
        await fs.writeFile('result.txt', processedData);
        
        return '处理完成';
    } catch (error) {
        console.error('处理过程中出错:', error.message);
        throw error;
    }
}

async function processData(data1, data2) {
    // 模拟异步数据处理
    return new Promise(resolve => {
        setTimeout(() => {
            resolve(data1 + data2);
        }, 1000);
    });
}

// 调用 async 函数
processFiles()
    .then(result => console.log(result))
    .catch(err => console.error(err));
```

**错误处理最佳实践：**
```javascript
async function robustAsyncFunction() {
    try {
        // 可能失败的操作
        const data = await riskyOperation();
        return data;
    } catch (error) {
        // 记录错误
        console.error('操作失败:', error);
        
        // 返回默认值或重新抛出
        return null; // 或 throw error;
    }
}

// 错误边界处理
async function handleMultipleOperations() {
    const operations = [
        asyncOperation1(),
        asyncOperation2(),
        asyncOperation3()
    ];

    const results = [];
    for (let i = 0; i < operations.length; i++) {
        try {
            const result = await operations[i];
            results.push({ success: true,  result });
        } catch (error) {
            results.push({ success: false, error: error.message });
        }
    }

    return results;
}
```

### 错误优先回调约定

**自定义错误处理：**
```javascript
// 统一错误处理中间件
function createErrorHandler(callback) {
    return function(error, result) {
        if (error) {
            console.error('操作失败:', error.message);
            // 可以添加日志记录、监控等
            if (callback) callback(error);
            return;
        }
        if (callback) callback(null, result);
    };
}

// 使用错误处理中间件
function readFileWithHandler(filename, callback) {
    const handler = createErrorHandler(callback);
    
    fs.readFile(filename, 'utf8', (err, data) => {
        if (err) return handler(err);
        handler(null, data.toUpperCase());
    });
}

// 链式错误处理
function chainOperations(callback) {
    const handler = createErrorHandler(callback);
    
    step1((err, result1) => {
        if (err) return handler(err);
        
        step2(result1, (err, result2) => {
            if (err) return handler(err);
            
            step3(result2, handler);
        });
    });
}
```

## 16.2 进程管理

### process 对象使用

**process 对象属性和方法：**
```javascript
// 进程信息
console.log('进程ID:', process.pid);
console.log('进程标题:', process.title);
console.log('Node.js版本:', process.version);
console.log('平台信息:', process.platform);
console.log('架构信息:', process.arch);
console.log('当前工作目录:', process.cwd());
console.log('环境变量:', process.env);

// 内存使用情况
const memoryUsage = process.memoryUsage();
console.log('内存使用:', {
    rss: `${Math.round(memoryUsage.rss / 1024 / 1024)} MB`,
    heapTotal: `${Math.round(memoryUsage.heapTotal / 1024 / 1024)} MB`,
    heapUsed: `${Math.round(memoryUsage.heapUsed / 1024 / 1024)} MB`,
    external: `${Math.round(memoryUsage.external / 1024 / 1024)} MB`
});

// CPU 使用时间
const cpuUsage = process.cpuUsage();
console.log('CPU使用:', cpuUsage);

// 进程控制
process.nextTick(() => {
    console.log('下次事件循环开始时执行');
});

// 退出处理
process.on('exit', (code) => {
    console.log(`进程即将退出，退出码: ${code}`);
});

process.on('beforeExit', (code) => {
    console.log(`进程准备退出，退出码: ${code}`);
});

// 信号处理
process.on('SIGINT', () => {
    console.log('接收到 SIGINT 信号 (Ctrl+C)');
    process.exit(0);
});

process.on('SIGTERM', () => {
    console.log('接收到 SIGTERM 信号');
    process.exit(0);
});

// 异常处理
process.on('uncaughtException', (err) => {
    console.error('未捕获的异常:', err);
    process.exit(1);
});

process.on('unhandledRejection', (reason, promise) => {
    console.error('未处理的 Promise 拒绝:', reason);
    process.exit(1);
});
```

### 子进程创建和管理

**child_process 模块使用：**
```javascript
const { spawn, exec, execFile, fork } = require('child_process');
const path = require('path');

// spawn - 执行命令
function spawnExample() {
    const ls = spawn('ls', ['-lh', '/usr']);

    ls.stdout.on('data', (data) => {
        console.log(`stdout: ${data}`);
    });

    ls.stderr.on('data', (data) => {
        console.error(`stderr: ${data}`);
    });

    ls.on('close', (code) => {
        console.log(`子进程退出，退出码 ${code}`);
    });
}

// exec - 执行命令并缓存输出
function execExample() {
    exec('node --version', (error, stdout, stderr) => {
        if (error) {
            console.error(`执行错误: ${error}`);
            return;
        }
        if (stderr) {
            console.error(`stderr: ${stderr}`);
            return;
        }
        console.log(`stdout: ${stdout}`);
    });
}

// execFile - 执行可执行文件
function execFileExample() {
    const child = execFile('node', ['--version'], (error, stdout, stderr) => {
        if (error) {
            throw error;
        }
        console.log(stdout);
    });
}

// fork - 创建 Node.js 子进程
function forkExample() {
    const child = fork(path.join(__dirname, 'child.js'));

    child.on('message', (message) => {
        console.log('来自主进程的消息:', message);
    });

    child.send({ hello: 'world' });

    child.on('exit', (code) => {
        console.log(`子进程退出，退出码: ${code}`);
    });
}
```

**子进程通信：**
```javascript
// parent.js
const { fork } = require('child_process');
const path = require('path');

const child = fork(path.join(__dirname, 'worker.js'));

// 向子进程发送消息
child.send({ type: 'start',  [1, 2, 3, 4, 5] });

// 接收子进程消息
child.on('message', (message) => {
    switch (message.type) {
        case 'result':
            console.log('计算结果:', message.data);
            break;
        case 'progress':
            console.log('进度:', message.data);
            break;
        case 'error':
            console.error('子进程错误:', message.data);
            break;
    }
});

child.on('exit', (code) => {
    console.log('子进程退出，代码:', code);
});

// worker.js
process.on('message', (message) => {
    if (message.type === 'start') {
        const data = message.data;
        
        // 模拟长时间运行的任务
        let result = 0;
        for (let i = 0; i < data.length; i++) {
            result += data[i] * data[i];
            
            // 发送进度更新
            if (i % 1000 === 0) {
                process.send({
                    type: 'progress',
                    data: { current: i, total: data.length }
                });
            }
        }
        
        // 发送结果
        process.send({
            type: 'result',
             result
        });
    }
});

process.on('disconnect', () => {
    console.log('与父进程断开连接');
    process.exit(0);
});
```

### 集群模式应用

**cluster 模块使用：**
```javascript
const cluster = require('cluster');
const http = require('http');
const numCPUs = require('os').cpus().length;

if (cluster.isMaster) {
    console.log(`主进程 ${process.pid} 正在运行`);
    
    // 衍生工作进程
    for (let i = 0; i < numCPUs; i++) {
        cluster.fork();
    }
    
    // 工作进程死亡时重新衍生
    cluster.on('exit', (worker, code, signal) => {
        console.log(`工作进程 ${worker.process.pid} 已死亡`);
        cluster.fork(); // 重新启动
    });
    
    // 监听工作进程消息
    cluster.on('message', (worker, message) => {
        console.log(`来自主进程 ${worker.id} 的消息:`, message);
    });
    
} else {
    // 工作进程可以共享任何 TCP 连接
    // 在本例中，它是一个 HTTP 服务器
    http.createServer((req, res) => {
        res.writeHead(200);
        res.end(`Hello World from worker ${process.pid}`);
        
        // 向主进程发送消息
        process.send({ 
            pid: process.pid, 
            url: req.url,
            timestamp: Date.now()
        });
    }).listen(8000);
    
    console.log(`工作进程 ${process.pid} 已启动`);
}
```

**负载均衡集群：**
```javascript
const cluster = require('cluster');
const express = require('express');

if (cluster.isMaster) {
    const numWorkers = require('os').cpus().length;
    
    console.log(`主进程 ${process.pid} 启动，创建 ${numWorkers} 个工作进程`);
    
    // 创建工作进程
    for (let i = 0; i < numWorkers; i++) {
        const worker = cluster.fork();
        
        // 监控工作进程状态
        worker.on('message', (msg) => {
            if (msg.cmd === 'status') {
                console.log(`工作进程 ${worker.id}: ${msg.data}`);
            }
        });
    }
    
    // 处理工作进程死亡
    cluster.on('exit', (worker, code, signal) => {
        console.log(`工作进程 ${worker.process.pid} 退出 (code: ${code})`);
        
        // 重启工作进程
        if (!worker.exitedAfterDisconnect) {
            console.log('重新启动工作进程...');
            cluster.fork();
        }
    });
    
} else {
    // 工作进程代码
    const app = express();
    
    // 中间件统计请求
    let requestCount = 0;
    app.use((req, res, next) => {
        requestCount++;
        next();
    });
    
    // 路由
    app.get('/', (req, res) => {
        res.json({
            message: 'Hello from worker',
            workerId: cluster.worker.id,
            pid: process.pid,
            requestCount: requestCount
        });
    });
    
    app.get('/status', (req, res) => {
        res.json({
            workerId: cluster.worker.id,
            pid: process.pid,
            requestCount: requestCount,
            uptime: process.uptime()
        });
    });
    
    // 定期向主进程报告状态
    setInterval(() => {
        process.send({
            cmd: 'status',
            data: `Worker ${cluster.worker.id} serving ${requestCount} requests`
        });
    }, 5000);
    
    const server = app.listen(3000, () => {
        console.log(`工作进程 ${process.pid} 监听端口 3000`);
    });
    
    // 优雅关闭
    process.on('SIGTERM', () => {
        console.log(`工作进程 ${process.pid} 正在关闭`);
        server.close(() => {
            process.exit(0);
        });
    });
}
```

### 进程间通信机制

**IPC 通信示例：**
```javascript
// master.js
const cluster = require('cluster');
const numCPUs = require('os').cpus().length;

if (cluster.isMaster) {
    console.log('主进程启动');
    
    // 存储工作进程引用
    const workers = [];
    
    // 创建工作进程
    for (let i = 0; i < numCPUs; i++) {
        const worker = cluster.fork();
        workers.push(worker);
        
        // 处理工作进程消息
        worker.on('message', (msg) => {
            handleWorkerMessage(worker, msg, workers);
        });
    }
    
    // 向所有工作进程广播消息
    function broadcast(message) {
        workers.forEach(worker => {
            if (worker.isConnected()) {
                worker.send(message);
            }
        });
    }
    
    // 处理工作进程消息
    function handleWorkerMessage(sender, message, allWorkers) {
        switch (message.type) {
            case 'task':
                console.log(`收到任务请求 from worker ${sender.id}`);
                // 分配任务给其他工作进程
                const otherWorkers = allWorkers.filter(w => w.id !== sender.id);
                if (otherWorkers.length > 0) {
                    const targetWorker = otherWorkers[0];
                    targetWorker.send({
                        type: 'assigned_task',
                        data: message.data,
                        from: sender.id
                    });
                }
                break;
                
            case 'result':
                console.log(`收到结果 from worker ${sender.id}:`, message.data);
                // 将结果转发给原始请求者
                if (message.originalSender) {
                    const originalWorker = allWorkers.find(w => w.id == message.originalSender);
                    if (originalWorker && originalWorker.isConnected()) {
                        originalWorker.send({
                            type: 'task_result',
                            data: message.data
                        });
                    }
                }
                break;
                
            case 'health_check':
                console.log(`健康检查 from worker ${sender.id}`);
                sender.send({ type: 'health_response', status: 'ok' });
                break;
        }
    }
    
} else {
    // worker.js
    console.log(`工作进程 ${process.pid} 启动`);
    
    // 处理主进程消息
    process.on('message', (message) => {
        switch (message.type) {
            case 'assigned_task':
                console.log(`收到分配的任务:`, message.data);
                // 处理任务
                setTimeout(() => {
                    const result = `处理完成: ${message.data}`;
                    process.send({
                        type: 'result',
                        data: result,
                        originalSender: message.from
                    });
                }, 1000);
                break;
                
            case 'health_response':
                console.log('健康检查响应:', message.status);
                break;
                
            case 'broadcast':
                console.log('广播消息:', message.data);
                break;
        }
    });
    
    // 定期发送健康检查
    setInterval(() => {
        if (process.connected) {
            process.send({ type: 'health_check' });
        }
    }, 10000);
    
    // 发送任务请求
    setTimeout(() => {
        process.send({
            type: 'task',
             '处理大量数据'
        });
    }, 2000);
}
```

## 16.3 网络编程

### HTTP 服务器创建

**基础 HTTP 服务器：**
```javascript
const http = require('http');
const url = require('url');
const querystring = require('querystring');

// 创建 HTTP 服务器
const server = http.createServer((req, res) => {
    const parsedUrl = url.parse(req.url, true);
    const pathname = parsedUrl.pathname;
    const query = parsedUrl.query;
    const method = req.method;
    
    // 设置 CORS 头
    res.setHeader('Access-Control-Allow-Origin', '*');
    res.setHeader('Access-Control-Allow-Methods', 'GET, POST, PUT, DELETE, OPTIONS');
    res.setHeader('Access-Control-Allow-Headers', 'Content-Type, Authorization');
    
    // 处理预检请求
    if (method === 'OPTIONS') {
        res.writeHead(200);
        res.end();
        return;
    }
    
    // 路由处理
    if (pathname === '/api/users' && method === 'GET') {
        handleGetUsers(req, res, query);
    } else if (pathname === '/api/users' && method === 'POST') {
        handleCreateUser(req, res);
    } else if (pathname.startsWith('/api/users/') && method === 'GET') {
        const userId = pathname.split('/')[3];
        handleGetUser(req, res, userId);
    } else if (pathname === '/upload' && method === 'POST') {
        handleFileUpload(req, res);
    } else {
        res.writeHead(404, { 'Content-Type': 'application/json' });
        res.end(JSON.stringify({ error: 'Not Found' }));
    }
});

// 处理 GET /api/users
function handleGetUsers(req, res, query) {
    const users = [
        { id: 1, name: 'Alice', email: 'alice@example.com' },
        { id: 2, name: 'Bob', email: 'bob@example.com' }
    ];
    
    // 支持分页和过滤
    const page = parseInt(query.page) || 1;
    const limit = parseInt(query.limit) || 10;
    const offset = (page - 1) * limit;
    
    const filteredUsers = users.slice(offset, offset + limit);
    
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({
        data: filteredUsers,
        pagination: {
            page,
            limit,
            total: users.length
        }
    }));
}

// 处理 POST /api/users
function handleCreateUser(req, res) {
    let body = '';
    
    req.on('data', chunk => {
        body += chunk.toString();
    });
    
    req.on('end', () => {
        try {
            const userData = JSON.parse(body);
            
            // 验证数据
            if (!userData.name || !userData.email) {
                res.writeHead(400, { 'Content-Type': 'application/json' });
                res.end(JSON.stringify({ error: 'Name and email are required' }));
                return;
            }
            
            // 创建用户（模拟）
            const newUser = {
                id: Date.now(),
                ...userData,
                createdAt: new Date().toISOString()
            };
            
            res.writeHead(201, { 'Content-Type': 'application/json' });
            res.end(JSON.stringify(newUser));
        } catch (error) {
            res.writeHead(400, { 'Content-Type': 'application/json' });
            res.end(JSON.stringify({ error: 'Invalid JSON' }));
        }
    });
}

// 处理 GET /api/users/:id
function handleGetUser(req, res, userId) {
    const user = { id: userId, name: 'User Name', email: 'user@example.com' };
    
    if (!user) {
        res.writeHead(404, { 'Content-Type': 'application/json' });
        res.end(JSON.stringify({ error: 'User not found' }));
        return;
    }
    
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify(user));
}

// 处理文件上传
function handleFileUpload(req, res) {
    const contentType = req.headers['content-type'];
    
    if (!contentType || !contentType.includes('multipart/form-data')) {
        res.writeHead(400, { 'Content-Type': 'application/json' });
        res.end(JSON.stringify({ error: 'Content-Type must be multipart/form-data' }));
        return;
    }
    
    let body = '';
    
    req.on('data', chunk => {
        body += chunk.toString();
    });
    
    req.on('end', () => {
        // 这里应该解析 multipart 数据
        // 实际应用中建议使用 multer 等库
        res.writeHead(200, { 'Content-Type': 'application/json' });
        res.end(JSON.stringify({ 
            message: 'File uploaded successfully',
            size: body.length 
        }));
    });
}

// 服务器配置
server.on('clientError', (err, socket) => {
    socket.end('HTTP/1.1 400 Bad Request\r\n\r\n');
});

server.listen(3000, () => {
    console.log('服务器运行在 http://localhost:3000');
});

// 优雅关闭
process.on('SIGTERM', () => {
    console.log('接收到 SIGTERM 信号，正在关闭服务器...');
    server.close(() => {
        console.log('服务器已关闭');
        process.exit(0);
    });
});
```

### WebSocket 实时通信

**WebSocket 服务器：**
```javascript
const WebSocket = require('ws');
const http = require('http');

// 创建 HTTP 服务器
const server = http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('WebSocket Server');
});

// 创建 WebSocket 服务器
const wss = new WebSocket.Server({ server });

// 存储连接的客户端
const clients = new Set();

// 处理新连接
wss.on('connection', (ws, req) => {
    console.log('新的 WebSocket 连接');
    
    // 添加客户端到集合
    clients.add(ws);
    
    // 发送欢迎消息
    ws.send(JSON.stringify({
        type: 'welcome',
        message: '连接成功',
        timestamp: Date.now()
    }));
    
    // 处理消息
    ws.on('message', (message) => {
        try {
            const data = JSON.parse(message);
            handleWebSocketMessage(ws, data);
        } catch (error) {
            console.error('消息解析错误:', error);
            ws.send(JSON.stringify({
                type: 'error',
                message: 'Invalid message format'
            }));
        }
    });
    
    // 处理连接关闭
    ws.on('close', () => {
        console.log('WebSocket 连接关闭');
        clients.delete(ws);
        broadcast({
            type: 'user_left',
            timestamp: Date.now()
        });
    });
    
    // 处理错误
    ws.on('error', (error) => {
        console.error('WebSocket 错误:', error);
        clients.delete(ws);
    });
    
    // 通知其他用户有新用户加入
    broadcast({
        type: 'user_joined',
        timestamp: Date.now()
    });
});

// 处理 WebSocket 消息
function handleWebSocketMessage(ws, data) {
    switch (data.type) {
        case 'chat_message':
            // 广播聊天消息
            broadcast({
                type: 'chat_message',
                user: data.user,
                message: data.message,
                timestamp: Date.now()
            }, ws); // 排除发送者
            break;
            
        case 'typing':
            // 广播打字状态
            broadcast({
                type: 'typing',
                user: data.user,
                typing: data.typing
            }, ws);
            break;
            
        case 'ping':
            // 回复 pong
            ws.send(JSON.stringify({
                type: 'pong',
                timestamp: Date.now()
            }));
            break;
            
        default:
            ws.send(JSON.stringify({
                type: 'error',
                message: 'Unknown message type'
            }));
    }
}

// 广播消息给所有客户端
function broadcast(message, excludeClient = null) {
    const messageString = JSON.stringify(message);
    
    clients.forEach(client => {
        if (client !== excludeClient && client.readyState === WebSocket.OPEN) {
            client.send(messageString);
        }
    });
}

// 定期发送心跳
setInterval(() => {
    broadcast({
        type: 'heartbeat',
        timestamp: Date.now()
    });
}, 30000);

// 启动服务器
server.listen(8080, () => {
    console.log('WebSocket 服务器运行在 ws://localhost:8080');
});
```

**WebSocket 客户端示例：**
```javascript
// client.js
const WebSocket = require('ws');

// 连接到 WebSocket 服务器
const ws = new WebSocket('ws://localhost:8080');

ws.on('open', () => {
    console.log('连接已建立');
    
    // 发送聊天消息
    ws.send(JSON.stringify({
        type: 'chat_message',
        user: 'Alice',
        message: 'Hello everyone!'
    }));
    
    // 发送打字状态
    ws.send(JSON.stringify({
        type: 'typing',
        user: 'Alice',
        typing: true
    }));
});

ws.on('message', (data) => {
    try {
        const message = JSON.parse(data);
        console.log('收到消息:', message);
        
        switch (message.type) {
            case 'chat_message':
                console.log(`${message.user}: ${message.message}`);
                break;
            case 'user_joined':
                console.log('有用户加入聊天室');
                break;
            case 'user_left':
                console.log('有用户离开聊天室');
                break;
            case 'typing':
                console.log(`${message.user} 正在输入...`);
                break;
        }
    } catch (error) {
        console.error('消息解析错误:', error);
    }
});

ws.on('close', () => {
    console.log('连接已关闭');
});

ws.on('error', (error) => {
    console.error('连接错误:', error);
});
```

### TCP/UDP 网络编程

**TCP 服务器：**
```javascript
const net = require('net');

// 创建 TCP 服务器
const tcpServer = net.createServer((socket) => {
    console.log(`客户端连接: ${socket.remoteAddress}:${socket.remotePort}`);
    
    // 发送欢迎消息
    socket.write('欢迎连接到 TCP 服务器!\n');
    
    // 处理数据接收
    socket.on('data', (data) => {
        const message = data.toString().trim();
        console.log(`收到消息: ${message}`);
        
        // 回显消息
        socket.write(`服务器回复: ${message}\n`);
        
        // 特殊命令处理
        if (message.toLowerCase() === 'quit') {
            socket.write('再见!\n');
            socket.end();
        } else if (message.toLowerCase() === 'time') {
            socket.write(`当前时间: ${new Date().toISOString()}\n`);
        }
    });
    
    // 处理连接关闭
    socket.on('end', () => {
        console.log('客户端断开连接');
    });
    
    // 处理错误
    socket.on('error', (err) => {
        console.error('Socket 错误:', err);
    });
});

// 服务器错误处理
tcpServer.on('error', (err) => {
    console.error('服务器错误:', err);
});

// 启动服务器
tcpServer.listen(9000, () => {
    console.log('TCP 服务器监听端口 9000');
});
```

**TCP 客户端：**
```javascript
const net = require('net');

// 创建 TCP 客户端
const client = new net.Socket();

client.connect(9000, 'localhost', () => {
    console.log('连接到服务器');
    client.write('Hello Server!\n');
});

client.on('data', (data) => {
    console.log('服务器回复:', data.toString());
    
    // 模拟用户输入
    setTimeout(() => {
        client.write('time\n');
    }, 1000);
    
    setTimeout(() => {
        client.write('quit\n');
    }, 2000);
});

client.on('close', () => {
    console.log('连接关闭');
});

client.on('error', (err) => {
    console.error('客户端错误:', err);
});
```

**UDP 服务器：**
```javascript
const dgram = require('dgram');

// 创建 UDP 服务器
const udpServer = dgram.createSocket('udp4');

udpServer.on('message', (msg, rinfo) => {
    console.log(`收到消息: ${msg} from ${rinfo.address}:${rinfo.port}`);
    
    // 回复消息
    const reply = `服务器回复: ${msg}`;
    udpServer.send(reply, rinfo.port, rinfo.address, (err) => {
        if (err) {
            console.error('发送回复失败:', err);
        }
    });
});

udpServer.on('listening', () => {
    const address = udpServer.address();
    console.log(`UDP 服务器监听 ${address.address}:${address.port}`);
});

udpServer.on('error', (err) => {
    console.error('UDP 服务器错误:', err);
    udpServer.close();
});

// 启动服务器
udpServer.bind(9001);
```

**UDP 客户端：**
```javascript
const dgram = require('dgram');

// 创建 UDP 客户端
const client = dgram.createSocket('udp4');

const message = Buffer.from('Hello UDP Server!');
const port = 9001;
const host = 'localhost';

client.send(message, port, host, (err) => {
    if (err) {
        console.error('发送失败:', err);
    } else {
        console.log('消息已发送');
    }
});

client.on('message', (msg, rinfo) => {
    console.log(`收到回复: ${msg} from ${rinfo.address}:${rinfo.port}`);
    client.close();
});

client.on('error', (err) => {
    console.error('客户端错误:', err);
    client.close();
});
```

### 网络安全考虑

**HTTPS 服务器：**
```javascript
const https = require('https');
const fs = require('fs');

// HTTPS 配置
const options = {
    key: fs.readFileSync('private-key.pem'),
    cert: fs.readFileSync('certificate.pem'),
    // 可选：CA 证书
    ca: fs.readFileSync('ca-certificate.pem')
};

// 创建 HTTPS 服务器
const httpsServer = https.createServer(options, (req, res) => {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Hello HTTPS World!\n');
});

httpsServer.listen(443, () => {
    console.log('HTTPS 服务器运行在 https://localhost');
});
```

**安全头设置：**
```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    // 设置安全头
    res.setHeader('X-Content-Type-Options', 'nosniff');
    res.setHeader('X-Frame-Options', 'DENY');
    res.setHeader('X-XSS-Protection', '1; mode=block');
    res.setHeader('Strict-Transport-Security', 'max-age=31536000; includeSubDomains');
    res.setHeader('Content-Security-Policy', "default-src 'self'");
    
    res.writeHead(200, { 'Content-Type': 'text/html' });
    res.end(`
        <!DOCTYPE html>
        <html>
        <head>
            <title>安全示例</title>
        </head>
        <body>
            <h1>Hello Secure World!</h1>
        </body>
        </html>
    `);
});

server.listen(3000);
```

**速率限制实现：**
```javascript
const http = require('http');

// 简单的速率限制
const rateLimiter = new Map();

function isRateLimited(ip, maxRequests = 10, windowMs = 60000) {
    const now = Date.now();
    const windowStart = now - windowMs;
    
    if (!rateLimiter.has(ip)) {
        rateLimiter.set(ip, []);
    }
    
    const requests = rateLimiter.get(ip);
    
    // 清除过期请求
    const validRequests = requests.filter(time => time > windowStart);
    validRequests.push(now);
    rateLimiter.set(ip, validRequests);
    
    return validRequests.length > maxRequests;
}

const server = http.createServer((req, res) => {
    const clientIP = req.connection.remoteAddress;
    
    if (isRateLimited(clientIP)) {
        res.writeHead(429, { 'Content-Type': 'application/json' });
        res.end(JSON.stringify({ error: 'Too Many Requests' }));
        return;
    }
    
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({ message: 'Hello World!' }));
});

server.listen(3000);
```

# 十七、Node.js 生态系统

## 17.1 包管理工具

### npm 包管理器使用

**npm 基本命令：**
```bash
# 初始化项目
npm init
npm init -y  # 快速初始化，使用默认配置

# 安装包
npm install express              # 安装最新版本
npm install express@4.18.0       # 安装指定版本
npm install express@^4.18.0      # 安装兼容版本
npm install express --save       # 安装并添加到 dependencies
npm install express --save-dev   # 安装并添加到 devDependencies
npm install -g nodemon           # 全局安装

# 卸载包
npm uninstall express
npm uninstall express --save

# 更新包
npm update express
npm update                       # 更新所有包

# 查看包信息
npm list                         # 查看已安装的包
npm list --depth=0              # 只显示顶层依赖
npm outdated                     # 查看过期的包
npm info express                 # 查看包详细信息

# 搜索包
npm search express

# 运行脚本
npm run start
npm run test
npm run build
```

**npm 高级用法：**
```bash
# 安装特定版本范围
npm install express@">=4.0.0 <5.0.0"
npm install express@"~4.18.0"  # 兼容补丁版本
npm install express@"^4.18.0"  # 兼容次要版本

# 安装 peer dependencies
npm install --save-peer react@18.0.0

# 安装可选依赖
npm install --save-optional fsevents

# 生产环境安装（不安装 devDependencies）
npm install --production

# 清理缓存
npm cache clean --force

# 查看 npm 配置
npm config list
npm config get registry
npm config set registry https://registry.npmjs.org/
```

### package.json 配置文件

**完整的 package.json 示例：**
```json
{
  "name": "my-awesome-project",
  "version": "1.0.0",
  "description": "一个很棒的 Node.js 项目",
  "keywords": ["node", "express", "api"],
  "homepage": "https://github.com/user/my-awesome-project#readme",
  "bugs": {
    "url": "https://github.com/user/my-awesome-project/issues",
    "email": "support@example.com"
  },
  "license": "MIT",
  "author": {
    "name": "张三",
    "email": "zhangsan@example.com",
    "url": "https://zhangsan.com"
  },
  "contributors": [
    {
      "name": "李四",
      "email": "lisi@example.com"
    }
  ],
  "files": [
    "dist/",
    "lib/",
    "README.md"
  ],
  "main": "lib/index.js",
  "module": "es/index.js",
  "browser": "dist/bundle.js",
  "bin": {
    "my-cli": "bin/cli.js"
  },
  "directories": {
    "lib": "lib",
    "test": "test"
  },
  "repository": {
    "type": "git",
    "url": "https://github.com/user/my-awesome-project.git"
  },
  "scripts": {
    "prestart": "npm run build",
    "start": "node dist/server.js",
    "dev": "nodemon src/server.js",
    "build": "webpack --mode=production",
    "test": "jest",
    "test:watch": "jest --watch",
    "test:coverage": "jest --coverage",
    "lint": "eslint src/**/*.js",
    "lint:fix": "eslint src/**/*.js --fix",
    "prepublishOnly": "npm run build",
    "postinstall": "node scripts/postinstall.js"
  },
  "dependencies": {
    "express": "^4.18.0",
    "mongoose": "^6.0.0",
    "cors": "^2.8.5"
  },
  "devDependencies": {
    "jest": "^28.0.0",
    "webpack": "^5.0.0",
    "babel-loader": "^8.0.0",
    "eslint": "^8.0.0",
    "nodemon": "^2.0.0"
  },
  "peerDependencies": {
    "react": "^18.0.0"
  },
  "optionalDependencies": {
    "fsevents": "^2.0.0"
  },
  "engines": {
    "node": ">=14.0.0",
    "npm": ">=6.0.0"
  },
  "os": ["darwin", "linux"],
  "cpu": ["x64"],
  "private": false,
  "publishConfig": {
    "access": "public"
  },
  "config": {
    "port": "3000"
  }
}
```

**脚本生命周期钩子：**
```json
{
  "scripts": {
    "preinstall": "echo '安装前'",
    "install": "echo '安装中'",
    "postinstall": "echo '安装后'",
    "prepublish": "echo '发布前'",
    "prepare": "echo '准备阶段'",
    "prepublishOnly": "echo '仅发布前'",
    "prepack": "echo '打包前'",
    "postpack": "echo '打包后'",
    "prestart": "npm run build",
    "start": "node server.js",
    "poststart": "echo '启动后'",
    "pretest": "npm run lint",
    "test": "jest",
    "posttest": "echo '测试后'"
  }
}
```

### 依赖版本管理

**语义化版本控制 (SemVer)：**
```json
{
  "dependencies": {
    "express": "4.18.0",        // 精确版本
    "lodash": "~4.17.20",       // 兼容补丁版本 (4.17.x)
    "moment": "^2.29.0",        // 兼容次要版本 (2.x.x)
    "axios": ">=0.21.0",        // 大于等于
    "react": "16.8.0 - 17.0.0", // 版本范围
    "vue": "latest",            // 最新版本
    "jquery": "*",              // 任意版本
    "bootstrap": "4.x || 5.x"   // 或关系
  }
}
```

**版本锁定和更新策略：**
```bash
# package-lock.json 的作用
# - 锁定依赖的确切版本
# - 确保团队间的一致性
# - 提高安装速度

# 生成 package-lock.json
npm install

# 忽略 package-lock.json
npm install --no-package-lock

# 更新 package-lock.json
npm install --package-lock-only

# 审计安全漏洞
npm audit
npm audit fix
npm audit fix --force
```

**依赖类型详解：**
```json
{
  "dependencies": {
    "express": "^4.18.0"        // 生产环境必需依赖
  },
  "devDependencies": {
    "jest": "^28.0.0",          // 开发环境依赖
    "eslint": "^8.0.0"          // 代码检查工具
  },
  "peerDependencies": {
    "react": "^18.0.0"          // 对等依赖（插件使用）
  },
  "optionalDependencies": {
    "fsevents": "^2.0.0"        // 可选依赖（可失败）
  },
  "bundledDependencies": [
    "lodash"                    // 捆绑依赖（打包发布）
  ]
}
```

### 脚本命令配置

**常用脚本配置：**
```json
{
  "scripts": {
    "dev": "nodemon src/index.js",
    "start": "node dist/index.js",
    "build": "webpack --mode=production",
    "build:dev": "webpack --mode=development",
    "test": "jest --passWithNoTests",
    "test:watch": "jest --watch",
    "test:coverage": "jest --coverage",
    "lint": "eslint src/**/*.js",
    "lint:fix": "eslint src/**/*.js --fix",
    "format": "prettier --write src/**/*.js",
    "format:check": "prettier --check src/**/*.js",
    "type-check": "tsc --noEmit",
    "clean": "rimraf dist",
    "prebuild": "npm run clean",
    "postbuild": "echo '构建完成'",
    "deploy": "npm run build && gh-pages -d dist",
    "docker:build": "docker build -t myapp .",
    "docker:run": "docker run -p 3000:3000 myapp"
  }
}
```

**环境变量和配置：**
```json
{
  "scripts": {
    "start": "node index.js",
    "start:dev": "NODE_ENV=development node index.js",
    "start:prod": "NODE_ENV=production node index.js",
    "debug": "node --inspect index.js",
    "profile": "node --prof index.js",
    "analyze": "webpack-bundle-analyzer dist/stats.json"
  },
  "config": {
    "port": "3000",
    "host": "localhost"
  }
}
```

## 17.2 构建工具

### Webpack 模块打包

**webpack.config.js 基础配置：**
```javascript
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
const { CleanWebpackPlugin } = require('clean-webpack-plugin');

module.exports = (env, argv) => {
    const isProduction = argv.mode === 'production';
    
    return {
        entry: {
            main: './src/index.js',
            vendor: './src/vendor.js'
        },
        output: {
            path: path.resolve(__dirname, 'dist'),
            filename: isProduction ? '[name].[contenthash].js' : '[name].js',
            chunkFilename: isProduction ? '[name].[contenthash].chunk.js' : '[name].chunk.js',
            publicPath: '/'
        },
        module: {
            rules: [
                {
                    test: /\.js$/,
                    exclude: /node_modules/,
                    use: {
                        loader: 'babel-loader',
                        options: {
                            presets: ['@babel/preset-env']
                        }
                    }
                },
                {
                    test: /\.css$/,
                    use: [
                        isProduction ? MiniCssExtractPlugin.loader : 'style-loader',
                        'css-loader',
                        'postcss-loader'
                    ]
                },
                {
                    test: /\.scss$/,
                    use: [
                        isProduction ? MiniCssExtractPlugin.loader : 'style-loader',
                        'css-loader',
                        'sass-loader'
                    ]
                },
                {
                    test: /\.(png|jpe?g|gif|svg)$/i,
                    type: 'asset/resource',
                    generator: {
                        filename: 'images/[name].[hash][ext]'
                    }
                },
                {
                    test: /\.(woff|woff2|eot|ttf|otf)$/i,
                    type: 'asset/resource',
                    generator: {
                        filename: 'fonts/[name].[hash][ext]'
                    }
                }
            ]
        },
        plugins: [
            new CleanWebpackPlugin(),
            new HtmlWebpackPlugin({
                template: './src/index.html',
                minify: isProduction ? {
                    removeComments: true,
                    collapseWhitespace: true,
                    removeRedundantAttributes: true
                } : false
            }),
            ...(isProduction ? [
                new MiniCssExtractPlugin({
                    filename: '[name].[contenthash].css'
                })
            ] : [])
        ],
        optimization: {
            splitChunks: {
                chunks: 'all',
                cacheGroups: {
                    vendor: {
                        test: /[\\/]node_modules[\\/]/,
                        name: 'vendors',
                        chunks: 'all'
                    }
                }
            }
        },
        devServer: {
            contentBase: path.join(__dirname, 'dist'),
            compress: true,
            port: 3000,
            hot: true,
            open: true,
            historyApiFallback: true
        },
        devtool: isProduction ? 'source-map' : 'eval-source-map'
    };
};
```

**高级 Webpack 配置：**
```javascript
const webpack = require('webpack');
const BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin;

module.exports = {
    // ... 基础配置
    
    resolve: {
        extensions: ['.js', '.jsx', '.json'],
        alias: {
            '@': path.resolve(__dirname, 'src'),
            '@components': path.resolve(__dirname, 'src/components'),
            '@utils': path.resolve(__dirname, 'src/utils')
        },
        modules: [
            'node_modules',
            path.resolve(__dirname, 'src')
        ]
    },
    
    externals: {
        'lodash': '_',
        'jquery': 'jQuery'
    },
    
    performance: {
        maxAssetSize: 250000,
        maxEntrypointSize: 250000,
        hints: 'warning'
    },
    
    plugins: [
        // ... 其他插件
        
        new webpack.DefinePlugin({
            'process.env.NODE_ENV': JSON.stringify(process.env.NODE_ENV),
            'API_URL': JSON.stringify('https://api.example.com')
        }),
        
        new BundleAnalyzerPlugin({
            analyzerMode: 'static',
            openAnalyzer: false
        })
    ]
};
```

### Gulp 任务自动化

**gulpfile.js 基础配置：**
```javascript
const gulp = require('gulp');
const sass = require('gulp-sass')(require('sass'));
const uglify = require('gulp-uglify');
const concat = require('gulp-concat');
const sourcemaps = require('gulp-sourcemaps');
const rename = require('gulp-rename');
const cleanCSS = require('gulp-clean-css');
const imagemin = require('gulp-imagemin');
const del = require('del');
const browserSync = require('browser-sync').create();

// 清理任务
gulp.task('clean', () => {
    return del(['dist/**/*']);
});

// CSS 处理任务
gulp.task('styles', () => {
    return gulp.src('src/scss/**/*.scss')
        .pipe(sourcemaps.init())
        .pipe(sass().on('error', sass.logError))
        .pipe(cleanCSS())
        .pipe(rename({ suffix: '.min' }))
        .pipe(sourcemaps.write('.'))
        .pipe(gulp.dest('dist/css'))
        .pipe(browserSync.stream());
});

// JavaScript 处理任务
gulp.task('scripts', () => {
    return gulp.src('src/js/**/*.js')
        .pipe(sourcemaps.init())
        .pipe(concat('main.js'))
        .pipe(uglify())
        .pipe(rename({ suffix: '.min' }))
        .pipe(sourcemaps.write('.'))
        .pipe(gulp.dest('dist/js'))
        .pipe(browserSync.stream());
});

// 图片优化任务
gulp.task('images', () => {
    return gulp.src('src/images/**/*')
        .pipe(imagemin([
            imagemin.gifsicle({ interlaced: true }),
            imagemin.mozjpeg({ quality: 75, progressive: true }),
            imagemin.optipng({ optimizationLevel: 5 }),
            imagemin.svgo({
                plugins: [
                    { removeViewBox: true },
                    { cleanupIDs: false }
                ]
            })
        ]))
        .pipe(gulp.dest('dist/images'));
});

// HTML 复制任务
gulp.task('html', () => {
    return gulp.src('src/**/*.html')
        .pipe(gulp.dest('dist'))
        .pipe(browserSync.stream());
});

// 文件监听任务
gulp.task('watch', () => {
    gulp.watch('src/scss/**/*.scss', gulp.series('styles'));
    gulp.watch('src/js/**/*.js', gulp.series('scripts'));
    gulp.watch('src/**/*.html', gulp.series('html'));
    gulp.watch('src/images/**/*', gulp.series('images'));
});

// 浏览器同步
gulp.task('serve', () => {
    browserSync.init({
        server: {
            baseDir: './dist'
        },
        port: 3000,
        open: true
    });
});

// 构建任务
gulp.task('build', gulp.series(
    'clean',
    gulp.parallel('styles', 'scripts', 'images', 'html')
));

// 开发任务
gulp.task('dev', gulp.series(
    'build',
    gulp.parallel('serve', 'watch')
));

// 默认任务
gulp.task('default', gulp.series('build'));
```

**高级 Gulp 任务：**
```javascript
const gulp = require('gulp');
const babel = require('gulp-babel');
const eslint = require('gulp-eslint');
const jest = require('gulp-jest').default;
const zip = require('gulp-zip');
const ftp = require('vinyl-ftp');

// 代码检查任务
gulp.task('lint', () => {
    return gulp.src(['src/js/**/*.js'])
        .pipe(eslint())
        .pipe(eslint.format())
        .pipe(eslint.failAfterError());
});

// 测试任务
gulp.task('test', () => {
    return gulp.src('test/').pipe(jest({
        "preprocessorIgnorePatterns": [
            "<rootDir>/dist/", "<rootDir>/node_modules/"
        ],
        "automock": false
    }));
});

// Babel 转换任务
gulp.task('babel', () => {
    return gulp.src('src/js/**/*.js')
        .pipe(babel({
            presets: ['@babel/env']
        }))
        .pipe(gulp.dest('dist/js'));
});

// 打包任务
gulp.task('package', () => {
    return gulp.src('dist/**/*')
        .pipe(zip('project.zip'))
        .pipe(gulp.dest('packages'));
});

// 部署任务
gulp.task('deploy', () => {
    const conn = ftp.create({
        host: 'mywebsite.com',
        user: process.env.FTP_USER,
        password: process.env.FTP_PASSWORD,
        parallel: 10
    });
    
    return gulp.src('dist/**/*', { base: 'dist', buffer: false })
        .pipe(conn.dest('/public_html'));
});

// 复合任务
gulp.task('ci', gulp.series(
    'lint',
    'test',
    'build',
    'package'
));
```

### Babel 代码转换

**babel.config.js 配置：**
```javascript
module.exports = {
    presets: [
        [
            '@babel/preset-env',
            {
                targets: {
                    browsers: ['> 1%', 'last 2 versions', 'not ie <= 8']
                },
                useBuiltIns: 'usage',
                corejs: 3
            }
        ],
        '@babel/preset-react'
    ],
    plugins: [
        '@babel/plugin-proposal-class-properties',
        '@babel/plugin-proposal-object-rest-spread',
        [
            '@babel/plugin-transform-runtime',
            {
                corejs: 3,
                helpers: true,
                regenerator: true
            }
        ]
    ],
    env: {
        development: {
            plugins: ['@babel/plugin-transform-runtime']
        },
        production: {
            plugins: [
                '@babel/plugin-transform-runtime',
                'babel-plugin-transform-remove-console'
            ]
        }
    }
};
```

**按需加载配置：**
```javascript
// babel.config.js
module.exports = {
    presets: [
        [
            '@babel/preset-env',
            {
                modules: false, // 保持 ES6 模块语法
                useBuiltIns: 'usage',
                corejs: 3,
                targets: {
                    browsers: ['> 1%', 'last 2 versions']
                }
            }
        ]
    ],
    plugins: [
        [
            '@babel/plugin-transform-runtime',
            {
                corejs: 3,
                helpers: true,
                regenerator: true,
                useESModules: true
            }
        ],
        // 装饰器支持
        ['@babel/plugin-proposal-decorators', { legacy: true }],
        ['@babel/plugin-proposal-class-properties', { loose: true }]
    ]
};
```

### ESLint 代码检查

**.eslintrc.js 配置：**
```javascript
module.exports = {
    env: {
        browser: true,
        es2021: true,
        node: true,
        jest: true
    },
    extends: [
        'eslint:recommended',
        '@typescript-eslint/recommended',
        'plugin:react/recommended',
        'plugin:import/errors',
        'plugin:import/warnings'
    ],
    parser: '@typescript-eslint/parser',
    parserOptions: {
        ecmaFeatures: {
            jsx: true
        },
        ecmaVersion: 12,
        sourceType: 'module'
    },
    plugins: [
        'react',
        '@typescript-eslint',
        'import'
    ],
    settings: {
        react: {
            version: 'detect'
        },
        'import/resolver': {
            node: {
                paths: ['src'],
                extensions: ['.js', '.jsx', '.ts', '.tsx']
            }
        }
    },
    rules: {
        'indent': ['error', 2],
        'linebreak-style': ['error', 'unix'],
        'quotes': ['error', 'single'],
        'semi': ['error', 'always'],
        'no-unused-vars': 'warn',
        'no-console': 'warn',
        'react/prop-types': 'off',
        'import/order': [
            'error',
            {
                'groups': ['builtin', 'external', 'internal'],
                'pathGroups': [
                    {
                        'pattern': 'react',
                        'group': 'external',
                        'position': 'before'
                    }
                ],
                'pathGroupsExcludedImportTypes': ['react'],
                'alphabetize': {
                    'order': 'asc',
                    'caseInsensitive': true
                }
            }
        ]
    },
    overrides: [
        {
            files: ['*.test.js', '*.spec.js'],
            env: {
                jest: true
            }
        }
    ]
};
```

**高级 ESLint 配置：**
```javascript
// .eslintrc.js
module.exports = {
    // ... 基础配置
    
    rules: {
        // 代码质量规则
        'no-console': ['warn', { allow: ['warn', 'error'] }],
        'no-debugger': 'error',
        'no-alert': 'warn',
        'no-var': 'error',
        'prefer-const': 'error',
        'no-duplicate-imports': 'error',
        
        // 风格规则
        'comma-dangle': ['error', 'always-multiline'],
        'object-curly-spacing': ['error', 'always'],
        'array-bracket-spacing': ['error', 'never'],
        'space-before-function-paren': ['error', {
            'asyncArrow': 'always',
            'anonymous': 'never',
            'named': 'never'
        }],
        
        // 复杂度控制
        'complexity': ['warn', 10],
        'max-depth': ['warn', 4],
        'max-lines': ['warn', 300],
        'max-params': ['warn', 3],
        
        // 导入规则
        'import/no-unresolved': 'error',
        'import/named': 'error',
        'import/default': 'error',
        'import/no-self-import': 'error',
        'import/no-cycle': 'error'
    },
    
    // 自定义规则
    plugins: [
        // ... 其他插件
        'sonarjs'  // 代码质量分析
    ],
    
    extends: [
        // ... 其他扩展
        'plugin:sonarjs/recommended'
    ]
};
```

## 17.3 测试框架

### Jest 测试框架

**Jest 基础配置：**
```javascript
// jest.config.js
module.exports = {
    testEnvironment: 'node',
    testMatch: [
        '**/__tests__/**/*.{js,jsx,ts,tsx}',
        '**/?(*.)+(spec|test).{js,jsx,ts,tsx}'
    ],
    testPathIgnorePatterns: [
        '/node_modules/',
        '/dist/'
    ],
    collectCoverageFrom: [
        'src/**/*.{js,jsx,ts,tsx}',
        '!src/**/*.d.ts'
    ],
    coverageDirectory: 'coverage',
    coverageReporters: ['text', 'lcov', 'html'],
    setupFilesAfterEnv: ['<rootDir>/test/setup.js'],
    moduleNameMapper: {
        '^@/(.*)$': '<rootDir>/src/$1',
        '\\.(css|less|scss|sass)$': 'identity-obj-proxy'
    },
    transform: {
        '^.+\\.(js|jsx|ts|tsx)$': 'babel-jest'
    },
    watchPlugins: [
        'jest-watch-typeahead/filename',
        'jest-watch-typeahead/testname'
    ]
};
```

**基础测试示例：**
```javascript
// math.js
function add(a, b) {
    return a + b;
}

function subtract(a, b) {
    return a - b;
}

function divide(a, b) {
    if (b === 0) {
        throw new Error('Division by zero');
    }
    return a / b;
}

module.exports = { add, subtract, divide };

// math.test.js
const { add, subtract, divide } = require('./math');

describe('数学运算测试', () => {
    describe('加法运算', () => {
        test('应该正确计算两个正数的和', () => {
            expect(add(2, 3)).toBe(5);
        });

        test('应该正确计算负数和正数的和', () => {
            expect(add(-1, 1)).toBe(0);
        });

        test('应该正确计算小数的和', () => {
            expect(add(0.1, 0.2)).toBeCloseTo(0.3);
        });
    });

    describe('减法运算', () => {
        test('应该正确计算两个数的差', () => {
            expect(subtract(5, 3)).toBe(2);
        });

        test('应该正确处理负数', () => {
            expect(subtract(-1, -2)).toBe(1);
        });
    });

    describe('除法运算', () => {
        test('应该正确计算两个数的商', () => {
            expect(divide(10, 2)).toBe(5);
        });

        test('应该在除零时抛出错误', () => {
            expect(() => divide(10, 0)).toThrow('Division by zero');
        });

        test('应该正确处理小数除法', () => {
            expect(divide(1, 3)).toBeCloseTo(0.333333, 5);
        });
    });
});
```

**异步测试：**
```javascript
// api.js
const fetch = require('node-fetch');

async function fetchUser(id) {
    const response = await fetch(`https://jsonplaceholder.typicode.com/users/${id}`);
    if (!response.ok) {
        throw new Error('User not found');
    }
    return response.json();
}

function fetchUserWithCallback(id, callback) {
    fetch(`https://jsonplaceholder.typicode.com/users/${id}`)
        .then(response => {
            if (!response.ok) {
                throw new Error('User not found');
            }
            return response.json();
        })
        .then(data => callback(null, data))
        .catch(error => callback(error));
}

module.exports = { fetchUser, fetchUserWithCallback };

// api.test.js
const { fetchUser, fetchUserWithCallback } = require('./api');

// Mock fetch
global.fetch = jest.fn();

describe('API 测试', () => {
    beforeEach(() => {
        fetch.mockClear();
    });

    test('应该成功获取用户数据', async () => {
        const mockUser = { id: 1, name: 'John Doe' };
        
        fetch.mockResolvedValue({
            ok: true,
            json: () => Promise.resolve(mockUser)
        });

        const user = await fetchUser(1);
        expect(user).toEqual(mockUser);
        expect(fetch).toHaveBeenCalledWith('https://jsonplaceholder.typicode.com/users/1');
    });

    test('应该在用户不存在时抛出错误', async () => {
        fetch.mockResolvedValue({
            ok: false
        });

        await expect(fetchUser(999)).rejects.toThrow('User not found');
    });

    test('应该支持回调函数方式', (done) => {
        const mockUser = { id: 1, name: 'John Doe' };
        
        fetch.mockResolvedValue({
            ok: true,
            json: () => Promise.resolve(mockUser)
        });

        fetchUserWithCallback(1, (error, user) => {
            expect(error).toBeNull();
            expect(user).toEqual(mockUser);
            done();
        });
    });
});
```

### Mocha 测试运行器

**Mocha 基础配置：**
```javascript
// .mocharc.js
module.exports = {
    require: [
        '@babel/register',
        'chai/register-expect'
    ],
    reporter: 'spec',
    timeout: 5000,
    recursive: true,
    extension: ['js'],
    file: ['./test/setup.js'],
    watchFiles: ['src/**/*.js', 'test/**/*.js']
};
```

**Mocha 测试示例：**
```javascript
// 使用 Chai 断言库
const { expect } = require('chai');
const sinon = require('sinon');
const { add, subtract } = require('../src/math');

describe('数学运算测试', function() {
    describe('加法运算', function() {
        it('应该正确计算两个正数的和', function() {
            const result = add(2, 3);
            expect(result).to.equal(5);
        });

        it('应该正确计算负数和正数的和', function() {
            const result = add(-1, 1);
            expect(result).to.equal(0);
        });

        it('应该正确计算小数的和', function() {
            const result = add(0.1, 0.2);
            expect(result).to.be.closeTo(0.3, 0.001);
        });
    });

    describe('减法运算', function() {
        it('应该正确计算两个数的差', function() {
            const result = subtract(5, 3);
            expect(result).to.equal(2);
        });
    });

    // 异步测试
    describe('异步操作', function() {
        it('应该处理 Promise', function() {
            return Promise.resolve(42)
                .then(value => {
                    expect(value).to.equal(42);
                });
        });

        it('应该处理 async/await', async function() {
            const result = await Promise.resolve('hello');
            expect(result).to.equal('hello');
        });

        it('应该处理回调函数', function(done) {
            setTimeout(() => {
                expect(true).to.be.true;
                done();
            }, 100);
        });
    });

    // 钩子函数
    before(function() {
        console.log('所有测试开始前执行');
    });

    after(function() {
        console.log('所有测试结束后执行');
    });

    beforeEach(function() {
        console.log('每个测试开始前执行');
    });

    afterEach(function() {
        console.log('每个测试结束后执行');
    });
});
```

### Chai 断言库

**Chai 断言风格：**
```javascript
const { expect, should, assert } = require('chai');

// Expect 风格 (推荐)
describe('Chai Expect 风格', function() {
    it('基本断言', function() {
        const value = 42;
        expect(value).to.equal(42);
        expect(value).to.be.a('number');
        expect(value).to.be.above(40);
        expect(value).to.be.below(50);
    });

    it('对象断言', function() {
        const obj = { name: 'John', age: 30 };
        expect(obj).to.have.property('name');
        expect(obj).to.have.property('name', 'John');
        expect(obj).to.include({ name: 'John' });
        expect(obj).to.deep.equal({ name: 'John', age: 30 });
    });

    it('数组断言', function() {
        const arr = [1, 2, 3];
        expect(arr).to.be.an('array');
        expect(arr).to.include(2);
        expect(arr).to.have.lengthOf(3);
        expect(arr).to.deep.equal([1, 2, 3]);
    });

    it('字符串断言', function() {
        const str = 'Hello World';
        expect(str).to.be.a('string');
        expect(str).to.contain('World');
        expect(str).to.match(/Hello/);
        expect(str).to.have.lengthOf(11);
    });

    it('函数断言', function() {
        const fn = () => { throw new Error('Oops!'); };
        expect(fn).to.throw();
        expect(fn).to.throw(Error);
        expect(fn).to.throw('Oops!');
    });
});

// Should 风格
describe('Chai Should 风格', function() {
    it('基本断言', function() {
        should();
        const value = 42;
        value.should.equal(42);
        value.should.be.a('number');
        value.should.be.above(40);
    });
});

// Assert 风格
describe('Chai Assert 风格', function() {
    it('基本断言', function() {
        const value = 42;
        assert.equal(value, 42);
        assert.typeOf(value, 'number');
        assert.isAbove(value, 40);
        assert.isBelow(value, 50);
    });
});
```

**Chai 插件使用：**
```javascript
const chai = require('chai');
const chaiAsPromised = require('chai-as-promised');
const chaiHttp = require('chai-http');
const sinonChai = require('sinon-chai');

// 注册插件
chai.use(chaiAsPromised);
chai.use(chaiHttp);
chai.use(sinonChai);

const { expect } = chai;

describe('Chai 插件测试', function() {
    // Promise 断言
    it('应该处理 Promise 断言', async function() {
        const promise = Promise.resolve('success');
        await expect(promise).to.eventually.equal('success');
        
        const rejectedPromise = Promise.reject(new Error('failure'));
        await expect(rejectedPromise).to.be.rejectedWith('failure');
    });

    // HTTP 断言
    it('应该处理 HTTP 请求', function() {
        // 注意：这需要真实的服务器
        // return chai.request(app)
        //     .get('/api/users')
        //     .then(res => {
        //         expect(res).to.have.status(200);
        //         expect(res).to.be.json;
        //     });
    });
});
```

### 测试覆盖率工具

**Istanbul/nyc 配置：**
```json
// package.json
{
  "scripts": {
    "test": "jest",
    "test:coverage": "jest --coverage",
    "test:coverage:html": "jest --coverage --coverageReporters=html",
    "test:watch": "jest --watch"
  },
  "nyc": {
    "extends": "@istanbuljs/nyc-config-babel",
    "all": true,
    "include": [
      "src/**/*.js"
    ],
    "exclude": [
      "src/**/*.test.js",
      "src/**/index.js"
    ],
    "reporter": [
      "text",
      "html",
      "lcov"
    ],
    "report-dir": "./coverage"
  }
}
```

**覆盖率报告分析：**
```javascript
// calculator.js
class Calculator {
    add(a, b) {
        if (typeof a !== 'number' || typeof b !== 'number') {
            throw new Error('参数必须是数字');
        }
        return a + b;
    }

    subtract(a, b) {
        return a - b;
    }

    multiply(a, b) {
        return a * b;
    }

    divide(a, b) {
        if (b === 0) {
            throw new Error('除数不能为零');
        }
        return a / b;
    }

    // 这个方法没有被测试覆盖
    power(base, exponent) {
        return Math.pow(base, exponent);
    }
}

module.exports = Calculator;

// calculator.test.js
const { expect } = require('chai');
const Calculator = require('./calculator');

describe('Calculator', function() {
    let calculator;

    beforeEach(function() {
        calculator = new Calculator();
    });

    describe('add', function() {
        it('应该正确计算两个数字的和', function() {
            expect(calculator.add(2, 3)).to.equal(5);
        });

        it('应该在参数不是数字时抛出错误', function() {
            expect(() => calculator.add('2', 3)).to.throw('参数必须是数字');
            expect(() => calculator.add(2, '3')).to.throw('参数必须是数字');
        });
    });

    describe('subtract', function() {
        it('应该正确计算两个数字的差', function() {
            expect(calculator.subtract(5, 3)).to.equal(2);
        });
    });

    describe('multiply', function() {
        it('应该正确计算两个数字的积', function() {
            expect(calculator.multiply(3, 4)).to.equal(12);
        });
    });

    describe('divide', function() {
        it('应该正确计算两个数字的商', function() {
            expect(calculator.divide(10, 2)).to.equal(5);
        });

        it('应该在除数为零时抛出错误', function() {
            expect(() => calculator.divide(10, 0)).to.throw('除数不能为零');
        });
    });

    // 注意：power 方法没有被测试，这会在覆盖率报告中显示
});
```

**CI/CD 集成：**
```yaml
# .github/workflows/test.yml
name: Test

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    
    strategy:
      matrix:
        node-version: [14.x, 16.x, 18.x]
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v3
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'
    
    - name: Install dependencies
      run: npm ci
    
    - name: Run lint
      run: npm run lint
    
    - name: Run tests
      run: npm run test:coverage
    
    - name: Upload coverage to Codecov
      uses: codecov/codecov-action@v3
      with:
        file: ./coverage/lcov.info
        flags: unittests
        name: codecov-umbrella
```
# 十八、Node.js 应用开发

## 18.1 Web 框架

### Express.js 框架特性

**Express.js 基础应用：**
```javascript
const express = require('express');
const path = require('path');
const cors = require('cors');
const helmet = require('helmet');
const compression = require('compression');
const rateLimit = require('express-rate-limit');

const app = express();

// 中间件配置
app.use(helmet()); // 安全头
app.use(compression()); // 压缩响应
app.use(cors()); // 跨域支持
app.use(express.json({ limit: '10mb' })); // JSON 解析
app.use(express.urlencoded({ extended: true })); // URL 编码解析

// 静态文件服务
app.use(express.static(path.join(__dirname, 'public')));

// 速率限制
const limiter = rateLimit({
    windowMs: 15 * 60 * 1000, // 15分钟
    max: 100, // 限制每个IP 100个请求
    message: '请求过于频繁，请稍后再试'
});
app.use('/api/', limiter);

// 路由定义
app.get('/', (req, res) => {
    res.json({ message: '欢迎使用 Express.js' });
});

// API 路由
app.get('/api/users', async (req, res) => {
    try {
        const page = parseInt(req.query.page) || 1;
        const limit = parseInt(req.query.limit) || 10;
        
        // 模拟数据获取
        const users = await getUsers(page, limit);
        
        res.json({
            data: users,
            pagination: {
                page,
                limit,
                total: 100
            }
        });
    } catch (error) {
        res.status(500).json({ error: error.message });
    }
});

app.post('/api/users', async (req, res) => {
    try {
        const { name, email } = req.body;
        
        // 数据验证
        if (!name || !email) {
            return res.status(400).json({ 
                error: '姓名和邮箱是必填项' 
            });
        }
        
        // 创建用户
        const user = await createUser({ name, email });
        res.status(201).json(user);
    } catch (error) {
        res.status(500).json({ error: error.message });
    }
});

// 错误处理中间件
app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).json({ error: '服务器内部错误' });
});

// 404 处理
app.use((req, res) => {
    res.status(404).json({ error: '页面未找到' });
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
    console.log(`服务器运行在端口 ${PORT}`);
});
```

**Express.js 高级特性：**
```javascript
const express = require('express');
const session = require('express-session');
const RedisStore = require('connect-redis')(session);
const redis = require('redis');
const multer = require('multer');
const sharp = require('sharp');

const app = express();

// Redis 客户端
const redisClient = redis.createClient({
    host: 'localhost',
    port: 6379
});

// Session 配置
app.use(session({
    store: new RedisStore({ client: redisClient }),
    secret: 'your-secret-key',
    resave: false,
    saveUninitialized: false,
    cookie: {
        secure: process.env.NODE_ENV === 'production',
        maxAge: 24 * 60 * 60 * 1000 // 24小时
    }
}));

// 文件上传配置
const storage = multer.diskStorage({
    destination: (req, file, cb) => {
        cb(null, 'uploads/');
    },
    filename: (req, file, cb) => {
        const uniqueSuffix = Date.now() + '-' + Math.round(Math.random() * 1E9);
        cb(null, file.fieldname + '-' + uniqueSuffix + path.extname(file.originalname));
    }
});

const upload = multer({ 
    storage: storage,
    limits: {
        fileSize: 5 * 1024 * 1024 // 5MB
    },
    fileFilter: (req, file, cb) => {
        if (file.mimetype.startsWith('image/')) {
            cb(null, true);
        } else {
            cb(new Error('只允许上传图片文件'));
        }
    }
});

// 文件上传路由
app.post('/api/upload', upload.single('avatar'), async (req, res) => {
    try {
        if (!req.file) {
            return res.status(400).json({ error: '请选择文件' });
        }

        // 图片处理
        const outputPath = `processed/${req.file.filename}`;
        await sharp(req.file.path)
            .resize(300, 300)
            .jpeg({ quality: 80 })
            .toFile(outputPath);

        res.json({
            message: '文件上传成功',
            file: {
                originalName: req.file.originalname,
                fileName: req.file.filename,
                path: outputPath,
                size: req.file.size
            }
        });
    } catch (error) {
        res.status(500).json({ error: error.message });
    }
});

// 路由模块化
const userRouter = express.Router();

userRouter.get('/', async (req, res) => {
    // 获取用户列表
});

userRouter.get('/:id', async (req, res) => {
    const { id } = req.params;
    // 获取单个用户
});

userRouter.put('/:id', async (req, res) => {
    const { id } = req.params;
    // 更新用户
});

userRouter.delete('/:id', async (req, res) => {
    const { id } = req.params;
    // 删除用户
});

app.use('/api/users', userRouter);

// 自定义中间件
const authMiddleware = (req, res, next) => {
    const token = req.headers.authorization;
    
    if (!token) {
        return res.status(401).json({ error: '未提供认证令牌' });
    }
    
    try {
        // 验证令牌
        const user = verifyToken(token);
        req.user = user;
        next();
    } catch (error) {
        res.status(401).json({ error: '无效的认证令牌' });
    }
};

app.use('/api/protected', authMiddleware);
```

### Koa.js 中间件机制

**Koa.js 基础应用：**
```javascript
const Koa = require('koa');
const Router = require('@koa/router');
const bodyParser = require('koa-bodyparser');
const cors = require('@koa/cors');
const helmet = require('koa-helmet');
const logger = require('koa-logger');
const serve = require('koa-static');
const path = require('path');

const app = new Koa();
const router = new Router();

// 中间件注册顺序很重要
app.use(logger()); // 日志
app.use(helmet()); // 安全头
app.use(cors()); // 跨域
app.use(bodyParser()); // 请求体解析
app.use(serve(path.join(__dirname, 'public'))); // 静态文件

// 错误处理中间件
app.use(async (ctx, next) => {
    try {
        await next();
    } catch (err) {
        ctx.status = err.status || 500;
        ctx.body = { error: err.message };
        ctx.app.emit('error', err, ctx);
    }
});

// 自定义中间件
const timingMiddleware = async (ctx, next) => {
    const start = Date.now();
    await next();
    const ms = Date.now() - start;
    ctx.set('X-Response-Time', `${ms}ms`);
};

app.use(timingMiddleware);

// 条件中间件
const conditionalMiddleware = (condition) => {
    return async (ctx, next) => {
        if (condition(ctx)) {
            // 执行特定逻辑
            console.log('条件满足，执行特定逻辑');
        }
        await next();
    };
};

app.use(conditionalMiddleware((ctx) => {
    return ctx.path.startsWith('/api');
}));

// 路由定义
router.get('/', async (ctx) => {
    ctx.body = { message: '欢迎使用 Koa.js' };
});

router.get('/api/users', async (ctx) => {
    try {
        const page = parseInt(ctx.query.page) || 1;
        const limit = parseInt(ctx.query.limit) || 10;
        
        const users = await getUsers(page, limit);
        
        ctx.body = {
            data: users,
            pagination: {
                page,
                limit,
                total: 100
            }
        };
    } catch (error) {
        ctx.throw(500, error.message);
    }
});

router.post('/api/users', async (ctx) => {
    try {
        const { name, email } = ctx.request.body;
        
        if (!name || !email) {
            ctx.throw(400, '姓名和邮箱是必填项');
        }
        
        const user = await createUser({ name, email });
        ctx.status = 201;
        ctx.body = user;
    } catch (error) {
        ctx.throw(500, error.message);
    }
});

// 路由参数验证中间件
const validateUserId = async (ctx, next) => {
    const { id } = ctx.params;
    if (!id || isNaN(id)) {
        ctx.throw(400, '无效的用户ID');
    }
    await next();
};

router.get('/api/users/:id', validateUserId, async (ctx) => {
    const { id } = ctx.params;
    const user = await getUserById(id);
    if (!user) {
        ctx.throw(404, '用户未找到');
    }
    ctx.body = user;
});

app.use(router.routes());
app.use(router.allowedMethods());

// 全局错误处理
app.on('error', (err, ctx) => {
    console.error('服务器错误:', err, ctx);
});

app.listen(3000, () => {
    console.log('Koa.js 服务器运行在端口 3000');
});
```

**Koa.js 高级中间件：**
```javascript
const Koa = require('koa');
const compose = require('koa-compose');

// 异步中间件
const asyncMiddleware = async (ctx, next) => {
    console.log('中间件开始');
    
    // 异步操作
    await new Promise(resolve => setTimeout(resolve, 1000));
    
    ctx.state.middlewareData = '来自中间件的数据';
    
    await next();
    
    console.log('中间件结束');
};

// 流控制中间件
const rateLimitMiddleware = (maxRequests = 100, windowMs = 60000) => {
    const requestCounts = new Map();
    
    return async (ctx, next) => {
        const ip = ctx.ip;
        const now = Date.now();
        const windowStart = now - windowMs;
        
        if (!requestCounts.has(ip)) {
            requestCounts.set(ip, []);
        }
        
        const requests = requestCounts.get(ip);
        const validRequests = requests.filter(time => time > windowStart);
        validRequests.push(now);
        requestCounts.set(ip, validRequests);
        
        if (validRequests.length > maxRequests) {
            ctx.status = 429;
            ctx.body = { error: '请求过于频繁' };
            return;
        }
        
        await next();
    };
};

// 缓存中间件
const cacheMiddleware = (duration = 300000) => { // 5分钟
    const cache = new Map();
    
    return async (ctx, next) => {
        const key = ctx.url;
        const cached = cache.get(key);
        
        if (cached && Date.now() - cached.timestamp < duration) {
            ctx.body = cached.data;
            ctx.status = 200;
            return;
        }
        
        await next();
        
        if (ctx.status === 200) {
            cache.set(key, {
                data: ctx.body,
                timestamp: Date.now()
            });
        }
    };
};

// 响应时间中间件
const responseTimeMiddleware = async (ctx, next) => {
    const start = Date.now();
    await next();
    const ms = Date.now() - start;
    ctx.set('X-Response-Time', `${ms}ms`);
};

// 中间件组合
const middlewareStack = compose([
    responseTimeMiddleware,
    rateLimitMiddleware(),
    asyncMiddleware,
    cacheMiddleware()
]);

const app = new Koa();
app.use(middlewareStack);

// 条件中间件组合
const conditionalCompose = (condition, middleware) => {
    return async (ctx, next) => {
        if (condition(ctx)) {
            await middleware(ctx, next);
        } else {
            await next();
        }
    };
};

app.use(conditionalCompose(
    ctx => ctx.path.startsWith('/api'),
    compose([rateLimitMiddleware(), cacheMiddleware()])
));
```

### Fastify 性能优化

**Fastify 基础应用：**
```javascript
const fastify = require('fastify')({
    logger: true,
    ajv: {
        customOptions: {
            strict: 'log',
            keywords: ['kind', 'modifier']
        }
    }
});

// 插件注册
fastify.register(require('@fastify/cors'));
fastify.register(require('@fastify/helmet'));
fastify.register(require('@fastify/compress'));
fastify.register(require('@fastify/rate-limit'));
fastify.register(require('@fastify/static'), {
    root: path.join(__dirname, 'public'),
    prefix: '/public/'
});

// Schema 验证
const userSchema = {
    body: {
        type: 'object',
        required: ['name', 'email'],
        properties: {
            name: { type: 'string' },
            email: { type: 'string', format: 'email' }
        }
    },
    response: {
        201: {
            type: 'object',
            properties: {
                id: { type: 'number' },
                name: { type: 'string' },
                email: { type: 'string' }
            }
        }
    }
};

// 路由定义
fastify.get('/', async (request, reply) => {
    return { message: '欢迎使用 Fastify' };
});

fastify.get('/api/users', {
    schema: {
        querystring: {
            type: 'object',
            properties: {
                page: { type: 'integer', minimum: 1, default: 1 },
                limit: { type: 'integer', minimum: 1, maximum: 100, default: 10 }
            }
        },
        response: {
            200: {
                type: 'object',
                properties: {
                    data: {
                        type: 'array',
                        items: {
                            type: 'object',
                            properties: {
                                id: { type: 'number' },
                                name: { type: 'string' },
                                email: { type: 'string' }
                            }
                        }
                    },
                    pagination: {
                        type: 'object',
                        properties: {
                            page: { type: 'number' },
                            limit: { type: 'number' },
                            total: { type: 'number' }
                        }
                    }
                }
            }
        }
    }
}, async (request, reply) => {
    const { page, limit } = request.query;
    const users = await getUsers(page, limit);
    
    return {
        data: users,
        pagination: {
            page,
            limit,
            total: 100
        }
    };
});

fastify.post('/api/users', { schema: userSchema }, async (request, reply) => {
    const { name, email } = request.body;
    const user = await createUser({ name, email });
    
    reply.code(201);
    return user;
});

// 错误处理
fastify.setErrorHandler((error, request, reply) => {
    fastify.log.error(error);
    
    if (error.validation) {
        reply.status(400).send({
            error: '验证错误',
            details: error.validation
        });
        return;
    }
    
    reply.status(500).send({
        error: '服务器内部错误'
    });
});

// 启动服务器
const start = async () => {
    try {
        await fastify.listen({ port: 3000, host: '0.0.0.0' });
        fastify.log.info(`服务器运行在端口 3000`);
    } catch (err) {
        fastify.log.error(err);
        process.exit(1);
    }
};

start();
```

**Fastify 高级特性：**
```javascript
const fastify = require('fastify')({ logger: true });

// 自定义插件
fastify.register(async (instance, opts) => {
    instance.decorate('db', {
        async query(sql, params) {
            // 数据库查询逻辑
            return { rows: [] };
        }
    });
    
    instance.decorateRequest('user', null);
    
    instance.addHook('onRequest', async (request, reply) => {
        // 请求前处理
        request.startTime = Date.now();
    });
    
    instance.addHook('onResponse', async (request, reply) => {
        // 响应后处理
        const duration = Date.now() - request.startTime;
        instance.log.info(`${request.method} ${request.url} - ${duration}ms`);
    });
});

// 装饰器和钩子
fastify.decorate('utils', {
    async hashPassword(password) {
        // 密码哈希逻辑
        return 'hashed_password';
    },
    
    async verifyToken(token) {
        // 令牌验证逻辑
        return { userId: 1, username: 'user' };
    }
});

// 认证插件
fastify.register(async (instance, opts) => {
    instance.decorateRequest('authenticate', async function() {
        const token = this.headers.authorization?.replace('Bearer ', '');
        if (!token) {
            throw new Error('未提供认证令牌');
        }
        
        try {
            const user = await instance.utils.verifyToken(token);
            this.user = user;
        } catch (error) {
            throw new Error('无效的认证令牌');
        }
    });
    
    // 认证钩子
    instance.addHook('preHandler', async (request, reply) => {
        if (request.routeConfig?.authRequired) {
            await request.authenticate();
        }
    });
});

// 需要认证的路由
fastify.get('/api/profile', {
    config: { authRequired: true }
}, async (request, reply) => {
    return { user: request.user };
});

// 缓存插件
fastify.register(async (instance, opts) => {
    const cache = new Map();
    
    instance.decorateReply('cache', function(duration = 300000) {
        this.header('Cache-Control', `public, max-age=${duration / 1000}`);
        return this;
    });
});

// 带缓存的路由
fastify.get('/api/public-data', async (request, reply) => {
    reply.cache(300000); // 缓存5分钟
    return { data: 'public information' };
});

// 监控和指标
fastify.get('/metrics', async (request, reply) => {
    return {
        uptime: process.uptime(),
        memory: process.memoryUsage(),
        cpu: process.cpuUsage()
    };
});
```

### NestJS 企业级框架

**NestJS 基础应用：**
```typescript
// main.ts
import { NestFactory } from '@nestjs/core';
import { ValidationPipe } from '@nestjs/common';
import { AppModule } from './app.module';

async function bootstrap() {
    const app = await NestFactory.create(AppModule);
    
    // 全局管道
    app.useGlobalPipes(new ValidationPipe({
        whitelist: true,
        forbidNonWhitelisted: true,
        transform: true
    }));
    
    // CORS
    app.enableCors();
    
    await app.listen(3000);
}
bootstrap();

// app.module.ts
import { Module } from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';
import { UserModule } from './user/user.module';
import { AuthModule } from './auth/auth.module';

@Module({
    imports: [
        TypeOrmModule.forRoot({
            type: 'postgres',
            host: 'localhost',
            port: 5432,
            username: 'postgres',
            password: 'password',
            database: 'myapp',
            autoLoadEntities: true,
            synchronize: true,
        }),
        UserModule,
        AuthModule,
    ],
})
export class AppModule {}

// user.entity.ts
import { Entity, PrimaryGeneratedColumn, Column } from 'typeorm';

@Entity()
export class User {
    @PrimaryGeneratedColumn()
    id: number;

    @Column()
    name: string;

    @Column({ unique: true })
    email: string;

    @Column({ select: false }) // 不在查询中返回
    password: string;

    @Column({ default: () => 'CURRENT_TIMESTAMP' })
    createdAt: Date;
}

// user.dto.ts
import { IsEmail, IsNotEmpty, MinLength } from 'class-validator';

export class CreateUserDto {
    @IsNotEmpty()
    name: string;

    @IsEmail()
    email: string;

    @IsNotEmpty()
    @MinLength(6)
    password: string;
}

// user.service.ts
import { Injectable } from '@nestjs/common';
import { InjectRepository } from '@nestjs/typeorm';
import { Repository } from 'typeorm';
import { User } from './user.entity';
import { CreateUserDto } from './user.dto';

@Injectable()
export class UserService {
    constructor(
        @InjectRepository(User)
        private userRepository: Repository<User>,
    ) {}

    async findAll(page: number = 1, limit: number = 10): Promise<[User[], number]> {
        return this.userRepository.findAndCount({
            skip: (page - 1) * limit,
            take: limit,
        });
    }

    async findOne(id: number): Promise<User> {
        return this.userRepository.findOne({ where: { id } });
    }

    async create(createUserDto: CreateUserDto): Promise<User> {
        const user = this.userRepository.create(createUserDto);
        return this.userRepository.save(user);
    }

    async findByEmail(email: string): Promise<User> {
        return this.userRepository.findOne({ where: { email } });
    }
}

// user.controller.ts
import {
    Controller,
    Get,
    Post,
    Body,
    Param,
    ParseIntPipe,
    Query,
    HttpStatus,
} from '@nestjs/common';
import { UserService } from './user.service';
import { CreateUserDto } from './user.dto';

@Controller('users')
export class UserController {
    constructor(private readonly userService: UserService) {}

    @Get()
    async findAll(
        @Query('page') page: number = 1,
        @Query('limit') limit: number = 10,
    ) {
        const [data, total] = await this.userService.findAll(page, limit);
        
        return {
            data,
            pagination: {
                page,
                limit,
                total,
            },
        };
    }

    @Get(':id')
    async findOne(@Param('id', ParseIntPipe) id: number) {
        const user = await this.userService.findOne(id);
        if (!user) {
            throw new HttpException('用户未找到', HttpStatus.NOT_FOUND);
        }
        return user;
    }

    @Post()
    async create(@Body() createUserDto: CreateUserDto) {
        return await this.userService.create(createUserDto);
    }
}
```

**NestJS 高级特性：**
```typescript
// auth.guard.ts
import {
    Injectable,
    CanActivate,
    ExecutionContext,
    UnauthorizedException,
} from '@nestjs/common';
import { JwtService } from '@nestjs/jwt';

@Injectable()
export class AuthGuard implements CanActivate {
    constructor(private jwtService: JwtService) {}

    async canActivate(context: ExecutionContext): Promise<boolean> {
        const request = context.switchToHttp().getRequest();
        const token = this.extractTokenFromHeader(request);
        
        if (!token) {
            throw new UnauthorizedException();
        }
        
        try {
            const payload = await this.jwtService.verifyAsync(token, {
                secret: process.env.JWT_SECRET,
            });
            request['user'] = payload;
        } catch {
            throw new UnauthorizedException();
        }
        
        return true;
    }

    private extractTokenFromHeader(request: any): string | undefined {
        const [type, token] = request.headers.authorization?.split(' ') ?? [];
        return type === 'Bearer' ? token : undefined;
    }
}

// roles.guard.ts
import { Injectable, CanActivate, ExecutionContext } from '@nestjs/common';
import { Reflector } from '@nestjs/core';

@Injectable()
export class RolesGuard implements CanActivate {
    constructor(private reflector: Reflector) {}

    canActivate(context: ExecutionContext): boolean {
        const requiredRoles = this.reflector.getAllAndOverride<string[]>('roles', [
            context.getHandler(),
            context.getClass(),
        ]);
        
        if (!requiredRoles) {
            return true;
        }
        
        const { user } = context.switchToHttp().getRequest();
        return requiredRoles.some((role) => user.roles?.includes(role));
    }
}

// user.controller.ts (with guards)
import { UseGuards, SetMetadata } from '@nestjs/common';

@Controller('users')
@UseGuards(AuthGuard)
export class UserController {
    constructor(private readonly userService: UserService) {}

    @Get(':id')
    @UseGuards(RolesGuard)
    @SetMetadata('roles', ['admin'])
    async findOne(@Param('id', ParseIntPipe) id: number) {
        return await this.userService.findOne(id);
    }

    @Post()
    async create(@Body() createUserDto: CreateUserDto) {
        return await this.userService.create(createUserDto);
    }
}

// app.interceptor.ts
import {
    Injectable,
    NestInterceptor,
    ExecutionContext,
    CallHandler,
} from '@nestjs/common';
import { Observable } from 'rxjs';
import { tap } from 'rxjs/operators';

@Injectable()
export class LoggingInterceptor implements NestInterceptor {
    intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
        console.log('Before...');
        const now = Date.now();
        
        return next
            .handle()
            .pipe(
                tap(() => console.log(`After... ${Date.now() - now}ms`)),
            );
    }
}

// app.filter.ts
import {
    ExceptionFilter,
    Catch,
    ArgumentsHost,
    HttpException,
    HttpStatus,
} from '@nestjs/common';

@Catch()
export class AllExceptionsFilter implements ExceptionFilter {
    catch(exception: unknown, host: ArgumentsHost) {
        const ctx = host.switchToHttp();
        const response = ctx.getResponse();
        const request = ctx.getRequest();

        const status = exception instanceof HttpException
            ? exception.getStatus()
            : HttpStatus.INTERNAL_SERVER_ERROR;

        response
            .status(status)
            .json({
                statusCode: status,
                timestamp: new Date().toISOString(),
                path: request.url,
                message: exception instanceof HttpException
                    ? exception.message
                    : 'Internal server error',
            });
    }
}

// main.ts (with interceptors and filters)
async function bootstrap() {
    const app = await NestFactory.create(AppModule);
    
    app.useGlobalInterceptors(new LoggingInterceptor());
    app.useGlobalFilters(new AllExceptionsFilter());
    
    await app.listen(3000);
}
```

## 18.2 数据库集成

### 关系型数据库连接

**MySQL 集成：**
```javascript
const mysql = require('mysql2/promise');
const { createPool } = require('mysql2/promise');

// 基础连接
const connection = mysql.createConnection({
    host: 'localhost',
    user: 'root',
    password: 'password',
    database: 'myapp',
    charset: 'utf8mb4'
});

// 连接池配置
const pool = createPool({
    host: 'localhost',
    user: 'root',
    password: 'password',
    database: 'myapp',
    waitForConnections: true,
    connectionLimit: 10,
    queueLimit: 0,
    acquireTimeout: 60000,
    timeout: 60000
});

// 用户模型
class UserModel {
    constructor(pool) {
        this.pool = pool;
    }

    async findAll(page = 1, limit = 10) {
        const offset = (page - 1) * limit;
        const [rows] = await this.pool.execute(
            'SELECT * FROM users LIMIT ? OFFSET ?',
            [limit, offset]
        );
        const [[countResult]] = await this.pool.execute('SELECT COUNT(*) as total FROM users');
        
        return {
            data: rows,
            pagination: {
                page,
                limit,
                total: countResult.total
            }
        };
    }

    async findById(id) {
        const [rows] = await this.pool.execute(
            'SELECT * FROM users WHERE id = ?',
            [id]
        );
        return rows[0];
    }

    async create(userData) {
        const { name, email, password } = userData;
        const [result] = await this.pool.execute(
            'INSERT INTO users (name, email, password) VALUES (?, ?, ?)',
            [name, email, password]
        );
        return { id: result.insertId, ...userData };
    }

    async update(id, userData) {
        const fields = [];
        const values = [];
        
        Object.keys(userData).forEach(key => {
            if (key !== 'id') {
                fields.push(`${key} = ?`);
                values.push(userData[key]);
            }
        });
        
        values.push(id);
        
        const [result] = await this.pool.execute(
            `UPDATE users SET ${fields.join(', ')} WHERE id = ?`,
            values
        );
        
        return result.affectedRows > 0;
    }

    async delete(id) {
        const [result] = await this.pool.execute(
            'DELETE FROM users WHERE id = ?',
            [id]
        );
        return result.affectedRows > 0;
    }

    async findByEmail(email) {
        const [rows] = await this.pool.execute(
            'SELECT * FROM users WHERE email = ?',
            [email]
        );
        return rows[0];
    }
}

// 事务处理
class UserService {
    constructor(userModel) {
        this.userModel = userModel;
    }

    async createUserWithProfile(userData, profileData) {
        const connection = await pool.getConnection();
        
        try {
            await connection.beginTransaction();
            
            // 创建用户
            const [userResult] = await connection.execute(
                'INSERT INTO users (name, email, password) VALUES (?, ?, ?)',
                [userData.name, userData.email, userData.password]
            );
            
            const userId = userResult.insertId;
            
            // 创建用户资料
            await connection.execute(
                'INSERT INTO user_profiles (user_id, bio, avatar) VALUES (?, ?, ?)',
                [userId, profileData.bio, profileData.avatar]
            );
            
            await connection.commit();
            
            return { userId, ...userData };
        } catch (error) {
            await connection.rollback();
            throw error;
        } finally {
            connection.release();
        }
    }
}

// 使用示例
const userModel = new UserModel(pool);
const userService = new UserService(userModel);

// 查询优化
class OptimizedUserModel {
    async findWithPosts(userId) {
        const [rows] = await this.pool.execute(`
            SELECT u.*, 
                   JSON_ARRAYAGG(
                       JSON_OBJECT(
                           'id', p.id,
                           'title', p.title,
                           'content', p.content
                       )
                   ) as posts
            FROM users u
            LEFT JOIN posts p ON u.id = p.user_id
            WHERE u.id = ?
            GROUP BY u.id
        `, [userId]);
        
        return rows[0];
    }
}
```

**PostgreSQL 集成：**
```javascript
const { Pool, Client } = require('pg');
const { promisify } = require('util');

// PostgreSQL 连接池
const pool = new Pool({
    user: 'postgres',
    host: 'localhost',
    database: 'myapp',
    password: 'password',
    port: 5432,
    max: 20,
    idleTimeoutMillis: 30000,
    connectionTimeoutMillis: 2000,
});

// 数据库查询构建器
class QueryBuilder {
    constructor(pool) {
        this.pool = pool;
        this.table = '';
        this.selectFields = ['*'];
        this.whereConditions = [];
        this.orderByClause = '';
        this.limitClause = '';
        this.offsetClause = '';
    }

    table(tableName) {
        this.table = tableName;
        return this;
    }

    select(fields) {
        this.selectFields = Array.isArray(fields) ? fields : [fields];
        return this;
    }

    where(field, operator, value) {
        this.whereConditions.push({ field, operator, value });
        return this;
    }

    orderBy(field, direction = 'ASC') {
        this.orderByClause = `ORDER BY ${field} ${direction}`;
        return this;
    }

    limit(count) {
        this.limitClause = `LIMIT ${count}`;
        return this;
    }

    offset(count) {
        this.offsetClause = `OFFSET ${count}`;
        return this;
    }

    async execute() {
        if (!this.table) {
            throw new Error('Table name is required');
        }

        let query = `SELECT ${this.selectFields.join(', ')} FROM ${this.table}`;
        const values = [];

        if (this.whereConditions.length > 0) {
            const whereClause = this.whereConditions
                .map((condition, index) => {
                    values.push(condition.value);
                    return `${condition.field} ${condition.operator} $${values.length}`;
                })
                .join(' AND ');
            query += ` WHERE ${whereClause}`;
        }

        if (this.orderByClause) query += ` ${this.orderByClause}`;
        if (this.limitClause) query += ` ${this.limitClause}`;
        if (this.offsetClause) query += ` ${this.offsetClause}`;

        const result = await this.pool.query(query, values);
        return result.rows;
    }
}

// 用户服务
class UserService {
    constructor(pool) {
        this.pool = pool;
    }

    async findAll(options = {}) {
        const { page = 1, limit = 10, sortBy = 'id', sortOrder = 'ASC' } = options;
        
        const offset = (page - 1) * limit;
        
        const query = `
            SELECT u.*, 
                   COUNT(p.id) as post_count
            FROM users u
            LEFT JOIN posts p ON u.id = p.user_id
            GROUP BY u.id
            ORDER BY ${sortBy} ${sortOrder}
            LIMIT $1 OFFSET $2
        `;
        
        const countQuery = 'SELECT COUNT(*) as total FROM users';
        
        const [result, countResult] = await Promise.all([
            this.pool.query(query, [limit, offset]),
            this.pool.query(countQuery)
        ]);
        
        return {
            data: result.rows,
            pagination: {
                page,
                limit,
                total: parseInt(countResult.rows[0].total)
            }
        };
    }

    async findById(id) {
        const query = `
            SELECT u.*, 
                   json_agg(
                       json_build_object(
                           'id', p.id,
                           'title', p.title,
                           'created_at', p.created_at
                       )
                   ) as posts
            FROM users u
            LEFT JOIN posts p ON u.id = p.user_id
            WHERE u.id = $1
            GROUP BY u.id
        `;
        
        const result = await this.pool.query(query, [id]);
        return result.rows[0];
    }

    async create(userData) {
        const { name, email, password } = userData;
        
        const query = `
            INSERT INTO users (name, email, password, created_at)
            VALUES ($1, $2, $3, NOW())
            RETURNING *
        `;
        
        const result = await this.pool.query(query, [name, email, password]);
        return result.rows[0];
    }

    async update(id, userData) {
        const fields = [];
        const values = [];
        let index = 1;
        
        Object.keys(userData).forEach(key => {
            if (key !== 'id') {
                fields.push(`${key} = $${index}`);
                values.push(userData[key]);
                index++;
            }
        });
        
        if (fields.length === 0) {
            throw new Error('No fields to update');
        }
        
        values.push(id);
        
        const query = `
            UPDATE users 
            SET ${fields.join(', ')}, updated_at = NOW()
            WHERE id = $${index}
            RETURNING *
        `;
        
        const result = await this.pool.query(query, values);
        return result.rows[0];
    }

    async delete(id) {
        const query = 'DELETE FROM users WHERE id = $1 RETURNING *';
        const result = await this.pool.query(query, [id]);
        return result.rowCount > 0;
    }
}

// 数据库连接管理
class DatabaseManager {
    constructor() {
        this.pool = pool;
        this.setupListeners();
    }

    setupListeners() {
        this.pool.on('connect', (client) => {
            console.log('数据库连接建立');
        });

        this.pool.on('error', (err) => {
            console.error('数据库连接错误:', err);
        });

        this.pool.on('acquire', (client) => {
            console.log('获取数据库连接');
        });

        this.pool.on('release', (client) => {
            console.log('释放数据库连接');
        });
    }

    async query(text, params) {
        const start = Date.now();
        const res = await this.pool.query(text, params);
        const duration = Date.now() - start;
        console.log('执行查询', { text, duration, rows: res.rowCount });
        return res;
    }

    async close() {
        await this.pool.end();
    }
}

// 使用示例
const dbManager = new DatabaseManager();
const userService = new UserService(dbManager.pool);

// 批量操作
class BatchOperations {
    static async batchInsert(pool, tableName, data) {
        if (data.length === 0) return [];
        
        const columns = Object.keys(data[0]);
        const values = data.map(row => Object.values(row));
        
        const placeholders = values.map((_, index) => {
            const start = index * columns.length + 1;
            return `(${Array(columns.length).fill().map((_, i) => `$${start + i}`).join(', ')})`;
        }).join(', ');
        
        const flatValues = values.flat();
        const query = `INSERT INTO ${tableName} (${columns.join(', ')}) VALUES ${placeholders} RETURNING *`;
        
        const result = await pool.query(query, flatValues);
        return result.rows;
    }

    static async batchUpdate(pool, tableName, updates, conditionField) {
        const client = await pool.connect();
        
        try {
            await client.query('BEGIN');
            
            for (const update of updates) {
                const fields = Object.keys(update).filter(key => key !== conditionField);
                const values = fields.map(field => update[field]);
                values.push(update[conditionField]);
                
                const query = `
                    UPDATE ${tableName}
                    SET ${fields.map((field, index) => `${field} = $${index + 1}`).join(', ')}
                    WHERE ${conditionField} = $${fields.length + 1}
                `;
                
                await client.query(query, values);
            }
            
            await client.query('COMMIT');
        } catch (error) {
            await client.query('ROLLBACK');
            throw error;
        } finally {
            client.release();
        }
    }
}
```

### NoSQL 数据库操作

**MongoDB 集成：**
```javascript
const mongoose = require('mongoose');
const { MongoClient } = require('mongodb');

// Mongoose 模型定义
const userSchema = new mongoose.Schema({
    name: {
        type: String,
        required: true,
        trim: true,
        maxlength: 100
    },
    email: {
        type: String,
        required: true,
        unique: true,
        lowercase: true,
        match: [/^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/, '请输入有效的邮箱']
    },
    password: {
        type: String,
        required: true,
        minlength: 6
    },
    profile: {
        bio: String,
        avatar: String,
        location: String
    },
    preferences: {
        newsletter: { type: Boolean, default: false },
        notifications: {
            email: { type: Boolean, default: true },
            push: { type: Boolean, default: true }
        }
    },
    roles: [{
        type: String,
        enum: ['user', 'admin', 'moderator']
    }],
    isActive: {
        type: Boolean,
        default: true
    }
}, {
    timestamps: true,
    toJSON: { virtuals: true },
    toObject: { virtuals: true }
});

// 虚拟字段
userSchema.virtual('fullName').get(function() {
    return `${this.firstName} ${this.lastName}`;
});

// 索引
userSchema.index({ email: 1 });
userSchema.index({ createdAt: -1 });
userSchema.index({ 'profile.location': 1 });

// 中间件
userSchema.pre('save', function(next) {
    if (this.isModified('password')) {
        // 密码加密逻辑
        this.password = hashPassword(this.password);
    }
    next();
});

userSchema.pre('find', function() {
    this.where({ isActive: true });
});

// 实例方法
userSchema.methods.comparePassword = function(candidatePassword) {
    return comparePasswords(candidatePassword, this.password);
};

// 静态方法
userSchema.statics.findByEmail = function(email) {
    return this.findOne({ email: email.toLowerCase() });
};

userSchema.statics.findActiveUsers = function() {
    return this.find({ isActive: true });
};

const User = mongoose.model('User', userSchema);

// MongoDB 原生驱动
class MongoService {
    constructor() {
        this.client = null;
        this.db = null;
    }

    async connect(uri, dbName) {
        this.client = new MongoClient(uri, {
            useNewUrlParser: true,
            useUnifiedTopology: true,
            maxPoolSize: 10,
            serverSelectionTimeoutMS: 5000,
            socketTimeoutMS: 45000,
        });
        
        await this.client.connect();
        this.db = this.client.db(dbName);
        console.log('MongoDB 连接成功');
    }

    async disconnect() {
        if (this.client) {
            await this.client.close();
            console.log('MongoDB 连接关闭');
        }
    }

    getCollection(collectionName) {
        return this.db.collection(collectionName);
    }

    // 聚合查询
    async getUserStats() {
        const collection = this.getCollection('users');
        
        const pipeline = [
            {
                $group: {
                    _id: null,
                    totalUsers: { $sum: 1 },
                    activeUsers: {
                        $sum: {
                            $cond: [{ $eq: ['$isActive', true] }, 1, 0]
                        }
                    },
                    avgAge: { $avg: '$age' }
                }
            }
        ];
        
        const result = await collection.aggregate(pipeline).toArray();
        return result[0] || { totalUsers: 0, activeUsers: 0, avgAge: 0 };
    }

    // 复杂查询
    async searchUsers(searchTerm, options = {}) {
        const { page = 1, limit = 10, sortBy = 'createdAt', sortOrder = -1 } = options;
        const skip = (page - 1) * limit;
        
        const collection = this.getCollection('users');
        
        const searchPipeline = [
            {
                $search: {
                    index: 'default',
                    text: {
                        query: searchTerm,
                        path: ['name', 'email', 'bio']
                    }
                }
            },
            {
                $match: {
                    isActive: true
                }
            },
            {
                $addFields: {
                    score: { $meta: 'searchScore' }
                }
            },
            {
                $sort: {
                    score: { $meta: 'textScore' },
                    [sortBy]: sortOrder
                }
            },
            {
                $skip: skip
            },
            {
                $limit: limit
            }
        ];
        
        const [results, totalCount] = await Promise.all([
            collection.aggregate(searchPipeline).toArray(),
            collection.countDocuments({
                $text: { $search: searchTerm },
                isActive: true
            })
        ]);
        
        return {
            data: results,
            pagination: {
                page,
                limit,
                total: totalCount
            }
        };
    }
}

// Redis 集成
const redis = require('redis');

class CacheService {
    constructor() {
        this.client = redis.createClient({
            host: 'localhost',
            port: 6379,
            retry_strategy: (options) => {
                if (options.error && options.error.code === 'ECONNREFUSED') {
                    return new Error('Redis 服务器拒绝连接');
                }
                if (options.total_retry_time > 1000 * 60 * 60) {
                    return new Error('重试时间已用完');
                }
                if (options.attempt > 10) {
                    return undefined;
                }
                return Math.min(options.attempt * 100, 3000);
            }
        });
        
        this.client.on('error', (err) => {
            console.error('Redis 错误:', err);
        });
        
        this.client.on('connect', () => {
            console.log('Redis 连接成功');
        });
    }

    async get(key) {
        try {
            const value = await this.client.get(key);
            return value ? JSON.parse(value) : null;
        } catch (error) {
            console.error('Redis GET 错误:', error);
            return null;
        }
    }

    async set(key, value, expireSeconds = 3600) {
        try {
            await this.client.setex(key, expireSeconds, JSON.stringify(value));
            return true;
        } catch (error) {
            console.error('Redis SET 错误:', error);
            return false;
        }
    }

    async del(key) {
        try {
            await this.client.del(key);
            return true;
        } catch (error) {
            console.error('Redis DEL 错误:', error);
            return false;
        }
    }

    async exists(key) {
        try {
            const result = await this.client.exists(key);
            return result === 1;
        } catch (error) {
            console.error('Redis EXISTS 错误:', error);
            return false;
        }
    }

    async hset(hashKey, field, value) {
        try {
            await this.client.hset(hashKey, field, JSON.stringify(value));
            return true;
        } catch (error) {
            console.error('Redis HSET 错误:', error);
            return false;
        }
    }

    async hget(hashKey, field) {
        try {
            const value = await this.client.hget(hashKey, field);
            return value ? JSON.parse(value) : null;
        } catch (error) {
            console.error('Redis HGET 错误:', error);
            return null;
        }
    }
}

// 使用示例
const mongoService = new MongoService();
const cacheService = new CacheService();

class UserService {
    constructor(mongoService, cacheService) {
        this.mongoService = mongoService;
        this.cacheService = cacheService;
    }

    async getUserById(id) {
        // 先从缓存获取
        const cacheKey = `user:${id}`;
        let user = await this.cacheService.get(cacheKey);
        
        if (user) {
            console.log('从缓存获取用户数据');
            return user;
        }
        
        // 从数据库获取
        const collection = this.mongoService.getCollection('users');
        user = await collection.findOne({ _id: new ObjectId(id), isActive: true });
        
        if (user) {
            // 存入缓存
            await this.cacheService.set(cacheKey, user, 3600); // 缓存1小时
        }
        
        return user;
    }

    async updateUser(id, updateData) {
        const collection = this.mongoService.getCollection('users');
        const result = await collection.updateOne(
            { _id: new ObjectId(id) },
            { $set: { ...updateData, updatedAt: new Date() } }
        );
        
        if (result.modifiedCount > 0) {
            // 清除缓存
            const cacheKey = `user:${id}`;
            await this.cacheService.del(cacheKey);
        }
        
        return result.modifiedCount > 0;
    }
}
```

### ORM 框架使用

**Sequelize ORM：**
```javascript
const { Sequelize, DataTypes, Model } = require('sequelize');

// 数据库连接
const sequelize = new Sequelize('database', 'username', 'password', {
    host: 'localhost',
    dialect: 'mysql',
    pool: {
        max: 5,
        min: 0,
        acquire: 30000,
        idle: 10000
    },
    logging: false, // 生产环境关闭日志
    timezone: '+08:00'
});

// 模型定义
class User extends Model {
    // 实例方法
    getFullName() {
        return `${this.firstName} ${this.lastName}`;
    }
    
    // 验证方法
    async isValidPassword(password) {
        return await bcrypt.compare(password, this.password);
    }
}

User.init({
    id: {
        type: DataTypes.INTEGER,
        primaryKey: true,
        autoIncrement: true
    },
    firstName: {
        type: DataTypes.STRING,
        allowNull: false,
        validate: {
            notEmpty: true,
            len: [2, 50]
        }
    },
    lastName: {
        type: DataTypes.STRING,
        allowNull: false,
        validate: {
            notEmpty: true,
            len: [2, 50]
        }
    },
    email: {
        type: DataTypes.STRING,
        allowNull: false,
        unique: true,
        validate: {
            isEmail: true,
            notEmpty: true
        }
    },
    password: {
        type: DataTypes.STRING,
        allowNull: false,
        validate: {
            notEmpty: true,
            len: [6, 100]
        }
    },
    isActive: {
        type: DataTypes.BOOLEAN,
        defaultValue: true
    }
}, {
    sequelize,
    modelName: 'User',
    tableName: 'users',
    timestamps: true,
    paranoid: true, // 软删除
    indexes: [
        {
            unique: true,
            fields: ['email']
        }
    ],
    hooks: {
        beforeCreate: async (user) => {
            if (user.password) {
                user.password = await bcrypt.hash(user.password, 10);
            }
        },
        beforeUpdate: async (user) => {
            if (user.changed('password')) {
                user.password = await bcrypt.hash(user.password, 10);
            }
        }
    }
});

// 关联关系
class Post extends Model {}
Post.init({
    title: DataTypes.STRING,
    content: DataTypes.TEXT,
    published: {
        type: DataTypes.BOOLEAN,
        defaultValue: false
    }
}, { sequelize, modelName: 'Post' });

// 一对多关系
User.hasMany(Post, { foreignKey: 'userId' });
Post.belongsTo(User, { foreignKey: 'userId' });

// 多对多关系
class Tag extends Model {}
Tag.init({ name: DataTypes.STRING }, { sequelize, modelName: 'Tag' });

const PostTag = sequelize.define('PostTag', {}, { timestamps: false });

Post.belongsToMany(Tag, { through: PostTag });
Tag.belongsToMany(Post, { through: PostTag });

// 查询构建器
class UserQuery {
    constructor() {
        this.options = {
            where: {},
            include: [],
            order: [],
            limit: null,
            offset: 0
        };
    }

    where(conditions) {
        Object.assign(this.options.where, conditions);
        return this;
    }

    include(models) {
        this.options.include = this.options.include.concat(models);
        return this;
    }

    order(field, direction = 'ASC') {
        this.options.order.push([field, direction]);
        return this;
    }

    paginate(page = 1, limit = 10) {
        this.options.limit = limit;
        this.options.offset = (page - 1) * limit;
        return this;
    }

    async execute() {
        return await User.findAndCountAll(this.options);
    }
}

// 服务层
class UserService {
    static async createUser(userData) {
        try {
            const user = await User.create(userData);
            return user;
        } catch (error) {
            if (error.name === 'SequelizeUniqueConstraintError') {
                throw new Error('邮箱已存在');
            }
            throw error;
        }
    }

    static async findUsers(options = {}) {
        const { page = 1, limit = 10, search, sortBy = 'id', sortOrder = 'ASC' } = options;
        
        const query = new UserQuery()
            .paginate(page, limit)
            .order(sortBy, sortOrder);

        if (search) {
            query.where({
                [Sequelize.Op.or]: [
                    { firstName: { [Sequelize.Op.like]: `%${search}%` } },
                    { lastName: { [Sequelize.Op.like]: `%${search}%` } },
                    { email: { [Sequelize.Op.like]: `%${search}%` } }
                ]
            });
        }

        const result = await query.execute();
        
        return {
            data: result.rows,
            pagination: {
                page,
                limit,
                total: result.count
            }
        };
    }

    static async getUserWithPosts(userId) {
        return await User.findByPk(userId, {
            include: [{
                model: Post,
                where: { published: true },
                required: false
            }]
        });
    }

    static async getUserWithTags(userId) {
        return await User.findByPk(userId, {
            include: [{
                model: Post,
                include: [Tag]
            }]
        });
    }
}

// 事务处理
class TransactionService {
    static async transferMoney(fromUserId, toUserId, amount) {
        const transaction = await sequelize.transaction();
        
        try {
            // 扣除金额
            const fromUser = await User.findByPk(fromUserId, { transaction });
            if (fromUser.balance < amount) {
                throw new Error('余额不足');
            }
            await fromUser.update({ balance: fromUser.balance - amount }, { transaction });
            
            // 增加金额
            const toUser = await User.findByPk(toUserId, { transaction });
            await toUser.update({ balance: toUser.balance + amount }, { transaction });
            
            // 记录交易
            await Transaction.create({
                fromUserId,
                toUserId,
                amount,
                status: 'completed'
            }, { transaction });
            
            await transaction.commit();
            return { success: true };
        } catch (error) {
            await transaction.rollback();
            throw error;
        }
    }
}

// 数据库同步
async function syncDatabase() {
    try {
        await sequelize.authenticate();
        console.log('数据库连接成功');
        
        // 同步模型
        await sequelize.sync({ alter: true }); // 开发环境使用
        // await sequelize.sync({ force: true }); // 生产环境谨慎使用
        
        console.log('数据库同步完成');
    } catch (error) {
        console.error('数据库连接失败:', error);
    }
}

syncDatabase();
```

### 数据库连接池

**连接池管理：**
```javascript
// 通用连接池管理器
class ConnectionPool {
    constructor(createConnection, options = {}) {
        this.createConnection = createConnection;
        this.maxConnections = options.maxConnections || 10;
        this.minConnections = options.minConnections || 2;
        this.idleTimeout = options.idleTimeout || 30000;
        this.acquireTimeout = options.acquireTimeout || 30000;
        
        this.pool = [];
        this.busy = new Set();
        this.waiting = [];
        this.closed = false;
        
        // 初始化最小连接数
        this.initialize();
    }

    async initialize() {
        for (let i = 0; i < this.minConnections; i++) {
            try {
                const connection = await this.createConnection();
                this.pool.push({
                    connection,
                    lastUsed: Date.now(),
                    idle: true
                });
            } catch (error) {
                console.error('连接池初始化失败:', error);
            }
        }
    }

    async acquire() {
        return new Promise((resolve, reject) => {
            const timeout = setTimeout(() => {
                reject(new Error('获取连接超时'));
            }, this.acquireTimeout);

            const tryAcquire = () => {
                // 查找空闲连接
                const idleIndex = this.pool.findIndex(item => item.idle);
                if (idleIndex !== -1) {
                    const item = this.pool[idleIndex];
                    item.idle = false;
                    item.lastUsed = Date.now();
                    this.busy.add(item.connection);
                    clearTimeout(timeout);
                    resolve(item.connection);
                    return;
                }

                // 创建新连接（如果未达到最大连接数）
                if (this.pool.length + this.busy.size < this.maxConnections) {
                    this.createConnection()
                        .then(connection => {
                            const item = {
                                connection,
                                lastUsed: Date.now(),
                                idle: false
                            };
                            this.pool.push(item);
                            this.busy.add(connection);
                            clearTimeout(timeout);
                            resolve(connection);
                        })
                        .catch(error => {
                            clearTimeout(timeout);
                            reject(error);
                        });
                    return;
                }

                // 等待连接释放
                this.waiting.push({ resolve, reject, timeout });
            };

            tryAcquire();
        });
    }

    release(connection) {
        const item = this.pool.find(item => item.connection === connection);
        if (item) {
            item.idle = true;
            item.lastUsed = Date.now();
            this.busy.delete(connection);
            
            // 处理等待队列
            if (this.waiting.length > 0) {
                const { resolve, reject, timeout } = this.waiting.shift();
                clearTimeout(timeout);
                this.acquire().then(resolve).catch(reject);
            }
        }
    }

    async close() {
        this.closed = true;
        
        // 关闭所有连接
        const connections = [...this.pool.map(item => item.connection)];
        await Promise.all(connections.map(conn => this.closeConnection(conn)));
        
        this.pool = [];
        this.busy.clear();
        this.waiting.forEach(({ reject }) => {
            reject(new Error('连接池已关闭'));
        });
        this.waiting = [];
    }

    async closeConnection(connection) {
        if (typeof connection.end === 'function') {
            await connection.end();
        } else if (typeof connection.close === 'function') {
            await connection.close();
        }
    }

    getStats() {
        return {
            total: this.pool.length,
            idle: this.pool.filter(item => item.idle).length,
            busy: this.busy.size,
            waiting: this.waiting.length
        };
    }

    // 定期清理空闲连接
    startCleanup() {
        this.cleanupInterval = setInterval(() => {
            const now = Date.now();
            const idleConnections = this.pool
                .filter(item => item.idle && now - item.lastUsed > this.idleTimeout);
            
            idleConnections.forEach(async (item) => {
                const index = this.pool.indexOf(item);
                if (index !== -1) {
                    this.pool.splice(index, 1);
                    await this.closeConnection(item.connection);
                }
            });
        }, this.idleTimeout);
    }

    stopCleanup() {
        if (this.cleanupInterval) {
            clearInterval(this.cleanupInterval);
            this.cleanupInterval = null;
        }
    }
}

// MySQL 连接池
const mysql = require('mysql2/promise');

class MySQLPool extends ConnectionPool {
    constructor(options) {
        const createConnection = () => mysql.createConnection(options);
        super(createConnection, {
            maxConnections: options.connectionLimit || 10,
            minConnections: 2,
            idleTimeout: 30000,
            acquireTimeout: 30000
        });
    }
}

// 使用示例
const mysqlPool = new MySQLPool({
    host: 'localhost',
    user: 'root',
    password: 'password',
    database: 'myapp',
    connectionLimit: 10
});

mysqlPool.startCleanup();

// 数据库操作类
class DatabaseService {
    constructor(pool) {
        this.pool = pool;
    }

    async query(sql, params = []) {
        const connection = await this.pool.acquire();
        
        try {
            const [rows] = await connection.execute(sql, params);
            return rows;
        } finally {
            this.pool.release(connection);
        }
    }

    async transaction(callback) {
        const connection = await this.pool.acquire();
        
        try {
            await connection.beginTransaction();
            
            const result = await callback(connection);
            
            await connection.commit();
            return result;
        } catch (error) {
            await connection.rollback();
            throw error;
        } finally {
            this.pool.release(connection);
        }
    }

    getStats() {
        return this.pool.getStats();
    }
}

// 使用连接池
const dbService = new DatabaseService(mysqlPool);

// 查询操作
async function getUsers() {
    return await dbService.query('SELECT * FROM users LIMIT 10');
}

// 事务操作
async function transferMoney(fromId, toId, amount) {
    return await dbService.transaction(async (connection) => {
        await connection.execute(
            'UPDATE accounts SET balance = balance - ? WHERE id = ?',
            [amount, fromId]
        );
        
        await connection.execute(
            'UPDATE accounts SET balance = balance + ? WHERE id = ?',
            [amount, toId]
        );
        
        await connection.execute(
            'INSERT INTO transactions (from_id, to_id, amount) VALUES (?, ?, ?)',
            [fromId, toId, amount]
        );
    });
}

// 监控连接池状态
setInterval(() => {
    console.log('连接池状态:', dbService.getStats());
}, 5000);
```

## 18.3 实时应用

### Socket.IO 实时通信

**Socket.IO 服务器：**
```javascript
const express = require('express');
const http = require('http');
const socketIo = require('socket.io');
const redis = require('redis');
const redisAdapter = require('socket.io-redis');

const app = express();
const server = http.createServer(app);
const io = socketIo(server, {
    cors: {
        origin: "*",
        methods: ["GET", "POST"]
    }
});

// Redis 适配器（用于多实例部署）
const pubClient = redis.createClient({ host: 'localhost', port: 6379 });
const subClient = redis.createClient({ host: 'localhost', port: 6379 });

io.adapter(redisAdapter({ pubClient, subClient }));

// 在线用户管理
const onlineUsers = new Map();
const rooms = new Map();

// Socket.IO 中间件
io.use((socket, next) => {
    const token = socket.handshake.auth.token;
    if (token) {
        // 验证令牌
        try {
            const user = verifyToken(token);
            socket.userId = user.id;
            socket.username = user.username;
            next();
        } catch (error) {
            next(new Error('认证失败'));
        }
    } else {
        next(new Error('未提供认证令牌'));
    }
});

// 连接处理
io.on('connection', (socket) => {
    console.log('用户连接:', socket.userId);
    
    // 用户上线
    onlineUsers.set(socket.userId, {
        socketId: socket.id,
        username: socket.username,
        joinTime: new Date()
    });
    
    // 广播用户上线
    socket.broadcast.emit('user:joined', {
        userId: socket.userId,
        username: socket.username,
        time: new Date()
    });
    
    // 发送在线用户列表
    socket.emit('users:online', Array.from(onlineUsers.values()));
    
    // 房间相关事件
    socket.on('room:join', (roomId) => {
        socket.join(roomId);
        
        if (!rooms.has(roomId)) {
            rooms.set(roomId, {
                id: roomId,
                users: new Set(),
                createdAt: new Date()
            });
        }
        
        const room = rooms.get(roomId);
        room.users.add(socket.userId);
        
        // 通知房间内其他用户
        socket.to(roomId).emit('room:user:joined', {
            userId: socket.userId,
            username: socket.username,
            roomId: roomId
        });
        
        // 发送房间信息
        socket.emit('room:joined', {
            roomId: roomId,
            users: Array.from(room.users)
        });
    });
    
    socket.on('room:leave', (roomId) => {
        socket.leave(roomId);
        
        if (rooms.has(roomId)) {
            const room = rooms.get(roomId);
            room.users.delete(socket.userId);
            
            // 通知房间内其他用户
            socket.to(roomId).emit('room:user:left', {
                userId: socket.userId,
                username: socket.username,
                roomId: roomId
            });
            
            // 清理空房间
            if (room.users.size === 0) {
                rooms.delete(roomId);
            }
        }
    });
    
    // 聊天消息
    socket.on('chat:message', (data) => {
        const { roomId, message, type = 'text' } = data;
        
        const messageData = {
            id: Date.now(),
            userId: socket.userId,
            username: socket.username,
            message: message,
            type: type,
            timestamp: new Date(),
            roomId: roomId
        };
        
        // 存储消息到数据库（可选）
        saveMessage(messageData);
        
        // 广播消息到房间
        io.to(roomId).emit('chat:message', messageData);
        
        // 发送消息确认
        socket.emit('chat:message:sent', { messageId: messageData.id });
    });
    
    // 打字状态
    socket.on('typing:start', (data) => {
        const { roomId } = data;
        socket.to(roomId).emit('typing:start', {
            userId: socket.userId,
            username: socket.username,
            roomId: roomId
        });
    });
    
    socket.on('typing:stop', (data) => {
        const { roomId } = data;
        socket.to(roomId).emit('typing:stop', {
            userId: socket.userId,
            username: socket.username,
            roomId: roomId
        });
    });
    
    // 通知相关事件
    socket.on('notification:send', (data) => {
        const { targetUserId, type, content } = data;
        
        const notification = {
            id: Date.now(),
            fromUserId: socket.userId,
            toUserId: targetUserId,
            type: type,
            content: content,
            timestamp: new Date(),
            read: false
        };
        
        // 存储通知
        saveNotification(notification);
        
        // 发送实时通知
        const targetUser = onlineUsers.get(targetUserId);
        if (targetUser) {
            io.to(targetUser.socketId).emit('notification:received', notification);
        }
    });
    
    // 文件传输
    socket.on('file:upload:start', (data) => {
        const { roomId, fileName, fileSize } = data;
        
        const fileInfo = {
            id: Date.now(),
            userId: socket.userId,
            roomId: roomId,
            fileName: fileName,
            fileSize: fileSize,
            uploadId: generateUploadId(),
            timestamp: new Date()
        };
        
        // 广播文件上传开始
        socket.to(roomId).emit('file:upload:start', fileInfo);
        
        socket.emit('file:upload:ready', { uploadId: fileInfo.uploadId });
    });
    
    // 实时游戏事件
    socket.on('game:move', (data) => {
        const { roomId, move } = data;
        
        const gameData = {
            userId: socket.userId,
            move: move,
            timestamp: new Date()
        };
        
        socket.to(roomId).emit('game:move', gameData);
    });
    
    // 断开连接处理
    socket.on('disconnect', (reason) => {
        console.log('用户断开连接:', socket.userId, reason);
        
        // 用户下线
        onlineUsers.delete(socket.userId);
        
        // 通知其他用户
        socket.broadcast.emit('user:left', {
            userId: socket.userId,
            username: socket.username,
            time: new Date()
        });
        
        // 从所有房间移除用户
        rooms.forEach((room, roomId) => {
            if (room.users.has(socket.userId)) {
                room.users.delete(socket.userId);
                socket.to(roomId).emit('room:user:left', {
                    userId: socket.userId,
                    username: socket.username,
                    roomId: roomId
                });
                
                // 清理空房间
                if (room.users.size === 0) {
                    rooms.delete(roomId);
                }
            }
        });
    });
    
    // 错误处理
    socket.on('error', (error) => {
        console.error('Socket 错误:', error);
    });
});

// 工具函数
function verifyToken(token) {
    // 实现令牌验证逻辑
    return { id: 1, username: 'user' };
}

async function saveMessage(messageData) {
    // 实现消息存储逻辑
    console.log('保存消息:', messageData);
}

async function saveNotification(notification) {
    // 实现通知存储逻辑
    console.log('保存通知:', notification);
}

function generateUploadId() {
    return Math.random().toString(36).substr(2, 9);
}

// API 路由
app.get('/api/online-users', (req, res) => {
    res.json({
        count: onlineUsers.size,
        users: Array.from(onlineUsers.values()).map(user => ({
            userId: user.userId,
            username: user.username,
            joinTime: user.joinTime
        }))
    });
});

app.get('/api/rooms', (req, res) => {
    res.json({
        count: rooms.size,
        rooms: Array.from(rooms.values()).map(room => ({
            id: room.id,
            userCount: room.users.size,
            createdAt: room.createdAt
        }))
    });
});

const PORT = process.env.PORT || 3000;
server.listen(PORT, () => {
    console.log(`Socket.IO 服务器运行在端口 ${PORT}`);
});
```

**Socket.IO 客户端：**
```javascript
// 客户端实现
class ChatClient {
    constructor() {
        this.socket = null;
        this.userId = null;
        this.username = null;
        this.currentRoom = null;
        this.isTyping = false;
    }

    connect(token) {
        this.socket = io('http://localhost:3000', {
            auth: { token }
        });

        this.setupEventListeners();
    }

    setupEventListeners() {
        // 连接事件
        this.socket.on('connect', () => {
            console.log('连接成功');
        });

        this.socket.on('disconnect', (reason) => {
            console.log('连接断开:', reason);
        });

        // 用户事件
        this.socket.on('user:joined', (data) => {
            this.onUserJoined(data);
        });

        this.socket.on('user:left', (data) => {
            this.onUserLeft(data);
        });

        this.socket.on('users:online', (users) => {
            this.onOnlineUsers(users);
        });

        // 房间事件
        this.socket.on('room:joined', (data) => {
            this.onRoomJoined(data);
        });

        this.socket.on('room:user:joined', (data) => {
            this.onRoomUserJoined(data);
        });

        this.socket.on('room:user:left', (data) => {
            this.onRoomUserLeft(data);
        });

        // 聊天事件
        this.socket.on('chat:message', (data) => {
            this.onChatMessage(data);
        });

        this.socket.on('chat:message:sent', (data) => {
            this.onMessageSent(data);
        });

        // 打字状态
        this.socket.on('typing:start', (data) => {
            this.onTypingStart(data);
        });

        this.socket.on('typing:stop', (data) => {
            this.onTypingStop(data);
        });

        // 通知事件
        this.socket.on('notification:received', (data) => {
            this.onNotificationReceived(data);
        });

        // 文件传输
        this.socket.on('file:upload:start', (data) => {
            this.onFileUploadStart(data);
        });

        this.socket.on('file:upload:ready', (data) => {
            this.onFileUploadReady(data);
        });

        // 错误处理
        this.socket.on('connect_error', (error) => {
            console.error('连接错误:', error);
        });

        this.socket.on('error', (error) => {
            console.error('Socket 错误:', error);
        });
    }

    // 用户操作方法
    joinRoom(roomId) {
        this.socket.emit('room:join', roomId);
    }

    leaveRoom(roomId) {
        this.socket.emit('room:leave', roomId);
    }

    sendMessage(roomId, message, type = 'text') {
        this.socket.emit('chat:message', {
            roomId: roomId,
            message: message,
            type: type
        });
    }

    startTyping(roomId) {
        if (!this.isTyping) {
            this.isTyping = true;
            this.socket.emit('typing:start', { roomId: roomId });
        }
    }

    stopTyping(roomId) {
        if (this.isTyping) {
            this.isTyping = false;
            this.socket.emit('typing:stop', { roomId: roomId });
        }
    }

    sendNotification(targetUserId, type, content) {
        this.socket.emit('notification:send', {
            targetUserId: targetUserId,
            type: type,
            content: content
        });
    }

    // 事件处理方法
    onUserJoined(data) {
        console.log('用户加入:', data);
        // 更新用户界面
    }

    onUserLeft(data) {
        console.log('用户离开:', data);
        // 更新用户界面
    }

    onOnlineUsers(users) {
        console.log('在线用户:', users);
        // 更新在线用户列表
    }

    onRoomJoined(data) {
        this.currentRoom = data.roomId;
        console.log('加入房间:', data);
        // 更新房间界面
    }

    onRoomUserJoined(data) {
        console.log('房间用户加入:', data);
        // 更新房间用户列表
    }

    onRoomUserLeft(data) {
        console.log('房间用户离开:', data);
        // 更新房间用户列表
    }

    onChatMessage(data) {
        console.log('收到消息:', data);
        // 显示消息
    }

    onMessageSent(data) {
        console.log('消息发送成功:', data);
        // 更新消息状态
    }

    onTypingStart(data) {
        console.log('用户开始打字:', data);
        // 显示打字状态
    }

    onTypingStop(data) {
        console.log('用户停止打字:', data);
        // 隐藏打字状态
    }

    onNotificationReceived(data) {
        console.log('收到通知:', data);
        // 显示通知
    }

    onFileUploadStart(data) {
        console.log('文件上传开始:', data);
        // 显示文件上传进度
    }

    onFileUploadReady(data) {
        console.log('文件上传准备就绪:', data);
        // 开始文件上传
    }

    // 断开连接
    disconnect() {
        if (this.socket) {
            this.socket.disconnect();
        }
    }
}

// 使用示例
const chatClient = new ChatClient();

// 连接
chatClient.connect('your-jwt-token');

// 加入房间
chatClient.joinRoom('room-123');

// 发送消息
chatClient.sendMessage('room-123', 'Hello World!');

// 打字状态
chatClient.startTyping('room-123');
setTimeout(() => {
    chatClient.stopTyping('room-123');
}, 2000);
```

### 事件驱动架构

**事件总线实现：**
```javascript
const EventEmitter = require('events');

// 事件总线
class EventBus extends EventEmitter {
    constructor() {
        super();
        this.setMaxListeners(20);
    }

    // 发布事件
    publish(eventName, data) {
        this.emit(eventName, data);
        this.emit('*', { eventName, data }); // 通配符事件
    }

    // 订阅事件
    subscribe(eventName, handler) {
        this.on(eventName, handler);
        return () => this.unsubscribe(eventName, handler);
    }

    // 取消订阅
    unsubscribe(eventName, handler) {
        this.removeListener(eventName, handler);
    }

    // 订阅一次
    subscribeOnce(eventName, handler) {
        this.once(eventName, handler);
    }

    // 异步发布
    async publishAsync(eventName, data) {
        return new Promise((resolve) => {
            this.emit(eventName, data, resolve);
        });
    }

    // 获取事件统计
    getStats() {
        const eventNames = this.eventNames();
        const stats = {};
        
        eventNames.forEach(eventName => {
            stats[eventName] = this.listenerCount(eventName);
        });
        
        return stats;
    }
}

const eventBus = new EventBus();

// 领域事件
class UserRegisteredEvent {
    constructor(userId, email, registrationDate) {
        this.userId = userId;
        this.email = email;
        this.registrationDate = registrationDate;
        this.timestamp = new Date();
    }
}

class OrderCreatedEvent {
    constructor(orderId, userId, items, totalAmount) {
        this.orderId = orderId;
        this.userId = userId;
        this.items = items;
        this.totalAmount = totalAmount;
        this.timestamp = new Date();
    }
}

class PaymentProcessedEvent {
    constructor(paymentId, orderId, amount, status) {
        this.paymentId = paymentId;
        this.orderId = orderId;
        this.amount = amount;
        this.status = status;
        this.timestamp = new Date();
    }
}

// 事件处理器
class UserEventHandler {
    static handleUserRegistered(event) {
        console.log('处理用户注册事件:', event);
        
        // 发送欢迎邮件
        EmailService.sendWelcomeEmail(event.email);
        
        // 创建用户资料
        ProfileService.createProfile(event.userId);
        
        // 发布用户欢迎完成事件
        eventBus.publish('user.welcome.completed', {
            userId: event.userId,
            timestamp: new Date()
        });
    }

    static handleUserWelcomeCompleted(event) {
        console.log('用户欢迎完成:', event);
        
        // 记录日志
        Logger.info('User welcome completed', event);
        
        // 更新统计
        AnalyticsService.track('user_welcome_completed', event.userId);
    }
}

class OrderEventHandler {
    static handleOrderCreated(event) {
        console.log('处理订单创建事件:', event);
        
        // 更新库存
        InventoryService.updateStock(event.items);
        
        // 发送订单确认邮件
        EmailService.sendOrderConfirmation(event.userId, event.orderId);
        
        // 处理支付
        PaymentService.processPayment(event.orderId, event.totalAmount);
    }

    static handleOrderCancelled(event) {
        console.log('处理订单取消事件:', event);
        
        // 恢复库存
        InventoryService.restoreStock(event.items);
        
        // 发送取消通知
        EmailService.sendOrderCancellation(event.userId, event.orderId);
        
        // 退款处理
        PaymentService.processRefund(event.orderId);
    }
}

class PaymentEventHandler {
    static handlePaymentProcessed(event) {
        console.log('处理支付完成事件:', event);
        
        if (event.status === 'success') {
            // 更新订单状态
            OrderService.updateStatus(event.orderId, 'paid');
            
            // 发送支付成功通知
            NotificationService.sendPaymentSuccess(event.userId, event.amount);
            
            // 积分奖励
            LoyaltyService.addPoints(event.userId, event.amount);
        } else {
            // 处理支付失败
            OrderService.updateStatus(event.orderId, 'payment_failed');
            
            // 发送支付失败通知
            NotificationService.sendPaymentFailed(event.userId, event.amount);
        }
    }
}

// 服务类
class UserService {
    static async registerUser(userData) {
        try {
            // 创建用户
            const user = await this.createUser(userData);
            
            // 发布用户注册事件
            const event = new UserRegisteredEvent(
                user.id,
                user.email,
                new Date()
            );
            
            eventBus.publish('user.registered', event);
            
            return user;
        } catch (error) {
            console.error('用户注册失败:', error);
            throw error;
        }
    }

    static async createUser(userData) {
        // 实现用户创建逻辑
        return { id: 1, email: userData.email };
    }
}

class OrderService {
    static async createOrder(userId, items) {
        try {
            // 计算总金额
            const totalAmount = this.calculateTotal(items);
            
            // 创建订单
            const order = await this.createOrderRecord(userId, items, totalAmount);
            
            // 发布订单创建事件
            const event = new OrderCreatedEvent(
                order.id,
                userId,
                items,
                totalAmount
            );
            
            eventBus.publish('order.created', event);
            
            return order;
        } catch (error) {
            console.error('订单创建失败:', error);
            throw error;
        }
    }

    static async cancelOrder(orderId) {
        try {
            // 获取订单信息
            const order = await this.getOrderById(orderId);
            
            // 取消订单
            await this.updateOrderStatus(orderId, 'cancelled');
            
            // 发布订单取消事件
            eventBus.publish('order.cancelled', {
                orderId: orderId,
                userId: order.userId,
                items: order.items,
                timestamp: new Date()
            });
        } catch (error) {
            console.error('订单取消失败:', error);
            throw error;
        }
    }

    static calculateTotal(items) {
        return items.reduce((total, item) => total + item.price * item.quantity, 0);
    }

    static async createOrderRecord(userId, items, totalAmount) {
        // 实现订单创建逻辑
        return { id: 1, userId, items, totalAmount };
    }

    static async getOrderById(orderId) {
        // 实现订单查询逻辑
        return { id: orderId, userId: 1, items: [] };
    }

    static async updateOrderStatus(orderId, status) {
        // 实现订单状态更新逻辑
        console.log(`订单 ${orderId} 状态更新为 ${status}`);
    }

    static async updateStatus(orderId, status) {
        await this.updateOrderStatus(orderId, status);
    }
}

class PaymentService {
    static async processPayment(orderId, amount) {
        try {
            // 处理支付
            const payment = await this.chargePayment(orderId, amount);
            
            // 发布支付完成事件
            const event = new PaymentProcessedEvent(
                payment.id,
                orderId,
                amount,
                payment.status
            );
            
            eventBus.publish('payment.processed', event);
        } catch (error) {
            console.error('支付处理失败:', error);
            
            // 发布支付失败事件
            const event = new PaymentProcessedEvent(
                null,
                orderId,
                amount,
                'failed'
            );
            
            eventBus.publish('payment.processed', event);
        }
    }

    static async processRefund(orderId) {
        try {
            // 处理退款
            const refund = await this.refundPayment(orderId);
            
            // 发布退款完成事件
            eventBus.publish('payment.refunded', {
                orderId: orderId,
                refundId: refund.id,
                amount: refund.amount,
                timestamp: new Date()
            });
        } catch (error) {
            console.error('退款处理失败:', error);
            throw error;
        }
    }

    static async chargePayment(orderId, amount) {
        // 实现支付逻辑
        return { id: 1, status: 'success' };
    }

    static async refundPayment(orderId) {
        // 实现退款逻辑
        return { id: 1, amount: 100 };
    }
}

// 事件订阅
eventBus.subscribe('user.registered', UserEventHandler.handleUserRegistered);
eventBus.subscribe('user.welcome.completed', UserEventHandler.handleUserWelcomeCompleted);
eventBus.subscribe('order.created', OrderEventHandler.handleOrderCreated);
eventBus.subscribe('order.cancelled', OrderEventHandler.handleOrderCancelled);
eventBus.subscribe('payment.processed', PaymentEventHandler.handlePaymentProcessed);

// 使用示例
async function example() {
    // 注册用户
    await UserService.registerUser({
        email: 'user@example.com',
        password: 'password123'
    });

    // 创建订单
    await OrderService.createOrder(1, [
        { productId: 1, quantity: 2, price: 50 },
        { productId: 2, quantity: 1, price: 30 }
    ]);
}

example().catch(console.error);

// 事件监控
setInterval(() => {
    console.log('事件总线统计:', eventBus.getStats());
}, 10000);
```

### 消息队列集成

**RabbitMQ 集成：**
```javascript
const amqp = require('amqplib');
const { v4: uuidv4 } = require('uuid');

// RabbitMQ 连接管理器
class RabbitMQService {
    constructor(options = {}) {
        this.url = options.url || 'amqp://localhost';
        this.connection = null;
        this.channel = null;
        this.reconnectInterval = options.reconnectInterval || 5000;
        this.maxRetries = options.maxRetries || 5;
        this.retryCount = 0;
    }

    async connect() {
        try {
            this.connection = await amqp.connect(this.url);
            this.channel = await this.connection.createChannel();
            
            console.log('RabbitMQ 连接成功');
            this.retryCount = 0;
            
            // 设置连接事件监听
            this.setupConnectionEvents();
            
            return this.channel;
        } catch (error) {
            console.error('RabbitMQ 连接失败:', error);
            
            if (this.retryCount < this.maxRetries) {
                this.retryCount++;
                console.log(`第 ${this.retryCount} 次重连，${this.reconnectInterval}ms 后重试`);
                
                setTimeout(() => {
                    this.connect();
                }, this.reconnectInterval);
            } else {
                console.error('达到最大重连次数，停止重连');
            }
        }
    }

    setupConnectionEvents() {
        this.connection.on('error', (error) => {
            console.error('RabbitMQ 连接错误:', error);
            this.handleConnectionError();
        });

        this.connection.on('close', () => {
            console.log('RabbitMQ 连接关闭');
            this.handleConnectionError();
        });
    }

    handleConnectionError() {
        if (this.retryCount < this.maxRetries) {
            setTimeout(() => {
                this.connect();
            }, this.reconnectInterval);
        }
    }

    async disconnect() {
        try {
            if (this.channel) {
                await this.channel.close();
            }
            if (this.connection) {
                await this.connection.close();
            }
            console.log('RabbitMQ 连接已关闭');
        } catch (error) {
            console.error('关闭 RabbitMQ 连接时出错:', error);
        }
    }

    async createQueue(queueName, options = {}) {
        if (!this.channel) {
            throw new Error('Channel not available');
        }
        
        return await this.channel.assertQueue(queueName, {
            durable: options.durable !== false,
            ...options
        });
    }

    async createExchange(exchangeName, type, options = {}) {
        if (!this.channel) {
            throw new Error('Channel not available');
        }
        
        return await this.channel.assertExchange(exchangeName, type, {
            durable: options.durable !== false,
            ...options
        });
    }

    async bindQueue(queueName, exchangeName, pattern = '') {
        if (!this.channel) {
            throw new Error('Channel not available');
        }
        
        return await this.channel.bindQueue(queueName, exchangeName, pattern);
    }
}

// 消息生产者
class MessageProducer {
    constructor(rabbitMQService) {
        this.rabbitMQ = rabbitMQService;
    }

    async sendToQueue(queueName, message, options = {}) {
        if (!this.rabbitMQ.channel) {
            throw new Error('Channel not available');
        }

        const content = Buffer.from(JSON.stringify(message));
        
        return await this.rabbitMQ.channel.sendToQueue(queueName, content, {
            persistent: true,
            messageId: uuidv4(),
            timestamp: Date.now(),
            ...options
        });
    }

    async publishToExchange(exchangeName, routingKey, message, options = {}) {
        if (!this.rabbitMQ.channel) {
            throw new Error('Channel not available');
        }

        const content = Buffer.from(JSON.stringify(message));
        
        return await this.rabbitMQ.channel.publish(exchangeName, routingKey, content, {
            persistent: true,
            messageId: uuidv4(),
            timestamp: Date.now(),
            ...options
        });
    }

    async sendWithDelay(queueName, message, delayMs) {
        const delayQueue = `${queueName}_delay_${delayMs}`;
        
        // 创建延迟队列
        await this.rabbitMQ.channel.assertQueue(delayQueue, {
            durable: true,
            arguments: {
                'x-message-ttl': delayMs,
                'x-dead-letter-exchange': '',
                'x-dead-letter-routing-key': queueName
            }
        });
        
        return await this.sendToQueue(delayQueue, message);
    }
}

// 消息消费者
class MessageConsumer {
    constructor(rabbitMQService) {
        this.rabbitMQ = rabbitMQService;
    }

    async consumeQueue(queueName, handler, options = {}) {
        if (!this.rabbitMQ.channel) {
            throw new Error('Channel not available');
        }

        // 设置预取数量
        await this.rabbitMQ.channel.prefetch(options.prefetch || 1);
        
        return await this.rabbitMQ.channel.consume(queueName, async (msg) => {
            if (msg !== null) {
                try {
                    const content = JSON.parse(msg.content.toString());
                    const result = await handler(content, msg);
                    
                    // 确认消息
                    this.rabbitMQ.channel.ack(msg);
                    
                    return result;
                } catch (error) {
                    console.error('消息处理失败:', error);
                    
                    // 处理失败的消息
                    if (options.retryOnError) {
                        this.handleRetry(msg, error);
                    } else {
                        this.rabbitMQ.channel.nack(msg, false, false);
                    }
                }
            }
        }, { noAck: false });
    }

    handleRetry(msg, error) {
        const headers = msg.properties.headers || {};
        const retryCount = headers['x-retry-count'] || 0;
        const maxRetries = 3;
        
        if (retryCount < maxRetries) {
            // 重新入队
            const newHeaders = {
                ...headers,
                'x-retry-count': retryCount + 1,
                'x-last-error': error.message
            };
            
            this.rabbitMQ.channel.publish(
                '',
                msg.fields.routingKey,
                msg.content,
                {
                    ...msg.properties,
                    headers: newHeaders
                }
            );
            
            this.rabbitMQ.channel.ack(msg);
        } else {
            // 移到死信队列
            console.error('消息重试次数已达上限，移至死信队列:', error);
            this.rabbitMQ.channel.nack(msg, false, false);
        }
    }

    async consumeWithDLX(queueName, handler, dlxOptions = {}) {
        const dlxName = dlxOptions.name || `${queueName}_dlx`;
        const dlqName = dlxOptions.queue || `${queueName}_dlq`;
        
        // 创建死信交换机和队列
        await this.rabbitMQ.channel.assertExchange(dlxName, 'direct', { durable: true });
        await this.rabbitMQ.channel.assertQueue(dlqName, { durable: true });
        await this.rabbitMQ.channel.bindQueue(dlqName, dlxName, dlqName);
        
        // 创建主队列，绑定死信
        await this.rabbitMQ.channel.assertQueue(queueName, {
            durable: true,
            arguments: {
                'x-dead-letter-exchange': dlxName,
                'x-dead-letter-routing-key': dlqName
            }
        });
        
        return await this.consumeQueue(queueName, handler);
    }
}

// 具体业务消息处理器
class OrderMessageHandler {
    static async handleOrderCreated(message, msg) {
        console.log('处理订单创建消息:', message);
        
        try {
            // 处理订单创建逻辑
            await this.processOrder(message.orderId);
            
            // 发送通知
            await NotificationService.sendOrderConfirmation(message.userId, message.orderId);
            
            console.log('订单创建处理完成:', message.orderId);
        } catch (error) {
            console.error('订单创建处理失败:', error);
            throw error;
        }
    }

    static async handlePaymentProcessed(message, msg) {
        console.log('处理支付完成消息:', message);
        
        try {
            // 更新订单状态
            await OrderService.updateStatus(message.orderId, 'paid');
            
            // 处理库存
            await InventoryService.updateStock(message.items);
            
            console.log('支付处理完成:', message.orderId);
        } catch (error) {
            console.error('支付处理失败:', error);
            throw error;
        }
    }

    static async processOrder(orderId) {
        // 模拟订单处理
        await new Promise(resolve => setTimeout(resolve, 1000));
        console.log(`订单 ${orderId} 处理完成`);
    }
}

class EmailMessageHandler {
    static async handleSendEmail(message, msg) {
        console.log('处理邮件发送消息:', message);
        
        try {
            // 发送邮件
            await EmailService.send(message.to, message.subject, message.body);
            
            console.log('邮件发送完成:', message.to);
        } catch (error) {
            console.error('邮件发送失败:', error);
            throw error;
        }
    }
}

// 服务类
class OrderService {
    constructor(producer) {
        this.producer = producer;
    }

    async createOrder(orderData) {
        try {
            // 创建订单
            const order = await this.createOrderInDB(orderData);
            
            // 发送订单创建消息
            await this.producer.sendToQueue('order.created', {
                orderId: order.id,
                userId: order.userId,
                items: order.items,
                totalAmount: order.totalAmount,
                timestamp: new Date()
            });
            
            return order;
        } catch (error) {
            console.error('订单创建失败:', error);
            throw error;
        }
    }

    async processPayment(orderId, paymentData) {
        try {
            // 处理支付
            const payment = await this.processPaymentInDB(orderId, paymentData);
            
            // 发送支付完成消息
            await this.producer.sendToQueue('payment.processed', {
                orderId: orderId,
                paymentId: payment.id,
                amount: payment.amount,
                status: payment.status,
                timestamp: new Date()
            });
            
            return payment;
        } catch (error) {
            console.error('支付处理失败:', error);
            throw error;
        }
    }

    async createOrderInDB(orderData) {
        // 实现数据库操作
        return { id: 1, ...orderData };
    }

    async processPaymentInDB(orderId, paymentData) {
        // 实现数据库操作
        return { id: 1, orderId, ...paymentData };
    }

    static async updateStatus(orderId, status) {
        console.log(`更新订单 ${orderId} 状态为 ${status}`);
        // 实现数据库更新
    }
}

class NotificationService {
    constructor(producer) {
        this.producer = producer;
    }

    async sendOrderConfirmation(userId, orderId) {
        await this.producer.sendToQueue('email.send', {
            to: `user${userId}@example.com`,
            subject: '订单确认',
            body: `您的订单 ${orderId} 已创建成功`,
            type: 'order_confirmation'
        });
    }

    static async send(to, subject, body) {
        // 实现邮件发送逻辑
        console.log(`发送邮件到 ${to}: ${subject}`);
        await new Promise(resolve => setTimeout(resolve, 500));
    }
}

class InventoryService {
    static async updateStock(items) {
        console.log('更新库存:', items);
        // 实现库存更新逻辑
    }
}

// 应用启动
async function startApplication() {
    // 初始化 RabbitMQ 服务
    const rabbitMQ = new RabbitMQService({
        url: process.env.RABBITMQ_URL || 'amqp://localhost',
        reconnectInterval: 5000,
        maxRetries: 5
    });
    
    await rabbitMQ.connect();
    
    // 创建队列和交换机
    await rabbitMQ.createQueue('order.created', { durable: true });
    await rabbitMQ.createQueue('payment.processed', { durable: true });
    await rabbitMQ.createQueue('email.send', { durable: true });
    
    // 初始化生产者和消费者
    const producer = new MessageProducer(rabbitMQ);
    const consumer = new MessageConsumer(rabbitMQ);
    
    // 初始化服务
    const orderService = new OrderService(producer);
    
    // 启动消费者
    await consumer.consumeQueue('order.created', OrderMessageHandler.handleOrderCreated, {
        prefetch: 5,
        retryOnError: true
    });
    
    await consumer.consumeQueue('payment.processed', OrderMessageHandler.handlePaymentProcessed, {
        prefetch: 3
    });
    
    await consumer.consumeQueue('email.send', EmailMessageHandler.handleSendEmail, {
        prefetch: 10
    });
    
    // 示例：创建订单
    setTimeout(async () => {
        await orderService.createOrder({
            userId: 1,
            items: [{ productId: 1, quantity: 2, price: 50 }],
            totalAmount: 100
        });
    }, 2000);
    
    // 优雅关闭
    process.on('SIGTERM', async () => {
        console.log('接收到 SIGTERM 信号，正在关闭...');
        await rabbitMQ.disconnect();
        process.exit(0);
    });
    
    process.on('SIGINT', async () => {
        console.log('接收到 SIGINT 信号，正在关闭...');
        await rabbitMQ.disconnect();
        process.exit(0);
    });
}

startApplication().catch(console.error);
```

### 微服务架构

**微服务基础框架：**
```javascript
const express = require('express');
const axios = require('axios');
const redis = require('redis');
const { v4: uuidv4 } = require('uuid');

// 服务注册与发现
class ServiceRegistry {
    constructor(redisClient) {
        this.redis = redisClient;
        this.services = new Map();
    }

    async register(serviceName, serviceInfo) {
        const serviceId = `${serviceName}:${uuidv4()}`;
        const key = `service:${serviceName}:${serviceId}`;
        const ttl = 30; // 30秒TTL
        
        await this.redis.setex(key, ttl, JSON.stringify({
            ...serviceInfo,
            id: serviceId,
            registeredAt: Date.now()
        }));
        
        // 保持心跳
        const heartbeat = setInterval(async () => {
            try {
                await this.redis.expire(key, ttl);
            } catch (error) {
                console.error('心跳失败:', error);
                clearInterval(heartbeat);
            }
        }, (ttl - 5) * 1000);
        
        return serviceId;
    }

    async discover(serviceName) {
        const pattern = `service:${serviceName}:*`;
        const keys = await this.redis.keys(pattern);
        
        const services = [];
        for (const key of keys) {
            try {
                const serviceData = await this.redis.get(key);
                if (serviceData) {
                    services.push(JSON.parse(serviceData));
                }
            } catch (error) {
                console.error('发现服务失败:', error);
            }
        }
        
        return services;
    }

    async getService(serviceName) {
        const services = await this.discover(serviceName);
        if (services.length === 0) {
            throw new Error(`服务 ${serviceName} 未找到`);
        }
        
        // 简单的负载均衡（随机选择）
        return services[Math.floor(Math.random() * services.length)];
    }
}

// API 网关
class ApiGateway {
    constructor(serviceRegistry, redisClient) {
        this.serviceRegistry = serviceRegistry;
        this.redis = redisClient;
        this.app = express();
        this.setupMiddleware();
    }

    setupMiddleware() {
        this.app.use(express.json());
        this.app.use(express.urlencoded({ extended: true }));
        
        // 限流中间件
        this.app.use('/api/', this.rateLimitMiddleware());
        
        // 缓存中间件
        this.app.use(this.cacheMiddleware());
    }

    rateLimitMiddleware() {
        const rateLimits = new Map();
        
        return (req, res, next) => {
            const ip = req.ip;
            const now = Date.now();
            const windowMs = 60000; // 1分钟
            const maxRequests = 100;
            
            if (!rateLimits.has(ip)) {
                rateLimits.set(ip, []);
            }
            
            const requests = rateLimits.get(ip);
            const validRequests = requests.filter(time => now - time < windowMs);
            validRequests.push(now);
            rateLimits.set(ip, validRequests);
            
            if (validRequests.length > maxRequests) {
                return res.status(429).json({ error: '请求过于频繁' });
            }
            
            next();
        };
    }

    cacheMiddleware() {
        return async (req, res, next) => {
            if (req.method !== 'GET') {
                return next();
            }
            
            const cacheKey = `cache:${req.originalUrl}`;
            const cached = await this.redis.get(cacheKey);
            
            if (cached) {
                res.set('X-Cache', 'HIT');
                return res.json(JSON.parse(cached));
            }
            
            // 重写 res.json 方法来缓存响应
            const originalJson = res.json;
            res.json = function(body) {
                res.set('X-Cache', 'MISS');
                this.redis.setex(cacheKey, 300, JSON.stringify(body)); // 缓存5分钟
                return originalJson.call(this, body);
            }.bind({ redis: this.redis, originalJson });
            
            next();
        };
    }

    async proxy(serviceName, req, res) {
        try {
            const service = await this.serviceRegistry.getService(serviceName);
            const url = `http://${service.host}:${service.port}${req.url}`;
            
            const response = await axios({
                method: req.method,
                url: url,
                data: req.body,
                headers: req.headers,
                timeout: 5000
            });
            
            res.status(response.status).json(response.data);
        } catch (error) {
            console.error('代理请求失败:', error);
            res.status(502).json({ error: '服务不可用' });
        }
    }

    setupRoutes() {
        // 用户服务路由
        this.app.use('/api/users', async (req, res) => {
            await this.proxy('user-service', req, res);
        });

        // 订单服务路由
        this.app.use('/api/orders', async (req, res) => {
            await this.proxy('order-service', req, res);
        });

        // 支付服务路由
        this.app.use('/api/payments', async (req, res) => {
            await this.proxy('payment-service', req, res);
        });

        // 健康检查
        this.app.get('/health', (req, res) => {
            res.json({ status: 'ok', timestamp: new Date().toISOString() });
        });

        // 服务发现
        this.app.get('/services', async (req, res) => {
            try {
                const services = await this.serviceRegistry.discover('*');
                res.json(services);
            } catch (error) {
                res.status(500).json({ error: error.message });
            }
        });
    }

    start(port) {
        this.setupRoutes();
        this.app.listen(port, () => {
            console.log(`API 网关运行在端口 ${port}`);
        });
    }
}

// 微服务基类
class MicroService {
    constructor(serviceName, options = {}) {
        this.serviceName = serviceName;
        this.port = options.port || 3000;
        this.host = options.host || 'localhost';
        this.app = express();
        this.setupMiddleware();
    }

    setupMiddleware() {
        this.app.use(express.json());
        this.app.use(express.urlencoded({ extended: true }));
        
        // 健康检查中间件
        this.app.use('/health', (req, res) => {
            res.json({ 
                status: 'ok', 
                service: this.serviceName,
                timestamp: new Date().toISOString()
            });
        });
        
        // 错误处理中间件
        this.app.use((err, req, res, next) => {
            console.error(`${this.serviceName} 错误:`, err);
            res.status(500).json({ error: '内部服务器错误' });
        });
    }

    async registerService(registry) {
        this.serviceId = await registry.register(this.serviceName, {
            host: this.host,
            port: this.port,
            pid: process.pid
        });
        
        console.log(`${this.serviceName} 注册成功，ID: ${this.serviceId}`);
    }

    start() {
        this.app.listen(this.port, () => {
            console.log(`${this.serviceName} 运行在端口 ${this.port}`);
        });
    }
}

// 具体微服务实现
class UserService extends MicroService {
    constructor(options) {
        super('user-service', options);
        this.setupRoutes();
    }

    setupRoutes() {
        this.app.get('/users', async (req, res) => {
            try {
                const users = await this.getUsers();
                res.json(users);
            } catch (error) {
                res.status(500).json({ error: error.message });
            }
        });

        this.app.get('/users/:id', async (req, res) => {
            try {
                const user = await this.getUserById(req.params.id);
                if (!user) {
                    return res.status(404).json({ error: '用户未找到' });
                }
                res.json(user);
            } catch (error) {
                res.status(500).json({ error: error.message });
            }
        });

        this.app.post('/users', async (req, res) => {
            try {
                const user = await this.createUser(req.body);
                res.status(201).json(user);
            } catch (error) {
                res.status(400).json({ error: error.message });
            }
        });
    }

    async getUsers() {
        // 模拟数据库查询
        return [
            { id: 1, name: 'Alice', email: 'alice@example.com' },
            { id: 2, name: 'Bob', email: 'bob@example.com' }
        ];
    }

    async getUserById(id) {
        // 模拟数据库查询
        const users = await this.getUsers();
        return users.find(user => user.id == id);
    }

    async createUser(userData) {
        // 模拟数据库插入
        return {
            id: Date.now(),
            ...userData,
            createdAt: new Date().toISOString()
        };
    }
}

class OrderService extends MicroService {
    constructor(options) {
        super('order-service', options);
        this.setupRoutes();
    }

    setupRoutes() {
        this.app.get('/orders', async (req, res) => {
            try {
                const orders = await this.getOrders();
                res.json(orders);
            } catch (error) {
                res.status(500).json({ error: error.message });
            }
        });

        this.app.get('/orders/:id', async (req, res) => {
            try {
                const order = await this.getOrderById(req.params.id);
                if (!order) {
                    return res.status(404).json({ error: '订单未找到' });
                }
                res.json(order);
            } catch (error) {
                res.status(500).json({ error: error.message });
            }
        });

        this.app.post('/orders', async (req, res) => {
            try {
                const order = await this.createOrder(req.body);
                res.status(201).json(order);
            } catch (error) {
                res.status(400).json({ error: error.message });
            }
        });
    }

    async getOrders() {
        // 模拟数据库查询
        return [
            { id: 1, userId: 1, total: 100, status: 'pending' },
            { id: 2, userId: 2, total: 200, status: 'completed' }
        ];
    }

    async getOrderById(id) {
        // 模拟数据库查询
        const orders = await this.getOrders();
        return orders.find(order => order.id == id);
    }

    async createOrder(orderData) {
        // 模拟数据库插入
        return {
            id: Date.now(),
            ...orderData,
            status: 'pending',
            createdAt: new Date().toISOString()
        };
    }
}

// 服务启动
async function startServices() {
    // 初始化 Redis
    const redisClient = redis.createClient({
        host: 'localhost',
        port: 6379
    });
    
    await redisClient.connect();
    
    // 初始化服务注册中心
    const serviceRegistry = new ServiceRegistry(redisClient);
    
    // 启动微服务
    const userService = new UserService({ port: 3001 });
    const orderService = new OrderService({ port: 3002 });
    
    await userService.registerService(serviceRegistry);
    await orderService.registerService(serviceRegistry);
    
    userService.start();
    orderService.start();
    
    // 启动 API 网关
    const apiGateway = new ApiGateway(serviceRegistry, redisClient);
    apiGateway.start(3000);
    
    // 优雅关闭
    const shutdown = async () => {
        console.log('正在关闭服务...');
        await redisClient.quit();
        process.exit(0);
    };
    
    process.on('SIGTERM', shutdown);
    process.on('SIGINT', shutdown);
}

startServices().catch(console.error);
```

# 十九、部署和运维

## 19.1 应用部署

### 服务器环境配置

**Ubuntu 服务器基础配置：**
```bash
# 系统更新和安全配置
sudo apt update && sudo apt upgrade -y

# 安装基础工具
sudo apt install -y curl wget git vim htop tree unzip

# 配置防火墙
sudo ufw enable
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw status verbose

# 创建专用用户
sudo adduser appuser
sudo usermod -aG sudo appuser
sudo su - appuser

# SSH 安全配置
sudo nano /etc/ssh/sshd_config
# 修改配置：
# Port 2222                    # 修改SSH端口
# PermitRootLogin no           # 禁止root登录
# PasswordAuthentication no    # 禁用密码认证
# PubkeyAuthentication yes     # 启用密钥认证

sudo systemctl restart ssh

# 安装 Node.js (使用 NodeSource)
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

# 安装 PM2
sudo npm install -g pm2

# 安装 Nginx
sudo apt install -y nginx

# 配置 Nginx 防火墙
sudo ufw allow 'Nginx Full'

# 安装数据库 (以 PostgreSQL 为例)
sudo apt install -y postgresql postgresql-contrib
sudo systemctl start postgresql
sudo systemctl enable postgresql

# 创建数据库用户和数据库
sudo -u postgres createuser --interactive
sudo -u postgres createdb myapp_production
```

**环境变量配置：**
```bash
# ~/.bashrc 或 ~/.profile
export NODE_ENV=production
export PORT=3000
export DATABASE_URL=postgresql://username:password@localhost:5432/myapp_production
export REDIS_URL=redis://localhost:6379
export JWT_SECRET=your-super-secret-jwt-key
export API_KEY=your-api-key

# 应用特定的环境变量文件
# .env.production
NODE_ENV=production
PORT=3000
DB_HOST=localhost
DB_PORT=5432
DB_NAME=myapp_production
DB_USER=appuser
DB_PASS=secure_password
REDIS_URL=redis://localhost:6379
JWT_SECRET=super_secret_key_here
LOG_LEVEL=info
API_RATE_LIMIT=100
```

**系统服务配置：**
```bash
# 创建 systemd 服务文件
sudo nano /etc/systemd/system/myapp.service

[Unit]
Description=My Node.js Application
After=network.target

[Service]
Type=simple
User=appuser
WorkingDirectory=/home/appuser/myapp
ExecStart=/usr/bin/node server.js
Restart=always
RestartSec=10
Environment=NODE_ENV=production
Environment=PORT=3000
EnvironmentFile=/home/appuser/myapp/.env.production

# 安全配置
NoNewPrivileges=true
PrivateTmp=true
ProtectSystem=full
ProtectHome=true

[Install]
WantedBy=multi-user.target

# 启用服务
sudo systemctl daemon-reload
sudo systemctl enable myapp
sudo systemctl start myapp
sudo systemctl status myapp

# 查看日志
sudo journalctl -u myapp -f
```

### 进程管理工具 PM2

**PM2 基础配置：**
```javascript
// ecosystem.config.js
module.exports = {
    apps: [
        {
            name: 'myapp-api',
            script: './dist/server.js',
            instances: 'max', // 根据CPU核心数自动调整
            exec_mode: 'cluster',
            env: {
                NODE_ENV: 'development',
                PORT: 3000
            },
            env_production: {
                NODE_ENV: 'production',
                PORT: 3000,
                LOG_LEVEL: 'error'
            },
            // 日志配置
            error_file: './logs/err.log',
            out_file: './logs/out.log',
            log_file: './logs/combined.log',
            log_date_format: 'YYYY-MM-DD HH:mm:ss',
            
            // 重启策略
            max_memory_restart: '1G',
            restart_delay: 1000,
            max_restarts: 10,
            min_uptime: '5m',
            
            // 监控配置
            watch: false, // 生产环境不开启
            ignore_watch: ['node_modules', 'logs'],
            
            // 负载均衡
            node_args: '--max-old-space-size=4096',
            
            // 健康检查
            listen_timeout: 3000,
            kill_timeout: 1600
        },
        {
            name: 'myapp-worker',
            script: './dist/worker.js',
            instances: 1,
            exec_mode: 'fork',
            env_production: {
                NODE_ENV: 'production'
            }
        }
    ],
    
    // 部署配置
    deploy: {
        production: {
            user: 'appuser',
            host: ['192.168.1.100'],
            ref: 'origin/main',
            repo: 'git@github.com:user/myapp.git',
            path: '/home/appuser/myapp',
            'pre-deploy-local': '',
            'post-deploy': 'npm install && npm run build && pm2 reload ecosystem.config.js --env production',
            'pre-setup': ''
        }
    }
};
```

**PM2 高级配置和监控：**
```bash
# 启动应用
pm2 start ecosystem.config.js --env production

# 启动并保存配置
pm2 start ecosystem.config.js --env production
pm2 save

# 设置开机自启
pm2 startup

# 监控命令
pm2 list                    # 查看所有应用
pm2 monit                   # 实时监控
pm2 show myapp-api          # 查看应用详情
pm2 logs myapp-api          # 查看日志
pm2 logs myapp-api --lines 100  # 查看最后100行日志
pm2 logs myapp-api --nostream   # 查看日志但不持续监听

# 应用管理
pm2 restart myapp-api       # 重启应用
pm2 reload myapp-api        # 优雅重载
pm2 stop myapp-api          # 停止应用
pm2 delete myapp-api        # 删除应用

# 集群管理
pm2 scale myapp-api +3      # 增加3个实例
pm2 scale myapp-api 5       # 设置为5个实例

# 性能监控
pm2 monit                   # 交互式监控界面
pm2 web                     # 启动Web监控界面 (端口9615)
```

**PM2 日志管理：**
```javascript
// logrotate 配置
// /etc/logrotate.d/pm2-myapp
"/home/appuser/.pm2/logs/*.log" {
    daily
    rotate 30
    compress
    delaycompress
    missingok
    notifempty
    copytruncate
    create 0644 appuser appuser
}

// 自定义日志格式化
const winston = require('winston');
const { format, transports } = winston;
const { combine, timestamp, printf, colorize } = format;

const logFormat = printf(({ level, message, timestamp, ...metadata }) => {
    let msg = `${timestamp} [${level}] : ${message} `;
    if (metadata && Object.keys(metadata).length > 0) {
        msg += JSON.stringify(metadata);
    }
    return msg;
});

const logger = winston.createLogger({
    level: process.env.LOG_LEVEL || 'info',
    format: combine(
        timestamp(),
        logFormat
    ),
    transports: [
        new transports.File({ 
            filename: 'logs/error.log', 
            level: 'error',
            maxsize: 5242880, // 5MB
            maxFiles: 5
        }),
        new transports.File({ 
            filename: 'logs/combined.log',
            maxsize: 5242880,
            maxFiles: 5
        }),
        new transports.Console({
            format: combine(
                colorize(),
                timestamp(),
                logFormat
            )
        })
    ]
});

// 在应用中使用
logger.info('应用启动', { port: 3000 });
logger.error('数据库连接失败', { error: 'Connection timeout' });
```

### Docker 容器化部署

**Dockerfile 配置：**
```dockerfile
# 多阶段构建
# 构建阶段
FROM node:18-alpine AS builder

WORKDIR /app

# 复制 package 文件
COPY package*.json ./

# 安装依赖
RUN npm ci --only=production && npm cache clean --force

# 复制源代码
COPY . .

# 构建应用
RUN npm run build

# 生产阶段
FROM node:18-alpine AS production

# 创建非root用户
RUN addgroup -g 1001 -S nodejs
RUN adduser -S nextjs -u 1001

WORKDIR /app

# 安装生产依赖
COPY package*.json ./
RUN npm ci --only=production && npm cache clean --force

# 复制构建产物
COPY --from=builder --chown=nextjs:nodejs /app/dist ./dist
COPY --from=builder --chown=nextjs:nodejs /app/public ./public

# 复制环境变量文件
COPY --chown=nextjs:nodejs .env.production .env

# 切换到非root用户
USER nextjs

# 健康检查
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
    CMD curl -f http://localhost:3000/health || exit 1

# 暴露端口
EXPOSE 3000

# 启动命令
CMD ["node", "dist/server.js"]
```

**Docker Compose 配置：**
```yaml
# docker-compose.yml
version: '3.8'

services:
  app:
    build: .
    container_name: myapp
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - DATABASE_URL=postgresql://postgres:password@db:5432/myapp
      - REDIS_URL=redis://redis:6379
    env_file:
      - .env.production
    depends_on:
      - db
      - redis
      - nginx
    volumes:
      - ./logs:/app/logs
      - ./uploads:/app/uploads
    restart: unless-stopped
    networks:
      - app-network
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:3000/health"]
      interval: 30s
      timeout: 10s
      retries: 3

  db:
    image: postgres:14-alpine
    container_name: myapp-db
    environment:
      POSTGRES_DB: myapp
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: password
    volumes:
      - postgres_data:/var/lib/postgresql/data
      - ./init.sql:/docker-entrypoint-initdb.d/init.sql
    ports:
      - "5432:5432"
    restart: unless-stopped
    networks:
      - app-network
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U postgres"]
      interval: 10s
      timeout: 5s
      retries: 5

  redis:
    image: redis:7-alpine
    container_name: myapp-redis
    command: redis-server --appendonly yes
    volumes:
      - redis_data:/data
    ports:
      - "6379:6379"
    restart: unless-stopped
    networks:
      - app-network
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 10s
      timeout: 3s
      retries: 3

  nginx:
    image: nginx:alpine
    container_name: myapp-nginx
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
      - ./ssl:/etc/nginx/ssl
      - ./logs/nginx:/var/log/nginx
    depends_on:
      - app
    restart: unless-stopped
    networks:
      - app-network

volumes:
  postgres_data:
  redis_data:

networks:
  app-network:
    driver: bridge
```

**Nginx 配置：**
```nginx
# nginx.conf
events {
    worker_connections 1024;
}

http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    # 日志格式
    log_format main '$remote_addr - $remote_user [$time_local] "$request" '
                    '$status $body_bytes_sent "$http_referer" '
                    '"$http_user_agent" "$http_x_forwarded_for"';

    access_log /var/log/nginx/access.log main;
    error_log /var/log/nginx/error.log;

    # 性能优化
    sendfile on;
    tcp_nopush on;
    tcp_nodelay on;
    keepalive_timeout 65;
    types_hash_max_size 2048;

    # Gzip 压缩
    gzip on;
    gzip_vary on;
    gzip_min_length 1024;
    gzip_types text/plain text/css application/json application/javascript text/xml application/xml;

    # 安全头
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-XSS-Protection "1; mode=block" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header Referrer-Policy "no-referrer-when-downgrade" always;
    add_header Content-Security-Policy "default-src 'self' http: https: data: blob: 'unsafe-inline'" always;

    upstream app_servers {
        server app:3000;
    }

    server {
        listen 80;
        server_name example.com www.example.com;

        # 重定向到 HTTPS
        return 301 https://$server_name$request_uri;
    }

    server {
        listen 443 ssl http2;
        server_name example.com www.example.com;

        # SSL 配置
        ssl_certificate /etc/nginx/ssl/fullchain.pem;
        ssl_certificate_key /etc/nginx/ssl/privkey.pem;
        ssl_protocols TLSv1.2 TLSv1.3;
        ssl_ciphers ECDHE-RSA-AES256-GCM-SHA512:DHE-RSA-AES256-GCM-SHA512:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES256-GCM-SHA384;
        ssl_prefer_server_ciphers off;

        # 客户端证书验证（可选）
        # ssl_client_certificate /etc/nginx/ssl/client-cert.pem;
        # ssl_verify_client optional;

        # 静态文件缓存
        location ~* \.(jpg|jpeg|png|gif|ico|css|js)$ {
            root /app/public;
            expires 1y;
            add_header Cache-Control "public, immutable";
        }

        # API 代理
        location /api/ {
            proxy_pass http://app_servers;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection 'upgrade';
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
            proxy_cache_bypass $http_upgrade;
            proxy_read_timeout 90;
        }

        # 主应用
        location / {
            proxy_pass http://app_servers;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection 'upgrade';
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
            proxy_cache_bypass $http_upgrade;
        }

        # 健康检查
        location /health {
            access_log off;
            return 200 "healthy\n";
            add_header Content-Type text/plain;
        }

        # 速率限制
        limit_req_zone $binary_remote_addr zone=api:10m rate=10r/s;
        limit_req zone=api burst=20 nodelay;
    }
}
```

### 云平台部署方案

**AWS 部署方案：**
```bash
# AWS CLI 配置
aws configure
# 输入 Access Key ID, Secret Access Key, Region, Output format

# 使用 Elastic Beanstalk
# 安装 EB CLI
pip install awsebcli

# 初始化 EB 应用
eb init
# 选择区域和应用名称

# 部署应用
eb create production-env
eb deploy

# EB 配置文件
# .ebextensions/01_environment.config
option_settings:
  aws:elasticbeanstalk:application:environment:
    NODE_ENV: production
    DATABASE_URL: 
  aws:elasticbeanstalk:container:nodejs:
    NodeCommand: "npm start"
  aws:autoscaling:asg:
    MinSize: 2
    MaxSize: 10
  aws:autoscaling:trigger:
    BreachDuration: 5
    UpperThreshold: 60
    LowerThreshold: 20

# 使用 ECS 部署
# task-definition.json
{
  "family": "myapp-task",
  "containerDefinitions": [
    {
      "name": "myapp",
      "image": "123456789012.dkr.ecr.us-west-2.amazonaws.com/myapp:latest",
      "portMappings": [
        {
          "containerPort": 3000,
          "hostPort": 3000
        }
      ],
      "environment": [
        {
          "name": "NODE_ENV",
          "value": "production"
        }
      ],
      "logConfiguration": {
        "logDriver": "awslogs",
        "options": {
          "awslogs-group": "/ecs/myapp",
          "awslogs-region": "us-west-2",
          "awslogs-stream-prefix": "ecs"
        }
      },
      "healthCheck": {
        "command": ["CMD-SHELL", "curl -f http://localhost:3000/health || exit 1"],
        "interval": 30,
        "timeout": 5,
        "retries": 3
      }
    }
  ]
}
```

**Azure 部署方案：**
```bash
# Azure CLI 配置
az login

# 创建资源组
az group create --name myapp-rg --location eastus

# 创建容器注册表
az acr create --resource-group myapp-rg --name myappregistry --sku Basic

# 构建并推送镜像
az acr build --image myapp:v1 --registry myappregistry --file Dockerfile .

# 创建应用服务
az appservice plan create --name myapp-plan --resource-group myapp-rg --sku B1 --is-linux
az webapp create --resource-group myapp-rg --plan myapp-plan --name myapp-webapp --deployment-container-image-name myappregistry.azurecr.io/myapp:v1

# 配置环境变量
az webapp config appsettings set --resource-group myapp-rg --name myapp-webapp --settings NODE_ENV=production DATABASE_URL=

# 部署代码
az webapp deployment source config-local-git --resource-group myapp-rg --name myapp-webapp
```

## 19.2 性能监控

### 应用性能监控

**APM 工具集成：**
```javascript
// New Relic 集成
const newrelic = require('newrelic');

const express = require('express');
const app = express();

// 中间件监控
app.use(newrelic.getMiddleware());

app.get('/api/users', async (req, res) => {
    // 自定义监控
    newrelic.setControllerName('UserController', 'getUsers');
    
    try {
        const users = await getUsers();
        res.json(users);
    } catch (error) {
        newrelic.noticeError(error);
        res.status(500).json({ error: error.message });
    }
});

// Datadog 集成
const tracer = require('dd-trace').init({
    service: 'myapp',
    env: process.env.NODE_ENV,
    version: '1.0.0'
});

// 自定义指标
const { DogStatsD } = require('hot-shots');
const statsd = new DogStatsD({ host: 'localhost', port: 8125 });

// 数据库查询监控
async function getUsers() {
    const startTime = Date.now();
    
    try {
        const users = await db.query('SELECT * FROM users LIMIT 100');
        
        // 记录查询时间
        statsd.timing('db.query.users', Date.now() - startTime);
        statsd.increment('db.query.users.success');
        
        return users;
    } catch (error) {
        statsd.increment('db.query.users.error');
        throw error;
    }
}

// Prometheus 指标
const client = require('prom-client');
const collectDefaultMetrics = client.collectDefaultMetrics;
collectDefaultMetrics({ timeout: 5000 });

// 自定义指标
const httpRequestDuration = new client.Histogram({
    name: 'http_request_duration_seconds',
    help: 'Duration of HTTP requests in seconds',
    labelNames: ['method', 'route', 'status_code']
});

const httpRequestTotal = new client.Counter({
    name: 'http_requests_total',
    help: 'Total number of HTTP requests',
    labelNames: ['method', 'route', 'status_code']
});

// 监控中间件
app.use((req, res, next) => {
    const startTime = Date.now();
    
    res.on('finish', () => {
        const duration = (Date.now() - startTime) / 1000;
        
        httpRequestDuration.observe({
            method: req.method,
            route: req.route ? req.route.path : req.path,
            status_code: res.statusCode
        }, duration);
        
        httpRequestTotal.inc({
            method: req.method,
            route: req.route ? req.route.path : req.path,
            status_code: res.statusCode
        });
    });
    
    next();
});

// 指标端点
app.get('/metrics', async (req, res) => {
    res.set('Content-Type', client.register.contentType);
    res.end(await client.register.metrics());
});
```

**性能分析工具：**
```javascript
// 内存使用监控
const memwatch = require('@airbnb/node-memwatch');

// 内存泄漏检测
memwatch.on('leak', (info) => {
    console.error('内存泄漏检测:', info);
    // 发送告警
    sendAlert('Memory leak detected', info);
});

memwatch.on('stats', (stats) => {
    console.log('内存统计:', stats);
});

// CPU 使用监控
const os = require('os');

function getSystemMetrics() {
    const cpuUsage = os.loadavg();
    const memoryUsage = process.memoryUsage();
    const uptime = os.uptime();
    
    return {
        cpu: {
            load1: cpuUsage[0],
            load5: cpuUsage[1],
            load15: cpuUsage[2]
        },
        memory: {
            rss: memoryUsage.rss,
            heapTotal: memoryUsage.heapTotal,
            heapUsed: memoryUsage.heapUsed,
            external: memoryUsage.external
        },
        uptime: uptime,
        platform: os.platform(),
        arch: os.arch()
    };
}

// 定期报告系统指标
setInterval(() => {
    const metrics = getSystemMetrics();
    console.log('系统指标:', JSON.stringify(metrics, null, 2));
    
    // 发送到监控系统
    sendMetrics(metrics);
}, 30000);

// 性能基准测试
const Benchmark = require('benchmark');
const suite = new Benchmark.Suite;

suite
    .add('Array#forEach', function() {
        const arr = [1, 2, 3, 4, 5];
        arr.forEach(item => item * 2);
    })
    .add('for loop', function() {
        const arr = [1, 2, 3, 4, 5];
        for (let i = 0; i < arr.length; i++) {
            arr[i] * 2;
        }
    })
    .on('cycle', function(event) {
        console.log(String(event.target));
    })
    .on('complete', function() {
        console.log('Fastest is ' + this.filter('fastest').map('name'));
    })
    .run({ 'async': true });
```

### 日志管理策略

**结构化日志：**
```javascript
const winston = require('winston');
const { format, transports } = winston;
const { combine, timestamp, label, printf, errors } = format;

// 自定义日志格式
const logFormat = printf(({ level, message, label, timestamp, stack, ...metadata }) => {
    let logObject = {
        timestamp,
        level,
        label,
        message
    };

    if (stack) {
        logObject.stack = stack;
    }

    if (metadata && Object.keys(metadata).length > 0) {
        logObject.metadata = metadata;
    }

    return JSON.stringify(logObject);
});

// 日志配置
const logger = winston.createLogger({
    level: process.env.LOG_LEVEL || 'info',
    format: combine(
        label({ label: 'myapp' }),
        timestamp(),
        errors({ stack: true }),
        logFormat
    ),
    defaultMeta: { service: 'myapp' },
    transports: [
        // 控制台输出
        new transports.Console({
            format: combine(
                format.colorize(),
                label({ label: 'myapp' }),
                timestamp(),
                printf(({ level, message, label, timestamp }) => {
                    return `${timestamp} [${label}] ${level}: ${message}`;
                })
            )
        }),
        
        // 错误日志文件
        new transports.File({
            filename: 'logs/error.log',
            level: 'error',
            maxsize: 5242880, // 5MB
            maxFiles: 5,
            tailable: true
        }),
        
        // 综合日志文件
        new transports.File({
            filename: 'logs/combined.log',
            maxsize: 5242880,
            maxFiles: 10,
            tailable: true
        })
    ]
});

// 生产环境添加远程日志传输
if (process.env.NODE_ENV === 'production') {
    // 添加 ELK 栈支持
    const { ElasticsearchTransport } = require('winston-elasticsearch');
    
    logger.add(new ElasticsearchTransport({
        level: 'info',
        clientOpts: {
            node: process.env.ELASTICSEARCH_URL || 'http://localhost:9200'
        },
        indexPrefix: 'myapp-logs',
        indexSuffixPattern: 'YYYY.MM.DD',
        messageType: 'log',
        transformer: (logData) => {
            return {
                '@timestamp': logData.timestamp,
                severity: logData.level,
                message: logData.message,
                fields: logData.meta
            };
        }
    }));
}

// 请求日志中间件
const requestLogger = (req, res, next) => {
    const startTime = Date.now();
    
    // 记录请求开始
    logger.info('HTTP Request', {
        method: req.method,
        url: req.url,
        ip: req.ip,
        userAgent: req.get('User-Agent'),
        requestId: req.headers['x-request-id'] || require('crypto').randomBytes(16).toString('hex')
    });
    
    res.on('finish', () => {
        const duration = Date.now() - startTime;
        
        // 记录响应
        logger.info('HTTP Response', {
            method: req.method,
            url: req.url,
            statusCode: res.statusCode,
            duration: duration,
            contentLength: res.get('Content-Length'),
            requestId: req.headers['x-request-id']
        });
    });
    
    next();
};

// 错误日志中间件
const errorLogger = (err, req, res, next) => {
    logger.error('Unhandled error', {
        error: err.message,
        stack: err.stack,
        method: req.method,
        url: req.url,
        ip: req.ip,
        userAgent: req.get('User-Agent'),
        requestId: req.headers['x-request-id']
    });
    
    next(err);
};

// 在应用中使用
app.use(requestLogger);
app.use(errorLogger);

// 业务逻辑中的日志
class UserService {
    async createUser(userData) {
        const startTime = Date.now();
        
        try {
            logger.info('Creating user', { 
                email: userData.email,
                action: 'user.create'
            });
            
            const user = await this.db.create(userData);
            
            logger.info('User created successfully', {
                userId: user.id,
                email: user.email,
                duration: Date.now() - startTime,
                action: 'user.create.success'
            });
            
            return user;
        } catch (error) {
            logger.error('Failed to create user', {
                email: userData.email,
                error: error.message,
                stack: error.stack,
                duration: Date.now() - startTime,
                action: 'user.create.error'
            });
            
            throw error;
        }
    }
}
```

### 错误追踪系统

**错误处理和追踪：**
```javascript
const Sentry = require('@sentry/node');
const Tracing = require('@sentry/tracing');

// Sentry 初始化
Sentry.init({
    dsn: process.env.SENTRY_DSN,
    integrations: [
        new Sentry.Integrations.Http({ tracing: true }),
        new Tracing.Integrations.Express({ app }),
        new Tracing.Integrations.Postgres()
    ],
    tracesSampleRate: 1.0,
    environment: process.env.NODE_ENV,
    release: process.env.RELEASE_VERSION || '1.0.0'
});

// 全局错误处理
process.on('uncaughtException', (error) => {
    Sentry.captureException(error);
    console.error('未捕获的异常:', error);
    process.exit(1);
});

process.on('unhandledRejection', (reason, promise) => {
    Sentry.captureException(reason);
    console.error('未处理的 Promise 拒绝:', reason);
    process.exit(1);
});

// Express 错误处理中间件
app.use(Sentry.Handlers.requestHandler());
app.use(Sentry.Handlers.tracingHandler());

// 自定义错误类
class AppError extends Error {
    constructor(message, statusCode, isOperational = true) {
        super(message);
        this.statusCode = statusCode;
        this.isOperational = isOperational;
        this.isAppError = true;
        
        Error.captureStackTrace(this, this.constructor);
    }
}

// 错误处理中间件
const globalErrorHandler = (err, req, res, next) => {
    let error = { ...err };
    error.message = err.message;
    
    // 记录错误
    console.error(err);
    
    // 操作错误：客户端错误
    if (err.isAppError) {
        return res.status(err.statusCode).json({
            status: 'error',
            message: err.message
        });
    }
    
    // 编程错误：服务器错误
    if (process.env.NODE_ENV === 'development') {
        // 开发环境显示详细错误
        res.status(500).json({
            status: 'error',
            message: err.message,
            stack: err.stack,
            error: err
        });
    } else {
        // 生产环境隐藏详细错误
        Sentry.captureException(err);
        
        res.status(500).json({
            status: 'error',
            message: '服务器内部错误'
        });
    }
};

app.use(globalErrorHandler);

// API 错误处理
app.get('/api/users/:id', async (req, res, next) => {
    try {
        const user = await User.findById(req.params.id);
        
        if (!user) {
            return next(new AppError('用户未找到', 404));
        }
        
        res.json(user);
    } catch (error) {
        next(new AppError('获取用户失败', 500));
    }
});

// 自定义错误追踪
class ErrorTracker {
    static trackError(error, context = {}) {
        const errorInfo = {
            message: error.message,
            stack: error.stack,
            timestamp: new Date().toISOString(),
            context: context,
            environment: process.env.NODE_ENV,
            version: process.env.RELEASE_VERSION
        };
        
        // 发送到多个监控系统
        this.sendToSentry(error, context);
        this.sendToLog(errorInfo);
        this.sendToSlack(errorInfo);
    }
    
    static sendToSentry(error, context) {
        Sentry.withScope((scope) => {
            scope.setContext('context', context);
            Sentry.captureException(error);
        });
    }
    
    static sendToLog(errorInfo) {
        logger.error('Application Error', errorInfo);
    }
    
    static sendToSlack(errorInfo) {
        // 发送到 Slack 或其他通知系统
        if (process.env.SLACK_WEBHOOK_URL) {
            const axios = require('axios');
            axios.post(process.env.SLACK_WEBHOOK_URL, {
                text: `🚨 应用错误: ${errorInfo.message}`,
                attachments: [{
                    color: 'danger',
                    fields: [
                        {
                            title: '环境',
                            value: errorInfo.environment,
                            short: true
                        },
                        {
                            title: '时间',
                            value: errorInfo.timestamp,
                            short: true
                        },
                        {
                            title: '上下文',
                            value: JSON.stringify(errorInfo.context, null, 2),
                            short: false
                        }
                    ]
                }]
            }).catch(console.error);
        }
    }
}

// 使用错误追踪
try {
    await someRiskyOperation();
} catch (error) {
    ErrorTracker.trackError(error, {
        userId: req.user?.id,
        operation: 'someRiskyOperation',
        params: req.body
    });
    throw error;
}
```

### 资源使用监控

**系统资源监控：**
```javascript
const os = require('os');
const fs = require('fs');
const si = require('systeminformation');

class SystemMonitor {
    constructor() {
        this.metrics = {
            cpu: {},
            memory: {},
            disk: {},
            network: {},
            process: {}
        };
    }

    async collectMetrics() {
        try {
            // CPU 信息
            this.metrics.cpu = {
                usage: await this.getCpuUsage(),
                load: os.loadavg(),
                cores: os.cpus().length,
                model: os.cpus()[0]?.model
            };

            // 内存信息
            this.metrics.memory = {
                total: os.totalmem(),
                free: os.freemem(),
                used: os.totalmem() - os.freemem(),
                usagePercent: ((os.totalmem() - os.freemem()) / os.totalmem() * 100).toFixed(2)
            };

            // 磁盘信息
            this.metrics.disk = await this.getDiskUsage();

            // 网络信息
            this.metrics.network = await this.getNetworkUsage();

            // 进程信息
            this.metrics.process = {
                pid: process.pid,
                memory: process.memoryUsage(),
                uptime: process.uptime(),
                cpuUsage: process.cpuUsage()
            };

            return this.metrics;
        } catch (error) {
            console.error('收集系统指标失败:', error);
            return null;
        }
    }

    async getCpuUsage() {
        const start = this.getCpuTimes();
        await new Promise(resolve => setTimeout(resolve, 1000));
        const end = this.getCpuTimes();
        
        const idle = end.idle - start.idle;
        const total = end.total - start.total;
        const usage = 100 - ~~(100 * idle / total);
        
        return usage;
    }

    getCpuTimes() {
        const cpus = os.cpus();
        let idle = 0;
        let total = 0;
        
        cpus.forEach(cpu => {
            for (const type in cpu.times) {
                total += cpu.times[type];
            }
            idle += cpu.times.idle;
        });
        
        return { idle, total };
    }

    async getDiskUsage() {
        try {
            const diskInfo = await si.fsSize();
            return diskInfo.map(disk => ({
                fs: disk.fs,
                type: disk.type,
                size: disk.size,
                used: disk.used,
                available: disk.available,
                usePercent: disk.use.toFixed(2)
            }));
        } catch (error) {
            return [];
        }
    }

    async getNetworkUsage() {
        try {
            const networkStats = await si.networkStats();
            return networkStats.map(interface => ({
                interface: interface.iface,
                rxBytes: interface.rx_bytes,
                txBytes: interface.tx_bytes,
                rxErrors: interface.rx_errors,
                txErrors: interface.tx_errors
            }));
        } catch (error) {
            return [];
        }
    }

    async checkThresholds() {
        const metrics = await this.collectMetrics();
        if (!metrics) return;

        const alerts = [];

        // CPU 使用率检查
        if (metrics.cpu.usage > 80) {
            alerts.push({
                type: 'CPU_USAGE_HIGH',
                message: `CPU 使用率过高: ${metrics.cpu.usage}%`,
                severity: 'warning'
            });
        }

        // 内存使用率检查
        if (metrics.memory.usagePercent > 85) {
            alerts.push({
                type: 'MEMORY_USAGE_HIGH',
                message: `内存使用率过高: ${metrics.memory.usagePercent}%`,
                severity: 'warning'
            });
        }

        // 磁盘使用率检查
        metrics.disk.forEach(disk => {
            if (disk.usePercent > 90) {
                alerts.push({
                    type: 'DISK_USAGE_HIGH',
                    message: `磁盘 ${disk.fs} 使用率过高: ${disk.usePercent}%`,
                    severity: 'critical'
                });
            }
        });

        return alerts;
    }

    startMonitoring(interval = 30000) {
        setInterval(async () => {
            const alerts = await this.checkThresholds();
            if (alerts && alerts.length > 0) {
                this.sendAlerts(alerts);
            }
        }, interval);
    }

    sendAlerts(alerts) {
        alerts.forEach(alert => {
            console.warn(`[${alert.severity.toUpperCase()}] ${alert.message}`);
            
            // 发送到监控系统
            if (alert.severity === 'critical') {
                this.sendToPagerDuty(alert);
            }
            
            // 记录到日志
            logger.warn('System Alert', alert);
        });
    }

    sendToPagerDuty(alert) {
        // 实现 PagerDuty 集成
        if (process.env.PAGERDUTY_INTEGRATION_KEY) {
            const axios = require('axios');
            axios.post('https://events.pagerduty.com/v2/enqueue', {
                routing_key: process.env.PAGERDUTY_INTEGRATION_KEY,
                event_action: 'trigger',
                payload: {
                    summary: alert.message,
                    severity: alert.severity,
                    source: os.hostname()
                }
            }).catch(console.error);
        }
    }
}

// 使用系统监控
const monitor = new SystemMonitor();
monitor.startMonitoring(60000); // 每分钟检查一次

// 提供监控 API
app.get('/api/system/metrics', async (req, res) => {
    const metrics = await monitor.collectMetrics();
    res.json(metrics);
});

app.get('/api/system/health', async (req, res) => {
    const metrics = await monitor.collectMetrics();
    const health = {
        status: 'healthy',
        timestamp: new Date().toISOString(),
        metrics: metrics
    };
    
    // 检查关键指标
    if (metrics.cpu.usage > 90 || metrics.memory.usagePercent > 95) {
        health.status = 'degraded';
    }
    
    res.status(health.status === 'healthy' ? 200 : 503).json(health);
});
```

## 19.3 安全防护

### 服务器安全配置

**安全加固脚本：**
```bash
#!/bin/bash
# security-setup.sh

echo "开始服务器安全加固..."

# 1. 更新系统
sudo apt update && sudo apt upgrade -y

# 2. 安装安全工具
sudo apt install -y fail2ban ufw logwatch clamav

# 3. 配置防火墙
sudo ufw --force enable
sudo ufw default deny incoming
sudo ufw default allow outgoing

# 允许必要端口
sudo ufw allow ssh
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

# 4. 配置 SSH 安全
sudo sed -i 's/#Port 22/Port 2222/' /etc/ssh/sshd_config
sudo sed -i 's/PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config
sudo sed -i 's/#PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config
sudo systemctl restart ssh

# 5. 配置 fail2ban
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local

# 自定义 fail2ban 规则
sudo tee /etc/fail2ban/jail.local > /dev/null <<EOL
[DEFAULT]
bantime = 1h
findtime = 10m
maxretry = 3

[sshd]
enabled = true
port = 2222
filter = sshd
logpath = /var/log/auth.log
maxretry = 3
bantime = 1h

[nginx-http-auth]
enabled = true
filter = nginx-http-auth
port = http,https
logpath = /var/log/nginx/error.log

[nginx-botsearch]
enabled = true
filter = nginx-botsearch
port = http,https
logpath = /var/log/nginx/access.log
maxretry = 2
EOL

sudo systemctl restart fail2ban

# 6. 配置自动安全更新
sudo apt install -y unattended-upgrades
sudo dpkg-reconfigure -plow unattended-upgrades

# 7. 禁用不必要的服务
sudo systemctl disable bluetooth
sudo systemctl disable cups
sudo systemctl disable avahi-daemon

# 8. 设置文件权限
sudo chmod 700 /home/appuser
sudo chown root:root /etc/passwd /etc/shadow /etc/group /etc/gshadow

echo "安全加固完成！"
```

**用户和权限管理：**
```bash
# 创建安全用户
sudo adduser --disabled-password --gecos "" appuser
sudo usermod -aG docker appuser  # 如果使用 Docker

# 设置 SSH 密钥认证
sudo mkdir -p /home/appuser/.ssh
sudo cp /tmp/id_rsa.pub /home/appuser/.ssh/authorized_keys
sudo chown -R appuser:appuser /home/appuser/.ssh
sudo chmod 700 /home/appuser/.ssh
sudo chmod 600 /home/appuser/.ssh/authorized_keys

# 限制 sudo 权限
sudo tee /etc/sudoers.d/appuser > /dev/null <<EOL
appuser ALL=(ALL) NOPASSWD: /usr/bin/systemctl, /usr/bin/docker
EOL

# 禁用 root SSH 登录
sudo sed -i 's/PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config

# 设置密码策略
sudo apt install -y libpam-pwquality
sudo tee -a /etc/pam.d/common-password > /dev/null <<EOL
password requisite pam_pwquality.so retry=3 minlen=12 difok=3 ucredit=-1 lcredit=-1 dcredit=-1 ocredit=-1
EOL
```

### HTTPS 证书管理

**Let's Encrypt 证书管理：**
```bash
# 安装 Certbot
sudo apt install -y certbot python3-certbot-nginx

# 获取证书
sudo certbot --nginx -d example.com -d www.example.com

# 自动续期
sudo crontab -e
# 添加以下行：
# 0 12 * * * /usr/bin/certbot renew --quiet

# 手动续期测试
sudo certbot renew --dry-run

# 证书监控脚本
#!/bin/bash
# ssl-monitor.sh

DOMAINS=("example.com" "www.example.com")
EMAIL="admin@example.com"

for domain in "${DOMAINS[@]}"; do
    EXPIRY_DATE=$(echo | openssl s_client -servername $domain -connect $domain:443 2>/dev/null | openssl x509 -noout -enddate | cut -d= -f2)
    EXPIRY_SECONDS=$(date -d "$EXPIRY_DATE" +%s)
    CURRENT_SECONDS=$(date +%s)
    DAYS_LEFT=$(( (EXPIRY_SECONDS - CURRENT_SECONDS) / 86400 ))
    
    if [ $DAYS_LEFT -lt 30 ]; then
        echo "警告: $domain 证书将在 $DAYS_LEFT 天后过期" | mail -s "SSL证书即将过期" $EMAIL
    fi
done
```

**Nginx HTTPS 配置：**
```nginx
# nginx.conf
server {
    listen 80;
    server_name example.com www.example.com;
    
    # Let's Encrypt 验证
    location /.well-known/acme-challenge/ {
        root /var/www/certbot;
    }
    
    # 重定向到 HTTPS
    location / {
        return 301 https://$server_name$request_uri;
    }
}

server {
    listen 443 ssl http2;
    server_name example.com www.example.com;
    
    # SSL 证书
    ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;
    
    # SSL 安全配置
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384;
    ssl_prefer_server_ciphers off;
    
    # HSTS
    add_header Strict-Transport-Security "max-age=63072000" always;
    
    # OCSP Stapling
    ssl_stapling on;
    ssl_stapling_verify on;
    
    # 安全头
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-XSS-Protection "1; mode=block" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header Referrer-Policy "no-referrer-when-downgrade" always;
    
    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

### 访问控制策略

**API 访问控制：**
```javascript
const rateLimit = require('express-rate-limit');
const slowDown = require('express-slow-down');

// 基础速率限制
const basicLimiter = rateLimit({
    windowMs: 15 * 60 * 1000, // 15分钟
    max: 100, // 限制每个IP 100个请求
    message: {
        error: '请求过于频繁，请稍后再试'
    },
    standardHeaders: true,
    legacyHeaders: false,
});

// 严格速率限制（敏感API）
const strictLimiter = rateLimit({
    windowMs: 15 * 60 * 1000, // 15分钟
    max: 5, // 限制每个IP 5个请求
    message: {
        error: '请求过于频繁，账户已被临时限制'
    },
    standardHeaders: true,
    legacyHeaders: false,
});

// 速率减缓
const speedLimiter = slowDown({
    windowMs: 15 * 60 * 1000, // 15分钟
    delayAfter: 100, // 100个请求后开始减缓
    delayMs: 500 // 每个请求增加500ms延迟
});

// IP 白名单
const ipWhitelist = [
    '127.0.0.1',
    '::1',
    // 添加可信IP
];

const ipWhitelistMiddleware = (req, res, next) => {
    const clientIP = req.ip || req.connection.remoteAddress;
    
    if (ipWhitelist.includes(clientIP)) {
        return next();
    }
    
    res.status(403).json({ error: '访问被拒绝' });
};

// JWT 认证中间件
const jwt = require('jsonwebtoken');

const authenticateToken = (req, res, next) => {
    const authHeader = req.headers['authorization'];
    const token = authHeader && authHeader.split(' ')[1];
    
    if (!token) {
        return res.status(401).json({ error: '未提供访问令牌' });
    }
    
    jwt.verify(token, process.env.JWT_SECRET, (err, user) => {
        if (err) {
            return res.status(403).json({ error: '无效的访问令牌' });
        }
        
        req.user = user;
        next();
    });
};

// 角色权限控制
const checkPermission = (requiredRole) => {
    return (req, res, next) => {
        if (!req.user) {
            return res.status(401).json({ error: '需要认证' });
        }
        
        if (req.user.role !== requiredRole && req.user.role !== 'admin') {
            return res.status(403).json({ error: '权限不足' });
        }
        
        next();
    };
};

// API 密钥认证
const authenticateApiKey = (req, res, next) => {
    const apiKey = req.headers['x-api-key'] || req.query.api_key;
    
    if (!apiKey || apiKey !== process.env.API_KEY) {
        return res.status(401).json({ error: '无效的 API 密钥' });
    }
    
    next();
};

// CORS 配置
const cors = require('cors');

const corsOptions = {
    origin: function (origin, callback) {
        const allowedOrigins = [
            'https://example.com',
            'https://www.example.com',
            'http://localhost:3000'
        ];
        
        if (!origin || allowedOrigins.includes(origin)) {
            callback(null, true);
        } else {
            callback(new Error('不允许的来源'));
        }
    },
    credentials: true,
    optionsSuccessStatus: 200
};

// 在应用中使用
app.use('/api/', basicLimiter);
app.use('/api/auth/', strictLimiter);
app.use('/api/', speedLimiter);
app.use('/api/', cors(corsOptions));

// 敏感路由保护
app.post('/api/admin/*', authenticateToken, checkPermission('admin'));
app.get('/api/private/*', authenticateApiKey);
app.get('/api/internal/*', ipWhitelistMiddleware);
```

**安全中间件：**
```javascript
const helmet = require('helmet');
const hpp = require('hpp');
const xss = require('xss-clean');

// 安全头设置
app.use(helmet({
    contentSecurityPolicy: {
        directives: {
            defaultSrc: ["'self'"],
            styleSrc: ["'self'", "'unsafe-inline'"],
            scriptSrc: ["'self'"],
            imgSrc: ["'self'", "data:", "https:"],
            connectSrc: ["'self'"],
            fontSrc: ["'self'", "https:", "data:"],
            objectSrc: ["'none'"],
            mediaSrc: ["'self'"],
            frameSrc: ["'none'"],
        },
    },
    dnsPrefetchControl: { allow: false },
    frameguard: { action: 'deny' },
    hidePoweredBy: true,
    hsts: {
        maxAge: 31536000,
        includeSubDomains: true,
        preload: true
    },
    ieNoOpen: true,
    noSniff: true,
    referrerPolicy: { policy: 'no-referrer' },
    xssFilter: true,
}));

// 防止 HTTP 参数污染
app.use(hpp());

// 防止 XSS 攻击
app.use(xss());

// 输入验证中间件
const { body, validationResult } = require('express-validator');

const validateUserInput = [
    body('email').isEmail().normalizeEmail(),
    body('password').isLength({ min: 8 }).matches(/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)/),
    body('name').trim().isLength({ min: 2, max: 50 }),
    
    (req, res, next) => {
        const errors = validationResult(req);
        if (!errors.isEmpty()) {
            return res.status(400).json({ 
                error: '输入验证失败',
                details: errors.array() 
            });
        }
        next();
    }
];

// 在路由中使用
app.post('/api/users', validateUserInput, async (req, res) => {
    // 处理用户创建逻辑
});
```

### 数据备份方案

**自动化备份脚本：**
```bash
#!/bin/bash
# backup.sh

# 配置
BACKUP_DIR="/backup"
DATE=$(date +%Y%m%d_%H%M%S)
RETENTION_DAYS=30

# 创建备份目录
mkdir -p $BACKUP_DIR

# 数据库备份
backup_database() {
    local db_name=$1
    local backup_file="$BACKUP_DIR/db_${db_name}_${DATE}.sql.gz"
    
    echo "备份数据库: $db_name"
    
    if [ "$db_name" = "postgresql" ]; then
        pg_dump -U postgres -h localhost $db_name | gzip > $backup_file
    elif [ "$db_name" = "mysql" ]; then
        mysqldump -u root -p $db_name | gzip > $backup_file
    fi
    
    if [ $? -eq 0 ]; then
        echo "数据库备份成功: $backup_file"
        return 0
    else
        echo "数据库备份失败"
        return 1
    fi
}

# 文件备份
backup_files() {
    local source_dir=$1
    local backup_file="$BACKUP_DIR/files_${DATE}.tar.gz"
    
    echo "备份文件: $source_dir"
    
    tar -czf $backup_file $source_dir
    
    if [ $? -eq 0 ]; then
        echo "文件备份成功: $backup_file"
        return 0
    else
        echo "文件备份失败"
        return 1
    fi
}

# 上传到云存储
upload_to_cloud() {
    local backup_file=$1
    local bucket_name=$2
    
    echo "上传到云存储: $backup_file"
    
    # AWS S3
    if [ ! -z "$AWS_ACCESS_KEY_ID" ]; then
        aws s3 cp $backup_file s3://$bucket_name/backups/
    fi
    
    # Google Cloud Storage
    if [ ! -z "$GOOGLE_APPLICATION_CREDENTIALS" ]; then
        gsutil cp $backup_file gs://$bucket_name/backups/
    fi
}

# 清理旧备份
cleanup_old_backups() {
    echo "清理 $RETENTION_DAYS 天前的备份"
    find $BACKUP_DIR -name "*.gz" -mtime +$RETENTION_DAYS -delete
}

# 主备份流程
main() {
    echo "开始备份流程 - $(date)"
    
    # 备份数据库
    backup_database "postgresql" || exit 1
    
    # 备份重要文件
    backup_files "/home/appuser/uploads" || exit 1
    backup_files "/home/appuser/logs" || exit 1
    
    # 上传到云存储
    if [ ! -z "$BACKUP_BUCKET" ]; then
        for file in $BACKUP_DIR/*.gz; do
            upload_to_cloud $file $BACKUP_BUCKET
        done
    fi
    
    # 清理旧备份
    cleanup_old_backups
    
    echo "备份流程完成 - $(date)"
}

# 执行备份
main
```

**备份策略配置：**
```bash
# crontab 配置
# 每天凌晨2点执行完整备份
0 2 * * * /home/appuser/scripts/backup.sh >> /var/log/backup.log 2>&1

# 每小时执行增量备份
0 * * * * /home/appuser/scripts/incremental_backup.sh >> /var/log/incremental_backup.log 2>&1

# 每周日凌晨3点执行完整备份并清理
0 3 * * 0 /home/appuser/scripts/backup.sh && /home/appuser/scripts/cleanup.sh >> /var/log/weekly_backup.log 2>&1

# 备份监控脚本
#!/bin/bash
# backup_monitor.sh

check_backup_status() {
    local log_file="/var/log/backup.log"
    local last_backup=$(tail -20 $log_file | grep "备份流程完成" | tail -1)
    
    if [ -z "$last_backup" ]; then
        echo "警告: 最近没有成功的备份"
        # 发送告警
        echo "备份失败告警" | mail -s "备份失败" admin@example.com
        return 1
    fi
    
    local backup_time=$(echo $last_backup | cut -d'-' -f3- | xargs)
    local backup_timestamp=$(date -d "$backup_time" +%s)
    local current_timestamp=$(date +%s)
    local time_diff=$((current_timestamp - backup_timestamp))
    
    # 如果超过25小时没有备份，发送告警
    if [ $time_diff -gt 90000 ]; then
        echo "警告: 备份已超过25小时未执行"
        echo "备份超时告警" | mail -s "备份超时" admin@example.com
        return 1
    fi
    
    echo "备份状态正常"
    return 0
}

# 检查备份完整性
check_backup_integrity() {
    local backup_dir="/backup"
    local latest_backup=$(ls -t $backup_dir/*.gz | head -1)
    
    if [ ! -f "$latest_backup" ]; then
        echo "错误: 没有找到备份文件"
        return 1
    fi
    
    # 检查文件大小
    local file_size=$(stat -c%s "$latest_backup")
    if [ $file_size -lt 1024 ]; then
        echo "错误: 备份文件过小，可能不完整"
        return 1
    fi
    
    echo "备份文件完整性检查通过"
    return 0
}

# 主监控函数
monitor_backups() {
    echo "开始备份监控 - $(date)"
    
    check_backup_status
    local status_result=$?
    
    check_backup_integrity
    local integrity_result=$?
    
    if [ $status_result -ne 0 ] || [ $integrity_result -ne 0 ]; then
        echo "备份监控发现问题"
        return 1
    else
        echo "备份监控正常"
        return 0
    fi
}

# 执行监控
monitor_backups
```

**灾难恢复计划：**
```bash
#!/bin/bash
# disaster_recovery.sh

# 灾难恢复脚本
restore_database() {
    local backup_file=$1
    local db_name=$2
    
    echo "恢复数据库: $db_name 从 $backup_file"
    
    if [ ! -f "$backup_file" ]; then
        echo "错误: 备份文件不存在"
        return 1
    fi
    
    # 停止应用服务
    sudo systemctl stop myapp
    
    # 恢复数据库
    if [ "$db_name" = "postgresql" ]; then
        gunzip -c $backup_file | psql -U postgres -h localhost $db_name
    elif [ "$db_name" = "mysql" ]; then
        gunzip -c $backup_file | mysql -u root -p $db_name
    fi
    
    if [ $? -eq 0 ]; then
        echo "数据库恢复成功"
        sudo systemctl start myapp
        return 0
    else
        echo "数据库恢复失败"
        return 1
    fi
}

restore_files() {
    local backup_file=$1
    local target_dir=$2
    
    echo "恢复文件到: $target_dir 从 $backup_file"
    
    if [ ! -f "$backup_file" ]; then
        echo "错误: 备份文件不存在"
        return 1
    fi
    
    # 创建备份
    sudo tar -czf "${target_dir}_backup_$(date +%Y%m%d_%H%M%S).tar.gz" $target_dir
    
    # 恢复文件
    sudo tar -xzf $backup_file -C /
    
    if [ $? -eq 0 ]; then
        echo "文件恢复成功"
        return 0
    else
        echo "文件恢复失败"
        return 1
    fi
}

# 快速恢复脚本
quick_restore() {
    local backup_date=$1
    
    echo "执行快速恢复到: $backup_date"
    
    # 查找最近的备份
    local db_backup=$(ls -t /backup/db_postgresql_${backup_date}*.sql.gz | head -1)
    local files_backup=$(ls -t /backup/files_${backup_date}*.tar.gz | head -1)
    
    # 恢复数据库
    restore_database $db_backup "postgresql"
    
    # 恢复文件
    restore_files $files_backup "/home/appuser"
    
    echo "快速恢复完成"
}

# 完整恢复脚本
full_restore() {
    local backup_date=$1
    
    echo "执行完整恢复到: $backup_date"
    
    # 停止所有服务
    sudo systemctl stop nginx
    sudo systemctl stop myapp
    sudo systemctl stop postgresql
    
    # 恢复步骤
    quick_restore $backup_date
    
    # 启动服务
    sudo systemctl start postgresql
    sudo systemctl start myapp
    sudo systemctl start nginx
    
    echo "完整恢复完成"
}

# 使用说明
case "$1" in
    quick)
        quick_restore $2
        ;;
    full)
        full_restore $2
        ;;
    *)
        echo "使用方法: $0 {quick|full} [备份日期]"
        echo "示例: $0 quick 20231201"
        ;;
esac
```

# 二十、现代开发实践

## 20.1 开发工具链

### 代码编辑器配置

**VS Code 配置：**
```json
// .vscode/settings.json
{
    "editor.tabSize": 2,
    "editor.insertSpaces": true,
    "editor.renderWhitespace": "boundary",
    "editor.renderControlCharacters": true,
    "editor.formatOnSave": true,
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true,
        "source.organizeImports": true
    },
    "files.trimTrailingWhitespace": true,
    "files.insertFinalNewline": true,
    "files.trimFinalNewlines": true,
    "emmet.includeLanguages": {
        "javascript": "javascriptreact",
        "typescript": "typescriptreact"
    },
    "javascript.preferences.importModuleSpecifier": "relative",
    "typescript.preferences.importModuleSpecifier": "relative",
    "search.exclude": {
        "**/node_modules": true,
        "**/dist": true,
        "**/build": true,
        "**/.git": true
    },
    "files.exclude": {
        "**/__pycache__": true,
        "**/*.pyc": true
    }
}
```

**VS Code 扩展推荐：**
```json
// .vscode/extensions.json
{
    "recommendations": [
        "ms-vscode.vscode-typescript-next",
        "esbenp.prettier-vscode",
        "dbaeumer.vscode-eslint",
        "bradlc.vscode-tailwindcss",
        "ms-azuretools.vscode-docker",
        "ms-vscode.vscode-node-azure-pack",
        "ms-vscode.vscode-typescript-next",
        "ms-vscode.vscode-json",
        "ms-vscode.vscode-javascript",
        "ms-vscode.vscode-css",
        "ms-vscode.vscode-html",
        "ms-vscode.vscode-debugger",
        "ms-vscode.vscode-terminal",
        "ms-vscode.vscode-remote",
        "ms-vscode.vscode-remote-extensionpack",
        "ms-vscode.vscode-docker",
        "ms-vscode.vscode-kubernetes-tools",
        "ms-vscode.vscode-azure-account",
        "ms-vscode.vscode-azure-app-service",
        "ms-vscode.vscode-azure-storage",
        "ms-vscode.vscode-azure-databases",
        "ms-vscode.vscode-azure-resource-groups",
        "ms-vscode.vscode-azure-static-web-apps",
        "ms-vscode.vscode-azure-vm",
        "ms-vscode.vscode-azure-iot-edge",
        "ms-vscode.vscode-azure-iot-toolkit",
        "ms-vscode.vscode-azure-iot-hub",
        "ms-vscode.vscode-azure-event-hub",
        "ms-vscode.vscode-azure-service-bus",
        "ms-vscode.vscode-azure-cosmosdb",
        "ms-vscode.vscode-azure-functions",
        "ms-vscode.vscode-azure-app-service",
        "ms-vscode.vscode-azure-storage",
        "ms-vscode.vscode-azure-databases",
        "ms-vscode.vscode-azure-resource-groups",
        "ms-vscode.vscode-azure-static-web-apps",
        "ms-vscode.vscode-azure-vm",
        "ms-vscode.vscode-azure-iot-edge",
        "ms-vscode.vscode-azure-iot-toolkit",
        "ms-vscode.vscode-azure-iot-hub",
        "ms-vscode.vscode-azure-event-hub",
        "ms-vscode.vscode-azure-service-bus",
        "ms-vscode.vscode-azure-cosmosdb",
        "ms-vscode.vscode-azure-functions"
    ]
}
```

**代码片段配置：**
```json
// .vscode/snippets/javascript.json
{
    "Express Route Handler": {
        "prefix": "exroute",
        "body": [
            "app.${1:get}('${2:/api/route}', async (req, res) => {",
            "  try {",
            "    ${3:// Your code here}",
            "    res.status(200).json({ message: 'Success' });",
            "  } catch (error) {",
            "    console.error(error);",
            "    res.status(500).json({ error: error.message });",
            "  }",
            "});"
        ],
        "description": "Express route handler with async/await"
    },
    "Try-Catch Block": {
        "prefix": "trycatch",
        "body": [
            "try {",
            "  ${1:// Your code here}",
            "} catch (error) {",
            "  console.error('${2:Error occurred}:', error);",
            "  ${3:// Handle error}",
            "}"
        ],
        "description": "Try-catch block with error logging"
    },
    "Jest Test Suite": {
        "prefix": "jesttest",
        "body": [
            "describe('${1:Test Suite Name}', () => {",
            "  beforeEach(() => {",
            "    ${2:// Setup code}",
            "  });",
            "",
            "  test('${3:should do something}', async () => {",
            "    ${4:// Test code}",
            "  });",
            "",
            "  afterEach(() => {",
            "    ${5:// Cleanup code}",
            "  });",
            "});"
        ],
        "description": "Jest test suite template"
    }
}
```

**调试配置：**
```json
// .vscode/launch.json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "Launch Program",
            "skipFiles": [
                "<node_internals>/**"
            ],
            "program": "${workspaceFolder}/src/index.js",
            "env": {
                "NODE_ENV": "development"
            },
            "console": "integratedTerminal"
        },
        {
            "type": "node",
            "request": "attach",
            "name": "Attach to Process",
            "port": 9229,
            "restart": true,
            "skipFiles": [
                "<node_internals>/**"
            ]
        },
        {
            "type": "node",
            "request": "launch",
            "name": "Debug Jest Tests",
            "program": "${workspaceFolder}/node_modules/.bin/jest",
            "args": [
                "--runInBand",
                "--no-cache"
            ],
            "console": "integratedTerminal",
            "internalConsoleOptions": "neverOpen",
            "disableOptimisticBPs": true
        },
        {
            "type": "node",
            "request": "launch",
            "name": "Debug with Nodemon",
            "runtimeExecutable": "nodemon",
            "program": "${workspaceFolder}/src/index.js",
            "console": "integratedTerminal",
            "restart": true,
            "env": {
                "NODE_ENV": "development"
            }
        }
    ]
}
```

### 调试工具使用

**Node.js 调试器：**
```javascript
// 调试工具类
class Debugger {
    constructor(options = {}) {
        this.enabled = options.enabled || process.env.NODE_ENV === 'development';
        this.logLevel = options.logLevel || 'info';
    }

    log(level, message, data = {}) {
        if (!this.enabled) return;
        
        const levels = ['debug', 'info', 'warn', 'error'];
        const currentLevel = levels.indexOf(this.logLevel);
        const messageLevel = levels.indexOf(level);
        
        if (messageLevel >= currentLevel) {
            const timestamp = new Date().toISOString();
            const logMessage = `[${timestamp}] [${level.toUpperCase()}] ${message}`;
            
            if (Object.keys(data).length > 0) {
                console.log(logMessage, data);
            } else {
                console.log(logMessage);
            }
        }
    }

    debug(message, data) {
        this.log('debug', message, data);
    }

    info(message, data) {
        this.log('info', message, data);
    }

    warn(message, data) {
        this.log('warn', message, data);
    }

    error(message, data) {
        this.log('error', message, data);
    }

    // 性能监控
    time(label) {
        if (this.enabled) {
            console.time(label);
        }
    }

    timeEnd(label) {
        if (this.enabled) {
            console.timeEnd(label);
        }
    }

    // 内存使用监控
    memoryUsage() {
        if (this.enabled) {
            const usage = process.memoryUsage();
            this.info('Memory Usage', {
                rss: `${Math.round(usage.rss / 1024 / 1024)} MB`,
                heapTotal: `${Math.round(usage.heapTotal / 1024 / 1024)} MB`,
                heapUsed: `${Math.round(usage.heapUsed / 1024 / 1024)} MB`,
                external: `${Math.round(usage.external / 1024 / 1024)} MB`
            });
        }
    }

    // 调用栈跟踪
    trace(message) {
        if (this.enabled) {
            const stack = new Error().stack;
            this.debug(message, { stack });
        }
    }
}

// 使用示例
const debugger = new Debugger({ enabled: true, logLevel: 'debug' });

// 调试中间件
const debugMiddleware = (req, res, next) => {
    debugger.info('Incoming Request', {
        method: req.method,
        url: req.url,
        ip: req.ip,
        userAgent: req.get('User-Agent')
    });

    const startTime = Date.now();
    
    res.on('finish', () => {
        const duration = Date.now() - startTime;
        debugger.info('Response Sent', {
            method: req.method,
            url: req.url,
            statusCode: res.statusCode,
            duration: `${duration}ms`
        });
    });

    next();
};

// 调试路由处理器
app.get('/api/debug', debugMiddleware, async (req, res) => {
    debugger.time('api-debug-operation');
    
    try {
        debugger.debug('Starting debug operation');
        
        // 模拟一些操作
        await new Promise(resolve => setTimeout(resolve, 1000));
        
        debugger.memoryUsage();
        debugger.trace('Operation completed');
        
        res.json({ message: 'Debug operation completed' });
    } catch (error) {
        debugger.error('Debug operation failed', { error: error.message });
        res.status(500).json({ error: error.message });
    } finally {
        debugger.timeEnd('api-debug-operation');
    }
});
```

**Chrome DevTools 调试：**
```bash
# 启动带调试的 Node.js 应用
node --inspect src/index.js

# 启动带调试和断点的 Node.js 应用
node --inspect-brk src/index.js

# 使用 nodemon 调试
nodemon --inspect src/index.js

# Docker 调试
docker run -p 9229:9229 --rm -it myapp node --inspect=0.0.0.0:9229 src/index.js
```

**调试工具集成：**
```javascript
// 自定义调试工具
class AdvancedDebugger {
    constructor(options = {}) {
        this.enabled = options.enabled || false;
        this.outputFile = options.outputFile || null;
        this.filters = options.filters || [];
        this.logs = [];
    }

    // 条件调试
    conditionalLog(condition, message, data) {
        if (this.enabled && condition) {
            this.log(message, data);
        }
    }

    // 过滤调试
    logWithFilter(filter, message, data) {
        if (this.enabled && this.filters.includes(filter)) {
            this.log(message, data);
        }
    }

    // 异步调试
    async asyncLog(asyncOperation, label) {
        if (this.enabled) {
            const startTime = Date.now();
            console.time(label);
            
            try {
                const result = await asyncOperation();
                const duration = Date.now() - startTime;
                
                this.log(`${label} completed`, {
                    duration: `${duration}ms`,
                    result: result
                });
                
                return result;
            } catch (error) {
                this.error(`${label} failed`, {
                    error: error.message,
                    duration: `${Date.now() - startTime}ms`
                });
                throw error;
            } finally {
                console.timeEnd(label);
            }
        } else {
            return await asyncOperation();
        }
    }

    // 数据库查询调试
    async debugQuery(query, params, connection) {
        if (this.enabled) {
            const startTime = Date.now();
            
            this.log('Executing query', {
                query: query,
                params: params
            });
            
            try {
                const result = await connection.query(query, params);
                const duration = Date.now() - startTime;
                
                this.log('Query executed successfully', {
                    rowCount: result.rowCount,
                    duration: `${duration}ms`
                });
                
                return result;
            } catch (error) {
                this.error('Query execution failed', {
                    error: error.message,
                    query: query,
                    duration: `${Date.now() - startTime}ms`
                });
                throw error;
            }
        } else {
            return await connection.query(query, params);
        }
    }

    // API 调用调试
    async debugApiCall(url, options = {}) {
        if (this.enabled) {
            const startTime = Date.now();
            
            this.log('Making API call', {
                url: url,
                method: options.method || 'GET',
                headers: options.headers
            });
            
            try {
                const response = await fetch(url, options);
                const duration = Date.now() - startTime;
                
                this.log('API call completed', {
                    status: response.status,
                    statusText: response.statusText,
                    duration: `${duration}ms`
                });
                
                return response;
            } catch (error) {
                this.error('API call failed', {
                    error: error.message,
                    url: url,
                    duration: `${Date.now() - startTime}ms`
                });
                throw error;
            }
        } else {
            return await fetch(url, options);
        }
    }
}

// 使用示例
const advancedDebugger = new AdvancedDebugger({
    enabled: true,
    filters: ['database', 'api', 'business-logic'],
    outputFile: './debug.log'
});

// 在服务中使用
class UserService {
    constructor(db, debugger) {
        this.db = db;
        this.debugger = debugger;
    }

    async getUserById(id) {
        return await this.debugger.debugQuery(
            'SELECT * FROM users WHERE id = $1',
            [id],
            this.db
        );
    }

    async createUser(userData) {
        return await this.debugger.asyncLog(
            async () => {
                const result = await this.db.query(
                    'INSERT INTO users (name, email) VALUES ($1, $2) RETURNING *',
                    [userData.name, userData.email]
                );
                return result.rows[0];
            },
            'createUser'
        );
    }
}
```

### 性能分析工具

**内置性能分析：**
```javascript
// 性能分析工具类
class PerformanceAnalyzer {
    constructor() {
        this.metrics = new Map();
        this.timers = new Map();
    }

    // 启动计时器
    startTimer(label) {
        this.timers.set(label, process.hrtime());
    }

    // 停止计时器并记录
    stopTimer(label) {
        const startTime = this.timers.get(label);
        if (!startTime) return null;

        const diff = process.hrtime(startTime);
        const nanoseconds = diff[0] * 1e9 + diff[1];
        const milliseconds = nanoseconds / 1e6;

        this.timers.delete(label);
        
        if (!this.metrics.has(label)) {
            this.metrics.set(label, []);
        }
        
        this.metrics.get(label).push(milliseconds);
        return milliseconds;
    }

    // 获取统计信息
    getStats(label) {
        const times = this.metrics.get(label);
        if (!times || times.length === 0) return null;

        const sorted = [...times].sort((a, b) => a - b);
        const sum = times.reduce((a, b) => a + b, 0);
        const avg = sum / times.length;
        const min = sorted[0];
        const max = sorted[sorted.length - 1];
        const median = sorted[Math.floor(sorted.length / 2)];

        return {
            count: times.length,
            avg: avg.toFixed(2),
            min: min.toFixed(2),
            max: max.toFixed(2),
            median: median.toFixed(2),
            total: sum.toFixed(2)
        };
    }

    // 获取所有统计信息
    getAllStats() {
        const stats = {};
        for (const [label, times] of this.metrics) {
            stats[label] = this.getStats(label);
        }
        return stats;
    }

    // 清除指标
    clearMetrics() {
        this.metrics.clear();
        this.timers.clear();
    }

    // 性能装饰器
    performanceMonitor(label) {
        return (target, propertyName, descriptor) => {
            const method = descriptor.value;
            
            descriptor.value = async function(...args) {
                const analyzer = new PerformanceAnalyzer();
                analyzer.startTimer(label);
                
                try {
                    const result = await method.apply(this, args);
                    const duration = analyzer.stopTimer(label);
                    
                    console.log(`${label}: ${duration.toFixed(2)}ms`);
                    return result;
                } catch (error) {
                    analyzer.stopTimer(label);
                    throw error;
                }
            };
            
            return descriptor;
        };
    }
}

// 使用示例
const perfAnalyzer = new PerformanceAnalyzer();

// 手动性能分析
perfAnalyzer.startTimer('database-query');
// 执行数据库查询
const users = await db.query('SELECT * FROM users LIMIT 1000');
perfAnalyzer.stopTimer('database-query');

console.log('查询性能统计:', perfAnalyzer.getStats('database-query'));

// 装饰器使用
class UserService {
    @perfAnalyzer.performanceMonitor('getUserById')
    async getUserById(id) {
        return await this.db.query('SELECT * FROM users WHERE id = $1', [id]);
    }

    @perfAnalyzer.performanceMonitor('createUser')
    async createUser(userData) {
        return await this.db.query(
            'INSERT INTO users (name, email) VALUES ($1, $2) RETURNING *',
            [userData.name, userData.email]
        );
    }
}
```

**外部性能分析工具：**
```javascript
// 使用 clinic.js 进行性能分析
const Clinic = require('clinic');
const { promisify } = require('util');
const { spawn } = require('child_process');

class ClinicAnalyzer {
    constructor() {
        this.clinic = new Clinic();
    }

    async analyzeDoctor(scriptPath, options = {}) {
        const collect = promisify(this.clinic.doctor.bind(this.clinic));
        const html = promisify(this.clinic.doctor.html.bind(this.clinic.doctor));
        
        try {
            // 收集数据
            const dataPath = await collect([process.execPath, scriptPath], {
                duration: options.duration || 30000,
                ...options
            });
            
            // 生成报告
            const htmlPath = await html(dataPath, {
                outputDir: options.outputDir || './clinic-reports'
            });
            
            console.log(`性能报告生成在: ${htmlPath}`);
            return htmlPath;
        } catch (error) {
            console.error('性能分析失败:', error);
            throw error;
        }
    }

    async analyzeBubbleprof(scriptPath, options = {}) {
        const collect = promisify(this.clinic.bubbleprof.bind(this.clinic));
        const html = promisify(this.clinic.bubbleprof.html.bind(this.clinic.bubbleprof));
        
        try {
            const dataPath = await collect([process.execPath, scriptPath], options);
            const htmlPath = await html(dataPath, {
                outputDir: options.outputDir || './clinic-reports'
            });
            
            console.log(`BubbleProf 报告生成在: ${htmlPath}`);
            return htmlPath;
        } catch (error) {
            console.error('BubbleProf 分析失败:', error);
            throw error;
        }
    }

    async analyzeFlame(scriptPath, options = {}) {
        const collect = promisify(this.clinic.flame.bind(this.clinic));
        const html = promisify(this.clinic.flame.html.bind(this.clinic.flame));
        
        try {
            const dataPath = await collect([process.execPath, scriptPath], options);
            const htmlPath = await html(dataPath, {
                outputDir: options.outputDir || './clinic-reports'
            });
            
            console.log(`火焰图报告生成在: ${htmlPath}`);
            return htmlPath;
        } catch (error) {
            console.error('火焰图分析失败:', error);
            throw error;
        }
    }
}

// 使用 0x 生成火焰图
class FlameGraphAnalyzer {
    async generateFlameGraph(scriptPath, options = {}) {
        return new Promise((resolve, reject) => {
            const args = [
                '--output-dir', options.outputDir || './flamegraphs',
                scriptPath
            ];
            
            if (options.duration) {
                args.unshift('--duration', options.duration.toString());
            }
            
            const child = spawn('0x', args, { stdio: 'inherit' });
            
            child.on('close', (code) => {
                if (code === 0) {
                    console.log('火焰图生成完成');
                    resolve();
                } else {
                    reject(new Error(`火焰图生成失败，退出码: ${code}`));
                }
            });
        });
    }
}

// 内存泄漏检测
class MemoryLeakDetector {
    constructor() {
        this.snapshots = [];
    }

    takeHeapSnapshot() {
        const snapshot = {
            timestamp: Date.now(),
            memory: process.memoryUsage(),
            heap: v8.getHeapStatistics()
        };
        
        this.snapshots.push(snapshot);
        return snapshot;
    }

    analyzeMemoryGrowth() {
        if (this.snapshots.length < 2) {
            return null;
        }
        
        const first = this.snapshots[0];
        const last = this.snapshots[this.snapshots.length - 1];
        
        const growth = {
            heapUsed: last.memory.heapUsed - first.memory.heapUsed,
            heapTotal: last.memory.heapTotal - first.memory.heapTotal,
            external: last.memory.external - first.memory.external,
            duration: last.timestamp - first.timestamp
        };
        
        return {
            growth,
            isLeaking: growth.heapUsed > 10 * 1024 * 1024, // 超过10MB增长
            snapshots: this.snapshots.length
        };
    }

    startMonitoring(interval = 5000) {
        setInterval(() => {
            const snapshot = this.takeHeapSnapshot();
            console.log('内存快照:', {
                heapUsed: `${Math.round(snapshot.memory.heapUsed / 1024 / 1024)} MB`,
                heapTotal: `${Math.round(snapshot.memory.heapTotal / 1024 / 1024)} MB`
            });
        }, interval);
    }
}

// 使用示例
const memoryDetector = new MemoryLeakDetector();
memoryDetector.startMonitoring(10000); // 每10秒记录一次

// 在应用中定期检查
setInterval(() => {
    const analysis = memoryDetector.analyzeMemoryGrowth();
    if (analysis && analysis.isLeaking) {
        console.warn('检测到可能的内存泄漏:', analysis.growth);
    }
}, 30000);
```

## 20.2 项目架构

### MVC 架构模式

**经典 MVC 实现：**
```javascript
// models/User.js
class User {
    constructor(data) {
        this.id = data.id;
        this.name = data.name;
        this.email = data.email;
        this.createdAt = data.createdAt || new Date();
    }

    // 验证方法
    static validate(userData) {
        const errors = [];
        
        if (!userData.name || userData.name.trim().length < 2) {
            errors.push('姓名至少需要2个字符');
        }
        
        if (!userData.email || !/\S+@\S+\.\S+/.test(userData.email)) {
            errors.push('请输入有效的邮箱地址');
        }
        
        return errors;
    }

    // 数据库操作方法
    static async findById(id, db) {
        const result = await db.query('SELECT * FROM users WHERE id = $1', [id]);
        return result.rows[0] ? new User(result.rows[0]) : null;
    }

    static async findAll(db, options = {}) {
        const { limit = 10, offset = 0, sortBy = 'id', sortOrder = 'ASC' } = options;
        const result = await db.query(
            `SELECT * FROM users ORDER BY ${sortBy} ${sortOrder} LIMIT $1 OFFSET $2`,
            [limit, offset]
        );
        return result.rows.map(row => new User(row));
    }

    static async create(userData, db) {
        const errors = this.validate(userData);
        if (errors.length > 0) {
            throw new Error(errors.join(', '));
        }

        const result = await db.query(
            'INSERT INTO users (name, email, created_at) VALUES ($1, $2, $3) RETURNING *',
            [userData.name, userData.email, new Date()]
        );
        
        return new User(result.rows[0]);
    }

    static async update(id, userData, db) {
        const updates = [];
        const values = [];
        let index = 1;

        Object.keys(userData).forEach(key => {
            if (key !== 'id' && userData[key] !== undefined) {
                updates.push(`${key} = $${index}`);
                values.push(userData[key]);
                index++;
            }
        });

        if (updates.length === 0) {
            throw new Error('没有要更新的数据');
        }

        values.push(id);
        const result = await db.query(
            `UPDATE users SET ${updates.join(', ')}, updated_at = $${index} WHERE id = $${index + 1} RETURNING *`,
            values
        );

        return result.rows[0] ? new User(result.rows[0]) : null;
    }

    static async delete(id, db) {
        const result = await db.query('DELETE FROM users WHERE id = $1 RETURNING *', [id]);
        return result.rowCount > 0;
    }
}

// views/userView.js
class UserView {
    static renderUser(user) {
        return {
            id: user.id,
            name: user.name,
            email: user.email,
            createdAt: user.createdAt.toISOString()
        };
    }

    static renderUsers(users) {
        return users.map(user => this.renderUser(user));
    }

    static renderError(error) {
        return {
            error: error.message,
            timestamp: new Date().toISOString()
        };
    }

    static renderSuccess(message, data = null) {
        const response = { message };
        if (data) {
            response.data = data;
        }
        return response;
    }
}

// controllers/userController.js
class UserController {
    constructor(userModel, userView) {
        this.User = userModel;
        this.UserView = userView;
    }

    async getAllUsers(req, res) {
        try {
            const { page = 1, limit = 10, sortBy = 'id', sortOrder = 'ASC' } = req.query;
            const offset = (page - 1) * limit;
            
            const users = await this.User.findAll(req.db, { limit, offset, sortBy, sortOrder });
            const totalCount = await this.User.count(req.db);
            
            res.json({
                data: this.UserView.renderUsers(users),
                pagination: {
                    page: parseInt(page),
                    limit: parseInt(limit),
                    total: totalCount,
                    pages: Math.ceil(totalCount / limit)
                }
            });
        } catch (error) {
            res.status(500).json(this.UserView.renderError(error));
        }
    }

    async getUserById(req, res) {
        try {
            const { id } = req.params;
            const user = await this.User.findById(id, req.db);
            
            if (!user) {
                return res.status(404).json(this.UserView.renderError(new Error('用户未找到')));
            }
            
            res.json(this.UserView.renderUser(user));
        } catch (error) {
            res.status(500).json(this.UserView.renderError(error));
        }
    }

    async createUser(req, res) {
        try {
            const user = await this.User.create(req.body, req.db);
            res.status(201).json(this.UserView.renderUser(user));
        } catch (error) {
            res.status(400).json(this.UserView.renderError(error));
        }
    }

    async updateUser(req, res) {
        try {
            const { id } = req.params;
            const user = await this.User.update(id, req.body, req.db);
            
            if (!user) {
                return res.status(404).json(this.UserView.renderError(new Error('用户未找到')));
            }
            
            res.json(this.UserView.renderUser(user));
        } catch (error) {
            res.status(400).json(this.UserView.renderError(error));
        }
    }

    async deleteUser(req, res) {
        try {
            const { id } = req.params;
            const deleted = await this.User.delete(id, req.db);
            
            if (!deleted) {
                return res.status(404).json(this.UserView.renderError(new Error('用户未找到')));
            }
            
            res.json(this.UserView.renderSuccess('用户删除成功'));
        } catch (error) {
            res.status(500).json(this.UserView.renderError(error));
        }
    }
}

// routes/userRoutes.js
const express = require('express');
const router = express.Router();

// 依赖注入
let userController;

function setUserController(controller) {
    userController = controller;
}

router.get('/', (req, res) => userController.getAllUsers(req, res));
router.get('/:id', (req, res) => userController.getUserById(req, res));
router.post('/', (req, res) => userController.createUser(req, res));
router.put('/:id', (req, res) => userController.updateUser(req, res));
router.delete('/:id', (req, res) => userController.deleteUser(req, res));

module.exports = { router, setUserController };

// app.js
const express = require('express');
const { Pool } = require('pg');
const { router, setUserController } = require('./routes/userRoutes');
const User = require('./models/User');
const UserView = require('./views/UserView');
const UserController = require('./controllers/UserController');

const app = express();
const pool = new Pool({
    user: 'postgres',
    host: 'localhost',
    database: 'myapp',
    password: 'password',
    port: 5432,
});

// 数据库连接中间件
app.use((req, res, next) => {
    req.db = pool;
    next();
});

app.use(express.json());

// 初始化控制器
const userController = new UserController(User, UserView);
setUserController(userController);

app.use('/api/users', router);

app.listen(3000, () => {
    console.log('服务器运行在端口 3000');
});
```

### 分层架构设计

**分层架构实现：**
```javascript
// layers/presentation/controllers/userController.js
class UserController {
    constructor(userService) {
        this.userService = userService;
    }

    async getAllUsers(req, res) {
        try {
            const { page, limit, sortBy, sortOrder } = req.query;
            const result = await this.userService.getUsers({
                page: parseInt(page) || 1,
                limit: parseInt(limit) || 10,
                sortBy: sortBy || 'id',
                sortOrder: sortOrder || 'ASC'
            });
            
            res.json(result);
        } catch (error) {
            this.handleError(res, error, 500);
        }
    }

    async getUserById(req, res) {
        try {
            const { id } = req.params;
            const user = await this.userService.getUserById(id);
            
            if (!user) {
                return this.handleError(res, new Error('用户未找到'), 404);
            }
            
            res.json(user);
        } catch (error) {
            this.handleError(res, error, 500);
        }
    }

    async createUser(req, res) {
        try {
            const user = await this.userService.createUser(req.body);
            res.status(201).json(user);
        } catch (error) {
            this.handleError(res, error, 400);
        }
    }

    handleError(res, error, statusCode) {
        console.error('Controller Error:', error);
        res.status(statusCode).json({
            error: error.message,
            timestamp: new Date().toISOString()
        });
    }
}

// layers/application/services/userService.js
class UserService {
    constructor(userRepository, eventPublisher) {
        this.userRepository = userRepository;
        this.eventPublisher = eventPublisher;
    }

    async getUsers(options) {
        // 业务逻辑验证
        if (options.page < 1) throw new Error('页码必须大于0');
        if (options.limit < 1 || options.limit > 100) throw new Error('每页数量必须在1-100之间');

        const users = await this.userRepository.findAll(options);
        const totalCount = await this.userRepository.count();
        
        return {
            data: users,
            pagination: {
                page: options.page,
                limit: options.limit,
                total: totalCount,
                pages: Math.ceil(totalCount / options.limit)
            }
        };
    }

    async getUserById(id) {
        if (!id || isNaN(id)) throw new Error('无效的用户ID');
        
        const user = await this.userRepository.findById(id);
        if (user) {
            // 业务逻辑处理
            user.lastAccessed = new Date();
            await this.userRepository.updateLastAccessed(id, user.lastAccessed);
        }
        
        return user;
    }

    async createUser(userData) {
        // 业务规则验证
        this.validateUserData(userData);
        
        // 检查邮箱是否已存在
        const existingUser = await this.userRepository.findByEmail(userData.email);
        if (existingUser) {
            throw new Error('邮箱已被使用');
        }

        // 创建用户
        const user = await this.userRepository.create(userData);
        
        // 发布用户创建事件
        await this.eventPublisher.publish('user.created', {
            userId: user.id,
            email: user.email,
            timestamp: new Date()
        });
        
        return user;
    }

    validateUserData(userData) {
        const errors = [];
        
        if (!userData.name || userData.name.trim().length < 2) {
            errors.push('姓名至少需要2个字符');
        }
        
        if (!userData.email || !this.isValidEmail(userData.email)) {
            errors.push('请输入有效的邮箱地址');
        }
        
        if (!userData.password || userData.password.length < 6) {
            errors.push('密码至少需要6个字符');
        }
        
        if (errors.length > 0) {
            throw new Error(errors.join(', '));
        }
    }

    isValidEmail(email) {
        return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
    }
}

// layers/domain/repositories/userRepository.js
class UserRepository {
    constructor(database) {
        this.db = database;
    }

    async findAll(options = {}) {
        const { page = 1, limit = 10, sortBy = 'id', sortOrder = 'ASC' } = options;
        const offset = (page - 1) * limit;
        
        const result = await this.db.query(
            `SELECT id, name, email, created_at, last_accessed 
             FROM users 
             ORDER BY ${sortBy} ${sortOrder} 
             LIMIT $1 OFFSET $2`,
            [limit, offset]
        );
        
        return result.rows;
    }

    async findById(id) {
        const result = await this.db.query(
            'SELECT id, name, email, created_at, last_accessed FROM users WHERE id = $1',
            [id]
        );
        
        return result.rows[0] || null;
    }

    async findByEmail(email) {
        const result = await this.db.query(
            'SELECT id, name, email, created_at FROM users WHERE email = $1',
            [email]
        );
        
        return result.rows[0] || null;
    }

    async create(userData) {
        const result = await this.db.query(
            `INSERT INTO users (name, email, password, created_at) 
             VALUES ($1, $2, $3, $4) 
             RETURNING id, name, email, created_at`,
            [userData.name, userData.email, userData.password, new Date()]
        );
        
        return result.rows[0];
    }

    async updateLastAccessed(id, lastAccessed) {
        await this.db.query(
            'UPDATE users SET last_accessed = $1 WHERE id = $2',
            [lastAccessed, id]
        );
    }

    async count() {
        const result = await this.db.query('SELECT COUNT(*) as count FROM users');
        return parseInt(result.rows[0].count);
    }
}

// layers/infrastructure/database/postgresql.js
const { Pool } = require('pg');

class PostgreSQLDatabase {
    constructor(config) {
        this.pool = new Pool(config);
    }

    async query(text, params) {
        const start = Date.now();
        const res = await this.pool.query(text, params);
        const duration = Date.now() - start;
        
        console.log('执行查询', { text, duration, rows: res.rowCount });
        return res;
    }

    async getClient() {
        return await this.pool.connect();
    }

    async close() {
        await this.pool.end();
    }
}

// layers/infrastructure/events/eventPublisher.js
const EventEmitter = require('events');

class EventPublisher extends EventEmitter {
    constructor() {
        super();
        this.setMaxListeners(20);
    }

    async publish(eventName, eventData) {
        console.log(`发布事件: ${eventName}`, eventData);
        this.emit(eventName, eventData);
        
        // 异步处理事件
        setImmediate(() => {
            this.emit(`${eventName}.async`, eventData);
        });
    }

    subscribe(eventName, handler) {
        this.on(eventName, handler);
        return () => this.unsubscribe(eventName, handler);
    }

    unsubscribe(eventName, handler) {
        this.removeListener(eventName, this);
    }
}

// 应用启动配置
const express = require('express');
const app = express();

// 依赖注入容器
class DIContainer {
    constructor() {
        this.services = new Map();
    }

    register(name, factory) {
        this.services.set(name, factory);
    }

    resolve(name) {
        const factory = this.services.get(name);
        if (!factory) {
            throw new Error(`Service ${name} not found`);
        }
        return factory(this);
    }
}

// 配置依赖注入
const container = new DIContainer();

container.register('database', () => {
    return new PostgreSQLDatabase({
        user: 'postgres',
        host: 'localhost',
        database: 'myapp',
        password: 'password',
        port: 5432,
    });
});

container.register('eventPublisher', () => {
    return new EventPublisher();
});

container.register('userRepository', (container) => {
    return new UserRepository(container.resolve('database'));
});

container.register('userService', (container) => {
    return new UserService(
        container.resolve('userRepository'),
        container.resolve('eventPublisher')
    );
});

container.register('userController', (container) => {
    return new UserController(container.resolve('userService'));
});

// 初始化应用
const userController = container.resolve('userController');

app.use(express.json());
app.get('/api/users', (req, res) => userController.getAllUsers(req, res));
app.get('/api/users/:id', (req, res) => userController.getUserById(req, res));
app.post('/api/users', (req, res) => userController.createUser(req, res));

app.listen(3000, () => {
    console.log('分层架构应用启动在端口 3000');
});
```

### 微服务架构

**微服务基础框架：**
```javascript
// microservices/framework/service.js
const express = require('express');
const axios = require('axios');
const redis = require('redis');

class MicroService {
    constructor(name, options = {}) {
        this.name = name;
        this.port = options.port || 3000;
        this.app = express();
        this.dependencies = options.dependencies || [];
        this.setupMiddleware();
    }

    setupMiddleware() {
        this.app.use(express.json());
        this.app.use(express.urlencoded({ extended: true }));
        
        // 健康检查
        this.app.get('/health', (req, res) => {
            res.json({
                status: 'healthy',
                service: this.name,
                timestamp: new Date().toISOString(),
                dependencies: this.dependencies
            });
        });
        
        // 请求追踪中间件
        this.app.use((req, res, next) => {
            req.requestId = req.headers['x-request-id'] || require('crypto').randomBytes(16).toString('hex');
            req.startTime = Date.now();
            
            res.on('finish', () => {
                const duration = Date.now() - req.startTime;
                console.log(`${this.name} - ${req.method} ${req.path} - ${res.statusCode} - ${duration}ms - ${req.requestId}`);
            });
            
            next();
        });
    }

    // 服务发现
    async discoverService(serviceName) {
        try {
            const response = await axios.get(`http://service-registry:3000/services/${serviceName}`);
            return response.data;
        } catch (error) {
            throw new Error(`无法发现服务 ${serviceName}: ${error.message}`);
        }
    }

    // 调用其他服务
    async callService(serviceName, path, options = {}) {
        try {
            const service = await this.discoverService(serviceName);
            const url = `http://${service.host}:${service.port}${path}`;
            
            const response = await axios({
                method: options.method || 'GET',
                url: url,
                data: options.data,
                headers: {
                    'x-request-id': options.requestId,
                    ...options.headers
                },
                timeout: options.timeout || 5000
            });
            
            return response.data;
        } catch (error) {
            console.error(`调用服务 ${serviceName} 失败:`, error.message);
            throw error;
        }
    }

    // 错误处理中间件
    setupErrorHandler() {
        this.app.use((err, req, res, next) => {
            console.error(`${this.name} 错误:`, err);
            
            res.status(err.status || 500).json({
                error: err.message || '内部服务器错误',
                requestId: req.requestId,
                service: this.name
            });
        });
    }

    start() {
        this.setupErrorHandler();
        this.app.listen(this.port, () => {
            console.log(`${this.name} 服务启动在端口 ${this.port}`);
        });
    }
}

// 用户服务
class UserService extends MicroService {
    constructor() {
        super('user-service', {
            port: 3001,
            dependencies: ['database-service', 'auth-service']
        });
        this.setupRoutes();
    }

    setupRoutes() {
        this.app.get('/users', async (req, res) => {
            try {
                const users = await this.getUsers();
                res.json(users);
            } catch (error) {
                res.status(500).json({ error: error.message });
            }
        });

        this.app.get('/users/:id', async (req, res) => {
            try {
                const user = await this.getUserById(req.params.id);
                if (!user) {
                    return res.status(404).json({ error: '用户未找到' });
                }
                res.json(user);
            } catch (error) {
                res.status(500).json({ error: error.message });
            }
        });

        this.app.post('/users', async (req, res) => {
            try {
                const user = await this.createUser(req.body);
                res.status(201).json(user);
            } catch (error) {
                res.status(400).json({ error: error.message });
            }
        });
    }

    async getUsers() {
        return [
            { id: 1, name: 'Alice', email: 'alice@example.com' },
            { id: 2, name: 'Bob', email: 'bob@example.com' }
        ];
    }

    async getUserById(id) {
        const users = await this.getUsers();
        return users.find(user => user.id == id);
    }

    async createUser(userData) {
        return {
            id: Date.now(),
            ...userData,
            createdAt: new Date().toISOString()
        };
    }
}

// 订单服务
class OrderService extends MicroService {
    constructor() {
        super('order-service', {
            port: 3002,
            dependencies: ['user-service', 'payment-service']
        });
        this.setupRoutes();
    }

    setupRoutes() {
        this.app.get('/orders', async (req, res) => {
            try {
                const orders = await this.getOrders();
                res.json(orders);
            } catch (error) {
                res.status(500).json({ error: error.message });
            }
        });

        this.app.get('/orders/:id', async (req, res) => {
            try {
                const order = await this.getOrderById(req.params.id);
                if (!order) {
                    return res.status(404).json({ error: '订单未找到' });
                }
                res.json(order);
            } catch (error) {
                res.status(500).json({ error: error.message });
            }
        });

        this.app.post('/orders', async (req, res) => {
            try {
                // 验证用户
                const user = await this.callService('user-service', `/users/${req.body.userId}`);
                
                const order = await this.createOrder(req.body);
                res.status(201).json(order);
            } catch (error) {
                res.status(400).json({ error: error.message });
            }
        });
    }

    async getOrders() {
        return [
            { id: 1, userId: 1, total: 100, status: 'pending' },
            { id: 2, userId: 2, total: 200, status: 'completed' }
        ];
    }

    async getOrderById(id) {
        const orders = await this.getOrders();
        return orders.find(order => order.id == id);
    }

    async createOrder(orderData) {
        return {
            id: Date.now(),
            ...orderData,
            status: 'pending',
            createdAt: new Date().toISOString()
        };
    }
}

// API 网关
class ApiGateway extends MicroService {
    constructor() {
        super('api-gateway', { port: 3000 });
        this.serviceRegistry = new Map();
        this.setupRoutes();
    }

    setupRoutes() {
        // 用户服务路由
        this.app.use('/api/users', async (req, res) => {
            await this.proxyToService('user-service', req, res);
        });

        // 订单服务路由
        this.app.use('/api/orders', async (req, res) => {
            await this.proxyToService('order-service', req, res);
        });
    }

    async proxyToService(serviceName, req, res) {
        try {
            const service = await this.discoverService(serviceName);
            const url = `http://${service.host}:${service.port}${req.url}`;
            
            const response = await axios({
                method: req.method,
                url: url,
                data: req.body,
                headers: req.headers,
                timeout: 10000
            });
            
            res.status(response.status).json(response.data);
        } catch (error) {
            console.error('代理请求失败:', error);
            res.status(502).json({ error: '服务不可用' });
        }
    }

    async discoverService(serviceName) {
        // 简单的服务发现实现
        const services = {
            'user-service': { host: 'localhost', port: 3001 },
            'order-service': { host: 'localhost', port: 3002 }
        };
        
        return services[serviceName];
    }
}

// 启动服务
async function startServices() {
    const userService = new UserService();
    const orderService = new OrderService();
    const apiGateway = new ApiGateway();
    
    userService.start();
    orderService.start();
    apiGateway.start();
}

startServices().catch(console.error);
```

### 无服务器架构

**Serverless 函数实现：**
```javascript
// serverless/functions/user/handler.js
const AWS = require('aws-sdk');
const dynamodb = new AWS.DynamoDB.DocumentClient();

class UserHandler {
    static async createUser(event) {
        try {
            const userData = JSON.parse(event.body);
            
            // 验证输入
            if (!userData.name || !userData.email) {
                return {
                    statusCode: 400,
                    headers: {
                        'Content-Type': 'application/json',
                        'Access-Control-Allow-Origin': '*'
                    },
                    body: JSON.stringify({
                        error: '姓名和邮箱是必填项'
                    })
                };
            }

            // 创建用户
            const user = {
                id: require('uuid').v4(),
                name: userData.name,
                email: userData.email,
                createdAt: new Date().toISOString()
            };

            await dynamodb.put({
                TableName: process.env.USERS_TABLE,
                Item: user
            }).promise();

            return {
                statusCode: 201,
                headers: {
                    'Content-Type': 'application/json',
                    'Access-Control-Allow-Origin': '*'
                },
                body: JSON.stringify(user)
            };
        } catch (error) {
            console.error('创建用户失败:', error);
            
            return {
                statusCode: 500,
                headers: {
                    'Content-Type': 'application/json',
                    'Access-Control-Allow-Origin': '*'
                },
                body: JSON.stringify({
                    error: '内部服务器错误'
                })
            };
        }
    }

    static async getUser(event) {
        try {
            const userId = event.pathParameters.id;
            
            const result = await dynamodb.get({
                TableName: process.env.USERS_TABLE,
                Key: { id: userId }
            }).promise();

            if (!result.Item) {
                return {
                    statusCode: 404,
                    headers: {
                        'Content-Type': 'application/json',
                        'Access-Control-Allow-Origin': '*'
                    },
                    body: JSON.stringify({
                        error: '用户未找到'
                    })
                };
            }

            return {
                statusCode: 200,
                headers: {
                    'Content-Type': 'application/json',
                    'Access-Control-Allow-Origin': '*'
                },
                body: JSON.stringify(result.Item)
            };
        } catch (error) {
            console.error('获取用户失败:', error);
            
            return {
                statusCode: 500,
                headers: {
                    'Content-Type': 'application/json',
                    'Access-Control-Allow-Origin': '*'
                },
                body: JSON.stringify({
                    error: '内部服务器错误'
                })
            };
        }
    }

    static async listUsers(event) {
        try {
            const result = await dynamodb.scan({
                TableName: process.env.USERS_TABLE
            }).promise();

            return {
                statusCode: 200,
                headers: {
                    'Content-Type': 'application/json',
                    'Access-Control-Allow-Origin': '*'
                },
                body: JSON.stringify({
                    data: result.Items,
                    count: result.Count
                })
            };
        } catch (error) {
            console.error('列出用户失败:', error);
            
            return {
                statusCode: 500,
                headers: {
                    'Content-Type': 'application/json',
                    'Access-Control-Allow-Origin': '*'
                },
                body: JSON.stringify({
                    error: '内部服务器错误'
                })
            };
        }
    }
}

module.exports = UserHandler;
```

**Serverless 配置文件：**
```yaml
# serverless.yml
service: user-service

provider:
  name: aws
  runtime: nodejs18.x
  region: us-east-1
  environment:
    USERS_TABLE: ${self:service}-${opt:stage, self:provider.stage}-users
  iamRoleStatements:
    - Effect: Allow
      Action:
        - dynamodb:Query
        - dynamodb:Scan
        - dynamodb:GetItem
        - dynamodb:PutItem
        - dynamodb:UpdateItem
        - dynamodb:DeleteItem
      Resource: "arn:aws:dynamodb:${opt:region, self:provider.region}:*:table/${self:provider.environment.USERS_TABLE}"

functions:
  createUser:
    handler: functions/user/handler.createUser
    events:
      - http:
          path: users
          method: post
          cors: true

  getUser:
    handler: functions/user/handler.getUser
    events:
      - http:
          path: users/{id}
          method: get
          cors: true

  listUsers:
    handler: functions/user/handler.listUsers
    events:
      - http:
          path: users
          method: get
          cors: true

resources:
  Resources:
    UsersTable:
      Type: AWS::DynamoDB::Table
      Properties:
        TableName: ${self:provider.environment.USERS_TABLE}
        AttributeDefinitions:
          - AttributeName: id
            AttributeType: S
        KeySchema:
          - AttributeName: id
            KeyType: HASH
        BillingMode: PAY_PER_REQUEST

plugins:
  - serverless-offline
  - serverless-webpack

custom:
  webpack:
    webpackConfig: ./webpack.config.js
    includeModules: true
```

**本地开发工具：**
```javascript
// serverless/local/server.js
const express = require('express');
const bodyParser = require('body-parser');
const UserHandler = require('../functions/user/handler');

const app = express();
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));

// 模拟 Serverless 环境
const createEvent = (method, path, body, pathParameters = {}) => ({
    httpMethod: method,
    path: path,
    body: body ? JSON.stringify(body) : null,
    pathParameters: pathParameters,
    headers: {
        'Content-Type': 'application/json'
    }
});

// 用户路由
app.post('/users', async (req, res) => {
    const event = createEvent('POST', '/users', req.body);
    const response = await UserHandler.createUser(event);
    res.status(response.statusCode).json(JSON.parse(response.body));
});

app.get('/users/:id', async (req, res) => {
    const event = createEvent('GET', `/users/${req.params.id}`, null, { id: req.params.id });
    const response = await UserHandler.getUser(event);
    res.status(response.statusCode).json(JSON.parse(response.body));
});

app.get('/users', async (req, res) => {
    const event = createEvent('GET', '/users');
    const response = await UserHandler.listUsers(event);
    res.status(response.statusCode).json(JSON.parse(response.body));
});

// 错误处理中间件
app.use((err, req, res, next) => {
    console.error('服务器错误:', err);
    res.status(500).json({ error: '内部服务器错误' });
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
    console.log(`本地开发服务器运行在端口 ${PORT}`);
    console.log('可用端点:');
    console.log('  POST   /users     - 创建用户');
    console.log('  GET    /users/:id - 获取用户');
    console.log('  GET    /users     - 列出用户');
});
```

## 20.3 最佳实践

### 代码规范和风格

**ESLint 配置：**
```javascript
// .eslintrc.js
module.exports = {
    env: {
        browser: true,
        es2021: true,
        node: true,
        jest: true
    },
    extends: [
        'eslint:recommended',
        '@typescript-eslint/recommended',
        'plugin:import/errors',
        'plugin:import/warnings',
        'plugin:import/typescript',
        'plugin:jest/recommended',
        'plugin:jest/style',
        'plugin:sonarjs/recommended'
    ],
    parser: '@typescript-eslint/parser',
    parserOptions: {
        ecmaFeatures: {
            jsx: true
        },
        ecmaVersion: 12,
        sourceType: 'module'
    },
    plugins: [
        '@typescript-eslint',
        'import',
        'jest',
        'sonarjs',
        'unused-imports'
    ],
    settings: {
        'import/resolver': {
            node: {
                paths: ['src'],
                extensions: ['.js', '.jsx', '.ts', '.tsx']
            }
        }
    },
    rules: {
        // 基本规则
        'indent': ['error', 2],
        'linebreak-style': ['error', 'unix'],
        'quotes': ['error', 'single'],
        'semi': ['error', 'always'],
        
        // 导入规则
        'import/order': [
            'error',
            {
                'groups': ['builtin', 'external', 'internal'],
                'pathGroups': [
                    {
                        'pattern': 'react',
                        'group': 'external',
                        'position': 'before'
                    }
                ],
                'pathGroupsExcludedImportTypes': ['react'],
                'alphabetize': {
                    'order': 'asc',
                    'caseInsensitive': true
                }
            }
        ],
        'import/no-unresolved': 'error',
        'import/named': 'error',
        'import/default': 'error',
        'import/no-self-import': 'error',
        'import/no-cycle': 'error',
        
        // 未使用导入
        'unused-imports/no-unused-imports': 'error',
        'unused-imports/no-unused-vars': [
            'warn',
            {
                'vars': 'all',
                'varsIgnorePattern': '^_',
                'args': 'after-used',
                'argsIgnorePattern': '^_'
            }
        ],
        
        // 复杂度控制
        'complexity': ['warn', 10],
        'max-depth': ['warn', 4],
        'max-lines': ['warn', 300],
        'max-params': ['warn', 3],
        'max-statements': ['warn', 20],
        
        // 代码质量
        'no-console': ['warn', { allow: ['warn', 'error'] }],
        'no-debugger': 'error',
        'no-alert': 'warn',
        'no-var': 'error',
        'prefer-const': 'error',
        'no-duplicate-imports': 'error',
        
        // 风格规则
        'comma-dangle': ['error', 'always-multiline'],
        'object-curly-spacing': ['error', 'always'],
        'array-bracket-spacing': ['error', 'never'],
        'space-before-function-paren': ['error', {
            'asyncArrow': 'always',
            'anonymous': 'never',
            'named': 'never'
        }],
        
        // Jest 规则
        'jest/expect-expect': 'off',
        'jest/valid-title': 'error'
    },
    overrides: [
        {
            files: ['*.test.js', '*.spec.js'],
            env: {
                jest: true
            }
        }
    ]
};
```

**Prettier 配置：**
```javascript
// .prettierrc.js
module.exports = {
    semi: true,
    trailingComma: 'es5',
    singleQuote: true,
    printWidth: 80,
    tabWidth: 2,
    useTabs: false,
    bracketSpacing: true,
    arrowParens: 'avoid',
    endOfLine: 'lf',
    proseWrap: 'preserve'
};
```

**Git Hooks 配置：**
```json
// package.json
{
  "scripts": {
    "lint": "eslint src/**/*.js",
    "lint:fix": "eslint src/**/*.js --fix",
    "format": "prettier --write src/**/*.js",
    "format:check": "prettier --check src/**/*.js",
    "test": "jest",
    "test:watch": "jest --watch",
    "pre-commit": "lint-staged"
  },
  "lint-staged": {
    "*.{js,jsx,ts,tsx}": [
      "eslint --fix",
      "prettier --write",
      "git add"
    ],
    "*.{json,md,yml,yaml}": [
      "prettier --write",
      "git add"
    ]
  },
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged",
      "pre-push": "npm run test"
    }
  }
}
```

### 设计模式应用

**常见设计模式实现：**
```javascript
// 单例模式
class DatabaseConnection {
    constructor() {
        if (DatabaseConnection.instance) {
            return DatabaseConnection.instance;
        }
        
        this.connection = null;
        DatabaseConnection.instance = this;
    }
    
    async connect() {
        if (!this.connection) {
            // 实现数据库连接逻辑
            this.connection = await createConnection();
        }
        return this.connection;
    }
    
    static getInstance() {
        if (!DatabaseConnection.instance) {
            DatabaseConnection.instance = new DatabaseConnection();
        }
        return DatabaseConnection.instance;
    }
}

// 工厂模式
class LoggerFactory {
    static createLogger(type) {
        switch (type) {
            case 'console':
                return new ConsoleLogger();
            case 'file':
                return new FileLogger();
            case 'remote':
                return new RemoteLogger();
            default:
                return new ConsoleLogger();
        }
    }
}

class ConsoleLogger {
    log(message) {
        console.log(`[Console] ${message}`);
    }
}

class FileLogger {
    log(message) {
        // 实现文件日志
        console.log(`[File] ${message}`);
    }
}

class RemoteLogger {
    log(message) {
        // 实现远程日志
        console.log(`[Remote] ${message}`);
    }
}

// 观察者模式
class EventEmitter {
    constructor() {
        this.events = {};
    }
    
    on(event, callback) {
        if (!this.events[event]) {
            this.events[event] = [];
        }
        this.events[event].push(callback);
    }
    
    emit(event, data) {
        if (this.events[event]) {
            this.events[event].forEach(callback => callback(data));
        }
    }
    
    off(event, callback) {
        if (this.events[event]) {
            this.events[event] = this.events[event].filter(cb => cb !== callback);
        }
    }
}

// 策略模式
class PaymentProcessor {
    constructor(strategy) {
        this.strategy = strategy;
    }
    
    setStrategy(strategy) {
        this.strategy = strategy;
    }
    
    async processPayment(amount, data) {
        return await this.strategy.process(amount, data);
    }
}

class CreditCardStrategy {
    async process(amount, data) {
        // 信用卡支付逻辑
        console.log(`使用信用卡支付 ${amount}`);
        return { success: true, transactionId: 'cc_' + Date.now() };
    }
}

class PayPalStrategy {
    async process(amount, data) {
        // PayPal 支付逻辑
        console.log(`使用 PayPal 支付 ${amount}`);
        return { success: true, transactionId: 'pp_' + Date.now() };
    }
}

// 装饰器模式
class UserService {
    async getUser(id) {
        // 基础用户获取逻辑
        return { id, name: 'User' + id };
    }
}

function withLogging(target, propertyName, descriptor) {
    const method = descriptor.value;
    
    descriptor.value = async function(...args) {
        console.log(`调用方法 ${propertyName}，参数:`, args);
        const result = await method.apply(this, args);
        console.log(`方法 ${propertyName} 返回:`, result);
        return result;
    };
    
    return descriptor;
}

function withCache(target, propertyName, descriptor) {
    const method = descriptor.value;
    const cache = new Map();
    
    descriptor.value = async function(...args) {
        const key = JSON.stringify(args);
        if (cache.has(key)) {
            console.log(`从缓存获取 ${propertyName}`);
            return cache.get(key);
        }
        
        const result = await method.apply(this, args);
        cache.set(key, result);
        return result;
    };
    
    return descriptor;
}

class EnhancedUserService extends UserService {
    @withLogging
    @withCache
    async getUser(id) {
        return super.getUser(id);
    }
}

// 使用示例
const userService = new EnhancedUserService();
userService.getUser(1); // 会记录日志并缓存
userService.getUser(1); // 从缓存获取
```

### 文档编写规范

**API 文档生成：**
```javascript
// 使用 JSDoc 编写文档
/**
 * 用户服务类
 * 提供用户相关的业务逻辑处理
 * @class UserService
 */
class UserService {
    /**
     * 创建新用户
     * @param {Object} userData - 用户数据
     * @param {string} userData.name - 用户姓名
     * @param {string} userData.email - 用户邮箱
     * @param {string} userData.password - 用户密码
     * @returns {Promise<Object>} 创建的用户对象
     * @throws {Error} 当用户数据验证失败时抛出错误
     * @example
     * const user = await userService.createUser({
     *   name: '张三',
     *   email: 'zhangsan@example.com',
     *   password: 'password123'
     * });
     */
    async createUser(userData) {
        // 实现逻辑
    }

    /**
     * 根据ID获取用户
     * @param {number} id - 用户ID
     * @returns {Promise<Object|null>} 用户对象或null
     * @example
     * const user = await userService.getUserById(1);
     */
    async getUserById(id) {
        // 实现逻辑
    }
}

// 使用 Swagger/OpenAPI 生成文档
/**
 * @swagger
 * components:
 *   schemas:
 *     User:
 *       type: object
 *       required:
 *         - name
 *         - email
 *       properties:
 *         id:
 *           type: integer
 *           description: 用户ID
 *         name:
 *           type: string
 *           description: 用户姓名
 *         email:
 *           type: string
 *           description: 用户邮箱
 *       example:
 *         id: 1
 *         name: 张三
 *         email: zhangsan@example.com
 */

/**
 * @swagger
 * /api/users:
 *   get:
 *     summary: 获取用户列表
 *     tags: [Users]
 *     parameters:
 *       - in: query
 *         name: page
 *         schema:
 *           type: integer
 *         description: 页码
 *       - in: query
 *         name: limit
 *         schema:
 *           type: integer
 *         description: 每页数量
 *     responses:
 *       200:
 *         description: 成功获取用户列表
 *         content:
 *           application/json:
 *             schema:
 *               type: object
 *               properties:
 *                 data:
 *                   type: array
 *                   items:
 *                     $ref: '#/components/schemas/User'
 *                 pagination:
 *                   type: object
 *                   properties:
 *                     page:
 *                       type: integer
 *                     limit:
 *                       type: integer
 *                     total:
 *                       type: integer
 */
app.get('/api/users', async (req, res) => {
    // 实现逻辑
});
```

**项目文档结构：**
```markdown
# 项目名称

## 项目概述
简要描述项目的目标、功能和价值。

## 技术栈
- Node.js
- Express.js
- PostgreSQL
- Redis
- Docker

## 快速开始

### 环境要求
- Node.js >= 16.0.0
- npm >= 8.0.0
- Docker (可选)

### 安装依赖
```bash
npm install
```

### 环境配置
复制 `.env.example` 文件并重命名为 `.env`，然后根据需要修改配置。

### 启动开发服务器
```bash
npm run dev
```

## 项目结构
```
src/
├── controllers/     # 控制器层
├── models/         # 数据模型层
├── routes/         # 路由定义
├── middleware/     # 中间件
├── utils/          # 工具函数
├── config/         # 配置文件
└── services/       # 业务逻辑层
```

## API 文档
详细的 API 接口文档请参考 [API文档](docs/API.md)。

## 部署指南
### Docker 部署
```bash
docker-compose up -d
```

### 手动部署
1. 安装依赖
2. 配置环境变量
3. 启动服务

## 测试
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

## 贡献指南
请阅读 [CONTRIBUTING.md](CONTRIBUTING.md) 了解如何为项目做贡献。

## 许可证
本项目采用 MIT 许可证 - 请查看 [LICENSE](LICENSE) 文件了解详情。
```

### 团队协作流程

**Git 工作流：**
```bash
# Git 分支策略 (Git Flow)
# 主要分支
main        # 生产环境代码
develop     # 开发环境代码

# 辅助分支
feature/*   # 功能开发分支
release/*   # 发布准备分支
hotfix/*    # 紧急修复分支

# 创建功能分支
git checkout -b feature/user-authentication develop

# 开发完成后
git add .
git commit -m "feat: 实现用户认证功能"
git push origin feature/user-authentication

# 合并到 develop
git checkout develop
git merge --no-ff feature/user-authentication
git push origin develop

# 删除功能分支
git branch -d feature/user-authentication
git push origin --delete feature/user-authentication

# 发布分支
git checkout -b release/1.2.0 develop
# 进行发布前的准备工作（版本号更新、文档更新等）
git checkout main
git merge --no-ff release/1.2.0
git tag -a v1.2.0 -m "Release version 1.2.0"
git push origin main --tags

git checkout develop
git merge --no-ff release/1.2.0
git push origin develop

git branch -d release/1.2.0

# 紧急修复
git checkout -b hotfix/critical-bug main
# 修复问题
git checkout main
git merge --no-ff hotfix/critical-bug
git tag -a v1.2.1 -m "Hotfix version 1.2.1"
git push origin main --tags

git checkout develop
git merge --no-ff hotfix/critical-bug
git push origin develop

git branch -d hotfix/critical-bug
```

**代码审查流程：**
```markdown
# 代码审查清单

## 功能性审查
- [ ] 代码是否实现了预期功能
- [ ] 是否有适当的错误处理
- [ ] 边界条件是否考虑充分
- [ ] 性能是否满足要求

## 代码质量审查
- [ ] 代码是否遵循团队编码规范
- [ ] 变量命名是否清晰有意义
- [ ] 函数是否单一职责
- [ ] 是否有重复代码需要重构
- [ ] 注释是否清晰准确

## 安全性审查
- [ ] 是否有SQL注入风险
- [ ] 是否有XSS攻击风险
- [ ] 敏感信息是否妥善处理
- [ ] 认证授权是否正确实现

## 测试审查
- [ ] 是否有足够的单元测试
- [ ] 测试覆盖率是否达标
- [ ] 测试用例是否覆盖边界条件
- [ ] 集成测试是否通过

## 文档审查
- [ ] API文档是否更新
- [ ] 代码注释是否完整
- [ ] README是否需要更新
```

**持续集成/持续部署 (CI/CD)：**
```yaml
# .github/workflows/ci.yml
name: CI/CD Pipeline

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main, develop ]

jobs:
  test:
    runs-on: ubuntu-latest
    
    strategy:
      matrix:
        node-version: [16.x, 18.x]
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v3
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'
    
    - name: Install dependencies
      run: npm ci
    
    - name: Run lint
      run: npm run lint
    
    - name: Run tests
      run: npm run test:coverage
    
    - name: Upload coverage to Codecov
      uses: codecov/codecov-action@v3
      with:
        file: ./coverage/lcov.info
        flags: unittests

  build:
    needs: test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Set up Docker Buildx
      uses: docker/setup-buildx-action@v2
    
    - name: Login to DockerHub
      uses: docker/login-action@v2
      with:
        username: ${{ secrets.DOCKERHUB_USERNAME }}
        password: ${{ secrets.DOCKERHUB_TOKEN }}
    
    - name: Build and push
      uses: docker/build-push-action@v4
      with:
        context: .
        push: true
        tags: myapp:latest
    
    - name: Deploy to production
      run: |
        ssh ${{ secrets.SERVER_USER }}@${{ secrets.SERVER_HOST }} << 'EOF'
          cd /app/myapp
          docker-compose pull
          docker-compose up -d
          docker image prune -f
        EOF
```
