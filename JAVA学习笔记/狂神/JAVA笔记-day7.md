---

typora-copy-images-to: upload
---

# java笔记-day7

[TOC]

## 面向对象11:方法重写

- ![image-20211028093949813](https://tva1.sinaimg.cn/large/008i3skNgy1gvus1a8ukoj31og0ha779.jpg)



- **==重写：需要有继承关系，子类重写父类的方法==**
  1. 方法名必须相同
  2. 参数列表必须相同
  3. 修饰符：范围可以扩大，但不能缩小：  public > protected > default > private
  4. 抛出的异常：范围可以被缩小，但不能扩大：ClassNotFoundException----->Exception（大）
- **重写，子类的方法和父类必须一致；方法体不同**



- **为什么需要重写：**
  1. 父类的功能，子类不一定需要，或者不一定满足子类的实际需求
  2. Alt + insert     override



- **不能被重写的方法：**
  1. static方法，属于类，它不属于实例
  2. final 常量
  3. private方法



## 面向对象12:什么是多态

- **同一方法可以根据不同的发送对象，采取不同的行为方法，这就叫多态**
- **一个对象的实际类型是确定的，但可以指向对象的引用的类型有很多**



- 多态存在的条件
  - 有继承关系
  - 子类重写父类方法
  - 父类引用指向子类对象



- **==注意：多态是方法的多态，属性没有多态性==**
- **==子类重写了父类的方法，则执行子类的方法==**



- **多态注意事项：**
  1. 多态是方法的多态，属性没有多态
  2. 父类和子类有联系，类型转换异常！ClassCastException
  3. 存在条件：继承关系，方法需要重写，父类引用指向子类对象



## 面向对象13:instanceof和类型转换

- **instanceof：判断两个类之间是否存在继承关系**



- **类型转换**
  1. 父类引用指向子类的对象
  2. 把子类转换成父类，向上转换类型
  3. 把父类转换为子类，向下转换类型：强制转换



## 面向对象14:static关键字详解

- ![image-20211028102351856](https://tva1.sinaimg.cn/large/008i3skNgy1gvutb2v901j315m0l6wgg.jpg)



- ![image-20211028102438356](https://tva1.sinaimg.cn/large/008i3skNgy1gvutbvob35j31ec0qw41h.jpg)



## 面向对象15:抽象类

- **abstract修饰符可以用来修饰方法，也可以修饰类，如果修饰方法，那么该方法就是抽象方法；如果修饰类，那么该类就是抽象类**
- **抽象类中可以没有抽象方法，但是有抽象方法的类一定要声明为抽象类**



- **抽象类不能使用new关键字来创建对象，它是用来让子类继承的**
- **抽象方法只有方法的声明，没有方法的实现，它是用来让子类实现的**



- **子类继承抽象类，那么就必须要实现抽象类没有实现的抽象方法，否则该子类也要声明为抽象类**

- ![image-20211028103025408](https://tva1.sinaimg.cn/large/008i3skNgy1gvuthwrvlwj31e60nqtbz.jpg)



## 面向对象16:接口的定义与实现

- **普通类：只有具体实现**
- **抽象类：具体实现和规范（抽象方法）都有**
- **接口：只有规范**



- **接口就是规范，定义的是一组规则，体现了现实世界中“如果你是......则必须能........**
- **接口的本质是契约，制定好后大家在使用时都要去遵守**
- **oop的精髓就是对对象的抽象，最能体现这一点的就是接口。**



==声明类的关键字是class，声明接口的关键字是interface==



- **接口**
  1. 作为约束条件
  2. 可以让不同的人实现定义的一些方法
  3. 接口不能被实例化，接口中没有构造方法
  4. implement可以实现多个接口
  5. 必须要重写接口中的方法



## 面向对象17:N种内部类

- **内部类就是在一个类的内部再定义一个类，比如A类中定义一个B类，那么B类相对A类来说就是内部类，而A类相对B类来说就是外部类了**



- **内部类分类：**
  1. 成员内部类
  2. 静态内部类
  3. 局部内部类
  4. 匿名内部类

==一个java类中可以有多个class类，但是只能有一个public class类==



## 异常01:Error和Exception

- **异常指程序运行过程中出现的不期而至的的各种情况，其发生在程序运行期间，它影响了正常程序执行流程**



- **异常简单分类**

  ![image-20211028154424890](https://tva1.sinaimg.cn/large/008i3skNgy1gvv2ko916bj31700iitcr.jpg)

- **异常体系结构**
  ![image-20211028154540145](https://tva1.sinaimg.cn/large/008i3skNgy1gvv2lwqec9j31f00pmn0h.jpg)



- **Error**
  ![image-20211028154655642](https://tva1.sinaimg.cn/large/008i3skNgy1gvv2n86c7fj31hy0ke78p.jpg)

- **Exception**
  ![image-20211028154827641](https://tva1.sinaimg.cn/large/008i3skNgy1gvv2ouh45aj31hu0putey.jpg)



## 异常02:捕获和抛出异常

- **异常处理五个关键字**
  ==try、catch、finally、throw、throws==



```java
public class Test{
  public static void main(String[] args){
    int a= 1;
    int b = 0;
    try{//try监控区域
      System.out.println(a/b);
    }catch(Throwable e){//catch捕获异常
      System.out.println("程序出现异常，变量b不能为0");
    }finally{//处理善后工作
      System.out.println("finally");
    }
  }
}
```



## 异常03:自定义异常及经验小结

- **自定义异常**
  ![image-20211028160340367](https://tva1.sinaimg.cn/large/008i3skNgy1gvv34nmnvbj31800g2q6e.jpg)

  

- **实际应用中的经验**
  ![image-20211028160900540](https://tva1.sinaimg.cn/large/008i3skNgy1gvv3a8ydkaj316s0bq778.jpg)

  





