title: Kotlin伴生对象与属性委托
tags:
  - Kotlin

categories:
  - Kotlin
author: 散人
---

在我的前一篇文章[设计模式之单例模式]()中Kotlin实现中，有涉及到Kotlin中的伴生对象和属性委托的概念，这篇文章就来谈谈这两个概念。

#### 伴生对象

在正式谈伴生对象之前，要先提及Kotlin中的一个关键字“object”。这个关键字与Java中的Object类不同，Kotlin中object关键字用以修饰类，在声明类的同时创建一个实例（即该类的一个对象）。可以理解成Java中的静态
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDY2MTk4OTk0LDE3NDg4OTczMDksLTU5Nz
YwNjA4Ml19
-->