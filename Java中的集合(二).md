---
tags:
  - "#Java"
  - "#集合"
  - "#Set"
  - Collecion
  - "#数据结构"
  - "#哈希表"
---
上一篇:[[Java中的集合(一)]]

---

# 一.`Set`集合

**`Set`集合特点:不重复,无索引

`Set`系列集合有三个实现类:

 - **`HashSet`:无序,不重复,无索引(重要)
 - `LinkedHashSet`:有序,不重复,无索引
 - `TreeSet`:排序(默认一定要大小升序排序),不重复,无索引

因为`Set`集合无索引,所以也没有与索引相关的方法,用到的常用方法基本上都是`Collection`提供的

---

# 二.`HashSet`的原理(常用)

`HashSet`是基于**哈希表**存储数据的

### 哈希值

哈希值就是一个`int`类型的**随机值,Java中每个对象都有一个哈希值**

Java中的所有对象,都可以调用`Object`类提供`hashCode()`方法,返回该对象自己的哈希值

对象哈希值的特点:

- 同一个对象多次调用`hashCode()`方法返回的哈希值是相同的
- 不同的对象,他们的哈希值大概率不相等,但也有可能会相等(哈希碰撞)

## [[哈希表]]

- JDK8之前: 哈希表 = **数组 + 链表"
- JDK8开始: 哈希表 = 数组 + 链表　+ **[[红黑树]]**
- 哈希表是一种**增删改查数据,性能都很好的数据结构**

![[HashSet的底层原理.png]]

- 当有16 * 0.75 = 12 个位置不为`null`时,`table`就会扩容为32

- JDK8 开始,当链表的长度超过 8.且数组长度>=64时,自动将链表转成[[红黑树]]

以上两个措施都是为了保证哈希表的性能,用空间换时间

缺点:
- 不能重复
- 没有索引
- 占用内存大  

## 去重问题

虽然`HashSet`是不重复的,但是也存在一些问题,比如:

```Java
Student s1 = new Student("张三");
Student s2 = new Student("张三");
```

`s1`和`s2`看上去内容完全一样,但是Java会认为是两个对象,此时如果

```java
Set<Student> students = new HashSet<>();
students.add(s1);
students.add(s2);
```

`students`集合中仍然会同时包含`s1`和`s2`,无法做到去重

解决办法是在`Student`类中重写`HashCode()`和`equals()`方法,保证内容相同的两个不同对象在编译器看来是一个对象

---

# 三.`LinkedHashSet`的底层原理

特点:有序,不重复,无索引

`LinkedHashSet`底层原理依然是基于**哈希表**实现的,但是.它的**每个元素都额外的多了一个双链表的机制记录它前后元素的位置**, 因此,`LinkedHashSet`是有序的,

![[LinkedHashSet的底层原理.png]]

`LinkedHashSet`更加占用内存

---

# 四.`TreeSet`的底层原理

特点:
- 不重复,无索引,可排序(默认升序排序)
- 底层是基于**红黑树**实现的排序

注意:
- 对于数值类型:`Integer`,`Double`,默认按照数值本身的大小进行排序
- 对于字符串类型,默认按照首字符的编号升序排序
- 对于自定义类型如`Student`,`TreeSet`默认无法直接排序,因此需要**自定义排序规则

### 自定义排序规则

两种方法:
1. 对象类实现一个`Comparable<T>`接口,重写`compareTo()`方法,指定大小比较规则
2. `public TreeSet(Comparator c)`集合自带比较器`Comparator`对象,指定比较规则

方法一:
```Java
public class Teacher implements Comparable<Teacher>{  
    private int age;  
    //比较者.compareTo(被比较者);  
    //this -> 比较者(主调)  
    //o -> 被比较者(被调)  
    //规定:  
    //如果比较者>被比较者,返回正整数;  
    //如果比较者<被比较者,返回负整数;  
    //如果比较者=被比较者,返回0;  
    @Override  
    public int compareTo(Teacher o) {  
       //按照年龄升序排序  
       return this.age - o.age;  
    }  
}

```

Java规定:
- 如果比较者>被比较者,返回正整数;
- 如果比较者<被比较者,返回负整数;
- 如果比较者=被比较者,返回0;

方法二同理

---

下一篇:[[Java中的集合(三)]]