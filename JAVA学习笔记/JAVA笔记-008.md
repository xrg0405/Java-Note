---
typora-copy-images-to: upload
---

# JAVA笔记-008

[TOC]

## 多态性

**理解多态性：**可以理解为一个事物的多种形态

**何为多态性：**

- 对象的多态性：父类的引用指向子类的对象（子类的对象赋给父类的引用）
- 多态的使用：当调用子父类同名同参的方法时，实际执行的是子类重写父类的方法--------虚拟方法调用

**多态的使用：**

- 有了对象的多态性以后，我们在编译期，只能调用父类中声明的方法，但在运行期，我们实际执行的是子类重写父类的方法。

  总结：编译看左边；运行看右边

**多态性的使用前提：**

- 有类的继承关系

- 有方法的重写

  

```java
public class Person{
  String name;
  int age;
  
  public void eat(){
    System.out.println("Person eat!");
  }
  public void walk(){
    System.out.println("Person walk!");
  }
}
```

```java
public class Man extends Person{
  boolean isSmoking;
  
  public void earnMoney(){
    System.out.println("earn money！"); 
  }
  
  //重写
  public void eat(){
    System.out.println("Man eat!");
  }
  public void walk(){
    System.out.println("Man walk!");
  }
}
```

```java
public class Woman extends Person{
  boolean isBeauty;
  
  public void goShopping(){
    System.out.println("go shopping!");
  }
  
  //重写
  public void eat(){
    System.out.println("Woman eat!");
  }
  public void walk(){
    System.out.println("Woman walk!");
  }
}
```

```java
public class PersonTest{
  public static void main(String[] args){
    Person p1 = new Person();
    p1.eat();
    
    Man man = new Man();
    man.eat();
    man.age = 25;
    man.earnMoney();
    
    //对象的多态性：父类的引用指向子类的对象
    Person p2 = new Man();
    p2.eat(); //调用子类的方法
    p2.walk();
  }
}
```



## 多态性的使用举例

```java
public class AnimalTest{
  public static void main(String[] args){
    AnimalTest test = new AnimalTest();
    test.func(new Dog());
    
    test.func(new Cat());
    
  }
  
  public void func(Animal animal){
    animal.eat();
    animal.shout();
  }
  
  //多态性能省略如下代码
  public void func(Dog Dog){
    Dog.eat();
    Dog.shout();
  }
  public void func(Cat Cat){
    Cat.eat();
    Cat.shout();
  }
}

class Animal{
  
  public void eat(){
    System.out.println("Animal eat!");
  }
  public void shout(){
    System.out.println("Animal shout!");
  }
}

class Dog extends Animal{
  
  public void eat(){
    System.out.println("Dog eat!");
  }
  public void shout(){
    System.out.println("Dog shout!");
  }
}

class Cat extends Animal{
  
  ublic void eat(){
    System.out.println("Dog eat!");
  }
  public void shout(){
    System.out.println("Dog shout!");
  }
}
```



## 多态性不适用于属性

- 多态性只适用于方法，不适用于属性
- 属性编译和运行都看左边



## 虚拟方法调用

**正常的使用方法**

```java
Person e = new Person();
e.getInfo();

Student e = new Student();
e.getInfo()
```

**虚拟方法调用（多态情况下）**

- 子类中定义了与父类同名同参的方法，在多态的情况下，将此时父类的方法称为虚拟方法
- 父类根据赋给它的不同子类对象，动态调用属于子类的该方法。这样的方法调用在编译期是无法确定的

```java
Person e = new Student();
e.getInfo(); //调用Student类的getInfo()方法
```

- 编译时类型和运行时类型：
  编译时e为Person类型，而方法的调用是在运行时确定的，所以调用的事Student类的getInfo()方法——动态绑定



==重写的重，是重新的重；重载的重，是重复的重==



## 向下转型地使用

- 有了对象的多态性后，内存中实际上是加载了子类特有属性和方法的，但是由于变量声明为父类类型，导致编译时只能调用父类中声明的属性和方法。
- 子类特有的属性和方法不能调用



**如何才能调用子类特有的属性和方法？**
使用强制类型转换符（精度有可能会发生损失或者转换失败）



**关键字instanceof：**
**a** instanceof **A**$\to$判断对象a是否是类A的实例。如果是，返回true，如果不是，返回false

**使用情景：**为了避免在向下转型时出现ClassCastException的异常，我们在向下转型之前，先进行instanceof的判断，一旦返回true，就进行向下转型。如果返回false，不进行向下转型。



## Object类的使用

- Object类是所有Java类的根父类
- 如果在类中声明未使用extends关键字指明其父类，则默认父类为java.lang.Object类
- Object类中的功能（属性、方法）具有通用性



## ==和equals()的区别

1. **回顾 == 的使用**
   - ==：运算符
   - 可以使用在基本数据类型变量和引用数据类型变量中
   - 如果比较的是基本数据类型，比较两个变量保存的数据是否相等（不一定类型要相同）
   - 如果比较的是引用数据类型变量，比较两个对象的地址值是否相同，即两个引用是否指向同一个对象实体
2. **equals()的使用方法**
   - equals()：方法
   - 只能用于引用数据类型
   - Object类中equals()的定义：

```java
public boolean equals(Object obj){
  return (this == obj);
}
```

​			说明：Object类中定义的equals()和 == 的作用是相同的

像String、Date、File、包装类等都重写了Object类中的equals()方法。重写以后，比较的不是两个引用地址是否相同，而是比较两个对象的实体内容是否相同。



- == 既可以比较基本类型，也可以比较引用类型。对于基本类型就是比较值，对于因引用类型，就是比较内存地址。
- equals是属于java.lang.Object类里面的方法，如果该方法没有被重写过，默认也是 ==；我们可以看到String等类的equals是被重写过的，而String类在日常开发中用的比较多。
- 具体要看自定义类型里有没有重写Object的equals方法来判断
- 通常情况下啊，重写equals方法，会比较类中相应的属性是否都相等。



## 重写equals()方法

```java
//重写的原则：比较两个对象的实体内容
@override
public boolean equals(Object obj){
  if(this == obj){
    return true;
  }
  if(obj instanceof Customer){
    Customer Cust = (Customer)obj;
    //比较两个对象的每个属性是否都相同
    if(this.age == cust.age && this.name.equals(cust.name)){
      return true;
    }else{
      return false;
    }
  }
  return false;
}
```



**重写equals()方法的原则：**

- 对称性：

  如果x.equals(y) 返回的是true，则y.equals(x) 返回的也是true

- 自反性：
  x.equals(x) 返回值必须是true

- 传递性：
  如果x.equals(y) 返回的是true，y.equals(z) 返回的是true，则x.equals(x) 返回的也是true

- 一致性：

  只要比较的内容不变，返回值永远是true

- 任何情况下，x.equals(null) ，永远返回false；null.equals(x) 、x.equals(和x不同类型的对象) 永远返回false



## toString()的使用

1. 当我们输出一个对象的引用时，实际上就是调用当前对象的toString()
2. 像String、Date、File、包装类等都重写了Object类中toString()方法，使得调用对象的toString()时，返回“实体内容”信息
3. 自定义类也可以重写toString()方法，当调用此方法时，返回对象的“实体内容”



## 单元测试方法的使用

- 对整体的代码分成一块一块进行测试
- 每一块代码为一个单元



## 包装类（Wrapper）的使用

- 针对八种基本数据类型定义相应的引用类型——包装类（封装类）
- 有了类的特点，就可以调用类中的方法，Java才是真正的面向对象

**基本数据类型对应的包装类**

- byte  $\to$  Byte
- short  $\to$  Short
- int  $\to$  Integer
- long  $\to$  Long
- float  $\to$  Float
- double  $\to$  Double
- boolean  $\to$  Boolean
- char  $\to$  Character

  ![image-20220302195834264](https://tva1.sinaimg.cn/large/e6c9d24ely1gzvsdl9vqzj21bq0k6juc.jpg)

```java
public class WrapperTest{
  //基本数据类型------>包装类：调用包装类的构造器
  @test
  public void test1(){
    int num1 = 10;
    Integer in1 = new Integer(num1);
    System.out.println(in1.toString());
    
    Integer in2 = new Integer("1234");
    System.out.println(in2.toString());
    
    Boolean b1 = new Boolean(true);
    Boolean b2 = new Boolean("true");
    
    Boolean b3 = new Boolean("true123");
    System.out.println(b3);
  }
  
  //包装类------->基本数据类型：调用包装类的xxxValue()
  @test
  public void test2(){
    Integer in1 = new Integer(12);
    int i1 = in1.intValue();
  }
  
  //自动装箱与拆箱
  @test
  public void test3(){
    //自动装箱
    int num2 = 10;
    Integer in1 = num2; 
    
    boolean b1 = true;
    Boolean b2 = b1;
    
    //自动拆箱
    System.out.println(int1.toString());
    it num3 = in1;
  }
  public void method(Object obj){
    System.out.println(obj);
  }
  
  //基本数据类型、包装类------->String类型
  @test
  public void test4(){
    int num1 = 10;
    //方式一，连接运算
    String str1 = num1+"";
    
    //方式二，调用String的valueOf(xxxxxx)
    float f1 = 12.3f;
    String str2 = String.valueOf(f1);
    System.out.println(str2);
  }
  
  //String类型------->基本数据类型、包装类：调用包装类的parseXxxx()方法
  @test
  public void test5(){
    String str1 = "1234";
    //错误方式
    int num1 = (int)str1;
    Integer in1 = (Integer)str1;
    
    //正确方式，可能会爆NumberFormatException
    int num2 = Integer.parseint(str1);
    System.out.println(num2 + 1);
  }
}
```



