## JAVA笔记-012

[TOC]

## IDEA编译器的使用

- 在IDEA中只有 project 和 module的概念
- project 代表的是一整个的项目
- module 代表一整个项目下的不同小工程



**IDEA中快捷键的使用：**

- 自行百度，MAC和WIN下的快捷键略有区别



**IDEA中含有许多代码模版可以使用，如sout 为System.out.println()**



## 程序、进程、线程

- **程序**：
  一段静态的代码，静态对象

- **进程：**

  是程序的一次执行过程，或是正在运行的一个程序。是一个动态的过程：有它自身的产生、存在和消亡的过程（即生命周期）

- **线程：**
  进程可以进一步细化为线程，是一个程序内部的一条执行路径



**一个Java应用程序，其实至少有3个线程：main()主线程， gc()垃圾回收线程、异常处理线程。如果发生异常，会影响主线程**



**并行与并发；**

- 并行：多个CPU同时执行多个任务
- 并发：一个CPU同时执行多个任务



**使用多线程的优点：**

- 提高应用程序的响应。对图像化界面更有意义，可增强用户体验。
- 提高计算机系统CPU的利用率
- 改善程序结构。将既长，又复杂的进程分为多个线程，独立运行，利于理解和修改



**什么时候应该使用多线程：**

- 程序需要同时执行两个或多个任务
- 程序需要实现一些需要等待的任务时，如用户输入、文件读写操作、网络操作、搜索等
- 需要一些后台运行的程序时



## 创建对线程的方式

**非多线程：**

```java
public class Sample{
  public void method1(String str){
    System.out.println(str);
  }
  
  public void method2(String str){
    method1(str);
  }
  
  public static void main(String[] args){
    Sample s = new Sample();
    s.method2("Hello!");
  }
}
```



**多线程：**

1. 继承与Thread类

```java
class MyThread extends Thread{
  @Override
  public void run(){
    for (int i = 0; i < 100; i++){
      if (i % 2 == 0){
        System.out.println(i);
      }
    }
  }
}

public class ThreadTest{
  public static void mian(String[] args){
    MyThread t1 = new MyThread();
    t1.start();
    System.out.println("hello!");
  }
}
```

Exercise: 创建两个分线程，其中一个线程遍历100以内的偶数，另一个线程遍历100以内的奇数

```java
public class ThreadDemo{
  public static void main(String[] args){
    MyThread1 m1 = new MyThread1();
    MyThread2 m2 = new MyThread2();
    
    m1.start();
    m2.start();
    
    //创建Thread类的匿名子类的方式
    new Thread(){
      @Override
      public void run(){
        for (int i = 0; i < 100; i++){
      if (i % 2 == 0){
        System.out.println(Thread.currentThread().getName() + ":" + i);
      }
    }
      }
    }.start();
    
    new Thread(){
      @Override
      public void run(){
        for (int i = 0; i < 100; i++){
      if (i % 2 != 0){
        System.out.println(Thread.currentThread().getName() + ":" + i);
      }
    }
      }
    }.start();
    
  }
}

class MyThread1 extends Thread{
  @Override
  public void run(){
    for (int i = 0; i < 100; i++){
      if (i % 2 == 0){
        System.out.println(Thread.currentThread().getName() + ":" + i);
      }
    }
  }
}

class MyThread2 extends Thread{
  @Override
  public void run(){
    for (int i = 0; i < 100; i++){
      if (i % 2 != 0){
        System.out.println(Thread.currentThread().getName() + ":" + i);
      }
    }
  }
}
```

**Thread类的有关方法：**

- `void start():` 启动线程，并执行对象的==run()==方法
- `run():` 线程在被调度时执行的操作
- `String getName():` 返回线程的名称
- `void setNmae(String name):` 设置该线程名称
- `static Thread currentThread():` 返回当前线程。在Thread子类中就是==this== ，通常用于主线程和==Runnable==实现类

```java
class HelloThread extends Thread{
  @Override
  public void run(){
    for (int i = 0; i < 100; i++){
      if(i % 2 ==0){
        System.out.println(Thread.currentThread().getName() + ":" + i);
      }
      if(i % 20 == 0){
        this.yield(); //释放当前CPU的执行权
        // join():在线程a中调用线程b的join方法，此时线程a进入阻塞状态；直到线程b完全执行完后，线程a才结束阻塞状态。
      }
    }
  }
}

public class ThreadMethodTest{
  public static void main(String[] args){
    HelloThread h1 = new HelloThread();
    h1.setName("线程一");
    h1.start();
    
    //主线程命名
    Thread.currentThread().setName("主线程");
    for (int i = 0; i < 100; i++){
      if(i % 2 ==0){
        System.out.println(Thread.currentThread().getName() + ":" + i);
      }
    }
      
  }
}
```



**Java的调度方法：**

- 同优先级线程组成先进先出队列（先到先服务），使用时间片策略
- 对高优先级，使用优先调度的抢占式策略



**线程的优先级：**

- **线程的优先级等级**
  1. ==MAX_PRIORIYT==：10
  2. ==MIN_PRIORITY==：1
  3. ==NORM_PRIORITY==：5
- **涉及的方法**
  1. ==getPriority()==：返回线程优先级
  2. ==setPriority(int newPriority)==：改变线程的优先级
- **说明**
  - 线程创建时继承父线程的优先级
  - 低优先级只是获得调度的概率低，并非一定是在高优先级线程之后才被调用

```java
class Window extends Thread{
  private static int ticket = 100;
  // 存在线程安全问题，待解决
  @Override
  public void run(){
    while(true){
      if(ticket > 0){
        System.out.println(getName() + "：卖票，票号为：" + ticket);
        ticket--;
      } else{
        break;
      }
    }
  }
}

public class WindowTest{
  public static vopid main(String[] args){
    Window t1 = new Window();
    Window t2 = new Window();
    Window t3 = new Window();
    
    t1.setName("窗口1");
    t2.setName("窗口2");
    t3.setName("窗口3");
    
    t1.start();
    t2.start();
    t3.start(); 
  } 
}
```



**创建多线程的方式二：实现Runnable接口：**

1. 创建一个实现了Runnable接口的类
2. 实现类去实现Runnable中的抽象方法：run()
3. 创建实现类的对象
4. 将此对象作为参数传递到Thread类的构造器中，创建Thread类的对象
5. 通过Thread类的对象调用start()

```java
class Mthread implements Runnable{
  @Override
  public void run(){
    for (int i = 0; i < 100; i++){
      if(i % 2 == 0){
        System.out.println(i);
      }
    }
  }
}

public class ThreadTest1{
  public static void main(String[] args){
    MThread mThread = new MThread();
    Thread t1 = new Thread(mThread);
    t1.start();
  }
}
```



```java
class Window1 implements Runnable{
  private static int ticket = 100;
  @Override
  public void run(){
    while(true){
      if(ticket > 0){
        System.out.println(Thread.currentThread.getName() + "：卖票，票号为：" + ticket);
        ticket--;
      } else{
        break;
      }
    }
    
  }
}

public class WindowTest1{
  public static void main(String[] args){
    Window1 w = new Window1();
    
    Thread t1 = new Thread(w);
    Thread t2 = new Thread(w);
    Thread t3 = new Thread(w);
    
    t1.setName("窗口1");
    t2.setName("窗口2");
    t3.setName("窗口3");
    
    t1.start();
    t2.start();
    t3.start();
  }
  
}
```



## 比较创建线程的两种方式

- 开发中，优先选择实现Runnable接口的方式
  - 实现的方式没有类的单继承性的局限性
  - 实现的方式更适合来处理多个线程有共享数据的情况
- 两种方式都需要重写run()方法，将线程要执行的逻辑声明在run()中



**线程的分类：**

Java中的线程分为两类：一种是守护线程，一种是用户线程

- 它们几乎在每个方面都是相同的，唯一的区别是判断JVM何时离开
- 守护线程是用来服务用户线程的，通过start()方法前调用==thread.seDaemon(true)==可以把一个用户线程变成一个守护线程
- Java垃圾回收就是一个典型的守护线程
- 若JVM中都是守护线程，当前JVM将退出



