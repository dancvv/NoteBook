# Jenkins

主要讲述Jenkins+SVN

使用Jenkins apt安装

```
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-get install jenkins
```

# Jenkins+SVN

需要三台机器

`rpm -ql jenkins`

启动Jenkins

`systemctl start jenkins`

查看进程

`ps -ef|grep jenkins`

查看端口

`netstat -antp 8080`

安装完成之后，打开8080端口网页，按照提示输入密码，密码存储在本地日志中

进入之后开始默认安装插件

```
管理密码
wangblack
Mountain
```

MasterSlave

