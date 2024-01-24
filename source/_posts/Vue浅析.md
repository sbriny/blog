---
title: Vue 浅析
date: 2022-08-08 20:52:35
category: Vue
tags: [front,javascript,vue]
---


## Web开发架构


**Web应用程序的开发模型**
1. B/S（Browser-Server）模型：浏览器与服务器进行交互的网络应用程序。浏览器：应用程序的客户端。
2. C/S（Client-server）模型：客户端程序与服务器进行交互的网络应用程序。客户端程序：基于操作系统的自行开发的应用程序。
3. 前后端分离开发模式，在服务器端提供数据接口（WebApi）。目前来说，是一种适用客户端多平台客户端（iOS Android）需求的主流开发模式。其提供了前后端分离的开发模式的技术生态圈，主要生态圈分为：Vue、React以及其他。
<!--more-->
## Vue生态圈

### Vue框架
Vue是一种渐进式的JavaScript框架。
 Vue框架结构
   VueFramework （核心框架）（基于组件系统(Component)实现）
    Component（组件系统）（MVVM模式:混合的分层的开发模式）
   Router（路由）（网关过滤器）（基于Router实现单页面（模块化Modul）开发）
   VueX（状态管理）（数据的同步和异步的分离）（数据和状态的分离）
   Vue-Cli（脚手架）（项目构建）（数据管理）（初始化构建标准化的项目工程，并进行打包和压缩）
   Axios（通信交互组件）（高度封装的AJAX组件）（服务端渲染=交互）

### Vue-Framework
##### 实例化
1.**MVVM**
MVVM是一个操作DOM的模型结构，同时也是一个模板语法结构。  
Vue应用的模型虽然没有完全遵循MVVM模型，但是受其V(View)-M(Model)模式的影响，Vue的开发采用混合式开发，整个语言的设计与其关系密切。  
```
M:model（数据模型）：Vue（根）实例中的属性（数据）
V:view（视图层）：DOM
VM:view-model（视图模型）（使用element绑定视图模型层））：根实例
```

在MVVM中，数据的声明具有两种方式：JSON对象式和函数式。
模板语言分为视图模板和数据模板。
而在DOM中，我们不仅可以把数据绑定到 DOM 文本或 attribute，还可以绑定到 DOM 结构。

#### Vue-View（视图层）
Vue中的View代表了在HTML文档结构中所有元素、节点、节点内容和属性，指定了元素的特殊属性进行DOM和数据的交互。
这一个具有Vue属性的元素：
```
<input type="text" v-bind:value="brand" :disabled="disabled"/>
```
这些Vue定义的特殊属性有被称为的模板语法视图模板视图层指令等。
Vue-View模板语法两大类：
1.插值语法
写法为\{{\}}。
可以直接读取data中的属性，用于解析标签体的内容（文本）。
<!-- 插值语法指令 -->
2.指令语法（属性）
格式为v-xxx，例如v-text，v-html等。
解析标签的文本内容、标签属性和事件绑定，直接读取data中的属性。
数据解析对象：
v-text 指定数据填充到视图标签中，引入文本内容，不去解析内容中的html。
v-html 指定数据填充到视图标签中，引入文本内容，并解析内容中的html。
v-pre 显示原始信息，跳过解析过程，直接加快显示速度。
v-bind DOM节点对象的属性绑定。用于绑定任何节点对象的相关属性，并且可以直接读取data中的所有属性，进行数据绑定。
v-bind语法：
`v-bind:attribute=data-property`，元素通过`:attribute=data-property`进行属性值获取(v-bind能够省略)。

`v-bind:节点属性名(attribute)=值（数据模型中的属性值）`，简写为`:属性名=值`，如`v-bind:value="brand"`，绑定该元素的value属性，通过根实例的data属性，将brand的值替换，即vue实例中的数据从实例指向并替换了元素属性的值。该式简写为`:value=brand`.
Vue数据绑定方式：
单向绑定（数据从data（数据模型）指向view（视图））和双向绑定（动态绑定）。
**model视图层模板**
1. 数据模型的绑定
动态attribue（针对class属性和style属性）
`b-bind:[data-property]=data-property`，例如`<input type="checkbox" :[attribute_name]="attribute_value"/>`
class属性：绑定class属性值（强制绑定），`v-bind:class"data-property"`
style属性：绑定style属性值，`v-bind:class"data-property"`
2. 数据模型的写法
v-if="boolean 条件表达式"，通过条件控制视图层的显示（自动按照条件表达式判断条件，决定是否在页面中输入元素。）（指令的封装）。
v-show 表示元素是否显示。根据表达式判断条件决定，是单独的指令，不是指令结构（相当于diplay添加了一个判断）（display:block/none)（display封装）。
**v-for**
按照提供的数据，进行自动迭代，循环地输出到网页。
for(s of list){}转换为v-for="s of list"，自动会从stu对象提取各个属性，给到s对象。
（添加key提高循环效率）
v-for="(s,index) of list"，index是索引值。

单向绑定：v-bind
双向绑定：v-model

数据不仅能从data（实例）流向view（页面），也能从view流向data。会监听节点对象的数据绑定，一旦有变动，会自动更新data，视图层随之更新。
一般用在表单元素居，例如input、radio、select
v-model: value等同于v-model（默认绑定value值）

**事件**
在view中，.lazy:lazy，v-model修饰符对象，添加监听事件，例如`v-model.lazy:value="property"`。
**事件的基本使用**
根实例中添加methods对象属性来存放函数（用函数表示事件）。
v-on:event="function()"
event参数为click mouseover mouseout submit
**v-on简写为@**
>data属性中当然可以定义函数对象，但是大部分事件函数定义在method中。需要注意的是不可使用箭头函数：例如var x=(x,y) =>this.x+y，对象会冲突。加载数据时fetch多使用箭头函数。
**冒泡事件**
点击事件会有传递，从里面一层层往外执行，因此该情况下需要阻止事件的传递，组织冒泡需要使用.stop方法。
self 只对自身有效，点击当前元素才会触发事件，不受传递影响。用于跳过冒泡事件。
prevent 阻止当前路径
**methods**
**computed**
computed用于监测和控制data数据的变化。
对已知属性的计算（扩展）（功能的操作的限定），其实就是对data中的属性的处理（属性的扩展和变化）。  
data已经设置好了数据，将其保护起来、做隐藏、封装。而封装使用getter和setter，功能返回出来，所以需要调用方法。  
computed针对的是属性，必需带return，使用函数表示（函数封装了属性getXXX()）。
computed中的方法常作为插值。
> methods与computed的区别
> methods针对功能函数，用户行为（普通行为的调用），传参（或无参）方法，无缓存。
> computed针对属性（根实例成员属性的变化），属性变化，封装包装，无传参，使用返回值，有缓存。
> 虽然两者的定义不同，但是methods能够包含computed的闭包函数。
**watch**
针对数据模型中data属性，一旦指定后，值的改变会自动执行watch中的定义和方法。
特点：
1.以data属性名称作为函数名称。强制性地针对某属性进行监控。
2.绑定、监控、全程
3.具有强制性命令操作，监测重要数据时适合使用watch，同时消耗也比较大。
**components 定义**
组件可以扩展HTML页面，允许页面的一部分内，单独编写，这部分内容可以重复的使用，易于维护、修改和扩展。多用于页面内的宫格视图等。
组件分为全局组件和局部组件。
组件使用的三个步骤：1.定义（创建）组件；2.注册（全局组件默认注册，所以不需要注册在实例的components中。局部组件使用其名称在Vue实例的components对象中注册。）；3.使用组件（全局组件直接使用组件名标注到视图层中。局部组件使用component属性中引用的子组件名称标注到视图层中）；
组件对根实例和视图产生影响。
根实例是最大的父组件，（全局）组件是它的子组件。
组件名的视图层引用需要小写，组件名的定义不区分大小写。
组件元素名称不可被定义为HTML已存在的标签名。
实际开发中，可以将组件单独作为一个或多个JS文件引入。
**组件之间的数传递**
外部的父元素传递给内容组件，需要接收参数的组件，必需声明props成员。

### Vue3的使用
**组件（组件化）**
1.**Vue3实例需要写在组件之前，而Vue2组件需要写在实例之前进行加载。**
**模块化组件**
**slot标签**
> 用插槽来...，来代替视图的HTML标签。
slot多用于文本等内容的复用。
slot不是组件自定义元素，是已经Vue中已被定义了名称的特殊元素，能够在component的template中直接使用，从而替代视图层的组件内的元素内容。
**is绑定组件**
is是属性，用于指定组件的别名，对组件进行指定扩展。
component元素通常与其他标签混合，尤其是固定搭配例如列表元素，使用is属性动态绑定组件名称。
**:is动态绑定组件**
:is，动态绑定组件，根据Vue的属性挂载不同的组件，结合组件容器component使用。
动态绑定的属性值为字符串，例如`v-bind:is="'alert_success'"`。
is="组件名"直接指定组件别名。
:is=动态绑定组件名称，根据属性切换组件。
指定时需要加载字符串，例如comp为组件名，解析字符串组件：
```html
<component :is="'comp''></component>
```
**keep-laive标签**
使用标签<keep-alive>包裹组件元素，从而在切换页面或刷新时，在页面保留原来输入内容（状态持久化）。
切换页面或刷新页面时，通常页面某些缓存数据被重置，故为了保留这些数据，Vue使用keep-alive。
**transition动画标签**
Vue动画过渡效果
**动画wow.js和animate.css**
wow.js和animate.css是一种第三方插件。
wow.js是工具类，主要用于与视图层的的交互，而animate.css用于视图样式和布局。
apear 过渡效果设置
mode 过渡模式 `mode="out-in"`
enter-class 显示过程开始 
enter-to-class 显示过程结束
enter-active-class 显示的整个过程 `enter-active-class="animated bounceOutLeft"`
leave-class 消失过程
leave-to-class 显示过程结束
leave-active-class 消失的整个过程

## Vue-Cli
<!-- 
需要掌握：
Vue-cli工程的创建，项目的导入和运行。
Vue-cli项目的框架结构。
 -->
Vue-cli是Vue.js的脚手架。
Vue-cli用于Vue项目工程的自动构建或生成，以及打包。
**使用环境**
VUe-cli的使用需要借助Node JS，使用npm构建项目工程。
> Node JS 是一种基于Chrome V8内核的JavaScript运行环境。
> npm是Node JS的内置命令。
> node package manager包的管理的工具已经成为非官方的项目发布的Node模块（包）的标准。
> cnpm使npm的国内镜像
```
npm -v
cnpm -v
npm -g 全局的（安装到电脑系统上）
npm --save （安装到指定的独立的工程项目中）
npm install -g cnpm --registry=https://registry.npm.taobao.org
```
**Vue-cli的工程的创建**
1. 安装Vue-cli脚手架命令
`npm install -g @vue/cli --registry=https://registry.npm.taobao.org`
`cnpm install -g @vue/cli --registry=https://registry.npm.taobao.org`
查看vue-cli版本号（出现版本号则安装成功）
`vue -v`
2. 创建Vue-cli的工程
进入想要创建工程的路径，并创建工程项目（**工程项目名称禁止大写**）
`vue create vueclidemo`
出现并选择预设：
```
Vue CLI v5.0.8
? Please pick a preset: 
  Default ([Vue 3] babel, eslint) 
  Default ([Vue 2] babel, eslint) 
 Manually select features 

```
**选择工程中需要的技术组件：**
```
Vue CLI v5.0.8
? Please pick a preset: Manually select features
? Check the features needed for your project: (Press <space> to select, <a> to toggle all, <i> to 
invert selection, and <enter> to proceed)
 Babel （EMCS的向下兼容）
  TypeScript （JS语法糖，代表ES6语法）
  Progressive Web App (PWA) Support （WEB应用支持）
  Router （Vue路由）
  Vuex （Vue状态管理，代表数据的状态管理）
  CSS Pre-processors （CSS预处理器）
  Linter / Formatter （代码检测）
  Unit Testing （单元测试）
  E2E Testing （测试工具）
```
**出现并选择版本：**
```
Vue CLI v5.0.8
? Please pick a preset: Manually select features
? Check the features needed for your project: Babel, PWA(Progress Web App), Router, Vuex, Linter
? Choose a version of Vue.js that you want to start the project with (Use arrow keys)
 3.x 
  2.x 
```
**路由是否需要记录历史：**
```
Vue CLI v5.0.8
? Please pick a preset: Manually select features
? Check the features needed for your project: Babel, PWA, Router, Vuex, Linter
? Choose a version of Vue.js that you want to start the project with 3.x
? Use history mode for router? (Requires proper server setup for index fallback in production) (Y/n)
```
**代码错误检测方式：**
```
Vue CLI v5.0.8
? Please pick a preset: Manually select features
? Check the features needed for your project: Babel, PWA, Router, Vuex, Linter
? Choose a version of Vue.js that you want to start the project with 3.x
? Use history mode for router? (Requires proper server setup for index fallback in production) Yes
? Pick a linter / formatter config: （ESLint是代码的检测方式）
 ESLint with error prevention only
  ESLint + Airbnb config 
  ESLint + Standard config 
  ESLint + Prettier 
```
**代码（错误）检测时间：**
```
Vue CLI v5.0.8
? Please pick a preset: Manually select features
? Check the features needed for your project: Babel, PWA, Router, Vuex, Linter
? Choose a version of Vue.js that you want to start the project with 3.x
? Use history mode for router? (Requires proper server setup for index fallback in production) Yes
? Pick a linter / formatter config: Basic
? Pick additional lint features: (Press <space> to select, <a> to toggle all, <i> to invert 
selection, and <enter> to proceed)
 Lint on save （保存文件时进行一次检测）
  Lint and fix on commit
```
**文件配置方式**
```

Vue CLI v5.0.8
? Please pick a preset: Manually select features
? Check the features needed for your project: Babel, PWA, Router, Vuex, Linter
? Choose a version of Vue.js that you want to start the project with 3.x
? Use history mode for router? (Requires proper server setup for index fallback in production) Yes
? Pick a linter / formatter config: Basic
? Pick additional lint features: Lint on save
? Where do you prefer placing config for Babel, ESLint(代码检测方式), etc.? 
 In dedicated config files （每个组件的配置方式：每个文件自己有独立的配置文件）
  In package.json 
```
**保存预设配置(可供下次直接选择使用改配置)**
```
Vue CLI v5.0.8
? Please pick a preset: Manually select features
? Check the features needed for your project: Babel, PWA, Router, Vuex, Linter
? Choose a version of Vue.js that you want to start the project with 3.x
? Use history mode for router? (Requires proper server setup for index fallback in production) Yes
? Pick a linter / formatter config: Basic
? Pick additional lint features: Lint on save
? Where do you prefer placing config for Babel, ESLint, etc.? In dedicated config files
? Save this as a preset for future projects? (y/N) 
```
**预设配置保存的名称**
```
Vue CLI v5.0.8
? Please pick a preset: Manually select features
? Check the features needed for your project: Babel, PWA, Router, Vuex, Linter
? Choose a version of Vue.js that you want to start the project with 3.x
? Use history mode for router? (Requires proper server setup for index fallback in production) Yes
? Pick a linter / formatter config: Basic
? Pick additional lint features: Lint on save
? Where do you prefer placing config for Babel, ESLint, etc.? In dedicated config files
? Save this as a preset for future projects? Yes
? Save preset as: vue0720
```
**安装并成功**
```
Vue CLI v5.0.8
  Creating project in /Users/moony/class/Vue.js/vueclidemo25.
  Installing CLI plugins. This might take a while...

Debugger attached.

> yorkie@2.0.0 install /Users/moony/class/Vue.js/vueclidemo25/node_modules/yorkie
> node bin/install.js

Debugger attached.
setting up Git hooks
can't find .git directory, skipping Git hooks installation
Waiting for the debugger to disconnect...

> core-js@3.23.5 postinstall /Users/moony/class/Vue.js/vueclidemo25/node_modules/core-js
> node -e "try{require('./postinstall')}catch(e){}"

Debugger attached.
Waiting for the debugger to disconnect...
added 950 packages from 493 contributors in 57.056s

116 packages are looking for funding
  run `npm fund` for details



                 npm update check failed                  
           Try running with sudo or get access            
           to the local update config store via           
 sudo chown -R $USER:$(id -gn $USER) /Users/moony/.config 

Waiting for the debugger to disconnect...
  Invoking generators...
  Installing additional dependencies...

Debugger attached.
added 98 packages from 63 contributors in 13.977s

127 packages are looking for funding
  run `npm fund` for details



                 npm update check failed                  
           Try running with sudo or get access            
           to the local update config store via           
 sudo chown -R $USER:$(id -gn $USER) /Users/moony/.config 

Waiting for the debugger to disconnect...
  Running completion hooks...

  Generating README.md...

  Successfully created project vueclidemo25.
  Get started with the following commands:

 $ cd vueclidemo25
 $ npm run serve（告诉你如何启动该工程项目）

Waiting for the debugger to disconnect...
```
**（根据开发环境和软件不同）将项目包文件导入IDE，选择项目**
**运行Vue-cli项目：**
`cd`进入工程文件夹，并输入`npm run serve`。或者使用开发软件通过main.js选项（运行 -> npm run serve选项）直接启动服务。

> 因为项目中的node_modules模块（文件夹）体积过大，有时项目中并不存在。若无此模块文件包，则需要安装依赖模块即可。

**Vue-cli项目安装依赖模块**
1. `cd`进入当前项目路径
2. `npm install`或`cnpm install`安装node-modules依赖模块。

### Vue-cli的项目工程结构
```
.
 /node_modules（依赖模块，当前项目工程所依赖的组件包）
 /src（用于存放项目编译的资源文件，启动时编译运行。）
  /assets（受保护的文件夹，用于静态资源，可额外用于反爬虫。）
  /components（组件文件夹，公共级别的组件，例如footer.js页脚组件,coursel.js轮播组件,navbar.js导航栏组件,aside.js侧边栏组件，都可以放在此处。）
  /router 路由的文件夹，存放路由代码
  /store 存放VueX代码文件
  /views （组件文件夹，页面级别的组件）（单页面组件为"xxx.vue"后缀格式文件，文件名称必须大写开头，小写无法编译）
  App.vue（根组件，挂载到根页面index.html）（先渲染它，再渲染views组件，由vue-router控制。）
  main.js（启动项目时的入口文件，多用于设置拦截器。）
  registerServiceWorker.js（工程的提示文件）
 /public（存放公共的资源文件夹）
  index.html（当前项目的视图容器，main.js启动时会加载一次，并且只加载一次结束，是工程中唯一的一个HTML页面。）
 
.browserlistrc  （浏览器兼容性文件）
.eslintrc.js （语法规则的检测的配置文件）
 babel.config.js （JS配置文件）
 jsconfig.json （JS的标准的配置文件）
 package-lock.json （当前项目的锁定的依赖和插件的清单）
 package.json （当前项目的依赖和插件的清单）
 vue.config.js（当前项目跨域的文件的配置）
 .gitignore （git传输时需要忽略的文件）
 README.md
```

### 单页面组件开发
spa，single page application ，单页面应用组件，即xxx.vue文件。
注意：一般来说，对于空格和Tab缩进较为敏感。

### VueRouter
VueRouter是VUe官方提供的路由组件（器）。
路由的开发应用：
1. 组件管理：又叫路由表10个页面，通过vue渲染不同组件，如需呈现其中某个页面，就需要路由控制例如导航。每个导航选项对应着真实资源（url地址与真实资源的对应关系）。每个导航栏可以做不同的组件，之后通过router控制（url地址对应页面）
2. 渲染管理：先针对大的访问量的需求，先渲染对应的页面，之后的点击直接点击，而不是发送服务器的请求再响应。

路由创建 导出路由 配置路由表 渲染视图 
路由链接
<router-link to="/">首页<router-link>
路由视图
<router-view></router-view>

**子路由（二级路由）**
子路由的定义：在路由列表中，在对应路径JSON中创建children对象。
子路由的path路径中无需添加"/"。

#### 路由守卫
路由守卫主要是指router路由对象的beforeEach功能。
路由守卫在路由跳转的时候做一些判断或其他操作。
**前置守卫**：于页面跳转之前所定义的功能（路由跳转前触发），一般用于页面的预加载，例如先进行相关的判断验证。
**后置守卫**：于页面跳转之后所定义的功能（路由跳转后触发）。
**"\$router"与"\$route"**
$router，所操作的路由对象，针对路由页面。主要操作：push(), go()
Vue中，$router被定义为全局对象。使用`$`动态地引用router对象。
{{$route}} 路由信息对象，针对路由的基本信息。基本信息有：name, path, params, meta

### WEB应用概念

超文本传输网络应用层协议，简称HTTP，通过URL（资源定位符）向服务器发送Request（请求），从而与服务器建立连接。
HTTP具有报文格式（请求头和响应头）、具有响应状态（200或404等）、具有固定的URL格式(http://[host]:[port]/[path]?[searchpart])。
>计算机**网络七层模型**：应用层、表示层、会话层、传输层、网络层、数据链路层、物理层。
**应用层**：为应用程序提供交互服务。在互联网中的应用层协议很多，如域名系统DNS、HTTP协议、SMTP协议等。
表示层：负责数据格式的转换，如加密解密、压缩解压缩等。
会话层：负责在网络中的两节点之间建立、维持和终止通信，如服务器验证用户登录便是由会话层完成的。
**传输层**：负责向两台主机进程之间的通信提供数据传输服务。传输层的协议主要有传输控制协议TCP和用户数据协议UDP。
网络层：选择合适的路由和交换结点，确保数据及时传送。主要包括IP协议。
数据链路层：将网络层传下来的IP数据包组装成帧，并再相邻节点的链路上传送帧。
物理层：实现相邻节点间比特流的透明传输，尽可能屏蔽传输介质和通信手段的差异。

域名系统，简称DNS，域名映射，互联网服务，能够使人更方便地访问。

#### RestFul
Rest: 表像性的状态改变，使用JSON、HTML、XML等语言标准的轻量级跨语言架构设计。
是Web架构的一种风格（访问资源的架构的设计）。
并非标准，而是风格，目的是为了优化访问，更为快速和简单。
get请求查询商品，post添加商品，put和patch修改商品，delete删除商品。
传统访问：相应的请求加地址的格式
(get)     http://127.0.0.1:8001/brand?cate_id=1916
(post)    http://127.0.0.1:8001/add?xxx
(update)  http://127.0.0.1:8001/update?xxx
(delete)  http://127.0.0.1:8001/delete?xxx
RestFul访问: 统一路径加请求
(get)     http://127.0.0.1:8001/brand/id/1916
(post)    http://127.0.0.1:8001/brand/id/1916
(update)  http://127.0.0.1:8001/brand/id/1916
(delete)  http://127.0.0.1:8001/brand/id/1916

**API**
访问服务器地址（接口路径）的程序的方法。使用URL对应关系。

#### 端口域 
端口，应用程序的标识。
1. **origin网络域**
origin网络域：ip端口号
前端应用程序所在的域：127.0.0.1:8080
后端应用程序所在的域：127.0.0.1:8001
2. **CORS跨域**
当前端应用程序访问后端应用程序时（8080 -> 8001）会出现跨域问题。
**配置反向代理**
后端应用程序的反向代理：127.0.0.1:8080/api
反向代理减轻服务器压力，有利于负载均衡。
Vue中，在cli-router项目vue.config.js文件中配置：
```JavaScript
module.exports = defineConfig({
    transpileDependencies: true
    //开发环境：服务器端配置
    derServer:{
        //反向代理配置
        proxy:{
        //代理路径 http://127.0.01:8080/api
        '/api':{
            //后端路径
            target:'http://127.0.0.1:8001',
            //允许跨域
            changeOrigin:true,
            //重写路径
            pathRewrite:{
                '^/api':''
            }
        }
    }
  }
})
```

### Axios
交互对象：Ajax promise fetch
**概述**
Axios是Vue全家桶的一个特殊对象。
Axios是第三方插件、通讯交互组件。
Axios能够满足RestFul风格。
Axios的底层是Ajax的封装（不会看到Ajax的原始写法）。
Axios支持promise的使用(then)。
Axios自动转换JSON数据。
**引入Axios**
`import axios from 'axios'`
**Axios发送请求**
axios.get(String url,Object args)
axios.post(String url,Object args)
axios.put(String url,Object args)
axios.delete(String url,Object args)
String URL : 请求访问路径，
Object Args：
method [请求类型(get,put,post,delete)]
params  请求参数cate_id=1916
data  post请求参数（body参数）
timeout 请求超时毫秒数
transformRequest  Post请求前对data数据的转换(JSON)
ValidateStatus    验证响应的状态（默认200-300）
**Axios GET Send**
用户数据查询
``` JavaScript
export default{
    mounted(){//Axios的直接使用
        //发送GET请求（查询资源）
        axios.get("/api/brand",{params:{cate_id:1916}}.then(response=>{console.log("Axios~!");console.log(response)})),
        ()=>{console.log("Unsuccessed!")}
    }
}
```
请求路径：`http://localhost:8080/api/brand?cate_id=1916`
**Axios Post Send**
用户注册

用户登录
```JavaScript
//POST请求 添加收货信息
axios.create()({
    url:"/api/customer/useraddress",
    method:"POST",
    headers:{
        Authorizaiton:localStorage.getItem("token")
    },
    data:qs.stringify({
        uaddr_name:"jack",
        uaddr_phone:"13900000123",
        uaddr_province:"shanghai",
        uaddr_city:"shanghai",
        uaddr_district:"huangpu",
        uaddr_address:"peoplesquler No1",
        uaddr_isdefault:0
    })
}).then(response=>{
    console.log("Axios~!")
})
```
用户修改
```JavaScript
aixos.create()({
				url: "/api/customer/useraddress",
				method : "POST",
				headers :{
					Authorization :localStorage.getItem("token")
				},
				data:qs.stringify({
					uaddr_name : "mary",
					uaddr_phone : "13900000123",
					uaddr_province : "beijing",
					uaddr_city : "beijing",
					uaddr_district : "chaoyang" ,
					uaddr_address : "pepolesquler No1",
					uaddr_isdefault : 0 
				})
			})
			.then(response => {
				console.log("请求成功")
				console.log(response)
			},()=>{
				console.log("请求失败")
			})
```
用户删除
```JavaScript
//发送DELETE请求（删除收货信息）
			axios.create()({
				url:"customer/useraddress/16",
				method:DELETE,
				headers:{
					Authorization:localStorage.getItem("token")
				},

			}).then(response => {
				console.log("请求成功")
				console.log(response)
			},()=>{
				console.log("请求失败")
			})
```

Axios的封装使用
**封装**
创建类似工具类实现各种请求方式
封装表现方式，例如：
```
URL地址(http://localhost)
后端的网络域：http://localhost:8001 -> http://localhost:8080/api
资源路径：customer/useraddress/
资源id:28 (用户id、主键)
```
2.请求的方式
get\post\put\delete 中的data参数放入qs.stringify(data)中。
3.headers
每次请求从localStorage中获取并添加Authorization。
1. 请求错误时，根据业务状态号2统一处理。
直接使用：Vue
封装使用：建立封装各种请求方法的工具（axios的创建、 66截器等）
request.js -> Axios获取后端数据的工具类，用于各个业务模块中。
**封装业务模块**
request.js : 获取当前业务需要执行的操作的数据，同时也是一个api目录，体现了各个模块的业务访问方法。
封装的业务模块 ： api目录
后端数据：App.vue
页面级数据：
后端 -> axios（交互获取） -> VueX（仓管） ->页面级组件(product.vue,order.vue)

### Vuex
**概述**
对应用组件的（数据）进行集中性管理。
针对Axios不同的业务模块（例如api中的order.js）获取的数据进行集中性管理。
> 分库（使用state、mutations、actions、modules较多）
```JavaScript
import { createStore } from 'vuex'
import custom from '../store/mudules/customer.js'

export default createStore({ //状态仓库、index总仓库
  state: {//状态数据 (setter)
    name:"Jack",
    nameList:[]
  },
  getters: {
  },
  mutations: {//同步方法仓库
    getName(){
      this.name=""
    }
  },
  actions: {
    commit("getname",{"name":"Jack"})//调用同步方法
    getAge(){}//异步方法
    dispatch("getAge")//调用本仓库的异步方法
  },
  modules: {//总仓库对子仓库的管理
    customer
  }
})
```

#### Vuex的状态管理
1.State状态数据
用于存放Vuex需要统一管理的数据。State等同于vue实例中的data成员。
2.Mutation同步方法
用于存放针对state数据统一管理的方法（针对state属性的操作）。
（同步方法请求的是内存中的数据。）
3.Action异步方法（多为交互方法）
针对mutations方法的方法，穿插在程序当中，提高了效率（耗费一定资源）。
通过commit方法触发mutations中定义的方法，通过dispatch方法触发actions中定义的方法。
（异步方法请求的是服务端的数据。）
4.Module模块化
modules是对分仓库的整合和拼装，根据业务模块分仓的统一管理和注册。

**Store分仓库**
```JavaScript
//针对customer业务封装模块的store仓库
export default{
    state:{},
    mutations:{},
    actions:{}
    //使用独立的命名
    namespaced:true
}
```
