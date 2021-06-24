> 当前位置：【Java】12_EfficiencyTools（效率工具） -> 12.7_DevOps（运维部署） -> 02_Nacos安装和配置



# 0、Nacos 的下载

- GitHub：https://github.com/alibaba/nacos/releases
- 控制台操作文档：https://nacos.io/zh-cn/docs/console-guide.html



# 1、Docker -  Nacos 安装和配置

```shell
# 获取镜像
docker pull nacos/nacos-server:1.4.2

# 创建配置文件和日志文件目录
mkdir -p /xxxx/nacos/init.d
mkdir -p /xxxx/nacos/logs
mkdir -p /xxxx/nacos/data
cd /xxxx/nacos/init.d
touch custom.properties

# 在 custom.properties 文件中填写配置
management.endpoints.web.exposure.include=*

# 创建并启动容器（单机模式）
docker run -itd \
-p 8848:8848 \
-e MODE=standalone \
-e SPRING_DATASOURCE_PLATFORM=mysql \
-e MYSQL_SERVICE_HOST=172.17.0.2 \
-e MYSQL_SERVICE_PORT=3306 \
-e MYSQL_SERVICE_USER=root \
-e MYSQL_SERVICE_PASSWORD=admin \
-e MYSQL_SERVICE_DB_NAME=nacos \
-v /Users/td/Documents/03_DevTools/docker_data/nacos/init.d/custom.properties:/home/nacos/init.d/custom.properties \
-v /Users/td/Documents/03_DevTools/docker_data/nacos/logs:/home/nacos/logs \
-v /Users/td/Documents/03_DevTools/docker_data/nacos/data:/home/nacos/data \
--restart always \
--name nacos \
nacos/nacos-server:1.4.2

```

http://localhost:8848/nacos/#/login



# 2、Linux系统 -  Nacos 安装和配置

## 2.1 Nacos 基本信息

```shell
- 安装目录：/usr/local/nacos
```



## 2.2 Nacos 安装和配置

- 安装

```shell
# 上传 /usr/local/upload/ 文件夹

# 解压
cd /usr/local/upload/
tar -xzvf /usr/local/upload/nacos-server-1.4.0.tar.gz
mv /usr/local/upload/nacos /usr/local/
cd /usr/local/
```



- 配置

```shell
# 步骤1：修改 Nacos 下的 conf/application.properties 文件
vim /usr/local/nacos/conf/application.properties

### If use MySQL as datasource:
spring.datasource.platform=mysql

### Count of DB:
db.num=1

### Connect URL of DB:
db.url.0=jdbc:mysql://192.168.31.130:3306/nacos?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true&useUnicode=true&useSSL=false&serverTimezone=UTC
db.user=td
db.password=td
```



- 数据库脚本执行

```shell
新建本地数据库 Nacos，执行 conf/nacos-mysql.sql 文件
```



## 2.3 Nacos 启动

```shell
# 切换目录
cd /usr/local/nacos/bin/

# 启动方式1：单机模式（根据 startup.sh 文件中的 export MODE 的值进行启动）
./startup.sh -m standalone &

# 启动方式2：单机模式（忽略输入并把输出追加到"nohup.out"）
nohup sh startup.sh -m standalone &


# 可以修改 startup.sh 文件，把集群模式 export MODE="cluster" 修改为单机模式 export MODE="standalone"
vim /usr/local/nacos/bin/startup.sh
```



## 2.4 Nacos 访问

- 地址：http://192.168.31.130:8848/nacos/#/login

- 用户名：nacos

- 密码：nacos



# 3、Win系统 -  Nacos 安装和配置

## 3.1 Nacos 基本信息

```shell
- 安装目录：E:\06_study\nacos-server-1.4.0
```



## 3.2 Nacos 配置

```shell
# 步骤1：修改 Nacos 下的 conf/application.properties 文件
### If use MySQL as datasource:
spring.datasource.platform=mysql

### Count of DB:
db.num=1

### Connect URL of DB:
db.url.0=jdbc:mysql://192.168.31.130:3306/nacos?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true&useUnicode=true&useSSL=false&serverTimezone=UTC
db.user=td
db.password=td

# 可以修改 startup.cmd 文件，把集群模式 export MODE="cluster" 修改为单机模式 export MODE="standalone"
```

- 数据库脚本执行

```shell
新建本地数据库 Nacos，执行 conf/nacos-mysql.sql 文件
```



## 3.3 Nacos 启动

```shell
- 运行文件 E:\06_study\nacos-server-1.4.0\bin\startup.cmd
```



## 3.4 Nacos 访问

- 地址：http://localhost:8848/nacos/#/login

- 用户名：nacos

- 密码：nacos



# 4、Mac系统 -  Nacos 安装和配置