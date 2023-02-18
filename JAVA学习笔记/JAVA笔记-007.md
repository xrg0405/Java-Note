# JAVA笔记-007

[TOC]

## 方法的重写

定义：

- 在子类中可以根据需要对从父类继承来的方法进行改造，也称为方法的重置、覆盖。在执行程序时，子类的方法将覆盖父类的方法。

**要求：**

- 子类重写的方法必须和父类被重写的方法具有相同的方法名称、参数列表
- 子类重写的方法的返回值类型不能大于父类被重写的方法的返回值类型
- 子类重写的方法使用的访问权限不能小于父类被重写的方法的访问权限
  - 子类不能重写父类声明中为private权限的方法
- 子类方法跑出的异常不能大于父类被重写方法的异常

`子类与父类的同名参数的方法必须同时声明为非static的（即为重写），或者同时声明为static（不是重写）。因为static方法是属于类的，子类无法覆盖父类的方法。`  

```java
public class Person{
  String name;
  int age;
  
  public Person(){
    
  }
  public Person(String name, int age){
    this.name = name;
    this.age = age;
  }
  
  public void eat(){
    System.out.println("eat!");
  }
  public void walk(int distance){
    System.out.println("walk for "+ distance);
  }
}
```

```java
public class Student extends Person{
  String major;
  
  public Student(){
    
  }
  public Student(String major){
    this.major = major;
  }
  
  public void study(){
    System.out.println("study! major is "+major);
  }
  //对父类中的方法进行重写
  public void eat(){
    System.out.println("eat!！！！！！！");
  }
}
```

```java
public class PersonTest{
  public static void main(String[] args){
    Student s = new Student("chinese");
    s.eat();
    s.walk(10);
    
    s.study();
    
    Person p1 = new Person();
    p1.eat();
  }
}
```

1. 重写：子类继承父类以后，可以对父类中同名参数的方法进行覆盖操作
2. 应用：重写以后，当创建子类对象后，通过子类独享调用子父类中同名同参的方法·时，实际执行的是值了重写写父类的方法



## 四种权限修饰符

JAVA权限修饰符public、protected、（缺省）、private置于类的成员定义前，用来限定对象对该类成员的访问权限

- 对于class的权限修饰只可以用public和default（缺省）
  - public类可以在任意地方被访问
  - default类只可以被同一个包内部的类访问

```java
public class Order{
  
  private int orderPrivate;
  int orderDefault;
  protected int orderProtected;
  public int orderPublic;
  
  private viod methodPrivate(){
    orderPrivate = 1;
    orderDefault = 2;
    orderProtected = 3;
    orderPublic = 4;
    
  }
  void methodDefalut(){
    orderPrivate = 1;
    orderDefault = 2;
    orderProtected = 3;
    orderPublic = 4;
  }
  protected void menthodProtected(){
    orderPrivate = 1;
    orderDefault = 2;
    orderProtected = 3;
    orderPublic = 4;
  }
  public void methodPublic(){
    orderPrivate = 1;
    orderDefault = 2;
    orderProtected = 3;
    orderPublic = 4;
  }
}
```



## super关键字

- super理解为：父类的xxx
- super可以用来调用：属性、方法、构造器



- 我们可以在子类的方法或构造器中，通过使用“super.属性“或”super.方法“的方式，显式地调用父类中声明的属性或方法。但是通常情况下，我们习惯省略”super.“
- **super调用构造器**
  - 我们可以在子类的构造器中显式的使用“super（形参列表）”的方式，调用父类中声明的指定的构造器。
  - “Super(形参列表)” 的使用，必须声明在子类构造器的首行。
  - 我们在类的构造器中，针对于“this(形参列表)"或者“super(形参列表)"只能二选一，不能同时出现
  - 在构造器的首行，没有显示的声明，默认调用的父类是空参列表的构造器。
  - 在类的多个构造器中，至少有一个类的构造器使用了“super（形参列表）”，调用父类的构造器

```java
public class Person{
  String name;
  int age;
  int id;//身份证号
  
  public Person(){
    
  }
  public Person(String name){
    this.name = name;
  }
  public Person(String name, int age){
    this.name = name;
    this.age = age;
  }
  
  public void eat(){
    System.out.println("eat some thing!");
  }
  public void walk(){
    System.out.println("walk!");
  }
}
```

```java
public class Student extends Person{
  String major;
  int id;//学号
  
  public Student(){
    
  }
  public Student(String major){
    this.major = major;
  }
  public Student(String name, int age, String major){
    //this.name = name;
    //this.age = age;
    
    
    //调用父类中的构造器
    super(name, age);
    this.major = major;
  }
  
  @override
  public void eat(){
    System.out.println("student eat!");
  }
  
  public void study(){
    System.out.println("student study!");
  }
  
  public void show(){
    System.out.println("student id = "+this.id+"Person id = "+super.id);
  }
}
```

```java
public class SuperTest{
  public static void main(Sting[] args){
    
    Student s = new Student();
    s.show();
    
    Student s1 = new Student("Tom", 21, "IT");
    s1.show();
  }
}
```



## 子类对象的实例化的过程

1. 从结果上来看：（继承性）
   - 子类继承父类以后，就获取了父类中声明的属性或方法
   - 创建子类的对象，在堆空间中就会加载所有父类中声明的属性
2. 从过程上来看：
   - 当我们通过子类的构造器创建子类对象时，我们一定会直接或间接地调用其父类的构造器，进而调用父类的父类的构造器，知道调用了java.lang.object类中空参的构造器为止。正因为加载过所有的父类结构，所以才可以看到内存中有父类中的结构，子类对象才可以进行调用。
   - ==虽然创建子类对象时，调用了父类的构造器，但是自始至终就创建了一个对象，即new的对象。==

```java
public class Account{
  private int id; //账号
  private double balance; //余额
  private double annualInterestRate; //年利率
  
  public Account(int id, double balance, double annualInterestRate){
    super();
    this.id = id;
    this.balance = balance;
    this.annualInterestRate = annualInterestRate;
  }
  
  public int getId(){
    return id;
  }
  public double getBalance(){
    return balance;
  }
  public double getAnnualInterestRate(){
    return annualInterestRate;
  }
  public void setId(int id){
    this.id = id;
  }
  public void setBalance(double balance){
    this.balance = balance;
  }
  public void setAnnualInterestRate(double annualInterestRate){
    this.annualInterestRate = annualInterestRate;
  }
  
  //返回月利率
  public double getMonthlyInterest(){
    return annualInterestRate /12;
  }
  public void withdraw(double amount){
    if(balance >= amount){
      balance -= amount;
      return;
    }
    System.out.println("余额不足");
  }
  //存钱
  public void deposit(double amount){
    if(amount > 0)
      balance += amount;
  }
  
}
```

```java
public class AccountTest{
  public static void main(String[] args){
    Account acct = new Account(1122, 20000, 0.045);
    
    acct.withdraw(30000);
    System.out.println("你的账户余额为：" + acct.getBalance());
    acct.withdraw(2500);
    System.out.println("你的账户余额为：" + acct.getBalance());
    acct.deposit(3000);
    System.out.println("你的账户余额为：" + acct.getBalance());
    
    System.out.println("月利率为；" + acc.ggetMonthlyInterest());
  }
}
```

```java
public class CheckAccount extends Account{
  
  private double overdraft; //可透支额度
  
  public CheckAccount(int id, double balance, double annualInterestRate, double overdraft){
    super(id, balance, annualInterestRate);
    this.overdraft = overdraft;
  }
  
  public double getOverdraft(){
    return overdraft;
  }
  
  public void withdraw(double amount){
    if(getBalance() >= amount){ //余额足够
      //setBlance(getBalance() - amount);
      super.withdraw(amount); 
    }
    else if(overdraft >= amount -getBlance()){//透支额度足够消费
      overdraft -= (amount -getBalance());
      setBalance(0); 
    }else{
      System.out.println("超出可透支额度！");
    }
  }
  
  
}
```

```java
public class AccountTest{
  public static void main(String[] args){
    Account acct = new Account(1122, 20000, 0.045, 5000);
    
    acct.withdraw(5000);
    System.out.println("你的账户余额为：" + acct.getBalance());
    System.out.println("你的可透支额度为：" + acct.getOverdraft()); 
    
    acct.withdraw(18000);
    System.out.println("你的账户余额为：" + acct.getBalance());
    System.out.println("你的可透支额度为：" + acct.getOverdraft()); 
    
    acct.withdraw(3000);
    System.out.println("你的账户余额为：" + acct.getBalance());
    System.out.println("你的可透支额度为：" + acct.getOverdraft());  
  }
}
```

