# 杨烽 的个人简历

Github: [http://github.com/smartwalle](http://github.com/smartwalle)


## 基本信息

* 杨烽 / 男 / 1988
* 大专 / 计算机网络 / 成都大学
* 互联网从业时间: 2009年12月 ～ 至今
* 期望职位: Go 开发工程师
* 期望城市: 成都、深圳

## 联系方式

* 手机号码: <a href="tel:18180103029">181 8010 3029</a>
* 电子邮箱: <smartwalle@gmail.com>
* 微信: smartwalle

## 工作经历

### 深圳市艾维普思科技有限公司 (SMOK) (2014.03 ~ 至今)

#### SMOK 电子商务平台

SMOK 电子商务平台包含两个部分，一个是针对分销商的 [B2B](https://order.smoktech.com/) 平台，另一个是针对 C 端用户的 [B2C](https://store.smoktech.com/) 平台。

电商平台主要包含订单、客户、商品、库存、财务、业务员、权限、配送等模块；

本项目是基于 [Gin](https://github.com/gin-gonic/gin) 来构建的，数据库采用的是 MySQL、缓存用的是 Redis。

B2B 的订单处理流程：

1. 客户通过 B2B 站点进行下单；
2. 跟单人员进行审单，并发订金付款申请书；
3. 客户提交银行水单记录；（由于涉及到的金额比较大，所以分销用户都是经银行转账）
4. 财务人员进行入账审核（可选）；
5. 跟单人员进行订金分账；
6. 财务人员进行分账审核；
7. 工厂收到订单并进行生产；
8. 工厂生产完成，生成发货单；
9. 客户收到通知，支付尾款；
10. 跟单人员进行尾款分账；
11. 财务人员进行分账审核；
12. 仓库发货；

B2C 的订单处理处理流程：

1. 客户通过 B2C 站点进行下单；
2. 客户进行在线支付，在线支付采用的是 PayPal；
3. 财务人员进行财务审核；
4. 客服人员导出发货单，将发货单导入 U8 系统；
5. 工厂发货；

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

## Go 开源项目
* [dbs] (https://github.com/smartwalle/dbs)
	
	一个 SQL 拼接库，本人在实际项目中没有采用 ORM 框架，所以实现了一个 SQL 拼接库，能够很直观地进行 SQL 拼接，比如：

```
var sb = NewSelectBuilder()
sb.Selects("u.id", "u.age")
sb.Select(Alias("CONCAT(u.last_name, u.first_name)", "name"))
sb.Select("ue.email")
sb.From("user", "AS u")
sb.LeftJoin("user_email", "AS ue ON ue.user_id=u.id")
fmt.Println(sb.ToSQL())
```
如要阅读代码，建议查看 v4 分支。

* [dbr] (https://github.com/smartwalle/dbr)

	dbr 是 Redis 操作库 [redigo](github.com/garyburd/redigo/redis) 的一个扩展，封装了一些 Redis 操作命令，便于复用。

* [ngx] (https://github.com/smartwalle/ngx)

	ngx 是一个网络请求库。

* [pool4go] (https://github.com/smartwalle/pool4go)

	pool4go 是一个通用的连接池库，可以用于任何需要连接池的地方。

* [task4go] (https://github.com/smartwalle/task4go)

	task4go 是一个多任务管理库，实现对并发任务数量的控制。

* [log4go] (https://github.com/smartwalle/log4go)
	
	log4go 是一个日志库，可以将日志写入文件，自动进行日志文件的分隔、清理，并且可以设置邮件提醒。

* [form] (https://github.com/smartwalle/form)

	form 是一个将 http.Request 的 Form 数据映射到 Go struct 的库。

* [validator] (https://github.com/smartwalle/validator)
	
	validator 是一个数据验证库，实现该库的主要思想是自由，只提供接口，不提供验证具体格式的验证（比如验证是邮箱、手机号码）。

* [ini4go] (https://github.com/smartwalle/ini4go)

	ini4go 是一个 ini 格式的文件读取及写入库。

* [odin] (https://github.com/smartwalle/odin)
	
	odin 是一个基于 redis 的权限管理库。

* [支付宝 SDK For Go](https://github.com/smartwalle/alipay)
* [PayPal SDK For Go] (https://github.com/smartwalle/paypal)
* [微信支付 SDK For Go] (https://github.com/smartwalle/wxpay)

## 教育经历

2008.09 ～ 2010.07 成都大学 计算机网络专业

## 自我评价

2009年参加工作，从事 Flex 开发。从2011年开始接触 iOS 应用开发，能够独立完成 App 的开发，有多款成功上线的应用，拥有比较丰富的移动应用开发经验。日常接触的事情主要包括与客户沟通、需求整理、功能梳理、原型图、开发团队管理以及编码。为人比较随和，有很强的自制能力，能够自我驱动进行工作、学习。有较强的团队意识，能够与团队成员共同努力，出色地完成任务。目前主要投身于 iOS 和 Go 开发。

## 专业技能
* 熟练掌握 Objective-c 开发语言、iOS SDK, 能够快速进行 iOS App 的开发及发布。
* 熟练使用 iOS 开发工具 Xcode, 能够使用代码或者 Interface Builder 进行页面布局，熟悉内存检测工具 Instruments 的使用。
* 熟悉 iOS 平台上 BLE(Bluetooth low energy, 低功耗蓝牙) 开发，并有多款成功上线项目经验。
* 熟练使用 Go 进行服务器端接口开发，对于 Go 也累积了一套常用的工具类库，并有成功上线运行项目。
* 具有良好的编程风格，开发过程中不断的对功能进行测试，以保证应用的稳定性。
* 喜欢对开发过程中可复用的功能进行重新组织封装，以供其它项目使用。
* 能够在 Linux 下进行开发或者生产环境的配置。
* 使用 Redmine 进行项目管理。


