# exit
`目的`：用来退出当前shell进程，并返回一个退出状态，使用`$?`可以接收这个退出状态

exit 命令可以接受一个整数值作为参数，代表退出的状态，如果不指定，默认状态是0

```
#!/bin/bash

echo "before exit"
exit 8
echo "after exit" # 调用exit之后的代码不会再执了
```