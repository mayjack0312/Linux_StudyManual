```bash
while [ 条件判断式 ]
  do
    # 程序
  done
```

e.g.

```bash
#!/bin/bash
# 从1加到100
i=1
s=0
while [ $i -le 100 ]
  do
    s=$(( $s+$i ))
    i=$(( $i+1 ))
  done
echo "The sum of 1+2+...+100 is: $s"
```
