---
layout: post
title: java学习笔记：继承_instanceof运算符
category: java
tags: [java]
---

## 继承的概念

继承是java面向对象编程技术的一块基石，因为它允许创建分等级层次的类。

继承就是子类继承父类的特征和行为，使得子类对象（实例）具有父类的实例域和方法，或子类从父类继承方法，使得子类具有父类相同的行为。

## 继承的特性

1. 子类拥有父类非 private 的属性、方法。

2. 子类可以拥有自己的属性和方法，即子类可以对父类进行扩展。

3. 子类可以用自己的方式实现父类的方法。

4. Java 的继承是单继承，但是可以多重继承，单继承就是一个子类只能继承一个父类，多重继承就是，例如 A 类继承 B 类，B 类继承 C 类，所以按照关系就是 C 类是 B 类的父类，B 类是 A 类的父类，这是 Java 继承区别于 C++ 继承的一个特性。

5. 提高了类之间的耦合性（继承的缺点，耦合度高就会造成代码之间的联系越紧密，代码独立性越差）。

**【示例】使用extends实现继承**
```java
public class TestExtends {
    public static void main(String[] args) {
        Student stu = new Student("小明",20,"java");
        stu.rest();//拥有父类的方法
        stu.study();
    }
}

class Person {
    String name;
    int age;
    public void rest() {
        System.out.println("take rest!");
    }
}

class Student extends Person {
    String major;//专业
    public void study () {
        System.out.println(this.name+"在学习");
    }
    public Student(String name,int age,String major) {
        //拥有父类的属性：name,age
        this.name = name;
        this.age = age;
        this.major = major;
    }
}
```

## instanceof运算符

instanceof是二元运算符，左边是对象，右边是类；当对象是右面类或子类所创建对象时，返回true；否则，返回false。比如：

**【示例】使用instanceof运算符进行类型判断**

```java
public class TestExtends {
    public static void main(String[] args) {
        Student stu = new Student("小明",20,"java");
        System.out.println(stu instanceof Person);//true
        System.out.println(stu instanceof Student);//true
        stu.rest();//拥有父类的方法
        stu.study();
    }
}
```
