系统服务

​	1)开机启动

```
systemctl enable httpd
```

​	2)查看状态

```
systemctl status httpd
```

​	3)重新加载

```
systemctl deamon-reload
```

​    4)启动服务

```
systemctl start httpd
```



```
[Unit]  启动顺序与依赖关系
Description=服务描述
Documentation=文档地址
# 启动顺序
# after：在哪些服务启动之后再启动该服务
After=network.target
Before=

[Service]  启动行为
ExecStart= 定义启动进程时执行的命令

          ExecReload字段：重启服务时执行的命令

　　　　　　ExecStop字段：停止服务时执行的命令

　　　　　　ExecStartPre字段：启动服务之前执行的命令

　　　　　　ExecStartPost字段：启动服务之后执行的命令

　　　　　　ExecStopPost字段：停止服务之后执行的命令
　　　　　　
　　　　　
Type= 定义自动类型
    simple(默认):ExecStart字段启动的进程为主进程
    forking:ExecStart字段将以fork（）方式启动， 此时父进程会退出，子进程会成为主进程
    onshot:类似于simple,但只执行一次， Systemd会等他执行完， 才启动其他服务
    
    notify：类似于simple，启动结束后会发出通知信号，然后 Systemd 再启动其他服务

    idle：类似于simple，但是要等到其他任务都执行完，才会启动该服务。一种使用场合是为让该服务的输出，不与其他服务的输出相混合
    
   
KillMode:定义了如何停止服务
    control-group（默认值）：当前控制组里面的所有子进程，都会被杀掉
	process：只杀主进程
	mixed：主进程将收到 SIGTERM 信号，子进程收到 SIGKILL 信号
	none：没有进程会被杀掉，只是执行服务的 stop 命令。

Restart:定义服务退出后， systemd的重启方式
	no（默认值）：退出后不会重启
	on-success：只有正常退出时（退出状态码为0），才会重启
	on-failure：非正常退出时（退出状态码非0），包括被信号终止和超时，才会重启
	on-abnormal：只有被信号终止和超时，才会重启
	on-abort：只有在收到没有捕捉到的信号终止时，才会重启
	on-watchdog：超时退出，才会重启
	always：不管是什么退出原因，总是重启
   对于守护进程， 推荐on-failure,对于允许发生错误退出的服务可以设置on-abnormal
   
RestartSec:标识systemd服务重启前，需要等待的秒数


[Install]  如何安装这个配置
WantedBy= 还表示该服务所在的Target
    multi-user.target(默认方式)：在这个组里的所有服务豆浆开机启动
    graphical.target= 表示图形用户状态
```

设置依赖关系，需要使用Wants字段和Requires字段。

　　　　Wants字段：表示sshd.service与sshd-keygen.service之间存在"弱依赖"关系，即如果"sshd-keygen.service"启动失败或停止运行，不影响sshd.service继续执行。

　　　　Requires字段则表示"强依赖"关系，即如果该服务启动失败或异常退出，那么sshd.service也必须退出。

　　注意，Wants字段与Requires字段只涉及依赖关系，与启动顺序无关，默认情况下是同时启动的





示例：

Jupyter

```shell
[Unit]
Description=Jupyter Service

[Service]
Type=forking
ExecStart=/usr/bin/python3 -m IPython notebook
KillMode=process
Restart=on-failure
RestartSec=3s

[Install]
WantedBy=multi-user.target
```



Frps  (服务文件：/usr/lib/systemd/system/frps.service)

```shell
[Unit]
Description=Frp Server Service
After=network.target

[Service]
Type=simple
User=nobody
Restart=on-failure
RestartSec=5s
ExecStart=/usr/bin/frps -c /etc/frp/frps.ini
LimitNOFILE=1048576

[Install]
WantedBy=multi-user.target
```





