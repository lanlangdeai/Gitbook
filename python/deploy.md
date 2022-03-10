# 项目部署



## 项目启动

[uWSGI]

配置文档：https://uwsgi.readthedocs.io/en/latest/Configuration.html



安装：

```
pip3 install uwsgi
or
apt-get install uwsgi
```

添加配置文件：

1.uwsgi_params文件

```
uwsgi_param  QUERY_STRING       $query_string;
uwsgi_param  REQUEST_METHOD     $request_method;
uwsgi_param  CONTENT_TYPE       $content_type;
uwsgi_param  CONTENT_LENGTH     $content_length;
uwsgi_param  REQUEST_URI        $request_uri;
uwsgi_param  PATH_INFO          $document_uri;
uwsgi_param  DOCUMENT_ROOT      $document_root;
uwsgi_param  SERVER_PROTOCOL    $server_protocol;
uwsgi_param  REQUEST_SCHEME     $scheme;
uwsgi_param  HTTPS              $https if_not_empty;
uwsgi_param  REMOTE_ADDR        $remote_addr;
uwsgi_param  REMOTE_PORT        $remote_port;
uwsgi_param  SERVER_PORT        $server_port;
uwsgi_param  SERVER_NAME        $server_name;
```

2.项目配置文件mrdoc_uwsgi.ini

```
[uwsgi]
; 绑定端口 socket 与nginx机型通信  http可以直接做web服务
socket = :8008
;http = :8008
; 项目目录
chdir = /www/MrDoc
; 设置虚拟环境的路径
virtualenv = /www/MrDoc/mrdoc_env
;指定wsgi文件。在与settings.py同级目录中会有一个wsgi.py文件
module = MrDoc.wsgi:application
; 项目中wsgi.py文件的目录
wsgi-file = MrDoc/wsgi.py
master = true
; 指定日志文件(会自动创建)。这个很重要，如果uwsgi出现错误，可以通过日志文件来查错
logto = %(chdir)/uwsgi.log
; 主进程，之后操作用到
pidfile = %(chdir)/uwsgi.pid
;  设置uwsgi后台运行，用uwsgi.log保存日志信息
daemonize = %(chdir)/uwsgi.log
; 进程数
process = 1
; 线程数
threads = 2
;是否开启热加载
py-autoreload = 1 
vacuum = true
thunder-lock = true
harakiri = 60
disable-logging = true
uid=1000
gid=1000
```

3.启动及相关操作

```
启动：
uwsgi --ini  wsgi.ini
停止：
uwsgi --stop uwsgi.pid
重启：
uwsgi --reload uwsgi.pid

```

4.nginx配置文件

```nginx
server {
    listen  8000;
    server_name localhost;
    access_log  /var/log/nginx/mrdoc_access.log;
    error_log   /var/log/nginx/mrdoc_error.log;

    client_max_body_size 75M;

    location / {
        include /www/MrDoc/deploy/uwsgi_params;
        uwsgi_pass 127.0.0.1:8008;
        uwsgi_read_timeout 60;
    }

    location /static {
        expires 30d;
        autoindex on;
        add_header Cache-Control private;
        alias  /www/MrDoc/static;
    }

    location /media {
        alias  /www/MrDoc/media;
    }

}
```













[gunicorn]







[uvicorn]





















