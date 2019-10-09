---
title: Python语言基础笔记
date: 2019-9-15 17:16:36
categories: 编程语言
tags:
   - Python
cover: https://i.loli.net/2019/09/15/s3pEh17grebmZ6l.jpg
---




### Python 变量类型


<style>
table th:first-of-type {
	width: 100px;
}
</style>

<center>名称|<center>类型|<center>说明
:-:|:-:|:-:
整数|int|不带小数点的数：5、16、-24、0
小数|float|带小数点的数:3.14、-6.7、4.0
字符串|string|有序的字符序列："你好"、"Hello"、"100"、'3.14'
布尔值|bool|用于逻辑运算的类型，值只有 True 或者False
列表|list|有序序列：[100,"Hello",-12.5,100]
字典|dictionary|无序的键值对：{"小明":"66分","小红":"23分"}
元组|tuple|有序且不可变序列:(100,"Hello",-12.5,100)
集合|set|无序且无重复元素：{"A","B","C"}

变量使用前必须先赋值,可连续赋值如:a,b,c = 1,2,3  

<font size=6 >浮点数和小数不完全相同！！！</font>



### 特殊算数运算


<center>符号|<center>作用
:-:|:-:|
\**|指数运算
%|取余
//|整数除法


### 控制台输入输出

``` python
name = input("请输入名字")
print(name+",hello")
```



### 类型转换
Python中"+"只能连接两个类型一样的值，当需要连接的值类型不同时需要强制转换
``` python
hp=358
max_hp=1462
result= hp/ max_hp
result *= 100
# 将result转换为int型
result = int(result)   
# 将result转换为字符串型，方便连接
print(str(result)+"%")  
```



### 关于字符串和字符

>首先字符串不可变

#### 字符串下标

![](https://i.loli.net/2019/09/14/kvKb5Bn3YXAz4p7.png)

特殊用法(字符串倒序)【判断回文串】
``` python
my_string = "0123456789"
print(my_string[::-1])
```

#### 字符串方法
>my_string = "Hello, World"
<center>函数|<center>作用|<center>说明
:-:|:-:|:-:
len()|获取字符串长度|len(my_string)  #输出结果为13
find()|查找子字符串|find('w') #输出结果为7
count()|字符串出现的次数|count('l')  #输出结果为3
in和not in|是否包含子字符串|"Hello" in my_string  #输出结果为True
replace|字符串替换|my_string.replace("o","-") #输出结果为"Hell-,W-rld"
split|字符串分割|my_string.replace("o") #返回数组或list类型，输出结果为['Hell',',World']

>所有操作对my_string没有影响

``` python
my_string = "Hello, World"
c = my_string.count("e")
index = my_string.find("o")
new string = my_string.replace("o","") #空字符串相当于删除o
is_in = "H"in my_string  #只返回True或False
```

#### 转义字符

>转换字符原本的意义
<center>符号|<center>表示
:-:|:-:|
\\"| "
\\'|'
//|/
\n|换行
\t|制表符 Tab

#### 原始字符串


>r"..." 表示原始字符串 使所有的转义字符失效  比如 r"C:\test"

>"""创建多行字符串

``` python
html = """<html>
     <head>
     </head>

     <body>
     </body>
   <html>"""  #中间可直接回车换行
```

``` python
my_string = "\""  #这样才能正常运行
my_string = r"\n表示换行"  #大写R也可以
```

### 格式化 

#### 格式化字符串

> 将其它类型的数据按照指定格式转换成字符串(用str（）显得代码过长)

+ F-String

```python
age = 16
result = f"小明今年{age}岁了！"
```

+ format()

```python
age = 16
result = "小明今年{}岁了".format(age)  # {}占位符
```

#### 格式化数字

> 对数字进行精度等操作(下图为保留两位小数)

![](https://i.loli.net/2019/09/16/4GZnPEdwNxarX7I.png)

```python
result1 = f"这个数{pi:#b}以二进制显示"
result2= f"这个数{pi:#o}以八进制显示"
result3 = f"这个数{pi:#x}以十六进制显示"
print(result1,result2,result3)   #  {}里#表示开头标志可不加
```

![](https://i.loli.net/2019/09/16/WSRXpj2JMmq3DNZ.png)

### 运算



#### 关系运算

![](https://i.loli.net/2019/09/16/1R9OJetn5jpwEsK.png)

> string 0 1 2 ... 9 < A B C ... Z < a b c ... z

```python
print("Hello">"Hi")  #输出为False  先比较第一位，再比较第二位，i>e 
```

#### 逻辑运算

> 结果为bool值

in    //    not in       

is    //    is not    

### if语句

#### if和else

> if 语句需要冒号和缩进4个空格(一个tab)

```python
num = input("请输入一个整数")
num = int(num)
if num & 2 == 0 :
    print(f"输入的是{num},是偶数")
else:
    print(f"输入的是{num},是奇数")
```



#### if语句练习

1.提示用户输入一个年份，判断这一年是不是闰年（闰年条件：能被400整除或者能被4整除但不能被100整除）

```python
year = int(input("输入一个年份"))
if (year % 400 == 0 ) or(year % 4 ==0 and year % 100!=0):
    print(f"{year}年是闰年")
else:
    print(f"{year}年不是闰年")
```

2.提示用户输入一个1——99999之间的整数，分别显示这个数字个十百千万位上的数字

```python
number = int(input("请输入一个1——99999之间的整数"))
a1 = number % 10
a10 = number // 10 % 10
a100 = number // 100 % 10
a1000 = number // 1000 % 10
a10000 = number // 10000 % 10
print(f"{number}每位上的值：个：{a1} 十位：{a10} 百位:{a100} 千位:{a1000} 万位：{a10000} ")
```

3.实现一个剪刀、石头、布的猜拳游戏：玩家输入1、2、3来表示剪刀、石头、布，程序随机选择剪刀、石头、布与玩家比较。

```python
# Python中生成随机数的方法：
# import random
# number = random. randint(1,3)
import random
number = random.randint(1,3)
a = int(input("请输入1、2、3代表剪刀 石头 布\n"))
print(f'电脑输入的是{number}')
if a == number:
    print("平局")
else:
    if a > number and not (a == 3 and number == 1):
        print("win")
    elif a == 1 and number == 3:
        print("win")
    else:
        print("lose")
```

### 列表和下标

#### 列表（list）

也叫数据容器，Python中list支持不同类型元素

```python
my_list = [12,"A",3.5,6,'Hi',True]
my_list[2]  #列表下标从0开始
my_list[-1] #也可以用负数下标
my_lisy[1:4] #[start:end:step]进行截取
```



#### 列表简单使用

1. 使用in或not in判断列表是否包含某个元素  #12 in my_list
2. 使用len()函数获取列表中的元素个数  #len(my_list)
3. 使用加法+拼接两个列表  #new_list = list1+list2
4. 使用乘法*重复某个列表  #new_list = my_list * 3
5. 使用reverse()方法反序某个列表  #my_list.reverse()
6. 使用**max()**或min()函数h获取列表中**最大**或最小的元素    #max(my_list)  或min(my_list)
7. 使用sort()方法排序某个列表  #my_list.sort()

```python
# 反序
a=['hi','hello']
a.reverse()
print(a)   
# 排序
b=[1,3,5,7,2,4]
b.sort()
print(b)
```

#### 修改查找元素

1. 通过下标查找元素内容
2. 查找内容首次出现的下标  # my_list.index("Hi") **出现多次的话只显示第一次出现的下标**
3. 查找指定内容出现的次数  # my_list.count(6)

```python
s = "周一,周二,周三,周四,周五,周六,周日"
a = s.split(",")  #将字符串分为列表
print(a)
s2 = "+".join(a)  #将列表连接为字符串 （a）中所有元素需为字符串类型
print(s2)
```

#### 增加元素

