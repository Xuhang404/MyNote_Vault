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
>`Map`系列集合的特点都是由键决定的,值只是一个附属品

- `HashMap`:无序,不重复,无索引(用的最多)
- `LinkedHashMap`有序,不重复,无索引
- `TreeMap`:按照大小默认升序排序,不重复,无索引

