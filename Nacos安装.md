# Nacos安装

## 1.环境准备

#### 拉取镜像

```shell
docker pull nacos/nacos-server
```

#### 创建nacos文件目录

```shell
sudo mkdir -p /data/nacos
sudo chmod -R 777 /data/nacos
mkdir -p /data/nacos/init.d
mkdir -p /data/nacos/logs
mkdir -p /data/nacos/data
mkdir -p /data/nacos/conf
sudo chmod -R 777 /data/nacos
```

#### 创建配置文件

```shell
cd /data/nacos/init.d
vi custom.properties
# 文件内容：
management.endpoints.web.exposure.include=*
```

```
cd /data/nacos/conf
vi application.properties
# 文件内容：
# key是“odcsz@1236547890odcsz@1236547890odcsz@1236547890odcsz@1236547890”的base64编码的值
nacos.core.auth.plugin.nacos.token.secret.key=b2Rjc3pAMTIzNjU0Nzg5MG9kY3N6QDEyMzY1NDc4OTBvZGNzekAxMjM2NTQ3ODkwb2Rjc3pAMTIzNjU0Nzg5MA==
```

## 2.启动

创建容器并启动

```shell
docker run -d --restart always \
--name nacos \
-p 8848:8848 \
-p 9848:9848 \
-e MODE=standalone \
-v /data/nacos/init.d/custom.properties:/home/nacos/init.d/custom.properties \
-v /data/nacos/logs:/home/nacos/logs \
-v /data/nacos/data:/home/nacos/data \
-v /data/nacos/conf/application.properties:/home/nacos/conf/application.properties \
nacos/nacos-server
```

下次启动

```
docker restart nacos
```

## 3.访问

http://ip:8848/nacos

默认登录用户名密码 nacos/nacos 注意修改管理员密码
