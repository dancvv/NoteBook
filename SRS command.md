# SRS

## 启动

````
sudo ./etc/init.d/srs stop
sudo ./etc/init.d/srs start
sudo ./etc/init.d/srs status
````

```
sudo ./objs/srs -c conf/srs.conf
```

flv分发

```
sudo ./objs/srs -c conf/http.flv.live.conf

sudo gedit conf/http.flv.live.conf
```



### flv文件

```
listen              1935;
max_connections     1000;
daemon              on;
http_server {
    enabled         on;
    listen          8080;
    dir             ./objs/nginx/html;
}
vhost __defaultVhost__ {

    http_remux {
        enabled     on;
        mount       [vhost]/[app]/[stream].flv;
        hstrs		on;
    }
}
```

### srs默认文件

```
listen              1935;
max_connections     1000;
srs_log_tank        file;
srs_log_file        ./objs/srs.log;
daemon              on;
http_api {
    enabled         on;
    listen          1985;
}
http_server {
    enabled         on;
    listen          8080;
    dir             ./objs/nginx/html;
}
vhost __defaultVhost__ {
    hls {
        enabled         on;
    }
    http_remux {
        enabled     on;
        mount       [vhost]/[app]/[stream].flv;
    }
}
```
