---
title: 解决 GitPage Actions Deplod 图片无法显示
date: 2024-01-23 22:41
tag: Blog
---

修改配置文件
`post_asset_folder: false`，值改为true。
此时创建新文章需要使用`hexo new "title"`，创建后在`source/_posts`中会创建同名文件夹，用于存储asset image。

`post_asset_folder`模式下引用图片两种写法：
1. 不安装图片插件，仅开启post_asset_folder配置
{% asset_img label 2023-05-15-17-38-50.png %}
1. 安装hexo-image-link插件
`npm install hexo-image-link --save`
![label](Swagger-接口请求路径被url编码/2023-05-15-17-38-50.png)