---
title: Hexo Next 隐藏发布文章
date: 2023-05-15 13:40
category: Hexo
tag: hexo
---

两种方式隐藏 Hexo Next Blog，一是通过自定义front-matter的参数并修改主题的index.swig，二是通过安装插件hexo-hide-posts；
> front-matter：每次`hexo new`的文章属性，显示在source/_posts中的markdown文章中。

### 安装hexo-hide-posts
`$ npm install hexo-hide-posts --save` 
配置Hexo根目录`_config.yml`（注意yaml格式）；
```
# hexo-hide-posts
hide_posts:
    # 过滤front-matter中为hidden的值
    filter: hidden
    # 指定传递隐藏文章位置，留空默认全部隐藏，常见的位置：index, tag, category, archive, sitemap, feed, etc.
    public_generators: []
    # 添加noindex meta标签，阻止搜索引擎收录
    noindex: true
```
使用：
```
title: Hidden Post
date: date
hidden: true
```
`$ hexo hidden:list`命令显示当前所有已隐藏文章列表
### 