# Tomcat



## 安装

1.下载源码

```
wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.56/bin/apache-tomcat-9.0.56.tar.gz

tar -xf apache-tomcat-9.0.56.tar.gz -C /usr/local/

mv /usr/local/apache-tomcat-9.0.56 /usr//local/tomcat
```

2.添加配置文件

```
vim /etc/profile.d/tomcat.sh

加入配置
export TOMCAT_HOME=/usr/local/tomcat/

source /etc/profile.d/tomcat.sh
```



## 使用

```
1.启动
/usr/local/tomcat/bin/startup.sh

2.查看版本信息
/usr/local/tomcat/bin/version.sh

3.停止服务
/usr/loca/tomcat/bin/shutdown.sh

4.查看服务
ps -ef|grep tomcat

服务启动默认端口：8080
```









