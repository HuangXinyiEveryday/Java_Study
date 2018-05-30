[TOC]

# 第一部分 Java for mac安装配置指南

## 一、安装软件

1.jdk—java运行环境

2.IntelliJ IDEA—java IDE集成开发软件

2.tomcat—web应用服务器（Apache服务器的扩展）

## 二、安装步骤（以mac电脑为例）

1.jdk官网下载http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

2.IntelliJ IDEA-mac破解博客http://www.sdifen.com/intellijidea15.html

3.tomcat 下载地址https://tomcat.apache.org

下载后，通过mac电脑文件夹前往usr/local文件夹，将解压后的tomcat拷贝到该文件夹下

注：tomcat就是一个压缩文件，只需要拷贝到对应目录文件夹下即可

------

# 第二部分 微服务架构及基础介绍

## 一、什么是微服务

​	将一个完整的应用（单体应用）按照一定的拆分规则（后文讲述）拆分成多个不同的服务，每个服务都能独立地进行开发、部署、扩展。服务于服务之间通过注入RESTful api或其他方式调用

​	每个服务运行在其独立的进程中，服务与服务之间采用轻量级的通信机制互相沟通（Spring Cloud基于HTTP的RESTFul API，阿里云dubbo基于RPC），每个服务都围绕其具体业务进行构建，并且能够被独立地部署到生产环境。微服务的优势在于规避统一集中式的服务管理，对于每一个服务而言都可以根据业务上下文的特征选择合适的语言、工具对其进行构建

## 二、Spring Cloud组件架构

### 1.SpringCloud概念

​	SpringCloud是一系列框架的有序集合，利用Spring Boot开发的便利性简化分布式系统基础设施的开发。Spring是将开发比较成熟的服务框架组合起来，通过SpringBoot风格进行再封装，屏蔽复杂的配置和实现原理。

### 2.SpringCloud组件架构

![img](/Users/x/Documents/GitHub/huangxinyieveryday/Java_Study/image/Center.png)

​	工作流程：所有请求（包括网页、app等不同媒介）通过统一的API网关（**Zuul**）访问内部服务

​                           网关接收请求后，从注册中心（**EurekaServer**）获取可用服务

​                           由**Ribbon**进行负载均衡后，分发到后端的具体实例

​                          微服务之间通过**Feign**进行通信处理业务

​                          **Hystrix**负责处理服务之间的超时熔断（即网络链接断掉后如何处理）

​                          **Turbine**监控服务间的调用和熔断的相关指标

​	*注：SpringCloud架构体系的所有微服务都通过Zuul来对提供统一的访问入口，所有需要和微服务架构内部服务进行通讯的请求都走统一的网关API*

Eureka服务发现与Ribbon客户端负载均衡的结合，为内部“微服务”提供通信支持，但是，如果你想要与外界通信时（你提供外部API，或只是从你的页面使用AJAX），将各种服务隐藏在一个代理之后是一个明智的选择。Ribbon 是 Netflix 发布的云中间层服务开源项目，其主要功能是提供客户侧软件负载均衡算法。

### 3.SpringCloud核心功能

​	分布式/版本化配置、服务注册和发现、路由、服务和服务之间的调用、负载均衡、断路器、分布式消息传递

​	微服务是一种架构理念，提出了微服务的设计原则，从理论为具体的技术提供指导，Springboot是一套快速配置的脚手架，可以基于SpringBoot开发单个微服务。SpringCloud是一个基于SpringBoot实现的服务治理工具包，**Springboot专注于快速、方便集成的单个微服务个体；SpringCloud关注全局的服务治理框架** 

## 三、微服务架构设计概念

### 1.服务种类

基础服务：一些基础组件，与具体业务无关；例如：短信服务、邮件服务、文件存储服务、消息通知服务、邮件服务…...

业务服务：一些垂直的业务系统，只处理单一的业务类型；

前置服务：服务的接入或者输出服务，比如网站的前端服务、app的服务接口等等

### 2.服务拆分

<u>横向拆分</u>：按照不同的业务域进行拆分，例如卫生间、厨房等等形成独立的业务域微服务集群

<u>纵向拆分</u>：把横向拆分的业务域根据不同模块和组件进行拆分，例如公共组件拆分成独立的原子服务、厨房拆分到具体每个传感器锁提供的服务（例如燃气、冰箱等等）

### 3.步骤方法

- 在确定使用SpringBoot/Cloud技术下进行微服务之前，要先梳理出系统的服务，对不同的服务进行分类，以确认演化的节奏
- 熟悉SpringBoot技术，优先在基础服务上进行微服务设计
- SpringBoot对每一个微服务设计完成后，使用SpringCloud进行整个项目系统的改造
- 前期可以少量项目进行微服务化，逐渐推进整体微服务化

## 四、微服务数据库挑战

持续更新……...

因为微服务数据库部分相对比较复杂，后续在进行细节切分，先将微服务数据库搭建起来

------

# 第三部分 SmartHome项目微服务设计

## 一、准备工作

Java、Maven、SpringBoot、SpringCloud

## 二、SmartHome功能架构

![Smarthome功能架构](/Users/x/Documents/GitHub/huangxinyieveryday/Java_Study/image/Smarthome%E5%8A%9F%E8%83%BD%E6%9E%B6%E6%9E%84.png)

## 三、SmartHome物理结构

![smarthome物理结构图](/Users/x/Documents/GitHub/huangxinyieveryday/Java_Study/image/smarthome%E7%89%A9%E7%90%86%E7%BB%93%E6%9E%84%E5%9B%BE.png)



## 四、SmartHome技术栈选型

### 1.SmartHome架构说明

- App、Web和微信端实现前后端分离技术
- 前端使用Vue+Webpack技术
- 服务端使用SpringCloud技术栈实现微服务架构
- 微服务之间使用rocketmq+mysql做消息100%可达，保证微服务持久化（rocketmq还可以提高消息吞吐量）
- 统一网关API使用基于OAuth2.0的安全认证，app、web及微信使用基于JWT的安全认证
- 目前每个独立的微服务使用java（基于SpringBoot）构建工程
- 使用客户的负载均衡Ribbon从服务注册中心（Eureka）拉取服务列表，根据业务特点加权负载调用
- 使用Hystrix做服务熔断/降级处理，避免单个微服务不可用引起整个系统崩溃，提高系统可用程度
- 使用Boot admin做服务监控指标
- 使用Zipkin做调用链监控
- 使用阿里云短信服务，进行第三方短信平台发送；使用百度API接口

------

### 2.SmartHome技术选型（可能会根据实际需求修改）

SpringBoot——基础构建框架，用于快速整合资源

SpringFramework——底层容器

SpringCloud——微服务框架

SpringCloudEureka——微服务注册中心

SpringCloudZuul——微服务网关

SpringCloudHystrix——微服务容错框架

SpringCloudFeign——微服务声明式调用框架

SpringBootAdmin——微服务管理中心

SpringDataJpa——微服务持久化框架

SpringDataRedis——缓存框架

ApacheShiro——安全框架

SpringValidator——后端验证框架

Maven——项目构建管理

Redis——分布式缓存数据库

Mysql——对象关系数据库

CAS——单点登录认证

------

### 3.SmartHome技术栈

- 前端

  VUE.js

- 服务端（JAVA）

  SpringCloud、Zuul（统一网关）、Feign（微服务之间通信）

  Hystrix（超时熔断）、Turbine（汇总系统内多个服务的数据）、Eureka（服务注册）

  Ribbon(负载均衡)、BootAdmin（服务监控）、Zipkin（调用链监控）

  OAuht2（安全认证）、JWT（前端安全认证）、Hibernate/Mybatis（持久层框架）

  Mapper3、PageHelper、Security

  Mysql(数据库）、Redis（数据库功能））、,MQ（消息服务）

  zookeeper（分布式协调服务）、elastic-job（分布式定时任务框架）、mail（邮件服务）

- 第三方服务

  阿里云短信服务

  百度地图API

------

## 五、SmartHome项目模块划分

### 1.服务管理模块—smarthome_sm

- smarthome_sm_admin:系统管理后台
- smarthome_sm_api:系统服务对外接口
- smarthome_sm_api_feign:基于Spring Cloud Feign的调用实现
- smarthome_sm_core:系统管理核心
- smarthome_sm_server:系统管理服务

------

### 2.配置模块—smarthome_configuration

------

### 3.用户登录模块—smarthome_usrlogin

- smarthome_usrlogin_client 客户端jar包，用于集成到需要CAS授权的系统
- smarthome_usrlogin_server CAS服务端，单独部署，用于完成用户的登录，进入主界面功能
- smarthome_usrlogin_manager CAS服务管理，用于管理授权服务等

------

### 4.公共模块—smarthome_common

- smarthome_common_api:前后端数据传输公共接口，实现后端数据传输给前端
- smarthome_common_getdata:数据库读取数据公共模块，实现从数据库取数据

------

### 5.接口模块—smarthome_api

- smarthome_api_kitchen:厨房接口
- smarthome_api_livingroom:卧室接口
- smarthome_api_sleep:睡眠接口
- smarthome_api_bathroom:卫生间接口
- smarthome_api_healthy:生理指标接口
- smarthome_api_danger：危险隐患接口
- smarthome_api_notification：物品报警接口
- smarthome_api_abnormal：异常指标接口
- smarthome_api_healthyreport：健康报告接口
- smarthome_api_gps：gps数据接口

------

### 6.居家养老模块—smarthome_jjyl

| 模块名                            | 内容                                             |
| --------------------------------- | ------------------------------------------------ |
| smarthome_jjyl_usercenter         | 居家养老用户中心                                 |
| smarthome_jjyl_backmanager        | 居家养老后台管理                                 |
| smarthome_jjyl_fridgesensor       | 冰箱传感器数据处理                               |
| smarthome_jjyl_gassensor          | 燃气传感器数据处理                               |
| smarthome_jjyl_dietsensor         | 饮食传感器数据处理                               |
| smarthome_jjyl_lamp               | 电灯数据处理（包括卧室、厨房、客厅、卫生间等）   |
| smarthome_jjyl_mattresssensor     | 床垫传感器数据处理（包括睡眠、翻身、心率等信息） |
| smarthome_jjyl_sofasensor         | 沙发传感器数据处理                               |
| smarthome_jjyl_aircondition       | 空调数据处理                                     |
| smarthome_jjyl_tv                 | 电视数据处理                                     |
| smarthome_jjyl_stoolsensor        | 马桶传感器数据处理                               |
| smarthome_jjyl_washsensor         | 洗澡传感器数据处理                               |
| smarthome_jjyl_hydrovalvesensor   | 水阀传感器数据处理                               |
| smarthome_jjyl_sos                | sos呼救处理                                      |
| smarthome_jjyl_tumblesensor       | 跌到检测传感器数据处理                           |
| smarthome_jjyl_notificationsensor | 物品忘带提醒传感器数据处理                       |
| smarthome_jjyl_gps                | gps定位数据                                      |
| smarthome_jjyl_bloodglucose       | 血糖数据处理                                     |
| smarthome_jjyl_bloodpressure      | 血压数据处理                                     |
| smarthome_jjyl_temperature        | 体温数据处理                                     |
| smarthome_jjyl_heartrate          | 心率数据处理                                     |
| smarthome_jjyl_bmi                | bmi数据处理                                      |
| smarthome_jjyl_medicinebox        | 药盒数据处理                                     |
| smarthome_jjyl_devicecontrol      | 设备控制                                         |

------

### 7.养老机构模块—smarthome_yljg

后期更新

------

### 8.大数据平台分析模块—smarthome_datacenter

后期更新

------

### 9.消息推送模块—smarthome_notification

用来推送到app、web及微信小程序端日常消息、异常报警、系统分析等信息

------

### 10.支付模块—smarthome_pay

用来提供支付功能，调用第三方平台支付接口（支付宝、微信）

------

### 11.数据处理行为分析模块—smarthome_machinelearning

对不同模块采用机器学习的方式进行数据处理及行为分析，主要分为两个部分

- 单独模块及传感器的数据处理分析
- 综合老人各项指标数据（包括历史数据）进行行为分析等

```markdown
注：7、8另外两个需要开发的系统
   9、10为后期需要开发的服务模块
   11是机器学习核心模块
```

------

### 12.设备数据采集模块—smarthome_datacollect

涉及将硬件数据采集到数据库，后期使用模块化、可视化方式进行开发

*<u>**注:后一阶段工作**（涉及具体设计工作）</u>*

------

### 13.工作流模块—smarthome_bpm

用来对不同微服务进行工作流程、步骤及逻辑的串联，保证系统获取有效信息，实现功能

**<u>注：主要是用来实现后台工作流串联（后期可以使用可视化的方式进行编程开发）</u>**

------

### 14.内容管理模块—smarthome_cms

前端网站开发模块，用来加速网站开发，通过提供大量固定的模板减少开发人员开发时间，即使用可视化的方式辅助开发人员进行前端网站的开发。

<u>***注：后期拓展***</u>

```markdown
12/13/14是开发可视化、流程化的拓展辅助，有助于后期开发，因此优先级最后
```

------

## 六、主机规划



