# JAVA笔记-021

[TOC]

## JAVA反射机制

- 发射（Reflection）被视为动态语言的关键，反射机制允许程序在执行期间借助Reflection API取得任何类内部信息，并能直接操作任意对象的内部属性及方法
- 加载完类之后，在堆内存的方法区中就产生了一个Class类型的对象（一个类只有一个class对象），这个对象就包含了完整的类的结构信息，我们可以通过这个对象看到类的结构。这个对象就像一面镜子，透过镜子看到类的结构，我们称之为反射



**正常方式：**

- 引入需要的包类名称$\to$通过new实例化$\to$获取实例化对象

**反射方式：**

- 实例化对象$\to$getClass()方法$\to$得到完整的包类名称



**JAVA反射机制提供的功能**

- 在运行时判断任意一个对象所属的类
- 在运行时构造任意一个类的对象
- 在运行时判断任意一个类所具有的成员变量和方法
- 在运行时获取泛型信息
- 在运行时调用任意一个对象的成员变量和方法
- 在运行时处理注解
- 生成动态代理



```java
public class ReflectionTest{
  // 反射之前对类的操作
  @Test
  public void test1(){
    Person p1 = new Person("Tom", 12);
    p1.age = 10;
    System.out.println(p1.toString());
    p1.show();
  }
  
  // 使用反射
  @Test
  public void test2() throws Exception{
    Class clazz = Person.class;
    // 1.通过反射创建对象
    Constructor cons = clazz.getConstructor(String.class, int.class);
    Object obj = cons.newInstance("Tom", 12);
    Person p = (Person)obj;
    System.out.println(p.toString());
    // 2.通过反射调用对象指定的属性方法
    Field age = clazz.getDeclaredField("age");
    age.set(p, 10);
    System.out.println(p.toString());
    
    Method show = clazz.getDeclaredMethod("show");
    show.invoke(p);
    
    // 通过反射可以 调用类的私有结构
    Constructor cons1 = clazz.getDeclaredConstructor(String.class);
    cons1.setAccessible(true);
    Person p1 = (Person)cons1.newInstance("Jerry");
    System.out.println(p1);
    
    Field name = clazz.getDeclaredField("name");
    name.setAccessible(true);
    name.set(p1, "HanMeimei");
    System.out.println(p1);
    
    Method showNation = clazz.getDeclaredMethod("showNation", String.class);
    showNation.setAccessible(true);
    String nation = showNation.invoke(p1, "中国");
    System.out.println(nation);
  }
}
```



## 反射与封装性

**反射机制与面向对象中的封装性是不是矛盾？如何看待这两个技术？**

- 不矛盾
- 封装性是能不能调的问题
- 反射机制是应不应该调的问题
- 如果恰好有需要，就应该用反射机制调用，相当于多添加了一个保障



**通过直接new的方式或反射的方式都可以调用公共结构，开发中到底用哪个？**

- 建议直接使用new的方式



## Class类的理解

**关于java.lang.Class类的理解：**

1. 类的加载过程：
   程序经过javac.exe命令后，会生成多个字节码文件（.class结尾），接着使用java.exe命令对某个字节码文件进行解释运行。相当于将某个字节码文件加载到内存中，此过程称为类的加载。加载到内存中的类被称为运行时类，此时运行类就充当了Class的一个实例
2. Class的实例就对应着一个运行时类
3. 加载到内存中的运行类会缓存一定的时间，在此时间内，我们可以通过不同的方式获取此运行时类



**哪些类型可以有Class对象？**

1. class：外部类、成员（成员内部类、静态内部类），局部内部类，匿名内部类
2. interface：接口
3. []：数组
4. enum：枚举
5. annotation：注解@interface
6. primitive type：基本数据类型
7. void



## 类的加载器

**类加载的作用：**

- 将class文件字节码内容加载到内存中，并将这些静态数据转换成方法区的运行时数据结构，然后在堆中生成一个代表这个类的java.lang.Class对象，作为方法区中类数据的访问入口

**类缓存：**

- 标准的JavaSE类加载器可以按照要求查找类，但一旦某个类被加载到类加载器中，它将维持加载（缓存）一段时间。不过JVM垃圾回收机制可以回收这些Class对象



1. 对于自定义类，使用系统类加载器进行加载
2. 调用系统类加载器的getParent()：获取扩展类记载器
3. 调用扩展类加载器的getParent()：无法获引导类加载器
4. 引导类加载器主要负责加载java的核心类库，无法加载自定义了的。



## 创建运行时类的对象

**在javabean中要求提供一个public的空参构造器，原因：**

1. 便于通过反射，创建运行时类的对象
2. 便于子类继承此运行类时，默认调用super()时，保证父类有此构造器



**框架 = 反射 + 注解 + 设计模式**



**反射应用：**

- 创建运行时对象
- 获取运行时类的完整结构
- 调用运行时类的指定结构
- 动态代理



