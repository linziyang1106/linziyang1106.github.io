---
title: C++语言入门
date: 2019-9-29 17:16:36
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

```c++
//数组查找
#include <iostream>
using namespace std;
int main()
{
    int nums[] = {8,4,2,1,23,344,12};
    int numslen = sizeof(nums) / sizeof(int); //数组长度
    int searchNum;        //用户要查找的数字
    int searchIndex = -1; //用户查找数字的下标
    cout <<"请输入要查找的数字";
    cin >> searchNum;
    for(int i = 0; i<numslen; i++)
    {
        if(nums[i] == searchNum)
        {
            searchIndex = i;
            break;
        }
    }
   
    cout <<"下标为"<<searchIndex;
}
```

```c++
//数组奇数偶数
#include <iostream>
using namespace std;
int main()
{
    int nums[] = {8,4,2,1,23,344,12};
    int numslen = sizeof(nums) / sizeof(int);
    int Jcount = 0, Ocount = 0;
    for(int i = 0; i < numslen; i++)
    {
        if(nums[i] % 2 == 0)
        {
            Ocount++;
        }
        else
        {
            Jcount++;
        }
        
    }
    cout <<"奇数个数是"<< Jcount <<"偶数个数是"<< Ocount << endl;

}
```

```c++
 //动态地从键盘录入信息并赋值
#include <iostream>
using namespace std;
int main()
{
    const int N = 5;
    double scores[N];
    for(int i = 0; i < N; i++)
    {
        cout <<"请输入第"<< (i+1) <<"门课的成绩：";
        cin >> scores[i];
    }
    for(int i = 0; i < N; i++)
    {
        cout <<"第"<< (i+1) <<"门课的成绩："<<scores[i]<<endl;
    }

}
```

#### 冒泡排序(升序)

```c++
for (int j = 0; j < a.length - 1; j++) {
            for (int i = 0; i < a.length - 1 - j; i++) {
                if (a[i] > a[i + 1]) {
                    // change
                    temp = a[i + 1];
                    a[i + 1] = a[i];
                    a[i] = temp;
                }
            }
}
```

#### 选择排序(升序)

```c++
for (int j = 0; j <length- 1;j++) {
            for (int i = j; i < length- 1; i++) {
                if (a[j] > a[i + 1]) {
                    // change
                    temp = a[j];
                    a[j] = a[i + 1];
                    a[i + 1] = temp;
                }
            }
}
```

#### 数组的删除和插入



#### 二维数组

```c++
//
// Created by Administrator on 2019-10-12.
//
#include <iostream>
using namespace std;
int main()
{
    string stuName[] = {"林子洋","马云","lin"};
    string courseName[] = {"语文","数学","英语"};
    const int ROW = 3;
    const int COL = 3;

    double score[ROW][COL];

    for(int i = 0; i < ROW; i++) // 外层循环控制学生
    {
        for(int j = 0; j < COL; j++) //内层循环控制课程
        {
            cout << stuName[i] <<"的"<<courseName[j]<<"成绩"<<endl;
            cin >> score[i][j];
        }
    }
    //打印结果
    cout <<"\t";
    for(int i = 0; i < COL; i++)
    {
        cout << courseName[i]<<"\t";
    }
    cout << endl;
    for(int i = 0; i < ROW; i++)
    {
        cout << stuName[i] <<"\t";
        for(int j = 0;j <COL; j++)
            {cout << score[i][j] <<"\t";}
        cout << endl;
    }
    
    system("pause");
}

```

#### 指针

```c++
// * 读地址   &取地址
// 空指针：不指向任何对象，在
int *ptr1 = nullptr; //等价于int *ptr1 = 0;
int *ptr2 = 0;       //直接将ptr2初始化为字面常量0
```

void *指针

```c++
    double num = 3.14;
    double *ptr_num1 = &num;
    void *ptr_num2 = &num;
    cout << boolalpha; // 打印bool类型
    cout << (ptr_num1 == ptr_num2) <<endl;
```

void *指针存放一个内存地址，地址指向的内容是什么类型不能确定。

一般用来拿来和别的指针比较、作为函数的输入和输出；赋值给另一个void *指针

#### 引用

```c++
int int_value = 1024;
//refValue指向int_value,是int_value的另一个名字
int& refValue = int_value;
//错误:引用必须被初始化
int& refValue2;
```

1. 引用并非对象，只是为一个已经存在的对象起的别名

2. 引用只能绑定在对象上，不能与字面值或某个表达式的计算结果绑定在一起。

   ```c++
   int &ref_value = 10;//错误
   ```

3. 引用必须初始化，所以使用引用之前不需要测试其有效性，因此使用引用可能会比使用指针效率高。

引用和指针的关系

> 引用对指针进行了简单封装，底层仍然是指针
>
> 获取引用地址时，编译器会进行内部转换

```c++
int num = 108;
int& rel_num = num;
rel_num = 118;
cout << &num <<"\t"<< &rel_num<< endl;
```

相当于

```c++
int num = 108;
int* rel_num = &num;
*rel_num = 118;
cout << &num << "\t" << rel_num << endl;
```

#### 使用引用参数

```c++
#include <iostream>
using namespace std;
void Swap1(int num1, int num2)
{
    int temp;
    temp = num1; num1 = num2; num2 = temp;
    cout << num1 << "\t" << num2 << endl;
}

void Swap2(int *p1, int *p2)
{
    int temp;
    temp = *p1; 
    *p1 = *p2; 
    *p2 = temp;
}

void Swap3(int &ref1,int &ref2)
{
    int temp;
    temp = ref1;
    ref1 = ref2;
    ref2 = temp;
}
int main()
{
    int num1 = 10, num2 = 5;
    Swap1(num1,num2);
    cout << "执行Swap1之后："<< num1 << "\t" << num2 << endl;
    Swap2(&num1, &num2);
    cout << "执行Swap2之后："<< num1 << "\t" << num2 << endl;
    Swap3(num1, num2);
    cout << "执行Swap3之后："<< num1 << "\t" << num2 << endl;
}
```

使用引用的理由

1. 可以更加简便地书写代码
2. 可以直接传递某个对象，而不只是把对象复制一份

#### 指针与数组

### 内联函数（inline）

是C++为提高程序运行速度所做的一项改进，与常规函数的区别不在于编写方式，**而在于被调用时的运行机制不同；编译器使用函数代码替换函数调用**，速度快，效率高

+ 常规函数是通过函数的地址来寻找运行
+ inline是直接把函数内容复制过来

使用建议：如果执行函数代码的时间比处理函数调用机制的时间长，则节省的时间只占整个过程的很小一部分；

> 如果**代码执行时间很短**，内联调用就可以节省大部分时间

### 函数重载

+ 指可以用多个同名的函数
+ 函数名相同，参数列表不同（特征标不同）

```c++
void eating(string food){
    //相当于 eating_string
}
void eating(int food){
    //相当于 eating_int
}
```

举例

```c++
//使用重载实现数组的排序
#include <iostream>
using namespace std;
//int inums[] = {56,54,12,89,43}
//float fnums[] = {78.0f, 5.7f, 42.8f, 99.1f}
//double dnums[] = {78.9, 23.6, 77.8, 98.5, 33.3}
void Sort(int[],int len);
void Sort(float[],int len);   //重载：函数名相同，参数名不同
void Sort(double[],int len);

void Sort(int nums[],int len)
{
    int temp;
    
    for(int i = 0; i < len - 1; i++)
    {
        for(int j = 0; j < len - i - 1; j++)
        {
            if(nums[j] > nums[j+1])
            {
                temp = nums[j];
                nums[j] = nums[j+1];
                nums[j+1] = temp;
            }
        }
    }
}
void Sort(float nums[],int len)
{
    int temp;
    for(int i = 0; i < len - 1; i++)
    {
        for(int j = 0; j < len - i - 1; j++)
        {
            if(nums[j] > nums[j+1])
            {
                temp = nums[j];
                nums[j] = nums[j+1];
                nums[j+1] = temp;
            }
        }
    }
}
void Sort(double nums[],int len)
{
    int temp;
    for(int i = 0; i < len - 1; i++)
    {
        for(int j = 0; j < len - i - 1; j++)
        {
            if(nums[j] > nums[j+1])
            {
                temp = nums[j];
                nums[j] = nums[j+1];
                nums[j+1] = temp;
            }
        }
    }
}
//输出排序前数组
void li(int nums[], int len)
{
    cout<< "排序前:";
    for(int i = 0; i < len; i++){
        cout << nums[i] << ", ";
    }
    cout << endl;
}
//输出排序后数组
void Show(int nums[], int len)
{
    cout<< "排序后:";
    for(int i = 0; i < len; i++){
        cout << nums[i] << ", ";
    }
    cout << endl;
}
int main()
{
    int inums[] = {56,54,12,89,43};
    float fnums[] = {78.0f, 5.7f, 42.8f, 99.1f};
    double dnums[] = {78.9, 23.6, 77.8, 98.5, 33.3};
    li(inums,sizeof(inums) / sizeof(int));
    Sort(inums,sizeof(inums) / sizeof(int));
    Show(inums,sizeof(inums) / sizeof(int));
}
```

