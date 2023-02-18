# JAVA笔记-013

[TOC]

## 线程的生命周期

- 指线程从创建到消亡的过程

**线程的5个状态：**

- 新建
- 就绪
- 运行
- 阻塞
- 死亡



**线程的不安全问题**

- 多个线程执行不确定性引起执行结果的不稳定
- 多个线程对账本的共享会造成操作的不完整性，会破坏数据



## 线程的同步机制

- **方式一：同步代码块**

  ```java
  synchronized(同步监视器){
    //需要被同步的代码
  }
  说明：操作共享数据的代码，即为需要被同步的代码
    	 共享数据：多个线程共同操作的变量
    	 同步监视器：俗称“锁”，任何一个类的对象都可以充当锁
    	 要求：多个线程必须要共同用一把锁
  ```

  **补充：**在实现Runnable接口创建多线程的方式中，我们可以考虑使用this充当同步监视器

  在继承Thread类创建多线程的方式中，慎用this充当同步监视器

- **方式二：同步方法**
  如果操作共享数据的代码完整的生命在一个方法中，我们不妨将此方法生命为同步的。

  1. 同步方法仍然涉及到同步监视器，只是不需要我们显示地声明
  2. 非静态的同步方法，同步监视器是this；静态的同步方法，同步监视器是当前类本身

  ```java
  private synchronized void show(){
    //需要同步的代码
    //此时同步监视器为this
  }
  
  private static synchronized void show(){
    //此时监视器为本类
  }
  ```

  

```java
public class bankTest{
  
}

class Bank{
  private Bank(){}
  
  private static Bank instance = null;
  
  //线程安全
  public static synchronized Bank getinstance(){
    if (instance == null){
      instance = new Bank();
    }
    return instance;
  }
}
```

```java
public class bankTest{
  
}

class Bank{
  private Bank(){}
  
  private static Bank instance = null;
  
  //线程安全
  public static Bank getinstance(){
    //方式一：效率稍差
    synchronized (Bank.class){
      if (instance == null){
        instance = new Bank();
      }
      return instance;
    } 
    //方式二：效率比方式一要好
    if (instance == null){
      synchronized (Bank.class){
        if (instance == null){
          instance = new Bank();
        }
      }
    }
    return instance;
  }
}
```



## 线程的死锁问题

**死锁：**

- 不同的线程分别占用对方需要的同步资源不放弃，都在等待对方放弃自己需要的同步的资源，就形成了线程的死锁
- 出现死锁后，不会出现异常，不会出现提示，只是所有的线程都处于阻塞状态，无法继续

**解决方法：**

- 专门的算法、原则
- 尽量减少同步资源的定义
- 尽量避免嵌套同步



**死锁示例代码：**

```java
public class ThreadTest{
  public static void main(String[] args){
    StringBuffer s1 = new StringBuffer();
    StringBuffer s2 = new StringBuffer();
    
    
    new Thread(){
      @Override
      public void run(){
        synchronized(s1){
          s1.append("a");
          s2.append("1");
          
          try{
            Thread.sleep(100);
          } catch (InterruptedException e){
            e.printStackTrace();
          }
          
          synchronized(s2){
            s1.append("b");
            s2.append("2");
            System.out.println(s1);
            System.out.println(s2);
          }
        }
      }
    }.start();
    
    new Thread(new Runnable(){
      @Override
      public void run(){
        synchronized(s2){
          s1.append("c");
          s2.append("3");
          
           try{
            Thread.sleep(100);
          } catch (InterruptedException e){
            e.printStackTrace();
          }
          
          synchronized(s1){
            s1.append("d");
            s2.append("4");
            System.out.println(s1);
            System.out.println(s2);
          }
        }
      }
    }).start();
  }
}
```



## Lock锁

- 可以通过显式定义同步锁对象来实现同步。同步锁使用Lock独享充当
- ==java.util.concurrent.locks.Lock==接口是控制多个线程对共享资源进行访问的工具。
- 锁提供了对共享资源的独占访问，每次只能有一个线程对Lock独享加锁，线程开始访问共享资源之前应先获得Lock对象
- ==ReentrantLock==类实现了Lock，它拥有与synchronized相同的并发性和内存语义，在实现线程安全的控制中，比较常用的是ReentrantLock，可以显式加锁、释放锁

```java
class Window implements Runnale{
  private int ticket = 100;
  
  private ReentrantLock lock = new ReentrantLock(); 
  
  @Override
  public void run(){
    while(true){
      try{
        lock.lock();
        
        if(ticket > 0){
          try{
            Thread.sleep(100);
          } catch (InterruptedException e){
            e.printStackTrace();
          }
          
          System.out.println(Thread.currentThread().getName() + ": " + ticket);
          ticket--;
       } else
         	break;
      }
    }finally{
      lock.unlock;
    }
      
  }
}

public class LockTest{
  public static void main(String[] args){
    Window w = new Window();
    
    Thread t1 = new Thread(w);
    Thread t2 = new Thread(w);
    Thread t3 = new Thread(w);
    
    t1.setName("窗口1");
    t2.setName("窗口2");
    t3.setName("窗口3");
    
    t1.start();
    t2.start();
    t3.start();
  }
}
```



**synchronized 与 Lock 方式的异同：**

- 二者都可以解决线程安全问题
- synchronized 机制在执行完相应的同步代码块后，自动释放同步监视器；Lock需要手动启动同步，同时结束同步也需要手动来实现

**优先使用顺序：**

1. Lock
2. 同步代码块（已经进入方法体，分配了相应资源）
3. 同步方法（在方法体之外）



## 线程的通信

```java
class Number implements Runnalbe{ 
  private int number = 1;
  
  @Override
  public void run(){
    while (true){
      
      synchronized (this){
        
        notifyAll();
        
        if (number <= 100){
          Thread.sleep(100);
          System.out.println(Thread.currentThread().getName() + ":" + number);
          number++;
          
          // 调用使得如下wait()方法的线程进入阻塞状态
          try{
            wait();
          } catch (InterruptedException e){
            e.printStackTrace();
          }
        } else{
          break;
        }
      }
    }
  }
}
public class CommunicationTest{
  public static void mian(String[] args){
    Number number = new Number();
    Thread t1 = new Thread(number);
    Thread t2 = new Thread(number);
    
    t1.setName("线程1");
    t2.setName("线程2");
    
    t1.start();
    t2.start();
    
  }
}
```



**sleep()方法和wait()方法的异同：**

- 一旦执行方法，都可以使得当前的线程进入阻塞状态。
- 两个方法声明的位置不同：Thread类中声明sleep()，object类中声明wait()
- 调用的请求不同：sleep() 可以在任何需要的场景下调用，wait() 必须使用在同步代码块中
- 关于是否释放同步监视器：如果两个方法都使用在同步代码块或同步方法中，sleep() 不会释放锁，wait() 会释放锁



```java
// 生产者/消费者问题

class Clerk{
  private int productCount = 0；
  //生产产品
  public void produceProduct(){
    if (productCount < 20){
      productCount++;
      System.out.println(Thread.currentThread().getName() + ": 开始生产第" + productCount +"个产品");
      notify();
    } else{
      //等待
      try{
        wait();
      } catch(InterruptedException e){
        e.printStackTrace();
      }
    }
  }
  
  //消费产品
  public void consumeProduct(){
    if (productCount > 0){
      System.out.println(Thread.currentThread().getName() + ": 开始消费第" + productCount +"个产品");
      productCount--;
      notify();
    } else{
      //等待
      try{
        wait();
      } catch(InterruptedException e){
        e.printStackTrace();
      }
    }
  }
  
}

class Producer extends Thread{ //生产者
  
  private Clerk clerk;
  
  public Producer(Clerk clerk){
    this.clerk = clerk;
  }
  
  @Override
  public void run(){
    System.out.println( getName() + ": 开始生产产品.....");
    
    while(true){
      try{
        Thread.sleep(100);
      } catch (InterruptedException e){
        e.printStackTrace();
      }
      clerk.produceProduct();
    }
  }
}

class Consumer extends Thread{ //消费者
  
  private Clerk clerk;
  
  public Producer(Clerk clerk){
    this.clerk = clerk;
  }
  
  @Override
  public void run(){
    System.out.println(getName() + ": 开始消费产品.....");
    
    while(true){
      try{
        Thread.sleep(100);
      } catch (InterruptedException e){
        e.printStackTrace();
      }
      clerk.consumerProduct();
    }
  }
}

public class ProductTest{
  public static void mian(String[] args){
    Clerk clerk = new Clerk();
    
    Producer p1 = new Producer(clerk);
    p1.setName("生产者1");
    
    Consumer c1 =new Consumer(clerk);
    c1.setName("消费者1");
    
    p1.start();
    c1.start();
  }  
}
```



**创建线程的方式三；实现callable 接口 -------JDk 5 新增**

```java
class NumThread implements Callable{
  
  @Override
  public Object call() throws Exception{
    int sum = 0;
    for (int i = 1; i <= 100; i++){
      if (i % 2 == 0){
        sum += i;
      }
    }
    return sum;
  }
}

public class ThreadNew{
  public static void main(String[] args){
    NumThread numThread = new NumThread();
    
    FutureTask futureTask = new FutureTask(numThread);
    new Thrtead().start();
    try{
      Oject sum = futureTask.get();
      System.out.println(sum);
    } catch(InterruptedException e){
      e.printStackTrace();
    } catch(WxcutionException){
      e.printStacktrace();
    }
  }
}
```



## 使用线程池的好处

**背景：**

- 经常创建和销毁、使用量特别大的资源，比如并发情况下的线程，对性能影响很大

**思路：**

- 提前创建好多个线程，放入线程池中，使用时直接获取，使用完放回池中，可以避免频繁创建销毁、实现重复利用。

```java
class NumberThread implements Runnable{
  
  @Override
  public void run(){
    for (int i = 0; i <= 100; i++){
      if (i % 2 == 0){
        System.out.println(Thread.currentThread().getName() + ":" + i);
      }
    }
  }
}

class NumberThread1 implements Runnable{
  
  @Override
  public void run(){
    for (int i = 0; i <= 100; i++){
      if (i % 2 != 0){
        System.out.println(Thread.currentThread().getName() + ":" + i);
      }
    }
  }
}

public class Threadpool{
  public static void main(String[] args){
    ExcutorService service = Executors.newFixedThreadPool(10);
    
    //执行指定的线程的操作。需要提供实现Runnable接口或Callable接口实现类的对象
    service.execute(new NumberThread()); // 适用于Runnable
    service.execute(new NumberThread1());
    //service.submit(); // 适用于Callable
    
    service.shutdown();//关闭连接池
    
  }
}
```



