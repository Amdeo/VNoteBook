# docker
由于国内docker安装和镜像网速很慢，推荐使用[华为镜像](https://mirrors.huaweicloud.com/)

## 安装
![](_v_images/20200401222347272_15280.png =800x)


## 修改镜像源
![](_v_images/20200401222223645_9881.png =933x)

## 获取镜像
```
docker pull ubuntu #拉取镜像
```

## 启动镜像
```
docker run -it ubuntu /bin/bash
```
参数说明：
- -i: 交互式操作。
- -t: 终端。
- ubuntu: ubuntu 镜像。
- /bin/bash：放在镜像名后的是命令，这里我们希望有个交互式 Shell，因此用的是 /bin/bash。

## 查看所有容器命令
```
docker ps -a
```

直接做停止运行容器的批量删除
```
docker rm $(docker ps -a -q)
```
