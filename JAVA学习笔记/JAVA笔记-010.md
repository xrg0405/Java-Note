# JAVA笔记-010

[TOC]

## 设计模式和单例设计模式

- 设计模式是在大量的实践中总结和理论化之后优选的代码结构、编程风格、以及解决问题的思考方式。
- 所谓的类的单例设计模式，就是采取一定的方法保证在整个的软件系统中，对某个类只能==存在一个对象实例==，并且该类只提供一个取得其对象实例的方法。

```java
//单例设计模式 //饿汉式
public class SingletonTest1{
  public static void main(String[] args){
    
    Bank bank1 = Bank.getInstance();
  }
}
class Bank{
  //1. 私有化类的构造器
  private Bank{
    
  }
  
  //2. 内部创建类的静态对象
  private static Bank instance = new Bank();
  
  //3. 提供公共的静态方法，返回类的对象
  public static Bank getInstance(){
    return instance;
  }
}

//单例设计模式/ /懒汉式
public class SingletonTest2{
  public static void main(String[] args){
    
    Bank bank1 = Bank.getInstance();
  } 
}

class Order{
  
  //1. 私有化类的构造器
  private Order(){
    
  }
  
  //2. 声明当前类对象，没有初始化
  private static Order instance = null;
  
  //3. 声明public、static的返回当前类对象的方法
  public static Order getinstance(){
    if(instance == null){
      instance = new Order();
    }
    return instance; 
  } 
}
```





## Mian()方法的使用说明

1. main()方法作为程序的入口
2. 是一个普通的静态方法
3. 也可以作为我们与控制台交互的方式。



```java
public class MainTest{
  public static void main(String[] args){
    Main.main(new String[100]);
    
    MainTest test = new MainTest();
    test.show();
  }
  
  public void show(){
    
  }
}

class Main{
  public static void main(String[] args){
    args = new String[100];
    for(int i = 0; i < args.length; i++){
      args[i] = "args" + i;
      System.out.println(args[i]);
    }
  }
}
```



## 类中的代码块

1. 代码块的作用：用来初始化类、对象
2. 代码块如果有修饰的话，只能用static



**静态代码块随着类的加载而执行，并且只执行一次；非静态代码块随着对象的创建而执行，每创建一个对象就执行一次**

**静态代码块可以初始化类的属性；非静态代码块可以在创建对象时，对对对象的属性进行初始化**

==静态代码的执行要优先于非静态代码块的执行==

```java
public class BlockTest{
  public static void main(String[] args){
    String desc = Person.desc;
    
    Person p1 = new Person();
    Person p2 = new Person();
  }
  
}

class Person{
  //属性
  String name;
  int age;
  static String desc = "I am a person!";
  
  //构造器
  public Person(){
    
  }
  public Person(String name, int age){
    this.name = name;
    this.age = age;
  }
  
  //代码块
  static{
    System.out.println("static block!");
  }
  {
    System.out.println("block!");
  }
  
  
  //方法
  public void eat(){
    System.out.println("Eat!");
  }
  @override
  public String toString(){
    return "Person {name = " + name + " age = " + age + "}");
  }
  public static void info(){
    System.out.println("static void info()!");
  }
}
```



## final修饰属性和方法

- final 可以用来修饰的结构：**类、方法、变量**
- 使用final 修饰类，则该类不能被其他类继承
  比如：String类、system类、StringBuffer类
- **final 用来修饰方法：表明此方法不能被重写**
  如：Object中的getClass()

- final 用来修饰变量：此时的变量就称为常量（可以看成是常量）
- static final 用来修饰属性，通常将该属性称为全局常量



## 抽象类与抽象方法的使用

- 抽象类是没有任何具体的实例的类
- 一旦一个类抽象了，则该类就不能实例化



**抽象类中一定有构造器，方便子类使用**
**开发中都会提供抽象类的子类，让子类对象那个实例化，完成相关操作**



==包含抽象方法的类一定是抽象类==

==抽象类中是可以没有抽象的方法的==



- 若子类重写了父类中的所有抽象方法后，此类可实例化



```java
public class PersonTest{
  public static void main(String[] args){
    
    method(new Student()); //匿名对象
    
    Worker worker = new Worker();
    menthod1(worker); // 非匿名的类 非匿名对象
    
    method1(new Worker()); //非匿名的类 匿名的对象
  }
  
  public static void method1(Person p){
    p.eat();
    p.walk();
  }
  public static void method(Student s){
  }
}

class Worker extends Person{
  @override
  public void eat(){
    
  }
  @override
  public void breath(){
    
  }
  
}
```



## 模版方法设计模式

- 抽象类体现的就是一种模版模式的设计
- 抽象类作为多个子类的通用模版，子类在抽象类的基础上进行拓展、改造，但子类总体上会保留抽象类的行为方式
- **解决的问题：**
  - 当功能内部一部分实现是确定的，一部分实现是不确定的。这时可以把不确定的部分暴露出去，让子类去实现

```java
// 模版方法的设计模式
public class Templatetest{
  public static void main(String[] args){
    SubTemplate t = new SubTemplate();
    t.spendTime(); 
  }
  
}

abstract class Template{
  
  // 计算某段代码执行所需要花费地时间
  public void spendTime(){
    
    long start = System.currentTimeMillis();
    this.code(); //易变部分
    long end = System.currentTimeMillis();
    System.out.println("花费的时间为：" + (end - start));
    
  }
  
  public abstract void code();
}



class SubTemplate extends Template{
  
  @override
  public void code(){
    
    for(int i = 2; i <= 1000; i++){
      boolean isFlag = true;
      for(int j = 2; j <= Math.sqrt(i); j++){
        if(i % j == 0){
          isFlag = false;
          break;
        }
      }
      if(isFlag){
        System.out.println(i);
      }
    }
  }
}
```



## 对接口（interface）的理解

- 接口就是规范，定义的是一组规则。
- 接口的本质是契约、标准和规范。

