## quick start

![quick-start](D:\postman-readme\README\quick-start.png)

## 规范化

```
                    	   API 测试项目
                         	   │
                 ┌───────┴───────┐
                 ↓                         ↓
             Collection                Environment
                 │                         │
     ┌──────┼──────┐             │
      ↓         ↓          ↓              ↓
      登录       用户       项目            测试环境
        │      │          │
     └──────┼──────┘
                 ↓
             Tests 断言
                 ↓
          Collection Runner
                 ↓
              CI/CD
```



## 第三原则：敏感信息绝对不要乱放

这是公司里非常重要的规范。

比如：

```
password
token
api_key
client_secret
数据库密码
```

不要直接写：

```
password = 123456
```

然后把整个 Collection 导出给别人。

Postman 的环境变量可以区分共享值和本地值，并支持对敏感变量进行 Secure 处理；官方也明确建议用 Environment 管理这类环境相关信息。

你可以理解成：

```
普通变量：

base_url
username

敏感变量：

password
token
api_key
```

尤其是公司环境：

> **千万不要把生产环境 token、密码提交到 Git。**

------

## 第七原则：接口之间应该建立业务链路

这是公司 API 测试非常重要的一点。

例如：

```
登录
 ↓
获得 Token
 ↓
查询用户
 ↓
创建项目
 ↓
查询项目
 ↓
创建 Issue
 ↓
删除 Issue
```

不能每个接口都独立：

```
Login
User
Project
Issue
```

而应该能够形成：

```
登录
 ↓
Token
 ↓
User
 ↓
Project
 ↓
Issue
```

Postman 的 Collection Runner 可以按照指定顺序运行 Collection/Folder，并通过脚本在请求之间传递数据。

------

## 十、例如登录 Token 自动传给下一个接口

假设登录返回：

```
{
    "token": "abc123"
}
```

登录接口的 Post-response Script 可以保存：

```
const json = pm.response.json();

pm.environment.set("token", json.token);
```

然后下一个接口：

```
Authorization: Bearer {{token}}
```

这样：

```
Login
 ↓
自动提取 token
 ↓
保存 token
 ↓
User API
 ↓
Project API
```

不用你手工复制 Token。

这就是**自动化测试思维**。

## 十二、第九原则：最终要进入 CI/CD

这个就是“公司级”和“个人手工测试”最大的区别之一。

例如：

```
开发提交代码
      ↓
Git
      ↓
Jenkins / GitLab CI
      ↓
启动测试环境
      ↓
执行 API 测试
      ↓
Postman Collection
      ↓
PASS / FAIL
```

Postman 的 Collection 可以通过命令行工具运行并接入 CI/CD。现在官方提供 Postman CLI；历史上也广泛使用 Newman。

例如 CI 里最终类似：

```
postman collection run collection.yaml
```

或者旧的 Newman：

```
newman run collection.json
```

Newman 官方文档也明确支持把 Collection 放进 CI 环境，并根据退出码让 CI 判断成功/失败。

## 最后给你一个“公司里真正应该形成的闭环”

你以后可以把 API 测试理解成：

```
          接口文档
             ↓
        Postman Collection
             ↓
        Environment
             ↓
        API Request
             ↓
          Test断言
             ↓
       Collection Runner
             ↓
       Postman CLI / CI
             ↓
          Jenkins
             ↓
        测试结果/报告
```

而你之前学的东西又能接上：

```
Charles
  ↓
抓真实请求
  ↓
Postman
  ↓
验证接口功能
  ↓
Requests + Pytest
  ↓
代码化接口自动化
  ↓
JMeter
  ↓
性能/压力测试
```

## 若登录接口成功码是 302，但是 postman 其他的地方没有错误，总是返回 200，特别是 data 表单提交

- 可能解决
  - setting —— Automatically follow redirects 取消勾选