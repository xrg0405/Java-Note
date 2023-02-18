# JAVA笔记-015

[TOC]

## Java比较器

**JAVA实现对象排序的方式有两种：**

- 自然排序：==java.lang.Comparable==
- 定制排序：==java.util.Comparator==



```java
public class CompareTest{
  
  @Test
  public void test1(){
    String[] arr = new String[]{"AA", "CC", "KK", "MM", "GG", "JJ", "DD"};
    Arrays.sort(arr);
    System.out.println(Arrays.toString(arr));
  }
}
```

**封装成对象相当于装箱，通过重写Java的比价器，相当于重写一个工具，将对象拆箱，然后根据需要对对象的属性进行对比**

- Comparable接口的方式一旦一定，保证Comparable接口实现的对象在任何位置都可以比较大小
- Comparator接口属于临时性的比较



## BigInteger 与 BigDecimal

- Integer类作为int的包装类，能存储的最大整数型数值为$2^{31} -1$，Long类也是有限的，最大为$2^{63} -1$。如果要表示再大的整数，不管是基本类型数据还是它们的包装类都不能够满足条件
- java.math 包的BigInter可以表示==不可变的任意精度的整数==。BigInter提供所有Java的基本整数操作符的对应物，并提供java.lang.Math 的所有相关方啊。
- 另外BigInter还提供以下运算：模算术，GCD计算，质数测试，素数生成，位操作以及一些其他操作
- **构造器：**
  - **BigInteger(String val)：**根据字符串构建BigInteger 对象



## 枚举类

- ==类的对象只有有限个，确定的==；当需要定义一组常量时，强烈建议使用枚举类

```java
public class SeasonTest{
  public static void main(String[] args){
    Season spring = Season.SPRING;
    System.out.println(spring.toString);
  }  
}


class Season{
  // 声明season对象的属性
  private final String seasonName;
  private final String seasonDesc;
  
  // 私有化类的构造器，并给对象赋值
  private Season(String seasonName, seasonDesc){
    this.seasonName = seasonName;
    this.seasonDesc = seasonDesc;
  }
  
  // 提供当前枚举类的多个对象
  public static final Season SPRING = new Season("Spring"，"nice!");
  public static final Season SUMMER = new Season("Summer"，"hot!");
  public static final Season AUTUMN = new Season("Autumn"，"cool!");
  public static final Season WINTER = new Season("Winter"，"cold!");
  
  // 获取枚举类对象的属性
  public String getSeasonName(){
    return seasonName;
  }
  public String getSeasonDesc(){
    return seasonDesc;
  }
  @Override
  public String toString(){
    return "Season{seasonName=" + seasonName +", seasonDesc=" + seasonDesc;
  }
}
```



```java
public class SeasonTest{
  
}


enum Season{
   // 提供当前枚举类的多个对象
  SPRING("Spring"，"nice!"),
  SUMMER("Summer"，"hot!"),
  AUTUMN("Autumn"，"cool!"),
  WINTER("Winter"，"cold!");
  
  
  
  // 声明season对象的属性
  private final String seasonName;
  private final String seasonDesc;
  
  // 私有化类的构造器，并给对象赋值
  private Season(String seasonName, seasonDesc){
    this.seasonName = seasonName;
    this.seasonDesc = seasonDesc;
  }
  
  // 获取枚举类对象的属性
  public String getSeasonName(){
    return seasonName;
  }
  public String getSeasonDesc(){
    return seasonDesc;
  }
}
```



**Enum类的主要方法：**

- ==values()：==返回枚举类型的对象数组。该方法可以很方便地便利所有的枚举值
- ==valueOf(String str)：==可以把一个字符串转为对应的枚举类型。要求字符串必须是枚举类对象的名字。如果不是，会有运行时异常
- ==toString()：==返回当前枚举类对象常量的名称



## 注解

- 注解就是代码里的特殊标记，这些标记可以在编译，类加载，运行时被读取，并执行相应的处理。
- 通过使用注解，程序员可以在不改变原有逻辑的情况下在源文件中嵌入一些补充信息。
- 代码分析工具、开发工具和部署工具可以通过这些补充信息进行验证或部署
- **注解可以像修饰符一样被使用，可用于修饰包、类、构造器，方法、成员变量、参数和局部变量的声明。**这些信息被保存在Annotation的“ name = value ”对中

**框架 = 注解 + 反射 + 设计模式**



**在编译时进行格式检查（JDK内置的三个基本注解）**

- @Override ：限定重写父类方法，该注解只能用于方法
- @Deprecated：用于表示所修饰的元素（类，方法等）已经过时。通常是因为修饰的结构危险或存在更好的选择
- @SuppressWarnings：忽视编译器警告



**跟踪代码依赖性，实现代替配置文件功能**

- Servlet3.0 提供了注解（annotation），使得不再需要在web.xml文件中进行Servlet 的部署



**自定义注解：**

- 基本上不会使用
- 需要使用时再进行百度
- 如果注解有成员，在使用注解时，需要知明成员的值
- 自定义注解必须配上注解的信息处理流程（使用反射）才有意义



**元注解：**

- 对注解注解的注解





