title: Kotlin伴生对象与属性委托
tags:
  - Kotlin

categories:
  - Kotlin
author: 散人
---

在我的前一篇文章[设计模式之单例模式]()中Kotlin实现中，有涉及到Kotlin中的伴生对象和属性委托的概念，这篇文章就来谈谈这两个概念。

#### 伴生对象

在正式谈伴生对象之前，要先提及Kotlin中的一个关键字“object”。这个关键字与Java中的Object类不同，Kotlin中object关键字用以修饰类，在声明类的同时创建一个实例（即该类的一个对象）。可以理解成Java中的静态单例。

object关键字使用的几种不同的场景：
- 用以声明一个单例类;
- 伴生对象（可以持有工厂方法和其他与这个类相关，但在调用时不依赖于容器类的方法。他们的成员可以通过容器类的类名来访问即相当与Java中的静态成员形式）;
- 对象表达式（Java的匿名内部类）;

##### 单例类
先来看object关键字修饰下的类的形式。
```Kotlin
object Factory
```
这是最简单的单例声明方法。为了更方便的了解这是但里
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ1NzY0MzUyMywxMjYzMzE0OTU1LDE3ND
g4OTczMDksLTU5NzYwNjA4Ml19
-->