# 配置篇



1. 非www，默认跳转www地址

   ```
   server {
       listen 80;
       server_name www.xxx.com xxx.com;
       if ($host != 'www.xxx.com') {
           rewrite ^/(.*)$ http://www.xxx.com/$1 permanent;
       }
   }
   ```

   



2. 生产环境基本配置

    ```
    upstream common {
        server 127.0.0.1:5101;
        server 127.0.0.1:5102;
    }
    upstream search {
        server 172.16.114.52:5301;
        server 172.16.114.52:5302;
    }
    limit_req_zone $binary_remote_addr zone=one:10m rate=5r/s;
    server {
            listen       80;
            server_name  www.demo.com;
    		return       301 https://www.demo.com$request_uri;
    }
    
    server {
    	listen       443 ssl;
    	server_name  www.demo.com;
    	ssl on;
        ssl_certificate      /etc/nginx/ssl/demo.com.fullchain.cert;
        ssl_certificate_key  /etc/nginx/ssl/demo.com.key;
    
    	client_max_body_size 20m;
    	gzip on;
    	limit_req zone=one burst=10;
    	access_log  /data0/varlog/nginx/www_demo.access.log  main;
    	error_log   /data0/varlog/nginx/www_demo.error.log error;
    
    	if ( $host != 'www.demo.com' ) {
    		rewrite ^(.*)$ https://www.demo.com$1 permanent;
    	}
    
    	location / {
    		proxy_pass http://127.0.0.1:3000;
    	}
    
    	location ~* /fbmain/(common|account|monitor|history_crawl|user|pay|need) {
    		proxy_pass_header Server;
    		proxy_set_header Host $http_host;
    		proxy_redirect off;
    		proxy_set_header X-Real-IP $remote_addr;
    		proxy_pass http://common;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    	}
    
    	location ~ /fbmain/search {
    		proxy_pass_header Server;
    		proxy_set_header Host $http_host;
    		proxy_redirect off;
    		proxy_set_header X-Real-IP $remote_addr;
    		proxy_pass http://search;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    	}
    
    	location /static {
    		root /data0/wwwroot/nuxt/main_monitor_flask;
    	}
    
    	location ~ /static/v1/auto_login {
    		proxy_pass_header Server;
    		proxy_set_header Host $http_host;
    		proxy_redirect off;
    		proxy_set_header X-Real-IP $remote_addr;
    		proxy_pass http://127.0.0.1:5101;
    	}
    
    }
    ```








