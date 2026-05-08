
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
