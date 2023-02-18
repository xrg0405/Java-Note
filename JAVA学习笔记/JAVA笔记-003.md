# JAVA笔记-003

[TOC]

## 冒泡排序

```java
//数组的冒泡排序
public static void main(String[] args){
  int[] arr = new int[20];
  
  //初始化数组
  System.out.println("The arr before bubble sort are:");
  for(int i=0; i<arr.length; i++){
    arr[i] = (int)(Math.random()*20) + 10;
    System.out.print(arr[i] + "\t");
  }
  
  //冒泡排序
  int temp;
  for(int i=0; i<arr.length-1; i++){
    for(int j=0; j<arr.length-1-i; j++){
      if(arr[j] > arr[j+1]){
        temp = arr[j];
        arr[j] = arr[j+1];
        arr[j+1] = temp;
      }
    }
  }
  
  //打印冒泡排序后的数组
  System.out.println();
  System.out.println("The arr after bubble sort are:");
  for(int i=0; i<arr.length; i++){
    System.out.print(arr[i] + "\t");
  } 
}
```



## 快速排序

```java
//数组的快速排序
public static void main(String[] args){
  int[] arr = new int[10];
  
  //初始化数组
  System.out.println("The arr before quick sort are:");
  for(int i=0; i<arr.length; i++){
    arr[i] = (int)(Math.random()*100) + 1;
    System.out.print(arr[i] + "\t");
  }
  
  //快速排序
  
}
```



## 排序算法的横向对比

- ==从平均时间而言==，快速排序最佳。但是在最坏情况下时间性能不如堆排序和归并排序。
- ==从算法简单性看==，由于直接选择排序、直接插入排序和冒泡排序的算法比较简单，将其认为是简单算法。对于shell排序、堆排序、快速排序和归并排序算法，其算法比较复杂，认为是复杂排序。
- ==从稳定性看==，直接插入排序、冒泡排序和归并排序是稳定的；而直接选择排序、快速排序、shell排序和堆排序是不稳定的。
- ==从待排序的记录数n的大小看==，n较小时，适合采用简单排序；n比较大时宜采用改进排序。



## Arrays工具类的使用

- **详细的使用方法可以直接使用Arrays工具类的文档**

java.util.Arrays类即为操作数组的工具类，包含了用来操作数组（比如排序和搜索）的各种方法。

**实例demo**

```java
public static void main(String[] args){
  //判断两个数组是否相等
  int[] arr1 = new int[]{1,2,3,4,5};
  int[] arr2 = new int[]{2,4,5,2,2};
  boolean isEquals = Arrays.equals(arr1, arr2);
  System.out.println(isEquals);
  
  //将数组变成一个字符串
  System.out.println(Arrays.toString(arr1));
  
  //将指定的值填充满数组，当前填充值会覆盖数组原有值
  Arrays.fill(arr1, 10);
  System.out.println(Arrays.toString(arr1));
  
  //对数组进行排序
  Arrays.sort(arr2);
  System.out.println(Arrays.toString(arr2));
  
  //二分查找
  int[] arr = new int[]{12,34,454,23,455,65,23,56,5};
  int index = Arrays.binarySearch(arr, 455);
  System.out.println(index);
}
```



## 数组中的常见异常

1. 数组下标越界异常：ArrayIndexOutOfBoundsException
2. 空指针异常：NullPointerException



## 面向对象编程的学习主线

1. JAVA类以及类的成员：

   ==属性、方法、构造器==、代码块、内部类

2. 面向对象的三大特征

   ==封装性、继承性、多态性==、抽象性

3. 其他关键字

   this、super、static、final、abstract、interface、package、import等



## 理解面向对象和面向过程

**面向过程（POP）**

**面向对象（OOP）**

- ==类（class）==和==对象（object）==是面向对象的核心概念
  - 类是对一类事物的描述，是抽象的、概念上的定义
  - 对象是实际存在的该类事物的每个个体，因而也称为实例。



**面向对象的重点就是类的设计**
**设计类，就是设计类的成员**



