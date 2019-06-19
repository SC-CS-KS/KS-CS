# Cookie 分流
## 场景
* 测试环境隔离

## 配置
***group.conf***
```md
	map $COOKIE_username $group {
    chenguangsunnychan chenguang;
    zhujiahui chenguang;
    anfengxiang_i chenguang;

    default default_group;
}
```
***upstream.conf***
```md
	upstream chenguang_8541 {
    server 127.0.0.1:8545;
}

upstream chenguang_8542 {
    server 127.0.0.1:8546;
}

upstream default_group_8541 {
    server 127.0.0.1:8547;
}

upstream default_group_8542 {
    server 127.0.0.1:8548;
}
```
***servers/dps_report_rest.conf***
```md
	server {
    listen 8541;
    server_name bigdata-test.xiaojukeji.com;

    location / {
        proxy_pass "http://${group}_8541";
        proxy_set_header Host $host:$server_port;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

server {
    listen 8542;
    server_name bigdata-test.xiaojukeji.com;

    location / {
        proxy_pass "http://${group}_8542";
        proxy_set_header Host $host:$server_port;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```