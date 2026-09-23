## docker-compose.yml 文件

> 作用：编排项目的镜像环境，一键启动容器服务，省的 docker 一个一个开启容器服务

## 构建服务系列

> **写完 Dockerfile、docker-compose.yml 后就执行**
>
> ```bash
> docker compose up -d --build
> ```
>
> **检查容器状态**
>
> ```bash
> docker ps
> ```
>
> **查看 web 容器日志后面 20 行（查看服务是否启动）**
>
> ```bash
> docker logs --tail 20 application-extension-container-web
> ```
>
> **初始化数据库表（首次必跑）**
>
> **会在 MySQL 的 application_extension 库中建 application 表和 django_migrations 表，无报错即完成**
>
> ```bash
> docker exec application-extension-container-web python manage.py migrate
> ```
>
> **查看数据是否通**
>
> ```bash
> curl http://127.0.0.1:8000/api/			# 返回空数据或者数据库原来的数据即可
> ```
>
> **重启 compose.yml 文件中的 web 服务，而不是重启容器名**
>
> ```bash
> docker compose restart web
> ```

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

