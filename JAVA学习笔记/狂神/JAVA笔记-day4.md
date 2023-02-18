# JAVA笔记-day4

[TOC]

## java流程控制09:打印九九乘法表

```java
//打印九九乘法表
//For循环解法主要代码
for(int i=1; i<10; i++){
  for(int j=1; j<=i; j++){
    int temp = j*i;
    if(j < i) 
      System.out.print(j+"*"i+"="+temp+" ");
    else 
      System.out.print(j+"*"i+"="+temp);
  }
  Systm.out.println();
}

```



## java流程控制10:增强For循环

- 有点类似于python里的列表迭代其对象。

  ```java
  public class ForDemo05{
    public static void main(String[] args){
      //定义一个数组
      int[] numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9};
      
      //增强型For循环
      for(int number:numbers)
        System.out.println(number);
    }
  }
  ```

- 增强For循环主要用于迭代数组和集合



## java流程控制11:break、continue、goto的使用

- break用于强行退出循环，不执行循环中的语句
- continue语句用在循环语句体中，用于终止某次循环过程，即跳过循环体中尚未执行的语句（continue后的语句），接着进行下一次是否执行循环的判定。
- 关于goto关键字，一般很少用，如果需要使用，建议直接百度



## java流程控制12:打印三角形及Debug

```java
//打印三角形主要代码
int n = 5;
for(int i=1; i<=n; i++){
  for(int j=n; j>=i; j--)
    System.out.print(" ");
  for(int j=n; j<=i; j++)
    System.out.print("*");
  for(int j=n; j<i; j++)
    System.out.print("*");
  System.out.print()
}
```

- 使用IDEA deBug的方法：

  （参见百度）

## java方法01:什么是方法

- 什么是方法：
  java中的方法相当于C语言中的函数

  1. **java方法是语句的集合，他们在一起执行一个功能：**
     - 方法是解决一类问题的步骤的有序组合
     - 方法包含于类或对象中
     - 方法在程序中被创建，在其他地方被引用

- 设计方法的原则：

  方法的本质是功能块，就是实现某个功能的语句快的集合。我们设计方法的时候最好保持方法的原子性，==就是一个方法只完成1个功能，这样有利于后期拓展==

- 方法的命名规则：

  驼峰规则——如addWord()

- 方法举例：
  ![image-20211023155617575](https://tva1.sinaimg.cn/large/008i3skNgy1gvplizbh4hj610q0e2ab902.jpg)



## java方法02:方法的定义和调用

- ==方法包含一个方法头和一个方法体==，下面是一个方法的所有部分：
  ![image-20211023155939839](https://tva1.sinaimg.cn/large/008i3skNgy1gvplj2o9dmj61dw0ggn1b02.jpg)

- 方法中return的使用

  ![image-20211023160732914](https://tva1.sinaimg.cn/large/008i3skNgy1gvplj3q6pmj61dw0ggn1b02.jpg)

- **方法的调用：**

  ![image-20211023160838843](https://tva1.sinaimg.cn/large/008i3skNgy1gvplj4q98ij619w0m2taq02.jpg)

- **什么是值传递和引用传递**

  1. 值传递：
     值传递（pass by value）是指在调用函数时将实际参数复制一份传递到函数中，这样在函数中如果对参数进行修改，将不会影响到实际参数。 
  2. 引用传递：
     引用传递（pass by reference）是指在调用函数时将实际参数的地址直接传递到函数中，那么在函数中对参数所进行的修改，将影响到实际参数。

## java方法03:方法的重载

- **重载就是在一个类中，有相同的函数名称，但形参不同的函数**
- 方法的重载规则：
  1. **方法的名称必须相同**
  2. 参数列表必须不同（个数不同、或类型不同、参数排列循序不同等）
  3. 方法的返回类型可以相同，也可以不相同
  4. 仅仅返回值不同不足以成为方法的重载
- **实现理论**
  ==<u>方法名称相同时，编译器会根据调用方法的参数个数、参数类型等逐一匹配，以选择对应的方法，如果匹配失败，则编译器报错</u>==
- 例子
  ![image-20211023161836860](https://tva1.sinaimg.cn/large/008i3skNgy1gvpljikgw0j619y0do40702.jpg)



## java方法04:命令行传递参数

- 有时候你希望运行一个程序的时候再给它传递消息，这个时候就要靠传递命令行参数给main()函数实现

  ![image-20211023162253309](https://tva1.sinaimg.cn/large/008i3skNgy1gvpljfs9lmj61740da75f02.jpg)

- 更详细的用法自行百度，目前还没有需要用到的地方

## java方法05:可变参数

- **可变参数可以解决同一类型参数过多时，需要方法中重复进行大量定义参数的问题**

- 如何使用可变参数？

  ==在方法的声明中，在指定参数类型后加上一个省略号（...）==

- 一个方法中只能指定一个可变参数，它必须是方法的最后一个参数。任何普通的参数必须在它之前声明

- 举个例子：
  ![image-20211023163343009](https://tva1.sinaimg.cn/large/008i3skNgy1gvpljd51nuj619u0o0ad902.jpg)

  

## java方法06:递归讲解

- **递归就是自己调用自己**

- 利用递归可以用简单的程序来解决一些复杂的问题。它通常把一个大型复杂的问题层层转化为一个与原问题相似的、规模较小的问题来求解。递归策略只需要少量的程序就可描述出解题过程所需要的多次重复计算，大大地减少了程序的代码量。==递归的能力在于用有限的语句来定义对象的无限集合。==

- **递归机构包括两部分：**

  1. 递归头：什么时候不调用自身方法。如果没有递归头，程序将陷入死循环
  2. 递归体：什么时候需要调用自身方法。

- 例子：

  ```java
  //递归求阶乘
  public static int f(int n){
    if(n==1)
      return 1;
    else
      return n*f(n-1);
  }
  ```

- ==java使用的就是栈技术，能不用递归就不用==

