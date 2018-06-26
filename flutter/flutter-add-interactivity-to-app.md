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
>   - [话]
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI1NTcxODAyLC0yMzg5NTA1MTMsMTcwNT
QyNDQwOV19
-->