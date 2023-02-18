---
typora-copy-images-to: upload
---

# JAVA笔记-day9——尚硅谷系列

[TOC]

## JAVA语言概述

### java学习时间表

- 学习方向

  - 软件开发
  - 大数据开发

  

==软件开发方向时间安排：==

- **JavaSE**

  <img src="https://tva1.sinaimg.cn/large/008i3skNly1gwj36f0ybej30xa04cmxq.jpg" alt="image-20211118101856344" style="zoom:67%;" />

- **JavaWeb**

  <img src="https://tva1.sinaimg.cn/large/008i3skNly1gwj36xn7awj30xa0d4go3.jpg" alt="image-20211118101928462" style="zoom:67%;" />

- **JavaEE框架**
  <img src="https://tva1.sinaimg.cn/large/008i3skNly1gwj37yj4a8j30xc06ydhe.jpg" alt="image-20211118102027931" style="zoom:67%;" />



- **JavaEE高级**
  <img src="https://tva1.sinaimg.cn/large/008i3skNly1gwj3b5vl4oj30xc0egn0b.jpg" alt="image-20211118102332591" style="zoom:67%;" />



### Java主要应用场景

**Java基础是JavaEE、大数据、Android开发的基石**



### 软件开发介绍

- 软件概念
  软件，即一系列按照特定顺序组织的计算机数据和指令的集合。有系统软件和应用软件之分



- 人机交互方式
  - 图形化界面（GUI）
  - 命令行方式（CLI）



### 常用命令行指令（Windows）

- **常用的DOS命令**
  - **dir：**列出当前目录下的文件以及文件夹
  - **md：**创建目录
  - **rd：**删除目录
  - **cd：**进入指定目录
  - **cd..：**退回到上一级目录
  - **cd \：**退回到根目录
  - **del：**删除文件
  - **exit：**退出dos命令行



- **常用快捷键**
  - 上下查看历史命令，左右移动光标
  - Delete和Backspace删除字符



### 计算机编程语言介绍

- **第一代语言：**
  - 机器语言。指令以二进制代码形式存在。
- **第二代语言**
  - 汇编语言。使用助记符表示一条机器指令。
    <img src="https://tva1.sinaimg.cn/large/008i3skNly1gwj508zcrej30sk048glt.jpg" alt="image-20211118112215135" style="zoom:67%;" />
- **第三代语言：高级语言**
  - 面向过程：C、Pascal等
  - 面向对象：Java，C++



### JDK、JRE与JVM

- **jdk：**java开发工具包

  jdk中已经包含了jre

  

- **jre：**java运行坏境
  jre中包含了jvm虚拟机和标准类库



- 三者关系图
  <img src="https://tva1.sinaimg.cn/large/008i3skNly1gwjbmimhkhj30vy0eagmb.jpg" alt="image-20211118151115035" style="zoom:50%;" />



### 什么是环境变量

相当于全局化某个文件夹，使得该文件夹中的东西在任何目录下都可以使用。

**path：**Windows系统执行命令时要搜索的路径



- 开发中常用的配置环境变量的的方式

  <img src="https://tva1.sinaimg.cn/large/008i3skNly1gwjbz3eqr3j30x60c475c.jpg" alt="image-20211118152319904" style="zoom: 50%;" />



### java编译方式

- 编写.java文件
- 通过javac.exe编译成.class文件
- .class文件通过java.exe运行，得出结果

<img src="https://tva1.sinaimg.cn/large/008i3skNly1gwjcaivk1uj30v406qdg9.jpg" alt="image-20211118153418966" style="zoom:50%;" />



### java注释

- **java中的注释类型：**

  - 单行注释
  - 多行注释

  <img src="https://tva1.sinaimg.cn/large/008i3skNly1gwjcsxykubj30wi098q3v.jpg" alt="image-20211118155201093" style="zoom: 50%;" />

  - 文档注释（java特有）

  <img src="https://tva1.sinaimg.cn/large/008i3skNly1gwjcy2v0ppj30tm0d0ta9.jpg" alt="image-20211118155657404" style="zoom:50%;" />



- **注释的作用：**
  - 提高了代码的阅读性；是调试程序的重要方法
  - 注释是一个程序员必须要具备的良好编程习惯
  - 将自己的思路通过注释先整理出来，再用代码去实现



- **多行注释是不能嵌套使用的**



### java API文档

<img src="https://tva1.sinaimg.cn/large/008i3skNly1gwjd5uf4woj30w80cagn8.jpg" alt="image-20211118160425340" style="zoom:50%;" />



### 良好的编程风格

- **正确的注释和注释风格**

  - 使用文档注释来注释整个类或整个方法
  - 如果注释方法中的某一个步骤，使用单行或多行注释

- **正确的缩进和空白**

  - 使用一次tab操作，实现缩进
  - 云算法两边习惯性各加一个空格。

- **块的风格**

  - Java API源代码中的行尾风格

  <img src="https://tva1.sinaimg.cn/large/008i3skNly1gwjdzhpy67j30vo06ydgn.jpg" alt="image-20211118163255145" style="zoom:50%;" />







## JAVA基础语法

### 关键字和保留字

- **关键字：**

  - 定义：被java赋予了特殊含义，用作专门用途的字符串
  - 特点：关键字中所有的字母都为小写

  <img src="https://tva1.sinaimg.cn/large/008i3skNly1gwkpwddc7vj31280dqtaq.jpg" alt="image-20211119201036660" style="zoom:50%;" />

  <img src="https://tva1.sinaimg.cn/large/008i3skNly1gwkpx5qob7j312s0iytbw.jpg" alt="image-20211119201112704" style="zoom:50%;" />

- **保留字：**
  - 现有java版本尚未使用，但以后版本可能会作为关键字使用。自己命名标识符时要避免使用这些保留字（goto、const）



### 标识符以及命名规则

- **定义合法 标识符规则：**
  1. 由英文字母大小写，数字，_或$组成
  2. 数字不可以作为开头
  3. 不刻意使用关键字和保留字，但能包含关键字和保留字
  4. JAVA中严格区分大小写，长度无限制
  5. 标识符不能包含空格



- **命名规则：**

  <img src="https://tva1.sinaimg.cn/large/008i3skNly1gwkqc59xffj312e0f40v6.jpg" alt="image-20211119202547523" style="zoom:50%;" />



### 变量

- **变量的概念：**
  - 内存中的一个存储区域
  - 该区域的数据可以在同一个类型范围内不断变化
  - 变量是程序中最基本的存储单元，包含变量类型、变量名和存储的值
- **变量的作用：**
  - 用于在内存中保存数据



- **使用变量需要注意的事情：**
  1. ==java中每个变量必须先声明，后使用==
  2. 变量的作用域：其定义所在的一对中括号{}内
  3. 变量只有在其作用域内才有效
  4. 同一个作用域内，不能定义重名的变量

```java
/*
	变量的使用
*/
	public class VariableTest{
    public static void main(String[] args){
      int myAge = 12;
      System.out.println(myAge);
      
      int myNum = 10001;
      System.out.println(myNum); 
    }
  }
```



- **变量的类型：**
  对于每一种数据都定义了明确的具体数据类型（强类型语言），在内存中分配了不同大小的内存空间



<img src="https://tva1.sinaimg.cn/large/008i3skNly1gwkr6nvnq1j310y0by0tv.jpg" alt="image-20211119205502971" style="zoom:50%;" />

- **数据类型间的区别：**

  <img src="https://tva1.sinaimg.cn/large/008i3skNly1gwkrcgafkgj310a0iujuk.jpg" alt="image-20211119210041253" style="zoom:50%;" />

  

  <img src="https://tva1.sinaimg.cn/large/008i3skNly1gwkrhxwztuj310m0ioad9.jpg" alt="image-20211119210558528" style="zoom:50%;" />

  

  <img src="https://tva1.sinaimg.cn/large/008i3skNly1gwkrmyp4n9j311q0iwn03.jpg" alt="image-20211119211048806" style="zoom:50%;" />

   

### 乱码的情况和字符集说明

- **乱码出现的原因：**

  字符集不一致，导致字符翻译的时候出现错误。

  

- **关于ASCLL码：**

  自行百度！！！

  - 缺点：

    1. 不能表示所有字符
    2. 相同编码表示的字符不一样。

    

- **UTF-8:**

  <img src="https://tva1.sinaimg.cn/large/008i3skNly1gwkrwmgd5zj310u0gsq55.jpg" alt="image-20211119211957672" style="zoom:50%;" />



### 数据类型转换

- **自动类型提升**
  byte  ——》 short  ——》 int  ——》 long  ——》 float ——》double

  <img src="https://tva1.sinaimg.cn/large/008i3skNly1gwksyrimmbj31d005mt9x.jpg" alt="image-20211119215644639" style="zoom:50%;" />

  

- **强制类型转换**
  自动类型提升运算的逆运算
  1. 需要使用强转符：（）
  2. ==强制类型转换可能导致精度损失==



### String类型变量的使用

- String不是基本数据类型，属于引用数据类型
- 使用方式与基本数据类型一致。
- 一个字符串可以串接另一个字符串，也可以直接串接其它类型的数据



### 不同进制的表示方式

- **所有的数字在计算机中都是以二进制的形式存在**
- **对于整数，有四种表示方式：**
  - 二进制：以0b或0B开头
  - 十进制
  - 八进制：以数字0开头
  - 十六进制：以0x或0X开头

<img src="../../../Library/Application Support/typora-user-images/image-20211121122131691.png" alt="image-20211121122131691" style="zoom:50%;" />



### 二进制转化成十进制说明

- **二进制中，最高位作为符号位（0:正数；1:负数）**



- **Java整数常量默认是int类型，当用二进制定义整数时，其第32位是符号位；当是long类型时，二进制默认占64位，第64位是符号位**



- **二进制的整数有如下三种形式：**
  1. 原码：直接将一个数值换成二进制。最高位是符号位
  2. 负数的反码：是对原码按位取反，只是最高位（符号位）确定为1
  3. 负数的补码：其反码加1



- **计算机以二进制补码的形式保存所有整数。**
  - 正数的原码、反码、补码都相同
  - 负数的补码是其反码加1











