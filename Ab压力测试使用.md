# Ab简介

ab是apache自带的压力测试工具,ab是apachebench命令的缩写。

ab不仅可以对apache服务器进行网站访问压力测试，也可以对或其它类型的服务器进行压力测试。

ab是一个httpd自带的很好用的压力测试工具，ab命令会创建多个并发访问线程，模拟多个访问者同时对某一URL地址进行访问。

可以用来测试apache的负载压力，也可以 用来测试nginx、lighthttp、tomcat、IIS等其它Web服务器的压力负载性能。

官网：https://httpd.apache.org/docs/2.4/programs/ab.html

示例：http://www.cnblogs.com/qmfsun/p/6476290.html

# Centos安装

**安装ab**

yum -y install httpd-tools

**查看版本**

[root@gzf~]# ab -V

[root@gzf~]# which ab

# 参数说明

查看帮助

[root@tj-32-42 ~]# ab --help

```shell
ab: wrong number of arguments
Usage: ab [options] [http[s]://]hostname[:port]/path
Options are:
-n 要执行请求数，默认会执行一个请求
-c 一次执行多个请求的数量，默认是一次一个请求。
-t 用于基准测试的最大秒数，使用它在固定的总时间内对服务器进行基准测试。默认情况下，没有时间限制。
-s 超时之前等待的最大秒数。 默认值是30秒。
-b TCP发送/接收缓冲区的大小，以字节为单位。
-B 进行传出连接时要绑定的地址。
-p 包含数据到POST的文件。 还请记住设置-T。
-u 包含PUT数据的文件。 还请记住设置-T 。
-T Content-type用于POST / PUT数据的内容类型内容类型标题，例如：'application/x-www-form-urlencoded' 默认是'text/plain'
-v verbosity 要打印多少个疑难解答信息，设置详细级别 - 4和以上打印标题信息，3和以上打印响应代码（404,200等），2和以上打印警告和信息。
-w 在HTML表格中打印结果。
-i 使用HEAD代替GET。
-x 用作<table>的属性的字符串。 属性被插入<table here>。
-y 用作<tr>的属性的字符串。
-z 用作<td>的属性的字符串。
-C 将cookie添加到请求。 参数通常采用名称=值对的形式。 这个字段是可重复的。
-H attribute 例如 ‘Accept-Encoding: gzip’ 插入所有普通标题行之后。（重复）
-A 添加基本的WWW认证，该属性是一个冒号分隔的用户名和密码，auth-username:password
-P 添加基本代理验证，属性是一个冒号分隔的用户名和密码，proxy-auth-username:password
-X 使用代理服务器和端口号。
-V 打印版本号并退出。
-k 使用HTTP KeepAlive功能。
-d 不要显示百分点服务表。
-S 不要显示信心估计和警告。
-q 做超过150个请求时不要显示进度。
-g 将收集的数据输出到gnuplot格式文件。
-e 输出提供百分比的CSV文件。
-r 不要退出套接字接收错误。
-h 显示使用情况信息（此消息）。
-Z 密码套件指定SSL / TLS密码套件（请参阅openssl密码）
-f 指定SSL / TLS协议 (SSL3, TLS1, TLS1.1, TLS1.2 or ALL)
```

# 关于登录的问题

有时候进行压力测试需要用户登录，怎么办？

请参考以下步骤：

先用账户和密码登录后，用开发者工具找到标识这个会话的Cookie值（Session ID）记下来

- 如果只用到一个Cookie，那么只需键入命令：
  - `ab －n 100 －C key＝value http://test.com/`
- 如果需要多个Cookie，就直接设Header：
  - `ab -n 100 -H “Cookie: Key1=Value1; Key2=Value2” http://test.com/`

# 测试结果说明

```shell
lin:~ pingguo$ ab -n 10000 -c 100 http://www.baidu.com/  
This is ApacheBench, Version 2.3 <$Revision: 1757674 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/  
Licensed to The Apache Software Foundation, http://www.apache.org/  

Benchmarking www.baidu.com (be patient)
Completed 1000 requests  

Server Software:        BWS/1.1         //服务器软件
Server Hostname:        www.baidu.com  //请求的地址
Server Port:            80              //请求的端口号

Document Path:          /           //页面路劲
Document Length:        112056 bytes  //页面长度

Concurrency Level:      100         //并发数
Time taken for tests:   119.428 seconds  //共使用多长时间
Complete requests:      1286    //请求数
Failed requests:        1284     //失败请求数
(Connect: 0, Receive: 0, Length: 1284, Exceptions: 0)  
Total transferred:      149524294 bytes  //总共传输字节数，包含http的头信息等
HTML transferred:       148232704 bytes  //html字节数，实际的页面传递字节数 
Requests per second:    10.77 [#/sec] (mean)  //每秒多少请求，这个是非常重要的参数数值，服务器的吞吐量
Time per request:       9286.783 [ms] (mean)  //用户平均请求等待时间 
Time per request:       92.868 [ms] (mean, across all   concurrent requests)        //服务器平均处理时间，也就是服务器吞吐量的倒数 
Transfer rate:          1222.66 [Kbytes/sec] received  //每秒获取的数据长度

Connection Times (ms)  
min  mean[+/-sd] median   max  
Connect:       91 1401 3495.4   1204   72808  Processing:  2788 6865 4579.5   5943   46294  
Waiting:       87 1363 591.0   1283    5082  
Total:       2996 8266 5699.1   7184   80615  

Percentage of the requests served within a certain time (ms)  
50%   7184        // 50%的请求在7184ms内返回 
66%   8651  
75%   9142  
80%   9460  
90%  10783  
95%  15674  
98%  25099  
99%  29224  
100%  80615 (longest request)    
lin:~ pingguo$ ab -n 100 -c 10 http://www.baidu.com/
This is ApacheBench, Version 2.3 <$Revision: 1757674 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/  
Licensed to The Apache Software Foundation, http://www.apache.org/  

Benchmarking www.baidu.com (be patient)...apr_pollset_poll: The timeout specified has expired (70007)  
Total of 99 requests completed  
```

# 其他压力工具

总的来说ab工具ab小巧简单，上手学习较快，可以提供需要的基本性能指标，但是没有图形化结果，不能监控。因此ab工具可以用作临时紧急任务和简单测试。
同类型的压力测试工具还有：webbench、siege、http_load等