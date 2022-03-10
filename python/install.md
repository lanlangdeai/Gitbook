# Python安装篇



【Linux】

1.安装依赖包

```
yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel
```

2.下载python源码包到指定目录

```
cd /usr/local/src
wget https://www.python.org/ftp/python/3.8.12/Python-3.8.12.tgz

其他版本：
37)
wget https://www.python.org/ftp/python/3.7.12/Python-3.7.12.tgz
39)
wget https://www.python.org/ftp/python/3.9.9/Python-3.9.9.tgz

```

3.创建安装目录并安装

```
mkdir -p /usr/local/python3

# 解压
tar -zxvf Python-3.8.12.tgz

# 安装编译器gcc
yum install gcc

# 安装libffi-devel(3.7版本之后需要的包)
yum install libffi-devel -y

cd Python-3.8.12
.configure --prefix=/usr/local/python3
make && make install
```

4.检查是否安装成功

```
/usr/local/python3/bin/python3 -V


```

5.建立python软链接

```
ln -s /usr/local/python3/bin/python3 /usr/bin/python3
ln -s /usr/local/python3/bin/pip3  /usr/bin/pip3
```

6.添加环境变量

```
vim /etc/profile

最后添加代码
PATH=$PATH:$HOME/bin:/usr/local/python3/bin
export PATH

：wq


# 立即生效
source /etc/profile
```















