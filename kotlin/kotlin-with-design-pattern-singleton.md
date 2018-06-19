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
  
    public static Singleton getInstance() {  
        return INSTANCE;  
    }  
}
```
对应Kotlin实现：
```Kotlin
object Singleton
```

这里是最简单的实现方式，但对于不想一开始就创建实力，可以
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5NzcyMzgxMTAsLTYwOTk0Nzg2OSw3Mj
EzNzMzMjcsLTI0NTM3ODc2NSwxNTUxNTkwNzYwXX0=
-->