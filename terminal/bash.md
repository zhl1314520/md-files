## 嵌套 grep

> ```bash
> ls | grep -i error | grep -i massage		# -i：不区分大小写
> ```

**查看 wsl 下的服务**

```bash
wsl -l
```

**查看 wsl Ubuntu 版本等信息**

```bash
wsl -d Ubuntu -- cat /etc/os-release
```
