> 当前位置：【Java】12_EfficiencyTools（效率工具） -> 12.2_BuildTools（项目构建工具）  -> 02_Gradle安装和配置



# 0、Gradle 的下载

https://services.gradle.org/distributions/



# 1、Win系统 -  Gradle安装和配置





# 2、Linux系统 -  Gradle安装和配置





# 3、Mac系统 -  Gradle安装和配置

### （1）在终端打开 .bash_profile 文件

```bash
open -e .bash_profile
```

### （2）配置环境变量并保存

```bash
GRADLE_HOME=/Users/td/Documents/03_DevTools/gradle-6.6-rc-1
export GRADLE_HOME
export PATH=$PATH:$GRADLE_HOME/bin
```

### （3）刷新配置

```bash
source .bash_profile
```

### （4）验证配置是否成功

```css
gradle -v
```

出现以下界面表示成功

```bash
Welcome to Gradle 6.6-rc-1!

Here are the highlights of this release:
 - Experimental build configuration caching
 - Java compilation supports --release flag
 - Built-in conventions for handling credentials

For more details see https://docs.gradle.org/6.6-rc-1/release-notes.html


------------------------------------------------------------
Gradle 6.6-rc-1
------------------------------------------------------------

Build time:   2020-07-13 13:53:25 UTC
Revision:     1ed79f4fbe18d90df8cb759235804f95a99b30a2

Kotlin:       1.3.72
Groovy:       2.5.12
Ant:          Apache Ant(TM) version 1.10.8 compiled on May 10 2020
JVM:          1.8.0_231 (Oracle Corporation 25.231-b11)
OS:           Mac OS X 10.15.5 x86_64
```



# 4、Gradle 下载的依赖jar包

- Mac系统默认下载路径：/Users/(用户名)/.gradle/caches/modules-2/files-2.1
- Win系统默认下载路径：C:\Users(用户名).gradle\caches\modules-2\files-2.1



修改Gradle的缓存路径修改的四种方法

https://blog.csdn.net/github_38616039/article/details/79933133?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase