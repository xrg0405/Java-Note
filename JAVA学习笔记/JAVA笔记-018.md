# JAVA笔记-018

[TOC]

## Properties处理属性文件

- Properties类是Hashtable的子类，该对象用于处理属性文件
- Properties里的key 和 Value 都是字符串类型的数据
- 存取数据是，建议使用setProperty( String key, String value)方法和getProperty(String key)方法

```java
Properties pros = new Properties();
pros.load(new FileInputStream("jdbc.properties"));
String user = pros.getProperty("user");
System.out.println(user);
```



## Collections工具类

- Collections是一个操作Set、List和Map等集合的工具类
- Collections中提供了一系列静态方法对集合元素进行排序、查询和修改等操作，还提供了对集合对象设置不可变、对集合对象实现同步控制等方法
- ==排序操作==（均为static方法）
  - `reverse(List)`：反转List中元素的顺序
  - `shuffle(List)`：对List集合元素进行随机排序
  - `sort(List)`：根据元素的自然顺序对指定List集合元素按升序排序
  - `sort(List, Comparator)`：根据指定Comparator产生的顺序对List集合元素进行排序
  - `swap(List, int, int)`：将指定List集合中的 i 处元素和 j 处元素进行交换



## JAVA版数据结构

- 树形结构
- 最短路径
- 搜索理论



## 泛型与File

- 泛型：可以理解为标签
- 集合容器类在设计阶段/声明阶段不能明确确定这个容器到底实际存的是什么类型的对象，所以引入泛型这个概念。因为这个时候除了元素的类型不确定，其他部分是确定的。把元素的类型设计成一个参数，这个类型参数叫做泛型



- 所谓泛型就是允许在定义类、接口时通过一个标识表示类中某个属性的类型或者是某个方面的返回值及参数类型。这个类型参数将在使用时确定

```java
public class GeneriTest{
  // 在集合中使用泛型之前的情况
  @Test
  public void test1(){
    ArrayList list = new ArrayList();
    // 需求：存放学生的成绩
    list.add(78);
    list.add(76);
    list.add(89);
    list.add(99);
    // 问题一：类型不安全
    list.add("Tom");
    
    for(Object score : list){
      // 问题二：强转时，可能出现ClassCastException
      int stuScore = (Integer)score;
      System,out,println(stuScore);
    }
  }
  
  // 在集合中使用泛型的情况
  @Test
  public void test2(){
    ArrayList<Integer> list = new ArrayList<Integer>();
    // 需求：存放学生的成绩
    list.add(78);
    list.add(76);
    list.add(89);
    list.add(99);
    // 编译时就会进行类型检查，保证数据安全
    // list.add("Tom");
    
    for(Integer score : list){
      // 避免了强转操作
      System.out.println(score);
    }
  }
  
  // 以HashMap为例
  @Test
  public void test3(){
    Map<String,Integer> map = new HashMap<String,Integer>();
    map.put("AA", 123);
    map.put("AC", 127);
    map.put("AD", 143);
    map.put("Tom", 153);
    
    // 泛型的嵌套
    Set<Map.Entry<String,Integer>> entry = map.entrySet();
    Iterator<Map.Entry<String, Integer>> iterator = entry.iterator();
    
    while(iterator.hasNext()){
      Map.Entry<String, Integer> e = iterator.next();
      String key = e.getKey();
      Integer value = e.getValue();
      System.out.println(key + "------" + value);
    }
    
  }
}
```

**在集合中使用泛型总结：**

1. 集合接口或者集合类在JDK5.0时都修改为带泛型的结构
2. 在实例化集合类时，可以致命具体的泛型类型
3. 指明完后，在集合类或者接口中凡是定义类或接口时，内部结构使用到类的泛型的位置，都指定为实例化时的泛型
4. ==泛型的类型必须是类，不能是基本的数据类型==
5. 如果实例化时没有指明泛型的类型，都默认为java.lang.Object类型



**泛型方法：在方法中出现了泛型的结构，泛型参数与类的方向参数没有任何关系**

**换句话说就是泛型方法所属的类是不是泛型都没有关系**
**泛型方法可以声明为静态，因为泛型参数是在调用方法是确定的，并非在实例化类的对象时确定**



## 通配符的使用

- 通配符：？

```java
list<?> list = null;
```

对于list<?>，不能向其添加数据



## File类的使用

- java.io.File类：文件和文件目录路径的抽象表示形式，与平台无关
- File能新建、删除、重命名文件和目录，当File不能访问文件内容本身。如果需要访问文件内容本身，则需要使用输入/输出流
- ==想要在Java程序中表示一个真实存在的文件或者目录，那么必须要有一个File对象，但是Java程序中的一个File对象，可能没有一个真实存在的文件或者目录==
- File对像可以作为参数传递给流的构造器

```java
public class FileTest{
  
  @Test
  public void test1(){
    // 构造器1
    File file1 = new File("文件目录");
    System.out.println(file1);
    
    // 构造器2
    File file2 = new File("文件路径"，"文件名")
    System.out.println(file2);
    
    // 构造器3
    File file3 = new File(文件（如file3），"文件名")
    System.out.println(file3);
  }
  
  @Test
  public void test2(){
    File file1 = new File("文件目录相对路径");
    System.out.println(file1.getAbsolutePath());
    System.out.println(file1.getPath());
    System.out.println(file1.getName());
    System.out.println(file1.getParent());
    System.out.println(file1.length());
    System.out.println(file1.lastModified());
    System.out.println();
    
    File file2 = new File("文件目录绝对对路径");
    System.out.println(file2.getAbsolutePath());
    System.out.println(file2.getPath());
    System.out.println(file2.getName());
    System.out.println(file2.getParent());
    System.out.println(file2.length());
    System.out.println(file2.lastModified()); 
  }
  
  @Test
  public void test3(){
    File file = new File("文件目录路径");
    
    String[] list = file.list();
    for(String s : list){
      System.out.println(s);
    }
    
    File[] files =file.listFiles();
    for(File f : files){
      System.out.println(f);
    }
  }
  
  @Test
  public void test4(){
    File file1 = new File("文件相对路径");
    File file2 = new File("文件绝对路径");
    
    boolean renameTo = file1.renameTo(file2);
    System.out.println(renameTo);
  }
  
  @Test
  public void test5(){
    File file1 = new File("文件路径");
    
    System.out.println(file1.isDirectory());
    System.out.println(file1.isFalse());
    System.out.println(file1.exists());
    System.out.println(file1.canRead());
    System.out.println(file1.canWrite());
    System.out.println(file1.isHidden());
  }
  
  @Test
  public void test6() throws IOException{
    // 文件的创建
    File file1 = new File("文件路径");
    if(!file1.exists()){
      file1.createNewFile();
      System.out.println("创建成功");
    }else{
      System.out.println("删除成功");
    }
  }
  
  @Test
  public void test7(){
    // 文件目录的创建
    File file1 = new File("文件路径");
    
    boolean mkdir = file1.mkdir();
    if(mkdir){
      System.out.println("创建成功");
    }
  }
  
}
```



