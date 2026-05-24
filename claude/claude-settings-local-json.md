## 控制 Claude CLI 在这个项目里用什么模型、能用哪些工具、	 按什么规则执行任务的本地最高优先级配置文件

# ① 全栈开发（偏 UI + 产品实现）

> 目标：代码质量 + UI一致性 + 稳定输出（适合做 Web / 前后端联调）

```json
{
  "model_reasoning_effort": "medium",
  "temperature": 0.3,	# 控制“回答像不像人写的 & 是否有创造性”。数字越小越确定
  "max_tokens": 8000,
  "disable_response_storage": true,	# 控制“是否记录对话历史”（true → 不落盘 / 不保存 response）
										不会“失忆”（false → 保存到本地 history/session）
  "debug": false,	# true → 输出内部执行信息；false → 只输出正常回答
  "log_level": "error",
  "tools": {
    "browser": true,
    "shell": true
  }
}
```

# ② 测试开发（测开 / 自动化测试）

> 目标：稳定性 + 可复现 + 低随机性（核心是“严谨”）

```json
{
  "model_reasoning_effort": "medium",
  "temperature": 0.1,
  "max_tokens": 8000,
  "disable_response_storage": true,
  "debug": false,
  "log_level": "error",
  "tools": {
    "browser": true,
    "shell": true
  }
}
```

# ③ Debug 强化模式（排错 / 排障 / CLI分析）

> 目标：最大可观测性 + 最强日志 + 不隐藏任何信息

```json
{
  "model_reasoning_effort": "high",
  "temperature": 0.0,
  "max_tokens": 8000,
  "disable_response_storage": true,
  "debug": true,
  "log_level": "debug",
  "tools": {
    "browser": true,	# 浏览网页
    "shell": true
  }
}
```

