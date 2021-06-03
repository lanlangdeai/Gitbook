# 安装篇



## NODE









## NPM

[Node.js](https://nodejs.org/) 的依赖包管理生态系统 [npm](https://www.npmjs.com/), 是世界上最大的生态系统开源库。





### NPM加速

​    原因：npm 默认是从国外的源获取和下载包信息，有时甚至被墙，导致无法正常安装软件。

​    解决：

1. ​		在安装软件的时候使用--registry来注册镜像地址到国内的镜像（每次使用都需要指定国内的镜像）

```
npm install gitbook-cli -g --registry=http://registry.npm.taobao.org
```

2.  可以将国内镜像设置为默认的镜像源

```
npm config set registry=http://registry.npm.taobao.org
```

3.  使用cnpm来替代npm

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
* 安装完成之后就可以使用cnpm来进行相关软件的安装
cnpm install  [name]
```



