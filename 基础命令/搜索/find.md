```bash
find [搜索范围][搜索条件]
```

- 搜索文件

```bash
find / -name install.log
```

- 注意：避免大范围搜索

```bash
find /root -iname install.log
# 不区分大小写
```

```bash
find /root -user root
# 按照所有者搜索
```

```bash
find /root -nouser
# 查找没有所有者的文件
```

```bash
find /var/log -mtime +10
# 查找 10 天前修改的文件
```

### 选项

| 选项  | 备注              |
| ----- | ----------------- |
| -10   | 10 天内修改文件   |
| 10    | 10 天当天修改文件 |
| +10   | 10 天前修改文件   |
| atime | 文件访问时间      |
| ctime | 改变文件属性      |
| mtime | 修改文件内容      |

```bash
find . -size 25k
# 查找文件大小是 25KB 的文件
```

### 选项

| 选项 | 备注             |
| ---- | ---------------- |
| -25k | 小于 25KB 的文件 |
| 25k  | 等于 25KB 的文件 |
| +25k | 大于 25KB 的文件 |

```bash
find . -inum 262422
# 查找 i 节点是 262422 的文件
```

```bash
find /etc -size +20k -a -size -50k
# 查找/etc/目录下，大于 20KB 并且小于 50KB 的文件
-a and # 逻辑与
-o or # 逻辑或
```

```bash
find /etc -size +20k -a -size -50k -exec ls -lh {} \;
# 查找/etc/目录下，大于 20KB 并且小于 50KB 的文件,并详细显示信息
# -exec/-ok 命令 {} \; 对搜索结果执行操作
```

```bash
find /root -inum 262421 -exec rm -rf {} \;
# 查找/root/目录下，i节点号为262421 的文件,并删除该文件
```

```bash
find .
# 查找当前文件夹内的文件
find . | grep .txt
# 查找当前文件夹内.txt结尾的文件
find . -type f
# 查找当前文件夹内的文件类型的文件
find . -type d
# 查找当前文件夹内的目录类型的文件
find . -type f -exec ls -l '{}' ';'
# 查找当前文件夹内的文件类型的文件并列出详细信息
find . -type f -exec grep hello '{}' ';'
# 查找当前文件夹内的文件类型的文件，并找出含有hello的那行
find . -type f -exec grep hello '{}' ';' -print
# 查找当前文件夹内的文件类型的文件，并找出含有hello的那行，并打印出该文件名
find . -type f -exec grep -n hello '{}' ';' -print
# 查找当前文件夹内的文件类型的文件，并找出含有hello的那行及行号，并打印出该文件名
find . -type f -exec grep -ni hello '{}' ';' -print
# 查找当前文件夹内的文件类型的文件，并找出含有hello（不区分大小写）的那行及行号，并打印出该文件名
```

e.g.

```bash
find ./ -name services
# 查找当前文件夹下名为services的文件
find ./ -iname services
# 查找当前文件夹下名为services（忽略大小写）的文件
find ./ -empty
# 查找当前文件夹及其子文件夹下的空文件夹
find ./ ! -empty
# 查找当前文件夹及其子文件夹下的非空文件夹
```
