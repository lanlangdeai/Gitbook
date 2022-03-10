# 常用命令



## 1. 查看过期日志并删除

```bash
# 删除10天前文件
find -mtime +10 -name "*.log" | xargs rm -f


```



## 2. 查看Mac地址

```bash
cat /sys/class/net/eth0/address
```



### 3. 抑制空格和注释查看文件内容

```bash
grep -v '^#\|^$' /etc/default/ufw
```











