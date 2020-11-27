> 当前位置：【Java】05_JavaWeb开源框架  -> HuTool（工具类库）



# 0、HuTool 简介

## （1）模块简介

| 模块               | 介绍                                                         |
| ------------------ | ------------------------------------------------------------ |
| hutool-aop         | JDK动态代理封装，提供非IOC下的切面支持                       |
| hutool-bloomFilter | 布隆过滤，提供一些Hash算法的布隆过滤                         |
| hutool-cache       | 简单缓存实现                                                 |
| hutool-core        | 核心，包括Bean操作、日期、各种Util等                         |
| hutool-cron        | 定时任务模块，提供类Crontab表达式的定时任务                  |
| hutool-crypto      | 加密解密模块，提供对称、非对称和摘要算法封装                 |
| hutool-db          | JDBC封装后的数据操作，基于ActiveRecord思想                   |
| hutool-dfa         | 基于DFA模型的多关键字查找                                    |
| hutool-extra       | 扩展模块，对第三方封装（模板引擎、邮件、Servlet、二维码、Emoji、FTP、分词等） |
| hutool-http        | 基于HttpUrlConnection的Http客户端封装                        |
| hutool-log         | 自动识别日志实现的日志门面                                   |
| hutool-script      | 脚本执行封装，例如Javascript                                 |
| hutool-setting     | 功能更强大的Setting配置文件和Properties封装                  |
| hutool-system      | 系统参数调用封装（JVM信息等）                                |
| hutool-json        | JSON实现                                                     |
| hutool-captcha     | 图片验证码实现                                               |
| hutool-poi         | 针对POI中Excel和Word的封装                                   |
| hutool-socket      | 基于Java的NIO和AIO的Socket封装                               |



## （2）引用方式

### Maven
- 在项目的 pom.xml 的 dependencies 中加入以下内容

```xml
<dependency>
    <groupId>cn.hutool</groupId>
    <artifactId>hutool-all</artifactId>
    <version>5.5.1</version>
</dependency>
```

### Gradle
```shell
compile 'cn.hutool:hutool-all:5.5.1'
```



# 1、hutool-aop

# 2、hutool-bloomFilter

# 3、hutool-cache

# 4、hutool-core

# 5、hutool-cron 

# 6、hutool-crypto

# 7、hutool-db  

# 8、hutool-dfa

# 9、hutool-extra

# 10、hutool-http

# 11、hutool-log 

# 12、hutool-script

# 13、hutool-setting 

# 14、hutool-system

# 15、hutool-json 

# 16、hutool-captcha（图片验证码实现）

### （1）cn.hutool.captcha

| 文件名和路径                                         | 功能                           |
| ---------------------------------------------------- | ------------------------------ |
| src/main/java/cn/hutool/captcha/AbstractCaptcha.java | 验证码的抽象实现类             |
| src/main/java/cn/hutool/captcha/CaptchaUtil.java     | 图形验证码工具（创建方法）     |
| src/main/java/cn/hutool/captcha/CircleCaptcha.java   | 圆圈干扰验证码（具体实现方法） |
| src/main/java/cn/hutool/captcha/ICaptcha.java        | 验证码对象接口定义             |
| src/main/java/cn/hutool/captcha/LineCaptcha.java     | 干扰线验证码（具体实现方法）   |
| src/main/java/cn/hutool/captcha/ShearCaptcha.java    | 扭曲干扰验证码（具体实现方法） |

### （2）cn.hutool.captcha.generator

| 文件名和路径                                                 | 功能                 |
| ------------------------------------------------------------ | -------------------- |
| src/main/java/cn/hutool/captcha/generator/AbstractGenerator.java | 随机字符验证码生成器 |
| src/main/java/cn/hutool/captcha/generator/CodeGenerator.java | 随机文字验证码生成器 |
| src/main/java/cn/hutool/captcha/generator/MathGenerator.java | 数字计算验证码生成器 |
| src/main/java/cn/hutool/captcha/generator/RandomGenerator.java | 随机字符验证码生成器 |

### （3）测试类
| 文件名和路径                                     | 功能           |
| ------------------------------------------------ | -------------- |
| src/test/java/cn/hutool/captcha/CaptchaTest.java | 验证码单元测试 |



# 17、hutool-poi

# 18、hutool-socket



