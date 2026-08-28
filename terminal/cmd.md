## 端口占用问题

- #### netstat -ano | findstr ":8080"		// Listening 后面的数字就是 PID

- #### taskkill /PID xxxxx /F                               // F: 强制执行，千万不要 kill PID 为 0 的进程 