L2TP-VPN-连接

```bash
make /usr/local/vpn/ && mv vpn.env /usr/local/vpn/
#启动容器
docker run --restart=always \
    --name ipsec-vpn-server \
    --env-file /usr/local/vpn/vpn.env \
    --restart=always \
    -v ikev2-vpn-data:/etc/ipsec.d \
    -v /lib/modules:/lib/modules:ro \
    -v /usr/local/vpn/vpn.env:/usr/local/vpn/vpn.env \
    -p 500:500/udp \
    -p 4500:4500/udp \
    -d --privileged \
    hwdsl2/ipsec-vpn-server
#启动脚本 vpn.sh
chmod +X ./vpn.sh
```

github地址

https://github.com/hwdsl2/docker-ipsec-vpn-server/blob/master/README-zh.md
