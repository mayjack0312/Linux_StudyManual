```bash
case $变量名 in
  "值1")
    如果变量的值等于值1，则执行程序1
    ;;
  "值2")
    如果变量的值等于值2，则执行程序2
    ;;
  # ...
  *)
    如果变量的值都不是以上值，则执行此程序
    ;;
esac
```

e.g.

```bash
#!/bin/bash
# 判断用户输入
read -p "Please choose yes/no" -t 30 cho
case $cho in
  "yes")
    echo "Your choose is yes!"
    ;;
  "no")
    echo "Your choose is no!"
    ;;
  *)
    echo "Your choose is error!"
    ;;
esac
```
