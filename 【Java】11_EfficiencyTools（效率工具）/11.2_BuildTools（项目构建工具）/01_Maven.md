> 当前位置：【Java】11_EfficiencyTools（效率工具） -> 11.2_BuildTools（项目构建工具） -> 01_Maven安装和配置



# Maven 下载安装和配置

## 0、Maven 下载

- Maven 官网：https://maven.apache.org

  

## 1、Docker - Maven 安装和配置



## 2、Linux 系统 - Maven 安装和配置

### 步骤1：下载

- 地址：https://maven.apache.org/download.cgi



### 步骤2：配置环境变量

```bash
# 解压
cd /usr/local/
tar -zxvf apache-maven-3.8.4-bin.tar.gz

vi /etc/profile
export MAVEN_HOME=/usr/local/apache-maven-3.8.4
export PATH=$PATH:$MAVEN_HOME/bin

source /etc/profile

mvn -v
```





## 3、Win系统 -  Maven 安装和配置



## 4、Mac系统 -  Maven 安装和配置

- 修改本地仓库默认路径
- 





那国内可以用的 Maven 的镜像地址其实有很多，比如说

阿里云
https://maven.aliyun.com/mvn/guide


网易：
https://mirrors.163.com/.help/maven.html

腾讯云：
https://mirrors.cloud.tencent.com/help/maven.html