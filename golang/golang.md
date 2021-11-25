# golang基础



官网：[Downloads - The Go Programming Language (google.cn)](https://golang.google.cn/dl/)









【安装】

1.下载包

```
wget https://golang.google.cn/dl/go1.16.8.linux-amd64.tar.gz
```

2.解压

```
tar -C /usr/local -zxvf go1.16.1.linux-amd64.tar.gz
```











【常用命令】

1.查看变量

```
go env
```

2.设置代理（由于默认是走国外，比较慢， 需要更换代理）

```
go env -w GO111MODULE=on
go env -w GOPROXY=https://goproxy.cn,direct


其他代理：
  https://goproxy.io
  https://mirrors.aliyun.com/goproxy/
```











