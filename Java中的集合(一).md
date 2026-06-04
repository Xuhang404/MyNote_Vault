---
tags:
  - "#Java"
  - "#集合"
  - "#Collecion"
  - "#Lambda"
  - "#并发修改异常"
  - "#数据结构"
---
----

**集合是一种容器,用来装数**

集合体系分两类
1. Collection 单列集合
2. Map 双列集合
- Collection代表单列集合,每个元素只包含一个值
- Map包含两个值,即一个键值对

---

# 单列集合Collection

[[Java中的Collection集合体系结构.canvas]]

上图表示了Java中的单列集合体系结构

Collection集合特点

- List系列集合:添加的元素**有序,可重复,有索引**
- Set系列集合:添加的元素**无序,不重复,无索引**
	- HashSet:无序,不重复,无索引
	- LinkedHashSet:**有序**,不重复,无索引
	- TreeSet:按照大小默认升序排序,不重复,无索引

其中最常用的就是ArrayList和HashSet,二者的特点完全相反

---

## Collection的常用方法

为什么要先学习Collection的方法?
- Collection是单列集合的祖宗接口,它规定的方法是全部单列集合继承的


Collection提供的通用方法:
- 获取集合的元素个数:`size()`
- 去删除元素:`list()`
- 判断是否为空:`isEmpty()`
- 清空集合:`clear()`
- 判断集合中是否存在某个数据:`contains()`
- 把集合转换成数组:`toArray()`
	- 例如: `Object[] arr = list.toArray();`

---
## Collection的遍历方式

### 一.迭代器遍历

迭代器是用来**遍历集合的专用方式**,在Java中迭代器的代表是`Iterator`

**Collection集合获取迭代器的方法:

方法名称:  `Iterator<E> iterator()`,它可以返回集合中的迭代器对象,该迭代器对象默认指向当前集合的第一个元素

**Iterator迭代器的常用方法

- `boolean hasNext()`,询问当前位置是否有元素存在
- `E next()`获取当前位置的元素,并同时将迭代器对象

```Java
public static CollectionIterator{
	public static void main(String[] args){
		
		Collection<String> list = new ArrayList<>();
		list.add("!");
		list.add("\");
		list.add("/");
		list.add("?");
		
		
		Iterator<String> it = list.iterator();
		
		while(it.hasNext()){//hasNext()询问当前位置有无数据,若有则返回true
			String str = it.next();
			sout("name");
		}
	
	}
}
```

>[!注意]
>迭代器会在一开始站在**第一个位置**,`next()`会先将迭代器当前所指的元素做返回,然后将迭代器迭代到下一个位置.

如果迭代器越界,会报`NoSuchElementException`异常

### 二.增强for循环

格式:
```Java
for(元素的数据类型 变量名:数组或者集合){

}
```

```Java
public static CollectionIterator{
	public static void main(String[] args){
		
		Collection<String> list = new ArrayList<>();
		list.add("!");
		list.add("\");
		list.add("/");
		list.add("?");
		
		for(String str:list){
			sout(str);
		}
	}
}
```

### 三.Lambda表达式(待补充)

[[Java中的Lambda表达式]]


### 四.三种遍历方式的区别

**认识并发修改异常问题:

遍历集合的同时又在对集合进行增删操作,可能出现业务异常,这个问题在[[Python基础语法(五)#^226950]]中已经遇到过

 ```Java
import java.util.ArrayList;  
import java.util.List;  
  
public class Test1 {  
  
    //认识并发修改异常  
    static void main() {  
       //创建一个集合对象  
       List<String> list = new ArrayList<>();  
       //添加一些元素  
       list.add("油条");  
       list.add("枸杞");  
       list.add("枸杞子");  
       list.add("特级枸杞");  
       list.add("包子")  ;
  
       for (int i = 0; i < list.size(); i++) {  
          String element = list.get(i);  
          //在迭代过程中修改集合  
          if (element.contains("枸杞")) {  
             list.remove(element); //这会导致ConcurrentModificationException异常  
          }  
       }  
  
       System.out.println(list);  
  
    }  
}
 ```
 
在这段代码中,遍历list集合,如果集合中的元素包含"枸杞",则将其移除,这看起来没有什么问题.

但是,程序的输出为:

```bash
[油条, 枸杞子, 包子]
```

显然没有完成需求,出现了bug

我们这样想:当遍历到第二个元素枸杞时,`remove()`方法将这个元素移除,与此同时,下一个元素补上了枸杞的位置.但是,在执行完这次循环后程序仍然进行了`i++`的操作,这就导致了错位,出现了并发修改异常问题

解决方法也很简单

1. 在删除数据后做一步`i--`操作

```Java
for (int i = 0; i < list.size(); i++) {  
          String element = list.get(i);  
          //在迭代过程中修改集合  
          if (element.contains("枸杞")) {  
             list.remove(element); 
             i--;  
          }  
       }  
```

2. 倒着遍历并删除,这也是[[Python基础语法(五)#^96ea04]]中提供的方法

前提是,进行遍历的集合或者容器支持索引,而显然`ArrayList`作为`List`的继承,是支持索引的

```JAVA
import java.util.ArrayList;  
import java.util.List;  
  
public class Test1 {  
  
    //认识并发修改异常  
    static void main() {  
       //创建一个集合对象  
       List<String> list = new ArrayList<>();  
       //添加一些元素  
       list.add("油条");  
       list.add("枸杞");  
       list.add("枸杞子");  
       list.add("特级枸杞");  
       list.add("包子");  
  
       for (int i = list.size() - 1; i > 0; i--) {  
          String element = list.get(i);  
          //在迭代过程中修改集合  
          if (element.contains("枸杞")) {  
             list.remove(element);   
          }  
       }  
  
       System.out.println(list);  
  
    }  
}

```

倒着遍历时,后一个元素仍然会补上来,但此时,我们遍历指针的运动方向和后补元素的运动方向是**同向**的,此时不会出现并发修改异常问题

接下来,我们来看看三种遍历方式能否解决并法修改异常问题

#### 1. 迭代器遍历

```Java
import java.util.ArrayList;  
import java.util.Iterator;  
import java.util.List;  
  
public class Test1 {  
  
    //认识并发修改异常  
    static void main() {  
       //创建一个集合对象  
       List<String> list = new ArrayList<>();  
       //添加一些元素  
       list.add("油条");  
       list.add("枸杞");  
       list.add("枸杞子");  
       list.add("特级枸杞");  
       list.add("包子");  
  
       Iterator<String> it = list.iterator();  
  
       while(it.hasNext()){  
          String str = it.next();  
          if(str.contains("枸杞")){  
             list.remove(str);  
          }  
       }  
  
       System.out.println(list);  
    }  
}
```

这段代码,看上去没什么问题,实则根本跑不起来,直接报错

```bash
Exception in thread "main" java.util.ConcurrentModificationException
	at java.base/java.util.ArrayList$Itr.checkForComodification(ArrayList.java:1096)
	at java.base/java.util.ArrayList$Itr.next(ArrayList.java:1050)
	at Test1.main(Test1.java:21)
```

`ConcurrentModificationException`就是并发修改异常

在底层源码上,迭代器遍历是不允许并发修改的,一旦编译器发现进行了并发修改,就会抛出异常

解决方法是:将`list.remove(str);`变为`it.remove();`而且在这以后底层会帮助我们进行退步的操作

#### 2. 增强for循环/3. Lambda循环

**直接说结论**:

这两种方式都不能解决并发修改异常问题,因为实际上底层这两种方法都是迭代器,但是在代码层面我们又拿不到他们的迭代器,就会抛出异常,这和上面抛出异常的原理是一样的


由此可以得到结论:

***增强for和Lambda表达式,只适合遍历,不适合在遍历时进行增删的场景,而迭代器遍历可以解决这个问题***

---

# List集合

特点:有序,可重复,有索引

list集合的特有方法:都与索引有关
- `add(int index,E element)`增
- `remove(int index)`删
- `set(int index ,E element)`改
- `get(int index)`查

## ArrayList和LinkedList

- ArrayList底层是基于[[数组]]存储数据的
- LinkedList底层是基于[[链表]]存储数据的

数组的特点:
- 连续的一块内存区域
- 根据索引查询数据的速度快--数组名记录数组首地址,根据索引加上对应的单位长度,查询任意数据耗时相同
- 增删数据效率低:需要把后面很多的数据进行前移

链表的特点:
- 链表中的数据是由一个一个独立的结点组成的,每个结点包含数据值和下一个结点的地址.
- **查询慢**,无论查询哪个数据都要从头开始找
- **增删相对快**,比如说在BD之间添加一个C,只需要
	1. 数据C对应的下一个结点的位置指向D
	2. 数据B对应的下一个结点的位置指向C
	删除同理
- LinkedList基于双链表实现,每个结点不仅包含下一个结点的位置,还包含上一个节点的位置,缺点是占内存大,优点是**对首尾元素进行增删改查的速度极快**,时间复杂度几乎是O(1)

因此LinkedList新增了很多首尾操作的特有方法:
- `addFirst(E e)`头插指定元素
- `addLast(E e)`尾插指定元素
- `E getFirst()`查询首元素
- `E getLast()`查询尾元素
- `E removeFirst()`删除头元素
- `E removeLast()`删除尾元素

LinkedList的应用场景:

1. 可以用来设计[[队列]](先进先出,后进后出),只是在首尾增删元素,用LinkedList来设计非常合适
