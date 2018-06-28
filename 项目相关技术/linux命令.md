- #### linux查看当前运行的jar程序

```
ps -ef | grep java
```

- #### linux杀死jar进程

```
sudo kill -9 <进程号>
```

- #### linux查看端口

```
列出所有端口
netstat -ntlp
```

- #### linux查看端口防火墙设置

```
sudo iptables -L -n
```

- #### linux上传文件到远程服务器

```
//进入需要拷贝的文件目录下，直接拷贝文件到远程服务器tmp目录下(默认只有tmp目录下有权限)
scp DoorContact20180625.sql smarthome@192.168.85.208:/tmp
```

- #### linux打开防火墙端口

```
iptables直接打开端口
iptables -I INPUT -p tcp --dport 8000 -j ACCEPT
保存
iptables save
重启服务
service iptables restart
查看需要打开的端口是否生效
iptables status
```

```
永久打开端口 直接编辑
sudo vim /etc/sysconfig/iptables
键盘输入i，插入
-A INPUT -p tcp -m tcp --dport 4000 -j ACCEPT
esc退出 输入:wq!保存
保存服务
sudo service iptables save
再重启服务:
sudo service iptables restart
```

注：如果报错，可以尝试安装sudo yum install iptables-service