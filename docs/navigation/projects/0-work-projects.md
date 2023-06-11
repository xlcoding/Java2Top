---
title: 一期 | 优质面试求职开源项目
category: 
    - 开源项目
    - Java项目
    - Java经典项目
    - Java2Top
    - 求职项目
icon:

---

> Java2Top，校招面试求职，大厂学习导航~
>
> 致力于打造全网最佳大厂学习进阶平台！

对于校招求职，关于项目这块是特别重要的，可以说项目间接决定了你的生死。在此前的文章介绍了可以从 Github 等找寻一个适合自己的开源项目，但是网上项目资源满天飞，去找到一款可以让面试官眼前一亮的项目还是有点困难。

**本站会根据当下面试热点，技术潮流持续收集适合用于《校招面试求职》的精品项目，和人手一个的秒杀，商城，管理系统说拜拜吧，您~。**

## 求职面试推荐

### 1、从零实现一个操作系统内核

对于编程学习来说， 学习操作系统有助于我们了解计算机的工作原理。操作系统中的很多思想、很多经典的算法，你都可以在我们日常开发使用的各种工具或者框架中找到它们的影子。

![img](https://camo.githubusercontent.com/0cb75538b5ea92e01bafbaaa6c94f9f10910823731c0e896ae6d6140e0eb0c00/68747470733a2f2f747661312e73696e61696d672e636e2f6c617267652f30303833317253546c793167646c366a38627877376a333137733075307464392e6a7067)

在学校我们老师也会叫我们写一个简单的操作系统来体会其中的原理。

如果你能够自己独立写一个操作系统内核的话，即使是简易的实现，我相信也能够为自己的简历加分不少。

> 项目地址：https://github.com/Simple-XX/SimpleKernel

### 2、proxyee-down（Http下载器）

`Proxyee Down` 是一款开源的免费 HTTP 高速下载器，底层使用`netty`开发，支持自定义 HTTP 请求下载且支持扩展功能，可以通过安装扩展实现特殊的下载需求。

![img](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/java202304231414330.jpeg)

本项目后端主要使用 `java` + `spring` + `boot` + `netty`，前端使用 `vue.js` + `iview`

> 项目地址：https://github.com/proxyee-down-org/proxyee-down

### 3、基于人工智能的智慧校园助手

本项目旨在为同城高校学子提供一个集校园服务，商城服务，二手交易，智能问答，消息推送，动态分享功能于一体的综合性智慧服务平台

![img](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/java/k202304182303253.jpg)

技术栈：SpringBoot+SpringCloud+Redis+Kafka+XXL-Job+Vue.js+其他第三方 SDK 等

- 将校内服务与百度地图结合实现信息视觉呈现；采用人脸识别打造安全机制，通过模型训练数据采集提供了智能系统问 

  答服务

- 对系统慢 SQL 进行优化，使得系统性能大幅度提高。 

- 用 Redis 存储登录 ticket 和验证码，解决分布式 session 问题 

- 定义热点数据并缓存在 Redis，降低了数据库访问压力 

- 将校内服务与百度地图结合实现信息视觉呈现；采用人脸识别打造安全机制，通过模型训练数据采集提供了智能系统问 

  答服务 

- 对热帖排行模块，使用分布式缓存 Redis 和本地缓存 Caffeine 作为多级缓存，避免了缓存雪崩，将 QPS 提升了20倍 

  (10-200)，大大提升了网站访问速度。并使用 Quartz 定时更新热帖排行 

- 利用 JVM 指令排查出 GC 问题，调整 JVM 配置，降低 GC 次数使 

- 用 Kafka 打造强大的异步消息系统

version1.0 可以公众号后台回复【**基于人工智能的智慧校园助手**】

后期迭代升级更新优化 会发布 github 持续关注，第一时间接收通知。

> 项目演示：https://www.bilibili.com/video/BV1XT4y1w7Xc

### 4、一个手把手教你造轮子的项目

通过这个项目，你能学会如何创造自己的操作系统、编程语言、搜索引擎、框架，工具库……

这个项目聚集了很多车轮子项目。

**构建一个简易Doker**

![img](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/concurrent202303201054928.png)

> https://github.com/danistefanovic/build-your-own-x#build-your-own-docker

**构建一个简易数据库**

![img](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/concurrent202303201054095.png)

> https://github.com/danistefanovic/build-your-own-x#build-your-own-database

.........

**整个仓库地址**

> 项目地址：https://github.com/danistefanovic/build-your-own-x

### 5、牛客论坛

一个仿照牛客网实现的讨论社区，不仅实现了基本的注册，登录，发帖，评论，点赞，回复功能，同时使用前缀树实现敏感词过滤，使用wkhtmltopdf 生成长图和 PDF，实现网站 UV 和 DAU 统计，并将用户头像等信息存于七牛云服务器。

![img](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/java202304231453823.png)

**功能介绍**

- 使用 Spring Security 做权限控制，替代拦截器的拦截控制，并使用自己的认证方案替代Security 认证流程，使权限认证和控制更加方便灵活。
- 使用 Redis 的 set 实现点赞，zset 实现关注，并使用 Redis 存储登录 ticket 和验证码，解决分布式 session 问题。
- 使用 Redis 高级数据类型 HyperLogLog 统计 UV(Unique Visitor), 使用 Bitmap 统计 DAU (Daily Active User)。
- 使用 Kafka 处理发送评论、点赞和关注等系统通知，并使用事件进行封装，构建了强大的异步消息系统。
- 使用 Elasticsearch 做全局搜索，并通过事件封装，增加关键词高亮显示等功能。
- 对热帖排行模块，使用分布式缓存 Redis 和本地缓存 Caffeine 作为多级缓存，避免了缓存雪崩，将 QPS 提升了 20倍(10-200)，大大提升了网站访问速度。并使用 Quartz 定时更新热帖排行。

> 项目地址：https://www.nowcoder.com/study/live/246

## 其他学习项目

这里收集的一些开源项目也可以看看~

**电商类**

- 天猫整站 Springboot：https://how2j.cn/module/156.html
- mall-learning：https://github.com/macrozheng/mall-learningmall（学习教程，架构、业务、技术要点全方位解析）
- miaosha：https://github.com/qiurunze123/miaosha （秒杀系统设计与实现）
- mall-swarm：https://github.com/macrozheng/mall-swarm（一套微服务商城系统，采用了 Spring Cloud Greenwich、Spring Boot 2、MyBatis、Docker、Elasticsearch 等核心技术，同时提供了基于 Vue 的管理后台方便快速搭建系统）

**管理系统类**

- [Spring-Cloud-Admin](https://github.com/wxiaoqi/Spring-Cloud-Admin)：Cloud-Admin 是国内首个基于 Spring Cloud 微服务化开发平台，具有统一授权、认证后台管理系统，其中包含具备用户管理、资源权限管理、网关 API 管理等多个模块，支持多业务系统并行开发，可以作为后端服务的开发脚手架。代码简洁，架构清晰，适合学习和直接项目中使用。核心技术采用 Spring Boot2 以及 Spring Cloud Gateway 相关核心组件，前端采用 vue-element-admin 组件。
- [pig](https://gitee.com/log4j/pig)：基于 Spring Boot 2.2、 Spring Cloud Hoxton & Alibaba、 OAuth2 的 RBAC 权限管理系统。
- [悟空CRM](https://github.com/72crm/72crm-java)：基于jfinal+vue+ElementUI的前后端分离CRM系统

**博客类**

- [favorites-web](https://github.com/cloudfavorites/favorites-web):云收藏 Spring Boot 2.X 开源项目。云收藏是一个使用 Spring Boot 构建的开源网站，可以让用户在线随时随地收藏的一个网站，在网站上分类整理收藏的网站或者文章。
- [community](https://github.com/codedrinker/community)：码问，开源论坛、问答系统，现有功能提问、回复、通知、最新、最热、消除零回复功能。技术栈 Spring、Spring Boot、MyBatis、MySQL/H2、Bootstrap
- [vhr](https://github.com/lenve/vhr)：微人事是一个前后端分离的人力资源管理系统，项目采用 SpringBoot+Vue 开发。

**其他**

- [PassJava-Platform](https://github.com/Jackson0714/PassJava-Platform)：一款面试刷题的 Spring Cloud 开源系统
- [moti-cloud](https://github.com/373675032/moti-cloud)：莫提网盘，基于 SpringBoot+MyBatis+ThymeLeaf+BootStrap，适合初学者
- [threadandjuc](https://github.com/qiurunze123/threadandjuc)：three-high-import 高可用\高可靠\高性能，三高多线程导入系统（该项目意义为理论贯通)

## 篇末

我个人觉得，现在这个状况，相比于做分布式什么的，做一些偏基础或者车轮子（**体会计算机运行原理，体会先人思想**）的项目可能反而让面试官眼前一面，只是个人看法，每个人根据自己的想法去找到一个适合自己项目认真准备就可以。

