# shell脚本
查看可用的shell
`cat /etc/shells`

查看目前使用的shell
`echo $SHELL`

## 变量
```
var1=value
var2='value1'
var3="value2"
```
`=号之间不能有空格`

## 作用域
局部变量
shell脚本在函数中定义的变量，默认也是`全局变量`


## 输出和输入
输出
```
echo "string" # 直接输出一个字符串

url=xxx
echo $url # 将变量输出的终端
```

输入
read 
|选项|说明|
|---|---|
|-a|把读取的数据赋值给数组 array，从下标 0 开始。|
|-d|用字符串 delimiter 指定读取结束的位置，而不是一个换行符（读取到的数据不包括 delimiter）。|
|-e|在获取用户输入的时候，对功能键进行编码转换，不会直接显式功能键对应的字符。|
|-n|读取num个字符，而不是整行字符|
|-p|显示提示信息，提示内容为 prompt。|
|-r|原样读取（Raw mode），不把反斜杠字符解释为转义字符。|
|-s|静默模式（Silent mode），不会在屏幕上显示输入的字符。当输入密码和其它确认信息的时候，这是很有必要的。|
|-t|设置超时时间，单位为秒。如果用户没有在指定时间内输入完成，那么 read 将会返回一个非 0 的退出状态，表示读取失败。|
|-u|使用文件描述符 fd 作为输入源，而不是标准输入，类似于重定向。|



```
  #! /bin/bash

  read -p "Enter some information >" name url age
  echo "网站名字: $name"
  echo "网址：$url"
  echo "年龄：$age"
```
注意，必须在一行内输入所有的值，不能换行，否则只能给第一个变量赋值，后续变量都会赋值失败。
`每个输入之间需用空格`

## 如何运行shell脚本
`交互式`：在Shell中一个个地输入命令并及时查看它们的输出结果，整个过程都在在跟Shell不停地互动
`非交互式`：让所有命令批量化、一次性地执行,使用shell就是非交互式
`登入式`：需要使用用户名和密码登入后，才可以使用shell
`非登入式`：不需要登入直接使用shell

Shell一共有四种运行方式：
- 交互式的登入的Shell
- 交互式的非登入Shell
- 非交互式的登入Shell
- 非交互式的非登入Shell

### 判断shell是否式交互式
```
echo $-
# 输出的值中包含i,表示交互式
```
输出
```
himBH
```

我们在shell脚本中在执行下这个命令
```
#!/bin/bash

echo $-
```
输出
```
hB
```

## 判断shell是否为登入式
在命令行中输入：
```
shopt login_shell
```
输出
```
login_shell    on    登入shi

login_shell    off  非登入式
```






