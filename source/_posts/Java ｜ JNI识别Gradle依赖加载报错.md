---
title: Could not resolve all dependencies for configuration ':compileClasspath'.
date: 2023-05-18 09:08
category: Java
tags: [maven,gradle,java]
---

Could not resolve all dependencies for configuration ':compileClasspath'.
![](../images/20230518/2023-05-18-09-09-37.png)

`$ gradle --warning-mode all` build succeed.
![](../images/20230518/2023-05-18-09-31-49.png)

**resolve：**
Add the insecure protocol param in init.gradle or build.gradle file.
``` gradle
repositories{
    ...
    maven{
        allowInsecureProtocol = true
        ...
    }
}
```
![](../images/20230518/2023-05-18-09-38-36.png)