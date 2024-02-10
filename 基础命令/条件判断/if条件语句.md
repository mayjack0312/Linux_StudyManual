## 单条件分支语句

```bash
if [ 条件判断式 ];then
  # 程序
fi
# 或者
if [ 条件判断式 ]
  then
  # 程序
fi
```

e.g.

```bash
#!/bin/bash
test=$(env | grep "USER" | cut -d "=" -f2)
if [ "$test" == root ]
  then
  echo "Current user is root"
fi
```

### 判断分区使用率

```bash
#!/bin/bash
# 统计根分区使用率
rate=$(df -h | grep "/dev/sda3" | awk '{print $5}' | cut -d "%" -f1)
# 把根分区使用率作为变量值赋予变量rate
if [ "$rate" -ge "80" ]
  then
  echo "Waring dev/sda3 is full!!"
fi
```

## 双条件分支语句

```bash
if [ 条件判断式 ]
  then
  # 条件成立时执行的程序
else
  # 条件不成立时执行的程序
fi
```

e.g.

```bash
#!/bin/bash
read -t 30 -p "Please input a dir:" dir
if [ -d "$dir" ]
  then
  echo "It's a dir"
else
  echo "It's not a dir"
fi
```

### 判断 apache 是否启动

```bash
#!/bin/bash
test=$(ps aux | grep httpd | grep -v grep)
# 截取http进程，并把结果赋予变量
if [ -n "$test" ]
# 如果test的值不为空，则执行then中的命令
  then
  echo "$(date) httpd is ok!" >> /tmp/autostart-acc.log
else
  /etc/rc.d/init.d/httpd start &>/dev/null
  echo "$(date) restart httpd !!" >> /tmp/autostart-errlog
fi
```

## 多条件分支语句

```bash
if [ 条件判断式 ]
  then
  # 条件成立时执行的程序
elif [ 条件判断式 ]
  then
  # 条件成立时执行的程序
else
  # 条件不成立时执行的程序
fi
```

### 判断用户输入的是什么文件

```bash
#!/bin/bash
# 判断用户输入的是什么文件
read -p "Please input a filename:" file
# 接受键盘输入，并赋予变量file
if [ -z "$file" ]
# 判断file的值是否为空
  then
  echo "Error,please input a filename"
  exit 1
elif [ ! -e "$file" ]
# 判断file的值是否存在
  then
  echo "Your input is not a file"
  exit 2
elif [ -f "$file" ]
# 判断file的值是否为普通文件
  then
  echo "$file is a regular file!"
elif [ -d "$file" ]
# 判断file的值是否为目录文件
  then
  echo "$file is a directory!"
else
  echo "$file is an other file!"
fi
```
