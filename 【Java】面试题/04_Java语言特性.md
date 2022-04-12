# JDK 版本差异新特性

# 动态代理

# 反射

# 数据类型

# 常用集合

## 1、String

### 1.1 String 的特点

（1）JDK 版本 1.8 来说，String 内部实际存储结构为 char 数组

```java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence {
    // 用于存储字符串的值
    private final char value[];

    // 缓存字符串的 hash code
    private int hash; // Default to 0
    
    // ......其他内容
}
```

（2）String类对象的相等判断使用equals() 方法完成，“==”实现的是地址数值的比较。

（3）字符串内容一旦声明则不可改变，String类对象内容的改变是依靠引用关系的变更实现的。

（4）String类有两种实例化方式，使用直接赋值可以不产生垃圾空间，并且可以自动入池，不要使用构造方法完成



#### 【扩展问题】== 和 equals 的区别

#### 【扩展问题】final 修饰 string 的好处

#### 【扩展问题】String 常见的创建方式



### 1.2 String 的重要方法





# 对象引用

# 异常机制

# SPI机制

# 注解处理机制