# JAVA笔记-006

[TOC]

## 继承性的理解

**继承性的好处**

- 减少了代码的冗余，提高代码的复用性
- 便于后续功能的拓展
- 为之后多态性的使用提供了前提

```java
public class Person{
  String name;
  int age;
  
  public Person{
    
  }
  
  public Person(String name, int age){
    this.name = name;
    this.age =age;
  }
  
  public void eat(){
    System,out.println("吃饭！");
  }
  
  public void sleep(){
    System.out.println("睡觉！");
  }
}
```

```java
public class Student{
  String name;
  int age;
  String major;
  
  public Student(){
    
  }
  
  public Student(String name, int age, String major){
    this.name = name;
    this.age = age;
    this.major = major;
  }
  
  public void eat(){
    System,out.println("吃饭！");
  }
  
  public void sleep(){
    System.out.println("睡觉！");
  }
  
  public void study(){
    System.out.println("学习！");
  }
  
}
```

```java
public  class ExtendsTest{
  public static void main(String[] args){
    Person p1 = new Person;
    p1.age = 1;
    p1.eat();
    
    Student s1 = new Student();
    s1.eat();
    s1.sleep();
  }
}
```

```java
public class Student extends Person{
  //String name;
  //int age;
  String major;
  
  public Student(){
    
  }
  
  public Student(String name, int age, String major){
    this.name = name;
    this.age = age;
    this.major = major;
  }
  
  //public void eat(){
   //System,out.println("吃饭！");
  //}
  
  //public void sleep(){
    //System.out.println("睡觉！");
  //}
  
  public void study(){
    System.out.println("学习！");
  }
  
}
```

## 继承性的使用

- 继承性格式：class A extends B{}
  - A：子类、派生类、subclass
  - B：父类、超类、基类、superclass
  - 一旦子类A继承了父类B以后，子类A中就获取了父类B中声明的结构：属性、方法
- **子类继承父类后，还可以声明自己特有的属性或方法，实现功能的拓展。**

## 继承性的再说明

**为什么要有继承：**

- 多个类中存在相同属性和行为时，将这些内容抽取到一个单独的类中，那么多个类无需再定义这些属性和行为，只要继承那个类即可。

**相关规定：**

- ==JAVA只支持单继承和多层继承，不允许多重继承==
  - 一个子类只能有一个父类
  - 一个父类可以派生出多个子类

```java
public class Mankid{
  private int sex;
  private int salary;
  
  public Mankind{
    
  }
  
  public ManKind(int sex, int salary){
    this.sex = sex;
    this.salary = salary;
  }
  
  public void manOrWoman(){
    if(sex == 1)
      System.out.println("man");
    else if(sex == 0)
      system.out.println("woman");
  }
  
  public void employeed(){
    if(salary == 0)
      System.out.println("no job");
    else
      System.out.println("job");
  }
}




public class Kids extends ManKid{
  private int yearsold;
  
  public Kids{
    
  }
  
  public Kids(int yearsOld){
    this.yearsOld = yearsOld;
  }
  
  public void printAge(){
    System.out.println("I am "+yearsold+" years old");
  }
  
  public int getYearsold(){
    return yearsOld;
  }
  
  public void setYearsOld(int yearsOld){
    this.yearsOld = yearsOld;
  }

}




public class KidsTest{
  public static void main(String[] args){
    Kids someKid = new Kids(12);
    someKid.printAge();
    someKid.setSalary(0);
    someKid.setSex(1);
    
    someKid.employeed();
    someKid.manOrWoman();
  }
}
```



