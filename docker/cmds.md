## 查看 Docker 占用内存情况

```bash
docker system df
```

## 删除构建缓存 Build Cache

```bash
docker builder prune
```

## 查看具体的 Images 镜像

```bash
docker image ls
```

## 通过 ID 删除镜像

```bash
docker rmi 04204fc18b5c dad1f0b93201
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
docker compose -f docker-compose-local.yml up -d

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
