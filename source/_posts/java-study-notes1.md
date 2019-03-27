---
title: Java学习笔记(1)-初识
date: 2018-02-19 19:51:24
tags:
  - Java
---

>接下来的Java学习笔记系列，是我通过业余时间学习Java的一些内容后总结而成的。

## Java简介
### JVM
- JVM(Java Virtual Machine), Java虚拟机
- JVM是Java平台无关性实现的`关键`

#### Java程序执行流程
源文件(.Java)-->编译器(compiler)-->字节码文件(.class)-->解释器(interpreter)-->程序
`解释执行由 JVM 来执行`

### JDK
- JDK(Java Development Kit), Java语言的软件开发工具包
- 两个主要的组件：
    1. -javac -编译器，将源程序转换成字节码
    2. -java -运行编译后的java程序(.class)

### JRE
- JRE(Java Runtime Environment)
- 包括Java虚拟机(JVM)、Java核心类库和支持文件 - 如果只需要运行Java程序，安装JRE即可
- 如果需要开发Java软件，需安装JDK
- `JDK`是面向开发人员 `JRE`面向使用者
- JDK中附带有JRE

```
JRE=JVM+JavaSE标准类库
JDK=JRE+开发工具集
```

### Java平台
Java SE | Java EE | Java ME
:-: | :-: | :-:
桌面程序 | Web程序 | 移动设备*
Java标准版 | Java企业版 | Java微型版

---

## Java程序的结构
- class (类名) \*class是定义类的关键字
- public 公开
- static 静态修饰符
- void 返回空值
- main 主方法体
- String 字符串类
```java
class Hello{
    public static void main(String[] args){
        System.out.println("Hello World!");
    }
}

```
