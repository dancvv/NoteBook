# mongoDB学习日记

mongod.conf文件

![image-20211020194512852](mongoDB.assets/image-20211020194512852.png)

## MongoDB卸载

linux下的卸载命令

1.停止 mongodb服务

`sudo service mongod stop`

2.卸载mongodb

`sudo apt-get remove mongodb`

3.移除相关包

```
sudo apt-get purge mongodb-org*

sudo apt-get purge mongodb

sudo apt-get autoremove

sudo apt-get autoclean
```

4.移除相关目录

```
sudo rm -r /var/log/mongodb
sudo rm -r /var/lib/mongodb
```

5.查看系统还有哪些残留的文件或目录

```
whereis mongo

whereis mongodb

whereis mongod

which mongo

which mongodb

which mongod
```

# Docker

![image-20211020203023234](mongoDB.assets/image-20211020203023234.png)

![image-20211020203038735](mongoDB.assets/image-20211020203038735.png)

Dockfile 自动化脚本

### 配置

windows下mongodb安装需要在bin同级目录下创建data文件夹

利用cmd将mongod.exe与data文件夹创建关联

```
mongod -dbpath=..\data\db
```

 使用shell链接

```
mongo --host=localhost --port=27017
```

#### linux安装

### 创建数据和日志目录。

创建一个目录，MongoDB实例将在该目录中存储其数据。例如：

```
sudo mkdir -p /var/lib/mongo
```

创建一个目录，MongoDB实例将在该目录中存储其日志。例如：

```
sudo mkdir -p /var/log/mongodb
```

启动MongoDB进程的用户必须具有对这些目录的读写权限。例如，如果您打算自己运行MongoDB：

```
sudo chown `whoami` /var/lib/mongo     # Or substitute another user
sudo chown `whoami` /var/log/mongodb   # Or substitute another user
```

#### 问题解决

出现`mongod.service: Failed with result 'exit-code'.`问题解决方法

新建两个目录

```
sudo mkdir /var/lib/mongodb
sudo mkdir /var/log/mongodb
```

改变拥有属性

```
sudo chown -R mongodb:mongodb /var/lib/mongodb
sudo chown -R mongodb:mongodb /var/log/mongodb
```

### 使用

```
use 数据库名
没有的话会自动创建

展示当前数据库
db

展示数据库
show dbs or database

```

admin：用户数据权限

local：

#### 删除

删除数据库`db.dropDatabase`

#### 集合

显示创建

```
db.createCollection("my")
```

##### 集合删除

````
db.my.drop()
````

##### 集合插入

使用insert和save语句插入

```
db.集合名.insert
如果没有集合名会隐式的创建
插入成功
WriteResult({ "nInserted" : 1 })
```

批量插入

```
db.集合名.insertMany([
	{},
	{}.
])
类似json数组

```



##### 集合查询

```mongo
查询所有
db.集合名.find()
查询单个
db.集合名.find({aritcle:"1000"})
```

查询第一条数据，{}中写入要查询的数据

```
db.comment.findOne({articleid:"10001"})
```

#### 投影查询

我们对文档进行查询并不是需要所有的字段, 比如只需要 id 或者 用户名, 我们可以对文档进行“投影”

`db.commnet.find({article:id},{article:1})`表示只显示改行，`db.commnet.find({article:id},{article:1，_id:0})`表示排除主键

批量插入文档时，为了防止某一条数据插入错误，无法定位错误源。使用try/catch解决

主键id一般不自己生成

```
try{
db.集合名.insertMany(
	{},
	{},
	{}
	)
}catch(e){
	print(e)
}

try {
  db.comment.insertMany([
    {"_id":"1","articleid":"100001","content":"我们不应该把清晨浪费在手机上, 健康很重要, 一杯温水幸福你我 他.","userid":"1002","nickname":"相忘于江湖","createdatetime":new Date("2019-0805T22:08:15.522Z"),"likenum":NumberInt(1000),"state":"1"},
    {"_id":"2","articleid":"100001","content":"我夏天空腹喝凉开水, 冬天喝温开水","userid":"1005","nickname":"伊人憔 悴","createdatetime":new Date("2019-08-05T23:58:51.485Z"),"likenum":NumberInt(888),"state":"1"},
    {"_id":"3","articleid":"100001","content":"我一直喝凉开水, 冬天夏天都喝.","userid":"1004","nickname":"杰克船 长","createdatetime":new Date("2019-08-06T01:05:06.321Z"),"likenum":NumberInt(666),"state":"1"},
    {"_id":"4","articleid":"100001","content":"专家说不能空腹吃饭, 影响健康.","userid":"1003","nickname":"凯 撒","createdatetime":new Date("2019-08-06T08:18:35.288Z"),"likenum":NumberInt(2000),"state":"1"},
    {"_id":"5","articleid":"100001","content":"研究表明, 刚烧开的水千万不能喝, 因为烫 嘴.","userid":"1003","nickname":"凯撒","createdatetime":new Date("2019-0806T11:01:02.521Z"),"likenum":NumberInt(3000),"state":"1"}

]);

} catch (e) {
  print (e);
}
```

#### 文档的更新

语法

```
db.集合名.update({query},{update},options)
db.commnet.update()
```

覆盖性更新

这种更新方式会覆盖该条件下所有的数据项

```
 db.comment.update({_id:"1"},{userid:NumberInt(10)})
```

局部更新，只更新那一条数据

```
 db.comment.update({_id:"2"},{$set:{userid:NumberInt(10)}})
```

批量修改数据

更新所有查询数据

```
db.comment.update({userid:"1003"},{$set:{nickname:"list"}},{multi:true})
```

**列值增长修改**

如果我们想实现对某列值在原有值的基础上进行增加或减少, 可以使用 `$inc` 运算符来实现

```
db.comment.update({_id:"3"},{$inc:{likenum:NumberInt(1)}})
```

**删除文档**

```
db.集合名.remove(选项)
删除某一项
```

### 文档的分页查询

1. 统计所有记录数

```
db.集合名.count()
```

2. 按条件统计记录数

```
db.集合名.count({条件})
```

3. 分页列表查询

`db.comment.find({},{userid:"1003"})`其中find({},{条件})会限制其他条件的出现，导致仅出现userid这一个

仅显示前几条数据

```
db.集合名.find().limit(数字)
```

skip方法，跳过查询出来所有的n条数据

```
db.集合名.find().limit(数字).skip(n)
```

4. 排序查询

`db.集合名.find().sort({userid:1})`查询出来的数据，按照userid进行升序排列，1表示升序，0表示降序排列

##### 正则查询

```
db.集合名.find({content:/开水/})
后面紧跟着正则查询
```

##### 比较查询

```
db.集合名.find({field:{$gt:value}}) //大于：field>value
```

##### 包含查询

查询评论的集合中userid字段包含1003或1004的文档id in{1,2,3}

`db.comment.find({userid:{$in:["1003","1004"]}})`

不包含使用`$nin`操作符，查询出的结果不包含这几个文档

##### 连接查询

```
db.comment.find({$and:[{条件1}，{条件2]})
db.集合名.find($and:[{likenum:{$gte:NumberInt(700)}},{likenum:{$lt:NumberInt(2000)}}])
```

#### 常用小结

![image-20211023205540383](mongoDB.assets/image-20211023205540383.png)

### 索引

![image-20211023205803111](mongoDB.assets/image-20211023205803111.png)

#### 索引的查看

返回一个集合中的所有索引的数组。

```
db.集合名.getIndexes()
```

![image-20211023210426956](mongoDB.assets/image-20211023210426956.png)

_id:表示升序

#### 创建索引

```
db.集合名.createIndex(keys,options)
```

![image-20211023210615527](mongoDB.assets/image-20211023210615527.png)

单字段索引示例

```
db.comment.createIndex({userid:1})
建立一个升序的索引
```

![image-20211023211039243](mongoDB.assets/image-20211023211039243.png)

##### 索引的删除

![image-20211023211153302](mongoDB.assets/image-20211023211153302.png)

```
db.集合名.dropIndex(index)
删除userid的升序索引
db.comment.dropIndex({userid:1})
删除所有索引
db.comment.dropIndexes()
```

