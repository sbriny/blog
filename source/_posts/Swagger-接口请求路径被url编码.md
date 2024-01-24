---
title: 解决 Swagger UI 请求参数乱码问题
date: 2023-04-23 15:43
category: Swagger
tags: [swagger,openapi]
---

今天用Swagger-ui测试请求参数的时候，发现请求的路径被URL Encoding了，所以参数一直不正确，导致报错。
![](../2023-05-15-17-35-44.png)

<!--more-->

有效请求地址：`http://localhost:19052/publicity/article/queryall?pageIndex=1&pageSize=5`
无效请求地址：`http://localhost:19052/publicity/article/queryall?%E5%88%86%E9%A1%B5%E6%95%B0%E6%8D%AE%E9%87%8F=5&%E5%88%86%E9%A1%B5%E7%B4%A2%E5%BC%95=1`

原因是因为在接口文档中，为了显示对应参数的名称，使用Swagger注解@ApiParams中的name参数，参数值是中文，且在参数中无法传递中文而被编译。解决方式是使用value参数代替name参数。
```Java
//接口参数
@RequestParam(required = true)
@ApiParams(value = "分页索引", example = "1")
Integer pageIndex,
@RequestParam(required = true)
@ApiParams(value = "分页数据量", example = "5")
Integer pageSize
```

修改后请求生效。
![](2023-05-15-17-38-50.png)