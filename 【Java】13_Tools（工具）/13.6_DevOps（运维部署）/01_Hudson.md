> 当前位置：【Java】13_Tools（工具）-> 13.6_DevOps（运维部署）-> 01_Hudson



## 1、Hudson - 简介

- Hudson是Jenkins的前身

- 是基于Java开发的一种持续集成工具

- 用于监控程序重复的工作

## 2、Hudson - 功能

- 持续的软件版本发布/测试项目

- 监控外部调用执行的工作

## 3、Hudson - 特性

- 易于安装-只要把hudson.war部署到servlet容器，不需要数据库支持

- 易于配置-所有配置都是通过其提供的web界面实现

- 集成RSS/E-mail/IM-通过RSS发布构建结果或当构建失败时通过e-mail实时通知

- 生成JUnit/TestNG测试报告

- 分布式构建支持-Hudson能够让多台计算机一起构建/测试

- 文件识别- Hudson能够跟踪哪次构建生成哪些jar，哪次构建使用哪个版本的jar等

- 插件支持-Hudson可以通过插件扩展，你可以开发适合自己团队使用的工具