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
你现在需要写一篇论文，论文题目为：基于拍照识别的校园植物百科检索系统。论文写在项目文件夹中的“2311多媒体技术报告.docx”文件中，目前这个.docx文件第一页已经写好，你不要动第一页，你从第二页开始写（没有页码自己创建）。
内容要求：
1. 论文包含摘要、目录、正文、参考文献。
2. 论文页数控制在18~30页范围，最好是25页。
3. 需求分析主要做系统功能性需求分析，结合相关图表工具（用例图、系统功能结构图等）。
4. 概要设计（系统架构设计与数据库设计，注意我们是强调多媒体数据库设计，这里大家可以借助AI大模型对系统进行分析，如何具体实现多媒体数据结构设计与存储）。
5. 系统详细实现方法介绍（这一章主要介绍核心功能模块实现流程方法，不需要给出具体代码）。
6. 论文围绕着题目“基于拍照识别的校园植物百科检索系统”来写。
格式要求：
- 页面设置 ：A4纸，上下边距2.54cm，左右边距均为3.17cm，纵向
- 论文标题 ：黑体，小二号（22磅），加粗，居中，无首行缩进
- 摘要/Abstract标题 ：黑体，小三号（15磅），加粗，居中，段后15磅
- 章标题（Heading 1） ：黑体，小三号（15磅），加粗，左对齐，1.5倍行距，段前12磅/段后9磅
- 节标题（Heading 2） ：黑体，四号（14磅），加粗，左对齐，1.5倍行距，段前9磅/段后6磅
- 小节标题（Heading 3） ：黑体，小四号（12磅），加粗，左对齐，1.5倍行距，段前6磅/段后4磅
- 正文 ：宋体，小四号（12磅），不加粗，两端对齐，首行缩进0.85cm，1.5倍行距
- 关键词/Keywords ：宋体，小四号（12磅），不加粗，两端对齐，无首行缩进，1.5倍行距
- 参考文献条目 ：宋体，小四号（12磅），不加粗，两端对齐，无首行缩进，1.5倍行距
- 表格内容 ：宋体，小四号（12磅），表头加粗/数据行不加粗，居中对齐
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

# 1.1 只是拉去最新的提交版本
git clone --depth 1 https://github.。。。/.git

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
