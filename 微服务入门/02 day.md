1.dao层是一个依赖模块而已，并不能独立运行 ，配置文件由引用他的服务决定 

所以如果新增的服务需要使用dao层，除了dao层增加持久化方法，还需要在自己的服务层进行配置，扫描自己新增的mapper

```
dao层 src/main/java/dao 
      resources/mapper/test
resources层中配置xml文件，配置sql语句
```

```
自己新建资源服务
smarthome-**-**
如果需要使用mybatis和dao层
需要在自己服务resources中的application.yml配置mybatis-plus中mapper-locations(一般配置相同)
```

注：idea可以选择project files，避免idea缩进文件夹××.××的形式

​      每个模块引用自己的mapper.模块名  把每个都独立出来 ，然后每个不同的服务都扫不同的路径 

2.