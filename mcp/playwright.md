# playwright  for Claude code CLI 

## 添加

- 方法 1

> /mcp add playwright npx @playwright/mcp@latest		# claude 对话框输入

- 方法 2（常用）

> ```powershell
> # 作用整个 user
> 任意盘下> claude mcp add --scope user playwright -- npx @playwright/mcp@latest
> ```

## 常用命令

> ```powershell
> claude mcp list				# 查看所有 mcp
> 
> claude mcp get playwright   # 查看某个 mcp
> 
> claude mcp remove playwright# 删除
> ```