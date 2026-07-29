## FastAPI 运行命令（热启动）

### uvicorn main:app --reload

- reload：刷新网页不用重启项目，实时更新网页数据
- uvicorn：是一个**高性能的 ASGI（Asynchronous Server Gateway Interface）服务器**，专为 Python 的异步 Web 框架（如FastAPI）设计

## 项目根目录下的 requirements.txt

> 一般 Python 项目不会推 .venv，但是会上传 "依赖列表 : requirements.txt"

- 执行


```powershell
pip freeze > requirements.txt

git add requirements.txt

git commit -m "添加依赖列表"

git push
```

> 别人只需要下面命令就可以恢复环境

```powershell
pip install -r requirements.txt
```

## 中间件（middleware）与依赖注入（DI）的区别

- 中间件：处理统一的逻辑（所有位置生效）
- 依赖注入：处理统一的逻辑（指定的位置生效）Depends

## 虚拟环境 venv

- #### 进入目录

- #### python -m venv .venv（创建名为：.venv 的虚拟环境）

- #### .venv\Scripts\Activate（激活虚拟环境）

- #### deactivate（退出虚拟环境）

- #### pip install -r requirements.txt（虚拟环境被破坏）

- ####  .\.venv\Scripts\Activate（文件中存在.venv虚拟环境，重新激活）     

##  pip 

> ```powershell
> pip show fastapi 	# 展示某个包的版本信息
> ```

## java 集合 & python 集合

> Java                       Python
>
> HashMap     ≈       dict
> HashSet       ≈       set
> ArrayList      ≈       list
> LinkedList    ≈      deque/list

## 包，模块，函数，类

> package = 一个包含多个 module 的目录
> module = 一个 `.py` 文件
>
> 一个 module = 多个类
