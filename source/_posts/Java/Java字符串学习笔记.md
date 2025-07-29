---
title: Java字符串学习笔记
date: 2025-06-22 19:27:56
tags: ['Java', '字符串', 'String']
categories: 'Java'
cover: https://www4.bing.com//th?id=OHR.SerengetiGiraffe_ZH-CN2613013393_1920x1080.jpg&rf=LaDigue_1920x1080.jpg&pid=hp
---

# 定义字符串

一般情况下有两种情况可以定义字符串:

*   通过直接复制定义（推荐）：

```java
String name = "zhangsan";
```

> 直接赋值出来的字符串存储在串池里面，如果定义同样内容的字符串，直接复制可以节省内存。
>
> ```java
> String name = "zhangsan";
> String nm = "zhangsan";
> ```

*   通过new出来定义（不常用，而且不节省内存）：

```java
String name = new String("zhangsan");
```

# 字符串比较

> 一般情况下不能直接使用`==`来比较字符串，因为如果这两个字符串是直接赋值定义的，`==`可以正确比较。如果是用new关键字定义的，`==`不能正确比较。<br/>
> 所以注意：<mark>不建议使用`==`比较字符串。</mark>

比如：

```java
String name = new String("zhangsan");
String nm = new String("zhangsan");

System.out.println(name==nm);
```

最终输出的结果是`false`。

## 字符串比较工具方法

Java给我们提供了两个比较字符串的方法：

| boolean equals(要比较的字符串)           | 完全一样结果才true，否则为false。 |
| --------------------------------- | --------------------- |
| boolean equalsIgnoreCase(要比较的字符串) | 忽略大小写比较。              |

```java
String name = new String("zhangsan");
String nm = new String("ZHANGSAN");

System.out.println(name.equals(nm));
```

输出`false`。

```java
String name = new String("zhangsan");
String nm = new String("ZHANGSAN");

System.out.println(name.equalsIgnoreCase(nm));
```

输出`true`。

# 遍历字符串

遍历字符串我们用到一下方法

| public char charAt(int index) | 根据索引返回字符                  |
| ----------------------------- | ------------------------- |
| public int length()           | 返回字符串的长度(注意是length()，有括号) |

比如：

```java
public class Demo01 {
    public static void main(String[] args) {
        String name = new String("zhangsan");

       for (int i = 0; i< name.length(); i++) {
           System.out.println(name.charAt(i));
       }
    }
}
```

# StringBuilder

`StringBuilder`可以看作是一个容器，创建之后里面的内容是可变的。因为我们都知道，一个普通字符串的内容是不可变的，有些操作比较麻烦。

作用：提高字符串的操作效率。

## 创建StringBuilder

```java
StringBuilder sb = new StringBuilder("zhangsan");
```

## StringBuilder成员方法

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20250622194411930.webp)

# 常用的字符串方法

## ①英文大写转换

```java
String name = "zhangsan";

String resultString = name.toUpperCase();
System.out.println(resultString);
```

输出：ZHANGSAN

## ②英文小写转换

```java
String name = "ZHANGSAN";

String resultString = name.toLowerCase();
System.out.println(resultString);
```

输出：zhangsan

## ③字符串截取substring

*   `substring(beginIndex)`：从指定的`beginIndex`开始，到字符串的末尾，返回一个新的字符串（包含beginIndex）

```java
String s = "hello world";

String sub = s.substring(6);
System.out.println(sub);
```

输出：world

*   `substring(beginIndex,endIndex)`：从`beginIndex`开始（包括`beginIndex`处的字符），到`endIndex`结束（不包括`endIndex`处的字符），返回一个新的字符串。

```java
String s = "hello world";

String sub = s.substring(6,11);
System.out.println(sub);
```

输出：world

## ④lastIndexOf查找字符最后出现的位置

```java
String s = "hello world";

int index = s.lastIndexOf("o");
System.out.println(index);
```

输出：7

## ⑤split字符串分割

`split()` 方法用于根据指定的分隔符将字符串分割成一个有序的子串列表，并将其放入一个数组中，然后返回这个数组1。

比如：

```java
String s = "hello world";

    String[] chars = s.split("o");
    for (String c: chars) {
        System.out.println(c);
    }
}
```

输出：

```text
hell
 w
rld
```

比如下面这是`阿里云oss`上传文件以后返回文件地址：

```text
ENDPOINT = https://oss-cn-beijing.aliyuncs.com
BUCKET_NAME = blog-ultimate
```

要求返回这样的地址：

```text
https://blog-ultimate.oss-cn-beijing.aliyuncs.com/88224a5c-7a11-4457-b6e7-65b40091b1a5.png
```

我们可以这样写：

```java
String url = ENDPOINT.split("//")[0] + "//" + BUCKET_NAME + "." + ENDPOINT.split("//")[1] + "/" + fileName;
```

## ⑥isEmpty判断字符串是否为空

`String` 类的 `isEmpty()` 方法是一个原生方法，用来判断一个字符串是否为空。具体来说，它会检查字符串是否为 `null` 或者其长度是否为 0。

```java
String str1 = "";
String str2 = " ";
String str3 = "Hello";
String str4 = null;

System.out.println(str1.isEmpty());  // true，空字符串
System.out.println(str2.isEmpty());  // false，非空字符串
System.out.println(str3.isEmpty());  // false，非空字符串
System.out.println(str4.isEmpty());  // 会抛出 NullPointerException
```

# spring框架提供的字符串操作方法

> spring boot写项目的过程中，我们老师会用一些spring框架给我们提供的String操作方法。

## ①hasLength()

检查字符串是否非 null 且长度大于 0。

```java
StringUtils.hasLength(str);
```
