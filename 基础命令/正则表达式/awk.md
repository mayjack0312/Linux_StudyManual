```bash
awk '条件1{动作1}条件2{动作2}...' 文件名
```

### 条件（pattern）

- 一般使用关系表达式作为条件
- x>10 判断变量 x 是否大于 10
- x>=10 大于等于
- x<=10 小于等于

### 动作（action）

- 格式化输出
- 流程控制语句

```bash
awk '{printf $2 "\t" $4 "\n"}' 文件名
awk '{print $2 "\t" $4}' 文件名
awk 'BEGIN{printf "This is a transcript \n"}{printf $2 "\t" $4 "\n"}' 文件名
```

e.g.

```bash
df -h | awk '{printf $5}'
df -h | grep "/dev/sda1" | awk '{printf $5}'
df -h | grep "/dev/sda1" | awk '{printf $5}' | cut -d "%" -f 1
```

## FS 内置变量

```bash
cat /etc/passwd | grep "/bin/bash" | \
awk 'BEGIN{FS=":"}{printf $1 "\t" $3 "\n"}'
# 指定分隔符
```

```bash
cat a.txt | grep -v Name | \
awk '$4>=70{printf $2 "\n"}'
# 关系运算符
```
