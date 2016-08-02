---
layout: post
title: "MongoDB 权限管理 - 用户管理"
date: 2016-08-02 19:00:00 +0800
categories: MongoDB
---

说明：由于 MongoDB 2.x 和 MongoDB 3.x 在用户管理上一些差别，本文所描述的内容只针对 MongoDB 3.x，默认的操作都是在本机完成，所以 MongoDB 的端口为默认的 27017。

MongoDB 服务在启动的时候，默认是没有开启权限认证的，如果需要开启这一功能，可以在启动服务的时候添加 --auth 参数，即：

```
./mongod --auth --dbpath xxx
```

当然，如果你之前没有添加过用户，启动 MongoDB 服务的时候带上 ```--auth``` 参数是没有任何意义的，因为 MongoDB 默认并不存在任何内置的用户，所以一切的操作都需要由你自己来完成。

### 创建用户

由于 MongoDB 并没有提供默认用户，所以在开启权限认证之前，应该至少创建一个拥有```用户管理角色```的用户，首先以无权限认证启动 MongoDB :
 
```
./mongod --dbpath xxx # 注意，不能带上 --auth 参数。
```

打开 MongoDB shell

```
./mongo
```

切换到 admin 数据库（如果你是一个全新的环境，这时候应该是没有 admin 这个数据库的）

```
> use admin # 切换到 admin 数据库
```

使用 db.createUser() 命令创建用户，该命令需要两个参数，第一个参数为 user ，第二个为 writeConcern，是可选的，在此不作介绍。

user 参数为 MongoDB 的文档类型，其主要有 user、pwd、customData、roles 几个字段。

* user: 用户名
* pwd: 密码
* customData: 自定义数据，MongoDB 文档类型，主要存放一些自定义的信息，对权限认证不影响。
* roles: 角色列表，该用户拥有的角色。

下面我们创建一个用户名和密码都为 admin 的用户，其拥有管理所有数据库用户的权限:

```
> db.createUser({
    user: "admin",
	 pwd: "admin", 
	 roles:[
	  {role: "userAdminAnyDatabase", db:"admin"}
	 ]
	})
  Successfully added user: {
	"user" : "admin",
	"roles" : [
		{
			"role" : "userAdminAnyDatabase",
			"db" : "admin"
		}
	]
}
```

如果创建用户成功，shell 将会返回 Successfully added user 的信息。

至此，我们已经成功创建了一个拥有管理所有数据库用户权限的用户 - admin。

### 权限验证

成功创建用户之后，我们想要验证刚刚创建的用户是否可用，这时候可以关闭 MongoDB 服务:

```
> use admin
> db.shutdownServer()
```

然后带上 ```--auth``` 参数重新启动 MongoDB 服务。

```
./mongod --auth --dbpath xxx
```

重新打开 shell，这时候在 shell 中执行```show dbs```命令，会提示```not authorized on admin to execute command ```的错误，证明成功开启了权限认证。

这时候我们需要切换到 admin 数据库，并执行认证操作：

```
> use admin
> db.auth("admin", "admin")
1
```

如上所示，如果用户验证成功，会返回信息```1```，否则将返回 ```Error: 18 Authentication failed.```

这时候执行 ```show users ``` 命令，将会看到在该库下面的所有用户信息。当然，你也可以使用 ```db.getUser(username)``` 来查看指定信息。

### 用户管理

现在我们已经能够创建用户，并且也成功验证通过，接下来了解一下 MongoDB 的用户管理。

在前面的示例中，我们执行 db.createUser() 命令的时候，需要切换到 admin 数据库下面，当我们执行 db.auth() 命令的时候，也需要先切换到 admin 数据库下面。

现在我们继续切换到数据库 admin，然后执行 show users 命令：

```
> use admin
> show user
{
	"_id" : "admin.admin",
	"user" : "admin",
	"db" : "admin",
	"roles" : [
		{
			"role" : "userAdminAnyDatabase",
			"db" : "admin"
		}
	]
}
```

我们看到了 admin 数据库中所有的用户信息（当然目前只有 admin 这一个用户），用户文档中有一个 db 字段，该字段决定了用户所处的库，即我们需要连接那一库来进行授权验证。role 文档也有一个 db 字段，该字段决定了这个角色针对的数据库是那一个，即该角色管理的数据库。请看下面的例子：

```
>use db1
>db.createUser({
    user:"user1", 
    pwd:"user1", 
    roles:[
     {role:"readWrite", db:"db1"}
     ]
    })
```

执行上述命令之后，我们成功在数据库 db1 中创建了一个拥有对数据库 db2 读写权限的用户 user1。

如何验证？

这时候可以切换到 db2，执行```show collections```命令，会收到 ```not authorized on db2 to execute command```错误，证明我们对 db2 是没有访问权限的。

我们直接在 db2 中执行 ```db.auth("user1", "user1")```命令，也会收到```Error: 18 Authentication failed.```验证失败的错误。

我们切换到 db1，然后执行```db.auth("user1", "user1")```命令，ok，这时候 shell 输出了```1```，我们再切换到 db2，执行```show collections```命令，虽然没有返回任何信息，因为目前没有任何集合，但是我们没有收到任何错误信息，这证明了我们之前所说的是正确的。

但是我们在 db1 中执行```db.system.users.find()``` 没有返回任何信息，这是因为所有的用户信息都是保存在数据库 admin 的 users 集合中。

```
> use admin
> db.system.users.find()
{ "_id" : "admin.admin", "user" : "admin", "db" : "admin", "credentials" : { "SCRAM-SHA-1" : { "iterationCount" : 10000, "salt" : "1Q2n4wdefLOe6ePTJI3N/A==", "storedKey" : "/rD3Bqu1pgFGzx9TGP0KEmBaN6I=", "serverKey" : "MNSw9ONNgfIgHzVzNxgveO7/ONc=" } }, "roles" : [ { "role" : "userAdminAnyDatabase", "db" : "admin" } ] }
{ "_id" : "db1.user1", "user" : "user1", "db" : "db1", "credentials" : { "SCRAM-SHA-1" : { "iterationCount" : 10000, "salt" : "QtPEcTSjWsXABRtmDHO5MQ==", "storedKey" : "Opep1Hu5TICKfJN1+mzc08JI7tA=", "serverKey" : "9Cyc3YWDNETgiuum01JaTCPnghg=" } }, "roles" : [ { "role" : "readWrite", "db" : "db2" } ] }
```

可以看到我们刚才创建的两个用户信息。

MongoDB 的用户管理是随着库走的，即在哪一个库下面执行了创建用户的命令，就需要在哪一个库下面执行授权验证的操作，所以在创建用户和授权验证的时候，千万别搞错了库。 

### 修改用户信息

#### db.updateUser(username, update, writeConcern)
修改指定用户的信息。

* username 为要修改的用户的用户名。
* update 文档类型，需要修改的信息，有 customData、roles、pwd 字段。

#### db.grantRolesToUser(username, roles, writeConcern)
把角色授权给指定的用户。

#### db.revokeRolesFromUser(username, roles, writeConcern)
取消对用户的角色授权。

#### db.changeUserPassword(username, password)
修改指定用户的密码。

### 删除用户
#### db.dropUser(username, writeConcern)
从当前的数据库中删除指定的用户。

#### db.dropAllUsers(writeConcern)
从当前的数据库中删除所有的用户。
