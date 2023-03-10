# JAVA笔记——day 1

[TOC]



## 前言01:JAVA用途

**java的用途广泛，可用于开发：**

银行系统、支付系统、政企信息系统、大数据平台、网站后台、SaaS云、手机APP、云管理系统后台、电商系统后台、桌面工具等 





## 前言02:JAVA与PYTHON的抉择

**JAVA：** 

java更基础，Java 程序中的封装概念、接口概念很重要，这是Java这门语言的核心。Java更适合用于开发项目，在软件领域会有这更大的应用



**python：** 

python的语法更接近英语，比较简单。主要用于机器学习和日常一些小应用，国内很少大企业是完全使用python进行开发工作的。会使用python，会在工作上锦上添花。



## 前言03:走进java

**C语言：** 主要用于比较底层应用的构建-------〉内存管理、进程管理、指针类的东西



**java学习路线：**

（早上九点到晚上6点）

1.  java的基础	（18～20天）

   1. 计算机基础

   2. 博客的重要性

   3. Java基础语法

   4. 流程控制和方法

   5. 数组

   6. 面向对象

      - 实例

      - 继承
      - 多态
      - 抽象类
      - 接口

   7. 异常

   8. 常用类

   9. 集合框架

   10. IO

   11. 多线程

   12. GUI（可选）

   13. 网络编程

   14. 注解和反射

   15. JUC编程

   16. JVM探究

   17. 【扩展】23种设计模式

   18. 【扩展】XML

   19. 【扩展】数据结构和算法

   20. 【扩展】正则表达式

2. 数据库	（4天）
   - MySQL
   - JDBC
   - UM类图
   - 数据库设计 

3. 前端知识（7天）

4. java Web（7天）

5. SSM框架（9天）
   - GIt
   - MyBatis
   - Spring
   - SpringMVC

6. Linux（7天）
   (主要用于服务器)
   - Linux基础
   - Redis
   - Nginx
   - Docker

7. SpringBoot（8天）
   - SpringBoot基础
   - SpringBoot配置及其原理
   - 持久层操作
   - Web开发
   - 缓存
   - 消息
   - 检索
   - 任务
   - 安全
   - Dubbo+Zookeeper分布式开发

8. SpringCloud（7天）
   - 微服务及微服务架构
   - SpringCloud
   - Eureka微服务注册与发现
   - Feign、Ribbon负载均衡
   - Hystrix熔断机制
   - Zuul路由网关
   - SprinCloud Config配置中心

9. Hadoop（8天）
   - 大数据时代
     - 概念
     - 特点
     - 应用
     - 前景
     - 技术发展
   - Hadoop简介
   - Hadoop环境搭建
   - HDFS
   - MapReduce
   - Yarn
   - Hive
   - Hbase



## 前言04:如何更好更高效地学习java

1. 多写代码、多记笔记、多写文章
2. 多交流、多思考、多练技能
3. 多分享知识、多提问为什么、多思考为什么
4. 最重要的是坚持



## 预科01:博客的重要性

1. 需要总结和思考
2. 提升文笔组织能力
3. 提升学习总结能力------>反思总结所学知识
4. 提升逻辑思维能力
5. 帮助他人、结交朋友
6. 练习坚持能力



## 预科02:MarkDown语法

### 知识补充

1. 可以插入网络图片，只要把图片的网址出入到小括号里面即可。这个非常好用，不用把图片保存到本地。
2. 插入超链接-------->[文字描述]（指定网址）

### 列表

1. 减号+空格  
   - xxxxxxx

### 表格

右键插入

### 代码

三个～那里的小点+代码语言( 英文格式 )

```python
hello python
```



## 预科03:什么是计算机

- 能够按照程序运行、自动高速处理海量数据的现代化智能电子设备

- 广泛应用在科学计算、数据处理、自动控制、计算机辅助设计、人工智能、网络等领域

### 计算机硬件

- 一些物理装置按照系统结构的要求构成一个有机整体为计算机软件运行提供物质基础
- 计算机主要硬件组成
  1. CPU
  2. 主板
  3. 内存
  4. 硬盘
  5. 显卡
  6. IO设备
- 冯诺伊曼体系
  ![image-20211020183909794](https://tva1.sinaimg.cn/large/008i3skNgy1gvplf24npwj617o0natbg02.jpg)

### 计算机软件

- 计算机软件可以使得计算机按照事先预定好的程序完成特定的功能
- 计算机软件按照其功能划分为系统软件和应用软件
  系统软件：操作系统
  应用软件：第三方软件，如Matlab
- 人机交互（图形化界面、命令行）

### 电脑常用快捷键

该部分内容可自行百度，一般都能搜到相应系统的快捷键列表

### Windows和其他系统的常用Dos命令

1. 打开CMD，win+R
2. cd 切换目录
3. ls 查看当前目录下的所有文件
4. cd .. 返回上级目录
5. cls 清除屏幕
6. ipconfig 查看电脑IP
7. ping 测试指定网络地址连通性



## 预科04:计算机语言的发展史

- 计算机的基本方式都是基于二进制的方式
- 汇编语言
  1. 解决人类无法读懂机器语言的问题
  2. 指令代替二进制
  3. 目前应用
     - 逆向工程
     - 机器人底层代码编写
     - 计算机病毒开发
- 高级语言
  1. 大体上分为面向过程和面向对象两大类
     C语言是典型的面向过程的语言、C++、java是典型的面向对象的语言
  2. 现在比较热门的语言
     java、python、goland



## 入门01:JAVA历史和介绍

- C语言

  1. 贴近硬件、运行极快、效率高
  2. 常用于操作系统、编译器、数据库、网络系统的开发
  3. 指针和内存管理

- java的历史略，自行百度

- java特性和优势

  1. 简单性---->没有指针、内存管理
  2. 面向对象
  3. 可移植性----->通过JVM虚拟机，同一个程序可以在不同的平台运行
  4. 高性能
  5. 分布式
  6. 动态性
  7. 多线程----->更好的交互（比如同时看视频做笔记）
  8. 安全性
  9. 健壮性

- java三大版本

  1.  javaEE：标准版（桌面程序、控制台开发）
  2. javaME：嵌入式开发（手机、小家电）
  3. javaEE：E企业级开发（web端、服务器开发等）

- JDK、JRE、JVM

  1. jdk：java开发工具
  2. jre：java运行环境
  3. jvm：java虚拟机

  ![image-20211020192640771](https://tva1.sinaimg.cn/large/008i3skNgy1gvplfwmz93j610q0eowh102.jpg)



## 入门02:java文件目录介绍

- bin ：用于存放可执行文件.exe
- include：存放其他语言的一些头文件
- jre：Java运行环境文件
- lib：存放java的类库文件
- src压缩包：资源文件、存放很多java自带的类的源代码



## 入门03:java程序运行机制

- 编译型语言---->直接将所有的东西转译好，存成一个文件
- 解释型语言---->边运行边转译，不保存成文件

Java兼具以上两种特性

- java程序运行机制

  ![image-20211020194551563](https://tva1.sinaimg.cn/large/008i3skNgy1gvplfy6jjpj60sq0but9c02.jpg)

