
# 1. Docker 简介与核心概念

## 📌 什么是 Docker？

Docker 是一个开源的应用容器引擎，让开发者可以将应用及其依赖打包在一个标准化的环境中运行 —— **一次构建，到处运行**。

## 🧩 核心概念

| 名称 | 含义 |
|------|------|
| **Image（镜像）** | 应用的静态模板，包含运行所需的所有文件和配置。 |
| **Container（容器）** | 镜像的运行实例，是动态的、可启动的。 |
| **Volume（卷）** | 用于持久化数据，避免容器删除后数据丢失。 |
| **Network（网络）** | 容器之间通信的虚拟网络。 |
| **Dockerfile** | 构建镜像的脚本文件。 |
| **docker-compose.yml** | 多个服务（如 Web + DB）的编排配置文件。 |

---

# 2. Docker 架构组成

Docker 使用客户端-服务端架构：

- **Docker Client（客户端）**：用户使用的命令行工具（`docker` 命令）
- **Docker Daemon（守护进程）**：负责管理镜像、容器、网络等
- **Docker Registry（仓库）**：存储和分发镜像的地方（如 Docker Hub）

```
+-------------------+
|   Docker Client   |
+-------------------+
         |
         v
+-------------------+
| Docker Daemon     |
| - Images          |
| - Containers      |
| - Volumes         |
| - Networks        |
+-------------------+
         |
         v
+-------------------+
| Docker Registry   |
| (e.g., Docker Hub)|
+-------------------+
```

---

# 3. Docker 安装与环境搭建

## ✅ Windows 安装

推荐使用 [Docker Desktop for Windows](https://www.docker.com/products/docker-desktop)

- 支持 WSL2（推荐）
- 自带图形界面（GUI）
- 可以轻松切换 Linux/Windows 容器模式

## ✅ Linux 安装（Ubuntu）

```bash
sudo apt update
sudo apt install docker.io
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker $USER
```

> 重启终端或重新登录使 `docker` 用户组生效。

---

# 4. Docker 基本命令详解

## 🔍 查看版本信息

```bash
docker --version
docker info
```

## 🐣 镜像相关操作

```bash
docker images            # 列出本地所有镜像
docker pull ubuntu       # 从远程拉取镜像
docker build -t myapp .  # 构建镜像
docker rmi ubuntu        # 删除镜像
```

## 📦 容器相关操作

```bash
docker run hello-world   # 运行一个容器
docker ps                # 查看正在运行的容器
docker ps -a             # 查看所有容器（包括停止的）
docker stop <container>  # 停止容器
docker rm <container>    # 删除容器
docker logs <container>  # 查看容器日志
```

## 📥 数据挂载与目录共享

```bash
docker run -v /宿主机路径:/容器路径 myapp
```

例如：

```bash
docker run -v D:/data:/app/data myapp
```

## 🌐 网络操作

```bash
docker network create mynet
docker network ls
docker network inspect mynet
```

---

# 5. Dockerfile：构建镜像的配方文件

## 📝 示例 Dockerfile

```Dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["python", "app.py"]
```

## 🛠️ 构建镜像

```bash
docker build -t my-flask-app .
```

---

# 6. Volume：持久化数据管理

## 📂 挂载命名卷（Named Volume）

```yaml
volumes:
  - my_data:/path/in/container
```

## 💾 挂载本地目录（Bind Mount）

```bash
docker run -v D:/data:/app/data myapp
```

## 🧼 管理卷

```bash
docker volume ls
docker volume inspect my_data
docker volume rm my_data
```

---

# 7. 网络（Networking）：容器间通信

## 🌐 创建自定义网络

```bash
docker network create my_network
```

## 🔄 将容器加入网络

```bash
docker run --network my_network --name webserver nginx
docker run --network my_network --name db mysql
```

这样两个容器就可以通过名称互相访问：

```bash
ping webserver
ping db
```

---

# 8. Docker Compose：多服务编排工具

## 📄 示例 `docker-compose.yml`

```yaml
version: '3'
services:
  web:
    image: myweb
    ports:
      - "80:80"
  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: rootpass
```

## 🚀 启动服务

```bash
docker-compose up -d
```

## 🛑 停止并删除服务

```bash
docker-compose down
```

---

# 9. Docker 与 CI/CD 集成

## 🧱 构建自动化流程

```yaml
# .github/workflows/docker-build.yml (GitHub Actions 示例)
name: Build and Push Docker Image

on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Build the Docker image
        run: |
          docker build . -t yourusername/myapp
      - name: Push to Docker Hub
        run: |
          docker login -u ${{ secrets.DOCKER_USER }} -p ${{ secrets.DOCKER_PASS }}
          docker push yourusername/myapp
```

---

# 10. 常见问题与最佳实践

## ❓ 常见问题

| 问题 | 解决方案 |
|------|----------|
| 容器启动失败 | `docker logs <container>` 查看日志 |
| 容器无法访问 | 检查端口映射是否正确 |
| 数据丢失 | 使用 Volume 持久化数据 |
| 容器之间无法通信 | 使用自定义网络 |
| 构建镜像太慢 | 使用 `.dockerignore` 忽略不必要的文件 |

## ✅ 最佳实践

- **保持镜像小而精**：使用轻量基础镜像（如 Alpine、slim）
- **不要在容器中写入数据**：使用 Volume 存储数据
- **使用标签命名镜像**：如 `myapp:1.0`
- **容器只运行一个主进程**：遵循“一个容器一个服务”原则
- **定期清理无用镜像和容器**

---

# 🎁 附录：常用命令速查表

| 功能 | 命令 |
|------|------|
| 构建镜像 | `docker build -t myapp .` |
| 运行容器 | `docker run -d -p 80:80 myapp` |
| 查看容器 | `docker ps` |
| 查看日志 | `docker logs <container>` |
| 挂载目录 | `-v D:/data:/app/data` |
| 创建网络 | `docker network create mynet` |
| 使用 compose 启动 | `docker-compose up -d` |
| 清理未使用镜像 | `docker image prune -a` |

---

# 📘 推荐学习资源

| 类型 | 资源链接 |
|------|----------|
| 官方文档 | <https://docs.docker.com> |
| Docker Hub | <https://hub.docker.com> |
| 在线教程 | <https://labs.play-with-docker.com> |
| 视频课程 | Bilibili / YouTube 搜索 “Docker 教程” |
| 书籍推荐 | 《Docker——从入门到实践》《Docker 技术入门与实战》 |

---

# ❤️ 总结

Docker 是现代开发和部署中不可或缺的工具，它简化了环境差异带来的麻烦，提高了开发效率和部署可靠性。

掌握 Docker，你就能：

- 快速部署项目
- 实现跨平台一致性
- 构建微服务架构
- 与 CI/CD 流水线无缝集成

---

如果你希望我为你定制一份 **Docker 学习路线图** 或者生成一个 **Flask + MySQL + Redis 的完整 Docker 示例项目结构**，也可以告诉我 😊

需要 PDF 版本？我也可以帮你生成 👇
