---
title: about
date: 2021-01-07 15:35:35
---

## 基本资料
- 姓名：刘先生
- 电子邮箱：ruyiliuchild@gmail.com

## 技能
1. 非常熟练使用Java编程语言，IntelliJ IDEA工具，深入理解OOP编程思想；
2. 非常熟练搭建和使用SpringBoot+SpringCloud+MybatisPlus(SpringdataJPA)等开源框架来进行JavaWeb开发，熟悉微服务架构，熟悉Spring底层源码及实现；
3. 熟练使用JaveScript，Ajax，jQuery等前台开发技术，熟练使用和进一步封装常用的js插件；
4. 熟练使用git/svn，maven/gradle命令来进行项目管理和项目构建，熟练使用禅道来进行项目开发管控；
5. 熟练使用Linux，熟练编写shell脚本，拥抱开源，有个人博客网站作为平时开发经验的分享；
6. 熟悉MySQL关系型数据库，熟悉分库分表技术，掌握SQL语言，熟悉redis缓存技术的使用；
7. 熟悉消息中间件Rabbitmq使用，有大型高并发网站设计经验，能根据业务需求选择合适的稳定技术；
8. 良好的表达与沟通能力，能快速融入团队，积极主动，对工作尽心尽责；
9. 熟练使用draw.io绘制流程图和脑图，使用网易云笔记来做团队间技能分享；
10. 熟练使用python编程语言，熟练搭建django框架来进行pythonWeb开发；
11. 熟悉爬虫技术，熟练使用python和java进行网站信息的爬取。

## 项目
### TMS
#### 项目描述：
运输管理系统（Transportation Management System，TMS）是一套基于运输作业流程的管理系统，该系统以系统管理、信息管理、运输作业、财务管理四大线索设计开发。  
系统管理是TMS系统的技术后台，起到支持系统高效运转的作用；信息管理是通过对企业的客户信息、车辆信息、人员信息、货物信息的管理，建立运输决策的知识库，也起到促进企业整体运营更加优化的作用；运输作业是该管理系统的核心，系统通过对运输任务的订单处理、调度配载、运输状态跟踪，确定任务的执行状况；财务管理是伴随着运输任务发生的应收应付费用，通过对应收应付的管理及运输任务对应的收支的核算，生成实时全面的统计报表，能够有效地促进运输决策。
#### 技术及框架：
JavaScript+Jquery+BootStrap  
SpringBoot+SpringCloud+SpringDataJPA+Redis+Jsoup+easypoi+Quartz  
MySQL+Mycat  
Git+Maven  
Centos+shell脚本
#### 责任描述：
1. 系统需求分析，搭建微服务架构开发环境,放入码云使用git进行版本控制
2. 爬虫爬取全国行政区域:根据甲方反应行政区域更新不及时及难以维护的问题进行解决.物流行业对行政区域极为敏感,鉴于维护耗时耗力,采用爬虫爬取国家行政区域的方法解决问题
3. 系统整体问题的统一解决:  
   (1). 现spring提供的定时任务调度无法在系统崩溃重启后进行之前保存的定时任务,根据此问题作出相应的解决方案;  
   (2). 系统启动时必要缓存的统一刷新;  
   (3). Java事件的监听  
   (4). 测试发现搜索等功能通过前台影响后台sql,springdatajpa框架封装的部分方法无法进行安全检测,根据测试问题统一解决.
4. 编写shell脚本,方便版本升级及测试
5. 根据架构师分解的模块通过禅道给开发分配具体任务
6. 带新员工熟悉项目及开发日常问题的解决
### OMS

### IDEA禅道插件
#### 项目描述：
编写此插件主要是为了方便开发人员使用禅道来做任务管理和Bug处理,禅道为开源项目。  
[此项目为开源项目](https://gitee.com/herolxl/zentao)
#### 技术及框架：
Java+jsoup+fastjson+datepicker  
禅道  
Intellij IDEA
#### 责任描述:
1. 使用爬虫来获取禅道的基本信息,开发人员的当前任务和当前Bug
2. 对用户账号密码的保存及用户的持续保持登录
3. 通过爬虫来进行任务的新增,开始,暂停,继续,取消
4. 通过爬虫来进行Bug的开始,完成,驳回



























