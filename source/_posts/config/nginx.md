---
title: nginx配置
date: 2021/2/23 20:13:56
tags: Config
categories: Config
---

### nginx.conf

```sh
user www-data;
worker_processes 4;
pid /run/nginx.pid;

events {
    worker_connections 65535;
    # multi_accept on;
    use epoll;
}

http {
    ##
    # Basic Settings
    ##
    sendfile on;
    tcp_nopush on;
    tcp_nodelay on;
    keepalive_timeout 65;
    types_hash_max_size 2048;
    # server_tokens off;

    # server_names_hash_bucket_size 64;
    # server_name_in_redirect off;

    include /etc/nginx/mime.types;
    default_type application/octet-stream;

    ##
    # Logging Settings
    ##
    log_format main '$remote_addr - $remote_user  [$time_local]  "$request" $status $body_bytes_sent "$http_referer" "$http_user_agent" "$request_body" $request_time "$upstream_response_time" $upstream_status';
    access_log /var/log/nginx/access.log;
    error_log /var/log/nginx/error.log;

    ##
    # Gzip Settings
    ##
    gzip on;
    gzip_disable "msie6";
    gzip_vary on;
    gzip_proxied any;
    gzip_comp_level 6;
    gzip_buffers 16 8k;
    gzip_http_version 1.1;
    gzip_types text/plain text/css application/json application/javascript application/x-javascript text/xml application/xml application/xml+rss text/javascript;
     
    include /etc/nginx/conf.d/*.conf;
    include /etc/nginx/sites-enabled/*;
}


```



---

```sh
server {
    listen      80;
    index       index.html index.htm;
    server_name dev-saas.dding.net;
    access_log  /var/log/nginx/dev-saas.dding.net.log;
    error_log   /var/log/nginx/dev-saas.dding.net.error.log warn;
    root        /home/gitlab-runner/saas-fe-3.0/dist/;
    
    charset     utf-8;
    client_max_body_size        16m;
    
    location / {
        expires 5m;
        try_files $uri $uri/ /index.html;
    }
    
    location /v3/ {
        proxy_pass http://127.0.0.1:7001/v3/;

    }
    
    location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$ {
        expires 30d;
    }
    
    location ~ .*\.(js|css)?$ {
        expires 7d;
    }
}
```

---


```sh
server {
    listen      80;
    index       index.html index.htm;
    server_name dev-manage.dding.net;
    access_log  /var/log/nginx/dev-manage.dding.net.log main;
    error_log   /var/log/nginx/dev-manage.dding.net.error.log warn;
    root        /home/gitlab-runner/saas-manager-fe/dist/;
    charset     utf-8;
    client_max_body_size        16m;
    
    location / {
        expires 5m;
    }
    
    location /v3/ {
        proxy_pass http://127.0.0.1:7002/v3/;

    }
    
    location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$ {
        expires 30d;
    }
    
    location ~ .*\.(js|css)?$ {
        expires 7d;
    }
}
```

```sh
    location ^~/user/ {
        proxy_set_header Host $host;
        proxy_set_header  X-Real-IP        $remote_addr;
        proxy_set_header  X-Forwarded-For  $proxy_add_x_forwarded_for;
        proxy_set_header X-NginX-Proxy true;

        rewrite ^/user/(.*)$ /$1 break;
        proxy_pass http://user;
    }
    
    location ^~/user/ {
        proxy_set_header Host $host;
        proxy_set_header  X-Real-IP        $remote_addr;
        proxy_set_header  X-Forwarded-For  $proxy_add_x_forwarded_for;
        proxy_set_header X-NginX-Proxy true;

        proxy_pass http://user/;
    }

```
