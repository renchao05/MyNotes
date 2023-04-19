[10分钟讲清楚Java SLF4J，Java日志框架的扛把子，从原理到实践 #安员外很有码_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1aS4y1Y7iP)

# 日志框架介绍

![image-20220430175943602](https://renchao05.oss-cn-hangzhou.aliyuncs.com/img/image-20220430175943602.png)

![image-20220430180420305](https://renchao05.oss-cn-hangzhou.aliyuncs.com/img/image-20220430180420305.png)

![image-20220430180537888](https://renchao05.oss-cn-hangzhou.aliyuncs.com/img/image-20220430180537888.png)

![image-20220430180950472](https://renchao05.oss-cn-hangzhou.aliyuncs.com/img/image-20220430180950472.png)

![image-20220430183543122](https://renchao05.oss-cn-hangzhou.aliyuncs.com/img/image-20220430183543122.png)

![image-20220430183648523](https://renchao05.oss-cn-hangzhou.aliyuncs.com/img/image-20220430183648523.png)

# 应用实例

## slf4j 绑定 logback

- pom引入依赖

  ```xml
  <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-api</artifactId>
      <version>1.7.7</version>
  </dependency>
  
  <dependency>
      <groupId>ch.qos.logback</groupId>
      <artifactId>logback-classic</artifactId>
      <version>1.2.3</version>
  </dependency>
  ```

- 测试

  ```java
  import org.slf4j.Logger;
  import org.slf4j.LoggerFactory;
  
  public class TestLog {
      public static void main(String[] args) {
          Logger logger = LoggerFactory.getLogger(TestLog.class);
          logger.info("hello world!");
      }
  }
  ```

## slf4j 绑定 reload4j

- pom引入依赖

  ```xml
          <dependency>
              <groupId>org.slf4j</groupId>
              <artifactId>slf4j-api</artifactId>
              <version>1.7.7</version>
          </dependency>
  
          <dependency>
              <groupId>org.slf4j</groupId>
              <artifactId>slf4j-reload4j</artifactId>
              <version>1.7.36</version>
          </dependency>
  ```

- 配置文件 log4j.properties

  ```properties
  log4j.rootLogger=DEBUG, stdout
  #控制台输出
  log4j.appender.stdout=org.apache.log4j.ConsoleAppender
  log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
  log4j.appender.stdout.layout.ConversionPattern=%p [%t] - %m%n
  ```

- 测试

  ```java
  import org.slf4j.Logger;
  import org.slf4j.LoggerFactory;
  
  public class TestLog {
      public static void main(String[] args) {
          Logger logger = LoggerFactory.getLogger(TestLog.class);
          logger.info("hello world!");
      }
  }
  ```

  