```bash
declare [+/-][选项] 变量名
```

### 选项

| 选项 | 备注                       |
| ---- | -------------------------- |
| -    | 给变量设定类型属性         |
| +    | 取消变量的类型属性         |
| -a   | 将变量声明为数组型         |
| -i   | 将变量声明为整数型         |
| -x   | 将变量声明为环境变量       |
| -r   | 将变量声明为只读变量，慎用 |
| -p   | 显示指定变量的被声明的类型 |

e.g.

```bash
declare -i cc=$aa+$bb
```

## 定义数组变量

### 定义数组

```bash
movie[0]=zp
movie[1]=tp
declare -a movie[2]=live
# 相当于
movie[2]=live
```

### 查看数组

```bash
echo ${movie}
# 相当于
echo ${movie[0]}
echo ${movie[2]}
# 列出movie[2]
echo ${movie[*]}
# 列出数组
```

```bash
declare -x test=123
# 和export作用相似，但其实是declare命令的作用
```

```bash
declare -p
# 查询所有变量的属性
declare -p 变量名
# 查询指定变量的属性
```
