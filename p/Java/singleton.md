# 单例模式

特点：
1.单例类只有一个实例
2.单例类必须自己创建自己的唯一实例
3.必须有私有的构造方法
4.单例类必须给所有其他对象提供这一实例,必须有一个以自己实例为返回值的静态公有方法

## 饿汉式单例模式
```java
public class Singleton{
  private static Singleton singleton = new Signleton();
  private Singleton(){}
  
  public static Singleton getInstance(){
    return singleton;
  }  
}

```

## 懒汉单例模式

1.普通懒汉 （多线程会失败）

``` java
public class Singleton {

    private static Singleton singleton;

    private Singleton() {

    }

    public static synchronized Singleton getInstance(){
        if (singleton == null){
            singleton = new Singleton();
        }
        return singleton;
    }
}
```

2.双重锁定检查 （DCL）

``` java
    public static Singleton getInstance(){
        if (singleton == null){
            synchronized (Singleton.class){
                if (singleton == null){
                    singleton = new Singleton();
                }
            }
        }
        return singleton;
    }
```

3.延迟初始化占位（Holder）类模式

```java
public class Singleton {


    private static class LazyHolder {
        private static final Singleton INSTANCE = new Singleton();
    }

    private Singleton() {
    }

    public static final Singleton getInstance(){
        return LazyHolder.INSTANCE;
    }
}
```

第三种方式最优,一个静态内部类（占位类），在内部类中提前初始化实例，既保证了Singleton实例的延迟初始化，又保证了同步。这是一种提前初始化（饿汉式）和延迟初始化（懒汉式）的综合模式


### 优缺
优点

- 节省内存空间（只有一个对象）
- 避免频繁的开销
- 避免对共享资源的多重占用
- 全局访问

缺点

- 线程安全问题,饿汉式天生就是线程安全,懒汉式的话,为了线程安全的问题，才实现了以上三种方式。

### 三种懒汉模式的区别

1.在方法调用上加了同步关键字,虽然线程安全了，但每次都要同步，影响性能。非多线程环境下,基本99%的场景应该都不需要同步。
2.在getInstance中做了两次null检查,确保了只有第一次调用单例的时候才会做同步,解决了安全问题，也避免了资源消耗,但会存在指令重排序问题。
3.利用了classloader的机制来保证初始化instance时只有一个线程，所以也是线程安全的，同时没有性能损耗，所以一般我倾向于使用这一种。



参考:

1.http://blog.csdn.net/zhangzeyuaaa/article/details/42673245
2.http://blog.csdn.net/jason0539/article/details/23297037/

