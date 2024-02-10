```bash
cat 文件名
cat 文件名 | uniq
cat 文件名 | uniq | grep txt
cat 文件名 | uniq | grep txt | sort
```

### 选项

| 选项               | 备注                                   |
| ------------------ | -------------------------------------- |
| -b                 | 对非空输出行编号                       |
| -n                 | 对输出的所有行编号                     |
| -v                 | 使用^ 和 M- 引用，除了 LFD 和 TAB 之外 |
| --show-nonprinting | 使用^ 和 M- 引用，除了 LFD 和 TAB 之外 |
| -E                 | 在每行结束处显示"$"                    |
| --show-ends        | 在每行结束处显示"$"                    |
| -T                 | 将跳格字符显示为^I                     |
| --show-tabs        | 将跳格字符显示为^I                     |
| -A                 | 等于-vET                               |

e.g.

```bash
cat 文件名
cat -b 文件名
cat -n 文件名
cat -A 文件名
```
