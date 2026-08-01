## 使用 pytest 命令行跑用例
> ```powershell
> pytest tests\ui -v				    # 跑所有 UI 用例
> 
> pytest tests\ui\test_login.py -v	# 跑登录模块
> 
> pytest tests\ui\test_login.py::test_login -v -s		# 跑单个登录用例
> 
> allure server allure-results		# 打开报告
> ```

## 如何生成 Allure 测试报告

1. #### 在用例(.py)所在文件夹中：pytest -v --alluredir=allure-results

2. #### 跑指定用例：pytest xx.py -v --alluredir=allure-results

3. #### cmd 里面输入：allure serve allure-results

## pytest [-k，-m，-v，-x，-s]

- #### pytest -k login：只要函数名包含 login 就执行

- #### pytest -v：详细输出

- #### pytest -x：遇到失败就停止

- #### pytest -s：显示  print 语句的内容

## pytest 为什么要设计 fixture ？

1. 减少重复工作
   - 打开浏览器
   - 登录账号
   - 初始化数据
   - 清理数据
   - 建立连接（SQL）
   - quit
2. 统一封装重复的代码
3. 自动 setup/teardown（资源）
4. 自动注入依赖
