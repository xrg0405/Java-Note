---
typora-copy-images-to: upload
---

# java笔记-day5

[TOC]

## java数组01:什么是数组

- 数组是java中最简单的数据结构

- **数组的定义：**

  1. 数组是相同类型的数据的有序集合
  2. 数组描述的是相同类型的若干个数据，按照一定的先后次序排列组合而成
  3. 数组中的每一个数据称作一个数组元素，每个数组元素可以通过一个下标来访问它们

  

## java数组02:数组的声明和创建

- **首先必须声明数组变量才能在程序中使用数组（这个步骤相当于先在内存中开辟出一块空间，用来专门存放数组的数据，这样就不会出现数组因内存不足而无法添加的问题**



- 声明数组变量的语法：

  ```java
  dataType[] arrayRefVar = new dataType[arraySize] ;//这样就定义好了一个数组
  //例：定义一个长度为7的int型数组
  int[] arrayA = new int[7];
  ```

- **数组的元素是通过索引访问的，数组索引从0开始**

- 获取数组长度：==arrays.length==

- JAVA中新动态初始化创建的数组，里面的值默认为0



## java数组03:三种初始化及内存分析

- **Java内存分析：**

  1. **堆**

     - 存放new的对象和数组

     - 可以被所有的线程共享，不会存放别的引用对象

  2. **栈**

     - 存放基本变量类型（会包含这个基本变量类型的具体数值。
     - 引用对象的变量（会存放这个引用在堆里面的具体地址）

  3. **方法区**

     - 可以被所有的线程共享
     - 包含了所有的class和static变量

![image-20211024151329752](https://tva1.sinaimg.cn/large/008i3skNgy1gvqf77f0n1j614o0jemy702.jpg)

- **数组的三种初始化：**

  1. 静态初始化
  2. 动态初始化
  3. 数组的默认初始化
     - 数组是引用类型，它的元素相当于类的实例变量，因此数组一经分配空间，其中的每个元素也被按照实例变量同样的方式被隐式初始化

  ```java
  public class Demo01{
    public static void mian(String[] args){
      //静态初始化：创建 + 赋值
      int[] a = {1, 2, 3, 4, 5, 6, 7};
      //动态初始化(数组每个元素的值默认为0，所以包含了默认初始化)
      int[] b = new int[7];
    }
  }
  ```

  

## java数组04:下标越界

- **数组的四个基本特点：**

  1. 数组的长度是确定，数组一旦被创建，它的大小就是不可以改变的。
  2. 数组的元素必须是相同的类型，不允许出现混合类型
  3. 数组中的元素可以是任何数据类型，包括基本数据类型和引用类型
  4. 数组变量属于引用类型，数组也可以看成是对象，数组中的每个元素相当于该对象的成员变量。数组本身就是对象，java中对象是在堆中的，因此数组无论保存原始数据类型还是其他对象类型，==数组对象本身是在堆中的==

- **数组边界：**

  1. 下标的合法区间：[0, length-1]，如果越界就会报错，如下：

     ```java
     public static void main(String[] args){
       int[] a = new int[2];
       System.out.print(a[2]);
     }
     //程序会报错——ArrayIndexOutOfBoundsException：数组下标越界异常
     ```

     

- **总结：**
  1. 数组是数据类型相同的有序集合
  2. 数组也是对象。数组元素相当于对象的成员变量
  3. 数组的长度是确定的，不可变的，超出数组长度，程序会报错



## java数组05:数组的使用

- **循环遍历方法**

  1. 使用for循环，通过数组下标读取数组

     ```java
     public class Demo{
       public static void main(String[] args){
         int[] a = {1,2,3,4,5,6,7,8,9,10};
         for(int i=0; i<a.length; i++){
           System.out.println("数组第"+(i+1)+"个输出为："+a[i]);
         }
       }
     }
     ```

  2. 使用for-each增强循环

     ```java
     public class Demo{
       public static void main(String[] args){
         int[] a = {1,2,3,4,5,6,7,8,9,10};
         int i = 0;
         for(int num : a){
           System.out.println("数组第"+(i+1)+"个输出为："+num);
           i++;
         }
       }
     }
     ```

     

- **数组作为方法的传入参数**

  ```java
  //反转数组
  public static int[] reverse(int[] arrays){
    int[] result = new int[arrays.length];
    //反转操作
    for(int i=0, j=arrays.length-1; i<arrays.length; i++,j--){
      result[j] = arrays[i];
    }
    return result;
  }
  ```

  

- **数组作为返回值**

  如上



## java数组06:多维数组

- **多维数组可以看成是数组的数组，比如二维数组就是一个特殊的一维数组，其每个元素都是一个一维数组**

  1. 二维数组：

     ```java
     int arrays = new int[2][5];
     //该数组可以看成是一个两行列的数组
     ```

  2. 多维数组同理（可以参照python里的多维列表去理解）



## java数组07:Arrays类讲解

- **数组的工具类java.util.Arrays**

  

- **由于数组对象本身并没有什么方法可以供我们调用，但API中提供了一个工具类Arrays供我们使用，从而可以对数据对象进行一些基本的操作**

  

- ==了解Arrays类最好的办法就是查看JDK帮助文档==
       

- **Arrays类中的方法都是static修饰的静态方法，在使用的时候可以直接使用类名进行调用，而不用使用使用对象来调用（也可以使用对象来调用，但一般都不会使用）**
       

- **Arrays类具有以下常用功能：**

  1. 通过fill方法赋值

  2. 通过sort方法对数组进行升序排序

  3. 通过equals方法比较数组中元素值是否相等

  4. 通过binarySearch方法能对排序好的数组进行二分查找法操作

  5. 使用举例：

     ```java
     import java.utils.Arrays;
     public class Demo{
       public static void main(String[] args){
         int[] arrays = {,1,3,4,6,7,32,3,4,5,4};
         //对数组进行排序，升序
         Arrays.sort(arrays);
         
         //将数组第2个到第4个元素替换为0
         Arrays.fill(a, 2, 4, 0);
       }
     }
     ```



## java数组08:冒泡排序

- **冒泡排序无疑是最为出名的排序算法之一，==总共有8大排序算法==**

     

- **冒泡排序算法有两成循环，外层冒泡轮数，里层依次比较（两两比较，谁大谁靠后**

  ```java
  public class demo{
    public static void main(String[] args){
      //冒泡排序
      //1.比较数组中两个相邻的元素，如果第一个数比第二个数大，这两个数就相互交换位置
      //每一次比较都会产生一个最大或者最小的数字
      //下一轮可以减少一次排序
      //依次循环，直到结束
      int[] arrays = {1,4,554,6,6,3,23,45,6,7};
      int temp = 0;
      
      //外层循环，判断我们要走多少次
      for(int i=0; i<arrays.length-1; i++){
        //内层循环，比较两个数的大小
        for(int j=0; j<arrays.length-1-i; j++){
          if(arrays[j+1] < arrays[j]){
            temp = arrays[j];
            arrays[j] = arrays[j+1];
            arrays[j+1] = temp;
          }
        }
      }
    }
  }
  ```

-  ==冒泡算法的时间复杂度为O(n^2)==



- **冒泡排序有哪些优化方法？**
  自行百度，多做练习！！！



## java数组09:稀疏矩阵

- **稀疏数组是一种数据结构**

  ​      

- ![image-20211024170827097](https://tva1.sinaimg.cn/large/008i3skNgy1gvqiiuh8hqj61dm0p4ae702.jpg)

- 例子：

  ```java
  public class Demo{
    public static void main(String[] args){
      //1.创建一个二维数组 11*11 0:没有棋子，1:黑棋，2:白棋
      int[][] array1 = new int[11][11];
      array1[1][2] = 1;
      array1[2][3] = 2;
      //输出原来的数组
      System.out,println("输出原始的数组：");
      for(int[] ints : array1){
        for(int anInt : ints){
          System.out.print(anInt+"\t");
        }
        System.out.println();
      }
      
      //转为为稀疏数组保存
      //获取有效值的个数
      int sum = 0;
      for(int i=0; i<11; i++){
        for(int j=0; j<11; j++){
          if(array1[i][j] != 0){
            sum++;
          }
        }
      }
      System.out.println("有效值的个数："+sum);
      
      //2.创建一个稀疏数组
      int[][] array2 = new int[sum+1][3];
      
      array2[0][0] = 11;
      array2[0][1] = 11;
      array2[0][2] = sum;
      
      //遍历二维数，将非0的值存放在稀疏数组中
      int count = 0;
      for(int i=0; i<array1.length; i++){
        for(int j=0; j<array1[i].length; j++){
          if(array[i][j] != 0){
            count++;
            array2[count][0] = i;
            array2[count][1] = j;
            array2[count][2] = array1[i][j];
          }
        }
      }
      
      //输出稀疏数组
      System.out.println("稀疏数组：");
      for(int i=0; i<arrays.length; i++){
        System.out.println(array2[i][0]+"\t"+array2[i][1]+"\t"+array2[i][2]+"\t");
      }
      
      //稀疏数组还原
      System.out.println("稀疏数组还原：");
      //1.读取稀疏数组
      int[][] array3 = new int[array2[0][0]][array2[0][1]];
      
      //2.给其中的元素还原它的值
      for(int i=1; i<array2.length; i++){
        array3[array2[i][0]][array2[i][1]] = array2[i][2];
      }
      
      //3.打印
      System.out.println("输出还原的数组：");
      for(int[] ints : array3){
        for(int anInt : ints){
          System.out.print(anInt+"\t");
        }
        System.out.println();
      }
      
      
    }  
  }
  ```

  



