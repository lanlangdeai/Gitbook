# 常用命令



## 1. 查看过期日志并删除

```bash
# 删除10天前文件
find -mtime +10 -name "*.log" -exec rm -rf {} \;


```

