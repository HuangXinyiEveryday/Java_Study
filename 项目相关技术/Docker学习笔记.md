Docker包括三个概念 镜像；容器；仓库

#### Docker下载镜像

```
docker pull 镜像名:特定版本
#默认下载最新版本
```

#### **启动Docker服务（命令行）**

```
service docker start
```



#### Docker运行启动

```
#运行镜像为容器的命令
docker run -d -p [本机端口]:[docker服务器端口] --name container-name image-name
//容器不需要自己独立的ip和网卡
docker run -d --net=host --name container-name image-name
```

#### Docker查看，删除镜像

```
#查看本地镜像列表
docker images
#其中REPOSITORY是镜像名；TAG是软件版本，latest为最新版；IMAGE ID是当前镜像的唯一标识；CREATED是当前镜像创建时间；VIRTUAL SIZE是当前镜像的大小。
#删除镜像
docker rmi image-id
```

#### Docker再次启动和停止容器

```
docker stop container-name/container-id 
docker start container-name/container-id 
```

#### Docker容器显示

```
#显示正在运行的容器
docker ps
#docker ps -a
#显示所有容器
```



#### Docker删除容器

```
docker rm container-id 
```

#### Docker运行mysql实例

```
# docker启动mysql
docker run --name smarthome-mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag
```

- smarthome-mysql： 容器别名(自己定义)
- my-secret-pw：初始化设置的root用户的密码
- tag：mysql的版本，不写默认使用最新版
- -p 3306:3306：表示在这个容器中使用3306端口(第二个)映射到本机的端口号也为3306(第一个)

```
#docker连接本地mysql
docker run -it --link smarthome-mysql:mysql --rm mysql sh -c 'exec mysql -h"$MYSQL_PORT_3306_TCP_ADDR" -P"$MYSQL_PORT_3306_TCP_PORT" -uroot -p"$MYSQL_ENV_123456"'
#docker连接远程mysql
ocker run -it --rm mysql mysql -hsome.mysql.host -usome-mysql-user -p
```

#### Docker运行redis实例

```
#docker启动redis
docker run --name smarthome-redis -p 6379:6379 -d redis:tag
```

