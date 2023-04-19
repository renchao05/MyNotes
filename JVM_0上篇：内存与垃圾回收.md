# 一、 JVM和Java体系架构
## 1、前言
你是否也遇到过这些问题？

1. 运行着的线上系统突然卡死，系统无法访问，甚至直接OOM！
2. 想解决线上JVM GC问题，但却无从下手。
3. 新项目上线，对各种JVM参数设置一脸茫然，直接默认吧然后就JJ了。
4. 每次面试之前都要重新背一遍JVM的一些原理概念性的东西，然而面试官却经常问你在实际项目中如何调优VM参数，如何解决GC、OOM等问题，一脸懵逼。

![](image/1663729623150-f5eef6eb-c953-4003-b265-a4b380ef24cf.png)
大部分Java开发人员，除了会在项目中使用到与Java平台相关的各种高精尖技术，对于Java技术的核心Java虚拟机了解甚少。
### 开发人员如何看待上层框架

1. 一些有一定工作经验的开发人员，打心眼儿里觉得SSM、微服务等上层技术才是重点，基础技术并不重要，这其实是一种本末倒置的“病态”。
2. 如果我们把核心类库的API比做数学公式的话，那么Java虚拟机的知识就好比公式的推导过程。

![](image/1663729621096-38b9e8ad-2d58-4684-ad75-b798e75f1b72.png)

- 计算机系统体系对我们来说越来越远，在不了解底层实现方式的前提下，通过高级语言很容易编写程序代码。但事实上计算机并不认识高级语言。
### 架构师每天都在思考什么？

1. 应该如何让我的系统更快？
2. 如何避免系统出现瓶颈？

**知乎上有条帖子：应该如何看招聘信息，直通年薪50万+？**

1. 参与现有系统的性能优化，重构，保证平台性能和稳定性
2. 根据业务场景和需求，决定技术方向，做技术选型
3. 能够独立架构和设计海量数据下高并发分布式解决方案，满足功能和非功能需求
4. 解决各类潜在系统风险，核心功能的架构与代码编写
5. 分析系统瓶颈，解决各种疑难杂症，性能调优等
### 我们为什么要学习JVM

1. 面试的需要（BATJ、TMD，PKQ等面试都爱问）
2. 中高级程序员必备技能
- 项目管理、调优的需要
1. 追求极客的精神，
   - 比如：垃圾回收算法、JIT、底层原理
### Java VS C++

1. 垃圾收集机制为我们打理了很多繁琐的工作，大大提高了开发的效率，但是，垃圾收集也不是万能的，懂得JVM内部的内存结构、工作机制，是设计高扩展性应用和诊断运行时问题的基础，也是Java工程师进阶的必备能力。
2. C++语言需要程序员自己来分配内存和回收内存，对于高手来说可能更加舒服，但是对于普通开发者，如果技术实力不够，很容易造成内存泄漏。而Java全部交给JVM进行内存分配和回收，这也是一种趋势，减少程序员的工作量。

![](image/1663729621341-0ca57475-e898-46f2-b4db-8a41980f396f.png)
### 什么人需要学JVM？

1. 拥有一定开发经验的Java开发人员，希望升职加薪
2. 软件设计师，架构师
3. 系统调优人员
4. 虚拟机爱好者，JVM实践者
### 推荐及参考书籍
**官方文档**
**英文文档规范**：[https://docs.oracle.com/javase/specs/index.html](https://docs.oracle.com/javase/specs/index.html)
![](image/1663729621881-f157d413-6641-4957-be60-4366ae0a0623.png)
**中文书籍：**
![](image/1663729622386-14e0ef1f-f7a4-4abf-9eae-3799ffaaba4e.png)
周志明老师的这本书**非常推荐看**，不过只推荐看第三版，第三版较第二版更新了很多，个人觉得没必要再看第二版。
![](image/1663729622543-33fecc7d-3359-4bf3-ac79-edbb24d5c753.png)
![](image/1663729623983-a5c045b3-74c4-42ec-976e-8ed4f6741064.png)
### TIOBE排行榜
**TIOBE 排行榜**：[https://www.tiobe.com/tiobe-index/](https://www.tiobe.com/tiobe-index/)
![](image/1663729624409-35709953-11d3-4a01-93d9-9b74d1e06c4c.png)

- 世界上没有最好的编程语言，只有最适用于具体应用场景的编程语言。
- 目前网上一直流传Java被python，go撼动Java第一的地位。学习者不需要太担心，Java强大的生态圈，也不是说是朝夕之间可以被撼动的。
## 2、Java生态圈
Java是目前应用最为广泛的软件开发平台之一。随着Java以及Java社区的不断壮大Java 也早已不再是简简单单的一门计算机语言了，它更是一个平台、一种文化、一个社区。

1. 作为一个平台，Java虚拟机扮演着举足轻重的作用
   - Groovy、Scala、JRuby、Kotlin等都是Java平台的一部分
2. 作为一种文化，Java几乎成为了“开源”的代名词。
   - 第三方开源软件和框架。如Tomcat、Struts，MyBatis，Spring等。
   - 就连JDK和JVM自身也有不少开源的实现，如openJDK、Harmony。
3. 作为一个社区，Java拥有全世界最多的技术拥护者和开源社区支持，有数不清的论坛和资料。从桌面应用软件、嵌入式开发到企业级应用、后台服务器、中间件，都可以看到Java的身影。其应用形式之复杂、参与人数之众多也令人咋舌。
### Java-跨平台的语言
![](image/1663729625664-46e89686-bd4c-400d-a6a0-daf343bd6763.png)
### JVM-跨语言的平台
![](image/1663729624928-3e276932-3377-427a-9ea9-c9e351a78918.png)

1. 随着Java7的正式发布，Java虚拟机的设计者们通过JSR-292规范基本实现在Java虚拟机平台上运行非Java语言编写的程序。
2. Java虚拟机根本不关心运行在其内部的程序到底是使用何种编程语言编写的，它只关心“字节码”文件。也就是说Java虚拟机拥有语言无关性，并不会单纯地与Java语言“终身绑定”，只要其他编程语言的编译结果满足并包含Java虚拟机的内部指令集、符号表以及其他的辅助信息，它就是一个有效的字节码文件，就能够被虚拟机所识别并装载运行。
- Java不是最强大的语言，但是JVM是最强大的虚拟机
1. 我们平时说的java字节码，指的是用java语言编译成的字节码。准确的说任何能在jvm平台上执行的字节码格式都是一样的。所以应该统称为：jvm字节码。
2. 不同的编译器，可以编译出相同的字节码文件，字节码文件也可以在不同的JVM上运行。
3. Java虚拟机与Java语言并没有必然的联系，它只与特定的二进制文件格式——Class文件格式所关联，Class文件中包含了Java虚拟机指令集（或者称为字节码、Bytecodes）和符号表，还有一些其他辅助信息。
### 多语言混合编程

1. Java平台上的多语言混合编程正成为主流，通过特定领域的语言去解决特定领域的问题是当前软件开发应对日趋复杂的项目需求的一个方向。
2. 试想一下，在一个项目之中，并行处理用Clojure语言编写，展示层使用JRuby/Rails，中间层则是Java，每个应用层都将使用不同的编程语言来完成，而且，接口对每一层的开发者都是透明的，各种语言之间的交互不存在任何困难，就像使用自己语言的原生API一样方便，因为它们最终都运行在一个虚拟机之上。
3. 对这些运行于Java虚拟机之上、Java之外的语言，来自系统级的、底层的支持正在迅速增强，以JSR-292为核心的一系列项目和功能改进（如DaVinci Machine项目、Nashorn引擎、InvokeDynamic指令、java.lang.invoke包等），推动Java虚拟机从“Java语言的虚拟机”向 “多语言虚拟机”的方向发展。
### 如何真正搞懂JVM？

1. Java虚拟机非常复杂，要想真正理解它的工作原理，最好的方式就是自己动手编写一个！
2. 自己动手写一个Java虚拟机，难吗？
3. 天下事有难易乎？为之，则难者亦易矣；不为，则易者亦难矣

![](image/1663729625236-44f65a90-4204-4de2-ba13-c334f1c83c40.png)
### Java发展重大事件

- 1990年，在Sun计算机公司中，由Patrick Naughton、MikeSheridan及James Gosling领导的小组Green Team，开发出的新的程序语言，命名为Oak，后期命名为Java
- 1995年，Sun正式发布Java和HotJava产品，Java首次公开亮相。
- 1996年1月23日Sun Microsystems发布了JDK 1.0。
- 1998年，JDK1.2版本发布。同时，Sun发布了JSP/Servlet、EJB规范，以及将Java分成了J2EE、J2SE和J2ME。这表明了Java开始向企业、桌面应用和移动设备应用3大领域挺进。
- 2000年，JDK1.3发布，Java HotSpot Virtual Machine正式发布，成为Java的默认虚拟机。
- 2002年，JDK1.4发布，古老的Classic虚拟机退出历史舞台。
- 2003年年底，Java平台的scala正式发布，同年Groovy也加入了Java阵营。
- 2004年，JDK1.5发布。同时JDK1.5改名为JavaSE5.0。
- 2006年，JDK6发布。同年，Java开源并建立了OpenJDK。顺理成章，Hotspot虚拟机也成为了OpenJDK中的默认虚拟机。
- 2007年，Java平台迎来了新伙伴Clojure。
- 2008年，oracle收购了BEA，得到了JRockit虚拟机。
- 2009年，Twitter宣布把后台大部分程序从Ruby迁移到Scala，这是Java平台的又一次大规模应用。
- 2010年，Oracle收购了Sun，获得Java商标和最真价值的HotSpot虚拟机。此时，Oracle拥有市场占用率最高的两款虚拟机HotSpot和JRockit，并计划在未来对它们进行整合：HotRockit。JCP组织管理Java语言
- 2011年，JDK7发布。在JDK1.7u4中，正式启用了新的垃圾回收器G1。
- **2017年，JDK9发布。将G1设置为默认GC，替代CMS**
- 同年，IBM的J9开源，形成了现在的Open J9社区
- 2018年，Android的Java侵权案判决，Google赔偿Oracle计88亿美元
- 同年，Oracle宣告JavagE成为历史名词JDBC、JMS、Servlet赠予Eclipse基金会
- **同年，JDK11发布，LTS版本的JDK，发布革命性的ZGC，调整JDK授权许可**
- 2019年，JDK12发布，加入RedHat领导开发的Shenandoah GC
### Open JDK和Oracle JDK
![](image/1663729625870-ecaff3ad-e9a3-445c-a38c-9d24f5804463.png)

- 在JDK11之前，Oracle JDK中还会存在一些Open JDK中没有的，闭源的功能。但在JDK11中，我们可以认为Open JDK和Oracle JDK代码实质上已经达到完全一致的程度了。
- 主要的区别就是两者更新周期不一样
## 3、虚拟机
### 虚拟机概念

- 所谓虚拟机（Virtual Machine），就是一台虚拟的计算机。它是一款软件，用来执行一系列虚拟计算机指令。大体上，虚拟机可以分为系统虚拟机和程序虚拟机。
   - 大名鼎鼎的Virtual Box，VMware就属于系统虚拟机，它们完全是对物理计算机硬件的仿真(模拟)，提供了一个可运行完整操作系统的软件平台。
   - 程序虚拟机的典型代表就是Java虚拟机，它专门为执行单个计算机程序而设计，在Java虚拟机中执行的指令我们称为Java字节码指令。
- 无论是系统虚拟机还是程序虚拟机，在上面运行的软件都被限制于虚拟机提供的资源中。
### Java虚拟机

1. Java虚拟机是一台执行Java字节码的虚拟计算机，它拥有独立的运行机制，其运行的Java字节码也未必由Java语言编译而成。
2. JVM平台的各种语言可以共享Java虚拟机带来的跨平台性、优秀的垃圾回器，以及可靠的即时编译器。
3. **Java技术的核心就是Java虚拟机**（JVM，Java Virtual Machine），因为所有的Java程序都运行在Java虚拟机内部。

**作用：**
Java虚拟机就是二进制字节码的运行环境，负责装载字节码到其内部，解释/编译为对应平台上的机器指令执行。每一条Java指令，Java虚拟机规范中都有详细定义，如怎么取操作数，怎么处理操作数，处理结果放在哪里。
**特点：**

1. 一次编译，到处运行
2. 自动内存管理
3. 自动垃圾回收功能
### JVM的位置
JVM是运行在操作系统之上的，它与硬件没有直接的交互
![](image/1663729626000-aadc0f6a-bc03-493b-8545-ff3e77a92a62.png)
![](image/1663729626612-154678ec-0509-446b-8071-17dd026ed739.png)
### JVM的整体结构

1. HotSpot VM是目前市面上高性能虚拟机的代表作之一。
2. 它采用解释器与即时编译器并存的架构。
3. 在今天，Java程序的运行性能早已脱胎换骨，已经达到了可以和C/C++程序一较高下的地步。

![](image/1663729632337-dd8836f6-ac80-4809-8148-c0102e18ea4b.png)
### Java代码执行流程
凡是能生成被Java虚拟机所能解释、运行的字节码文件，那么理论上我们就可以自己设计一套语言了
![](image/1663729628447-1450be83-55fc-48ff-8e64-4c4b8f4ff448.png)
### JVM的架构模型
Java编译器输入的指令流基本上是一种**基于栈的指令集架构**，另外一种指令集架构则是**基于寄存器的指令集架构**。具体来说：这两种架构之间的区别：
#### 基于栈的指令集架构
基于栈式架构的特点：

1. 设计和实现更简单，适用于资源受限的系统；
2. 避开了寄存器的分配难题：使用零地址指令方式分配
3. 指令流中的指令大部分是零地址指令，其执行过程依赖于操作栈。指令集更小，编译器容易实现
4. 不需要硬件支持，可移植性更好，更好实现跨平台
#### 基于寄存器的指令级架构
基于寄存器架构的特点：

1. 典型的应用是x86的二进制指令集：比如传统的PC以及Android的Davlik虚拟机。
2. 指令集架构则完全依赖硬件，与硬件的耦合度高，可移植性差
3. 性能优秀和执行更高效
4. 花费更少的指令去完成一项操作
5. 在大部分情况下，基于寄存器架构的指令集往往都以一地址指令、二地址指令和三地址指令为主，而基于栈式架构的指令集却是以零地址指令为主
#### 两种架构的举例
同样执行2+3这种逻辑操作，其指令分别如下：

- **基于栈的计算流程（以Java虚拟机为例）：**
```bash
iconst_2 #常量2入栈
istore_1
iconst_3 #常量3入栈
istore_2
iload_1
iload_2
iadd #常量2/3出栈，执行相加
istore_0 #结果5入栈
```

- **而基于寄存器的计算流程**
```bash
mov eax,2 #将eax寄存器的值设为1
add eax,3 #使eax寄存器的值加3
```
#### JVM架构总结

1. **由于跨平台性的设计，Java的指令都是根据栈来设计的**。不同平台CPU架构不同，所以不能设计为基于寄存器的。栈的优点：跨平台，指令集小，编译器容易实现，缺点是性能比寄存器差一些。
2. 时至今日，尽管嵌入式平台已经不是Java程序的主流运行平台了（准确来说应该是HotSpot VM的宿主环境已经不局限于嵌入式平台了），那么为什么不将架构更换为基于寄存器的架构呢？
- 因为基于栈的架构跨平台性好、指令集小，虽然相对于基于寄存器的架构来说，基于栈的架构编译得到的指令更多，执行性能也不如基于寄存器的架构好，但考虑到其跨平台性与移植性，我们还是选用栈的架构
### JVM的生命周期
#### 虚拟机的启动
Java虚拟机的启动是通过引导类加载器（bootstrap class loader）创建一个初始类（initial class）来完成的，这个类是由虚拟机的具体实现指定的。
#### 虚拟机的执行

1. 一个运行中的Java虚拟机有着一个清晰的任务：执行Java程序
2. 程序开始执行时他才运行，程序结束时他就停止
3. **执行一个所谓的Java程序的时候，真真正正在执行的是一个叫做Java虚拟机的进程**
#### 虚拟机的退出
**有如下的几种情况：**

1. 程序正常执行结束
2. 程序在执行过程中遇到了异常或错误而异常终止
3. 由于操作系统用现错误而导致Java虚拟机进程终止
4. 某线程调用Runtime类或System类的exit()方法，或Runtime类的halt()方法，并且Java安全管理器也允许这次exit()或halt()操作。
5. 除此之外，JNI（Java Native Interface）规范描述了用JNI Invocation API来加载或卸载 Java虚拟机时，Java虚拟机的退出情况。
## 4、常见JVM虚拟机
### Sun Classic VM

1. 早在1996年Java1.0版本的时候，Sun公司发布了一款名为sun classic VM的Java虚拟机，它同时也是**世界上第一款商用Java虚拟机**，JDK1.4时完全被淘汰。
2. 这款虚拟机内部只提供解释器，没有即时编译器，因此效率比较低。【即时编译器会把热点代码的本地机器指令缓存起来，那么以后使用热点代码的时候，效率就比较高】
3. 如果使用JIT编译器，就需要进行外挂。但是一旦使用了JIT编译器，JIT就会接管虚拟机的执行系统。解释器就不再工作，解释器和编译器不能配合工作。
   - 我们将字节码指令翻译成机器指令也是需要花时间的，如果只使用JIT，就需要把所有字节码指令都翻译成机器指令，就会导致翻译时间过长，也就是说在程序刚启动的时候，等待时间会很长。
   - 而解释器就是走到哪，解释到哪。
4. 现在Hotspot内置了此虚拟机。
### Exact VM

1. 为了解决上一个虚拟机问题，jdk1.2时，Sun提供了此虚拟机。
2. Exact Memory Management：准确式内存管理
   - 也可以叫Non-Conservative/Accurate Memory Management
   - 虚拟机可以知道内存中某个位置的数据具体是什么类型。
3. 具备现代高性能虚拟机的维形
   - 热点探测（寻找出热点代码进行缓存）
   - 编译器与解释器混合工作模式
4. 只在Solaris平台短暂使用，其他平台上还是classic vm，英雄气短，终被Hotspot虚拟机替换
### HotSpot VM（重点）

1. HotSpot历史
   - 最初由一家名为“Longview Technologies”的小公司设计
   - 1997年，此公司被Sun收购；2009年，Sun公司被甲骨文收购。
   - JDK1.3时，HotSpot VM成为默认虚拟机
2. 目前**Hotspot占有绝对的市场地位，称霸武林**。
   - 不管是现在仍在广泛使用的JDK6，还是使用比例较多的JDK8中，默认的虚拟机都是HotSpot
   - Sun/oracle JDK和openJDK的默认虚拟机
   - 因此本课程中默认介绍的虚拟机都是HotSpot，相关机制也主要是指HotSpot的GC机制。（比如其他两个商用虚机都没有方法区的概念）
3. 从服务器、桌面到移动端、嵌入式都有应用。
4. 名称中的HotSpot指的就是它的热点代码探测技术。
   - 通过计数器找到最具编译价值代码，触发即时编译或栈上替换
   - 通过编译器与解释器协同工作，在最优化的程序响应时间与最佳执行性能中取得平衡
### JRockit（商用三大虚拟机之一）

1. 专注于服务器端应用：它可以不太关注程序启动速度，因此JRockit内部不包含解析器实现，全部代码都靠即时编译器编译后执行。
2. 大量的行业基准测试显示，JRockit JVM是世界上最快的JVM：使用JRockit产品，客户已经体验到了显著的性能提高（一些超过了70%）和硬件成本的减少（达50%）。
3. 优势：全面的Java运行时解决方案组合
   - JRockit面向延迟敏感型应用的解决方案JRockit Real Time提供以毫秒或微秒级的JVM响应时间，适合财务、军事指挥、电信网络的需要
   - Mission Control服务套件，它是一组以极低的开销来监控、管理和分析生产环境中的应用程序的工具。
4. 2008年，JRockit被Oracle收购。
5. Oracle表达了整合两大优秀虚拟机的工作，大致在JDK8中完成。整合的方式是在HotSpot的基础上，移植JRockit的优秀特性。
6. 高斯林：目前就职于谷歌，研究人工智能和水下机器人
### IBM的J9（商用三大虚拟机之一）

1. 全称：IBM Technology for Java Virtual Machine，简称IT4J，内部代号：J9
2. 市场定位与HotSpot接近，服务器端、桌面应用、嵌入式等多用途VM广泛用于IBM的各种Java产品。
3. 目前，有影响力的三大商用虚拟机之一，也号称是世界上最快的Java虚拟机。
4. 2017年左右，IBM发布了开源J9VM，命名为openJ9，交给Eclipse基金会管理，也称为Eclipse OpenJ9
5. OpenJDK -> 是JDK开源了，包括了虚拟机
### KVM和CDC/CLDC Hotspot

1. Oracle在Java ME产品线上的两款虚拟机为：CDC/CLDC HotSpot Implementation VM
2. KVM（Kilobyte）是CLDC-HI早期产品
3. 目前移动领域地位尴尬，智能机被Android和iOS二分天下。
4. KVM简单、轻量、高度可移植，面向更低端的设备上还维持自己的一片市场
   - 智能控制器、传感器
   - 老人手机、经济欠发达地区的功能手机
5. 所有的虚拟机的原则：一次编译，到处运行。
### Azul VM

1. 前面三大“高性能Java虚拟机”使用在**通用硬件平台上**
2. 这里Azul VW和BEA Liquid VM是与**特定硬件平台绑定**、软硬件配合的专有虚拟机：高性能Java虚拟机中的战斗机。
3. Azul VM是Azul Systems公司在HotSpot基础上进行大量改进，运行于Azul Systems公司的专有硬件Vega系统上的Java虚拟机。
4. 每个Azul VM实例都可以管理至少数十个CPU和数百GB内存的硬件资源，并提供在巨大内存范围内实现可控的GC时间的垃圾收集器、专有硬件优化的线程调度等优秀特性。
5. 2010年，Azul Systems公司开始从硬件转向软件，发布了自己的Zing JVM，可以在通用x86平台上提供接近于Vega系统的特性。
### Liquid VM

1. 高性能Java虚拟机中的战斗机。
2. BEA公司开发的，直接运行在自家Hypervisor系统上
3. Liquid VM即是现在的JRockit VE（Virtual Edition）。**Liquid VM不需要操作系统的支持，或者说它自己本身实现了一个专用操作系统的必要功能，如线程调度、文件系统、网络支持等**。
4. 随着JRockit虚拟机终止开发，Liquid vM项目也停止了。
### Apache Marmony

1. Apache也曾经推出过与JDK1.5和JDK1.6兼容的Java运行平台Apache Harmony。
2. 它是IElf和Intel联合开发的开源JVM，受到同样开源的Open JDK的压制，Sun坚决不让Harmony获得JCP认证，最终于2011年退役，IBM转而参与OpenJDK
3. 虽然目前并没有Apache Harmony被大规模商用的案例，但是它的Java类库代码吸纳进了Android SDK。
### Micorsoft JVM

1. 微软为了在IE3浏览器中支持Java Applets，开发了Microsoft JVM。
2. 只能在window平台下运行。但确是当时Windows下性能最好的Java VM。
3. 1997年，Sun以侵犯商标、不正当竞争罪名指控微软成功，赔了Sun很多钱。微软WindowsXP SP3中抹掉了其VM。现在Windows上安装的jdk都是HotSpot。
### Taobao JVM

1. 由AliJVM团队发布。阿里，国内使用Java最强大的公司，覆盖云计算、金融、物流、电商等众多领域，需要解决高并发、高可用、分布式的复合问题。有大量的开源产品。
2. **基于OpenJDK开发了自己的定制版本AlibabaJDK**，简称AJDK。是整个阿里Java体系的基石。
3. 基于OpenJDK Hotspot VM发布的国内第一个优化、深度定制且开源的高性能服务器版Java虚拟机。
   - 创新的GCIH（GCinvisible heap）技术实现了off-heap，**即将生命周期较长的Java对象从heap中移到heap之外，并且GC不能管理GCIH内部的Java对象，以此达到降低GC的回收频率和提升GC的回收效率的目的**。
   - GCIH中的**对象还能够在多个Java虚拟机进程中实现共享**
   - 使用crc32指令实现JvM intrinsic降低JNI的调用开销
   - PMU hardware的Java profiling tool和诊断协助功能
   - 针对大数据场景的ZenGC
4. taobao vm应用在阿里产品上性能高，**硬件严重依赖inte1的cpu，损失了兼容性，但提高了性能**
- 目前已经在淘宝、天猫上线，把Oracle官方JvM版本全部替换了。
### Dalvik VM

1. 谷歌开发的，应用于Android系统，并在Android2.2中提供了JIT，发展迅猛。
2. **Dalvik VM只能称作虚拟机，而不能称作“Java虚拟机”**，它没有遵循 Java虚拟机规范
3. 不能直接执行Java的Class文件
4. 基于寄存器架构，不是jvm的栈架构。
5. 执行的是编译以后的dex（Dalvik Executable）文件。执行效率比较高。
- 它执行的dex（Dalvik Executable）文件可以通过class文件转化而来，使用Java语法编写应用程序，可以直接使用大部分的Java API等。
1. Android 5.0使用支持提前编译（Ahead of Time Compilation，AoT）的ART VM替换Dalvik VM。
### Graal VM（未来虚拟机）

1. 2018年4月，Oracle Labs公开了GraalvM，号称 “**Run Programs Faster Anywhere**”，勃勃野心。与1995年java的”write once，run anywhere"遥相呼应。
2. GraalVM在HotSpot VM基础上增强而成的**跨语言全栈虚拟机，可以作为“任何语言”**的运行平台使用。语言包括：Java、Scala、Groovy、Kotlin；C、C++、Javascript、Ruby、Python、R等
3. 支持不同语言中混用对方的接口和对象，支持这些语言使用已经编写好的本地库文件
4. 工作原理是将这些语言的源代码或源代码编译后的中间格式，通过解释器转换为能被Graal VM接受的中间表示。Graal VM提供Truffle工具集快速构建面向一种新语言的解释器。在运行时还能进行即时编译优化，获得比原生编译器更优秀的执行效率。
5. **如果说HotSpot有一天真的被取代，Graalvm希望最大**。但是Java的软件生态没有丝毫变化。
### 总结
具体JVM的内存结构，其实取决于其实现，不同厂商的JVM，或者同一厂商发布的不同版本，都有可能存在一定差异。主要以Oracle HotSpot VM为默认虚拟机。


# 二、 类加载子系统
## 1、内存结构概述
### 简图
![](image/1663809162262-6e3d0f82-e2fb-4944-8eb6-df7ceaaf1324.png)
### 详细图
英文版
[![](https://cdn.nlark.com/yuque/0/2022/jpeg/26368762/1663809164160-ce1359c5-c258-4d7a-88ee-f017fbb69715.jpeg#clientId=u253d8d4a-de97-4&crop=0&crop=0&crop=1&crop=1&from=paste&id=u03c75907&margin=%5Bobject%20Object%5D&originHeight=1577&originWidth=1668&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u28d92a8f-fcac-42e4-9655-d648ba49b0f&title=)](https://camo.githubusercontent.com/122c24f7d79e3919b4c77029528b6c26a3c1492365693510b9d3e9667d7dfd62/68747470733a2f2f6e706d2e656c656d6563646e2e636f6d2f796f7574686c716c40312e302e382f4a564d2f636861707465725f3030322f303030322e6a7067)
中文版
[![](https://cdn.nlark.com/yuque/0/2022/jpeg/26368762/1663809162486-04b7be68-5a19-4a2a-8f15-83616e2abdaa.jpeg#clientId=u253d8d4a-de97-4&crop=0&crop=0&crop=1&crop=1&from=paste&id=u8166374c&margin=%5Bobject%20Object%5D&originHeight=1579&originWidth=1669&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u0b05cb15-82b6-4699-bd15-2507d2cde15&title=)](https://camo.githubusercontent.com/910cc3ce5f121524aaeec0279b9a83c8d25ff711a4d5151f5d08316e99947e12/68747470733a2f2f6e706d2e656c656d6563646e2e636f6d2f796f7574686c716c40312e302e382f4a564d2f636861707465725f3030322f303030332e6a7067)
注意：方法区只有HotSpot虚拟机有，J9，JRockit都没有
如果自己想手写一个Java虚拟机的话，主要考虑哪些结构呢？

1. 类加载器
2. 执行引擎
## 2、类加载器子系统
### 类加载器子系统作用

1. 类加载器子系统负责从文件系统或者网络中加载Class文件，class文件在文件开头有特定的文件标识。
2. ClassLoader只负责class文件的加载，至于它是否可以运行，则由Execution Engine决定。
3. **加载的类信息存放于一块称为方法区的内存空间**。除了类的信息外，方法区中还会存放运行时常量池信息，可能还包括字符串字面量和数字常量（这部分常量信息是Class文件中常量池部分的内存映射）

![](image/1663809161521-658cbc7d-c26b-47a2-9709-0d63d8dea127.png)
### 类加载器ClassLoader

1. class file（在下图中就是Car.class文件）存在于本地硬盘上，可以理解为设计师画在纸上的模板，而最终这个模板在执行的时候是要加载到JVM当中来根据这个文件实例化出n个一模一样的实例。
2. class file加载到JVM中，被称为DNA元数据模板（在下图中就是内存中的Car Class），放在方法区。
3. 在.class文件–>JVM–>最终成为元数据模板，此过程就要一个运输工具（类装载器Class Loader），扮演一个快递员的角色。

![](image/1663809161891-c6d05037-ab91-4619-b7e0-dc7c4e7526b2.png)
## 3、类加载过程
### 概述
```java
/**
 *示例代码
 */
public class HelloLoader {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```
加载过程

- 执行 main() 方法（静态方法）就需要先加载main方法所在类 HelloLoader
- 加载成功，则进行链接、初始化等操作。完成后调用 HelloLoader 类中的静态方法 main
- 加载失败则抛出异常

![](image/1663809163418-6756dce3-72e0-470a-9f45-c26cec03ae39.png)
完整的流程图如下所示：
![](image/1663809167340-4a12e45a-1057-41fc-b08a-d5752157c407.png)
### 加载阶段

1. 通过一个类的全限定名获取定义此类的二进制字节流
2. 将这个字节流所代表的静态存储结构转化为方法区的运行时数据结构
3. **在内存中生成一个代表这个类的java.lang.Class对象**，作为方法区这个类的各种数据的访问入口

**加载class文件的方式：**

1. 从本地系统中直接加载
2. 通过网络获取，典型场景：Web Applet
3. 从zip压缩包中读取，成为日后jar、war格式的基础
4. 运行时计算生成，使用最多的是：动态代理技术
5. 由其他文件生成，典型场景：JSP应用从专有数据库中提取.class文件，比较少见
6. 从加密文件中获取，典型的防Class文件被反编译的保护措施
### 链接阶段
链接分为三个子阶段：验证 -> 准备 -> 解析
#### 验证(Verify)

1. 目的在于确保Class文件的字节流中包含信息符合当前虚拟机要求，保证被加载类的正确性，不会危害虚拟机自身安全
2. 主要包括四种验证，文件格式验证，元数据验证，字节码验证，符号引用验证。

使用 BinaryViewer软件查看字节码文件，其开头均为 CAFE BABE ，如果出现不合法的字节码文件，那么将会验证不通过。
![image.png](image/1663810629491-87c7be41-206d-404c-9753-d23c25922223.png)

#### 准备(Prepare)

1. 为类变量（static变量）分配内存并且设置该类变量的默认初始值，即零值
2. 这里不包含用final修饰的static，因为**final在编译的时候就会分配好了默认值**，准备阶段会显式初始化
3. 注意：这里不会为实例变量分配初始化，类变量会分配在方法区中，而实例变量是会随着对象一起分配到Java堆中

**举例**
代码：变量a在准备阶段会赋初始值0
```java
public class HelloApp {
    private static int a = 1;//prepare：a = 0 ---> initial : a = 1

    public static void main(String[] args) {
        System.out.println(a);
    }
}
```
#### 解析(Resolve)

1. **将常量池内的符号引用转换为直接引用的过程**
2. 事实上，解析操作往往会伴随着JVM在执行完初始化之后再执行
3. 符号引用就是一组符号来描述所引用的目标。符号引用的字面量形式明确定义在《java虚拟机规范》的class文件格式中。直接引用就是直接指向目标的指针、相对偏移量或一个间接定位到目标的句柄
4. 解析动作主要针对**类或接口、字段、类方法、接口方法、方法类型**等。对应常量池中的CONSTANT Class info、CONSTANT Fieldref info、CONSTANT Methodref info等

**符号引用**

- 反编译 class 文件后可以查看符号引用，下面带# 的就是符号引用

![](image/1663809169801-66932248-a3ac-45f3-ae66-02b571858234.png)
### 初始化阶段
#### 初始化时机

1. 创建类的实例
2. 访问某个类或接口的静态变量，或者对该静态变量赋值
3. 调用类的静态方法
4. 反射（比如：Class.forName(“com.atguigu.Test”)）
5. 初始化一个类的子类
6. Java虚拟机启动时被标明为启动类的类
7. JDK7开始提供的动态语言支持：java.lang.invoke.MethodHandle实例的解析结果REF_getStatic、REF putStatic、REF_invokeStatic句柄对应的类没有初始化，则初始化
> 除了以上七种情况，其他使用Java类的方式都被看作是对类的被动使用，都不会导致类的初始化。
> 即不会执行初始化阶段（不会调用 clinit() 方法和 init() 方法）

#### clinit()

1. 初始化阶段就是执行类构造器方法<clinit>()的过程
2. 此方法不需定义，是javac编译器自动收集类中的所有**类变量**的赋值动作和静态代码块中的语句合并而来。也就是说，当我们代码中包含static变量的时候，就会有clinit方法
3. <clinit>()方法中的指令按语句在源文件中出现的顺序执行
4. <clinit>()不同于类的构造器。（关联：构造器是虚拟机视角下的<init>()）
5. 若该类具有父类，JVM会保证子类的<clinit>()执行前，父类的<clinit>()已经执行完毕
6. 虚拟机必须保证一个类的<clinit>()方法在多线程下被同步加锁
> IDEA 中安装 JClassLib Bytecode viewer 插件，可以很方便的看字节码。安装过程可以自行百度

#### 案例
**举例1：有static变量**
查看下面这个代码的字节码，可以发现有一个<clinit>()方法。
![](image/1663809172768-04dee99f-1879-4680-893a-2747ee644cc6.png)
> 当我们代码中包含static变量的时候，就会有clinit方法



**举例2：无 static 变量**
![](image/1663809180350-834d03be-8896-49ea-9688-adae6d11aff4.png)
加上之后就有了
![](image/1663809182435-3b6565f2-7e0c-4f05-91fe-53f84db1ee3e.png)

案例3：
![](image/1663809182179-b075b964-47fb-4f13-8394-bbc2feb7bfdc.png)
> 在构造器中：
> - 先将类变量 a 赋值为 10
> - 再将局部变量赋值为 20


案例4：
若该类具有父类，JVM会保证子类的<clinit>()执行前，父类的<clinit>()已经执行完毕
![](image/1663809182292-8a26bf5e-62dd-4f5b-8be7-63c238965974.png)
如上代码，加载流程如下：

- 首先，执行 main() 方法需要加载 ClinitTest1 类
- 获取 Son.B 静态变量，需要加载 Son 类
- Son 类的父类是 Father 类，所以需要先执行 Father 类的加载，再执行 Son 类的加载

案例5：
虚拟机必须保证一个类的<clinit>()方法在多线程下被同步加锁
```java
public class DeadThreadTest {
    public static void main(String[] args) {
        Runnable r = () -> {
            System.out.println(Thread.currentThread().getName() + "开始");
            DeadThread dead = new DeadThread();
            System.out.println(Thread.currentThread().getName() + "结束");
        };

        Thread t1 = new Thread(r,"线程1");
        Thread t2 = new Thread(r,"线程2");

        t1.start();
        t2.start();
    }
}

class DeadThread{
    static{
        if(true){
            System.out.println(Thread.currentThread().getName() + "初始化当前类");
            while(true){

            }
        }
    }
}
```
输出结果：
线程2开始 线程1开始 线程2初始化当前类 /然后程序卡死了 
程序卡死，分析原因：

- 两个线程同时去加载 DeadThread 类，而 DeadThread 类中静态代码块中有一处死循环
- 先加载 DeadThread 类的线程抢到了同步锁，然后在类的静态代码块中执行死循环，而另一个线程在等待同步锁的释放
- 所以无论哪个线程先执行 DeadThread 类的加载，另外一个类也不会继续执行。（一个类只会被加载一次）
## 4、类加载器的分类
### 概述

1. JVM严格来讲支持两种类型的类加载器 。分别为引导类加载器（Bootstrap ClassLoader）和自定义类加载器（User-Defined ClassLoader）
2. **所有派生于抽象类ClassLoader的类加载器都划分为自定义类加载器**
3. 无论类加载器的类型如何划分，在程序中我们最常见的类加载器始终只有3个，如下所示

![](image/1663809184887-97387388-80e7-41a9-a818-7a45a0c78be2.png)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/26368762/1663811970308-64a6f250-710c-488e-b0d1-54da419c144f.png#clientId=u253d8d4a-de97-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=326&id=udfb3ee5c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=326&originWidth=445&originalType=binary&ratio=1&rotation=0&showTitle=false&size=12034&status=done&style=none&taskId=u696be251-69e0-4e94-b237-3677dbb641f&title=&width=445)

```java
public class ClassLoaderTest {
    public static void main(String[] args) {

        //获取系统类加载器
        ClassLoader systemClassLoader = ClassLoader.getSystemClassLoader();
        System.out.println(systemClassLoader);//sun.misc.Launcher$AppClassLoader@18b4aac2

        //获取其上层：扩展类加载器
        ClassLoader extClassLoader = systemClassLoader.getParent();
        System.out.println(extClassLoader);//sun.misc.Launcher$ExtClassLoader@1540e19d

        //获取其上层：获取不到引导类加载器
        ClassLoader bootstrapClassLoader = extClassLoader.getParent();
        System.out.println(bootstrapClassLoader);//null

        //对于用户自定义类来说：默认使用系统类加载器进行加载
        ClassLoader classLoader = ClassLoaderTest.class.getClassLoader();
        System.out.println(classLoader);//sun.misc.Launcher$AppClassLoader@18b4aac2

        //String类使用引导类加载器进行加载的。---> Java的核心类库都是使用引导类加载器进行加载的。
        ClassLoader classLoader1 = String.class.getClassLoader();
        System.out.println(classLoader1);//null

    }
}
```

- 我们尝试获取引导类加载器，获取到的值为 null ，这并不代表引导类加载器不存在，**因为引导类加载器右 C/C++ 语言，我们获取不到**
- 两次获取系统类加载器的值都相同：sun.misc.Launcher$AppClassLoader@18b4aac2 ，这说明**系统类加载器是全局唯一的**
### 启动类加载器
> **引导类加载器，Bootstrap ClassLoader**
> 虚拟机自带的加载器

1. 这个类加载使用C/C++语言实现的，嵌套在JVM内部
2. 它用来加载Java的核心库（JAVA_HOME/jre/lib/rt.jar、resources.jar或sun.boot.class.path路径下的内容），用于提供JVM自身需要的类
3. 并不继承自java.lang.ClassLoader，没有父加载器
4. 加载扩展类和应用程序类加载器，并作为他们的父类加载器
5. 出于安全考虑，Bootstrap启动类加载器只加载包名为java、javax、sun等开头的类
### 扩展类加载器
**Extension ClassLoader**

1. Java语言编写，由sun.misc.Launcher$ExtClassLoader实现
2. 派生于ClassLoader类
3. 父类加载器为启动类加载器
4. 从java.ext.dirs系统属性所指定的目录中加载类库，或从JDK的安装目录的jre/lib/ext子目录（扩展目录）下加载类库。如果用户创建的JAR放在此目录下，也会自动由扩展类加载器加载
### 系统类加载器
**应用程序类加载器（也称为系统类加载器，AppClassLoader）**

1. Java语言编写，由sun.misc.LaunchersAppClassLoader实现
2. 派生于ClassLoader类
3. 父类加载器为扩展类加载器
4. 它负责加载环境变量classpath或系统属性java.class.path指定路径下的类库
5. 该类加载是程序中默认的类加载器，一般来说，Java应用的类都是由它来完成加载
6. 通过classLoader.getSystemclassLoader()方法可以获取到该类加载器
```java
public class ClassLoaderTest1 {
    public static void main(String[] args) {
        System.out.println("**********启动类加载器**************");
        //获取BootstrapClassLoader能够加载的api的路径
        URL[] urLs = sun.misc.Launcher.getBootstrapClassPath().getURLs();
        for (URL element : urLs) {
            System.out.println(element.toExternalForm());
        }
        //从上面的路径中随意选择一个类,来看看他的类加载器是什么:引导类加载器
        ClassLoader classLoader = Provider.class.getClassLoader();
        System.out.println(classLoader);

        System.out.println("***********扩展类加载器*************");
        String extDirs = System.getProperty("java.ext.dirs");
        for (String path : extDirs.split(";")) {
            System.out.println(path);
        }

        //从上面的路径中随意选择一个类,来看看他的类加载器是什么:扩展类加载器
        ClassLoader classLoader1 = CurveDB.class.getClassLoader();
        System.out.println(classLoader1);//sun.misc.Launcher$ExtClassLoader@1540e19d

    }
}

```
**输出结果**
```bash
**********启动类加载器**************
file:/C:/Program%20Files/Java/jdk1.8.0_131/jre/lib/resources.jar
file:/C:/Program%20Files/Java/jdk1.8.0_131/jre/lib/rt.jar
file:/C:/Program%20Files/Java/jdk1.8.0_131/jre/lib/sunrsasign.jar
file:/C:/Program%20Files/Java/jdk1.8.0_131/jre/lib/jsse.jar
file:/C:/Program%20Files/Java/jdk1.8.0_131/jre/lib/jce.jar
file:/C:/Program%20Files/Java/jdk1.8.0_131/jre/lib/charsets.jar
file:/C:/Program%20Files/Java/jdk1.8.0_131/jre/lib/jfr.jar
file:/C:/Program%20Files/Java/jdk1.8.0_131/jre/classes
null
***********扩展类加载器*************
C:\Program Files\Java\jdk1.8.0_131\jre\lib\ext
C:\Windows\Sun\Java\lib\ext
sun.misc.Launcher$ExtClassLoader@29453f44
```
### 用户自定义类加载器
**什么时候需要自定义类加载器？**
在Java的日常应用程序开发中，类的加载几乎是由上述3种类加载器相互配合执行的，在必要时，我们还可以自定义类加载器，来定制类的加载方式。那为什么还需要自定义类加载器？

1. 隔离加载类（比如说我假设现在Spring框架，和RocketMQ有包名路径完全一样的类，类名也一样，这个时候类就冲突了。不过一般的主流框架和中间件都会自定义类加载器，实现不同的框架，中间价之间是隔离的）
2. 修改类加载的方式
3. 扩展加载源（还可以考虑从数据库中加载类，路由器等等不同的地方）
4. 防止源码泄漏（对字节码文件进行解密，自己用的时候通过自定义类加载器来对其进行解密）

**如何自定义类加载器？**

1. 开发人员可以通过继承抽象类java.lang.ClassLoader类的方式，实现自己的类加载器，以满足一些特殊的需求
2. 在JDK1.2之前，在自定义类加载器时，总会去继承ClassLoader类并重写loadClass()方法，从而实现自定义的类加载类，但是在JDK1.2之后已不再建议用户去覆盖loadClass()方法，而是建议把自定义的类加载逻辑写在findclass()方法中
3. 在编写自定义类加载器时，如果没有太过于复杂的需求，可以直接继承URIClassLoader类，这样就可以避免自己去编写findclass()方法及其获取字节码流的方式，使自定义类加载器编写更加简洁。

**代码示例**
```java
public class CustomClassLoader extends ClassLoader {
    @Override
    protected Class<?> findClass(String name) throws ClassNotFoundException {

        try {
            byte[] result = getClassFromCustomPath(name);
            if (result == null) {
                throw new FileNotFoundException();
            } else {
                //defineClass和findClass搭配使用
                return defineClass(name, result, 0, result.length);
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }

        throw new ClassNotFoundException(name);
    }
	//自定义流的获取方式
    private byte[] getClassFromCustomPath(String name) {
        //从自定义路径中加载指定类:细节略
        //如果指定路径的字节码文件进行了加密，则需要在此方法中进行解密操作。
        return null;
    }

    public static void main(String[] args) {
        CustomClassLoader customClassLoader = new CustomClassLoader();
        try {
            Class<?> clazz = Class.forName("One", true, customClassLoader);
            Object obj = clazz.newInstance();
            System.out.println(obj.getClass().getClassLoader());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
### 关于ClassLoader
**ClassLoader 类介绍**
ClassLoader类，它是一个抽象类，其后所有的类加载器都继承自ClassLoader（不包括启动类加载器）
![](image/1663809188310-62fb78bb-3936-4780-9789-4d16d8ec3187.png)
sun.misc.Launcher 它是一个java虚拟机的入口应用
![](image/1663809191437-d0967aad-c990-4a0e-8fb7-aa4dcdddaae8.png)
**获取ClassLoader途径**
![](image/1663809194226-74401dee-f364-4a0c-9357-b975b98fe47a.png)
```java
public class ClassLoaderTest2 {
    public static void main(String[] args) {
        try {
            //1.
            ClassLoader classLoader = Class.forName("java.lang.String").getClassLoader();
            System.out.println(classLoader);
            //2.
            ClassLoader classLoader1 = Thread.currentThread().getContextClassLoader();
            System.out.println(classLoader1);

            //3.
            ClassLoader classLoader2 = ClassLoader.getSystemClassLoader().getParent();
            System.out.println(classLoader2);

        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}

```
## 5、双亲委派机制
### 原理
Java虚拟机对class文件采用的是**按需加载**的方式，也就是说当需要使用该类时才会将它的class文件加载到内存生成class对象。而且加载某个类的class文件时，Java虚拟机采用的是双亲委派模式，即把请求交由父类处理，它是一种任务委派模式

1. 如果一个类加载器收到了类加载请求，它并不会自己先去加载，而是把这个请求委托给父类的加载器去执行；
2. 如果父类加载器还存在其父类加载器，则进一步向上委托，依次递归，请求最终将到达顶层的启动类加载器；
3. 如果父类加载器可以完成类加载任务，就成功返回，倘若父类加载器无法完成此加载任务，子加载器才会尝试自己去加载，这就是双亲委派模式。
4. 父类加载器一层一层往下分配任务，如果子类加载器能加载，则加载此类，如果将加载任务分配至系统类加载器也无法加载此类，则抛出异常

![](image/1663809199129-352df6ad-69ea-4b1e-a7f0-79d3f8988ba2.png)
### 代码演示
#### 举例1
1、我们自己建立一个 java.lang.String 类，写上 static 代码块
```java
public class String {
    static{
        System.out.println("我是自定义的String类的静态代码块");
    }
}
```
2、在另外的程序中加载 String 类，看看加载的 String 类是 JDK 自带的 String 类，还是我们自己编写的 String 类
```java
public class StringTest {

    public static void main(String[] args) {
        java.lang.String str = new java.lang.String();
        System.out.println("hello,atguigu.com");

        StringTest test = new StringTest();
        System.out.println(test.getClass().getClassLoader());
    }
}
```
输出结果：
hello,atguigu.com
sun.misc.Launcher$AppClassLoader@18b4aac2

程序并没有输出我们静态代码块中的内容，可见仍然加载的是 JDK 自带的 String 类。
把刚刚的类改一下
```java
package java.lang;
public class String {
    //
    static{
        System.out.println("我是自定义的String类的静态代码块");
    }
    //错误: 在类 java.lang.String 中找不到 main 方法
    public static void main(String[] args) {
        System.out.println("hello,String");
    }
}
```
![](image/1663809206482-25ed073a-98a7-4c1a-b716-427d86f9bda7.png)
由于双亲委派机制一直找父类，所以最后找到了Bootstrap ClassLoader，Bootstrap ClassLoader找到的是 JDK 自带的 String 类，在那个String类中并没有 main() 方法，所以就报了上面的错误。
#### 举例2
```java
package java.lang;

public class ShkStart {
    public static void main(String[] args) {
        System.out.println("hello!");
    }
}
```
输出异常结果：
java.lang.SecurityException: Prohibited package name: java.lang
> 即使类名没有重复，也禁止使用java.lang这种包名。这是一种保护机制

#### 举例3
当我们加载jdbc.jar 用于实现数据库连接的时候

1. 我们现在程序中需要用到SPI接口，而SPI接口属于rt.jar包中Java核心api
2. 然后使用双清委派机制，引导类加载器把rt.jar包加载进来，而rt.jar包中的SPI存在一些接口，接口我们就需要具体的实现类了
3. 具体的实现类就涉及到了某些第三方的jar包了，比如我们加载SPI的实现类jdbc.jar包【首先我们需要知道的是 jdbc.jar是基于SPI接口进行实现的】
4. 第三方的jar包中的类属于系统类加载器来加载
5. 从这里面就可以看到SPI核心接口由引导类加载器来加载，SPI具体实现类由系统类加载器来加载

![](image/1663809208545-c0d4f1b7-ac43-485b-b19a-6e2f19c78a05.png)
### 优势
通过上面的例子，我们可以知道，双亲机制可以

1. 避免类的重复加载
2. 保护程序安全，防止核心API被随意篡改
   - 自定义类：自定义java.lang.String 没有被加载。
   - 自定义类：java.lang.ShkStart（报错：阻止创建 java.lang开头的类）
### 沙箱安全机制

1. 自定义String类时：在加载自定义String类的时候会率先使用引导类加载器加载，而引导类加载器在加载的过程中会先加载jdk自带的文件（rt.jar包中java.lang.String.class），报错信息说没有main方法，就是因为加载的是rt.jar包中的String类。
2. 这样可以保证对java核心源代码的保护，这就是沙箱安全机制。
## 6、其他
### 判断两个class对象是否相同
在JVM中表示两个class对象是否为同一个类存在两个必要条件：

1. 类的完整类名必须一致，包括包名
2. **加载这个类的ClassLoader（指ClassLoader实例对象）必须相同**
3. 换句话说，在JVM中，即使这两个类对象（class对象）来源同一个Class文件，被同一个虚拟机所加载，但只要加载它们的ClassLoader实例对象不同，那么这两个类对象也是不相等的
### 加载器的引用

1. JVM必须知道一个类型是由启动加载器加载的还是由用户类加载器加载的
2. **如果一个类型是由用户类加载器加载的，那么JVM会将这个类加载器的一个引用作为类型信息的一部分保存在方法区中**
3. 当解析一个类型到另一个类型的引用的时候，JVM需要保证这两个类型的类加载器是相同的（后面讲）

# 三、 运行时数据区概述及线程
## 1、前言
本节主要讲的是运行时数据区，也就是下图这部分，它是在类加载完成后的阶段
![](image/1663897877611-20f4e594-8976-4413-a759-8eaf5666ab19.png)
当我们通过前面的：类的加载 --> 验证 --> 准备 --> 解析 --> 初始化，这几个阶段完成后，就会用到执行引擎对我们的类进行使用，同时执行引擎将会使用到我们运行时数据区
![](image/1663897877451-798829cb-b05c-4512-aa67-a3103a287602.png)
类比一下也就是大厨做饭，我们把大厨后面的东西（切好的菜，刀，调料），比作是运行时数据区。而厨师可以类比于执行引擎，将通过准备的东西进行制作成精美的菜品。
![](image/1663897877364-9af6058a-fd5d-418f-8e6d-5834ce92fdea.png)
## 2、结构
### 运行时数据区与内存

1. 内存是非常重要的系统资源，是硬盘和CPU的中间仓库及桥梁，承载着操作系统和应用程序的实时运行。JVM内存布局规定了Java在运行过程中内存申请、分配、管理的策略，保证了JVM的高效稳定运行。**不同的JVM对于内存的划分方式和管理机制存在着部分差异**。结合JVM虚拟机规范，来探讨一下经典的JVM内存布局。
2. 我们通过磁盘或者网络IO得到的数据，都需要先加载到内存中，然后CPU从内存中获取数据进行读取，也就是说内存充当了CPU和磁盘之间的桥梁

下图来自阿里巴巴手册JDK8
[![](https://cdn.nlark.com/yuque/0/2022/jpeg/26368762/1663897877384-bc120808-7590-4a26-b60f-3b4892a521ac.jpeg#clientId=u5d44e548-f845-4&crop=0&crop=0&crop=1&crop=1&from=paste&id=u14fb8489&margin=%5Bobject%20Object%5D&originHeight=576&originWidth=1215&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u14a41f41-f4a3-45ab-9482-3657eb33f9c&title=)](https://camo.githubusercontent.com/70afcba8a93e640fa141d02d45f60857ccbae61b46d3d1db7dbc20b2b5c4f8de/68747470733a2f2f6e706d2e656c656d6563646e2e636f6d2f796f7574686c716c40312e302e382f4a564d2f636861707465725f3030332f303030342e6a7067)
### 线程的内存空间

1. Java虚拟机定义了若干种程序运行期间会使用到的运行时数据区：其中有一些会随着虚拟机启动而创建，随着虚拟机退出而销毁。另外一些则是与线程一一对应的，这些与线程对应的数据区域会随着线程开始和结束而创建和销毁。
2. 灰色的为单独线程私有的，红色的为多个线程共享的。即：
   - 线程独有：独立包括程序计数器、栈、本地方法栈
   - 线程间共享：堆、堆外内存（永久代或元空间、代码缓存）

![](image/1663897877537-bfa9485b-b39a-4b9e-9609-b0eebddd495f.png)
### Runtime类
**每个JVM只有一个Runtime实例**。即为运行时环境，相当于内存结构的中间的那个框框：运行时环境。
![](image/1663897878278-8d501033-d410-4f07-93e2-e7ea1b139e34.png)
## 3、线程
#### JVM 线程

1. 线程是一个程序里的运行单元。JVM允许一个应用有多个线程并行的执行
2. **在Hotspot JVM里，每个线程都与操作系统的本地线程直接映射**
   - 当一个Java线程准备好执行以后，此时一个操作系统的本地线程也同时创建。Java线程执行终止后，本地线程也会回收
3. 操作系统负责将线程安排调度到任何一个可用的CPU上。一旦本地线程初始化成功，它就会调用Java线程中的run()方法

关于线程，并发可以看笔者的Java并发系列
#### JVM 系统线程

- 如果你使用jconsole或者是任何一个调试工具，都能看到在后台有许多线程在运行。这些后台线程不包括调用public static void main(String[])的main线程以及所有这个main线程自己创建的线程。
- 这些主要的后台系统线程在Hotspot JVM里主要是以下几个：
1. **虚拟机线程**：这种线程的操作是需要JVM达到安全点才会出现。这些操作必须在不同的线程中发生的原因是他们都需要JVM达到安全点，这样堆才不会变化。这种线程的执行类型括"stop-the-world"的垃圾收集，线程栈收集，线程挂起以及偏向锁撤销
2. **周期任务线程**：这种线程是时间周期事件的体现（比如中断），他们一般用于周期性操作的调度执行
3. **GC线程**：这种线程对在JVM里不同种类的垃圾收集行为提供了支持
4. **编译线程**：这种线程在运行时会将字节码编译成到本地代码
5. **信号调度线程**：这种线程接收信号并发送给JVM，在它内部通过调用适当的方法进行处理
# 四、 程序计数器(PC寄存器)
## 1、介绍
官方文档网址：[https://docs.oracle.com/javase/specs/jvms/se8/html/index.html](https://docs.oracle.com/javase/specs/jvms/se8/html/index.html)
![](image/1663897878524-8bce2eb0-4f96-4074-8a9e-4a8a53fa86b2.png)

1. JVM中的程序计数寄存器（Program Counter Register）中，Register的命名源于CPU的寄存器，**寄存器存储指令相关的现场信息**。CPU只有把数据装载到寄存器才能够运行。
2. 这里，并非是广义上所指的物理寄存器，或许将其翻译为PC计数器（或指令计数器）会更加贴切（也称为程序钩子），并且也不容易引起一些不必要的误会。**JVM中的PC寄存器是对物理PC寄存器的一种抽象模拟**。
3. 它是一块很小的内存空间，几乎可以忽略不记。也是运行速度最快的存储区域。
4. 在JVM规范中，每个线程都有它自己的程序计数器，是线程私有的，生命周期与线程的生命周期保持一致。
5. 任何时间一个线程都只有一个方法在执行，也就是所谓的**当前方法**。程序计数器会存储当前线程正在执行的Java方法的JVM指令地址；或者，如果是在执行native方法，则是未指定值（undefned）。
6. 它是**程序控制流**的指示器，分支、循环、跳转、异常处理、线程恢复等基础功能都需要依赖这个计数器来完成。
7. 字节码解释器工作时就是通过改变这个计数器的值来选取下一条需要执行的字节码指令。
8. 它是**唯一一个**在Java虚拟机规范中没有规定任何OutofMemoryError情况的区域。
## 2、作用
PC寄存器用来存储指向下一条指令的地址，也即将要执行的指令代码。由执行引擎读取下一条指令，并执行该指令。
![](image/1663897878595-66c93bcb-fdee-426a-ab38-2af02a3023c5.png)
## 3、举例说明
左边的数字代表**指令地址（指令偏移）**，即 PC 寄存器中可能存储的值，然后执行引擎读取 PC 寄存器中的值，并执行该指令
![](image/1663897879492-fb8771e4-48e6-4acd-b72a-ff94b1430b40.png)
## 4、两个面试题
**使用PC寄存器存储字节码指令地址有什么用呢？或者问为什么使用 PC 寄存器来记录当前线程的执行地址呢？**

1. 因为CPU需要不停的切换各个线程，这时候切换回来以后，就得知道接着从哪开始继续执行
2. JVM的字节码解释器就需要通过改变PC寄存器的值来明确下一条应该执行什么样的字节码指令

![](image/1663897882757-bd14d813-5b5a-4aff-9804-454a37c2ec16.png)
**PC寄存器为什么被设定为私有的？**

1. 我们都知道所谓的多线程在一个特定的时间段内只会执行其中某一个线程的方法，CPU会不停地做任务切换，这样必然导致经常中断或恢复，如何保证分毫无差呢？**为了能够准确地记录各个线程正在执行的当前字节码指令地址，最好的办法自然是为每一个线程都分配一个PC寄存器**，这样一来各个线程之间便可以进行独立计算，从而不会出现相互干扰的情况。
2. 由于CPU时间片轮限制，众多线程在并发执行过程中，任何一个确定的时刻，一个处理器或者多核处理器中的一个内核，只会执行某个线程中的一条指令。
3. 这样必然导致经常中断或恢复，如何保证分毫无差呢？每个线程在创建后，都会产生自己的程序计数器和栈帧，程序计数器在各个线程之间互不影响。

注意并行和并发的区别，笔者的并发系列有讲
## 5、CPU 时间片

1. CPU时间片即CPU分配给各个程序的时间，每个线程被分配一个时间段，称作它的时间片。
2. 在宏观上：我们可以同时打开多个应用程序，每个程序并行不悖，同时运行。
3. 但在微观上：由于只有一个CPU，一次只能处理程序要求的一部分，如何处理公平，一种方法就是引入时间片，**每个程序轮流执行**。

![](image/1663897885343-7a88397c-68c0-4cf6-aa1c-db63e5706e00.png)
# 五、 虚拟机栈
## 1、简介
### 虚拟机栈的出现背景

1. 由于跨平台性的设计，Java的指令都是根据栈来设计的。不同平台CPU架构不同，所以不能设计为基于寄存器的【如果设计成基于寄存器的，耦合度高，性能会有所提升，因为可以对具体的CPU架构进行优化，但是跨平台性大大降低】。
2. 优点是跨平台，指令集小，编译器容易实现，缺点是性能下降，实现同样的功能需要更多的指令。
### 内存中的栈与堆

1. 首先栈是运行时的单位，而堆是存储的单位。
2. 即：栈解决程序的运行问题，即程序如何执行，或者说如何处理数据。堆解决的是数据存储的问题，即数据怎么放，放哪里

![](image/1663899341179-afea2d8a-7efe-4078-bbc5-bc00ee573de8.png)
### 虚拟机栈基本内容

- Java虚拟机栈是什么？
   - Java虚拟机栈（Java Virtual Machine Stack），早期也叫Java栈。每个线程在创建时都会创建一个虚拟机栈，其内部保存一个个的栈帧（Stack Frame），**对应着一次次的Java方法调用**，栈是线程私有的

![](https://cdn.nlark.com/yuque/0/2022/png/26368762/1663899344506-bd9fb08e-37f7-4703-b791-f6ce4d970cac.png#clientId=u5d44e548-f845-4&crop=0&crop=0&crop=1&crop=1&from=paste&id=u676695e9&margin=%5Bobject%20Object%5D&originHeight=650&originWidth=978&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=uffb5ea33-a622-4f08-8999-36d4e02d5f8&title=)

- 虚拟机栈的生命周期
   - 生命周期和线程一致，也就是线程结束了，该虚拟机栈也销毁了
- 虚拟机栈的作用
   - 主管Java程序的运行，它保存方法的局部变量（8 种基本数据类型、对象的引用地址）、部分结果，并参与方法的调用和返回。
   - 局部变量，它是相比于成员变量来说的（或属性）
   - 基本数据类型变量 VS 引用类型变量（类、数组、接口）
### 虚拟机栈的特点

- 栈是一种快速有效的分配存储方式，访问速度仅次于程序计数器。
- JVM直接对Java栈的操作只有两个：
   - 每个方法执行，伴随着**进栈**（入栈、压栈）
   - 执行结束后的**出栈**工作
- 对于栈来说不存在垃圾回收问题
   - 栈不需要GC，但是可能存在OOM

![](image/1663899341295-1374fbaf-dabb-47a4-afe2-cf4810d83e0c.png)
### 虚拟机栈的异常
**面试题：栈中可能出现的异常？**

- Java 虚拟机规范允许Java栈的大小是动态的或者是固定不变的。
   - 如果采用固定大小的Java虚拟机栈，那每一个线程的Java虚拟机栈容量可以在线程创建的时候独立选定。如果线程请求分配的栈容量超过Java虚拟机栈允许的最大容量，Java虚拟机将会抛出一个**StackoverflowError** 异常。
   - 如果Java虚拟机栈可以动态扩展，并且在尝试扩展的时候无法申请到足够的内存，或者在创建新的线程时没有足够的内存去创建对应的虚拟机栈，那Java虚拟机将会抛出一个 **OutofMemoryError** 异常。
### 设置栈内存大小
官方文档：[https://docs.oracle.com/en/java/javase/11/tools/java.html#GUID-3B1CE181-CD30-4178-9602-230B800D4FAE](https://docs.oracle.com/en/java/javase/11/tools/java.html#GUID-3B1CE181-CD30-4178-9602-230B800D4FAE)
我们可以使用参数 **-Xss** 选项来设置线程的最大栈空间，栈的大小直接决定了函数调用的最大可达深度。
Sets the thread stack size (in bytes). Append the letter k or K to indicate KB, m or M to indicate MB, and g or G to indicate GB. The default value depends on the platform:

- Linux/x64 (64-bit): 1024 KB
- macOS (64-bit): 1024 KB
- Oracle Solaris/x64 (64-bit): 1024 KB
- Windows: The default value depends on virtual memory

The following examples set the thread stack size to 1024 KB in different units:
-Xss1m -Xss1024k -Xss1048576

## 2、原理与结构
### 栈中存储单位

1. 每个线程都有自己的栈，栈中的数据都是以**栈帧**（Stack Frame）的格式存在
2. 在这个线程上正在执行的每个方法都各自对应一个栈帧（Stack Frame）。
3. 栈帧是一个内存区块，是一个数据集，维系着方法执行过程中的各种数据信息。
### 栈运行原理

1. JVM直接对Java栈的操作只有两个，就是对栈帧的**压栈和出栈**，遵循先进后出（后进先出）原则
2. 在一条活动线程中，一个时间点上，只会有一个活动的栈帧。即只有当前正在执行的方法的栈帧（栈顶栈帧）是有效的。这个栈帧被称为**当前栈帧（Current Frame）**，与当前栈帧相对应的方法就是**当前方法（Current Method）**，定义这个方法的类就是**当前类（Current Class）**
3. 执行引擎运行的所有字节码指令只针对当前栈帧进行操作。
4. 如果在该方法中调用了其他方法，对应的新的栈帧会被创建出来，放在栈的顶端，成为新的当前帧。

![](image/1663899341295-3508a98a-0acc-4abf-bde8-ae47fe1e8247.png)

1. **不同线程中所包含的栈帧是不允许存在相互引用的**，即不可能在一个栈帧之中引用另外一个线程的栈帧。
2. 如果当前方法调用了其他方法，方法返回之际，当前栈帧会传回此方法的执行结果给前一个栈帧，接着，虚拟机会丢弃当前栈帧，使得前一个栈帧重新成为当前栈帧。
3. Java方法有两种返回函数的方式。
   - 一种是正常的函数返回，使用return指令。
   - 另一种是方法执行中出现未捕获处理的异常，以抛出异常的方式结束。
   - 但不管使用哪种方式，都会导致栈帧被弹出。
### 内部结构
每个栈帧中存储着：

- 局部变量表（Local Variables）
- 操作数栈（Operand Stack）（或表达式栈）
- 动态链接（Dynamic Linking）（或指向运行时常量池的方法引用）
- 方法返回地址（Return Address）（或方法正常退出或者异常退出的定义）
- 一些附加信息

![](image/1663899341925-769b98b3-e660-446c-898a-687812986e04.png)
并行每个线程下的栈都是私有的，因此每个线程都有自己各自的栈，并且每个栈里面都有很多栈帧，栈帧的大小主要由局部变量表 和 操作数栈决定的
![](image/1663899342104-d094ad56-59e8-4009-b314-b6a6cab7ced9.png)
## 3、局部变量表
### 认识局部变量表

1. 局部变量表也被称之为局部变量数组或本地变量表
2. **定义为一个数字数组，主要用于存储方法参数和定义在方法体内的局部变量**，这些数据类型包括各类基本数据类型、对象引用（reference），以及returnAddress返回值类型。
3. 由于局部变量表是建立在线程的栈上，是线程的私有数据，因此**不存在数据安全问题**
4. **局部变量表所需的容量大小是在编译期确定下来的**，并保存在方法的Code属性的**maximum local variables**数据项中。在方法运行期间是不会改变局部变量表的大小的。
5. 方法嵌套调用的次数由栈的大小决定。一般来说，栈越大，方法嵌套调用次数越多。
   - 对一个函数而言，它的参数和局部变量越多，使得局部变量表膨胀，它的栈帧就越大，以满足方法调用所需传递的信息增大的需求。
   - 进而函数调用就会占用更多的栈空间，导致其嵌套调用次数就会减少。
6. 局部变量表中的变量只在当前方法调用中有效。
   - 在方法执行时，虚拟机通过使用局部变量表完成参数值到参数变量列表的传递过程。
   - 当方法调用结束后，随着方法栈帧的销毁，局部变量表也会随之销毁。

![](image/1663899342707-37cd3784-cf05-4d7e-b1d8-9e5487ffe5b4.png)
看完字节码后，可得结论：所以局部变量表所需的容量大小是在编译期确定下来的。
### Slot的理解

1. 参数值的存放总是从局部变量数组索引 0 的位置开始，到数组长度-1的索引结束。
2. 局部变量表，**最基本的存储单元是Slot（变量槽）**，局部变量表中存放编译期可知的各种基本数据类型（8种），引用类型（reference），returnAddress类型的变量。
3. 在局部变量表里，**32位以内的类型只占用一个slot**（包括returnAddress类型），**64位的类型占用两个slot**（long和double）。
   - byte、short、char在储存前被转换为int，boolean也被转换为int，0表示false，非0表示true
   - long和double则占据两个slot
4. JVM会为局部变量表中的每一个Slot都分配一个访问索引，通过这个索引即可成功访问到局部变量表中指定的局部变量值
5. 当一个实例方法被调用的时候，它的方法参数和方法体内部定义的局部变量将会**按照顺序被复制**到局部变量表中的每一个slot上
6. 如果需要访问局部变量表中一个64bit的局部变量值时，只需要使用前一个索引即可。（比如：访问long或double类型变量）
7. 如果当前帧是由构造方法或者实例方法创建的，那么**该对象引用this将会存放在index为0的slot处**，其余的参数按照参数表顺序继续排列。（this也相当于一个变量）

![](image/1663899343802-366af194-85ac-4e57-b5d4-1a22dce8b760.png)
**Slot的重复利用**
栈帧中的局部变量表中的槽位是可以重用的，如果一个局部变量过了其作用域，那么在其作用域之后申明新的局部变量变就很有可能会复用过期局部变量的槽位，从而达到节省资源的目的。
```java
    public void test4() {
        int a = 0;
        {
            int b = 0;
            b = a + 1;
        }
        //变量c使用之前已经销毁的变量b占据的slot的位置
        int c = a + 1;
    }
```
局部变量 c 重用了局部变量 b 的 slot 位置
![](image/1663899344678-fdfb39e2-d36f-4f13-8c5b-0eb8cccdee32.png)
### 静态变量与局部变量的对比
```bash
变量的分类：
1、按照数据类型分：① 基本数据类型  ② 引用数据类型
2、按照在类中声明的位置分：
  2-1、成员变量：在使用前，都经历过默认初始化赋值
       2-1-1、类变量: linking的prepare阶段：给类变量默认赋值
              ---> initial阶段：给类变量显式赋值即静态代码块赋值
       2-1-2、实例变量：随着对象的创建，会在堆空间中分配实例变量空间，并进行默认赋值
  2-2、局部变量：在使用前，必须要进行显式赋值的！否则，编译不通过。
```

1. 参数表分配完毕之后，再根据方法体内定义的变量的顺序和作用域分配。
2. 我们知道成员变量有两次初始化的机会**，**第一次是在“准备阶段”，执行系统初始化，对类变量设置零值，另一次则是在“初始化”阶段，赋予程序员在代码中定义的初始值。
3. 和类变量初始化不同的是，**局部变量表不存在系统初始化的过程**，这意味着一旦定义了局部变量则必须人为的初始化，否则无法使用。
### 补充说明

1. 在栈帧中，与性能调优关系最为密切的部分就是前面提到的局部变量表。在方法执行时，虚拟机使用局部变量表完成方法的传递。
2. 局部变量表中的变量也是重要的垃圾回收根节点，只要被局部变量表中直接或间接引用的对象都不会被回收。
## 4、操作数栈
### 特点

1. 每一个独立的栈帧除了包含局部变量表以外，还包含一个后进先出（Last - In - First -Out）的 操作数栈，也可以称之为**表达式栈**（Expression Stack）
2. 操作数栈，在方法执行过程中，**根据字节码指令，往栈中写入数据或提取数据**，即入栈（push）和 出栈（pop）
- 某些字节码指令将值压入操作数栈，其余的字节码指令将操作数取出栈。使用它们后再把结果压入栈，
- 比如：**执行复制、交换、求和等操作**

![](image/1663899345415-ef238420-8f76-4680-a8ef-cd108b1f8505.png)
![](image/1663899345437-6a6c77b5-a48d-468a-be00-f9ed04187f69.png)
### 作用

1. 操作数栈，**主要用于保存计算过程的中间结果，同时作为计算过程中变量临时的存储空间**。
2. 操作数栈就是JVM执行引擎的一个工作区，当一个方法刚开始执行的时候，一个新的栈帧也会随之被创建出来，这时方法的操作数栈是空的。
3. 每一个操作数栈都会拥有一个明确的栈深度用于存储数值，其所需的最大深度在编译期就定义好了，保存在方法的Code属性中，为**maxstack**的值。
4. 栈中的任何一个元素都是可以任意的Java数据类型
   - 32bit的类型占用一个栈单位深度
   - 64bit的类型占用两个栈单位深度
5. 操作数栈并非采用访问索引的方式来进行数据访问的，而是只能通过标准的入栈和出栈操作来完成一次数据访问。**只不过操作数栈是用数组这个结构来实现的而已**
6. 如果被调用的方法带有返回值的话，其返回值将会被压入当前栈帧的操作数栈中，并更新PC寄存器中下一条需要执行的字节码指令。
7. 操作数栈中元素的数据类型必须与字节码指令的序列严格匹配，这由编译器在编译器期间进行验证，同时在类加载过程中的类检验阶段的数据流分析阶段要再次验证。
8. 另外，**我们说Java虚拟机的解释引擎是基于栈的执行引擎，其中的栈指的就是操作数栈**。

[![](https://cdn.nlark.com/yuque/0/2022/jpeg/26368762/1663899345563-519e4629-e207-40ca-90da-34d9384adea8.jpeg#clientId=u5d44e548-f845-4&crop=0&crop=0&crop=1&crop=1&from=paste&id=u59f5728a&margin=%5Bobject%20Object%5D&originHeight=773&originWidth=1291&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u52825602-1fed-45ec-9faf-7cc6e13478b&title=)](https://camo.githubusercontent.com/1b85a4e4383fa6697c136ca34fbb59a86a2dacb445d361bff1282c98433ef832/68747470733a2f2f6e706d2e656c656d6563646e2e636f6d2f796f7574686c716c40312e302e382f4a564d2f636861707465725f3030342f303032302e6a7067)
局部变量表就相当于食材
操作数栈就相当于做法步骤
### 代码追踪
	public void testAddOperation() {         //byte、short、char、boolean：都以int型来保存         byte i = 15;         int j = 8;         int k = i + j;        // int m = 800;     }
对应字节码指令
 0 bipush 15  2 istore_1  3 bipush 8  5 istore_2  6 iload_1  7 iload_2  8 iadd  9 istore_3 10 return
![](image/1663899345578-425caa30-2580-4303-af73-d97a8c8a00e9.png)
### 一步一步看流程
1、首先执行第一条语句，PC寄存器指向的是0，也就是指令地址为0，然后使用bipush让操作数15入操作数栈。
![](image/1663899346123-5e0cf04f-5bd6-42e1-a757-bf453354c94c.png)
2、执行完后，PC寄存器往下移，指向下一行代码，下一行代码就是将操作数栈的元素存储到局部变量表1的位置（istore_1），我们可以看到局部变量表的已经增加了一个元素。并且操作数栈为空了

- 解释为什么局部变量表索引从 1 开始，因为该方法为实例方法，局部变量表索引为 0 的位置存放的是 this

![](image/1663899346450-f7deffe6-e9fd-4f5d-a4c2-d110d9083bf2.png)
3、然后PC下移，指向的是下一行。让操作数8也入栈，同时执行store操作，存入局部变量表中
![](image/1663899349528-97e344dd-ca9a-4a63-9896-e8d9b2d394c9.png)
4、然后从局部变量表中，依次将数据放在操作数栈中，等待执行 add 操作
iload_1：取出局部变量表中索引为1的数据入操作数栈
![](image/1663899346624-3eee0fe0-1d5c-4808-ba76-6edf26bd238d.png)
5、然后将操作数栈中的两个元素执行相加操作，并存储在局部变量表3的位置
![](image/1663899347159-e7ce1c85-3a9a-4875-bdcc-37b646eebce1.png)
### **类型转换**
![](image/1663899348389-b667ded2-3399-4965-8b08-4ccd18aa4990.png)

- 因为 8 可以存放在 byte 类型中，所以压入操作数栈的类型为 byte ，而不是 int ，所以执行的字节码指令为 bipush 8
- 但是存储在局部变量的时候，会转成 int 类型的变量：istore_4
- m改成800之后，byte存储不了，就成了short型，sipush 800

**如果被调用的方法带有返回值，返回值入操作数栈**
getSum() 方法字节码指令：最后带着个 ireturn
![](image/1663899349053-db9f423c-6a61-4174-aa7d-e715152a75b9.png)
testGetSum() 方法字节码指令：一上来就加载 getSum() 方法的返回值()
![](image/1663899350058-e5402796-1215-4037-9fb8-4bacb125d9ea.png)
## 5、栈顶缓存技术
**栈顶缓存技术：Top Of Stack Cashing**

1. 前面提过，基于栈式架构的虚拟机所使用的零地址指令更加紧凑，但完成一项操作的时候必然需要使用更多的入栈和出栈指令，这同时也就意味着将需要更多的指令分派（instruction dispatch）次数（也就是你会发现指令很多）和导致内存读/写次数多，效率不高。
2. 由于操作数是存储在内存中的，因此频繁地执行内存读/写操作必然会影响执行速度。为了解决这个问题，HotSpot JVM的设计者们提出了栈顶缓存（Tos，Top-of-Stack Cashing）技术，**将栈顶元素全部缓存在物理CPU的寄存器中，以此降低对内存的读/写次数，提升执行引擎的执行效率。**
3. 寄存器的主要优点：指令更少，执行速度快，但是指令集（也就是指令种类）很多
## 6、动态链接
**动态链接（或指向运行时常量池的方法引用）**

1. 每一个栈帧内部都包含**一个指向运行时常量池中该栈帧所属方法的引用**。包含这个引用的目的就是**为了支持当前方法的代码能够实现动态链接**（Dynamic Linking），比如：invokedynamic指令
2. 在Java源文件被编译到字节码文件中时，所有的变量和方法引用都作为符号引用（Symbolic Reference）保存在class文件的常量池里。比如：描述一个方法调用了另外的其他方法时，就是通过常量池中指向方法的符号引用来表示的，那么**动态链接的作用就是为了将这些符号引用转换为调用方法的直接引用**
```java
public class DynamicLinkingTest {

    int num = 10;

    public void methodA(){
        System.out.println("methodA()....");
    }

    public void methodB(){
        System.out.println("methodB()....");

        methodA();

        num++;
    }

}
```
对应字节码
```bash
Classfile /F:/IDEAWorkSpaceSourceCode/JVMDemo/out/production/chapter05/com/atguigu/java1/DynamicLinkingTest.class
  Last modified 2020-11-10; size 712 bytes
  MD5 checksum e56913c945f897c7ee6c0a608629bca8
  Compiled from "DynamicLinkingTest.java"
public class com.atguigu.java1.DynamicLinkingTest
  minor version: 0
  major version: 52
  flags: ACC_PUBLIC, ACC_SUPER
Constant pool:
   #1 = Methodref          #9.#23         // java/lang/Object."<init>":()V
   #2 = Fieldref           #8.#24         // com/atguigu/java1/DynamicLinkingTest.num:I
   #3 = Fieldref           #25.#26        // java/lang/System.out:Ljava/io/PrintStream;
   #4 = String             #27            // methodA()....
   #5 = Methodref          #28.#29        // java/io/PrintStream.println:(Ljava/lang/String;)V
   #6 = String             #30            // methodB()....
   #7 = Methodref          #8.#31         // com/atguigu/java1/DynamicLinkingTest.methodA:()V
   #8 = Class              #32            // com/atguigu/java1/DynamicLinkingTest
   #9 = Class              #33            // java/lang/Object
  #10 = Utf8               num
  #11 = Utf8               I
  #12 = Utf8               <init>
  #13 = Utf8               ()V
  #14 = Utf8               Code
  #15 = Utf8               LineNumberTable
  #16 = Utf8               LocalVariableTable
  #17 = Utf8               this
  #18 = Utf8               Lcom/atguigu/java1/DynamicLinkingTest;
  #19 = Utf8               methodA
  #20 = Utf8               methodB
  #21 = Utf8               SourceFile
  #22 = Utf8               DynamicLinkingTest.java
  #23 = NameAndType        #12:#13        // "<init>":()V
  #24 = NameAndType        #10:#11        // num:I
  #25 = Class              #34            // java/lang/System
  #26 = NameAndType        #35:#36        // out:Ljava/io/PrintStream;
  #27 = Utf8               methodA()....
  #28 = Class              #37            // java/io/PrintStream
  #29 = NameAndType        #38:#39        // println:(Ljava/lang/String;)V
  #30 = Utf8               methodB()....
  #31 = NameAndType        #19:#13        // methodA:()V
  #32 = Utf8               com/atguigu/java1/DynamicLinkingTest
  #33 = Utf8               java/lang/Object
  #34 = Utf8               java/lang/System
  #35 = Utf8               out
  #36 = Utf8               Ljava/io/PrintStream;
  #37 = Utf8               java/io/PrintStream
  #38 = Utf8               println
  #39 = Utf8               (Ljava/lang/String;)V
{
  int num;
    descriptor: I
    flags:

  public com.atguigu.java1.DynamicLinkingTest();
    descriptor: ()V
    flags: ACC_PUBLIC
    Code:
      stack=2, locals=1, args_size=1
         0: aload_0
         1: invokespecial #1                  // Method java/lang/Object."<init>":()V
         4: aload_0
         5: bipush        10
         7: putfield      #2                  // Field num:I
        10: return
      LineNumberTable:
        line 7: 0
        line 9: 4
      LocalVariableTable:
        Start  Length  Slot  Name   Signature
            0      11     0  this   Lcom/atguigu/java1/DynamicLinkingTest;

  public void methodA();
    descriptor: ()V
    flags: ACC_PUBLIC
    Code:
      stack=2, locals=1, args_size=1
         0: getstatic     #3                  // Field java/lang/System.out:Ljava/io/PrintStream;
         3: ldc           #4                  // String methodA()....
         5: invokevirtual #5                  // Method java/io/PrintStream.println:(Ljava/lang/String;)V
         8: return
      LineNumberTable:
        line 12: 0
        line 13: 8
      LocalVariableTable:
        Start  Length  Slot  Name   Signature
            0       9     0  this   Lcom/atguigu/java1/DynamicLinkingTest;

  public void methodB();
    descriptor: ()V
    flags: ACC_PUBLIC
    Code:
      stack=3, locals=1, args_size=1
         0: getstatic     #3                  // Field java/lang/System.out:Ljava/io/PrintStream;
         3: ldc           #6                  // String methodB()....
         5: invokevirtual #5                  // Method java/io/PrintStream.println:(Ljava/lang/String;)V
         8: aload_0
         9: invokevirtual #7                  // Method methodA:()V
        12: aload_0
        13: dup
        14: getfield      #2                  // Field num:I
        17: iconst_1
        18: iadd
        19: putfield      #2                  // Field num:I
        22: return
      LineNumberTable:
        line 16: 0
        line 18: 8
        line 20: 12
        line 21: 22
      LocalVariableTable:
        Start  Length  Slot  Name   Signature
            0      23     0  this   Lcom/atguigu/java1/DynamicLinkingTest;
}
SourceFile: "DynamicLinkingTest.java"
```
1、在字节码指令中，methodB() 方法中通过 invokevirtual #7 指令调用了方法 A
2、往上面翻，找到常量池的定义：#7 = Methodref #8.#31

- 先找 #8 ：
   - #8 = Class #32 ：去找 #32
   - #32 = Utf8 com/atguigu/java1/DynamicLinkingTest
   - 结论：通过 #8 我们找到了 DynamicLinkingTest 这个类
- 再来找 #31：
   - #31 = NameAndType #19:#13 ：去找 #19 和 #13
   - #19 = Utf8 methodA ：方法名为 methodA
   - #13 = Utf8 ()V ：方法没有形参，返回值为 void

3、结论：通过 #7 我们就能找到需要调用的 methodA() 方法，并进行调用
4、在上面，其实还有很多符号引用，比如 Object、System、PrintStream 等等
![](image/1663899350442-66809a85-6c68-4543-9306-d9cb1a6f47b9.png)
**为什么要用常量池呢？**

1. 因为在不同的方法，都可能调用常量或者方法，所以只需要存储一份即可，然后记录其引用即可，节省了空间。
2. 常量池的作用：就是为了提供一些符号和常量，便于指令的识别
## 7、方法的调用
### 静态链接与动态链接
在JVM中，将符号引用转换为调用方法的直接引用与方法的绑定机制相关

- **静态链接**：

当一个字节码文件被装载进JVM内部时，如果被调用的目标方法在编译期确定，且运行期保持不变时，这种情况下将调用方法的符号引用转换为直接引用的过程称之为静态链接

- **动态链接**：

如果被调用的方法在编译期无法被确定下来，也就是说，只能够在程序运行期将调用的方法的符号转换为直接引用，由于这种引用转换过程具备动态性，因此也被称之为动态链接。
### 早期绑定与晚期绑定
静态链接与动态链接针对的是方法。早期绑定和晚期绑定范围更广。早期绑定涵盖了静态链接，晚期绑定涵盖了动态链接。
静态链接和动态链接对应的方法的绑定机制为：早期绑定（Early Binding）和晚期绑定（Late Binding）。**绑定是一个字段、方法或者类在符号引用被替换为直接引用的过程**，这仅仅发生一次。

- **早期绑定**

早期绑定就是指被调用的目标方法如果在编译期可知，且运行期保持不变时，即可将这个方法与所属的类型进行绑定，这样一来，由于明确了被调用的目标方法究竟是哪一个，因此也就**可以使用静态链接的方式将符号引用转换为直接引用**。

- **晚期绑定**

如果被调用的方法在编译期无法被确定下来，**只能够在程序运行期根据实际的类型绑定相关的方法**，这种绑定方式也就被称之为晚期绑定。
```java
class Animal {

    public void eat() {
        System.out.println("动物进食");
    }
}

interface Huntable {
    void hunt();
}

class Dog extends Animal implements Huntable {
    @Override
    public void eat() {
        System.out.println("狗吃骨头");
    }

    @Override
    public void hunt() {
        System.out.println("捕食耗子，多管闲事");
    }
}

class Cat extends Animal implements Huntable {

    public Cat() {
        super();//表现为：早期绑定
    }

    public Cat(String name) {
        this();//表现为：早期绑定
    }

    @Override
    public void eat() {
        super.eat();//表现为：早期绑定
        System.out.println("猫吃鱼");
    }

    @Override
    public void hunt() {
        System.out.println("捕食耗子，天经地义");
    }
}

public class AnimalTest {
    public void showAnimal(Animal animal) {
        animal.eat();//表现为：晚期绑定
    }

    public void showHunt(Huntable h) {
        h.hunt();//表现为：晚期绑定
    }
}

```
invokevirtual 体现为晚期绑定
invokeinterface 也体现为晚期绑定
invokespecial 体现为早期绑定
### 多态与绑定

1. 随着高级语言的横空出世，类似于Java一样的基于面向对象的编程语言如今越来越多，尽管这类编程语言在语法风格上存在一定的差别，但是它们彼此之间始终保持着一个共性，那就是都支持封装、继承和多态等面向对象特性，既然这一类的编程语言具备多态特性，那么自然也就具备早期绑定和晚期绑定两种绑定方式。
2. Java中任何一个普通的方法其实都具备虚函数的特征，它们相当于C++语言中的虚函数（C++中则需要使用关键字virtual来显式定义）。如果在Java程序中不希望某个方法拥有虚函数的特征时，则可以使用关键字final来标记这个方法。

**虚方法与非虚方法的区别**

1. 如果方法在编译期就确定了具体的调用版本，这个版本在运行时是不可变的。这样的方法称为非虚方法。
2. 静态方法、私有方法、final方法、实例构造器、父类方法都是非虚方法。
3. 其他方法称为虚方法。

**子类对象的多态的使用前提：**

1. 类的继承关系
2. 方法的重写
### 调用方法指令

- **普通指令：**
1. invokestatic：调用静态方法，解析阶段确定唯一方法版本
2. invokespecial：调用<init>方法、私有及父类方法，解析阶段确定唯一方法版本
3. invokevirtual：调用所有虚方法
4. invokeinterface：调用接口方法
- **动态调用指令**

invokedynamic：动态解析出需要调用的方法，然后执行
> 前四条指令固化在虚拟机内部，方法的调用执行不可人为干预。而invokedynamic指令则支持由用户确定方法版本。其中invokestatic指令和invokespecial指令调用的方法称为非虚方法，其余的（final修饰的除外）称为虚方法。


### invokedynamic 指令

1. JVM字节码指令集一直比较稳定，一直到Java7中才增加了一个invokedynamic指令，这是Java为了实现【动态类型语言】支持而做的一种改进。
2. 但是在Java7中并没有提供直接生成invokedynamic指令的方法，需要借助ASM这种底层字节码工具来产生invokedynamic指令。直到Java8的Lambda表达式的出现，invokedynamic指令的生成，在Java中才有了直接的生成方式。
3. Java7中增加的动态语言类型支持的本质是对Java虚拟机规范的修改，而不是对Java语言规则的修改，这一块相对来讲比较复杂，增加了虚拟机中的方法调用，最直接的受益者就是运行在Java平台的动态语言的编译器。
```java
@FunctionalInterface
interface Func {
    public boolean func(String str);
}

public class Lambda {
    public void lambda(Func func) {
        return;
    }

    public static void main(String[] args) {
        Lambda lambda = new Lambda();

        Func func = s -> {
            return true;
        };

        lambda.lambda(func);

        lambda.lambda(s -> {
            return true;
        });
    }
}
```
![](image/1663899351808-17a1642c-c147-4ab6-b95b-5a292a866e5d.png)
动态语言和静态语言

1. 动态类型语言和静态类型语言两者的区别就在于**对类型的检查是在编译期还是在运行期**，满足前者就是静态类型语言，反之是动态类型语言。
2. 说的再直白一点就是，静态类型语言是判断变量自身的类型信息；动态类型语言是判断变量值的类型信息，变量没有类型信息，变量值才有类型信息，这是动态语言的一个重要特征。

Java：String info = "mogu blog"; (Java是静态类型语言的，会先编译就进行类型检查) JS：var name = "shkstart"; var name = 10; （运行时才进行检查）
Python: info = 130.5 (运行时才检查) 
### 重写的本质

1. 找到操作数栈顶的第一个元素所执行的对象的实际类型，记作C。
2. 如果在类型C中找到与常量中的描述符合简单名称都相符的方法，则进行访问权限校验。
   - 如果通过则返回这个方法的直接引用，查找过程结束
   - 如果不通过，则返回java.lang.IllegalAccessError 异常
3. 否则，按照继承关系从下往上依次对C的各个父类进行第2步的搜索和验证过程。
4. 如果始终没有找到合适的方法，则抛出java.lang.AbstractMethodError异常。

上面这个过程称为**动态分派**
**IllegalAccessError介绍**

1. 程序试图访问或修改一个属性或调用一个方法，这个属性或方法，你没有权限访问。一般的，这个会引起编译器异常。这个错误如果发生在运行时，就说明一个类发生了不兼容的改变。
2. 比如，你把应该有的jar包放从工程中拿走了，或者Maven中存在jar包冲突
### 虚方法表

1. 在面向对象的编程中，会很频繁的使用到**动态分派**，如果在每次动态分派的过程中都要重新在类的方法元数据中搜索合适的目标的话就可能影响到执行效率。因此，为了提高性能，**JVM采用在类的方法区建立一个虚方法表（virtual method table）来实现**，非虚方法不会出现在表中。使用索引表来代替查找。【上面动态分派的过程，我们可以看到如果子类找不到，还要从下往上找其父类，非常耗时】
2. 每个类中都有一个虚方法表，表中存放着各个方法的实际入口。
3. 虚方法表是什么时候被创建的呢？虚方法表会在类加载的链接阶段被创建并开始初始化，类的变量初始值准备完成之后，JVM会把该类的虚方法表也初始化完毕。

**例子1**
如图所示：如果类中重写了方法，那么调用的时候，就会直接在该类的虚方法表中查找
![](image/1663899351940-406583eb-1a2d-46bd-b67d-e353f0fa3227.png)
1、比如说son在调用toString的时候，Son没有重写过，Son的父类Father也没有重写过，那就直接调用Object类的toString。那么就直接在虚方法表里指明toString直接指向Object类。
2、下次Son对象再调用toString就直接去找Object，不用先找Son-->再找Father-->最后才到Object的这样的一个过程。
## 8、方法返回地址
![](image/1663899360652-2fdcff12-399c-4b98-8fcb-67115ee9a6fc.png)
在一些帖子里，方法返回地址、动态链接、一些附加信息 也叫做帧数据区

1. 存放调用该方法的pc寄存器的值。一个方法的结束，有两种方式：
   - 正常执行完成
   - 出现未处理的异常，非正常退出
2. 无论通过哪种方式退出，在方法退出后都返回到该方法被调用的位置。方法正常退出时，**调用者的pc计数器的值作为返回地址，即调用该方法的指令的下一条指令的地址**。而通过异常退出的，返回地址是要通过异常表来确定，栈帧中一般不会保存这部分信息。
3. 本质上，方法的退出就是当前栈帧出栈的过程。此时，需要恢复上层方法的局部变量表、操作数栈、将返回值压入调用者栈帧的操作数栈、设置PC寄存器值等，让调用者方法继续执行下去。
4. 正常完成出口和异常完成出口的区别在于：通过异常完成出口退出的不会给他的上层调用者产生任何的返回值。

**方法退出的两种方式**
当一个方法开始执行后，只有两种方式可以退出这个方法，
**正常退出：**

1. 执行引擎遇到任意一个方法返回的字节码指令（return），会有返回值传递给上层的方法调用者，简称**正常完成出口**；
2. 一个方法在正常调用完成之后，究竟需要使用哪一个返回指令，还需要根据方法返回值的实际数据类型而定。
3. 在字节码指令中，返回指令包含：
   - ireturn：当返回值是boolean，byte，char，short和int类型时使用
   - lreturn：Long类型
   - freturn：Float类型
   - dreturn：Double类型
   - areturn：引用类型
   - return：返回值类型为void的方法、实例初始化方法、类和接口的初始化方法

**异常退出：**

1. 在方法执行过程中遇到异常（Exception），并且这个异常没有在方法内进行处理，也就是只要在本方法的异常表中没有搜索到匹配的异常处理器，就会导致方法退出，简称**异常完成出口**。
2. 方法执行过程中，抛出异常时的异常处理，存储在一个异常处理表，方便在发生异常的时候找到处理异常的代码

![](image/1663899361671-78729627-4dcf-4b40-a93b-d41e61e7b4ac.png)
异常处理表：

- 反编译字节码文件，可得到 Exception table
- from ：字节码指令起始地址
- to ：字节码指令结束地址
- target ：出现异常跳转至地址为 11 的指令执行
- type ：捕获异常的类型

![](image/1663899362228-43a74fd1-eecd-495b-94b3-0c2a3b2dc803.png)
## 9、一些附加信息
栈帧中还允许携带与Java虚拟机实现相关的一些附加信息。例如：对程序调试提供支持的信息。
## 10、栈相关面试题
### 举例栈溢出的情况？
SOF（StackOverflowError），栈大小分为固定的，和动态变化。如果是固定的就可能出现StackOverflowError。如果是动态变化的，内存不足时就可能出现OOM
### 调整栈大小，就能保证不出现溢出么？
不能保证不溢出，只能保证SOF出现的几率小
### 分配的栈内存越大越好么？
不是，一定时间内降低了OOM概率，但是会挤占其它的线程空间，因为整个虚拟机的内存空间是有限的
### 垃圾回收是否涉及到虚拟机栈？
不会

| **位置**                                    | **是否有Error** | **是否存在GC** |
| ------------------------------------------- | --------------- | -------------- |
| PC计数器                                    | 无              | 不存在         |
| 虚拟机栈                                    | 有，SOF         | 不存在         |
| 本地方法栈(在HotSpot的实现中和虚拟机栈一样) |                 |                |
| 堆                                          | 有，OOM         | 存在           |
| 方法区                                      | 有              | 存在           |

### 方法中定义的局部变量是否线程安全？
具体问题具体分析

1. 如果只有一个线程才可以操作此数据，则必是线程安全的。
2. 如果有多个线程操作此数据，则此数据是共享数据。如果不考虑同步机制的话，会存在线程安全问题。

**具体问题具体分析：**

- 如果对象是在内部产生，并在内部消亡，没有返回到外部，那么它就是线程安全的，反之则是线程不安全的。
```java
/**
 * 面试题：
 * 方法中定义的局部变量是否线程安全？具体情况具体分析
 *
 *   何为线程安全？
 *      如果只有一个线程才可以操作此数据，则必是线程安全的。
 *      如果有多个线程操作此数据，则此数据是共享数据。如果不考虑同步机制的话，会存在线程安全问题。
 */
public class StringBuilderTest {

    int num = 10;

    //s1的声明方式是线程安全的（只在方法内部用了）
    public static void method1(){
        //StringBuilder:线程不安全
        StringBuilder s1 = new StringBuilder();
        s1.append("a");
        s1.append("b");
        //...
    }
    //sBuilder的操作过程：是线程不安全的（作为参数传进来，可能被其它线程操作）
    public static void method2(StringBuilder sBuilder){
        sBuilder.append("a");
        sBuilder.append("b");
        //...
    }
    //s1的操作：是线程不安全的（有返回值，可能被其它线程操作）
    public static StringBuilder method3(){
        StringBuilder s1 = new StringBuilder();
        s1.append("a");
        s1.append("b");
        return s1;
    }
    //s1的操作：是线程安全的（s1自己消亡了，最后返回的只是s1.toString的一个新对象）
    public static String method4(){
        StringBuilder s1 = new StringBuilder();
        s1.append("a");
        s1.append("b");
        return s1.toString();
    }

    public static void main(String[] args) {
        StringBuilder s = new StringBuilder();


        new Thread(() -> {
            s.append("a");
            s.append("b");
        }).start();

        method2(s);

    }

}

```

# 六、 本地方法接口
## 1、本地方法
![](image/1663897886095-badf5a6d-5078-4f5d-88cf-94f58f7f7186.png)

1. 简单地讲，**一个Native Method是一个Java调用非Java代码的接囗**一个Native Method是这样一个Java方法：该方法的实现由非Java语言实现，比如C。这个特征并非Java所特有，很多其它的编程语言都有这一机制，比如在C++中，你可以用extern 告知C++编译器去调用一个C的函数。
2. “A native method is a Java method whose implementation is provided by non-java code.”（本地方法是一个非Java的方法，它的具体实现是非Java代码的实现）
3. 在定义一个native method时，并不提供实现体（有些像定义一个Java interface），因为其实现体是由非java语言在外面实现的。
4. 本地接口的作用是融合不同的编程语言为Java所用，它的初衷是融合C/C++程序。
> 需要注意的是：标识符native可以与其它java标识符连用，但是abstract除外

```java
public class IHaveNatives {
    public native void Native1(int x);
    public native static long Native2();
    private native synchronized float Native3(Object o);
    native void Native4(int[] ary) throws Exception;
}
```
## 2、为什么要使用 Native Method？
Java使用起来非常方便，然而有些层次的任务用Java实现起来不容易，或者我们对程序的效率很在意时，问题就来了。
### 与Java环境外交互
**有时Java应用需要与Java外面的硬件环境交互，这是本地方法存在的主要原因**。你可以想想Java需要与一些**底层系统**，如操作系统或某些硬件交换信息时的情况。本地方法正是这样一种交流机制：它为我们提供了一个非常简洁的接口，而且我们无需去了解Java应用之外的繁琐的细节。
### 与操作系统的交互

1. JVM支持着Java语言本身和运行时库，它是Java程序赖以生存的平台，它由一个解释器（解释字节码）和一些连接到本地代码的库组成。
2. 然而不管怎样，它毕竟不是一个完整的系统，它经常依赖于一底层系统的支持。这些底层系统常常是强大的操作系统。
3. **通过使用本地方法，我们得以用Java实现了jre的与底层系统的交互，甚至JVM的一些部分就是用C写的**。
4. 还有，如果我们要使用一些Java语言本身没有提供封装的操作系统的特性时，我们也需要使用本地方法。
### Sun’s Java

1. Sun的解释器是用C实现的，这使得它能像一些普通的C一样与外部交互。jre大部分是用Java实现的，它也通过一些本地方法与外界交互。
2. 例如：类java.lang.Thread的setPriority()方法是用Java实现的，但是它实现调用的是该类里的本地方法setPriority0()。这个本地方法是用C实现的，并被植入JVM内部在Windows 95的平台上，这个本地方法最终将调用Win32 setpriority() API。这是一个本地方法的具体实现由JVM直接提供，更多的情况是本地方法由外部的动态链接库（external dynamic link library）提供，然后被JVM调用。
### 本地方法的现状
目前该方法使用的越来越少了，除非是与硬件有关的应用，比如通过Java程序驱动打印机或者Java系统管理生产设备，在企业级应用中已经比较少见。因为现在的异构领域间的通信很发达，比如可以使用Socket通信，也可以使用Web Service等等，不多做介绍。
# 七、 本地方法栈
## 1、介绍

1. **Java虚拟机栈于管理Java方法的调用，而本地方法栈用于管理本地方法的调用**。
2. 本地方法栈，也是线程私有的。
3. 允许被实现成固定或者是可动态扩展的内存大小（在内存溢出方面和虚拟机栈相同）
   - 如果线程请求分配的栈容量超过本地方法栈允许的最大容量，Java虚拟机将会抛出一个stackoverflowError 异常。
   - 如果本地方法栈可以动态扩展，并且在尝试扩展的时候无法申请到足够的内存，或者在创建新的线程时没有足够的内存去创建对应的本地方法栈，那么Java虚拟机将会抛出一个outofMemoryError异常。
4. 本地方法一般是使用C语言或C++语言实现的。
5. 它的具体做法是Native Method Stack中登记native方法，在Execution Engine 执行时加载本地方法库。

![](image/1663897886021-3112d9eb-d92f-4f26-b252-f1b7e18ca541.png)
## 2、注意事项

1. 当某个线程调用一个本地方法时，它就进入了一个全新的并且不再受虚拟机限制的世界。它和虚拟机拥有同样的权限。
   - 本地方法可以通过本地方法接口来访问虚拟机内部的运行时数据区
   - 它甚至可以直接使用本地处理器中的寄存器
   - 直接从本地内存的堆中分配任意数量的内存
2. 并不是所有的JVM都支持本地方法。因为Java虚拟机规范并没有明确要求本地方法栈的使用语言、具体实现方式、数据结构等。如果JVM产品不打算支持native方法，也可以无需实现本地方法栈。
3. 在Hotspot JVM中，直接将本地方法栈和虚拟机栈合二为一。


# 八、 堆
## 1、核心概述
### 堆与进程

1. 堆针对一个JVM进程来说是唯一的。也就是**一个进程只有一个JVM实例**，一个JVM实例中就有一个运行时数据区，一个运行时数据区只有一个堆和一个方法区。
2. 但是**进程包含多个线程，他们是共享同一堆空间的**。

![](image/1663942569048-7e40f053-6272-44f6-8a88-50b6366c5372.png)

1. 一个JVM实例只存在一个堆内存，堆也是Java内存管理的核心区域。
2. Java堆区在JVM启动的时候即被创建，其空间大小也就确定了，堆是JVM管理的最大一块内存空间，并且堆内存的大小是可以调节的。
3. 《Java虚拟机规范》规定，堆可以处于物理上不连续的内存空间中，但在逻辑上它应该被视为连续的。
4. 所有的线程共享Java堆，在这里还可以划分线程私有的缓冲区（Thread Local Allocation Buffer，**TLAB**）。
5. 《Java虚拟机规范》中对Java堆的描述是：**所有的对象实例以及数组都应当在运行时分配在堆上**。（The heap is the run-time data area from which memory for all class instances and arrays is allocated）
   - 从实际使用角度看：“几乎”所有的对象实例都在堆分配内存，但并非全部。因为还有一些对象是在栈上分配的（逃逸分析，标量替换）
6. 数组和对象可能永远不会存储在栈上（**不一定**），因为栈帧中保存引用，这个引用指向对象或者数组在堆中的位置。
7. 在方法结束后，堆中的对象不会马上被移除，仅仅在垃圾收集的时候才会被移除。
   - 也就是触发了GC的时候，才会进行回收
   - 如果堆中对象马上被回收，那么用户线程就会收到影响，因为有stop the world
8. 堆，是GC（Garbage Collection，垃圾收集器）执行垃圾回收的重点区域。
> 随着JVM的迭代升级，原来一些绝对的事情，在后续版本中也开始有了特例，变的不再那么绝对。

![](image/1663942569477-fe29231c-0a31-4224-b7ca-d2b8961e2c64.png)
### 堆内存细分
现代垃圾收集器大部分都基于分代收集理论设计，堆空间细分为：

1. Java7 及之前堆内存逻辑上分为三部分：新生区+养老区+永久区
   - Young Generation Space 新生区 Young/New
      - 又被划分为Eden区和Survivor区
   - Old generation space 养老区 Old/Tenure
   - Permanent Space 永久区 Perm
2. Java 8及之后堆内存逻辑上分为三部分：新生区+养老区+元空间
   - Young Generation Space 新生区，又被划分为Eden区和Survivor区
   - Old generation space 养老区
   - Meta Space 元空间 Meta

约定：

- 新生区 = 新生代 = 年轻代 
- 养老区 = 老年区 = 老年代
- 永久区 = 永久代

![](image/1663942571433-4f111095-c191-47a3-9b69-8829fa21a914.png)

1. 堆空间内部结构，JDK1.8之前从永久代 替换成 元空间

![](image/1663942570039-09189b88-cf10-4365-b678-6a61f7e89aa6.png)
## 2、JVisualVM
运行下面代码
```java
public class HeapDemo {
    public static void main(String[] args) {
        System.out.println("start...");
        try {
            TimeUnit.MINUTES.sleep(30);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("end...");
    }

}
```
1、双击jdk目录下的这个文件
![](image/1663942569981-e47eb6fe-27e2-4a45-9d29-3b0908302744.png)
2、工具 -> 插件 -> 安装Visual GC插件
![](image/1663942572236-7971f0c6-17bc-4d1a-a63d-89e3cb172ba8.png)
3、运行上面的代码
![](image/1663942573849-e8668554-662e-437f-8297-a6d355b312c9.png)
## 3、设置堆大小与 OOM
### 设置堆内存

1. Java堆区用于存储Java对象实例，那么堆的大小在JVM启动时就已经设定好了，大家可以通过选项"-Xms"和"-Xmx"来进行设置。
   - **-Xms**用于表示堆区的起始内存，等价于**-XX:InitialHeapSize**
   - **-Xmx**则用于表示堆区的最大内存，等价于**-XX:MaxHeapSize**
2. 一旦堆区中的内存大小超过“-Xmx"所指定的最大内存时，将会抛出OutofMemoryError异常。
3. 通常会将-Xms和-Xmx两个参数配置相同的值
- 原因：假设两个不一样，初始内存小，最大内存大。在运行期间如果堆内存不够用了，会一直扩容直到最大内存。如果内存够用且多了，也会不断的缩容释放。频繁的扩容和释放造成不必要的压力，避免在GC之后调整堆内存给服务器带来压力。
- 如果两个设置一样的就少了频繁扩容和缩容的步骤。内存不够了就直接报OOM
1. 默认情况下:
   - 初始内存大小：物理电脑内存大小/64
   - 最大内存大小：物理电脑内存大小/4
```java
/**
 * 1. 设置堆空间大小的参数
 * -Xms 用来设置堆空间（年轻代+老年代）的初始内存大小
 *      -X 是jvm的运行参数
 *      ms 是memory start
 * -Xmx 用来设置堆空间（年轻代+老年代）的最大内存大小
 *
 * 2. 默认堆空间的大小
 *    初始内存大小：物理电脑内存大小 / 64
 *             最大内存大小：物理电脑内存大小 / 4
 * 3. 手动设置：-Xms600m -Xmx600m
 *     开发中建议将初始堆内存和最大的堆内存设置成相同的值。
 *
 * 4. 查看设置的参数：方式一： jps   /  jstat -gc 进程id
 *                  方式二：-XX:+PrintGCDetails
 */
public class HeapSpaceInitial {
    public static void main(String[] args) {

        //返回Java虚拟机中的堆内存总量
        long initialMemory = Runtime.getRuntime().totalMemory() / 1024 / 1024;
        //返回Java虚拟机试图使用的最大堆内存量
        long maxMemory = Runtime.getRuntime().maxMemory() / 1024 / 1024;

        System.out.println("-Xms : " + initialMemory + "M");
        System.out.println("-Xmx : " + maxMemory + "M");

        System.out.println("系统内存大小为：" + initialMemory * 64.0 / 1024 + "G");
        System.out.println("系统内存大小为：" + maxMemory * 4.0 / 1024 + "G");

        try {
            Thread.sleep(1000000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```
输出结果：
```bash
-Xms : 245M
-Xmx : 3637M
系统内存大小为：15.3125G
系统内存大小为：14.20703125G
```
1、电脑内存大小是16G，不足16G的原因是操作系统自身还占据了一些。
设置下参数再看
![](image/1663942571267-5aac5c0f-719f-42b4-b857-41d5b26277cb.png)
输出结果：
```bash
-Xms : 575M
-Xmx : 575M
```
为什么会少25M
**方式一： jps / jstat -gc 进程id**
![](image/1663942572544-6b268308-5052-4a91-8e4e-e2c61b0c422d.png)
jps：查看java进程
jstat：查看某进程内存使用情况
```bash
SOC: S0区总共容量
S1C: S1区总共容量
S0U: S0区使用的量
S1U: S1区使用的量
EC: 伊甸园区总共容量
EU: 伊甸园区使用的量
OC: 老年代总共容量
OU: 老年代使用的量
```
1、
25600+25600+153600+409600 = 614400K
614400 /1024 = 600M
2、
25600+153600+409600 = 588800K
588800 /1024 = 575M
3、
并非巧合，S0区和S1区两个只有一个能使用，另一个用不了（后面会详解）
**方式二：-XX:+PrintGCDetails**
![1663944675791-cf3aecfa-26c9-4c98-b9e7-61b65b54ac70](image/1663944675791-cf3aecfa-26c9-4c98-b9e7-61b65b54ac70.png)

### OOM
```java
public class OOMTest {
    public static void main(String[] args) {
        ArrayList<Picture> list = new ArrayList<>();
        while(true){
            try {
                Thread.sleep(20);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            list.add(new Picture(new Random().nextInt(1024 * 1024)));
        }
    }
}

class Picture{
    private byte[] pixels;

    public Picture(int length) {
        this.pixels = new byte[length];
    }
}
```
1、设置虚拟机参数
-Xms600m -Xmx600m
最终输出结果：
```bash
Exception in thread "main" java.lang.OutOfMemoryError: Java heap space
	at com.renchao.java.Picture.<init>(OOMTest.java:24)
	at com.renchao.java.OOMTest.main(OOMTest.java:15)
```
2、堆内存变化图
![](image/1663942572604-55fb7861-debf-4ed8-be09-335ddbc0d501.png)
3、原因：大对象导致堆内存溢出
![](image/1663942573312-bb85c212-003a-4b08-a06e-47e4c9c4c66b.png)
## 4、年轻代与老年代
1、存储在JVM中的Java对象可以被划分为两类：
- 一类是生命周期较短的瞬时对象，这类对象的创建和消亡都非常迅速 - 另外一类对象的生命周期却非常长，在某些极端的情况下还能够与JVM的生命周期保持一致 
2、Java堆区进一步细分的话，可以划分为年轻代（YoungGen）和老年代（oldGen）
3、其中年轻代又可以划分为Eden空间、Survivor0空间和Survivor1空间（有时也叫做from区、to区）
![](image/1663942573511-72b3ef2d-cae0-4fd3-a2a7-2a104b233b90.png)
![](image/1663942575830-e748a4aa-e997-4948-b136-9053af6c64a1.png)

- 配置新生代与老年代在堆结构的占比
   - 默认**-XX:NewRatio**=2，表示新生代占1，老年代占2，新生代占整个堆的1/3
   - 可以修改**-XX:NewRatio**=4，表示新生代占1，老年代占4，新生代占整个堆的1/5
1. 在HotSpot中，Eden空间和另外两个survivor空间缺省所占的比例是8 : 1 : 1，
2. 当然开发人员可以通过选项**-XX:SurvivorRatio**调整这个空间比例。比如-XX:SurvivorRatio=8
3. 几乎所有的Java对象都是在Eden区被new出来的。
4. 绝大部分的Java对象的销毁都在新生代进行了（有些大的对象在Eden区无法存储时候，将直接进入老年代），IBM公司的专门研究表明，新生代中80%的对象都是“朝生夕死”的。
5. 可以使用选项"-Xmn"设置新生代最大内存大小，但这个参数一般使用默认值就可以了。

![](image/1663942579766-b5273b41-99a7-42a7-b21a-9de6bbdaacec.png)
```java
/**
 * -Xms600m -Xmx600m
 *
 * -XX:NewRatio ： 设置新生代与老年代的比例。默认值是2.
 * -XX:SurvivorRatio ：设置新生代中Eden区与Survivor区的比例。默认值是8
 * -XX:-UseAdaptiveSizePolicy ：关闭自适应的内存分配策略  （暂时用不到）
 * -Xmn:设置新生代的空间的大小。 （一般不设置）
 *
 * @author shkstart  shkstart@126.com
 * @create 2020  17:23
 */
public class EdenSurvivorTest {
    public static void main(String[] args) {
        System.out.println("我只是来打个酱油~");
        try {
            Thread.sleep(1000000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```
## 5、对象分配过程
为新对象分配内存是一件非常严谨和复杂的任务，JVM的设计者们不仅需要考虑内存如何分配、在哪里分配等问题，并且由于内存分配算法与内存回收算法密切相关，所以还需要考虑GC执行完内存回收后是否会在内存空间中产生内存碎片。
**具体过程**

1. new的对象先放伊甸园区。此区有大小限制。
2. 当伊甸园的空间填满时，程序又需要创建对象，JVM的垃圾回收器将对伊甸园区进行垃圾回收（MinorGC），将伊甸园区中的不再被其他对象所引用的对象进行销毁。再加载新的对象放到伊甸园区。
3. 然后将伊甸园中的剩余对象移动到幸存者0区。
4. 如果再次触发垃圾回收，此时上次幸存下来的放到幸存者0区的，如果没有回收，就会放到幸存者1区。
5. 如果再次经历垃圾回收，此时会重新放回幸存者0区，接着再去幸存者1区。
6. 啥时候能去养老区呢？可以设置次数。默认是15次。可以设置新生区进入养老区的年龄限制，设置 JVM 参数：**-XX:MaxTenuringThreshold**=N 进行设置
7. 在养老区，相对悠闲。当养老区内存不足时，再次触发GC：Major GC，进行养老区的内存清理
8. 若养老区执行了Major GC之后，发现依然无法进行对象的保存，就会产生OOM异常。
### 图解对象分配（一般情况）
1、我们创建的对象，一般都是存放在Eden区的，**当我们Eden区满了后，就会触发GC操作**，一般被称为 YGC / Minor GC操作
![](image/1663942577028-68d64a0b-d455-4faf-b5b9-60330e21d8a2.png)
2、当我们进行一次垃圾收集后，红色的对象将会被回收，而绿色的独享还被占用着，存放在S0(Survivor From)区。同时我们给每个对象设置了一个年龄计数器，经过一次回收后还存在的对象，将其年龄加 1。
3、同时Eden区继续存放对象，当Eden区再次存满的时候，又会触发一个MinorGC操作，此时GC将会把 Eden和Survivor From中的对象进行一次垃圾收集，把存活的对象放到 Survivor To（S1）区，同时让存活的对象年龄 + 1
下一次再进行GC的时候，
1、这一次的s0区为空，所以成为下一次GC的S1区
2、这一次的s1区则成为下一次GC的S0区
3、也就是说s0区和s1区在互相转换。
![image.png](image/1663945239302-e09c12f7-5979-41fb-96d5-067e9e89a73b.png)
4、我们继续不断的进行对象生成和垃圾回收，当Survivor中的对象的年龄达到15的时候，将会触发一次 Promotion 晋升的操作，也就是将年轻代中的对象晋升到老年代中
![image.png](image/1663945256864-b9607c0d-bbed-43c2-b259-4416bdf8416b.png)
关于垃圾回收：频繁在新生区收集，很少在养老区收集，几乎不在永久区/元空间收集。

### 特殊情况说明
**对象分配的特殊情况**

1. 如果来了一个新对象，先看看 Eden 是否放的下？
   - 如果 Eden 放得下，则直接放到 Eden 区
   - 如果 Eden 放不下，则触发 YGC ，执行垃圾回收，看看还能不能放下？
2. 将对象放到老年区又有两种情况：
   - 如果 Eden 执行了 YGC 还是无法放不下该对象，那没得办法，只能说明是超大对象，只能直接放到老年代
   - 那万一老年代都放不下，则先触发FullGC ，再看看能不能放下，放得下最好，但如果还是放不下，那只能报 OOM
3. 如果 Eden 区满了，将对象往幸存区拷贝时，发现幸存区放不下啦，那只能便宜了某些新对象，让他们直接晋升至老年区

![](image/1663942585461-ada4c03f-f1c0-4343-87b0-9ae73ced8941.png)
### 常用调优工具

1. JDK命令行
2. Eclipse：Memory Analyzer Tool
3. Jconsole
4. Visual VM（实时监控，推荐）
5. Jprofiler（IDEA插件）
6. Java Flight Recorder（实时监控）
7. GCViewer
8. GCEasy
## 6、GC分类

1. 我们都知道，JVM的调优的一个环节，也就是垃圾收集，我们需要尽量的避免垃圾回收，因为在垃圾回收的过程中，容易出现STW（Stop the World）的问题，**而 Major GC 和 Full GC出现STW的时间，是Minor GC的10倍以上**
2. JVM在进行GC时，并非每次都对上面三个内存区域一起回收的，大部分时候回收的都是指新生代。针对Hotspot VM的实现，它里面的GC按照回收区域又分为两大种类型：一种是部分收集（Partial GC），一种是整堆收集（FullGC）
- 部分收集：不是完整收集整个Java堆的垃圾收集。其中又分为：
   - **新生代收集**（Minor GC/Young GC）：只是新生代（Eden，s0，s1）的垃圾收集
   - **老年代收集**（Major GC/Old GC）：只是老年代的圾收集。
   - 目前，只有CMS GC会有单独收集老年代的行为。
   - 注意，很多时候Major GC会和Full GC混淆使用，需要具体分辨是老年代回收还是整堆回收。
   - 混合收集（Mixed GC）：收集整个新生代以及部分老年代的垃圾收集。目前，只有G1 GC会有这种行为
- **整堆收集**（Full GC）：收集整个java堆和方法区的垃圾收集。

由于历史原因，外界各种解读，majorGC和Full GC有些混淆。
### Young GC
**年轻代 GC（Minor GC）触发机制**

1. 当年轻代空间不足时，就会触发Minor GC，这里的年轻代满指的是Eden代满。Survivor满不会主动引发GC，在Eden区满的时候，会顺带触发s0区的GC，也就是被动触发GC（每次Minor GC会清理年轻代的内存）
2. 因为Java对象大多都具备朝生夕灭的特性，所以Minor GC非常频繁，一般回收速度也比较快。这一定义既清晰又易于理解。
3. Minor GC会引发STW（Stop The World），暂停其它用户的线程，等垃圾回收结束，用户线程才恢复运行

![](image/1663942587090-0a16fd1b-fef4-4fd1-8911-6ca34c56d8fb.png)
### Major/Full GC
Full GC有争议，后续详解两者区别，暂时先看着
**老年代GC（MajorGC）触发机制**

1. 指发生在老年代的GC，对象从老年代消失时，我们说 “Major Gc” 或 “Full GC” 发生了
2. 出现了MajorGc，经常会伴随至少一次的Minor GC。（但非绝对的，在Parallel Scavenge收集器的收集策略里就有直接进行MajorGC的策略选择过程）
   - 也就是在老年代空间不足时，会先尝试触发Minor GC（哈？我有点迷？），如果之后空间还不足，则触发Major GC
3. Major GC的速度一般会比Minor GC慢10倍以上，STW的时间更长。
4. 如果Major GC后，内存还不足，就报OOM了

**Full GC 触发机制（后面细讲）**
**触发Full GC执行的情况有如下五种：**

1. 调用System.gc()时，系统建议执行FullGC，但是不必然执行
2. 老年代空间不足
3. 方法区空间不足
4. 通过Minor GC后进入老年代的平均大小大于老年代的可用内存
5. 由Eden区、survivor space0（From Space）区向survivor space1（To Space）区复制时，对象大小大于To Space可用内存，则把该对象转存到老年代，且老年代的可用内存小于该对象大小

说明：Full GC 是开发或调优中尽量要避免的。这样STW时间会短一些

### 补充
> P76解读有误，PPT相关信息可在CSDN找到，贴个大佬的：
> 作者：RednaxelaFX
> 链接：https://www.zhihu.com/question/41922036/answer/93079526
> 来源：知乎
> 针对HotSpot VM的实现，它里面的GC其实准确分类只有两大种：
>
> - Partial GC：并不收集整个GC堆的模式
>    - Young GC：只收集young gen的GC
>    - Old GC：只收集old gen的GC。只有CMS的concurrent collection是这个模式
>    - Mixed GC：收集整个young gen以及部分old gen的GC。只有G1有这个模式 
> - Full GC：收集整个堆，包括young gen、old gen、perm gen（如果存在的话）等所有部分的模式

### GC日志分析
```java
/**
 * 测试MinorGC 、 MajorGC、FullGC
 * -Xms9m -Xmx9m -XX:+PrintGCDetails
 * @author shkstart  shkstart@126.com
 * @create 2020  14:19
 */
public class GCTest {
    public static void main(String[] args) {
        int i = 0;
        try {
            List<String> list = new ArrayList<>();
            String a = "atguigu.com";
            while (true) {
                list.add(a);
                a = a + a;
                i++;
            }

        } catch (Throwable t) {
            t.printStackTrace();
            System.out.println("遍历次数为：" + i);
        }
    }
}

```
输出：
```bash
[GC (Allocation Failure) [PSYoungGen: 2037K->504K(2560K)] 2037K->728K(9728K), 0.0455865 secs] [Times: user=0.00 sys=0.00, real=0.06 secs] 
[GC (Allocation Failure) [PSYoungGen: 2246K->496K(2560K)] 2470K->1506K(9728K), 0.0009094 secs] [Times: user=0.00 sys=0.00, real=0.00 secs] 
[GC (Allocation Failure) [PSYoungGen: 2294K->488K(2560K)] 3305K->2210K(9728K), 0.0009568 secs] [Times: user=0.00 sys=0.00, real=0.00 secs] 
[GC (Allocation Failure) [PSYoungGen: 1231K->488K(2560K)] 7177K->6434K(9728K), 0.0005594 secs] [Times: user=0.00 sys=0.00, real=0.00 secs] 
[GC (Allocation Failure) [PSYoungGen: 488K->472K(2560K)] 6434K->6418K(9728K), 0.0005890 secs] [Times: user=0.00 sys=0.00, real=0.00 secs] 
[Full GC (Allocation Failure) [PSYoungGen: 472K->0K(2560K)] [ParOldGen: 5946K->4944K(7168K)] 6418K->4944K(9728K), [Metaspace: 3492K->3492K(1056768K)], 0.0045270 secs] [Times: user=0.00 sys=0.00, real=0.01 secs] 
[GC (Allocation Failure) [PSYoungGen: 0K->0K(1536K)] 4944K->4944K(8704K), 0.0004954 secs] [Times: user=0.00 sys=0.00, real=0.00 secs] 
[Full GC (Allocation Failure) java.lang.OutOfMemoryError: Java heap space
	at java.util.Arrays.copyOf(Arrays.java:3332)
	at java.lang.AbstractStringBuilder.ensureCapacityInternal(AbstractStringBuilder.java:124)
	at java.lang.AbstractStringBuilder.append(AbstractStringBuilder.java:448)
	at java.lang.StringBuilder.append(StringBuilder.java:136)
	at com.atguigu.java1.GCTest.main(GCTest.java:20)
[PSYoungGen: 0K->0K(1536K)] [ParOldGen: 4944K->4877K(7168K)] 4944K->4877K(8704K), [Metaspace: 3492K->3492K(1056768K)], 0.0076061 secs] [Times: user=0.00 sys=0.02, real=0.01 secs] 
遍历次数为：16
Heap
 PSYoungGen      total 1536K, used 60K [0x00000000ffd00000, 0x0000000100000000, 0x0000000100000000)
  eden space 1024K, 5% used [0x00000000ffd00000,0x00000000ffd0f058,0x00000000ffe00000)
  from space 512K, 0% used [0x00000000fff80000,0x00000000fff80000,0x0000000100000000)
  to   space 1024K, 0% used [0x00000000ffe00000,0x00000000ffe00000,0x00000000fff00000)
 ParOldGen       total 7168K, used 4877K [0x00000000ff600000, 0x00000000ffd00000, 0x00000000ffd00000)
  object space 7168K, 68% used [0x00000000ff600000,0x00000000ffac3408,0x00000000ffd00000)
 Metaspace       used 3525K, capacity 4502K, committed 4864K, reserved 1056768K
  class space    used 391K, capacity 394K, committed 512K, reserved 1048576K
```

- [PSYoungGen: 2037K->504K(2560K)]：年轻代总空间为 2560K ，当前占用 2037K ，经过垃圾回收后剩余504K
- 2037K->728K(9728K)：堆内存总空间为 9728K ，当前占用2037K ，经过垃圾回收后剩余728K
## 7、堆空间分代思想
为什么要把Java堆分代？不分代就不能正常工作了吗？经研究，不同对象的生命周期不同。70%-99%的对象是临时对象。

- 新生代：有Eden、两块大小相同的survivor（又称为from/to或s0/s1）构成，to总为空。
- 老年代：存放新生代中经历多次GC仍然存活的对象。

![](image/1663942587396-c0f4ae29-c202-43de-9b18-daed97c47fe2.png)
其实不分代完全可以，分代的唯一理由就是优化GC性能。

- 如果没有分代，那所有的对象都在一块，就如同把一个学校的人都关在一个教室。GC的时候要找到哪些对象没用，这样就会对堆的所有区域进行扫描。（性能低）
- 而很多对象都是朝生夕死的，如果分代的话，把新创建的对象放到某一地方，当GC的时候先把这块存储“朝生夕死”对象的区域进行回收，这样就会腾出很大的空间出来。（多回收新生代，少回收老年代，性能会提高很多）

![](image/1663942588843-ea40b912-720f-4c34-9f83-4c1e489b3148.png)
## 8、对象内存分配策略

1. 如果对象在Eden出生并经过第一次Minor GC后仍然存活，并且能被Survivor容纳的话，将被移动到Survivor空间中，并将对象年龄设为1。
2. 对象在Survivor区中每熬过一次MinorGC，年龄就增加1岁，当它的年龄增加到一定程度（默认为15岁，其实每个JVM、每个GC都有所不同）时，就会被晋升到老年代
3. 对象晋升老年代的年龄阀值，可以通过选项`-XX:MaxTenuringThreshold`来设置

**针对不同年龄段的对象分配原则如下所示：**

1. **优先分配到Eden**：开发中比较长的字符串或者数组，会直接存在老年代，但是因为新创建的对象都是朝生夕死的，所以这个大对象可能也很快被回收，但是因为老年代触发Major GC的次数比 Minor GC要更少，因此可能回收起来就会比较慢
2. **大对象直接分配到老年代**：尽量避免程序中出现过多的大对象
3. **长期存活的对象分配到老年代**
4. **动态对象年龄判断**：如果Survivor区中相同年龄的所有对象大小的总和大于Survivor空间的一半，年龄大于或等于该年龄的对象可以直接进入老年代，无须等到MaxTenuringThreshold中要求的年龄。
5. **空间分配担保**： -XX:HandlePromotionFailure 。
## 9、TLAB
### 为什么有 TLAB

1. 堆区是线程共享区域，任何线程都可以访问到堆区中的共享数据
2. 由于对象实例的创建在JVM中非常频繁，因此在并发环境下从堆区中划分内存空间是线程不安全的
3. 为避免多个线程操作同一地址，需要使用**加锁等机制**，进而影响分配速度。
### 什么是 TLAB
TLAB（Thread Local Allocation Buffer）

1. 从内存模型而不是垃圾收集的角度，对Eden区域继续进行划分，**JVM为每个线程分配了一个私有缓存区域，它包含在Eden空间内**。
2. 多线程同时分配内存时，使用TLAB可以避免一系列的非线程安全问题，同时还能够提升内存分配的吞吐量，因此我们可以将这种内存分配方式称之为**快速分配策略**。
3. 据我所知所有OpenJDK衍生出来的JVM都提供了TLAB的设计。

![](image/1663942589909-28911f6f-50e5-4b7a-8388-b6448292103c.png)
1、每个线程都有一个TLAB空间
2、当一个线程的TLAB存满时，可以使用公共区域（蓝色）的
### TLAB再说明

1. 尽管不是所有的对象实例都能够在TLAB中成功分配内存，但**JVM确实是将TLAB作为内存分配的首选**。
2. 在程序中，开发人员可以通过选项“**-XX:UseTLAB**”设置是否开启TLAB空间。
3. 默认情况下，TLAB空间的内存非常小，仅占有整个Eden空间的1%，当然我们可以通过选项“**-XX:TLABWasteTargetPercent**”设置TLAB空间所占用Eden空间的百分比大小。
4. 一旦对象在TLAB空间分配内存失败时，JVM就会尝试着通过**使用加锁机制确保数据操作的原子性**，从而直接在Eden空间中分配内存。
> 1、哪个线程要分配内存，就在哪个线程的本地缓冲区中分配，只有本地缓冲区用完 了，**分配新的缓存区时才需要同步锁定** ----这是《深入理解JVM》--第三版里说的
> 2、和这里讲的有点不同。我猜测说的意思是某一次分配，如果TLAB用完了，那么**这一次**先在Eden区直接分配。空闲下来后再加锁分配新的TLAB（TLAB内存较大，分配时间应该较长）


**TLAB 分配过程**
![](image/1663942590754-e5d5b1dd-2b7d-47ff-9e1d-d8a58c7c928d.png)
## 10、堆空间参数设置
### 常用参数设置
**官方文档**：[https://docs.oracle.com/javase/8/docs/technotes/tools/unix/java.html](https://docs.oracle.com/javase/8/docs/technotes/tools/unix/java.html)
只说常用的
```bash
/**
 * 测试堆空间常用的jvm参数：
 * -XX:+PrintFlagsInitial : 查看所有的参数的默认初始值
 * -XX:+PrintFlagsFinal  ：查看所有的参数的最终值（可能会存在修改，不再是初始值）
 *      具体查看某个参数的指令： jps：查看当前运行中的进程
 *                             jinfo -flag SurvivorRatio 进程id
 *
 * -Xms：初始堆空间内存 （默认为物理内存的1/64）
 * -Xmx：最大堆空间内存（默认为物理内存的1/4）
 * -Xmn：设置新生代的大小。(初始值及最大值)
 * -XX:NewRatio：配置新生代与老年代在堆结构的占比
 * -XX:SurvivorRatio：设置新生代中Eden和S0/S1空间的比例
 * -XX:MaxTenuringThreshold：设置新生代垃圾的最大年龄
 * -XX:+PrintGCDetails：输出详细的GC处理日志
 * 打印gc简要信息：① -XX:+PrintGC   ② -verbose:gc
 * -XX:HandlePromotionFailure：是否设置空间分配担保
 */
```
### 空间分配担保
1、在发生Minor GC之前，**虚拟机会检查老年代最大可用的连续空间是否大于新生代所有对象的总空间。**

- 如果大于，则此次Minor GC是安全的
- 如果小于，则虚拟机会查看`-XX:HandlePromotionFailure`设置值是否允担保失败。
   - 如果HandlePromotionFailure=true，那么会继续检查**老年代最大可用连续空间是否大于历次晋升到老年代的对象的平均大小**。
      - 如果大于，则尝试进行一次Minor GC，但这次Minor GC依然是有风险的；
      - 如果小于，则进行一次Full GC。
   - 如果HandlePromotionFailure=false，则进行一次Full GC。

**历史版本**

1. 在JDK6 Update 24之后，HandlePromotionFailure参数不会再影响到虚拟机的空间分配担保策略，观察openJDK中的源码变化，虽然源码中还定义了HandlePromotionFailure参数，但是在代码中已经不会再使用它。
2. JDK6 Update 24之后的规则变为**只要老年代的连续空间大于新生代对象总大小或者历次晋升的平均大小就会进行Minor GC**，否则将进行Full GC。即 HandlePromotionFailure=true
## 11、堆是分配对象的唯一选择么？
**在《深入理解Java虚拟机》中关于Java堆内存有这样一段描述：**

1. 随着JIT编译期的发展与**逃逸分析技术**逐渐成熟，**栈上分配、标量替换**优化技术将会导致一些微妙的变化，所有的对象都分配到堆上也渐渐变得不那么“绝对”了。
2. 在Java虚拟机中，对象是在Java堆中分配内存的，这是一个普遍的常识。但是，有一种特殊情况，那就是**如果经过逃逸分析（Escape Analysis）后发现，一个对象并没有逃逸出方法的话，那么就可能被优化成栈上分配**。这样就无需在堆上分配内存，也无须进行垃圾回收了。这也是最常见的堆外存储技术。
3. 此外，前面提到的基于OpenJDK深度定制的TaoBao VM，其中创新的GCIH（GC invisible heap）技术实现off-heap，将生命周期较长的Java对象从heap中移至heap外，并且GC不能管理GCIH内部的Java对象，以此达到降低GC的回收频率和提升GC的回收效率的目的。
### 逃逸分析

1. 如何将堆上的对象分配到栈，需要使用逃逸分析手段。
2. 这是一种可以有效减少Java程序中同步负载和内存堆分配压力的跨函数全局数据流分析算法。
3. 通过逃逸分析，Java Hotspot编译器能够分析出一个新的对象的引用的使用范围从而决定是否要将这个对象分配到堆上。
4. 逃逸分析的基本行为就是分析对象动态作用域：
   - 当一个对象在方法中被定义后，对象只在方法内部使用，则认为没有发生逃逸。
   - 当一个对象在方法中被定义后，它被外部方法所引用，则认为发生逃逸。例如作为调用参数传递到其他地方中。

**逃逸分析举例**
1、没有发生逃逸的对象，则可以分配到栈（无线程安全问题）上，随着方法执行的结束，栈空间就被移除（也就无需GC）

```java
public void my_method() {
    V v = new V();
    // use v
    // ....
    v = null;
}
```
2、下面代码中的 StringBuffer sb 发生了逃逸，不能在栈上分配
```java
public static StringBuffer createStringBuffer(String s1, String s2) {
    StringBuffer sb = new StringBuffer();
    sb.append(s1);
    sb.append(s2);
    return sb;
}
```
3、如果想要StringBuffer sb不发生逃逸，可以这样写
```java
public static String createStringBuffer(String s1, String s2) {
    StringBuffer sb = new StringBuffer();
    sb.append(s1);
    sb.append(s2);
    return sb.toString();
}
```
```java

/**
 * 逃逸分析
 *
 *  如何快速的判断是否发生了逃逸分析，大家就看new的对象实体是否有可能在方法外被调用。
 */
public class EscapeAnalysis {

    public EscapeAnalysis obj;

    /*
    方法返回EscapeAnalysis对象，发生逃逸
     */
    public EscapeAnalysis getInstance(){
        return obj == null? new EscapeAnalysis() : obj;
    }
    /*
    为成员属性赋值，发生逃逸
     */
    public void setObj(){
        this.obj = new EscapeAnalysis();
    }
    //思考：如果当前的obj引用声明为static的？仍然会发生逃逸。

    /*
    对象的作用域仅在当前方法中有效，没有发生逃逸
     */
    public void useEscapeAnalysis(){
        EscapeAnalysis e = new EscapeAnalysis();
    }
    /*
    引用成员变量的值，发生逃逸
     */
    public void useEscapeAnalysis1(){
        EscapeAnalysis e = getInstance();
        //getInstance().xxx()同样会发生逃逸
    }
}

```
**逃逸分析参数设置**

1. 在JDK 1.7 版本之后，HotSpot中默认就已经开启了逃逸分析
2. 如果使用的是较早的版本，开发人员则可以通过：
   - 选项“-XX:+DoEscapeAnalysis"显式开启逃逸分析
   - 通过选项“-XX:+PrintEscapeAnalysis"查看逃逸分析的筛选结果

**总结**
开发中能使用局部变量的，就不要使用在方法外定义。
### 代码优化
使用逃逸分析，编译器可以对代码做如下优化：

1. **栈上分配**：将堆分配转化为栈分配。如果一个对象在子程序中被分配，要使指向该对象的指针永远不会发生逃逸，对象可能是栈上分配的候选，而不是堆上分配
2. **同步省略**：如果一个对象被发现只有一个线程被访问到，那么对于这个对象的操作可以不考虑同步。
3. **分离对象或标量替换**：有的对象可能不需要作为一个连续的内存结构存在也可以被访问到，那么对象的部分（或全部）可以不存储在内存，而是存储在CPU寄存器中。
### 栈上分配

1. JIT编译器在编译期间根据逃逸分析的结果，发现如果一个对象并没有逃逸出方法的话，就可能被优化成栈上分配。分配完成后，继续在调用栈内执行，最后线程结束，栈空间被回收，局部变量对象也被回收。这样就无须进行垃圾回收了。
2. 常见的栈上分配的场景：在逃逸分析中，已经说明了，分别是给成员变量赋值、方法返回值、实例引用传递。

**栈上分配举例**
```java
/**
 * 栈上分配测试
 * -Xmx128m -Xms128m -XX:-DoEscapeAnalysis -XX:+PrintGCDetails
 */
public class StackAllocation {
    public static void main(String[] args) {
        long start = System.currentTimeMillis();

        for (int i = 0; i < 10000000; i++) {
            alloc();
        }
        // 查看执行时间
        long end = System.currentTimeMillis();
        System.out.println("花费的时间为： " + (end - start) + " ms");
        // 为了方便查看堆内存中对象个数，线程sleep
        try {
            Thread.sleep(1000000);
        } catch (InterruptedException e1) {
            e1.printStackTrace();
        }
    }

    private static void alloc() {
        User user = new User();//未发生逃逸
    }

    static class User {

    }
}
```
输出结果：
```bash
[GC (Allocation Failure) [PSYoungGen: 33280K->808K(38400K)] 33280K->816K(125952K), 0.0483350 secs] [Times: user=0.00 sys=0.00, real=0.06 secs] 
[GC (Allocation Failure) [PSYoungGen: 34088K->808K(38400K)] 34096K->816K(125952K), 0.0008411 secs] [Times: user=0.00 sys=0.00, real=0.00 secs] 
[GC (Allocation Failure) [PSYoungGen: 34088K->792K(38400K)] 34096K->800K(125952K), 0.0008427 secs] [Times: user=0.00 sys=0.00, real=0.00 secs] 
[GC (Allocation Failure) [PSYoungGen: 34072K->808K(38400K)] 34080K->816K(125952K), 0.0012223 secs] [Times: user=0.08 sys=0.00, real=0.00 secs] 
花费的时间为： 114 ms
```
1、JVM 参数设置
-Xmx128m -Xms128m -XX:-DoEscapeAnalysis -XX:+PrintGCDetails
2、日志打印：发生了 GC ，耗时 114ms
**开启逃逸分析的情况**
输出结果：
花费的时间为： 5 ms 
1、参数设置
-Xmx128m -Xms128m -XX:+DoEscapeAnalysis -XX:+PrintGCDetails
2、日志打印：并没有发生 GC ，耗时5ms 。
### 同步省略（同步消除）

1. 线程同步的代价是相当高的，同步的后果是降低并发性和性能。
2. 在动态编译同步块的时候，JIT编译器可以借助逃逸分析来**判断同步块所使用的锁对象是否只能够被一个线程访问而没有被发布到其他线程**。
3. 如果没有，那么JIT编译器在编译这个同步块的时候就会取消对这部分代码的同步。这样就能大大提高并发性和性能。这个**取消同步的过程就叫同步省略，也叫锁消除**。

例如下面的代码
```java
public void f() {
    Object hollis = new Object();
    synchronized(hollis) {
        System.out.println(hollis);
    }
}
```
代码中对hollis这个对象加锁，但是hollis对象的生命周期只在f()方法中，并不会被其他线程所访问到，所以在JIT编译阶段就会被优化掉，优化成：
```java
public void f() {
    Object hellis = new Object();
	System.out.println(hellis);
}
```
**字节码分析**
注意：字节码文件中并没有进行优化，可以看到加锁和释放锁的操作依然存在，**同步省略操作是在解释运行时发生的**
### 标量替换
**分离对象或标量替换**

1. 标量（scalar）是指一个无法再分解成更小的数据的数据。Java中的原始数据类型就是标量。
2. 相对的，那些还可以分解的数据叫做聚合量（Aggregate），Java中的对象就是聚合量，因为他可以分解成其他聚合量和标量。
3. 在JIT阶段，如果经过逃逸分析，发现一个对象不会被外界访问的话，那么经过JIT优化，就会把这个对象拆解成若干个其中包含的若干个成员变量来代替。这个过程就是标量替换。

**标量替换举例**
代码
```java
public static void main(String args[]) {
    alloc();
}
private static void alloc() {
    Point point = new Point(1,2);
    System.out.println("point.x" + point.x + ";point.y" + point.y);
}
class Point {
    private int x;
    private int y;
}
```
以上代码，经过标量替换后，就会变成
```java
private static void alloc() {
    int x = 1;
    int y = 2;
    System.out.println("point.x = " + x + "; point.y=" + y);
}
```

1. 可以看到，Point这个聚合量经过逃逸分析后，发现他并没有逃逸，就被替换成两个聚合量了。
2. 那么标量替换有什么好处呢？就是可以大大减少堆内存的占用。因为一旦不需要创建对象了，那么就不再需要分配堆内存了。
3. 标量替换为栈上分配提供了很好的基础。

**标量替换参数设置**
参数 -XX:+ElimilnateAllocations：开启了标量替换（默认打开），允许将对象打散分配在栈上。
**代码示例**
```java
/**
 * 标量替换测试
 *  -Xmx100m -Xms100m -XX:+DoEscapeAnalysis -XX:+PrintGC -XX:-EliminateAllocations
 * @author shkstart  shkstart@126.com
 * @create 2020  12:01
 */
public class ScalarReplace {
    public static class User {
        public int id;
        public String name;
    }

    public static void alloc() {
        User u = new User();//未发生逃逸
        u.id = 5;
        u.name = "www.atguigu.com";
    }

    public static void main(String[] args) {
        long start = System.currentTimeMillis();
        for (int i = 0; i < 10000000; i++) {
            alloc();
        }
        long end = System.currentTimeMillis();
        System.out.println("花费的时间为： " + (end - start) + " ms");
    }
}
```
**未开启标量替换**
1、JVM 参数
-Xmx100m -Xms100m -XX:+DoEscapeAnalysis -XX:+PrintGC -XX:-EliminateAllocations
2、日志
```bash
[GC (Allocation Failure)  25600K->880K(98304K), 0.0012658 secs]
[GC (Allocation Failure)  26480K->832K(98304K), 0.0012124 secs]
[GC (Allocation Failure)  26432K->784K(98304K), 0.0009719 secs]
[GC (Allocation Failure)  26384K->832K(98304K), 0.0009071 secs]
[GC (Allocation Failure)  26432K->768K(98304K), 0.0010643 secs]
[GC (Allocation Failure)  26368K->824K(101376K), 0.0012354 secs]
[GC (Allocation Failure)  32568K->712K(100864K), 0.0011291 secs]
[GC (Allocation Failure)  32456K->712K(100864K), 0.0006368 secs]
花费的时间为： 99 ms
```
**开启标量替换**
1、JVM 参数
-Xmx100m -Xms100m -XX:+DoEscapeAnalysis -XX:+PrintGC -XX:+EliminateAllocations
2、日志：时间减少很多，且无GC
花费的时间为： 6 ms 
上述代码在主函数中调用了1亿次alloc()方法，进行对象创建由于User对象实例需要占据约16字节的空间，因此累计分配空间达到将近1.5GB。如果堆空间小于这个值，就必然会发生GC。使用如下参数运行上述代码：
-server -Xmx100m -Xms100m -XX:+DoEscapeAnalysis -XX:+PrintGC -XX:+EliminateAllocations
这里设置参数如下：

1. 参数 -server：启动Server模式，因为在server模式下，才可以启用逃逸分析。
2. 参数 -XX:+DoEscapeAnalysis：启用逃逸分析
3. 参数 -Xmx10m：指定了堆空间最大为10MB
4. 参数 -XX:+PrintGC：将打印GC日志。
5. 参数 -XX:+EliminateAllocations：开启了标量替换（默认打开），允许将对象打散分配在栈上，比如对象拥有id和name两个字段，那么这两个字段将会被视为两个独立的局部变量进行分配
### 逃逸分析的不足

1. 关于逃逸分析的论文在1999年就已经发表了，但直到JDK1.6才有实现，而且这项技术到如今也并不是十分成熟的。
2. 其根本原因就是无法保证逃逸分析的性能消耗一定能高于他的消耗。虽然经过逃逸分析可以做标量替换、栈上分配、和锁消除。但是逃逸分析自身也是需要进行一系列复杂的分析的，这其实也是一个相对耗时的过程。
3. 一个极端的例子，就是经过逃逸分析之后，发现没有一个对象是不逃逸的。那这个逃逸分析的过程就白白浪费掉了。
4. 虽然这项技术并不十分成熟，但是它也是即时编译器优化技术中一个十分重要的手段。
5. 注意到有一些观点，认为通过逃逸分析，JVM会在栈上分配那些不会逃逸的对象，这在理论上是可行的，但是取决于JVM设计者的选择。据我所知，**Oracle Hotspot JVM中并未这么做**（刚刚演示的效果，是因为HotSpot实现了标量替换），这一点在逃逸分析相关的文档里已经说明，**所以可以明确在HotSpot虚拟机上，所有的对象实例都是创建在堆上**。
6. 目前很多书籍还是基于JDK7以前的版本，JDK已经发生了很大变化，intern字符串的缓存和静态变量曾经都被分配在永久代上，而永久代已经被元数据区取代。但是**intern字符串缓存和静态变量并不是被转移到元数据区，而是直接在堆上分配**，**所以这一点同样符合前面一点的结论：对象实例都是分配在堆上**。

**堆是分配对象的唯一选择么？**
综上：**对象实例都是分配在堆上**。What the fuck？
## 12、小结

1. 年轻代是对象的诞生、成长、消亡的区域，一个对象在这里产生、应用，最后被垃圾回收器收集、结束生命。
2. 老年代放置长生命周期的对象，通常都是从Survivor区域筛选拷贝过来的Java对象。
3. 当然，也有特殊情况，我们知道普通的对象可能会被分配在TLAB上；
4. 如果对象较大，无法分配在 TLAB 上，则JVM会试图直接分配在Eden其他位置上；
5. 如果对象太大，完全无法在新生代找到足够长的连续空闲空间，JVM就会直接分配到老年代。
6. 当GC只发生在年轻代中，回收年轻代对象的行为被称为Minor GC。
7. 当GC发生在老年代时则被称为Major GC或者Full GC。
8. 一般的，Minor GC的发生频率要比Major GC高很多，即老年代中垃圾回收发生的频率将大大低于年轻代。

# 九、方法区
## 1、概述
### 栈、堆、方法区的交互关系
**从线程共享与否的角度来看**
ThreadLocal：如何保证多个线程在并发环境下的安全性？典型场景就是数据库连接管理，以及会话管理。
![](image/1664065384337-183769b5-5829-4a61-9f8d-3d6150e42dbf.png)
**栈、堆、方法区的交互关系**
**下面涉及了对象的访问定位**

1. Person 类的 .class 信息存放在方法区中
2. person 变量存放在 Java 栈的局部变量表中
3. 真正的 person 对象存放在 Java 堆中
4. 在 person 对象中，有个指针指向方法区中的 person 类型数据，表明这个 person 对象是用方法区中的 Person 类 new 出来的

![](image/1664065384114-5a045720-9f11-4017-be00-f1d9016b89ad.png)
方法区的理解
**官方文档**：[https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-2.html#jvms-2.5.4](https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-2.html#jvms-2.5.4)

### 方法区在哪里？

1. 《Java虚拟机规范》中明确说明：尽管所有的方法区在逻辑上是属于堆的一部分，但一些简单的实现可能不会选择去进行垃圾收集或者进行压缩。但对于HotSpotJVM而言，方法区还有一个别名叫做Non-Heap（非堆），目的就是要和堆分开。
2. 所以，**方法区可以看作是一块独立于Java堆的内存空间**。

![](image/1664065385446-d03790c0-5d64-4a3e-a479-6c81a41c87b8.png)
### 方法区的基本理解
**方法区主要存放的是 Class，而堆中主要存放的是实例化的对象**

1. 方法区（Method Area）与Java堆一样，是各个线程共享的内存区域。多个线程同时加载统一个类时，只能有一个线程能加载该类，其他线程只能等等待该线程加载完毕，然后直接使用该类，即类只能加载一次。
2. 方法区在JVM启动的时候被创建，并且它的实际的物理内存空间中和Java堆区一样都可以是不连续的。
3. 方法区的大小，跟堆空间一样，可以选择固定大小或者可扩展。
4. 方法区的大小决定了系统可以保存多少个类，如果系统定义了太多的类，导致方法区溢出，虚拟机同样会抛出内存溢出错误：java.lang.OutofMemoryError:PermGen space 或者 java.lang.OutOfMemoryError:Metaspace
   - 加载大量的第三方的jar包
   - Tomcat部署的工程过多（30~50个）
   - 大量动态的生成反射类
5. 关闭JVM就会释放这个区域的内存。

**代码举例**
```java
public class MethodAreaDemo {
    public static void main(String[] args) {
        System.out.println("start...");
        try {
            Thread.sleep(1000000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("end...");
    }
}
```
简单的程序，加载了1600多个类
![](image/1664065384610-06ccba43-f5de-4055-a66a-0752656bdbb0.png)
### HotSpot方法区演进

1. 在 JDK7 及以前，习惯上把方法区，称为永久代。JDK8开始，使用元空间取代了永久代。我们可以将方法区类比为Java中的接口，将永久代或元空间类比为Java中具体的实现类
2. 本质上，方法区和永久代并不等价。仅是对Hotspot而言的可以看作等价。《Java虚拟机规范》对如何实现方法区，不做统一要求。例如：BEAJRockit / IBM J9 中不存在永久代的概念。
   - 现在来看，当年使用永久代，不是好的idea。导致Java程序更容易OOM（超过-XX:MaxPermsize上限）
3. 而到了JDK8，终于完全废弃了永久代的概念，改用与JRockit、J9一样在本地内存中实现的元空间（Metaspace）来代替
4. 元空间的本质和永久代类似，都是对JVM规范中方法区的实现。不过元空间与永久代最大的区别在于：
   - **元空间不在虚拟机设置的内存中，而是使用本地内存**。
5. 永久代、元空间二者并不只是名字变了，内部结构也调整了
6. 根据《Java虚拟机规范》的规定，如果方法区无法满足新的内存分配需求时，将抛出OOM异常

![](image/1664065385616-070564d1-20a5-4724-a631-d475ed4f91b0.png)
## 2、大小设置与 OOM
方法区的大小不必是固定的，JVM可以根据应用的需要动态调整。
### JDK7及以前(永久代)

1. 通过-XX:Permsize来设置永久代初始分配空间。默认值是20.75M
2. -XX:MaxPermsize来设定永久代最大可分配空间。32位机器默认是64M，64位机器模式是82M
3. 当JVM加载的类信息容量超过了这个值，会报异常OutofMemoryError:PermGen space。

![](image/1664065386031-37073f48-0fab-4908-9588-7b0799efc818.png)
### JDK8及以后(元空间)
**JDK8 版本设置元空间大小**

1. 元数据区大小可以使用参数 **-XX:MetaspaceSize** 和 **-XX:MaxMetaspaceSize** 指定
2. 默认值依赖于平台，Windows下，-XX:MetaspaceSize 约为21M，-XX:MaxMetaspaceSize的值是-1，即没有限制。
3. 与永久代不同，如果不指定大小，默认情况下，虚拟机会耗尽所有的可用系统内存。如果元数据区发生溢出，虚拟机一样会抛出异常OutOfMemoryError:Metaspace
4. -XX:MetaspaceSize：设置初始的元空间大小。对于一个 64位 的服务器端 JVM 来说，其默认的 -XX:MetaspaceSize值为21MB。这就是初始的高水位线，一旦触及这个水位线，Full GC将会被触发并卸载没用的类（即这些类对应的类加载器不再存活），然后这个高水位线将会重置。新的高水位线的值取决于GC后释放了多少元空间。如果释放的空间不足，那么在不超过MaxMetaspaceSize时，适当提高该值。如果释放空间过多，则适当降低该值。
5. 如果初始化的高水位线设置过低，上述高水位线调整情况会发生很多次。通过垃圾回收器的日志可以观察到Full GC多次调用。为了避免频繁地GC，建议将-XX:MetaspaceSize设置为一个相对较高的值。
### 方法区OOM
举例：
代码：OOMTest 类继承 ClassLoader 类，获得 defineClass() 方法，可自己进行类的加载
```java
/**
 * jdk6/7中：
 * -XX:PermSize=10m -XX:MaxPermSize=10m
 *
 * jdk8中：
 * -XX:MetaspaceSize=10m -XX:MaxMetaspaceSize=10m
 *
 */
public class OOMTest extends ClassLoader {
    public static void main(String[] args) {
        int j = 0;
        try {
            OOMTest test = new OOMTest();
            for (int i = 0; i < 10000; i++) {
                //创建ClassWriter对象，用于生成类的二进制字节码
                ClassWriter classWriter = new ClassWriter(0);
                //指明版本号，修饰符，类名，包名，父类，接口
                classWriter.visit(Opcodes.V1_8, Opcodes.ACC_PUBLIC, "Class" + i, null, "java/lang/Object", null);
                //返回byte[]
                byte[] code = classWriter.toByteArray();
                //类的加载
                test.defineClass("Class" + i, code, 0, code.length);//Class对象
                j++;
            }
        } finally {
            System.out.println(j);
        }
    }
}

```
**不设置元空间的上限**
使用默认的 JVM 参数，元空间不设置上限
输出结果：
10000
**设置元空间的上限**
JVM 参数
-XX:MetaspaceSize=10m -XX:MaxMetaspaceSize=10m
输出结果：
```bash
3331
Exception in thread "main" java.lang.OutOfMemoryError: Compressed class space
	at java.lang.ClassLoader.defineClass1(Native Method)
	at java.lang.ClassLoader.defineClass(ClassLoader.java:756)
	at java.lang.ClassLoader.defineClass(ClassLoader.java:635)
	at com.renchao.java.OOMTest.main(OOMTest.java:27)
```
### 如何解决OOM
这个属于调优的问题，这里先简单的说一下

1. 要解决OOM异常或heap space的异常，一般的手段是首先通过内存映像分析工具（如Ec1ipse Memory Analyzer）对dump出来的堆转储快照进行分析，重点是确认内存中的对象是否是必要的，也就是要先分清楚到底是出现了内存泄漏（Memory Leak）还是内存溢出（Memory Overflow）
2. **内存泄漏**就是有大量的引用指向某些对象，但是这些对象以后不会使用了，但是因为它们还和GC ROOT有关联，所以导致以后这些对象也不会被回收，这就是内存泄漏的问题
3. 如果是内存泄漏，可进一步通过工具查看泄漏对象到GC Roots的引用链。于是就能找到泄漏对象是通过怎样的路径与GC Roots相关联并导致垃圾收集器无法自动回收它们的。掌握了泄漏对象的类型信息，以及GC Roots引用链的信息，就可以比较准确地定位出泄漏代码的位置。
4. 如果不存在内存泄漏，换句话说就是内存中的对象确实都还必须存活着，那就应当检查虚拟机的堆参数（-Xmx与-Xms），与机器物理内存对比看是否还可以调大，从代码上检查是否存在某些对象生命周期过长、持有状态时间过长的情况，尝试减少程序运行期的内存消耗。
## 3、内部结构
### 方法区存储什么？
![](image/1664065386780-b839fba5-df14-4293-82c1-b6bb6a60bbb1.png)
《深入理解Java虚拟机》书中对方法区（Method Area）存储内容描述如下：
它用于存储已被虚拟机加载的**类型信息、常量、静态变量、即时编译器编译后的代码缓存**等。
![](image/1664065387198-9720cf94-784d-4091-84a2-4c58d68aff96.png)

> 静态变量（引用地址）在JDK1.7以后，移到堆中。

### 类型信息
对每个加载的类型（类class、接口interface、枚举enum、注解annotation），JVM必须在方法区中存储以下类型信息：

1. 这个类型的完整有效名称（全名=包名.类名）
2. 这个类型直接父类的完整有效名（对于interface或是java.lang.Object，都没有父类）
3. 这个类型的修饰符（public，abstract，final的某个子集）
4. 这个类型直接接口的一个有序列表
### 域（Field）信息
也就是我们常说的成员变量，域信息是比较官方的称呼

1. JVM必须在方法区中保存类型的所有域的相关信息以及域的声明顺序。
2. 域的相关信息包括：域名称，域类型，域修饰符（public，private，protected，static，final，volatile，transient的某个子集）
### 方法（Method）信息
JVM必须保存所有方法的以下信息，同域信息一样包括声明顺序：

1. 方法名称
2. 方法的返回类型（包括 void 返回类型），void 在 Java 中对应的为 void.class
3. 方法参数的数量和类型（按顺序）
4. 方法的修饰符（public，private，protected，static，final，synchronized，native，abstract的一个子集）
5. 方法的字节码（bytecodes）、操作数栈、局部变量表及大小（abstract和native方法除外）
6. 异常表（abstract和native方法除外），异常表记录每个异常处理的开始位置、结束位置、代码处理在程序计数器中的偏移地址、被捕获的异常类的常量池索引
```java
**
 * 测试方法区的内部构成
 */
public class MethodInnerStrucTest extends Object implements Comparable<String>,Serializable {
    //属性
    public int num = 10;
    private static String str = "测试方法的内部结构";
    //构造器
    //方法
    public void test1(){
        int count = 20;
        System.out.println("count = " + count);
    }
    public static int test2(int cal){
        int result = 0;
        try {
            int value = 30;
            result = value / cal;
        } catch (Exception e) {
            e.printStackTrace();
        }
        return result;
    }

    @Override
    public int compareTo(String o) {
        return 0;
    }
}

```
javap -v -p MethodInnerStrucTest.class > test.txt

- 反编译字节码文件，并输出值文本文件中，便于查看。参数 -p 确保能查看 private 权限类型的字段或方法

### 类信息
在运行时方法区中，类信息中记录了哪个加载器加载了该类，同时类加载器也记录了它加载了哪些类
```java
//类信息      
public class com.atguigu.java.MethodInnerStrucTest extends java.lang.Object implements java.lang.Comparable<java.lang.String>, java.io.Serializable
```
### 域信息

1. descriptor: I 表示字段类型为 Integer
2. flags: ACC_PUBLIC 表示字段权限修饰符为 public
```java
//域信息
  public int num;
    descriptor: I
    flags: ACC_PUBLIC

  private static java.lang.String str;
    descriptor: Ljava/lang/String;
    flags: ACC_PRIVATE, ACC_STATIC
```
### 方法信息

1. descriptor: ()V 表示方法返回值类型为 void
2. flags: ACC_PUBLIC 表示方法权限修饰符为 public
3. stack=3 表示操作数栈深度为 3
4. locals=2 表示局部变量个数为 2 个（实力方法包含 this）
5. test1() 方法虽然没有参数，但是其 args_size=1 ，这时因为将 this 作为了参数
```bash
public void test1();
    descriptor: ()V
    flags: ACC_PUBLIC
    Code:
      stack=3, locals=2, args_size=1
         0: bipush        20
         2: istore_1
         3: getstatic     #3                  // Field java/lang/System.out:Ljava/io/PrintStream;
         6: new           #4                  // class java/lang/StringBuilder
         9: dup
        10: invokespecial #5                  // Method java/lang/StringBuilder."<init>":()V
        13: ldc           #6                  // String count =
        15: invokevirtual #7                  // Method java/lang/StringBuilder.append:(Ljava/lang/String;)Ljava/lang/StringBuilder;
        18: iload_1
        19: invokevirtual #8                  // Method java/lang/StringBuilder.append:(I)Ljava/lang/StringBuilder;
        22: invokevirtual #9                  // Method java/lang/StringBuilder.toString:()Ljava/lang/String;
        25: invokevirtual #10                 // Method java/io/PrintStream.println:(Ljava/lang/String;)V
        28: return
      LineNumberTable:
        line 17: 0
        line 18: 3
        line 19: 28
      LocalVariableTable:
        Start  Length  Slot  Name   Signature
            0      29     0  this   Lcom/atguigu/java/MethodInnerStrucTest;
            3      26     1 count   I

```
### non-final 类型的类变量

1. 静态变量和类关联在一起，随着类的加载而加载，他们成为类数据在逻辑上的一部分
2. 类变量被类的所有实例共享，即使没有类实例时，你也可以访问它

**举例**

1. 如下代码所示，即使我们把order设置为null，也不会出现空指针异常
2. 这更加表明了 static 类型的字段和方法随着类的加载而加载，并不属于特定的类实例
```java
public class MethodAreaTest {
    public static void main(String[] args) {
        Order order = null;
        order.hello();
        System.out.println(order.count);
    }
}

class Order {
    public static int count = 1;
    public static final int number = 2;


    public static void hello() {
        System.out.println("hello!");
    }
}
```
输出结果：
hello! 1 
**全局常量：static final**

1. 全局常量就是使用 static final 进行修饰
2. 被声明为final的类变量的处理方法则不同，每个全局常量在编译的时候就会被分配了。
3. 可以在类不加载的情况下访问 static final 修饰的常量。

查看上面代码，这部分的字节码指令
```java
class Order {
    public static int count = 1;
    public static final int number = 2;
    ...
}    
```
```bash
public static int count;
    descriptor: I
    flags: ACC_PUBLIC, ACC_STATIC

  public static final int number;
    descriptor: I
    flags: ACC_PUBLIC, ACC_STATIC, ACC_FINAL
    ConstantValue: int 2
```
可以发现 staitc和final同时修饰的number 的值在编译上的时候已经写死在字节码文件中了。
### 运行时常量池
**运行时常量池 VS 常量池**
**官方文档**：[https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-4.html](https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-4.html)
后面会细讲常量池，这里为了讲清楚方法区，简单带一下。
![](image/1664065387656-62fec585-8221-4a9d-b1f0-c42ead4b88e2.png)

1. 方法区，内部包含了运行时常量池
2. 字节码文件，内部包含了常量池。（之前的字节码文件中已经看到了很多Constant pool的东西，这个就是常量池）
3. 要弄清楚方法区，需要理解清楚ClassFile，因为加载类的信息都在方法区。
4. 要弄清楚方法区的运行时常量池，需要理解清楚ClassFile中的常量池。

**常量池**

1. 一个有效的字节码文件中除了包含类的版本信息、字段、方法以及接口等描述符信息外。还包含一项信息就是**常量池表**（**Constant Pool Table**），包括各种字面量和对类型、域和方法的符号引用。
2. 字面量： 10 ， “我是某某”这种数字和字符串都是字面量

![](image/1664065388361-244fb58b-aa65-4085-9537-cbc2a58b9d6f.png)
**为什么需要常量池？**

1. 一个java源文件中的类、接口，编译后产生一个字节码文件。而Java中的字节码需要数据支持，通常这种数据会很大以至于不能直接存到字节码里，换另一种方式，可以存到常量池。这个字节码包含了指向常量池的引用。在动态链接的时候会用到运行时常量池，之前有介绍

比如：如下的代码：
```java
public class SimpleClass {
    public void sayHello() {
        System.out.println("hello");
    }
}
```

1. 虽然上述代码只有194字节，但是里面却使用了String、System、PrintStream及Object等结构。
2. 比如说我们这个文件中有6个地方用到了"hello"这个字符串，如果不用常量池，就需要在6个地方全写一遍，造成臃肿。我们可以将"hello"等所需用到的结构信息记录在常量池中，并通过**引用的方式**，来加载、调用所需的结构
3. 这里的代码量其实很少了，如果代码多的话，引用的结构将会更多，这里就需要用到常量池了。

![](image/1664065388910-a44d7fcc-25b4-4e7a-b826-132593ab67b4.png)
**常量池中有啥？**

1. 数量值
2. 字符串值
3. 类引用
4. 字段引用
5. 方法引用

MethodInnerStrucTest 的 test1方法的字节码
```bash
 0 bipush 20
 2 istore_1
 3 getstatic #3 <java/lang/System.out>
 6 new #4 <java/lang/StringBuilder>
 9 dup
10 invokespecial #5 <java/lang/StringBuilder.<init>>
13 ldc #6 <count = >
15 invokevirtual #7 <java/lang/StringBuilder.append>
18 iload_1
19 invokevirtual #8 <java/lang/StringBuilder.append>
22 invokevirtual #9 <java/lang/StringBuilder.toString>
25 invokevirtual #10 <java/io/PrintStream.println>
28 return
```
1、#3，#5等等这些带# 的，都是引用了常量池。
**常量池总结**
常量池、可以看做是一张表，虚拟机指令根据这张常量表找到要执行的类名、方法名、参数类型、字面量等类型。

1. 运行时常量池（Runtime Constant Pool）是方法区的一部分。
2. 常量池表（Constant Pool Table）是Class字节码文件的一部分，用于存放编译期生成的各种字面量与符号引用，**这部分内容将在类加载后存放到方法区的运行时常量池中**。（运行时常量池就是常量池在程序运行时的称呼）
3. 运行时常量池，在加载类和接口到虚拟机后，就会创建对应的运行时常量池。
4. JVM为每个已加载的类型（类或接口）都维护一个常量池。池中的数据项像数组项一样，是通过索引访问的。
5. 运行时常量池中包含多种不同的常量，包括编译期就已经明确的数值字面量，也包括到运行期解析后才能够获得的方法或者字段引用。**此时不再是常量池中的符号地址了，这里换为真实地址**。
- 运行时常量池，相对于Class文件常量池的另一重要特征是：具备动态性。
1. 运行时常量池类似于传统编程语言中的符号表（symbol table），但是它所包含的数据却比符号表要更加丰富一些。
2. 当创建类或接口的运行时常量池时，如果构造运行时常量池所需的内存空间超过了方法区所能提供的最大值，则JVM会抛OutofMemoryError异常。
## 4、举例说明
```java
public class MethodAreaDemo {
    public static void main(String[] args) {
        int x = 500;
        int y = 100;
        int a = x / y;
        int b = 50;
        System.out.println(a + b);
    }
}
```
字节码
```bash
public class com.atguigu.java1.MethodAreaDemo
  minor version: 0
  major version: 51
  flags: ACC_PUBLIC, ACC_SUPER
Constant pool:
   #1 = Methodref          #5.#24         // java/lang/Object."<init>":()V
   #2 = Fieldref           #25.#26        // java/lang/System.out:Ljava/io/PrintStream;
   #3 = Methodref          #27.#28        // java/io/PrintStream.println:(I)V
   #4 = Class              #29            // com/atguigu/java1/MethodAreaDemo
   #5 = Class              #30            // java/lang/Object
   #6 = Utf8               <init>
   #7 = Utf8               ()V
   #8 = Utf8               Code
   #9 = Utf8               LineNumberTable
  #10 = Utf8               LocalVariableTable
  #11 = Utf8               this
  #12 = Utf8               Lcom/atguigu/java1/MethodAreaDemo;
  #13 = Utf8               main
  #14 = Utf8               ([Ljava/lang/String;)V
  #15 = Utf8               args
  #16 = Utf8               [Ljava/lang/String;
  #17 = Utf8               x
  #18 = Utf8               I
  #19 = Utf8               y
  #20 = Utf8               a
  #21 = Utf8               b
  #22 = Utf8               SourceFile
  #23 = Utf8               MethodAreaDemo.java
  #24 = NameAndType        #6:#7          // "<init>":()V
  #25 = Class              #31            // java/lang/System
  #26 = NameAndType        #32:#33        // out:Ljava/io/PrintStream;
  #27 = Class              #34            // java/io/PrintStream
  #28 = NameAndType        #35:#36        // println:(I)V
  #29 = Utf8               com/atguigu/java1/MethodAreaDemo
  #30 = Utf8               java/lang/Object
  #31 = Utf8               java/lang/System
  #32 = Utf8               out
  #33 = Utf8               Ljava/io/PrintStream;
  #34 = Utf8               java/io/PrintStream
  #35 = Utf8               println
  #36 = Utf8               (I)V
{
  public com.atguigu.java1.MethodAreaDemo();
    descriptor: ()V
    flags: ACC_PUBLIC
    Code:
      stack=1, locals=1, args_size=1
         0: aload_0
         1: invokespecial #1                  // Method java/lang/Object."<init>":()V
         4: return
      LineNumberTable:
        line 7: 0
      LocalVariableTable:
        Start  Length  Slot  Name   Signature
            0       5     0  this   Lcom/atguigu/java1/MethodAreaDemo;

  public static void main(java.lang.String[]);
    descriptor: ([Ljava/lang/String;)V
    flags: ACC_PUBLIC, ACC_STATIC
    Code:
      stack=3, locals=5, args_size=1
         0: sipush        500
         3: istore_1
         4: bipush        100
         6: istore_2
         7: iload_1
         8: iload_2
         9: idiv
        10: istore_3
        11: bipush        50
        13: istore        4
        15: getstatic     #2                  // Field java/lang/System.out:Ljava/io/PrintStream;
        18: iload_3
        19: iload         4
        21: iadd
        22: invokevirtual #3                  // Method java/io/PrintStream.println:(I)V
        25: return
      LineNumberTable:
        line 9: 0
        line 10: 4
        line 11: 7
        line 12: 11
        line 13: 15
        line 14: 25
      LocalVariableTable:
        Start  Length  Slot  Name   Signature
            0      26     0  args   [Ljava/lang/String;
            4      22     1     x   I
            7      19     2     y   I
           11      15     3     a   I
           15      11     4     b   I
}
SourceFile: "MethodAreaDemo.java"

```
**图解字节码指令执行流程：**
1、初始状态
![](image/1664065392209-cc2f9587-11dd-4304-ab96-8e121492d9e5.png)
2、首先将操作数500压入操作数栈中
![](image/1664065390635-0b335de7-19a8-4f32-903e-be4bce67b1f3.png)
3、然后操作数 500 从操作数栈中取出，存储到局部变量表中索引为 1 的位置
![](image/1664065389871-af019722-a88c-4aac-ab96-85577604f92f.png)
4、
![](image/1664065391193-9a71ad54-a6e4-41e2-9f00-e8ee0501ef74.png)
5、
![](image/1664065392533-22bbe6bc-e92a-4e02-ad3c-9b0b54bcc7f4.png)
6、
![](image/1664065393247-0fd3e77d-c78b-4326-9a1c-775eab2b0fb4.png)
7、
![](image/1664065393867-95f7e861-0680-40ac-b80e-48d0e0a39611.png)
8、
![](image/1664065394931-44f6a54e-6900-4095-af4e-a2f9fe207104.png)
9、
![](image/1664065397310-5afe3738-162f-446b-bb3b-8c39f36cc134.png)
10、
![](image/1664065399065-d8fc0b5e-262b-42e1-9854-99dd830a3164.png)
11、图片写错了是#25和#26（获得System类）
![](image/1664065399020-a2c62842-8707-4343-8d5f-9d9e484eb7ea.png)
12、
![](image/1664065400148-32ededd7-c17a-4506-a739-fe5069ca8d8f.png)
13、
![](image/1664065401409-916ca8b2-5851-4802-aec5-b86002952b65.png)
15、执行加法运算后，将计算结果放在操作数栈顶
![](image/1664065401903-ab3f8fb7-8793-4586-ba00-9d5e08f799c3.png)
16、就是真正的打印
![](image/1664065403712-8eb79ee5-89b1-44ca-b279-bbfe8afa1fbf.png)
17、
![](image/1664065402564-ec6a92ff-0b27-49fb-9273-41729cd7cde8.png)
**符号引用 --> 直接引用**

1. 上面代码调用 System.out.println() 方法时，首先需要看看 System 类有没有加载，再看看 PrintStream 类有没有加载
2. 如果没有加载，则执行加载，执行时，将常量池中的符号引用（字面量）转换为运行时常量池的直接引用（真正的地址值）
## 5、演进细节
### 永久代演进过程

1. 首先明确：只有Hotspot才有永久代。BEA JRockit、IBMJ9等来说，是不存在永久代的概念的。原则上如何实现方法区属于虚拟机实现细节，不受《Java虚拟机规范》管束，并不要求统一
2. Hotspot中方法区的变化：
| **JDK1.6及以前** | **有永久代（permanent generation），静态变量存储在永久代上** |
| ---------------- | ------------------------------------------------------------ |
| JDK1.7           | 有永久代，但已经逐步 “去永久代”，**字符串常量池，静态变量移除，保存在堆中** |
| JDK1.8           | 无永久代，类型信息，字段，方法，常量保存在本地内存的元空间，但字符串常量池、静态变量仍然在堆中。 |

**JDK6**
方法区由永久代实现，使用 JVM 虚拟机内存（虚拟的内存）
![](image/1664065407461-f4fb271a-ca7e-409b-82c3-358cfcf64e18.png)
**JDK7**
方法区由永久代实现，使用 JVM 虚拟机内存
![](image/1664065407244-22bff3e8-6087-4695-af57-5e804575b832.png)
**JDK8**
方法区由元空间实现，使用物理机本地内存
![](image/1664065410899-0161c7c2-d75d-4402-a39c-8b0cf28a7477.png)
> 这里的静态变量指的是 变量的引用地址。变量的对象始终都是在堆中的。

### 为什么被元空间替代？
**官方文档**：[http://openjdk.java.net/jeps/122](http://openjdk.java.net/jeps/122)

1. 随着Java8的到来，HotSpot VM中再也见不到永久代了。但是这并不意味着类的元数据信息也消失了。这些数据被移到了一个与堆不相连的本地内存区域，这个区域叫做元空间（Metaspace）。
2. 由于类的元数据分配在本地内存中，元空间的最大可分配空间就是系统可用内存空间。
3. 这项改动是很有必要的，原因有：
   1. 为永久代设置空间大小是很难确定的。在某些场景下，如果动态加载类过多，容易产生Perm区的OOM。比如某个实际Web工程中，因为功能点比较多，在运行过程中，要不断动态加载很多类，经常出现致命错误。Exception in thread 'dubbo client x.x connector' java.lang.OutOfMemoryError:PermGen space而元空间和永久代之间最大的区别在于：元空间并不在虚拟机中，而是使用本地内存。 因此，默认情况下，元空间的大小仅受本地内存限制。
   2. 对永久代进行调优是很困难的。方法区的垃圾收集主要回收两部分内容：常量池中废弃的常量和不再用的类型，方法区的调优主要是为了降低**Full GC**
      1. 有些人认为方法区（如HotSpot虚拟机中的元空间或者永久代）是没有垃圾收集行为的，其实不然。《Java虚拟机规范》对方法区的约束是非常宽松的，提到过可以不要求虚拟机在方法区中实现垃圾收集。事实上也确实有未实现或未能完整实现方法区类型卸载的收集器存在（如JDK11时期的ZGC收集器就不支持类卸载）。
      2. 一般来说这个区域的回收效果比较难令人满意，尤其是类型的卸载，条件相当苛刻。但是这部分区域的回收有时又确实是必要的。以前Sun公司的Bug列表中，曾出现过的若干个严重的Bug就是由于低版本的HotSpot虚拟机对此区域未完全回收而导致内存泄漏。
### 字符串常量池
**字符串常量池 StringTable 为什么要调整位置？**

- JDK7中将StringTable放到了堆空间中。因为永久代的回收效率很低，在Full GC的时候才会执行永久代的垃圾回收，而Full GC是老年代的空间不足、永久代不足时才会触发。
- 这就导致StringTable回收效率不高，而我们开发中会有大量的字符串被创建，回收效率低，导致永久代内存不足。放到堆里，能及时回收内存。
### 静态变量放在哪里
#### 对象实体在哪里放着？
```java
/**
 * 结论：
 * 1、静态引用对应的对象实体(也就是这个new byte[1024 * 1024 * 100])始终都存在堆空间，
 * 2、只是那个变量(相当于下面的arr变量名)在JDK6,JDK7,JDK8存放位置中有所变化
 *
 * jdk7：
 * -Xms200m -Xmx200m -XX:PermSize=300m -XX:MaxPermSize=300m -XX:+PrintGCDetails
 * jdk 8：
 * -Xms200m -Xmx200m -XX:MetaspaceSize=300m -XX:MaxMetaspaceSize=300m -XX:+PrintGCDetails
 */
public class StaticFieldTest {
    private static byte[] arr = new byte[1024 * 1024 * 100];//100MB

    public static void main(String[] args) {
        System.out.println(StaticFieldTest.arr);
    }
}
```
JDK6环境下
![](image/1664065407958-eac9a9bf-c49c-4912-800d-723baf3c1dcd.png)

JDK7环境下
![image.png](image/1664250933590-bcca6dd7-1fb7-4533-8ff7-7f2856912c9e.png)

JDK8环境
![](image/1664065408409-e5698214-49c1-492e-b5f2-bbe06fdff66a.png)

#### 变量(名)存放在哪里？
> jdk1.6及以前，变量名存放在方法区。
> jdk1.7及以后，变量名存放在堆中。

这个问题需要用JHSDB工具来进行分析，这个工具是JDK9开始自带的(JDK9以前没有)，在bin目录下可以找到
```java
package com.atguigu.java1;

/**
 * 《深入理解Java虚拟机》中的案例：
 * staticObj、instanceObj、localObj存放在哪里？
 */
public class StaticObjTest {
    static class Test {
        static ObjectHolder staticObj = new ObjectHolder();
        ObjectHolder instanceObj = new ObjectHolder();

        void foo() {
            ObjectHolder localObj = new ObjectHolder();
            System.out.println("done");
        }
    }

    private static class ObjectHolder {
    }

    public static void main(String[] args) {
        Test test = new StaticObjTest.Test();
        test.foo();
    }
}

```
**JDK6环境下**
1、staticObj随着Test的类型信息存放在方法区
2、instanceObj随着Test的对象实例存放在Java堆
3、localObject则是存放在foo()方法栈帧的局部变量表中。
4、测试发现：三个对象的数据在内存中的地址都落在Eden区范围内，所以结论：**只要是对象实例必然会在Java堆中分配**。
![](image/1664065410849-2801e012-8271-4b3d-a763-270b8613c344.png)
1、0x00007f32c7800000(Eden区的起始地址) ---- 0x00007f32c7b50000(Eden区的终止地址)
2、可以发现三个变量都在这个范围内
3、所以可以得到上面结论
5、接着，找到了一个引用该staticObj对象的地方，是在一个java.lang.Class的实例里，并且给出了这个实例的地址，通过Inspector查看该对象实例，可以清楚看到这确实是一个java.lang.Class类型的对象实例，里面有一个名为staticobj的实例字段：
![](image/1664065409880-0a4b438b-9b06-48a8-b6f1-0901bafda3b0.png)
从《Java虚拟机规范》所定义的概念模型来看，所有Class相关的信息都应该存放在方法区之中，但方法区该如何实现，《Java虚拟机规范》并未做出规定，这就成了一件允许不同虚拟机自己灵活把握的事情。JDK7及其以后版本的HotSpot虚拟机选择把静态变量与类型在Java语言一端的映射Class对象存放在一起，**存储于Java堆之中**，从我们的实验中也明确验证了这一点
## 6、方法区垃圾回收

1. 有些人认为方法区（如Hotspot虚拟机中的元空间或者永久代）是没有垃圾收集行为的，其实不然。《Java虚拟机规范》对方法区的约束是非常宽松的，提到过可以不要求虚拟机在方法区中实现垃圾收集。事实上也确实有未实现或未能完整实现方法区**类型卸载**的收集器存在（如JDK11时期的ZGC收集器就不支持类卸载）。
2. 一般来说这个区域的回收效果比较难令人满意，尤其是类型的卸载，条件相当苛刻。但是这部分区域的回收有时又确实是必要的。以前sun公司的Bug列表中，曾出现过的若干个严重的Bug就是由于低版本的HotSpot虚拟机对此区域未完全回收而导致内存泄漏。
3. 方法区的垃圾收集主要回收两部分内容：**常量池中废弃的常量和不再使用的类型**。
4. 先来说说方法区内常量池之中主要存放的两大类常量：字面量和符号引用。字面量比较接近Java语言层次的常量概念，如文本字符串、被声明为final的常量值等。而符号引用则属于编译原理方面的概念，包括下面三类常量：
   - 类和接口的全限定名
   - 字段的名称和描述符
   - 方法的名称和描述符
5. HotSpot虚拟机对常量池的回收策略是很明确的，只要常量池中的常量没有被任何地方引用，就可以被回收。
6. 回收废弃常量与回收Java堆中的对象非常类似。（关于常量的回收比较简单，重点是类的回收）

下面也称作**类卸载**
1、判定一个常量是否“废弃”还是相对简单，而要判定一个类型是否属于“不再被使用的类”的条件就比较苛刻了。需要同时满足下面三个条件：

- 该类所有的实例都已经被回收，也就是Java堆中不存在该类及其任何派生子类的实例。
- 加载该类的类加载器已经被回收，这个条件除非是经过精心设计的可替换类加载器的场景，如OSGi、JSP的重加载等，否则通常是很难达成的。
- 该类对应的java.lang.Class对象没有在任何地方被引用，无法在任何地方通过反射访问该类的方法。

2、Java虚拟机被允许对满足上述三个条件的无用类进行回收，这里说的仅仅是“被允许”，而并不是和对象一样，没有引用了就必然会回收。关于是否要对类型进行回收，HotSpot虚拟机提供了-Xnoclassgc参数进行控制，还可以使用-verbose:class 以及 -XX：+TraceClass-Loading、-XX：+TraceClassUnLoading查看类加载和卸载信息
3、在大量使用反射、动态代理、CGLib等字节码框架，动态生成JSP以及OSGi这类频繁自定义类加载器的场景中，通常都需要Java虚拟机具备类型卸载的能力，以保证不会对方法区造成过大的内存压力。
## 7、运行时数据区总结
![](image/1664065411387-af9fd5a7-c1b4-4479-aa43-ba30899037f8.png)

# 十、 对象的内存布局与访问定位
## 1、对象的实例化
**大厂面试题**
美团：

1. 对象在JVM中是怎么存储的？
2. 对象头信息里面有哪些东西？

蚂蚁金服：
二面：java对象头里有什么
![](image/1664086816702-2c91d83e-e46d-4067-b80c-b53d4c263bd5.png)
### 对象创建的方式

1. new：最常见的方式、单例类中调用getInstance的静态类方法，XXXFactory的静态方法
2. Class的newInstance方法：在JDK9里面被标记为过时的方法，因为只能调用空参构造器，并且权限必须为 public
3. Constructor的newInstance(Xxxx)：反射的方式，可以调用空参的，或者带参的构造器
4. 使用clone()：不调用任何的构造器，要求当前的类需要实现Cloneable接口中的clone方法
5. 使用序列化：从文件中，从网络中获取一个对象的二进制流，序列化一般用于Socket的网络传输
6. 第三方库 Objenesis
### 对象创建的步骤
**从字节码看待对象的创建过程**
```java
public class ObjectTest {
    public static void main(String[] args) {
        Object obj = new Object();
    }
}
```
```bash
 public static void main(java.lang.String[]);
    descriptor: ([Ljava/lang/String;)V
    flags: ACC_PUBLIC, ACC_STATIC
    Code:
      stack=2, locals=2, args_size=1
         0: new           #2                  // class java/lang/Object
         3: dup           
         4: invokespecial #1                  // Method java/lang/Object."<init>":()V
         7: astore_1
         8: return
      LineNumberTable:
        line 9: 0
        line 10: 8
      LocalVariableTable:
        Start  Length  Slot  Name   Signature
            0       9     0  args   [Ljava/lang/String;
            8       1     1   obj   Ljava/lang/Object;
}
```
**1、判断对象对应的类是否加载、链接、初始化**

1. 虚拟机遇到一条new指令，首先去检查这个指令的参数能否在Metaspace的常量池中定位到一个类的符号引用，并且检查这个符号引用代表的类是否已经被加载，解析和初始化。（即判断类元信息是否存在）。
2. 如果该类没有加载，那么在双亲委派模式下，使用当前类加载器以ClassLoader + 包名 + 类名为key进行查找对应的.class文件，如果没有找到文件，则抛出ClassNotFoundException异常，如果找到，则进行类加载，并生成对应的Class对象。

**2、为对象分配内存**

1. 首先计算对象占用空间的大小，接着在堆中划分一块内存给新对象。如果实例成员变量是引用变量，仅分配引用变量空间即可，即4个字节大小
2. 如果内存规整：采用指针碰撞分配内存
   - 如果内存是规整的，那么虚拟机将采用的是指针碰撞法（Bump The Point）来为对象分配内存。
   - 意思是所有用过的内存在一边，空闲的内存放另外一边，中间放着一个指针作为分界点的指示器，分配内存就仅仅是把指针往空闲内存那边挪动一段与对象大小相等的距离罢了。
   - 如果垃圾收集器选择的是Serial ，ParNew这种基于压缩算法的，虚拟机采用这种分配方式。一般使用带Compact（整理）过程的收集器时，使用指针碰撞。
   - 标记压缩（整理）算法会整理内存碎片，堆内存一存对象，另一边为空闲区域
3. 如果内存不规整
   - 如果内存不是规整的，已使用的内存和未使用的内存相互交错，那么虚拟机将采用的是空闲列表来为对象分配内存。
   - 意思是虚拟机维护了一个列表，记录上哪些内存块是可用的，再分配的时候从列表中找到一块足够大的空间划分给对象实例，并更新列表上的内容。这种分配方式成为了 “空闲列表（Free List）”
   - 选择哪种分配方式由Java堆是否规整所决定，而Java堆是否规整又由所采用的垃圾收集器是否带有压缩整理功能决定
   - 标记清除算法清理过后的堆内存，就会存在很多内存碎片。

**3、处理并发问题**

1. 采用CAS+失败重试保证更新的原子性
2. 每个线程预先分配TLAB - 通过设置 -XX:+UseTLAB参数来设置（区域加锁机制）
3. 在Eden区给每个线程分配一块区域

**4、初始化分配到的空间**

- 所有属性设置默认值，保证对象实例字段在不赋值可以直接使用
- 给对象属性赋值的顺序：
   1. 属性的默认值初始化
   2. 显示初始化/代码块初始化（并列关系，谁先谁后看代码编写的顺序）
   3. 构造器初始化

**5、设置对象的对象头**
将对象的所属类（即类的元数据信息）、对象的HashCode和对象的GC信息、锁信息等数据存储在对象的对象头中。这个过程的具体设置方式取决于JVM实现。
**6、执行init方法进行初始化**

1. 在Java程序的视角看来，初始化才正式开始。初始化成员变量，执行实例化代码块，调用类的构造方法，并把堆内对象的首地址赋值给引用变量
2. 因此一般来说（由字节码中跟随invokespecial指令所决定），new指令之后会接着就是执行init方法，把对象按照程序员的意愿进行初始化，这样一个真正可用的对象才算完成创建出来。

**从字节码角度看 init 方法**
```java
/**
 * 测试对象实例化的过程
 *  ① 加载类元信息 - ② 为对象分配内存 - ③ 处理并发问题  - ④ 属性的默认初始化（零值初始化）
 *  - ⑤ 设置对象头的信息 - ⑥ 属性的显式初始化、代码块中初始化、构造器中初始化
 *
 *
 *  给对象的属性赋值的操作：
 *  ① 属性的默认初始化 - ② 显式初始化 / ③ 代码块中初始化 - ④ 构造器中初始化
 */

public class Customer{
    int id = 1001;
    String name;
    Account acct;

    {
        name = "匿名客户";
    }
    public Customer(){
        acct = new Account();
    }

}
class Account{

}
```
**Customer类的字节码**
```bash
 0 aload_0
 1 invokespecial #1 <java/lang/Object.<init>>
 4 aload_0
 5 sipush 1001
 8 putfield #2 <com/atguigu/java/Customer.id>
11 aload_0
12 ldc #3 <匿名客户>
14 putfield #4 <com/atguigu/java/Customer.name>
17 aload_0
18 new #5 <com/atguigu/java/Account>
21 dup
22 invokespecial #6 <com/atguigu/java/Account.<init>>
25 putfield #7 <com/atguigu/java/Customer.acct>
28 return
```

- init() 方法的字节码指令：
   - 属性的默认值初始化：id = 1001;
   - 显示初始化/代码块初始化：name = "匿名客户";
   - 构造器初始化：acct = new Account();
## 2、对象的内存布局
![image.png](image/1664087333349-614a5a82-dc67-44c6-b7f3-dcb3b7de2577.png)
**内存布局总结**

```java
public class Customer{
    int id = 1001;
    String name;
    Account acct;

    {
        name = "匿名客户";
    }
    public Customer(){
        acct = new Account();
    }
    public static void main(String[] args) {
        Customer cust = new Customer();
    }
}
class Account{

}
```
图解内存布局
![image.png](image/1664087410356-9dfaa29f-2d47-4fb3-8f60-8c68ede8c038.png)

## 3、对象的访问定位
**JVM是如何通过栈帧中的对象引用访问到其内部的对象实例呢？**
![](image/1664086820426-54d4ea45-994e-4c55-a109-adaec49dce61.png)
定位，通过栈上reference访问
**对象的两种访问方式：句柄访问和直接指针**
**1、句柄访问**

1. 缺点：在堆空间中开辟了一块空间作为句柄池，句柄池本身也会占用空间；通过两次指针访问才能访问到堆中的对象，效率低
2. 优点：reference中存储稳定句柄地址，对象被移动（垃圾收集时移动对象很普遍）时只会改变句柄中实例数据指针即可，reference本身不需要被修改

![](image/1664086817520-7740d438-6aef-42e3-842d-3fafd22a6055.png)
**2、直接指针（HotSpot采用）**

1. 优点：直接指针是局部变量表中的引用，直接指向堆中的实例，在对象实例中有类型指针，指向的是方法区中的对象类型数据
2. 缺点：对象被移动（垃圾收集时移动对象很普遍）时需要修改 reference 的值

![image.png](image/1664087585354-53b3f6fb-6621-4255-98b3-72a062008275.png)

# 十一、 直接内存
## 1、概述

1. 不是虚拟机运行时数据区的一部分，也不是《Java虚拟机规范》中定义的内存区域。
2. 直接内存是在Java堆外的、直接向系统申请的内存区间。
3. 来源于NIO，通过存在堆中的DirectByteBuffer操作Native内存
4. 通常，访问直接内存的速度会优于Java堆。即读写性能高。
5. 因此出于性能考虑，读写频繁的场合可能会考虑使用直接内存。
6. Java的NIO库允许Java程序使用直接内存，用于数据缓冲区
```java
/**
 *  IO                  NIO (New IO / Non-Blocking IO)
 *  byte[] / char[]     Buffer
 *  Stream              Channel
 *
 * 查看直接内存的占用与释放
 */
public class BufferTest {
    private static final int BUFFER = 1024 * 1024 * 1024;//1GB

    public static void main(String[] args){
        //直接分配本地内存空间
        ByteBuffer byteBuffer = ByteBuffer.allocateDirect(BUFFER);
        System.out.println("直接内存分配完毕，请求指示！");

        Scanner scanner = new Scanner(System.in);
        scanner.next();

        System.out.println("直接内存开始释放！");
        byteBuffer = null;
        System.gc();
        scanner.next();
    }
}

```
直接占用了 1G 的本地内存
[![](https://cdn.nlark.com/yuque/0/2022/jpeg/26368762/1664065412128-954b6b86-4b7a-4c57-a378-969486164536.jpeg#clientId=u54289ea9-e2c1-4&crop=0&crop=0&crop=1&crop=1&from=paste&id=u6033a325&margin=%5Bobject%20Object%5D&originHeight=641&originWidth=1525&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u26e8a683-3cb1-44f3-abab-f294659536e&title=)](https://camo.githubusercontent.com/18b18046e1ad9c841a6e3cb83e61d41610d7eade97da6a8810200b5833795a1d/68747470733a2f2f6e706d2e656c656d6563646e2e636f6d2f796f7574686c716c40312e302e382f4a564d2f636861707465725f3030362f303033372e6a7067)
## 2、BIO 与 NIO
**非直接缓存区（BIO）**
原来采用BIO的架构，在读写本地文件时，我们需要从用户态切换成内核态
![](image/1664065412209-c982e9ba-6559-47f5-88f0-731f5d23f404.png)
**直接缓冲区（NIO）**
NIO 直接操作物理磁盘，省去了中间过程
![](image/1664065412707-67f32ad1-6700-4e1c-be1b-cb30a4df4d8d.png)
## 3、直接内存与 OOM

1. 直接内存也可能导致OutofMemoryError异常
2. 由于直接内存在Java堆外，因此它的大小不会直接受限于-Xmx指定的最大堆大小，但是系统内存是有限的，Java堆和直接内存的总和依然受限于操作系统能给出的最大内存。
3. 直接内存的缺点为：
   - 分配回收成本较高
   - 不受JVM内存回收管理
4. 直接内存大小可以通过MaxDirectMemorySize设置
5. 如果不指定，默认与堆的最大值-Xmx参数值一致
```java
/**
 * 本地内存的OOM:  OutOfMemoryError: Direct buffer memory
 *
 */
public class BufferTest2 {
    private static final int BUFFER = 1024 * 1024 * 20;//20MB

    public static void main(String[] args) {
        ArrayList<ByteBuffer> list = new ArrayList<>();

        int count = 0;
        try {
            while(true){
                ByteBuffer byteBuffer = ByteBuffer.allocateDirect(BUFFER);
                list.add(byteBuffer);
                count++;
                try {
                    Thread.sleep(100);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        } finally {
            System.out.println(count);
        }


    }
}

```
```bash
Exception in thread "main" java.lang.OutOfMemoryError: Direct buffer memory
	at java.nio.Bits.reserveMemory(Bits.java:694)
	at java.nio.DirectByteBuffer.<init>(DirectByteBuffer.java:123)
	at java.nio.ByteBuffer.allocateDirect(ByteBuffer.java:311)
	at com.atguigu.java.BufferTest2.main(BufferTest2.java:21)
```
[![](https://cdn.nlark.com/yuque/0/2022/jpeg/26368762/1664065413860-3e15264b-6ff7-472b-86fb-89166882df53.jpeg#clientId=u54289ea9-e2c1-4&crop=0&crop=0&crop=1&crop=1&from=paste&id=u83a5774b&margin=%5Bobject%20Object%5D&originHeight=728&originWidth=1268&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u46a42588-6f4a-4a87-970c-9f3dc3804d0&title=)](https://camo.githubusercontent.com/a342edf74fca9fddf59097c436ee684cb128406fe556a9a4ee372a50094fea14/68747470733a2f2f6e706d2e656c656d6563646e2e636f6d2f796f7574686c716c40312e302e382f4a564d2f636861707465725f3030362f303034302e6a7067)
## 常见面试题

1. 百度
   - 三面：说一下JVM内存模型吧，有哪些区？分别干什么的？
2. 蚂蚁金服：
   - Java8的内存分代改进
   - JVM内存分哪几个区，每个区的作用是什么？
   - 一面：JVM内存分布/内存结构？栈和堆的区别？堆的结构？为什么两个survivor区？
   - 二面：Eden和survior的比例分配
3. 小米：
   - jvm内存分区，为什么要有新生代和老年代
4. 字节跳动：
   - 二面：Java的内存分区
   - 二面：讲讲vm运行时数据库区
   - 什么时候对象会进入老年代？
5. 京东：
   - JVM的内存结构，Eden和Survivor比例。
   - JVM内存为什么要分成新生代，老年代，持久代。新生代中为什么要分为Eden和survivor。
6. 天猫：
   - 一面：Jvm内存模型以及分区，需要详细到每个区放什么。
   - 一面：JVM的内存模型，Java8做了什么改
7. 拼多多：
   - JVM内存分哪几个区，每个区的作用是什么？
8. 美团：
   - java内存分配
   - jvm的永久代中会发生垃圾回收吗？
   - 一面：jvm内存分区，为什么要有新生代和老年代？

# 十二、 执行引擎
## 1、概述
![](image/1664087674608-17bb5ca0-090f-4bf1-8b44-1b02e27f7235.png)

1. 执行引擎是Java虚拟机核心的组成部分之一。
2. “虚拟机”是一个相对于“物理机”的概念，这两种机器都有代码执行能力，其区别是物理机的执行引擎是直接建立在处理器、缓存、指令集和操作系统层面上的，而**虚拟机的执行引擎则是由软件自行实现的**，因此可以不受物理条件制约地定制指令集与执行引擎的结构体系，**能够执行那些不被硬件直接支持的指令集格式**。
3. JVM的主要任务是负责**装载字节码到其内部**，但字节码并不能够直接运行在操作系统之上，因为字节码指令并非等价于本地机器指令，它内部包含的仅仅只是一些能够被JVM所识别的字节码指令、符号表，以及其他辅助信息。
4. 那么，如果想要让一个Java程序运行起来，执行引擎（Execution Engine）的任务就是**将字节码指令解释/编译为对应平台上的本地机器指令才可以**。简单来说，JVM中的执行引擎充当了将高级语言翻译为机器语言的译者。

![](image/1664087673690-48c96391-6688-4c4a-84ff-dff31c44a9e0.png)
1、前端编译：从Java程序员-字节码文件的这个过程叫前端编译
2、执行引擎这里有两种行为：一种是解释执行，一种是编译执行（这里的是后端编译）。
**执行引擎工作过程**

1. 执行引擎在执行的过程中究竟需要执行什么样的字节码指令完全依赖于PC寄存器。
2. 每当执行完一项指令操作后，PC寄存器就会更新下一条需要被执行的指令地址。
3. 当然方法在执行的过程中，执行引擎有可能会通过存储在局部变量表中的对象引用准确定位到存储在Java堆区中的对象实例信息，以及通过对象头中的元数据指针定位到目标对象的类型信息。
4. 从外观上来看，所有的Java虚拟机的执行引擎输入、处理、输出都是一致的：输入的是字节码二进制流，处理过程是字节码解析执行、即时编译的等效过程，输出的是执行过程。

![](image/1664087674437-c320b53d-ba54-4cdb-af0b-073b428e6861.png)
## 2、Java代码编译和执行过程
### 解释执行和即时编译
大部分的程序代码转换成物理机的目标代码或虚拟机能执行的指令集之前，都需要经过下图中的各个步骤：

1. 前面橙色部分是编译生成生成字节码文件的过程（javac编译器来完成，也就是前端编译器），和JVM没有关系。
2. 后面绿色（解释执行）和蓝色（即时编译）才是JVM需要考虑的过程

![](image/1664087673684-11f9d486-36a9-4d65-9307-590b9b76a394.png)

1. javac编译器（前端编译器）流程图如下所示：![](image/1664087677318-e1673741-ee4e-4ba1-87bf-028c0bbd6e18.png)
2. Java字节码的执行是由JVM执行引擎来完成，流程图如下所示![](image/1664087674759-9056afd9-89f6-48ae-8c06-38e5c882f0f1.png)
### 解释器和JIT编译器

- 解释器：
   - 当Java虚拟机启动时会根据预定义的规范对字节码采用**逐行**解释的方式**执行**，将每条字节码文件中的内容“翻译”为对应平台的本地机器指令执行。
- JIT（Just In Time Compiler）编译器：
   - 就是虚拟机将源代码**一次性直接**编译成和本地机器平台相关的机器语言，**但并不是马上执行**。

**为什么Java是半编译半解释型语言？**

1. JDK1.0时代，将Java语言定位为“解释执行”还是比较准确的。再后来，Java也发展出可以直接生成本地代码的编译器。
2. 现在JVM在执行Java代码的时候，通常都会将解释执行与编译执行二者结合起来进行。
3. JIT编译器将字节码翻译成本地代码后，就可以做一个缓存操作，存储在方法区的JIT 代码缓存中（执行效率更高了），并且在翻译成本地代码的过程中可以做优化。

**用图总结一下**
![](image/1664087675865-cf2cfc5e-8ce2-4ff4-8702-1585cf58b15c.png)
## 3、机器码、指令、汇编语言
### 机器码

1. 各种用二进制编码方式表示的指令，叫做机器指令码。开始，人们就用它采编写程序，这就是机器语言。
2. 机器语言虽然能够被计算机理解和接受，但和人们的语言差别太大，不易被人们理解和记忆，并且用它编程容易出差错。
3. 用它编写的程序一经输入计算机，CPU直接读取运行，因此和其他语言编的程序相比，执行速度最快。
4. 机器指令与CPU紧密相关，所以不同种类的CPU所对应的机器指令也就不同。
### 指令和指令集
**指令**

1. 由于机器码是由0和1组成的二进制序列，可读性实在太差，于是人们发明了指令。
2. 指令就是把机器码中特定的0和1序列，简化成对应的指令（一般为英文简写，如mov，inc等），可读性稍好
3. 由于不同的硬件平台，执行同一个操作，对应的机器码可能不同，所以不同的硬件平台的同一种指令（比如mov），对应的机器码也可能不同。

**指令集**
不同的硬件平台，各自支持的指令，是有差别的。因此每个平台所支持的指令，称之为对应平台的指令集。如常见的

1. x86指令集，对应的是x86架构的平台
2. ARM指令集，对应的是ARM架构的平台
### 汇编语言

1. 由于指令的可读性还是太差，于是人们又发明了汇编语言。
2. 在汇编语言中，用助记符（Mnemonics）代替机器指令的操作码，用地址符号（Symbol）或标号（Label）代替指令或操作数的地址。
3. 在不同的硬件平台，汇编语言对应着不同的机器语言指令集，通过汇编过程转换成机器指令。
4. 由于计算机只认识指令码，所以用汇编语言编写的程序还必须翻译（汇编）成机器指令码，计算机才能识别和执行。
### 高级语言

1. 为了使计算机用户编程序更容易些，后来就出现了各种高级计算机语言。高级语言比机器语言、汇编语言更接近人的语言
2. 当计算机执行高级语言编写的程序时，仍然需要把程序解释和编译成机器的指令码。完成这个过程的程序就叫做解释程序或编译程序。

![](image/1664087676804-1f4b6152-4813-41b2-8d1b-78ad2f714389.png)
### 字节码

1. 字节码是一种中间状态（中间码）的二进制代码（文件），它比机器码更抽象，需要直译器转译后才能成为机器码
2. 字节码主要为了实现特定软件运行和软件环境、与硬件环境无关。
3. 字节码的实现方式是通过编译器和虚拟机器。编译器将源码编译成字节码，特定平台上的虚拟机器将字节码转译为可以直接执行的指令。
4. 字节码典型的应用为：Java bytecode
### C、C++源程序执行过程
**编译过程又可以分成两个阶段：编译和汇编。**

1. 编译过程：是读取源程序（字符流），对之进行词法和语法的分析，将高级语言指令转换为功能等效的汇编代码
2. 汇编过程：实际上指把汇编语言代码翻译成目标机器指令的过程。

![](image/1664087676096-70e89f71-06fa-4337-9fb1-09a6b036fe55.png)
## 4、解释器
### 为什么要有解释器

1. JVM设计者们的初衷仅仅只是单纯地为了满足Java程序实现跨平台特性，因此避免采用静态编译的方式由高级语言直接生成本地机器指令，从而诞生了实现解释器在运行时采用逐行解释字节码执行程序的想法（也就是产生了一个中间产品**字节码**）。
2. 解释器真正意义上所承担的角色就是一个运行时“翻译者”，将字节码文件中的内容“翻译”为对应平台的本地机器指令执行。
3. 当一条字节码指令被解释执行完成后，接着再根据PC寄存器中记录的下一条需要被执行的字节码指令执行解释操作。

![](image/1664087675951-d25bd0e4-439b-4626-a9b9-60a7cf69c1f7.png)
### 解释器的分类

1. 在Java的发展历史里，一共有两套解释执行器，即古老的**字节码解释器**、现在普遍使用的**模板解释器**。
   - 字节码解释器在执行时通过纯软件代码模拟字节码的执行，效率非常低下。
   - 而模板解释器将每一条字节码和一个模板函数相关联，模板函数中直接产生这条字节码执行时的机器码，从而很大程度上提高了解释器的性能。
2. 在HotSpot VM中，解释器主要由Interpreter模块和Code模块构成。
   - Interpreter模块：实现了解释器的核心功能
   - Code模块：用于管理HotSpot VM在运行时生成的本地机器指令
### 解释器的现状

1. 由于解释器在设计和实现上非常简单，因此除了Java语言之外，还有许多高级语言同样也是基于解释器执行的，比如Python、Perl、Ruby等。但是在今天，基于解释器执行已经沦落为低效的代名词，并且时常被一些C/C++程序员所调侃。
2. 为了解决这个问题，JVM平台支持一种叫作即时编译的技术。即时编译的目的是避免函数被解释执行，而是将整个函数体编译成为机器码，每次函数执行时，只执行编译后的机器码即可，这种方式可以使执行效率大幅度提升。
3. 不过无论如何，基于解释器的执行模式仍然为中间语言的发展做出了不可磨灭的贡献。
## 5、JIT编译器
### Java 代码执行的分类

1. 第一种是将源代码编译成字节码文件，然后在运行时通过解释器将字节码文件转为机器码执行
2. 第二种是编译执行（直接编译成机器码）。现代虚拟机为了提高执行效率，会使用即时编译技术（JIT，Just In Time）将方法编译成机器码后再执行
3. HotSpot VM是目前市面上高性能虚拟机的代表作之一。**它采用解释器与即时编译器并存的架构**。在Java虚拟机运行时，解释器和即时编译器能够相互协作，各自取长补短，尽力去选择最合适的方式来权衡编译本地代码的时间和直接解释执行代码的时间。
4. 在今天，Java程序的运行性能早已脱胎换骨，已经达到了可以和C/C++ 程序一较高下的地步。
### 为啥我们还需要解释器呢？

1. 有些开发人员会感觉到诧异，既然HotSpot VM中已经内置JIT编译器了，那么为什么还需要再使用解释器来“拖累”程序的执行性能呢？比如JRockit VM内部就不包含解释器，字节码全部都依靠即时编译器编译后执行。
2. JRockit虚拟机是砍掉了解释器，也就是只采及时编译器。那是因为呢JRockit只部署在服务器上，一般已经有时间让他进行指令编译的过程了，对于响应来说要求不高，等及时编译器的编译完成后，就会提供更好的性能

**首先明确两点：**

1. 当程序启动后，解释器可以马上发挥作用，**响应速度快**，省去编译的时间，立即执行。
2. 编译器要想发挥作用，把代码编译成本地代码，**需要一定的执行时间**，但编译为本地代码后，执行效率高。

**所以：**

1. 尽管JRockit VM中程序的执行性能会非常高效，但程序在启动时必然需要花费更长的时间来进行编译。对于服务端应用来说，启动时间并非是关注重点，但对于那些看中启动时间的应用场景而言，或许就需要采用解释器与即时编译器并存的架构来换取一个平衡点。
2. 在此模式下，在Java虚拟器启动时，解释器可以首先发挥作用，而不必等待即时编译器全部编译完成后再执行，这样可以省去许多不必要的编译时间。随着时间的推移，编译器发挥作用，把越来越多的代码编译成本地代码，获得更高的执行效率。
3. 同时，解释执行在编译器进行激进优化不成立的时候，作为编译器的“逃生门”（后备方案）。
### 案例

- 当虚拟机启动的时候，解释器可以首先发挥作用，而不必等待即时编译器全部编译完成再执行，这样可以省去许多不必要的编译时间。随着程序运行时间的推移，即时编译器逐渐发挥作用，根据热点探测功能，将有价值的字节码编译为本地机器指令，以换取更高的程序执行效率。
1. 注意解释执行与编译执行在线上环境微妙的辩证关系。**机器在热机状态（已经运行了一段时间叫热机状态）可以承受的负载要大于冷机状态（刚启动的时候叫冷机状态）**。如果以热机状态时的流量进行切流，可能使处于冷机状态的服务器因无法承载流量而假死。
2. 在生产环境发布过程中，以分批的方式进行发布，根据机器数量划分成多个批次，每个批次的机器数至多占到整个集群的1/8。曾经有这样的故障案例：某程序员在发布平台进行分批发布，在输入发布总批数时，误填写成分为两批发布。如果是热机状态，在正常情况下一半的机器可以勉强承载流量，但由于刚启动的JVM均是解释执行，还没有进行热点代码统计和JIT动态编译，导致机器启动之后，当前1/2发布成功的服务器马上全部宕机，此故障说明了JIT的存在。—**阿里团队**

![](image/1664087676906-d2457725-481e-4c5a-b128-19e9ffe0be6a.png)
```java
public class JITTest {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();

        for (int i = 0; i < 1000; i++) {
            list.add("让天下没有难学的技术");

            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

    }
}
```
通过 JVisualVM 查看 JIT 编译器执行的编译次数
![image.png](https://cdn.nlark.com/yuque/0/2022/png/26368762/1664088609788-ffb411ad-c8d6-4a62-9e7e-f2ae1c5e4c7d.png)

### JIT编译器相关概念

1. Java 语言的“编译期”其实是一段“不确定”的操作过程，因为它可能是指一个前端编译器（其实叫“编译器的前端”更准确一些）把.java文件转变成.class文件的过程。
2. 也可能是指虚拟机的后端运行期编译器（JIT编译器，Just In Time Compiler）把字节码转变成机器码的过程。
3. 还可能是指使用静态提前编译器（AOT编译器，Ahead of Time Compiler）直接把.java文件编译成本地机器代码的过程。（可能是后续发展的趋势）

**典型的编译器：**

1. 前端编译器：Sun的javac、Eclipse JDT中的增量式编译器（ECJ）。
2. JIT编译器：HotSpot VM的C1、C2编译器。
3. AOT 编译器：GNU Compiler for the Java（GCJ）、Excelsior JET。
### 热点代码及探测方式

1. 当然是否需要启动JIT编译器将字节码直接编译为对应平台的本地机器指令，则需要根据代码被调用**执行的频率**而定。
2. 关于那些需要被编译为本地代码的字节码，也被称之为“热点代码”**，JIT编译器在运行时会针对那些频繁被调用的“热点代码”做出**深度优化，将其直接编译为对应平台的本地机器指令，以此提升Java程序的执行性能。
3. 一个被多次调用的方法，或者是一-个方法体内部循环次数较多的循环体都可以被称之为“热点代码”，因此都可以通过JIT编译器编译为本地机器指令。由于这种编译方式发生在方法的执行过程中，因此也被称之为栈上替换，或简称为OSR (On StackReplacement)编译。
4. 一个方法究竟要被调用多少次，或者一个循环体究竟需要执行多少次循环才可以达到这个标准？必然需要一个明确的阈值，JIT编译器才会将这些“热点代码”编译为本地机器指令执行。这里主要依靠热点探测功能。
5. **目前HotSpot VM所采用的热点探测方式是基于计数器的热点探测**。
6. 采用基于计数器的热点探测，HotSpot VM将会为每一个方法都建立2个不同类型的计数器，分别为方法调用计数器（Invocation Counter）和回边计数器（Back Edge Counter）。
   1. 方法调用计数器用于统计方法的调用次数
   2. 回边计数器则用于统计循环体执行的循环次数
#### 方法调用计数器

1. 这个计数器就用于统计方法被调用的次数，它的默认阀值在Client模式下是1500次，在Server模式下是10000次。超过这个阈值，就会触发JIT编译。
2. 这个阀值可以通过虚拟机参数 -XX:CompileThreshold 来人为设定。
3. 当一个方法被调用时，会先检查该方法是否存在被JIT编译过的版本
   - 如果存在，则优先使用编译后的本地代码来执行
   - 如果不存在已被编译过的版本，则将此方法的调用计数器值加1，然后判断方法调用计数器与回边计数器值之和是否超过方法调用计数器的阀值。
      - 如果已超过阈值，那么将会向即时编译器提交一个该方法的代码编译请求。
      - 如果未超过阈值，则使用解释器对字节码文件解释执行

![](image/1664087677839-0393021d-11dd-4fa0-8d42-c7c77fa27d6a.png)
#### 热度衰减

1. 如果不做任何设置，方法调用计数器统计的并不是方法被调用的绝对次数，而是一个相对的执行频率，即**一段时间之内方法被调用的次数**。当超过一定的时间限度，如果方法的调用次数仍然不足以让它提交给即时编译器编译，那这个方法的调用计数器就会被减少一半，这个过程称为方法调用计数器热度的衰减（Counter Decay），而这段时间就称为此方法统计的半衰周期（Counter Half Life Time）（半衰周期是化学中的概念，比如出土的文物通过查看C60来获得文物的年龄）
2. 进行热度衰减的动作是在虚拟机进行垃圾收集时顺便进行的，可以使用虚拟机参数 -XX:-UseCounterDecay 来关闭热度衰减，让方法计数器统计方法调用的绝对次数，这样的话，只要系统运行时间足够长，绝大部分方法都会被编译成本地代码。
3. 另外，可以使用-XX:CounterHalfLifeTime参数设置半衰周期的时间，单位是秒。
#### 回边计数器
它的作用是统计一个方法中循环体代码执行的次数，在字节码中遇到控制流向后跳转的指令称为“回边”（Back Edge）。显然，建立回边计数器统计的目的就是为了触发OSR编译。
![](image/1664087678053-ec494c9a-16b2-410d-8d6b-b313b65553a2.png)
### 设置程序执行方法
> HotSpotVM可以设置程序执行方法

缺省情况下HotSpot VM是采用解释器与即时编译器并存的架构，当然开发人员可以根据具体的应用场景，通过命令显式地为Java虚拟机指定在运行时到底是完全采用解释器执行，还是完全采用即时编译器执行。如下所示：

1. -Xint：完全采用解释器模式执行程序；
2. -Xcomp：完全采用即时编译器模式执行程序。如果即时编译出现问题，解释器会介入执行
3. -Xmixed：采用解释器+即时编译器的混合模式共同执行程序。

![](image/1664087678591-ec79ac2b-7c68-4e11-b0ea-065e109b4fe0.png)
**代码测试**
```java
/**
 * 测试解释器模式和JIT编译模式
 *  -Xint  : 6520ms
 *  -Xcomp : 950ms
 *  -Xmixed : 936ms
 */
public class IntCompTest {
    public static void main(String[] args) {

        long start = System.currentTimeMillis();

        testPrimeNumber(1000000);

        long end = System.currentTimeMillis();

        System.out.println("花费的时间为：" + (end - start));

    }

    public static void testPrimeNumber(int count){
        for (int i = 0; i < count; i++) {
            //计算100以内的质数
            label:for(int j = 2;j <= 100;j++){
                for(int k = 2;k <= Math.sqrt(j);k++){
                    if(j % k == 0){
                        continue label;
                    }
                }
                //System.out.println(j);
            }

        }
    }
}

```
结论：只用解释器执行是真的慢
### JIT 分类
在HotSpot VM中内嵌有两个JIT编译器，分别为Client Compiler和Server Compiler，但大多数情况下我们简称为C1编译器 和 C2编译器。开发人员可以通过如下命令显式指定Java虚拟机在运行时到底使用哪一种即时编译器，如下所示：

1. -client：指定Java虚拟机运行在Client模式下，并使用C1编译器；
   - C1编译器会对字节码进行简单和可靠的优化，耗时短，以达到更快的编译速度。
2. -server：指定Java虚拟机运行在server模式下，并使用C2编译器。
   - C2进行耗时较长的优化，以及激进优化，但优化的代码执行效率更高。（使用C++）
### C1和C2编译器不同的优化策略

1. 在不同的编译器上有不同的优化策略，C1编译器上主要有方法内联，去虚拟化、元余消除。
   - 方法内联：将引用的函数代码编译到引用点处，这样可以减少栈帧的生成，减少参数传递以及跳转过程
   - 去虚拟化：对唯一的实现樊进行内联
   - 冗余消除：在运行期间把一些不会执行的代码折叠掉
2. C2的优化主要是在全局层面，逃逸分析是优化的基础。基于逃逸分析在C2上有如下几种优化：
   - 标量替换：用标量值代替聚合对象的属性值
   - 栈上分配：对于未逃逸的对象分配对象在栈而不是堆
   - 同步消除：清除同步操作，通常指synchronized

也就是说之前的逃逸分析，只有在C2（server模式下）才会触发。那是否说明C1就用不了了？
### 分层编译策略

1. 分层编译（Tiered Compilation）策略：程序解释执行（不开启性能监控）可以触发C1编译，将字节码编译成机器码，可以进行简单优化，也可以加上性能监控，C2编译会根据性能监控信息进行激进优化。
2. 不过在Java7版本之后，一旦开发人员在程序中显式指定命令“-server"时，默认将会开启分层编译策略，由C1编译器和C2编译器相互协作共同来执行编译任务。
3. 一般来讲，JIT编译出来的机器码性能比解释器解释执行的性能高
4. C2编译器启动时长比C1慢，系统稳定执行以后，C2编译器执行速度远快于C1编译器
#### Graal 编译器

- 自JDK10起，HotSpot又加入了一个全新的即时编译器：Graal编译器
- 编译效果短短几年时间就追平了G2编译器，未来可期（对应还出现了Graal虚拟机，是有可能替代Hotspot的虚拟机的）
- 目前，带着实验状态标签，需要使用开关参数去激活才能使用-XX:+UnlockExperimentalvMOptions -XX:+UseJVMCICompiler
#### AOT编译器

1. jdk9引入了AoT编译器（静态提前编译器，Ahead of Time Compiler）
2. Java 9引入了实验性AOT编译工具jaotc。它借助了Graal编译器，将所输入的Java类文件转换为机器码，并存放至生成的动态共享库之中。
3. 所谓AOT编译，是与即时编译相对立的一个概念。我们知道，即时编译指的是**在程序的运行过程中**，将字节码转换为可在硬件上直接运行的机器码，并部署至托管环境中的过程。而AOT编译指的则是，**在程序运行之前**，便将字节码转换为机器码的过程。
   - .java -> .class -> (使用jaotc) -> .so

**AOT编译器编译器的优缺点**
**最大的好处：**

1. Java虚拟机加载已经预编译成二进制库，可以直接执行。
2. 不必等待即时编译器的预热，减少Java应用给人带来“第一次运行慢” 的不良体验

**缺点：**

1. 破坏了 java “ 一次编译，到处运行”，必须为每个不同的硬件，OS编译对应的发行包
2. 降低了Java链接过程的动态性，加载的代码在编译器就必须全部已知。
3. 还需要继续优化中，最初只支持Linux X64 java base

# 十三、 StringTable（字符串常量池）
## 1、概述

1. String：字符串，使用一对 “” 引起来表示
2. String被声明为final的，不可被继承
3. String实现了Serializable接口：表示字符串是支持序列化的。实现了Comparable接口：表示String可以比较大小
4. String在jdk8及以前内部定义了final char value[]用于存储字符串数据。JDK9时改为byte[]
### JDK9 改变String结构
**官方文档**：[http://openjdk.java.net/jeps/254](http://openjdk.java.net/jeps/254)
**为什么改为 byte[] 存储？**

1. String类的当前实现将字符存储在char数组中，每个字符使用两个字节(16位)。
2. 从许多不同的应用程序收集的数据表明，字符串是堆使用的主要组成部分，而且大多数字符串对象只包含拉丁字符（Latin-1）。这些字符只需要一个字节的存储空间，因此这些字符串对象的内部char数组中有一半的空间将不会使用，产生了大量浪费。
3. 之前 String 类使用 UTF-16 的 char[] 数组存储，现在改为 byte[] 数组 外加一个编码标识存储。该编码表示如果你的字符是ISO-8859-1或者Latin-1，那么只需要一个字节存。如果你是其它字符集，比如UTF-8，你仍然用两个字节存
4. 结论：String再也不用char[] 来存储了，改成了byte [] 加上编码标记，节约了一些空间
5. 同时基于String的数据结构，例如StringBuffer和StringBuilder也同样做了修改
### 基本特性

- String：代表不可变的字符序列。简称：不可变性。
   - 当对字符串重新赋值时，需要重写指定内存区域赋值，不能使用原有的value进行赋值。
   - 当对现有的字符串进行连接操作时，也需要重新指定内存区域赋值，不能使用原有的value进行赋值。
   - 当调用String的replace()方法修改指定字符或字符串时，也需要重新指定内存区域赋值，不能使用原有的value进行赋值。
- 通过字面量的方式（区别于new）给一个字符串赋值，此时的字符串值声明在字符串常量池中。

**一道笔试题**
```java
public class StringExer {
    String str = new String("good");
    char[] ch = {'t', 'e', 's', 't'};

    public void change(String str, char ch[]) {
        str = "test ok";
        ch[0] = 'b';
    }

    public static void main(String[] args) {
        StringExer ex = new StringExer();
        ex.change(ex.str, ex.ch);
        System.out.println(ex.str);//good
        System.out.println(ex.ch);//best
    }

}
```
> str 的内容并没有变：“test ok” 位于字符串常量池中的另一个区域（地址），进行赋值操作并没有修改原来 str 指向的引用的内容

### 底层结构
**字符串常量池是不会存储相同内容的字符串的**

1. String 的 String Pool（字符串常量池）是一个固定大小的Hashtable。
2. 使用-XX:StringTablesize可设置StringTable的长度
3. 在JDK6中StringTable是固定的，就是1009的长度，所以如果常量池中的字符串过多就会导致效率下降很快，StringTablesize设置没有要求
4. 在JDK7中，StringTable的长度默认值是60013，StringTablesize设置没有要求
5. 在JDK8中，StringTable的长度默认值是60013，StringTable可以设置的最小值为1009

![](image/1664089220273-61b6e437-8c61-4472-8dee-214d6e0d4f91.png)
![](image/1664089221774-8cd3be31-4d81-401e-8a08-4d5585727251.png)
**测试不同 StringTable 长度下，程序的性能**
代码

```java
/**
 * 产生10万个长度不超过10的字符串，包含a-z,A-Z
 */
public class GenerateString {
    public static void main(String[] args) throws IOException {
        FileWriter fw =  new FileWriter("words.txt");

        for (int i = 0; i < 100000; i++) {
            //1 - 10
           int length = (int)(Math.random() * (10 - 1 + 1) + 1);
            fw.write(getString(length) + "\n");
        }

        fw.close();
    }

    public static String getString(int length){
        String str = "";
        for (int i = 0; i < length; i++) {
            //65 - 90, 97-122
            int num = (int)(Math.random() * (90 - 65 + 1) + 65) + (int)(Math.random() * 2) * 32;
            str += (char)num;
        }
        return str;
    }
}

```
```java
public class StringTest2 {
    public static void main(String[] args) {

        BufferedReader br = null;
        try {
            br = new BufferedReader(new FileReader("words.txt"));
            long start = System.currentTimeMillis();
            String data;
            while((data = br.readLine()) != null){
                data.intern(); //如果字符串常量池中没有对应data的字符串的话，则在常量池中生成
            }

            long end = System.currentTimeMillis();

            System.out.println("花费的时间为：" + (end - start));//1009:143ms  100009:47ms
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if(br != null){
                try {
                    br.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }

            }
        }
    }
}

```

- -XX:StringTableSize=1009 ：程序耗时 143ms
- -XX:StringTableSize=100009 ：程序耗时 47ms
## 2、内存分配

1. 在Java语言中有8种基本数据类型和一种比较特殊的类型String。这些类型为了使它们在运行过程中速度更快、更节省内存，都提供了一种常量池的概念。
2. 常量池就类似一个Java系统级别提供的缓存。8种基本数据类型的常量池都是系统协调的，String类型的常量池比较特殊。它的主要使用方法有两种。
   - 直接使用双引号声明出来的String对象会直接存储在常量池中。比如：String info="atguigu.com";
   - 如果不是用双引号声明的String对象，可以使用String提供的intern()方法。这个后面重点谈
3. Java 6及以前，字符串常量池存放在永久代
4. Java 7中 Oracle的工程师对字符串池的逻辑做了很大的改变，即将字符串常量池的位置调整到Java堆内
   - 所有的字符串都保存在堆（Heap）中，和其他普通对象一样，这样可以让你在进行调优应用时仅需要调整堆大小就可以了。
   - 字符串常量池概念原本使用得比较多，但是这个改动使得我们有足够的理由让我们重新考虑在Java 7中使用String.intern()。
5. Java8元空间，字符串常量在堆

![](image/1664089221620-e737c8fa-d23b-493a-a163-912b1601d001.png)
![](image/1664089221405-47e9a969-e2ce-4518-a374-4d8b3820edda.png)
**StringTable 为什么要调整？**
**官方文档**:[https://www.oracle.com/java/technologies/javase/jdk7-relnotes.html#jdk7changes](https://www.oracle.com/java/technologies/javase/jdk7-relnotes.html#jdk7changes)

1. 为什么要调整位置？
   - 永久代的默认空间大小比较小
   - 永久代垃圾回收频率低，大量的字符串无法及时回收，容易进行Full GC产生STW或者容易产生OOM：PermGen Space
   - 堆中空间足够大，字符串可被及时回收
2. 在JDK 7中，interned字符串不再在Java堆的永久代中分配，而是在Java堆的主要部分（称为年轻代和年老代）中分配，与应用程序创建的其他对象一起分配。
3. 此更改将导致驻留在主Java堆中的数据更多，驻留在永久生成中的数据更少，因此可能需要调整堆大小。

**代码示例**
```java
/**
 * jdk6中：
 * -XX:PermSize=6m -XX:MaxPermSize=6m -Xms6m -Xmx6m
 *
 * jdk8中：
 * -XX:MetaspaceSize=6m -XX:MaxMetaspaceSize=6m -Xms6m -Xmx6m
 */
public class StringTest3 {
    public static void main(String[] args) {
        //使用Set保持着常量池引用，避免full gc回收常量池行为
        Set<String> set = new HashSet<String>();
        //在short可以取值的范围内足以让6MB的PermSize或heap产生OOM了。
        short i = 0;
        while(true){
            set.add(String.valueOf(i++).intern());
        }
    }
}
```
输出结果：字符串确实在堆中（JDK8）
```bash
Exception in thread "main" java.lang.OutOfMemoryError: Java heap space
	at java.util.HashMap.resize(HashMap.java:703)
	at java.util.HashMap.putVal(HashMap.java:662)
	at java.util.HashMap.put(HashMap.java:611)
	at java.util.HashSet.add(HashSet.java:219)
	at com.atguigu.java.StringTest3.main(StringTest3.java:22)

Process finished with exit code 1
```
## 3、举例
```java
//官方示例代码
class Memory {
    public static void main(String[] args) {//line 1
        int i = 1;//line 2
        Object obj = new Object();//line 3
        Memory mem = new Memory();//line 4
        mem.foo(obj);//line 5
    }//line 9

    private void foo(Object param) {//line 6
        String str = param.toString();//line 7
        System.out.println(str);
    }//line 8
}
```
分析运行时内存（foo() 方法是实例方法，其实图中少了一个 this 局部变量）
![1664091483010-c7baa4d5-c2fe-42ee-a65e-31cd80fa06ee](image/1664091483010-c7baa4d5-c2fe-42ee-a65e-31cd80fa06ee.png)

## 4、字符串拼接操作
### 先说结论

1. 常量与常量的拼接结果在常量池，原理是编译期优化
2. 常量池中不会存在相同内容的变量
3. 拼接前后，只要其中有一个是变量，结果就在堆中。变量拼接的原理是StringBuilder
4. 如果拼接的结果调用intern()方法，根据该字符串是否在常量池中存在，分为：
   - 如果存在，则返回字符串在常量池中的地址
   - 如果字符串常量池中不存在该字符串，则在常量池中创建一份，并返回此对象的地址

**1、常量与常量的拼接结果在常量池，原理是编译期优化**
代码
```java
@Test
public void test1(){
    String s1 = "a" + "b" + "c";//编译期优化：等同于"abc"
    String s2 = "abc"; //"abc"一定是放在字符串常量池中，将此地址赋给s2
    /*
     * 最终.java编译成.class,再执行.class
     * String s1 = "abc";
     * String s2 = "abc"
     */
    System.out.println(s1 == s2); //true
    System.out.println(s1.equals(s2)); //true
}
```
从字节码指令看出：编译器做了优化，将 “a” + “b” + “c” 优化成了 “abc”
```bash
0 ldc #2 <abc>
2 astore_1
3 ldc #2 <abc>
5 astore_2
6 getstatic #3 <java/lang/System.out>
9 aload_1
10 aload_2
11 if_acmpne 18 (+7)
14 iconst_1
15 goto 19 (+4)
18 iconst_0
19 invokevirtual #4 <java/io/PrintStream.println>
22 getstatic #3 <java/lang/System.out>
25 aload_1
26 aload_2
27 invokevirtual #5 <java/lang/String.equals>
30 invokevirtual #4 <java/io/PrintStream.println>
33 return
```
IDEA 反编译 class 文件后，来看这个问题
![](image/1664089226678-82cae4ef-8f28-4bee-b7e0-1f2eb7a7d963.png)
**2、拼接前后，只要其中有一个是变量，结果就在堆中**
**调用 intern() 方法，则主动将字符串对象存入字符串常量池中，并将其地址返回**
```java
@Test
    public void test2(){
        String s1 = "javaEE";
        String s2 = "hadoop";

        String s3 = "javaEEhadoop";
        String s4 = "javaEE" + "hadoop";//编译期优化
        //如果拼接符号的前后出现了变量，则相当于在堆空间中new String()，具体的内容为拼接的结果：javaEEhadoop
        String s5 = s1 + "hadoop";
        String s6 = "javaEE" + s2;
        String s7 = s1 + s2;

        System.out.println(s3 == s4);//true
        System.out.println(s3 == s5);//false
        System.out.println(s3 == s6);//false
        System.out.println(s3 == s7);//false
        System.out.println(s5 == s6);//false
        System.out.println(s5 == s7);//false
        System.out.println(s6 == s7);//false
        //intern():判断字符串常量池中是否存在javaEEhadoop值，如果存在，则返回常量池中javaEEhadoop的地址；
        //如果字符串常量池中不存在javaEEhadoop，则在常量池中加载一份javaEEhadoop，并返回次对象的地址。
        String s8 = s6.intern();
        System.out.println(s3 == s8);//true
    }

```
从字节码角度来看：拼接前后有变量，都会使用到 StringBuilder 类
```bash
0 ldc #6 <javaEE>
2 astore_1
3 ldc #7 <hadoop>
5 astore_2
6 ldc #8 <javaEEhadoop>
8 astore_3
9 ldc #8 <javaEEhadoop>
11 astore 4
13 new #9 <java/lang/StringBuilder>
16 dup
17 invokespecial #10 <java/lang/StringBuilder.<init>>
20 aload_1
21 invokevirtual #11 <java/lang/StringBuilder.append>
24 ldc #7 <hadoop>
26 invokevirtual #11 <java/lang/StringBuilder.append>
29 invokevirtual #12 <java/lang/StringBuilder.toString>
32 astore 5
34 new #9 <java/lang/StringBuilder>
37 dup
38 invokespecial #10 <java/lang/StringBuilder.<init>>
41 ldc #6 <javaEE>
43 invokevirtual #11 <java/lang/StringBuilder.append>
46 aload_2
47 invokevirtual #11 <java/lang/StringBuilder.append>
50 invokevirtual #12 <java/lang/StringBuilder.toString>
53 astore 6
55 new #9 <java/lang/StringBuilder>
58 dup
59 invokespecial #10 <java/lang/StringBuilder.<init>>
62 aload_1
63 invokevirtual #11 <java/lang/StringBuilder.append>
66 aload_2
67 invokevirtual #11 <java/lang/StringBuilder.append>
70 invokevirtual #12 <java/lang/StringBuilder.toString>
73 astore 7
75 getstatic #3 <java/lang/System.out>
78 aload_3
79 aload 4
81 if_acmpne 88 (+7)
84 iconst_1
85 goto 89 (+4)
88 iconst_0
89 invokevirtual #4 <java/io/PrintStream.println>
92 getstatic #3 <java/lang/System.out>
95 aload_3
96 aload 5
98 if_acmpne 105 (+7)
101 iconst_1
102 goto 106 (+4)
105 iconst_0
106 invokevirtual #4 <java/io/PrintStream.println>
109 getstatic #3 <java/lang/System.out>
112 aload_3
113 aload 6
115 if_acmpne 122 (+7)
118 iconst_1
119 goto 123 (+4)
122 iconst_0
123 invokevirtual #4 <java/io/PrintStream.println>
126 getstatic #3 <java/lang/System.out>
129 aload_3
130 aload 7
132 if_acmpne 139 (+7)
135 iconst_1
136 goto 140 (+4)
139 iconst_0
140 invokevirtual #4 <java/io/PrintStream.println>
143 getstatic #3 <java/lang/System.out>
146 aload 5
148 aload 6
150 if_acmpne 157 (+7)
153 iconst_1
154 goto 158 (+4)
157 iconst_0
158 invokevirtual #4 <java/io/PrintStream.println>
161 getstatic #3 <java/lang/System.out>
164 aload 5
166 aload 7
168 if_acmpne 175 (+7)
171 iconst_1
172 goto 176 (+4)
175 iconst_0
176 invokevirtual #4 <java/io/PrintStream.println>
179 getstatic #3 <java/lang/System.out>
182 aload 6
184 aload 7
186 if_acmpne 193 (+7)
189 iconst_1
190 goto 194 (+4)
193 iconst_0
194 invokevirtual #4 <java/io/PrintStream.println>
197 aload 6
199 invokevirtual #13 <java/lang/String.intern>
202 astore 8
204 getstatic #3 <java/lang/System.out>
207 aload_3
208 aload 8
210 if_acmpne 217 (+7)
213 iconst_1
214 goto 218 (+4)
217 iconst_0
218 invokevirtual #4 <java/io/PrintStream.println>
221 return
```
### 字符串拼接的底层细节
**举例1**
```java
    @Test
    public void test3(){
        String s1 = "a";
        String s2 = "b";
        String s3 = "ab";
        /*
        如下的s1 + s2 的执行细节：(变量s是我临时定义的）
        ① StringBuilder s = new StringBuilder();
        ② s.append("a")
        ③ s.append("b")
        ④ s.toString()  --> 约等于 new String("ab")，但不等价

        补充：在jdk5.0之后使用的是StringBuilder,在jdk5.0之前使用的是StringBuffer
         */
        String s4 = s1 + s2;//
        System.out.println(s3 == s4);//false
    }
```
字节码指令
```bash
0 ldc #14 <a>
2 astore_1
3 ldc #15 <b>
5 astore_2
6 ldc #16 <ab>
8 astore_3
9 new #9 <java/lang/StringBuilder>
12 dup
13 invokespecial #10 <java/lang/StringBuilder.<init>>
16 aload_1
17 invokevirtual #11 <java/lang/StringBuilder.append>
20 aload_2
21 invokevirtual #11 <java/lang/StringBuilder.append>
24 invokevirtual #12 <java/lang/StringBuilder.toString>
27 astore 4
29 getstatic #3 <java/lang/System.out>
32 aload_3
33 aload 4
35 if_acmpne 42 (+7)
38 iconst_1
39 goto 43 (+4)
42 iconst_0
43 invokevirtual #4 <java/io/PrintStream.println>
46 return
```
**举例2**
```java
/*
    1. 字符串拼接操作不一定使用的是StringBuilder!
       如果拼接符号左右两边都是字符串常量或常量引用，则仍然使用编译期优化，即非StringBuilder的方式。
    2. 针对于final修饰类、方法、基本数据类型、引用数据类型的量的结构时，能使用上final的时候建议使用上。
     */
    @Test
    public void test4(){
        final String s1 = "a";
        final String s2 = "b";
        String s3 = "ab";
        String s4 = s1 + s2;
        System.out.println(s3 == s4);//true
    }
```
从字节码角度来看：为变量 s4 赋值时，直接使用 #16 符号引用，即字符串常量 “ab”
```bash
0 ldc #14 <a>
2 astore_1
3 ldc #15 <b>
5 astore_2
6 ldc #16 <ab>
8 astore_3
9 ldc #16 <ab>
11 astore 4
13 getstatic #3 <java/lang/System.out>
16 aload_3
17 aload 4
19 if_acmpne 26 (+7)
22 iconst_1
23 goto 27 (+4)
26 iconst_0
27 invokevirtual #4 <java/io/PrintStream.println>
30 return
```
**拼接操作与 append 操作的效率对比**
```java

    @Test
    public void test6(){

        long start = System.currentTimeMillis();

//        method1(100000);//4014
        method2(100000);//7

        long end = System.currentTimeMillis();

        System.out.println("花费的时间为：" + (end - start));
    }

    public void method1(int highLevel){
        String src = "";
        for(int i = 0;i < highLevel;i++){
            src = src + "a";//每次循环都会创建一个StringBuilder、String
        }
//        System.out.println(src);

    }

    public void method2(int highLevel){
        //只需要创建一个StringBuilder
        StringBuilder src = new StringBuilder();
        for (int i = 0; i < highLevel; i++) {
            src.append("a");
        }
//        System.out.println(src);
    }
```

1. 体会执行效率：通过StringBuilder的append()的方式添加字符串的效率要远高于使用String的字符串拼接方式！
2. 原因：
   1. StringBuilder的append()的方式：
      - 自始至终中只创建过一个StringBuilder的对象
   2. 使用String的字符串拼接方式：
      - 创建过多个StringBuilder和String（调的toString方法）的对象，内存占用更大；
      - 如果进行GC，需要花费额外的时间（在拼接的过程中产生的一些中间字符串可能永远也用不到，会产生大量垃圾字符串）。
3. 改进的空间：
   - 在实际开发中，如果基本确定要前前后后添加的字符串长度不高于某个限定值highLevel的情况下，建议使用构造器实例化：
   - StringBuilder s = new StringBuilder(highLevel); //new char[highLevel]
   - 这样可以避免频繁扩容
## 5、intern() 的使用
### intern() 方法的说明

1. intern是一个native方法，调用的是底层C的方法
2. 字符串常量池池最初是空的，由String类私有地维护。在调用intern方法时，如果池中已经包含了由equals(object)方法确定的与该字符串内容相等的字符串，则返回池中的字符串地址。否则，该字符串对象将被添加到池中，并返回对该字符串对象的地址。（这是源码里的大概翻译）
3. 如果不是用双引号声明的String对象，可以使用String提供的intern方法：intern方法会从字符串常量池中查询当前字符串是否存在，若不存在就会将当前字符串放入常量池中。比如：`String myInfo = new string("I love atguigu").intern(); `
4. 也就是说，如果在任意字符串上调用String.intern方法，那么其返回结果所指向的那个类实例，必须和直接以常量形式出现的字符串实例完全相同。因此，下列表达式的值必定是true`("a"+"b"+"c").intern()=="abc" `
5. 通俗点讲，Interned String就是确保字符串在内存里只有一份拷贝，这样可以节约内存空间，加快字符串操作任务的执行速度。注意，这个值会被存放在字符串内部池（String Intern Pool）
### new String() 的说明
**new String(“ab”)会创建几个对象？**
```java
/**
 * 题目：
 * new String("ab")会创建几个对象？看字节码，就知道是两个。
 *     一个对象是：new关键字在堆空间创建的
 *     另一个对象是：字符串常量池中的对象"ab"。 字节码指令：ldc
 *
 */
public class StringNewTest {
    public static void main(String[] args) {
        String str = new String("ab");
    }
}
```
字节码指令
```bash
0 new #2 <java/lang/String>
3 dup
4 ldc #3 <ab>
6 invokespecial #4 <java/lang/String.<init>>
9 astore_1
10 return
```
> 0 new #2 <java/lang/String>：在堆中创建了一个 String 对象
> 4 ldc #3 <ab> ：在字符串常量池中放入 “ab”（如果之前字符串常量池中没有 “ab” 的话）

**new String(“a”) + new String(“b”) 会创建几个对象？**
代码
```java
/**
 * 思考：
 * new String("a") + new String("b")呢？
 *  对象1：new StringBuilder()
 *  对象2： new String("a")
 *  对象3： 常量池中的"a"
 *  对象4： new String("b")
 *  对象5： 常量池中的"b"
 *
 *  深入剖析： StringBuilder的toString():
 *      对象6 ：new String("ab")
 *       强调一下，toString()的调用，在字符串常量池中，没有生成"ab"
 *
 */
public class StringNewTest {
    public static void main(String[] args) {

        String str = new String("a") + new String("b");
    }
}
```
字节码指令
```bash
0 new #2 <java/lang/StringBuilder>
3 dup
4 invokespecial #3 <java/lang/StringBuilder.<init>>
7 new #4 <java/lang/String>
10 dup
11 ldc #5 <a>
13 invokespecial #6 <java/lang/String.<init>>
16 invokevirtual #7 <java/lang/StringBuilder.append>
19 new #4 <java/lang/String>
22 dup
23 ldc #8 <b>
25 invokespecial #6 <java/lang/String.<init>>
28 invokevirtual #7 <java/lang/StringBuilder.append>
31 invokevirtual #9 <java/lang/StringBuilder.toString>
34 astore_1
35 return
```
**答案是6个**
字节码指令分析：

1. `0 new #2 <java/lang/StringBuilder> `：拼接字符串会创建一个 StringBuilder 对象
2. `7 new #4 <java/lang/String>` ：创建 String 对象，对应于 new String(“a”)
3. `11 ldc #5 <a>` ：在字符串常量池中放入 “a”（如果之前字符串常量池中没有 “a” 的话）
4. `19 new #4 <java/lang/String>` ：创建 String 对象，对应于 new String(“b”)
5. `23 ldc #8 <b>` ：在字符串常量池中放入 “b”（如果之前字符串常量池中没有 “b” 的话）
6. `31 invokevirtual #9 <java/lang/StringBuilder.toString>` ：调用 StringBuilder 的 toString() 方法，会生成一个 String 对象
   - 这里的toString()没有在常量池中放入"ab"

![](image/1664089228012-bf8cdbb9-5fb7-4ea0-952f-cc0350e3d564.png)
### 有点难的面试题
**有点难的面试题**
```java
**
 * 如何保证变量s指向的是字符串常量池中的数据呢？
 * 有两种方式：
 * 方式一： String s = "shkstart";//字面量定义的方式
 * 方式二： 调用intern()
 *         String s = new String("shkstart").intern();
 *         String s = new StringBuilder("shkstart").toString().intern();
 *
 */
public class 	StringIntern {
    public static void main(String[] args) {

        String s = new String("1");
        s.intern();//调用此方法之前，字符串常量池中已经存在了"1"
        String s2 = "1";
        System.out.println(s == s2);//jdk6：false   jdk7/8：false
        
        /*
         1、s3变量记录的地址为：new String("11")
         2、经过上面的分析，我们已经知道执行完pos_1的代码，在堆中有了一个new String("11")
         这样的String对象。但是在字符串常量池中没有"11"
         3、接着执行s3.intern()，在字符串常量池中生成"11"
           3-1、在JDK6的版本中，字符串常量池还在永久代，所以直接在永久代生成"11",也就有了新的地址
           3-2、而在JDK7的后续版本中，字符串常量池被移动到了堆中，此时堆里已经有new String（"11"）了
           出于节省空间的目的，直接将堆中的那个字符串的引用地址储存在字符串常量池中。没错，字符串常量池
           中存的是new String（"11"）在堆中的地址
         4、所以在JDK7后续版本中，s3和s4指向的完全是同一个地址。
         */
        String s3 = new String("1") + new String("1");//pos_1
	    s3.intern();
        
        String s4 = "11";//s4变量记录的地址：使用的是上一行代码代码执行时，在常量池中生成的"11"的地址
        System.out.println(s3 == s4);//jdk6：false  jdk7/8：true
    }


}

```
解释的已经比较清楚了，下面看一下内存图
**内存分析**
JDK6 ：正常眼光判断即可

- new String() 即在堆中
- str.intern() 则把字符串放入常量池中

![](image/1664089230315-4f595ee8-3330-4550-bb4c-ee398ef9eb46.png)
JDK7及后续版本，**注意大坑**
![](image/1664089230230-75a5e9b5-899a-4a31-adae-0420a4dd42f2.png)
#### 面试题的拓展
```java
/**
 * StringIntern.java中练习的拓展：
 *
 */
public class StringIntern1 {
    public static void main(String[] args) {
        //执行完下一行代码以后，字符串常量池中，是否存在"11"呢？答案：不存在！！
        String s3 = new String("1") + new String("1");//new String("11")
        //在字符串常量池中生成对象"11"，代码顺序换一下，实打实的在字符串常量池里有一个"11"对象
        String s4 = "11";  
        String s5 = s3.intern();

        // s3 是堆中的 "ab" ，s4 是字符串常量池中的 "ab"
        System.out.println(s3 == s4);//false

        // s5 是从字符串常量池中取回来的引用，当然和 s4 相等
        System.out.println(s5 == s4);//true
    }
}
```
### intern() 方法的练习
**练习 1**
```java
public class StringExer1 {
    public static void main(String[] args) {
        String x = "ab";
        String s = new String("a") + new String("b");//new String("ab")
        //在上一行代码执行完以后，字符串常量池中并没有"ab"
		/*
		1、jdk6中：在字符串常量池（此时在永久代）中创建一个字符串"ab"
        2、jdk8中：字符串常量池（此时在堆中）中没有创建字符串"ab",而是创建一个引用，指向new String("ab")，		  将此引用返回
        3、详解看上面
		*/
        String s2 = s.intern();

        System.out.println(s2 == "ab");//jdk6:true  jdk8:true
        System.out.println(s == "ab");//jdk6:false  jdk8:true
    }
}
```
**JDK6**
![](image/1664089229745-b013a7e2-dd27-455c-9aa2-b75d5cde46f2.png)
**JDK7/8**
![](image/1664089233916-0d93cc92-63c6-4884-8774-bd8c9aaf30cc.png)
**练习2**
```java
public class StringExer1 {
    public static void main(String[] args) {
        //加一行这个
        String x = "ab";
        String s = new String("a") + new String("b");//new String("ab")

        String s2 = s.intern();

        System.out.println(s2 == "ab");//jdk6:true  jdk8:true
        System.out.println(s == "ab");//jdk6:false  jdk8:true
    }
}
```
![](image/1664089237403-9dab3c72-0ee4-4f69-908a-089b9ef58661.png)
**练习3**
```java
public class StringExer2 {
    public static void main(String[] args) {
        String s1 = new String("ab");//执行完以后，会在字符串常量池中会生成"ab"

        s1.intern();
        String s2 = "ab";
        System.out.println(s1 == s2);//false
    }
}
```
**验证**
```java
public class StringExer2 {
    // 对象内存地址可以使用System.identityHashCode(object)方法获取
    public static void main(String[] args) {
        String s1 = new String("a") + new String("b");//执行完以后，不会在字符串常量池中会生成"ab"
        System.out.println(System.identityHashCode(s1));
        s1.intern();
        System.out.println(System.identityHashCode(s1));
        String s2 = "ab";
        System.out.println(System.identityHashCode(s2));
        System.out.println(s1 == s2); // true
    }
}
```
### intern() 的效率测试（空间角度）
```java
/**
 * 使用intern()测试执行效率：空间使用上
 *
 * 结论：对于程序中大量存在存在的字符串，尤其其中存在很多重复字符串时，使用intern()可以节省内存空间。
 *
 */
public class StringIntern2 {
    static final int MAX_COUNT = 1000 * 10000;
    static final String[] arr = new String[MAX_COUNT];

    public static void main(String[] args) {
        Integer[] data = new Integer[]{1,2,3,4,5,6,7,8,9,10};

        long start = System.currentTimeMillis();
        for (int i = 0; i < MAX_COUNT; i++) {
//            arr[i] = new String(String.valueOf(data[i % data.length]));
            arr[i] = new String(String.valueOf(data[i % data.length])).intern();

        }
        long end = System.currentTimeMillis();
        System.out.println("花费的时间为：" + (end - start));

        try {
            Thread.sleep(1000000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.gc();
    }
}
```
1、直接 new String ：由于每个 String 对象都是 new 出来的，所以程序需要维护大量存放在堆空间中的 String 实例，程序内存占用也会变高
`arr[i] = new String(String.valueOf(data[i % data.length]));`
![image.png](image/1664094589252-579522dd-1179-47af-97f8-de22c563c708.png)



![image.png](image/1664094604547-fb9762b0-aa32-4b02-8ae7-b86aab6db982.png)



2、使用 intern() 方法：由于数组中字符串的引用都指向字符串常量池中的字符串，所以程序需要维护的 String 对象更少，内存占用也更低

```java
//调用了intern()方法使用了字符串常量池里的字符串，那么前面堆里的字符串便会被GC掉，这也是intern省内存的关键原因
arr[i] = new String(String.valueOf(data[i % data.length])).intern();
```
![](image/1664089256166-a9058be5-4c06-4586-bec2-833b98c3e5ed.png)



![image.png](image/1664094645363-84d4c567-c85b-4777-a4a9-02ea961d4288.png)

**结论**：

1. 对于程序中大量使用存在的字符串时，尤其存在很多已经重复的字符串时，使用intern()方法能够节省很大的内存空间。
2. 大的网站平台，需要内存中存储大量的字符串。比如社交网站，很多人都存储：北京市、海淀区等信息。这时候如果字符串都调用intern() 方法，就会很明显降低内存的大小。
## 6、StringTable 的垃圾回收
```java
/**
 * String的垃圾回收:
 * -Xms15m -Xmx15m -XX:+PrintStringTableStatistics -XX:+PrintGCDetails
 */
public class StringGCTest {
    public static void main(String[] args) {
        for (int j = 0; j < 100000; j++) {
            String.valueOf(j).intern();
        }
    }
}
```
输出结果：

- 在 PSYoungGen 区发生了垃圾回收
- Number of entries 和 Number of literals 明显没有 100000
- 以上两点均说明 StringTable 区发生了垃圾回收

![image.png](image/1664095210138-320f3b06-cadf-4ccc-905b-8913bc34ae2e.png)

![image.png](image/1664095236739-a56ee7d9-8009-480d-a6ab-fbf100bb8e48.png)

## 7、G1 中的 String 去重操作
**官方文档**：[http://openjdk.java.net/jeps/192](http://openjdk.java.net/jeps/192)
暂时了解一下，后面会详解垃圾回收器
**String去重操作的背景**
注意不是字符串常量池的去重操作，字符串常量池本身就没有重复的

1. 背景：对许多Java应用（有大的也有小的）做的测试得出以下结果：
   - 堆存活数据集合里面String对象占了25%
   - 堆存活数据集合里面重复的String对象有13.5%
   - String对象的平均长度是45
2. 许多大规模的Java应用的瓶颈在于内存，测试表明，在这些类型的应用里面，Java堆中存活的数据集合差不多25%是String对象。更进一步，这里面差不多一半String对象是重复的，重复的意思是说：str1.equals(str2)= true。堆上存在重复的String对象必然是一种内存的浪费。这个项目将在G1垃圾收集器中实现自动持续对重复的String对象进行去重，这样就能避免浪费内存。

**String 去重的的实现**

1. 当垃圾收集器工作的时候，会访问堆上存活的对象。对每一个访问的对象都会检查是否是候选的要去重的String对象。
2. 如果是，把这个对象的一个引用插入到队列中等待后续的处理。一个去重的线程在后台运行，处理这个队列。处理队列的一个元素意味着从队列删除这个元素，然后尝试去重它引用的String对象。
3. 使用一个Hashtable来记录所有的被String对象使用的不重复的char数组。当去重的时候，会查这个Hashtable，来看堆上是否已经存在一个一模一样的char数组。
4. 如果存在，String对象会被调整引用那个数组，释放对原来的数组的引用，最终会被垃圾收集器回收掉。
5. 如果查找失败，char数组会被插入到Hashtable，这样以后的时候就可以共享这个数组了。

**命令行选项**

1. UseStringDeduplication(bool) ：开启String去重，默认是不开启的，需要手动开启。
2. PrintStringDeduplicationStatistics(bool) ：打印详细的去重统计信息
3. stringDeduplicationAgeThreshold(uintx) ：达到这个年龄的String对象被认为是去重的候选对象

# 十四、 垃圾回收概述
![](image/1664153879475-dbc399fb-6fcc-4fa5-8600-e8390fc8d49d.png)

1. Java 和 C++语言的区别，就在于垃圾收集技术和内存动态分配上，C++语言没有垃圾收集技术，需要程序员手动的收集。
2. 垃圾收集，不是Java语言的伴生产物。早在1960年，第一门开始使用内存动态分配和垃圾收集技术的Lisp语言诞生。
3. 关于垃圾收集有三个经典问题：
   - 哪些内存需要回收？
   - 什么时候回收？
   - 如何回收？
4. 垃圾收集机制是Java的招牌能力，极大地提高了开发效率。如今，垃圾收集几乎成为现代语言的标配，即使经过如此长时间的发展，Java的垃圾收集机制仍然在不断的演进中，不同大小的设备、不同特征的应用场景，对垃圾收集提出了新的挑战，这当然也是面试的热点。
## 1、大厂面试题
### 蚂蚁金服

1. 你知道哪几种垃圾回收器，各自的优缺点，重点讲一下CMS和G1？
2. JVM GC算法有哪些，目前的JDK版本采用什么回收算法？
3. G1回收器讲下回收过程GC是什么？为什么要有GC？
4. GC的两种判定方法？CMS收集器与G1收集器的特点
### 百度

1. 说一下GC算法，分代回收说下
2. 垃圾收集策略和算法
### 天猫

1. JVM GC原理，JVM怎么回收内存
2. CMS特点，垃圾回收算法有哪些？各自的优缺点，他们共同的缺点是什么？
### 滴滴

1. Java的垃圾回收器都有哪些，说下G1的应用场景，平时你是如何搭配使用垃圾回收器的
### 京东

1. 你知道哪几种垃圾收集器，各自的优缺点，重点讲下CMS和G1，
2. 包括原理，流程，优缺点。垃圾回收算法的实现原理
### 阿里

1. 讲一讲垃圾回收算法。
2. 什么情况下触发垃圾回收？
3. 如何选择合适的垃圾收集算法？
4. JVM有哪三种垃圾回收器？
### 字节跳动

1. 常见的垃圾回收器算法有哪些，各有什么优劣？
2. System.gc()和Runtime.gc()会做什么事情？
3. Java GC机制？GC Roots有哪些？
4. Java对象的回收方式，回收算法。
5. CMS和G1了解么，CMS解决什么问题，说一下回收的过程。
6. CMS回收停顿了几次，为什么要停顿两次?
## 2、什么是垃圾？

1. 垃圾是指**在运行程序中没有任何指针指向的对象**，这个对象就是需要被回收的垃圾。
2. 外文：An object is considered garbage when it can no longer be reached from any pointer in the running program.
3. 如果不及时对内存中的垃圾进行清理，那么，这些垃圾对象所占的内存空间会一直保留到应用程序结束，被保留的空间无法被其他对象使用。甚至可能导致内存溢出。
## 3、为什么需要GC？
**想要学习GC，首先需要理解为什么需要GC？**

1. 对于高级语言来说，一个基本认知是如果不进行垃圾回收，**内存迟早都会被消耗完**，因为不断地分配内存空间而不进行回收，就好像不停地生产生活垃圾而从来不打扫一样。
2. 除了释放没用的对象，垃圾回收也可以清除内存里的记录碎片。碎片整理将所占用的堆内存移到堆的一端，**以便JVM将整理出的内存分配给新的对象**。
3. 随着应用程序所应付的业务越来越庞大、复杂，用户越来越多，**没有GC就不能保证应用程序的正常进行**。而经常造成STW的GC又跟不上实际的需求，所以才会不断地尝试对GC进行优化。
## 4、早期垃圾回收

1. 在早期的C/C++时代，垃圾回收基本上是手工进行的。开发人员可以使用new关键字进行内存申请，并使用delete关键字进行内存释放。比如以下代码：
```cpp
  MibBridge *pBridge= new cmBaseGroupBridge（）；
  //如果注册失败，使用Delete释放该对象所占内存区域
  if（pBridge->Register（kDestroy）！=NO ERROR）
  	delete pBridge；
```

2. 这种方式可以灵活控制内存释放的时间，但是会给开发人员带来**频繁申请和释放内存的管理负担**。倘若有一处内存区间由于程序员编码的问题忘记被回收，那么就会产生**内存泄漏**，垃圾对象永远无法被清除，随着系统运行时间的不断增长，垃圾对象所耗内存可能持续上升，直到出现内存溢出并造成**应用程序崩溃**。
3. 有了垃圾回收机制后，上述代码极有可能变成这样
```cpp
  MibBridge *pBridge=new cmBaseGroupBridge(); 
  pBridge->Register(kDestroy);
```

4. 现在，除了Java以外，C#、Python、Ruby等语言都使用了自动垃圾回收的思想，也是未来发展趋势，可以说这种自动化的内存分配和来及回收方式已经成为了现代开发语言必备的标准。
## 5、Java 垃圾回收机制
### 自动内存管理
**官网介绍**：[https://docs.oracle.com/javase/8/docs/technotes/guides/vm/gctuning/toc.html](https://docs.oracle.com/javase/8/docs/technotes/guides/vm/gctuning/toc.html)
**自动内存管理的优点**

1. 自动内存管理，无需开发人员手动参与内存的分配与回收，这样降低内存泄漏和内存溢出的风险
2. 没有垃圾回收器，java也会和cpp一样，各种悬垂指针，野指针，泄露问题让你头疼不已。
3. 自动内存管理机制，将程序员从繁重的内存管理中释放出来，可以更专心地专注于业务开发

**关于自动内存管理的担忧**

1. 对于Java开发人员而言，自动内存管理就像是一个黑匣子，如果过度依赖于“自动”，那么这将会是一场灾难，最严重的就会**弱化Java开发人员在程序出现内存溢出时定位问题和解决问题的能力**。
2. 此时，了解JVM的自动内存分配和内存回收原理就显得非常重要，只有在真正了解JVM是如何管理内存后，我们才能够在遇见OutofMemoryError时，快速地根据错误异常日志定位问题和解决问题。
3. 当需要排查各种内存溢出、内存泄漏问题时，当垃圾收集成为系统达到更高并发量的瓶颈时，我们就必须对这些“自动化”的技术**实施必要的监控和调节**。
### 关注的区域
![](image/1664153879879-4644e18c-8e75-4939-b6b4-f5e012094f62.png)

1. 垃圾收集器可以对年轻代回收，也可以对老年代回收，甚至是全栈和方法区的回收，
2. 其中，**Java堆是垃圾收集器的工作重点**
3. 从次数上讲：
   1. 频繁收集Young区
   2. 较少收集Old区
   3. 基本不收集Perm区（元空间）
# 十五、 垃圾回收相关算法
## 1、标记阶段：引用计数算法
### 标记阶段的目的
**垃圾标记阶段：主要是为了判断对象是否存活**

1. 在堆里存放着几乎所有的Java对象实例，在GC执行垃圾回收之前，首先**需要区分出内存中哪些是存活对象，哪些是已经死亡的对象。只有被标记为己经死亡的对象，GC才会在执行垃圾回收时，释放掉其所占用的内存空间，因此这个过程我们可以称为垃圾标记阶段**。
2. 那么在JVM中究竟是如何标记一个死亡对象呢？简单来说，当一个对象已经不再被任何的存活对象继续引用时，就可以宣判为已经死亡。
3. 判断对象存活一般有两种方式：**引用计数算法**和**可达性分析算法**。
### 引用计数算法

1. 引用计数算法（Reference Counting）比较简单，对每个对象保存一个整型的引用计数器属性。用于记录对象被引用的情况。
2. 对于一个对象A，只要有任何一个对象引用了A，则A的引用计数器就加1；当引用失效时，引用计数器就减1。只要对象A的引用计数器的值为0，即表示对象A不可能再被使用，可进行回收。
3. 优点：实现简单，垃圾对象便于辨识；判定效率高，回收没有延迟性。
4. 缺点：
   1. 它需要单独的字段存储计数器，这样的做法增加了**存储空间的开销**。
   2. 每次赋值都需要更新计数器，伴随着加法和减法操作，这增加了**时间开销**。
   3. 引用计数器有一个严重的问题，即**无法处理循环引用**的情况。这是一条致命缺陷，导致在Java的垃圾回收器中没有使用这类算法。
### 循环引用
![](image/1664153879617-9c9a1896-f904-4198-9142-2b88ec0f78dd.png)
当p的指针断开的时候，内部的引用形成一个循环，计数器都还算1，无法被回收，这就是循环引用，从而造成内存泄漏
### 小结

1. 引用计数算法，是很多语言的资源回收选择，例如因人工智能而更加火热的Python，它更是同时支持引用计数和垃圾收集机制。
2. 具体哪种最优是要看场景的，业界有大规模实践中仅保留引用计数机制，以提高吞吐量的尝试。
3. Java并没有选择引用计数，是因为其存在一个基本的难题，也就是很难处理循环引用关系。
4. Python如何解决循环引用？
   - 手动解除：很好理解，就是在合适的时机，解除引用关系。
   - 使用弱引用weakref，weakref是Python提供的标准库，旨在解决循环引用。
## 2、标记阶段：可达性分析算法
**可达性分析算法：也可以称为根搜索算法、追踪性垃圾收集**

1. 相对于引用计数算法而言，可达性分析算法不仅同样具备实现简单和执行高效等特点，更重要的是该算法可以有效地**解决在引用计数算法中循环引用的问题，防止内存泄漏的发生**。
2. 相较于引用计数算法，这里的可达性分析就是Java、C#选择的。这种类型的垃圾收集通常也叫作**追踪性垃圾收集**（Tracing Garbage Collection）
### 实现思路

- 所谓"GCRoots”根集合就是一组必须活跃的引用
- 其基本思路如下：
1. 可达性分析算法是以根对象集合（GCRoots）为起始点，按照从上至下的方式**搜索被根对象集合所连接的目标对象是否可达。**
2. 使用可达性分析算法后，内存中的存活对象都会被根对象集合直接或间接连接着，搜索所走过的路径称为**引用链**（Reference Chain）
3. 如果目标对象没有任何引用链相连，则是不可达的，就意味着该对象己经死亡，可以标记为垃圾对象。
4. 在可达性分析算法中，只有能够被根对象集合直接或者间接连接的对象才是存活对象。

![](image/1664153880714-93067c63-93c3-4214-9ff6-a0d8e9c585b7.png)
### GC Roots 元素

1. 虚拟机栈中引用的对象
   - 比如：各个线程被调用的方法中使用到的参数、局部变量等。
2. 本地方法栈内JNI（通常说的本地方法）引用的对象
3. 方法区中类静态属性引用的对象
   - 比如：Java类的引用类型静态变量
4. 方法区中常量引用的对象
   - 比如：字符串常量池（StringTable）里的引用
5. 所有被同步锁synchronized持有的对象
6. Java虚拟机内部的引用。
   - 基本数据类型对应的Class对象，一些常驻的异常对象（如：NullPointerException、OutofMemoryError），系统类加载器。
7. 反映java虚拟机内部情况的JMXBean、JVMTI中注册的回调、本地代码缓存等。

![](image/1664153880710-1a0d238e-75ae-4e4a-893f-c6017ffa54ca.png)

1. 总结一句话就是，除了堆空间的周边，比如：虚拟机栈、本地方法栈、方法区、字符串常量池等地方对堆空间进行引用的，都可以作为GC Roots进行可达性分析
2. 除了这些固定的GC Roots集合以外，根据用户所选用的垃圾收集器以及当前回收的内存区域不同，还可以有其他对象“临时性”地加入，共同构成完整GC Roots集合。比如：**分代收集**和局部回收（PartialGC）。
   - 如果只针对Java堆中的某一块区域进行垃圾回收（比如：典型的只针对新生代），必须考虑到内存区域是虚拟机自己的实现细节，更不是孤立封闭的，这个区域的对象完全有可能被其他区域的对象所引用，这时候就需要一并将关联的区域对象也加入GC Roots集合中去考虑，才能保证可达性分析的准确性。

**小技巧**
由于Root采用栈方式存放变量和指针，所以如果一个指针，它保存了堆内存里面的对象，但是自己又不存放在堆内存里面，那它就是一个Root。
### 注意

1. 如果要使用可达性分析算法来判断内存是否可回收，那么分析工作必须在一个能保障一致性的快照中进行。这点不满足的话分析结果的准确性就无法保证。
2. 这点也是导致GC进行时必须“Stop The World”的一个重要原因。即使是号称（几乎）不会发生停顿的CMS收集器中，**枚举根节点时也是必须要停顿的**。
## 3、finalization 机制
### finalize() 方法机制
**对象销毁前的回调函数：finalize()**

1. Java语言提供了对象终止（finalization）机制来允许开发人员提供**对象被销毁之前的自定义处理逻辑**。
2. 当垃圾回收器发现没有引用指向一个对象，即：垃圾回收此对象之前，总会先调用这个对象的finalize()方法。
3. finalize() 方法允许在子类中被重写，**用于在对象被回收时进行资源释放**。通常在这个方法中进行一些资源释放和清理的工作，比如关闭文件、套接字和数据库连接等。

Object 类中 finalize() 源码
```java
// 等待被重写
protected void finalize() throws Throwable { }
```

1. 永远不要主动调用某个对象的finalize()方法，应该交给垃圾回收机制调用。理由包括下面三点：
   1. 在finalize()时可能会导致对象复活。
   2. finalize()方法的执行时间是没有保障的，它完全由GC线程决定，极端情况下，若不发生GC，则finalize()方法将没有执行机会。
   3. 一个糟糕的finalize()会严重影响GC的性能。比如finalize是个死循环
2. 从功能上来说，finalize()方法与C++中的析构函数比较相似，但是Java采用的是基于垃圾回收器的自动内存管理机制，所以finalize()方法在**本质上不同于C++中的析构函数**。
3. finalize()方法对应了一个finalize线程，因为优先级比较低，即使主动调用该方法，也不会因此就直接进行回收
### 生存还是死亡？
由于finalize()方法的存在，**虚拟机中的对象一般处于三种可能的状态。**
如果从所有的根节点都无法访问到某个对象，说明对象己经不再使用了。一般来说，此对象需要被回收。但事实上，也并非是“非死不可”的，这时候它们暂时处于“缓刑”阶段。**一个无法触及的对象有可能在某一个条件下“复活”自己**，如果这样，那么对它立即进行回收就是不合理的。为此，定义虚拟机中的对象可能的三种状态。如下：

1. 可触及的：从根节点开始，可以到达这个对象。
2. 可复活的：对象的所有引用都被释放，但是对象有可能在finalize()中复活。
3. 不可触及的：对象的finalize()被调用，并且没有复活，那么就会进入不可触及状态。
   - 不可触及的对象不可能被复活，**因为finalize()只会被调用一次**。

以上3种状态中，是由于finalize()方法的存在，进行的区分。只有在对象不可触及时才可以被回收。
### 具体过程
判定一个对象objA是否可回收，至少要经历两次标记过程：

1. 如果对象objA到GC Roots没有引用链，则进行第一次标记。
2. 进行筛选，判断此对象是否有必要执行finalize()方法
   1. 如果对象objA没有重写finalize()方法，或者finalize()方法已经被虚拟机调用过，则虚拟机视为“没有必要执行”，objA被判定为不可触及的。
   2. 如果对象objA重写了finalize()方法，且还未执行过，那么objA会被插入到F-Queue队列中，由一个虚拟机自动创建的、低优先级的Finalizer线程触发其finalize()方法执行。
   3. finalize()方法是对象逃脱死亡的最后机会，稍后GC会对F-Queue队列中的对象进行第二次标记。如果objA在finalize()方法中与引用链上的任何一个对象建立了联系，那么在第二次标记时，objA会被移出“即将回收”集合。之后，对象会再次出现没有引用存在的情况。在这个情况下，finalize()方法不会被再次调用，对象会直接变成不可触及的状态，也就是说，一个对象的finalize()方法只会被调用一次。

**通过 JVisual VM 查看 Finalizer 线程**
![](image/1664153880613-f1b68c34-ad99-49c4-82c0-4422be508ce4.png)
### 演示复活对象
我们重写 CanReliveObj 类的 finalize()方法，在调用其 finalize()方法时，将 obj 指向当前类对象 this
```java
/**
 * 测试Object类中finalize()方法，即对象的finalization机制。
 *
 */
public class CanReliveObj {
    public static CanReliveObj obj;//类变量，属于 GC Root


    //此方法只能被调用一次
    @Override
    protected void finalize() throws Throwable {
        super.finalize();
        System.out.println("调用当前类重写的finalize()方法");
        obj = this;//当前待回收的对象在finalize()方法中与引用链上的一个对象obj建立了联系
    }


    public static void main(String[] args) {
        try {
            obj = new CanReliveObj();
            // 对象第一次成功拯救自己
            obj = null;
            System.gc();//调用垃圾回收器
            System.out.println("第1次 gc");
            // 因为Finalizer线程优先级很低，暂停2秒，以等待它
            Thread.sleep(2000);
            if (obj == null) {
                System.out.println("obj is dead");
            } else {
                System.out.println("obj is still alive");
            }
            System.out.println("第2次 gc");
            // 下面这段代码与上面的完全相同，但是这次自救却失败了
            obj = null;
            System.gc();
            // 因为Finalizer线程优先级很低，暂停2秒，以等待它
            Thread.sleep(2000);
            if (obj == null) {
                System.out.println("obj is dead");
            } else {
                System.out.println("obj is still alive");
            }
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}

```
**如果注释掉finalize()方法**
```java
 //此方法只能被调用一次
    @Override
    protected void finalize() throws Throwable {
        super.finalize();
        System.out.println("调用当前类重写的finalize()方法");
        obj = this;//当前待回收的对象在finalize()方法中与引用链上的一个对象obj建立了联系
    }
```
输出结果：
```bash
第1次 gc
obj is dead
第2次 gc
obj is dead
```
**放开finalize()方法**
输出结果：
```bash
第1次 gc
调用当前类重写的finalize()方法
obj is still alive
第2次 gc
obj is dead
```
第一次自救成功，但由于 finalize() 方法只会执行一次，所以第二次自救失败
## 4、MAT与JProfiler的GC Roots溯源
### MAT 介绍

- MAT是Memory Analyzer的简称，它是一款功能强大的Java堆内存分析器。用于查找内存泄漏以及查看内存消耗情况。
- MAT是基于Eclipse开发的，是一款免费的性能分析工具。
- 可以在[http://www.eclipse.org/mat/](http://www.eclipse.org/mat/%E4%B8%8B%E8%BD%BD%E5%B9%B6%E4%BD%BF%E7%94%A8MAT) 下载使用
> 虽然Jvisualvm很强大，但是在内存分析方面，还是MAT更好用一些
> 此小节主要是为了实时分析GC Roots是哪些东西，中间需要用到一个dump的文件

### 获取 dump 文件
#### 命令行使用 jmap 获取
![](image/1664153881837-cf769a5c-3435-46bf-aad9-860e2231d233.png)
#### 使用JVisualVM
捕获的heap dump文件是一个临时文件，关闭JVisualVM后自动删除，若要保留，需要将其另存为文件。可通过以下方法捕获heap dump：
代码：
> numList 和 birth 在第一次捕捉内存快照的时候，为 GC Roots
> 之后 numList 和 birth 置为 null ，对应的引用对象被回收，在第二次捕捉内存快照的时候，就不再是 GC Roots

```java
public class GCRootsTest {
    public static void main(String[] args) {
        List<Object> numList = new ArrayList<>();
        Date birth = new Date();

        for (int i = 0; i < 100; i++) {
            numList.add(String.valueOf(i));
            try {
                Thread.sleep(10);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

        System.out.println("数据添加完毕，请操作：");
        new Scanner(System.in).next();
        numList = null;
        birth = null;

        System.out.println("numList、birth已置空，请操作：");
        new Scanner(System.in).next();

        System.out.println("结束");
    }
}

```
**捕捉堆内存快照**
1、先执行第一步，然后停下来，去生成此步骤dump文件
![](image/1664153881963-7237dc1e-54c8-4a13-8e9d-b7344f8f6034.png)
2、 点击【堆 Dump】
![](image/1664153882815-1d743f4b-6b32-4cce-b675-8428027f1bbd.png)
3、右键 --> 另存为即可
[![](https://cdn.nlark.com/yuque/0/2022/jpeg/26368762/1664153883271-9a4401f6-62f2-4138-8423-5e039c4dde78.jpeg#clientId=ueb17fe36-951f-4&crop=0&crop=0&crop=1&crop=1&from=paste&id=u94ea5b73&margin=%5Bobject%20Object%5D&originHeight=884&originWidth=1461&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u4ae2018f-6635-4753-9b33-ab825b92dbb&title=)](https://camo.githubusercontent.com/ffb781f842377c01fd1ddfa1d6ca45c8da31cff8ba8a438cc11b0997d5d3341e/68747470733a2f2f6e706d2e656c656d6563646e2e636f6d2f796f7574686c716c40312e302e382f4a564d2f636861707465725f3031302f303031322e6a7067)
4、输入命令，继续执行程序
![](image/1664153884150-f130265c-a18a-45bf-9a27-c3f76cbe767a.png)
5、我们接着捕获第二张堆内存快照
[![](https://cdn.nlark.com/yuque/0/2022/jpeg/26368762/1664153885103-fd549d1a-d2bc-4243-be09-4491e4452663.jpeg#clientId=ueb17fe36-951f-4&crop=0&crop=0&crop=1&crop=1&from=paste&id=u9b1c16bf&margin=%5Bobject%20Object%5D&originHeight=872&originWidth=1486&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=ub1a51f6b-6c12-451d-a7ac-1a509f78290&title=)](https://camo.githubusercontent.com/1802f269e35dc4f5ef77af1e9ac2461f443085f4a2d33a0e9404bcbe0bbb9142/68747470733a2f2f6e706d2e656c656d6563646e2e636f6d2f796f7574686c716c40312e302e382f4a564d2f636861707465725f3031302f303031342e6a7067)
### MAT 查看堆内存快照
1、打开 MAT ，选择File --> Open File，打开刚刚的两个dump文件，**我们先打开第一个dump文件**
点击Open Heap Dump也行
![](image/1664153893861-83603e61-72c9-4d69-b08a-4c495b0e7d21.png)
2、选择Java Basics --> GC Roots
![](image/1664153895982-ae50a6cc-416d-4c79-9ff3-e555abccdfe0.png)
3、第一次捕捉堆内存快照时，GC Roots 中包含我们定义的两个局部变量，类型分别为 ArrayList 和 Date，Total:21
[![](https://cdn.nlark.com/yuque/0/2022/jpeg/26368762/1664153896064-ea738247-d6ec-4212-9b80-30b6f6f36358.jpeg#clientId=ueb17fe36-951f-4&crop=0&crop=0&crop=1&crop=1&from=paste&id=u4be76130&margin=%5Bobject%20Object%5D&originHeight=740&originWidth=1300&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=uc37fa37d-c643-45e1-935f-337b1ea112b&title=)](https://camo.githubusercontent.com/9bb4ae0a6a8a250160ef2ac50fdb20e205ab4303d2a5391be874ee460d6fc074/68747470733a2f2f6e706d2e656c656d6563646e2e636f6d2f796f7574686c716c40312e302e382f4a564d2f636861707465725f3031302f303031372e6a7067)
4、打开第二个dump文件，第二次捕获内存快照时，由于两个局部变量引用的对象被释放，所以这两个局部变量不再作为 GC Roots ，从 Total Entries = 19 也可以看出（少了两个 GC Roots）
[![](https://cdn.nlark.com/yuque/0/2022/jpeg/26368762/1664153897282-e11f31af-6343-46b4-94c7-aed1966c26b1.jpeg#clientId=ueb17fe36-951f-4&crop=0&crop=0&crop=1&crop=1&from=paste&id=u8ed9bb04&margin=%5Bobject%20Object%5D&originHeight=750&originWidth=1040&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=uc38e9b79-0cbd-40b4-b16b-daa4f005a93&title=)](https://camo.githubusercontent.com/21bf6eea502c4d2777c63ec2dca3e3a96960bfc80ffa79c951658c9727407372/68747470733a2f2f6e706d2e656c656d6563646e2e636f6d2f796f7574686c716c40312e302e382f4a564d2f636861707465725f3031302f303031382e6a7067)
### JProfiler GC Roots 溯源
1、在实际开发中，我们很少会查看所有的GC Roots。一般都是查看某一个或几个对象的GC Root是哪个，这个过程叫**GC Roots 溯源**
2、下面我们使用使用 JProfiler 进行 GC Roots 溯源演示
依然用上面代码
1、
[![](https://cdn.nlark.com/yuque/0/2022/jpeg/26368762/1664153897585-566e4a8a-3c63-4af6-ae8e-ef8962055ca7.jpeg#clientId=ueb17fe36-951f-4&crop=0&crop=0&crop=1&crop=1&from=paste&id=u6b5c8ae2&margin=%5Bobject%20Object%5D&originHeight=712&originWidth=1300&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u863abaa9-61ef-4fef-9250-72e39475825&title=)](https://camo.githubusercontent.com/4701d4c35a3c3498643856b05e2dbf9bacdcbc2bff81f8c8c6a513d8af0a14ef/68747470733a2f2f6e706d2e656c656d6563646e2e636f6d2f796f7574686c716c40312e302e382f4a564d2f636861707465725f3031302f303031392e6a7067)
2、
![](image/1664153900051-280fcb59-f2cb-44f8-baec-7cd7ac4acba0.png)
[![](https://cdn.nlark.com/yuque/0/2022/jpeg/26368762/1664153900608-1612ea11-bec7-49e7-825c-1cc9d05ed688.jpeg#clientId=ueb17fe36-951f-4&crop=0&crop=0&crop=1&crop=1&from=paste&id=u45b47304&margin=%5Bobject%20Object%5D&originHeight=587&originWidth=1300&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u6a1ffc60-525b-4310-864a-b2c3b83beef&title=)](https://camo.githubusercontent.com/38f47697da87ad045c67430b391a252687d08683166f8e348cdaf1f3101b9b41/68747470733a2f2f6e706d2e656c656d6563646e2e636f6d2f796f7574686c716c40312e302e382f4a564d2f636861707465725f3031302f303032312e6a7067)
可以发现颜色变绿了，可以动态的看变化
3、右击对象，选择 Show Selection In Heap Walker，单独的查看某个对象
![](image/1664153900581-0eb38433-cd54-4829-bbe8-65e65030cbb7.png)
![](image/1664153901789-261ee648-d78e-4b95-9b67-f8bf1c818bea.png)
4、选择Incoming References，表示追寻 GC Roots 的源头
点击Show Paths To GC Roots，在弹出界面中选择默认设置即可
[![](https://cdn.nlark.com/yuque/0/2022/jpeg/26368762/1664153902609-03243623-0911-4668-a8ca-5b5d326b9b2d.jpeg#clientId=ueb17fe36-951f-4&crop=0&crop=0&crop=1&crop=1&from=paste&id=u68195a1a&margin=%5Bobject%20Object%5D&originHeight=524&originWidth=1300&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u21371d58-e2c3-4b1e-a14b-bd39ff594db&title=)](https://camo.githubusercontent.com/6b4fc31a2754d74563fa5908ef0a3839d4960df9ecf8083c6ad116c9bc59fe0d/68747470733a2f2f6e706d2e656c656d6563646e2e636f6d2f796f7574686c716c40312e302e382f4a564d2f636861707465725f3031302f303032342e6a7067)
![](image/1664153910478-427a8ca1-16b8-404c-82cb-a682e8146abb.png)
![](image/1664153911633-5c0676ec-cf81-46c2-b4c0-6badce79d199.png)
### JProfiler 分析 OOM
这里是简单的讲一下，后面篇章会详解
```java
/**
 * -Xms8m -Xmx8m 
 * -XX:+HeapDumpOnOutOfMemoryError  这个参数的意思是当程序出现OOM的时候就会在当前工程目录生成一个dump文件
 */
public class HeapOOM {
    byte[] buffer = new byte[1 * 1024 * 1024];//1MB

    public static void main(String[] args) {
        ArrayList<HeapOOM> list = new ArrayList<>();

        int count = 0;
        try{
            while(true){
                list.add(new HeapOOM());
                count++;
            }
        }catch (Throwable e){
            System.out.println("count = " + count);
            e.printStackTrace();
        }
    }
}
```
程序输出日志
```bash
com.atguigu.java.HeapOOM
java.lang.OutOfMemoryError: Java heap space
Dumping heap to java_pid14608.hprof ...
java.lang.OutOfMemoryError: Java heap space
	at com.atguigu.java.HeapOOM.<init>(HeapOOM.java:12)
	at com.atguigu.java.HeapOOM.main(HeapOOM.java:20)
Heap dump file created [7797849 bytes in 0.010 secs]
count = 6
```
打开这个dump文件
1、看这个超大对象
![](image/1664153912402-38eb0022-1ea0-4e12-86c6-776d015318b6.png)
2、揪出 main() 线程中出问题的代码
![](image/1664153913356-10fd8d50-ba9a-462a-96c5-66c6fdc06050.png)
## 5、清除阶段：标记-清除算法
**垃圾清除阶段**

- 当成功区分出内存中存活对象和死亡对象后，GC接下来的任务就是执行垃圾回收，释放掉无用对象所占用的内存空间，以便有足够的可用内存空间为新对象分配内存。目前在JVM中比较常见的三种垃圾收集算法是
1. **标记-清除算法**（Mark-Sweep）
2. **复制算法**（Copying）
3. **标记-压缩算法**（Mark-Compact）

**背景**
标记-清除算法（Mark-Sweep）是一种非常基础和常见的垃圾收集算法，该算法被J.McCarthy等人在1960年提出并并应用于Lisp语言。
**执行过程**
当堆中的有效内存空间（available memory）被耗尽的时候，就会停止整个程序（也被称为stop the world），然后进行两项工作，第一项则是标记，第二项则是清除

1. 标记：Collector从引用根节点开始遍历，标记所有被引用的对象。一般是在对象的Header中记录为可达对象。
   - 注意：标记的是被引用的对象，也就是可达对象，并非标记的是即将被清除的垃圾对象
2. 清除：Collector对堆内存从头到尾进行线性的遍历，如果发现某个对象在其Header中没有标记为可达对象，则将其回收

![](image/1664153913681-990ab669-a9d4-4a16-a1aa-bb4ec502fc7d.png)
**标记-清除算法的缺点**

1. 标记清除算法的效率不算高
2. 在进行GC的时候，需要停止整个应用程序，用户体验较差
3. 这种方式清理出来的空闲内存是不连续的，产生内碎片，需要维护一个空闲列表

**注意：何为清除？**
这里所谓的清除并不是真的置空，而是把需要清除的对象地址保存在空闲的地址列表里。下次有新对象需要加载时，判断垃圾的位置空间是否够，如果够，就存放（也就是覆盖原有的地址）。
关于空闲列表是在为对象分配内存的时候提过：

1. 如果内存规整
   - 采用指针碰撞的方式进行内存分配
2. 如果内存不规整
   - 虚拟机需要维护一个空闲列表
   - 采用空闲列表分配内存
## 6、清除阶段：复制算法
**背景**

1. 为了解决标记-清除算法在垃圾收集效率方面的缺陷，M.L.Minsky于1963年发表了著名的论文，“使用双存储区的Lisp语言垃圾收集器CA LISP Garbage Collector Algorithm Using Serial Secondary Storage）”。M.L.Minsky在该论文中描述的算法被人们称为复制（Copying）算法，它也被M.L.Minsky本人成功地引入到了Lisp语言的一个实现版本中。

**核心思想**
将活着的内存空间分为两块，每次只使用其中一块，在垃圾回收时将正在使用的内存中的存活对象复制到未被使用的内存块中，之后清除正在使用的内存块中的所有对象，交换两个内存的角色，最后完成垃圾回收
![](image/1664153917002-d2c396c7-f1f8-4f07-905b-1fac1612b7ce.png)
新生代里面就用到了复制算法，Eden区和S0区存活对象整体复制到S1区
**复制算法的优缺点**
**优点**

1. 没有标记和清除过程，实现简单，运行高效
2. 复制过去以后保证空间的连续性，不会出现“碎片”问题。

**缺点**

1. 此算法的缺点也是很明显的，就是需要两倍的内存空间。
2. 对于G1这种分拆成为大量region的GC，复制而不是移动，意味着GC需要维护region之间对象引用关系，不管是内存占用或者时间开销也不小

**复制算法的应用场景**

1. 如果系统中的垃圾对象很多，复制算法需要复制的存活对象数量并不会太大，效率较高
2. 老年代大量的对象存活，那么复制的对象将会有很多，效率会很低
3. 在新生代，对常规应用的垃圾回收，一次通常可以回收70% - 99% 的内存空间。回收性价比很高。所以现在的商业虚拟机都是用这种收集算法回收新生代。

![](image/1664153917239-9d0fc5e9-8236-4e20-8c98-1e4f08d106fe.png)
## 7、清除阶段：标记-压缩算法
**标记-压缩（或标记-整理、Mark - Compact）算法**
**背景**

1. 复制算法的高效性是建立在存活对象少、垃圾对象多的前提下的。这种情况在新生代经常发生，但是在老年代，更常见的情况是大部分对象都是存活对象。如果依然使用复制算法，由于存活对象较多，复制的成本也将很高。因此，**基于老年代垃圾回收的特性，需要使用其他的算法。**
2. 标记-清除算法的确可以应用在老年代中，但是该算法不仅执行效率低下，而且在执行完内存回收后还会产生内存碎片，所以JVM的设计者需要在此基础之上进行改进。标记-压缩（Mark-Compact）算法由此诞生。
3. 1970年前后，G.L.Steele、C.J.Chene和D.s.Wise等研究者发布标记-压缩算法。在许多现代的垃圾收集器中，人们都使用了标记-压缩算法或其改进版本。

**执行过程**

1. 第一阶段和标记清除算法一样，从根节点开始标记所有被引用对象
2. 第二阶段将所有的存活对象压缩到内存的一端，按顺序排放。之后，清理边界外所有的空间。

![](image/1664153918801-a256ceca-e91e-457b-8beb-1fcddddc1618.png)
**标记-压缩算法与标记-清除算法的比较**

1. 标记-压缩算法的最终效果等同于标记-清除算法执行完成后，再进行一次内存碎片整理，因此，也可以把它称为标记-清除-压缩（Mark-Sweep-Compact）算法。
2. 二者的本质差异在于标记-清除算法是一种**非移动式的回收算法**，标记-压缩是**移动式的**。是否移动回收后的存活对象是一项优缺点并存的风险决策。
3. 可以看到，标记的存活对象将会被整理，按照内存地址依次排列，而未被标记的内存会被清理掉。如此一来，当我们需要给新对象分配内存时，JVM只需要持有一个内存的起始地址即可，这比维护一个空闲列表显然少了许多开销。

**标记-压缩算法的优缺点**
**优点**

1. 消除了标记-清除算法当中，内存区域分散的缺点，我们需要给新对象分配内存时，JVM只需要持有一个内存的起始地址即可。
2. 消除了复制算法当中，内存减半的高额代价。

**缺点**

1. 从效率上来说，标记-整理算法要低于复制算法。
2. 移动对象的同时，如果对象被其他对象引用，则还需要调整引用的地址（因为HotSpot虚拟机采用的不是句柄池的方式，而是直接指针）
3. 移动过程中，需要全程暂停用户应用程序。即：STW
## 8、垃圾回收算法小结
**对比三种清除阶段的算法**

1. 效率上来说，复制算法是当之无愧的老大，但是却浪费了太多内存。
2. 而为了尽量兼顾上面提到的三个指标，标记-整理算法相对来说更平滑一些，但是效率上不尽如人意，它比复制算法多了一个标记的阶段，比标记-清除多了一个整理内存的阶段。
|              | **标记清除**       | **标记整理**     | **复制**                              |
| ------------ | ------------------ | ---------------- | ------------------------------------- |
| **速率**     | 中等               | 最慢             | 最快                                  |
| **空间开销** | 少（但会堆积碎片） | 少（不堆积碎片） | 通常需要活对象的2倍空间（不堆积碎片） |
| **移动对象** | 否                 | 是               | 是                                    |

## 9、分代收集算法
Q：难道就没有一种最优的算法吗？
A：无，没有最好的算法，只有最合适的算法
**为什么要使用分代收集算法**

1. 前面所有这些算法中，并没有一种算法可以完全替代其他算法，它们都具有自己独特的优势和特点。分代收集算法应运而生。
2. 分代收集算法，是基于这样一个事实：**不同的对象的生命周期是不一样的。因此，不同生命周期的对象可以采取不同的收集方式，以便提高回收效率。**一般是把Java堆分为新生代和老年代，这样就可以根据各个年代的特点使用不同的回收算法，以提高垃圾回收的效率。
3. 在Java程序运行的过程中，会产生大量的对象，其中有些对象是与业务信息相关:
   - 比如Http请求中的Session对象、线程、Socket连接，这类对象跟业务直接挂钩，因此生命周期比较长。
   - 但是还有一些对象，主要是程序运行过程中生成的临时变量，这些对象生命周期会比较短，比如：String对象，由于其不变类的特性，系统会产生大量的这些对象，有些对象甚至只用一次即可回收。

**目前几乎所有的GC都采用分代收集算法执行垃圾回收的**
在HotSpot中，基于分代的概念，GC所使用的内存回收算法必须结合年轻代和老年代各自的特点。

1. 年轻代（Young Gen）
   - 年轻代特点：区域相对老年代较小，对象生命周期短、存活率低，回收频繁。
   - 这种情况复制算法的回收整理，速度是最快的。复制算法的效率只和当前存活对象大小有关，因此很适用于年轻代的回收。而复制算法内存利用率不高的问题，通过hotspot中的两个survivor的设计得到缓解。
2. 老年代（Tenured Gen）
   - 老年代特点：区域较大，对象生命周期长、存活率高，回收不及年轻代频繁。
   - 这种情况存在大量存活率高的对象，复制算法明显变得不合适。一般是由标记-清除或者是标记-清除与标记-整理的混合实现。
      - Mark阶段的开销与存活对象的数量成正比。
      - Sweep阶段的开销与所管理区域的大小成正相关。
      - Compact阶段的开销与存活对象的数据成正比。
3. 以HotSpot中的CMS回收器为例，CMS是基于Mark-Sweep实现的，对于对象的回收效率很高。对于碎片问题，CMS采用基于Mark-Compact算法的Serial Old回收器作为补偿措施：当内存回收不佳（碎片导致的Concurrent Mode Failure时），将采用Serial Old执行Full GC以达到对老年代内存的整理。
4. 分代的思想被现有的虚拟机广泛使用。几乎所有的垃圾回收器都区分新生代和老年代
## 10、增量收集算法和分区算法
### 增量收集算法
上述现有的算法，在垃圾回收过程中，应用软件将处于一种Stop the World的状态。在**Stop the World**状态下，应用程序所有的线程都会挂起，暂停一切正常的工作，等待垃圾回收的完成。如果垃圾回收时间过长，应用程序会被挂起很久，将严重影响用户体验或者系统的稳定性。为了解决这个问题，即对实时垃圾收集算法的研究直接导致了增量收集（Incremental Collecting）算法的诞生。
**增量收集算法基本思想**

1. 如果一次性将所有的垃圾进行处理，需要造成系统长时间的停顿，那么就可以让垃圾收集线程和应用程序线程交替执行。**每次，垃圾收集线程只收集一小片区域的内存空间，接着切换到应用程序线程。依次反复，直到垃圾收集完成。**
2. 总的来说，增量收集算法的基础仍是传统的标记-清除和复制算法。增量收集算法通过**对线程间冲突的妥善处理，允许垃圾收集线程以分阶段的方式完成标记、清理或复制工作**

**增量收集算法的缺点**
使用这种方式，由于在垃圾回收过程中，间断性地还执行了应用程序代码，所以能减少系统的停顿时间。但是，因为线程切换和上下文转换的消耗，会使得垃圾回收的总体成本上升，**造成系统吞吐量的下降**。
### 分区算法
主要针对G1收集器来说的

1. 一般来说，在相同条件下，堆空间越大，一次GC时所需要的时间就越长，有关GC产生的停顿也越长。为了更好地控制GC产生的停顿时间，将一块大的内存区域分割成多个小块，根据目标的停顿时间，每次合理地回收若干个小区间，而不是整个堆空间，从而减少一次GC所产生的停顿。
2. 分代算法将按照对象的生命周期长短划分成两个部分，分区算法将整个堆空间划分成连续的不同小区间。每一个小区间都独立使用，独立回收。这种算法的好处是可以控制一次回收多少个小区间。

![](image/1664153917820-c169fb3f-c836-4b98-bf63-9f3f61f89229.png)
## 11、写在最后
注意，这些只是基本的算法思路，实际GC实现过程要复杂的多，目前还在发展中的前沿GC都是复合算法，并且并行和并发兼备。


# 十六、 垃圾回收相关概念
## 1、System.gc()

1. 在默认情况下，通过System.gc()是对Runtime.getRuntime().gc() 的调用。
2. **会显式触发Full GC**，同时对老年代和新生代进行回收，尝试释放被丢弃对象占用的内存。
3. 然而System.gc()调用附带一个免责声明，无法保证对垃圾收集器的调用(不能确保立即生效)。
4. JVM实现者可以通过System.gc() 调用来决定JVM的GC行为。而一般情况下，垃圾回收应该是自动进行的，无须手动触发。
5. 在一些特殊情况下，如我们正在编写一个性能基准，我们可以在运行之间调用System.gc()。

**代码示例：手动执行 GC 操作**
```java
public class SystemGCTest {
    public static void main(String[] args) {
        new SystemGCTest();
        System.gc();//提醒jvm的垃圾回收器执行gc,但是不确定是否马上执行gc
        //与Runtime.getRuntime().gc();的作用一样。

//        System.runFinalization();//强制调用使用引用的对象的finalize()方法
    }
    //如果发生了GC，这个finalize()一定会被调用
    @Override
    protected void finalize() throws Throwable {
        super.finalize();
        System.out.println("SystemGCTest 重写了finalize()");
    }
}
```
输出结果不确定：有时候会调用 finalize() 方法，有时候并不会调用
**手动 GC 理解不可达对象的回收行为**
```java
//加上参数：  -XX:+PrintGCDetails
public class LocalVarGC {
    // 执行 System.gc() 仅仅是将年轻代的 buffer 数组对象放到了老年代，buffer对象仍然没有回收
    public void localvarGC1() {
        byte[] buffer = new byte[10 * 1024 * 1024];//10MB
        System.gc();
    }

    // 由于 buffer 数组对象没有引用指向它，执行 System.gc() 将被回收
    public void localvarGC2() {
        byte[] buffer = new byte[10 * 1024 * 1024];
        buffer = null;
        System.gc();
    }

    // 虽然出了代码块的作用域，但是 buffer 数组对象并没有被回收
    // 因为局部变量表的槽还在，没有被覆盖
    public void localvarGC3() {
        {
            byte[] buffer = new byte[10 * 1024 * 1024];
        }
        System.gc();
    }

    // 槽被覆盖后，彻底没有指针指向，数组对象被回收
    public void localvarGC4() {
        {
            byte[] buffer = new byte[10 * 1024 * 1024];
        }
        int value = 10;
        System.gc();
    }

    // 局部变量除了方法范围就是失效了，堆中的字节数组铁定被回收
    public void localvarGC5() {
        localvarGC1();
        System.gc();
    }

    public static void main(String[] args) {
        LocalVarGC local = new LocalVarGC();
        //通过在main方法调用这几个方法进行测试
        local.localvarGC1();
    }
}

```
> 这里需要注意大对象阈值

## 2、内存溢出与内存泄漏
### 内存溢出

1. 内存溢出相对于内存泄漏来说，尽管更容易被理解，但是同样的，内存溢出也是引发程序崩溃的罪魁祸首之一。
2. 由于GC一直在发展，所有一般情况下，除非应用程序占用的内存增长速度非常快，造成垃圾回收已经跟不上内存消耗的速度，否则不太容易出现OOM的情况。
3. 大多数情况下，GC会进行各种年龄段的垃圾回收，实在不行了就放大招，来一次独占式的Full GC操作，这时候会回收大量的内存，供应用程序继续使用。
4. Javadoc中对OutofMemoryError的解释是，没有空闲内存，并且垃圾收集器也无法提供更多内存。

**内存溢出（OOM）原因分析**
首先说没有空闲内存的情况：说明Java虚拟机的堆内存不够。原因有二：

1. Java虚拟机的堆内存设置不够。
   - 比如：可能存在内存泄漏问题；也很有可能就是堆的大小不合理，比如我们要处理比较可观的数据量，但是没有显式指定JVM堆大小或者指定数值偏小。我们可以通过参数-Xms 、-Xmx来调整。
2. 代码中创建了大量大对象，并且长时间不能被垃圾收集器收集（存在被引用）
   - 对于老版本的Oracle JDK，因为永久代的大小是有限的，并且JVM对永久代垃圾回收（如，常量池回收、卸载不再需要的类型）非常不积极，所以当我们不断添加新类型的时候，永久代出现OutOfMemoryError也非常多见。尤其是在运行时存在大量动态类型生成的场合；类似intern字符串缓存占用太多空间，也会导致OOM问题。对应的异常信息，会标记出来和永久代相关：“java.lang.OutOfMemoryError:PermGen space"。
   - 随着元数据区的引入，方法区内存已经不再那么窘迫，所以相应的OOM有所改观，出现OOM，异常信息则变成了：“java.lang.OutofMemoryError:Metaspace"。直接内存不足，也会导致OOM。
3. 这里面隐含着一层意思是，在抛出OutofMemoryError之前，通常垃圾收集器会被触发，尽其所能去清理出空间。
   - 例如：在引用机制分析中，涉及到JVM会去尝试**回收软引用指向的对象**等。
   - 在java.nio.Bits.reserveMemory()方法中，我们能清楚的看到，System.gc()会被调用，以清理空间。
4. 当然，也不是在任何情况下垃圾收集器都会被触发的
   - 比如，我们去分配一个超大对象，类似一个超大数组超过堆的最大值，JVM可以判断出垃圾收集并不能解决这个问题，所以直接抛出OutofMemoryError。
### 内存泄漏

1. 也称作“存储渗漏”。严格来说，**只有对象不会再被程序用到了，但是GC又不能回收他们的情况，才叫内存泄漏。**
2. 但实际情况很多时候一些不太好的实践（或疏忽）会导致对象的生命周期变得很长甚至导致OOM，也可以叫做宽泛意义上的“内存泄漏”。
3. 尽管内存泄漏并不会立刻引起程序崩溃，但是一旦发生内存泄漏，程序中的可用内存就会被逐步蚕食，直至耗尽所有内存，最终出现OutofMemory异常，导致程序崩溃。
4. 注意，这里的存储空间并不是指物理内存，而是指虚拟内存大小，这个虚拟内存大小取决于磁盘交换区设定的大小。

**内存泄露官方例子**
左边的图：Java使用可达性分析算法，最上面的数据不可达，就是需要被回收的对象。
右边的图：后期有一些对象不用了，按道理应该断开引用，但是存在一些链没有断开（图示中的Forgotten Reference Memory Leak），从而导致没有办法被回收。
![](image/1664240345892-7c64afa7-2668-4d58-8ff8-beea88563ce3.png)
**常见例子**

1. 单例模式
   - 单例的生命周期和应用程序是一样长的，所以在单例程序中，如果持有对外部对象的引用的话，那么这个外部对象是不能被回收的，则会导致内存泄漏的产生。
2. 一些提供close()的资源未关闭导致内存泄漏
   - 数据库连接 dataSourse.getConnection()，网络连接socket和io连接必须手动close，否则是不能被回收的。
## 3、Stop the World

1. Stop-the-World，简称STW，指的是GC事件发生过程中，会产生应用程序的停顿。**停顿产生时整个应用程序线程都会被暂停，没有任何响应**，有点像卡死的感觉，这个停顿称为STW。
2. 可达性分析算法中枚举根节点（GC Roots）会导致所有Java执行线程停顿，为什么需要停顿所有 Java 执行线程呢？
   - 分析工作必须在一个能确保一致性的快照中进行
   - 一致性指整个分析期间整个执行系统看起来像被冻结在某个时间点上
   - **如果出现分析过程中对象引用关系还在不断变化，则分析结果的准确性无法保证**
3. 被STW中断的应用程序线程会在完成GC之后恢复，频繁中断会让用户感觉像是网速不快造成电影卡带一样，所以我们需要减少STW的发生。
4. STW事件和采用哪款GC无关，所有的GC都有这个事件。
5. 哪怕是G1也不能完全避免Stop-the-world情况发生，只能说垃圾回收器越来越优秀，回收效率越来越高，尽可能地缩短了暂停时间。
6. STW是JVM在**后台自动发起和自动完成**的。在用户不可见的情况下，把用户正常的工作线程全部停掉。
7. 开发中不要用System.gc() ，这会导致Stop-the-World的发生。

**代码感受 Stop the World：**
```java
public class StopTheWorldDemo {
    public static class WorkThread extends Thread {
        List<byte[]> list = new ArrayList<byte[]>();

        public void run() {
            try {
                while (true) {
                    for(int i = 0;i < 1000;i++){
                        byte[] buffer = new byte[1024];
                        list.add(buffer);
                    }

                    if(list.size() > 10000){
                        list.clear();
                        System.gc();//会触发full gc，进而会出现STW事件
                     
                    }
                }
            } catch (Exception ex) {
                ex.printStackTrace();
            }
        }
    }

    public static class PrintThread extends Thread {
        public final long startTime = System.currentTimeMillis();

        public void run() {
            try {
                while (true) {
                    // 每秒打印时间信息
                    long t = System.currentTimeMillis() - startTime;
                    System.out.println(t / 1000 + "." + t % 1000);
                    Thread.sleep(1000);
                }
            } catch (Exception ex) {
                ex.printStackTrace();
            }
        }
    }

    public static void main(String[] args) {
        WorkThread w = new WorkThread();
        PrintThread p = new PrintThread();
        w.start();
        p.start();
    }
}

```
关闭工作线程 w ，观察输出：当前时间间隔与上次时间间隔**基本**是每隔1秒打印一次
0.1 1.1 2.2 3.2 4.3 5.3 6.3 7.3 Process finished with exit code -1
开启工作线程 w ，观察打印输出：当前时间间隔与上次时间间隔相差 1.3s ，可以明显感受到 Stop the World 的存在
0.1 1.4 2.7 3.8 4.12 5.13 Process finished with exit code -1
## 4、并行与并发
### 并发的概念

1. 在操作系统中，是指**一个时间段**中有几个程序都处于已启动运行到运行完毕之间，且这几个程序都是在同一个处理器上运行
2. 并发不是真正意义上的“同时进行”，只是CPU把一个时间段划分成几个时间片段（时间区间），然后在这几个时间区间之间来回切换。由于CPU处理的速度非常快，只要时间间隔处理得当，即可让用户感觉是多个应用程序同时在进行

![](image/1664240353475-c9267e80-851f-4025-8dcf-58978c163021.png)
### 并行的概念

1. 当系统有一个以上CPU时，当一个CPU执行一个进程时，另一个CPU可以执行另一个进程，两个进程互不抢占CPU资源，可以**同时**进行，我们称之为并行（Parallel）
2. 其实决定并行的因素不是CPU的数量，而是CPU的核心数量，比如一个CPU多个核也可以并行
3. 适合科学计算，后台处理等弱交互场景

![](image/1664240349947-c874720d-3dd4-4528-a24d-bc0956527c10.png)
**并发与并行的对比**

1. 并发，指的是多个事情，在同一时间段内同时发生了。
2. 并行，指的是多个事情，在同一时间点上（或者说同一时刻）同时发生了。
3. 并发的多个任务之间是互相抢占资源的。并行的多个任务之间是不互相抢占资源的。
4. 只有在多CPU或者一个CPU多核的情况中，才会发生并行。否则，看似同时发生的事情，其实都是并发执行的。
### 垃圾回收的并发与并行

1. 并行（Parallel）：指多条垃圾收集线程并行工作，但此时用户线程仍处于等待状态。
   - 如ParNew、Parallel Scavenge、Parallel Old
2. 串行（Serial）
   - 相较于并行的概念，单线程执行。
   - 如果内存不够，则程序暂停，启动JVM垃圾回收器进行垃圾回收（单线程）

![](image/1664240350535-72d13481-f5de-4c79-8a5d-ff28e3a28996.png)
并发和并行，在谈论垃圾收集器的上下文语境中，它们可以解释如下：

1. 并发（Concurrent）：指**用户线程与垃圾收集线程同时执行**（但不一定是并行的，可能会交替执行），垃圾回收线程在执行时不会停顿用户程序的运行。
   - 比如用户程序在继续运行，而垃圾收集程序线程运行于另一个CPU上；
2. 典型垃圾回收器：CMS、G1

![](image/1664240350389-5da4d93d-5cb9-454d-9115-1eb22f3a449b.png)
## 5、HotSpot的算法实现细节
### 根节点枚举

1. 固定可作为GC Roots的节点主要在全局性的引用（例如常量或类静态属性）与执行上下文（例如栈帧中的本地变量表）中，尽管目标明确，但查找过程要做到高效并非一件容易的事情，现在Java应用越做越庞大，光是方法区的大小就常有数百上千兆，里面的类、常量等更是恒河沙数，若要逐个检查以这里为起源的引用肯定得消耗不少时间。
2. 迄今为止，**所有收集器在根节点枚举这一步骤时都是必须暂停用户线程的**，因此毫无疑问根节点 枚举与之前提及的整理内存碎片一样会面临相似的“Stop The World”的困扰。现在可达性分析算法耗时 最长的查找引用链的过程已经可以做到与用户线程一起并发，**但根节点枚举始终还 是必须在一个能保障一致性的快照中才得以进行**——这里“一致性”的意思是整个枚举期间执行子系统 看起来就像被冻结在某个时间点上，不会出现分析过程中，根节点集合的对象引用关系还在不断变化 的情况，若这点不能满足的话，分析结果准确性也就无法保证。这是导致垃圾收集过程必须停顿所有 用户线程的其中一个重要原因，即使是号称停顿时间可控，或者（几乎）不会发生停顿的CMS、G1、 ZGC等收集器，枚举根节点时也是必须要停顿的。
3. 由于目前主流Java虚拟机使用的都是**准确式垃圾收集**，所以当用户线程停顿下来之后，其实并不需要一个不漏地检查完所有 执行上下文和全局的引用位置，虚拟机应当是有办法直接得到哪些地方存放着对象引用的。在HotSpot 的解决方案里，是使用一组称为**OopMap的数据结构**来达到这个目的。一旦类加载动作完成的时候， HotSpot就会把对象内什么偏移量上是什么类型的数据计算出来，在即时编译过程中，也 会在特定的位置记录下栈里和寄存器里哪些位置是引用。这样收集器在扫描时就可以直接得知这些信 息了，**并不需要真正一个不漏地从方法区等GC Roots开始查找**。
4. Exact VM因它使用**准确式内存管理**（Exact Memory Management，也可以叫Non-Con- servative/Accurate Memory Management）而得名。准确式内存管理是指虚拟机可以知道内存中某个位 置的数据具体是什么类型。譬如内存中有一个32bit的整数123456，虚拟机将有能力分辨出它到底是一 个指向了123456的内存地址的引用类型还是一个数值为123456的整数，准确分辨出哪些内存是引用类 型，这也是在垃圾收集时准确判断堆上的数据是否还可能被使用的前提。【**这个不是特别重要，了解一下即可**】

常考面试：**在OopMap的协助下，HotSpot可以快速准确地完成GC Roots枚举**
### 安全点与安全区域
**安全点（Safepoint）**

1. 程序执行时并非在所有地方都能停顿下来开始GC，只有在特定的位置才能停顿下来开始GC，这些位置称为“安全点（Safepoint）”。
2. Safe Point的选择很重要，**如果太少可能导致GC等待的时间太长，如果太频繁可能导致运行时的性能问题**。大部分指令的执行时间都非常短暂，通常会根据“**是否具有让程序长时间执行的特征**”为标准。比如：选择一些执行时间较长的指令作为Safe Point，**如方法调用、循环跳转和异常跳转等**。

**如何在GC发生时，检查所有线程都跑到最近的安全点停顿下来呢？**

1. 抢先式中断：（目前没有虚拟机采用了）首先中断所有线程。如果还有线程不在安全点，就恢复线程，让线程跑到安全点。
2. 主动式中断：设置一个中断标志，各个线程运行到Safe Point的时候**主动轮询**这个标志，如果中断标志为真，则将自己进行中断挂起。

**安全区域（Safe Region）**

1. Safepoint 机制保证了程序执行时，在不太长的时间内就会遇到可进入GC的Safepoint。但是，程序“不执行”的时候呢？
2. 例如线程处于Sleep状态或Blocked 状态，这时候线程无法响应JVM的中断请求，“走”到安全点去中断挂起，JVM也不太可能等待线程被唤醒。对于这种情况，就需要安全区域（Safe Region）来解决。
3. **安全区域是指在一段代码片段中，对象的引用关系不会发生变化，在这个区域中的任何位置开始GC都是安全的**。我们也可以把Safe Region看做是被扩展了的Safepoint。

**安全区域的执行流程**

1. 当线程运行到Safe Region的代码时，首先标识已经进入了Safe Region，如果这段时间内发生GC，JVM会忽略标识为Safe Region状态的线程
2. 当线程即将离开Safe Region时，会检查JVM是否已经完成根节点枚举（即GC Roots的枚举），如果完成了，则继续运行，否则线程必须等待直到收到可以安全离开Safe Region的信号为止；
### 记忆集与卡表
#### 什么是跨代引用？
1、一般的垃圾回收算法至少会划分出两个年代，年轻代和老年代。但是单纯的分代理论在垃圾回收的时候存在一个巨大的缺陷：为了找到年轻代中的存活对象，却不得不遍历整个老年代，反过来也是一样的。
![](image/1664240352658-5422aa7a-4490-4df7-81a5-f9bb95bf2b53.png)
2、如果我们从年轻代开始遍历，那么可以断定N, S, P, Q都是存活对象。但是，V却不会被认为是存活对象，其占据的内存会被回收了。这就是一个惊天的大漏洞！因为U本身是老年代对象，而且有外部引用指向它，也就是说U是存活对象，而U指向了V，也就是说V也应该是存活对象才是！而这都是因为我们只遍历年轻代对象！
3、所以，为了解决这种跨代引用的问题，最笨的办法就是遍历老年代的对象，找出这些跨代引用来。这种方案存在极大的性能浪费。因为从两个分代假说里面，其实隐含了一个推论：跨代引用是极少的。也就是为了找出那么一点点跨代引用，我们却得遍历整个老年代！从上图来说，很显然的是，我们根本不必遍历R。
4、因此，为了避免这种遍历老年代的性能开销，通常的分代垃圾回收器会引入一种称为**记忆集**的技术。**简单来说，记忆集就是用来记录跨代引用的表。**
#### 记忆集与卡表
1、为解决对象跨代引用所带来的问题，垃圾收集器在新生代中建 立了名为**记忆集（Remembered Set）的数据结构**，用以避免把整个老年代加进GC Roots扫描范围。事实上并不只是新生代、老年代之间才有跨代引用的问题，所有涉及部分区域收集（Partial GC）行为的 垃圾收集器，典型的如G1、ZGC和Shenandoah收集器，都会面临相同的问题，因此我们有必要进一步 理清记忆集的原理和实现方式，以便在后续章节里介绍几款最新的收集器相关知识时能更好地理解。
2、记忆集是一种用于记录**从非收集区域指向收集区域的指针集合的抽象数据结构**。如果我们不考虑效率和成本的话，最简单的实现可以用非收集区域中所有含跨代引用的对象数组来实现这个数据结构。
比如说我们有老年代（非收集区域）和年轻代（收集区域）的对象之间有一条引用链
3、这种记录全部含跨代引用对象的实现方案，无论是空间占用还是维护成本都相当高昂。而在垃圾 收集的场景中，收集器只需要通过记忆集判断出某一块非收集区域是否存在有指向了收集区域的指针 就可以了，并不需要了解这些跨代指针的全部细节。那设计者在实现记忆集的时候，便可以选择更为 粗犷的记录粒度来节省记忆集的存储和维护成本，下面列举了一些可供选择（当然也可以选择这个范 围以外的）的记录精度：

- 字长精度：每个记录精确到一个机器字长（就是处理器的寻址位数，如常见的32位或64位，这个 精度决定了机器访问物理内存地址的指针长度），该字包含跨代指针。
- 对象精度：每个记录精确到一个对象，该对象里有字段含有跨代指针。
- 卡精度：每个记录精确到一块内存区域，该区域内有对象含有跨代指针。

4、其中，第三种“卡精度”所指的是用一种称为“卡表”（Card Table）的方式去实现记忆集，这也是 目前最常用的一种记忆集实现形式，一些资料中甚至直接把它和记忆集混为一谈。前面定义中提到记 忆集其实是一种“抽象”的数据结构，抽象的意思是只定义了记忆集的行为意图，并没有定义其行为的 具体实现。卡表就是记忆集的一种具体实现，它定义了记忆集的记录精度、与堆内存的映射关系等。 关于卡表与记忆集的关系，读者不妨按照Java语言中HashMap与Map的关系来类比理解。 卡表最简单的形式可以只是一个字节数组，而HotSpot虚拟机确实也是这样做的
读者只需要知道有这个东西，面试的时候能说出来，再细致一点的就需要看周志明老师的第三版书了
## 6、再谈引用
### 概述

1. 我们希望能描述这样一类对象：当内存空间还足够时，则能保留在内存中；如果内存空间在进行垃圾收集后还是很紧张，则可以抛弃这些对象。
2. 既偏门又非常高频的面试题：强引用、软引用、弱引用、虚引用有什么区别？具体使用场景是什么？
3. 在JDK1.2版之后，Java对引用的概念进行了扩充，将引用分为：
   - 强引用（Strong Reference）
   - 软引用（Soft Reference）
   - 弱引用（Weak Reference）
   - 虚引用（Phantom Reference）
4. 这4种引用强度依次逐渐减弱。除强引用外，其他3种引用均可以在java.lang.ref包中找到它们的身影。如下图，显示了这3种引用类型对应的类，开发人员可以在应用程序中直接使用它们。

![](image/1664240352787-d500640c-f7c6-48f1-b72c-aeff7e162ac6.png)
Reference子类中只有终结器引用是包内可见的，其他3种引用类型均为public，可以在应用程序中直接使用

1. 强引用（StrongReference）：最传统的“引用”的定义，是指在程序代码之中普遍存在的引用赋值，即类似“object obj=new Object()”这种引用关系。无论任何情况下，只要强引用关系还存在，垃圾收集器就永远不会回收掉被引用的对象。宁可报OOM，也不会GC强引用
2. 软引用（SoftReference）：在系统将要发生内存溢出之前，将会把这些对象列入回收范围之中进行第二次回收。如果这次回收后还没有足够的内存，才会抛出内存溢出异常。
3. 弱引用（WeakReference）：被弱引用关联的对象只能生存到下一次垃圾收集之前。当垃圾收集器工作时，无论内存空间是否足够，都会回收掉被弱引用关联的对象。
4. 虚引用（PhantomReference）：一个对象是否有虚引用的存在，完全不会对其生存时间构成影响，也无法通过虚引用来获得一个对象的实例。为一个对象设置虚引用关联的唯一目的就是能在这个对象被收集器回收时收到一个系统通知。
### 强引用

1. 在Java程序中，最常见的引用类型是强引用（普通系统99%以上都是强引用），也就是我们最常见的普通对象引用，**也是默认的引用类型**。
2. 当在Java语言中使用new操作符创建一个新的对象，并将其赋值给一个变量的时候，这个变量就成为指向该对象的一个强引用。
3. **只要强引用的对象是可触及的，垃圾收集器就永远不会回收掉被引用的对象。**只要强引用的对象是可达的，jvm宁可报OOM，也不会回收强引用。
4. 对于一个普通的对象，如果没有其他的引用关系，只要超过了引用的作用域或者显式地将相应（强）引用赋值为null，就是可以当做垃圾被收集了，当然具体回收时机还是要看垃圾收集策略。
5. 相对的，软引用、弱引用和虚引用的对象是软可触及、弱可触及和虚可触及的，在一定条件下，都是可以被回收的。所以，强引用是造成Java内存泄漏的主要原因之一。

**强引用代码举例**
```java
public class StrongReferenceTest {
    public static void main(String[] args) {
        StringBuffer str = new StringBuffer ("Hello,尚硅谷");
        StringBuffer str1 = str;

        str = null;
        System.gc();

        try {
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println(str1);
    }
}
```
输出
`Hello,尚硅谷`
局部变量str指向stringBuffer实例所在堆空间，通过str可以操作该实例，那么str就是stringBuffer实例的强引用对应内存结构：
StringBuffer str = new StringBuffer("hello,尚硅谷");
![](image/1664240357670-265e42c4-6009-4c85-bec9-7f6720d77e07.png)
**总结**
本例中的两个引用，都是强引用，强引用具备以下特点：

1. 强引用可以直接访问目标对象。
2. 强引用所指向的对象在任何时候都不会被系统回收，虚拟机宁愿抛出OOM异常，也不会回收强引用所指向对象。
3. 强引用可能导致内存泄漏。
### 软引用
**软引用（Soft Reference）：内存不足即回收**

1. 软引用是用来描述一些还有用，但非必需的对象。只被软引用关联着的对象，在系统将要发生内存溢出异常前，会把这些对象列进回收范围之中进行第二次回收，如果这次回收还没有足够的内存，才会抛出内存溢出异常。注意，这里的第一次回收是不可达的对象
2. 软引用通常用来实现内存敏感的缓存。比如：高速缓存就有用到软引用。如果还有空闲内存，就可以暂时保留缓存，当内存不足时清理掉，这样就保证了使用缓存的同时，不会耗尽内存。
3. 垃圾回收器在某个时刻决定回收软可达的对象的时候，会清理软引用，并可选地把引用存放到一个引用队列（Reference Queue）。
4. 类似弱引用，只不过Java虚拟机会尽量让软引用的存活时间长一些，迫不得已才清理。
5. 一句话概括：当内存足够时，不会回收软引用可达的对象。内存不够时，会回收软引用的可达对象

在JDK1.2版之后提供了SoftReference类来实现软引用
```java
Object obj = new Object();// 声明强引用
SoftReference<Object> sf = new SoftReference<>(obj);
obj = null; //销毁强引用
```
**软引用代码举例**
代码
```java
public class SoftReferenceTest {
    public static class User {
        public User(int id, String name) {
            this.id = id;
            this.name = name;
        }

        public int id;
        public String name;

        @Override
        public String toString() {
            return "[id=" + id + ", name=" + name + "] ";
        }
    }

    public static void main(String[] args) {
        //创建对象，建立软引用
//        SoftReference<User> userSoftRef = new SoftReference<User>(new User(1, "songhk"));
        //上面的一行代码，等价于如下的三行代码
        User u1 = new User(1,"songhk");
        SoftReference<User> userSoftRef = new SoftReference<User>(u1);
        u1 = null;//取消强引用


        //从软引用中重新获得强引用对象
        System.out.println(userSoftRef.get());

        System.out.println("---目前内存还不紧张---");
        System.gc();
        System.out.println("After GC:");
//        //垃圾回收之后获得软引用中的对象
        System.out.println(userSoftRef.get());//由于堆空间内存足够，所有不会回收软引用的可达对象。
        System.out.println("---下面开始内存紧张了---");
        try {
            //让系统认为内存资源紧张、不够
//            byte[] b = new byte[1024 * 1024 * 7];
            byte[] b = new byte[1024 * 7168 - 635 * 1024];
        } catch (Throwable e) {
            e.printStackTrace();
        } finally {
            //再次从软引用中获取数据
            System.out.println(userSoftRef.get());//在报OOM之前，垃圾回收器会回收软引用的可达对象。
        }
    }
}


```
JVM参数
-Xms10m -Xmx10m
在 JVM 内存不足时，会清理软引用对象
输出结果：
```bash
[id=1, name=songhk] 
---目前内存还不紧张---
After GC:
[id=1, name=songhk] 
---下面开始内存紧张了---
null
java.lang.OutOfMemoryError: Java heap space
	at com.atguigu.java1.SoftReferenceTest.main(SoftReferenceTest.java:48)

Process finished with exit code 0
```
### 弱引用
**弱引用（Weak Reference）发现即回收**

1. 弱引用也是用来描述那些非必需对象，**只被弱引用关联的对象只能生存到下一次垃圾收集发生为止。在系统GC时，只要发现弱引用，不管系统堆空间使用是否充足，都会回收掉只被弱引用关联的对象**。
2. 但是，由于垃圾回收器的线程通常优先级很低，因此，并不一定能很快地发现持有弱引用的对象。在这种情况下，弱引用对象可以存在较长的时间。
3. 弱引用和软引用一样，在构造弱引用时，也可以指定一个引用队列，当弱引用对象被回收时，就会加入指定的引用队列，通过这个队列可以跟踪对象的回收情况。
4. 软引用、弱引用都非常适合来保存那些可有可无的缓存数据。如果这么做，当系统内存不足时，这些缓存数据会被回收，不会导致内存溢出。而当内存资源充足时，这些缓存数据又可以存在相当长的时间，从而起到加速系统的作用。

在JDK1.2版之后提供了WeakReference类来实现弱引用
```java
WeakReference<Object> sf = new WeakReference<>(new Object());
```
弱引用对象与软引用对象的最大不同就在于，当GC在进行回收时，需要通过算法检查是否回收软引用对象，而对于弱引用对象，GC总是进行回收。弱引用对象更容易、更快被GC回收。
**面试题：你开发中使用过WeakHashMap吗？**
**弱引用代码举例**
```java
public class WeakReferenceTest {
    public static class User {
        public User(int id, String name) {
            this.id = id;
            this.name = name;
        }

        public int id;
        public String name;

        @Override
        public String toString() {
            return "[id=" + id + ", name=" + name + "] ";
        }
    }

    public static void main(String[] args) {
        //构造了弱引用
        WeakReference<User> userWeakRef = new WeakReference<User>(new User(1, "songhk"));
        //从弱引用中重新获取对象
        System.out.println(userWeakRef.get());

        System.gc();
        // 不管当前内存空间足够与否，都会回收它的内存
        System.out.println("After GC:");
        //重新尝试从弱引用中获取对象
        System.out.println(userWeakRef.get());
    }
}

```
执行垃圾回收后，软引用对象必定被清除
```bash
[id=1, name=songhk] 
After GC:
null

Process finished with exit code 0
```
### 虚引用
**虚引用（Phantom Reference）：对象回收跟踪**

1. 也称为“幽灵引用”或者“幻影引用”，是所有引用类型中最弱的一个
2. 一个对象是否有虚引用的存在，完全不会决定对象的生命周期。如果一个对象仅持有虚引用，那么它和没有引用几乎是一样的，随时都可能被垃圾回收器回收。
3. 它不能单独使用，也无法通过虚引用来获取被引用的对象。当试图通过虚引用的get()方法取得对象时，总是null 。**即通过虚引用无法获取到我们的数据**
4. **为一个对象设置虚引用关联的唯一目的在于跟踪垃圾回收过程。比如：能在这个对象被收集器回收时收到一个系统通知。**
5. 虚引用必须和引用队列一起使用。虚引用在创建时必须提供一个引用队列作为参数。当垃圾回收器准备回收一个对象时，如果发现它还有虚引用，就会在回收对象后，将这个虚引用加入引用队列，以通知应用程序对象的回收情况。
6. 由于虚引用可以跟踪对象的回收时间，因此，也可以将一些资源释放操作放置在虚引用中执行和记录。

在JDK1.2版之后提供了PhantomReference类来实现虚引用。
```java
// 声明引用队列
ReferenceQueue phantomQueue = new ReferenceQueue();
// 声明虚引用（还需要传入引用队列）
PhantomReference<Object> sf = new PhantomReference<>(new Object(), phantomQueue);
```
**虚引用代码示例**
```java
public class PhantomReferenceTest {
    public static PhantomReferenceTest obj;//当前类对象的声明
    static ReferenceQueue<PhantomReferenceTest> phantomQueue = null;//引用队列

    public static class CheckRefQueue extends Thread {
        @Override
        public void run() {
            while (true) {
                if (phantomQueue != null) {
                    PhantomReference<PhantomReferenceTest> objt = null;
                    try {
                        objt = (PhantomReference<PhantomReferenceTest>) phantomQueue.remove();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    if (objt != null) {
                        System.out.println("追踪垃圾回收过程：PhantomReferenceTest实例被GC了");
                    }
                }
            }
        }
    }

    @Override
    protected void finalize() throws Throwable { //finalize()方法只能被调用一次！
        super.finalize();
        System.out.println("调用当前类的finalize()方法");
        obj = this;
    }

    public static void main(String[] args) {
        Thread t = new CheckRefQueue();
        t.setDaemon(true);//设置为守护线程：当程序中没有非守护线程时，守护线程也就执行结束。
        t.start();

        phantomQueue = new ReferenceQueue<PhantomReferenceTest>();
        obj = new PhantomReferenceTest();
        //构造了 PhantomReferenceTest 对象的虚引用，并指定了引用队列
        PhantomReference<PhantomReferenceTest> phantomRef = new PhantomReference<PhantomReferenceTest>(obj, phantomQueue);

        try {
            //不可获取虚引用中的对象
            System.out.println(phantomRef.get());
			System.out.println("第 1 次 gc");
            //将强引用去除
            obj = null;
            //第一次进行GC,由于对象可复活，GC无法回收该对象
            System.gc();
            Thread.sleep(1000);
            if (obj == null) {
                System.out.println("obj 是 null");
            } else {
                System.out.println("obj 可用");
            }
            System.out.println("第 2 次 gc");
            obj = null;
            System.gc(); //一旦将obj对象回收，就会将此虚引用存放到引用队列中。
            Thread.sleep(1000);
            if (obj == null) {
                System.out.println("obj 是 null");
            } else {
                System.out.println("obj 可用");
            }
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```
1、第一次尝试获取虚引用的值，发现无法获取的，这是因为虚引用是无法直接获取对象的值，然后进行第一次GC，因为会调用finalize方法，将对象复活了，所以对象没有被回收
2、但是调用第二次GC操作的时候，因为finalize方法只能执行一次，所以就触发了GC操作，将对象回收了，同时将会触发第二个操作就是将待回收的对象存入到引用队列中。
输出结果：
```bash
null
第 1 次 gc
调用当前类的finalize()方法
obj 可用
第 2 次 gc
追踪垃圾回收过程：PhantomReferenceTest实例被GC了
obj 是 null

Process finished with exit code 0
```
### 终结器引用（了解）

1. 它用于实现对象的finalize() 方法，也可以称为终结器引用
2. 无需手动编码，其内部配合引用队列使用
3. 在GC时，终结器引用入队。由Finalizer线程通过终结器引用找到被引用对象调用它的finalize()方法，第二次GC时才回收被引用的对象

# 十七、垃圾回收器GC
## 1、分类与性能指标
### 概述
垃圾收集器没有在规范中进行过多的规定，可以由不同的厂商、不同版本的JVM来实现。
由于JDK的版本处于高速迭代过程中，因此Java发展至今已经衍生了众多的GC版本。
从不同角度分析垃圾收集器，可以将GC分为不同的类型。
> **Java不同版本新特性**
> 语法层面：Lambda表达式、switch、自动拆箱装箱、enum、泛型
> API层面：Stream API、新的日期时间、Optional、String、集合框架
> 底层优化：JVM优化、GC的变化、元空间、静态域、字符串常量池等

### 垃圾回收器分类
**按线程数分（垃圾回收线程数），可以分为串行垃圾回收器和并行垃圾回收器。**
![](image/1664244589978-c1f7f2e3-2087-491b-9df5-1c51a9c11aa5.png)
串行回收指的是在同一时间段内只允许有一个CPU用于执行垃圾回收操作，此时工作线程被暂停，直至垃圾收集工作结束。

1. 在诸如单CPU处理器或者较小的应用内存等硬件平台不是特别优越的场合，串行回收器的性能表现可以超过并行回收器和并发回收器。所以，串行回收默认被应用在客户端的Client模式下的JVM中
2. 在并发能力比较强的CPU上，并行回收器产生的停顿时间要短于串行回收器

和串行回收相反，并行收集可以运用多个CPU同时执行垃圾回收，因此提升了应用的吞吐量，不过并行回收仍然与串行回收一样，采用独占式，使用了“Stop-the-World”机制。
**按照工作模式分，可以分为并发式垃圾回收器和独占式垃圾回收器。**

1. 并发式垃圾回收器与应用程序线程交替工作，以尽可能减少应用程序的停顿时间。
2. 独占式垃圾回收器（Stop the World）一旦运行，就停止应用程序中的所有用户线程，直到垃圾回收过程完全结束。

![](image/1664244590048-3209cb6c-6380-4fc0-80b0-dbeb84dc6bb5.png)
**按碎片处理方式分，可分为压缩式垃圾回收器和非压缩式垃圾回收器。**

1. 压缩式垃圾回收器会在回收完成后，对存活对象进行压缩整理，消除回收后的碎片。再分配对象空间使用指针碰撞
2. 非压缩式的垃圾回收器不进行这步操作，分配对象空间使用空闲列表

**按工作的内存区间分，又可分为年轻代垃圾回收器和老年代垃圾回收器。**
### 评估 GC 的性能指标
**指标**

1. **吞吐量：**运行用户代码的时间占总运行时间的比例（总运行时间 = 程序的运行时间 + 内存回收的时间）
2. 垃圾收集开销：吞吐量的补数，垃圾收集所用时间与总运行时间的比例。
3. **暂停时间：**执行垃圾收集时，程序的工作线程被暂停的时间。
4. 收集频率：相对于应用程序的执行，收集操作发生的频率。
5. **内存占用：**Java堆区所占的内存大小。
6. 快速：一个对象从诞生到被回收所经历的时间。

吞吐量、暂停时间、内存占用这三者共同构成一个“不可能三角”。三者总体的表现会随着技术进步而越来越好。一款优秀的收集器通常最多同时满足其中的两项。
这三项里，暂停时间的重要性日益凸显。因为随着硬件发展，内存占用多些越来越能容忍，硬件性能的提升也有助于降低收集器运行时对应用程序的影响，即提高了吞吐量。而内存的扩大，对延迟反而带来负面效果。
简单来说，主要抓住两点：

- 吞吐量
- 暂停时间

**吞吐量（throughput）**
吞吐量就是CPU用于运行用户代码的时间与CPU总消耗时间的比值，即吞吐量=运行用户代码时间 /（运行用户代码时间+垃圾收集时间）

- 比如：虚拟机总共运行了100分钟，其中垃圾收集花掉1分钟，那吞吐量就是99%。

这种情况下，应用程序能容忍较高的暂停时间，因此，高吞吐量的应用程序有更长的时间基准，快速响应是不必考虑的
吞吐量优先，意味着在单位时间内，STW的时间最短：0.2+0.2=0.4
![](image/1664244590220-5f409d33-f4a1-4827-a470-c373e3637ccf.png)
**暂停时间（pause time）**
“暂停时间”是指一个时间段内应用程序线程暂停，让GC线程执行的状态。

- 例如，GC期间100毫秒的暂停时间意味着在这100毫秒期间内没有应用程序线程是活动的

暂停时间优先，意味着尽可能让单次STW的时间最短：0.1+0.1 + 0.1+ 0.1+ 0.1=0.5，但是总的GC时间可能会长
![](image/1664244590571-8490c0f5-299c-415e-8727-7f024bc72ede.png)
**吞吐量 vs 暂停时间**
**高吞吐量较好**因为这会让应用程序的最终用户感觉只有应用程序线程在做“生产性”工作。直觉上，吞吐量越高程序运行越快。
低暂停时间（低延迟）较好，是从最终用户的角度来看，不管是GC还是其他原因导致一个应用被挂起始终是不好的。这取决于应用程序的类型，有时候甚至短暂的200毫秒暂停都可能打断终端用户体验。因此，具有较低的暂停时间是非常重要的，特别是对于一个交互式应用程序（就是和用户交互比较多的场景）。
不幸的是”高吞吐量”和”低暂停时间”是一对相互竞争的目标（矛盾）。

- 因为如果选择以吞吐量优先，那么**必然需要降低内存回收的执行频率**，但是这样会导致GC需要更长的暂停时间来执行内存回收。
- 相反的，如果选择以低延迟优先为原则，那么为了降低每次执行内存回收时的暂停时间，也只能频繁地执行内存回收，但这又引起了年轻代内存的缩减和导致程序吞吐量的下降。

在设计（或使用）GC算法时，我们必须确定我们的目标：一个GC算法只可能针对两个目标之一（即只专注于较大吞吐量或最小暂停时间），或尝试找到一个二者的折衷。
现在标准：**在最大吞吐量优先的情况下，降低停顿时间**
## 2、不同的垃圾回收器
垃圾收集机制是Java的招牌能力，极大地提高了开发效率。这当然也是面试的热点。
那么，Java常见的垃圾收集器有哪些？
### 垃圾收集器发展史
有了虚拟机，就一定需要收集垃圾的机制，这就是Garbage Collection，对应的产品我们称为Garbage Collector。

1. 1999年随JDK1.3.1一起来的是串行方式的Serial GC，它是第一款GC。ParNew垃圾收集器是Serial收集器的多线程版本
2. 2002年2月26日，Parallel GC和Concurrent Mark Sweep GC跟随JDK1.4.2一起发布·
3. Parallel GC在JDK6之后成为HotSpot默认GC。
4. 2012年，在JDK1.7u4版本中，G1可用。
5. 2017年，JDK9中G1变成默认的垃圾收集器，以替代CMS。
6. 2018年3月，JDK10中G1垃圾回收器的并行完整垃圾回收，实现并行性来改善最坏情况下的延迟。
7. 2018年9月，JDK11发布。引入Epsilon 垃圾回收器，又被称为 "No-Op(无操作)“ 回收器。同时，引入ZGC：可伸缩的低延迟垃圾回收器（Experimental）
8. 2019年3月，JDK12发布。增强G1，自动返回未用堆内存给操作系统。同时，引入Shenandoah GC：低停顿时间的GC（Experimental）。
9. 2019年9月，JDK13发布。增强ZGC，自动返回未用堆内存给操作系统。
10. 2020年3月，JDK14发布。删除CMS垃圾回收器。扩展ZGC在macOS和Windows上的应用
### 7款经典的垃圾收集器

1. 串行回收器：Serial、Serial old
2. 并行回收器：ParNew、Parallel Scavenge、Parallel old
3. 并发回收器：CMS、G1

![](image/1664244590125-ef5dfdb6-38ab-4001-8c6d-176ec8c5910c.png)
**官方文档**
[![](https://cdn.nlark.com/yuque/0/2022/jpeg/26368762/1664244592358-a208ac56-549e-4b95-a55c-25d7a250af7c.jpeg#clientId=ue9516613-2cc2-4&crop=0&crop=0&crop=1&crop=1&from=paste&id=u9de415e6&margin=%5Bobject%20Object%5D&originHeight=732&originWidth=1249&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u9e302463-ccde-4e62-9c85-12ebb9cbed9&title=)](https://camo.githubusercontent.com/d78c30c3a75b269abc31d69edc03c6a742715d8a8eadc3cb6f3fe2d4f6b0cb11/68747470733a2f2f6e706d2e656c656d6563646e2e636f6d2f796f7574686c716c40312e302e382f4a564d2f636861707465725f3031322f303030362e6a7067)
**7款经典回收器与垃圾分代之间的关系**
![](image/1664244591472-20e2cd09-cc6e-446d-8c61-987784f309a6.png)

1. 新生代收集器：Serial、ParNew、Parallel Scavenge；
2. 老年代收集器：Serial old、Parallel old、CMS；
3. 整堆收集器：G1；
### 垃圾收集器的组合关系
![1664245445556-f46c8166-c335-4a48-9cef-6582e6a964c1](image/1664245445556-f46c8166-c335-4a48-9cef-6582e6a964c1.png)
两个收集器间有连线，表明它们可以搭配使用：

- Serial/Serial old
- Serial/CMS （JDK9废弃）
- ParNew/Serial Old （JDK9废弃）
- ParNew/CMS
- Parallel Scavenge/Serial Old （预计废弃）
- Parallel Scavenge/Parallel Old
- G1

其中Serial Old作为CMS出现"Concurrent Mode Failure"失败的后备预案。
（橙色虚线）由于维护和兼容性测试的成本，在JDK 8时将Serial+CMS、ParNew+Serial Old这两个组合声明为废弃（JEP173），并在JDK9中完全取消了这些组合的支持（JEP214），即：移除。
（绿色虚线）JDK14中：弃用Parallel Scavenge和Serial Old GC组合（JEP366）
（青色虚线）JDK14中：删除CMS垃圾回收器（JEP363）
> 为什么要有很多收集器，一个不够吗？因为Java的使用场景很多，移动端，服务器等。所以就需要针对不同的场景，提供不同的垃圾收集器，提高垃圾收集的性能。
> 虽然我们会对各个收集器进行比较，但并非为了挑选一个最好的收集器出来。没有一种放之四海皆准、任何场景下都适用的完美收集器存在，更加没有万能的收集器。所以**我们选择的只是对具体应用最合适的收集器**。

### 查看默认垃圾收集器
-XX:+PrintCommandLineFlags：查看命令行相关参数（包含使用的垃圾收集器）

使用命令行指令：jps ->  jinfo -flag 相关垃圾回收器参数 进程ID
![](image/1664244593071-a3394e19-fd0b-48ed-975d-38f0874ee25c.png)JDK8
### 设置垃圾收集器
```bash
-XX:+UseG1GC # 使用 G1 收集器
-XX:+UseParallelGC # 使用 Paralle 收集器，同时开启  ParalleOld
-XX:+UseSerialGC # 使用 Serial/Serial old 收集器
```

## 3、Serial：串行回收
**Serial 回收器：串行回收**

1. Serial收集器是最基本、历史最悠久的垃圾收集器了。JDK1.3之前回收新生代唯一的选择。
2. Serial收集器作为HotSpot中Client模式下的默认新生代垃圾收集器。
3. Serial收集器采用复制算法、串行回收和"Stop-the-World"机制的方式执行内存回收。
4. 除了年轻代之外，Serial收集器还提供用于执行老年代垃圾收集的Serial Old收集器。Serial old收集器同样也采用了串行回收和"Stop the World"机制，只不过内存回收算法使用的是标记-压缩算法。
5. Serial Old是运行在Client模式下默认的老年代的垃圾回收器，Serial Old在Server模式下主要有两个用途：①与新生代的Parallel Scavenge配合使用②作为老年代CMS收集器的后备垃圾收集方案

这个收集器是一个单线程的收集器，“单线程”的意义：它只会使用一个CPU（串行）或一条收集线程去完成垃圾收集工作。更重要的是在它进行垃圾收集时，必须暂停其他所有的工作线程，直到它收集结束（Stop The World）
![](image/1664244593429-d7146785-5519-4200-a96e-124d2af879f8.png)
**Serial 回收器的优势**

1. 优势：简单而高效（与其他收集器的单线程比），对于限定单个CPU的环境来说，Serial收集器由于没有线程交互的开销，专心做垃圾收集自然可以获得最高的单线程收集效率。运行在Client模式下的虚拟机是个不错的选择。
2. 在用户的桌面应用场景中，可用内存一般不大（几十MB至一两百MB），可以在较短时间内完成垃圾收集（几十ms至一百多ms），只要不频繁发生，使用串行回收器是可以接受的。
3. 在HotSpot虚拟机中，使用-XX:+UseSerialGC参数可以指定年轻代和老年代都使用串行收集器。
   - 等价于新生代用Serial GC，且老年代用Serial Old GC

**总结**

1. 这种垃圾收集器大家了解，现在已经不用串行的了。而且在限定单核CPU才可以用。现在都不是单核的了。
2. 对于交互较强的应用而言，这种垃圾收集器是不能接受的。一般在Java Web应用程序中是不会采用串行垃圾收集器的。
## 4、ParNew：并行回收
如果说Serial GC是年轻代中的单线程垃圾收集器，那么ParNew收集器则是Serial收集器的多线程版本。

- Par是Parallel的缩写，New：只能处理新生代

ParNew 收集器除了采用**并行回收**的方式执行内存回收外，两款垃圾收集器之间几乎没有任何区别。ParNew收集器在年轻代中同样也是采用复制算法、"Stop-the-World"机制。
ParNew 是很多JVM运行在Server模式下新生代的默认垃圾收集器。
![](image/1664244596508-fa8137cf-7907-44d5-90ad-247b90d0a683.png)

1. 对于新生代，回收次数频繁，使用并行方式高效。
2. 对于老年代，回收次数少，使用串行方式节省资源。（CPU并行需要切换线程，串行可以省去切换线程的资源）

**ParNew 回收器与 Serial 回收器比较**
Q：由于ParNew收集器基于并行回收，那么是否可以断定ParNew收集器的回收效率在任何场景下都会比Serial收集器更高效？
A：**不能**

1. ParNew收集器运行在多CPU的环境下，由于可以充分利用多CPU、多核心等物理硬件资源优势，可以更快速地完成垃圾收集，提升程序的吞吐量。
2. 但是在单个CPU的环境下，ParNew收集器不比Serial收集器更高效。虽然Serial收集器是基于串行回收，但是由于CPU不需要频繁地做任务切换，因此可以有效避免多线程交互过程中产生的一些额外开销。
3. 除Serial外，目前只有ParNew GC能与CMS收集器配合工作

**设置 ParNew 垃圾回收器**

1. 在程序中，开发人员可以通过选项"-XX:+UseParNewGC"手动指定使用ParNew收集器执行内存回收任务。它表示年轻代使用并行收集器，不影响老年代。
2. -XX:ParallelGCThreads限制线程数量，默认开启和CPU数据相同的线程数。
## 5、Parallel：吞吐量优先
### 介绍
**Parallel Scavenge 回收器：吞吐量优先**

1. HotSpot的年轻代中除了拥有ParNew收集器是基于并行回收的以外，Parallel Scavenge收集器同样也采用了复制算法、并行回收和"Stop the World"机制。
2. 那么Parallel收集器的出现是否多此一举？
   - 和ParNew收集器不同，Parallel Scavenge收集器的目标则是达到一个**可控制的吞吐量**（Throughput），它也被称为吞吐量优先的垃圾收集器。
   - 自适应调节策略也是Parallel Scavenge与ParNew一个重要区别。（动态调整内存分配情况，以达到一个最优的吞吐量或低延迟）
3. 高吞吐量则可以高效率地利用CPU时间，尽快完成程序的运算任务，**主要适合在后台运算而不需要太多交互的任务**。因此，常见在服务器环境中使用。例如，那些执行批量处理、订单处理、工资支付、科学计算的应用程序。
4. Parallel收集器在JDK1.6时提供了用于执行老年代垃圾收集的Parallel Old收集器，用来代替老年代的Serial Old收集器。
5. Parallel Old收集器采用了标记-压缩算法，但同样也是基于并行回收和"Stop-the-World"机制。

![](image/1664244595530-8b4df25a-a529-43ec-b734-3bd6a48bd448.png)

1. 在程序吞吐量优先的应用场景中，Parallel收集器和Parallel Old收集器的组合，在server模式下的内存回收性能很不错。
2. **在Java8中，默认是此垃圾收集器。**
### 参数设置
`-XX:+UseParallelGC` 手动指定年轻代使用Parallel并行收集器执行内存回收任务。
`-XX:+UseParallelOldGC` 手动指定老年代都是使用并行回收收集器。

- 分别适用于新生代和老年代
- 上面两个参数分别适用于新生代和老年代。默认jdk8是开启的。默认开启一个，另一个也会被开启。（互相激活）

`-XX:ParallelGCThreads` 设置年轻代并行收集器的线程数。一般地，最好与CPU数量相等，以避免过多的线程数影响垃圾收集性能。

- 在默认情况下，当CPU数量小于8个，ParallelGCThreads的值等于CPU数量。
- 当CPU数量大于8个，ParallelGCThreads的值等于3+[5*CPU_Count]/8]

`-XX:MaxGCPauseMillis` 设置垃圾收集器最大停顿时间（即STW的时间）。单位是毫秒。

- 为了尽可能地把停顿时间控制在XX:MaxGCPauseMillis 以内，收集器在工作时会调整Java堆大小或者其他一些参数。
- 对于用户来讲，停顿时间越短体验越好。但是在服务器端，我们注重高并发，整体的吞吐量。所以服务器端适合Parallel，进行控制。
- 该参数使用需谨慎。

`-XX:GCTimeRatio` 垃圾收集时间占总时间的比例，即等于 1 / (N+1) ，用于衡量吞吐量的大小。

- 取值范围(0, 100)。默认值99，也就是垃圾回收时间占比不超过1。
- 与前一个-XX:MaxGCPauseMillis参数有一定矛盾性，STW暂停时间越长，Radio参数就容易超过设定的比例。

`-XX:+UseAdaptiveSizePolicy` 设置Parallel Scavenge收集器具有**自适应调节策略**

- 在这种模式下，年轻代的大小、Eden和Survivor的比例、晋升老年代的对象年龄等参数会被自动调整，已达到在堆大小、吞吐量和停顿时间之间的平衡点。
- 在手动调优比较困难的场合，可以直接使用这种自适应的方式，仅指定虚拟机的最大堆、目标的吞吐量（GCTimeRatio）和停顿时间（MaxGCPauseMillis），让虚拟机自己完成调优工作。
## 6、CMS：低延迟
### 概述

1. 在JDK1.5时期，Hotspot推出了一款在强交互应用中（就是和用户打交道的引用）几乎可认为有划时代意义的垃圾收集器：CMS（Concurrent-Mark-Sweep）收集器，**这款收集器是HotSpot虚拟机中第一款真正意义上的并发收集器，它第一次实现了让垃圾收集线程与用户线程同时工作。**
2. CMS收集器的关注点是尽可能缩短垃圾收集时用户线程的停顿时间。停顿时间越短（低延迟）就越适合与用户交互的程序，良好的响应速度能提升用户体验。
   - 目前很大一部分的Java应用集中在互联网站或者B/S系统的服务端上，这类应用尤其重视服务的响应速度，希望系统停顿时间最短，以给用户带来较好的体验。CMS收集器就非常符合这类应用的需求。
3. CMS的垃圾收集算法采用标记-清除算法，并且也会"Stop-the-World"
4. 不幸的是，CMS作为老年代的收集器，却无法与JDK1.4.0中已经存在的新生代收集器Parallel Scavenge配合工作（因为实现的框架不一样，没办法兼容使用），所以在JDK1.5中使用CMS来收集老年代的时候，新生代只能选择ParNew或者Serial收集器中的一个。
5. 在G1出现之前，CMS使用还是非常广泛的。一直到今天，仍然有很多系统使用CMS GC。
### 工作原理（过程）
![](image/1664244596449-d190d05a-66e4-43ff-83d7-ced082c27a2f.png)
CMS整个过程比之前的收集器要复杂，整个过程分为4个主要阶段，即初始标记阶段、并发标记阶段、重新标记阶段和并发清除阶段。(涉及STW的阶段主要是：初始标记 和 重新标记)

1. 初始标记（Initial-Mark）阶段：在这个阶段中，程序中所有的工作线程都将会因为“Stop-the-World”机制而出现短暂的暂停，**这个阶段的主要任务仅仅只是标记出GC Roots能直接关联到的对象**。一旦标记完成之后就会恢复之前被暂停的所有应用线程。由于直接关联对象比较小，所以这里的**速度非常快**。
2. 并发标记（Concurrent-Mark）阶段：从GC Roots的直接关联对象开始遍历整个对象图的过程，这个过程耗时较长但是**不需要停顿用户线程**，**可以与垃圾收集线程一起并发运行**。
3. 重新标记（Remark）阶段：由于在并发标记阶段中，程序的工作线程会和垃圾收集线程同时运行或者交叉运行，因此为了修正并发标记期间，因用户程序继续运作而导致标记产生变动的那一部分对象的标记记录，这个阶段的停顿时间通常会比初始标记阶段稍长一些，并且也会导致“Stop-the-World”的发生，但也远比并发标记阶段的时间短。
4. 并发清除（Concurrent-Sweep）阶段：此阶段清理删除掉标记阶段判断的已经死亡的对象，释放内存空间。**由于不需要移动存活对象，所以这个阶段也是可以与用户线程同时并发的**
### 分析

1. 尽管CMS收集器采用的是并发回收（非独占式），**但是在其初始化标记和再次标记这两个阶段中仍然需要执行“Stop-the-World”机制**暂停程序中的工作线程，不过暂停时间并不会太长，因此可以说明目前所有的垃圾收集器都做不到完全不需要“Stop-the-World”，只是尽可能地缩短暂停时间。
2. **由于最耗费时间的并发标记与并发清除阶段都不需要暂停工作，所以整体的回收是低停顿的**。
3. 另外，由于在垃圾收集阶段用户线程没有中断，所以在CMS回收过程中，还应该确保应用程序用户线程有足够的内存可用。因此，CMS收集器不能像其他收集器那样等到老年代几乎完全被填满了再进行收集，**而是当堆内存使用率达到某一阈值时，便开始进行回收**，以确保应用程序在CMS工作过程中依然有足够的空间支持应用程序运行。要是CMS运行期间预留的内存无法满足程序需要，就会出现一次**“Concurrent Mode Failure”** 失败，这时虚拟机将启动后备预案：临时启用Serial old收集器来重新进行老年代的垃圾收集，这样停顿时间就很长了。
4. CMS收集器的垃圾收集算法采用的是**标记清除算法**，这意味着每次执行完内存回收后，由于被执行内存回收的无用对象所占用的内存空间极有可能是不连续的一些内存块，**不可避免地将会产生一些内存碎片**。那么CMS在为新对象分配内存空间时，将无法使用指针碰撞（Bump the Pointer）技术，而只能够选择空闲列表（Free List）执行内存分配。

![](image/1664244597824-3614bbf0-9233-4c7f-ab04-3129788feb7d.png)
**为什么 CMS 不采用标记-压缩算法呢？**
答案其实很简答，因为当并发清除的时候，用Compact整理内存的话，原来的用户线程使用的内存还怎么用呢？要保证用户线程能继续执行，前提的它运行的资源不受影响嘛。Mark Compact更适合“stop the world”这种场景下使用
### 优点与弊端
**优点**

1. 并发收集
2. 低延迟

**弊端**

1. **会产生内存碎片**，导致并发清除后，用户线程可用的空间不足。在无法分配大对象的情况下，不得不提前触发Full GC。
2. **CMS收集器对CPU资源非常敏感**。在并发阶段，它虽然不会导致用户停顿，但是会因为占用了一部分线程而导致应用程序变慢，总吞吐量会降低。
3. **CMS收集器无法处理浮动垃圾**。可能出现“Concurrent Mode Failure"失败而导致另一次Full GC的产生。在并发标记阶段由于程序的工作线程和垃圾收集线程是同时运行或者交叉运行的，**那么在并发标记阶段如果产生新的垃圾对象，CMS将无法对这些垃圾对象进行标记，最终会导致这些新产生的垃圾对象没有被及时回收，**从而只能在下一次执行GC时释放这些之前未被回收的内存空间。
### CMS 参数配置
`-XX:+UseConcMarkSweepGC` 手动指定使用CMS收集器执行内存回收任务。开启该参数后会自动将-XX:+UseParNewGC打开。

- 即：ParNew（Young区）+CMS（Old区）+Serial Old（Old区备选方案）的组合。

`-XX:CMSInitiatingOccupanyFraction` 设置堆内存使用率的阈值，一旦达到该阈值，便开始进行回收。

- JDK5及以前版本的默认值为68，即当老年代的空间使用率达到68%时，会执行一次CMS回收。JDK6及以上版本默认值为92%
- 如果内存增长缓慢，则可以设置一个稍大的值，大的阀值可以有效降低CMS的触发频率，减少老年代回收的次数可以较为明显地改善应用程序性能。反之，如果应用程序内存使用率增长很快，则应该降低这个阈值，以避免频繁触发老年代串行收集器。因此通过该选项便可以有效降低Full GC的执行次数。

`-XX:+UseCMSCompactAtFullCollection` 用于指定在执行完Full GC后对内存空间进行压缩整理，以此避免内存碎片的产生。不过由于内存压缩整理过程无法并发执行，所带来的问题就是停顿时间变得更长了。
`-XX:CMSFullGCsBeforeCompaction` 设置在执行多少次Full GC后对内存空间进行压缩整理。
`-XX:ParallelCMSThreads` 设置CMS的线程数量。

- CMS默认启动的线程数是 (ParallelGCThreads + 3) / 4，ParallelGCThreads是年轻代并行收集器的线程数，可以当做是 CPU 最大支持的线程数。当CPU资源比较紧张时，受到CMS收集器线程的影响，应用程序的性能在垃圾回收阶段可能会非常糟糕。
### 小结
HotSpot有这么多的垃圾回收器，那么如果有人问，Serial GC、Parallel GC、Concurrent Mark Sweep GC这三个GC有什么不同呢？

- 如果你想要最小化地使用内存和并行开销，请选Serial GC；
- 如果你想要最大化应用程序的吞吐量，请选Parallel GC；
- 如果你想要最小化GC的中断或停顿时间，请选CMS GC。
### JDK 后续版本中 CMS 的变化

1. JDK9新特性：CMS被标记为Deprecate了（JEP291）
   - 如果对JDK9及以上版本的HotSpot虚拟机使用参数-XX:+UseConcMarkSweepGC来开启CMS收集器的话，用户会收到一个警告信息，提示CMS未来将会被废弃。
2. JDK14新特性：删除CMS垃圾回收器（JEP363）移除了CMS垃圾收集器，
   - 如果在JDK14中使用XX:+UseConcMarkSweepGC的话，JVM不会报错，只是给出一个warning信息，但是不会exit。JVM会自动回退以默认GC方式启动JVM
## 7、G1：区域化分代式
### 概述
**既然我们已经有了前面几个强大的 GC ，为什么还要发布 Garbage First（G1）GC？**

1. 原因就在于应用程序所应对的业务越来越庞大、复杂，用户越来越多，没有GC就不能保证应用程序正常进行，而经常造成STW的GC又跟不上实际的需求，所以才会不断地尝试对GC进行优化。
2. G1（Garbage-First）垃圾回收器是在Java7 update4之后引入的一个新的垃圾回收器，是当今收集器技术发展的最前沿成果之一。
3. 与此同时，**为了适应现在不断扩大的内存和不断增加的处理器数量**，进一步降低暂停时间（pause time），同时兼顾良好的吞吐量。
4. 官方给G1设定的目标是在延迟可控的情况下获得尽可能高的吞吐量，所以才担当起“全功能收集器”的重任与期望。

**为什么名字叫Garbage First(G1)呢？**

1. 因为G1是一个并行回收器，它把堆内存分割为很多不相关的区域（Region）（物理上不连续的）。使用不同的Region来表示Eden、幸存者0区，幸存者1区，老年代等。
2. G1 GC有计划地避免在整个Java堆中进行全区域的垃圾收集。G1跟踪各个Region里面的垃圾堆积的价值大小（回收所获得的空间大小以及回收所需时间的经验值），在后台维护一个优先列表，**每次根据允许的收集时间，优先回收价值最大的Region。**
3. 由于这种方式的侧重点在于回收垃圾最大量的区间（Region），所以我们给G1一个名字：垃圾优先（Garbage First）。
4. G1（Garbage-First）是一款面向服务端应用的垃圾收集器，主要针对配备多核CPU及大容量内存的机器，以极高概率满足GC停顿时间的同时，还兼具高吞吐量的性能特征。
5. 在JDK1.7版本正式启用，移除了Experimental的标识，**是JDK9以后的默认垃圾回收器**，取代了CMS回收器以及Parallel+Parallel Old组合。被Oracle官方称为**“全功能的垃圾收集器”**。
6. 与此同时，CMS已经在JDK9中被标记为废弃（deprecated）。**G1在JDK8中还不是默认的垃圾回收器**，需要使用-XX:+UseG1GC来启用。
### 优势与缺点
#### 优势
与其他GC收集器相比，G1使用了全新的分区算法，其特点如下所示：

1. **并行与并发兼备**
   - 并行性：G1在回收期间，可以有多个GC线程同时工作，有效利用多核计算能力。此时用户线程STW
   - 并发性：G1拥有与应用程序交替执行的能力，部分工作可以和应用程序同时执行，因此，一般来说，不会在整个回收阶段发生完全阻塞应用程序的情况
2. **分代收集**
   - 从分代上看，G1依然属于分代型垃圾回收器，它会区分年轻代和老年代，年轻代依然有Eden区和Survivor区。但从堆的结构上看，它不要求整个Eden区、年轻代或者老年代都是连续的，也不再坚持固定大小和固定数量。
   - 将堆空间分为若干个区域（Region），这些区域中包含了逻辑上的年轻代和老年代。
   - 和之前的各类回收器不同，它同时兼顾年轻代和老年代。对比其他回收器，或者工作在年轻代，或者工作在老年代；

G1的分代，已经不是下面这样的了
![](image/1664244599429-627b466b-75bf-4b64-9ede-12d3615331d7.png)
G1的分区是这样的一个区域
![](image/1664244598843-57389940-674b-4557-8d14-0117b0c7db47.png)
**空间整合**

1. CMS：“标记-清除”算法、内存碎片、若干次GC后进行一次碎片整理
2. G1将内存划分为一个个的region。内存的回收是以region作为基本单位的。**Region之间是复制算法，但整体上实际可看作是标记-压缩（Mark-Compact）算法**，两种算法都可以避免内存碎片。这种特性有利于程序长时间运行，分配大对象时不会因为无法找到连续内存空间而提前触发下一次GC。尤其是当Java堆非常大的时候，G1的优势更加明显。

**可预测的停顿时间模型（即：软实时soft real-time）**
这是G1相对于CMS的另一大优势，G1除了追求低停顿外，还能建立可预测的停顿时间模型，能让使用者明确指定在一个长度为M毫秒的时间片段内，消耗在垃圾收集上的时间不得超过N毫秒。

1. 由于分区的原因，G1可以只选取部分区域进行内存回收，这样缩小了回收的范围，因此对于全局停顿情况的发生也能得到较好的控制。
2. G1跟踪各个Region里面的垃圾堆积的价值大小（回收所获得的空间大小以及回收所需时间的经验值），在后台维护一个优先列表，**每次根据允许的收集时间，优先回收价值最大的Region**。保证了G1收集器在有限的时间内可以获取尽可能高的收集效率。
3. 相比于CMS GC，G1未必能做到CMS在最好情况下的延时停顿，但是最差情况要好很多。
#### 缺点

1. 相较于CMS，G1还不具备全方位、压倒性优势。比如在用户程序运行过程中，G1无论是为了垃圾收集产生的内存占用（Footprint）还是程序运行时的额外执行负载（overload）都要比CMS要高。
2. 从经验上来说，在小内存应用上CMS的表现大概率会优于G1，而G1在大内存应用上则发挥其优势。平衡点在6-8GB之间。
### 参数设置
`-XX:+UseG1GC`：手动指定使用G1垃圾收集器执行内存回收任务
`-XX:G1HeapRegionSize`：设置每个Region的大小。值是2的幂，范围是1MB到32MB之间，目标是根据最小的Java堆大小划分出约2048个区域。默认是堆内存的1/2000。
`-XX:MaxGCPauseMillis`：设置期望达到的最大GC停顿时间指标，JVM会尽力实现，但不保证达到。默认值是200ms
`-XX:+ParallelGCThread`：设置STW工作线程数的值。最多设置为8
`-XX:ConcGCThreads`：设置并发标记的线程数。将n设置为并行垃圾回收线程数（ParallelGcThreads）的1/4左右。
`-XX:InitiatingHeapOccupancyPercent`：设置触发并发GC周期的Java堆占用率阈值。超过此值，就触发GC。默认值是45。
### 常见操作步骤
G1的设计原则就是简化JVM性能调优，开发人员只需要简单的三步即可完成调优：

1. 第一步：开启G1垃圾收集器
2. 第二步：设置堆的最大内存
3. 第三步：设置最大的停顿时间

G1中提供了三种垃圾回收模式：YoungGC、Mixed GC和Full GC，在不同的条件下被触发。
### G1 的适用场景

1. 面向服务端应用，针对具有大内存、多处理器的机器。（在普通大小的堆里表现并不惊喜）
2. 最主要的应用是需要低GC延迟，并具有大堆的应用程序提供解决方案；
3. 如：在堆大小约6GB或更大时，可预测的暂停时间可以低于0.5秒；（G1通过每次只清理一部分而不是全部的Region的增量式清理来保证每次GC停顿时间不会过长）。
4. 用来替换掉JDK1.5中的CMS收集器；在下面的情况时，使用G1可能比CMS好：
   - 超过50%的Java堆被活动数据占用；
   - 对象分配频率或年代提升频率变化很大；
   - GC停顿时间过长（长于0.5至1秒）
5. HotSpot垃圾收集器里，除了G1以外，其他的垃圾收集器均使用内置的JVM线程执行GC的多线程操作，而G1 GC可以采用应用线程承担后台运行的GC工作，即当JVM的GC线程处理速度慢时，系统会调用应用程序线程帮助加速垃圾回收过程。
### 分区 Region
**分区 Region：化整为零**

1. 使用G1收集器时，它将整个Java堆划分成约2048个大小相同的独立Region块，每个Region块大小根据堆空间的实际大小而定，整体被控制在1MB到32MB之间，且为2的N次幂，即1MB，2MB，4MB，8MB，16MB，32MB。可以通过
2. `XX:G1HeapRegionSize`设定。**所有的Region大小相同，且在JVM生命周期内不会被改变。**
3. 虽然还保留有新生代和老年代的概念，但新生代和老年代不再是物理隔离的了，它们都是一部分Region（不需要连续）的集合。通过Region的动态分配方式实现逻辑上的连续。
4. 一个Region有可能属于Eden，Survivor或者Old/Tenured内存区域。但是一个Region只可能属于一个角色。图中的E表示该Region属于Eden内存区域，S表示属于Survivor内存区域，O表示属于Old内存区域。图中空白的表示未使用的内存空间。
5. G1垃圾收集器还增加了一种新的内存区域，叫做Humongous内存区域，如图中的H块。主要用于存储大对象，如果超过0.5个Region，就放到H。

纠错：尚硅谷视频里这里写的是超过1.5个region。根据[官方文档](https://www.oracle.com/technetwork/tutorials/tutorials-1876574.html): **The G1 Garbage Collector Step by Step**
As shown regions can be allocated into Eden, survivor, and old generation regions. In addition, there is a fourth type of object known as Humongous regions. These regions are designed to hold objects that are 50% the size of a standard region or larger. They are stored as a set of contiguous regions. Finally the last type of regions would be the unused areas of the heap.
翻译：
如图所示，可以将区域分配到Eden，幸存者和旧时代区域。 此外，还有第四种类型的物体被称为巨大区域。 这些区域旨在容纳标准区域大小的50％或更大的对象。 它们存储为一组连续区域。 最后，最后一种区域类型是堆的未使用区域。
![](image/1664244599005-6b70a510-b6a8-4eeb-9369-976e50c5fbe4.png)
**设置 H 的原因**
对于堆中的大对象，默认直接会被分配到老年代，但是如果**它是一个短期存在的大对象**就会对垃圾收集器造成负面影响。为了解决这个问题，G1划分了一个Humongous区，它用来专门存放大对象。如**果一个H区装不下一个大对象，那么G1会寻找连续的H区来存储**。为了能找到连续的H区，有时候不得不启动Full GC。G1的大多数行为都把H区作为老年代的一部分来看待。
**Regio的细节**
![](image/1664244599492-b0280a9a-68b3-4d22-b09c-bd0d6c6000b8.png)

1. 每个Region都是通过指针碰撞来分配空间
2. G1为每一个Region设 计了两个名为TAMS（Top at Mark Start）的指针，把Region中的一部分空间划分出来用于并发回收过程中的新对象分配，并发回收时新分配的对象地址都必须要在这两个指针位置以上。
3. TLAB 线程专用 的内存分配区域
### 回收流程
G1 GC的垃圾回收过程主要包括如下三个环节：

- 年轻代GC（Young GC）
- 老年代并发标记过程（Concurrent Marking）
- 混合回收（Mixed GC）
- （如果需要，单线程、独占式、高强度的Full GC还是继续存在的。它针对GC的评估失败提供了一种失败保护机制，即强力回收。）

![](image/1664244599972-5d7bc3fb-25e2-444b-815d-bf36e713212c.png)
顺时针，Young GC --> Young GC+Concurrent Marking --> Mixed GC顺序，进行垃圾回收
**回收流程**

1. 应用程序分配内存，当年轻代的Eden区用尽时开始年轻代回收过程；G1的年轻代收集阶段是一个并行的独占式收集器。在年轻代回收期，G1 GC暂停所有应用程序线程，启动多线程执行年轻代回收。然后从年轻代区间移动存活对象到Survivor区间或者老年区间，也有可能是两个区间都会涉及。
2. 当堆内存使用达到一定值（默认45%）时，开始老年代并发标记过程。
3. 标记完成马上开始混合回收过程。对于一个混合回收期，G1 GC从老年区间移动存活对象到空闲区间，这些空闲区间也就成为了老年代的一部分。和年轻代不同，老年代的G1回收器和其他GC不同，**G1的老年代回收器不需要整个老年代被回收，一次只需要扫描/回收一小部分老年代的Region就可以了**。同时，这个老年代Region是和年轻代一起被回收的。
4. 举个例子：一个Web服务器，Java进程最大堆内存为4G，每分钟响应1500个请求，每45秒钟会新分配大约2G的内存。G1会每45秒钟进行一次年轻代回收，每31个小时整个堆的使用率会达到45%，会开始老年代并发标记过程，标记完成后开始四到五次的混合回收。
### Remembered Set（记忆集）

1. 一个对象被不同区域引用的问题
2. 一个Region不可能是孤立的，一个Region中的对象可能被其他任意Region中对象引用，判断对象存活时，是否需要扫描整个Java堆才能保证准确？
3. 在其他的分代收集器，也存在这样的问题（而G1更突出，因为G1主要针对大堆）
4. 回收新生代也不得不同时扫描老年代？这样的话会降低Minor GC的效率

**解决方法：**

1. 无论G1还是其他分代收集器，JVM都是使用Remembered Set来避免全堆扫描；
2. 每个Region都有一个对应的Remembered Set
3. 每次Reference类型数据写操作时，都会产生一个Write Barrier暂时中断操作；
4. 然后检查将要写入的引用指向的对象是否和该Reference类型数据在不同的Region（其他收集器：检查老年代对象是否引用了新生代对象）；
5. 如果不同，通过CardTable把相关引用信息记录到引用指向对象的所在Region对应的Remembered Set中；
6. 当进行垃圾收集时，在GC根节点的枚举范围加入Remembered Set；就可以保证不进行全局扫描，也不会有遗漏。

![](image/1664244600625-275b93e6-6fb2-44e5-858f-3ed38f9a2f98.png)

1. 在回收 Region 时，为了不进行全堆的扫描，引入了 Remembered Set
2. Remembered Set 记录了当前 Region 中的对象被哪个对象引用了
3. 这样在进行 Region 复制时，就不要扫描整个堆，只需要去 Remembered Set 里面找到引用了当前 Region 的对象
4. Region 复制完毕后，修改 Remembered Set 中对象的引用即可

### 回收过程分析
#### 过程一：年轻代 GC
JVM启动时，G1先准备好Eden区，程序在运行过程中不断创建对象到Eden区，当Eden空间耗尽时，G1会启动一次年轻代垃圾回收过程。
年轻代回收只回收Eden区和Survivor区
YGC时，首先G1停止应用程序的执行（Stop-The-World），G1创建回收集（Collection Set），回收集是指需要被回收的内存分段的集合，年轻代回收过程的回收集包含年轻代Eden区和Survivor区所有的内存分段。
![](image/1664244600763-146a6129-ea94-47de-aa83-c4fddc4fcb10.png)
图的大致意思就是：

- 回收完E和S区，剩余存活的对象会复制到新的S区
- S区达到一定的阈值可以晋升为O区

**细致过程：**
**然后开始如下回收过程：**

1. 第一阶段，扫描根根是指GC Roots，根引用连同RSet记录的外部引用作为扫描存活对象的入口。
2. 第二阶段，更新RSet
3. 第三阶段，处理RSet识别被老年代对象指向的Eden中的对象，这些被指向的Eden中的对象被认为是存活的对象。
4. 第四阶段，复制对象。
   - 此阶段，对象树被遍历，Eden区内存段中存活的对象会被复制到Survivor区中空的内存分段，Survivor区内存段中存活的对象
   - 如果年龄未达阈值，年龄会加1，达到阀值会被会被复制到Old区中空的内存分段。
   - 如果Survivor空间不够，Eden空间的部分数据会直接晋升到老年代空间。
5. 第五阶段，处理引用处理Soft，Weak，Phantom，Final，JNI Weak 等引用。最终Eden空间的数据为空，GC停止工作，而目标内存中的对象都是连续存储的，没有碎片，所以复制过程可以达到内存整理的效果，减少碎片。

**备注：**

1. 对于应用程序的引用赋值语句 oldObject.field（这个是老年代）=object（这个是新生代），JVM会在之前和之后执行特殊的操作以在dirty card queue中入队一个保存了对象引用信息的card。在年轻代回收的时候，G1会对Dirty Card Queue中所有的card进行处理，以更新RSet，保证RSet实时准确的反映引用关系。
2. 那为什么不在引用赋值语句处直接更新RSet呢？这是为了性能的需要，RSet的处理需要线程同步，开销会很大，使用队列性能会好很多。
#### 过程二：并发标记过程

1. 初始标记阶段：标记从根节点直接可达的对象。这个阶段是STW的，并且会触发一次年轻代GC。正是由于该阶段时STW的，所以我们只扫描根节点可达的对象，以节省时间。
2. 根区域扫描（Root Region Scanning）：G1 GC扫描Survivor区直接可达的老年代区域对象，并标记被引用的对象。这一过程必须在Young GC之前完成，因为Young GC会使用复制算法对Survivor区进行GC。
3. 并发标记（Concurrent Marking）：
   1. 在整个堆中进行并发标记（和应用程序并发执行），此过程可能被Young GC中断。
   2. **在并发标记阶段，若发现区域对象中的所有对象都是垃圾，那这个区域会被立即回收。**
   3. 同时，并发标记过程中，会计算每个区域的对象活性（区域中存活对象的比例）。
4. 再次标记（Remark）：由于应用程序持续进行，需要修正上一次的标记结果。是STW的。G1中采用了比CMS更快的原始快照算法：Snapshot-At-The-Beginning（SATB）。
5. 独占清理（cleanup，STW）：计算各个区域的存活对象和GC回收比例，并进行排序，识别可以混合回收的区域。为下阶段做铺垫。是STW的。这个阶段并不会实际上去做垃圾的收集
6. 并发清理阶段：识别并清理完全空闲的区域。
#### 过程三：混合回收过程
当越来越多的对象晋升到老年代Old Region时，为了避免堆内存被耗尽，虚拟机会触发一个混合的垃圾收集器，即Mixed GC，该算法并不是一个Old GC，除了回收整个Young Region，还会回收一部分的Old Region。这里需要注意：是一部分老年代，而不是全部老年代。可以选择哪些Old Region进行收集，从而可以对垃圾回收的耗时时间进行控制。也要注意的是Mixed GC并不是Full GC。
![image.png](https://cdn.nlark.com/yuque/0/2022/png/26368762/1664249218885-0dc1ce42-a49b-46a9-a6e4-fb8a098db104.png#clientId=ue9516613-2cc2-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=382&id=uac4ec780&margin=%5Bobject%20Object%5D&name=image.png&originHeight=382&originWidth=448&originalType=binary&ratio=1&rotation=0&showTitle=false&size=135425&status=done&style=none&taskId=u34c1d0ed-9b30-4636-941b-84834499108&title=&width=448)
**混合回收的细节**

1. 并发标记结束以后，老年代中百分百为垃圾的内存分段被回收了，部分为垃圾的内存分段被计算了出来。默认情况下，这些老年代的内存分段会分8次（可以通过-XX:G1MixedGCCountTarget设置）被回收。【意思就是一个Region会被分为8个内存段】
2. 混合回收的回收集（Collection Set）包括八分之一的老年代内存分段，Eden区内存分段，Survivor区内存分段。混合回收的算法和年轻代回收的算法完全一样，只是回收集多了老年代的内存分段。具体过程请参考上面的年轻代回收过程。
3. 由于老年代中的内存分段默认分8次回收，G1会优先回收垃圾多的内存分段。垃圾占内存分段比例越高的，越会被先回收。并且有一个阈值会决定内存分段是否被回收。XX:G1MixedGCLiveThresholdPercent，默认为65%，意思是垃圾占内存分段比例要达到65%才会被回收。如果垃圾占比太低，意味着存活的对象占比高，在复制的时候会花费更多的时间。
4. 混合回收并不一定要进行8次。有一个阈值-XX:G1HeapWastePercent，默认值为10%，意思是允许整个堆内存中有10%的空间被浪费，意味着如果发现可以回收的垃圾占堆内存的比例低于10%，则不再进行混合回收。因为GC会花费很多的时间但是回收到的内存却很少。
#### 可选的过程四：Full GC

1. G1的初衷就是要避免Full GC的出现。但是如果上述方式不能正常工作，G1会停止应用程序的执行（Stop-The-World），使用**单线程**的内存回收算法进行垃圾回收，性能会非常差，应用程序停顿时间会很长。
2. 要避免Full GC的发生，一旦发生Full GC，需要对JVM参数进行调整。什么时候会发生Ful1GC呢？比如堆内存太小，当G1在复制存活对象的时候没有空的内存分段可用，则会回退到Full GC，这种情况可以通过增大内存解决。

导致G1 Full GC的原因可能有两个：

1. EVacuation的时候没有足够的to-space来存放晋升的对象；
2. 并发处理过程完成之前空间耗尽。
### G1补充
从Oracle官方透露出来的信息可获知，回收阶段（Evacuation）其实本也有想过设计成与用户程序一起并发执行，但这件事情做起来比较复杂，考虑到G1只是回一部分Region，停顿时间是用户可控制的，所以并不迫切去实现，**而选择把这个特性放到了G1之后出现的低延迟垃圾收集器（即ZGC）中。**另外，还考虑到G1不是仅仅面向低延迟，停顿用户线程能够最大幅度提高垃圾收集效率，为了保证吞吐量所以才选择了完全暂停用户线程的实现方案。
**G1 回收器的优化建议**
年轻代大小

- 避免使用-Xmn或-XX:NewRatio等相关选项显式设置年轻代大小，因为固定年轻代的大小会覆盖可预测的暂停时间目标。我们让G1自己去调整

暂停时间目标不要太过严苛

- G1 GC的吞吐量目标是90%的应用程序时间和10%的垃圾回收时间
- 评估G1 GC的吞吐量时，暂停时间目标不要太严苛。目标太过严苛表示你愿意承受更多的垃圾回收开销，而这些会直接影响到吞吐量。
## 8、收集器总结比较
### 7 种垃圾回收器的比较
截止JDK1.8，一共有7款不同的垃圾收集器。每一款的垃圾收集器都有不同的特点，在具体使用的时候，需要根据具体的情况选用不同的垃圾收集器。
[![](https://cdn.nlark.com/yuque/0/2022/jpeg/26368762/1664244603179-eb8aa90f-3eb2-4b0e-937f-151f8bd2e413.jpeg#clientId=ue9516613-2cc2-4&crop=0&crop=0&crop=1&crop=1&from=paste&id=udd9e3df4&margin=%5Bobject%20Object%5D&originHeight=344&originWidth=1313&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u8d291a66-13a0-4164-af9c-b59039d1466&title=)](https://camo.githubusercontent.com/23db37f59b836e48d2db93912e6e3311160fc68ff348b2ed321dd314ebcb38aa/68747470733a2f2f6e706d2e656c656d6563646e2e636f6d2f796f7574686c716c40312e302e382f4a564d2f636861707465725f3031322f303033342e6a7067)
![](image/1664244602185-438153c0-42e8-4671-a1fd-d3fbd9fa62a4.png)
### 怎么选择垃圾回收器
Java垃圾收集器的配置对于JVM优化来说是一个很重要的选择，选择合适的垃圾收集器可以让JVM的性能有一个很大的提升。怎么选择垃圾收集器？

1. 优先调整堆的大小让JVM自适应完成。
2. 如果内存小于100M，使用串行收集器
3. 如果是单核、单机程序，并且没有停顿时间的要求，串行收集器
4. 如果是多CPU、需要高吞吐量、允许停顿时间超过1秒，选择并行或者JVM自己选择
5. 如果是多CPU、追求低停顿时间，需快速响应（比如延迟不能超过1秒，如互联网应用），使用并发收集器
6. 官方推荐G1，性能高。现在互联网的项目，基本都是使用G1。

最后需要明确一个观点：

1. 没有最好的收集器，更没有万能的收集算法
2. 调优永远是针对特定场景、特定需求，不存在一劳永逸的收集器

**面试**

1. 对于垃圾收集，面试官可以循序渐进从理论、实践各种角度深入，也未必是要求面试者什么都懂。但如果你懂得原理，一定会成为面试中的加分项。
2. 这里较通用、基础性的部分如下：
   - 垃圾收集的算法有哪些？如何判断一个对象是否可以回收？
   - 垃圾收集器工作的基本流程。
3. 另外，大家需要多关注垃圾回收器这一章的各种常用的参数
## 9、GC 日志分析
### 常用参数配置
**GC 日志参数设置**
**通过阅读GC日志，我们可以了解Java虚拟机内存分配与回收策略。**
内存分配与垃圾回收的参数列表

- `-XX:+PrintGC` ：输出GC日志。类似：-verbose:gc
- `-XX:+PrintGCDetails` ：输出GC的详细日志
- `-XX:+PrintGCTimestamps` ：输出GC的时间戳（以基准时间的形式）
- `-XX:+PrintGCDatestamps` ：输出GC的时间戳（以日期的形式，如2013-05-04T21: 53: 59.234 +0800）
- `-XX:+PrintHeapAtGC` ：在进行GC的前后打印出堆的信息
- `-Xloggc:…/logs/gc.log` ：日志文件的输出路径

**PrintGCDetails**
1、JVM 参数
-XX:+PrintGCDetails
2、输入信息如下
![](image/1664244605364-39336de3-c9f2-4212-ad8b-a68f610c41a8.png)
3、参数解析
![](image/1664244606849-a9e0309b-6aaf-4c4b-a817-09adb8c5b817.png)

### 补充说明

1. “[GC"和”[Full GC"说明了这次垃圾收集的停顿类型，如果有"Full"则说明GC发生了"Stop The World"
2. 使用Serial收集器在新生代的名字是Default New Generation，因此显示的是"[DefNew"
3. 使用ParNew收集器在新生代的名字会变成"[ParNew"，意思是"Parallel New Generation"
4. 使用Parallel scavenge收集器在新生代的名字是”[PSYoungGen"
5. 老年代的收集和新生代道理一样，名字也是收集器决定的
6. 使用G1收集器的话，会显示为"garbage-first heap"
7. Allocation Failure表明本次引起GC的原因是因为在年轻代中没有足够的空间能够存储新的数据了。
8. [ PSYoungGen: 5986K->696K(8704K) ] 5986K->704K (9216K)
   - 中括号内：GC回收前年轻代大小，回收后大小，（年轻代总大小）
   - 括号外：GC回收前年轻代和老年代大小，回收后大小，（年轻代和老年代总大小）
9. user代表用户态回收耗时，sys内核态回收耗时，real实际耗时。由于多核线程切换的原因，时间总和可能会超过real时间
#### Young GC
![](image/1664244614500-0d6838bd-c5e6-4ba9-8ff6-e8edf7a13809.png)
#### Full GC
![](image/1664244616351-c652e731-3d55-43bf-92bd-3eebef67d753.png)
#### 举例
```java
/**
 * 在jdk7 和 jdk8中分别执行
 * -verbose:gc -Xms20M -Xmx20M -Xmn10M -XX:+PrintGCDetails -XX:SurvivorRatio=8 -XX:+UseSerialGC
 */
public class GCLogTest1 {
    private static final int _1MB = 1024 * 1024;

    public static void testAllocation() {
        byte[] allocation1, allocation2, allocation3, allocation4;
        allocation1 = new byte[2 * _1MB];
        allocation2 = new byte[2 * _1MB];
        allocation3 = new byte[2 * _1MB];
        allocation4 = new byte[4 * _1MB];
    }

    public static void main(String[] agrs) {
        testAllocation();
    }
}
```
**JDK7 中的情况**
1、首先我们会将3个2M的数组存放到Eden区，然后后面4M的数组来了后，将无法存储，因为Eden区只剩下2M的剩余空间了，那么将会进行一次Young GC操作，将原来Eden区的内容，存放到Survivor区，但是Survivor区也存放不下，那么就会直接晋级存入Old 区
![](image/1664244616934-c89cccbd-e348-49fa-8a2c-7980cf792f50.png)
2、然后我们将4M对象存入到Eden区中
![](image/1664244617917-71d99276-b827-4b12-b9b5-c8862efbebe2.png)
老年代图画的有问题，free应该是4M
**JDK8 中的情况**
[![](https://cdn.nlark.com/yuque/0/2022/jpeg/26368762/1664244621672-cf518114-31a4-4752-b24e-9f5fed870f11.jpeg#clientId=ue9516613-2cc2-4&crop=0&crop=0&crop=1&crop=1&from=paste&id=u1574d2c7&margin=%5Bobject%20Object%5D&originHeight=508&originWidth=1095&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u52482cbc-d3d4-49af-b864-7efc15fea74&title=)](https://camo.githubusercontent.com/068088b71ffe465cabb6c6c68bb7a430802e4445f39d543bb859c6d3b7e3ebd3/68747470733a2f2f6e706d2e656c656d6563646e2e636f6d2f796f7574686c716c40312e302e382f4a564d2f636861707465725f3031322f303033352e6a7067)
与 JDK7 不同的是，JDK8 直接判定 4M 的数组为大对象，直接怼到老年区去了
### 常用日志分析工具
**保存日志文件**
**JVM参数**：-XLoggc:./logs/gc.log， ./ 表示当前目录，在 IDEA中程序运行的当前目录是工程的根目录，而不是模块的根目录
可以用一些工具去分析这些GC日志，常用的日志分析工具有：
GCViewer、GCEasy、GCHisto、GCLogViewer、Hpjmeter、garbagecat等
**推荐：GCeasy**
在线分析网址：gceasy.io
[![](https://cdn.nlark.com/yuque/0/2022/jpeg/26368762/1664244622632-ff5a7fa3-ed51-4d4c-bcc1-732d0a8edfdc.jpeg#clientId=ue9516613-2cc2-4&crop=0&crop=0&crop=1&crop=1&from=paste&id=ua22043dc&margin=%5Bobject%20Object%5D&originHeight=793&originWidth=1684&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u77c93ce7-3c46-4d9d-a097-0a5eba78a81&title=)](https://camo.githubusercontent.com/31bf1c05e294c2e26bb86f73c688a8dc48720284a75c0c055e6a5a807df21c36/68747470733a2f2f6e706d2e656c656d6563646e2e636f6d2f796f7574686c716c40312e302e382f4a564d2f636861707465725f3031322f303033362e6a7067)
![](image/1664244622915-0820fa2c-cbee-45a1-845d-c05e8a05827d.png)
![](image/1664244623193-d0da058b-c77f-4b97-a13d-53bed5e40b59.png)
## 10、垃圾回收器的新发展
### 发展过程

1. GC仍然处于飞速发展之中，目前的默认选项G1 GC在不断的进行改进，很多我们原来认为的缺点，例如串行的Full GC、Card Table扫描的低效等，都已经被大幅改进，例如，JDK10以后，Fu11GC已经是并行运行，在很多场景下，其表现还略优于ParallelGC的并行Ful1GC实现。
2. 即使是SerialGC，虽然比较古老，但是简单的设计和实现未必就是过时的，它本身的开销，不管是GC相关数据结构的开销，还是线程的开销，都是非常小的，所以随着云计算的兴起，在serverless等新的应用场景下，Serial Gc找到了新的舞台。
3. 比较不幸的是CMSGC，因为其算法的理论缺陷等原因，虽然现在还有非常大的用户群体，但在JDK9中已经被标记为废弃，并在JDK14版本中移除
4. 现在G1回收器已成为默认回收器好几年了。我们还看到了引入了两个新的收集器：ZGC（JDK11出现）和Shenandoah（Open JDK12），其特点：主打低停顿时间
### Shenandoah GC
**Open JDK12的Shenandoash GC：低停顿时间的GC（实验性）**

1. Shenandoah无疑是众多GC中最孤独的一个。是第一款不由Oracle公司团队领导开发的Hotspot垃圾收集器。不可避免的受到官方的排挤。比如号称openJDK和OracleJDK没有区别的Oracle公司仍拒绝在OracleJDK12中支持Shenandoah。
2. Shenandoah垃圾回收器最初由RedHat进行的一项垃圾收集器研究项目Pauseless GC的实现，旨在针对JVM上的内存回收实现低停顿的需求。在2014年贡献给OpenJDK。
3. Red Hat研发Shenandoah团队对外宣称，Shenandoah垃圾回收器的暂停时间与堆大小无关，这意味着无论将堆设置为200MB还是200GB，99.9%的目标都可以把垃圾收集的停顿时间限制在十毫秒以内。不过实际使用性能将取决于实际工作堆的大小和工作负载。

这是RedHat在2016年发表的论文数据，测试内容是使用ES对200GB的维基百科数据进行索引。从结果看：

1. 停顿时间比其他几款收集器确实有了质的飞跃，但也未实现最大停顿时间控制在十毫秒以内的目标。
2. 而吞吐量方面出现了明显的下降，总运行时间是所有测试收集器里最长的。

![](image/1664244624120-a5fe2c2c-473e-48d1-abe9-2b743fd0e8a2.png)
总结

1. Shenandoah GC的弱项：高运行负担下的吞吐量下降。
2. Shenandoah GC的强项：低延迟时间。
### 令人震惊、革命性的 ZGC

1. 官方文档：[https://docs.oracle.com/en/java/javase/12/gctuning/](https://docs.oracle.com/en/java/javase/12/gctuning/)
2. ZGC与Shenandoah目标高度相似，在尽可能对吞吐量影响不大的前提下，实现在任意堆内存大小下都可以把垃圾收集的停颇时间限制在十毫秒以内的低延迟。
3. 《深入理解Java虚拟机》一书中这样定义ZGC：ZGC收集器是一款基于Region内存布局的，（暂时）不设分代的，使用了读屏障、染色指针和内存多重映射等技术来实现可并发的标记-压缩算法的，以低延迟为首要目标的一款垃圾收集器。
4. ZGC的工作过程可以分为4个阶段：并发标记 - 并发预备重分配 - 并发重分配 - 并发重映射 等。
5. ZGC几乎在所有地方并发执行的，除了初始标记的是STW的。所以停顿时间几乎就耗费在初始标记上，这部分的实际时间是非常少的。

**吞吐量**
![](image/1664244625435-79639903-abd3-4444-9db1-bd29499ddc22.png)
max-JOPS：以低延迟为首要前提下的数据
critical-JOPS：不考虑低延迟下的数据
**低延迟**
![](image/1664244625491-d5e5f25d-1a5d-41c6-98d7-3772231f591e.png)
在ZGC的强项停顿时间测试上，它毫不留情的将Parallel、G1拉开了两个数量级的差距。无论平均停顿、95%停顿、998停顿、99. 98停顿，还是最大停顿时间，ZGC都能毫不费劲控制在10毫秒以内。
虽然ZGC还在试验状态，没有完成所有特性，但此时性能已经相当亮眼，用“令人震惊、革命性”来形容，不为过。未来将在服务端、大内存、低延迟应用的首选垃圾收集器。
![](image/1664244628127-3afca50a-7244-4bde-9aea-c977d347b7b5.png)

1. JDK14之前，ZGC仅Linux才支持。
2. 尽管许多使用ZGC的用户都使用类Linux的环境，但在Windows和macOS上，人们也需要ZGC进行开发部署和测试。许多桌面应用也可以从ZGC中受益。因此，ZGC特性被移植到了Windows和macOS上。
3. 现在mac或Windows上也能使用ZGC了，示例如下：-XX:+UnlockExperimentalVMOptions-XX：+UseZGC
### 面向大堆的 AliGC
AliGC是阿里巴巴JVM团队基于G1算法，面向大堆（LargeHeap）应用场景。指定场景下的对比：
![image.png](https://cdn.nlark.com/yuque/0/2022/png/26368762/1664250005875-a0e747b0-8a00-4083-90eb-fff6197bd730.png#clientId=ue9516613-2cc2-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=291&id=ua8f0a70d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=291&originWidth=786&originalType=binary&ratio=1&rotation=0&showTitle=false&size=88776&status=done&style=none&taskId=ub2718af3-2728-4b3d-86d5-7c98db3e3c0&title=&width=786)