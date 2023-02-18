# JAVA笔记-017

[TOC]

## Set结构

- **Collection接口：单列集合，用来存储一个一个的对象**
  - Set接口：存储无序的、不可重复的数据
    - HashSet：作为Set接口的主要实现类；线程不安全；可存储null值
    - LinkedHashSet：作为HashSet的子类；遍历其内部数据时，可以按照添加时的顺序遍历
    - TreeSet：可以按照添加对象的指定属性进行排序



- **无序性：**不等于随机性。存储的数据在底层数组中并非按照数组索引的顺序添加，而是根据数据的哈希值
- **不可重复性：**保证添加的元素按照equals判断时，不能返回true。即：相同元素只能添加一个

```java
public class SetTest{
  
  @Test
  public void test1(){
    Set set = new HashSet();
    set.add(456);
    set.add(123);
    set.add(457);
    set.add(129);
    set.add("AA");
    set.add("CC");
    
    Iterator iterator = set.iterator();
    while(iterator.hasNext()){
      System.out.println(iterator.next());
    }
  }
}
```

- **添加元素的过程：**
  - 我们向HashSet中添加元素a，首先调用元素a所在类的hashCode方法，计算其哈希值
  - 此哈希值接着通过某种算法计算出a在HashSet底层数组中存放的位置（索引位置），判断数组在此位置上是否已经有其他元素
  - 如果此位置上没有其他元素，则元素a添加成功
  - 如果此位置上有其他元素b，则比较元素a与b的哈希值；如果哈希值不同，则元素a添加成功；如果哈希值相同，进而需要调用元素a所在类的equals方法，equals方法返回true，则添加成工，返回false，则添加失败



**重写HashCode()方法的基本原则：**

- 在程序运行时，同一个对象多次调用hashCode() 方法应该返回相同的值
- 当两个对象地equals() 方法比较返回true时，这两个对象的hashCode() 方法的返回值也应相等
- 对象中用作equals() 方法比较的Field，都应该用来计算hashCode值



**向TreeSet中添加的数据要求是相同类的对象**

```java
public class TreeSetTest{
  
  @Test
  public void test1(){
    TreeSet set = new TreeSet();
    set.add(456);
    set.add(123);
    set.add(457);
    set.add(129);
    
    //不能添加不同类的对象
    //set.add("AA");
    //set.add("CC");
    
     Iterator iterator = set.iterator();
    while(iterator.hasNext()){
      System.out.println(iterator.next());
    }
  }
}
```



## Map实现类的结构

- **Map：**双列数据，存储key-value对数据



- ==HashMap:== 作为map的主要实现类；线程不安全，效率高；可以存储null的key和value
  - LinkwdHashMap: 保证在遍历map元素时可以按照添加的顺序实现遍历；因为在原有的HashMap底层结构基础上，添加了一对指针，指向前一个元素和后一个元素；对于频繁的遍历操作，此类执行效率高于HashMap
- TreeMap: 保证按照添加的key-value对进行排序，实现排序遍历；底层使用红黑树
- Hashtable: map的古老类，现在基本不使用；线程安全，效率低
  - Properties: 常用来处理配置文件。key和value都是String类型。



**HashMap的底层：**数组+i链表（JDK7及之前）；数组+链表+红黑树（JDK8）

```java
public class MapTest{
  
  @Test
  public void test1(){
    Map map = new HashMap();
    map.put(null, null);
    
    //此处会报错
    //Map map = new Hashtable();
    //map.put(null, null);
  }
}
```



## Map结构的理解

- map中的key是无序的，不可重复的，使用set存储所有的key
- map中的value是无序的，但是可以重复，使用collection存储
- 一个键值对 key-value构成了一个Entry对象
- map中的Entry是无序的，不可重复的，使用set存储所有的Entry



## HashMap的底层实现原理（JDK7为例）

`HashMap map = new HashMap()；`

在实例化以后，底层创建了长度是16的一维数组Entry[] table；

`map.put(key1, value1);`

首先调用key1 所在类的hashCode() 计算key1 哈希值，此哈希值经过某种算法计算后，得到在Entry数组中的存放位置；如果此位置上对的数据为空，此时key1-value1添加成功；如果位置上不为空，（意味着此位置上存在一个或多个数据（以链表的形式存在）），比较key1 和已经存在的一个或多个数据的哈希值：

1. 如果key1 的哈希值与已经存在的数据的哈希值都不相同，此时key1-value1添加成功
2. 如果key1 的哈希值与已经存在的数据的哈希值都相同，继续比较：调用key1所在类的equals()，如果返回false，添加成功；如果返回true，使用value1替换value2.



在添加过程中，会涉及到扩容问题，默认的扩容方式为扩容为原来容量的2倍，并将原有的数据复制过来。



**Jdk 8相较于JDK7在底层实现方面的不同：**

1. new HashMap() ：底层没有创建一个长度为16的数组
2. Jdk8 底层的数组是：Node[],，而非Entry[]
3. 首次调用put() 方法时，底层会创建长度为16的数组
4. Jdk7底层结构只有数组+链表；jdk8中是数组+链表+红黑树（当数组的某一个索引位置上的元素以链表形式存在的数据个数 > 8 且当前数组的长度 > 64时，此时此索引位置上的所有数据改为使用红黑树存储）



## Map中常用的方法

```java
public class MapTest{
  
  @Test
  public void test1(){
    Map map = new HashMap();
    //添加
    map.put("AA", 1234);
    map.put("Aa", 1134);
    map.put("As", 14);
    map.put("Ac", 12134);
    //修改
    map.put("AA", 1224);
    System.out.println(map);
    
    Map map1 = new HashMap();
    map1.put("CC", 123);
    map1.put("ss", 45654);
    map.putAll(map1);
    System.out.println(map);
    
    Object value = map.remove("CC");
    System.out.println(value);
    System.out.println(map);
    
    map.clear();
    System.out.println(map.size());
  }
  
  @Test
  public void test2(){
    Map map = new HashMap();
    //添加
    map.put("AA", 1234);
    map.put("Aa", 1134);
    map.put("As", 14);
    map.put("Ac", 12134);
    
    System.out.println(map.get("AA"));
    
    System.out.println(map.containsKey("BB"));
    
    System.out.println(map.containsValue("1234"));
    
    System.out.println(map.isEmpty());
  }
  
  @Test
  public void test3(){
    Map map = new HashMap();
    //添加
    map.put("AA", 1234);
    map.put("Aa", 1134);
    map.put("As", 14);
    map.put("Ac", 12134);
    
    // 遍历所有的key
    Set set = map.KeySet();
    Iterator iterator = set.iterator();
    while(iterator.hasNext()){
      System.out.println(iterator.next());
    }
    
    // 遍历所有的value
    Collection values = map.values();
    Iterator iterator = values.iterator();
    while(iterator.hasNext()){
      System.out.println(iterator.next());
    }
    
    // 遍历所有的key-value
    // 方式1
    Set entrySet = map.entrySet();
    Iterator iterator = entrySet.iterator();
    while(iterator.hasNext()){
      System.out.println(iterator.next().getKey()+" "+iterator.next().getValue());
    }
    // 方式2
    Set keySet = map.keySet();
    Iterator iterator2 = keySet.iterator();
    while(iterator2.hasNext()){
      Object key = iterator2.next();
      Object value = map.get(key);
      System.out.println(key + "==" + value);
    }
    
  }
}
```



**常用方法总结：**

- 添加：put(key ， value)
- 删除：remove( key )
- 修改：put( key ,  value)
- 查询：get( key )
- 长度：size( )
- 遍历：keySet( ), values( ), entrySet( )

