# JAVA笔记-004

[TOC]

## JAVA类及其类成员

**==属性：==**对应类中的成员变量

**==行为：==**对应类中的成员方法

**Field = 属性 = 成员变量，Method =（成员）方法 = 函数**

```java
//测试类
public class PersonTest{
  public static void main(String[] args){
    //创建Person类的对象
    Person p1 = new Person();
    
    //调用属性
    p1.name = "Tom";
    p1.isMale = true;
    System.out.println(p1.name);
    
    //调用方法
    p1.eat();
    p1.sleep();
    p1.talk("Chinese");
    
    /*
    *如果创建了一个类的多个对象，则对象间是独立的
    *每个对象都有属于自己的类的属性
    */
    //创建第二个对象
    Person p2 = new Person();
    System.out.println(p2.name);
    System.out.println(p2.isMale);
  }
}

class Person{
  //属性
  String name;
  int age = 1;
  boolean isMale;
  
  
  //方法
  public void eat(){
    System.out.println("The person can eat!");
  }
  public void sleep(){
    System.out.println("The person can sleep!");
  }
  public void talk(String language){
    System.out.println("The person can talk by the " + language);
  }
  
}
```



**对象的内存解析：**

- new得时候，都是new在堆中（heap）
- 栈（stack）：先进后出



**属性与局部变量**

- 相同点：
  - 定义变量的格式都是一样的
  - 先声明，后使用
  - 变量都有其对应的作用域
- 不同点：
  - 属性直接定义在类中
  - 局部变量声明在方法内、方法形参、代码块内、构造器形参、构造器内部变量
  - 关于权限修饰符的不同
    - 属性可以在声明的时候就指明其权限，使用权限修饰符修饰。
    - 局部变量不可以使用权限修饰符
  - 默认初始化值的情况
    - 类的属性，根据其类型都有默认初始化值
    - 局部变量没有初始化值，调用局部变量时一定要给局部变量赋值。
  - 在内存中加载的位置不同
    - 属性加载到堆空间中
    - 局部变量加载到栈（stack）空间中

```java
public class UserTest{
  public static void main(String[] args){
    User u1 = new User();
    System.out.println(u1.name);
    System.out.println(u1.age);
    System.out.println(u1.isMale);
  }
}

class User{
  String name;
  int age = 1;
  boolean IsMale;
  
  public void talk(String language){//这里的language就是形参，局部变量
    System.out.println("We use the " + language + "to talk!");
  }
  
  public void eat(){
    String food = "rice"; //局部变量
    System.out.println("We always eat " + rice + "for dinner!");
  }
  
}
```



**类中方法的生命与使用**

- 方法：描述类应该具有的功能
- 方法的声明：权限修饰符、返回值类型、方法名（形参列表）

```java
public class CustomerTest{
  public static void main(String[] args){
    Customer cust1 = new Customer();
    cust1.eat();
  }
}

//客户类
class Customer{
  
  //属性
  String name;
  int age;
  boolean isMale;
  
  //方法
  public void eat(){
    System.out.println("客户吃饭")；
  }
  
  public void sleep(int hour){
    System.out.println("休息了" + hour + "个小时")；
  }
  
  public String getName(){
    return name;
  }
  
  public String getNation(String nation){
    String info = "我的国籍是：" + nation;
    return info;
  }
}
```



**return 关键字的使用**

- 使用范围：使用在方法体中
- 作用：1. 结束方法    2. 针对于有返回值类型的方法，返回指定数据 



**方法的使用**

- 方法中可以调用方法
- 方法中不可以定义新的方法



**小练习**

```java
public class test{
    public static void main(String[] args){
        Student st1 = new Student();
        String info = st1.say("xiaoming", 13, "数学", "打球和跑步");
        System.out.println(info);

        Teacher th1 = new Teacher();
      	th1.name = "Lihua";
      	th1.age = 35;
      	th1.teachAge = 15;
      	th1.course = "chinese";
        System.out.println(th1.say());
    }

}

class Student{
    String name;
    int age;
    String major;
    String interests;

    public String say(String name, int age, String major, String interests){
        this.name = name;
        this.age = age;
        this.major = major;
        this.interests = interests;
        String info = "My name is "+name+",age is "+age+",major is "+major+", interests are "+ interests;
        return info;
    }
}

class Teacher{
    String name;
    int age;
    int teachAge;
    String course;

    public String say(){
        String info = name+" "+age+" "+teachAge+" "+ course;
        return info;
    }
}
```





## JVM内存解析

- 编译完源程序后，生成一个或多个字节码文件
- 我们使用JVM中的类的加载器和解释器对生成的字节码文件进行解释运行。意味着需要将字节码文件对应的类加载到内存中，涉及到内存解析。
- 虚拟机栈，即为平时提到的栈结构，我们将局部变量存储在栈结构中。
- 堆，我们将new出来的结构放在该空间中。补充：对象的属性（非static的）加载在堆空间中。
- 方法区：类的加载信息、常量池，静态域。
- ==引用类型的变量，只可能存储两类值：null或地址（含变量的类型）==



**万物皆对象：**

- 在JAVA语言范畴中，我们将功能、结构封装到类中，通过类的实例化，来调用具体的功能结构。
- 涉及到JAVA语言与前端HTML、后端的数据库交互时，前后端的结构在JAVA层面交互时，都体现为类和对象。



## 匿名对象的使用



```java
public class InstanceTest{
  public static void main(String[] args){
    Phone p = new Phone();
    System.out.println(p);
    
    p.sendEmail();
    p.playGame();
    
    //匿名对象
    new Phone().sendEmail();
    new Phone().playGame();
    
    new Phone().price = 1999;
    new Phone().showPrice();
    
    PhoneMall mall = new PhoneMall();
    mall.show(new Phone());
  }
}

class PhoneMall{
  
  public void show(Phone phone){
    phone.sendEmail();
    phone.playGame();
  }
}

class Phone{
  double price; //价格
  
  public void sendEmail(){
    System.out.println("发送邮件！");
  }
  
  public void playGame(){
    System.out.println("玩游戏!")；
  }
  
  public void showPrice(){
    System.out.println(price);
  }
}
```



==在java中，对变量赋值，赋的是真实的值；对变量赋对象，赋的实际是地址。==



## 方法的重载

- 在同一个类中，允许存在一个以上的同名方法，只要他们的参数个数或者参数类型不同即可(==同名不同参==)
- 重载与返回值类型无关，只看参数列表，且参数列表必须不同（参数个数或者参数类型）。调用时根据方法参数列表的不同来区别。

```java
public class OverLoadTest{
  public static void main(String[] args){
    OverLoadTest test = new OverLoadTest();
    test.getSum(1, 2);
    test.getSum(1.0, 2.0);
  }
  
  // 如下两个方法构成重载	
  public void getSum(int i, int j){
    System.out.println(i + j);
  }
  
  public void getSum(double d1, double d2){
    System.out.println(d1 + d2);
  }
}
```



```java
public class OverloadExer{
  public static void main(String[] args){
    OverloadExer p = new OverloadExer();
    p.mOL(1);
    p.mOL(1,3);
    p.mOL("djsh");
    
    p.max(1,3);
    p.max(2.0, 3.0);
    p.max(2.0, 30.1, 40.4);
  }
  
  // 如下三个方法构成重载
  public void mOL(int i){
    System.out.println(i * i);
  }
  public void mOL(int i, int j){
    System.out.println(i * j);
  }
  public void mOL(String s){
    System.out.println(s);
  }
  
  //下面三个方法构成重载
  public int max(int i, int j){
    return (i > j)? i:j;
  }
  public double max(double d1, double d2){
    return (d1 > d2)? d1:d2;
  }
   public double max(double d1, double d2, double d3){
    int max =  (d1 > d2)? d1:d2;
    return (max > d3)? max : d3;
  }
}
```



**可变形参：**

- 参数类型 ... 参数名
- 当调用可变个数形参时，传入的参数个数可以从0到多个。
- 可变形参与其同名的正常参数构成重载。



## 方法参数的值传递机制

方法：必须由其所在类或对象调用才有意义。若方法含有参数：

- 形参：方法声明时的参数
- 实参：方法调用时实际传给形参的参数值

**java的实参值如何传入方法？**

- java里方法的参数传递方式只有值传递一种，即将实际参数值的副本传入方法内，而参数本身不受影响。
- 形参是基本数据类型，将实际参数基本数据类型变量的“数据值”传递给形参。
- 形参是引用数据类型，将实参引用数据类型变量的“地址值”传递给形参。

```java
public class ValueTransferTest{
  public static void main(String[] args){
    
    System.out.println("*********基本数据类型**********");
    int m = 10;
    int n = m;
    
    System.out.println("m=" + m + ", n=" + n);
    
    n = 20;
    System.out.println("m=" + m + ", n=" + n);
    
    System.out.println("*********引用数据类型**********");
    Order o1 = new Order();
    o1.orderId = 1001;
    Order o2 = o1;
    System.out.println("o1.orderId=" + o1.orderId + ", o2.orderId=" + o2.orderId);
    
    o2.orderId = 1002;
    System.out.println("o1.orderId=" + o1.orderId + ", o2.orderId=" + o2.orderId);
    
  }
}
class Order{
  int orderId;
}
```



## 值传递机制

- 如果参数是基本数据类型，此时实参赋给形参的是实参真实存储的数据值
- 如果参数是引用数据类型，此时实参赋给形参的是实参存储数据的地址值。



```java
public class Circle{
  double radius;
  
  public double findAreas(){
    return (radius/2)*(radius/2)*3.14;
  }
  
}

```

```java
public class PassObject{
  public static void main(String[] args){
    PassObject test = new PassObject();
    Circle c = new Circle();
    test.printAreas(c, 5);
    System.out.println("Now radius is " + c.radius);
  }
  
  public void printAreas(Circle c,int tiem){
    System.out.pritnln("Radius \t\t Area");
    
    //设置圆的半径
    for(int i=0; i<=time; i++){
      c.radius = i;
      System.out.println(c.radius + "\t\t" + c.findArea());
    }
    c.radius += 1;
  }
}
```



## 递归方法的使用

- 递归指的是一个方法体内调用方法自身

```java
	// 计算1到100之间所有自然数的和
public int sum(int num){
  if(num == 1)
    return 1;
  else
    return num + sum(num - 1);
}
```

