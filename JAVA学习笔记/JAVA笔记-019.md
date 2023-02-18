# JAVA笔记-019

[TOC]

## JAVA IO原理

- I/O用于处理设备之间的数据传输，如读写文件，网络通讯等
- Java程序中，对于数据的输入/输出操作，以“流（stream）”的方式进行
- java.io包下提供了各种“流”类接口，用来获取不同种类的数据，并通过标准的方法输入/输出数据



**流的分类：**

- 按操作数据单位不同，可分为字节流、字符流
- 按数据流的流向不同，可分为输入流、输出流
- 按流的角色不同，可分为节点流、处理流



```java
public class FileReaderWriterTest{
  
  @Test
  public void testFileReader(){
    FIleReader fr = null;
    try{
      // 实例化File类的对象，指明要操作的文件
      File file = new File("文件路径");
      // 提供具体的流
      fr = new FileReader(file);
    
      // 数据的读入
      // read(): 返回读入的一个字符，如果达到文件末尾，返回-1
      int data = fr.read();
      while(data != -1){
        System.out.print((char)data);
        data = fr.read();
      }
    } catch(IOException e){
      e.printStackTrace();
    } finally{
      // 关闭流
      try{
        if(fr != null)
          fr.close();
      } catch(IOException e){
        e.printStackTrace();
      }
    } 
  }
  
  // 对read()操作升级：使用read的重载方法
  @Test
  public void testFileReader1() throws IOException{
   FileReader fr = null;
    try{
      File file = new File("文件路径");
      fr = new FileReader(file);
      char[] cbuf = new char[5];
      int len;
      while((len =fr.read(cbuf)) != -1){
        // 方式一
        for(int i = 0; i < len; i++){
          System.out.print(cbuf[i]);
        }
        // 方式二
        String str = new String(cbuf,0,len);
        System.out.print(str);
      }
    } catch(IOException e){
      e.printStackTrace();
    } finally{
      if(fr != null){
        try{
          fr.close();
        } catch(IOException e){
          e.printStackTrace();
        }
      }
    }  
  }
  
  
  @Test
  public void testFileWriter() throws IOException{
    FileWriter fw = null;
    try{
      File file = new File("文件路径");
      fw = new FileWriter(file, false);
      fw.write("I have a dream\n");
      fw.write("You have a dream too!");
    } catch(IOException e){
      e.printStackTrace();
    } finally{
      if(fw != null){
        try{
          fw.clse();
        } catch(IOException e){
          e.printStackTrace();
        }
      }
    }
  }
  
  
  @Test
  public void testFileReaderFileWriter() throws IOException{
    FileReader fr = null;
    FileWriter fw = null;
    try{
      File srcFile = new File("文件路径");
      File destFile = new File("文件路径");
      
      fr = new FileReader(srcFile);
      fw = new FileWriter(destFile);
      
      char[] cbuf = new char[5];
      int len;
      while((len = fr.read(cbuf)) != -1){
        fw.write(cbuf,0,len);
      }
    } catch(IOException e){
      e.printStackTrace();
    } finally{
      try{
        if(fw != null){
          fw.close();
        } catch(IoException e){
          e.printStackTrace();
        }
        
        try{
        if(fw != null){
          fr.close();
        } catch(IoException e){
          e.printStackTrace();
        } 
      }
    }
  }
  
}
```



## FileInputStream和FIleOutpuStream的使用

- 对于文本文件（txt、java、c、cpp），使用字符流处理
- 对于非文本文件（图片，视频等），使用字节流处理

```java
public class FileInputPutputStreamTest{
  
  @Test
  public void testFileInputStream(){
    FileInputStream fis = null;
    try{
      File file = new File("文件路径");
      fis = new FIleInputStream(file);
      
      byte[] buffer = new byte[5];
      int len;
      while((len = fis.read(buffer)) != -1){
        String str = new String(buffer,0,len);
        System.out.print(str);
      }
    } catch(IOException e){
      e.printStackTrace();
    } finally{
      try{
        if(fis != null){
          fis.close();
        }
      } catch(IOException e){
        e.printStackTrace();
      }
    }
  }
  
  @Test
  public void testCopyFile(){
    long start = System.currentTimeMillis();
    String srcPath = "xxxxx";
    String destPath = "xxxxx";
    copyFile(srcPath, destpath);
    long end = System.currentTimeMillis();
    System.out.println("复制操作话费的时间为：" + (end - start));
  }
}
```



## 缓冲流

- 提高流的读取、写入速度

```java
public class BufferedTest{
  
  @Test
  public void BufferedStreamTest(){
     // 造文件
    File srcFile = new File("xxxxx");
    File destFile = new File("xxxxx");
    
    // 造流
      // 造节点流
    FileInputStream fis = new FileInputStream(srcFile);
    FileInputStream fos = new FileInputStream(destFile);
      // 造缓冲流
    BufferedInputStream bis = new BufferedInputStream(fis);
    BufferedInputStream bos = new BufferedInputStream(fos);
    
    // 复制的细节：读入、写入
    byte[] buffer = new byte[10];
    int len;
    while((len = bis.read(buffer)) != -1){
      bos.write(buffer, 0, len);
    }
    // 资源关闭：先关闭外层的流，再关闭内层的
    bos.close();
    bis.close();
      // 关闭外层流的同时，内层流也会关闭，如下带代码可以省略
    fos.close();
    fis.close();
  }
  
}
```

