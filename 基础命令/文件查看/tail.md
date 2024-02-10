```bash
tail test.log
# 显示最后10行
tail -n 15 /etc/services
tail -15 /etc/services
# 显示最后15行
tail -1000 test.log | more
# 使用more查看最后1000行
tail -f test.log
# 实时查看
```
