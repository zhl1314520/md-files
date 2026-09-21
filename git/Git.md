**Git** 

```bash
# 进入项目路径
如：cd D:\PyCharm\Project

# 把当前项目变成 Git 仓库
git init

# 添加所有文件
git add .

# 提交版本（参数可改）
git commit -m "first commit"

# 绑定仓库
git remote add origin https://gitee.com/你的用户名/仓库名.git

# 推送（master）
git push -u origin master/main
```

**更新**

```bash
# 添加所有文件
git add .

# 参数可改
git commit -m "update something"

git push
```



- 一般 Python 项目不会推 .venv，但是会上传 依赖列表 

  执行

  ```bash
  pip freeze > requirements.txt
  
  git add requirements.txt
  
  git commit -m "添加依赖列表"
  
  git push
  ```

- 别人只需要下面命令就可以恢复环境

  ```bash
  pip install -r requirements.txt
  ```

**Git 拉取项目**

```bash
# 1. 克隆仓库
git clone https://github.com/username/reponame.git

# 1.1 只是拉去最新的提交版本
git clone --depth 1 https://github.。。。/.git

# 2. 进入项目目录
cd reponame

# 3. 安装依赖
npm install

# 4. 启动开发模式
npm run dev
```

**Git 拉取项目中某个文件夹**

```bash
git clone --filter=blob:none --no-checkout 仓库名.git

cd 仓库

git sparse-checkout init --cone

git sparse-checkout set 所需文件夹名

git checkout main
```

**Git 回滚**

```bash
git reset --hard HEAD	# 回滚到上一次提交的版本（前提：中间没有再 commit 了）

git log --oneline		# 找到提交

git reset --hard f6g7h8i # 彻底回退到 f6g7h8i 所在版本（f6g7h8i 后面的版本会消失）

git checkout -b fix-from-v4.22 f6g7h8i  # 从 V4.22 创建新分支，不影响主分支
```

**查看本地仓库账号、邮箱**

```bash
git config --global user.name
git config --global user.email

# 一键查看
git config --global --list
```

**设置 username、email**

```bash
git config --global user.name "developer"
git config --global user.email "1XXXX@163.com"
```

**查看分支**

```bash
git branch
```

**查看 pull、push 地址**

```bash
git remote -v

# 输出
origin  git@github.com:zhl1314520/application-extension.git (fetch)
origin  git@github.com:zhl1314520/application-extension.git (push)
```

**修改本地分支：master -> main**

```bash
git branch -m master main
```

**.gitignore** 

```
是项目的工程级文件，放入 Git 上传仓库排除的对象
```

**Linux 开发还有个 SSH key 来避免频繁输入账号和token**

```bash
# 查看 ssh key
ls -al ~/.ssh

# 生成 ssh key
ssh-keygen -t ed25519 -C "GitHub邮箱"

# 获取 ssh key（3次回车）
cat ~/.ssh/id_ed25519.pub

# 生成 2 个 key
/home/zhl/.ssh/id_ed25519       ← 私钥，千万不要泄露
/home/zhl/.ssh/id_ed25519.pub   ← 公钥，可以放到 GitHub

# 测试是否配置成功(输出 successful)
ssh -T git@github.com			

# 需要改为 ssh
git remote set-url origin git@github.com:zhl1314520/application-extension.git

# 推送都是一样的
git push -u origin main
```

