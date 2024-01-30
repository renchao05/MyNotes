# 第 1 章 - 内容介绍【未整理】

# 第 2 章 - Java 概述

## CMD中javac中文乱码

右键“我的电脑”-->点击“属性”-->点击”高级系统设置”-->“点击环境变量”-->在系统变量中新建一个系统变量-->编辑环境变量名为JAVA_TOOL_OPTIONS-->编辑环境变量值为-Dfile.encoding=UTF-8



# 第 3 章 - 变量【未整理】

# 第 4 章 - 运算符【未整理】

# 第 5 章 - 程序控制结构【未整理】

# 第 6 章 - 数组、排序和查找【未整理】

# 第 7 章 - 面向对象编程(基础部分)【未整理】

# 第 8 章 - 面向对象编程(中级部分)【未整理】

# 第 9 章 - 项目-房屋出租系统【未整理】

# 第 10 章 - 面向对象编程(高级部分)【未整理】







# 第 11 章 - 枚举和注解

[【零基础 快速学Java】韩顺平 零基础30天学会Java_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1fh411y7R8?p=425)

## 11.1、枚举介绍

- 枚举对应英文(enumeration, 简写 enum) 

- 枚举是一组常量的集合。

- 可以这里理解：枚举属于一种特殊的类，里面只包含一组有限的特定的对象。

- 枚举的二种实现方式：

  > - 自定义类实现枚举
  > - 使用 enum 关键字实现枚举

## 11.2、自定义类实现枚举

- 不需要提供set方法，因为枚举对象通常为只读。
- 对枚举对象/属性使用final + static 共同修饰，实现底层优化。
- 枚举对象名通常使用全部大写，常量的命名规范。
- 枚举对象根据需要，也可以有多个属性。

```java
/**
 * 1) 构造器私有化
 * 2) 本类内部创建一组对象[四个 春夏秋冬]
 * 3) 对外暴露对象（通过为对象添加 public final static 修饰符）
 * 4) 可以提供 get 方法，但是不要提供 set 方法
 */
public class Season {
    private String name;
    private String des;

    public static final Season SPRING = new Season("春天","万物生长。。。");
    public static final Season SUMMER = new Season("夏天","天气炎热。。。");
    public static final Season FALL = new Season("秋天","到处落叶。。。");
    public static final Season WINTER = new Season("冬天","白雪皑皑。。。");

    public String getName() {
        return name;
    }

    public String getDes() {
        return des;
    }

    private Season(String name, String des) {
        this.name = name;
        this.des = des;
    }
}
```

## 11.3、enum 关键字实现枚举

```java
public enum Season {
    SPRING("春天","万物生长。。。"),
    SUMMER("夏天","天气炎热。。。"),
    FALL("秋天","到处落叶。。。"),
    WINTER("冬天","白雪皑皑。。。");
    private final String name;
    private final String des;

    public String getName() {
        return name;
    }

    public String getDes() {
        return des;
    }

    Season2(String name, String des) {
        this.name = name;
        this.des = des;
    }
}
```

注意：

>- enum 关键字枚举类默认会继承 Enum 类, 而且是一个 final 类，可以用 javap 工具验证
>- 传统的 `public static final Season SPRING = new Season("春天", "温暖")`; 简化成 `SPRING("春天", "温暖")`
>  这里是调用对应的构造器。
>- 如果使用无参构造器创建枚举对象，则实参列表和小括号都可以省略。
>- 当有多个枚举对象时，使用`,`间隔，最后有一个分号结尾。
>- 枚举对象必须放在枚举类的行首。



## 11.4、enum 常用方法

 ![image-20220320131340562](https://renchao05.oss-cn-hangzhou.aliyuncs.com/img/image-20220320131340562.png)

> - toString：Enum 类已经重写过了，返回的是当前对象名,子类可以重写该方法，用于返回对象的属性信息
> - name：返回当前对象名（常量名），子类中不能重写
> - ordinal：返回当前对象的位置号，默认从 0 开始
> - **values：返回当前枚举类中所有的常量**
> - valueOf：将字符串转换成枚举对象，要求字符串必须 为已有的常量名，否则报异常！
> - compareTo：比较两个枚举常量，比较的就是编号！



## 11.5、enum 实现接口

- 使用 enum 关键字后，就不能再继承其它类了，因为 enum 会隐式继承 Enum，而 Java 是单继承机制。
- 枚举类和普通类一样，可以实现接口，如下形式。
  `enum 类名 implements 接口1，接口2 {}`



## 11.6、注解的理解

- 注解(Annotation)也被称为元数据(Metadata)，用于修饰解释 包、类、方法、属性、构造器、局部变量等数据信息。
- 和注释一样，注解不影响程序逻辑，但注解可以被编译或运行，相当于嵌入在代码中的补充信息。
- 在 JavaSE 中，注解的使用目的比较简单，例如标记过时的功能，忽略警告等。
  在 JavaEE 中注解占据了更重要的角色，例如用来配置应用程序的任何切面，代替 java EE 旧版中所遗留的繁冗代码和 XML 配置等。

## 11.7、基本的 Annotation

- @Override: 限定某个方法，是重写父类方法, 该注解只能用于方法
- @Deprecated: 用于表示某个程序元素(类, 方法等)已过时
- @SuppressWarnings: 抑制编译器警告

## 11.8、JDK 的元注解

- 元注解的基本介绍

  JDK 的元注解用于修饰其他注解。

- 元注解的种类：

  - Retention
    指定注解的作用范围，三种 SOURCE,CLASS,RUNTIME

  - Target

    指定注解可以在哪些地方使用

  - Documented

    指定该注解是否会在 javadoc 体现

  - Inherited

    子类会继承父类注解

- **@Retention 注解**

  说明：

  > 只能用于修饰一个 Annotation 定义, 用于指定该 Annotation 可以保留多长时间
  >
  > @Rentention 包含一个 RetentionPolicy 类型的成员变量, 使用 @Rentention 时必须为该 value

  @Retention 的三种值：

  - RetentionPolicy.SOURCE: 
    编译器使用后，直接丢弃这种策略的注释
  - RetentionPolicy.CLASS: 
    编译器将把注解记录在 class 文件中。当运行 Java 程序时, JVM 不会保留注解。 这是默认值
  - RetentionPolicy.RUNTIME:
    编译器将把注解记录在 class 文件中. 当运行 Java 程序时, JVM 会保留注解. 程序可以 通过反射获取该注解

- **@Target**

  说明：

  > 用于修饰Annotation定义，用于指定被修饰的Annotation能用于修饰哪些程序元素
  >
  > @Target也包含一个名为value的成员变量。

  @Target的值：

  - ElementType.TYPE	//接口、类、枚举、注解
  - ElementType.FIELD	//字段、枚举的常量
  - ElementType.METHOD	//方法
  - ElementType.PARAMETER	//方法参数
  - ElementType.CONSTRUCTOR	//构造函数
  - ElementType.LOCAL_VARIABLE	//局部变量
  - ElementType.ANNOTATION_TYPE	//注解
  - ElementType.PACKAGE	//包

- **@Documented**

  > 用于指定被该元Annotation修饰的Annotation类将被javadoc工具提取成文档，即在生成文档时，可以看到该注解。

- @**Inherited**

  > 被它修饰的Annotation将具有继承性.如果某个类使用了被@Inherited修饰的Annotation,则其子类将自动具有该注解。

# 第 12 章 - 异常-Exception【未整理】





# 第 13 章 - 常用类【未整理】



# 第 14 章 - 集合【未整理】



# 第 15 章 - 泛型【未整理】



# 第 16 章 - 坦克大战 1【未整理】



# 第 17 章 - 多线程基础【未整理】



# 第 18 章 - 坦克大战2【未整理】



# 第 19 章 - IO 流

![img](https://renchao05.oss-cn-hangzhou.aliyuncs.com/img/20181010162011404)

## 19.1 文件

### 19.1.1 什么是文件

- 文件是计算机文件属于文件的一种，与普通文件载体不同，计算机文件是以计算机硬盘为载体存储在计算机上的信息集合。
- 文件可以是文本文档、图片、程序等等。
  文件通常具有三个字母的文件扩展名，用于指示文件类型（例如，图片文件常常以 JPEG 格式保存并且文件扩展名为 ．jpg）。

### 19.1.2 文件流

 ![image-20220413213316217](https://renchao05.oss-cn-hangzhou.aliyuncs.com/img/image-20220413213316217.png)

## 19.2 常用的文件操作

### 19.2.1 创建文件对象相关构造器和方法

- 根据路径构建文件对象

  ```java
  @Test
  public void create01() {
      String filePath = "d:\\news1.txt";
      File file = new File(filePath);
      try {
          //这里的 file 对象，在 java 程序中，只是一个对象
          //只有执行了 createNewFile 方法，才会真正的，在磁盘创建该文件
          boolean newFile = file.createNewFile();
          System.out.println("文件创建成功。");
      } catch (IOException e) {
          e.printStackTrace();
      }
  }
  ```

- 根据父目录文件 + 子路径构建

  ```java
  @Test
  public void create02() {
      File parentFile = new File("e:\\");
      String fileName = "news2.txt";
      //这里的 file 对象，在 java 程序中，只是一个对象
      //只有执行了 createNewFile 方法，才会真正的，在磁盘创建该文件
      File file =  new File(parentFile, fileName);
      try {
          boolean newFile = file.createNewFile();
          System.out.println("文件2创建成功。");
      } catch (IOException e) {
          e.printStackTrace();
      }
  }
  ```

- 根据父目录+子路径构建

  ```java
  @Test
  public void create03() {
      String path = "d:\\";
      String filePath = "KEFU\\news3.txt";
      File file = new File(path, filePath);
      try {
          System.out.println(file.createNewFile());
          System.out.println("文件3创建成功。");
      } catch (IOException e) {
          e.printStackTrace();
          System.out.println("文件创建失败。");
      }
  }
  ```

### 19.2.2 获取文件的相关信息

```java
public class FileInformation {
    public static void main(String[] args) {
        File file = new File("D:\\KEFU\\file.txt");
        System.out.println("文件名称：" + file.getName());
        System.out.println("绝对路径：" + file.getAbsolutePath());
        System.out.println("文件对象：" + file.getAbsoluteFile());
        System.out.println("父目录：" + file.getParent());
        System.out.println("文件大小(字节)：" + file.length());
        System.out.println("是否存在：" + file.exists());
        System.out.println("是否文件：" + file.isFile());
        System.out.println("是否目录：" + file.isDirectory());
    }
}
```

### 19.2.4 目录的操作和文件删除

- mkdir 创建一级目录
- mkdirs 创建多级目录
- delete 删除空目录或文件

## 19.3 IO 流原理及流的分类

### 19.3.1 Java IO 流原理

 ![image-20220413221516963](https://renchao05.oss-cn-hangzhou.aliyuncs.com/img/image-20220413221516963.png)

### 19.3.2 流的分类

 ![image-20220413221608587](https://renchao05.oss-cn-hangzhou.aliyuncs.com/img/image-20220413221608587.png)

## 19.4 IO 流体系图-常用的类

 ![image-20220413222057915](https://renchao05.oss-cn-hangzhou.aliyuncs.com/img/image-20220413222057915.png)

### 19.4.1 FileInputStream

- 构造方法

  - `FileInputStream(File file) `
    通过打开与实际文件的连接创建一个 FileInputStream ，该文件由文件系统中的 File对象 file命名。  
  - `FileInputStream(FileDescriptor fdObj)`
    创建 FileInputStream通过使用文件描述符 fdObj ，其表示在文件系统中的现有连接到一个实际的文件。  
  - `FileInputStream(String name)`
    通过打开与实际文件的连接来创建一个 FileInputStream ，该文件由文件系统中的路径名 name命名。 

- 方法

  | 返回值类型       | 方法与描述                                                   |
  | ---------------- | ------------------------------------------------------------ |
  | `int`            | `available()`  返回从此输入流中可以读取（或跳过）的剩余字节数的估计值，而不会被下一次调用此输入流的方法阻塞。 |
  | `void`           | `close()`  关闭此文件输入流并释放与流相关联的任何系统资源。  |
  | `void`           | `finalize()`  确保当这个文件输入流的 `close`方法没有更多的引用时被调用。 |
  | `FileChannel`    | `getChannel()`  返回与此文件输入流相关联的唯一的[`FileChannel`](../../java/nio/channels/FileChannel.html)对象。 |
  | `FileDescriptor` | `getFD()`  返回表示与此 `FileInputStream`正在使用的文件系统中实际文件的连接的  `FileDescriptor`对象。 |
  | `int`            | `read()`  从该输入流读取一个字节的数据。                     |
  | `int`            | `read(byte[] b)`  从该输入流读取最多 `b.length`个字节的数据为字节数组。 |
  | `int`            | `read(byte[] b,  int off, int len)`  从该输入流读取最多 `len`字节的数据为字节数组。 |
  | `long`           | `skip(long n)`  跳过并从输入流中丢弃 `n`字节的数据。         |

- 读取方式一：

  ```java
  fileInputStream = new FileInputStream("d:\\news2.txt");
  while ((i = fileInputStream.read()) != -1){
      System.out.print((char) i);
  }
  ```

- 读取方式二：

  ```java
  fileInputStream = new FileInputStream("d:\\news2.txt");
  while ((readLen = fileInputStream.read(buf)) != -1){//buf 字节数组
      System.out.print(new String(buf,0,readLen));//readLen 读取的长度
  }
  ```

### 19.4.2 FileOutputStream

- 构造方法

  - `FileOutputStream(File file) `
    File对象创建文件输出流。  
  - `FileOutputStream(File file, boolean append) `
    File对象创建文件输出流，true表示覆盖写入。  
  - `FileOutputStream(FileDescriptor fdObj) `
    创建文件输出流以写入指定的文件描述符，表示与文件系统中实际文件的现有连接。  
  - `FileOutputStream(String name) `
    绝对路径创建文件输出流。  
  - `FileOutputStream(String name, boolean append)` 
    绝对路径创建文件输出流，true表示覆盖写入。 

- 方法

  | 返回值类型       | 方法与描述                                                   |
  | ---------------- | ------------------------------------------------------------ |
  | `void`           | `close()`  关闭此文件输出流并释放与此流相关联的任何系统资源。 |
  | `protected void` | `finalize()`  清理与文件的连接，并确保当没有更多的引用此流时，将调用此文件输出流的 `close`方法。 |
  | `FileChannel`    | `getChannel()`  返回与此文件输出流相关联的唯一的[`FileChannel`](../../java/nio/channels/FileChannel.html)对象。 |
  | `FileDescriptor` | `getFD()`  返回与此流相关联的文件描述符。                    |
  | `void`           | `write(byte[] b)`  将 `b.length`个字节从指定的字节数组写入此文件输出流。 |
  | `void`           | `write(byte[] b,  int off, int len)`  将 `len`字节从位于偏移量 `off`的指定字节数组写入此文件输出流。 |
  | `void`           | `write(int b)`  将指定的字节写入此文件输出流。               |

- 实例

  ```java
  @Test
  public void writer() {
      try {
          String str = "hello,good morning!";
          file = new FileOutputStream("d:\\chao.txt",true);//追加方式写入
          file.write(str.getBytes());
      } catch (IOException e) {
          e.printStackTrace();
      } finally {
          try {
              file.close();
          } catch (IOException e) {
              e.printStackTrace();
          }
      }
  }
  ```

  

### 19.4.3 FileReader

- 构造方法

  - `FileReader(File file)` 
    创建一个新的 FileReader ，给出 File读取。  
  - `FileReader(FileDescriptor fd) `
    创建一个新的 FileReader ，给定 FileDescriptor读取。  
  - `FileReader(String fileName) `
    创建一个新的 FileReader ，给定要读取的文件的名称。

- 方法

  | 返回值类型 | 方法与描述                                                   |
  | ---------- | ------------------------------------------------------------ |
  | `void`     | `close()`  关闭流并释放与之相关联的任何系统资源。            |
  | `String`   | `getEncoding()`  返回此流使用的字符编码的名称。              |
  | `int`      | `read()`  读一个字符                                         |
  | `int`      | `read(char[] cbuf)`  读一个字符数组                          |
  | `int`      | `read(char[] cbuf,  int offset, int length)`  将字符读入数组的一部分。 |
  | `boolean`  | `ready()`  告诉这个流是否准备好被读取。                      |

- 实例

  ```java
  @Test
  public void test01() throws IOException {
      FileReader fileReader = null;
      int length = 0;
      char[] cbuf = new char[5];
      fileReader = new FileReader("d:\\chao.txt");
      while ((length = fileReader.read(cbuf)) != -1) {
          System.out.print(new String(cbuf, 0, length));
      }
      fileReader.close();
  }
  ```

  

### 19.4.4 FileWriter

- 构造方法

  - `FileWriter(File file) `
    给一个File对象构造一个FileWriter对象。  
  - `FileWriter(File file, boolean append)` 
    给一个File对象构造一个FileWriter对象。  
  - `FileWriter(FileDescriptor fd)`
    构造与文件描述符关联的FileWriter对象。  
  - `FileWriter(String fileName)` 
    构造一个给定文件名的FileWriter对象。  
  - `FileWriter(String fileName, boolean append)` 
    构造一个FileWriter对象，给出一个带有布尔值的文件名，表示是否附加写入的数据。 

- 方法

  | 返回值类型 | 方法与描述                                                   |
  | ---------- | ------------------------------------------------------------ |
  | `void`     | `close()`  关闭流，先刷新。                                  |
  | `void`     | `flush()`  刷新流。                                          |
  | `String`   | `getEncoding()`  返回此流使用的字符编码的名称。              |
  | `void`     | `write(char[] cbuf,  int off, int len)`  写入字符数组的一部分。 |
  | `void`     | `write(int c)`  写一个字符                                   |
  | `void`     | `write(String str,  int off, int len)`  写一个字符串的一部分。 |

  > 必须执行 `close()` 或者 `flush()` 才能将信息写入文件。

- 实例

  ```java
  @Test
  public void test01() throws IOException {
      FileWriter fileWriter = null;
      char[] chars = "风雨之后，定见彩虹".toCharArray();
      fileWriter = new FileWriter("d:\\note.txt");
      fileWriter.write(chars);
      fileWriter.close();
  }
  ```

## 19.5 节点流和处理流

### 19.5.1 基本介绍

 ![image-20220414093958248](https://renchao05.oss-cn-hangzhou.aliyuncs.com/img/image-20220414093958248.png)

### 19.5.2 节点流和处理流一览图

| 分类       | 字节输入流           | 字节输出流            | 字符输入流        | 字符输出流         |
| ---------- | -------------------- | --------------------- | ----------------- | ------------------ |
| 抽象基类   | InputStream          | OutputStream          | Reader            | Writer             |
| 访问文件   | FileInputStream      | FileOutputStream      | FileReader        | FileWriter         |
| 访问数组   | ByteArrayInputStream | ByteArrayOutputStream | CharArrayReader   | CharArrayWriter    |
| 访问管道   | PipedInputStream     | PipedOutputStream     | PipedReader       | PipedWriter        |
| 访问字符串 |                      |                       | StringReader      | StringWriter       |
| 缓冲流     | BufferedInputStream  | BufferedOutputStream  | BufferedReader    | BufferedWriter     |
| 转换流     |                      |                       | InputStreamReader | OutputStreamWriter |
| 对象流     | ObjectInputStream    | ObjectOutputStream    |                   |                    |
| 抽象基类   | FilterInputStream    | FilterOutputStream    | FilterReader      | FilterWriter       |
| 打印流     |                      | PrintStream           |                   | PrintWriter        |
| 推回输入流 | PushbackInputStream  |                       | PushbackReader    |                    |
| 特殊流     | DataInputStream      | DataOutputStream      |                   |                    |

> - **前 4 行是节点流。**
> - **后 7 行是处理流（包装流）。**

### 19.5.3 节点流 VS 处理流

1. 节点流是底层流/低级流，**直接跟数据源相接。**
2. 处理流(包装流)包装节点流，既可以消除不同节点流的实现差异，也可以提供更方便的方法来完成输入输出。[源码理解]

3. 处理流(也叫包装流)对节点流进行包装，使用了修饰器设计模式，不会直接与数据源相连[模拟修饰器设计模式=》小伙伴就会非常清楚]

### 19.5.4 处理流的功能主要体现

- **性能的提高：**
  主要以增加缓冲的方式来提高输入输出的效率。
- **操作的便捷：**
  处理流可能提供了一-系列便捷的方法来一次输入输出大批量的数据，使用更加灵活方便。

### 19.5.5 BufferedReader

- 构造方法

  - `BufferedReader(Reader in)`
    创建使用默认大小的输入缓冲区的缓冲字符输入流。
  - `BufferedReader(Reader in, int sz)`
    创建使用指定大小的输入缓冲区的缓冲字符输入流。

- 方法

  | 返回值类型       | 方法与描述                                                   |
  | ---------------- | ------------------------------------------------------------ |
  | `void`           | `close()`  关闭流并释放与之相关联的任何系统资源。            |
  | `Stream<String>` | `lines()`  返回一个 `Stream` ，其元素是从这个  `BufferedReader`读取的行。 |
  | `void`           | `mark(int readAheadLimit)`  标记流中的当前位置。             |
  | `boolean`        | `markSupported()`  告诉这个流是否支持mark（）操作。          |
  | `int`            | `read()`  读一个字符                                         |
  | `int`            | `read(char[] cbuf,  int off, int len)`  将字符读入数组的一部分。 |
  | `String`         | `readLine()`  读一行文字。                                   |
  | `boolean`        | `ready()`  告诉这个流是否准备好被读取。                      |
  | `void`           | `reset()`  将流重置为最近的标记。                            |
  | `long`           | `skip(long n)`  跳过字符                                     |

- 案例

  ```java
  public void test01() throws IOException {
      BufferedReader bufferedReader = new BufferedReader(new FileReader("d:\\note.txt"));
      //返回一个 Stream
      Stream<String> lines = bufferedReader.lines();
      lines.forEach(System.out::println);
  
      //整行读取
      String str;
      while ((str = bufferedReader.readLine()) != null) {
          System.out.println(str);
      }
  }
  ```

### 19.5.6 BufferedWriter

- 构造方法

  - `BufferedWriter(Writer out)`
    创建使用默认大小的输出缓冲区的缓冲字符输出流。  
  - `BufferedWriter(Writer out, int sz)`
    创建一个新的缓冲字符输出流，使用给定大小的输出缓冲区。 

- 方法

  | 返回值类型 | 方法与描述                                                   |
  | ---------- | ------------------------------------------------------------ |
  | `void`     | `close()`  关闭流，先刷新。                                  |
  | `void`     | `flush()`  刷新流。                                          |
  | `void`     | `newLine()`  写一行行分隔符。                                |
  | `void`     | `write(char[] cbuf,  int off, int len)`  写入字符数组的一部分。 |
  | `void`     | `write(int c)`  写一个字符                                   |
  | `void`     | `write(String s,  int off, int len)`  写一个字符串的一部分。 |

  > 必须执行 `close()` 或者 `flush()` 才能将信息写入文件。

- 案例

  ```java
  @Test
  public void test01() throws IOException {
      String str = "hello,任超你找到了你喜欢的事情";
      Stream<String> stream = Stream.of("hello_01", "hello_02", "hello_03", "hello_04");
      BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter("d:\\chao.txt",true));
      stream.forEach(s -> { //写入流
          try {
              bufferedWriter.write(s);
          } catch (IOException e) {
              e.printStackTrace();
          }
      });
      bufferedWriter.write(str);  //写入一行字符串
      bufferedWriter.close();
  }
  ```

  

### 19.5.7 BufferedInputStream

> - 处理流
> - 使用方法与 `InputStream` 类似



### 19.5.8 BufferedOutputStream

> - 处理流
> - 使用方法与 `OutputStream` 类似



## 19.6 序列化 和 反序列化

- 序列化就是在保存数据时，**保存数据的值和数据类型**。
- 反序列化就是在恢复数据时，**恢复数据的值和数据类型**。
- 如果某个类需要支持序列化机制，则该类必须实现如下两个接口之一:
  - Serializable // 标记接口， 没有方法【推荐使用】
  - Externalizable //该接口有方法需要实现

### 19.6.1 对象流介绍

功能：提供了对基本类型或对象类型的序列化和反序列化的方法

- ObjectOutputStream 提供 序列化功能
- ObjectInputStream 提供 反序列化功能

### 19.6.2 ObjectOutputStream

- 构造器

  - `ObjectOutputStream()`
    为完全重新实现ObjectOutputStream的子类提供一种方法，不必分配刚刚被ObjectOutputStream实现使用的私有数据。  
  - `ObjectOutputStream(OutputStream out)`
    创建一个写入指定的OutputStream的ObjectOutputStream。

- 方法

  | 返回值类型                    | 方法与描述                                                   |
  | ----------------------------- | ------------------------------------------------------------ |
  | `protected void`              | `annotateClass(类<?> cl)`  子类可以实现此方法，以允许类数据存储在流中。 |
  | `protected void`              | `annotateProxyClass(类<?> cl)`  子类可以实现这种方法来存储流中的自定义数据以及动态代理类的描述符。 |
  | `void`                        | `close()`  关闭流。                                          |
  | `void`                        | `defaultWriteObject()`  将当前类的非静态和非瞬态字段写入此流。 |
  | `protected void`              | `drain()`  排除ObjectOutputStream中的缓冲数据。              |
  | `protected boolean`           | `enableReplaceObject(boolean enable)`  启用流来替换流中的对象。 |
  | `void`                        | `flush()`  刷新流。                                          |
  | `ObjectOutputStream.PutField` | `putFields()`  检索用于缓冲要写入流的持久性字段的对象。      |
  | `protected Object`            | `replaceObject(Object obj)`  该方法将允许ObjectOutputStream的可信子类在序列化期间将一个对象替换为另一个对象。 |
  | `void`                        | `reset()`  复位将忽略已写入流的任何对象的状态。              |
  | `void`                        | `useProtocolVersion(int version)`  指定在编写流时使用的流协议版本。 |
  | `void`                        | `write(byte[] buf)`  写入一个字节数组。                      |
  | `void`                        | `write(byte[] buf,  int off, int len)`  写入一个子字节数组。 |
  | `void`                        | `write(int val)`  写一个字节。                               |
  | `void`                        | `writeBoolean(boolean val)`  写一个布尔值。                  |
  | `void`                        | `writeByte(int val)`  写入一个8位字节。                      |
  | `void`                        | `writeBytes(String str)`  写一个字符串作为字节序列。         |
  | `void`                        | `writeChar(int val)`  写一个16位的字符。                     |
  | `void`                        | `writeChars(String str)`  写一个字符串作为一系列的字符。     |
  | `protected void`              | `writeClassDescriptor(ObjectStreamClass desc)`  将指定的类描述符写入ObjectOutputStream。 |
  | `void`                        | `writeDouble(double val)`  写一个64位的双倍。                |
  | `void`                        | `writeFields()`  将缓冲的字段写入流。                        |
  | `void`                        | `writeFloat(float val)`  写一个32位浮点数。                  |
  | `void`                        | `writeInt(int val)`  写一个32位int。                         |
  | `void`                        | `writeLong(long val)`  写一个64位长                          |
  | `void`                        | `writeObject(Object obj)`  将指定的对象写入ObjectOutputStream。 |
  | `protected void`              | `writeObjectOverride(Object obj)`  子类使用的方法来覆盖默认的writeObject方法。 |
  | `void`                        | `writeShort(int val)`  写一个16位短。                        |
  | `protected void`              | `writeStreamHeader()`  提供了writeStreamHeader方法，因此子类可以在流中附加或预先添加自己的头。 |
  | `void`                        | `writeUnshared(Object obj)`  将“非共享”对象写入ObjectOutputStream。 |
  | `void`                        | `writeUTF(String str)`  此字符串的原始数据写入格式为 [modified  UTF-8](DataInput.html#modified-utf-8) 。 |

- 案例

  ```java
  public static void main(String[] args) throws IOException {
      ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("d:\\dat.dat"));
      oos.writeInt(100);
      oos.writeUTF("任超");
      oos.writeDouble(100);
      oos.writeBoolean(true);
      oos.writeObject(new Dog("小黄",3));
      oos.close();
  }
  ```

  

### 19.6.3 ObjectInputStream

- 构造器

  - `ObjectInputStream()`
    为完全重新实现ObjectInputStream的子类提供一种方法，不必分配刚刚被ObjectInputStream实现使用的私有数据。
  - `ObjectInputStream(InputStream in)`
    创建从指定的InputStream读取的ObjectInputStream。

- 方法

  | 返回值类型                    | 方法与描述                                                   |
  | ----------------------------- | ------------------------------------------------------------ |
  | `int`                         | `available()`  返回可以读取而不阻塞的字节数。                |
  | `void`                        | `close()`  关闭输入流。                                      |
  | `void`                        | `defaultReadObject()`  从此流读取当前类的非静态和非瞬态字段。 |
  | `protected boolean`           | `enableResolveObject(boolean enable)`  启用流以允许从流中读取的对象被替换。 |
  | `int`                         | `read()`  读取一个字节的数据。                               |
  | `int`                         | `read(byte[] buf,  int off, int len)`  读入一个字节数组。    |
  | `boolean`                     | `readBoolean()`  读取布尔值。                                |
  | `byte`                        | `readByte()`  读取一个8位字节。                              |
  | `char`                        | `readChar()`  读一个16位字符。                               |
  | `protected ObjectStreamClass` | `readClassDescriptor()`  从序列化流读取类描述符。            |
  | `double`                      | `readDouble()`  读64位双倍。                                 |
  | `ObjectInputStream.GetField`  | `readFields()`  从流中读取持久性字段，并通过名称获取它们。   |
  | `float`                       | `readFloat()`  读32位浮点数。                                |
  | `void`                        | `readFully(byte[] buf)`  读取字节，阻塞直到读取所有字节。    |
  | `void`                        | `readFully(byte[] buf,  int off, int len)`  读取字节，阻塞直到读取所有字节。 |
  | `int`                         | `readInt()`  读取一个32位int。                               |
  | `String`                      | `readLine()`  已弃用  此方法无法将字节正确转换为字符。 有关详细信息和替代方案，请参阅DataInputStream。 |
  | `long`                        | `readLong()`  读64位长。                                     |
  | `Object`                      | `readObject()`  从ObjectInputStream读取一个对象。            |
  | `protected Object`            | `readObjectOverride()`  此方法由ObjectOutputStream的受信任子类调用，该子类使用受保护的无参构造函数构造ObjectOutputStream。 |
  | `short`                       | `readShort()`  读取16位短。                                  |
  | `protected void`              | `readStreamHeader()`  提供了readStreamHeader方法来允许子类读取和验证自己的流标题。 |
  | `Object`                      | `readUnshared()`  从ObjectInputStream读取一个“非共享”对象。  |
  | `int`                         | `readUnsignedByte()`  读取一个无符号的8位字节。              |
  | `int`                         | `readUnsignedShort()`  读取无符号16位短。                    |
  | `String`                      | `readUTF()`  以 [modified  UTF-8](DataInput.html#modified-utf-8)格式读取字符串。 |
  | `void`                        | `registerValidation(ObjectInputValidation obj,  int prio)`  在返回图之前注册要验证的对象。 |
  | `protected 类<?>`             | `resolveClass(ObjectStreamClass desc)`  加载本地类等效的指定流类描述。 |
  | `protected Object`            | `resolveObject(Object obj)`  此方法将允许ObjectInputStream的受信任子类在反序列化期间将一个对象替换为另一个对象。 |
  | `protected 类<?>`             | `resolveProxyClass(String[] interfaces)`  返回一个代理类，它实现代理类描述符中命名的接口;  子类可以实现此方法从流中读取自定义数据以及动态代理类的描述符，从而允许它们为接口和代理类使用备用加载机制。 |
  | `int`                         | `skipBytes(int len)`  跳过字节。                             |

- 案例

  ```java
  public static void main(String[] args) throws IOException, ClassNotFoundException {
      //读取顺序必须与写入时的顺序一样。
      ObjectInputStream ois = new ObjectInputStream(new FileInputStream("d:\\dat.dat"));
      System.out.println(ois.readInt());
      System.out.println(ois.readUTF());
      System.out.println(ois.readDouble());
      System.out.println(ois.readBoolean());
      System.out.println(ois.readObject());
  }
  ```

  

### 19.6.4 注意事项和细节

1. 读写顺序要一致。

2. 要求序列化或反序列化对象,需要实现`Serializable`。

3. 序列化的类中建议添加`serialVersionUID`,为了提高版本的兼容性。

   ```java
   private static final long serialVersionUID = 4663089470380193050L;
   ```

4. 序列化对象时，默认将里面所有属性都进行序列化，但除了 `static` 或 `transient` 修饰的成员

5. 序列化对象时，要求对象属性的类型也需要实现序列化接口。

6. 序列化具备可继承性，也就是如果某类已经实现了序列化，则它的所有子类也已经默认实现了序列化。



## 19.7 转换流

### 19.7.1 文件乱码问题

```java
public static void main(String[] args) throws IOException {
    //读取 d:\\a.txt 文件编码是GBK
    //默认情况下，读取文件是按照 utf-8 编码，中文会乱码
    String filePath = "d:\\a.txt";
    BufferedReader br = new BufferedReader(new FileReader(filePath));
    String s = br.readLine();
    System.out.println("读取到的内容: " + s);
    br.close();
}
```

### 19.7.2 InputStreamReader

- 构造器

  - `InputStreamReader(InputStream in)`
    创建一个使用默认字符集的InputStreamReader。  
  - `InputStreamReader(InputStream in, Charset cs)`
    创建一个指定字符集的InputStreamReader。  
  - `InputStreamReader(InputStream in, CharsetDecoder dec)`
    创建一个指定字符集解码器的InputStreamReader。  
  - `InputStreamReader(InputStream in, String charsetName)`
    创建一个使用命名字符集的InputStreamReader。  

- 方法

  | 返回值类型 | 方法与描述                                                   |
  | ---------- | ------------------------------------------------------------ |
  | `void`     | `close()`  关闭流并释放与之相关联的任何系统资源。            |
  | `String`   | `getEncoding()`  返回此流使用的字符编码的名称。              |
  | `int`      | `read()`  读一个字符                                         |
  | `int`      | `read(char[] cbuf,  int offset, int length)`  将字符读入数组的一部分。 |
  | `boolean`  | `ready()`  告诉这个流是否准备好被读取。                      |

- 案例

  ```java
  @Test
  public void test01() throws IOException {
      //读取 d:\\a.txt 文件编码是GBK
      InputStreamReader isr = new InputStreamReader(new FileInputStream("d:\\a.txt"), "GBK");
      BufferedReader br = new BufferedReader(isr);
      Stream<String> stream = br.lines();
      stream.forEach(System.out::println);
  }
  ```



### 19.7.3 OutputStreamWriter

- 构造器

  - `OutputStreamWriter(OutputStream out)`
    创建一个使用默认字符编码的OutputStreamWriter。  
  - `OutputStreamWriter(OutputStream out, Charset cs)`
    创建一个使用给定字符集的OutputStreamWriter。  
  - `OutputStreamWriter(OutputStream out, CharsetEncoder enc)`
    创建一个使用给定字符集编码器的OutputStreamWriter。  
  - `OutputStreamWriter(OutputStream out, String charsetName)`
    创建一个使用命名字符集的OutputStreamWriter。 

- 方法

  | Modifier and Type | Method and Description                                       |
  | ----------------- | ------------------------------------------------------------ |
  | `void`            | `close()`  关闭流，先刷新。                                  |
  | `void`            | `flush()`  刷新流。                                          |
  | `String`          | `getEncoding()`  返回此流使用的字符编码的名称。              |
  | `void`            | `write(char[] cbuf,  int off, int len)`  写入字符数组的一部分。 |
  | `void`            | `write(int c)`  写一个字符                                   |
  | `void`            | `write(String str,  int off, int len)`  写一个字符串的一部分。 |

- 案例

  ```java
  @Test
  public void test01() throws IOException {
      String str = "hello,任超！！";
      //设置文件保存为“GBK”,默认是“UTF-8”
      OutputStreamWriter osw = new OutputStreamWriter(new FileOutputStream("d:\\b.txt"), "GBK");
      osw.write(str);
      osw.close();
  }
  ```

## 19.7 标准输入输出流

|                       | 编译类型    | 运行类型            | 默认设备 |
| --------------------- | ----------- | ------------------- | -------- |
| `System.in` 标准输入  | InputStream | BufferedInputStream | 键盘     |
| `System.out` 标准输出 | PrintStream | PrintStream         | 显示器   |

### 19.7.1 System.in

```java
//IntelliJ IDEA控制台junitTest不能用Scanner输入
public static void main(String[] args) throws IOException {
    Scanner scanner = new Scanner(System.in);
    System.out.print("请输入您的名字：");
    String str = scanner.nextLine();
    System.out.println("你的名字是：" + str);
}
```



### 19.7.2 PrintStream

- 构造器

  - `PrintStream(File file)`
    使用指定的文件创建一个新的打印流，而不需要自动换行。
  - `PrintStream(File file, String csn)`
    使用指定的文件和字符集创建新的打印流，而不需要自动换行。  
  - `PrintStream(OutputStream out)`
    创建一个新的打印流。
  - `PrintStream(OutputStream out, boolean autoFlush)`
    创建一个新的打印流。
  - `PrintStream(OutputStream out, boolean autoFlush, String encoding)`
    创建一个新的打印流。
  - `PrintStream(String fileName)`
    使用指定的文件名创建新的打印流，无需自动换行。
  - `PrintStream(String fileName, String csn)`
    创建一个新的打印流，不需要自动换行，具有指定的文件名和字符集。

- 方法
  参考JavaSE手册

- 案例

  ```java
  @Test
  public void test03() throws IOException {
      PrintStream out = System.out;
      //默认是打印到显示器
      out.println("任超您好。。。");
      //源码也是使用的 write() 方法
      out.write("任超您好！！！".getBytes());
  
      out = new PrintStream("d:\\aa.txt");
      out.println("打印到文件：d:\\aa.txt");
  
      //把结果保存到文件 d:\print.txt
      System.setOut(new PrintStream("d:\\print.txt"));
      System.out.println("任超您好。。。");
      System.out.write("任超您好！！！".getBytes());
  
      out.close();
  }
  ```

### 19.7.2 PrintWriter

- 构造器

  - `PrintWriter(File file)`
    使用指定的文件创建一个新的PrintWriter，而不需要自动的线路刷新。
  - `PrintWriter(File file, String csn)`
    使用指定的文件和字符集创建一个新的PrintWriter，而不需要自动进行线条刷新。
  - `PrintWriter(OutputStream out)`
    从现有的OutputStream创建一个新的PrintWriter，而不需要自动线路刷新。
  - `PrintWriter(OutputStream out, boolean autoFlush)`
    从现有的OutputStream创建一个新的PrintWriter。
  - `PrintWriter(String fileName)`
    使用指定的文件名创建一个新的PrintWriter，而不需要自动执行行刷新。
  - `PrintWriter(String fileName, String csn)`
    使用指定的文件名和字符集创建一个新的PrintWriter，而不需要自动线路刷新。
  - `PrintWriter(Writer out)`
    创建一个新的PrintWriter，没有自动线冲洗。
  - `PrintWriter(Writer out, boolean autoFlush)`
    创建一个新的PrintWriter。  

- 方法
  参考JavaSE手册

- 案例

  ```java
  public static void main(String[] args) throws FileNotFoundException {
      PrintWriter pw = new PrintWriter(System.out);
      pw.write("任超，您好====");  //打印到显示器
  
      //打印到文件
      pw = new PrintWriter("d:\\print.txt");
      pw.println("任超你号，哈哈！！！！");
      pw.close();
  }
  ```

  

## 19.8 Properties 类

- 构造器

  - `Properties()`
    创建一个没有默认值的空属性列表。
  - `Properties(Properties defaults)`
    创建具有指定默认值的空属性列表。 

- 方法

  | 返回值类型 | 方法与描述                                                   |
  | ---------- | ------------------------------------------------------------ |
  | `String`   | `getProperty(String key)`  使用此属性列表中指定的键搜索属性。 |
  | `String`   | `getProperty(String key, String defaultValue)`  使用此属性列表中指定的键搜索属性。 |
  | `void`     | `list(PrintStream out)`  将此属性列表打印到指定的输出流。    |
  | `void`     | `list(PrintWriter out)`  将此属性列表打印到指定的输出流。    |
  | `void`     | `load(InputStream inStream)`  从输入字节流读取属性列表（键和元素对）。 |
  | `void`     | `load(Reader reader)`  以简单的线性格式从输入字符流读取属性列表（关键字和元素对）。 |
  | `void`     | `loadFromXML(InputStream in)`  将指定输入流中的XML文档表示的所有属性加载到此属性表中。 |
  | `Object`   | `setProperty(String key, String value)`  致电 `Hashtable`方法 `put` 。 |
  | `void`     | `store(OutputStream out, String comments)`  将此属性列表（键和元素对）写入此 `Properties`表中，以适合于使用 [`load(InputStream)`](../../java/util/Properties.html#load-java.io.InputStream-)方法加载到  `Properties`表中的格式输出流。 |
  | `void`     | `store(Writer writer, String comments)`  将此属性列表（键和元素对）写入此 `Properties`表中，以适合使用 [`load(Reader)`](../../java/util/Properties.html#load-java.io.Reader-)方法的格式输出到输出字符流。 |
  | `void`     | `storeToXML(OutputStream os, String comment)`  发出表示此表中包含的所有属性的XML文档。 |

- 案例

  ```java
  @Test
  public void test01() throws IOException {
      Properties ps = new Properties();
      ps.load(new FileReader("d:\\aa.txt"));
      ps.list(System.out);
      System.out.println("===========");
      System.out.println("用户名：" + ps.getProperty("user"));
      System.out.println("密码：" + ps.getProperty("password"));
  }
  ```

  ```java
  @Test
  public void test02() throws IOException {
      Properties ps = new Properties();
      ps.setProperty("user", "任超");
      ps.setProperty("password", "12345");
      ps.store(new FileWriter("d:\\aa.properties"),null);
  }
  ```

  

# 第 20 章 - 坦克大战3【未整理】

# 第 21 章 - 网络编程【未整理】

# 第 22 章 - 用户即时通信系统【未整理】





# 第 20 章 - 反射reflection[部分]

## 通过反射设置final修饰属性

[Java反射修改final修饰的属性值 - 简书 (jianshu.com)](https://www.jianshu.com/p/2d490b0155ad)

```java
Field modifier = Field.class.getDeclaredField("modifiers");
modifier.setAccessible(true);

Field restTemplateField = IpUtils.class.getDeclaredField("restTemplate");
restTemplateField.setAccessible(true);
modifier.setInt(restTemplateField, restTemplateField.getModifiers() & ~Modifier.FINAL);
restTemplateField.set(null, restTemplate);
// 需要注意内联优化，会出现修改成功，但读取的还是旧值(String,Integer等)
```



