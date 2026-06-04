---
tags:
  - Python
---


本系列所有笔记基于B站黑马程序员python课程[课程链接](【黑马程序员Python+AI零基础入门到大神全套视频课程，覆盖Python核心语法、AI应用、数据分析及Web应用等python实战项目开发全流程】 https://www.bilibili.com/video/BV1sHU9BmEne/?p=7&share_source=copy_web&vd_source=3b33dbfeab9f1d66b195af736b04ed2f) -

开发工具:VScode

---

# 一 入门程序

```python
# 注释:#+空格为整行注释

print("hello world)

# 注意:python程序中不需要分号,但是若将两行代码写在一行,则需要分号分隔

print("hello world");print("hello world)"
```

---

# 二 字面量

**字面量:程序中直接书写的固定值.**

**字面量的种类:
- 数字类型:
	1. 整数(int)
	2. 浮点数(float)
- 布尔类型(bool):真或假,True(1),False(0),*首字母大写*
- 字符串(str) 所有引号囊括的内容都是字符串
-  空值(NoneType) 表示无或空值,仅包含一个值None
- 数据容器

---


# 三 变量

---

## 变量的定义

定义格式:
` 变量名 = 变量的值`
如:
`num = 1114.1`
`num = 114.2`

> [!说明]
> python是动态类型语言,在程序运行时才进行类型检查,变量的类型可以在程序运行过程中改变,且一个变量可以接受不同类型的值,故不需要类似其他语言一样在声明变量时确定变量的类型.


```Python
num = 1114.1
print(num)
num = num + 1
print(num)
num = "OK"
print(num)
```

输出如下

```Powershell
1114.1
1115.1
OK
```

Python还可以一次性定义多个变量
```python
num1,num2 = 30, 41
```

---

## 标识符

- **标识符**是程序员在代码中为变量,函数,类等元素所起的**名字
- **命名规则:
	1. 只能包含字母,数字,下划线
	2. 不能以数字开头
	3. 不能使用Python中的关键字
	4. 严格区分大小写
- **变量的命名规范(PEP8标准)
	1. 见名知意
	2. 蛇形命名法:多个部分使用下划线链接(update_time,my_name)
	3. 英文字母全小写

---

#例题

 **例:交换两个变量的值**
 
```python
num1,num2 = 10,20

print("Before swapping: num1 =",num1,"num2 =",num2)

temp = num1

num1 = num2

num2 = temp

print("After swapping: num1 =",num1,"num2 =",num2)
```


---

# 四 常见数据类型


| 数据类型     | 描述  | 说明                |
| -------- | --- | ----------------- |
| int      | 整数  | 数字类型,用于存放整数       |
| float    | 浮点数 | 数字类型,用于存放小数       |
| str      | 字符串 | 用引号包裹             |
| bool     | 布尔  | 描述真假,真True,假False |
| NoneType | 空值  | 仅包含值None          |

1. 通过`type( )`来得到数据的类型,`type(要查看的数据)`
```python
print(type("hello"))

num = 5

print(type(num))
```

2. 通过`isinstance(数据,类型)`检查数据是否属于指定的类型,返回一个bool类型的值
```python
num = 100

print(isinstance(num,int)) # 返回true
```

---
下一篇:[[Python基础语法(二)]]

