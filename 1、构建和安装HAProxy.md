# 1、构建和安装HAProxy

假设我们在ubuntu平台，需要安装以下依赖：

```bash
sudo apt update
sudo apt install build-essential libssl-dev libpcre3-dev zlib1g-dev
```

然后就可以编译HAProxy了：

```bash
cd haproxy-3.0.0
make TARGET=linux-glibc
```

安装HAProxy：

```bash
sudo make install
```

haproxy会被安装在/usr/local/sbin/
