

# 🧩 一、Maven 简介

## ✅ Maven 的核心功能

- **项目标准化**：定义统一的项目结构
- **依赖管理**：自动下载和管理第三方库（如 JAR 文件）
- **项目信息管理**：版本、开发者、组织等元数据
- **可扩展性**：支持丰富的插件体系，实现编译、打包、测试、部署等功能

---

# 📦 二、安装与环境配置

## 1. 下载 Maven

访问官网：[https://maven.apache.org](https://maven.apache.org)

选择合适的版本进行下载（推荐使用最新稳定版）。

## 2. 安装步骤

- 解压到本地目录（如 `C:\Program Files\Apache\maven` 或 `/usr/local/maven`）
- 配置环境变量：
  - `MAVEN_HOME` = Maven 安装路径
  - 将 `%MAVEN_HOME%\bin` 添加到 `PATH`

## 3. 验证安装

```bash
mvn -v
```

输出类似如下内容表示安装成功：

```
Apache Maven 3.8.6 (...)
Java version: 17, vendor: Oracle Corporation, runtime: /usr/lib/jvm/java-17
Default locale: en_US, platform encoding: UTF-8
OS name: "linux", version: "5.4.0-91-generic", arch: "amd64", family: "unix"
```

---

# 📁 三、Maven 项目结构

Maven 遵循约定优于配置的原则，提供了一套标准的目录结构：

```
my-project/
├── pom.xml
├── src/
│   ├── main/
│   │   ├── java/       # Java 源代码
│   │   └── resources/  # 资源文件（如配置文件）
│   └── test/
│       ├── java/       # 测试代码
│       └── resources/  # 测试资源文件
└── target/             # 构建输出目录（自动生成）
```

---

# 📄 四、POM 文件详解（pom.xml）

`pom.xml` 是 Maven 项目的核心配置文件，全称是 **Project Object Model**。

## 基本结构示例

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>demo</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging> <!-- 默认为 jar -->

    <name>demo</name>
    <url>http://www.example.com</url>

    <dependencies>
        <!-- 第三方依赖 -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <!-- 插件配置 -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>17</source>
                    <target>17</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

---

# 🔗 五、依赖管理（Dependencies）

Maven 会自动从远程仓库下载所需的依赖，并处理其传递依赖。

## 示例

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <version>3.1.0</version>
</dependency>
```

## 常用 `<scope>` 类型

| scope | 说明 |
|-------|------|
| `compile` | 默认值，适用于所有阶段 |
| `provided` | 编译时需要，运行时由容器提供（如 Servlet API） |
| `runtime` | 运行和测试时需要，编译不需要 |
| `test` | 只在测试阶段可用（如 JUnit） |
| `system` | 自定义本地依赖（不推荐） |

---

# ⚙️ 六、常用生命周期命令

Maven 有三个标准的生命周期阶段：

## 1. **clean**：清理构建输出目录（target）

```bash
mvn clean
```

## 2. **default（build）**：构建项目

常用阶段包括：

- `validate`：验证项目是否正确
- `compile`：编译主代码
- `test`：运行单元测试
- `package`：打包成 JAR/WAR/ZIP 等格式
- `verify`：运行集成测试
- `install`：将包安装到本地仓库
- `deploy`：部署到远程仓库

常用命令：

```bash
mvn compile      # 编译主代码
mvn test         # 执行测试
mvn package      # 打包项目
mvn install      # 安装到本地仓库
mvn deploy       # 部署到远程仓库
```

组合使用：

```bash
mvn clean package
```

---

# 🔌 七、Maven 插件（Plugins）

Maven 支持大量插件来增强构建能力。

## 常见插件

| 插件名称 | 功能 |
|----------|------|
| `maven-compiler-plugin` | 设置 Java 版本 |
| `maven-surefire-plugin` | 控制单元测试执行 |
| `maven-failsafe-plugin` | 控制集成测试执行 |
| `maven-jar-plugin` | 控制 JAR 包生成方式 |
| `maven-shade-plugin` | 打包包含依赖的“胖”JAR |
| `spring-boot-maven-plugin` | Spring Boot 项目打包部署 |

## 示例：设置 Java 17 编译

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
            <configuration>
                <source>17</source>
                <target>17</target>
            </configuration>
        </plugin>
    </plugins>
</build>
```

---

# 🌐 八、仓库管理（Repositories）

Maven 默认使用 [Maven Central](https://repo1.maven.org/) 作为中央仓库。

你也可以添加其他仓库：

```xml
<repositories>
    <repository>
        <id>spring-releases</id>
        <url>https://repo.spring.io/release</url>
    </repository>
</repositories>
```

---

# 📁 九、多模块项目（Multi-module Project）

大型项目可以划分为多个子模块，每个模块是一个独立的 Maven 项目。

## 父 POM 示例

```xml
<modules>
    <module>module-a</module>
    <module>module-b</module>
</modules>
```

---

# 💾 十、本地仓库与远程仓库

- **本地仓库**：默认位于用户目录下的 `.m2/repository` 目录
- **远程仓库**：可以从中央仓库或私有仓库获取依赖

---

# 🧼 十一、最佳实践建议

| 项目 | 建议 |
|------|------|
| 统一版本 | 使用 `<dependencyManagement>` 统一管理依赖版本 |
| 分离配置 | 不同环境使用不同的 `profiles` |
| 使用骨架创建项目 | 使用 `archetype` 快速生成项目结构 |
| 清理缓存 | 定期清理本地仓库以避免冲突 |
| 使用 CI 工具 | Jenkins、GitLab CI 等集成 Maven 构建流程 |

---

# 🧪 十二、常见问题排查

| 问题 | 解决方案 |
|------|----------|
| 找不到依赖 | 检查网络连接、仓库地址、依赖坐标是否正确 |
| 版本冲突 | 使用 `exclusion` 排除冲突依赖 |
| 构建失败 | 查看日志，定位具体错误模块 |
| 插件找不到 | 检查插件版本和仓库配置 |
| 打包后没有类 | 检查 `src/main/java` 是否放置正确，是否有编译错误 |

---

# 🧰 十三、Maven 命令大全（常用）

| 命令 | 说明 |
|------|------|
| `mvn clean` | 清理输出目录 |
| `mvn compile` | 编译主代码 |
| `mvn test` | 执行测试 |
| `mvn package` | 打包项目（如 JAR、WAR） |
| `mvn install` | 安装到本地仓库 |
| `mvn deploy` | 部署到远程仓库 |
| `mvn dependency:tree` | 查看依赖树 |
| `mvn archetype:generate` | 创建新项目 |
| `mvn site` | 生成项目站点文档 |
| `mvn verify` | 执行集成测试 |

---

# 📘 十四、推荐阅读

- [Maven 官方文档](https://maven.apache.org/guides/)
- [Maven 中央仓库](https://search.maven.org/)
- [Spring Boot + Maven 教程](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#build-tool-plugins.maven)
- 《Maven 实战》 —— 许晓斌 著
