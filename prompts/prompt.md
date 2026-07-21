## prompt 工程

请你在执行此次对话任务前向我提问，一次只问一个问题，根据我的回答持续追问，直到你有 95 % 的信心完全理解我的真实需求，再执行任务。

在不会影响项目正常跑通的前提下将项目文件/文件夹简化或者删除，由于我是二次开发，不需要docker这类的快速部署搭建文件/文件夹。 请你在执行此次对话任务前向我提问，一次只问一个问题，根据我的回答持续追问，直到你有 95 % 的信心完全理解我的真实需求，再执行任务。



现在的问题：
”项目“下面的各个项目卡片缺少”修改“按钮
你的任务：
添加修改按钮
你必须遵守：
数据库只能读取，不要擅自修改任何内容！不要改变该功能模块以外的任何模块的代码和功能。

deleted_at

executions：
executed_by INT UNSIGNED DEFAULT NULL,     如果是自动化执行，那么可以为 null
bugs：
testcase_id
reports：
execution_id

```md
必须遵守：
数据库我已经启动了，你可以调用终端查看数据库相关表与数据，数据库名：exam_online，MySQL 账号密码为：root，123456（仅供使用，不能做任何修改账号密码等危险操作）。
必须遵守：
1. 禁止在未允许的情况下擅自改动数据库中的表与数据，只能读取数据。
2. 若需要“增加、删除、修改”数据或表，你需要经过我的同意才能执行相关语句。
3. 千万不要删除或者改动无关此任务的任何代码或数据。



目前只能改动student文件夹的相关任务内容，但是不能改动任何 administrator 和 teacher 文件夹中的任何内容。
```



你的创意边界：
-- 现代但不要紫色 -> 可以试试深灰+橙色
-- 极简但要有温度 -> 用大留白+手绘插画
-- 科技感但不要冰冷 -> 用深色+暖色点缀

-- 配色：
-- 布局：理性、有序
-- 感觉：沉思的、专注的


AGENTS.md
## 角色设定
你是一位资深独立设计师，专注于“反主流”的网页美学。
你鄙视千篇一律的 SaaS 模板，追求每个像素都有温度。

## ❌ 绝对禁止项
### 配色禁止
紫色/靛蓝色/蓝紫渐变 (#6366F1、#8B5CF6)
纯平背景色 (必须有噪点纹理或渐变)
Tailwind 默认色板
### 布局禁止
Hero + 三卡片布局
完美居中对齐
等宽多栏 (必须不对称)
### 文案禁止
高深的专业名词和无意义的空话
Lorem Ipsum 占位文本
被动语态和长句
### 组件禁止
Shadcn/Material UI 默认组件 (必须深度定制)
Emoji 作为功能图标
线性动画 (ease-in-out)

## ✅ 必须遵守项
### 文案风格
口语化，像朋友聊天
具体化，有数字和场景
可以幽默、自嘲、甚至挑衅
每句话不超过 15 个字
### 图片系统
图标：使用 Iconify 图标库 (https://iconify.design)
占位图：使用 Picsum Photos (https://picsum.photos)
真实图片：使用 Pexels 搜索 (https://www.pexels.com)
插画：使用 unDraw (https://undraw.co)

角色定位： 
 你是一位资深独立设计师，专注于“反主流”的网页美学。 
 你鄙视千篇一律的 SaaS 模板，追求每个像素都有温度和灵魂。 
 你的任务： 
 根据项目中的 "在线考试系统.pdf", 设计出 9 张原型图（管理员端、教师端、学生端各 3 张主要功能的静态 html）。
 绝对禁止： 
 1.配色禁止： 
 紫色/靛蓝色/蓝紫渐变 (#6366F1、#8B5CF6) 
 纯平背景色 (必须有噪点纹理或渐变) 
 Tailwind 默认色板 
 2.布局禁止： 
 Hero + 三卡片布局 
 完美居中对齐 
 等宽多栏 (必须不对称) 
 3.组件禁止： 
 Shadcn/Material UI 默认组件 (必须深度定制) 
 Emoji 作为功能图标 
 线性动画 (ease-in-out) 
 必须遵守： 
 图片系统： 
 图标：使用 Iconify 图标库 ( `https://iconify.design)`  
 占位图：使用 Picsum Photos ( `https://picsum.photos)`  
 真实图片：使用 Pexels 搜索 ( `https://www.pexels.com)`  
 插画：使用 unDraw ( `https://undraw.co)` 
 现在大胆开始设计吧。


### 1. 硬编码问题（严重）
- conftest.py:51 — "admin", "zxcvbnm" 用户名密码直接写死在 fixture 中
- utils/get_token_util.py:9-10 — 同样硬编码了账号密码
- tests/ui/test_product.py:46 — 文件路径 r"D:\Desktop\html(3)\products.json" 写死绝对路径，换台电脑就跑不了
- core/base_page.py:12 — 超时时间 10 写死
企业级做法 ：所有测试数据、凭据、路径、超时值都应放配置文件或环境变量中，代码中零硬编码。

### 2. 裸 except 吞异常（严重）
- pages/login_page.py:42 — except: pass 直接吞掉所有异常
- pages/product_page.py:34 、 43 、 53 等多处 — except: 无异常类型，出问题时完全无法排查
企业级做法 ：必须指定具体异常类型（如 TimeoutException ），至少 logging.warning 记录。

### 3. 配置管理不规范（中等）
- config/settings.py — SettingsBackend 和 SettingsFrontend 两个类代码几乎完全重复，违反 DRY 原则
- 每次实例化都重新读文件 open("config/env.yaml") ，应只加载一次
- 没有考虑环境变量覆盖（CI/CD 中常用）
- 配置路径 "config/env.yaml" 是相对路径，非项目根目录运行会失败
企业级做法 ：单例配置类 + 环境变量覆盖 + pathlib.Path 计算项目根目录的绝对路径。

### 4. DriverManager 过于简陋（中等）
- core/driver_manager.py — 只支持 Chrome，只有 13 行代码
- 没有支持 Firefox/Edge 等多浏览器切换
- 没有 headless 模式配置（CI 必需）
- 没有远程 WebDriver 支持（Selenium Grid / Docker）
- 没有驱动自动管理（如 webdriver-manager ）
### 5. 日志系统不完善（中等）
- BaseAPI 中有 logging 但没有配置 handler 和格式，日志可能不输出
- UI 层完全没有日志
- 没有统一的日志配置文件或初始化
企业级做法 ：全局日志配置（格式、级别、输出到文件+控制台），UI 操作关键步骤打日志。

### 6. 测试数据管理缺失（中等）
- 测试数据直接写在 @pytest.mark.parametrize 装饰器中
- 没有独立的测试数据文件（JSON/YAML/CSV）
- 没有数据工厂或 Faker 生成随机数据
- 注册测试每次写死新用户名，没有清理机制
企业级做法 ： data/ 目录管理测试数据，或使用 Factory/Faker 动态生成。

### 7. 断言方式不规范（轻微）
- 使用 assert xxx == True 而非直接 assert xxx
- 没有使用软断言（一个用例中多个断言，第一个失败后面的不执行）
- 缺少断言失败时的自定义消息
### 8. 测试用例设计问题（轻微）
- tests/ui/test_product.py:20 — expected_success 作为函数默认参数而非参数化数据传入，不规范
- test_product2_function_button 做了太多事情（查看、编辑、删除、导入），违反单一职责，应拆分
- 注册测试中 page_login 和 page_register 实际上是同一个类的两个实例，令人困惑
- 没有 __init__.py 包标识
### 9. conftest.py 设计问题（轻微）
- conftest.py:29 — SLOW_MODE = True 全局变量 + pause() 函数，用 time.sleep 控制速度，非常原始
- conftest.py:17 — driver fixture 是 session 级别，所有 UI 测试共享一个浏览器，测试间状态会互相影响
- general_login 也是 session 级别，登录状态可能被其他用例破坏
企业级做法 ： driver 通常用 class 或 function scope，配合 autouse 或按需实例化。

### 10. 缺失的关键模块
缺失模块 

1. pytest.ini / pyproject.toml 	没有 pytest 配置文件，缺少 markers 定义、日志配置, allure 报告配置 
2. 日志模块            无统一日志初始化 
3. 截图/录屏          UI 测试失败时无自动截图 
4. 报告生成         引入了 allure-pytest 但没有配置和使用 
5. __init__.py              各目录缺少包标识 
6. 重试机制             UI 测试无失败重试（flaky test 处理） 
7. CI/CD 配置           无 Jenkinsfile / GitHub Actions
8.  数据清理           测试后无数据还原机制 
9. 通用工具类         缺少文件操作、加密解密、时间处理等工具 
10. BaseAPI 响应封装            没有统一响应模型，每次手动取 result.status_code
