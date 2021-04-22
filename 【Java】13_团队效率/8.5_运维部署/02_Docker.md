

# 1、CentOS下安装安装



```shell
# mirror Aliyun
curl -fsSL https://get.docker.com | bash -s docker 
```

启动并加入开机启动

```
sudo systemctl start docker
sudo systemctl enable docker
```

验证安装是否成功(有client和service两部分表示docker安装启动都成功了)

```
$ docker version
```







# Docker和k8s的区别与介绍

https://www.cnblogs.com/misswangxing/p/10669444.html