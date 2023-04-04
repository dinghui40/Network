# 通过python调用阿里云接口，实现公网动态IP实时与阿里云域名绑定

## 本地部署

```bash
#拷贝脚本至执行目录下
mv yuming.py /usr/local/aliyun/
```

### 环境准备

> python3

>pip最新版

yum安装python

```
sudo yum -y update
yum -y install epel-release
yum -y install python3
yum -y groupinstall "Development tools"
#查看
python3 -V
```

```
pip3 install --upgrade pip
pip install aliyun-python-sdk-core
pip install aliyun-python-sdk-domain
```

### 定时任务准备

```bash
crontab -u root -e
#定时任务保证时间与阿里云同步 #定时任务保证定期执行脚本保障IP同步
0 1 * * *  /usr/sbin/ntpdate -b ntp.aliyun.com;hwclock -w;
*/10 * * * *  python3  /usr/local/aliyun/yuming.py

crontab -u root -l

chmod +x /usr/local/aliyun/yuming.py
```

### 修改脚本

添加信息

```
ID = '' #AccessKey ID
SECRET = '' #AccessKey Secret
regionId = '' #地域
DomainName = '' #域名
```

保存执行

# docker 部署

> $path 本地挂载路径
>
> $image 镜像名

```bash
docker run -d --restart=always --name aliyun-ymtbjx -v $path:/usr/local/aliyun $image
```

# k8s 部署

```bash
#在本地创建日志源文件
touch yuming.log
#修改 yuming.py 文件
touch yuming.py
#修改 aliyun-ymtbjx.yaml 的 hostPath: 本地挂载路径
kubectl apply -f aliyun-ymtbjx.yaml
```

