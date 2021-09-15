# RuoYi（权限后台管理系统）

- 基于SpringBoot、Shiro、Mybatis的权限后台管理系统



# 1、简介

## 地址合集

- RuoYi 官网地址：[http://ruoyi.vip](http://ruoyi.vip/)
- RuoYi 在线文档：[http://doc.ruoyi.vip](http://doc.ruoyi.vip/)
- RuoYi 源码下载：https://gitee.com/y_project/RuoYi
- RuoYi GitHub源码下载：[https://github.com/yangzongzhuan/RuoYi](https://github.com/yangzongzhuan/RuoYi)
- RuoYi 在线提问：https://gitee.com/y_project/RuoYi/issues
- RuoYi 博客：https://www.oschina.net/p/ruoyi



## 在线体验	

- 项目地址：
  - [http://demo.ruoyi.vip/login](http://demo.ruoyi.vip/login)
  - [http://vue.ruoyi.vip/login](http://vue.ruoyi.vip/login) （RuoYi-Vue前端分离版）

- 账号密码：admin/admin123



## 项目地址

- SpringBoot + Spring + MyBatis + Shiro + MySQL
  - https://gitee.com/y_project/RuoYi

- Spring Boot + Spring Cloud & Alibaba + Nacos + Redis + Sentinel + Seata + MySQL
  - https://gitee.com/y_project/RuoYi-Cloud

- SpringBoot + Spring + MyBatis + Shiro + Oracle
  - https://github.com/yangzongzhuan/RuoYi-Oracle

- Spring Boot + Spring Cloud & Alibaba + Nacos + Redis + Sentinel + Seata + Oracle
  - https://github.com/yangzongzhuan/RuoYi-Cloud-Oracle



## 技术选型

```java
// 2021.08.04 

1、系统环境
Java EE 8
Servlet 3.0
Apache Maven 3

2、主框架
Spring Boot 2.2.x
Spring Framework 5.2.x
Apache Shiro 1.7

3、持久层
Apache MyBatis 3.5.x
Hibernate Validation 6.0.x
Alibaba Druid 1.2.x

4、视图层
Bootstrap 3.3.7
Thymeleaf 3.0.x
```



## 内置功能模块

```
- 用户管理：用户是系统操作者，该功能主要完成系统用户配置。
- 部门管理：配置系统组织机构（公司、部门、小组），树结构展现支持数据权限。
- 岗位管理：配置系统用户所属担任职务。
- 菜单管理：配置系统菜单，操作权限，按钮权限标识等。
- 角色管理：角色菜单权限分配、设置角色按机构进行数据范围权限划分。
- 字典管理：对系统中经常使用的一些较为固定的数据进行维护。
- 参数管理：对系统动态配置常用参数。
- 通知公告：系统通知公告信息发布维护。
- 操作日志：系统正常操作日志记录和查询；系统异常信息日志记录和查询。
- 登录日志：系统登录日志记录查询包含登录异常。
- 在线用户：当前系统中活跃用户状态监控。
- 定时任务：在线（添加、修改、删除)任务调度包含执行结果日志。
- 代码生成：前后端代码的生成（java、html、xml、sql)支持CRUD下载 。
- 系统接口：根据业务代码自动生成相关的api接口文档。
- 服务监控：监视当前系统CPU、内存、磁盘、堆栈等相关信息。
- 在线构建器：拖动表单元素生成相应的HTML代码。
- 连接池监视：监视当期系统数据库连接池状态，可进行分析SQL找出系统性能瓶颈。
```



## 主要特性

```
- 完全响应式布局（支持电脑、平板、手机等所有主流设备）
- 强大的一键生成功能（包括控制器、模型、视图、菜单等）
- 支持多数据源，简单配置即可实现切换。
- 支持按钮及数据权限，可自定义部门数据权限。
- 对常用js插件进行二次封装，使js代码变得简洁，更加易维护
- 完善的XSS防范及脚本过滤，彻底杜绝XSS攻击
- Maven多项目依赖，模块及插件分项目，尽量松耦合，方便模块升级、增减模块。
- 国际化支持，服务端及客户端支持
- 完善的日志记录体系简单注解即可实现
```



# 2、运行部署

## 运行环境

```java
JDK >= 1.8 (推荐1.8版本)
Mysql >= 5.5.0 (推荐5.7版本)
Maven >= 3.0
```



## 启动项目

- 下载项目源代码，导入编译器
- 创建数据库 ry 并导入数据脚本 ry_2021xxxx.sql，quartz.sql
- 运行com.ruoyi.RuoYiApplication.java
- 打开浏览器，输入：http://localhost:80 （默认账户 admin/admin123）

```java
- 建议使用Git克隆，因为克隆的方式可以和RuoYi随时保持更新同步。使用Git命令克隆
git clone https://gitee.com/y_project/RuoYi.git
```



## 部署项目



# 3、项目介绍





# 4、后台手册



# 5、前台手册

## 前端组件

| 名称     | 代码        | 介绍             |
| -------- | ----------- | ---------------- |
| 表格     | $.table     | 表格封装处理     |
| 表格树   | $.treeTable | 表格树封装处理   |
| 表单     | $.form      | 表单封装处理     |
| 弹出层   | $.modal     | 弹出层封装处理   |
| 操作     | $.operate   | 操作封装处理     |
| 校验     | $.validate  | 校验封装处理     |
| 树插件   | $.tree      | 树插件封装处理   |
| 通用方法 | $.common    | 通用方法封装处理 |



## 通用方法

| 通用方法 | $.common | 通用方法封装处理 |
| -------- | -------- | ---------------- |
|          |          |                  |





# 6、组件文档