> 当前位置：【Java】07_性能优化  -> 03_Tomcat 优化



### 1、Tomcat简介



### 2、Tomcat下载



### 3、Tomcat 架构设计



### 4、Tomcat源码分析



### 5、Tomcat性能优化

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

