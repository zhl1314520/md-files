## 服务生命周期管理

```bash
docker compose up 			# 创建并启动docker-compose.yml中定义的所有服务
-d: 后台运行
--build: 启动前重新构建镜像

docker compose down			# 停止并删除所有服务容器、网络等
-v: 同时删除关联的数据卷（数据会丢失）

docker compose start/stop/restart		# 启动/停止/重启已存在的服务
```

## 调试

```bash
docker compose ps		# 列出所有服务状态

docker compose logs		# 查看服务日志
```

