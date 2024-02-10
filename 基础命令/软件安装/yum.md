## yum 源文件

```bash
cd /etc/yum.repos.d/
ls
# 输出CentOS-Base.repo  CentOS-Debuginfo.repo  CentOS-Media.repo  CentOS-Vault.repo  gitlab_gitlab-ee.repo
vi /etc/yum.repos.d/CentOS-Base.repo
```

### 选项

| 选项       | 备注                                                                                                                |
| ---------- | ------------------------------------------------------------------------------------------------------------------- |
| [base]     | 容器名称，一定要放在[]中                                                                                            |
| name       | 容器说明，可以自己随便写                                                                                            |
| mirrorlist | 镜像站点，这个可以注释掉                                                                                            |
| baseurl    | 我们的 yum 源服务器的地址。默认是 CentOS 官方的 yum 源服务器，是可以使用的，如果你觉得慢可以改成你喜欢的 yum 源地址 |
| endabled   | 此容器是否生效，如果不写或写成 enable=1 都是生效，写成 enable=0 就是不生效                                          |
| gpgcheck   | 如果是 1 是指 RPM 的数字证书生效，如果是 0 则不生效                                                                 |
| gpgkey     | 数字证书的公钥文件保存位置，不用修改                                                                                |

## 光盘 yum 源搭建

1.  挂载光盘

```bash
mkdir /mnt/cdrom
# 建立挂载点
mount /dev/cdrom /mnt/cdrom/
# 挂载光盘
```

2.  使网络 yum 源失效

```bash
cd /etc/yum.repos.d/
# 进入yum源目录
mv CentOS-Base.repo CentOS-Base.repo.bak
# 修改yum源文件后缀名，使其失效
```

3.  使 yum 源生效

```bash
cd /etc/yum.repos.d/
ls
# 输出CentOS-Base.repo  CentOS-Debuginfo.repo  CentOS-Media.repo  CentOS-Vault.repo  gitlab_gitlab-ee.repo
vi /etc/yum.repos.d/CentOS-Media.repo
# 修改文件CentOS-Media.repo
baseurl=file:///mnt/cdrom # 地址为你自己的光盘挂载地址
#       file:///media/cdrom/
#       file:///media/cdrecorder/ # 注释这两个不存在的地址
enabled=1 # 把enabled=0改为enabled=1，把这个yum源文件生效
```

3.  验证 yum 源生效与否

```bash
yum list
```

## 常用 yum 命令

1.  查询

```bash
yum list
# 查询所有可用软件包列表
yum search 关键字
# 搜索服务器上所有和关键字相关的包
```

e.g.

```bash
yum search httpd
```

2.  安装

```bash
yum -y install 包名
```

### 选项

| 选项    | 备注         |
| ------- | ------------ |
| install | 安装         |
| -y      | 自动回答 yes |

e.g.

```bash
yum -y install httpd-devel
```

e.g.

```bash
yum -y install gcc
# 安装编译器
```

3.  升级

```bash
yum -y update 包名
```

| 选项   | 备注         |
| ------ | ------------ |
| update | 升级         |
| -y     | 自动回答 yes |

4.  卸载

- 服务器使用最小化安装，用什么软件安装什么，尽量不卸载

```bash
yum -y remove 包名
```

| 选项   | 备注         |
| ------ | ------------ |
| remove | 卸载         |
| -y     | 自动回答 yes |

## yum 软件组管理命令

```bash
yum grouplist
# 列出所有可用的软件组列表
yum groupinstall 软件组名
# 安装指定软件组，组名可以由grouplist查询出来
yum groupremove 软件组名
# 卸载指定软件组
```
