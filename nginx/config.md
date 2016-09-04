# Nginx安装配置

### 安装

**mac**

`brew install nginx`

### 命令

**1. 启动**

`nginx -c /usr/local/etc/nginx/nginx.conf`

**2. 平滑重启**

`nginx -s reload`

### 配置

```
// mac配置文件路径
/usr/local/etc/nginx/nginx.conf
```

```
# 引入其他配置文件，通常可以用来将配置按模块拆分
include  /usr/local/etc/nginx/conf/papi.conf;

# server配置
server {
    # 端口
    listen          80;
    # 访问host
    server_name     local.baidu.com;
    location / {
        # 转发到其他服务
        proxy_pass http://127.0.0.1:8086;
        # 根目录
        root   /home/www;
        # 默认文件
        index  index.html index.htm;
    }
}

# Content-Type 配置
http {
    # mime配置文件
    include /usr/local/etc/nginx/mime.types;
}

types {
    text/html  html;
    application/json json;
}
```
