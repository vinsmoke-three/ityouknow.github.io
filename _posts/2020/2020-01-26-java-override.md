---
layout: post
title: java学习笔记：方法的重写Override
category: java
tags: [java]
---

子类通过重写父类的方法，可以用自身的行为替换父类的行为。方法的重写是实现多态的必要条件。

## 方法的重写需要符合下面的三个要点：

1. “==”： 方法名、形参列表相同。

2. “≤”：返回值类型和声明异常类型，子类小于等于父类。

3. “≥”： 访问权限，子类大于等于父类。

**【示例】方法重写**

```java
public class TestOverride {
    public static void main(String[] args) {
        Vehicle v1 = new Vehicle();
        Vehicle v2 = new Horse();
        v1.run();
        v2.run();
        v2.stop();
    }
}

class Vehicle { // 交通工具类
    public void run() {
        System.out.println("跑....");
    }
    public void stop() {
        System.out.println("停止不动");
    }
}
class Horse extends Vehicle { // 马也是交通工具
    // 重写父类方法
    @Override
    public void run() {
        System.out.println("四蹄翻飞，嘚嘚嘚...");
    }
}
```
## Object类基本特性

Object类是所有Java类的根基类，也就意味着所有的Java对象都拥有Object类的属性和方法。如果在类的声明中未使用extends关键字指明其父类，则默认继承Object类。

**【示例】Object类**

```java
public class Person {
    ...
}
//等价于：
public class Person extends Object {
    ...
}
```

## toString方法

Object类中定义有public String toString()方法，其返回值是 String 类型。

Object类中toString方法的源码为：

```java
public String toString() {
    return getClass().getName() + "@" + Integer.toHexString(hashCode());
}
```

根据如上源码得知，默认会返回“类名+@+16进制的hashcode”。在打印输出或者用字符串连接对象时，会自动调用该对象的toString()方法。

**【示例】toString()方法测试和重写toString()方法**
```java
public class TestToString {
    public static void main (String[] args) {
        Person2 p = new Person2();
        p.age = 20;
        p.name="小明";
        System.out.println("info:"+p);//toString方法被重写的情况下
        Person3 p3 = new Person3();
        System.out.println(p3);//toString没有被重写的情况下
    }
}

class Person2 {
    String name;
    int age;
    @Override
    public String toString(){
        return name + ",年龄:" + age;
    }
}

class Person3 {

}
```

## ==和equals方法

“==”代表比较双方是否相同。如果是基本类型则表示值相等，如果是引用类型则表示地址相等即是同一个对象。

Object类中定义有：public boolean equals(Object obj)方法，提供定义“对象内容相等”的逻辑。

Object 的 equals 方法默认就是比较两个对象的hashcode，是同一个对象的引用时返回 true 否则返回 false。

但是，我们可以根据我们自己的要求重写equals方法。

**【示例】equals方法测试和自定义类重写equals方法**

```java
public class TestEquals {
    public static void main(String[] args) {
        Person4 p1 = new Person4(1001,"小明");
        Person4 p2 = new Person4(1001,"小红");
        System.out.println(p1 == p2);//false,不是同一个对象
        System.out.println(p1.equals(p2));//true,equals()已被重写，id相同则认为两个对象相同
    }
}
class Person4 {
    int id;
    String name;
    public Person4(int id ,String name) {
        this.id = id;
        this.name = name;
    }
    @Override
    public boolean equals(Object obj) {
        if (this == obj)
            return true;
        if (obj == null)
            return false;
        if (getClass() != obj.getClass())
            return false;
        Person4 other = (Person4) obj;
        if (id != other.id)
            return false;
        return true;
    }
}
```

**eclipse快速添加想要重写的equals方法：右键>source>Generate hashCode() and equals()...**

## super关键字

super是直接父类对象的引用。可以通过super来访问父类中被子类覆盖的方法或属性。

使用super调用普通方法，语句没有位置限制，可以在子类中随便调用。

若是构造方法的第一行代码没有显式的调用super(...)或者this(...);

那么Java默认都会调用super(),含义是调用父类的无参数构造方法。这里的super()可以省略。

**【示例】super关键字的使用**

```java
public class TestSuper {
    public static void main(String[] args) {
        new ChildClass().f();
    }
}
class FatherClass {
    public int value;
    public void f() {
        value = 100;
        System.out.println("FatherClass.value="+value);
    }
}
class ChildClass extends FatherClass{
    public int value;

    public void f() {
        super.f();//调用父类对象的方法f();
        value = 200;
        System.out.println("ChildClass.value="+value);
        System.out.println(value);
        System.out.println(super.value);//调用父类对象的成员变量
    }
}
```

## 构造方法调用顺序

构造方法第一句总是：super(…)来调用父类对应的构造方法。

所以，流程就是：先向上追溯到Object，然后再依次向下执行类的初始化块和构造方法，直到当前子类为止。

注：静态初始化块调用顺序，与构造方法调用顺序一样，不再重复。

**【示例】构造方法向上追溯执行测试**

```java
public class TestSuper2 {
    public static void main(String[] args) {
        System.out.println("开始创建一个ChildClass对象......");
        new ChildClass2();
    }
}
class FatherClass2 {
    public FatherClass2() {
        System.out.println("创建FatherClass");
    }
}
class ChildClass2 extends FatherClass2 {
    public ChildClass2() {
        System.out.println("创建ChildClass");
    }
}
```
```Java
//执行结果
开始创建一个ChildClass对象......
创建FatherClass
创建ChildClass
```
