```bash
alias
# 查看系统中所有的命令别名
alias 别名='原命令'
# 设置alias
```

e.g.

```bash
alias ls='ls --color=never'
```

```bash
vi ~/.bashrc
# 写入环境变量配置文件，别名永久生效
source ~/.bashrc
# or
. ~/.bashrc
```

```bash
unalias 别名
# 删除别名
```
