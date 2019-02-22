Jenkins
========

Jenkins 容器.

### 使用
初次运行
```
$ docker-compose up --build -d
```
> 第一次启动需要构建镜像，后面启动则不需要 --build 参数了

启动容器
```
$ docker-compose up -d
```

浏览器访问 `localhost:8080` 配置即可.

### 配置域名
给 `Jenkins` 配置域名而不用 `localhost:8080`.

利用 `Nginx` 反向代理实现.
```
$ cat jenkins.conf
server {
    listen 80;
    server_name jenkins.local.com;

    location / {
        proxy_pass http://jenkins;
    }
}

upstream jenkins {
    server localhost:8080;
}

$ sudo nginx -s reload # 平滑加载配置
```

修改本地 `hosts`
```
$ cat /etc/hosts
127.0.0.1 jenkins.local.com
```

浏览器直接访问 `jenkins.local.com` 即可访问 `Jenkins` 服务了.
