# Linux是什么

Linux是一种免费、开源的操作系统，由林纳斯·托瓦兹在1991年创建。Linux基于Unix操作系统，采用了分层的设计思想，支持多用户、多任务、多线程的操作，并具有良好的稳定性和安全性。Linux具有高度的可定制性，用户可以根据自己的需要自由地配置和修改系统。Linux广泛用于服务器、桌面电脑、移动设备等领域。

# Ubuntu、Debian、CentOS又是什么？

Linux是一种开放源代码的操作系统内核，而Ubuntu、Debian、CentOS等是基于Linux内核开发的操作系统。它们都使用了Linux内核，并且拥有自己的软件包管理工具、文件系统、命令行界面等等。这些操作系统在细节和特性上可能有所不同，但都遵循Linux内核的设计和实现。

# 实战

本文带入实际的文件与目录，来分享常用的Linux命令，目的方便大家学习和理解。命令可根据自己实际情况修改使用。希望对大家有所帮助。

# ubuntu/debian包管理命令

**更新系统所有**

```
apt update
```

**更新现有软件**

```
apt upgrade -y
```

**更新软件依赖关系更新现有软件删除依赖以外的软件**

```
apt full-upgrade -y
```

**安装或更新指定软件如：curl wget**

```
apt install -y curl wget
```

**删除指定软件如：curl wget**

```
apt remove -y curl wget

apt purge -y curl wget
```

# Alpine Linux包管理命令

**更新系统所有**

```
apk update
```

**更新现有软件**

```
apk upgrade
```

**安装或更新指定软件如：curl docker**

```
apk add curl docker
```

**删除指定软件如：curl wget**

```
apk del wget
```

# CentOS包管理命令

**更新系统所有**

```
yum update
```

**安装或更新指定软件如：curl wget**

```
yum install -y curl wget
```

**删除指定软件如：curl wget**

```
yum remove -y curl wget
```

# 文件管理相关

**查看home目录下内容**

```
ls /home/
```

**进入home目录**

```
cd /home
```

**创建web目录**

```
mkdir web
```

**创建空nginx.conf文件**

```
touch nginx.conf
```

**编辑docker-compose.yml文件**

```
nano docker-compose.yml
```

**压缩/home/web目录，压缩包存放到当前目录**

```
tar -czvf web.tar.gz /home/web
```

**当前目录解压web.tar.gz文件**

```
tar -xzvf web.tar.gz
```

**删除home/web目录下所有内容**

```
rm -r /home/web/*
```

**删除/home/web.tar.gz文件**

```
rm /home/web.tar.gz
```

**下载maccms10.zip文件到当前目录**

```
wget https://github.com/magicblack/maccms_down/raw/master/maccms10.zip
```

**移动home/web目录下所有文件到root目录**

```
mv /home/web/* /root/
```

**拷贝home/web目录到root**

```
cp -r /home/web /root
```

**拷贝home/web目录下的test.txt到root**

```
cp /home/web/test.txt /root
```

**赋予/var/www/html最高读写权限**

```
chmod -R 777 /var/www/html
```

**将home目录下的test.txt改名成root.txt**

```
mv /home/test.txt /home/root.txt
```

**将root.txt中所有的test替换成root**

```
sed -i 's/test/root/g' root.txt
```

**将root.txt文件所有内容删除添加一行文本root=12345保存退出**

```
cat > /home/root.txt << EOF

root=12345

EOF
```

**在root.txt文本中末尾添加一行end=yyds**

```
echo "end=yyds" >> root.txt
```
