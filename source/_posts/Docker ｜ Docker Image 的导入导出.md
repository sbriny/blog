---
title: Docker Image 的导入和导出
date: 2023-05-15 11:19
category: Docker
tags: [docker,m1]
---

内容：镜像文件的导入和导出使用
![](../images/2023-05-15-13-19-13.png)

<!-- more -->

> 镜像和容器两种操作方式不可混用
> 使用import导入save的镜像文件，虽不提示错误，但是启动容器时会失败，会提示类似"docker: Error response from daemon: Container command not found or dose not exist"错误。

### 镜像 save保存/load加载

* 原始镜像文件  
//导出原始镜像文件（无压缩、体积较大、原始）  
`$ docker save -o [FILE_PATH] [IMAGE_NAME]`  
`$ docker save -o ocr_image docker-image-ocr `  
//导入原始镜像文件  
`$ docker load -i [FILE_PATH]`  
`$ docker load -i ocr_image`  

* 压缩镜像文件  
//根据镜像ID压缩镜像文件  
`$ docker save -o [IMAGE_ID] [FILE_PATH]`  
`$ docker save -o 2f5c0fd16c33 > ocr_image.tar`  
//导入根据压缩镜像文件  
`$ docker load < [FILE_PATH]`  
`$ docker load < ocr_image.tar`  

### 容器 export导出/import导入  
* 压缩镜像文件  
//根据容器ID导出压缩镜像  
`$ docker export [CONTARINER_ID] > [FILE_PATH]`  
`$ docker export 84960d31ded5 > ocr_container.tar`  
//根据压缩镜像文件导入  
`$ docker import - [IMAGE_NAME] < [FILE_PATH]`  
`$ docker import - ocr_image < ocr_container.tar`  

### 应用场景

**export / import**  
主要用于制作基础镜像，比如从ubuntu镜像启动一个容器，进行一些软件的安装和设置后，使用docker export保存该镜像作为一个基础镜像，之后，再将这个镜像进行分发，可作为开发环境等。  
**save / load**  
如果应用程序需要使用docker-compose.yml编排多个镜像并进行组合，且客户服务器只有内网环境等情况下，可以使用`docker save`将镜像打包并拷贝至客服服务器并使用docker load载入。

### 区别

##### 文件体积

`docker export` < `docker save`  

##### 是否可对导入镜像进行重命名
|      method    |   rename   |
|----------------|------------|
|`docker import` | 导入重命名 ✓ |
|`docker load`   | 载入重命名 ✕ |


##### 是否包含镜像历史
**export / import**
根据container容器导出时，再导入时会丢失镜像的历史记录和元数据信息（即保存容器当时的快照状态），故无法进行回滚操作。
**save / load**
根据save load的镜像，没有丢失镜像的历史，可以回溯到之前的层（layer）。

##### 是否同时打包多个镜像打包到一个文件中
|      method    | package all|
|----------------|------------|
|`docker save`   |  保存打包 ✓ |
|`docker export` |  导出打包 ✕ |
