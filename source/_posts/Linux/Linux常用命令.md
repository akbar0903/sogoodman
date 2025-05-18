---
title: Linux 常用命令
date: 2025-05-18 15:16:50
tags: [Linux]
categories: Linux
cover: https: https://www4.bing.com//th?id=OHR.LeopardMother_ZH-CN6134353524_UHD.jpg
---



**命令格式：命令 [-选项] [参数]**

## `ls`显示目录文件

英文名称：list
	功能：显示目录文件
	语法：ls [-ald] [文件或目录]
	`-a`：显示所有文件（all）
	`-l`：详细信息显示（long）
	`-ld`：查看目录属性（一般用）
	`-lh`：人性化显示（用单位显示文件大小）
	`-i`：查询文件唯一标识

查看`temp`目录下的`C`目录下的所有文件：
`ls temp/C`

## 文件类型

`-`：表示文件
	`dr`：目录
	`l`：然链接

## `mkdir`创建目录

英文意思：make directories
	语法：`mkdir -p [目录名]`
	`p`：递归创建的意思
	示例：`mkdir temp`

## `cd`切换目录

英文意思：change directory
	比如，切换到temp目录：`cd temp`

回到上一级目录：`cd ..`

## `pwd`显示当前目录

在命令行敲一下`pwd`就可以查看当前目录

## `rmdir`删除空目录

英文意思：remove directory
	语法：`rmdir [目录名]`

## `cp`复制

英文意思：copy
	把`hellofunc.c`复制到`temp`目录下`cp hellofunc.c temp`

## `mv`剪切和更名

英文意思：move
	比如把`hellofunc.c`剪切到`C`目录下：`mv hellofunc.c C`

更名：`mv hellofunc.c hello.c`

## `clear`清屏

## `rm`删除

英文意思：remove
	功能：删除文件，删除目录
	删除文件：`rm hello.c`
	删除目录：`rm -r C`

## `touch`创建文件

创建Main.c文件：`touch Main.c`

## `cat`浏览文件

浏览文件`hellofunc.c`：`cat hellofunc.c`
	显示行号，方便阅读：`cat -n hellofunc.c`

## `more`浏览长文件

`more hellofunc.c`

## `less`全文检索

## 文件解压缩

zip 格式的文件Linux和Windows都可以加压缩



不保留源文件，只能压缩文件，不能压缩目录
	用gzip格式压缩：`gzip Main.c`
	用gunzip解压：`gunzip Main.c.gz`

打包的同时压缩：`tar -zcf temp.tar.gz temp`
	解包的同时解压：`tar -zxf temp.tar.gz`

## 编译运行C语言程序

`gcc Main.c -o Main`

`./Main`



