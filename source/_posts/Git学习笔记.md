---
title: Git学习笔记
date: 2025-04-01 14:00:35
tags: ['Git']
categories: Git
cover: https://blog-ultimate.oss-cn-beijing.aliyuncs.com/cover/R.jpg
---

# Windows Command

## dir

dir命令用于显示当前目录下的文件和子目录列表。

```bash
dir
```

## cd

cd命令用于更改当前工作目录。

```bash
# 进入某个目录
cd [目录路径]

# 返回上一级目录
cd ..
```

如果想换到某个盘

```bash
# 从C盘换到D盘
C:\Users\艾克拜尔>D:

D:\>
```

## mkdir

mkdir命令用于创建新目录。

```bash
mkdir [目录名]  
```

## rmdir

rmdir命令用于删除空目录。

```bash
rmdir [目录名]
```

`rmdir /s`命令用于删除非空目录及其所有内容。

```bash
rmdir /s [目录名]
```

## copy
copy命令用于复制文件。

```bash
copy [源文件路径] [目标文件路径]
```

如果想复制文件到上一个目录

```bash
copy test.txt ..
```

复制到上一个目录中的test文件夹

```bash
copy test.txt ..\test
```

## move

move命令用于移动或重命名文件。

```bash
move [源文件路径] [目标文件路径]
```

## echo

echo命令可以用于创建文件并向其中写入内容。

```bash
echo 这是文件内容 > [文件名.后缀]
```

如果不想写入内容，而是创建一个空文件，可以使用以下命令：

```bash
echo null > hello.js
```

## del

del命令用于删除文件。

```bash
del [文件名]
```

# 基础概念与文件状态

在 Git 中，文件主要有几种状态：**未跟踪 (Untracked)**、**已跟踪 (Tracked)**（包括**已暂存 (Staged)** 和 **已提交 (Committed)**）。

## 文件状态流转

- **未跟踪 (Untracked)**: 当我们在 Git 仓库中新建一个文件时，Git 并不知道它的存在，它还没有被添加到暂存区。
- **已跟踪 (Tracked)**: 当我们使用 `git add` 命令将文件添加到暂存区后，Git 开始监视它的变化。

## 常用基础命令

- **查看状态**:

  ```bash
  git status
  ```

  这是最常用的命令，用于查看工作区和暂存区的状态。

- **查看被跟踪的文件**:

  ```bash
  git ls-files
  ```

  列出当前版本库中所有被跟踪的文件。

- **添加文件到暂存区**:

  ```bash
  git add [文件名]
  git add .  # 添加当前目录下所有修改
  ```

- **提交到本地仓库**:
  ```bash
  git commit -m "提交说明"
  ```

# 查看日志与版本

查看提交历史是了解项目演进的重要方式。

- **详细日志**:

  ```bash
  git log
  ```

  ![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/Snipaste_2025-04-03_19-44-50.png)

- **简洁日志**:
  ```bash
  git log --oneline
  ```
  ![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/Snipaste_2025-04-03_19-20-42.png)

# 分支管理 (Branch)

分支是 Git 的核心概念之一。它允许你在不影响主线（通常是 `master` 或 `main`）的情况下进行开发和实验。

## 什么是 HEAD 指针？

HEAD 是一个指向当前分支最新提交的指针。简单来说，HEAD 告诉 Git 你当前所在的位置。当你切换分支时，HEAD 会自动更新。

## 分支操作命令 (新旧对比)

Git 2.23 版本引入了 `switch` 和 `restore` 命令，以分离 `checkout` 过于复杂的职责。

| 操作           | 旧命令 (`checkout`)        | 新命令 (`switch`)        |
| :------------- | :------------------------- | :----------------------- |
| **查看分支**   | `git branch`               | `git branch`             |
| **查看所有分支** | `git branch -a`           | `git branch -a`          |
| **查看远程分支** | `git branch -r`           | `git branch -r`          |
| **创建分支**   | `git branch [分支名]`      | `git branch [分支名]`    |
| **切换分支**   | `git checkout [分支名]`    | `git switch [分支名]`    |
| **创建并切换** | `git checkout -b [分支名]` | `git switch -c [分支名]` |
| **删除分支**   | `git branch -d [分支名]`   | `git branch -d [分支名]` |
| **强制删除**   | `git branch -D [分支名]`   | `git branch -D [分支名]` |

> **注意**: `git branch -d` 只能删除已经合并的分支，如果分支未合并，需要使用 `-D` 强制删除。

## Detached HEAD (游离 HEAD) 状态

当你检出一个具体的提交（Commit ID）而不是分支名时，HEAD 会进入 "detached HEAD" 状态。
在此状态下的提交不会属于任何分支，一旦切换走，这些提交很可能会丢失（除非你新建一个分支指向它们）。

# 合并与变基

## 合并分支 (Merge)

假设我们要把 `feature` 分支合并到 `master` 分支：

```bash
git switch master   # 1. 切换到目标分支
git merge feature   # 2. 执行合并
```

### 合并模式

- **Fast-forward (快进模式)**:
  当目标分支（master）没有新的提交，Git 只是简单地把指针向前移动。
  ![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251219084016353.png)

- **Recursive (递归/三方合并)**:
  当目标分支也有新的提交时，Git 会创建一个新的 **Merge Commit**。
  ![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251219090059645.png)

## 解决冲突 (Conflict)

当两个分支修改了同一文件的同一部分时，Git 无法自动合并，会产生冲突。

- 使用 `git status` 查看冲突文件。
- 手动编辑文件，选择保留的代码（Accept Current/Incoming/Both）。
- 解决后执行 `git add` 和 `git commit` 完成合并。

常用辅助命令：

```bash
git merge --abort   # 放弃合并，回到合并前状态
git log --merge     # 查看冲突的提交记录
git diff            # 查看具体差异
```

## 变基 (Rebase)

`rebase` 用于将一个分支的修改“重新播放”到另一个分支上，使提交历史变成线性的，而不是分叉的。

```bash
git switch feature
git rebase master
```

## 摘取提交 (Cherry-pick)

如果你只想要另一个分支的**某一个**特定提交，而不是合并整个分支：

```bash
git cherry-pick [Commit-ID]
```

# 撤销、回退与恢复

这是 Git 中最容易混淆的部分，Git 2.23 引入的 `restore` 命令让逻辑更清晰。

## 抛弃工作区的修改 (未 add)

当你修改了文件但还没添加到暂存区，想恢复原样：

| 场景             | 旧命令                     | 新命令                 |
| :--------------- | :------------------------- | :--------------------- |
| **恢复指定文件** | `git checkout -- [文件名]` | `git restore [文件名]` |
| **恢复所有文件** | `git checkout -- .`        | `git restore .`        |

## 撤销暂存区的修改 (已 add，未 commit)

当你执行了 `git add`，但想撤回这个操作（不删除文件内容，只是从暂存区移除）：

| 场景           | 旧命令                    | 新命令                          |
| :------------- | :------------------------ | :------------------------------ |
| **移出暂存区** | `git reset HEAD [文件名]` | `git restore --staged [文件名]` |

## 版本回退 (Reset)

用于回退到之前的提交版本。

- **Soft 回退 (保留修改)**:

  ```bash
  git reset --soft [版本号/HEAD^]
  ```

  **最常用**。回退后，工作区和暂存区的修改都会保留。你只是“撤销了 commit 动作”。

- **Hard 回退 (丢弃修改)**:
  ```bash
  git reset --hard [版本号/HEAD^]
  ```
  **危险操作**。回退后，工作区和暂存区的所有修改都会被**彻底删除**。

## 救命稻草：Reflog

如果你不小心 `reset --hard` 丢掉了重要代码，或者误删了分支，可以用 `reflog` 找回。
`git reflog` 记录了 HEAD 指针的所有变动历史。

```bash
# 1. 查看操作记录，找到丢失前的版本号 (例如 HEAD@{1})
git reflog

# 2. 恢复到那个版本
git reset --hard HEAD@{1}
# 或者创建一个新分支指向它
git branch recover-branch HEAD@{1}
```

# 文件操作与暂存技巧

## 删除文件

- **常规删除**:

  ```bash
  git rm test.txt
  git commit -m "删除文件"
  ```

- **仅停止跟踪 (保留本地文件)**:
  常用于误传了配置文件，想从 Git 中删除但本地还需要用。

  ```bash
  git rm --cached config.xml
  # 然后记得把 config.xml 加入 .gitignore
  ```

- **清理未跟踪文件**:
  ```bash
  git clean -f    # 强制删除所有未跟踪的文件
  ```

## 临时保存工作现场 (Stash)

当你正在开发功能 A，突然需要去修复 Bug B，但功能 A 还没写完不能提交时：

- **保存现场**:

  ```bash
  git stash
  git stash push -m "暂存功能A的修改"
  ```

- **查看列表**:

  ```bash
  git stash list
  ```

- **恢复现场**:
  ```bash
  git stash pop   # 恢复并删除记录
  git stash apply # 恢复但不删除记录
  ```

# 远程仓库 (Remote)

- **关联远程仓库**:

  ```bash
  git remote add origin [仓库地址]
  ```

- **查看远程仓库**:

  ```bash
  git remote -v
  ```

- **修改远程地址 (例如 HTTPS 转 SSH)**:

  ```bash
  git remote set-url origin [新地址]
  ```

- **删除远程关联**:
  ```bash
  git remote remove origin
  ```

- **推送到远程仓库**:

  ```bash
  git push -u origin master
  ```
  这里的 `-u` 参数会把本地的 `master` 分支和远程的 `master` 分支关联起来，后续只需执行 `git push` 即可。


## Local Branch 与 Remote Branch 对应关系

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251219102217793.png)
![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251219184813069.png)

把`Remote Tracking Branch`分支可以理解成远程仓库的本地镜像。不能直接修改它。
`Local Tracking Branch`分支是我们本地实际操作的分支。

我们进行`git push origin main`操作时，实际上是把本地的`main`分支推送到远程仓库的`main`分支，同时更新本地的`origin/main`分支。
我们进行`git pull origin main`操作时，实际上是先把远程仓库的`main`分支拉取到本地的`origin/main`分支，然后将`origin/main`分支的内容合并到本地的`main`分支。就是进行了`git fetch`和`git merge`两个操作。

- **git ls-remote**：查看远程仓库的引用信息，包括分支。

- **git fetch**：从远程仓库获取最新的分支和标签信息，但不进行合并操作。

- **git pull origin main**： 从远程仓库的 `main` 分支拉取最新的代码并合并到当前分支。
