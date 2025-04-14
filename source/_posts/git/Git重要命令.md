---
title: Git重要命令
date: 2025-04-01 14:00:35
tags: ['Git']
categories: Git
cover: https://blog-ultimate.oss-cn-beijing.aliyuncs.com/cover/R.jpg
---

# 查看日志，版本号
**详细日志用`git log`命令查看：**
![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/Snipaste_2025-04-03_19-44-50.png)

**也可以用`git log --oneline`命令查看简洁的日志：**
![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/Snipaste_2025-04-03_19-20-42.png)


# 回退版本Reset
`reset`命令用于退回版本，可以退回到之前的某个提交的状态。

## soft回退
```bash
git reset --soft [要退回的版本id]
```
`soft`回退保留工作区和暂存区所有修改内容，**最常用**

## hard回退
`hard`回退丢弃工作区和暂存区中的所有修改内容，也就是说，你本地的所有修改都会丢失，**谨慎使用这个命令**
```bash
git reset --hard [要退回的版本id]
```

## 直接回退到上一个版本
如果直接想回到上一个版本，版本号我们可以使用`HEAD^`
```bash
git reset --soft HEAD^

git reset --hard HEAD^
```

# git rm删除文件
上次的团队项目开发过程中，我不小心把阿里云oss的配置文件推送到远程仓库中去了，应该怎么取消git对该配置文件的跟踪呢？

我们第一个想到的是`.gitignore`文件，但是注意，我这个配置文件已经被git跟踪，所以只是把这个文件添加到`.gitignore`不能实现取消跟踪。

解决办法：
```bash
# 1.从暂存区中删除该文件，保留工作区中的文件
git rm --cached [文件名]

# 2.然后把该文件添加到.gitignore文件中

# 3.把所有修改添加到暂存区
git add -A

# 4.重新进行commit
git commit -m '停止跟踪某个文件'
```
{% note warning no-icon %}
**注意**
如果使用`git rm [文件名]`命令，直接从暂存区和工作区中同时删除该文件，所以谨慎使用该命令。
{% endnote %}

# 远程仓库（remote）配置
## 关联远程仓库
这个操作我们应该很熟悉，因为这是我们每次在GitHub上创建完仓库以后第一个要做的事情。
**命令：**
```bash
git remote add [远程仓库名字] [远程仓库地址]
```
**远程仓库名字**可以根据实际情况命名
- 但平台常用`origin`。
- 多平台见名知意就好，比如我有两个平台，一个是GitHub，一个是Gitee：
```bash
git remote add github [GitHub仓库地址]

git remote add gitee [Gitee仓库地址]
```
**远程仓库地址支持两种协议：**
- SSH协议：`git@github.com/repo.git`，这个配置有点麻烦，对初学者不友好。
- HTTPS协议： `https://github.com/user/repo.git`，这个不需要配置，对初学者含友好。

## 查看已配置的远程仓库
**命令：**
```bash
git remote -v
```

## 修改远程仓库地址
我原来关联的远程仓库是https协议的，因为各种原因，我想修改成ssh协议的，应该怎么做呢？
**命令：**
```bash
# 修改远程仓库地址（HTTPS → SSH）
git remote set-url [远程仓库名字] [新的远程仓库地址]
```

## 删除远程仓库
**命令：**
```bash
git remote remove [远程仓库名字]
```