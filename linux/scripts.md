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

2. 

