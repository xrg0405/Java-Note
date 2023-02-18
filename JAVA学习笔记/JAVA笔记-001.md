---
typora-copy-images-to: upload
---

# JAVA笔记-001

[TOC]

## java中label的用法

用法有点相当于C中的goto语句

```java
label: for(int i=1; i<=4; i++){
          for(int j=1; j<=10; j++){
            if(j%4 == 0){
              continue label;
            }
            System.out.print(j);
          }
          System.out.println();
}
```

上述代码先执行内层循环，当 j%4 == 0时，continue label，终止内层循环，跳到上一层循环，上一层循环开始执行。具体结果为：

```
123123123123
```

执行结果与如下代码不一样：

```java
for(int i=1; i<=4; i++){
  for(int j=1; j<=10; j++){
    if(j%4 == 0){
      continue;
    }
    System.out.print(j);
  }
  System.out.println();
}
```

上面的这个代码只是在 j%4 == 0时，打断一次循环，具体结果为

```
123567910
123567910
123567910
123567910
```



## 衡量一个功能代码的优劣

1. 代码的正确性
2. 代码的可读性
3. 代码的健壮性
4. 高效率与低存储：时间复杂度和空间复杂度（衡量算法好坏的主要标准）



## java中的数组

- 数组（Array）是多个相同类型数据按一定顺序排列的集合，并使用一个名字命名，并通过编号的方式对这些数据进行统一管理。
- 数组的常见概念：
  1. 数组名
  2. 下标（索引）
  3. 元素
  4. 数组的长度

定义数组与初始化：

```java
int[] ids = new int[]{1,2,3,4,5}; //第一种初始化方法
String[] names = new String[5]; //第二种初始化方法
int[] isd = new int[5];
```

- 数组本身是==引用数据类型==，而数组中的元素可以是任何数据类型，包括基本数据类型和引用数据类型。
- 创建数据对象会在内存中开辟一整块连续的空间，而数组名中引用的是这块连续空间的首地址。
- 数组的长度一旦确定，就不能再进行修改。
- `我们可以直接通过下标的方式调用指定位置的元素，速度很快`
- 数组的分类：
  - 按照维度：一维、二维等数组
  - 按照元素的数据类型：基本数据类型元素的数组、引用数据类型的数组（即对象数组）



数组元素的默认初始化：

1. 数组元素是整型：0
2. 数组元素是浮点型：0.0
3. 数组元素是char型：0或“\u0000“，打印是一个空格
4. 数组元素是boolean型：false
5. 数组元素是引用数据类型：null



**java中的内存结构：**

- 堆（heap）：用于存放new出来的结构，如对象、数组
- 栈（stack）：用于存放局部变量
- 方法区（method area）：内分为常量池和静态域



```java
public static void main(String[] args){
  Scanner scanner = new Scanner(System.in);
  System.out.println("Please inter the number of student:");
  int number = scanner.nextInt();
  
  int[] scores = new int[number];
  System.out.println("Please inter" + number + "student's score:");
  for(int i=0; i<scores.length; i++){
    scores[i] = scanner.nextInt();
  }
  
  int maxScore = 0;
  for(int i=0; i<scores.length; i++){
    if(maxScore < scores[i])
      maxScore = scores[i];
  }
  
  cahr level;
  for(int i=0; i<scores.length; i++){
    if(maxScore-scores[i] <= 10)
      level = 'A';
    else if(maxScore-scores[i] <=20)
      level = 'B';
    else if(maxScore-scores[i] <= 30)
      level = 'C';
    else
      level = 'D'
  }
  System.out.println("Student " + i +
                    "score is "+ scores[i] + 
                    ", grade is " + level);
}
```



**数据结构：**

1. 数据与数据之间的逻辑关系：集合、一对一、一对多、多对多
2. 数据的存储结构：
   - 线性表：顺序表（比如：数组），链表、栈、队列
   -  树形结构：二叉树
   - 图形结构：有向图和无向图

**算法：**

1. 排序算法
2. 检索算法





















