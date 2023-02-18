# JAVA笔记-005

[TOC]

```java
public class ValueTransferTest{
  public static void mian(String[] args){
    
    String s1 = "hello";
    ValueTransferTest test = new ValueTransferTest();
    test.change(s1);
    
    System.out.println(s1);
  }
  
  public void change(String s){
    s = "hi~~";
  }

}
```



## 封装与隐藏

- 我们的程序设计追求“高内聚、低耦合”
  - 高内聚：类的内部数据操作细节自己完成，不允许外界干涉
  - 低耦合：仅对外暴露少量的方法用于使用
- 隐藏对象内部的复杂性，只对外公开简单的借口。便于外界调用，从而提高系统的可拓展性、可维护性。

```java
public class AnimalTest{
  public static void main(String[] args){
    Animal a = new Animal();
   //a.name = "大黄";
   //a.age = 1;
   //a.legs = 4;
    a.setLegs(4);
    
    a.show();
  }
}

class Animal{
  //使用权限修饰符，使得a.name不能直接使用
  private String name;
  private int age;
  private int legs;
  
  public void setLegs(int l){
    if(l >= 0 && l%2 == 0)
      legs = l;
    else
      legs = 2;
  }
  
  public int getLegs(){
    return legs;
  }
  
  public void eat(){
    System.out.println("动物进食！");
  }
  
  public void show(){
    System.out.println("name = " + name + ", age = " + age + "legs = " + legs);
  }
}
```

- 我们创建一个类的对象后，我们可以通过“对象.属性“的方式对对象的属性进行赋值。这里赋值操作要受到属性的数据类型和存储范围的制约。除此之外，没有其他的限制条件。但是在实际问题中，我们往往需要给属性赋值时添加额外的限制条件。这个条件就不能在属性声明时体现，我们只能通过方法进行限制条件的添加，如上述代码。同时我们需要避免用户再使用“对象.属性“的方式对属性进行赋值，则需要将属性声明为私有的（private）

**封装性的体现**

- 我们将类的属性xxx私有化（private），同时提供公共的（public）方法来获取（getXxx）和设置（setXxx）属性。
- 封装性的体现需要权限修饰符来配合。
  - private < 缺省 < protected < public
  - ==private:== 类内部
  - ==缺省：==类内部、同一个包
  - ==protected:== 类内部、同一个包、不同包的子类
  - ==public：==类内部、同一个包、不同包的子类、同一个工程
  - 4种权限可以用来修饰类及类的内部结构：属性、方法、构造器、内部类

```java
public class Order{
  private int orderPrivate;
  int orderDefault;
  public int orderPublic;
  
  private void methodPrivate(){
    orderPrivate = 1;
    OrderDefault = 1;
    orderPublic = 1;
  }
  
  void methodDefault(){
    orderPrivate = 1;
    OrderDefault = 1;
    orderPublic = 1;
  }
  
  public void methodPublic(){
    orderPrivate = 1;
    OrderDefault = 1;
    orderPublic = 1;
  }
}
```



**小练习：**

```java
public class Person{
  private int age;
  
  public void setAge(int a){
    if(a<0 || a>130){
      throw new RuntimeException("传入的数据非法！");
    }
    else{
      age = a;
    }
  }
  
  public int getAge(){
    return age;
  }
}
```

```java
public class PersonTest{
  public static void main(String[] args){
    Person p1 = new Person();
    
    //错误方式
    p1.age = 1; //此处会报错
    System.out.println("The age is: " + p1.age);
    
    //正确方式
    p1.setAge(12);
    System.out.println("The age is: " + p1.getAge());
  }
}
```



## 构造器

**构造器的特征**

- 具有与类相同的名称
- 不声明返回值类型（与声明为void不同）
- 不能被static、final、synchronized、abstract、native修饰，不能有return语句返回值



**构造器的作用**

- 创建对象
- 给对象进行初始化



**如果没有显示的定义类的构造器的话，则系统默认提供一个空参的构造器**



```java
public class PersonTest{
  public static void main(String[] args){
    //创建类的对象
    Person p = new Person(); //构造器
    p.eat();
    
    Person p1 = new Person("Tom");
    p1.eat();
    
    Person p2 = new Person("Linda", 11);
    p2.eat();
  }
  
}

class Person{
  //属性
  String name;
  int age;
  
  //构造器
  public Person(){
    System.out.println("Person().......");
  }
  
  public Person(String n){
    name = n;
  }
  
  public Person(String n, int a){
    name = n;
    age = a;
  }
  
  //方法
  public void eat(){
    SYstem.out.println("人吃饭");
  }
  
  public void study(){
    System.out.println("人可以学习");
  }
  
}
```

 

## 属性赋值的先后顺序

- 默认初始化
- 显式初始化
- 构造器中赋值
- 通过“对象.方法“或”对象.属性“的方式赋值

```java
public class UserTest{
  public static void main(String[] args){
    User u = new User();
    System.out.println(u.age);
    
    User u1 = new User(2);
    u1.setAge(3);
    System.out.println(u1.age);
  }
}

class User{
  String name;
  int age = 1;
  
  
  public User(){
  }
  public User(int a){
    age = a;
  }
  
  
  public void setAge(int a){
    if(a >= 0){
      age = a;
    }
    else
      age = 0;
  }
  public int getAge(){
    return age;
  }
}
```



## JavaBean

**JavaBean是一种Java语言写成的可重用组件**

- 所谓JavaBean，是指符合如下标准的Java类
  - 类是公共的
  - 有一个无参的公共的构造器
  - 有属性，且有对应的get、set方法

- 用户可以使用JavaBean将功能、处理、值、数据库访问和其他任何可以用Java代码创造的对象进行打包，并且其他的开发者可以通过内部的JSP页面、Servlet、其他JavaBean、applet程序或者其他应用来使用这些对象。用户可以认为JavaBean提供了一种随时随地的复制和粘贴功能，而不用关心任何改变。



## this关键字的使用

```java
public class PersonTest{
  
}

class Person{
  private String name;
  private int age;
  
  public void setName(String name){
    this.name = name;
  }
  public void setAge(int age){
    this.age = age;
  }
  
  public String getName(){
    return name;
  }
  public String getAge(){
    return age;
  }
}
```

**this调用构造器**

- 我们在类的构造器中，可以显式的使用this方式，调用指定类的其他构造器
- 构造器中不能通过this调用自身
- 如果一个类中有n个构造器，则最多有n-1构造器使用了this
- 规定：this必须声明在当前构造器的首行



**小练习**

```java
public class Boy{
  private String name;
  private int age;
  
  public Boy{
    
  }
  public Boy(String name, int age){
    this.name = name;
    this.age = age;
  }
  
  public String getName(){
    return name;
  }
  public void setName(String name){
    this.name = name;
  }
  public int getAge(){
    return age;
  }
  public void setAge(int age){
    this.age = age;
  }
  
  public void marry(Girl girl){
    System.out.println("我想娶：" + girl.getName());
  }
  public void shout(){
    if(age >= 22){
      System.out.println("你可以去合法登记了！");
    }
    else{
      System.out.println("先多谈谈恋爱！");
    }
  }
}
```

```java
public class Girl{
  private String name;
  private int age;
  
  public Girl{
    
  }
  public Girl(String name, int age){
    this.name = name;
    this.age = age;
  }
  
  public String getName(){
    return name;
  }
  public void setName(String name){
    this.name = name;
  }
  
  public void marry(Boy boy){
    System.out.println("我想嫁给" + boy.getName());
    boy.marry(this);
  }
  public int compare(Girl girl){
    if(this.age > girl.age){
      return 1;
    }else if(this.age < girl.age){
      return 0;
    }else{
      return -1;
    }
  }

}
```

```java
public class BoyGirlTest{
  public static void main(String[] args){
    Boy boy = new Boy("lihua", 21);
    boy.shout();
    
    Girl girl = new Girl("lihong", 18);
    girl.marry(boy);
    
    Girl girl2 = new Girl("sb", 19);
    int compare = girl.compare(girl2);
    if(compare > 0){
      System.out.println(girl.getName() + "大");
    }else if(compare < 0){
      System.out.println(girl2.getName() + "大");
    }else{
      System.out.println("一样大");
    }
  }
}
```



## MVC设计模式

MVC是常用的设计模式之一，将整个程序分为3个层次：视图模型层、控制器层和数据模型层。

这种将程序输入输出、数据处理、以及数据的展示分离开来的设计模式使程序结构变得灵活且清晰，同时也描述了程序各个对象间的通信方式，降低了程序的耦合性。

- **模型层 model层主要处理数据**
  - 数据对象封装 model.bean/domain
  - 数据库操作类 model.dao
  - 数据库 model.db
- **控制层 controller层处理业务逻辑**
  - 应用界面相关 controller.activity
  - 存放fragment controller.fragment
  - 显示列表的适配器 controller.adapter
  - 服务相关的 controller.service
  - 抽取的基类 controller.base
- **视图层 view层显示数据**
  - 相关工具类 view.utils
  - 自定义 view  view.ui



**import关键字**

- 在源文件中显式地使用import结构导入指定包下的==类、接口==
- 声明在包的声明和类的声明之间
- 如果需要导入多个结构，并列写出即可
- 如果在源文件中，使用了不同包下的同名的类，则必须至少有一个类需要以全名的方式显示



