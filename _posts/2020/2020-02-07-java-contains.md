---
layout: post
title: java学习笔记：集合_Collection
category: java
tags: [java]
excerpt: Collection集合以及Collection集合实现类实例
---

## Collection接口

Collection 表示一组对象，它是集中、收集的意思。collection包含Set、List、Queue。

* List：list接口包含ArrayList，Vector，LinkedList。
* Set包含HashSet，TreeSet，EnumSet。
* Queueu包含LinkedList，PriorityQueue

**<center>Collection的框架图</center>**

![](/assets/images/java/2020/20200207_collection.jpg)

**Collection接口的常用方法**

方法 | 说明
- | -
boolean add(E e) | 向集合中添加一个元素
boolean addAll(Collection c) | 向集合中添加集合c中的所有元素
void clear() | 清除集合中的所有元素
boolean contains(Object o) | 判断集合中是否存在指定元素
boolean containsAll(Collection c) | 判断集合中是否包含集合c中的所有元素
boolean isEmpty() | 判断集合是否为空
Iterator\<E\>iterator() | 返回一个 Iterator 对象，用于遍历集合中的元素
boolean remove(Object o) | 从集合中删除一个指定元素
boolean removeAll(Collection c) | 从集合中删除所有在集合c中出现的元素
boolean retainAll(Collection c) | 从集合中删除集合c里不包含的元素
int size() | 返回集合中元素的个数
Object[] toArray() | 把集合转换为一个数组，所有的集合元素变成对应的数组元素

由于List、Set是Collection的子接口，意味着所有List、Set的实现类都有上面的方法。

## List接口

List是有序、可重复的容器。

**有序**：List中每个元素都有索引标记。可以根据元素的索引标记(在List中的位置)访问元素，从而精确控制这些元素。

**可重复**：List允许加入重复的元素。更确切地讲，List通常允许满足 e1.equals(e2) 的元素重复加入容器。

**List接口中新增方法**

方法 | 说明
- | -
void add(int index, Object element) | 在指定位置插入元素
Object set(int index, Object element)| 修改指定位置的元素
Object get(int index) | 返回指定位置的元素
Object remove(int index) | 删除指定位置元素，后年后面元素全部前移一位
int indexOf(Object o) | 返回第一个匹配元素的索引，如果没有该元素返回-1
int lastIndexOf(Object o) | 返回最后一个匹配元素的索引，如果没有该元素返回-1

List接口常用的实现类有3个：ArrayList、LinkedList和Vector。
* ArrayList：底层实现的数据结构是数组，查询快，增删慢。线程不安全，效率高
* LinkedList：底层实现的数据结构是链表，查询慢，增删块。线程不安全，效率高
* Vector：底层实现的数据结构是数组，查绚块，增删慢。线程安全，效率低

## Set接口

Set容器特点：无序、不可重复。无序指Set中的元素没有索引，我们只能遍历查找;不可重复指不允许加入重复的元素。

Set接口继承自Collection，Set接口中没有新增方法，方法和Collection保持完全一致。

* HashSet：底层数据结构是哈希表（无序，唯一）。保证元素唯一性依赖于两个方法：hashCode()和equals()
* LinkedHashSet：底层数据结构是链表和哈希表。（FIFO，有序，唯一）。通过链表保证有序性， 通过哈希表保证唯一性。
* TreeSet：底层数据结构是红黑树。（唯一，有序）

**HashSet的使用**

```java
public class Test {
    public static void main(String[] args) {
        Set<String> s = new HashSet<String>();
        s.add("hello");
        s.add("world");
        System.out.println(s);
        s.add("hello"); //相同的元素不会被加入
        System.out.println(s);
        s.add(null);
        System.out.println(s);
        s.add(null);
        System.out.println(s);
    }
}

//执行结果
//[world, hello]
//[world, hello]
//[null, world, hello]
//[null, world, hello]
```

TreeSet内部需要对存储的元素进行排序，因此，我们对应的类需要实现Comparable接口。

这样，才能根据compareTo()方法比较对象之间的大小，才能进行内部排序。

* 由于是二叉树，需要对元素做内部排序。 如果要放入TreeSet中的类没有实现Comparable接口，则会抛出异常：java.lang.ClassCastException。

* TreeSet中不能放入null元素。

**TreeSet的使用**
```java
import java.util.Iterator;
import java.util.Set;
import java.util.TreeSet;

public class TestCollection {
    public static void main(String[] args) {
        User u1 = new User(1001, "vinsomke", 18);
        User u2 = new User(2001, "zoro", 5);
        Set<User> set = new TreeSet<User>();
        set.add(u1);
        set.add(u2);
        //TreeSet类中跟HashSet类一样也没有get()方法来获取列表中的元素，所以也只能通过迭代器方法来获取。
        Iterator<User> it =set.iterator();
        while(it.hasNext()){
        	System.out.println(it.next().id);
        }
    }
}

class User implements Comparable<User> {
    int id;
    String uname;
    int age;

    public User(int id, String uname, int age) {
        this.id = id;
        this.uname = uname;
        this.age = age;
    }
    /**
     * 返回0 表示 this == obj 返回正数表示 this > obj 返回负数表示 this < obj
     */
    @Override
    public int compareTo(User o) {
        if (this.id > o.id) {
            return 1;
        } else if (this.id < o.id) {
            return -1;
        } else {
            return 0;
        }
    }
}
```
## Map接口

Map是一种储存键值对 (key-value)对像的collection,在key-value的结果储存中，key不能重复，value可以重复。

Map 接口的实现类有HashMap、TreeMap、HashTable、Properties等。

**Map接口的常用方法**

方法 | 说明
- | -
Object put(Object key,Object value)|存放键值对
Object get(Object key)|通过键对象查找得到值对象
Object remove(Object key)|删除键对象对应的键值对
boolean containsKey(Object key)|Map容器中是否包含键对象对应的键值对
boolean containsValue(Object value)|Map容器中是否包含值对象对应的键值对
int size()|键值对的数量
bollean isEmpty|Map是否为空
void putAll(Map t)|将t的所有键值对存放到本Map对象
void clear()|清空本Map对象的所有键值对

**HashMap和HashTable**

HashMap采用哈希算法实现，是Map接口最常用的实现类。 由于底层采用了哈希表存储数据，我们要求键不能重复，如果发生重复，新的键值对会替换旧的键值对。 HashMap在查找、删除、修改方面都有非常高的效率。

HashTable类和HashMap用法几乎一样，底层实现几乎一样，只不过HashTable的方法添加了synchronized关键字确保线程同步检查，效率较低。
* HashMap: 线程不安全，效率高。允许key或value为null。
* HashTable: 线程安全，效率低。不允许key或value为null。

**HashMap的使用**
```java
import java.util.HashMap;
import java.util.Map;

public class TestMap {
    public static void main(String[] args) {
        Map<Integer, String> m1 = new HashMap<Integer, String>();
        Map<Integer, String> m2 = new HashMap<Integer, String>();
        m1.put(1, "one");
        m1.put(2, "two");
        m1.put(3, "three");
        m2.put(1, "一");
        m2.put(2, "二");
        System.out.println(m1.size());
        System.out.println(m1.containsKey(1));
        System.out.println(m2.containsValue("two"));
        m1.put(3, "third"); //键重复了，则会替换旧的键值对
        Map<Integer, String> m3 = new HashMap<Integer, String>();
        m3.putAll(m1);
        m3.putAll(m2);
        System.out.println("m1:" + m1);
        System.out.println("m2:" + m2);
        System.out.println("m3:" + m3);
    }
}
```
## Iterator迭代器

所有实现了 Collection 接口的容器类都有一个 iterator() 方法，用来返回一个实现了 Iterator 接口的对象

**遍历List方法一：普通for循环**
```java
for(int i=0;i<list.size();i++){//list为集合的对象名
    String temp = (String)list.get(i);
    System.out.println(temp);
}
```
**遍历List方法二：增强for循环(使用泛型!)**
```java
for (String temp : list) {
System.out.println(temp);
}
```
**遍历List方法三：使用Iterator迭代器(1)**
```java
for(Iterator iter= list.iterator();iter.hasNext();){
    String temp = (String)iter.next();
    System.out.println(temp);
}
```
**遍历List方法四：使用Iterator迭代器(2)**
```java
Iterator  iter =list.iterator();
while(iter.hasNext()){
    Object  obj =  iter.next();
    iter.remove();//如果要遍历时，删除集合中的元素，建议使用这种方式！
    System.out.println(obj);
}
```
**遍历Set方法一：增强for循环**
```java
for(String temp:set){
System.out.println(temp);
}
```
**遍历Set方法二：使用Iterator迭代器**
```java
for(Iterator iter = set.iterator();iter.hasNext();){
    String temp = (String)iter.next();
    System.out.println(temp);
}
```
**遍历Map方法一：根据key获取value**
```java
Map<Integer, Man> maps = new HashMap<Integer, Man>();
Set<Integer>  keySet =  maps.keySet();
for(Integer id : keySet){
System.out.println(maps.get(id).name);
}
```
**遍历Map方法二：使用entrySet**
```java
Set<Entry<Integer, Man>>  ss = maps.entrySet();
for (Iterator iterator = ss.iterator(); iterator.hasNext();) {
    Entry e = (Entry) iterator.next();
    System.out.println(e.getKey()+"--"+e.getValue());
```
