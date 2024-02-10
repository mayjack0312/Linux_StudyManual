```bash
man 命令名
# 获取指定命令的帮助
```

```bash
man ls
# 查看ls的帮助
# 底行输入
/搜索条件
# 搜索包含搜索条件的字串
```

## man 的级别

1.  查看命名的帮助
2.  查看可被内核调用的函数的帮助
3.  查看函数和函数库的帮助
4.  查看特殊文件的帮助（主要是/dev 目录下的文件）
5.  查看配置文件的帮助
6.  查看游戏的帮助
7.  查看其他杂项的帮助
8.  查看系统管理员可用命令的帮助
9.  查看和内核相关文件的帮助

```bash
man -f 命令名
# 相当于
whatis 命令名
```

```bash
man 5 passwd
man 4 null
man 8 ifconfig
```

```bash
man -k 命令名
# 相当于
apropos 命令名
```

e.g.

```bash
apropos passwd
```
