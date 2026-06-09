## 命令行推代码

```bash
# 进入项目路径
如：cd D:\PyCharm\Project\toutiao

# 把当前项目变成 Git 仓库
git init

# 去除 .venv 推送
# 在项目位置（D:\PyCharm\Project\toutiao）里面新建文件（.gitignore）
# 里面写入规则
# 如下：
---------------
# Python虚拟环境
.venv/
venv/

# PyCharm配置
.idea/

# Python缓存
__pycache__/
*.pyc
----------------

# 添加所有文件
git add .

# 提交版本（参数可改）
git commit -m "first commit"

# 绑定仓库
git remote add origin https://gitee.com/你的用户名/仓库名.git

# 推送（master）
git push -u origin master/main

```

## 后续更新分支

```bash
# 添加所有文件
git add .

# 参数可改
git commit -m "update something"

git push
```



- ### 一般 Python 项目不会推 .venv，但是会上传 依赖列表 

  执行

  ```bash
  pip freeze > requirements.txt
  
  git add requirements.txt
  
  git commit -m "添加依赖列表"
  
  git push
  ```

- ### 别人只需要下面命令就可以恢复环境

  ```bash
  pip install -r requirements.txt
  ```

## Git 拉取项目

```bash
# 1. 克隆仓库
git clone https://github.com/username/reponame.git

# 2. 进入项目目录
cd reponame

# 3. 安装依赖
npm install

# 4. 启动开发模式
npm run dev
```

## Git 拉取项目中某个文件夹

```bash
git clone --filter=blob:none --no-checkout 仓库名.git

cd 仓库

git sparse-checkout init --cone

git sparse-checkout set 所需文件夹名

git checkout main
```

## Git 回滚

```bash
git reset --hard HEAD	# 回滚到上一次提交的版本（前提：中间没有再 commit 了）

git log --oneline		# 找到提交

git reset --hard f6g7h8i # 彻底回退到 f6g7h8i 所在版本（f6g7h8i 后面的版本会消失）

git checkout -b fix-from-v4.22 f6g7h8i  # 从 V4.22 创建新分支，不影响主分支
```

## 查看本地仓库邮箱

```bash
git config user.email
```

## 查看分支

```bash
git branch
```

## 修改本地分支：master -> main

```bash
git branch -m master main
```
