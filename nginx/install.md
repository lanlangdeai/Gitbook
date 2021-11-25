# Nginx之安装篇

## 安装













## 设置开启启动

1. 添加系统服务配置文件

   ```
   vim /lib/systemd/system/nginx.service
   ```

   

2. 添加配置项

   ```
   [Unit]
   Description=nginx
   After=network.target
   
   [Service]
   Type=forking
   ExecStart=/bin/nginx
   ExecReload=/bin/nginx -s reload
   ExecStop=/bin/nginx -s quit
   PrivateTmp=true
   
   [Install]
   WantedBy=multi-user.target
   ```

3. 说明与注意点

   ```
   [Unit]:服务的说明
   Description:描述服务
   After:描述服务类别
   
   [Service]服务运行参数的设置
   Type=forking是后台运行的形式
   ExecStart为服务的具体运行命令
   ExecReload为重启命令
   ExecStop为停止命令
   PrivateTmp=True表示给服务分配独立的临时空间
   
   [Install]运行级别下服务安装的相关设置，可设置为多用户，即系统运行级别为3
   
   
   注意：[Service]的启动、重启、停止命令全部要求使用绝对路径
   ```

 4. 常用命令

    ```
    a)加入开机启动
    systemctl enable nginx
    
    b)禁止开机启动
    systemctl disable nginx
    
    c)启动服务
    systemctl start nginx
    
    d)停止服务
    systemctl stop nginx
    
    e)查看服务状态
    systemctl status nginx
    
    f)查看所有已启动的服务
    systemctl list-units -type=service
    ```

    









