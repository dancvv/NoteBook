# Linux

### vi和vim

两个编辑器的快捷键一样

![image-20211002210317989](Linux.assets/image-20211002210317989.png)

三种操作模式



## clash配置

首先参照官方配置一个dameon

Copy Clash binary to `/usr/local/bin` and configuration files to `/etc/clash`:

```
$ cp clash /usr/local/bin
$ cp config.yaml /etc/clash/
$ cp Country.mmdb /etc/clash/
```

Create the systemd configuration file at `/etc/systemd/system/clash.service`:

```
[Unit]
Description=Clash daemon, A rule-based proxy in Go.
After=network.target

[Service]
Type=simple
Restart=always
ExecStart=/usr/local/bin/clash -d /etc/clash

[Install]
WantedBy=multi-user.target
```

Launch clashd on system startup with:

```
$ systemctl enable clash
```

Launch clashd immediately with:

```
$ systemctl start clash
```

Check the health and logs of Clash with:

```
$ systemctl status clash
$ journalctl -xe
```

#### 代理设置

由于服务器没有图形化界面，所以采用命令行配置全局代理

把代理服务器地址写入shell配置文件.bashrc或者.zshrc 直接在.bashrc或者.zshrc添加下面内容

把以下内容添加进去即可生效

```text
export http_proxy="http://localhost:port"
export https_proxy="http://localhost:port"
```

或者走socket5协议（ss,ssr）的话，代理端口是1080

```text
export http_proxy="socks5://127.0.0.1:1080"
export https_proxy="socks5://127.0.0.1:1080"
```

或者干脆直接设置ALL_PROXY

```text
export ALL_PROXY=socks5://127.0.0.1:1080
```

最后在执行如下命令应用设置

```text
source ~/.bashrc
```

#### 查看端口使用情况

已经连接的服务端口

`netstat -a`

查看所有的服务端口（LISTEN，ESTABLISHED）
`netstat -ap`
查看指定端口，可以结合grep命令：
`netstat -ap | grep 8080`
 也可以使用lsof命令：
`lsof -i:8888`
若要关闭使用这个端口的程序，使用kill + 对应的pid


`kill -9 PID号`

### 文件复制

#### 1、从本地复制到远程

命令格式：

```
scp local_file remote_username@remote_ip:remote_folder 
或者 
scp local_file remote_username@remote_ip:remote_file 
或者 
scp local_file remote_ip:remote_folder 
或者 
scp local_file remote_ip:remote_file 
```



- 第1,2个指定了用户名，命令执行后需要再输入密码，第1个仅指定了远程的目录，文件名字不变，第2个指定了文件名；
- 第3,4个没有指定用户名，命令执行后需要输入用户名和密码，第3个仅指定了远程的目录，文件名字不变，第4个指定了文件名；

应用实例：

```
scp /home/space/music/1.mp3 root@www.runoob.com:/home/root/others/music 
scp /home/space/music/1.mp3 root@www.runoob.com:/home/root/others/music/001.mp3 
scp /home/space/music/1.mp3 www.runoob.com:/home/root/others/music 
scp /home/space/music/1.mp3 www.runoob.com:/home/root/others/music/001.mp3
```

### 进程查看

`ps`指令

![image-20211005143811182](Linux.assets/image-20211005143811182.png)

三个指令组合使用

```
查看所有进程
ps -aux
grep 过滤用户
ps -aux | grep sshd
```

- user 进程执行用户
- PID 进程名
- MEM 占用物理内存的百分比
- STAT 运行状态， s表示sleep休眠，r表示run运行状态
- START 执行开始的时间
- TIME 占用的CPU时间
- command 进程名，执行该进程所用的命令和参数

![image-20211005144304591](Linux.assets/image-20211005144304591.png)

**父进程**

![image-20211005144528444](Linux.assets/image-20211005144528444.png)

可以有多个子进程

![image-20211005144611978](Linux.assets/image-20211005144611978.png)

```
ps -ef|grep sshd
```

**终止进程**

![image-20211005145118524](Linux.assets/image-20211005145118524.png)

```
kill 进程号，kill 11421
终止远程登录sshd
重启sshd
/bin/systemctl start sshd.service
终止所有gedit编辑器,通过进程名干掉所有子进程
killall gedit
强制终止
kill -9 进程号
```

