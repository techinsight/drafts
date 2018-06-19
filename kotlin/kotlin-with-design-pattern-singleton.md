title: 设计模式之单例模式
tags:
  - Kotlin
  - 设计模式

categories:
  - 设计模式
 author: 散人
---

单例模式应该是所有设计模式中最有名的设计模式了，原理简单：一个类型的实例在全局中只有一个对象，要调用这个实例的方法必须经由这个单例来完成。

最简单的Java实现方式:
```Java
public class Singleton {  
    private static final Singleton INSTANCE = new Singleton();  
    private Singleton() {}
    public static Singleton getInstance() {  
        return INSTANCE;  
    }  
}
```
对应Kotlin实现：
```Kotlin
object Singleton
```

这里是最简单的实现方式，但对于不想一开始就创建对象，即延迟创建，
```Java
public class Singleton {  
    private static Singleton INSTANCE;  
  
    private Singleton() {}  
  
    public static Singleton getInstance() {  
        if (INSTANCE == null) {  
            INSTANCE = new Singleton();  
        }  
        return INSTANCE;  
  }  
}
```
对应Kotlin实现：
```Kotlin
class Singleton private constructor() {  
    companion object {  
        val INSTANCE: Singleton by lazy { Singleton() }  
    }  
}
```

#### 为什么要延迟初始化呢？？
在《Java设计模式》(Steven John  Metsker, William C. Wake)一书中这样给出答案：

 1. 静态初始化时，没有足够信息对单例对象进行初始化。如工厂单例需要真正的工程类型才能建立起通信通道;
 2. 延迟加载也和资源获取有关，如数据库连接，尤其是在一个特定的会话中，它包含的应用程序并不需要该单例对象时。

换言之，采用延迟加载也有想对应的场景，

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIzMzYwMDY0OSw5OTA3NTg2OTAsLTEyOT
E1NzU5MjUsLTYwOTk0Nzg2OSw3MjEzNzMzMjcsLTI0NTM3ODc2
NSwxNTUxNTkwNzYwXX0=
-->