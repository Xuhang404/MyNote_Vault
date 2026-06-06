---
tags:
  - "#Java"
  - "#数据结构"
  - "#Map"
---
上一篇:[[Java中的集合(二)]]

---

# `Map`集合

`Map`集合不属于`Collection`系列

`Map`集合的特点:每个元素的数据是成对出现的,称为键值对,因此`Map`集合也被称之为键值对集合

格式:`{key1=value1,key2=value2,...}`

`Map`集合的所有`key`是不可以重复的,但`value`可以重复,`key`与`value`一一对应

`Map`集合的根接口就是`Map<K,V>`

[[Java中Map集合的体系结构.canvas]]

>[!注意]
>`Map`系列集合的特点都是由键决定的,值只是一个附属品,也就是说不能重复的是`key`,与`value`无关

- `HashMap`:无序,不重复,无索引(用的最多)
- `LinkedHashMap`有序,不重复,无索引
- `TreeMap`:按照大小默认升序排序,不重复,无索引
 
---

# `Map`集合的常用方法

与`Collection`类似,`Map`是双列集合的祖宗接口,它的功能是所有双列集合都可以继承使用的

| 方法名称                                 | 说明                   |
| ------------------------------------ | -------------------- |
| `V put(K key,V value)`               | 像集合中添加元素,返回值是`value` |
| `int size()`                         | 获取集合的大小              |
| `void clear()`                       | 清空集合                 |
| `boolean isEmpty()`                  | 判断集合是否为空             |
| `V get(Object key)`                  | 根据键获取对应值             |
| `V remove(Object key)`               | 根据键删除整个键值对           |
| `boolean containsKey(Object key)`    | 根据键判断是否包含某个键值对       |
| `boolean containValue(Object value)` | 根据值判断是否包含某个键值对       |
| `Set<K> keySet()`                    | 提取集合中所有的键            |
| `Collection<V> values()`             | 提取集合中所有的值            |

---

# `Map`集合的遍历方式

## 一.键找值

思路:先获取`Map`集合的全部的键,再通过遍历键来找值

