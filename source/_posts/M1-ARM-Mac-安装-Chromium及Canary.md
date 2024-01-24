---
title: M1 ARM Mac 安装所有Google Chrome系列
date: 2024-01-23 13:33
category: MOS
---

### Google Chromium 
Chromium是Google为发展浏览器Google Chrome而发布的自由开源软件，以BSD许可协议等数种许可发行。  Chromium与Google Chrome共享大部分代码和功能，但功能和商标之间有一些细微差别。 Google基于Chromium开发Chrome浏览器，后者具有更多功能。

[Chromium Doc](https://www.chromium.org/getting-involved/download-chromium/)
[Chromium Download](https://chromium.woolyss.com/download/#mac-arm)

### Google Chrome Canary
金丝雀（Canary）版Chrome是Google推出的一个特别版Chrome。

[Chrome Canary](https://www.google.com/chrome/canary/)
[什么是Chrome金丝雀版？有什么优势？](https://www.chrome64.com/course/jsqb/505.html)

### Google Chrome for Testing
[Try new features with Chrome Beta](https://www.google.com/intl/en_us/chrome/beta/)

### Google Chrome Dev
[Google Chrome for developers](https://www.google.com/intl/en_us/chrome/dev/)

### 解决安装出现Chromexxx已损坏
`sudo xattr -r -d com.apple.quarantine /Users/u/Downloads/chrome-mac/Chromium.app`