---
title: Python作业
categories: 编程语言
tags:
   - Python
   - 作业
cover: https://i.loli.net/2019/09/22/6wnyUf2ozePxtlg.jpg
---

###  回文串判断

以Python语言完成回文串的判断，以尽量多的方式或算法实现。目的在于熟悉最基本的Python语法。

```python
code = str(input("please input\n"))
ex_code = code[::-1]
if(ex_code==code):
    print("是回文数")
else:
    print("不是回文数")
```

### 猜数游戏

在程序中预设一个0~9之间的整数，让用户通过键盘输入所猜的数，如果大于预设的数，显示“遗憾，太大了”；如果小于预设的数，显示“遗憾，太小了”，如此循环，直至猜中该数，显示“预测N次，你猜中了！”，其中N是用户输入字数的次数。

```python
import random
number = random.randint(0,9)
print('请输入整数a:')
i = 0
while True:
    i = i + 1
    a = int(input())
    if a < number:
        print('遗憾，太小了')
    elif a > number:
        print('遗憾，太大了')
    else:
        print(f'预测{i}次，猜中了')
        break
```

改编第一题，让计算机能够随机产生一个预设数字，范围在0~100之间，其他游戏规则不变

```python
number = random.randint(0,100)
```

对于第二题，当用户输入的不是整数（如字母、浮点数等）时，程序会终止执行退出。改编该程序，当用户输入出错时给出“输入内容必须为整数！”的提示，并让用户重新输入。

```python
import random
number = random.randint(0, 9)  # 这里使用random()产生0~9之间整数
# print(secret)
print('------猜数字游戏！-----')
guess = -1
N = 0  # 记录次数
while guess != number:
    a = input('请输入数字0--9之间：\n')
    if not a.isdigit():  # 判断输入的是否为非整数
        print('输入内容必须为整数！！！！\n再来一次吧\n')
    else:
        N += 1
        guess = int(a)
        if guess > number:
            print('遗憾，太大了！\n')
        if guess < number:
            print('遗憾，太小了！\n')
if guess == number:
    print('预测{}次，你猜中了！'.format(N))
```

### 汉诺塔问题

用Python编写一个汉诺塔的移动函数，采用递归方法解决这个难题，要求输入汉诺塔的层数，输出整个移动流程。

```python
# 认识汉诺塔的目标：把A柱子上的N个盘子移动到C柱子
# 递归的思想就是把这个目标分解成三个子目标
# 子目标1：将前n-1个盘子从a移动到b上
# 子目标2：将最底下的最后一个盘子从a移动到c上
# 子目标3：将b上的n-1个盘子移动到c上
# 然后每个子目标又是一次独立的汉诺塔游戏，也就可以继续分解目标直到N为1
def move(n, a, b, c):
    if n == 1:
        print(a, '-->', c)
    else:
        move(n-1, a, c, b)  # 子目标1
        move(1, a, b, c)    # 子目标2
        move(n-1, b, a, c)  # 子目标3
n = input('enter the number:')
move(int(n), 'A', 'B', 'C')
```

讲下我对汉诺塔问题的理解

+ 第一步把a柱上除了最底下的一个圆盘也就是n-1个盘，通过c柱移动到b柱上。

```python
move(n-1,a,c,b)
```

+ 把n-1个盘移动到b上后，那么a上仅剩下最大一个盘，c上没有，那么就可以直接从a把最大盘移动到c上

```python
move(1,a,b,c)
```

+ c上已经有最大盘了，如何把b上n-1个盘再通过a，一个一个移动到c柱上（递归开始）

```python
move(n-1,b,a,c)
```

其实在最大盘放到c上以后，我可以理解c上没有盘，一切重新开始，只不过现在有n-1个盘，最大盘是n-1，因此重新走三步，不断地将剩余盘中最大的一个盘放到c柱，形成递归。

不断赋值的过程有点难以理解。

###  最大公约数

1. 枚举法

```python
def gys(a,b):
    if a>b:
        small=b
    else:
        small=a
    for i in range(1,small+1):  #range取值最后不包括small+1
        if (a%i==0) and (b%i==0) :
            c=i
    return c
num1=int(input("输入第一个数"))
num2=int(input("输入第二个数"))
gys(num1,num2)
print(f'{num1}和{num2}的最大公约数是{gys(num1,num2)}')
```

2.辗转相除法

```python
# 将两整数求余a%b=x
# 如果x=0；则b为最大公约数
# 如果x!=0，则a=b;b=x;继续从1开始执行
# 也就是说该循环的是否继续的判断条件就是x是否为0
def fun1(a,b):
    x = a % b
    while (x != 0):
        a = b
        b = x
        x = a % b
    return b
```

3.辗转相减法

```python
# 如果a>b,a=a-b;
# 如果b>a,b=b-a;
# 如果a=b,则a或b是最大公约数
# 如果a!=b，则继续相减，直至a=b
def fun2(a,b):
    while a != b:
        if a > b:
            a = a - b
        else:
            b = b - a
    return b
```

### python打印斐波那契数列第n项

```python
def fibo(n):
    if n==1 or n==2:
        return 1
    else:
        return fibo(n-1)+fibo(n-2)
```

###  从n个小球中取m个，问有多少种取法

```python
# n的阶乘
def C(n):
    result=1
    for a in range(1,n+1):
        result *= a
    return result

n=int(input("请输入n"))
m=int(input("请输入m"))
x=C(n)/(C(m)*C(n-m))
print(int(x))
```

### 打印出一个字符串中字符的所有排列(假设没有重复字符)

```python

```

### 重复元素判定

编写一个函数，接受列表作为参数，如果一个元素在列表中出现了不止一次，则返回True，但不要改变原来列表的值。同时编写调用这个函数和测试结果的程序。

续：利用集合的无重复性改编上一题，获得一个更快更简洁的版本。

```python
def Lbpd(a):    #定义函数Lbpd(a)
            a = a.split(" ")     #对参数a按照空格进行分词        
            if len(a)==len(set(a)):     #利用集合的不重复性，比较列表a和集合a的长度
                return "False,这是非重复序列"       #如相同则返回非重复序列

            else:       
                return "True,这是重复序列"       #如不同则返回重复序列

t = f = 0     #重复序列和非重复序列次数初始赋值
while True:     #让程序循环运行
    a =input("请输入一组序列，以空格隔开：")
    print(Lbpd(a))      #调用函数，打印函数参数为a时的返回值
    if Lbpd(a)=="True,这是重复序列":     #统计重复序列次数
        t +=1
    if Lbpd(a)=="False,这是非重复序列":     #统计非重复序列次数
        f +=1
    print("重复序列{}次，非重复序列{}次".format(t,f))       #打印输出统计结果语句
```

