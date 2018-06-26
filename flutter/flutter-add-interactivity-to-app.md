---
title: Flutter(五) 为App增加交互

tags:
  - Flutter
  - Dart

categories:
  - Flutter

author: 散人

---

> 这篇文章将会学习：
> - 如何响应点击
> - 如何创建自定义组件
> - 无状态与有状态组件的差异

怎样来为Flutter App添加交互行为呢？本篇文章将学习为仅包含一个非交互组件的App添加交互。特别是，我们将创建一个stateful组件，其中包含了两个stateless组件，来是的icon可点击。

> #### 内容
> - [stateful和stateless组件](#1)
> - [创建stateful组件](#2)
>   - [Step 1: 确定管理组件状态的对象](#3)
>   - [Step 2: 继承StatefulWidget](#4)
>   - [Step 3: 继承State](#5)  
>   - [Step 4: 将组件加入到组件树形结构中](#6)
>   - [问题？](#7)
> - [状态管理](#8)
>   - [组件管理自身状态](#9)
>   - [父组件管理当前组件状态](#10)
>   - [混搭方式管理状态](#11)
> - [其他交互组件](#12)
>   - [标准库组件](#13)
>   - [Material组件](#14)
> - [资源](#15)

### 准备工作
如果已经按[搭建布局](https://www.techlab.wang/2018/04/11/flutter/flutter-building-layouts/)一文构建过布局，那么可以跳过下面一步。

- 确认[Flutter环境](https://www.techlab.wang/2018/03/15/flutter/flutter-install/)已经搭建完成；
- [创建了Flutter App](https://www.techlab.wang/2018/03/29/flutter/flutter-create-your-first-app/)
- 可以从官方提供的Demo中去获取相关源文件，快速放入App工程中，也可以根据前面几篇文章，将源码复制出来，最好还是自己已经敲过的代码。[main.dart](https://raw.githubusercontent.com/flutter/website/master/_includes/code/layout/lakes/main.dart) [pubspec.yaml](https://raw.githubusercontent.com/flutter/website/master/_includes/code/layout/lakes/pubspec.yaml) [lake.jpg](https://github.com/flutter/website/blob/master/_includes/code/layout/lakes/images/lake.jpg)

以上资源拥有了，那么准备一台测试手机并且连接上它或者启动iOS模拟器，这样准备工作就完成了。

[搭建布局](https://www.techlab.wang/2018/04/11/flutter/flutter-building-layouts/)一文中教会我们如何构建布局，达到如下的效果。

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5NzY1NDg1NDEsLTIzODk1MDUxMywxNz
A1NDI0NDA5XX0=
-->