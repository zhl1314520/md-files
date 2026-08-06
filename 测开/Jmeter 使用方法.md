## 对于一般的 GET 请求压测时只要下面的 4 个

- ### 创建线程组

> Test Plan——>add——>Thread(Users)——>Thread Group
>
>
> 常见 3 个参数：
>
> 1. number of threads：模拟并发用户数
> 2. ramp-up period：启动这些用户所需要的时间（s)
> 3. Loop count：循环次数,每个用户执行请求的次数

- ### 添加 Http Request

> Thread Group——>add——>Sampler——>HTTP Request
>
> 参数：
>
> 1. protocol：协议
> 2. server name or ip：请求地址
> 3. port：端口
> 4. method：请求方法
> 5. path：具体路径，如：/login

- ### 添加查看结果树 view result tree

>Thread Group——>add——>Listener——>view results tree
>
>可以看到：
>
>- 请求内容（Request）
>- 响应内容（Response）
>- 响应头（Headers）
>- HTTP 状态码（200、404、500 等）等配置信息

- ### 添加 Summary Report（性能统计）

>Thread Group——>add——>Listener——>Summary Report统计：
>
>- 请求次数（Samples）
>- 平均响应时间（Average）
>- 最小/最大响应时间（Min/Max）
>- 错误率（Error %）
>- 吞吐量（Throughput）

## 对于  Django 项目压测 POST /login 接口，data 表单提交的配置

### 特殊：Django 项目需要先创建 GET 请求页来获取 CSRFMiddleWareToken 值

### data 表单提交

![Django 1](D:\Jmeter\操作图片\Django 1.png)

![Django 2](D:\Jmeter\操作图片\Django 2.png)

![Django 3](D:\Jmeter\操作图片\Django 3.png)

![Django 4](D:\Jmeter\操作图片\Django 4.png)

![Django 5](D:\Jmeter\操作图片\Django 5.png)

## JSON 提交

