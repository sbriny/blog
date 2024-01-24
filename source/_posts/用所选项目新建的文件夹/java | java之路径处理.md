---
title: Java不同环境下的协议头处理
date: 2023-07-26 10:44
tag: java
---
``` java
String dirURLString=URLDecoder.decode(String.valueOf(iTextAdapter.class.getResource("/")),"UTF-8");
String schema;
URI dirURI=new URL(dirURLString).toURI();
schema=dirURI.getScheme();
System.out.println(dirURI);
```
`jar:file:/Users/spring/自助机/iTextDemo/target/iTextDemo-1.0-SNAPSHOT.jar!/BOOT-INF/classes!/`
`file:/Users/spring/自助机/iTextDemo/target/classes/`