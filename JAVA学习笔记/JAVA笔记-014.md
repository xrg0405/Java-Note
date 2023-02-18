# JAVA笔记-014

[TOC]

## String类

- String是一个final类，代表==不可变的字符序列==

- String对象的字符内容是存储在一个字符数组value[]中的

- String实现了
  Serializable接口：表示字符串是支持序列化的
  Comparable接口：表示Striing可以比较大小

- 当调用String的replace() 方法修改字符或字符串时，也需要重新指定内存区域赋值，不能使用原有的value进行赋值

  

**方法区，包含字符常量池**

**new是产生新的东西，两个对象在内存中的地址不同；字面量赋值，如果两个变量的值相同，则二者共用一个在内存中同一地址的该值**。



**String类的拼接：**

- 常量与常量的拼接结果在常量池。且常量池中不会存在相同内容的常量
- 只要其中有一个是变量，结果就在堆中
- 如果拼接的结果调用intern()方法，返回值就在常量池中



**String中常用的方法：**

- [点击跳转](https://www.runoob.com/java/java-string.html)



**String类与其他结构之间的转换：**

- String  $\to$ 基本数据类型、包装类：使用parseXxx(str) 方法
- 基本数据类型、包装类  $\to$ String：调用String重载的valueOf(xxxxx) 方法；加上“”
- String $\to$ Char[] ：char[] charArray = str1.toCharArray()
- Char[] $\to$ String ：调用String的构造器
- String $\to$ byte[] ：调用String的getBytes() 方法

```java
public class String StringTest{
  public void Test2(){
    String str1 = "abc123";
    
    char[] charArray = str1.toCharArray();
    for (int i = 0; i < charArray.length; i++){
      System.out.println(charArray[i]);
    }
    
    char[] arr = new char[]{'h', 'e', 'l', 'l', 'o'};
    String str2 = new String(arr);
    System.out.println(str2);
  }
  
  public void tes3(){
    String str1 = "abc123";
    byte[] bytes = str1.getBytes();
    System.out.println(Arrays.toString(bytes));
  }
}
```





## StringBuffer和StringBulider

- ==java.lang.StringBuffer==代表可变的字符序列，可以对字符穿内内容进行增删，此时不会产生新的对象

- 很多方法与String相同

- 作为参数传递时，方法内部可以改变值

  

**String、StringBuffer、StringBuilder三者的异同：**

- String为不可变字符序列，底层使用不可变**char型**数组进行存储
- StringBuffer为可变字符序列，**使用char型可变数组线存储**，程安全，但是效率低
- StringBulider为可变的字符序列，线程不安全，但是效率高

```java
public void test1(){
  StringBuffer sb1 = new StringBufer("abc");
  sb1.setCharAt(0, 'm');
  System.out.println(sb1);
  
  StringBuffer sb2 = new StringBuffer();
  System.out.println(sb2.length());
  
}
```

- **开发中建议使用StringBuffer 或StringBuilder**



**StringBuffer类的常用方法：**

- `append(xxx):`提供了很多的append() 方法，用于进行字符串拼接

- `delete(int start, int end):`删除指定位置的内容
- `replace(int start, int end, String str):`把[start, end) 的位置替换为str
- `insert(int offset, xxx):`在指定位置插入xxxx
- `reverse():`把当前字符序列逆转



**获取时间API：**

```java
public class DateTimeTest{
  
  @Test
  public void test1(){
    long time = System.currentTimeMillis();
    System.out.println(time);
  }
}
```

- ==java.util.Date类==
  表示特定的瞬间，精确到毫秒

- **构造器**

  - ==Date()==：使用无参构造器创建的对象可以获取本地当前时间

  - ==Date(long date)==

- **常用方法**

  - ==getTime()：==返回自1970年1月1日00:00:00 GMT以来此Date对象表示的毫秒数
  - ==toString()：==把Date对象转换为一下形式的String：dow mon dd hh:mm:ss zzz yyy



## SimpleDateFormat的使用

- ==java.text.SimpleDateFormat类==是一个不与语言环境有关的方式格式化和解析日期的具体类。
- 其允许进行格式化：日期$\to$文本；解析：文本$\to$日期
- **格式化：**
  - ==SimpleDateFormat()：==默认的模式和语言环境创建对象
  - ==public SimpleDateFormat(String pattern)：==该构造方法可以用参数pattern指定的格式创建一个对象
  - ==public String format(Date date)：==方法格式化时间对象date
- **解析：**
  - ==public Date parse(String source)：==从给定字符串的开始解析文本，以生成一个日期

```java
@Test
public void testSimpleDateFormat() throws ParseException{
  SimpleDateFormat sdf = new SipleDateFormat();
  
  Date date = new Date();
  system.out.println(date);
  
  String format = sdf.format(date);
  System.out.println(format);
  
  String str = "19-12-18 上午11:43";
  Date date1 = sdf.parse(str);
  System.out.println(date1);
  
  SimpleDateFormat sdf1 = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss");
  String format1 = sdf1.format(date);
  System.out.println(format1);
  
  Date date2 = sdf1.parse("2020-02-18 11:48:27");
  System.out.println(date2);
}
```

























