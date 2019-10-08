---
title: C++语言入门
categories: 编程语言
tags:
   - C++
cover: https://i.loli.net/2019/09/27/OGRYuThsSbi9jqv.jpg
---

### 为什么要学C++

考研复试有C++上机，笔试的数据结构也是C++实现的😅

### 配置vscode

[一键配置文件](https://github.com/SDchao/AutoVScodeCEnvironment/releases)（方法：解压并打开exe文件并指向vscode中打开的c++文件夹内）

### C++对C语言的扩充

1. 变量的定义可以出现在程序中的任何行
2. 提供了标准输入输出流对象**cin**，**cout**
3. 用const定义常变量
4. 函数重载、函数模板、带默认值的函数
5. 引用类型
6. 单目作用域运算
7. string类型字符串
8. 使用new和delete代替malloc和free函数等

### Hello world

```c++
#include <iostream>
using namespace std; //使用名称空间std

int main()
{
    cout << "Hello world" << endl;
    // <<符号把字符串发送给cout打印
    return 0;
}
```

### Start

#### 变量

变量是一块内存空间

变量名规则与C几乎一样

变量命名规范：在之前的语言学习中并没有注意到变量名命名规范的重要性。所以在此总结一下

1. 尽量不使用缩写

2. 本地变量名一律小写单词以下划线连接

   ```c++
   int use_imput_size;
   int error_count;
   class Student{}  //都是好的命名
   ```

3. 预处理指令：一般指#defined这样的命名定义

   ```c++
   #defined _DEFINED_STUDENT_CLASS_//或者
   #defined PIE_VALUE 3.14159
   ```

4. 函数：函数名以大小写字母开头每个单词的首字母大写

   ```c++
   class Block{
   public:
       ...
           CalculatorMinWidth(){} //正确写法
       ...
   }
   ```

   对于存取函数（get/set）而言建议和成员变量名称保持一致。例如

   ```c++
   class Block{
   public:
       ...
           int get_width() const {return width;}
           int set_width(int width){this.width = width;}
       ...
   private:
       int width;
       int height;
   }
   ```

5. 命名空间：名称全小写，基于项目名称和目录结构如：

   ```c++
   namespace linziyang_demo_space{
       
   }
   ```

6. 类：每个单词以大写字母开头，不包含下划线

   ```c++
   class DatabaseMetaData{}
   ```

   

#### 数据类型

比C更方便的就是string字符串，其他与C一样

size_t类型   、   枚举类型    、自定义类型、指针类型、空类型

枚举型

```c++
enum days{one, two, three}day; // 默认 one，two，three以0，1，2
    day = one;
    switch(day){
        case 0:
            cout << "one" << endl;
            break;
        case 1:
            cout << "two" << endl;
            break;
        default:
            cout << "three" << endl;
            break;
    }
    return 0;
```



#### 控制cout显示精度(double)

```c++
#include <iostream>
#include <cmath>
#include <iomanip> //控制符

using namespace std;

int main()
{
    //控制cout显示精度
    double doubleNum = 100.0 / 3.0;
    //1.强制以小数的方式显示
    cout <<fixed;
    //2.控制显示的精度
    cout <<setprecision(2);
    cout << doubleNum<<endl;
    return 0;
}
// 全局设置 cout << fixed << setprecision(2);
```

#### setfill( )与setw( )

```c++
#include <iostream>
#include <iomanip> //控制符
using namespace std;
int main()
{
    double attack1 = 287;
    double attack2 = 836;
    double attack3 = 234;
    cout << left;  // 左对齐
    cout << setfill('*');  //填充_
    cout << setw(8)<< attack1 <<endl 
         << setw(8)<< attack2 <<"\n"
         << setw(8)<< attack3 <<endl;
}
```



### 表达式，条件结构

```c++
    cout << boolalpha; // 打印真假 true false 不加则显示1 0
    cout << "15 > 88 么?\t" << (15>88) << endl;
    cout << "12 < 33 么?\t" << (12<33) << endl;
```

#### 位(bit运算符

| 运算符 |   作用   |                  实例                  |
| :----: | :------: | :------------------------------------: |
|   &    |  按位与  |        两个操作数同时位1结果为1        |
|   \|   |  按位或  |   两个操作数只要有一个为1，结果就为1   |
|   ~    |  按位非  | 操作数为1，结果为0；操作数为0，结果为1 |
|   ^    | 按位异或 | 两个操作数相同，结果为0；不相同结果为1 |
|   <<   |   左移   |              右侧空位补0               |
|   >>   |   右移   |            左侧空位补符号位            |

#### sizeof**运算符**

获得数据类型占用内存空间的大小，结果以字节为单位

```c++
//sizeof(type_name)
//char   	  占1个字节
//short  	  占2个
//int         占4个
//long        占4个
//long long	  占8个
//float       占4个
//double      占8个
//long double 占12个
string类型会+1
```

#### 随机数rand()

time 函数返回从 1970 年 1 月 1 日午夜开始到现在逝去的秒数，因此每次运行程序时，它都将提供不同的种子值。下面程序演示了 time 函数的用法。请注意，在调用它时必须给它传递一个参数 0。同时程序中包含一个新的头文件 ctime，此头文件是使用 time 函数所必需的。

```c++
#include <iostream>
#include <cstdlib> // Header file needed to use srand and rand
#include <ctime> // Header file needed to use time
using namespace std;

int main()
{
    // srand(unsigned(time(NULL))); 简便写法
    unsigned seed;  // Random generator seed
    // Use the time function to get a "seed” value for srand
    seed = time(0);
    srand(seed);
    // Now generate and print three random numbers
    cout << rand() << " " ;
    cout << rand() << " " ;
    cout << rand() << endl;
    return 0;
}
```

限制随机数的范围

```c++
number = rand() % max + 1;
```

例如，要生成 1〜6 的随机数来代表骰子的点数，则可以使用以下语句：

```c++
dice = rand() % 6 + 1;
```

任意范围内的随机数，其通用公式如下：

```c++
number = (rand()%(maxValue - minValue +1)) + minValue;
```

在上述公式中，minValue 是范围内的最小值，而 maxValue 则是范围内的最大值。例如，要获得 10〜18 的随机数，可以使用以下代码给变量 number 赋值：

```c++
const int MIN_VALUE = 10;
const int MAX_VALUE = 18;
number = rand() % (MAX_VALUE - MIN_VALUE + 1) + MIN_VALUE;
```

在上述代码中，（MAX_VALUE - MIN_VALUE + 1）的值为 9，这是目标范围内整数的个数。余数运算符（％）返回的值是 0〜8 的数字，再用它加上 MIN_VALUE（也就是 10），即可获得 10〜18 的随机数。

实例：

```c++
int num=rand()%(n-m+1)+m;

// 其中的rand()%(n-m+1)+m算是一个公式，记录一下方便以后查阅。

// 比如产生10~30的随机整数：

srand(time(0));

int a = rand() % (21)+10
```

#### 无限循环

```c++
while(true)
for( ; ; )
```

```c++
char answer = 'n';
do{
    //循环体
    cout << "是否继续进行(y/n)" << endl;
    cin >> answer;
}while(answer == 'y'|| answer == 'Y')
```



### 数组、指针

#### 数组

