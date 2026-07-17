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

> 下面的全是 Git Bash 命令      

```bash
cd /d/plane

# 赋予执行权限
chmod +x setup.sh

./setup.sh

# 启动后端所有服务
docker compose -f docker-compose-local.yml up -d

# 查看后端各个服务启动情况（状态，端口）
docker compose -f docker-compose-local.yml ps --format "table {{.Service}}\t{{.Status}}\t{{.Ports}}"

# stop 后端服务
docker compose -f docker-compose-local.yml stop
```

> Powershell 

```shell
# 分别启动前端
pnpm install
pnpm run dev		# plane 项目理论上可以，但是环境原因，无果。。。
pnpm exec turbo run dev --concurrency=18 	# 启动，效果等同于 pnpm run dev

# 多命令启动
pnpm --filter web dev
pnpm --filter admin dev
pnpm --filter space dev
pnpm --filter live dev
```

> pnpm run dev 报错分析：
>
> - 前置条件：win-powershell 环境运行
>   1. 尝试了 pnpm exec turbo run dev --concurrency=18，还是不能打开页面
>   2. pnpm dev 也不行
> - 解决：
>   - 前置条件：使用 git bash 的 Linux 环境
>   - pnpm run dev 打开
> - 原因：windows 下 plane 的兼容性不如 linux 下的环境
