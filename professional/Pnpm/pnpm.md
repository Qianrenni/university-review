# pnpm 完整使用教程

## 目录
1. [pnpm 简介](#pnpm-简介)
2. [安装与配置](#安装与配置)
3. [基础命令](#基础命令)
4. [包管理](#包管理)
5. [项目初始化](#项目初始化)
6. [依赖管理](#依赖管理)
7. [脚本管理](#脚本管理)
8. [工作区管理](#工作区管理)
9. [发布包](#发布包)
10. [高级功能](#高级功能)
11. [最佳实践](#最佳实践)

## pnpm 简介

pnpm 是一个快速、节省磁盘空间的包管理器，主要特点：

### 核心优势
- **速度快**：并行安装，避免重复下载
- **节省空间**：硬链接和符号链接存储
- **安全**：非扁平化的 node_modules 结构
- **兼容性**：完全兼容 npm 生态
- **支持 monorepo**：强大的工作区支持

### 与 npm/yarn 对比
```
安装速度：pnpm > yarn > npm
磁盘空间：pnpm << yarn ≈ npm
```

## 安装与配置

### 安装 pnpm
```bash
# 使用 npm 安装
npm install -g pnpm

# 使用 corepack（Node.js 16.13+）
corepack enable pnpm

# 使用脚本安装（推荐）
curl -fsSL https://get.pnpm.io/install.sh | sh -

# 使用包管理器安装
# macOS
brew install pnpm

# Windows (使用 Chocolatey)
choco install pnpm

# Ubuntu/Debian
curl -fsSL https://get.pnpm.io/install.sh | sudo -E bash -
```

### 验证安装
```bash
pnpm --version
pnpm -v

# 查看帮助
pnpm help
```

### 基本配置
```bash
# 查看当前配置
pnpm config list

# 设置镜像源（国内用户推荐）
pnpm config set registry https://registry.npmmirror.com

# 设置 store 路径
pnpm config set store-dir ~/.pnpm-store

# 查看配置
pnpm config get registry
```

## 基础命令

### 帮助命令
```bash
# 查看帮助
pnpm help

# 查看特定命令帮助
pnpm help install

# 查看版本
pnpm --version
pnpm -v
```

### 搜索包
```bash
# 搜索包
pnpm search express

# 查看包信息
pnpm info express
```

## 包管理

### 安装包

#### 全局安装
```bash
# 全局安装（通常用于命令行工具）
pnpm add -g nodemon
pnpm add --global typescript

# 查看全局安装的包
pnpm list -g --depth=0
```

#### 本地安装
```bash
# 安装生产依赖
pnpm add lodash

# 安装开发依赖
pnpm add --save-dev jest
pnpm add -D webpack

# 安装可选依赖
pnpm add --save-optional optional-dep

# 安装对等依赖
pnpm add --save-peer react
```

#### 安装指定版本
```bash
# 安装特定版本
pnpm add lodash@4.17.20

# 安装最新版本
pnpm add lodash@latest

# 安装 beta 版本
pnpm add lodash@beta

# 安装 tag
pnpm add lodash@next
```

### 卸载包
```bash
# 卸载本地包
pnpm remove lodash
pnpm rm lodash

# 卸载全局包
pnpm remove -g nodemon

# 卸载开发依赖
pnpm remove --save-dev jest
```

### 更新包
```bash
# 更新所有依赖
pnpm update

# 更新特定包
pnpm update lodash

# 更新到最新版本
pnpm update lodash@latest

# 检查过时的包
pnpm outdated

# 全局更新
pnpm update -g
```

### 交互式更新
```bash
# 交互式选择更新的包
pnpm update --interactive
pnpm up -i

# 交互式更新并查看差异
pnpm update --interactive --latest
```

## 项目初始化

### 创建 package.json
```bash
# 初始化项目（交互式）
pnpm init

# 快速初始化（使用默认值）
pnpm init -y
```

### pnpm 特有的初始化选项
```bash
# 初始化工作区
pnpm init -w

# 创建示例 package.json
pnpm init esm
pnpm init react
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
  },
  "engines": {
    "node": ">=16.0.0",
    "pnpm": ">=7.0.0"
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
pnpm install
pnpm i

# 仅安装生产依赖
pnpm install --prod

# 从 pnpm-lock.yaml 安装精确版本
pnpm install --frozen-lockfile
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

# 标签
"express": "beta"
```

### node_modules 结构
```bash
# pnpm 的 node_modules 结构
node_modules/
├── .pnpm/                    # 实际包存储
│   ├── express@4.17.1/
│   └── lodash@4.17.20/
└── express -> .pnpm/express@4.17.1/node_modules/express
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
pnpm run start
pnpm run dev
pnpm run test

# 简写（start、stop、test 可省略 run）
pnpm start
pnpm test

# 查看可用脚本
pnpm run
```

### 预设和后置脚本
```json
{
  "scripts": {
    "prebuild": "echo 'Building...'",
    "build": "webpack",
    "postbuild": "echo 'Build completed!'",
    "pretest": "pnpm run lint",
    "test": "jest"
  }
}
```

### 传递参数
```bash
# 向脚本传递参数
pnpm run build -- --mode=development

# 环境变量
pnpm run start -- --env.NODE_ENV=production
```

### 生命周期脚本
```json
{
  "scripts": {
    "preinstall": "node scripts/preinstall.js",
    "postinstall": "node scripts/postinstall.js",
    "prepublishOnly": "npm test",
    "prepare": "husky install"
  }
}
```

## 工作区管理

### 初始化工作区
```bash
# 创建工作区根目录
mkdir my-monorepo
cd my-monorepo
pnpm init -w

# 创建子包目录
mkdir packages
cd packages
mkdir pkg-a pkg-b
```

### pnpm-workspace.yaml 配置
```yaml
# pnpm-workspace.yaml
packages:
  # 所有在 packages/ 目录下的包
  - 'packages/*'
  # 排除测试包
  - '!**/test/**'
  # 嵌套工作区
  - 'components/**'
```

### 工作区命令
```bash
# 在所有工作区运行命令
pnpm -r run test

# 在特定工作区运行命令
pnpm --filter pkg-a run build

# 在多个工作区运行命令
pnpm --filter pkg-a --filter pkg-b run test

# 递归安装
pnpm install -r

# 添加依赖到特定包
pnpm --filter pkg-a add lodash

# 添加依赖到所有包
pnpm -r add lodash

# 链接包之间
pnpm --filter pkg-a add pkg-b --workspace
```

### 工作区示例结构
```
my-monorepo/
├── pnpm-workspace.yaml
├── package.json
└── packages/
    ├── pkg-a/
    │   ├── package.json
    │   └── index.js
    └── pkg-b/
        ├── package.json
        └── index.js
```

### 工作区依赖管理
```json
{
  "name": "pkg-a",
  "dependencies": {
    "pkg-b": "workspace:*",  // 链接到工作区中的 pkg-b
    "lodash": "^4.17.20"
  }
}
```

## 发布包

### 注册账号
```bash
# 注册新账号
pnpm adduser

# 登录
pnpm login

# 查看当前用户
pnpm whoami

# 登出
pnpm logout
```

### 发布流程
```bash
# 1. 检查包名是否可用
pnpm view my-package-name

# 2. 测试发布（dry run）
pnpm publish --dry-run

# 3. 正式发布
pnpm publish

# 4. 发布特定标签
pnpm publish --tag beta

# 5. 发布工作区中的包
pnpm --filter pkg-a publish
```

### 包配置
```json
{
  "name": "@username/my-package",
  "private": false,
  "files": [
    "dist/",
    "README.md"
  ],
  "main": "dist/index.js",
  "module": "dist/index.esm.js",
  "types": "dist/index.d.ts",
  "bin": {
    "my-cli": "./bin/cli.js"
  },
  "publishConfig": {
    "access": "public"
  }
}
```

### 工作区发布
```bash
# 发布所有可发布的包
pnpm -r publish

# 交互式发布
pnpm -r publish --otp

# 发布特定包
pnpm --filter @scope/pkg-name publish
```

## 高级功能

### 存储管理
```bash
# 查看存储使用情况
pnpm store status

# 添加包到存储
pnpm store add lodash@4.17.20

# 清理未使用的包
pnpm store prune

# 查看存储路径
pnpm store path
```

### 审计安全
```bash
# 安全审计
pnpm audit

# 自动修复安全问题
pnpm audit --fix

# 查看详细信息
pnpm audit --json
```

### 执行命令
```bash
# 在临时环境中执行命令
pnpm dlx create-react-app my-app

# 执行包中的命令
pnpm exec tsc --version

# 在特定包中执行命令
pnpm --filter pkg-a exec npm run build
```

### 链接包
```bash
# 链接本地包
pnpm link

# 链接到全局
pnpm link --global

# 链接其他包
pnpm link ../other-package

# 取消链接
pnpm unlink
```

### 配置管理
```bash
# .npmrc 配置（也适用于 pnpm）
registry=https://registry.npmmirror.com
@myscope:registry=https://npm.pkg.github.com
//registry.npmjs.org/:_authToken=your-token

# pnpm 特有配置
store-dir=~/.pnpm-store
state-dir=~/.pnpm-state
modules-dir=node_modules
```

### 镜像源管理
```bash
# 查看当前镜像源
pnpm config get registry

# 设置淘宝镜像
pnpm config set registry https://registry.npmmirror.com

# 临时使用镜像
pnpm add express --registry https://registry.npmmirror.com

# 使用第三方工具管理镜像源
npm install -g nrm
nrm use taobao
```

### 环境变量
```bash
# 设置环境变量
PNPM_REGISTRY=https://registry.npmmirror.com pnpm install

# 使用 .env 文件
# .env
PNPM_REGISTRY=https://registry.npmmirror.com
```

## 最佳实践

### 1. 性能优化
```bash
# 使用 .pnpmfile.cjs 自定义解析
// .pnpmfile.cjs
function readPackage(pkg) {
  // 修改包配置
  if (pkg.name === 'some-package') {
    pkg.dependencies = {
      ...pkg.dependencies,
      'some-dep': '^1.0.0'
    }
  }
  return pkg
}

module.exports = {
  hooks: {
    readPackage
  }
}
```

### 2. 锁文件管理
```bash
# 提交 lock 文件
git add pnpm-lock.yaml

# 更新 lock 文件
pnpm install --lockfile-only

# 验证 lock 文件
pnpm install --frozen-lockfile
```

### 3. 依赖策略
```json
{
  "pnpm": {
    "peerDependencyRules": {
      "ignoreMissing": ["eslint"],
      "allowedVersions": {
        "react": "17"
      }
    },
    "allowedDeprecatedVersions": {
      "request": "*"
    }
  }
}
```

### 4. CI/CD 配置
```yaml
# GitHub Actions
name: CI
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: pnpm/action-setup@v2
        with:
          version: 8
      - uses: actions/setup-node@v3
        with:
          node-version: 18
          cache: 'pnpm'
      - run: pnpm install --frozen-lockfile
      - run: pnpm test
```

### 5. monorepo 最佳实践
```json
{
  "scripts": {
    "build": "pnpm -r build",
    "test": "pnpm -r test",
    "changeset": "changeset",
    "release": "changeset publish"
  }
}
```

## 常见问题解决

### 1. 权限问题
```bash
# 设置正确的存储目录权限
pnpm config set store-dir ~/.pnpm-store
```

### 2. 网络问题
```bash
# 设置代理
pnpm config set proxy http://proxy-server:port
pnpm config set https-proxy http://proxy-server:port
```

### 3. node_modules 问题
```bash
# 重新安装
pnpm install --force

# 清理缓存
pnpm store prune
```

## 与 npm/yarn 的对比

| 特性 | pnpm | npm | yarn |
|------|------|-----|------|
| 速度 | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐ |
| 磁盘空间 | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐ |
| 安全性 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ |
| 兼容性 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| monorepo | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ |

