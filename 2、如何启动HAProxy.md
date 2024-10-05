# 2、如何启动HAProxy

添加用户haproxy
```bash
sudo useradd -s /bin/bash -d /home/haproxy -m haproxy
```

创建配置文件/home/haproxy/haproxy.cfg，haproxy.cfg的内容如下
```
global
    log /dev/log local0
    maxconn 2000
    user haproxy
    group haproxy
    daemon

defaults
    log global
    mode http
    option httplog
    timeout connect 5000ms
    timeout client 50000ms
    timeout server 50000ms

frontend http_front
    bind *:8001
    default_backend http_back

backend http_back
    server server1 localhost:80 maxconn 100
```

启动haproxy：
```bash
sudo haproxy -f /home/haproxy/haproxy.cfg
```
