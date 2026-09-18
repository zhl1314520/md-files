**实时定位并挑选 error 日志**

```bash
tail -f catlog.log | grep --line-buffered -i "error"
# 高亮显式
tail -f catlog.log | grep --line-buffered --color=always -i "error"
```

**awk 精准定位日志**

```bash
# 只看状态码非200的请求（假设第9列是状态码）
tail -f catlog.log | awk '$9 != "200"'

# 想看某次测试中所有请求的 URL（第7列）和状态码（第9列），过滤掉干扰信息
awk '{print $7, $9}' catlog.log

# 开发说“10点15分左右系统卡了一下”，你直接切出那 1 分钟的日志细细看
awk '$2 >= "10:15:00" && $2 < "10:16:00"' catlog.log

# 抓取 ERROR 行及其后面的堆栈，直到空行结束
awk '/ERROR/,/^$/' catlog.log
```

**定位 error 日志**

```bash
grep -i "error" catlog.log		# -i：不区分大小写
```

**端口占用**

```bash
sudo ss -tlnp | grep 8080

kill 8080
# 强制
kill -9 8080   
```

**刷新仓库资源包**

```bash
sudo apt update
```

**安装 ssh-server**

```bash
sudo apt install openssh-server
```

**启动 ssh-server**

```bash
sudo service ssh start
```

**查看 ssh 是否启动**

```bash
sudo service ssh status
```

