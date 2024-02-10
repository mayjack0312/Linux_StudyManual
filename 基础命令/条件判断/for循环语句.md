```bash
for 变量 in 值1 值2 值3...
  do
    # 程序
  done
```

e.g.

```bash
#!/bin/bash
for i in 1 2 3 4 5
  do
    echo $i
  done
```

e.g.

```bash
#!/bin/bash
cd /root/test/
ls *.tar.gz > ls.log
ls *.tgz >> ls.log

for i in $(cat ls.log)
  do
    echo tar -zxf $i &>/dev/null
  done
rm -rf ls.log
```

e.g.

```bash
#!/bin/bash
# 从1加到100
s=0
for ((i=1;i<=100;i=1+1))
  do
    s=$(( $s+$i ))
  done
echo "The sum of 1+2+...+100 is: $s"
```

e.g.

```bash
#!/bin/bash
# 批量添加指定数量的用户
read -p "Please input user name:" -t 30 name
read -p "Please input the number of users:" -t 30 num
read -p "Please input the password of users:" -t 30 pass
if [ ! -z "$name" -a ! -z "$num" -a ! -z "$pass" ]
  then
  y=$(echo $num | sed 's/[0-9]//g')
  if [ -z "$y" ]
    then
    for ((i=1;i<=$num;i=1+1))
      do
        /usr/sbin/useradd $name$i &>/dev/null
        echo $pass | usr/bin/passwd --stdin $name$i &>/dev/null
      done
  fi
fi
```
