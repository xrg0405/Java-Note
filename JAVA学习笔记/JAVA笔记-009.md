# JAVA笔记-009

[TOC]

## 对多态性的理解

- 多态性的目的是尽可能地实现代码的通用性

- Object类中定义的public boolean equals(Object obj){.    }

  利用多态性，Object obj可以是任何Object类的子类的实例化对象。



## static关键字

- 当我们编写一个类时，其实就是在描述其对象的属性和行为，而并没有产生实质上的对象。
- 只有通过new关键字才会产生出对象，这时系统才会分配内存空间给对象，其方法才可以供外部调用。
- static可以用来修饰属性、方法、代码块、内部类

```java
public class StaticTest{
  public static void mian(String[] args){
    
    System.out.println(Chinese.nation);
    
    Chinese c1 = new Chinese();
    c1.name = "xiaoming";
    c1.age = 40;
    
    Chinese c2 = new Chinese();
    c2.name = "xiaohong";
    c2.age = 30;
    c2.nation = "China";
    
    System.out.println(c1.nation);
    
    Chinese.show();
  }
}

//中国人
class Chinese{
  
  String name;
  int age;
  static String nation;
  
  public void eat(){
    System.out.println("Chinese eat!");
  }
  public static void show(){
    System.out.println("I am chinese!");
  }
}
```

- 静态变量随着类的加载而加载
- 静态变量的加载早于实例变量
- 由于类只会加载一次，故静态变量在方法取得静态域中只存在一份
- ==静态方法中，只能调用静态的方法或属性；非静态方法中，既可以调用非静态的方法或属性，也可以调用静态的方法或属性。==



**在静态方法中，不能使用this关键字、super关键字**

