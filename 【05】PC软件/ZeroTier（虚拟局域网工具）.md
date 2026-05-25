> 当前位置：【05】PC软件 -> ZeroTier（虚拟局域网工具）



# 1、ZeroTier 简介

- ZeroTier 是一个能让全球任意设备（电脑、手机、服务器、虚拟机）安全地组成一个虚拟局域网（VLAN）的工具。简单说，就是把你家、公司、云端的设备，全部拉到同一个 “虚拟房间” 里，直接互相访问，就像在同一个路由器下

- **新用户（2025.12 后注册）**：**最多 10 台设备**，无限网络。

  **老用户（legacy 账户）**：**最多 25 台设备**，无限网络。

  同一设备加入多个网络，**只算 1 台**。



# 2、ZeroTier 安装

- 官网：https://central.zerotier.com/
- Win系统

```bash
直接下载安装即可
```

- CentOS系统

```bash
sudo yum install -y curl
curl -s https://install.zerotier.com | sudo bash
```



# 3、ZeroTier 使用

- 目前配置：电脑1（Win系统）、电脑2（Win系统的Linux虚拟机）

## （1）创建网络

- 浏览器打开 ZeroTier 官网注册登录，**Create a Network**

- 得到一串 **16 位网络 ID**（比如：`abc123456789abcd`）

## （2）加入组网

- Windows 直接在任务栏 ZeroTier 右键 → Join Network 输入网络 ID（比如：`abc123456789abcd`）

- Linux

```bash
sudo zerotier-cli join abc123456789abcd
```

## （3）设备入网授权

- 官网后台同意设备入网，打勾授权

![image-20260515173918122](D:\DevCode\MyCode\MyNote_Dev\【05】PC软件\ZeroTier（虚拟局域网工具）.assets\image-20260515173918122.png)

## （4）访问

- 访问其中一方的ip地址：上图中的ZT IP

- 端口号：22

## （5）IP 跳转（管理员 PowerShell 执行，电脑A设置）

```bash
# 添加静态路由
# 把 192.168.126.200/32 网段的所有流量，都通过 10.170.146.19 转发
- `-p`：永久路由，重启后依然生效
- `mask 255.255.255.255`：仅针对单个 IP 生效
- `metric 1`：优先级设为最高
route -p add 192.168.126.200 mask 255.255.255.255 10.170.146.19 metric 1

# 验证路由是否生效
# 看输出里有没有 `192.168.126.200` 指向 `10.170.146.19` 的路由条目
route print

# 删除路由（不需要时）
route delete 192.168.126.200
```

- 优点：一次性配置，所有端口都自动转发，不需要逐个配置
- 缺点：需要确保你的网络环境支持路由转发，且目标 IP 可达

# 4、问题

## （1）容器没有用 `host` 网络模式，而是用了默认的 `bridge` 网络，导致 ZeroTier 流量无法正常转发

### 步骤1：找到你的 ZeroTier 网卡名

```bash
# 输出里会有类似 ztxxxxxx 的网卡，就是你的 ZeroTier 网卡
ip addr

# 得到 ZeroTier 网卡名：ztdiy6sne2
```

### 步骤2：放行 ZeroTier 网卡的所有 Docker 流量（不改动现有容器）

```bash
# 永久保存规则（CentOS/RHEL 系统）
yum install -y iptables-services
systemctl enable iptables
service iptables save

# 执行后，ZeroTier 网络就能直接访问所有 bridge 模式的 Docker 容器，不用改任何容器配置。
```

