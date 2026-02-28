# GitHub 命令使用指南

## 简介
本指南介绍如何使用 Git 命令行工具管理 GitHub 仓库，包括文件上传、版本控制等基本操作。

## 环境准备

### 1. 安装 Git

#### Windows
```bash
# 下载 Git for Windows
# 访问: https://git-scm.com/download/win

# 验证安装
git --version
```

#### macOS
```bash
# 使用 Homebrew 安装
brew install git

# 验证安装
git --version
```

#### Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install git

# 验证安装
git --version
```

### 2. 配置 Git

```bash
# 设置用户名
git config --global user.name "Your Name"

# 设置邮箱
git config --global user.email "your.email@example.com"

# 查看配置
git config --list
```

### 3. 配置 GitHub SSH 密钥

```bash
# 生成 SSH 密钥
ssh-keygen -t ed25519 -C "your.email@example.com"

# 查看公钥内容
cat ~/.ssh/id_ed25519.pub

# 将公钥添加到 GitHub 账户
# 1. 登录 GitHub
# 2. 进入 Settings > SSH and GPG keys
# 3. 点击 "New SSH key"
# 4. 粘贴公钥内容
```

## 基本操作命令

### 1. 克隆仓库

```bash
# 克隆远程仓库到本地
git clone <repository-url>

# 示例
git clone https://github.com/username/repository.git
```

### 2. 创建新仓库

```bash
# 初始化本地仓库
git init

# 创建并切换到新分支
git checkout -b main
```

### 3. 添加文件到暂存区

```bash
# 添加单个文件
git add filename.txt

# 添加所有文件
git add .

# 添加所有特定类型文件
git add *.md

# 添加除特定文件外的所有文件
git add . ':!node_modules'
```

### 4. 提交更改

```bash
# 提交暂存区的文件
git commit -m "提交信息"

# 添加并提交所有更改的文件
git commit -a -m "提交信息"

# 修改最后一次提交
git commit --amend -m "新的提交信息"
```

### 5. 推送到远程仓库

```bash
# 推送到主分支
git push origin main

# 推送到指定分支
git push origin <branch-name>

# 强制推送（谨慎使用）
git push -f origin main
```

### 6. 拉取远程更改

```bash
# 拉取并合并远程更改
git pull origin main

# 仅拉取不合并
git fetch origin
```

## 分支管理

### 1. 查看分支

```bash
# 查看所有本地分支
git branch

# 查看所有远程分支
git branch -r

# 查看所有分支（本地+远程）
git branch -a
```

### 2. 创建和切换分支

```bash
# 创建新分支
git branch <branch-name>

# 切换分支
git checkout <branch-name>

# 创建并切换到新分支
git checkout -b <branch-name>

# 使用 switch 命令（Git 2.23+）
git switch <branch-name>
git switch -c <new-branch-name>
```

### 3. 合并分支

```bash
# 切换到目标分支
git checkout main

# 合并指定分支
git merge <branch-name>

# 合并并压缩提交
git merge --squash <branch-name>
```

### 4. 删除分支

```bash
# 删除本地分支
git branch -d <branch-name>

# 强制删除分支
git branch -D <branch-name>

# 删除远程分支
git push origin --delete <branch-name>
```

## 文件上传完整流程

### 方法一：新仓库上传

```bash
# 1. 创建本地文件夹
mkdir my-project
cd my-project

# 2. 初始化 Git 仓库
git init

# 3. 创建或复制文件到文件夹
# 例如：创建 README.md
echo "# My Project" > README.md

# 4. 添加文件到暂存区
git add .

# 5. 提交更改
git commit -m "Initial commit"

# 6. 在 GitHub 创建新仓库（网页版）
# 登录 GitHub > New repository

# 7. 添加远程仓库地址
git remote add origin https://github.com/username/repository.git

# 8. 推送到远程仓库
git push -u origin main
```

### 方法二：现有仓库上传

```bash
# 1. 克隆现有仓库
git clone https://github.com/username/repository.git
cd repository

# 2. 复制要上传的文件到仓库文件夹
cp /path/to/your/file .

# 3. 添加文件到暂存区
git add .

# 4. 提交更改
git commit -m "Add new files"

# 5. 推送到远程仓库
git push origin main
```

## 状态查看命令

### 1. 查看仓库状态

```bash
# 查看当前状态
git status

# 简洁状态
git status -s
```

### 2. 查看提交历史

```bash
# 查看提交历史
git log

# 简洁历史
git log --oneline

# 图形化历史
git log --graph --oneline --all
```

### 3. 查看文件差异

```bash
# 查看工作区和暂存区的差异
git diff

# 查看暂存区和最新提交的差异
git diff --cached

# 查看两个提交之间的差异
git diff commit1 commit2
```

## 高级操作

### 1. 撤销操作

```bash
# 撤销工作区的修改
git checkout -- filename

# 撤销暂存区的修改
git reset HEAD filename

# 撤销最近一次提交
git reset --soft HEAD~1

# 彻底删除最近一次提交
git reset --hard HEAD~1
```

### 2. 标签管理

```bash
# 创建标签
git tag v1.0.0

# 推送标签到远程
git push origin v1.0.0

# 推送所有标签
git push origin --tags
```

### 3. 忽略文件

创建 `.gitignore` 文件：

```
# 忽略 node_modules 文件夹
node_modules/

# 忽略日志文件
*.log

# 忽略系统文件
.DS_Store
Thumbs.db

# 忽略配置文件
.env
config.json
```

## 常用工作流程

### 1. 日常开发流程

```bash
# 1. 拉取最新代码
git pull origin main

# 2. 创建功能分支
git checkout -b feature/new-feature

# 3. 开发完成后提交
git add .
git commit -m "Add new feature"

# 4. 推送到远程
git push origin feature/new-feature

# 5. 在 GitHub 创建 Pull Request
```

### 2. 修复 bug 流程

```bash
# 1. 从 main 分支创建修复分支
git checkout -b fix/bug-description main

# 2. 修复 bug 并提交
git add .
git commit -m "Fix: bug description"

# 3. 推送到远程
git push origin fix/bug-description

# 4. 创建 Pull Request
```

## 故障排除

### 1. 权限问题

```bash
# 检查 SSH 连接
ssh -T git@github.com

# 如果使用 HTTPS，配置凭据缓存
git config --global credential.helper cache
```

### 2. 合并冲突

```bash
# 当出现冲突时，手动编辑冲突文件
# 然后标记为已解决
git add conflicted-file.txt

# 完成合并
git commit
```

### 3. 推送失败

```bash
# 先拉取最新代码
git pull origin main

# 解决可能的冲突
# 然后再次推送
git push origin main
```

## 最佳实践

1. **提交信息规范**：
   - 使用清晰、简洁的提交信息
   - 遵循约定式提交规范

2. **分支策略**：
   - main 分支保持稳定
   - 功能开发使用 feature 分支
   - bug 修复使用 fix 分支

3. **定期同步**：
   - 经常拉取远程最新代码
   - 避免长时间在本地分支开发

4. **.gitignore**：
   - 及时更新忽略文件列表
   - 不要提交敏感信息

## 参考资源

- [Git 官方文档](https://git-scm.com/doc)
- [GitHub 官方指南](https://docs.github.com)
- [Pro Git 书籍](https://git-scm.com/book/zh/v2)

---

**文档创建时间**: 2026-02-28
**适用版本**: Git 2.23+
**最后更新**: 2026-02-28