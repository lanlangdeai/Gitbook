# 常用脚本



1. 守护进程

   ```bash
   #!/bin/bash
   #守护进程
   while true
   do
       c=`ps -ef | grep api/wx/deal_up_event | grep -v grep | wc -l`
       if [ $c -lt 1 ]
       then
           nohup php /www/wwwroot/SsCpc/index.php  api/wx/deal_up_event > /dev/null 2>&1 & echo $!
       fi
       sleep 10
   ```

2. 清理过期日志文件

```bash
#!/bin/bash
# 删除超过10天，并且以.log结尾的文件
cd /data/www/tt2kj_feedback/common/runtime
find -mtime +10 -name "*.log" -exec rm -rf {} \;
```



3.nginx日志分割

```shell
#!/bin/bash

dat=`date +"%Y%m%d" `
mon=`date +"%Y%m"`
echo $dat

nginx_path="/data/log/nginx/"
mondir=$nginx_path$mon

/bin/echo $mondir 
if [ ! -x "$mondir" ]; then 
    echo "开始创建日期文件夹"
    mkdir "$mondir"
    echo "创建日期文件夹结束"
fi
/bin/echo `date +"%Y-%m-%d %H:%M:%S"` 
/bin/echo ` ls -al $mondir`

# 声明需要分割的日志文件
logs=("access_bi.inner.tt2kj.com_80" "access_kf.inner.tt2kj.com_80" "nginx_error")
for log_name in ${logs[@]}
do
	echo $log_name 
    mv $nginx_path$log_name".log" $mondir/$log_name-$dat".log"
done

kill -USR1 `cat /var/run/nginx.pid`
/bin/echo "done "
```

