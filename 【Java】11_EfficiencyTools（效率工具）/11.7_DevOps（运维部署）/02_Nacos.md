> 当前位置：【Java】12_EfficiencyTools（效率工具） -> 12.7_DevOps（运维部署） -> 02_Nacos安装和配置



# 0、Nacos 下载

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

## 2.1 单机模式

### 步骤1：Nacos 安装

```shell
# 安装目录
/usr/local/nacos

# 上传 /usr/local/upload/ 文件夹

# 解压
cd /usr/local/upload/
tar -xzvf /usr/local/upload/nacos-server-1.4.0.tar.gz
mv /usr/local/upload/nacos /usr/local/
cd /usr/local/
```



### 步骤2：数据库脚本执行

```shell
新建本地数据库 Nacos，执行 conf/nacos-mysql.sql 文件
```



### 步骤3：Nacos 配置

- 修改 Nacos 下的 conf/application.properties 文件

```shell
### If use MySQL as datasource:
spring.datasource.platform=mysql

### Count of DB:
db.num=1

### Connect URL of DB:
db.url.0=jdbc:mysql://192.168.31.130:3306/nacos?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true&useUnicode=true&useSSL=false&serverTimezone=UTC
db.user=td
db.password=td
```

- 修改 startup.sh 文件

```bash
vim /usr/local/nacos/bin/startup.sh

# 把集群模式修改为单机模式
# export MODE="cluster"
export MODE="standalone"
```



### 步骤4：Nacos 启动

```shell
# 切换目录
cd /usr/local/nacos/bin/

# 启动方式1：单机模式（根据 startup.sh 文件中的 export MODE 的值进行启动）
./startup.sh -m standalone &

# 启动方式2：单机模式（忽略输入并把输出追加到"nohup.out"）
nohup sh startup.sh -m standalone &
```



### 步骤5：Nacos 访问

- 地址：http://192.168.31.130:8848/nacos/#/login
- 用户名：nacos

- 密码：nacos



## 2.2 集群模式

### 步骤1：Nacos 安装

```shell
# 安装目录

```



### 步骤2：数据库脚本执行

```shell
新建本地数据库 Nacos，执行 conf/nacos-mysql.sql 文件
```



### 步骤3：Nacos 配置

- 修改 Nacos 下的 conf/application.properties 文件

```properties
### Default web server port:
# 根据集群分别设置为 8851、8852、8853
server.port=8851

### Specify local server's IP:
nacos.inetutils.ip-address=127.0.0.1

### If use MySQL as datasource:
spring.datasource.platform=mysql

### Count of DB:
db.num=1

### Connect URL of DB:
db.url.0=jdbc:mysql://192.168.31.130:3306/nacos?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true&useUnicode=true&useSSL=false&serverTimezone=UTC
db.user=td
db.password=td
```

- 修改 Nacos 下的 conf/cluster.conf 文件

```properties
# 集群配置
127.0.0.1:8851
127.0.0.1:8852
127.0.0.1:8853
```

- 修改 startup.cmd 文件

```bash
vim /usr/local/nacos/bin/startup.sh

# 把单机模式修改为集群模式
#export MODE="standalone"
export MODE="cluster"
```



### 步骤4：Nacos 启动

```shell
# 切换目录

# 启动
sh startup.sh -m cluster
```



### 步骤5：Nacos 访问

- 地址
- 用户名：nacos
- 密码：nacos



# 3、Win系统 -  Nacos 安装和配置

## 3.1 单机模式

### 步骤1：Nacos 安装

```shell
# 安装目录
E:\06_study\nacos-server-1.4.0
```



### 步骤2：数据库脚本执行

```shell
新建本地数据库 Nacos，执行 conf/nacos-mysql.sql 文件
```



### 步骤3：Nacos 配置

- 修改 Nacos 下的 conf/application.properties 文件

```shell
### If use MySQL as datasource:
spring.datasource.platform=mysql

### Count of DB:
db.num=1

### Connect URL of DB:
db.url.0=jdbc:mysql://localhost:3306/nacos?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true&useUnicode=true&useSSL=false&serverTimezone=UTC
db.user=root
db.password=root
```

- 修改 startup.cmd 文件

```bash
# 把集群模式修改为单机模式 
# export MODE="cluster"
export MODE="standalone"
```



### 步骤4：Nacos 启动

```shell
# 运行文件
E:\06_study\nacos-server-1.4.0\bin\startup.cmd
```



### 步骤5：Nacos 访问

- 地址：http://localhost:8848/nacos/#/login

- 用户名：nacos

- 密码：nacos



## 3.2 集群模式

### 步骤1：Nacos 安装

```shell
# 安装目录
E:\06_DevSoft\nacos-server-1.4.0-8851
E:\06_DevSoft\nacos-server-1.4.0-8852
E:\06_DevSoft\nacos-server-1.4.0-8853
```



### 步骤2：数据库脚本执行

```shell
新建本地数据库 Nacos，执行 conf/nacos-mysql.sql 文件
```



### 步骤3：Nacos 配置

- 修改 Nacos 下的 conf/application.properties 文件

```properties
### Default web server port:
# 根据集群分别设置为 8851、8852、8853
server.port=8851

### Specify local server's IP:
nacos.inetutils.ip-address=127.0.0.1

### If use MySQL as datasource:
spring.datasource.platform=mysql

### Count of DB:
db.num=1

### Connect URL of DB:
db.url.0=jdbc:mysql://localhost:3306/nacos?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true&useUnicode=true&useSSL=false&serverTimezone=UTC
db.user=root
db.password=root
```

- 修改 Nacos 下的 conf/cluster.conf 文件

```properties
# 集群配置（本机ip地址:端口号）
192.168.31.197:8851
192.168.31.197:8852
192.168.31.197:8853
```

- 修改 startup.cmd 文件

```bash
# 把单机模式修改为集群模式
#set MODE="standalone"
s MODE="cluster"
```



### 步骤4：Nacos 启动

```shell
# 运行文件
E:\06_DevSoft\nacos-server-1.4.0-8851\bin\startup.cmd
E:\06_DevSoft\nacos-server-1.4.0-8852\bin\startup.cmd
E:\06_DevSoft\nacos-server-1.4.0-8853\bin\startup.cmd
```



### 步骤5：Nacos 访问

- 地址
  - http://localhost:8851/nacos/#/login
  - http://localhost:8852/nacos/#/login
  - http://localhost:8853/nacos/#/login

- 用户名：nacos
- 密码：nacos



# 4、Mac系统 -  Nacos 安装和配置

