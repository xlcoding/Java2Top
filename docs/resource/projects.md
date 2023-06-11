---
icon: creative
title: 精品开源项目
---
## Java 的高性能缓存库

![123](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/java/k202304192328446.png)

借鉴了 Guava 和 ConcurrentLinkedHashMap 的设计经验，青出于蓝而胜于蓝的 Java 本地缓存库，拥有更高的缓存命中率和更快的读写速度。

```java
LoadingCache<Key, Graph> graphs = Caffeine.newBuilder()
    .maximumSize(10_000)
    .expireAfterWrite(Duration.ofMinutes(5))
    .refreshAfterWrite(Duration.ofMinutes(1))
    .build(key -> createExpensiveGraph(key));
```

> https://github.com/ben-manes/caffeine

很多小伙伴都想找能跟着学习的完整实战项目。小龙分类整理了亿点点，都是开源免费的，适合系统学习，而且都是**可以写到简历上的企业级完整项目**！（其中很多项目还自带教程哦）更多优质 Java 开源项目推荐请看：[Java 开源项目精选]()。

## **电商秒杀**

[天猫整站 J2EE](https://link.zhihu.com/?target=https%3A//how2j.cn/module/115.html)

[天猫整站 SSM](https://link.zhihu.com/?target=https%3A//how2j.cn/module/134.html)

[天猫整站 Springboot](https://link.zhihu.com/?target=https%3A//how2j.cn/module/156.html)

[mall-learning](https://link.zhihu.com/?target=https%3A//github.com/macrozheng/mall-learning)：mall学习教程，架构、业务、技术要点全方位解析。

[SpringBoot 电商商城系统 Mall4j](https://link.zhihu.com/?target=https%3A//github.com/gz-yami/mall4j)

[SpringBoot 完整电商系统 Mall](https://link.zhihu.com/?target=https%3A//github.com/macrozheng/mall)：包括前台商城系统及后台管理系统，基于 SpringBoot+MyBatis 实现。

[newbee-mall](https://link.zhihu.com/?target=https%3A//github.com/newbee-ltd/newbee-mall)：newbee-mall 项目（新蜂商城）是一套电商系统，包括 newbee-mall 商城系统及 newbee-mall-admin 商城后台管理系统，基于 Spring Boot 2.X 及相关技术栈开发。

[paascloud-master](https://link.zhihu.com/?target=https%3A//github.com/paascloud/paascloud-master)：基于 spring cloud + vue + oAuth2.0，前后端分离商城系统

[mall-swarm](https://link.zhihu.com/?target=https%3A//github.com/macrozheng/mall-swarm)：mall-swarm 是一套微服务商城系统，采用了 Spring Cloud Greenwich、Spring Boot 2、MyBatis、Docker、Elasticsearch 等核心技术，同时提供了基于 Vue 的管理后台方便快速搭建系统。

[onemall](https://link.zhihu.com/?target=https%3A//github.com/YunaiV/onemall)：mall 商城，基于微服务的思想，构建在 B2C 电商场景下的项目实战。核心技术栈，是 Spring Boot + Dubbo 。未来，会重构成 Spring Cloud Alibaba 。

[litemall](https://link.zhihu.com/?target=https%3A//github.com/linlinjava/litemall)：又一个小商城。litemall = Spring Boot 后端 + Vue 管理员前端 + 微信小程序用户前端 + Vue 用户移动端。

[xmall](https://link.zhihu.com/?target=https%3A//github.com/Exrick/xmall)：基于SOA架构的分布式电商购物商城 前后端分离 前台商城:Vue全家桶 后台管理系统

[miaosha](https://link.zhihu.com/?target=https%3A//github.com/qiurunze123/miaosha)：秒杀系统设计与实现

[SecKill](https://link.zhihu.com/?target=https%3A//github.com/hfbin/Seckill)：基于 SpringBoot+Mybatis+Redis+RabbitMQ 秒杀系统

## **博客论坛**

[Mblog](https://link.zhihu.com/?target=https%3A//github.com/langhsu/mblog)：开源 Java 博客系统

[halo](https://link.zhihu.com/?target=https%3A//github.com/halo-dev/halo)：一个优秀的开源博客发布应用

[forum-java](https://link.zhihu.com/?target=https%3A//github.com/Qbian61/forum-java)：一款用 Java（spring boot） 实现的现代化社区（论坛/问答/BBS/社交网络/博客）系统平台

[vhr](https://link.zhihu.com/?target=https%3A//github.com/lenve/vhr)：微人事是一个前后端分离的人力资源管理系统，项目采用 SpringBoot+Vue 开发。

[favorites-web](https://link.zhihu.com/?target=https%3A//github.com/cloudfavorites/favorites-web):云收藏 Spring Boot 2.X 开源项目。云收藏是一个使用 Spring Boot 构建的开源网站，可以让用户在线随时随地收藏的一个网站，在网站上分类整理收藏的网站或者文章。

[community](https://link.zhihu.com/?target=https%3A//github.com/codedrinker/community)：码问，开源论坛、问答系统，现有功能提问、回复、通知、最新、最热、消除零回复功能。技术栈 Spring、Spring Boot、MyBatis、MySQL/H2、Bootstrap

[NiterForum](https://link.zhihu.com/?target=https%3A//github.com/yourkevin/NiterForum)：尼特社区-NiterForum-一个论坛/社区程序。后端Springboot/MyBatis/Maven/MySQL，前端Thymeleaf/Layui。可供初学者，学习、交流使用。

[VBlog](https://link.zhihu.com/?target=https%3A//github.com/lenve/VBlog)：V部落，Vue+SpringBoot实现的多用户博客管理平台!

[NiceFish](https://link.zhihu.com/?target=https%3A//github.com/damoqiongqiu/NiceFish)：SpringBoot/SpringCloud 前后端分离项目

[My-Blog](https://link.zhihu.com/?target=https%3A//github.com/ZHENFENG13/My-Blog)： My Blog 是由 SpringBoot + Mybatis + Thymeleaf 等技术实现的 Java 博客系统，页面美观、功能齐全、部署简单及完善的代码，一定会给使用者无与伦比的体验。

[My-Blog-layui](https://link.zhihu.com/?target=https%3A//github.com/ZHENFENG13/My-Blog-layui)：layui 版本的 My-Blog : A simple & beautiful blogging system implemented with spring-boot & layui & thymeleaf & mybatis My Blog 是由 SpringBoot + Layui + Mybatis + Thymeleaf 等技术实现的 Java 博客系统，页面美观、功能齐全、部署简单及完善的代码，一定会给使用者无与伦比的体验

[symphony](https://link.zhihu.com/?target=https%3A//github.com/88250/symphony)：Java 实现的现代化社区

## **管理系统**

[Spring-Cloud-Admin](https://link.zhihu.com/?target=https%3A//github.com/wxiaoqi/Spring-Cloud-Admin)：Cloud-Admin 是国内首个基于 Spring Cloud 微服务化开发平台，具有统一授权、认证后台管理系统，其中包含具备用户管理、资源权限管理、网关 API 管理等多个模块，支持多业务系统并行开发，可以作为后端服务的开发脚手架。代码简洁，架构清晰，适合学习和直接项目中使用。核心技术采用 Spring Boot2 以及 Spring Cloud Gateway 相关核心组件，前端采用 vue-element-admin 组件。

[bootshiro](https://link.zhihu.com/?target=https%3A//github.com/tomsun28/bootshiro)：基于 springboot+shiro+jwt 的资源无状态认证权限管理系统后端

[悟空CRM](https://link.zhihu.com/?target=https%3A//github.com/72crm/72crm-java)：基于jfinal+vue+ElementUI的前后端分离CRM系统

[EL-ADMIN](https://link.zhihu.com/?target=https%3A//github.com/elunez/eladmin)：基于 SpringBoot 的后台管理系统

[pig](https://link.zhihu.com/?target=https%3A//gitee.com/log4j/pig)：基于 Spring Boot 2.2、 Spring Cloud Hoxton & Alibaba、 OAuth2 的 RBAC 权限管理系统。

[FEBS-Shiro](https://link.zhihu.com/?target=https%3A//github.com/wuyouzhuguli/FEBS-Shiro)：Spring Boot 2.1.3，Shiro1.4.0 & Layui 2.5.4 权限管理系统。

[Spring Boot-Shiro-Vue](https://link.zhihu.com/?target=https%3A//github.com/Heeexy/SpringBoot-Shiro-Vue)：基于Spring Boot-Shiro-Vue 的权限管理

[studentmanager](https://link.zhihu.com/?target=https%3A//github.com/ZeroWdd/studentmanager)：基于springboot+mybatis学生管理系统

[jshERP](https://link.zhihu.com/?target=https%3A//github.com/jishenghua/jshERP)：华夏ERP基于SpringBoot框架和SaaS模式，立志为中小企业提供开源好用的ERP软件，目前专注进销存+财务功能。主要模块有零售管理、采购管理、销售管理、仓库管理、财务管理、报表查询、系统管理等。支持预付款、收入支出、仓库调拨、组装拆卸、订单等特色功能。拥有库存状况、出入库统计等报表。同时对角色和权限进行了细致全面控制，精确到每个按钮和菜单。

[HotelSystem](https://link.zhihu.com/?target=https%3A//github.com/misterchaos/HotelSystem)：酒店管理系统 Java,tomcat,mysql,servlet,jsp实现，没有使用任何框架

## **其他**

[学之思在线考试系统](https://link.zhihu.com/?target=https%3A//github.com/mindskip/xzs)：一款 java + vue 的前后端分离的考试系统

[PassJava-Platform](https://link.zhihu.com/?target=https%3A//github.com/Jackson0714/PassJava-Platform)：一款面试刷题的 Spring Cloud 开源系统

[kkFileView](https://link.zhihu.com/?target=https%3A//github.com/kekingcn/kkFileView)：使用spring boot打造文件文档在线预览项目

[dynamic-datasource](https://link.zhihu.com/?target=https%3A//github.com/baomidou/dynamic-datasource-spring-boot-starter)：一个基于springboot的快速集成多数据源的启动器

[moti-cloud](https://link.zhihu.com/?target=https%3A//github.com/373675032/moti-cloud)：莫提网盘，基于 SpringBoot+MyBatis+ThymeLeaf+BootStrap，适合初学者

[threadandjuc](https://link.zhihu.com/?target=https%3A//github.com/qiurunze123/threadandjuc)：three-high-import 高可用\高可靠\高性能，三高多线程导入系统（该项目意义为理论贯通)

[proxyee-down](https://link.zhihu.com/?target=https%3A//github.com/proxyee-down-org/proxyee-down)：http下载工具，基于http代理，支持多连接分块下载

[hosp_order](https://link.zhihu.com/?target=https%3A//github.com/sfturing/hosp_order)：医院预约挂号系统，基于 SSM 框架

[趋势投资 SpringCloud](https://link.zhihu.com/?target=https%3A//how2j.cn/module/170.html)

[DiyTomcat](https://link.zhihu.com/?target=https%3A//how2j.cn/module/176.html)