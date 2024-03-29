# 杨烽 的个人简历

Github: [https://github.com/smartwalle](https://github.com/smartwalle)

## 基本信息

* 杨烽 / 男 / 1988
* 大专 / 计算机网络 / 成都大学
* 互联网从业时间: 2009年12月 ～ 至今
* 期望职位: Go 开发工程师
* 期望城市: 成都

## 联系方式

* 手机号码: <a href="tel:18180103029">181 8010 3029</a>
* 电子邮箱: <smartwalle@gmail.com>
* 微信: smartwalle

## 工作经历(部分)

### 四川有乐信息技术有限公司 (2018.06 ~ 2024.02)

1. 统一开发框架和编码风格；
2. 公司源代码管理规范；
3. 优化项目管理和 Bug 管理流程；

#### 搓搓麻将

地方特色麻将手游，主要包含四川麻将、温岭麻将和黄岩麻将。在本项目中，我主要负责项目开发框架的搭建和非游戏对战功能的开发，包括但不限于商城、充值、签到、任务、福利、排行榜、邮件以及匹配等。

本项目采用微服务架构模式，基于 gRPC 框架开发，使用 ETCD 用于服务的注册与发现， NSQ 用于服务解耦和数据缓冲，MongoDB 用于数据持久化。

#### 圈本地

一款主打本地生活服务的小程序，用户通过小程序购买消费券然后到店进行消费。

本项目为一个电商项目，包含用户、商品、订单、支付、积分、物流、分销等功能。为了便于传播，用户端和商户端使用微信小程序平台作为载体，另提供管理后台作为各种信息的维护管理（商品、订单、账单）。

基于 Gin 框架构建，MySQL 用于数据持久化，数据库操作使用的是自研的工具，没有使用 ORM。

#### HotelDelins 酒店管理系统

主要分为酒店内务和房间预订两大板块，包含组织关系、内勤、房间、会员（企业用户和个人用户）、订单、工作流程等模块。

### 深圳市艾维普思科技有限公司 (SMOK) (2014.03 ~ 2018.05)

1. 从 0 开始组建公司的互联网研发团队；
2. 搭建公司电子商务平台，优化经销商下单流程；
3. 搭建公司产品防伪平台，用于帮助用户验证产品真伪;
4. 搭建公司 FAQ 平台，解决用户在使用产品过程中遇到的问题；

#### SMOK 电子商务平台

SMOK 电子商务平台包含两个部分，一个是针对分销商的 [B2B](https://order.smoktech.com/) 平台，另一个是针对 C 端用户的 [B2C](https://store.smoktech.com/) 平台。

电商平台主要包含订单、客户、商品、库存、财务、业务员、权限、配送等模块；

本项目是基于 Gin 框架构建，数据库采用的是 MySQL、缓存用的是 Redis。

#### SMOK 企业官网

* 英文版本：[https://www.smoktech.com](https://smoktech.com)
* 中文版本：[https://www.smoktech.cn](https://smoktech.cn)

SMOK 企业官网服务器端采用 Go 进行开发的，主要包含产品、新闻、售后服务、FAQ、防伪查询等模块。本项目是基于 [Gin](https://github.com/gin-gonic/gin) 来构建的，数据库采用的是 MySQL、缓存用的是 Redis、HTML 模板渲染用到的是 [Pongo2](https://github.com/flosch/pongo2)、静态文件存储用的是七年的云存储服务。

#### Vaping Tour (原 Smart BEC, 国内叫做蒸汽时光)

**项目介绍:** Vaping Tour 最开始是一款和蓝牙电子烟进行交互的 App，该 App 通过蓝牙4.0与电子烟进行通信，主要包含设置电子烟的工作参数、电子烟吸烟数据采集、吸烟健康管理、电子烟固件更新等等。
 
往后发展，加入了社交模块，使其成为了一个电子烟领域的垂直社交应用。社交模块包含话题、即时通信、电子烟评测等功能。

服务器端采用 Go 进行开发，数据库采用的是 MongoDB。含有用户、话题、电子烟设备、活动、评测、投票等等功能。

**责任描述:** 项目第一期负责 App 产品设计、需求设计和 iOS 端所有的开发工作。项目第二期主要负责服务器端接口开发、iOS 端开发和团队建设管理工作。

**下载地址:** [Vaping Tour (Smart BEC)](https://m.vapingtour.com)

## 主要开源项目
* [alipay - https://github.com/smartwalle/alipay](https://github.com/smartwalle/alipay)

	使用 Go  语言开发的开源项目，帮助开发者快速集成支付宝相关的功能 ，是目前 Go  社区中功能最完善、扩展最灵活的支付宝 SDK 。目前主要实现了电脑网页支付、手机网页支付、APP  支付、交易查询、退款、账单下载等接口。

* [dbs - https://github.com/smartwalle/dbs](https://github.com/smartwalle/dbs)

	一个 SQL 相关工具库，主要用于 sql.Stmt 的缓存管理、将查询结果和结构体对象进行映射和SQL语句拼接。

## 教育经历

2008.09 ～ 2010.07 成都大学 计算机网络专业

## 自我评价

于 2009 年参加工作，从事 Flex 开发，主要参与一个日本酒店前台预订系统的开发工作。从 2011 年开始接触 iOS 应用开发，能够独立完成 iOS 平台应用的开发，有多款成功上线的应用，拥有比较丰富的移动应用开发经验。于 2015 年开始接触 Go，然后逐渐投身 Go 相关的开发工作。日常接触的事情主要包括与客户沟通、需求整理、功能梳理、原型图、开发团队管理以及编码。有很强的自制能力，能够自我驱动进行工作。有较强的团队意识，能够与团队成员共同努力，出色地完成任务。

## 专业技能
* 熟练使用 Go 进行服务端应用开发，积累了一套常用的工具类库，并有多款成功上线运营的项目。
* 熟悉 MySQL、PostgreSQL、MongoDB、Redis 等常用数据库。
* 了解 ETCD、NSQ、 Kafaka 和 ElasticSearch 的基本使用。
* 熟悉基于 Gin 框架进行 API 接口开发，习惯手写 SQL。
* 熟悉常用设计模式并且加以运用，比如：策略模式、原型模式、工厂方法。
* 熟悉常用支付平台的对接，比如：支付宝、微信支付、银联支付、苹果支付。
* 可以使用 Flutter 进行网页应用程序和移动端应用程序开发。
* 具有良好的编程风格，开发过程中不断的对功能进行测试，以保证应用的稳定性。
* 喜欢对开发过程中可复用的功能进行重新组织封装，以供其它项目使用。
* 使用 Git 进行代码管理，Redmine 进行项目管理。