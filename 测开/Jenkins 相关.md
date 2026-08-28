## 启动 Jenkins 服务

- ##### PS D:\Jenkins> & "D:\JDK17\bin\java.exe" "-Dfile.encoding=UTF-8" -jar "jenkins.war" --httpPort=8081

## Jenkinsfile 文件自动化流水线逻辑

                    Jenkins Pipeline
                           │
                           ▼
                    parameters
                           │
          ┌────────────────┼────────────────┐
          │                           │                            │
         ENV                         SCOPE                          MARKERS
          │                           │                              │
       dev/test/prod                 all/ui/api                       smoke/...
          │                           │                             │
          └────────────────┼────────────────┘
                           ▼
                       Checkout
                           │
                           ▼
                    拉取 Git 代码
                           │
                           ▼
                         Setup
                           │
                           ▼
                  安装 Python 依赖
                           │
                           ▼
                ┌──────┴──────┐
                 │                      │
           SCOPE=all                SCOPE=api
                │                      │
                └──────┬──────┘
                           ▼
                       API Tests
                           │
                           ▼
                    ┌─────────────┐
                    │                      │
                 SCOPE=all              SCOPE=ui
                    │                      │
                    └──────┬──────┘
                           ▼
                        UI Tests
                           │
                           ▼
                     MARKERS 不为空？
                          │
                        是│
                          ▼
                       pytest -m
                          │
                          ▼
                      allure-results
                          │
                          ▼
                         post
                          │
             ┌────────┴────────┐
             │                             │
           always                        failure
             │                             │
        Allure 报告                        打印错误
             │
        cleanWs()

## 如何配置在 Jenkins 里面配置流水线（Pipeline）实现：

> Jenkins
>    ↓
> 使用 github-jenkins
>    ↓
> GitHub
>    ↓
> clone 你的仓库
>    ↓
> 找到 Jenkinsfile
>    ↓
> 执行 Jenkinsfile

1. 安装 Pipeline 插件（Jenkins 版本不能太低，插件有的要版本要求）
   - 点击右上角的 manage 图标，选择 available plugins，搜索：Pipeline，下载，重启 Jenkins
2. 创建 Item
   - 选择“流水线”，确定
   - 滑到最下面——定义——Pipeline Script from SCM
   - SCM：选择 Git，填写（Repository URL、指定分支、脚本路径：一般就是 Jenkinsfile）、Credentials（选填：public 项目不用填也行），若填写：
     - Credentials 值：先去 GitHub 找到 Credentials—Fine-grained personal access tokens
     - 选择 username + password：username = GitHub 的用户名（zhl1314520），password =  Credentials 值，ID = github-jenkins，Description = “。。。。。。”
   - 保存
3. 即可开始流水线了

## 必要的插件

### Allure Jenkins Plugin：allure 与 Jenkins 交流的桥梁

- 下载：available plugins：搜索 Allure ，下载即可

### Allure Commandline：配置（靶场框架项目使用的是 allure2）

- manage jenkins——tools：找到 Allure Commandline 安装，点击新增，name：。。。，Install automatically: ✓

- version：2.39.0（使用本地的 allure ），保存

## Jenkins 跑用例失败报错定位技巧

1. 进入 console output
2. 选择 view as text
3. 快捷键：搜索：
   - FAILED、ERROR、Traceback、Error
   - 最关键的信息：short test summary info

## 常见的错误

> 元素不可交互（不能点击）
>
> ```
> selenium.common.exceptions.ElementNotInteractableException: Message: element not interactable
> ```

- ### 原因

  > Jenkins 采用 headless 模式，浏览器窗口过小，看到元素，但是需要滑动窗口才能点击元素

- ### 解决

  > 设置 driver 里面的	driver.set_window_size(1920, 1080)
