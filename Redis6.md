# 一、NoSQL简介

[【尚硅谷】Redis 6 入门到精通 超详细 教程_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Rv41177Af)

Redis 命令参考:
[http://redisdoc.com/persistence/bgsave.html](http://redisdoc.com/persistence/bgsave.html)
## 1、技术发展
**技术的分类**

- **功能性：**
   - Java、Jsp、RDBMS、Tomcat、HTML、Linux、JDBC、SVN
- **扩展性：**
   - Struts、Spring、SpringMVC、Hibernate、Mybatis
- **性能：**
   - NoSQL、Java线程、Hadoop、Nginx、MQ、ElasticSearch
### 1.1、Web1.0时代
Web1.0的时代，数据访问量很有限，用一夫当关的高性能的单点服务器可以解决大部分问题。
![image.png](image/1653612393957-b7866d05-c2ac-4975-b043-f1161d9ba9ab.png)
### 1.2、Web2.0时代
随着Web2.0的时代的到来，用户访问量大幅度提升，同时产生了大量的用户数据。加上后来的智能移动设备的普及，所有的互联网平台都面临了巨大的性能挑战。
![image.png](image/1653612483709-af9df9ef-3f6f-4a6c-97a4-28e3f7bce88c.png)
### 1.3、解决CPU及内存压力
![image.png](image/1653612545820-792cae1d-0178-474c-b897-366d94331699.png)
### 1.4、解决IO压力
![image.png](image/1653612569926-01fa692e-6a45-494a-be2d-40e197414fd4.png)
## 2、NoSQL数据库
### 2.1、NoSQL数据库概述
NoSQL(NoSQL = **Not Only SQL** )，意即“不仅仅是SQL”，泛指**非关系型的数据库**。 
NoSQL 不依赖业务逻辑方式存储，而以简单的key-value模式存储。因此大大的增加了数据库的扩展能力。

- 不遵循SQL标准。
- 不支持ACID。
- 远超于SQL的性能。
### 2.2、NoSQL适用场景 

- 对数据高并发的读写
- 海量数据的读写
- 对数据高可扩展性的
### 2.3、NoSQL不适用场景

- 需要事务支持
- 基于sql的结构化查询存储，处理复杂的关系,需要即席查询。
- （用不着sql的和用了sql也不行的情况，也可以考虑用NoSql）
### 2.4、Memcache
![image.png](image/1653613111752-a435a6b9-e5e2-4414-bcde-7cb892f57f33.png)

- 很早出现的NoSql数据库
- 数据都在内存中，一般不持久化
- 支持简单的key-value模式，支持类型单一
- 一般是作为缓存数据库辅助持久化的数据库
### 2.5、Redis
![image.png](image/1653613225885-7b0b5787-3a6a-47f0-ac76-61b503492034.png)

- 几乎覆盖了Memcached的绝大部分功能
- 数据都在内存中，支持持久化，主要用作备份恢复
- 除了支持简单的key-value模式，还支持多种数据结构的存储，比如 list、set、hash、zset等。
- 一般是作为缓存数据库辅助持久化的数据库
### 2.6、MongoDB

- 高性能、开源、模式自由(schema  free)的文档型数据库
- 数据都在内存中， 如果内存不足，把不常用的数据保存到硬盘
- 虽然是key-value模式，但是对value（尤其是json）提供了丰富的查询功能
- 支持二进制数据及大型对象
- 可以根据数据的特点替代RDBMS ，成为独立的数据库。或者配合RDBMS，存储特定的数据。
## 3、大数据时代
### 3.1、行式数据库
![image.png](image/1653613588900-8bb0f116-f219-4609-93f3-ff639fc92350.png)
### 3.2、列式数据库
![image.png](image/1653613613135-4b59fbdb-cc74-404c-b534-73a4cead8664.png)
#### 3.2.1、Hbase
HBase是Hadoop项目中的数据库。它用于需要对大量的数据进行随机、实时的读写操作的场景中。
HBase的目标就是处理数据量**非常庞大**的表，可以用普通的计算机处理超过10亿行数据，还可处理有数百万列元素的数据表。
#### 3.2.2、Cassandra
Apache Cassandra是一款免费的开源NoSQL数据库，其设计目的在于管理由大量商用服务器构建起来的庞大集群上的**海量数据集(数据量通常达到PB级别)**。在众多显著特性当中，Cassandra最为卓越的长处是对写入及读取操作进行规模调整，而且其不强调主集群的设计思路能够以相对直观的方式简化各集群的创建与扩展流程。
## 4、图关系型数据库
![image.png](image/1653613864413-06376fc7-28e0-4c90-b462-b03b83acd803.png)
主要应用：社会关系，公共交通网络，地图及网络拓谱(n*(n-1)/2)
![image.png](image/1653613879786-63c5776c-cea1-498d-b035-48dededba955.png)
## 5、DB-Engines 数据库排名
[http://db-engines.com/en/ranking](http://db-engines.com/en/ranking)
![image.png](image/1653613983485-c6c321ad-7757-4733-8f2f-6274da911c15.png)
# 二、概述与安装

- Redis是一个**开源**的**key-value**存储系统。
- 和Memcached类似，它支持存储的value类型相对更多，包括**string**(字符串)、**list**(链表)、**set**(集合)、**zset**(sorted set --有序集合)和**hash**（哈希类型）。
- 这些数据类型都支持push/pop、add/remove及取交集并集和差集及更丰富的操作，而且这些操作都是**原子性**的。
- 在此基础上，Redis支持各种不同方式的**排序**。
- 与memcached一样，为了保证效率，数据都是**缓存在内存中**。
- 区别的是Redis会**周期性**的把更新的**数据写入磁盘**或者把修改操作写入追加的记录文件。
- 并且在此基础上实现了**master-slave(主从)**同步。
## 1、应用场景
### 1.1、配合关系型数据库做高速缓存

- 高频次，热门访问的数据，降低数据库IO
- 分布式架构，做session共享

![image.png](image/1653611982618-a6343bd9-246c-431b-b7e9-e17c0054eaf6.png)
### 1.2、多样的数据结构存储持久化数据
![image.png](image/1653614172942-bcfc8d53-0399-4183-a3b6-3b6fdf3a1830.png)
## 2、安装
| Redis官方网站                      | Redis中文官方网站                    |
| ---------------------------------- | ------------------------------------ |
| [http://redis.io](http://redis.io) | [http://redis.cn/](http://redis.cn/) |

### 2.1、安装版本

- 6.0.6 for Linux（redis-6.0.6.tar.gz）
- 不用考虑在windows环境下对Redis的支持
### 2.2、安装步骤

- 准备工作：下载安装最新版的gcc编译器安装C 语言的编译环境
```bash
yum install centos-release-scl scl-utils-build
yum install -y devtoolset-8-toolchain
scl enable devtoolset-8 bash

#测试 gcc版本
gcc --version
```

- 下载 redis-6.0.6.tar.gz   在/opt目录
wget http://download.redis.io/releases/redis-6.0.6.tar.gz
-  解压命令：`tar -zxvf redis-6.0.6.tar.gz` 
-  解压完成后进入目录：`cd redis-6.0.6` 
-  在 redis-6.0.6目录下执行 `make` 命令（只是编译好） 
-  如果没有准备好C语言编译环境，make 会报错—Jemalloc/jemalloc.h：没有那个文件 
-  解决方案：运行 `make distclean` 
-  在 redis-6.0.6 目录下再次执行 `make` 命令 
-  跳过 make test 继续执行: `make install` 
### 2.3、安装目录
> /usr/local/bin

查看默认安装目录：
`redis-benchmark`：性能测试工具，可以在自己本子运行，看看自己本子性能如何
`redis-check-aof`：修复有问题的AOF文件，rdb和aof后面讲
`redis-check-dump`：修复有问题的dump.rdb文件
`redis-sentinel`：Redis集群使用
`redis-server`：Redis服务器启动命令
`redis-cli`：客户端，操作入口
### 2.4、前台启动（不推荐）
在安装目录执行：`redis-server`
> 前台启动，命令行窗口不能关闭，否则服务器停止

### 2.5、后台启动（推荐）

-  备份 redis.conf，拷贝一份到其他目录
`cp /opt/redis-6.0.6/redis.conf /myredis/redis.conf` 
-  后台启动设置 redis.conf 中的 `daemonize no` 改成 `daemonize yes` 
-  Redis启动
`redis-server /myredis/redis.conf` 
-  用客户端访问：`redis-cli` 
-  多个端口可以：`redis-cli -p6379` 
-  测试验证： `ping` 
-  Redis关闭
   - 单实例关闭：`redis-cli shutdown`
   - 也可以进入终端后再执行 `shutdown` 关闭
   - 多实例关闭，指定端口关闭：`redis-cli -p 6379 shutdown`
### 2.6、开机启动

- 在 /usr/lib/systemd/system 目录下新建 redis.service 文件。
   - `vim /usr/lib/systemd/system/redis.service`
```bash
[Unit]
Description=Redis-Server
After=network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
ExecStart=/usr/local/bin/redis-server /root/redis.conf
ExecStop=kill -9 $(pidof redis-server)
ExecReload=kill -9 $(pidof redis-server) && /usr/local/bin/redis-server /root/redis.conf

[Install]
WantedBy=multi-user.target
```

- 重新加载服务文件：`systemctl daemon-reload`
```bash
# 启用开机自启
systemctl enable redis

# 禁用开机自启
systemctl disable redis

# 启动服务
service redis start

# 终止服务
service redis stop

# 重启服务
service redis restart
```
### 2.6、Redis介绍相关知识
#### 2.6.1、端口6379从何而来
![image.png](image/1653615018763-60e58f20-70a7-470f-9a1c-7863bc9afeca.png)
6379在是手机按键上MERZ对应的号码，而MERZ取自意大利歌女**Alessia Merz**的名字。MERZ长期以来被Redis作者antirez及其朋友当作愚蠢的代名词。后来Redis作者在开发Redis时就选用了这个端口。
#### 2.6.2、数据库

- 默认16个数据库，类似数组下标从0开始，初始默认使用0号库
- 使用命令 select   <dbid>来切换数据库。如: select 8 
- 统一密码管理，所有库同样密码。
- `dbsize`查看当前数据库的key的数量
- `flushdb`清空当前库
- `flushall`通杀全部库
#### 2.6.3、单线程+多路IO复用技术

- 多路复用是指使用一个线程来检查多个文件描述符（Socket）的就绪状态，比如调用select和poll函数，传入多个文件描述符，如果有一个文件描述符就绪，则返回，否则阻塞直到超时。得到就绪状态后进行真正的操作可以在同一个线程里执行，也可以启动线程执行（比如使用线程池）。
- **串行   vs   多线程+锁（memcached） vs   单线程+多路IO复用(Redis)**
- （与Memcache三点不同: **支持多数据类型，支持持久化，单线程+多路IO复用**）  

![图片1](image/%E5%9B%BE%E7%89%871.gif)
## 3、连接远程Redis
### 3.1、格式

- 先连接
   - `redis-cli -h <hostname> -p <port> [-c]`
- 然后验证密码
   - `auth password`
### 3.2、连接阿里云Redis
```shell
[root@renchao ~]# redis-cli -h r-bp1fba542pdbzt9yv7pd.redis.rds.aliyuncs.com -p 6379
r-bp1fba542pdbzt9yv7pd.redis.rds.aliyuncs.com:6379> auth user:password
OK
```
> 阿里云Redis的密码是**账号:密码**【是redis里面的账号密码，不是阿里云账号密码】

# 三、常用五大数据类型
哪里去获得redis常见数据类型操作命令[http://www.redis.cn/commands.html](http://www.redis.cn/commands.html)
## 1、Redis键(key)
| **命令**      | **说明**                                                     |
| ------------- | ------------------------------------------------------------ |
| keys *        | 查看当前库所有key (匹配：keys *1)                            |
| exists key    | 判断某个key是否存在                                          |
| type key      | 查看你的key是什么类型                                        |
| del key       | 删除指定的key数据                                            |
| unlink key    | 根据value选择非阻塞删除,仅将keys从keyspace元数据中删除，真正的删除会在后续异步操作。 |
| expire key 10 | 10秒钟：为给定的key设置过期时间                              |
| ttl key       | 查看还有多少秒过期，-1表示永不过期，-2表示已过期             |

| **命令** | **说明**                  |
| -------- | ------------------------- |
| select   | 切换数据库                |
| dbsize   | 查看当前数据库的key的数量 |
| flushdb  | 清空当前库                |
| flushall | 通杀全部库                |

## 2、字符串(String)
### 2.1、简介
String 是 Redis 最基本的类型，你可以理解成与Memcached一模一样的类型，一个key对应一个value。
String类型是二进制安全的。意味着Redis的string可以包含任何数据。比如jpg图片或者序列化的对象。
String类型是Redis最基本的数据类型，一个Redis中字符串value最多可以是512M。
### 2.2、常用命令
| **命令**                     | **说明**                                                     |
| ---------------------------- | ------------------------------------------------------------ |
| `set <key><value>`           | 添加键值对                                                   |
| `get <key>`                  | 查询对应键值                                                 |
| `append <key><value>`        | 将给定的<value> 追加到原值的末尾                             |
| `strlen <key>`               | 获得值的长度                                                 |
| `setnx <key><value>`         | 只有在 key 不存在时,设置 key 的值                            |
| `incr <key>`                 | 将 key 中储存的数字值增1(只能对数字值操作，如果为空，新增值为1) |
| `decr <key>`                 | 将 key 中储存的数字值减1(只能对数字值操作，如果为空，新增值为-1) |
| `incrby/decrby <key> <步长>` | 自定义步长。将 key 中储存的数字值增减。                      |

> *NX：当数据库中key不存在时，可以将key-value添加数据库
> *XX：当数据库中key存在时，可以将key-value添加数据库，与NX参数互斥
> *EX：key的超时秒数
> *PX：key的超时毫秒数，与EX互斥

| **命令**                                    | **说明**                                                     |
| ------------------------------------------- | ------------------------------------------------------------ |
| `mset <key1><value1><key2><value2>.....`    | 同时设置一个或多个 key-value对                               |
| `mget <key1><key2><key3>.....`              | 同时获取一个或多个 value                                     |
| `msetnx <key1><value1><key2><value2>..... ` | 同时设置一个或多个 key-value 对，当且仅当所有给定 key 都不存在。 |
| `getrange <key><起始位置><结束位置>`        | 获得值的范围，类似java中的substring，前包，后包              |
| `setrange <key><起始位置><value>`           | 用<value>覆写<key>所储存的字符串值，从<起始位置>开始(索引从0开始)。 |
| `setex <key><过期时间><value>`              | 设置键值的同时，设置过期时间，单位秒。                       |
| `getset <key><value>`                       | 以新换旧，设置了新值同时获得旧值。                           |

> msetnx 是原子性，有一个失败则都失败。

### 2.3、原子性
所谓原子操作是指不会被线程调度机制打断的操作。
这种操作一旦开始，就一直运行到结束，中间不会有任何 context switch （切换到另一个线程）。

- 在单线程中， 能够在单条指令中完成的操作都可以认为是"原子操作"，因为中断只能发生于指令之间。
- 在多线程中，不能被其它进程（线程）打断的操作就叫原子操作。

Redis单命令的原子性主要得益于Redis的单线程。
### 2.3、数据结构
String的数据结构为简单动态字符串(Simple Dynamic String,缩写SDS)。是可以修改的字符串，内部结构实现上类似于Java的ArrayList，采用预分配冗余空间的方式来减少内存的频繁分配。
 ![image.png](image/1653619596905-d28bb314-8007-4366-bc96-3a770bab6166.png)
如图中所示，内部为当前字符串实际分配的空间 capacity 一般要高于实际字符串长度len。
当字符串长度**小于1M时**，扩容都是加倍现有的空间
**如果超过1M**，扩容时一次只会多扩1M的空间。需要注意的是字符串**最大长度为512M**。

## 3、列表(List)
### 3.1、简介
单键多值
Redis 列表是简单的字符串列表，按照插入顺序排序。
你可以添加一个元素到列表的头部（左边）或者尾部（右边）。
它的底层实际是个双向链表，对两端的操作性能很高，通过索引下标的操作中间的节点性能会较差。
![image.png](image/1653622979618-9dd09f70-f2ae-473e-b988-66d9d2bf21a4.png)
### 3.2、常用命令
| **命令**                                        | **说明**                                           |
| ----------------------------------------------- | -------------------------------------------------- |
| `lpush/rpush <key><value1><value2><value3>....` | 从左边/右边插入一个或多个值。                      |
| `lpop/rpop <key>`                               | 从左边/右边吐出一个值。值在键在，值光键亡。        |
| `rpoplpush <key1><key2>`                        | 从<key1>列表右边吐出一个值，插到<key2>列表左边。   |
| `lrange <key><start><stop>`                     | 按照索引下标获得元素(从左到右)（0 -1表示获取所有） |
| `lindex <key><index>`                           | 按照索引下标获得元素(从左到右)                     |
| `llen <key>`                                    | 获得列表长度                                       |
| `linsert <key> before/after <value><newvalue>`  | 在<value>的前/后面插入<newvalue>插入值             |
| `lrem <key><n><value>`                          | 从左边删除n个value(从左到右)【删除相同的元素】     |
| `lset <key><index><value>`                      | 将列表key下标为index的值替换成value                |

### 3.3、数据结构
List 的数据结构为快速链表 quickList。
首先在列表元素较少的情况下会使用一块连续的内存存储，这个结构是ziplist，也即是压缩列表。
它将所有的元素紧挨着一起存储，分配的是一块连续的内存。
当数据量比较多的时候才会改成quicklist。
因为普通的链表需要的附加指针空间太大，会比较浪费空间。比如这个列表里存的只是int类型的数据，结构上还需要两个额外的指针 prev 和 next。
 ![image.png](image/1653623000474-6be07416-f69c-44f3-8dfe-db1456b9155f.png)
Redis将链表和ziplist结合起来组成了quicklist。也就是将多个ziplist使用双向指针串起来使用。这样既满足了快速的插入删除性能，又不会出现太大的空间冗余。

## 4、集合(Set)
### 4.1、简介
Redis set对外提供的功能与list类似是一个列表的功能，特殊之处在于set是可以自动排重的，当你需要存储一个列表数据，又不希望出现重复数据时，set是一个很好的选择，并且set提供了判断某个成员是否在一个set集合内的重要接口，这个也是list所不能提供的。
Redis的Set是string类型的无序集合。它底层其实是一个value为null的hash表，所以添加，删除，查找的复杂度都是O(1)。
### 4.2、常用命令
| **命令**                           | **说明**                                                     |
| ---------------------------------- | ------------------------------------------------------------ |
| `sadd <key><value1><value2>.....`  | 将一个或多个 member 元素加入到集合 key 中，已经存在的 member 元素将被忽略 |
| `smembers <key>`                   | 取出该集合的所有值。                                         |
| `sismember <key><value>`           | 判断集合<key>是否为含有该<value>值，有1，没有0               |
| `scard<key>`                       | 返回该集合的元素个数。                                       |
| `srem <key><value1><value2> ....`  | 删除集合中的某个元素。                                       |
| `spop <key>`                       | 随机从该集合中吐出一个值。**吐出多个，后面加上对应的数值**   |
| `srandmember <key><n>`             | 随机从该集合中取出n个值。不会从集合中删除 。                 |
| `smove <source><destination>value` | 把集合中一个值从一个集合移动到另一个集合                     |
| `sinter <key1><key2>`              | 返回两个集合的交集元素。【也可以多个】                       |
| `sunion <key1><key2>`              | 返回两个集合的并集元素。【也可以多个】                       |
| `sdiff <key1><key2>`               | 返回两个集合的差集元素(key1中的，不包含key2中的)【也可以多个，相当于k1-k2-k3-kn】 |

### 4.3、数据结构
Set 数据结构是 dict 字典，字典是用哈希表实现的。
Java中HashSet的内部实现使用的是HashMap，只不过所有的value都指向同一个对象。Redis的set结构也是一样，它的内部也使用hash结构，所有的value都指向同一个内部值。
## 5、哈希(Hash)
### 5.1、简介
Redis hash 是一个键值对集合。
Redis hash是一个string类型的field和value的映射表，hash特别适合用于存储对象。
类似Java里面的Map<String,Object>
用户ID为查找的key，存储的value用户对象包含姓名，年龄，生日等信息。
如果用普通的key/value结构来存储，主要有以下2种存储方式：
 ![image.png](image/1653624200672-3dde32d6-9c78-4ca2-a1b6-0785bf66e29b.png)
![image.png](image/1653624238161-dc193cb6-0c70-4b36-b87b-cabc5e878161.png)
通过 **key(用户ID) + field(属性标签) **就可以操作对应属性数据了，既不需要重复存储数据，也不会带来序列化和并发修改控制的问题
### 5.2、常用命令
| **命令**                                        | **说明**                                                     |
| ----------------------------------------------- | ------------------------------------------------------------ |
| hset <key><field><value>                        | 给<key>集合中的 <field>键赋值<value>【也可以批量】           |
| hget <key1><field>                              | 从<key1>集合<field>取出 value                                |
| hmset <key1><field1><value1><field2><value2>... | 批量设置hash的值【过时，新版hset 也可以批量操作】            |
| hexists <key1><field>                           | 查看哈希表 key 中，给定域 field 是否存在。                   |
| hkeys <key>                                     | 列出该hash集合的所有field                                    |
| hvals <key>                                     | 列出该hash集合的所有value                                    |
| hincrby <key><field><increment>                 | 为哈希表 key 中的域 field 的值加上增量 1 -1                  |
| hsetnx <key><field><value>                      | 将哈希表 key 中的域 field 的值设置为 value ，当且仅当域 field 不存在 |

### 5.3、数据结构
Hash类型对应的数据结构是两种：ziplist（压缩列表），hashtable（哈希表）。
当field-value长度较短且个数较少时，使用ziplist，否则使用hashtable。
## 6、有序集合Zset(sorted set) 
### 6.1、简介
Redis有序集合zset与普通集合set非常相似，是一个没有重复元素的字符串集合。
不同之处是有序集合的每个成员都关联了一个评分（score）,这个评分（score）被用来按照从最低分到最高分的方式排序集合中的成员。集合的成员是唯一的，但是评分可以是重复了 。
因为元素是有序的, 所以你也可以很快的根据评分（score）或者次序（position）来获取一个范围的元素。
访问有序集合的中间元素也是非常快的,因此你能够使用有序集合作为一个没有重复成员的智能列表。
### 6.2、常用命令
| **命令**                                    | **说明**                                                     |
| ------------------------------------------- | ------------------------------------------------------------ |
| zadd <key><score1><value1><score2><value2>… | 将一个或多个 member 元素及其 score 值加入到有序集 key 当中。 |
| zrange <key><start><stop> [WITHSCORES]      | 返回指定范围有序集 key 的元素。WITHSCORES让分数和值一起返回。 |
| zrangebyscore key min max                   | 返回 score 值指定范围 有序集 key 的元素(min < V < max )。(从小到大)。 |
| zrevrangebyscore key max min                | 同上，改为从大到小排列。                                     |
| zincrby <key><increment><value>             | 为元素的score加上增量                                        |
| zrem <key><value>                           | 删除该集合下，指定值的元素                                   |
| zcount <key><min><max>                      | 统计该集合，分数区间内的元素个数                             |
| zrank <key><value>                          | 返回该值在集合中的排名，从0开始。                            |

案例：如何利用zset实现一个文章访问量的排行榜？
### 6.3、数据结构
SortedSet(zset)是Redis提供的一个非常特别的数据结构，一方面它等价于Java的数据结构Map<String, Double>，可以给每一个元素value赋予一个权重score，另一方面它又类似于TreeSet，内部的元素会按照权重score进行排序，可以得到每个元素的名次，还可以通过score的范围来获取元素的列表。
zset底层使用了两个数据结构

- hash，hash的作用就是关联元素value和权重score，保障元素value的唯一性，可以通过元素value找到相应的score值。
- 跳跃表，跳跃表的目的在于给元素value排序，根据score的范围获取元素列表。
### 6.4、跳跃表（跳表）
#### 6.4.1、简介
有序集合在生活中比较常见，例如根据成绩对学生排名，根据得分对玩家排名等。对于有序集合的底层实现，可以用数组、平衡树、链表等。数组不便元素的插入、删除；平衡树或红黑树虽然效率高但结构复杂；链表查询需要遍历所有效率低。Redis采用的是跳跃表。跳跃表效率堪比红黑树，实现远比红黑树简单。
#### 6.4.2、实例
对比有序链表和跳跃表，从链表中查询出51

- 有序链表
![image.png](image/1653624675197-e32f314b-08ba-48b4-b627-f67818a55c79.png)
要查找值为51的元素，需要从第一个元素开始依次查找、比较才能找到。共需要6次比较。
- 跳跃表
![image.png](image/1653624732033-24ef60e4-4fbe-4fb9-848d-379a422d5cfc.png)
从第2层开始，1节点比51节点小，向后比较。
21节点比51节点小，继续向后比较，后面就是NULL了，所以从21节点向下到第1层
在第1层，41节点比51节点小，继续向后，61节点比51节点大，所以从41向下
在第0层，51节点为要查找的节点，节点被找到，共查找4次。

从此可以看出跳跃表比有序链表效率要高

# 四、配置文件
> 自定义目录/redis.conf

## 1、Units（单位）
配置大小单位,开头定义了一些基本的度量单位，只支持bytes，不支持bit
大小写不敏感
## 2、INCLUDES（包含）
类似jsp中的include，多实例的情况可以把公用的配置文件提取出来
## 3、NETWORK（网络）
### 3.1、bind
默认情况bind=127.0.0.1只能接受本机的访问请求
服务器是需要远程访问的，需要将其注释掉
如果开启了protected-mode，那么在没有设定bind ip且没有设密码的情况下，Redis只允许接受本机的响应。
### 3.2、protected-mode
本机访问保护模式
### 3.3、Port
端口号，默认 6379
### 3.4、tcp-backlog
设置tcp的backlog，backlog其实是一个连接队列，backlog队列总和 = 未完成三次握手队列 + 已经完成三次握手队列。
在高并发环境下你需要一个高backlog值来避免慢客户端连接问题。
> 注意：
> Linux内核会将这个值减小到`/proc/sys/net/core/somaxconn`的值（128）
> 所以需要确认增大`/proc/sys/net/core/somaxconn`和`/proc/sys/net/ipv4/tcp_max_syn_backlog`（128）两个值来达到想要的效果

### 3.5、timeout
一个空闲的客户端维持多少秒会关闭，0表示关闭该功能。即永不关闭。
### 3.6、tcp-keepalive
对访问客户端的一种心跳检测，每个n秒检测一次。
单位为秒，如果设置为0，则不会进行Keepalive检测，建议设置成60 
## 4、GENERAL（通用）
### 4.1、daemonize
是否为后台进程，设置为 yes
守护进程，后台启动
### 4.2、pidfile
存放pid文件的位置，每个实例会产生一个不同的pid文件
### 4.3、loglevel 
指定日志记录级别，Redis总共支持四个级别：
debug、verbose、notice、warning，**默认为notice**
四个级别根据使用阶段来选择，生产环境选择notice 或者warning
### 4.4、logfile 
日志文件名称
4.5、databases 16 
设定库的数量 默认16
默认数据库为0，可以使用`SELECT <dbid>`命令在连接上指定数据库id
## 5、SECURITY（安全）
### 5.1、设置密码
访问密码的查看、设置和取消
在命令中设置密码，只是临时的。重启redis服务器，密码就还原了。
永久设置，需要在配置文件中进行设置。
## 6、LIMITS（限制）
### 6.1、maxclients
设置redis同时可以与多少个客户端进行连接。
默认情况下为10000个客户端。
如果达到了此限制，redis则会拒绝新的连接请求，并且向这些连接请求方发出“max number of clients reached”以作回应。
### 6.2、maxmemory 
最大内存
建议必须设置，否则，将内存占满，造成服务器宕机。
设置redis可以使用的内存量。一旦到达内存使用上限，redis将会试图移除内部数据，移除规则可以通过maxmemory-policy来指定。
如果redis无法根据移除规则来移除内存中的数据，或者设置了“不允许移除”，那么redis则会针对那些需要申请内存的指令返回错误信息，比如SET、LPUSH等。
但是对于无内存申请的指令，仍然会正常响应，比如GET等。如果你的redis是主redis（说明你的redis有从redis），那么在设置内存使用上限时，需要在系统中留出一些内存空间给同步队列缓存，只有在你设置的是“不移除”的情况下，才不用考虑这个因素。
### 6.3、maxmemory-policy
volatile-lru：使用LRU算法移除key，只对设置了过期时间的键；（最近最少使用）
allkeys-lru：在所有集合key中，使用LRU算法移除key
volatile-random：在过期集合中移除随机的key，只对设置了过期时间的键
allkeys-random：在所有集合key中，移除随机的key
volatile-ttl：移除那些TTL值最小的key，即那些最近要过期的key
noeviction：不进行移除。针对写操作，只是返回错误信息
### 6.4、maxmemory-samples
设置样本数量，LRU算法和最小TTL算法都并非是精确的算法，而是估算值，所以你可以设置样本的大小，redis默认会检查这么多个key并选择其中LRU的那个。
一般设置3到7的数字，数值越小样本越不准确，但性能消耗越小。
# 五、发布和订阅
## 1、什么是发布和订阅
Redis 发布订阅 (pub/sub) 是一种消息通信模式：发送者 (pub) 发送消息，订阅者 (sub) 接收消息。
Redis 客户端可以订阅任意数量的频道。
## 2、发布和订阅
客户端可以订阅频道如下图
 ![image.png](image/1653651147248-d22c92ac-aa26-4bbe-9d52-17583abf56b3.png)
当给这个频道发布消息后，消息就会发送给订阅的客户端
![image.png](image/1653651237673-37f95f5e-4352-499c-b22e-b979562780dc.png)
## 3、发布订阅命令

- 打开一个客户端订阅channel1
   - `SUBSCRIBE channel1`
- 打开另一个客户端，给channel1发布消息hello
   - `publish channel1 hello`
   - 返回的1是订阅者数量
- 打开第一个客户端可以看到发送的消息
> 注：
> 发布的消息没有持久化，如果在订阅的客户端收不到hello，只能收到订阅后发布的消息

# 六、新数据类型
## 1、Bitmaps
### 1.1、简介
现代计算机用二进制（位） 作为信息的基础单位， 1个字节等于8位， 例如“abc”字符串是由3个字节组成， 但实际在计算机存储时将其用二进制表示， “abc”分别对应的ASCII码分别是97、 98、 99， 对应的二进制分别是01100001、 01100010和01100011，如下图
 ![image.png](image/1653667567933-9c8a6331-b2f3-4895-8dc0-a293c0e35fae.png)
合理地使用操作位能够有效地提高内存使用率和开发效率。
Redis提供了Bitmaps这个“数据类型”可以实现对位的操作：

- Bitmaps本身不是一种数据类型， 实际上它就是字符串（key-value） ， 但是它可以对字符串的位进行操作。
- Bitmaps单独提供了一套命令， 所以在Redis中使用Bitmaps和使用字符串的方法不太相同。 
- 可以把Bitmaps想象成一个以位为单位的数组， 数组的每个单元只能存储0和1， 数组的下标在Bitmaps中叫做偏移量。
![image.png](image/1653667734884-5bfc622f-cfc4-4141-80b3-27720214e3b6.png)
### 1.2、命令
#### 1.2.1、setbit
设置Bitmaps中某个偏移量的值（0或1）

- 格式
   - `setbit<key><offset><value>`
   - offset：偏移量从0开始。
- 实例
   - 每个独立用户是否访问过网站存放在Bitmaps中， 将访问的用户记做1， 没有访问的用户记做0， 用偏移量作为用户的id。
   - 设置键的第offset个位的值（从0算起） ， 假设现在有20个用户，userid=1， 6， 11， 15， 19的用户对网站进行了访问， 那么当前Bitmaps初始化结果如图
   ![image.png](image/1653668270494-1f258524-f513-44db-a639-f40e8da8c56f.png)
   - unique:users:20201106 代表 2020-11-06 这天的独立访问用户的 Bitmaps


> 注：
> 很多应用的用户id以一个指定数字（例如10000） 开头， 直接将用户id和Bitmaps的偏移量对应势必会造成一定的浪费， 通常的做法是每次做setbit操作时将用户id减去这个指定数字。
> 在第一次初始化Bitmaps时， 假如偏移量非常大， 那么整个初始化过程执行会比较慢， 可能会造成Redis的阻塞。


#### 1.2.2、getbit
获取Bitmaps中某个偏移量的值，获取键的第offset位的值（从0开始算）

- 格式
   - `getbit<key><offset>` 
- 实例
   - 获取id=8的用户是否在2020-11-06这天访问过， 返回0说明没有访问过：
   `getbit unique:users:20201106 8`
#### 1.2.3、bitcount
统计字符串被设置为1的bit数。一般情况下，给定的整个字符串都会被进行计数，通过指定额外的 start 或 end 参数，可以让计数只在特定的位上进行。
start 和 end 参数的设置，都可以使用负数值：比如 -1 表示最后一个位，而 -2 表示倒数第二个位，start、end 是指bit组的字节的下标数，二者皆包含。

- 格式
   - `bitcount<key>[start end] `统计字符串从**start字节**到**end字节**比特值为1的数量
- 举例： K1 【01000001 01000000  00000000 00100001】 对应下标 【0，1，2，3】
   -  统计下标1、2字节组中bit=1的个数，即01000000  00000000
   - `bitcount K1 1 2`　　--》1
   - 统计下标1、2字节组中bit=1的个数，即01000000  00000000 00100001
   - `bitcount K1 1 3`　　--》3
   -  统计下标0到下标倒数第2，字节组中bit=1的个数，即01000001  01000000   00000000
   - `bitcount K1 0 -2`　　--》3
>  注意：redis的setbit设置或清除的是bit位置，而bitcount计算的是byte位置。

#### 1.2.4、bitop
复合操作， 它可以做多个Bitmaps的and（交集） 、 or（并集） 、 not（非） 、 xor（异或） 操作并将结果保存在destkey中。

- 格式
   - `bitop  and(or/not/xor) <destkey> [key…]`
- 举例：K1【01100100 01000000】（1259）；K2【11001000 01000000】（0149）
- and
   - `bitop and d3 K1 K2`　　--》d3 【01000000 01000000】
- or
   - `bitop or d4 K1 K2`　　--》d4 【11101100 01000000】
- not
   - `bitop not d5 K1`　　--》d5 【10011011 10111111】
- xor
   - `bitop xor d6 K1 K2`　　--》d4 【10101100 00000000】
> 使用get key查看，控制台是以十六进制或者ASCII码显示的。

### 1.3、与set对比
假设网站有1亿用户， 每天独立访问的用户有5千万， 如果每天用集合类型和Bitmaps分别存储活跃用户可以得到表
![image.png](image/1653701592060-efef9214-b775-4387-bc48-614eb47f5d7c.png)
很明显， 这种情况下使用Bitmaps能节省很多的内存空间， 尤其是随着时间推移节省的内存还是非常可观的
![image.png](image/1653701684691-26affb5c-7243-4839-aba2-69c0564163c3.png)
但Bitmaps并不是万金油， 假如该网站每天的独立访问用户很少， 例如只有10万（大量的僵尸用户） ， 那么两者的对比如下表所示， 很显然， 这时候使用Bitmaps就不太合适了， 因为基本上大部分位都是0。
![image.png](image/1653701769618-6af4d0d9-2eba-496a-8c3f-981a76d79205.png)
## 2、HyperLogLog
### 2.1、简介
在工作当中，我们经常会遇到与统计相关的功能需求，比如统计网站PV（PageView页面访问量）,可以使用Redis的incr、incrby轻松实现。
但像UV（UniqueVisitor，独立访客）、独立IP数、搜索记录数等需要去重和计数的问题如何解决？
这种求集合中不重复元素个数的问题称为基数问题。
解决基数问题有很多种方案：

- 数据存储在MySQL表中，使用distinct count计算不重复个数
- 使用Redis提供的hash、set、bitmaps等数据结构来处理

以上的方案结果精确，但随着数据不断增加，导致占用空间越来越大，对于非常大的数据集是不切实际的。
能否能够降低一定的精度来平衡存储空间？**Redis推出了HyperLogLog**
Redis HyperLogLog 是用来做基数统计的算法，HyperLogLog 的优点是，在输入元素的数量或者体积非常非常大时，计算基数所需的空间总是固定的、并且是很小的。
在 Redis 里面，每个 HyperLogLog 键只需要花费 12 KB 内存，就可以计算接近 2^64 个不同元素的基数。这和计算基数时，元素越多耗费内存就越多的集合形成鲜明对比。
但是，因为 HyperLogLog 只会根据输入元素来计算基数，而不会储存输入元素本身，所以 HyperLogLog 不能像集合那样，返回输入的各个元素。
什么是基数?
比如数据集 {1, 3, 5, 7, 5, 7, 8}， 那么这个数据集的基数集为 {1, 3, 5 ,7, 8}, 基数(不重复元素)为5。 基数估计就是在误差可接受的范围内，快速计算基数。
### 2.2、命令
#### 2.2.1、pfadd
添加指定元素到 HyperLogLog 中

- 格式
   - `pfadd <key>< element> [element ...]`
- 实例
   - 将所有元素添加到指定HyperLogLog数据结构中。如果执行命令后HLL估计的近似基数发生变化，则返回1，否则返回0。
   ![image.png](image/1653703217799-3dd058bb-9403-49c4-b83a-0d88dcd4d813.png)
#### 2.2.2、pfcount
计算HLL的近似基数，可以计算多个HLL，比如用HLL存储每天的UV，计算一周的UV可以使用7天的UV合并计算即可

- 格式
   - `pfcount<key> [key ...]`
- 实例
   - 统计h1，h2
   ![image.png](image/1653703482521-b71dc5c1-2c8f-49c5-8aee-37cd8d77cc7a.png)

3、pfmerge
将一个或多个HLL合并后的结果存储在另一个HLL中，比如每月活跃用户可以使用每天的活跃用户来合并计算可得

- 格式
   - `pfmerge<destkey><sourcekey> [sourcekey ...]`
- 实例
   - 将h1，h2合并后放到h3里面
   ![image.png](image/1653703975196-b4950936-acc1-42e6-be79-dc7c909a35a3.png)
## 3、Geospatial
### 3.1、简介
Redis 3.2 中增加了对GEO类型的支持。GEO，Geographic，地理信息的缩写。该类型，就是元素的2维坐标，在地图上就是经纬度。redis基于该类型，提供了经纬度设置，查询，范围查询，距离查询，经纬度Hash等常见操作。
### 3.2、命令
#### 3.2.1、geoadd
添加地理位置（经度，纬度，名称）

- 格式
   - `geoadd<key>< longitude><latitude><member>[longitude latitude member...]`
- 实例
   - 添加上海，重庆，北京城市的坐标
   ![image.png](image/1653704551228-adaf8d98-c7e3-4d49-b607-68b5908b8ace.png)
> 两极无法直接添加，一般会下载城市数据，直接通过 Java 程序一次性导入。
> 有效的经度从 -180 度到 180 度。有效的纬度从 -85.05112878 度到 85.05112878 度。
> 当坐标位置超出指定范围时，该命令将会返回一个错误。
> 已经添加的数据，是无法再次往里面添加的。

#### 3.2.2、geopos
获得指定地区的坐标值

- 格式
   - `geopos  <key><member> [member...]`
- 实例
   - 获取上海和北京的坐标
   ![image.png](image/1653704790513-270ef636-aff4-41f6-b28a-6c3205d93016.png)
#### 3.2.3、geodist
获取两个位置之间的直线距离

- 格式
   - `geodist<key><member1><member2>  [m|km|ft|mi ]`
- 实例
   - 获取上海和北京之间的直线距离
   ![image.png](image/1653704933880-1c2d4a35-036d-4dbf-b229-64cf61fc3d59.png)
> 单位：
> m 表示单位为米[默认值]。
> km 表示单位为千米。
> mi 表示单位为英里。
> ft 表示单位为英尺。
> 如果用户没有显式地指定单位参数， 那么 GEODIST 默认使用米作为单位

#### 3.2.4、georadius
以给定的经纬度为中心，找出某一半径内的元素

- 格式
   - `georadius<key>< longitude><latitude>radius  m|km|ft|mi`
   - key 经度 纬度 距离 单位
- 实例
- 查找以经度110，维度30，半径1000km范围内的城市。（前提是已经添加）
![image.png](image/1653705352046-40cd1606-7dc0-4f20-9123-65ec51f30c0c.png)
# 七、Redis - Jedis
## 1、Java 操作流程
### 1.1、Maven工程
```xml
<dependency>
  <groupId>redis.clients</groupId>
  <artifactId>jedis</artifactId>
  <version>3.3.0</version>
</dependency>
```
### 1.2、测试程序
```java
Jedis jedis = new Jedis("192.168.137.3", 6379);
String pong = jedis.ping();
System.out.println("连接成功：" + pong);
jedis.close();
```
> 连接Redis注意事项：
> 配置文件
> - 注释掉 bind=127.0.0.1
> - 关闭 protected-mode no
>
> 防火墙开启 6379 端口
> - 开启端口 `firewall-cmd --permanent --add-port=6379/tcp`
> - 查看防火墙已开放端口 `firewall-cmd --zone=public --list-ports`

## 2、Jedis-API
参考 命令行操作，使用方法类似。
# 八、Spring Boot 整合
## 1、引入依赖
```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```
## 2、配置 Redis
```yaml
spring:
  redis:
    # 服务器地址
    host: 192.168.123.89
    # Redis 端口（默认为6379）
    port: 6379
    # Redis 密码，如果没有，可以不设置
    password: 1234
    # 数据库索引（默认为0）
    database: 0
    # 连接超时时间（毫秒）
    connect-timeout: 1800000

    lettuce:
      pool:
        # 连接池最大连接数（使用负值表示没有限制，默认8）
        max-active: 20
        # 最大阻塞等待时间(负数表示没限制)
        max-wait: -1
        # 连接池中的最大空闲连接
        max-idle: 5
        # 连接池中的最小空闲连接
        min-idle: 0
```
## 3、切换至Jedis（如果需要）

- 引入Jedis依赖
```xml
<dependency>
  <groupId>redis.clients</groupId>
  <artifactId>jedis</artifactId>
</dependency>
```

- 配置文件加
```yaml
spring:
  redis:
      client-type: jedis
```
# 九、事务 - 锁机制
## 1、Redis事务定义
Redis事务是一个单独的隔离操作：事务中的所有命令都会序列化、按顺序地执行。
事务在执行的过程中，不会被其他客户端发送来的命令请求所打断。
Redis事务的主要作用就是串联多个命令防止别的命令插队。
## 2、Multi、Exec、discard
从输入Multi命令开始，输入的命令都会依次进入命令队列中，但不会执行，直到输入Exec后，Redis会将之前的命令队列中的命令依次执行。
组队的过程中可以通过discard来放弃组队。  
 ![image.png](image/1653812924704-902caf6d-f3e0-4415-86aa-372278e10131.png)
> **执行情况说明**
> - 组队成功，提交成功
> - 组队阶段报错，提交失败
> - 组队成功，提交有成功有失败情况

## 3、事务错误处理
组队中某个命令出现了报告错误，执行时整个的所有队列都会被取消。
 ![image.png](image/1653813163425-fdd8276b-a6d4-4869-ae3d-70970cbc79c6.png)
如果执行阶段某个命令报出了错误，则只有报错的命令不会被执行，而其他的命令都会执行，不会回滚。
 ![image.png](image/1653813182358-495913f4-fb57-4b33-9900-6e3de792c053.png)
## 4、事务冲突的问题
场景：有很多人使用一个账户,同时去参加双十一抢购
### 4.1、例子
一个请求想给金额减8000
一个请求想给金额减5000
一个请求想给金额减1000
### 4.2、悲观锁
悲观锁(Pessimistic Lock), 顾名思义，就是很悲观，每次去拿数据的时候都认为别人会修改，所以每次在拿数据的时候都会上锁，这样别人想拿这个数据就会block直到它拿到锁。**传统的关系型数据库**里边就用到了很多这种锁机制，比如行锁，表锁等，读锁，写锁等，都是在做操作之前先上锁。
![image.png](image/1653813378533-608caed1-cb4c-474f-8235-a5abacf9117b.png)
### 4.3、乐观锁
乐观锁(Optimistic Lock), 顾名思义，就是很乐观，每次去拿数据的时候都认为别人不会修改，所以不会上锁，但是在更新的时候会判断一下在此期间别人有没有去更新这个数据，可以使用版本号等机制。乐观锁适用于多读的应用类型，这样可以提高吞吐量。Redis就是利用这种check-and-set机制实现事务的。
![image.png](image/1653813449077-95192ae9-c243-4dd3-8af4-98aa85d73c81.png)
### 4.4、WATCH key [key ...]
在执行multi之前，先执行watch key1 [key2]，可以监视一个(或多个) key。
如果在**事务执行之前这个(或这些) key 被其他命令所改动，那么事务将被打断。**
> WATCH 必须配合事务使用，不然没有作用。
> 如果监视的key被其他事务的命令改动，**整个队列的命令都会失败**。

### 4.5、unwatch
取消 WATCH 命令对所有 key 的监视。
如果在执行 WATCH 命令之后，EXEC 命令或DISCARD 命令先被执行了的话，那么就不需要再执行UNWATCH 了。
[http://doc.redisfans.com/transaction/exec.html](http://doc.redisfans.com/transaction/exec.html)
## 5、Redis事务三特性

- 单独的隔离操作
   - 事务中的所有命令都会序列化、按顺序地执行。
   - 事务在执行的过程中，不会被其他客户端发送来的命令请求所打断。
- 没有隔离级别的概念
   - 队列中的命令没有提交之前都不会实际被执行，因为事务提交前任何指令都不会被实际执行。
- 不保证原子性
   - 事务中如果有一条命令执行失败，其后的命令仍然会被执行，没有回滚。

# 十、事务 - 秒杀案例
## 1、计数器和人员记录
 ![image.png](image/1653834618345-6e16c580-47fa-4015-8783-8df47db2ceae.png)
## 2、秒杀并发模拟
> redis做压测也可以用自带的**redis-benchmark**工具

### 2.1、安装
使用工具ab模拟测试
CentOS6 默认安装
CentOS7需要手动安装
`yum install httpd-tools`
### 2.2、测试及结果
`vim postfile` 模拟表单提交参数,以&符号结尾;存放当前目录。
postfile内容：`prodid=0101&`
```shell
ab -n 2000 -c 200 -k -p ~/postfile -T application/x-www-form-urlencoded http://192.168.2.115:8081/Seckill/doseckill

-n 要执行请求数，默认会执行一个请求
-c 一次执行多个请求的数量，默认是一次一个请求。
-k 使用HTTP KeepAlive功能。
-p 包含数据到POST的文件。 还请记住设置-T。
-T Content-type用于POST / PUT数据的内容类型内容类型标题，例如：'application/x-www-form-urlencoded' 默认是'text/plain'
```
## 3、秒杀代码
### 3.1、乐观锁解决库存遗留
```java
//秒杀过程
public static boolean doSecKill(String uid,String prodid) throws IOException {
    // 1 uid和prodid非空判断
    if(uid == null || prodid == null) {
        return false;
    }

    // 2 连接redis
    // 通过连接池得到jedis对象
    JedisPool jedisPoolInstance = JedisPoolUtil.getJedisPoolInstance();
    Jedis jedis = jedisPoolInstance.getResource();

    // 3 拼接key
    // 3.1 库存key
    String kcKey = "sk:"+prodid+":qt";
    // 3.2 秒杀成功用户key
    String userKey = "sk:"+prodid+":user";

    // 监视库存
    jedis.watch(kcKey);

    // 4 获取库存(必须要监视以后获取)，如果库存null，秒杀还没有开始
    String kc = jedis.get(kcKey);
    if(kc == null) {
        System.out.println("秒杀还没有开始，请等待");
        jedis.close();
        return false;
    }

    // 5 判断用户是否重复秒杀操作
    if(jedis.sismember(userKey, uid)) {
        System.out.println("已经秒杀成功了，不能重复秒杀");
        jedis.close();
        return false;
    }

    //6 判断如果商品数量，库存数量小于1，秒杀结束
    if(Integer.parseInt(kc)<=0) {
        System.out.println("秒杀已经结束了");
        jedis.close();
        return false;
    }

    //7 秒杀过程
    //使用事务
    Transaction multi = jedis.multi();

    // 组队操作
    // 7.1 库存-1
    multi.decr(kcKey);
    // 7.2 把秒杀成功用户添加清单里面
    multi.sadd(userKey,uid);

    //执行
    List<Object> results = multi.exec();

    if(results == null || results.size()==0) {
        jedis.close();
        // 解决库存遗留问题，失败了重试
        return doSecKill(uid, prodid);
    }

    System.out.println("秒杀成功了..");
    jedis.close();
    return true;
}
```
###  3.2、LUA脚本解决库存遗留
#### 3.2.1、LUA介绍
Lua 是一个小巧的脚本语言，Lua脚本可以很容易的被C/C++ 代码调用，也可以反过来调用C/C++的函数，Lua并没有提供强大的库，一个完整的Lua解释器不过200k，所以Lua不适合作为开发独立应用程序的语言，而是作为嵌入式脚本语言。
很多应用程序、游戏使用LUA作为自己的嵌入式脚本语言，以此来实现可配置性、可扩展性。
这其中包括魔兽争霸地图、魔兽世界、博德之门、愤怒的小鸟等众多游戏插件或外挂。
[https://www.w3cschool.cn/lua/](https://www.w3cschool.cn/lua/)
#### 3.2.2、LUA脚本在Redis中的优势
将复杂的或者多步的redis操作，写为一个脚本，一次提交给redis执行，减少反复连接redis的次数。提升性能。
LUA脚本是类似redis事务，有一定的原子性，不会被其他命令插队，可以完成一些redis事务性的操作。
但是注意redis的lua脚本功能，只有在**Redis 2.6以上**的版本才可以使用。
利用lua脚本淘汰用户，解决超卖问题。
redis 2.6版本以后，通过lua脚本解决争抢问题，实际上是 redis **利用其单线程的特性，用任务队列的方式解决多任务并发问题**。
![image.png](image/1653838923806-4834bfec-fb5e-4a95-8ca2-7b3bdaa7274f.png)
```java
static String secKillScript = "" +
    "local userid=KEYS[1];\n" +
    "local prodid=KEYS[2];\n" +
    "local qtkey='sk:'..prodid..':qt';\n" +
    "local usersKey='sk:'..prodid..':usr';\n" +
    "local userExists=redis.call('sismember',usersKey,userid);\n" +
    "if tonumber(userExists)==1 then \n" +
    "   return 2;\n" +
    "end\n" +
    "local num= redis.call('get' ,qtkey);\n" +
    "if tonumber(num)<=0 then \n" +
    "   return 0;\n" +
    "else \n" +
    "   redis.call('decr',qtkey);\n" +
    "   redis.call('sadd',usersKey,userid);\n" +
    "end\n" +
    "return 1";

public static boolean doSecKill(String uid, String prodid) throws IOException {

    JedisPool jedispool = JedisPoolUtil.getJedisPoolInstance();
    Jedis jedis = jedispool.getResource();

    String sha1 = jedis.scriptLoad(secKillScript);
    Object result = jedis.evalsha(sha1, 2, uid, prodid);

    String reString = String.valueOf(result);
    if ("0".equals(reString)) {
        System.err.println("已抢空！！");
    } else if ("1".equals(reString)) {
        System.out.println("抢购成功！！！！");
    } else if ("2".equals(reString)) {
        System.err.println("该用户已抢过！！");
    } else {
        System.err.println("抢购异常！！");
    }
    jedis.close();

    return true;
}
```
# 十一、Redis持久化
## 1、总体介绍
Redis 提供了2个不同形式的持久化方式。

- RDB（Redis DataBase）
- AOF（Append Of File）
## 2、RDB（Redis DataBase）
在指定的时间间隔内将内存中的数据集快照写入磁盘， 也就是行话讲的Snapshot快照，它恢复时是将快照文件直接读到内存里
### 2.1、备份如何执行
Redis会单独创建（fork）一个子进程来进行持久化，会**先将数据写入到 一个临时文件中**，待持久化过程都结束了，**再用这个临时文件替换上次持久化好的文件**。 整个过程中，主进程是不进行任何IO操作的，这就确保了极高的性能 如果需要进行大规模数据的恢复，且对于数据恢复的完整性不是非常敏感，那RDB方式要比AOF方式更加的高效。RDB的**缺点是最后一次持久化后的数据可能丢失。**
### 2.2、Fork
ork的作用是复制一个与当前进程一样的进程。新进程的所有数据（变量、环境变量、程序计数器等） 数值都和原进程一致，但是是一个全新的进程，并作为原进程的子进程。
在Linux程序中，fork()会产生一个和父进程完全相同的子进程，但子进程在此后多会exec系统调用，出于效率考虑，Linux中引入了“写时复制技术”
**一般情况父进程和子进程会共用同一段物理内存**，只有进程空间的各段的内容要发生变化时，才会将父进程的内容复制一份给子进程。
### 2.3、RDB持久化流程
![image.png](image/1653882272717-6dd468ef-7450-42cd-b971-1412a21370dd.png)
### 2.4、dump.rdb文件
在redis.conf中配置文件名称，默认为dump.rdb
 ![image.png](image/1653882385929-caff4987-ab93-4bb4-90de-aa220190bc65.png)
### 2.5、配置位置
rdb文件的保存路径，也可以修改。默认为Redis启动时命令行所在的目录下
![image.png](image/1653882423954-c0f85e92-57af-4496-856e-143bee5bc6f5.png)
### 2.6、触发配置
#### 2.6.1、快照配置
```shell
# save <seconds> <changes>
#
# 如果给定的秒数和给定数量的对 DB 的写操作都发生，将保存 DB。
#
# 在下面的示例中，行为将是保存：
# 900 秒（15 分钟）后，如果至少 1 个键发生了变化
# 300 秒（5 分钟）后，如果至少有 10 个键被更改
# 如果至少有 10000 个键被更改，则在 60 秒后
#
# 注意：您可以通过注释掉所有“保存”行来完全禁用保存。
#
# 也可以把之前配置的save全部去掉
# 通过添加带有单个空字符串参数的保存指令来获得积分
# 就像下面的例子：
# save ""
save 900 1
save 300 10
save 60 10000
```
#### 2.6.2、save VS bgsave

- save ：save时只管保存，其它不管，会阻塞。手动保存。不建议。
- bgsave：Redis会在后台异步进行快照操作， 快照同时还可以响应客户端请求。
> 可以通过lastsave 命令获取最后一次成功执行快照的时间

#### 2.6.3、flushall命令
执行flushall命令，也会产生dump.rdb文件，但里面是空的。
#### 2.6.4、stop-writes-on-bgsave-error
当Redis无法写入磁盘的话，直接**关掉Redis的写操作**。推荐yes.
![image.png](image/1653883585950-8acdc737-6cba-4028-a69f-5c2be57c500a.png)
#### 2.6.5、rdbcompression
对于存储到磁盘中的快照，可以设置是否进行压缩存储。如果是的话，redis会采用LZF算法进行压缩。
如果你不想消耗CPU来进行压缩的话，可以设置为关闭此功能。推荐 yes 。
![image.png](image/1653883710418-a003441b-b938-4482-92d0-bf986fd33e4b.png)
#### 2.6.6、rdbchecksum
在存储快照后，还可以让redis使用CRC64算法来进行数据完整性校验，
但是这样做会增加大约10%的性能消耗，如果希望获取到最大的性能提升，可以关闭此功能
推荐yes 。
![image.png](image/1653883898991-8837334f-318e-4ed0-8a63-db867a245857.png)
### 2.7、备份与恢复
#### 2.7.1、备份

- 先通过config get dir  查询rdb文件的目录 
- 将 *.rdb 文件拷贝到别的地方
#### 2.7.2、恢复

- 关闭Redis
- 先把备份的文件拷贝到工作目录下。如 `cp dump2.rdb dump.rdb`
- 启动Redis, 备份数据会直接加载
### 2.8、优缺点
#### 2.8.1、优势

- 适合大规模的数据恢复
- 对数据完整性和一致性要求不高更适合使用
- 节省磁盘空间
- 恢复速度快
#### 2.8.2、劣势

- Fork的时候，内存中的数据被克隆了一份，大致2倍的膨胀性需要考虑
- 虽然Redis在fork时使用了写时拷贝技术,但是如果数据庞大时还是比较消耗性能。
- 在备份周期在一定间隔时间做一次备份，所以如果Redis意外down掉的话，就会丢失最后一次快照后的所有修改。
### 2.9、停止操作
动态停止RDB：`redis-cli config set save ""`
save后给空值，表示禁用保存策略
### 2.10、小结
![image.png](image/1653884320921-01d48787-674b-47d9-9f1a-e936f24b3bc7.png)
## 3、AOF（Append Only File）
以日志的形式来记录每个写操作（增量保存），将Redis执行过的所有写指令记录下来(读操作不记录)， 只许追加文件但不可以改写文件，redis启动之初会读取该文件重新构建数据，换言之，redis 重启的话就根据日志文件的内容将写指令从前到后执行一次以完成数据的恢复工作
### 3.1、AOF持久化流程
（1）客户端的请求写命令会被append追加到AOF缓冲区内；
（2）AOF缓冲区根据AOF持久化策略[always,everysec,no]将操作sync同步到磁盘的AOF文件中；
（3）AOF文件大小超过重写策略或手动重写时，会对AOF文件rewrite重写，压缩AOF文件容量；
（4）Redis服务重启时，会重新load加载AOF文件中的写操作达到数据恢复的目的；
![image.png](image/1653884711424-4b808890-0836-4136-9df0-60858b4ee1e7.png)
### 3.2、AOF开启
AOF默认是不开启的。
如果开启，`appendonly yes`
![image.png](image/1653884834842-06f82f6f-ff8a-40c5-9f2a-abcc0bb9bb5f.png)
也可以在redis.conf中配置文件名称，默认为 appendonly.aof
AOF文件的保存路径，同RDB的路径一致。
> AOF和RDB同时开启，系统默认取AOF的数据（数据不会存在丢失）

### 3.3、备份与恢复
AOF的备份机制和性能虽然和RDB不同, 但是备份和恢复的操作同RDB一样，都是拷贝备份文件，需要恢复时再拷贝到Redis工作目录下，启动系统即加载。
正常恢复

- 修改默认的appendonly no，改为yes
- 将有数据的aof文件复制一份保存到对应目录(查看目录：config get dir)
- 恢复：重启redis然后重新加载

### 3.4、异常恢复
修改默认的appendonly no，改为yes
如遇到AOF文件损坏，通过/usr/local/bin/redis-check-aof--fix appendonly.aof进行恢复
备份被写坏的AOF文件
恢复：重启redis，然后重新加载
### 3.5、AOF同步频率设置

- `appendfsync always`
   - 始终同步，每次Redis的写入都会立刻记入日志；性能较差但数据完整性比较好
- `appendfsync everysec`
   - 每秒同步，每秒记入日志一次，如果宕机，本秒的数据可能丢失。
- `appendfsync no`
   - redis不主动进行同步，把同步时机交给操作系统。
### 3.6、重写压缩
#### 3.6.1、介绍
AOF采用文件追加方式，文件会越来越大为避免出现此种情况，新增了重写机制, 当AOF文件的大小超过所设定的阈值时，Redis就会启动AOF文件的内容压缩， 只保留可以恢复数据的最小指令集。
也可以手动执行命令 `bgrewriteaof`。
#### 3.6.2、重写原理
AOF文件持续增长而过大时，会fork出一条新进程来将文件重写(也是先写临时文件最后再rename)，redis4.0版本后的重写，是指上就是把rdb 的快照，以二级制的形式附在新的aof头部，作为已有的历史数据，替换掉原来的流水账操作。
#### 3.6.3、no-appendfsync-on-rewrite
如果 `no-appendfsync-on-rewrite yes` ，不写入aof文件只写入缓存，用户请求不会阻塞，但是在这段时间如果宕机会丢失这段时间的缓存数据。（降低数据安全性，提高性能）
如果 `no-appendfsync-on-rewrite no`， 还是会把数据往磁盘里刷，但是遇到重写操作，可能会发生阻塞。（数据安全，但是性能降低）
#### 3.6.4、触发机制
Redis会记录上次重写时的AOF大小，默认配置是当AOF文件大小是上次rewrite后大小的一倍且文件大于64M时触发
重写虽然可以节约大量磁盘空间，减少恢复时间。但是每次重写还是有一定的负担的，因此设定Redis要满足一定条件才会进行重写。 
![image.png](image/1653885767412-ba3ec0b8-9939-40af-a120-210e60736b00.png)

- auto-aof-rewrite-percentage：设置重写的基准值，文件达到100%时开始重写（文件是原来重写后文件的2倍时触发）
- auto-aof-rewrite-min-size：设置重写的基准值，最小文件64MB。达到这个值开始重写。
#### 3.6.5、重写流程

1. bgrewriteaof触发重写，判断是否当前有bgsave或bgrewriteaof在运行，如果有，则等待该命令结束后再继续执行。
1. 主进程 fork 出子进程执行重写操作，保证主进程不会阻塞。
1. 子进程遍历redis内存中数据到临时文件，客户端的写请求同时写入 aof_buf 缓冲区和 aof_rewrite_buf 重写缓冲区保证原AOF文件完整以及新AOF文件生成期间的新的数据修改动作不会丢失。
1. 新的AOF
   1. 子进程写完新的AOF文件后，向主进程发信号，父进程更新统计信息。
   1. 主进程把aof_rewrite_buf中的数据写入到新的AOF文件。
5. 使用新的AOF文件覆盖旧的AOF文件，完成AOF重写。

 ![image.png](image/1653886328611-ac8ed7b8-a0b5-488f-8148-ce0fc5902486.png)

### 3.7、优缺点
#### 3.7.1、优点

- 备份机制更稳健，丢失数据概率更低。
- 可读的日志文本，通过操作AOF稳健，可以处理误操作。
#### 3.7.2、缺点

- 比起RDB占用更多的磁盘空间。
- 恢复备份速度要慢。
- 每次读写都同步的话，有一定的性能压力。
- 存在个别Bug，造成恢复不能。
### 3.8、总结
![image.png](image/1653886465613-5f88c2da-1ffd-449b-a706-2beeaa5e2abf.png)
## 4、RDB or AOF
官方推荐两个都启用。
如果对数据不敏感，可以选单独用RDB。
不建议单独用 AOF，因为可能会出现Bug。
如果只是做纯内存缓存，可以都不用。
### 4.1、同时开启两种持久化方式
在这种情况下,当redis重启的时候会优先载入AOF文件来恢复原始的数据, 因为在通常情况下AOF文件保存的数据集要比RDB文件保存的数据集要完整。
因为RDB更适合用于备份数据库(AOF在不断变化不好备份)， 快速重启，而且不会有AOF可能潜在的bug，留着作为一个万一的手段。
### 4.2、性能建议

- 因为RDB文件只用作后备用途，建议**只在从服务器(Slave)上持久化RDB文件，而且15分钟备份一次就够了，即只保留save 900 1这条规则。**
- 使用AOF，好处是在最恶劣情况下也只会丢失不超过两秒数据，启动脚本较简单只load自己的AOF文件就可以了。
   - 代价
      - 一是带来了持续的IO
      - 二是AOF rewrite的最后将rewrite过程中产生的新数据写到新文件造成的阻塞几乎是不可避免的。
   - 只要硬盘许可，应该尽量减少AOF rewrite的频率，AOF重写的基础大小默认值64M太小了，可以设到5G以上。
   - 默认超过原大小100%大小时重写可以改到适当的数值。
# 十二、主从复制
## 1、介绍
主机数据更新后根据配置和策略， 自动同步到备机的master/slaver机制。

- **Master**：写为主
- **Slave**：读为主

功能

- 读写分离，性能扩展
- 容灾快速恢复

![image.png](image/1653916593757-3499754c-9d5d-44d6-b10d-b6dada3fe956.png)

## 2、搭建模拟环境

1. 拷贝多个redis.conf文件【include导入公共部分】
1. 开启 `daemonize yes`【守护进程】
1. Pid 文件名字 pidfile
1. Log文件名字
1. 指定端口 port
1. 指定 dump.rdb 名字
1. Appendonly 关掉或者换名字
### 2.1、新建redis6379.conf
填写以下内容
```shell
include /myredis/redis.conf
pidfile /var/run/redis_6379.pid
port 6379
dbfilename dump6379.rdb
```

### 2.2、新建redis6380.conf
填写以下内容
```shell
include /myredis/redis.conf
pidfile /var/run/redis_6380.pid
port 6380
dbfilename dump6380.rdb
```

### 2.3、新建redis6381.conf
填写以下内容
```shell
include /myredis/redis.conf
pidfile /var/run/redis_6381.pid
port 6381
dbfilename dump6381.rdb
```
> slave-priority 10
> 设置从机的优先级，值越小，优先级越高，用于选举主机时使用。默认100

### 2.4、启动三台redis服务器
 ![image.png](image/1653917251666-2984ead7-0c10-4017-b99a-42857143ebed.png)
> `ps -ef | grep redis` 查看服务器是否启动

### 2.5、查看主从复制信息
`info replication`
```shell
#角色，master主；slave从
role:master
#下面的从服务器数量
connected_slaves:1
#从服务器信息
slave0:ip=127.0.0.1,port=6381,state=online,offset=25071,lag=0
master_replid:cc73b4ee2e468e418c61a529e82257d81898a7b7
master_replid2:ba7dce4de51667a1fc6c22ab69b3d95071da6599
#偏移信息
master_repl_offset:25071
second_repl_offset:16369
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:11005
repl_backlog_histlen:14067

```
## 3、主从配置
### 3.1、说明
配从(库)
不配主(库) 
`slaveof  <ip> <port>`
成为某个实例的从服务器
### 3.2、模拟实验

1. 在6380和6381上执行: slaveof 192.168.123.89 6379
1. 在主机上写，在从机上可以读取数据
   - **在从机上写数据报错**
3. **主机挂掉，重启就行，一切如初**
3. 从机重启需重设：slaveof 192.168.123.89 6379
   - 可以将`slaveof 192.168.123.89 6379`增加到配置文件中。永久生效。
## 4、常用3招
### 4.1、一主二仆

- 成为从服务器后，会把主服务器的数据全部复制过来。
- 从服务器不能写。
- 默认主机关闭后，从机会继续待命，主机重启后，自动恢复。
- 从机重启后需重设。也可以在配置文件中配置自动认主。
### 4.2、薪火相传
上一个Slave可以是下一个slave的Master，Slave同样可以接收其他 slaves的连接和同步请求，那么该slave作为了链条中下一个的master, 可以有效减轻master的写压力,去中心化降低风险。

- 用 `slaveof  <ip> <port>`
- 中途变更转向，会清除之前的数据，重新建立拷贝最新的
- 风险是一旦某个slave宕机，后面的slave都没法备份
- 主机挂了，从机还是从机，无法写数据了
### 4.3、反客为主
当一个master宕机后，后面的slave可以立刻升为master，其后面的slave不用做任何修改。
用 `slaveof no one`  将从机变为主机。

## 5、复制原理

- Slave启动成功连接到master后会发送一个sync命令
- Master接到命令启动后台的存盘进程，同时收集所有接收到的用于修改数据集命令， 在后台进程执行完毕之后，master将传送整个数据文件到slave,以完成一次完全同步
- 全量复制：而slave服务在接收到数据库文件数据后，将其存盘并加载到内存中。
- 增量复制：Master继续将新的所有收集到的修改命令依次传给slave,完成同步
- 但是只要是重新连接master,一次完全同步（全量复制)将被自动执行
## 6、哨兵模式(sentinel)
### 6.1、介绍
反客为主的自动版，能够后台监控主机是否故障，如果故障了根据投票数自动将从库转换为主库
![image.png](image/1653922345611-d12275e5-bcf1-4c8d-9019-296e4490dedd.png)
### 6.2、模拟操作

- 调整为一主二仆模式，6379带着6380、6381
- 自定义的/myredis目录下新建 sentinel.conf 文件，名字绝不能错
   - 配置哨兵,填写内容 `sentinel monitor mymaster 192.168.123.89 6379 1`
   - 其中mymaster为监控对象起的服务器名称， 1 为至少有多少个哨兵同意迁移的数量。 
- 启动哨兵
   - 哨兵文件 `/usr/local/bin/redis-sentinel`
   - 执行` redis-sentinel  /myredis/sentinel.conf `
> 当主机挂掉，从机选举中产生新的主机
> (大概10秒左右可以看到哨兵窗口日志，切换了新的主机)
> 根据优先级别：replica-priority 选择哪个为新主机，默认是100，越小，优先级越高。【老版是slave-priority】
> 原主机重启后会变为从机。

## 7、复制延时
由于所有的写操作都是先在Master上操作，然后同步更新到Slave上，所以从Master同步到Slave机器有一定的延迟，当系统很繁忙的时候，延迟问题会更加严重，Slave机器数量的增加也会使这个问题更加严重。
## 8、故障恢复
![image.png](image/1653922381522-b842640f-042f-4e57-8e96-6c904aede6d3.png)
优先级在redis.conf中默认：slave-priority 100，值越小优先级越高
偏移量是指获得原主机数据最全的
每个redis实例启动后都会随机生成一个40位的runid
## 9、主从复制 - Jedis
```java
private static JedisSentinelPool jedisSentinelPool=null;

public static Jedis getJedisFromSentinel(){
    if(jedisSentinelPool==null){
        Set<String> sentinelSet=new HashSet<>();
        // 哨兵的端口
        sentinelSet.add("192.168.123.89:26379");

        JedisPoolConfig jedisPoolConfig =new JedisPoolConfig();
        jedisPoolConfig.setMaxTotal(10); //最大可用连接数
        jedisPoolConfig.setMaxIdle(5); //最大闲置连接数
        jedisPoolConfig.setMinIdle(5); //最小闲置连接数
        jedisPoolConfig.setBlockWhenExhausted(true); //连接耗尽是否等待
        jedisPoolConfig.setMaxWaitMillis(2000); //等待时间
        jedisPoolConfig.setTestOnBorrow(true); //取连接的时候进行一下测试 ping pong

        jedisSentinelPool=new JedisSentinelPool("mymaster",sentinelSet,jedisPoolConfig);
        return jedisSentinelPool.getResource();
    }else{
        return jedisSentinelPool.getResource();
    }
}
```
# 十三、集群
## 1、介绍

- Redis 集群实现了对Redis的水平扩容，即启动N个redis节点，**将整个数据库分布存储在这N个节点中，每个节点存储总数据的1/N。**
- Redis 集群通过分区（partition）来提供一定程度的可用性（availability）： 
   - 即使集群中有一部分节点失效或者无法进行通讯， 集群也可以继续处理命令请求。
## 2、搭建模拟环境
制作6个实例，6379,6380,6381,6389,6390,6391
### 2.1、配置基本信息

- 开启daemonize yes
- Pid文件名字
- 指定端口
- Log文件名字
- Dump.rdb名字
- Appendonly 关掉或者换名字
### 2.2、cluster配置修改

- `cluster-enabled yes`    打开集群模式
- `cluster-config-file nodes-6379.conf`  设定节点配置文件名
- `cluster-node-timeout 15000`   设定节点失联时间，超过该时间（毫秒），集群自动进行主从切换。
### 2.3、创建redis6379.conf
```java
include /home/bigdata/redis.conf
port 6379
pidfile "/var/run/redis_6379.pid"
dbfilename "dump6379.rdb"
dir "/home/bigdata/redis_cluster"
logfile "/home/bigdata/redis_cluster/redis_err_6379.log"
cluster-enabled yes
cluster-config-file nodes-6379.conf
cluster-node-timeout 15000
```
### 2.4、创建剩余配置文件

- 创建文件
   - 例如：`cp redis6379.conf redis6380.conf`
- 然后分别查找替换端口
   - 例如：`:%s/6379/6380`
### 2.5、启动6个redis服务
![image.png](image/1653965521212-b5d985a9-1979-4cf4-a9a0-8d9d1c7dabe9.png)
## 3、合成集群
> 组合之前，请确保所有redis实例启动后，nodes-xxxx.conf文件都生成正常。

- 合体：
```bash
cd  /opt/redis-6.2.1/src
# 此处不要用127.0.0.1， 请用真实IP地址
# --replicas 1 采用最简单的方式配置集群，一台主机，一台从机，正好三组。
redis-cli --cluster create --cluster-replicas 1 192.168.11.101:6379 192.168.11.101:6380 192.168.11.101:6381 192.168.11.101:6389 192.168.11.101:6390 192.168.11.101:6391
```
## 4、登录方式

- -c 采用集群策略连接。（设置数据会自动切换到相应的写主机）
- 普通方式登录，存储数据时，可能会出现MOVED重定向操作错误。
   - 在redis-cli每次录入、查询键值，redis都会计算出该key应该送往的插槽，如果不是该客户端对应服务器的插槽，redis会报错，并告知应前往的redis实例地址和端口。
## 5、查看集群信息
在linux下查看：
`redis-cli --cluster check 192.168.123.205:6382`
登录redis后查看：
`cluster info`
通过 `cluster nodes` 命令查看集群信息
```bash
701ca7a9694be97c41af41934cf54bee5805aa03 192.168.123.89:6381@16381 myself,master - 0 1653962078000 3 connected 10923-16383
6377eed0c532f7b379fbbc1174850c1e1e87eae8 192.168.123.89:6391@16391 slave cb7b58263aeebb4ed607cb9da0d412c6a4335aa3 0 1653962080000 1 connected
fd2c87ed0235b6d5526575bc0f0f57db00ef7731 192.168.123.89:6389@16389 slave bfcd2c1529731f85802a73aa4cdd8bee23af0f03 0 1653962079000 2 connected
bfcd2c1529731f85802a73aa4cdd8bee23af0f03 192.168.123.89:6380@16380 master - 0 1653962080000 2 connected 5461-10922
cb7b58263aeebb4ed607cb9da0d412c6a4335aa3 192.168.123.89:6379@16379 master - 0 1653962080184 1 connected 0-5460
27f622db58c780b4490469332a374085017d7161 192.168.123.89:6390@16390 slave 701ca7a9694be97c41af41934cf54bee5805aa03 0 1653962081208 3 connected
```
**每个字段的含义如下：**

1. id：节点 ID，一个40个字符的随机字符串，当一个节点被创建时不会再发生变化（除非CLUSTER RESET HARD被使用）。
1. ip:port：客户端应该联系节点以运行查询的节点地址。
1. flags：逗号列表分隔的标志：myself，master，slave，fail?，fail，handshake，noaddr，noflags。标志在下一节详细解释。
1. master：如果节点是从属节点，并且主节点已知，则节点ID为主节点，否则为“ - ”字符。
1. ping-sent：以毫秒为单位的当前激活的ping发送的unix时间，如果没有挂起的ping，则为零。
1. pong-recv：毫秒 unix 时间收到最后一个乒乓球。
1. config-epoch：当前节点（或当前主节点，如果该节点是从节点）的配置时期（或版本）。每次发生故障切换时，都会创建一个新的，唯一的，单调递增的配置时期。如果多个节点声称服务于相同的哈希槽，则具有较高配置时期的节点将获胜。
1. link-state：用于节点到节点集群总线的链路状态。我们使用此链接与节点进行通信。可以是connected或disconnected。
1. slot：散列槽号或范围。从参数9开始，但总共可能有16384个条目（限制从未达到）。这是此节点提供的散列槽列表。如果条目仅仅是一个数字，则被解析为这样。如果它是一个范围，它是在形式start-end，并且意味着节点负责所有散列时隙从start到end包括起始和结束值。

**标志的含义（字段编号3）：**

- myself：您正在联系的节点。
- master：节点是主人。
- slave：节点是从属的。
- fail?：节点处于PFAIL状态。对于正在联系的节点无法访问，但仍然可以在逻辑上访问（不处于FAIL状态）。
- fail：节点处于FAIL状态。对于将PFAIL状态提升为FAIL的多个节点而言，这是无法访问的。
- handshake：不受信任的节点，我们握手。
- noaddr：此节点没有已知的地址。
- noflags：根本没有标志。
## 6、cluster 节点分配规则
一个集群至少要有三个主节点。
选项 `--cluster-replicas 1` 表示我们希望为集群中的每个主节点创建一个从节点。
分配原则尽量保证每个主数据库运行在不同的IP地址，每个从库和主库不在一个IP地址上。
## 7、slots
一个 Redis 集群包含 16384 个插槽（hash slot）， 数据库中的每个键都属于这 16384 个插槽的其中一个， 
集群使用公式 `CRC16(key) % 16384` 来计算键 key 属于哪个槽， 其中 CRC16(key) 语句用于计算键 key 的 CRC16 校验和 。
集群中的每个节点负责处理一部分插槽。 举个例子， 如果一个集群可以有主节点， 其中：

- 节点 A 负责处理 0 号至 5460 号插槽。
- 节点 B 负责处理 5461 号至 10922 号插槽。
- 节点 C 负责处理 10923 号至 16383 号插槽。
## 8、集群写操作

- redis-cli客户端提供了 –c 参数实现自动重定向。
   - 如 `redis-cli  -c –p 6379` 登入后，再录入、查询键值对可以自动重定向。
- 不在一个slot下的键值，不能使用mget,mset等多键操作。
   - 可以通过{}来定义组的概念，从而使key中{}内相同内容的键值对放到一个slot中去。
   - 例如可以：`mset k2{user} v2 k3{user} v3 k4{user} v4`


## 9、查询 slot 槽中的键

- `cluster keyslot <key>`查看key对应的slot
- `cluster getkeysinslot <slot><count>` 返回 count 个 slot 槽中的键。
## 10、故障恢复
### 10.1、主节点下线
如果主节点下线，超时后，从节点自动升为主节点（超时时间在配置文件中配置）
主节点恢复后，变成从机。
###  10.2、主从节点都下线

- 配置文件 `cluster-require-full-coverage yes` ，整个集群都挂掉。
- 配置文件 `cluster-require-full-coverage no` ，该插槽数据全都不能使用，也无法存储。
> redis.conf 中的参数  cluster-require-full-coverage

## 11、集群Jedis开发
```java
public static void main(String[] args) {
    Set<HostAndPort>set =new HashSet<>();
    // 可以多设置几个或者把集群的地址都设置，防止部分宕机
    set.add(new HostAndPort("192.168.123.89",6379));
    set.add(new HostAndPort("192.168.123.89",6380));
    JedisCluster jedisCluster=new JedisCluster(set);
    jedisCluster.set("k1", "v1_renchao");
    System.out.println(jedisCluster.get("k1"));
}
```
# 十四、Redis应用问题解决
## 1、缓存穿透
### 1.1、问题描述
key对应的数据在数据库并不存在，每次针对此key的请求从缓存获取不到，请求都会压到数据库，从而可能压垮数据库。
比如用一个不存在的用户id获取用户信息，不论缓存还是数据库都没有，若黑客利用此漏洞进行攻击可能压垮数据库。
![image.png](image/1653969227038-457a18ed-da5a-4089-be44-65dbc53b5c54.png)
### 1.2、解决方案
一个一定不存在缓存及查询不到的数据，由于缓存是不命中时被动写的，并且出于容错考虑，如果从存储层查不到数据则不写入缓存，这将导致这个不存在的数据每次请求都要到存储层去查询，失去了缓存的意义。
#### 1.2.1、对空值缓存
如果一个查询返回的数据为空（不管是数据是否不存在），我们仍然把这个空结果（null）进行缓存，设置空结果的过期时间会很短，最长不超过五分钟
#### 1.2.2、设置白名单
使用 bitmaps 类型定义一个可以访问的名单，名单id作为bitmaps的偏移量，每次访问和bitmap里面的id进行比较，如果访问id不在bitmaps里面，进行拦截，不允许访问。
#### 1.2.3、布隆过滤器
(布隆过滤器（Bloom Filter）是1970年由布隆提出的。它实际上是一个很长的二进制向量(位图)和一系列随机映射函数（哈希函数）。
布隆过滤器可以用于检索一个元素是否在一个集合中。它的优点是空间效率和查询时间都远远超过一般的算法，缺点是有一定的误识别率和删除困难。)
将所有可能存在的数据哈希到一个足够大的bitmaps中，一个一定不存在的数据会被 这个bitmaps拦截掉，从而避免了对底层存储系统的查询压力。
#### 1.2.4、进行实时监控
当发现Redis的命中率开始急速降低，需要排查访问对象和访问的数据，和运维人员配合，可以设置**黑名单限制服务。**
## 2、缓存击穿
### 2.1、问题描述
key对应的数据存在，但在redis中过期，此时若有大量并发请求过来，这些请求发现缓存过期一般都会从后端DB加载数据并回设到缓存，这个时候大并发的请求可能会瞬间把后端DB压垮。
![image.png](image/1653969665038-0712b3b5-d543-45d0-8f51-8691c7ce1565.png)


2.2、解决方案
key可能会在某些时间点被超高并发地访问，是一种非常“热点”的数据。这个时候，需要考虑一个问题：缓存被“击穿”的问题。
#### 2.2.1、预先设置热门数据
在redis高峰访问之前，把一些热门数据提前存入到redis里面，**加大这些热门数据key的时长**。
#### 2.2.2、实时调整
现场监控哪些数据热门，**实时调整key的过期时长**。
#### 2.2.3、使用锁
在缓存失效的时候（判断拿出来的值为空），不是立即去load db。
先使用缓存工具的某些带成功操作返回值的操作（比如Redis的SETNX）去set一个mutex key
当操作返回成功时，再进行load db的操作，并回设缓存,最后删除mutex key；
当操作返回失败，证明有线程在load db，当前线程睡眠一段时间再重试整个get缓存的方法。
![image.png](image/1653970553584-bf255149-1451-46d1-83ac-87a47eeb212e.png)
## 3、缓存雪崩
### 3.1、问题描述
key对应的数据存在，但在redis中过期，此时若有大量并发请求过来，这些请求发现缓存过期一般都会从后端DB加载数据并回设到缓存，这个时候大并发的请求可能会瞬间把后端DB压垮。
**缓存雪崩与缓存击穿的区别在于这里针对很多key缓存，前者则是某一个key。**
正常访问
 ![image.png](image/1653970609546-8e3b65a8-2c29-4601-a21e-ade8bab6eb89.png)
缓存失效瞬间
![image.png](image/1653970632823-ff309e22-2ea1-4c86-bd8c-444fdffa2154.png)
### 3.2、解决方案
缓存失效时的雪崩效应对底层系统的冲击非常可怕！
#### 3.2.1、构建多级缓存架构
nginx缓存 + redis缓存 +其他缓存（ehcache等）
#### 3.2.2、使用锁或队列
用加锁或者队列的方式来保证不会有大量的线程对数据库一次性进行读写，从而避免失效时大量的并发请求落到底层存储系统上。
不适用高并发情况。
#### 3.2.3、设置过期标志更新缓存
记录缓存数据是否过期（设置提前量），如果过期会触发通知另外的线程在后台去更新实际key的缓存。
#### 3.2.4、分散缓存失效时间
比如我们可以在原有的失效时间基础上增加一个随机值，比如1-5分钟随机，这样每一个缓存的过期时间的重复率就会降低，就很难引发集体失效的事件。
## 4、分布式锁
### 4.1、问题描述
随着业务发展的需要，原单体单机部署的系统被演化成分布式集群系统后，由于分布式系统多线程、多进程并且分布在不同机器上，这将使原单机部署情况下的并发控制锁策略失效，单纯的Java API并不能提供分布式锁的能力。为了解决这个问题就需要一种跨JVM的互斥机制来控制共享资源的访问，这就是分布式锁要解决的问题！
分布式锁主流的实现方案：

- 基于数据库实现分布式锁
- 基于缓存（Redis等）
- 基于Zookeeper

每一种分布式锁解决方案都有各自的优缺点：

- 性能：redis最高
- 可靠性：zookeeper最高
### 4.2、redis实现分布式锁
命令：`set sku:1:info "OK" NX PX 10000`
EX second ：设置键的过期时间为 second 秒。 SET key value EX second 效果等同于 SETEX key second value 。
PX millisecond ：设置键的过期时间为 millisecond 毫秒。 SET key value PX millisecond 效果等同于 PSETEX key millisecond value 。
NX ：只在键不存在时，才对键进行设置操作。 SET key value NX 效果等同于 SETNX key value 。
XX ：只在键已经存在时，才对键进行设置操作。
 ![image.png](image/1653978040937-7230c1c4-afd7-44dc-8160-ecc6ab1852ee.png)
1. 多个客户端同时获取锁（setnx）
2. 获取成功，执行业务逻辑{从db获取数据，放入缓存}，执行完成释放锁（del）
3. 其他客户端等待重试
### 4.3、基本代码
```java
@GetMapping("testLock")
public void testLock(){
    //1获取锁，setne
    Boolean lock = redisTemplate.opsForValue().setIfAbsent("lock", "111");
    //        System.out.println(lock);
    //2获取锁成功、查询num的值
    if(Boolean.TRUE.equals(lock)){
        Object value = redisTemplate.opsForValue().get("num");
        //2.1判断num为空return
        if(StringUtils.isEmpty(value)){
            // 返回前，释放锁，del
            redisTemplate.delete("lock");
            return;
        }
        //2.2有值就转成成int
        int num = Integer.parseInt(value+"");
        //2.3把redis的num加1
        redisTemplate.opsForValue().set("num", String.valueOf(++num));
        //2.4释放锁，del
        redisTemplate.delete("lock");
    }else{
        //3获取锁失败、每隔0.1秒再获取
        try {
            Thread.sleep(50);
            testLock();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```
通过网关压力测试：
`ab -n 2000 -c 100 http://192.168.123.189:8080/testLock`
### 4.4、锁的过期时间
如果处理业务时出现异常，会导致锁无法释放。
解决：设置过期时间，自动释放锁。
设置过期时间有两种方式：

- 通过expire设置过期时间（缺乏原子性：如果在setnx和expire之间出现异常，锁也无法释放）
- 在set时指定过期时间（推荐）
```java
Boolean lock = redisTemplate.opsForValue().setIfAbsent("lock", "111",3, TimeUnit.SECONDS);
```
### 4.5、UUID防误删
上面自动释放锁后，又会出现下面误删锁的情况。
解决方法：
取锁时，设置一个指定的唯一值（例如：uuid）；释放前获取这个值，判断是否自己的锁
![image.png](image/1654000088779-08230442-f6af-453f-ac3b-003a4f97ca59.png)
```java
String uuid = UUID.randomUUID().toString();
Boolean lock = redisTemplate.opsForValue().setIfAbsent("lock", uuid,3, TimeUnit.SECONDS);

。。。

//2.4释放锁，del
if (uuid.equals(redisTemplate.opsForValue().get(uuid))) {
    redisTemplate.delete("lock");
}
```
### 4.6、LUA保证删除的原子性
![image.png](image/1654002679714-64165100-01c1-4f58-9370-4b3b0a366d08.png)
命令 `SET resource-name anystring NX EX max-lock-time` 是一种在 Redis 中实现锁的简单方法。
客户端执行以上的命令：

- 如果服务器返回 OK ，那么这个客户端获得锁。
- 如果服务器返回 NIL ，那么客户端获取锁失败，可以在稍后再重试。
- 设置的过期时间到达之后，锁将自动释放。

可以通过以下修改，让这个锁实现更健壮：

- 不使用固定的字符串作为键的值，而是设置一个不可猜测（non-guessable）的长随机字符串，作为口令串（token）。
- 不使用 DEL 命令来释放锁，而是发送一个 Lua 脚本，这个脚本只在客户端传入的值和键的口令串相匹配时，才对键进行删除。
- 这两个改动可以防止持有过期锁的客户端误删现有锁的情况出现。

以下是一个简单的LUA解锁脚本示例：
```lua
if redis.call("get",KEYS[1]) == ARGV[1]
then
    return redis.call("del",KEYS[1])
else
    return 0
end
```
```java
/*使用lua脚本来锁*/
// 定义lua 脚本
String script = "if redis.call('get', KEYS[1]) == ARGV[1] then return redis.call('del', KEYS[1]) else return 0 end";
// 使用redis执行lua执行
DefaultRedisScript<Long> redisScript = new DefaultRedisScript<>();
redisScript.setScriptText(script);
// 设置一下返回值类型 为Long
// 因为删除判断的时候，返回的0,给其封装为数据类型。如果不封装那么默认返回String 类型，
// 那么返回字符串与0 会有发生错误。
redisScript.setResultType(Long.class);
// 第一个要是script 脚本 ，第二个需要判断的key，第三个就是key所对应的值。
redisTemplate.execute(redisScript, Arrays.asList(locKey), uuid);
```
### 4.7、总结
#### 4.7.1、主要流程

- 加锁
```java
// 1. 从redis中获取锁,set k1 v1 px 20000 nx
String uuid = UUID.randomUUID().toString();
Boolean lock = this.redisTemplate.opsForValue().setIfAbsent("lock", uuid, 2, TimeUnit.SECONDS);
```

- 使用lua释放锁
```java
// 2. 释放锁 del
String script = "if redis.call('get', KEYS[1]) == ARGV[1] then return redis.call('del', KEYS[1]) else return 0 end";
// 设置lua脚本返回的数据类型
DefaultRedisScript<Long> redisScript = new DefaultRedisScript<>();
// 设置lua脚本返回类型为Long
redisScript.setResultType(Long.class);
redisScript.setScriptText(script);
redisTemplate.execute(redisScript, Arrays.asList("lock"),uuid);
```
#### 4.7.2、满足四个条件
为了确保分布式锁可用，我们至少要确保锁的实现同时满足以下四个条件：

- 互斥性。在任意时刻，只有一个客户端能持有锁。
- 不会发生死锁。即使有一个客户端在持有锁的期间崩溃而没有主动解锁，也能保证后续其他客户端能加锁。
- 解铃还须系铃人。加锁和解锁必须是同一个客户端，客户端自己不能把别人加的锁给解了。
- 加锁和解锁必须具有原子性。

# 十五、Redis6 新功能
## 1、ACL
### 1.1、简介
Redis ACL是Access Control List（访问控制列表）的缩写，该功能允许根据可以执行的命令和可以访问的键来限制某些连接。
在Redis 5版本之前，Redis 安全规则只有密码控制，还有通过rename 来调整高危命令比如 flushdb ， KEYS* ， shutdown 等。Redis 6 则提供ACL的功能对用户进行更细粒度的权限控制 ：

- 接入权限:用户名和密码 
- 可以执行的命令 
- 可以操作的 KEY

参考官网：[https://redis.io/topics/acl](https://redis.io/topics/acl)
### 1.2、命令
#### 1.2.1、acl list
使用`acl list`命令展现用户权限列表
![image.png](image/1654007561651-52b6f978-b897-48d7-8518-9da498c82bfe.png)
#### 1.2.2、acl cat
使用`acl cat`命令

- 查看添加权限指令类别
![image.png](image/1654007838140-1d00cca1-44f4-4e1e-82bf-2e1896981d2c.png)
- 加参数类型名可以查看类型下具体命令
![image.png](image/1654007879315-60632d62-8d2a-4a47-8c93-ff2ff8cbac9d.png)
#### 1.2.3、acl whoami
使用`acl whoami`命令查看当前用户
![image.png](image/1654007944468-616f4483-e595-47a1-8293-7e36dc74af68.png)
#### 1.2.4、acl setuser
使用`acl setuser`命令创建和编辑用户ACL

- ACL规则
下面是有效ACL规则的列表。某些规则只是用于激活或删除标志，或对用户ACL执行给定更改的单个单词。其他规则是字符前缀，它们与命令或类别名称、键模式等连接在一起。
![image.png](image/1654008225084-11407e7b-9392-4ce9-b4a7-af920a494a3f.png)
- 通过命令创建新用户默认权限 
   - `acl setuser user1`
   - ![image.png](image/1654008500704-edbb542e-37c3-4cdb-90f7-f5374f0c83d4.png)
   - 在上面的示例中，我根本没有指定任何规则。
   - 如果用户不存在，这将使用just created的默认属性来创建用户。
   - 如果用户已经存在，则上面的命令将不执行任何操作。
- 设置有用户名、密码、ACL权限、并启用的用户。
   - `acl setuser user2 on >password123 ~cached:* +get`
   - ![image.png](image/1654008797187-c62725d3-29ab-430c-b695-eed211954e66.png)
- 切换用户，验证权限
   - ![image.png](image/1654009208155-55245c70-753d-40a5-92d9-192c3a98a7b6.png)
## 2、IO多线程
### 2.1、简介
IO多线程其实指客户端交互部分的网络IO交互处理模块多线程，而非执行命令多线程。Redis6执行命令依然是单线程。
### 2.2、原理架构
Redis 6 加入多线程,但跟 Memcached 这种从 IO处理到数据访问多线程的实现模式有些差异。Redis 的多线程部分只是用来处理网络数据的读写和协议解析，执行命令仍然是单线程。之所以这么设计是不想因为多线程而变得复杂，需要去控制 key、lua、事务，LPUSH/LPOP 等等的并发问题。整体的设计大体如下:
 ![image.png](image/1654009322188-2b54a962-eaac-43b3-8287-e555a6a19c71.png)

另外，多线程IO默认也是不开启的，需要再配置文件中配置

- `io-threads-do-reads  yes`
- `io-threads 4`
## 3、工具支持 Cluster
之前老版Redis想要搭集群需要单独安装ruby环境，Redis 5 将 redis-trib.rb 的功能集成到 redis-cli 。
另外官方 redis-benchmark 工具开始支持 cluster 模式了，通过多线程的方式对多个分片进行压测。
## 4、Redis新功能持续关注
Redis6新功能还有：
1、RESP3新的 Redis 通信协议：优化服务端与客户端之间通信
2、Client side caching客户端缓存：基于 RESP3 协议实现的客户端缓存功能。为了进一步提升缓存的性能，将客户端经常访问的数据cache到客户端。减少TCP网络交互。
3、Proxy集群代理模式：Proxy 功能，让 Cluster 拥有像单实例一样的接入方式，降低大家使用cluster的门槛。不过需要注意的是代理不改变 Cluster 的功能限制，不支持的命令还是不会支持，比如跨 slot 的多Key操作。
4、Modules API
Redis 6中模块API开发进展非常大，因为Redis Labs为了开发复杂的功能，从一开始就用上Redis模块。Redis可以变成一个框架，利用Modules来构建不同系统，而不需要从头开始写然后还要BSD许可。Redis一开始就是一个向编写各种系统开放的平台。