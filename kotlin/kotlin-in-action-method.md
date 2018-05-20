
title: Kotlin基础——函数定义及调用
tags:
  - Kotlin

categories:
  - Kotlin
author: 散人
---

#### 前言
函数是一门语言中最基本也是最重要的环节之一。这里就来说说Kotlin的函数部分的一些内容。

#### 顶层函数
我们知道的是Java中的方法定义离不开类，即所定义的方法必须在某个类中，即使一个类中只有一个单一的方法。

有时会遇到这样的情况，针对两个不同对象的处理方式相差无几，这样的方法定义不想依赖于具体的示例对象，这个时候一般的做法是将对应的方法定义到一个Util方法中。

Kotlin针对这种情况，则提供了提成函数的定义，即无需将函数定义到某一个类中，直接定义在代码文件的顶层。

如下的示例代码：
```Kotlin
package kt  
  
fun sayHelloWorld() {  
    println("hello world!")  
}
```
这就是一个最基本的顶层函数的定义。相应的，它被编译成Java就编程了
```Java
package kt;  

public final class TopMethodKt {  
   public static final void sayHelloWorld() {  
      String var0 = "hello world!";  
      System.out.println(var0);  
  }  
}
```
可以到，Kotlin文件TopMethod被编译成了TopMethodKt类，相应的顶层函数sayHelloWorld方法编程了静态方法。

Kotlin中顶层函数调用非常简单，
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNDAwNjk5ODYsLTI3OTAyMDg0OSwxMj
gxMjg0MzAzLDE2NTMzMDQwODAsLTE2MDU3NTA1MDUsLTc1NjQz
MDg4Ml19
-->