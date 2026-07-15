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
pnpm --filter web dev
pnpm --filter admin dev
pnpm --filter space dev
pnpm --filter live dev
```

