## **frpc内网穿透**

***使用方法介绍***

> frpc为内网穿透客户端
>
> 本文以windows举例

[Github仓库](https://github.com/fatedier/frp)

下载windows包

```
https://github.com/fatedier/frp/releases/download/v${version}/frp_${version}_windows_amd64.zip
```

解压文件到C盘下并更改目录名称为frpc

删除无用文件

```
删除
LICENSE frps.exe  frps.ini  frps_full.ini
留下
frpc.exe  frpc.ini  frpc_full.ini
```

把`frpc.bat`文件放在此目录下

修改`frpc.ini`文件

```
[common]
server_addr = frps公网地址
server_port = 7000
token = 12345678

[windows]
type = tcp
local_ip = 127.0.0.1           
local_port = 3389
remote_port = 3389
```

双击`frpc.bat`运行

构建镜像

```
docker build -t registry.cn-hangzhou.aliyuncs.com/offends/vpn:frpc .
```

Copy配置文件

```
docker run --name frp_slave \
-d registry.cn-hangzhou.aliyuncs.com/offends/vpn:frpc

docker cp frp_slave:/frp/frpc.ini .

docker rm -f frp_slave
```
启动容器

```
docker run --name frpc --restart=always \
--net=host \
-v ${pwd}/frpc.ini:/frp/frpc.ini \
-d registry.cn-hangzhou.aliyuncs.com/offends/vpn:frpc
```