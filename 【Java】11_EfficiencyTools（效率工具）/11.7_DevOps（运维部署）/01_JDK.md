> 当前位置：【Java】11_EfficiencyTools（效率工具） -> 11.7_DevOps（运维部署） ->  01_JDK安装和配置



# 0、JDK的下载

- Oracle官方网站：http://www.oracle.com
- Oracle官方网站中文页面：http://www.oracle.com/cn/index.html



# 1、Docker - JDK安装和配置

- 拉取镜像

```shell
docker pull openjdk:8-alpine3.9 
```

- 备份镜像

```shell
cd /docker_data/
docker save openjdk:8-alpine3.9 -o jdk8.tar 
```

- 导入镜像

```shell
docker load -i jdk8.tar
```



# 2、Linux系统 -  JDK安装和配置

### 2.1 使用上传安装包形式

```bash
# 查看当前Linux系统是否已经安装Java
rpm -qa | grep java

# 卸载两个openJD
rpm -e --nodeps java-1.6.0-openjdk-1.6.0.0-1.66.1.13.0.el6.x86_64rpm -e --nodeps java-1.7.0-openjdk-1.7.0.45-2.4.3.3.el6.x86_64

# 使用 FTP 工具上传JDK到Linux目录：/root/td_upload

# 切换到upload目录下
cd /root/

# 解压JDK到/usr/local目录下
tar -zxvf jdk-11.0.13_linux-x64_bin.tar.gz
tar -zxvf Linux_JDK_8u171_x64.tar.gz -C /usr/local/

# 配置JDK环境变量
vi /etc/profile

# 将配置拷贝到最后一行
# set java environment
export JAVA_HOME=/usr/local/jdk-11.0.13
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export PATH=$PATH:$JAVA_HOME/bin

export JAVA_HOME=/usr/local/jdk1.8.0_171
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export PATH=$PATH:$JAVA_HOME/bin

# 退出vim
:wq

# 使配置生效
source /etc/profile

# 验证JDK是否安装成功
java -version
```



### 2.2 使用yum安装JDK

```bash
yum -y list java*
yum -y install java-1.7.0-openjdk*

# 默认jdk安装路径：/usr/lib/jvm

# 配置环境变量
vi /etc/profile

# 配置
export JAVA_HOME=/usr/lib/jvm/java-1.7.0
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export PATH=$PATH:$JAVA_HOME/bin

# 使配置生效
source /etc/profile
```



# 3、Win系统 -  JDK安装和配置

## 步骤0：安装须知

- 开发工具最好安装目录统一
- 安装路径不要有中文或者特殊符号如空格等
- 当提示安装JRE时，可以选择不安装，建议还是安装上
- 安装路径中没有的文件夹,会自动创建
- JDK无需每次都安装，因为其本身就是绿色版本，可以直接存入U盘，在任何计算机上都可以直接使用
- 采用安装的方式使用JDK的好处在于其会在注册表中被注册，当JDK出现新版本，会自动更新



## 步骤1：配置 path 环境变量

- 配置目的
  - 为了能在DOS命令行窗口中，在任何目录下都能够执行Java的bin目录下javac命令
  - 需要将javac.exe命令文件所在目录的路径放入path环境变量中
  - path是记录所有在dos命令行中可直接运行的.exe文件的目录
  
- 原理
  - 在DOS命令提示符窗口中输入某个命令后，Windows系统会首先在当前目录下查找是否存在该命令文件可以执行
  - 如果没有，Windows系统就会在path环境变量路径中查找
  - 如果查找到，就会执行该命令，如果还没有找到，那么就会提示错误信息
  
- 操作步骤
  - 步骤1：计算机 -> 右键属性 -> 高级系统设置 -> 高级 -> 环境变量 -> 系统变量
  - 步骤2：创建新的变量名称：JAVA_HOME
  - 步骤3：为JAVA_HOME添加变量值：xxx（xxx为JDK安装根目录）
  - 步骤4：在path环境变量最前面添加如下内容：%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;
  - 步骤5：DOS下输入 java -version 后显示一串文字，则表示配置成功



## 步骤2：配置 classpath 环境变量

- 配置目的
  - 由于可能频繁执行多个class文件，并且多个class文件可能存储在不同的目录下，那么每次都在命令提示符窗口中切换目录会相当的麻烦
  - classpath环境变量的作用类似于path环境变量，但是它的作用在于告诉JVM去哪里找到class文件
  - classpath存储的是.class字节码文件的目录，是Java中的类路径
  
- JVM查找类文件的顺序
  - 如果没有配置classpath环境变量，JVM只在当前目录下查找要运行的类文件
  - 如果配置了classpath环境，JVM会先在classpath环境变量值的目录中查找要运行的类文件
  
- 操作步骤
  - 步骤1：计算机 -> 右键属性 -> 高级系统设置 -> 高级 -> 环境变量 -> 系统变量
  - 步骤2：创建新的变量名称：CLASSPATH
  - 步骤3：为CLASSPATH添加变量值：.;xxx（xxx为JDK安装根目录）
  
  

## 步骤3：配置临时环境变量：略



## 步骤4：验证是否安装成功

- 在DOS窗口中输入：JDK安装路径\bin\java.exe
- 在DOS窗口中输入：JDK安装路径\bin\javac.exe
- 如果正常显示一些内容，说明安装成功



# 4、Mac系统 -  JDK安装和配置

- 查看JDK安装路径

```sh
# 命令
/usr/libexec/java_home -V

# 找到JDK安装路径
/Library/Java/JavaVirtualMachines/jdk1.8.0_231.jdk/Contents/Home
```

- 配置环境变量

```sh
#（1）新建隐藏的.bash_profile配置文件
touch .bash_profile

#（2）打开配置文件
open -e .bash_profile

#（3）输入环境变量内容
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_231.jdk/Contents/Home
export PATH=$PATH:$JAVA_HOME/bin:.
export CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:.

#（4）使配置文件生效
source .bash_profile

#（5）验证环境配置是否成功（显示jdk路径即配置已生效）
echo $JAVA_HOME

#（6）查看JDK版本
java -version
```

