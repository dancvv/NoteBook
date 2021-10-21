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

