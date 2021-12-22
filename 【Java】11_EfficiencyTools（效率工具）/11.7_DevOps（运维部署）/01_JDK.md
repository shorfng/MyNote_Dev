> 当前位置：【Java】12_EfficiencyTools（效率工具） -> 12.7_DevOps（运维部署） ->  01_JDK安装和配置



# 第一章 JDK 下载安装和配置

## 0、JDK的下载



## 1、Docker - JDK安装和配置

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



## 2、Win系统 -  JDK安装和配置





## 3、Linux系统 -  JDK安装和配置

### 3.1 使用上传安装包形式

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



### 3.2 使用yum安装JDK

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



## 4、Mac系统 -  JDK安装和配置

- 查看JDK安装路径

```sh
命令：
/usr/libexec/java_home -V

找到JDK安装路径：
/Library/Java/JavaVirtualMachines/jdk1.8.0_231.jdk/Contents/Home
```

- 配置环境变量

```sh
（1）新建隐藏的.bash_profile配置文件
touch .bash_profile

（2）打开配置文件
open -e .bash_profile

（3）输入环境变量内容
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_231.jdk/Contents/Home
export PATH=$PATH:$JAVA_HOME/bin:.
export CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:.

（4）使配置文件生效
source .bash_profile

（5）验证环境配置是否成功（显示jdk路径即配置已生效）
echo $JAVA_HOME

（6）查看JDK版本
java -version
```

