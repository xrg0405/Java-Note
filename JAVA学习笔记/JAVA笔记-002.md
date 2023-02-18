## JAVA笔记-002

[TOC]

## 多维数组的使用

小练习：

```java
public static void main(String[] args){
  int[][] arr = new int[][]{{3,5,8},{12,9},{7,0,6,4}};
  
  int sum = 0;
  for(int i=0; i<arr.length; i++){
    for(int j=0; j<arr[i].length;j++){
      sum += arr[i][j];
    }
  }
  System.out.println("The sum is:" + sum);
}
```

小tips：

- 一维数组：int[] x 或者 int x[] 
- 二维数组：int[][\] y 或者 int[\] y[\] 或者int y[\][\]

**使用二维数组打印一个10行的杨辉三角**

```java
public static void main(String[] args){
  int[][] arr = new int[10][10];
  
  //赋值每一行的第一个元素和最后的一个元素
  for(int i=0; i<arr.length; i++){
    arr[i][0] = 1;
    arr[i][i] = 1;
  }
  
  //计算数组
  for(int i=1; i<arr.length; i++){
    for(int j=1; j<arr[i].length; j++){
      arr[i][j] = arr[i-1][j-1]+arr[i-1][j];
    }
  }
  
  //打印数组
  for(int i=0; i<arr.length; i++){
    for(int j=0; j<arr[i].length; j++){
      if(arr[i][j] != 0)
        System.out.print(arr[i][j]);
    }
    System.out.println();
  } 
}
```



**拓展之笔试题**
创建一个长度为6的int型数组，要求数组元素的值都在1到30之间，而且是随机赋值。同时要求元素的值各不相同。

```java
public static void main(String[] args){
  //创建数组
  int[] arr = new int[6];
  
  //给数组赋值
  for(int i=0; i<arr.length; i++){
    arr[i] = (int)(Math.random()*30) + 1;
    for(int j=0; j<i; j++){
      if(arr[i] == arr[j]){
        i--;
        break;
      }
    }
  }
  
  //打印数组
  for(int i=0; i<arr.length; i++)
    System.out.println(arr[i]);
}
```



## 数组中涉及到的常见算法

1. 数组元素的赋值（杨辉三角形、回形数）
2. 求数值型数组中元素的最大值、最小值、平均数、总和等）
3. 数组的复制、反转、查找（线性查找、二分查找）
4. 数组元素的排序算法



**小练习**

```java
//求平均值，最大值，最小值，总和
public static void main(String[] args){
  int[] arr = new int[10];
  int sum = 0;
  int maxNum = -1;
  int minNum = 10000;
  
  for(int i=0; i<arr.length; i++){
    arr[i] = (int)(Math.random()*10) + 10;
    System.out.println(arr[i]);
    sum += arr[i];
    if(arr[i] > maxNum)
      maxNum = arr[i];
    if(arr[i] < minNum)
      minNum = arr[i];
  }
  
  System.out.println("The sum is: " + sum);
  System.out.println("The average is: " + (sum/arr.length));
  System.out.println("The max number is: " + maxNum);
  System.out.println("The min number is: " + minNum);
}
```

```java
//数组的复制
public static void main(String[] args){
  int[] array1, array2;
  array1 = new int[]{2, 3, 5, 7, 11, 13, 17, 19};
  array2 = new int[array1.length];
  
  // array2 = array1 该操作不是对数组的复制，只是对堆中地址的引用，堆中依旧只存在一个数据实体
  
  System.out.println("The array1 are: ");
  for(int i=0; i<array1.length; i++){
    System.out.print(array1[i] + "\t");
    array2[i] = array1[i];
    if(i%2 == 0)
      array2[i] = i;
  }
  
  System.out.println();
  System.out.println("The array2 are:");
  for(int i=0; i<array2.length; i++)
    System.out.print(array2[i] + "\t"); 
}
```

```java
//数组的反转
public static void main(String[] args){
  int[] arr = new int[10];
  int temp;
  
  //赋值
  System.out.println("The arr are: ");
  for(int i=0; i<arr.length; i++){
    arr[i] = i;
    System.out.print(arr[i] + "\t");
  }
    
  //反转操作
  for(int i=0; i<(int)(arr.length/2); i++){
    temp = arr[i];
    arr[i] = arr[arr.length-1 - i];
    arr[arr.length-1 - i] = temp;
  }
  
  //打印
  System.out.println();
  System.out.println("The reverse of arr are: ");
  for(int i=0; i<arr.length; i++)
    System.out.print(arr[i] + "\t");
}
```

```java
//线性查找----->直接遍历寻找

//比较简单，略过
```

**小tips**

- 比较内容，使用==.equals(xxxxx)==
- 比较数值，使用===\===

```java
//二分法查找，相较于线性查找，较快
//使用的前提为该数组有序
public static void main(String[] args){
  int[] arr = new int[10];
  
  for(int i=0; i<arr.length; i++)
    arr[i] = i;
  
  int dest = 7;
  int head = 0;
  int end = arr.length-1;
  
  for(int i=0; ;i++){
    int mid = (head+end)/2;
    if(head == end){
      System.out.println("We can't find out the dest!");
      break;
    }
    if(arr[mid] == dest){
      System.out.print("Find the dest! And the location is in " + mid);
      break;
    }
    else if(arr[mid] < dest)
      head = mid;
    else
      end = mid;  
  } 
}
```



### 排序算法

**衡量排序算法的优劣：**

- ==时间复杂度：==
  分析关键字的比较次数和记录的移动次数
- ==空间复杂度：==
  分析排序算法中需要多少辅助内存
- ==稳定性：==
  若两个记录A和B的关键字值相等，但排序后A、B的先后次序保持不变， 则称这种排序算法是稳定的



**排序算法分类：**

- 内部排序
  整个排序过程不需要借助于外部存储器（如磁盘等），所有排序操作都在内存中完成。
- 外部排序
  参与排序的数据非常多，数据量非常大，计算机无法把整个排序过程放在内存中完成，必须借助外部存储器。外部排序最常见的就是多路并归排序，可以认为外部排序是由多次内部排序组成。



**十大内部排序算法**

- `选择排序`

  $\to$直接选择排序、堆排序

- `交换排序`

  $\to$冒泡排序、快速排序

- `插入排序`

  $\to$直接插入排序、折半出入排序、shell排序

- `归并排序`

- `桶式排序`

- `基数排序` 



**算法的5大特征**

- 输入
  有0个或者多个输入数据。

- 输出
  至少有一个或多个输出结果。

- 有穷性

  算法在有限的步骤之后会自动结束，而不会无限循环，并且每个步骤在可接受的时间范围内完成。

- 确定性
  算法中的每一个步骤都有确定的含义，不会出现二义性。

- 可行性
  算法的每一步骤都是清楚可行的，用户可以用自行计算出。