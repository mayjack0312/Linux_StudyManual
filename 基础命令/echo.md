```bash
echo 字符串
echo -e 字符串
echo -n 字符串
echo 字符串 > a.txt
# 覆盖
echo 字符串 >> a.txt
# 追加
```

### 选项

| 选项 | 备注       |
| ---- | ---------- |
| -e   | 解析转义符 |
| -n   | 尾部不换行 |

e.g.

```bash
echo 'ni \v hao \v a'
echo -e 'ni \v hao \v a'
echo -n 'ni \v hao \v a'
```
