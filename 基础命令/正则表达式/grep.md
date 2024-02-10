```bash
grep [选项] 字符串 文件名
```

- 截取
- 在文件当中匹配符合条件的字符串

### 选项

| 选项 | 备注           |
| ---- | -------------- |
| -i   | 忽略大小写     |
| -v   | 排除指定字符串 |
| -E   | 与 egrep 相似  |

```bash
egrep [选项] 字符串 文件名
```

e.g.

```bash
egrep '^$|^#' a.txt
grep -E '^$|^#' a.txt
# 显示空行或以#开头的行
egrep -v '^$|^#' a.txt
grep -Ev '^$|^#' a.txt
# 不显示空行或以#开头的行
```

e.g.

```bash
grep "/bin/bash" /etc/passwd | grep -v "root" | cut -f -d ":"
# 获取非root用户
```
