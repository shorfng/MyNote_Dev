> 【Java】12_EfficiencyTools（效率工具）-> 12.8_DeployContainer（部署容器）-> 01_ApacheTomcat



# 1、Tomcat 下载安装和配置

## 1.0 Tomcat 下载

- 官网地址：https://tomcat.apache.org/

![image-20210429110647776](image/image-20210429110647776.png)



## 1.1 Win系统 -  Tomcat安装和配置





## 1.2 Linux系统 -  Tomcat安装和配置





## 1.3 Mac系统 -  Tomcat安装和配置



## 1.4 Tomcat 目录结构

![image-20210429135128515](image/image-20210429135128515.png)

### （1）bin

```
- 该目录下存放的是二进制可执行文件
- 如果是安装版，这个目录下会有 tomcat6.exe（在控制台下启动Tomcat）、tomcat6w.exe（弹出UGI窗口启动Tomcat）
- 如果是解压版，这个目录下会有 startup.bat（用来启动Tomcat，需要先配置JAVA_HOME环境变量）、shutdown.bat（用来停止Tomcat）
```

### （2）conf

```
这个目录下有四个最为重要的文件:
- server.xml：配置整个服务器信息（例如修改端口号，添加虚拟主机等）

- tomcatusers.xml：存储tomcat用户的文件，这里保存的是tomcat的用户名及密码，以及用户的角色信息。可以按着该文件中的注释信息添加tomcat用户，然后就可以在Tomcat主页中进入Tomcat Manager页面了

- web.xml：部署描述符文件，这个文件中注册了很多MIME类型，即文档类型。这些MIME类型是客户端与服务器之间说明文档类型的，如用户请求一个html网页，那么服务器还会告诉客户端浏览器响应的文档是text/html类型的，这就是一个MIME类型。客户端浏览器通过这个MIME类型就知道如何处理它了。当然是在浏览器中显示这个html文件了。但如果服务器响应的是一个exe文件，那么浏览器就不可能显示它，而是应该弹出下载窗口才对。MIME就是用来说明文档的内容是什么类型的！

- context.xml：对所有应用的统一配置，通常不会去配置它
```

### （3）lib

```
- Tomcat的类库，里面是一大堆jar文件
- 如果需要添加Tomcat依赖的jar文件，可以把它放到这个目录中
- 也可以把应用依赖的jar文件放到这个目录中，这个目录中的jar所有项目都可以共享之，但如果应用再放到其他Tomcat下时就不能再共享这个目录下的Jar包了，所以建议只把Tomcat需要的Jar包放到这个目录下
```

### （4）logs

```
- 记录了Tomcat启动和关闭的信息
- 如果启动Tomcat时有错误，那么异常也会记录在日志文件中
```

### （5）temp

```
- 存放Tomcat的临时文件
- 这个目录下的东西可以在停止Tomcat后删除！
```

### （6）webapps

```
- 存放web项目的目录，其中每个文件夹都是一个项目
- 如果这个目录下已经存在了目录，那么都是tomcat自带的项目
- 其中ROOT是一个特殊的项目，在地址栏中没有给出项目目录时，对应的就是ROOT项目
- http://localhost:8080/examples，进入示例项目，其中examples就是项目名，即文件夹的名字
```

### （7）work

```
- 运行时生成的文件，最终运行的文件都在这里
- 通过webapps中的项目生成的！可以把这个目录下的内容删除，再次运行时会生再次生成work目录
- 当客户端用户访问一个JSP文件时，Tomcat会通过JSP生成Java文件，然后再编译Java文件生成class文件，生成的java和class文件都会存放到这个目录下
```



## 1.5 核心配置文件 conf/server.xml 详解

### （1）Server 根标签

```xml
<!-- Server 根元素，创建⼀个Server实例 -->
<Server>
	<!-- 定义监听器 -->
	<Listener/>
	
	<!-- 定义服务器的全局JNDI资源 -->
	<GlobalNamingResources/>
	
	<!-- 定义⼀个Service服务，⼀个Server标签可以有多个Service服务实例 -->
	<Service/>
</Server>
```



```xml
<!--
 port：关闭服务器的监听端⼝
 shutdown：关闭服务器的指令字符串
-->
<Server port="8005" shutdown="SHUTDOWN">
	<!-- 以⽇志形式输出服务器 、操作系统、JVM的版本信息 -->
	<Listener className="org.apache.catalina.startup.VersionLoggerListener"/>
	
	<!-- Security listener. Documentation at /docs/config/listeners.html
	<Listener className="org.apache.catalina.security.SecurityListener" />-->

	<!--APR library loader. Documentation at /docs/apr.html -->
	<!-- 加载（服务器启动）和 销毁 （服务器停⽌）APR。 如果找不到APR库，则会输出⽇志，并不影响 Tomcat 启动 -->
	<Listener SSLEngine="on" className="org.apache.catalina.core.AprLifecycleListener"/>

	<!-- Prevent memory leaks due to use of particular java/javax APIs-->
	<!-- 避免JRE内存泄漏问题 -->
	<Listener className="org.apache.catalina.core.JreMemoryLeakPreventionListener"/>
	
	<!-- 加载（服务器启动） 和 销毁（服务器停⽌） 全局命名服务 -->
	<Listener className="org.apache.catalina.mbPeans.GlobalResourcesLifecycleListener"/>
	
	<!-- 在Context停⽌时重建 Executor 池中的线程， 以避免ThreadLocal 相关的内存泄漏 -->
	<Listener className="org.apache.catalina.core.ThreadLocalLeakPreventionListener"/>
	
	<!-- Global JNDI resources  Documentation at /docs/jndi-resources-howto.html
	GlobalNamingResources 中定义了全局命名服务
	-->
	<GlobalNamingResources>
		<!-- Editable user database that can also be used by UserDatabaseRealm to authenticate users-->
		<Resource auth="Container" description="User database that can be updated and saved" factory="org.apache.catalina.users.MemoryUserDatabaseFactory" name="UserDatabase" pathname="conf/tomcat-users.xml" type="org.apache.catalina.UserDatabase"/>
	</GlobalNamingResources>
	
  <!-- A "Service" is a collection of one or more "Connectors" that share a single "Container" Note: A "Service" is not itself a "Container", so you may not define subcomponents such as "Valves" at this level.Documentation at /docs/config/service.html-->
	<Service name="Catalina">
		...
 	</Service>
</Server>
```

### （2）Service标签

```xml
<!-- 该标签⽤于创建 Service 实例，默认使⽤ org.apache.catalina.core.StandardService -->
<!-- 默认情况下，Tomcat 仅指定了Service 的名称， 值为 "Catalina" -->
<Service name="Catalina">
	<!-- ⽤于为Service添加⽣命周期监听器 -->
	<Listener/>

	<!-- ⽤于配置Service 共享线程池 -->
	<Executor/>

	<!-- ⽤于配置Service 包含的链接器 -->
	<Connector/>

	<!-- ⽤于配置Service中链接器对应的Servlet 容器引擎 -->
	<Engine/>
</Service>
```

### （3）Executor

```xml
<!--
 默认情况下，Service 并未添加共享线程池配置。
 如果想添加⼀个线程池， 可以在<Service>下添加如下配置：
 name：线程池名称，⽤于 Connector中指定
 namePrefix：所创建的每个线程的名称前缀，⼀个单独的线程名称为 namePrefix+threadNumber
 maxThreads：池中最⼤线程数
 minSpareThreads：活跃线程数，也就是核⼼池线程数，这些线程不会被销毁，会⼀直存在
 maxIdleTime：线程空闲时间，超过该时间后，空闲线程会被销毁，默认值为6000毫秒（1分钟）
 maxQueueSize：在被执⾏前最⼤线程排队数⽬，默认为Int的最⼤值，也就是⼴义的⽆限。除⾮特殊情况，这个值 不需要更改，否则会有请求不会被处理的情况发⽣
 prestartminSpareThreads：启动线程池时是否启动 minSpareThreads部分线程。默认值为false，即不启动
 threadPriority：线程池中线程优先级，默认值为5，值从1到10
 className：线程池实现类，未指定情况下，默认实现类为 org.apache.catalina.core.StandardThreadExecutor，如果想使⽤⾃定义线程池⾸先需要实现 org.apache.catalina.Executor 接⼝
-->
<Executor 
    className="org.apache.catalina.core.StandardThreadExecutor" 
    maxIdleTime="60000" 
    maxQueueSize="Integer.MAX_VALUE" 
    maxThreads="200" 
    minSpareThreads="100" 
    name="commonThreadPool" 
    namePrefix="thread-exec-" 
    prestartminSpareThreads="false" 
    threadPriority="5"
    />
```

### （4）Connector

```xml
<!--
port：端⼝号，Connector ⽤于创建服务端 Socket 并进⾏监听，以等待客户端请求链接，如果该属性设置为0， Tomcat将会随机选择⼀个可⽤的端⼝号给当前 Connector 使⽤

protocol：当前 Connector ⽀持的访问协议。 默认为 HTTP/1.1，并采⽤⾃动切换机制选择⼀个基于 Java NIO 的链接器或者基于本地APR的链接器（根据本地是否含有Tomcat的本地库判定）

connectionTimeOut:Connector 接收链接后的等待超时时间，单位为毫秒，-1 表示不超时

redirectPort：当前 Connector 不⽀持SSL请求，接收到了⼀个请求，并且也符合 security-constraint 约束，需要SSL传输，Catalina ⾃动将请求重定向到指定的端⼝。

executor：指定共享线程池的名称， 也可以通过 maxThreads、minSpareThreads 等属性配置内部线程池

URIEncoding:⽤于指定编码URI的字符编码，Tomcat8.x版本默认的编码为 UTF-8 , Tomcat7.x版本默认为ISO-
8859-1
-->
<!-- org.apache.coyote.http11.Http11NioProtocol，⾮阻塞式 Java NIO 链接器 -->
<Connector port="8080" protocol="HTTP/1.1" connectionTimeout="20000"redirectPort="8443" />
<Connector port="8009" protocol="AJP/1.3" redirectPort="8443" />

<!-- 共享线程池 -->
<Connector 
    URIEncoding="UTF-8" 
    acceptCount="1000" 
    compression="on" 
    compressionMinSize="2048" 
    connectionTimeout="20000" 
    disableUploadTimeout="true" 
    executor="commonThreadPool" 
    maxConnections="1000" 
    maxThreads="1000" 
    minSpareThreads="100" 
    port="8080" 
    protocol="HTTP/1.1" 
    redirectPort="8443"
    />
```

### （5）Engine（表示 Servlet 引擎）

```xml
<!--
name： ⽤于指定Engine 的名称，默认为 Catalina
defaultHost：默认使⽤的虚拟主机名称，当客户端请求指向的主机⽆效时，将交由默认的虚拟主机处理， 默认为 localhost
-->
<Engine defaultHost="localhost" name="Catalina">
    ...
</Engine>
```

### （6）Host

```xml
<!-- ⽤于配置⼀个虚拟主机 -->
<Host name="localhost" appBase="webapps" unpackWARs="true" autoDeploy="true">
    ...
</Host>
```

### （7）Context

```xml
<Host appBase="webapps" autoDeploy="true" name="www.abc.com" unpackWARs="true">
    <!-- ⽤于配置⼀个Web应⽤ -->
    <!-- docBase：Web应⽤⽬录或者War包的部署路径，可以是绝对路径，也可以是相对于 Host appBase 的相对路径 -->
    <!-- path：Web应⽤的Context 路径，如果我们Host名为localhost， 则该web应⽤访问的根路径为： http://localhost:8080/web_demo-->
    <Context docBase="/Users/yingdian/web_demo" path="/web3"/>
    <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs" pattern="%h %l %u %t &quot;%r&quot; %s %b" prefix="localhost_access_log" suffix=".txt"/>
</Host>
```



# 2、Tomcat 架构设计

## 2.0 浏览器访问服务器的流程



## 2.1 Tomcat 是一个 http 服务器

```
- Tomcat 能够接收并且处理 http 请求，所以它是一个 http 服务器

- 浏览器访问服务器使用的是Http协议，Http是应用层协议，用于定义数据通信的格式，具体的数据传输使用的是TCP/IP协议，Http服务器接收到这个请求之后，会调用具体的程序（Java类）进行处理，往往不同的请求由不同的Java类完成处理
```

- 浏览器访问服务器的流程

![image-20210429155727601](image/image-20210429155727601.png)

## 2.2 Tomcat 是一个 Servlet 容器

```
- HTTP 服务器接收到请求之后把请求交给Servlet容器来处理，Servlet 容器通过Servlet接口调用业务类。Servlet接口和Servlet容器这一整套内容叫作Servlet规范
```

- Tomcat Servlet容器处理流程

![image-20210429161026607](image/image-20210429161026607.png)

```
当用户请求某个URL资源时
（1）HTTP服务器会把请求信息使用 ServletRequest 对象封装起来
（2）进一步去调用 Servlet 容器中某个具体的 Servlet
（3）Servlet 容器拿到请求后，根据 URL 和 Servlet 的映射关系，找到相应的 Servlet
（4）如果 Servlet 还没有被加载，就使用反射机制创建这个 Servlet，并调用 Servlet 的 init 方法来完成初始化
（5）接着调用这个具体 Servlet 的 service 方法来处理请求，请求处理结果使用 ServletResponse 对象封装
（6）把 ServletResponse 对象返回给 HTTP 服务器，HTTP 服务器会把响应发送给客户端
```



## 2.3 Tomcat 总体架构

```
两大核心组件：连接器（Connector）和容器（Container）

连接器（Connector）：负责对外交流，处理Socket连接，负责网络字节流与 Request 和 Response 对象的转化
容器（Container）：负责内部处理，加载和管理 Servlet，以及具体处理 Request 请求
```

Tomcat是⼀个由⼀系列可配置（conf/server.xml）的组件构成的Web容器，⽽Catalina是Tomcat的servlet容器，是 Tomcat 的核心 ， 其他模块都是为Catalina 提供⽀撑的。 ⽐如 ： 通过 Coyote 模块提供链接通信，Jasper 模块提供 JSP 引擎，Naming 提供JNDI 服务，Juli 提供⽇志服务。

![image-20210505193118906](image/image-20210505193118906.png)





## 2.4 Tomcat 连接器组件 - Coyote

### （1）**Coyote** 简介

```
Coyote 是Tomcat 中连接器的组件名称 , 是对外的接口，客户端通过Coyote与服务器建⽴连接、发送请求并接受响应

（1）Coyote 封装了底层的⽹络通信（Socket 请求及响应处理）
（2）Coyote 使Catalina 容器（容器组件）与具体的请求协议及IO操作⽅式完全解耦
（3）Coyote 将Socket 输⼊转换封装为 Request 对象，进⼀步封装后交由Catalina 容器进⾏处理，处理请求完成后, Catalina 通过Coyote 提供的Response 对象将结果写⼊输出流
（4）Coyote 负责的是具体协议（应⽤层）和IO（传输层）相关内容
```

![image-20210505151135169](image/image-20210505151135169.png)



### （2）Coyote 支持的 IO 模型

- 传输层 IO模型

| IO模型 | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| BIO    | 同步阻塞I/O（Tomcat 8.0之前默认采用）                        |
| NIO    | 同步非阻塞I/O，采用Java NIO类库实现（默认的IO模型）          |
| NIO2   | 异步I/O，采用 JDK7 最新 NIO2 类库实现                        |
| APR    | 采用Apache 可移植运行库实现，是C/C++编写的本地库（需要单独安装APR库） |



### （3）Coyote 支持的协议

- 应用层协议

| 应用层协议 | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| HTTP/1.1   | 大部分Web应用采用的访问协议（Tomcat默认）                    |
| AJP        | 用于和WX集成以实现对静态资源的优化以及集群部署（当前支持AJP/1.3） |
| HTTP/2.0   | 大幅度提升了Web性能（Tomcat 8.5 和Tomcat 9.0版本之后支持）   |



### （4）Coyote的内部组件及流程

![image-20210505152306592](image/image-20210505152306592.png)

| **组件**        | 作用描述                                                     |
| --------------- | ------------------------------------------------------------ |
| EndPoint        | EndPoint 是 Coyote 通信端点，即通信监听的接⼝，是具体Socket接收和发送处理器，是对传输层的抽象，因此EndPoint⽤来实现TCP/IP协议的 |
| Processor       | Processor 是Coyote 协议处理接⼝ ，如果说EndPoint是⽤来实现TCP/IP协议的，那么Processor⽤来实现HTTP协议，Processor接收来⾃EndPoint的Socket，读取字节流解析成Tomcat Request和Response对象，并通过Adapter将其提交到容器处理，Processor是对应⽤层协议的抽象 |
| ProtocolHandler | Coyote 协议接⼝， 通过Endpoint 和 Processor ， 实现针对具体协议的处理能⼒。Tomcat 按照协议和I/O 提供了6个实现类 ： AjpNioProtocol ，AjpAprProtocol， AjpNio2Protocol ， Http11NioProtocol ，Http11Nio2Protocol ，Http11AprProtocol |
| Adapter         | 由于协议不同，客户端发过来的请求信息也不尽相同，Tomcat定义了⾃⼰的Request类来封装这些请求信息。ProtocolHandler接⼝负责解析请求并⽣成Tomcat Request类。但是这个Request对象不是标准的ServletRequest，不能⽤Tomcat Request作为参数来调⽤容器。Tomcat设计者的解决⽅案是引⼊CoyoteAdapter，这是适配器模式的经典运⽤，连接器调⽤CoyoteAdapter的Sevice⽅法，传⼊的是Tomcat Request对象，CoyoteAdapter负责将Tomcat Request转成ServletRequest，再调⽤容器 |



## 2.5 Tomcat Servlet 容器组件 -  Catalina

### （1）Tomcat/Catalina实例

- 整个Tomcat就是⼀个Catalina实例，Tomcat 启动的时候会初始化这个实例，Catalina实例通过加载server.xml完成其他实例的创建，创建并管理⼀个Server，Server创建并管理多个服务，每个服务又可以有多个Connector和⼀个Container

```
⼀个Catalina实例（容器）
		⼀个 Server实例（容器）
				多个Service实例（容器）
        		每⼀个Service实例下可以有多个Connector实例和⼀个Container实例
```



![image-20210505193346602](image/image-20210505193346602.png)



```
Catalina
- 负责解析 Tomcat 的配置⽂件（server.xml） , 以此来创建服务器 Server 组件并进行管理

Server
- 服务器表示整个 Catalina servlet 容器以及其它组件，负责组装并启动 servlet 引擎,Tomcat 连接器。Server 通过实现 Lifecycle 接口，提供了⼀种优雅的启动和关闭整个系统的⽅式

Service（多个）
- 服务是 Server 内部的组件，⼀个 Server 包含多个 Service。它将若干个 Connector 组件绑定到⼀个 Container

Container（一个）
- 容器，负责处理用户的 servlet 请求，并返回对象给 web 用户的模块
```



### （2）Container 组件结构

```
Engine（一个）
- 表示整个 Catalina 的 Servlet 引擎，⽤来管理多个虚拟站点，⼀个Service最多只能有⼀个Engine，但是⼀个引擎可包含多个Host

Host（多个）
- 代表⼀个虚拟主机，或者说⼀个站点，可以给Tomcat配置多个虚拟主机地址，⽽⼀个虚拟主机下可包含多个Context

Context（多个）
- 表示⼀个Web应⽤程序， ⼀个Web应⽤可包含多个Wrapper

Wrapper（多个）
- 表示⼀个Servlet，Wrapper 作为容器中的最底层，不能包含⼦容器

上述组件的配置其实就体现在conf/server.xml中。
```



![image-20210505193816464](image/image-20210505193816464.png)



# 3、Tomcat 迷你版实现



# 4、Tomcat 源码分析

## 4.1 下载源码

地址：https://tomcat.apache.org/

![image-20210510154933813](image/image-20210510154933813.png)

## 4.2 导入IDEA步骤

### （1）解压 tar.gz 压缩包

```
- 得到目录 apache-tomcat-8.5.50-src
```

### （2）创建 **source**文件夹（名字自定义）

```
- 在 apache-tomcat-8.5.50-src 根目录录中创建 source 文件夹
- 将 conf、webapps 目录移动到刚刚创建 source 文件夹
```

### （3）创建 pom.xml 文件（根目录）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
http://maven.apache.org/xsd/maven-4.0.0.xsd">
    
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.apache.tomcat</groupId>
    <artifactId>apache-tomcat-8.5.50-src</artifactId>
    <name>Tomcat8.5</name>
    <version>8.5</version>
    
    <build>
        <!-- 指定源目录 -->
        <finalName>Tomcat8.5</finalName>
        <sourceDirectory>java</sourceDirectory>
        
        <resources>
            <resource>
                <directory>java</directory>
            </resource>
        </resources>
        
        <plugins>
            <!--引入编译插件-->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.1</version>
                
                <configuration>
                    <encoding>UTF-8</encoding>
                    <source>11</source>
                    <target>11</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
    
    <!-- tomcat 依赖的基础包 -->
    <dependencies>
        <dependency>
            <groupId>org.easymock</groupId>
            <artifactId>easymock</artifactId>
            <version>3.4</version>
        </dependency>
        
        <dependency>
            <groupId>ant</groupId>
            <artifactId>ant</artifactId>
            <version>1.7.0</version>
        </dependency>
        
        <dependency>
            <groupId>wsdl4j</groupId>
            <artifactId>wsdl4j</artifactId>
            <version>1.6.2</version>
        </dependency>
        
        <dependency>
            <groupId>javax.xml</groupId>
            <artifactId>jaxrpc</artifactId>
            <version>1.1</version>
        </dependency>
        
        <dependency>
            <groupId>org.eclipse.jdt.core.compiler</groupId>
            <artifactId>ecj</artifactId>
            <version>4.5.1</version>
        </dependency>
        
        <dependency>
            <groupId>javax.xml.soap</groupId>
            <artifactId>javax.xml.soap-api</artifactId>
            <version>1.4.0</version>
        </dependency>
    </dependencies>
</project>
```

### （4）使用 IDEA 打开项目

### （5）启动 Bootstrap.java 类的 main 函数

```
文件路径：java/org/apache/catalina/startup/Bootstrap.java
```

### （4）配置VM选项，加入source的配置

```properties
-Dcatalina.home=D:\SourceCode-TD\apache-tomcat-8.5.50-src\source
-Dcatalina.base=D:\SourceCode-TD\apache-tomcat-8.5.50-src\source
-Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager
-Djava.util.logging.config.file=D:\SourceCode-TD\apache-tomcat-8.5.50-src\source\conf\logging.properties
```

![image-20210510160357681](image/image-20210510160357681.png)

### （5）初始化 Jsp 引擎

- org/apache/catalina/startup/ContextConfig.java
- 解决访问 http://localhost:8080/ 报错：org.apache.jasper.JasperException: Unable to compile class for JSP

```java
// 初始化jsp解析引擎-jasper
context.addServletContainerInitializer(new JasperInitializer(), null);
```



### 问题

#### （1）报错：程序包 sun.rmi.registry 已在模块 java.rmi 中声明, 但该模块未将它导出到未命名模块

```
解决方案：根据idea提示修复即可
```



## 4.3 



# 5、Tomcat 类加载机制



# 6、Tomcat 性能优化

##### 优化思路 1：核心组件

##### 优化思路 2：非核心组件 

##### 优化思路 3：web.xml 

##### 优化思路 4：JVM层面



##### 优化思路 5：启动速度优化

```xml
- 删除没用的web应用

- 关闭websocket

- 随机数优化

- 多线程启动web应用
<Host startStopThreads="0"> 
</Host>
```



##### 优化思路 6：其他方面

- Connector 配置压缩属性compression=“500”，文件大于500bytes才会压缩
- 数据库优化 减少对数据库访问等待的时间，缓存方案考虑一下
- 开启浏览器缓存、nginx静态资源部署等 开启浏览器缓存，cdn静态资源服务器，nginx
- too many open files 关掉无用的句柄或者增加句柄数:ulimit -n 10000







https://blog.csdn.net/qq_41517071/article/details/82181003