---
typora-copy-images-to: upload
---

# JAVA笔记-day10——尚硅谷系列

[TOC]

## JAVA中的运算符

- **算术运算符**

  ![image-20211125095329628](https://tva1.sinaimg.cn/large/008i3skNly1gwr5s657y6j31080gomzc.jpg)

- **赋值运算符**
  ![image-20211125101014662](https://tva1.sinaimg.cn/large/008i3skNly1gwr69ltcq3j31280cm757.jpg)

- **比较运算符（关系运算符）**
  ![image-20211125101429072](https://tva1.sinaimg.cn/large/008i3skNly1gwr6dxiw4hj312s0j0q5h.jpg)

- **逻辑运算符**
  ![image-20211125102327305](https://tva1.sinaimg.cn/large/008i3skNly1gwr6ncthtyj310c0gwq4z.jpg)

  - &：当有一个不满足条件时，继续往下检测条件，结果为false
  - &&：只要一个不满足条件，不再检测，结果为false

- **==位运算符==**
  ![image-20211125102958519](https://tva1.sinaimg.cn/large/008i3skNly1gwr6u1q5zmj30z20hcjtc.jpg)

  - 位运算符在计算x的幂的时候可以大幅度加快计算速度和减少计算资源。

- **三元运算符**

  ![image-20211125110204571](https://tva1.sinaimg.cn/large/008i3skNly1gwr7rftpxsj30q60hq75x.jpg)

  - 三元运算符可以嵌套使用

  - 所有三元运算符都可以改写成if-else，当if-else不一定能改写成三元运算符

    

- **运算符的优先级**

  ![image-20211125113353029](https://tva1.sinaimg.cn/large/008i3skNly1gwr8om6vyuj313k0kgn04.jpg)



## 程序流程控制

- **流程控制语句是用来控制程序中各语句执行顺序的语句，可以把语句组合成能完成一定功能的小逻辑模块**



- **三种基本流程结构：**
  - 顺序结构
  - 分支结构
  - 循环结构
- ![image-20211125145757500](https://tva1.sinaimg.cn/large/008i3skNly1gwrekuqkqsj30wy0fk0um.jpg)



- **if-else结构：**
  ![image-20211125145933110](https://tva1.sinaimg.cn/large/008i3skNly1gwremi51h8j30vw0h0jsq.jpg)

  

  ![image-20211125150141038](https://tva1.sinaimg.cn/large/008i3skNly1gwreoq7lmkj30y60g40u8.jpg)

## 从键盘获取输入

- **具体实现步骤：**
  1. 导包：import	java.util.Scanner;
  2. Scanner的实例化：Scanner scan = new Scanner(System.in); 
  3. 调用Scanner类的相关方法，来获取指定类型的变量

```java
import java.util.Scanner;
public class ScannerTest{
  public static void main(String[] args){
    Scanner scan = new Scanner(System.in);
    int num = scan.nextInt();
    System.out.println(num);
  }
}
```



- **注意：**对于char型的数据获取，Scanner没有提供相关的方法，只能获取一个字符串。



