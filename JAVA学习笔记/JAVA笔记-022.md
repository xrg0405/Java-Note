# JAVA笔记-022

[TOC]

## 动态代理

- **代理模式的原理：**
  使用一个代理将对象包装起来，然后用该代理对象取代原始对象。任何对原始对象的调用都要通过代理。代理对象决定是否以及何时将方法调用转到原始对象上。
- 代理机制的操作属于静态代理，特征是代理类和目标对象的类都是在编译期间确定下来，不利于程序的扩展。同时没一个代理类只能为一个接口服务，这样程序开发中必然产生过多的代理。最好可以通过一个代理类完成全部的代理功能



- 动态代理是指客户通过代理类来调用其它对象的方法，并且是在程序运行时根据需要动态创建目标类的代理对象
- 动态代理使用场合：
  - 调试
  - 远程方法调用
- 动态代理相比于静态代理的优点：
  抽象角色中（接口）声明所有方法都被转移调用处理器一个集中的方法中处理，这样我们可以更加灵活和统一的处理众多的方法

```java
// 静态代理举例

interface ClathFactory{
  void produceCloth();
}

// 代理类
class ProxyClothFactory implements ClothFactory{
  
  private ClothFactory factory; // 用被代理类对象进行实例化
  
  public ProxyClothFactory(ClothFactory factory){
    this.factory = factory;
  }
  
  @Override
  public void ProduceCloth(){
    System.out.println("代理工厂做一些准备工作");
    fatory.produceCloth();
    System.out.println("代理工厂做一些后续的收尾工作");
  } 
}


// 被代理类
class NikeClothFactory implements ClothFactory{
  
  @Override
  public void produceCloth(){
    System.out.println("Nike工厂生产一批运动服");
  }
}


public class StaticProxyTest{
  public static void main(String[] args){
    //创建被代理类对象
    NikeClothFactory nike = new NikeClothFactory();
    //创建代理类的对象
    ProxyClothFactory proxyClothFatory = new ProxyClothFactory(nike);
    
    proxyClothFactory.produceCloth();
    
  }
}
```

```java
// 动态代理的举例

interface Human{
  String getBelief();
  void eat(String food);
}

// 被代理类
class SuperMan implements Human{
  
  @Override
  public String getBelief(){
    return "I believe I can fly!";
  }
  @Override
  public String eat(String food){
    System.out.println("我喜欢吃" + food);
  }
}

// 代理类
class ProxyFactory{
  // 调用此方法， 返回一个代理对象,解决办法一
  public static Object getProxyInstance(Object objet){
    MyInvocationHandler hander = new MyInvocationHandler();
    handler.bind(obj);
    return Proxyt.newProxyInstance(obj.getClass.getClassLoader(),obj.getClass.getInterface(),handler)
  }
}

class MyInvocationHandler implements InvocationHandler{
  
  private Object obj;
  public void bind(Object obj){
    this.obj = obj;
  }
  // 当我们通过代理类的对象调用方法a时，就会自动调用如下方法
  // 将被嗲里类要执行的方法的功能就声明在invoke()中
  @Override
  public Object invoke(Object proxy, Method method, Object[] args) throws Throwable{
    
    // method即为代理类对象调用的方法，此方法也就作为了被代理类对象要调用的方法
    Object returnValue = method.invoke(obj, args)
    return returnValue;
  }
}



public class proxyTest{
  public static void main(String[] args){
    SuperMan superMan = new SuperMan();
    //proxyInstance:代理类的对象
    Human proxyInstance = (Human)ProxyFactory.getProxyInstance(superMan);
    proxyInstance.getBelief();
    proxyInstance.eat("四川麻辣烫");
    
  }
}
```



## Lambda表达式

**并行流和串行流：**
==并行流==就是把一个内容分成多个数据块，并用不同的线程分别处理每个数据块的流。相较于==串行流==，并行流可以很大程度上提高程序的执行效率



**Nashorn引擎：**允许在JVM上运行JS应用



**Lambda表达式的使用：**

1. 举例：(o1, o2) -> Integer.compare(o1, o2);

2. 格式：
   ->：lambda操作符 或 箭头操作符

   ->左边：lambda形参列表（接口中的抽象方法的形参列表）

   ->右边：lambda体（重写的抽象方法的方法体）

3. lambda的本质：作为接口的实例

```java
public class lambdaTest1{
  // 语法格式一：无参，无返回值
  @Test
  public void Test1(){
    Runnable r1 = new Runnable(){
      @Override
      public void run(){System.out.println("This is one!");}
    };
    r1.run();
    System.out.println("+++++++++++++++++++++++++");
    
    Runnable r2 = () -> System.out.println("This is two!");
    r2.run();
  }
  
  // 语法格式二：lambda需要一个参数，但是没有返回值
  @Test
  public void test2(){
    Consumer<String> con = new Consumer<String>(){
      @Override
      public void accept(String s){System.out.println(s);}
    };
    con.accept("This is three!");
    System.out.println("+++++++++++++++++++++++++");
    
    Consumer<String> con1 = (String s) -> {System.out.println(s);};
    con1.accept("This is four!");
  }
  
  // 语法格式三：数据类型可以省略，因为可由编译器推断得出，称为“类型推断”
  @Test
  public void test3(){
    Consumer<String> con1 = (String s) -> {System.out.println(s);};
    con1.accept("This is five!");
    System.out.println("+++++++++++++++++++++++++");
    
    Consumer<String> con2 = (s) -> {System.out.println(s);};
    con2.accept("This is seven!");
  }
  
  // 语法格式四：Lambda 若只需要一个参数时，参数的小括号可以省略
  @Test
  public void test4(){
    Consumer<String> con1 = (String s) -> {System.out.println(s);};
    con1.accept("This is eight!");
    System.out.println("+++++++++++++++++++++++++");
    
    Consumer<String> con2 = s -> {System.out.println(s);};
    con2.accept("This is nine!");
  }
  
  // 语法格式五：Lambda需要两个或两个以上的参数，多条执行语句，并且可以有返回值
  @Test
  public void test5(){
    Comparator<Integer> com1 = new Comparator<Integer>(){
      @Override
      public int compare(Integer o1, Integer o2){
        System.out.println(01);
        System.out.println(o2);
        return o1.compareTo(o2);
      }
    };
    System.out.println(com1.compare(12,21));
    System.out.println("+++++++++++++++++++++++++");
    
    Comparator<Integer> com2 = (o1, o2) -> {
      System.out.println(01);
      System.out.println(o2);
      return o1.compareTo(o2);
    };
    System.out.println(com2.compare(12,6));
  }
  
  // 语法格式六：当Lambda体只有一条语句时，return与大括号若有，都可以省略
  @Test
  public void test6(){
    Comparator<Integer> com1 = (o1, o2) -> {return o1.compareTo(o2);};
    System.out.println(com1.compare(12, 6));
    System.out.println("+++++++++++++++++++++++++");
    
    Comparator<Integer> com1 = (o1, o2) -> o1.compareTo(o2);
    System.out.println(com1.compare(12, 6));
  }
}
```





## Stream API

- ==Stream API（java.util.stream）==把真正的函数式编程风格引入到Java中，这是目前为止Java类库最好的补充
- Stream API是Java 8 中处理集合的关键抽象概念，它可以指定你希望对集合进行的操作，可以执行非常复杂的查找、过滤和映射数据等操作
- 使用Stream API 对集合数据进行操作，就类似于使用SQL执行的数据库查询。
- 也可以使用Stream API来并行执行操作，简而言之，Stream API提供了一种高效且易于使用的处理数据的方式



**Stream和Collection集合的区别：**
==Collection是一种静态的内存数据结构，而Stream是有关计算的。==前者是主要面向内存，存储在内存中，后者主要是面向CPU，通过CPU实现计算



**注意：**

- Stream自己不会存储元素
- Stream不会改变源对象，相反，它们会返回一个持有结果的新Stream
- Stream操作是延迟执行的，这意味着它们会等到需要结果的时候才执行



**创建Stream操作的三个步骤：**

1. 创建Stream
   一个数据源（如：集合、数组），获取一个流
2. 中间操作
   一个中间操作链，对数据源的数据进行处理
3. 终止操作（终端操作）
   一旦终止操作，就执行中间操作链并产生结果，之后不会再被使用



