---
title: Java爬虫（一）简单抓取HTTPS页面内容
date: 2023-05-24 09:57
category: [Java爬虫]
tags: [java,net]
---

## Java爬虫之简单抓去网页内容
1. 定义URL。
```Java
//使用URL类实例化URL
String s = "https://www.google.com/";
URL u = new URL(s);
```
2. 流化URL。
```Java
/**
 * 方式一：
 * 使用URL类自带方法直接流化URL；
 */
InputStream uis = u.openStream();
```
之后使用字符流包装转化，见《[Java InputStream与InputStreamReader]》；
1. 读流。
2. 关流。

> 下面两种写法，第一种返回正常，第二种返回基本为null。
> ![](2023-05-24-10-04-27.png)
> ![](2023-05-24-10-04-15.png)
> 分析原因，判断条件和方法体lines非同一行，原理见《[Java ReadLine指针问题](https://www.google.com/)》。