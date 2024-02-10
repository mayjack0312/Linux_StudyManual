## linux 配置 IP 地址的方法

1.  ifconfig 命令临时配置 IP 地址
2.  setup 工具永久配置 IP 地址（rethad 系列专有）
3.  修改网络配置文件
4.  图形界面配置 IP 地址

```bash
# ifconfig命令 查看与配置网络状态命令
ifconfig eth0 192.168.0.200 netmask 255.255.255.0
# 临时设置eth0网卡的IP地址与子网掩码
```

```bash
setup
service network restart
# 重启网络服务
```

```bash
vim /etc/sysconfig/network-scripts/ifcfg-eth0
# 网卡信息文件
```

| 网卡信息文件                              |                                             |
| ----------------------------------------- | ------------------------------------------- |
| DEVICE=eth0                               | 网卡设备名                                  |
| TYPE=Ethernet                             | 类型为以太网                                |
| UUID=28c74564-7cd8-48e5-9203-90f903a8f92e | 唯一识别码                                  |
| ONBOOT=yes                                | 是否随网络服务启动，eth0 生效               |
| NM_CONTROLLED=yes                         | 是否可以由 Network Manager 图形管理工具托管 |
| BOOTPROTO=dhcp                            | 是否自动获取 IP（none，static，dhcp）       |
| HWADDR=00:0c:29:2f:2d:d3                  | MAC 地址                                    |
| DEFROUTE=yes                              |                                             |
| PEERROUTES=yes                            |                                             |
| IPV4_FAILURE_FATAL=yes                    |                                             |
| IPV6INIT=no                               | IPv6 没有启动                               |
| NAME="System eth0"                        |                                             |
| USERCTL=no                                | 不允许非 root 用户控制此网卡                |
| IPADDR=192.168.0.252                      | IP 地址                                     |
| NETMASK=255.255.255.0                     | 子网掩码                                    |
| GATEWAY=192.168.0.1                       | 网关                                        |
| DNS1=202.106.0.20                         | DNS                                         |

```bash
vim /etc/sysconfig/network
# 主机名文件
hostname
# 查看主机名
```

```bash
vim /etc/resolv.conf
# DNS配置文件
hostname
# 查看主机名
```

1.  配置 linuxIP 地址

```bash
setup
```

2.  启动网卡

```bash
vim /etc/sysconfig/network-scripts/ifcfg-eth0
# 把
ONBOOT=no
# 改为
ONBOOT=yes
service network restart
# 重启网络服务
```

3.  修改 UUID

```bash
vim /etc/sysconfig/network-scripts/ifcfg-eth0
# 删除MAC地址行
rm -rf /etc/udev/rules.d/70-persistent-net.rules
# 删除网卡和MAC地址绑定文件
shutdown -r
# 重启动系统
```

4.  设置虚拟机网络连接方式

```bash
> 桥接
> NAT
> Host-only
```

5.  修改桥接网卡
