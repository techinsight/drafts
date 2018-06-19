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

##### 单例
先来看object关键字修饰下的类的形式。
```Kotlin
object Factory
```
这是最简单的单例声明方法。为了更方便的了解这是单例，完整的demo代码来看下。
```Kotlin
object Factory {
    val name: String = "object single"
}

fun main(args: Array<String>) {
    val factorySingle : Factory = Factory
    println(factorySingle.name)
}
```
在object类中定义一个name成员，然后在执行入口函数main()中引用这个单例，并且打印其成员name，实际的执行结果就是在控制台打印“object single”.
```
...
object single

Process finished with exit code 0
```
在函数main()中可以看到，引用创建时，等号右则直接是类名。Kotlin中使用object关键字修饰的类将一个类声明及该类的唯一实例创建结合在一起，这个功能也叫对象声明。

##### 伴生对象
再来说本篇文章的重点，即伴生对象。伴生对象从功能上的另外一个描述：<font color='red'><b>它是工厂方法和静态成员的地盘</b></font>。

与Java做一个比较，Kotlin本身是不支持static关键字的，即static关键字并不是Kotlin语言的一部分。作为替代方案，Kotlin提供了包级别函数（可以在大多数情况下替代Java的静态方法）和对象声明（大多数情况下替代Java的静态方法及静态成员），多数情况下，还是推荐使用顶层函数。

重点来了，标题是伴生对象，那么怎么来声明呢 ？

在类中定义一个用特殊关键字标记的对象：companion。companion修饰的对象，使得外部可以直接通过companion容器类来访问这个对象（companion object）的属性和方法，就像Java中对静态方法和静态成员的访问形式，不需要再通过具体实例来访问。

下来看下Factory类的另外一个写法，并同样打印Factory成员name的值。
```Kotlin
class Factory {
    companion object {
        const val name: String = "object single"
    }
}

fun main(args: Array<String>) {
    val factory : Factory = Factory()
    println(Factory.name)
}
```
可以看到Factory对象创建依然是普通类对象的创建方式，而对name成员的访问的形式使用的是类名. 方式访问，而不是具体实例factory.name方式访问。

在标题开始，写到伴生对象的另外一种描述是：工厂方法和静态成员的地盘。
静态成员的地盘这个描述相信通过上述的示例已经可以看出一二。

下来看看工厂方法是如何来表现的呢？
创建一个User对象，根据不同的参数来获取User属性name。
学习过Java的程序员首先想到的只怕是通过不同的构造方法，传入不同参数类型来实现。相应的Kotlin中也可以采用此种方式去实现。
```Kotlin
class User {
    val name: String

    constructor(name: String) {
        this.name = name
    }

    constructor(id: Int) {
        this.name = getNameBy(id)
    }

    private fun getNameBy(id: Int): String {
        // ...
        return ".."
    }
}
```

可以使用相同逻辑，但使用工厂方法来实现。
```Kotlin
class User private constructor(val name: String) {
    companion object {
        fun createUserByName(name: String): User {
            return User(name)
        }

        fun createUserById(id: Int): User {
            return User(getNameBy(id))
        }

        private fun getNameBy(id: Int): String {
            // ...
            return ".."
        }
    }
}
```
工厂方法非常有用，它可以返回声明这个方法的类的子类。但如果需


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MTc1NDg3MzYsMTIyNzQ3MTkzNCwtOD
U5OTkyNzI1LDE0MjkwNjA5MjMsLTE3MTI0Nzc2NjksMTgzNjg5
NjY4MiwxNTQxMzUyOTI4LDExODYxMjMyNDEsMTI2MzMxNDk1NS
wxNzQ4ODk3MzA5LC01OTc2MDYwODJdfQ==
-->