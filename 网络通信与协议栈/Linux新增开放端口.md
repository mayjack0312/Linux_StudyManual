Linux服务器上新增开放端口号开放端口的方法：

#方法一：命令行方式#
 - 1. 开放端口命令： `/sbin/iptables -I INPUT -p tcp --dport 8080 -j ACCEPT`
 - 2.保存：`/etc/rc.d/init.d/iptables save`
 - 3.重启服务：`/etc/init.d/iptables restart`
 - 4.查看端口是否开放：`/sbin/iptables -L -n`
    

#方法二：直接编辑/etc/sysconfig/iptables文件
- 1.编辑/etc/sysconfig/iptables文件：`vi /etc/sysconfig/iptables`
- 2 加入内容并保存：`-A RH-Firewall-1-INPUT -m state --state NEW -m tcp  p tcp --dport 8080 -j ACCEPT`
- 3.重启服务：`/etc/init.d/iptables restart`
- 4.查看端口是否开放：`/sbin/iptables -L -n`

查询端口是否有进程守护用如下命令grep对应端口，如80为端口号
例：`netstat -nap|grep 80`