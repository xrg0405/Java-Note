# JAVA笔记-016

[TOC]

## Java集合框架

Java集合可分为Collection 和 Map 两种体系

- ==Collection接口==：单列数据，定义了存取一组对象的方法的集合
  - ==List==：元素有序、可重复的集合
  - ==Set==：元素无序、不可重复的集合
- ==Map接口==：双列数据，保存具有映射关系“key-value对”的集合



**Collecton中常用的API**

```java
public class CollectionTest{
  
  @Test
  public void test1(){
    Collection coll = new ArrayList();
    
    // add() 方法
    coll.add("AA");
    coll.add("BB");
    coll.add(123);
    coll.add(new Date());
    
    // size() 方法
    System.out.println(coll.size());
    
    // addAll() 方法
    Collection collA = new ArrayList();
    collA.add(345);
    collA.add("CC");
    coll.addAll(collA);
    System.out.println(coll.size());
    
    // clean() 方法
    coll.clear();
    
    // isEmpty() 方法
    System.out.println(coll.isEmpty());
    
    // contains() 方法 判断当前集合中是否包含某个对象
    System.out.println(coll.contains(123));
    System.out.println(coll.contains("CBN"));
    
    // containsAll() 判断形参中的所有元素是否都存在当前集合中
    System.out.println(collA.containsAll(coll));
    
    // remove() 
    coll.remove("AA");
    System.out.println(coll);
    
    // removeAll() 从当前集合中移除指定集合中的所有元素
    collA.remove(coll);
    System.out.println(collA);
    
    // retainAll() 相当于求交集
    coll.retainAll(collA);
    System.out.println(coll);
    
    // equals() 判断两个集合（内容）是否一样
    
    // hashCode() 计算对象的哈希值
    
    // toArray() 集合转换为数组
    coll.toArray();
    
    // asList() 转换为List
    
    // iterator() 返回Iterator接口的实例，用于遍历集合元素
    
  }
}
```



## Iterator的使用

```java
public class iteratorTest{
  
  @Test
  public void test1(){
    Collection coll = new ArrayList();
    coll.add(123);
    coll.add(456);
    coll.add("AA");
    coll.add("BB");
    coll.add(false);
    
    Iterator iterator = coll.iterator();
    
    while(iterator.hasNext()){
      System.out.println(iterator.next());
    }
  }
  
  @Test
  public void test2(){
    Collection coll = new ArrayList();
    coll.add(123);
    coll.add(456);
    coll.add("AA");
    coll.add("BB");
    coll.add(false);
    
    Iterator iterator = coll.iterator();
    
    // remove 删除的是遍历中的内容，并不影响原集合内容
    while(iterator.hasNext()){
      Object obj = iterator.next();
      if("AA".equals(obj)){
        iterator.remove();
      }
      System.out.println(iterator.next());
    }
  }
}
```



## for each的使用

- For each用于遍历集合和数组，跟python里的差不多

e.g

```java
for(Person person: persons){
  System.out.pritnln(person.getName());
}
```



## List接口常用实现类的对比

- List集合类中元素有序、且可重复，集合中的每个牙素都有其对应的顺序索引
- List容器中的元素都对应一个整数型的序号记载其在容器中的位置，可以根据序号存取容器中的元素
- JDK API中List接口的实现类常用的有：ArrayList、LinkedList和Vector



```java
public class ListTest{
  
  @Test
  public void test1(){
    ArrayList list = new ArrayList();
    list.add(1);
    list.add(2);
    list.add(3);
    list.add(4);
    list.add(5);
    
    // add()
    list.add(1, "BB");
    System.out.println(list);
    
    // addAll()
    List list1 = Arrays.asList(1, 2, 3);
    list.addAll(list1);
    System.out.println(list);
    
    // get()
    System.out.println(list.get(0));
  }
  
  @Test
  public void test2(){
    ArrayList list = new ArrayList();
    list.add(1);
    list.add(2);
    list.add(3);
    list.add(4);
    list.add(5);
    
    // indexOf()
    System.out.println(list.indexOf(4));
    
    // remove()
    list.remove(2);
    
    // set()
    list.set(1, "CC");
    
    // sublist() 求左闭右开指定区间的list
  }
}
```

- ==ArrayList==：作为List接口的主要实现类；线程不安全，效率高，底层使用数组
- ==LinkedList==：对于频繁的插入、删除操作，使用此类效率比ArrayList高；底层使用双向链表
- ==Vector==：作为List接口的古老实现类；线程安全，效率低，底层使用数组



**常用方法：**

- 增  add(Object obj)
- 删  remove()
- 改  set()
- 查  get()
- 插入  add(int index, Objet obj)
- 长度  size()
- 遍历  iterator迭代器  foreach增强循环  普通循环



