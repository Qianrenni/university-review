# npm 完整使用教程

## 目录
1. [npm 简介](#npm-简介)
2. [安装与配置](#安装与配置)
3. [基础命令](#基础命令)
4. [包管理](#包管理)
5. [项目初始化](#项目初始化)
6. [依赖管理](#依赖管理)
7. [脚本管理](#脚本管理)
8. [版本管理](#版本管理)
9. [发布包](#发布包)
10. [高级功能](#高级功能)

## npm 简介

npm (Node Package Manager) 是 Node.js 的默认包管理器，用于：
- 安装、更新、卸载 JavaScript 包
- 管理项目依赖
- 运行脚本命令
- 发布自己的包

## 安装与配置

### 安装 Node.js (包含 npm)
```bash
# 推荐使用官方安装包
# https://nodejs.org/

# 或使用包管理器安装
# macOS
brew install node

# Ubuntu
sudo apt install nodejs npm

# Windows (使用 Chocolatey)
choco install nodejs
```

### 检查版本
```bash
node -v
npm -v
```

### 基本配置
```bash
# 查看当前配置
npm config list

# 设置镜像源（国内用户推荐）
npm config set registry https://registry.npmmirror.com

# 查看配置信息
npm config get registry
```

## 基础命令

### 帮助命令
```bash
# 查看帮助
npm help

# 查看特定命令帮助
npm help install

# 查看版本
npm --version
npm -v
```

### 搜索包
```bash
# 搜索包
npm search express

# 在线搜索（打开浏览器）
npm docs express
```

## 包管理

### 安装包

#### 全局安装
```bash
# 全局安装（通常用于命令行工具）
npm install -g nodemon
npm install --global typescript

# 查看全局安装的包
npm list -g --depth=0
```

#### 本地安装
```bash
# 本地安装（项目依赖）
npm install lodash

# 开发依赖
npm install --save-dev jest
npm install -D webpack

# 可选依赖
npm install --save-optional optional-dep
```

#### 安装指定版本
```bash
# 安装特定版本
npm install lodash@4.17.20

# 安装最新版本
npm install lodash@latest

# 安装 beta 版本
npm install lodash@beta
```

### 卸载包
```bash
# 卸载本地包
npm uninstall lodash

# 卸载全局包
npm uninstall -g nodemon

# 卸载开发依赖
npm uninstall --save-dev jest
```

### 更新包
```bash
# 更新所有依赖
npm update

# 更新特定包
npm update lodash

# 检查过时的包
npm outdated

# 全局更新
npm update -g
```

## 项目初始化

### 创建 package.json
```bash
# 初始化项目（交互式）
npm init

# 快速初始化（使用默认值）
npm init -y
npm init --yes
```

### package.json 结构
```json
{
  "name": "my-project",
  "version": "1.0.0",
  "description": "A sample project",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "test": "jest"
  },
  "keywords": ["sample", "project"],
  "author": "Your Name",
  "license": "MIT",
  "dependencies": {
    "express": "^4.17.1"
  },
  "devDependencies": {
    "jest": "^27.0.0"
  }
}
```

## 依赖管理

### 依赖类型
```json
{
  "dependencies": {
    // 生产环境依赖
    "express": "^4.17.1"
  },
  "devDependencies": {
    // 开发环境依赖
    "jest": "^27.0.0",
    "webpack": "^5.0.0"
  },
  "peerDependencies": {
    // 对等依赖（插件使用）
    "react": "^17.0.0"
  },
  "optionalDependencies": {
    // 可选依赖
    "fsevents": "^2.3.2"
  }
}
```

### 安装依赖
```bash
# 安装所有依赖
npm install

# 仅安装生产依赖
npm install --production

# 从 package-lock.json 安装精确版本
npm ci
```

### 依赖版本符号
```bash
# 精确版本
"express": "4.17.1"

# 兼容版本（推荐）
"express": "^4.17.1"  # >=4.17.1 <5.0.0

# 补丁版本
"express": "~4.17.1"  # >=4.17.1 <4.18.0

# 最新版本
"express": "*"

# 版本范围
"express": ">=4.0.0 <5.0.0"
```

## 脚本管理

### 基本脚本
```json
{
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js",
    "test": "jest",
    "build": "webpack --mode production",
    "lint": "eslint src/"
  }
}
```

### 运行脚本
```bash
# 运行脚本
npm run start
npm run dev
npm run test

# 简写（start、stop、test 可省略 run）
npm start
npm test

# 查看可用脚本
npm run
```

### 预设和后置脚本
```json
{
  "scripts": {
    "prebuild": "echo 'Building...'",
    "build": "webpack",
    "postbuild": "echo 'Build completed!'",
    "pretest": "npm run lint",
    "test": "jest"
  }
}
```

### 传递参数
```bash
# 向脚本传递参数
npm run build -- --mode=development

# 环境变量
npm run start -- --env.NODE_ENV=production
```

## 版本管理

### 语义化版本控制 (SemVer)
```bash
# 格式：MAJOR.MINOR.PATCH
# 1.0.0 -> 1.0.1 (补丁版本：向后兼容的 bug 修复)
# 1.0.1 -> 1.1.0 (次要版本：向后兼容的功能新增)
# 1.1.0 -> 2.0.0 (主要版本：破坏性变更)
```

### 版本标签
```bash
# 查看版本标签
npm dist-tag ls

# 添加标签
npm dist-tag add package@1.0.0 beta

# 使用标签安装
npm install package@beta
```

### 版本发布
```bash
# 更新版本号
npm version patch  # 1.0.0 -> 1.0.1
npm version minor  # 1.0.1 -> 1.1.0
npm version major  # 1.1.0 -> 2.0.0

# 自定义版本
npm version 1.2.3
```

## 发布包

### 注册账号
```bash
# 注册新账号
npm adduser

# 登录
npm login

# 查看当前用户
npm whoami

# 登出
npm logout
```

### 发布流程
```bash
# 1. 检查包名是否可用
npm view my-package-name

# 2. 测试发布（dry run）
npm publish --dry-run

# 3. 正式发布
npm publish

# 4. 发布特定标签
npm publish --tag beta
```

### 包配置
```json
{
  "name": "@username/my-package",  // 作用域包
  "private": false,                // 公开包
  "files": [                       // 包含文件
    "dist/",
    "README.md"
  ],
  "main": "dist/index.js",         // 入口文件
  "module": "dist/index.esm.js",   // ES 模块入口
  "types": "dist/index.d.ts",      // TypeScript 声明文件
  "bin": {                         // 可执行文件
    "my-cli": "./bin/cli.js"
  },
  "publishConfig": {               // 发布配置
    "access": "public"
  }
}
```

## 高级功能

### 工作区 (Workspaces)
```json
{
  "name": "my-monorepo",
  "workspaces": [
    "packages/*"
  ]
}
```

```bash
# 在所有工作区运行命令
npm run test --workspaces

# 在特定工作区运行命令
npm run build --workspace=package-a
```

### 审计安全
```bash
# 安全审计
npm audit

# 自动修复安全问题
npm audit fix

# 强制修复（可能破坏性）
npm audit fix --force
```

### 缓存管理
```bash
# 查看缓存
npm cache ls

# 清理缓存
npm cache clean --force

# 验证缓存
npm cache verify
```

### 自定义配置
```bash
# .npmrc 文件配置
registry=https://registry.npmmirror.com
@myscope:registry=https://npm.pkg.github.com
//registry.npmjs.org/:_authToken=your-token
```

### 镜像源管理
```bash
# 查看当前镜像源
npm config get registry

# 设置淘宝镜像
npm config set registry https://registry.npmmirror.com

# 临时使用镜像
npm install --registry https://registry.npmmirror.com

# 使用 nrm 管理镜像源
npm install -g nrm
nrm ls
nrm use taobao
```

## 常用技巧

### 1. 并行运行多个命令
```bash
# 安装 concurrently
npm install --save-dev concurrently

# package.json
{
  "scripts": {
    "dev": "concurrently \"npm run server\" \"npm run client\""
  }
}
```

### 2. 环境变量
```json
{
  "scripts": {
    "start": "NODE_ENV=production node server.js"
  }
}
```

### 3. 跨平台脚本
```bash
# 安装 cross-env
npm install --save-dev cross-env

# package.json
{
  "scripts": {
    "start": "cross-env NODE_ENV=production node server.js"
  }
}
```

### 4. 钩子脚本
```json
{
  "scripts": {
    "preinstall": "node scripts/preinstall.js",
    "postinstall": "node scripts/postinstall.js"
  }
}
```

## 最佳实践

1. **使用 package-lock.json**：确保团队间依赖版本一致
2. **区分依赖类型**：正确使用 dependencies 和 devDependencies
3. **语义化版本**：遵循 SemVer 规范
4. **定期更新**：保持依赖包更新，修复安全漏洞
5. **使用 .npmignore**：排除不需要发布的文件
6. **安全审计**：定期运行 npm audit
7. **脚本文档**：在 README 中说明常用脚本
