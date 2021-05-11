>当前位置：【Java】12_EfficiencyTools（效率工具） -> 12.1_DevTools（开发工具） ->  01_IDEA安装和配置

[toc]

- 本文截图为IDEA版本为2020.3，使用了官方中文插件



# 1、通用设置

### 设置Project面板展示内容

```xml
- 位置：Settings -> Editor -> File Types
- 添加内容：.idea;*.iml;target;.settings;.classpath;.project;.out;
```

![image-20210114095937658](image/001.png)



### 启动idea时，不自动打开上次的项目

![image-20210114100357376](image/002.png)



### 线的设置

![image-20210114102429849](image/003.png)

 

### 自动编译

```xml
- 步骤1：Settings -> Build -> Compile -> 勾选 Build project automatically
```

![image-20210114102743921](image/004.png)



```xml
- 步骤2：Ctrl + Shift + Alt + / -> 选择Registry -> 勾选compiler.automake.allow.when.app.running
```

![image-20210114102945461](image/005.png)



![image-20210114103036928](image/006.png)



### 智能导包

```xml
- 位置：Settings -> editor -> general -> auto import ->java相关

- 操作步骤：
  - insert imports on paste选择all
  - 勾选add UNambiguous imports on the fly
  - 勾选optimize imports on the fly
```

![image-20210114103208842](image/image-20210114103208842.png)



### 取消import合并成*

```xml
- 位置：Settings -> Editor -> Code Style -> java - > Imports
- 操作：调大统计使用'*'导入的类个数
```

![image-20210114103842439](image/image-20210114103842439.png)



### 悬浮提示开关

```xml
- 位置：Settings -> Editor -> general -> other相关
- 操作：勾选show quick documentation on mouse move
```

![image-20210114105114687](image/image-20210114105114687.png)



### 取消单行显示Tabs的操作

```xml
- 位置：Settings -> editor -> general -> editor tabs -> appearance相关
- 操作：取消勾选show tabs in one row
```

![image-20210114104858894](image/image-20210114104858894.png)



### 项目文件编码

```xml
- 位置：Settings -> editor -> file encodings

- 操作：
project encoding -> 选择utf-8
properties files相关 -> default enconding for properties files选择utf-8、勾选transparent native-to-ascii conversion
```

![image-20210114105405925](image/image-20210114105405925.png)



### 滚轴修改字体大小

```xml
- 位置：Settings -> editor -> general -> mouse相关
- 操作：勾选change font size（zoom）with ctrl+mouse wheel
```

![image-20210114105447082](image/image-20210114105447082.png)



### 修改注释的位置（不在行开头）

```xml
- 位置：Settings -> Editor -> Code Style -> Java -> Code generation -> Comment Code
- 操作：去掉勾选Line comment at first column
```

![image-20210114105653381](image/image-20210114105653381.png)



### 修改部分代码样式不折叠

```java
- 位置：Settings -> Editor -> General -> Code Folding
```

![image-20210114110033912](image/image-20210114110033912.png)



### 智能提示时忽略大小写（如string提示String）

```xml
- 位置：Settings -> Editor -> General -> Code Completion -> Case sensitive completion 
```

![image-20210114110224366](image/image-20210114110224366.png)



# 2、创建项目

### 2.1 创建动态Web项目



### 2.2 创建Maven项目
#### 创建类型1：创建maven父工程

- 步骤1：选择jdk、跳过骨架选择，直接下一步

  ![](image/010.png)

- 步骤2：填写父工程信息

  ![](image/011.png)

- 步骤3：填写项目信息

  ![1564558434134](image/012.png)

- 步骤4：创建完成后，父工程项目结构如下

  ![1564558462214](image/013.png)

  

#### 创建类型2：创建maven子工程（Java项目）

- 步骤1：在父工程项目名上右键选择 New -> module...

- 步骤2：填写子工程名，直接下一步

  ![1564558520876](image/014.png)

- 步骤3：填写子工程模块名，点击完成

  ![1564558549661](image/015.png)

  

#### 创建类型3：创建maven子工程（JavaWeb项目）

- 步骤1：选择jdk、选择骨架webapp，下一步

  ![1564558582855](image/016.png)

- 步骤2：填写子工程名，直接下一步

  ![1564558819859](image/017.png)

- 步骤3：设置maven环境（可直接下一步）

  ![1564558851504](image/018.png)

- 步骤4：填写子工程模块名，点击完成

  ![1564558876892](image/019.png)



# 3、配置项目

### 3.1 传统项目 - 添加jar包



### 3.2 Maven项目 - 添加依赖

#### （1）修改Maven repository配置文件

- 步骤1：配置本地仓库位置

```xml
<localRepository>此处为自定义Maven仓库路径</localRepository>
```
- 步骤2：配置阿里云仓库镜像

``` xml
<!-- 阿里云仓库镜像 -->
<mirror>
    <id>nexus-aliyun</id>
    <mirrorOf>*</mirrorOf>
    <name>Nexus aliyun</name>
    <url>http://maven.aliyun.com/nexus/content/groups/public</url>
</mirror>
```


#### （2）Maven创建web项目时，自定义web.xml的模板内容

- 步骤1：访问目录

```java
Maven3.5.2\repository\org\apache\maven\archetypes\maven-archetype-webapp\1.4
```

- 步骤2：右键用解压软件打开maven-archetype-webapp-1.4.jar

- 步骤3：访问解压软件打开的jar包目录

```java
maven-archetype-webapp-1.4.jar\archetype-resources\src\main\webapp\WEB-INF\web.xml
```

- 步骤4：修改web.xml文件模板

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app version="3.0" xmlns="http://java.sun.com/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee     http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd">
    <display-name>Archetype Created Web Application</display-name>

    <!-- 欢迎页面配置 -->
    <welcome-file-list>
        <welcome-file>index.jsp</welcome-file>
        <welcome-file>index.html</welcome-file>
        <welcome-file>index.htm</welcome-file>
        <welcome-file>default.html</welcome-file>
        <welcome-file>default.htm</welcome-file>
        <welcome-file>default.jsp</welcome-file>
    </welcome-file-list>

</web-app>
```



# 4、运行项目

### 4.1 使用Tomcat启动项目

-Dfile.encoding=UTF-8



### 4.2 使用Maven插件启动项目



# 5、导入项目

### 5.1 从 Maven 中导入项目



### 5.2 从 eclipse 中导入项目



# 6、内置工具的使用

### 6.1 Database的使用

- 位置：侧边栏

   ![1564561703200](image/020.png)

- 重构表名（在边栏展开的表名上使用快捷键，然后mapper的xml文件中的sql语句也会自动重构）
  Mac：FN + Shift + F6
  Win：Shift + F6

- 重构列名（在边栏展开的列名上使用快捷键，然后mapper的xml文件中的sql语句也会自动重构）
  Mac：FN + Shift + F6
  Win：Shift + F6



### 6.2 Maven的使用（待补充。。。）

- 



# 7、提升编码效率

### 7.1 Live Templates （动态模板）

- 位置：Settings -> Editor -> Live Templates



### 7.2 File and Code Template（文件和代码模板）

- 位置：Settings -> Editor -> File and Code Template



### 7.3 Postfix Completion

- 位置：Settings -> Editor -> General -> Postfix Completion
- 常用功能

```java
- for循环
- sout输出语句
- field生成“声明成员变量”的代码
- return（先写返回值，在写r就能自动写好）
- nn（xxx.nn可以写出xxx非空的判断语句）
	if (xxx != null) {
	
	}
```



# 8、翻译、生成API文档

```java
步骤1：创建项目
步骤2：在JDK安装目录下，找到 src.zip并解压
步骤3：只留下 "java"、"javax"、"org" 目录，其余目录干扰 Java 源码编译，且用不到，删除
步骤4：把"java"、"javax"、"org" 目录复制到项目中，然后build项目
步骤5：生成API文档（网页形式）
    - 位置：Tools工具栏 -> Generate JavaDoc
    - 配置界面：-encoding UTF-8 -charset UTF-8 -windowtitle "test"
```



  ![1564562101492](image/021.png)

 - 参数说明
```
Whole project（整个项目都生成）

Custom scope（自定义范围）
             project files 项目文件
             project production files 项目产品文件
             project test files 项目的测试文件
             未知范围
             class hierarchy 类层
             
include test source 包含测试目录

include JDK and … 包含jdk和其他的第三方jar

link to JDK documentation…链接到JDK api

output directy 生成的文档存放的位置

private、package、protected、public 生成文档的级别（类和方法）

右边的Generate…是选择生成的文档包含的内容，层级树、导航、索引..

再右边是生成的文档包含的内容信息，作者版本等信息

Locale 语言类型,zh-CN

Other command line arguments 其他参数

Maximum heep… 最大堆栈
```



# 9、插件

### Chinese (Simplified) Language Pack

```
- idea官方中文汉化包
- 需要2020.1版本以上才能在插件库中搜到
```



![简单演示 功能远不止于此](image/6b0879cc869a45b4b5565f370c88741a~tplv-k3u1fbpfcp-zoom-1.image)



### .ignore

```
- 快速生成git的忽略文件
```



### Grep Console

```

```



### Lombok Plugin

- 支持lombok的各种注解，从此不用写getter setter方法
- 可以把注解还原为原本的java代码



### Maven Helper

- 一键查看maven依赖，查看冲突的依赖，一键进行exclude依赖
- 一旦安装了Maven Helper插件，只要打开pom文件，就可以打开该pom文件的Dependency Analyzer视图（在文件打开之后，文件下面会多出这样一个tab），进入Dependency Analyzer视图之后有三个查看选项，支持搜索。
  - Conflicts(冲突)
  - All Dependencies as List(列表形式查看所有依赖)
  - All Dependencies as Tree(树结构查看所有依赖)



### Alibaba Java Coding Guidelines

- 阿里巴巴出品的java代码规范插件
- 可以扫描整个项目，找到不规范的地方，并且大部分可以自动修复



### FindBugs-IDEA

- 代码检测bug（一般是低级错误）



### GsonFormat

- 一键根据json文本生成java类
- 快捷键：alt+s或者cmd+n



### VisualVM Launcher

- 运行java程序的时候启动visualvm，方便查看jvm的情况 比如堆内存大小的分配

- 某个对象占用了多大的内存，jvm调优必备工具

- 安装完成后，在原来的Run和Debug按纽旁会多出两个按纽，点击后会出现选择VisualVM路径，选择本地JDK安装目录下的bin目录中的jvisualvm即可

  

### Easy-Translation

- 翻译插件
- 选中词语，然后alt+a



### activate-power-mode

- 发光特效



# 10、快捷键

### 10.1 界面操作

- ==打开界面侧边栏（只有带数字的才可以用）==

  - 快捷键：Ctrl + 1/2/3

     ![1564621550834](image/022.png)

- ==Ctrl + 1：Project（项目文件浏览）==

- ==Ctrl + 2：Favorite==

  - bookmarks（书签）：只在本项目有效

    - 订一个书签（F11）

       ![1564563795764](image/023.png)

    - 订一个带有属性的书签（Ctrl + F11）

       ![1564563839531](image/024.png)

    - 切换带有属性的书签（Ctrl + 1/2/3/4）

  - breakpoint（断点）

- ==Alt + 7：Structure（类结构）==

  - 查看当前field、method大纲（Ctrl + F12）
  
- ==Alt + 8：hierarchy（层次结构）==

  - 在某一方法上查看方法调用层次（Ctrl + Alt + H）
  
- ==diagram：查看类结构图、类与类之间关系图、Maven依赖包关系图==

  - 查看类结构图、类与类之间关系图：点击要生成的类文件（Ctrl + Alt + Shift + U）

    - 在类关系图中显示该类的父类（Ctrl + Alt + P）

    - 在类关系图中显示具有继承关系的子类（Ctrl + Alt + B）

  - 查看Maven依赖包关系图：点击要生成的pom.xml文件（Ctrl + Alt + Shift + U）



### 10.2 项目操作

- ==项目之间的跳转==：Ctrl + Alt + [ ]（左括号或右括号）



### 10.3 文件操作

- ==Ctrl + Shift + C==：拷贝的是文件的绝对路径/物理路径

- ==Ctrl + Alt + Shift + C==

  - 对于类文件：拷贝的是类的全限定名
  - 对于其他文件：拷贝的是文件的相对路径/虚拟路径

- ==剪切板功能==： Ctrl + Shitf + V（用哪个就敲数字几）

- ==最近文件列表==

  - 打开最近编辑的文件列表（仅限本项目中的文件）：Ctrl + Shift + E

  - 打开最近打开的文件列表（包括其他项目中的文件）：Ctrl + E

- ==文件之间的跳转==

  - 跳转到上次编辑的位置：Ctrl + Shift + Backspace
  - 位置：Navigate -> Last Edit Location
  - 跳转到下次编辑的位置：（没有默认指定，自定义）
    - 位置：Navigate -> Next Edit Location
  - 跳转/退回到浏览的位置：Ctrl + Alt + ←/→
  - 位置：Navigate -> back/forward

- ==标签页之间的跳转==：Ctrl + Tab

- ==编辑区和文件区之间的跳转==

  - 从右边的编辑区跳转到左边的文件区：Alt + 1
  - 从左边的文件区跳转到右边的编辑区：ESC
  
- ==在当前文件同级目录下新建一个文件==：Ctrl + N



### 10.4 代码操作

- ==注释==

  - （添加/删除）单行注释：Ctrl + /
  - （添加）多行注释：Ctrl + Shift + /
  - （删除）多行注释：Ctrl + Shift + \

- ==代码折叠和展开==

  - 方法折叠：Ctrl + 加号
  - 方法展开：Ctrl + 减号
  - 全部代码折叠：Ctrl + Shift + 加号
  - 全部代码折叠：Ctrl + Shift + 减号

- ==代码行操作==

  - 移动到上一行：Alt + Shift  + 向上箭头
  - 移动到下一行：Alt + Shift  + 向下箭头
  - 复制当前行：Ctrl + D
  - 删除当前行：Ctrl + X

- ==找到某个方法的具体实现== 

  - 方式1：Ctrl + Alt + 左键
  - 方式2：Ctrl + Alt + B

- ==大小写字母转换==：Ctrl + Shift + U

  - 位置：Edit -> Toggle Case

- ==字符操作==

  - Shift + →（选择要改变的字符或字符串）
  - Ctrl + Shift + →（选择要改变的单词）

- ==代码格式化==：Ctrl + Alt + L

  - 代码格式化配置界面：Ctrl + Alt + Shift + L

  - 配置界面如下：

     ![1564639070908](image/028.png)

    - Scope（格式化代码的作用范围）
      - Only VCS changed text（只有代码管理仓库检测到改变的代码才会格式化）
      - Selected text（选中的代码才会格式化）
      - Whole file（整个文件都会格式化）
    - Optional（可选项）
      - Optimize imports（最优化导入方式）
      - Rearrange code（最新整理代码）



### 10.5 搜索功能

- ==搜索某个文件（仅限本项目中）==：Ctrl + Shift + N

  - 位置：Navigate -> Files

  - 补充：勾选后，可以找到本项目中的文件和jar包中的文件

    ![1564627994533](image/025.png)

- ==搜索某个符号（仅限本项目中）==：Ctrl + Alt + Shift + N

  - 位置：Navigate -> Symbol

  - 补充：勾选后，可以找到本项目中的符号和jar包中的符号

    ![1564636950922](image/026.png)

- ==搜索某个字符串==：Ctrl + Shift + F

  - 位置：Edit -> Find -> Find in Path

  - 精确搜索条件

    ![1564637066748](image/027.png)



### 10.6 Debug功能

- ==添加/取消当前行断点==：Ctrl + F8

- ==单步调试==（进入函数内部）：F7 

  - 选择要进入的函数：Shift+F7
  
- ==单步调试==（不进入函数内部）：F8

  - 跳出函数：Shift+F8

- ==运行到断点==：Alt+F9

- ==进入下一个断点或执行完程序==：F9 

- ==查看所有断点（在非断点行按快捷键）==：Ctrl+Shift+F8

- ==条件断点（在断点行按快捷键）==： Ctrl + Shift +  F8

- ==执行表达式并查看结果 （evaluate expression）==：Alt + F8

- ==禁止所有断点==（断点都会变成白色）

   ![1564641827124](image/030.png)

- ==setvalue==：动态改变当前的值（在断点调试的窗口上按F2）

   ![1564641699419](image/029.png)



### 10.7 重构操作

- ==重构变量名/方法名/文件名==： Shift + F6



### 10.8 抽取操作

- 位置：Refactor -> Extract -> Variable/Constant/Field/Method/Parameter
- ==抽取变量==： Ctrl + Alt + V
- ==抽取静态变量==： Ctrl + Alt + C
- ==抽取成员变量==： Ctrl + Alt + F
- ==抽取函数/方法==： Ctrl + Alt + M
- ==抽取函数/方法==： Ctrl + Alt + P



### 10.9 Alt + Enter 的作用

- 自动创建函数
- list replace（选择最优代码，比如for循环用哪种for最简洁）
- 字符串format（转成c语言的那种，例如%c）
- 字符串builder（转成字符串拼接.append这种）
- 实现接口的实现类（在接口名上按下快捷键，会提示创建实现类）
- 单词拼写
- 导包
- 在方法上添加参数（先在方法上添加一个新的参数，然后快捷键修复）



### 10.10 自定义快捷键

- ==代码提示/自动补全==：Alt+/

  - 步骤1：Preferences -> KeyMap

  - 步骤2：移除原来的Cycle Expand Word 的 Alt+/ 快捷键绑定

    ![1564642534922](image/031.png)

  - 步骤3：在 Basic 上点击右键，去除原来的 Ctrl+空格绑定，然后添加 Alt+/ 快捷键

    ![1564642623671](image/032.png)

- ==关闭窗口==：Ctrl + W

- ==关闭项目==：Ctrl + Alt + Q

- ==进入全屏==：Alt+\




# 11、代码片段

### integer转String：integer

```
Integer.toString($var$)
```



### String转integer：string

```
Integer.parseInt($String$);
```



### 创建HashMap：newmap

```
Map<String, String> map = new HashMap<>();
```



### 创建ArrayList：newlist

```
List<Map<String, String>> list = new ArrayList<>();
```



### 打印异常信息：logger

```
logger.error("$message$异常: " + Arrays.toString(e.getStackTrace()), e);
```



### 去掉字符串的最后一个匹配的字符串：substring

```
$var1$.substring(0, $var1$.lastIndexOf("$var2$")); 
```



### 判断字符串不为空：ifstring

```
if ($var1$ != null && $var1$.length() != 0) {

}
```



# 12、问题报错

### 12.1 This file is indented with tabs instead of 4 spaces

*   分析原因：根据阿里巴巴Java开发手册，不能使用Tab字符，改成4个字符
*   解决方案：Setting -> Editor -> Code Style -> Java -> Tabs and Indents -> 勾选 Use tab character
![1564643091599](image/033.png)



### 12.2 解决Language Level版本问题

- 解决方案：maven项目的父工程的pom.xml里添加如下代码（这里设置编译版本为1.8）

```xml
     <properties>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
     </properties> 
```



### 12.3 SQL dialect is not configured

*   分析原因：Idea能自动给我们检查拼接的sql语句的语法正确性
*   解决方案：Setting -> Languages & Frameworks -> SQL Dialects -> 选择MySQL

     ![1564643173502](image/034.png)



### 12.4 JUnit无法从控制台读取 System.in

*   解决方案：help -> Edit Custom VM option打开配置文件，在最后一行添加如下命令
```xml
-Deditable.java.test.console=true
```





> 参考资料

https://juejin.cn/post/6960478730300948494



