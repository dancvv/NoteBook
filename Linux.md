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

