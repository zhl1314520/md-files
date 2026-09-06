## 📌Linux两台机器传文件用什么端口

常用：

```bash
tail -f catlog.log | grep --line-buffered -i "error"
# 高亮显式
tail -f catlog.log | grep --line-buffered --color=always -i "error"
sudo ss -tlnp | grep 8080
kill 8080
# 强制
kill -9 8080   
```

例如：

```bash
scp file root@ip:/home
```

------

## 📌Linux查看进程

```bash
# 查看当前终端的进程（简洁）
ps

# 查看当前用户所有进程
ps -u $USER

# 查看系统所有进程（推荐）
ps aux（进程占用多少 CPU/内存、排查卡顿）
ps -ef（查看进程归属，标准规范输出）

# 查看树状结构（显示父子关系）
ps auxf

# 查找特定进程（如 nginx）
ps aux | grep nginx

# 查看指定 PID 的详细信息（如 PID=1234）
ps -p 1234 -o pid
```

------

## 📌基本Linux命令

```bash
ls
cd
pwd
cp
mv
rm
mkdir
cat
grep
```

------

## 📌Linux查看进程、top、磁盘

- ### 查看进程


```bash
ps aux
```

- ### top


动态查看CPU和内存：

```bash
top
```

- ### 查看磁盘


```bash
df -h	# 查看整个系统的磁盘分区使用情况
du -sh  # 查看指定目录/文件的磁盘使用情况
```

------

## 📌说几个Linux指令

```bash
find	# 查找文件/目录
grep	# 一般配合管道符 | 使用，表示搜索
tail	# 查看文件末尾内容
head	# 。。。
chmod	# 修改文件权限
tar		# 打包压缩
```

## 📌两个文件交叉写入第三个文件

```bash
paste -d '\n' file1 file2 > file3
```

------

## 📌ping百度途径主机如何展示

Windows：

```
tracert www.baidu.com
```

Linux：

```bash
traceroute www.baidu.com
```

## 📌查看端口、日志、磁盘等命令

- ### 查看端口


```bash
# 查看所有监听端口（现代推荐）
ss -tunlp

# 旧版命令
netstat -tunlp

# 查看特定端口
ss -tunlp | grep :80
netstat -tunlp | grep :22

# 查看TCP连接状态
ss -tan
netstat -tan

# 查看端口占用进程
lsof -i :8080

# 服务器端口是否开启
telnet <服务器IP> <端口号>
屏幕变黑或出现空光标，说明端口可通。提示Connection refused或无法连接，则端口不通
```

- ### 查看日志


```bash
# 查看系统日志（CentOS/RHEL）
journalctl -f
journalctl -u service_name

# 查看传统日志文件
tail -f /var/log/messages
tail -f /var/log/syslog

# 应用程序日志
tail -f /var/log/nginx/access.log
tail -f /var/log/apache2/error.log


# 搜索关键词
grep "error" /var/log/messages
grep -i "failed" /var/log/auth.log
```

- ### 删除txt文件


```bash
rm *.txt
```

- ### 查看磁盘


```bash
df -h
```

------

## 📌crontab、uptime、du、netstat作用

- ### crontab


​		定时任务。

- ### uptime


​		查看系统运行时间和负载。

- ### du（disk usage）


​		查看目录大小。

- ### netstat


​		查看端口和网络连接。

------

## 📌vi替换字符串

- ### T替换为t


```bash
:%s/T/t/g
```

- ### 复制一行


```bash
yy
p
```