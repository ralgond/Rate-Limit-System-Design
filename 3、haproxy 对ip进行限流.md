# 3、haproxy 对ip进行限流

在 HAProxy 中对IP进行限流，可以使用 stick-table。以下是一个示例配置，限制对每个 IP 每秒10s最多 3 个请求。

```
frontend http_front
    bind *:8001

    # 定义 stick-table，存储每个源 IP 的请求计数
    stick-table type ip size 1m expire 60s store http_req_rate(10s)
    http-request track-sc0 src  # 跟踪源 IP
    http-request deny deny_status 429 if { sc_http_req_rate(0) gt 3 }  # 超过限制返回 429

    default_backend http_back

backend http_back
    server server1 192.168.1.10:80
    server server2 192.168.1.11:80
```

参考文献：

https://www.haproxy.com/blog/four-examples-of-haproxy-rate-limiting#setting-the-maximum-connections
