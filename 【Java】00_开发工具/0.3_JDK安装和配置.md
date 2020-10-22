> 当前位置：【Java】00_开发工具  -> 0.3_JDK安装和配置



### 1、Win系统 -  JDK安装和配置





### 2、Linux系统 -  JDK安装和配置





### 3、Mac系统 -  JDK安装和配置

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

