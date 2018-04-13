title: Kotlin基础
tags:
  - Kotlin
  - Android
categories:
  - Kotlin
author: 散人
date: 2018-04-13 09:44:32
---

Kotlin是一门静态类型语言且支持类型推导，允许维护正确性与性能的同时保持源码简洁。Kotlin支持面向对象和函数式两种编码风格，通过头等函数使更高级别的抽象成为可能，通过支持不可变值简化了测试和多线程开发。

<!-- more -->

Kotlin在服务器应用程序上也可以运行的很好，全面支持所有现存的Java框架。且Kotlin在Android上也可以工作，这得益于对Android API特殊的编译器支持以及丰富的库，为常见Android开发任务提供了Kotlin友好的函数。

它是免费和开源的，全面支持主流的IDE和构建系统。

<table><tr><td bgcolor=#A9A9A9>
本文内容：
<br/>- 声明函数、变量、类、枚举以及属性
<br/>- Kotlin中的控制结构
<br/>- 智能转换
<br/>- 抛出和异常处理
</td></tr></table>

### 函数和变量
#### 函数
首先看著名的hello world代码：
```kotlin
fun main(args: Array<String>) {
    println("Hello World!")
}
```

这里给出了最基本的函数声明
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMTUxMTkyMzYsODYwNDQ1MTQ2LDE4OD
QxNzA4NzBdfQ==
-->