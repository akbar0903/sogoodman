---
title: 把Element Plus的文档克隆到本地
date: 2025-12-23 18:46:35
tags: ['Element Plus']
categories: Element Plus
cover: https://www.bing.com/th?id=OHR.WintersolsticeY25_ZH-CN6462419684_1920x1080.jpg&rf=LaDigue_1920x1080.jpg&pid=hp
---

# 为什么把Element Plus的文档克隆到本地

有时候因为网络原因，查找Element Plus的在线文档非常慢，所以我想了一个办法，把Element Plus的文档克隆到本地，这样就可以快速访问了。

# 具体方法

## 先在Github上找到Element Plus的文档仓库

打开element-plus的官网，然后点击右上角的GitHub图标，进入Element Plus的GitHub主页。

然后找到element-plus的文档仓库分支，叫`gh-pages`：

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251223185240225.png)

## 克隆`gh-pages`分支到本地

复制`gh-pages`分支的克隆地址，其实赋值的是整个Element Plus仓库的地址：`https://github.com/element-plus/element-plus.git`。

我们只需要克隆`gh-pages`分支，所以在克隆的时候需要加上`-b gh-pages`参数。
```bash
git clone --branch gh-pages --depth 1 --single-branch https://github.com/element-plus/element-plus.git
```
解释一下参数的含义：
- `--branch gh-pages`：指定要克隆的分支是`gh-pages`
- `--depth 1`：表示只克隆最新的提交记录，减少下载的数据量
- `--single-branch`：只克隆指定的分支，而不是所有分支

{% note info flat %}
一定要只克隆`gh-pages`分支，否则会下载整个Element Plus仓库，文件会非常大。
{% endnote %}

## 访问本地的Element Plus文档

用vs-code打开这个项目，比如我的克隆下来叫`element-plus-docs`，然后在vs-code中安装一个叫`Live Server`的插件（如果没有）。然后直接点击vscode右下角的`Go Live`按钮，就可以在浏览器中访问本地的Element Plus文档了。

## 保持文档更新

如果Element Plus的文档有更新，可以进入克隆下来的`element-plus-docs`目录，然后执行下面的命令拉取最新的文档内容：
```bash
git pull origin gh-pages
```
![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251223190250261.png)