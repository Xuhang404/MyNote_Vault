---
tags:
  - Python
---
上一篇[[Python基础语法(三)]]

---

# if条件判断

```python
#if条件判断基本格式

if 要判断的条件: #判断语句的结果,必须是布尔类型,注意冒号
	条件成立时,要执行的操作 #前面需要缩进
```

>[!注意]
>Python是通过缩进来描述代码归属的,归属于if代码块的语句,需要在前方缩进

```python
#if...else 结构
if 要判断的条件:#注意冒号
	条件成立时,执行的语句
else:#注意else后要有冒号
	条件不成立时,执行的语句
```


---

#例题

需求:根据用户输入的年份,判断这一年是闰年还是平年

```PYTHON
'''
非整百年份,且能被4整除是闰年
整百年份能被400整除是闰年
'''

year = int(input("请输入年份:"))

if (year % 4 == 0 and year % 100 != 0)or(year % 400 == 0):

    print(f"{year}是闰年")

else:

    print(f"{year}不是闰年")
```

---
## if语句进阶-if..elif..else

```python
# if..elif..else
if 要判断的条件1:
	语句
elif 要判断的条件2:
	语句
else:
	语句
```

其实就等效于别的语言中的:
```C
if (条件一)
	{
	语句;
	}
else if(条件2)
	{
	语句;
	}
else
	{
	语句;
	}
```

题外话:可以看出Python极大的简化了语法格式,不需要分号,不需要大括号

---

#例题 

根据输入的用户名和密码进行登陆系统
- 用户名,密码为admin/666888或root/071025或xuhang/111111时登录成功
- 否则登陆失败

```python
account = input("请输入用户名")
password = input("请输入密码")

if account == "admin" and password == "666888":
    print("登录成功!")
elif account == "root" and password == "071025":
    print("登录成功!")
elif account == "xuhang" and password == "111111":
    print("登录成功!")
else:
    print("登录失败!")
``` 

---

# match模式匹配

类比于C和Java中的switch case

例如:

```python
day = int(input("请输入星期几"))

match day:
	case 1:
		语句
	case 2:
		语句
	case 3:
		语句
	case 5|6|7:
		语句
	case _:# 相当于switch case中的default
		语句	
```

---

# 循环

## 1. while循环

```python
# while语法
while 条件表达式:
	语句
	语句
	...
else:
	条件表达式为false 时执行的语句
```

其中:`else:`及其后面的代码段为非必要的

---

## 2 . for循环

while循环时通过条件表达式来控制是否要进行下一次循环的,而for循环本质上是一种**轮询遍历**机制,对一批内容进行逐个处理

*虽然我觉得在别的语言中,while和for本质上没有什么区别,for循环可以翻译成while,反之亦然,纯看开发者个人习惯*

**但是**,在python中:

先来看基础语法

```python
#for循环结构
for 元素 in 待处理数据集:
	循环体代码
else :
	循环结束时要执行的代码
```

什么叫待处理数据集?

简单来说，它就是一个**可迭代对象（Iterable）**

例如,遍历字符串:
```python
msg = "helloworld"

for i in msg:
	print(i)
else:
	print("over")
```

----

### range语句

- 作用:生成制定规则的数字序列

用法:
	1. range(end) -> 获取一个从0开始到end结束的序列,不含end本身
	   range(5)就是0.1.2.3.4
	2. range(start,end) -> 获取一个从start开始到end结束的序列,不含end本身
	   range(2,8) -> 234567
	3. range(start,end,step) -> 获取一个从start开始,到end结束的数字序列,step是步长(不含end本身)
	   range(0,10,2) -> 0.2.4.6.8

---

下一篇:[[Python基础语法(五)]]


