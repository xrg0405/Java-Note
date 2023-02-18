# JAVA笔记-011

[TOC]

## 接口的使用

1. 接口使用interface来定义
2. Java中，接口和类是并列的两个结构
3. 如何定义接口：定义接口中的成员：
   - 定义全局常量和抽象方法
   - 定义静态方法、默认方法

4. 接口中不能定义构造器！意味着接口不能实例化
5. Java开发中，接口通过让类去实现接口

```java
public class InterfaceTest{
  public static void main(String[] args){
    System.out.println(Flyable.MAX_SPEED);
    System.out.println(Flysble.MIN_SPEED);
    
    Plane plane = new Plane();
    plane.fly();
  }
  
}

interface Flyable{
  
  //全局常量
  public static final int MAX_SPEED = 7900;
  public static final int MIN_SPEED = 1;
  
  //抽象方法
  public abstract void fly();
  public abstract void stop();
}

class Plane implements Flyable{
  @Override
  public void fly(){
    System.out.println("起飞！！！");
  }
  @Override
  public void stop(){
    System.out.println("降落！！！");
  }
}

abstract class Kite implements Flyable{
  @Override
  public void fly(){
    System.out.println("Kite起飞！！！");
  }
}
```



- ==Java 类可以实现多接口==：弥补了Java单继承性的局限性

  **格式：**class	A	extends	B	implements	CC，DD，EE

- **接口与接口之间可以多继承**



**接口的使用；体现多态性；接口实际上就可以看成是一种规范**



```java
public class USBTest{
  public static void main(String[] args){
    Computer com = new Computer();
    //1. 创建了接口的非匿名实现类的非匿名对象
    Flash flash = new Flash();
    com.transferData(flash);
    
    //2. 创建了接口的非匿名实现类的匿名对象
    com.transferData(new Printer());
    
    //3. 创建了接口的匿名实现类的非匿名对象
    USB phone = new USB{
      @Override
      public void strat(){
        System.out.println("Phone start!!!");
      }
      @Override
      public void stop(){
        System.out.println("Phone stop!!!");
      }
    };
    com.transferData(phone);
    
    //4. 创建了接口的匿名实现类的匿名对象
    com.transferData(new USB{
      @Override
      public void strat(){
        System.out.println("USB start!!!");
      }
      @Override
      public void stop(){
        System.out.println("USB stop!!!");
      }
    });
    
  }
  
}
class Computer{
  public void transferData(USB usb){
    usb.start();
    System.out.println("具体传输数据细节！");
    usb.stop();
  }
}

interface USB{
  //常量
  
  //方法
  void start();
  void stop();

}

class Flash implements USB{
  @Override
  public void strat(){
    System.out.println("Flash start!!!");
  }
  @Override
  public void stop(){
    System.out.println("Flash stop!!!");
  }
}

class Printer implements USB{
  @Override
  public void strat(){
    System.out.println("Printer start!!!");
  }
  @Override
  public void stop(){
    System.out.println("Printer stop!!!");
  }
}
```



## 接口应用：代理模式

- 代理模式是JAVA开发中使用比较多的一种设计模式。代理设计就是为其他对象提供一种代理以控制对这个对象的访问。



```java
public class NetWorkTest{
  public static void main(String[] args){
    Server server = new Server();
    ProxyServer proxyServer = new ProxyServer(server);
    
    proxyServer.browse();
    
  }
}

interface NetWork{
  public void browse();
}

//被代理类
class Server implements NetWork{
  @Override
  public void browse(){
    System.out.println("真实的服务器访问网络！");
  }
}

//代理类
class ProxyServer implements NetWork{
  private NetWork work;
  
  public ProxyServer(NetWork work){
    this.work = work;
  }
  
  public void check(){
    System.out.println("联网前的检查工作")
  }
  @Override
  public void browse(){
    check();
    work.browse();
  }
}
```



**应用场景：**

- 安全代理：屏蔽对真实角色的直接访问
- 远程代理：通过代理类处理远程方法调用（RMI）
- 延迟加载：先加载轻量级的代理对象真正需要时再加载真实对象



**分类：**

- 静态代理（静态定义代理类）
- 动态代理（动态生成代理类）



## 内部类的分类

- 在JAVA中，允许一个类的定义位于另一个类的内部，前者称为内部类，后者称为外部类

```java
public class InnerClassTest{
  
}

class Person{
  
  //静态成员内部类
  static class Dog{
    
  }
  //非静态成员内部类
  class Bird{
    
  }
  
  //方法内说明
  public void method(){
    //局部内部类
    class AA{}
  }
  //代码块内说明
  {
    class BB{}
  }
}
```



## JAVA异常处理

- **==error：==**
  java虚拟机无法解决的严重问题。如：JVM系统内部错误，资源耗尽等严重情况。比如：StackOverflowError和OOM。一般不编写针对性的代码进行处理
- **==exception：==**
  其他因编程错误或偶然的外在因素导致的一般性问题，可以使用针对性的代码进行处理。如：
  - 空指针访问
  - 试图读取不存在的文件
  - 网络连接中断
  - 数据下边越界

```java
//资源耗尽错误-----栈溢出
public class ErrorTest{
  public static void main(String[] args){
    main(args);
  }
}

//资源耗尽错误-----OOM,堆溢出
public class ErrorTest{
  public static void main(String[] args){
    Integer[] arr = new Integer[1024*1024*1024];
  }
}
```

 

**JAVA异常处理的方式：**

- try—catch—finally
- throws + 异常类型



==像数据库连接、输入输出流、网络编程Scoket等资源，JVM是不能自动回收的，我们需要自己手动去释放资源。此时的资源释放就需要声明在finally中。==



## 重写异常处理

1. 子类重写的方法抛出的异常类型不大于父类被重写的方法抛出的异常类型

```java
public class OverrideTest{
  
  public static void main(String[] args){
    OverrideTest test = new OverrideTest();
    test.display(new SubClass());
  }
  
  public void display(SuperClass s){
    try{
      s.method();
    }catch(IOException e){
      e.printStackTrace();
    }
  }
}

class SuperClass{
  public void method() throws IOException{
    
  }
}

class SubClass extends SuperClass{
  public void method(){
    
  }
}

```



**开发中如何选择使用try-catch-finally还是throws？**

- 如果父类中被重写的方法没有thirows方式处理异常，则子类重写的方法也不能用throws，意味着如果子类重写的方法中有异常，必须使用try-catch-finally方式处理。
- 执行的方法中，先后有调用了另外的几个方法，这几个方法是递进关系执行的，我们建议这几个方法使用throws的方式进行处理，而执行的方法a可以考虑使用try-catch-finally的方式进行处理。



## 手动抛出异常

```java
public class StudentTest{
  public static void main(String[] args){
    try{
      Student s = new Student();
      s.regist(-10001);
      System.out.println(s);
    }catch(Exception e){
      System.out.println(e.getMessage());
    }
    
  }
  
}

class Student{
  private int id;
  
  public void regist(int id) throws Exception{
    if(id > 0){
      this.id = id;
    }else{
      //System.out.println("您输入的数据非法！");
      //手动抛出异常
      //throw new RuntimeException("您输入的数据非法！");
      throw new Exception("您输入的数据非法！");
    }
  }
}
```



