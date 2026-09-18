## 📌Linux两台机器传文件用什么端口

常用：

```bash



# 1. 看设备
adb devices -l
# 2. 覆盖安装（测试包）
adb install -r -t app.apk
# 3. 清应用数据
adb shell pm clear com.xxx.xxx
# 4. 启动 App
adb shell am start -n com.xxx.xxx/.MainActivity
# 5. 强制停止 App
adb shell am force-stop com.xxx.xxx
# 6. 抓日志
adb logcat -c
# 抓 error 日志(显示时间)
adb logcat -v time *:E
# 直接抓
adb logcat *:E
# 7. 看当前是哪个页面
adb shell dumpsys window | findstr mCurrentFocus

KEY idx_project_status_updated (project_id, status, updated_time)
这样 WHERE 和 ORDER BY 都能利用同一个联合索引，索引天然就是按 updated_time 有序的，避免了 filesort，也能快速定位到深分页的起始位置

限制返回条数：对搜索结果强制限制最大返回数量，避免用户输入过于宽泛的关键词导致大量扫描
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

- ### 查看磁盘


```bash
df -h
```
