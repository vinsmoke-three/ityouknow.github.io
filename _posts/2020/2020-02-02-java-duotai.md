---
layout: post
title: java学习笔记：多态简介
category: java
tags: [java]
---

多态指的是同一个方法调用，由于对象不同可能会有不同的行为。

## 多态的要点

1. 多态是方法的多态，不是属性的多态(多态与属性无关)。

2. 多态的存在要有3个必要条件：继承，方法重写，父类引用指向子类对象。

3. 父类引用指向子类对象后，用该父类引用调用子类重写的方法，此时多态就出现了。

**【示例】多态和类型转换测试**

```java
public class Polymorphism {
    public static void main(String[] args) {
        Human h1 = new Chinese();//向上自动转型
        //传的具体是哪一个类就调用哪一个类的方法。大大提高了程序的可扩展性。
        humanEat(h1);
        Human h2 = new American();
        humanEat(h2);

        //编写程序时，如果想调用运行时类型的方法，只能进行强制类型转换。
        // 否则通不过编译器的检查。
        Chinese h3 = (Chinese) h1;//向下转型
        h3.eatNoodle();
    }
    // 有了多态，只需要让增加的这个类继承Human类就可以了。
    static void humanEat(Human h) {
        h.eat();
    }
}

class Human {
    public void eat() {
        System.out.println("吃饭！！！");
    }
}

class Chinese extends Human {
    public void eat() {
        System.out.println("吃米饭！！！");
    }

    public void eatNoodle() {
        System.out.println("吃面条！！！");
    }
}

class American extends Human {
    public void eat() {
        System.out.println("吃面包！！！");
    }
}
```
