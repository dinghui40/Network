## **frps内网穿透**

***使用方法介绍***

> frps为内网穿透代理端

构建镜像

```
docker build -t registry.cn-hangzhou.aliyuncs.com/offends/frp:frps .
```

启动容器

```
docker run --name frps --restart=always \
--net=host \
-v ${pwd}/frps.ini:/frp/frps.ini \
-d registry.cn-hangzhou.aliyuncs.com/offends/frp:frps
```

