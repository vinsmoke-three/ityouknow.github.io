---
layout: post
title: java学习笔记：抽象类、抽象方法、接口
category: java
tags: [java]
---

## 抽象方法

使用abstract修饰的方法，没有方法体，只有声明。定义的是一种“规范”，就是告诉子类必须要给抽象方法提供具体的实现。

## 抽象类

包含抽象方法的类就是抽象类。通过abstract方法定义规范，然后要求子类必须定义具体实现。

**【示例】抽象类和抽象方法的基本用法**

```java
public class TestAbstract {
    public static void main (String[] args) {
        Chinese2 c = new Chinese2();
        c.eat();
    }
}

//抽象类
abstract class Human2 {
    abstract public void eat();
}

class Chinese2 extends Human2{

    //子类必须实现父类的抽象方法，否则编译错误
    @Override
    public void eat() {
        System.out.println("吃米饭");
    }
}
```

**抽象类的使用要点**

1. 有抽象方法的类只能定义成抽象类

2. 抽象类不能实例化，即不能用new来实例化抽象类。

3. 抽象类可以包含属性、方法、构造方法。但是构造方法不能用来new实例，只能用来被子类调用。

4. 抽象类只能用来被继承。

5. 抽象方法必须被子类实现。

## 接口

接口就是比“抽象类”还“抽象”的“抽象类”，可以更加规范的对子类进行约束。全面地专业地实现了：规范和具体实现的分离。

**声明格式**

```java
public interface TestInterfaceClass {
    //常量定义
    //方法定义
}
```

**定义接口的详细说明：**

1. 访问修饰符：只能是public或默认。

2. 接口名：和类名采用相同命名机制。

3. extends：接口可以多继承。

4. 常量：接口中的属性只能是常量，总是：public static final 修饰。不写也是。

5. 方法：接口中的方法只能是：public abstract。 省略的话，也是public abstract。

**要点**

1. 子类通过implements来实现接口中的规范。

2. 接口不能创建实例，但是可用于声明引用变量类型。

3. 一个类实现了接口，必须实现接口中所有的方法，并且这些方法只能是public的。

4. JDK1.7之前，接口中只能包含静态常量、抽象方法，不能有普通属性、构造方法、普通方法。

5. JDK1.8后，接口中包含普通的静态方法。

**接口的使用**

```java
public class TestInterface {
    public static void main(String[] args) {
        Sql p1 = new Project1();
        //p1.java();//只能调用Sql接口的实现
        p1.mySql();

        Program p2 = new Project1();
        p2.java();
    }
}

//sql接口
interface Sql {
    String NAME = "动物";//类型：public static final
    void mySql();//public abstract void mySql();
}
//编程语言接口
interface Program {
    void java();
}

//实现多个接口
class Project1 implements Sql,Program{

    @Override
    public void java() {
        System.out.println("编程语言接口实现");
    }

    @Override
    public void mySql() {
        System.out.println("sql接口实现");
    }
}

class Project2 implements Program{

    @Override
    public void java() {
        System.out.println("编程语言接口实现");
    }
}
```


## 接口的多继承

接口完全支持多继承。和类的继承类似，子接口扩展某个父接口，将会获得父接口中所定义的一切。

```java
interface A {
    void testa();
}
interface B {
    void testb();
}
/**接口可以多继承：接口C继承接口A和B*/
interface C extends A, B {
    void testc();
}
public class MyTest implements C {
    public void testc() {
    }
    public void testa() {
    }
    public void testb() {
    }
}
```
