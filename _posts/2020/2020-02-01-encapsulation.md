---
layout: post
title: java学习笔记：封装
category: java
tags: [java]
---

Java中4种“访问控制符”分别为private、default、protected、public，它们说明了面向对象的封装性，所以我们要利用它们尽可能的让访问权限降到最低，从而提高安全性。

## 访问控制符

1. private 表示私有，只有自己类能访问
2. default表示没有修饰符修饰，只有同一个包的类能访问
3. protected表示可以被同一个包的类以及其他包中的子类访问
4. public表示可以被该项目的所有包中的所有类访问

## 封装的使用细节

1. 一般使用private访问权限。

2.  提供相应的get/set方法来访问相关属性，这些方法通常是public修饰的，以提供对属性的赋值与读取操作(注意：boolean变量的get方法是is开头!)。

3. 一些只用于本类的辅助性方法可以用private修饰，希望其他类调用的方法用public修饰。

**【示例】封装实例**

```java
public class Encapsulation {
    //属性一般使用private修饰
    private String name;
    private int age;
    private boolean flag;
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        this.age = age;
    }
    public boolean isFlag() {
        return flag;
    }
    public void setFlag(boolean flag) {
        this.flag = flag;
    }
}
```
