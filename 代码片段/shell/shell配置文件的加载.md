# shell配置文件的加载

## 登录式的shell
会加载以下这些的文件：
- /etc/profiles 全局配置文件
- ~/.bash_profile 用户目录的文件
- ~/.bash_login 用户目录文件
- ~/.profile 用户目录文件
加载顺序是 ~/.bash_profile > ~/.bash_login > ~/.profile
文件存在就加载，没有就pass

## 非登录式的shell
如果以非登录的方式启动shell，那么就不会读取以上的配置文件，而是直接读取~/.bashrc
~/.bashrc文件还会嵌套加载/etc/bashrc
```
if [ -f /etc/bashrc ]; then
. /etc/bashrc
fi
```