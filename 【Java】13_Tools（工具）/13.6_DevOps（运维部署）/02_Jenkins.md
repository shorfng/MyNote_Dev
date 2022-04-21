> 当前位置：【Java】13_Tools（工具）-> 13.6_DevOps（运维部署）-> 02_Jenkins

# Jenkins 安装和配置

- 下载
  - https://jenkins.io/zh/download/
- 安装前提

  - 机器要求

    - 256 MB 内存，建议大于 512 MB

    - 10 GB 的硬盘空间（用于 Jenkins 和 Docker 镜像）

  - 软件要求

    - Java 8 ( JRE 或者 JDK 都可以)

    - Docker
- 安装

  - 打开终端进入到下载目录
  - 运行命令 java -jar jenkins.war --httpPort=8080
  - 打开浏览器进入链接 [http://localhost:8080](http://localhost:8080/)
  - 按照说明完成安装

# 第一章 Jenkins 简介

## 1、Jenkins - 概述

### 1.1 概述

- Jenkins 是一款开源 CI&CD 软件，用于自动化各种任务，包括构建、测试和部署软件

- Jenkins 支持各种运行方式，可通过系统包、Docker 或者通过一个独立的 Java 程序



## 2、Jenkins - 配置界面

### 2.1 Jenkins的左侧 -> Manage Jenkins 

### 2.2 配置系统（Configure System）

### 2.3 配置全局安全（Configure Global Security）

#### （1）启用安全（Enable security）：默认勾选

- 用户可以使用用户名和密码登录， 以执行匿名用户无法执行的操作

- 哪些操作需要用户登录取决于所选择的授权策略和它的配置

- 默认情况下匿名用户没有权限，已登录用户完全控制

- 对于任何非本地（测试）Jenkins环境，该复选框应该勾选



#### （2）访问控制（Access Control）：是保护Jenkins环境免受未经授权使用的主要机制

- Security Realm（安全域）

```bash
# 告诉Jenkins环境如何以及从何处获取用户（或身份）信息，也称为 "认证"

# Delegate to servlet container
- 对于委托认证运行Jenkins主机的servlet容器, 比如 Jetty
- 如果使用该选项, 请参考servlet 容器的 身份验证文档

# Jenkins’ own user database
- 使用Jenkins自己内置的用户数据存储来进行身份验证，而不是委托给外部系统
- 这是Jenkins 2.0或后来安装的Jenkins默认启用的，适用于小环境

# LDAP
- 把所有的身份认证委托给配置的LDAP 服务器， 包括用户和组
- 对于已经配置了外部身份提供者比如LDAP的组织的大型安装，该选项更为常见，也支持活动目录安装

# Unix user/group database
- 将身份验证委托给Jenkins主机上的底层Unix OS-级别的用户数据库
- 该模式允许重用Unix组进行授权
- 比如, Jenkins 能够配置为 "在 `developers`组中的所有人都有管理员访问权限" 来支持该特性，Jenkins 依赖于可能需要在Jenkins环境外配置的 PAM
```

- Authorization（授权）

```bash
# 告诉 Jenkins 环境， 哪些用户和/或组可以访问Jenkins的哪些方面。 以及何种程度

# Anyone can do anything
- 每个人都能完全控制Jenkins, 包括没有登陆的匿名用户
- 除了在本地测试Jenkins主机外，不要使用此设置

# Legacy mode
- 与Jenkins <1.164的行为完全相同
- 也就是说, 如果一个用户拥有 "admin" 角色, 就会被授予对系统的完全控制, 负责 (包括匿名用户) 只会拥有读访问权限。 
- 除了在本地测试Jenkins主机外，不要使用此设置

# Logged in users can do anything
- 在该模式下, 每个登陆的用户对Jenkins完全控制
- 根据一个高级选项, 匿名用户获取Jenkins的访问权限, 或者根本无法访问
- 该模式有助于强制用户在操作前进行登录, 以便于对用户的行为进行审计跟踪

# Matrix-based security（安全矩阵）
- 该授权方案对允许用户和组在Jenkins环境下能够进行哪些操作进行细粒度控制![img](https://api2.mubu.com/v3/document_image/6acc3cc5-401a-4295-b6ba-9d011d717b31-780133.jpg)

# Project-based Matrix Authorization Strategy（项目矩阵授权策略）
- 此授权方案是基于矩阵的安全性的扩展， 它允许为在项目配置屏幕中的 *each project*分别定义额外的访问控制列表 (ACL)
- 它允许特定的用户和组访问特定的项目, 而不是Jenkins 环境中的所有项目
- 基于项目的矩阵授权定义的ACL是附加的，在配置全局安全屏幕中定义的访问授权将与 指定项目的ACL相结合
```



#### （3）标记格式化程序（Markup Formatter）

- Jenkins允许用户输入大量不同的配置字段和文本域，这些字段和文本域会导致用户, 无心或恶意的, 输入不安全的HTML 和/或 JavaScript

- 默认情况下，Markup Formatter 配置将被设置为 Plain Text ，以避免诸如 < 和 & 对其各自的字段实体的不安全字符

- 使用 Safe HTML 标记格式化程序允许用户和管理员向项目描述和其他地方注入有用的和信息的HTML 片段



#### （4）代理（Agents）

- 使用TCP 端口通过JNLP协议与启用的代理通信

- JNLP TCP 端口：默认禁用

  - Random

    - JNLP 端口是随机选择的，来避免在 Jenkins 主机上繁盛冲突

    - 缺点是他们是在Jenkins主机的引导下选择的，这使得管理允许JNLP通信的防火墙规则变得困难

  - Fixed

    - JNLP端口由Jenkins管理员选择的，并且在Jenkins主机的重新引导下是一致的

    - 这使得管理基于JNLP代理连接到主服务器的防火墙规则变得容易



#### （5）跨站请求伪造（CSRF Protection）

- 当启用该选项时, Jenkins 会检查 在Jenkins环境中可能更改数据的任何请求的CSRF 令牌, 或 "crumb"

- 它包含对远程API的任何表单提交和调用，包含使用 "Basic"身份验证的表单



#### （6）代理/主机访问控制（Agent → Master Security）

- 允许Jenkins管理员在Jenkins主机和连接代理之间添加更细粒度的访问控制定义



### 2.4 配置全局工具（Global Tool Configuration）

- Maven

- JDK

- Git

- Gradle

- SonarQube Scanner for MSBuild

- SonarQube Scanner

- Ant

- Docker

### 2.5 配置插件（Manage Plugins）

- 安装插件

  - 方式1：在web UI使用 "插件管理器"

  - 方式2：使用Jenkins CLI install-plugin 命令

- 更新插件

- 删除插件

  - 卸载插件

  - 禁用插件

### 2.6 Jenkins CLI

### 2.7 Manage Users（管理用户）

## 3、Jenkins - 插件（Pipeline 流水线）
