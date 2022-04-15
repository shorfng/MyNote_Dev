> 当前位置：【Java】13_Tools（工具）-> 13.3_VcsTools（源码管理工具） -> 02_SVN



##  Linux下使用SVN创建新项目

### 步骤0：前置条件

```bash
svn 数据目录：/svn/svndata
```



```bash
# 1、创建仓库的命令
svn_td svnadmin create /svn/svndata/svn_td

# 2、进入到新的项目的conf目录下
cd /svn/svndata/svn_td/conf

# 3、修改 passwd 文件
vi passwd

[users]
# harry = harryssecret
# sally = sallyssecret
要添加的用户名 = 对应的密码 

# 4、修改 authz 文件
vi authz

# 添加项目权限配置，添加到最后
[svn_td:/]
td = rw 

# 5、修改svnserve.conf 文件
vi svnserve.conf

anon-access = none
auth-access = write
password-db = passwd
authz-db = authz 

# 6、停止svn
killall svnserve

# 7、启动svn项目
svnserve -d -r /svn/svndata/

8、测试是否创建成功
svn co svn://47.96.11.3/svn_td

9、创建目录
mkdir trunk
mkdir branches
mkdir tags
```

