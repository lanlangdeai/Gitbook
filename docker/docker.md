# Docker





## Docker镜像加速

```
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://pb84l2li.mirror.aliyuncs.com"]
}
EOF

sudo systemctl daemon-reload
sudo systemctl restart docker
```



## 常用命令

```
-d  后台运行

--name=定义服务名称

-p 5800:5800  端口映射，宿主机端口：容器端口

--shm-size 1g   设置共享内存大小

-e  DISPLAY_WIDTH=1366  设置环境变量

--privileged=true 享有特权

```









