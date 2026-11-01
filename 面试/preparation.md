1. 了解 POM吗？为什么要使用这个设计思想

   ```
   POM 全称是 Page Object Model，页面对象模型，是 UI 自动化测试中常用的一种设计模式
   核心思想：将页面元素定位和页面操作封装到对应的 Page 类中，测试用例只负责调用 Page 类提供的方法，不直接编写元素定位和操作
   业务和页面操作分离
   
   好处：
   降低代码重复：页面操作可以封装复用
   降低维护成本：页面元素发生变化时，通常只需要修改对应的 Page 类
   提高代码可读性：测试用例关注业务流程，而不是元素定位细节
   降低耦合：页面操作和测试业务逻辑分离
   ```

2. conftest.py 文件是干嘛的，在pytest框架中有什么作用

   ```
   专门用于存放共享测试配置和 Fixture 的文件，减少导入操作，pytest自动识别注入
   
   定义公共 Fixture，例如浏览器启动和关闭
   定义前置和后置操作
   定义 Hook，例如测试用例执行失败后自动截图
   定义测试数据或公共辅助逻辑
   ```

3. Jenkinsfile文件是是干嘛的，有什么作用

   ```
   流水线编排文件，一般 Groovy 编写
   取代人为操作：代码拉取、环境准备、执行测试、生成测试报告
   pipeline {
       agent any
       stages {
           stage('拉取代码') {
               steps {
                   git 'https://github.com/example/project.git'
               }
           }
           stage('安装依赖') {
               steps {
                   bat 'pip install -r requirements.txt'
               }
           }
           stage('执行测试') {
               steps {
                   bat 'pytest -m smoke'
               }
           }
           stage('生成报告') {
               steps {
                   bat 'allure generate allure-results -o allure-report --clean'
               }
           }
       }
   }
   ```

4. pytest.ini 文件是干嘛的，在pytest框架中有什么作用

   ```
   Pytest 的配置文件，主要用于统一管理测试框架的运行配置，如规定一些测试文件、测试类、测试函数的命名规则
   
   统一管理 Pytest 的运行规则，便于团队管理规范
   ```

5. 夹具的作用是什么

   ```
   主要用于处理测试用例执行前的准备工作和执行后的清理工作
   如：
   测试前启动浏览器
   测试前准备测试数据
   测试前登录系统
   测试后关闭浏览器
   测试后清理数据库中的测试数据
   ```

6. fixture生命周期

   ```
   通过 scope 参数控制生命周期，主要有 5 种：session、package、module、class、function（默认）
   ```

7. 如果只想执行某一类用例，怎么办？

   ```
   使用 Pytest 的 -m 参数，结合自定义 Marker 来筛选测试用例，Marker 需要在 pytest.ini 中注册
   如：
   @pytest.mark.ui
   def test_home_page():
       pass
   // 执行 ui
   pytest -m ui
   
   // 执行 ui和api
   pytest -m "ui or api"
   
   // 不执行 ui
   pytest -m "not ui"
   ```

8. 假如说执行test_login.py文件中的用例，想要使用命令行跑用例，怎么写命令

   ```
   pytest test_login.py
   
   // 执行某个函数
   pytest test_login.py::test_login
   pytest -v -s：详细执行信息、print信息
   ```

9. 什么是参数化

   ```
   测试数据和测试逻辑分离，批量操作
   ```

10. Fixture 相比传统 setup/teardown 的优势：

    ```
    1. 可以通过参数注入，灵活使用
    2. 可以设置不同的作用域
    3. 可以实现 Fixture 之间的依赖
    4. 可以通过 `autouse=True` 自动使用
    ```

11. 接口自动化框架怎么搭，数据驱动怎么做的

    ```
    Pytest + Requests 搭建接口自动化测试框架，整体采用分层设计：
    配置层、数据层、公共封装层（封装 Requests 请求、日志、断言等公共方法）、业务层、测试用例层、报告层
    
    数据可以放在 json 里面
    ```

12. SQL：索引什么时候会失效

    1. 在索引列上使用函数

       ```
       -- 假设 create_time 有索引
       SELECT *
       FROM orders
       WHERE YEAR(create_time) = 2026;
       ```

    2. 在索引列上进行计算

       ```
       -- 假设 age 有索引
       SELECT *
       FROM user
       WHERE age + 1 = 20;
       ```

    3. 模糊查询以 % 开头

       ```
       -- 通常无法利用普通 B+Tree 索引定位
       SELECT *
       FROM user
       WHERE username LIKE '%admin';
       ```

    4. 使用 OR，部分条件没有索引

       ```
       SELECT *
       FROM user
       WHERE username = 'admin'
          OR age = 20;
       ```

13. Fixture 中的 `autouse=True` 是什么意思？

    ```
    autouse=True 表示自动使用 Fixture
    正常情况下，Fixture 需要在测试函数的参数中声明，Pytest 才会执行它
    ```

14. 如果一个 Fixture 依赖另一个 Fixture，应该怎么写？

    ```
    可以直接在 Fixture 的函数参数中声明另一个 Fixture 的名称，Pytest 会自动解析依赖关系，并按照依赖顺序执行
    
    * 较高作用域的 Fixture 不能依赖较低作用域的 Fixture
    ```

15. 如果测试用例执行失败，如何自动截图并保存到 Allure 报告？

    ```
    pytest --alluredir=allure-results
    
    Pytest Hook → 获取执行结果 → 判断失败 → 获取 Driver → Selenium 截图 → Allure 附件
    ```

16. Fixture 和 unittest 中的 setUp、tearDown 有什么区别？

    | 对比       | Pytest Fixture                            | unittest setUp/tearDown            |
    | ---------- | ----------------------------------------- | ---------------------------------- |
    | 前置操作   | Fixture 函数                              | `setUp()`                          |
    | 后置操作   | `yield` 后的代码                          | `tearDown()`                       |
    | 数据传递   | 参数注入                                  | 通常通过 `self` 属性               |
    | 作用域控制 | function、class、module、package、session | 主要按测试方法执行，另有类级别方法 |
    | 依赖关系   | 支持 Fixture 之间依赖                     | 通常通过继承或公共方法组织         |
    | 自动使用   | 支持 `autouse=True`                       | 由 unittest 测试生命周期调用       |
    | 参数化     | 支持 `parametrize`                        | 可通过 `subTest` 或其他方式实现    |

17. Fixture 中的 `yield` 和 `return` 有什么区别？

    ```
    核心：是否支持后置清理操作
    
    yield：会先把数据提供给测试用例，等测试用例执行结束后，再继续执行 yield 后面的代码
    ```