```java

// 创建一个接口
public interface Player{
  void play();
}

// 创建实现接口的实体类
public class WindowMediaPlayer implements Player{
  @Override
  public void play(){
    System.out.println("正在使用WindowMediaPlayer播放多媒体")；
  }
}

public class RealPlayer implements Player{
  @Override
  public void play(){
    System.out.println("正在使用RealPlayer播放多媒体")；
  }
}

public class QuickTime implements Player{
  @Override
  public void play(){
    System.out.println("正在使用QuickTime播放多媒体")；
  }
}

// 创建工厂
public class PlayerFactory {
    
   //使用 getShape 方法获区用户选择player的类型
   public Player getPlayer(String playerType){
      if(playerType == null){
         return null;
      }        
      if(playerType.equals("WindowMediaPlayer")){
         return new WindowMediaPlayer();
      } else if(playerType.equals("RealPlayer")){
         return new RealPlayer();
      } else if(playerType.equals("QuickTime")){
         return new QuickTime();
      }
      return null;
   }
}

// 根据用户需求生产对象
public class PlayTest{
  public static void main(String[] args){
    // 创建工厂对象
    PlayerFactory factory = new PlayerFactory();
    
    // 根据需求选择player
    Player player1 = factory.getPlayer("WindowMediaPlayer");
    player1.play();
    
    Player player2 = factory.getPlayer("RealPlayer");
    player2.play();
    
    Player player3 = factory.getPlayer("QuickTime");
    player3.play();
  }
}
```



```java
//单例设计模式 饿汉式
// 构建Log类
public class Log{
  //1. 私有化类的构造器
  private Log{
    
  }
  
  //2. 内部创建类的静态对象
  private static Log instance = new Log();
  
  //3. 提供公共的静态方法，返回类的对象
  public static Log getInstance(){
    return instance;
  }
  
  //Log 类的其他方法
  public void writeLog(){
    System.out.println("正在写入日志");
  }
  public void showLog(){
    System.out.println("正在展示日志");
  }
}

public class logTest{
  public static void main(String[] args){
    
    //获取唯一可用的对象
    Log log = log.getInstance();
    log.writeLog();
    log.showLog();
  }
}
```



```java
//1. 为LogAdaptee和ILog创建接口
public interface LogAdaptee{
  public abstract writeLog();
}

public interface ILog{
  public abstract write();
}

//2. 创建实现Ilog接口的实现类
public class DatabaseLog implements ILog{
  @Override
  public void write(){
    Log.Write("Logging Message!（ILog，DatabaseLog）");
  }
}

public class FileLog implements ILog{
  @Override
  public void write(){
    Log.Write("Logging Message!（ILog，FileLog）");
  }
}

//3. 创建LogAdaptee接口的实现类
public class DatabaseLog implements LogAdaptee{
  @Override
  public void writeLog(){
    Log.Write("Logging Message!（LogAdaptee，DatabaseLog）");
  }
}

public class FileLog implements LogAdaptee{
  @Override
  public void writeLog(){
    Log.Write("Logging Message!（LogAdaptee，FileLog）");
  }
}

//4. 创建ILog接口的适配器类
public LogAdapter implements ILog{
  private LogAdaptee logadaptee;
  public LogAdapter(LogAdaptee logadaptee){
    this.logadaptee = logadaptee;
  }
  public void write(){
    logadaptee.writeLog();
  }
}

//5. 创建启动类
public class Demo{
  public static void main(String args[]){
    ILog dbLog = new LogAdapter(new DatabaseLog());
    dbLog.write();
    ILog fileLog = new LogAdapter(new fileLog());
    fileLog.write();
  }
}

```



```java
//1. 扩展所有InputStream的抽象装饰者FilterInputStream。
public class LowerCaseInputStream extends FilterInputStream {

    protected LowerCaseInputStream(InputStream in) {
        super(in);
    }

    @Override
    public int read() throws IOException {
        int c = super.read();
        return (c == -1 ? c : Character.toLowerCase((char)c));
    }

    /**
     * 实现两个read()方法，一个针对字节，一个针对字节数组，
     * 把每个是大写字符的字节（每个代表一个字符）转成小写。
     * @param b
     * @param off
     * @param len
     * @return
     * @throws IOException
     */
    @Override
    public int read(byte[] b, int off, int len) throws IOException {
        int result = super.read(b, off, len);
        for (int i = off; i < off + result; i++) {
            b[i] = (byte)Character.toLowerCase((char)b[i]);
        }
        return result;
    }
}

//2. 主函数，测试
public class InputTest {

    public static void main(String[] args) throws IOException {
        int c;
        //设置FileInputStream，先用BufferedInputStream装饰它，
        //再用我们新的LowerCaseInputStream过滤器装饰它。
        LowerCaseInputStream in = new LowerCaseInputStream(new BufferedInputStream(new FileInputStream("test.txt")));
        while ((c = in.read()) != -1){
            //只用流来读取字符，一直到文件尾端。每读一个字符，就马上将它显示出来。
            System.out.print((char)c);
        }
        in.close();
    }
}
```

