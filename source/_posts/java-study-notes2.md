---
title: Java学习笔记(2)-标识符与关键字
date: 2018-02-19 20:12:48
banner: https://images.gxuann.cn/banner/java-study-notes.png
tags:
  - Java
---

## 标识符
### 标识符的命名规则
- 标识符可以由字母、数字、下划线(\_)和美元符($)组成，不能以数字开头
- 标识符严格区分大小写
- 标识符不能使Java关键字和保留字
- 标识符的命名最好能反映出其作用


## 关键字
abstract | boolean | break | byte | case | catch
:-:|:-:|:-:|:-:|:-:|:-:
char|class|continue|default|do|double
else|extends|false|final|finally|float
for|if|implements|import|native|int
interface|long|instanceof|new|null|package
private|protected|public|return|short|static
super|switch|synchronized|this|throw|throws
transient|true|try|void|volatile|while

---

# 变量的概念与数据类型
## 变量
- 变量的三个元素：变量类型、变量名和变量值

### 变量的命名规则
- 满足标识符命名规则
- 符合**驼峰法**命名规则
- 尽量简单，做到见名知意
- 变量名的长度没有限制

### 类的命名规则
- 满足**Pascal**命名规范(首字母总要大小)

## 数据类型
![](https://images.gxuann.cn/archives/java-study-notes2-datatype.png)
- 引用数据类型：
    1. 类(class)
    2. 接口(interface)
    3. 数组
- 基本数据类型：
    1. 数值型
        1. 整数类型(byte、short、int、long)
        2. 浮点类型(float、double)
    2. 字符型(char)
    3. 布尔型(boolean)

## 基本数据类型
数据类型|说明|字节
:-:|:-:|:-:
byte|字节型|1
short|短整型|2
int|整型|4
long|长整型|8
float|单精度浮点型|4
double|双精度浮点型|8
char|字符型|2
boolean|布尔型|1

---

# 数据类型的字面值及变量定义
## 整型字面值及变量声明
- Java中有三种表示整数的方法：十进制、八进制、十六进制

#### 进制表示
- 八进制：以0开头，包括0-7的数字
- 十六进制：以0x或0X开头，包括0-9的数字以及字母A-F

## 变量声明
- 格式：`数据类型 变量名；`
    * 例： `int n; //声明整型变量n`
    * `long count; //声明长整型变量count`

## 赋值
- 使用`=`运算符进行赋值
- `=`叫做赋值运算符，将运算符右边的值赋给左边的变量
    * 例： `n=3; //将3赋值给n`
- 可以再定义变量的同事给变量赋值，即变量的初始化

## 浮点型字面值
- 浮点型字面值**默认情况**下表示**double类型**，也可以在值后加d或D
    * 例：123.43d或123.43D
- 如表示float类型，则需要在字面之后加f或者F

## 基本数据类型变量的存储
- 数据类型分为基本数据类型和引用数据类型
- 引用数据类型包括数组和类等
- 类定义的变量又叫做对象

#### 按照作用范围分为：<br>
- 类级
- 对象实例级
- 方法级 --->局部变量
- 块级

## 存储
![](https://images.gxuann.cn/archives/java-study-notes2-ram.png)
- 局部变量是存储在`栈`中
    * 如`int`，在定义之后会在，栈中划分一个`int`大小(4字节)的空间给`int`的变量
    * ![](https://images.gxuann.cn/archives/java-study-notes2-ram2.png)

## 字符型字面值
- 字符型字面值用单引号内的单个字符表示
    * 例： 'a' 'b' '$'
- 定义字符型变量，和整型和浮点型相同
    * 例 `char a = 'a'`

## Unicode编码
- Unicode编码又称为统一码、万国码
- 几乎上是支持所有字符集
- Unicode表示法，在值前加前缀`\u`
  ## 布尔类型字面值
- 布尔值只能定义为`true`和`false`
- 定义：`boolean b = true;`
  ## 字符串字面值
**字符串不属于基本数据类型，它属于类**
- 双引号引起来的0个或多个字符
- 定义：`String s = "String";`

## 转义字符
转义字符|描述
:-:|:-:
\uxxx|四位16进制数所表示的字符
\'|单引号字符
\"|双引号字符
'\\'|反斜杠字符
\r|回车
\n|换行
\t|横向跳格
\b|退格

##  类型转换
- 分为自动类型转换和强制类型转换

#### 自动类型转换顺序
![](https://images.gxuann.cn/archives/java-study-notes2-typeconversion.png)

#### 强制类型转换
- 如果A类型的数据表示范围比B类型大，则将A类型的值赋值给B类型，则需要强制类型转换
```java
double d = 123.4;
float f = (float)d;
```
  ## 常量
- 使用关键字`final`来定义常量
- 命名规则：一般使用大写字母来定义
    * `final double PI = 3.14;`
    * `final double MIN_VALUE = 0;`

## 基本数据类型范围
类型|位|字节|最小范围|最大范围
:-:|:-:|:-:|:-:|:-:
byte|8|1|-2^7|2^7
short|16|2|-2^15|2^15
int|32|4|-2^31|2^31
long|64|8|-2^63|2^63
float|32|4|1.4E-45|3.4028235E38
double|64|8|4.9E-324|1.7976931348623157E308
