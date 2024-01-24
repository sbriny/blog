---
title: hexo publish 报错 'no such file or directory'
date: 2022-04-28 11:40:56
tags: front
---
如果你第一次直接使用hexo publish命令，将会出现_drafts文件夹不存在的报错，原因是你没有使用hexo new 建立新的草稿，则草稿文件夹不会存在。  
所以首先使用`$ hexo new draft "your_draft_name"`建立新的草稿文件，将会自动在文档分区主目录下建立./source/_drafts草稿文件夹，之后将不会再报此类错误。  
