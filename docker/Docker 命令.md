## 查看 Docker 占用内存情况

```bash
docker system df
```

## 删除构建缓存 Build Cache

```bash
docker builder prune
```

## 查看Docker客户端和服务器版本

```bash
docker version
```

## 显示Docker系统级信息，如容器、镜像数量等

```bash
docker info
```

## 镜像管理类

```bash
docker pull 镜像名				# 默认从 dcoker hub 拉取

docker images				  # 列出本地的 images

docker rmi 镜像id				 # 删除本地的镜像

docker build -t 镜像名			# 使用 Dockerfile 构建新镜像
```

## 容器生命周期管理

```bash
docker run [选项] 镜像 			# 创建并启动一个新容器
-d: 后台运行
-p 主机端口:容器端口: 端口映射
--name 容器名: 指定容器名称
-e KEY=VALUE: 设置环境变量
-v 主机路径:容器路径: 挂载数据卷

docker ps					   # 查看运行中的容器，+ “-a”查看所有容器

docker stop 容器名/id

docker start 容器名/id

docker restart 容器名/id

docker rm 容器名/id		# 移除一个停止服务的容器
```

## 容器运维与调试

```bash
docker exec -it 容器名 bash		# 进入一个正在运行的容器内部，执行交互式命令

docker logs 容器名	
-f: 实时跟踪日志输出
--tail N: 显示最后N行日志
```

## Docker 快速跑项目（plane 项目为例）

> 后端

```bash
cd /d/plane

# 赋予执行权限
chmod +x setup.sh

./setup.sh

""" 
启动后端所有服务
compose：按照配置文件，一次性管理多个容器，不用 compose，需要一个一个启动服务
-f：--file
docker-compose-local.yml：使用这个文件，按照这个配置文件启动服务
up：启动
-d：后台运行，没有 -d，一直出现日志
"""
docker compose -f docker-compose-local.yml up -d		# 提前启动 docker

# 查看后端各个服务启动情况（状态，端口）
docker compose -f docker-compose-local.yml ps --format "table {{.Service}}\t{{.Status}}\t{{.Ports}}"

# stop 后端服务
docker compose -f docker-compose-local.yml stop
```

> 前端

```bash
pnpm install

pnpm run dev
```

> pnpm run dev 报错分析：
>
> - 前置条件：windows git bash环境运行
>   1. 尝试了package.json 中的 dev: pnpm exec turbo run dev --concurrency=18，报错
>   2. pnpm run dev 也不行
> - 尝试解决：
>   1. 退出 node 子进程：tasklist | findstr node
>   2. 杀端口号
>   3. pnpm run clean：清理缓存（.watch   .turbo 等）
> - 原因：
>   1. node 子进程未退出
>   2. 之前取消 git 代理配置，忘了重新配置了，导致连接不稳定

> i18n 显示不出中文包、页面元素名称问题（页面出现的是 key，如 settings.features.module，而不是 module）:
>
> - 前置条件：前后端都正常，i18n 也正常
>
> - 尝试解决：
>
>   1. 找 i18n 下面的 package.js 文件，排除
>   2. 找 zh-cn，en 文件，都有，排除
>   3. F12 找报错，排除
>
> - 解决：
>
>   1. 删除了损坏的 packages/i18n/locales 文本文件
>
>   2. 创建了一个 Windows Junction （目录联接） packages/i18n/locales → packages/i18n/src/locales
>      Junction 类似于快捷方式/符号链接，访问 packages/i18n/locales/en/common.json 时会透明地解析到 packages/i18n/src/locales/en/common.json 。
>
>      文件没有移动，只是修复了链接，让 dist/index.js 中的 import("../locales/...") 能正确找到 locale 文件。
>
> - 原因：
>
>   - packages/i18n/locales 是一个 Git 符号链接 （指向 src/locales ），但在 Windows 上 Git 默认不创建真正的符号链接，只生成了一个包含 src/locales 文本的普通文件。
>
>     i18n 的动态导入 import(\ ../locales/ [ o bj ec tO bj ec t ] l an gu a g e / {namespace}.json`) 从 dist/index.js 解析时， ../locales/ 指向这个损坏的"文件"，导致所有 locale 文件无法加载，i18next 找不到翻译值，直接返回原始 key 字符串如 common.display`
