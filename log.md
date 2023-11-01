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

  





# xml实例

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration debug="false">
    <!-- LOG目录 -->
    <property name="LOG_HOME" value="logs"/>
    <!-- JSON_LOG目录 -->
    <property name="JSON_LOG_HOME" value="logs/jsonlog"/>
    <!-- spring.application.name 作为参数 -->
    <springProperty scope="context" name="APP_NAME" source="spring.application.name"/>

    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <target>System.out</target>
        <encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">
            <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
            <charset>UTF-8</charset>
        </encoder>
    </appender>
    <!-- 按天压缩日志 -->
    <appender name="ZIP_FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>${LOG_HOME}/${APP_NAME}.log</file>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <!--日志文件输出的文件名-->
            <FileNamePattern>${LOG_HOME}/${APP_NAME}.log.%d{yyyy-MM-dd}.%i.log.zip</FileNamePattern>
            <timeBasedFileNamingAndTriggeringPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP">
                <!-- or whenever the file size reaches 100MB -->
                <maxFileSize>100MB</maxFileSize>
            </timeBasedFileNamingAndTriggeringPolicy>
        </rollingPolicy>
        <encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{50} - %msg%n</pattern>
            <charset>UTF-8</charset>
        </encoder>
    </appender>
    <!-- 不压缩日志,保留7天 -->
    <appender name="DEFAULT_INFO_FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <!--日志文件输出的文件名-->
            <FileNamePattern>${LOG_HOME}/${APP_NAME}.log.%d{yyyy-MM-dd}.%i.log</FileNamePattern>
            <maxHistory>7</maxHistory>
            <timeBasedFileNamingAndTriggeringPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP">
                <!-- or whenever the file size reaches 100MB -->
                <maxFileSize>100MB</maxFileSize>
            </timeBasedFileNamingAndTriggeringPolicy>
        </rollingPolicy>
        <encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{50} - %msg%n</pattern>
            <charset>UTF-8</charset>
        </encoder>
    </appender>
    <!-- LOGSTASH,输出seuleth项,保留7天 -->
    <appender name="LOGSTASH" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <!--日志文件输出的文件名-->
            <FileNamePattern>${JSON_LOG_HOME}/${APP_NAME}.json.%d{yyyy-MM-dd}.%i.log</FileNamePattern>
            <maxHistory>7</maxHistory>
            <timeBasedFileNamingAndTriggeringPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP">
                <!-- or whenever the file size reaches 100MB -->
                <maxFileSize>100MB</maxFileSize>
            </timeBasedFileNamingAndTriggeringPolicy>
        </rollingPolicy>
        <encoder charset="UTF-8" class="net.logstash.logback.encoder.LoggingEventCompositeJsonEncoder">
            <providers>
                <pattern>
                    <pattern>
                        {
                        "timestamp": "%d{yyyy-MM-dd HH:mm:ss.SSS}",
                        "severity": "%level",
                        "service": "${APP_NAME:-}",
                        "trace": "%X{X-B3-TraceId:-}",
                        "span": "%X{X-B3-SpanId:-}",
                        "parent": "%X{X-B3-ParentSpanId:-}",
                        "exportable": "%X{X-Span-Export:-}",
                        "pid": "${PID:-}",
                        "thread": "%thread",
                        "class": "%logger{40}",
                        "rest": "%message"
                        }
                    </pattern>
                </pattern>
            </providers>
        </encoder>
    </appender>
    <!-- 按天压缩Json日志 -->
    <appender name="JSON_ZIP_FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>${JSON_LOG_HOME}/${APP_NAME}.json.log</file>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <!--日志文件输出的文件名-->
            <FileNamePattern>${JSON_LOG_HOME}/${APP_NAME}.log.%d{yyyy-MM-dd}.%i.json.log.zip</FileNamePattern>
            <timeBasedFileNamingAndTriggeringPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP">
                <!-- or whenever the file size reaches 100MB -->
                <maxFileSize>100MB</maxFileSize>
            </timeBasedFileNamingAndTriggeringPolicy>
        </rollingPolicy>
        <encoder charset="UTF-8" class="net.logstash.logback.encoder.LoggingEventCompositeJsonEncoder">
            <providers>
                <pattern>
                    <pattern>
                        {
                        "timestamp": "%d{yyyy-MM-dd HH:mm:ss.SSS}",
                        "severity": "%level",
                        "service": "${APP_NAME:-}",
                        "trace": "%X{X-B3-TraceId:-}",
                        "span": "%X{X-B3-SpanId:-}",
                        "parent": "%X{X-B3-ParentSpanId:-}",
                        "exportable": "%X{X-Span-Export:-}",
                        "pid": "${PID:-}",
                        "thread": "%thread",
                        "class": "%logger{40}",
                        "rest": "%message"
                        }
                    </pattern>
                </pattern>
            </providers>
        </encoder>
    </appender>
    <appender name="STDERR" class="ch.qos.logback.core.ConsoleAppender">
        <target>System.err</target>
        <encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">
            <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>

    <logger name="org.apache.http" level="error"/>


    <!-- SiftingAppender，根据 MDC 属性 sift 日志 MDC.put("requestId", "当前请求标识"); -->
    <appender name="SIFT" class="ch.qos.logback.classic.sift.SiftingAppender">
        <discriminator>
            <!-- 使用 MDC 属性 "requestId" 作为区分标识 -->
            <key>requestId</key>
            <defaultValue>unknown</defaultValue>
        </discriminator>
        <sift>
            <appender name="FILE-${requestId}" class="ch.qos.logback.core.FileAppender">
                <file>sync-logs/${requestId}.log</file>
                <encoder>
                    <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
                </encoder>
            </appender>
        </sift>
    </appender>

    <!-- 配置特定类的日志输出 -->
    <logger name="com.jiuyv.sptcc.agile.batch.service.BatchService" level="DEBUG">
        <appender-ref ref="SIFT" />
    </logger>

    <root>
        <level value="INFO"/>
        <appender-ref ref="STDOUT"/>
        <appender-ref ref="ZIP_FILE"/>
        <appender-ref ref="DEFAULT_INFO_FILE"/>
        <appender-ref ref="LOGSTASH"/>
        <appender-ref ref="JSON_ZIP_FILE"/>
    </root>
</configuration>
```

