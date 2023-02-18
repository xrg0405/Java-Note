# JAVA笔记-day3

[TOC]



## java基础11:包机制

- ![image-20211022095810015](https://tva1.sinaimg.cn/large/008i3skNgy1gvplhaktugj61ae0lcdie02.jpg)

- 包的本质就是一个文件夹
- 一般利用公司域名的倒置作为域名
- 尽量不要使得包里面的类的名字相同，否则交叉引用的时候可能会报错



## java基础12:JavaDoc生成文档

- JavaDoc命令是用来生成自己的API文档的。
- 参数信息：
  1. @auther 作者名字
  2. @version 版本号
  3. @since 指明需要最早使用的JDK版本
  4. @param 参数名
  5. @return 返回值情况
  6. @throws 异常抛出情况
- 参数加入的位置：
  ![image-20211022100720413](https://tva1.sinaimg.cn/large/008i3skNgy1gvplhh956dj618o0kkq4902.jpg)

- 生成JavaDoc文档的方法：
  1. 通过命令行生成	javadoc  -encoding UTF-8 charset UTF-8 xxx.java
  2. 通过IDEA生成



## java流程控制01:用户交互Scanner

- 基本使用方法：

  ![image-20211022101423133](https://tva1.sinaimg.cn/large/008i3skNgy1gvplhjgps5j60ng038q2z02.jpg)

- 通过Scanner类的next()和nextLine()方法获取输入的字符串，在读取前我们一般需要使用hasNext()与hasNextLine()判断是否还有输入的数据。

- （<u>凡是IO流的类，使用完后都要关掉，即xxx.close()）</u>

- 注意事项：

  ![image-20211022102333950](https://tva1.sinaimg.cn/large/008i3skNgy1gvplhp65vnj61240fetap02.jpg)

- 使用举例：

  1. ![image-20211022102445462](https://tva1.sinaimg.cn/large/008i3skNgy1gvplhwp49wj60ui0cigmi02.jpg)
  2. ![image-20211022102519713](https://tva1.sinaimg.cn/large/008i3skNgy1gvpli1l6pvj61100ec75m02.jpg)



## java流程控制02:Scanner进阶使用

- scanner.hasNextxxx（xxx=数据类型），可以判断输入的数据类型
- 其他更精妙的方法可以自行百度。
- 在大项目的开发中，一般很少使用到scanner类，只有在学习Java初期会经常使用，通常用于解决有用户自定义输入的程序题。



## java流程控制03:顺序结构

- java的基本结构就是顺序结构，除非特别指明，否则就按照顺序一句一句地执行
- 顺序结构是最简单的算法结构
- 语句与语句之间是按从上到下的顺序执行的，它是由若干个依次执行的处理步骤组成，它是任何一个算法都离不开的一种基本算法结构。



## java流程控制04:if选择结构

- if单选择结构
  ![image-20211022104110507](https://tva1.sinaimg.cn/large/008i3skNgy1gvpli86keej61bu0j4wfs02.jpg)

  （<u>xxx.equals()，用于判断字符串是否相等，与“==”号有区别）</u>

- if双选择结构
  ![image-20211022104453275](https://tva1.sinaimg.cn/large/008i3skNgy1gvpli7f6bqj61bu0j4wfs02.jpg)

- if多选择结构
  ![image-20211022104652722](https://tva1.sinaimg.cn/large/008i3skNgy1gvpliadbd2j61bu0j4wfs02.jpg)

- 嵌套的if结构

  在一个if里嵌套一个if



## java流程控制05:Switch选择结构

- switch case语句判断一个变量与一系列值中的某个值是否相等，每个值称为一个分支。

  ![image-20211022140953725](https://tva1.sinaimg.cn/large/008i3skNgy1gvpliku7n8j61c80jqacl02.jpg)

- 写完case后必须写上break，防止case穿透现象

- 补充----反编译：java---->class（字节码文件）---->反编译（IDEA）

- 优秀程序员要学会看源码！！！



## java流程控制06:While循环详解

- ![image-20211022141833792](https://tva1.sinaimg.cn/large/008i3skNgy1gvpliljepgj61c80jqacl02.jpg)



## java流程控制07:DoWhile循环详解

- do.....while语句在不满足条件时，也会执行一次
- ![image-20211022142313407](https://tva1.sinaimg.cn/large/008i3skNgy1gvplis14nnj61bg0j60uv02.jpg)



## java流程控制08:For循环详解

- ![image-20211022142544235](/Users/kong/Library/Application Support/typora-user-images/image-20211022142544235.png)
- 关于for循环有以下几点那说明：
  1. 最先执行初始化步骤，可以声明一种类型，但可初始化一个或者多个循环控制变量，也可以是空语句。
  2. 布尔表达式也可以为空
  3. 迭代语句也可以为空